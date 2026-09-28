# MaxManager documentation

This folder is the written half of MaxManager. The [README](../README.md) is the tour; these pages are
the answers you reach for when the tour raised a question.

## Where to start, by who you are

| You are | Read this first |
| --- | --- |
| **A user** deciding whether to install it | [README → Install](../README.md#install) · then [compatibility](compatibility.md) |
| **A user** wondering what a screen does | [features](features.md) · [screenshots](screenshots/) |
| **A user** with a problem | [FAQ](faq.md) · the app's own **Settings → Diagnostics** and **Logs** |
| **A ROM developer** | [rom-integration](rom-integration.md) — the whole guide |
| **A kernel / platform engineer** | [architecture](architecture.md) · [thermal](thermal.md) · [profiles](profiles.md) |
| **Curious how it thinks** | [Max Atlas](max-atlas.md) · [Max AI](max-ai.md) |
| **Someone checking our claims** | [verification](verification.md) |

## The pages

| Page | One line |
| --- | --- |
| [features.md](features.md) | Every capability, what it is for, and where it lives in the app |
| [max-atlas.md](max-atlas.md) | The adaptation engine: discover → understand → map → adapt → execute → verify → learn |
| [max-ai.md](max-ai.md) | The decision engine: objective, safety, measurement, journal, learning |
| [architecture.md](architecture.md) | How the app, the daemons and the kernel interfaces fit together |
| [rom-integration.md](rom-integration.md) | Three integration paths, the AOSP kit, SELinux, verification |
| [compatibility.md](compatibility.md) | Android versions, ABIs, root managers, chipsets, what is not supported |
| [thermal.md](thermal.md) | The thermal daemon: policy, learning, cooling, prediction |
| [profiles.md](profiles.md) | Chipset strategies and the module's native executables |
| [verification.md](verification.md) | How every claim in this repository is measured, and what cannot be |
| [releases/v1.0.md](releases/v1.0.md) | The v1.0 release notes, and how to verify the download |
| [faq.md](faq.md) | The questions that keep coming back |
| [../DESIGN.md](../DESIGN.md) | The design language: tokens, roles, components, motion, and the gaps we know about |
| [screenshots/](screenshots/) | The 48 screens, in the order the app shows them |

## What this repository contains, and what it deliberately keeps

MaxManager is **proprietary software** (see [LICENSE](../LICENSE)): it is not an open-source project and
this repository is not a contribution surface. What it is, is the project's public face — the written
half and the downloads.

| Layer | Where | Audience |
| --- | --- | --- |
| Product story and documentation | `README.md` · `README.ar.md` · `docs/` | Everyone |
| Screenshots | `docs/screenshots/` | Everyone |
| Visual assets for the docs | `docs/assets/` | Everyone |
| Flashable module and checksums | the repository's **Releases** | Everyone |
| The app, the daemons, the installer | private | The project itself |

**The source is not published.** There is no build here and nothing to compile: the pages describe the
shipped product, and the measurements they quote are re-derived inside the private repository rather
than by a reader of this one. Where a number cannot be checked from here, the page says so instead of
implying otherwise — see [verification](verification.md).

**No secrets live here.** No keystore, no signing password, no API key, no device identifier.
