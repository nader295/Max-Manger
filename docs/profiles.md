# Chipset profiles and native executables

MaxManager ships five native binaries. Each one exists because a different kind of knowledge does not
belong inside an Android app.

| Binary | Language | What it knows |
| --- | --- | --- |
| `sys.maxmanager-service` | C (14 components) | The device-facing service: app loading, game preload, PID tracking, bypass charging, system profile, inotify, config, logging, startup sequencing |
| `sys.maxmanager-profilesettings` | Rust (`binprofiles/`) | **Chipset strategies** |
| `sys.maxmanager-utilityconf` | Rust (`binutils/`) | Utility configuration |
| `sys.maxmanager-rianixiathermalcore` | Rust (`thermalcore/`) | Thermal policy — see [thermal.md](thermal.md) |
| `sys.maxmanager-preloadbin` | C (`preloadbin/`) | Game library preloading |

## Profiles — `binprofiles`

| File | What it is |
| --- | --- |
| `chipsets/` | Five families, each with its own strategy: **Snapdragon · MediaTek · Exynos · Tensor · Unisoc** |
| `plan.rs` | The **pure table** of the binary's CLI contract: parsing, the ownership gate, and what each verb does — separated from I/O so the contract can be tested without a device |
| `props.rs` | The single source of truth for every `persist.sys.maxmanager*` property key this binary reads or writes |
| `profiles/` | The profile definitions themselves |

Two design points worth naming, because they are the difference between a profile system and a pile of
`if` statements:

1. **The CLI contract is data.** `plan.rs` holds the table; the main loop only executes it. That makes
   "what does this verb do" answerable by reading one file, and testable off-device.
2. **Property keys live in one place.** A property name spelled differently in two files is the classic
   silent bug in this domain: both files compile, one of them lies.

## The kernel CLI and its short name

The module exposes the daemons as ordinary binaries on `system/bin`, and symlinks the shorter names
so a terminal user can reach them quickly (including `zx` for the service binary). One name, one path —
see the path table in [rom-integration.md](rom-integration.md).

## The preloader — `preloadbin`

`preloadbin/jni/main.c` **embeds vmtouch 1.4.1** (BSD-3-Clause, © Doug Hoyte and contributors; measured
at 99.7 % identical, three lines different) and keeps that notice in the file header. It is what puts a
game's libraries into page cache before the game needs them.

That is a copied-and-adapted component, and it is credited as one rather than presented as original
work. The full accounting is in [THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md).

## The main daemon — `archdaemon`

Fourteen components, each one a single concern: `StartupInit`, `ConfigHandler`, `AppLoader`,
`AppMonitoring` (the Java companion), `GamePreload`, `PidTracker`, `BypassCharge`, `SystemProfile`,
`InotifyHandler`, `BinaryCLI`, `MaxManagerUtility`, `ShellUtility`, `FileUtility`, `SystemLogger`.

It descends from **Encore Tweaks** (Apache-2.0, © Rem01Gaming), whose notices are preserved in the files
that carry its header. The daemon builds with `-std=c23 -Werror -pedantic-errors` in the AOSP kit — it
is not a script with a C extension, it is C that has to survive a strict compiler.

## Why these are separate executables, not app code

- **They survive the app.** A daemon keeps working when the UI is not running, which is the entire point
  of applying a profile at boot.
- **They run with different privileges**, and keeping them separate keeps the app's blast radius small.
- **They can be verified as artifacts.** The build asserts the daemon is an executable ELF for the right
  ABI before packaging, and the module verifies its checksums after extraction.
