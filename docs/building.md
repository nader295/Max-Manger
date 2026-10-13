# Building, CI and releases

This is the engineering half of "how do I get a working artifact" — the parts a **user** never needs
(the [README](../README.md#install) is enough for them) and a developer or ROM maintainer does.

## Build the app from source

```sh
cd manager
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export ANDROID_HOME="$HOME/android-sdk" ANDROID_SDK_ROOT="$HOME/android-sdk"
./gradlew :app:testReleaseUnitTest :app:assembleDebug -x :app:lintVitalRelease \
  -Dorg.gradle.jvmargs="-Xmx6g -XX:MaxMetaspaceSize=1g" --build-cache --parallel
```

| Component | Version |
| --- | --- |
| Android Gradle Plugin | 9.2.0 |
| Kotlin / KSP | 2.3.10 / 2.3.10 |
| Compose BOM · Material 3 | 2025.10.01 · 1.4.0 |
| Hilt (Dagger) | 2.60.1 |
| Navigation Compose | 2.9.4 |
| libsu (the root boundary) | 6.0.0 |
| Haze · Coil | 2.0.0-alpha02 · 2.7.0 |
| Rust crates | edition 2024 (`maxmanager_native`, `thermalcore`, `binprofiles`, `binutils`) |
| SDK | `minSdk 29` · `compileSdk 37` · `targetSdk 37` |

**Signing is fail-fast by design.** `manager/app/build.gradle.kts` throws
`GradleException("KS_PWD must be set to produce a signed release artifact")` before doing any work, so
a release build cannot silently produce an unsigned artifact. No keystore, key or password is in this
repository — that is a rule here, not a preference.

## What the build must pass first

Before the NDK, the Rust crates and R8 run at all, CI runs **33 judgements — 16 assertions and 17
self-tests** in a step called *Contract gates*, measured locally in **32 s and 32 s** on two runs.
The full table of what each gate refuses to let through is in
[verification.md](verification.md#layer-1--contract-gates); the shortest version is that a broken tree
fails in seconds instead of after minutes of native compilation.

```sh
python3 tools/kt_balance.py --assert
python3 tools/code_health.py --assert
python3 tools/i18n_coverage.py --assert
python3 tools/readme_assets.py --assert     # assets and every link in the documentation
python3 tools/svg_review.py --assert        # readable, unclipped, static-correct visual assets
```

## What CI produces

From `.github/workflows/build.yml` (51 steps):

| Artifact | What it is |
| --- | --- |
| `MaxManager-V2.zip` | The flashable module — the artifact *is* the zip, no wrapper around it |
| `MaxManager-developer-bundle.zip` | The integration bundle for ROM developers |
| `MaxManager-checksums` | Checksums for both |

The version string is **single-sourced**: the [`version`](../version) file must match `module.prop`,
`update.json` and the daemon header, and `tools/bundle_contract.py` fails the build otherwise. The
on-device daemon greps `module.prop` at boot, so a one-byte difference there is not cosmetic — it is
the difference between a module that boots and one that removes itself.

## Releases

| Version | Channel | What it contains | Where to get it |
| --- | --- | --- | --- |
| **v1.0** | `stable` | First single-sourced release: one module zip, one version string, priv-app + five daemons | **CI Artifacts** → [latest run](https://github.com/catui0041-alt/Gg/actions/workflows/build.yml) |
| v1.0 | developer | Integration bundle (AOSP kit, KernelSU packaging, checksums) | Same run, `MaxManager-developer-bundle.zip` |

**Measured status, stated plainly: this repository has 0 published GitHub *Releases*.** The build
produces a flashable zip on every green run as a workflow **artifact** (30-day retention). For a
permanent, versioned release page — with the zip attached rather than an artifact that expires — the
version string is already single-sourced for it:

```sh
gh release create V2 MaxManager-V2.zip \
  --title "MaxManager V2" --notes-file changelog.md
```

History lives in [`changelog.md`](../changelog.md).

## The numbers, and how to re-derive them

Every count quoted anywhere in this repository can be re-derived; nothing is a rounded guess. Measured
on **2026-09-28**:

| Number | Command |
| --- | --- |
| 53 destinations | `grep -cE 'data object \w+ : MaxDestination' manager/app/src/main/java/nd/max/ui/navigation/MaxDestinations.kt` |
| 418 Kotlin files · 111,476 lines | `find manager/app/src/main/java/nd/max -name '*.kt' \| wc -l` (and `-exec cat {} + \| wc -l`) |
| 84 locales | `ls -d manager/app/src/main/res/values-* \| wc -l` |
| 1681 tests | `grep -rhoE '@Test' manager/app/src/test \| wc -l` |
| 16 `--assert` gates · 17 self-tests | `grep -cE '^\s+python3 tools/.*--assert$' .github/workflows/build.yml` (and `--self-test`) |
| 5 native binaries | `grep -oE 'libs/\$ARCH_TMP/[a-z.-]+' mainfiles/customize.sh \| sort -u` |
| 2006 source files | `python3 tools/source_manifest.py --summary` |

Two habits are why the numbers hold:

1. **A claim without a run is labelled.** Where something cannot be verified here — hardware
   behaviour, SELinux policy, boot, anything visual — it is written as *not verified in this
   environment* rather than softened into a maybe.
2. **The documentation is checked like code.** The SVGs and **every link in them** are validated by
   `tools/readme_assets.py --assert`: XML well-formedness, the animation rules GitHub actually honours
   (SMIL only; scripts and CSS keyframes are stripped), size thresholds, and whether each referenced
   file exists. And their *design* is measured by `tools/svg_review.py --assert` — text large enough to
   read at phone width, nothing clipped by the canvas, nothing that lands in the wrong place once
   motion is stripped. The contextual icons have their own contract inside the first gate: every
glyph drawn inside the safe area of its 24-unit grid, no glyph that depends on a font, and no icon
that appears on one language page without the other. That gate exists because four tiles of one
diagram were invisible for a whole revision while every file-level check passed — and because a
path that leaves its canvas is a shape no file-level check can see.
