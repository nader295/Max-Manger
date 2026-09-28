<a id="top"></a>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/assets/banner-dark.svg?v=2">
  <source media="(prefers-color-scheme: light)" srcset="docs/assets/banner-light.svg?v=2">
  <img src="docs/assets/banner-dark.svg?v=2" width="100%"
       alt="MaxManager — performance control that asks before it acts">
</picture>
</p>

<p align="center">
  <a href="https://github.com/nader295/Max-Manger/releases/latest"><img alt="Download" src="https://img.shields.io/badge/download-latest_release-2ea44f?style=for-the-badge"></a>
  <img alt="Android" src="https://img.shields.io/badge/Android-10%2B-3DDC84?style=for-the-badge&logo=android&logoColor=white">
  <img alt="Root" src="https://img.shields.io/badge/root-required-607D8F?style=for-the-badge">
  <img alt="Languages" src="https://img.shields.io/badge/languages-84%2B-607D8F?style=for-the-badge">
  <img alt="Licence" src="https://img.shields.io/badge/licence-proprietary-B36A42?style=for-the-badge">
</p>

<p align="center">
  <b>English</b> ·
  <a href="README.ar.md">العربية</a>
</p>

<p align="center">
  <a href="#install"><b>Install the module</b></a> ·
  <a href="#what-it-looks-like"><b>See the screens</b></a> ·
  <a href="docs/README.md"><b>Read the docs</b></a>
</p>

<p align="center"><b>This repository is MaxManager's public face</b> — the documentation, the
screenshots and the downloads. The application and its native layer are <b>private source</b>:
nothing here builds, and the command lines quoted in these pages run inside that repository.</p>

| | |
| --- | --- |
| **Platform** | Android 10 or newer (API 29) · `arm64-v8a` and `armeabi-v7a` |
| **Root** | Magisk · KernelSU · KernelSU Next — or Shizuku for part of it |
| **Screens** | 53 across nine control domains, plus a tools shelf |
| **Languages** | 84 locales plus English, right-to-left enforced by a gate |
| **Licence** | Proprietary — the copyright holder's written permission is required |

---

<a id="contents"></a>

<details>
<summary><b>Contents</b> — the seventeen sections of this page, in reading order</summary>

