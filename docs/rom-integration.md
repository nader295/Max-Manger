# ROM integration guide

MaxManager ships as a systemless module, but it is built to be *embeddable*. There are three paths, and
the repository already contains the files for all three.

> **Before anything else: permission.** MaxManager is proprietary software. The integration kit below
> is here so that ROM maintainers can evaluate and integrate it *with the copyright holder's written
> permission* — [LICENSE](../LICENSE) grants no right to use, copy or distribute it otherwise. Ask
> first; the community link is in the [README](../README.md#support).

---

## What the platform must provide

| Requirement | Detail |
| --- | --- |
| Android | 11+ (`minSdk 29`). Built against `compileSdk 37`, `targetSdk 37`. |
| ABIs | `arm64-v8a` (primary) and `armeabi-v7a`. |
| Init | A service definition for the daemon, started after `sys.boot_completed=1` (or by property). |
| SELinux | A domain for the daemon. The policy file is provided; `neverallow` must be checked against your tree. |
| Privileged app | The APK as a privileged app, with an allowlist for `WRITE_SECURE_SETTINGS`. |
| Sysfs / procfs | Read and write access to the interfaces the user enables. Nothing else is touched. |
| Root | Either Magisk/KernelSU (module path) or the platform-signed priv-app path (ROM path). |

Three interfaces must stay in agreement, and getting one wrong is the classic silent failure:

```
daemon path  : /system/bin/sys.maxmanager-service      ← one name, one path
init service : maxmanager.rc → service sys.maxmanager-service /system/bin/sys.maxmanager-service
SELinux      : file_contexts → /system/bin/sys.maxmanager-service  u:object_r:maxmanager_exec:s0
```

## The AOSP kit — `android/aosp/`

| File | Goes to | What it does |
| --- | --- | --- |
| `Android.bp` | your Soong tree | Builds the app (`android_app`, `platform_apis`, `certificate: "platform"`, `privileged`, `product_specific`, dex preopt) and the daemon (`cc_binary`, `-std=c23 -Werror -flto`) |
| `BoardConfig.mk` | `device/maxmanager/BoardConfig.mk` | `BOARD_SEPOLICY_DIRS += device/maxmanager/sepolicy` — and nothing else, deliberately |
| `product-inclusion.mk` | your product makefile | `PRODUCT_PACKAGES` (app, daemon, native lib), `PRODUCT_COPY_FILES` (the `.rc`, the permissions XML), `PRODUCT_PROPERTY_OVERRIDES` |
| `maxmanager.rc` | `/system/etc/init/maxmanager.rc` | The init service: `class main`, `user root`, `capabilities NET_ADMIN SYS_ADMIN`, `seclabel u:r:maxmanager:s0`, `disabled`, started on boot or by property |
| `sepolicy/maxmanager.te` | your sepolicy dir | The `maxmanager` domain: sysfs/procfs, thermal/battery/GPU char devices, properties, logging, its own data dir, binder to apps |
| `sepolicy/file_contexts` | your sepolicy dir | Labels for the daemon, the APK and the data directory |
| `../overlay/product/etc/permissions/privapp-permissions-nd.max.xml` | `/product/etc/permissions/` | The privileged permission allowlist (`WRITE_SECURE_SETTINGS`) |

**Why `BOARD_*` and `PRODUCT_*` are two files.** `PRODUCT_*` variables are not read from a
`BoardConfig.mk` at all — a line there passes silently and leaves you believing the app was included.
Splitting the fragments makes each variable live where the build actually reads it.

**Why the daemon is `system` and not `vendor`.** The init line, the file context and the Soong module
all name `/system/bin`. Declaring the module for another partition makes the build either publish it
where nothing starts it, or reject the policy as contradictory.

## Step by step — AOSP source build

1. Copy `android/aosp/` into `device/maxmanager/` in your tree (keeping `sepolicy/` inside it).
2. Copy `android/overlay/product/etc/permissions/privapp-permissions-nd.max.xml` to
   `device/maxmanager/product/etc/permissions/`.
3. Add the two fragments to your device's build:
   ```
   $(call inherit-product, device/maxmanager/product-inclusion.mk)
   ```
   and make sure `device/maxmanager/BoardConfig.mk` is included from your board config.
4. Point `Android.bp` at *your* checkout of this repository (`srcs` and `manifest` paths are relative to
   where the file lands).
5. Build and check the four things in the table below.
6. Verify SELinux with your own `neverallow` pass — the policy here has not been validated against a
   full AOSP tree, and that check is the one that decides.

## KernelSU variant — `android/kernelsu/`

The KernelSU Next packaging of the same module (`customize.sh`, `service.sh`, `action.sh`,
`uninstall.sh`, `module.prop`, `skip_mount`). Use it when your device roots with KernelSU and you do not
want the privileged-app path.

## The Magisk / systemless path

The shipped module (`MaxManager-v1.0.zip`) installs the APK to `system/product/priv-app/MaxManager/`
and the five daemons to `system/bin/`, with checksum verification, and pairs the privileged app with a
user-space copy so the root manager can still see it. This is the path a normal user takes; see
[README → Install](../README.md#install).

## Verification checklist after integration

| Check | How |
| --- | --- |
| The daemon exists and is executable | `ls -l /system/bin/sys.maxmanager-service` (expect `0755`) |
| It is actually running | `pidof sys.maxmanager-service` |
| Init accepted the service | `getprop init.svc.sys.maxmanager-service` → `running` |
| SELinux is not denying it | `dmesg | grep -i avc` right after boot (an empty result is the pass) |
| The app is privileged | `dumpsys package nd.max | grep -i privileged` |
| The permission allowlist landed | the app can write secure settings without a prompt |
| Nothing else moved | `ls -l /system/bin/sys.maxmanager-*` — five names, no aliases |

## Before you ship it — three things worth knowing

1. **The JNI library stanza in `Android.bp` is known-stale.** It declares a source path
   (`runtime/daemon-rust/src/lib.rs`) that does not exist in this tree; the real crate is
   `manager/src/main/rust/` (cdylib `maxmanager_native`). The file says so in its own comment. If your
   build evaluates that stanza, wire it to the real path or drop it and ship the library inside the APK
   (which is what the prebuilt path does).
2. **`file_contexts` labels the APK at a `/system/app/...` path**, while `Android.bp` installs the app
   as `product_specific` (and the Magisk module installs to `system/product/priv-app`). Those three
   cannot all be right at once. This was found while writing this page and is **not** fixed here,
   because the correct value depends on the partition you choose — pick one and make all three agree.
3. **The sepolicy file has never been through a real `neverallow` pass in this environment** (there is
   no AOSP tree here). Treat it as a reviewed starting point, not a validated policy.

## Support model for ROM maintainers

Bring: the device, the ROM base, which integration path, and the output of the four checks above.
`dmesg | grep -i avc` is the single most useful thing you can attach — a domain that is missing an
allow is a five-line fix when the denial is included and a guessing game otherwise.
