# Thermal — the `thermalcore` daemon

Thermal management is where "tuning" usually turns into a fire. The interesting engineering here is not
a ceiling value; it is behaving correctly while the device changes under you.

The daemon is `sys.maxmanager-rianixiathermalcore`, a Rust crate at `thermalcore/`. It descends from
**Rianixia-ThermalCore** (Apache-2.0, © ryanistr) and keeps that notice; see
[THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md).

## What is inside

| Module | Responsibility |
| --- | --- |
| `thermal_zones` | **Zone fusion** — multiple thermal zones read as one picture instead of N unrelated numbers |
| `state` | Thermal state definitions: the vocabulary the rest of the daemon reasons in |
| `monitor` | The sampling loop |
| `policy_manager` | The **PID controller** — the actual decision about how much to pull back |
| `prediction` | A predictive model, so the response starts before the limit is hit rather than after |
| `effectiveness` | Tracks whether a mitigation *worked*, instead of assuming it did |
| `learning` | Context awareness and target selection: the daemon adapts to this device |
| `cooling` | Cooling devices — using them as resources, not as a last resort |
| `cpu` | CPU statistics feeding the above |
| `context` | External context awareness |
| `android_ffi` | System properties and logging bindings |
| `constants`, `utils` | Tunables and monotonic time |
| `simulator` | A host-side simulator (cargo feature): run a trace and watch the policy react, without a phone |

## Why a PID controller and not thresholds

Two thresholds can only say "too hot / fine". A device that is 4 °C over the line and a device that is
20 °C over the line do not deserve the same response, and a fixed response to a fixed threshold is how
you get oscillation: pull back hard, cool instantly, spring back up, repeat. A controller that reacts to
the *magnitude* of the overshoot settles instead of oscillating — and the effectiveness tracker is what
tells it whether its last correction was worth anything.

## Honest limits

- **Constants are calibrated by trace, not by taste.** The interesting numbers (gains, floors, step
  sizes, windows) are chosen to behave on a simulated trace, and the simulator exists so that can be
  re-run instead of argued about.
- **A real device can still surprise it.** Vendor thermal behaviour under sustained load is not fully
  reproducible off-device; the calibration is a starting point that the learning layer moves from.
- **It does not touch the hardware's own protection.** Thermal trip points are on the never-touch list.
  The daemon manages *the performance ceiling you asked for*, not the safety mechanism that protects
  your phone from itself.

## How it connects to the rest

Thermal is a domain like any other: its ceiling is written through the same arbiter, verified by the
same read-back, and reported in the same vocabulary. Per-app thermal ceilings exist as their own model
(`ThermalCurve`, `ThermalGuard`, `ThermalCeilingRouter`) so that "this game gets more headroom" is a
policy decision expressed in the normal way, not a private loop inside a monitor.