| | Section | The one question it answers |
| --- | --- | --- |
| 1 | [In ten seconds](#in-ten-seconds) | What is this, and who is it for? |
| 2 | [What it looks like](#what-it-looks-like) | The screens, and the design document behind them |
| 3 | [Why it is built this way](#the-story) | The three layers and the one write path |
| 4 | [Max Atlas](#max-atlas) | Why anything works on *your* phone |
| 5 | [Max AI](#max-ai) | What changes, and how it is measured |
| 6 | [What you can control](#what-you-can-control) | The nine domains, per-app control, profiles |
| 7 | [Watching, measuring, diagnosing](#watching) | Live readings, overlays, logs, diagnostics |
| 8 | [Languages](#languages) | 84 locales, and RTL as a gate |
| 9 | [Requirements](#requirements) | Will it work on my phone? |
| 10 | [Install](#install) | How to get it running |
| 11 | [For ROM developers](#for-rom-developers) | The AOSP integration kit |
| 12 | [What it will not do](#what-it-wont-do) | The rules that cannot be switched off |
| 13 | [Documentation](#documentation) | Every page under `docs/` |
| 14 | [FAQ](#faq) | The questions that keep coming back |
| 15 | [Support](#support) | Where a bug report goes |
| 16 | [Licence](#licence) | Proprietary, stated plainly |
| 17 | [Credits](#credits) | Who wrote the parts this project did not |

</details>

---

<a id="in-ten-seconds"></a>

## <img src="docs/assets/ic-timer.svg?v=2" width="22" height="22" align="absmiddle" alt="Ten seconds"> In ten seconds

**MaxManager is a performance and power control panel for rooted Android — one that only shows you
controls that actually exist on your device.**

Rooting hands you hundreds of kernel interfaces and no map. Most tuning apps answer that with a wall
of switches: half of them do nothing on your hardware, none of them tell you what they changed, and
when something breaks you find out later. MaxManager is built the other way round.

- **A control your kernel does not expose is not on the screen.** Not greyed out — absent.
- **Every change is confirmed, not assumed.** The value is read back after it is written, and a change
  that did not hold is reported as a failure with a rollback attempted.
- **When it does not know, it says `status_unknown`.** Never a plausible zero.
- **Nothing runs behind your back.** The engines are off until you turn them on, and every write goes
  through one audited path.

Two doors in, depending on who you are:

| **I want to use it** | **I build ROMs** |
| --- | --- |
| [What it looks like](#what-it-looks-like) · [What you can control](#what-you-can-control) · [Install](#install) | [For ROM developers](#for-rom-developers) — the integration kit, on request |
| 53 screens across nine control domains, plus a tools shelf | Soong files, an init service, a sepolicy domain, a privileged-permission allowlist |
| [Requirements](#requirements): Android 10+, root (or Shizuku for part of it) | Permission-first: proprietary software, written permission required |

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="what-it-looks-like"></a>
<a id="screenshots"></a>

## <img src="docs/assets/ic-phone.svg?v=2" width="22" height="22" align="absmiddle" alt="Screens"> What it looks like

<!-- screenshots:start -->
<details open>
<summary><b>Home and Max AI</b> · 6 frames</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/01-start.png"><img src="docs/screenshots/01-start.png" width="140" alt="MaxManager — Start"></a><br><sub><b>Start</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/02-now-home.png"><img src="docs/screenshots/02-now-home.png" width="140" alt="MaxManager — Home"></a><br><sub><b>Home</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/03-max-ai.png"><img src="docs/screenshots/03-max-ai.png" width="140" alt="MaxManager — Max AI"></a><br><sub><b>Max AI</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/04-max-ai-plan.png"><img src="docs/screenshots/04-max-ai-plan.png" width="140" alt="MaxManager — Max AI plan"></a><br><sub><b>Max AI plan</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/05-max-ai-live.png"><img src="docs/screenshots/05-max-ai-live.png" width="140" alt="MaxManager — Live control"></a><br><sub><b>Live control</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/06-max-ai-loops.png"><img src="docs/screenshots/06-max-ai-loops.png" width="140" alt="MaxManager — Loop results"></a><br><sub><b>Loop results</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details open>
<summary><b>Per-app control</b> · 6 frames</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/26-apps-list.png"><img src="docs/screenshots/26-apps-list.png" width="140" alt="MaxManager — Apps"></a><br><sub><b>Apps</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/27-app-settings.png"><img src="docs/screenshots/27-app-settings.png" width="140" alt="MaxManager — Per-app"></a><br><sub><b>Per-app</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/28-app-settings-display.png"><img src="docs/screenshots/28-app-settings-display.png" width="140" alt="MaxManager — Per-app display"></a><br><sub><b>Per-app display</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/29-app-settings-gaming.png"><img src="docs/screenshots/29-app-settings-gaming.png" width="140" alt="MaxManager — Per-app gaming"></a><br><sub><b>Per-app gaming</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/30-app-settings-power.png"><img src="docs/screenshots/30-app-settings-power.png" width="140" alt="MaxManager — Per-app power"></a><br><sub><b>Per-app power</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/31-app-settings-tune.png"><img src="docs/screenshots/31-app-settings-tune.png" width="140" alt="MaxManager — Per-app tuning"></a><br><sub><b>Per-app tuning</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details>
<summary><b>Control hubs</b> · 8 frames</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/07-control-hub.png"><img src="docs/screenshots/07-control-hub.png" width="140" alt="MaxManager — Control"></a><br><sub><b>Control</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/08-control-lanes.png"><img src="docs/screenshots/08-control-lanes.png" width="140" alt="MaxManager — Control lanes"></a><br><sub><b>Control lanes</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/09-control-tools.png"><img src="docs/screenshots/09-control-tools.png" width="140" alt="MaxManager — Control tools"></a><br><sub><b>Control tools</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/10-control-tools-2.png"><img src="docs/screenshots/10-control-tools-2.png" width="140" alt="MaxManager — More tools"></a><br><sub><b>More tools</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/11-control-hub-2.png"><img src="docs/screenshots/11-control-hub-2.png" width="140" alt="MaxManager — Control (2)"></a><br><sub><b>Control (2)</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/12-hub-display.png"><img src="docs/screenshots/12-hub-display.png" width="140" alt="MaxManager — Display"></a><br><sub><b>Display</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/13-hub-responsiveness.png"><img src="docs/screenshots/13-hub-responsiveness.png" width="140" alt="MaxManager — Responsiveness"></a><br><sub><b>Responsiveness</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/14-hub-power.png"><img src="docs/screenshots/14-hub-power.png" width="140" alt="MaxManager — Power"></a><br><sub><b>Power</b></sub></td>
  </tr>
</table>

</details>

<details>
<summary><b>CPU and GPU</b> · 5 frames</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/15-cpu-cores.png"><img src="docs/screenshots/15-cpu-cores.png" width="140" alt="MaxManager — CPU cores"></a><br><sub><b>CPU cores</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/16-core-limits.png"><img src="docs/screenshots/16-core-limits.png" width="140" alt="MaxManager — Core limits"></a><br><sub><b>Core limits</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/17-cpu-preference-tweaks.png"><img src="docs/screenshots/17-cpu-preference-tweaks.png" width="140" alt="MaxManager — Tweaks"></a><br><sub><b>Tweaks</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/18-gpu-studio-profiles.png"><img src="docs/screenshots/18-gpu-studio-profiles.png" width="140" alt="MaxManager — GPU profiles"></a><br><sub><b>GPU profiles</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/19-gpu-studio-live.png"><img src="docs/screenshots/19-gpu-studio-live.png" width="140" alt="MaxManager — GPU live"></a><br><sub><b>GPU live</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details>
<summary><b>Memory and display</b> · 2 frames</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/20-memory-zram.png"><img src="docs/screenshots/20-memory-zram.png" width="140" alt="MaxManager — ZRAM"></a><br><sub><b>ZRAM</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/21-display-resolution.png"><img src="docs/screenshots/21-display-resolution.png" width="140" alt="MaxManager — Resolution"></a><br><sub><b>Resolution</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details>
<summary><b>Battery and charging</b> · 4 frames</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/22-power-charging.png"><img src="docs/screenshots/22-power-charging.png" width="140" alt="MaxManager — Charging"></a><br><sub><b>Charging</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/23-bypass-check.png"><img src="docs/screenshots/23-bypass-check.png" width="140" alt="MaxManager — Bypass check"></a><br><sub><b>Bypass check</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/24-doze.png"><img src="docs/screenshots/24-doze.png" width="140" alt="MaxManager — Doze"></a><br><sub><b>Doze</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/25-sleep-policy.png"><img src="docs/screenshots/25-sleep-policy.png" width="140" alt="MaxManager — Sleep policy"></a><br><sub><b>Sleep policy</b></sub></td>
  </tr>
</table>

</details>

<details>
<summary><b>Settings and tools</b> · 11 frames</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/32-settings-root.png"><img src="docs/screenshots/32-settings-root.png" width="140" alt="MaxManager — Settings"></a><br><sub><b>Settings</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/33-color-palette.png"><img src="docs/screenshots/33-color-palette.png" width="140" alt="MaxManager — Palette"></a><br><sub><b>Palette</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/34-logs.png"><img src="docs/screenshots/34-logs.png" width="140" alt="MaxManager — Logs"></a><br><sub><b>Logs</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/35-max-backup.png"><img src="docs/screenshots/35-max-backup.png" width="140" alt="MaxManager — Backup"></a><br><sub><b>Backup</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/36-backup-plan.png"><img src="docs/screenshots/36-backup-plan.png" width="140" alt="MaxManager — Backup plan"></a><br><sub><b>Backup plan</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/37-backup-apps.png"><img src="docs/screenshots/37-backup-apps.png" width="140" alt="MaxManager — Backup apps"></a><br><sub><b>Backup apps</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/38-permissions.png"><img src="docs/screenshots/38-permissions.png" width="140" alt="MaxManager — Permissions"></a><br><sub><b>Permissions</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/39-permissions-app.png"><img src="docs/screenshots/39-permissions-app.png" width="140" alt="MaxManager — App permissions"></a><br><sub><b>App permissions</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/40-permissions-2.png"><img src="docs/screenshots/40-permissions-2.png" width="140" alt="MaxManager — Permissions (2)"></a><br><sub><b>Permissions (2)</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/41-activity-launcher.png"><img src="docs/screenshots/41-activity-launcher.png" width="140" alt="MaxManager — Activities"></a><br><sub><b>Activities</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/42-set-edit.png"><img src="docs/screenshots/42-set-edit.png" width="140" alt="MaxManager — Property editor"></a><br><sub><b>Property editor</b></sub></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details>
<summary><b>Network, storage and HUD</b> · 6 frames</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/43-network-detail.png"><img src="docs/screenshots/43-network-detail.png" width="140" alt="MaxManager — Network"></a><br><sub><b>Network</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/44-network-scheduler.png"><img src="docs/screenshots/44-network-scheduler.png" width="140" alt="MaxManager — Scheduler"></a><br><sub><b>Scheduler</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/45-storage-detail.png"><img src="docs/screenshots/45-storage-detail.png" width="140" alt="MaxManager — Storage"></a><br><sub><b>Storage</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/46-fps-overlay.png"><img src="docs/screenshots/46-fps-overlay.png" width="140" alt="MaxManager — FPS overlay"></a><br><sub><b>FPS overlay</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/47-fps-overlay-metrics.png"><img src="docs/screenshots/47-fps-overlay-metrics.png" width="140" alt="MaxManager — HUD metrics"></a><br><sub><b>HUD metrics</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/48-fps-overlay-source.png"><img src="docs/screenshots/48-fps-overlay-source.png" width="140" alt="MaxManager — HUD source"></a><br><sub><b>HUD source</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

> **48 of 48 frames captured** · 0 optional extras. A frame not captured yet is absent from the grid above rather than broken; the <a href="docs/screenshots/">screenshots folder</a> holds all of them.
<!-- screenshots:end -->

Every frame here is a **real capture from a device**, taken to the contract in
[`docs/screenshots/`](docs/screenshots/): 1162×2480 PNG, under 400 KiB each, one status-bar
choice across all frames, dark theme throughout, with `-light` and `-ar` variants. The grid is
**generated from the frames that exist** — `tools/screenshot_gallery.py` emits an `<img>` only for a PNG
that is really there, so a frame that has not been captured is **absent rather than broken**, and a frame
dropped in under the contract's name appears the next time the generator runs.

The diagrams on this page — the write path, the Max Atlas cycle, the Max AI loop, the nine domains —
are drawn from the app's own behaviour, strings and tokens rather than from screenshots, and every
claim about a screen here is written from the interface's own words.

The interface is drawn by rules rather than by taste, and those rules are written down value by value
in **[DESIGN.md](DESIGN.md)** — with a gate (`tools/design_doc.py`) that fails the build when the
document and the code disagree.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="the-story"></a>

## <img src="docs/assets/ic-layers.svg?v=2" width="22" height="22" align="absmiddle" alt="Three layers"> Why it is built this way

<p align="center"><img src="docs/assets/control-plane.svg?v=2" width="100%" alt="One write path: screen, arbiter, ownership ledger, verification and rollback, then the kernel interface — and a control whose route is unproven here is labelled as such"></p>

Three layers, and they do not overlap:

1. **[Max Atlas](#max-atlas)** decides **how** a thing can work on this device — which interfaces exist,
   which routes reach them, and what actually succeeded last time.
2. **The control plane** is the only path that writes: one arbiter, an ownership ledger so two writers
   cannot race for the same knob, read-back verification, and a rollback when a write does not hold.
3. **[Max AI](#max-ai)** decides **what** should change and **when** — the smallest change that could
   close the gap, measured afterwards. Off until you turn it on.

One rule covers all three: **a change is written through one path, verified by reading it back, and
re-checked later for silent drift.** If it did not take, you are told — with a rollback attempted —
instead of being shown a green tick.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="max-atlas"></a>

## <img src="docs/assets/ic-atlas.svg?v=2" width="22" height="22" align="absmiddle" alt="Max Atlas"> Max Atlas — the reason anything works on *your* phone

<p align="center"><img src="docs/assets/atlas-cycle.svg?v=2" width="100%" alt="Max Atlas: Discover, Understand, Map, Adapt, Execute, Verify, Learn — what works here is proven here"></p>

Two phones of the same model can expose different kernel interfaces; two kernels can name the same
interface in different units and let you write it or not. Max Atlas asks each interface whether it is
*here*, what it is called, what unit it speaks, whether it can be written — and remembers the answer.

What you feel from that:

1. **Controls that cannot work are not shown.** No dead switches.
2. **Every control is labelled for what it is:** works and verified here · a route exists but is
   unproven here · readable only · present but this build cannot drive it · proved absent · never touch
   (a safety rule) · or **unknown**.
3. **Absence is proved, not assumed.** A read that failed is not an absence; only a listing that
   genuinely lacks a name counts as "not here".
4. **It gets better on your device.** What worked, what failed, and how long either fact stays true are
   remembered — the second run is not the same experiment as the first.

<details>
<summary><b>How this is proven</b> without making your phone the test bench</summary>

Discovery runs under an explicit budget (operations, entries, bytes, time), and when a bound stops a
scan the report says *a limit stopped it* — never "the device had nothing to say". A real run on a
device can be recorded as a **fixture**, and that fixture replays through the same read interface, so
"it needs a device" is not a permanent excuse for untested logic. Knowledge comes from a reviewed
catalogue we stand behind; a community-sourced vocabulary may *suggest* a route but never grants one.

</details>

Full page: **[docs/max-atlas.md](docs/max-atlas.md)**.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="max-ai"></a>

## <img src="docs/assets/ic-ai.svg?v=2" width="22" height="22" align="absmiddle" alt="Max AI"> Max AI — one measured change at a time

<p align="center"><img src="docs/assets/max-ai.svg?v=2" width="100%" alt="Max AI: Notice, Decide, Ask, Verify, Remember — one measured change at a time, and a list of what it will never do"></p>

Max AI watches how the device is actually behaving — speed, heat, battery, memory pressure, which app
is in front — and when the readings say something should change, it changes **one thing**, then
measures whether that helped. It is a loop, not a preset:

- <img src="docs/assets/ic-notice.svg?v=2" width="20" height="20" align="absmiddle" alt="Notice"> **Notice** — it reads this device: temperature, load, battery, memory, the active app. *You notice
  nothing: it is watching, not acting.*
- <img src="docs/assets/ic-decide.svg?v=2" width="20" height="20" align="absmiddle" alt="Decide"> **Decide** — against your objective (speed, balance, battery), it picks the *smallest* change that
  could close the gap. *One control moves, not eight.*
- <img src="docs/assets/ic-ask.svg?v=2" width="20" height="20" align="absmiddle" alt="Ask"> **Ask** — a safety layer with absolute priority says yes or no before anything is written. *A
  protected interface is never touched, engine on or off.*
- <img src="docs/assets/ic-verify.svg?v=2" width="20" height="20" align="absmiddle" alt="Verify"> **Verify** — the value is read back, then the result is measured after a response window. *A change
  that did not hold is not counted as a win.*
- <img src="docs/assets/ic-remember.svg?v=2" width="20" height="20" align="absmiddle" alt="Remember"> **Remember** — the outcome is recorded as a complete, measured episode. *It trusts what has been
  right, and stops trusting what has been wrong.*

**Why it is not a preset:** a preset applies the same numbers to every device and never finds out
whether it helped. Max AI only speaks the vocabulary Max Atlas found on *your* phone, its wins are
measured rather than predicted, and it knows when to stop — when you open a game with its own profile,
Max AI steps aside and keeps watching safety only.

**What it will never do:** write a protected interface · claim a change it did not measure · invent a
reading · hide a failure. Every cycle is kept as a record you can open: what it saw, what it wanted,
what it changed, what the device did afterwards, and what it learned.

**It is off until you turn it on.** Manual control is the default state, and the profile you choose
stays a manual baseline — never an instruction to the engine.

<details>
<summary><b>For sceptics:</b> how a decision is kept honest</summary>

A decision is only counted when it was executed through the single write path **and** verified. The
engine keeps an ownership ledger so no two writers race for the same knob, a trust model so a source
that has been wrong is no longer believed equally, and a journal of complete episodes rather than a
summary of intentions. If the user undoes a change by hand, that is recorded as a measured rejection —
not as noise.

</details>

Full page: **[docs/max-ai.md](docs/max-ai.md)**.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="what-you-can-control"></a>

## <img src="docs/assets/ic-sliders.svg?v=2" width="22" height="22" align="absmiddle" alt="Controls"> What you can control

<p align="center"><img src="docs/assets/domains.svg?v=2" width="100%" alt="Nine control domains: CPU, GPU, memory, display, responsiveness, thermal, power, storage and compiler, network"></p>

Nine areas, each in its own hub. The line under each name is the app's **own** one-line description of
the area, quoted from the interface.

- <img src="docs/assets/ic-cpu.svg?v=2" width="20" height="20" align="absmiddle" alt="CPU"> **CPU** — *Cores, governor, vendor boost and kernel preferences.* Turn individual cores on or off,
  pin scheduling groups to clusters, set a floor and ceiling per cluster, choose governors, edit kernel
  preferences.
- <img src="docs/assets/ic-gpu.svg?v=2" width="20" height="20" align="absmiddle" alt="GPU"> **GPU** — *GPU frequencies and graphics-specific vendor parameters.* Frequency presets and manual
  bounds, GPU governor, shader-core power policy, the vendor boost pipeline, and a documented
  thermal-throttle bypass.
- <img src="docs/assets/ic-memory.svg?v=2" width="20" height="20" align="absmiddle" alt="Memory"> **Memory** — *Compression, VM behaviour and swappiness.* Size ZRAM or turn it off, pick the
  compression engine, tune swappiness and reclaim. The engine reads **memory stall pressure**, not fill
  percentage — a nearly-full-but-idle device and a stalling device need opposite responses.
- <img src="docs/assets/ic-display.svg?v=2" width="20" height="20" align="absmiddle" alt="Display"> **Display** — *Refresh rate, colour and canvas scale.* Refresh rate, colour channels, saturation,
  gamut and HDR response, brightness curves, night light, animation scales, screen timeout.
- <img src="docs/assets/ic-touch.svg?v=2" width="20" height="20" align="absmiddle" alt="Responsiveness"> **Responsiveness** — *Touch, frame pacing and scheduling latency.* Touch sampling and smoothing,
  double-tap to wake, FPS GO / GED parameters, frame-aware scheduling.
- <img src="docs/assets/ic-thermal.svg?v=2" width="20" height="20" align="absmiddle" alt="Thermal"> **Thermal** — *Temperatures, throttling and thermal parameters.* Live zone temperatures, thermal
  policy, and what the device is throttling right now.
- <img src="docs/assets/ic-battery.svg?v=2" width="20" height="20" align="absmiddle" alt="Power"> **Power** — *Charging, bypass, sleep and battery health.* Charge current limits, a charge ceiling to
  slow battery wear, bypass charging, aggressive doze, standby whitelist, battery health.
- <img src="docs/assets/ic-storage.svg?v=2" width="20" height="20" align="absmiddle" alt="Storage and compiler"> **Storage & compiler** — *Compilation mode and storage health.* Re-run ART compilation with a chosen
  filter, reset compiled state, storage health.
- <img src="docs/assets/ic-network.svg?v=2" width="20" height="20" align="absmiddle" alt="Network"> **Network** — *Traffic scheduling and link state.* TCP congestion algorithm, fast-open/SACK/ECN, SYN
  cookies, socket reuse, I/O scheduler tunables, link state.

Anything your device does not expose in one of these areas simply is not listed.

### One app at a time

Open **Apps**, pick an app, and give it its own treatment without touching the rest of the system:
performance profile (Power / Balanced / Gaming / Performance / Custom) · refresh rate · render
resolution · thermal ceiling · CPU and GPU governor (only the ones your kernel reports, and only
governors supported by *all* CPU policies) · foreground priority lock · I/O priority boost · a per-app
reset.

Every app shows its **effective state** in plain words — per-app control is off · using the global
profile · app override active — and while a game with its own profile is in front, **Max AI switches to
monitoring only**.

### Profiles

A profile is a named set of behaviour you can apply, tune, save and share: **Power** (cool and frugal),
**Balanced** (the everyday baseline), **Gaming** (GPU held in the upper range for steadier frame
pacing), **Performance** (full capability, held as the hardware allows), **Custom** (yours).

Two things make profiles more than bookmarks:

- **They are shareable, and the source travels with the number.** On export each value carries where it
  came from — a shipped default, a value you changed, or a measurement *claimed* by whoever exported
  it. On import the app says exactly what it accepted and refused, and a profile from another chipset
  says so: a value measured over there is not a measurement over here.
- **They are reachable from Quick Settings.** A tile switches the profile without opening the app, and a
  second tile drives bypass charging.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="watching"></a>

## <img src="docs/assets/ic-pulse.svg?v=2" width="22" height="22" align="absmiddle" alt="Live readings"> Watching, measuring, diagnosing

- <img src="docs/assets/ic-pulse.svg?v=2" width="20" height="20" align="absmiddle" alt="Max Live"> **Max Live** — the live picture: current readings, what automation is allowed to do now and why, what
  it would do next, and whether it can be undone.
- <img src="docs/assets/ic-phone.svg?v=2" width="20" height="20" align="absmiddle" alt="Home"> **Home** — device state, the active app, the running profile, temperatures and storage at a glance.
- <img src="docs/assets/ic-display.svg?v=2" width="20" height="20" align="absmiddle" alt="FPS overlay"> **FPS overlay** — a draggable on-screen readout of FPS, CPU and RAM over any game, with a fallback
  reading method and a **Vulkan/OpenGL** label when that is how the app renders.
- <img src="docs/assets/ic-cpu.svg?v=2" width="20" height="20" align="absmiddle" alt="Process monitor"> **Process monitor** — per-process CPU and RAM, force-stop, SIGKILL, and a floating overlay.
- <img src="docs/assets/ic-doc.svg?v=2" width="20" height="20" align="absmiddle" alt="Log viewer"> **Log viewer** — live logcat with filtering and search, plus a shareable report whose **glossary is
  written into the log file itself**.
- <img src="docs/assets/ic-verify.svg?v=2" width="20" height="20" align="absmiddle" alt="Diagnostics"> **Diagnostics** — a live diagnostic centre, per-control route health, a reproducible device blueprint,
  and a support report you choose to send.
- <img src="docs/assets/ic-question.svg?v=2" width="20" height="20" align="absmiddle" alt="Why it did not work"> **"Why didn't it work?"** — for a per-app setting: what it wanted, what the hardware is holding, and
  where to look next.

Nothing here phones home. The support report is assembled locally, minimised, and leaves the device
only when you send it.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="languages"></a>

## <img src="docs/assets/ic-globe.svg?v=2" width="22" height="22" align="absmiddle" alt="Languages"> Languages

<p align="center"><img src="docs/assets/locales.svg?v=2" width="100%" alt="84 languages, and right-to-left is first class"></p>

- **84 locales** plus English; the picker follows the system language without a restart.
- **Light and dark**, with a themable key colour and a custom palette screen.
- **RTL is enforced** by a gate, not by hope — Arabic, Farsi, Hebrew and Urdu ship.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="requirements"></a>

## <img src="docs/assets/ic-checklist.svg?v=2" width="22" height="22" align="absmiddle" alt="Requirements"> Requirements

| | |
| --- | --- |
| **Android** | 10 or newer (API 29), built against API 37 |
| **Root** | Magisk, KernelSU or KernelSU Next — the module is the supported path. Shizuku gives ADB-level access without root, and several tools work with it |
| **Architecture** | `arm64-v8a`, `armeabi-v7a` |
| **Chipsets** | Dedicated strategies for Snapdragon · MediaTek · Exynos · Tensor · Unisoc. Everything else works through what your kernel exposes |
| **Out of scope** | No performance promises, and no benchmark deltas: a number measured on one device is not a claim about yours |

The real answer to *"will it work on my phone?"* is the capability map inside the app on your own
device. Details: **[docs/compatibility.md](docs/compatibility.md)**.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="install"></a>

## <img src="docs/assets/ic-download.svg?v=2" width="22" height="22" align="absmiddle" alt="Install"> Install

MaxManager ships as a **systemless module** — nothing in `/system` is modified permanently, and
uninstalling puts everything back.

1. Download `MaxManager-v1.0-module.zip` from **[Releases](https://github.com/nader295/Max-Manger/releases/latest)** and flash it in **Magisk** or **KernelSU** (or a compatible root manager).
2. Reboot.
3. Open **MaxManager** and walk through **Setup**, which explains what *your* device exposes.

The same release carries **`MaxManager-checksums.txt`** — one digest for the package and one for
each of its contents — so you can verify the download before flashing it; the two commands are in
**[docs/releases/v1.0.md](docs/releases/v1.0.md)**. If the
module fails to reach a stable boot twice in a row, it disables itself and says so in its own
description.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="for-rom-developers"></a>

## <img src="docs/assets/ic-cube.svg?v=2" width="22" height="22" align="absmiddle" alt="ROM developers"> For ROM developers

<p align="center"><img src="docs/assets/integration.svg?v=2" width="100%" alt="Three integration paths — systemless module, AOSP integration from android/aosp, KernelSU Next — and the three names that must agree: the binary path, the init service and the SELinux labels"></p>

The integration kit is **not published here** — the source is private. It is released to ROM
maintainers **on written request**: Soong build files, an init service, a sepolicy domain and a
privileged-permission allowlist, plus the same module packaged for KernelSU Next.

**What you get:** a privileged control app, five native binaries (the device service, chipset profiles,
the thermal daemon, a utility configurator and a game preloader), and a module that installs and
removes itself without touching `/system` permanently.

**What you need:** a platform-signed, privileged build of the app; the daemon on
`/system/bin/sys.maxmanager-service`; the init service; and the sepolicy rules. Three names must agree
exactly — the binary path, the init service and the SELinux label — and the diagram above shows them.

> **Permission first.** MaxManager is **proprietary software**. The kit is here so maintainers can
> evaluate and integrate it with the copyright holder's **written permission** — [`LICENSE`](LICENSE)
> grants no right otherwise. Ask first via [Support](#support).

Start here: **[docs/rom-integration.md](docs/rom-integration.md)** — three integration paths, the
checklist, and two mismatches we found in the kit and reported rather than papered over.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="what-it-wont-do"></a>

## <img src="docs/assets/ic-shield.svg?v=2" width="22" height="22" align="absmiddle" alt="Never touched"> What it will not do

The parts of the app you cannot turn off, and would not want to:

- **No screen writes to the kernel.** Every mutation goes through one arbiter with an ownership ledger
  and a journal — so "who changed this, when, and what happened next" is answerable.
- **No fabricated readings.** An unknown value is shown as `status_unknown`, never as a plausible `0`.
- **No success that was not verified.** Read-back after every write; drift is re-checked later.
- **Thermal trip points are never written**, on any device. That is a rule, not a limitation.
- **A reviewed never-touch list** guards the interfaces that must not be written, matched by fragment on
  purpose so vendor variants cannot slip through.
- **No telemetry, no accounts, no silent uploads.**

And where the honesty has an edge: **nothing in this repository claims hardware behaviour it has not
measured.** [`docs/verification.md`](docs/verification.md) lists what is proven here, what runs on any
machine without a device, and what *needs a phone* — written as "not verified in this environment"
rather than as a pass. That sentence is a rule in this project, not a hedge.

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="documentation"></a>

## <img src="docs/assets/ic-doc.svg?v=2" width="22" height="22" align="absmiddle" alt="Documentation"> Documentation

This page is the tour. The answers you reach for afterwards live in **[`docs/`](docs/README.md)**:

| Page | One line |
| --- | --- |
| [features.md](docs/features.md) | Every capability, what it is for, and where it is in the app |
| [max-ai.md](docs/max-ai.md) | The decision engine: objective, safety, measurement, journal, learning |
| [max-atlas.md](docs/max-atlas.md) | The adaptation engine, stage by stage |
| [rom-integration.md](docs/rom-integration.md) | Integration paths, the AOSP kit, SELinux, verification |
| [compatibility.md](docs/compatibility.md) | Android versions, ABIs, root managers, chipsets — and what is out of scope |
| [profiles.md](docs/profiles.md) | Chipset strategies and the module's native executables |
| [thermal.md](docs/thermal.md) | The thermal daemon: zone fusion, policy, prediction, learning |
| [architecture.md](docs/architecture.md) | How the app, the daemons and the kernel interfaces fit together |
| [releases/v1.0.md](docs/releases/v1.0.md) | The v1.0 release notes, and how to verify the download |
| [verification.md](docs/verification.md) | How every claim here is measured — and what cannot be measured |
| [faq.md](docs/faq.md) | The questions that keep coming back |
| [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) | The third-party components, with their notices |

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="faq"></a>

## <img src="docs/assets/ic-question.svg?v=2" width="22" height="22" align="absmiddle" alt="FAQ"> FAQ

<details>
<summary><b>Does it need root?</b></summary>

Yes, for the full control plane: it is a Magisk/KernelSU module, and the app reaches the kernel through
one audited root bridge. Shizuku (ADB-level, no root) is detected too and unlocks several read-and-write
tools.

</details>

<details>
<summary><b>Is Max AI on by default?</b></summary>

No. Manual control is the default state; nothing self-enables. When you do turn it on, the safety layer
keeps absolute priority.

</details>

<details>
<summary><b>What happens if something goes wrong?</b></summary>

Values are read back after being written, a mismatch is surfaced with a rollback attempted, a drift
guard re-checks later, and the installer disables itself if it fails to boot twice in a row.

</details>

<details>
<summary><b>Why does an unknown value show as <code>status_unknown</code> instead of 0?</b></summary>

Because `0` is a claim. The app says *unknown* when it does not know, rather than showing a
plausible-looking zero.

</details>

<details>
<summary><b>Does it send my data anywhere?</b></summary>

No telemetry and no silent upload. The diagnostic report is built locally, minimised, and leaves your
device only if you hand the file over yourself.

</details>

<details>
<summary><b>How do I remove it completely?</b></summary>

Uninstall the module in your root manager. Nothing in `/system` was permanently modified.

</details>

<details>
<summary><b>Why is the licence proprietary?</b></summary>

The project's own choice, stated in [`LICENSE`](LICENSE). A public repository is not the same thing as
an open-source project. Third-party components keep their own licences and are catalogued in
[`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md).

</details>

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="support"></a>

## <img src="docs/assets/ic-bubble.svg?v=2" width="22" height="22" align="absmiddle" alt="Support"> Support

- **Telegram:** [@ROBINHOOD_GROUP_RODIN](https://t.me/ROBINHOOD_GROUP_RODIN) — bug reports, ideas, builds.
- **Issues:** please include the device, the ROM, the root manager and what the app showed. If it said
  `status_unknown`, say so — that is a fact about your device, not a bug you have to fix first.

<a id="licence"></a>

## <img src="docs/assets/ic-seal.svg?v=2" width="22" height="22" align="absmiddle" alt="Licence"> Licence

**Proprietary.** Copyright (C) 2026 **Nader Magdy**. All rights reserved. See [`LICENSE`](LICENSE) for
the full terms — no right is granted to use, copy, modify or distribute without the copyright holder's
prior written permission.

Third-party components included in this repository, or built against it, keep **their own** licences
(Apache-2.0 for `archdaemon/` and `thermalcore/`, BSD-3-Clause for the embedded `vmtouch`, and others);
their notices are in [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md).

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>

---

<a id="credits"></a>

## <img src="docs/assets/ic-credit.svg?v=2" width="22" height="22" align="absmiddle" alt="Credits"> Credits

MaxManager is not written alone. These are the works it thanks — and every notice their licences
require stays in [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md), which remains the binding list.

| Project | Copyright | Licence |
| --- | --- | --- |
| [AZenith](https://github.com/Liliya2727/AZenith) | (C) 2025-2026 Zexshia | Apache-2.0 |
| [Encore Tweaks](https://github.com/Rem01Gaming/encore) | (C) 2024-2025 Rem01Gaming | Apache-2.0 |
| [Rianixia-ThermalCore](https://github.com/ryanistr/Rianixia-ThermalCore) | (C) 2025-2026 ryanistr | Apache-2.0 |
| [VMTouch](https://github.com/hoytech/vmtouch) | (c) 2009-2023 Doug Hoyte and contributors | BSD-3-Clause |

<sub><b>Missing from this list?</b> If a work of yours ends up used here and is not named above,
message me privately — or find me in the [group](https://t.me/ROBINHOOD_GROUP_RODIN) — and I will add it.</sub>

<p align="right"><sub><a href="#top">↑ Back to top</a></sub></p>
