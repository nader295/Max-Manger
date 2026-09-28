# Compatibility

The honest version: MaxManager runs on a wide range of rooted Android devices because it **asks before
it acts**, and it reports what it could not confirm rather than pretending. This page says what is
guaranteed, what is likely, and what is explicitly out of scope.

## Platform

| | Value | Source |
| --- | --- | --- |
| Minimum Android | **10** (API 29) | `minSdk = 29` in `manager/app/build.gradle.kts` |
| Built against | API 37 (`compileSdk` / `targetSdk`) | same file |
| ABIs | `arm64-v8a`, `armeabi-v7a` | module payload in `mainfiles/customize.sh` |
| Root managers | Magisk · KernelSU / KernelSU Next | `mainfiles/` (Magisk) and `android/kernelsu/` |
| Second privilege layer | **Shizuku** — used where it can help, never as a substitute for the module | `core/privilege/` |
| Chipsets with dedicated strategies | Snapdragon · MediaTek · Exynos · Tensor · Unisoc | `binprofiles/src/chipsets/` |
| Other chipsets | Supported through discovery: the app uses whatever the kernel exposes | [max-atlas.md](max-atlas.md) |

## What "supported" means here

The capability map has seven states, and only **one** of them claims success — `SUPPORTED`, which
requires a write that was verified by reading the device back, not a command that was sent.

| State | What the user sees |
| --- | --- |
| `SUPPORTED` | The control works here, and we have seen it settle |
| `WRITABLE` | A route exists; success is not yet proven on this device |
| `READ_ONLY` | We can read it, we cannot (or must not) write it |
| `NEEDS_ADAPTER` | The interface exists; this build has no proven way to drive it |
| `UNAVAILABLE` | Absence was **proved** by a listing |
| `NEVER_TOUCH` | A reviewed safety rule forbids writing it — always |
| `UNKNOWN` | Not measured, or nothing answered and absence was never proved |

So "is my device compatible?" has a better answer than a list: **open it and read the map.** A control
your device does not expose never appears as a switch that does nothing.

## Known limits, stated plainly

- **Root is required** for the module path. The app can do some read-only work with Shizuku, but the
  control plane is designed around the module being installed.
- **Some vendor interfaces are simply not writable** on some kernels (locked OPP tables, missing
  cpufreq policies, read-only sysfs). Atlas marks them and moves on; it does not substitute a value
  you did not ask for.
- **Thermal trip points are never written**, on any device. That is a rule, not a device limitation.
- **The AOSP integration kit is a reviewed starting point, not a validated policy** for your tree — see
  [rom-integration.md](rom-integration.md), including two mismatches we found and reported there.
- **No performance promises.** We do not publish benchmark deltas, because a number measured on one
  device with one workload is not a claim about yours. What is measured here is stated as measured,
  and everything else is written as what it is.

## Devices confirmed by the project

The most reliable device list is not a list — it is the capability map on your own phone, plus the
project's issue channel for reports from other users. If you integrate MaxManager into a ROM, say so in
the community group; the reports from ROM maintainers are the ones that tend to find real
incompatibilities first.
