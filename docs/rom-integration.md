# ROM integration guide

MaxManager ships as a systemless module, but it is built to be *embeddable*. There are three paths, and
the repository already contains the files for all three.

> **Before anything else: permission.** MaxManager is proprietary software. The integration kit below
> is here so that ROM maintainers can evaluate and integrate it *with the copyright holder's written
> permission* — [LICENSE](../LICENSE) grants no right to use, copy or distribute it otherwise. Ask
> first; the community link is in the [README](../README.md#support).

---

## Decision: the ROM build is a system app

On a ROM, the Manager app is a **platform-signed privileged app on the system partition**, at
`/system/priv-app/MaxManager/MaxManager.apk`, placed the same way MiCam is placed in a ROM. Its
allowlist sits beside it in `/system/etc/permissions/` (the allowlist matches by package name, so it
must live on the same partition as the APK, which is the kit's own rule). A seapp line maps the
package `nd.max` to the app's SELinux domain.

**Why system and not product.** The team's finding: a product-partition build compiles, but its sepolicy
does not work, because `neverallow` rules stop product apps from being granted the system SELinux access
they need. The team also reads the device layout as putting the Xiaomi components the app works with on
`/system`. Re-check both with your own `neverallow` pass. The daemon already lives in `/system/bin`, so
the app moving there as well puts the whole integration on one partition.

**What this does not do yet.** The code still builds the product layout. The
[pending changes](#pending-code-changes) list is exactly what must change. Nothing on this page has
been built for AOSP or booted in the environment where it was written.

---

## What the platform must provide

| Requirement | Detail |
| --- | --- |
| Android | 10+ (`minSdk 29`). Built against `compileSdk 37` and `targetSdk 37`. |
| ABIs | `arm64-v8a` (primary) and `armeabi-v7a`. |
| Init | A service definition for the daemon, started after `sys.boot_completed=1` (or by property). |
| SELinux | A domain for the daemon, and a seapp line that maps `nd.max` to the app's domain. The policy file is provided; `neverallow` must be checked against your tree. |
| Privileged app | Platform-signed, on `/system/priv-app`, with an allowlist for `WRITE_SECURE_SETTINGS` in `/system/etc/permissions/`. |
| Sysfs / procfs | Read and write access to the interfaces the user enables. Nothing else is touched. |
| Root | Either Magisk/KernelSU (module path) or the platform-signed priv-app path (ROM path). |

## Names that must agree

Three names and one partition must agree exactly. A mismatch fails silently. `tools/sepolicy_matrix.py`
checks several of these lines, so run it after every change.

```
daemon path   /system/bin/sys.maxmanager-service
init service  maxmanager.rc → service sys.maxmanager-service /system/bin/sys.maxmanager-service
SELinux       domain u:r:maxmanager:s0; the binary is labelled u:object_r:maxmanager_exec:s0 by file_contexts
app           /system/priv-app/MaxManager/MaxManager.apk, allowlist in /system/etc/permissions/
```

## The AOSP kit — `android/aosp/`

| File | Goes to | What it does |
| --- | --- | --- |
| `Android.bp` | your Soong tree | Builds the app (`android_app`, `platform_apis`, `certificate: "platform"`, `privileged`) and the daemon (`cc_binary`, `-std=c23 -Werror -flto`). Still carries `product_specific: true`; see [pending changes](#pending-code-changes). |
| `BoardConfig.mk` | `device/maxmanager/BoardConfig.mk` | `BOARD_SEPOLICY_DIRS += device/maxmanager/sepolicy`, and nothing else, deliberately. |
| `product-inclusion.mk` | your product makefile | `PRODUCT_PACKAGES` (app, daemon, native library), `PRODUCT_COPY_FILES` (the `.rc` and the allowlist), `PRODUCT_PROPERTY_OVERRIDES`. |
| `maxmanager.rc` | `/system/etc/init/maxmanager.rc` | The init service: `class main`, `user root`, `capabilities NET_ADMIN SYS_ADMIN`, `seclabel u:r:maxmanager:s0`, `disabled`, started on boot or by property. |
| `sepolicy/maxmanager.te` | your sepolicy dir | The `maxmanager` domain: sysfs and procfs, thermal, battery and GPU character devices, properties, logging, its data directory, and binder to apps. |
| `sepolicy/file_contexts` | your sepolicy dir | Labels for the daemon, the APK and the data directory. The APK line is pending. |
| `../overlay/product/etc/permissions/privapp-permissions-nd.max.xml` | `/product/etc/permissions/` today; `/system/etc/permissions/` on the decided path | The privileged allowlist (`WRITE_SECURE_SETTINGS`). |

**Why `BOARD_*` and `PRODUCT_*` are two files.** `PRODUCT_*` variables are not read from a
`BoardConfig.mk` at all. A line there passes silently and leaves you believing the app was included.
Splitting the fragments makes each variable live where the build reads it.

**Why the daemon is `system` and not `vendor`.** The init line, the file context and the Soong module
all name `/system/bin`. Declaring the module for another partition makes the build either publish it
where nothing starts it, or reject the policy as contradictory. The app follows the same rule now:
its module, its label and its allowlist all name `/system`.

## Step by step — AOSP source build

1. Copy `android/aosp/` into `device/maxmanager/` in your tree, keeping `sepolicy/` inside it. This
   places the init file at `device/maxmanager/maxmanager.rc` (`product-inclusion.mk` currently expects
   it one folder deeper; see [known gaps](#known-gaps-and-mismatches)).
2. Copy the allowlist XML to `device/maxmanager/system/etc/permissions/`. In this repository the file
   is still under `product/`; the pending change moves it.
3. Add the fragments to your device's build: `$(call inherit-product, device/maxmanager/product-inclusion.mk)`,
   and include `device/maxmanager/BoardConfig.mk` from your board config.
4. Point `Android.bp` at your checkout. Its `srcs` and `manifest` paths are relative to where the file lands.
5. Add the seapp line for `nd.max` (see [getting the policy right](#getting-the-policy-right-avc-denials)).
6. Build, then run the checks in the verification table below.
7. Run your own `neverallow` pass. The policy has not been validated against a full AOSP tree, and that
   pass is the one that decides.

## Getting the policy right: AVC denials

The `.te` file is a starting point. The real rules come from the denials a device logs while the
domain runs. This is the workflow the team agreed on.

1. Build a userdebug or eng image and set the domain to `permissive`, for collection only. Remove that
   line before anything ships.
2. Connect over wireless ADB: `adb pair <ip>:<pairing-port>`, then `adb connect <ip>:<port>`.
3. Use every function, profile and toggle the app and the daemon have. A denial you never trigger
   turns into a bug later.
4. Export the denials: `adb logcat -d | grep "avc: denied" | grep "permissive=1" > avc.txt` (or
   `adb shell dmesg` if your device logs there). The `permissive=1` field marks a denial that was logged
   but allowed, because the domain is permissive.
5. Turn the lines into rules with `audit2allow` against your built policy, or write them by hand, and
   review every rule. Reject anything broad: wildcard domains, blanket `*_device` allows, and new
   `neverallow` exceptions.
6. Remove `permissive`, build a full user image with no debug, boot it enforcing, and run
   `dmesg | grep -i avc` after boot. An empty result is the pass.

## Pending code changes

These changes make the code match this page. None of them is applied yet.

- **`android/aosp/Android.bp`**: delete `product_specific: true` from the `MaxManager` `android_app`.
  The file's own header already describes a system app, so the setting is the part that disagrees.
- **`android/aosp/sepolicy/file_contexts`**: move the APK line to
  `/system/priv-app/MaxManager/MaxManager.apk` and label it with the platform's `/system` label.
  This repository's own code uses `system_file` for `/system` content. The kit's current
  `system_app_file` appears nowhere else here, so check the type in your tree before using it.
- **Allowlist XML**: move `privapp-permissions-nd.max.xml` from `android/overlay/product/etc/permissions/`
  to `android/overlay/system/etc/permissions/`, and point `product-inclusion.mk` at
  `$(TARGET_COPY_OUT_SYSTEM)`. Two other files depend on the current path and must change in the same
  commit: `.github/scripts/build_developer_bundle.sh` copies the file from it, and
  `tools/bundle_contract.py` expects it there.
- **`android/aosp/product-inclusion.mk`**: the init file's source path is
  `device/maxmanager/system/etc/init/maxmanager.rc`, but step 1 places it at
  `device/maxmanager/maxmanager.rc`. One of the two must change.
- **App domain**: add the seapp line for `nd.max` and declare the domain it maps to.
- **Data location**: choose one (see [known gaps](#known-gaps-and-mismatches)) and make
  `MaxManager.h`, `maxmanager.te` and `file_contexts` agree.

## Known gaps and mismatches

Reported here, not papered over.

1. **The JNI library stanza is stale.** `Android.bp` declares `runtime/daemon-rust/src/lib.rs`, which
   does not exist in this tree, and it puts one module on both `vendor` and `product_specific`. The real
   crate is `manager/src/main/rust/` (cdylib `maxmanager_native`). Either wire the stanza to that crate,
   or drop it and ship the library inside the APK, which is what the prebuilt path does.
2. **The APK's partition and label disagreed.** `file_contexts` labelled `/system/app/...` while
   `Android.bp` installed the app as product. The decision above settles the partition; the pending
   list settles the code.
3. **The daemon's data path is not the policy's data path.** `archdaemon/jni/include/MaxManager.h`
   hard-codes `/data/adb/.config/MaxManager/...` and `/data/adb/modules/MaxManager/...`, and reads app
   files under `/data/data/nd.max/`. The kit labels `/data/misc/maxmanager`, which the daemon never
   uses, so the `maxmanager_data_file` rules guard a path nothing writes. `/data/adb` may not exist on a
   ROM build at all. Pick a data location for the ROM path, then make the header, the policy and the
   labels agree.
4. **The policy has not met a real `neverallow` pass.** There is no AOSP tree in this environment.
   Treat the `.te` file as a reviewed starting point, not a validated policy.
5. **The ROM kit builds one daemon.** The Magisk module installs five binaries under `system/bin/`: the
   device service, the profile settings, the thermal core, the utility configurator and the preloader.
   The ROM kit builds only `sys.maxmanager-service`, and the checks below expect exactly that.

## Verification checklist (ROM path)

| Check | How | Pass |
| --- | --- | --- |
| The daemon exists and is executable | `ls -l /system/bin/sys.maxmanager-service` | mode `0755` |
| It is running | `pidof sys.maxmanager-service` | a PID |
| Init accepted the service | `getprop init.svc.sys.maxmanager-service` | `running` |
| The daemon runs in its domain | `ps -Z \| grep sys.maxmanager-service` | `u:r:maxmanager:s0` |
| The app is on the system partition | `pm path nd.max` | a path under `/system/priv-app/` |
| The app is privileged | `dumpsys package nd.max \| grep -i privileged` | the privileged flag is set |
| The app runs in its mapped domain | `ps -Z \| grep nd.max` | the domain from your seapp line |
| The allowlist applied | the app writes secure settings without a prompt | yes |
| No denials | `dmesg \| grep -i avc` after boot | empty |
| Only one maxmanager binary | `ls /system/bin \| grep maxmanager` | `sys.maxmanager-service` only |

## KernelSU variant — `android/kernelsu/`

The KernelSU Next packaging of the same module (`customize.sh`, `service.sh`, `action.sh`,
`uninstall.sh`, `module.prop`, `skip_mount`). Use it when your device roots with KernelSU and you do not
want the privileged-app path.

## The Magisk / systemless path

The shipped module (`MaxManager-V2.zip`) installs the daemons to `system/bin/` and the Manager APK to
`app/MaxManager.apk`, outside `system/`, with checksum verification. The APK is installed with `pm install`
as a normal user app, so the launcher and root managers list it like any other app; it is no longer a
systemless privileged app. This is the path a normal user takes; see [README → Install](../README.md#install).

The developer bundle (`MaxManager-developer-bundle.zip`) still ships the `product/priv-app` layout until
the pending changes land. Its generator builds that layout, and the bundle check in `build.yml` looks for
that layout, so both move with the code.

## Support model for ROM maintainers

Bring: the device, the ROM base, which integration path, and the output of the checks above.
`dmesg | grep -i avc` is the single most useful thing you can attach. A domain that is missing an allow
is a five-line fix when the denial is included, and a guessing game otherwise.
