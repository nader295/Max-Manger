> **Context.** The gate commands quoted in this document run inside the **private repository**
> that holds the app; this page is the language itself, published so the interface can be read and
> judged.

---
version: alpha
name: MaxManager Design Language
description: >
  MaxManager is a performance and power control panel for rooted Android. Its design language is a
  measuring instrument, not a marketing site: a dark-first surface built from one 4dp spacing scale
  and one card contract, a single accent that belongs to the user's own theme while every status
  colour is fixed and contrast-checked, numbers set in a monospace face so live values never reflow,
  and a standing rule that a value the app does not know is rendered as an em dash — never as a
  plausible zero. Motion exists to explain a change; anything longer than 360ms is decoration and is
  not allowed.

# Every value below is measured from the app's own source, not invented. The source of truth is
# `MaxTokens.kt` (spacing, radii, sizes, alphas, motion, tone) and `theme/Type.kt` (the type scale).
# `tools/design_doc.py --assert` fails the build when this file and those sources disagree — so this
# document cannot quietly become fiction.
colors:
  # Accent follows the user's theme (Material You). There is no single hex for it, on purpose.
  accent: "MaxTone.Accent → MaterialTheme.colorScheme.primary"
  positive-dark: "#5FD9AC"
  positive-light: "#0B6B4F"
  caution-dark: "#FFB86B"
  caution-light: "#8A5200"
  critical-dark: "#FF9A90"
  critical-light: "#9A1B1B"
typography:
  display-large:
    fontFamily: Space Grotesk
    fontSize: 57sp
    lineHeight: 64sp
    letterSpacing: -0.5sp
    fontWeight: Bold
  display-small:
    fontFamily: Space Grotesk
    fontSize: 36sp
    lineHeight: 44sp
    fontWeight: Bold
  headline-small:
    fontFamily: Space Grotesk
    fontSize: 24sp
    lineHeight: 32sp
    fontWeight: SemiBold
  title-medium:
    fontFamily: Space Grotesk
    fontSize: 16sp
    lineHeight: 24sp
    letterSpacing: 0.1sp
    fontWeight: SemiBold
  title-small:
    fontFamily: Space Grotesk
    fontSize: 14sp
    lineHeight: 20sp
    letterSpacing: 0.1sp
    fontWeight: SemiBold
  body-medium:
    fontFamily: Manrope
    fontSize: 14sp
    lineHeight: 20sp
    letterSpacing: 0.25sp
  body-small:
    fontFamily: Manrope
    fontSize: 12sp
    lineHeight: 16sp
    letterSpacing: 0.2sp
  label-small:
    fontFamily: Manrope
    fontSize: 11sp
    lineHeight: 16sp
    letterSpacing: 0.6sp
    fontWeight: Bold
  live-value-large:
    fontFamily: monospace
    fontSize: 34sp
    lineHeight: 38sp
  live-value-medium:
    fontFamily: monospace
    fontSize: 16sp
    lineHeight: 20sp
  live-value-small:
    fontFamily: monospace
    fontSize: 12sp
    lineHeight: 16sp
rounded:
  chip: 10dp
  control: 12dp
  row: 14dp
  inset: 16dp
  tile: 18dp
  group: 22dp
  sheet: 28dp
  pill: 100dp
spacing:
  hairline: 2dp
  xs: 4dp
  sm: 8dp
  md: 12dp
  lg: 16dp
  xl: 20dp
  xxl: 28dp
components:
  page:
    gutter: 20dp
    section-gap: 28dp
    row-gap: 8dp
    group-padding: 4dp
    row-padding-horizontal: 14dp
    row-padding-vertical: 12dp
    page-bottom: 40dp
    bottom-bar-reserve: 112dp
  card:
    radius: 22dp
    border-width: 1dp
    padding: 16dp
    icon-container: 40dp
    icon-glyph: 20dp
    gap: 8dp
    min-height: 92dp
    grid-spacing: 12dp
    title-lines: 2
    description-lines: 2
    min-column-width: 148dp
  section-header:
    accent-width: 4dp
    accent-height: 18dp
    accent-rule-width: 28dp
    accent-rule-height: 4dp
    rule-gap: 8dp
    title-gap: 4dp
    space-before: 20dp
    space-after: 12dp
  touch:
    min-target: 48dp
  reading:
    max-width: 560dp
  alpha:
    border: 0.16f
    border-strong: 0.28f
    tone-wash: 0.045f
    tone-container: 0.10f
    tone-container-strong: 0.18f
    disabled-content: 0.38f
    supporting-text: 0.80f
    edge-light: 0.22f
    halo-glow: 0.07f
  motion:
    instant: 90
    quick: 160
    standard: 240
    deliberate: 360
---

# MaxManager Design Language

This is the design half of the project, written for the people and agents who add to it. It is not
brand poetry: **every number here is read out of the app's own source**, and a gate
(`tools/design_doc.py --assert`) fails when this document and the code disagree. If you change a
token, change it in `MaxTokens.kt` first and regenerate the numbers here.

| File | Who reads it | What it defines |
| --- | --- | --- |
| `AGENTS.md` | Coding agents | How to build the project |
| `DESIGN.md` (this file) | Design agents and reviewers | How the project should look and feel |
| `MAX_TOKENS` | The app | The tokens themselves, as code |

The language at a glance — every bar in this drawing is a value measured further down this page, and
nothing here is drawn from a screenshot:

<p align="center">
<picture>
  <source media="(prefers-color-scheme: light)" srcset="docs/assets/design-language-light.svg?v=2">
  <img src="docs/assets/design-language.svg?v=2" width="100%"
       alt="The MaxManager design language: one accent that follows the theme and three fixed warning colours, three typefaces with one job each, a single 4dp spacing scale, five meaningful corner radii, and a motion budget of at most 360ms">
</picture>
</p>

## Overview

MaxManager is a control panel for people who already know what a governor is. The interface is
therefore closer to an instrument than to an app: it reports, it asks before it writes, and it
refuses to guess. Three commitments shape almost every visual decision.

**One accent, borrowed; every warning, fixed.** The accent is the user's own theme colour
(`MaxTone.Accent` → `MaterialTheme.colorScheme.primary`), so the product takes on the shape of the
phone it runs on. Positive, Caution and Critical are the opposite: fixed hues, contrast-checked
against both surfaces, because a **thermal alert that looks decorative is a correctness bug in a
performance tool** — Material You's dynamic palette can turn `tertiary` into a pastel.

**Hierarchy by role, never by size alone.** There are exactly four ranks and no two share a size:
page title (`headlineSmall` and up) › **section title** (`titleMedium`, SemiBold) › card title
(`titleSmall`) › supporting copy (`bodySmall`). Before this contract the app drew three different
"section header" components — one in the design layer, one in the panel, one in app settings — and a
reader could not tell which rank they were looking at.

**A number the app does not have is an em dash.** `MAX_VALUE_UNAVAILABLE` is `—`. Not `0`, not `--%`,
not an empty cell. A zero is a claim, and this product does not make claims it cannot measure. The
same instinct produced `status_unknown` at the data layer and the five-state trust vocabulary below.

**Key characteristics**

- A dark-first instrument surface: charcoal panels with 1dp hairline borders and a gradient that
  gives them depth without a drop shadow.
- One 4dp spacing scale. `gutter` (20dp), `section` (28dp) and `row` (8dp) are the only values a
  screen body should need.
- One card contract, in one object (`MaxCardSpec`): radius, border, padding, icon container, the two
  reserved title lines that keep neighbours aligned, and the 148dp floor below which a grid drops a
  column instead of squeezing words.
- Monospace is reserved for **live values only** — MHz, percentages, core counts, temperatures. Using
  it for labels too would read as a "coder costume" rather than a decision.
- Radius carries meaning: rows are calm (14dp), groups frame them (22dp), sheets and dialogs are the
  softest (28dp), and **a pill means a status, never a primary action**.

## Colors

### Brand & Accent

- **Accent** (`MaxTone.Accent` → `MaterialTheme.colorScheme.primary`): the screen's own accent — "this
  is the thing you came here for". It is the *only* colour that follows the user's theme. There is no
  fixed hex for it, deliberately: theming is a feature, and pinning the accent would make the product
  fight the phone it lives on.
- The README surface uses `#5FD9AC` as its accent on dark, which is byte-identical to the app's
  Positive-on-dark tone. The page borrows the product's own green rather than inventing a brand colour.

### Semantic tones (fixed)

Tone is a semantic role, not a colour picker. Six exist: `Neutral`, `Accent`, `Positive`, `Caution`,
`Critical`, `Inactive`.

| Tone | On dark | Contrast | On light | Contrast |
| --- | --- | --- | --- | --- |
| Positive | `#5FD9AC` | 10.23 | `#0B6B4F` | 6.50 |
| Caution | `#FFB86B` | 10.50 | `#8A5200` | 6.39 |
| Critical | `#FF9A90` | 8.76 | `#9A1B1B` | 8.25 |

Contrast is measured against `#101820` (dark) and `#FFFFFF` (light). All six clear WCAG AA for normal
text; the lowest is 6.39.

Three of these are **not taken from the dynamic scheme**, and the source says why: "Material You can
turn `tertiary` into a pastel that reads as decoration, and a thermal alert that looks decorative is a
correctness bug in a performance tool."

### Surface

- **Panel / card**: charcoal with a vertical gradient (lighter at the top) and a 1dp hairline border at
  16% alpha. The gradient is the depth system; there is no shadow in the product surface.
- **Edge light**: a 1.4px inner highlight along a panel's leading edge at `MaxAlpha.edgeLight` (0.22f).
  Declared honestly: it adds no information, so it may never be the only thing distinguishing an
  element.
- **Halo**: an ambient glow behind an accented panel at `MaxAlpha.haloGlow` (0.07f).

### Text

Text colour is never specified as a literal in a component. It comes from the theme
(`onSurface`, `onSurfaceVariant`, `outline`) or from a tone accessor; `MaxAlpha.supportingText` (0.80f)
and `MaxAlpha.disabledContent` (0.38f) are the only opacity steps allowed on text.

### Data trust

The signature colour decision of the product, and the reason the palette has five more roles than a
normal app. Every reading carries how trustworthy it is:

| Trust | Tone | Shows the number? |
| --- | --- | --- |
| `Live` | Accent | yes |
| `Stale` | Caution | yes |
| `Snapshot` | Neutral | yes |
| `Unreadable` | Caution | **no** |
| `Unsupported` | Inactive | **no** |

Formatting a stale or missing value as if it were live is treated as a bug, not as a cosmetic issue.

## Typography

### Font Family

Three faces, each with one job:

1. **Space Grotesk** — display: page titles, headlines, section titles. Used with restraint and
   slightly tightened tracking so it reads as *engineered* rather than playful.
2. **Manrope** — body and labels. Chosen so long safety notes and descriptions never fight for
   attention.
3. **Monospace** — live values only: MHz, percentages, core counts, temperatures, with tabular
   figures so digits do not reflow horizontally as they change.

### Hierarchy

| Role | Size | Weight | Line height | Tracking | Use |
| --- | --- | --- | --- | --- | --- |
| `displayLarge` | 57sp | Bold | 64sp | -0.5sp | Onboarding / hero moments inside the app |
| `displaySmall` | 36sp | Bold | 44sp | 0 | Large numerals and first-run screens |
| `headlineSmall` | 24sp | SemiBold | 32sp | 0 | Page titles |
| `titleMedium` | 16sp | SemiBold | 24sp | 0.1sp | **Section titles** (the anchor rank) |
| `titleSmall` | 14sp | SemiBold | 20sp | 0.1sp | Card titles |
| `bodyLarge` | 16sp | Normal | 24sp | 0.3sp | Lead paragraphs |
| `bodyMedium` | 14sp | Normal | 20sp | 0.25sp | Descriptions, supporting copy |
| `bodySmall` | 12sp | Normal | 16sp | 0.2sp | Metadata, fine print |
| `labelLarge` | 14sp | SemiBold | 20sp | 0.4sp | Buttons and prominent chips |
| `labelMedium` | 12sp | SemiBold | 16sp | 0.5sp | Badges |
| `labelSmall` | 11sp | Bold | 16sp | 0.6sp | The "console eyebrow" — status labels |
| mono `live-value-large` | 34sp | SemiBold | 38sp | 0 | The headline reading on a metric card |
| mono `live-value-medium` | 16sp | SemiBold | 20sp | 0 | In-row readings |
| mono `live-value-small` | 12sp | Medium | 16sp | 0 | Dense tables |

Sizes and line heights follow the standard Material 3 scale — those numbers are already tuned for
Android reading distances. What this project changes is **family, weight and tracking**.

### Principles

- **Labels get more tracking than body text** (0.4–0.6sp against 0.2–0.3sp). It is the same
  "instrument panel" instinct that puts monospace on numbers, applied to text that annotates them.
- **Never mix monospace into labels or body copy.** A tool that sets everything in mono stops
  signalling which values are live.
- **Reserve two lines for a card title** (`MaxCardSpec.titleLines` = 2) so descriptions start at the
  same height across a row even when one title wraps and its neighbour does not.

### Note on font substitutes

Both faces are fetched through Google Fonts at runtime (`theme/Fonts.kt`). A build without network
falls back to the platform sans and mono; nothing in the layout depends on metrics that only those two
faces have, because every card reserves its lines and every metric uses tabular figures.

## Layout

### Spacing System

- **Base unit**: 4dp. Highest-contrast multiples only.

| Token | Value | Meaning |
| --- | --- | --- |
| `MaxSpace.hairline` | 2dp | The thinnest visible separation |
| `MaxSpace.xs` | 4dp | Inside a component |
| `MaxSpace.sm` | 8dp | Between siblings |
| `MaxSpace.md` | 12dp | Between groups of ideas |
| `MaxSpace.lg` | 16dp | Card interior |
| `MaxSpace.xl` | 20dp | Before a section title (see note) |
| `MaxSpace.xxl` | 28dp | A section's full separation |
| `MaxSpace.gutter` | 20dp | Horizontal page inset, every scrollable screen |
| `MaxSpace.section` | 28dp | Vertical gap between two sections |
| `MaxSpace.row` | 8dp | Gap between sibling rows |
| `MaxSpace.groupPadding` | 4dp | Inner padding of a grouped container |
| `MaxSpace.rowPaddingHorizontal` | 14dp | Inner padding of one row |
| `MaxSpace.rowPaddingVertical` | 12dp | Inner padding of one row |
| `MaxSpace.pageBottom` | 40dp | Clearance for the floating bottom bar |
| `MaxSpace.bottomBarReserve` | 112dp | Minimum footprint of that bar, so a long Arabic label cannot hide the last row |

**The one non-obvious value.** `MaxSpace.xl` (20dp) is what a section header adds *before itself*, and
it is smaller than `MaxSpace.section` (28dp) because the list that hosts it already inserts
`MaxSpace.row` (8dp) between children: 8 + 20 = 28. The named token for "the gap between two sections"
therefore describes what a reader actually sees, instead of double-counting.

### Grid & Container

- **Reading width**: `MaxSize.readingMaxWidth` (560dp) caps long explanatory copy on tablets and
  landscape.
- **Card grids**: columns are computed from available width against
  `MaxCardSpec.minColumnWidth` (148dp) — below that the grid drops a column rather than truncating a
  title. No call site may lower the floor to fit more cards in.
- **Grid gutters**: `MaxCardSpec.gridSpacing` (12dp), both axes.
- **Dialog lists**: `MaxSize.dialogListMax` (360dp) so a picker with a couple of hundred operation
  names cannot cover the screen it is asking about.

### Whitespace Philosophy

Space is the primary grouping device; borders are the second; colour is never the first. A group is
recognised by the air around it before anyone notices its container. This is why the card contract
carries both a padding (16dp) and a height floor (92dp): the floor exists so a one-word card does not
collapse next to a wordy neighbour and break the rhythm of a row.

## Elevation & Depth

| Level | Treatment | Use |
| --- | --- | --- |
| 0 — Flat | Panel colour, no border | Full-bleed bands |
| 1 — Hairline | 1dp border at `MaxAlpha.border` (0.16f) | Every card and grouped row |
| 2 — Gradient panel | Top-lit gradient + `MaxAlpha.edgeLight` (0.22f) | Sheets, the hero surfaces |
| 3 — Focus ring | 2dp ring (`MaxSize.activeRing`) | The one element that owns the next action |

**There are no drop shadows in the product surface.** Depth is a gradient plus a hairline. The 2dp
active ring is deliberately not colour-only: on a split screen the owning pane is also wider, because
"a colour alone is not an answer for anyone who cannot see it".

## Shapes

### Border Radius Scale

| Token | Value | Use |
| --- | --- | --- |
| `MaxRadius.chip` | 10dp | The smallest container: icon box, status chip, counter |
| `MaxRadius.control` | 12dp | Buttons and controls |
| `MaxRadius.row` | 14dp | A list row |
| `MaxRadius.inset` | 16dp | Inner container inside a card |
| `MaxRadius.tile` | 18dp | A tile smaller than a card |
| `MaxRadius.group` | 22dp | **The one card radius** (`MaxCardSpec.radius`) |
| `MaxRadius.sheet` | 28dp | Sheets and dialogs — the softest |
| `MaxRadius.pill` | 100dp | **Status only.** Never a primary action |

The tree previously carried 20 distinct literal corner radii and 14 padding values; the measured count
is now **5 distinct radii** across the whole UI layer, held by `tools/design_tokens.py`.

## Components

### Cards

`MaxCardSpec` is the single card contract, and it exists because the tree once held 38 separate
`*Card` composables plus a second metrics object that restated the same four numbers with different
values (cardRadius 28 against `MaxRadius.group` 22).

- Radius `MaxRadius.group` (22dp) · border `MaxSize.hairlineBorder` (1dp) · padding
  `MaxSpace.lg` (16dp)
- Icon container `MaxSize.iconContainer` (40dp), glyph `MaxSize.iconGlyph` (20dp)
- Gaps `MaxSpace.sm` (8dp) between icon, title and description; `MaxSpace.xs` (4dp) where it must be tighter
- Height floor `MaxCardSpec.minHeight` (92dp), title budget 2 lines, description budget 2 lines

### Section headers

One component defines what a section is; a second, competing shape is not allowed.

| | Value |
| --- | --- |
| Side accent bar | 4dp wide × 18dp tall, radius 2dp, gap `MaxSpace.md` (12dp) |
| Rule above a name (horizontal) | 28dp wide × 4dp tall, gap `MaxSpace.sm` (8dp) |
| Space before / after | 20dp / 12dp |
| Title → supporting copy | `MaxSectionSpec.titleGap` (4dp) |

The two bars are two tokens, not one value used twice: a bar *beside* a name reads as a vertical rule
that props the title, a bar *above* it reads as a horizontal rule that introduces it. The numbers
cannot serve both, so each direction keeps its own named contract.

### Rows and list items

Row padding `MaxSpace.rowPaddingHorizontal` (14dp) / `MaxSpace.rowPaddingVertical` (12dp), label
`labelLarge` or `titleSmall`, value in mono. The icon container inside a row is
`MaxSize.rowIconContainer` (34dp) — smaller than a card's, because a row is denser than a card.

### Status and data display

- A bar that shows a fraction (storage share, zone heat) is `MaxSize.barHeight` (8dp) tall — one token,
  because the storage screen and the thermal screen draw the same idea.
- A sparkline strip is `MaxSize.sparklineHeight` (28dp).
- Every tone-bearing component also renders an icon and a text label. Tone is never the only carrier of
  meaning, so state survives colour blindness, greyscale screenshots and high-contrast modes.

## Motion

| Token | Duration | Use |
| --- | --- | --- |
| `MaxDuration.instant` | 90ms | A state flip with no travel |
| `MaxDuration.quick` | 160ms | Small fades, chip and toggle states |
| `MaxDuration.standard` | 240ms | The default for anything that moves |
| `MaxDuration.deliberate` | 360ms | The ceiling |

**The rule, from the source:** motion exists to explain a transition or confirm a state change;
*anything longer than `deliberate` is decoration and is not allowed.* Two consequences:

1. Nothing in the app loops forever. A perpetual animation is a decoration by definition.
2. Motion is never the only signal that something changed — a state change is also a change in text,
   icon or tone.

## Responsive Behavior

### Breakpoints

| Name | Width | Key changes |
| --- | --- | --- |
| Phone | < 600dp | One column; card grid falls to 1-up below `MaxCardSpec.minColumnWidth` (148dp) |
| Large phone / foldable | 600–839dp | Two columns where the content is a grid |
| Tablet | ≥ 840dp | Reading copy capped at `MaxSize.readingMaxWidth` (560dp) |

### Touch targets

`MaxSize.minTouchTarget` (48dp) is an accessibility floor, not a preference. Anything clickable is at
least this large, including the scroll-to-top affordance that appears after eight rows in a long list.

### RTL

Right-to-left is not a mode: Arabic, Farsi, Hebrew and Urdu ship, and a gate (`tools/rtl_guard.py`)
enforces mirroring. Two layout facts fall out of it and are non-negotiable: the bottom bar reserves
`MaxSpace.bottomBarReserve` (112dp) because an Arabic label can wrap to two lines, and no label is
allowed to be sized on the assumption that it fits on one line in English.

### Image behavior

There is no photography and no illustration suite. Diagrams are vector and drawn from the product's own
words, and the app's screens are shipped as real captures rather than as mockups.

## The README surface

The public page is a **second register** of the same language, and is documented here so it stops being
an unwritten one.

- It reuses the product's own accent on dark (`#5FD9AC` — the app's Positive-on-dark tone) and the same
  4dp-derived rhythm, the same 22dp panel radius and the same 1dp hairline.
- It declares a **page palette** of its own for ink and secondary text, because those values come from
  the theme at runtime in the app and therefore have no fixed hex to import. The palette is listed in
  the README asset generator (private repository) and checked by the gate.
- **One deliberate exception to the motion rule lives here and only here.** The panels run slow ambient
  loops (2–11s), which the app's own ceiling forbids. They are allowed on the README because the page
  has to demonstrate over time what the product does — Atlas cycles, Max AI verifies, a write path is
  re-checked — and a still panel cannot. The exception is bounded by three rules: the static state is
  always complete and correct with the animations stripped, no loop carries information that is not
  also written in text, and each panel stays under 200KB.
- **Eight of the nine panels are dark-only**; only the hero banner ships a light variant. That is a
  known gap rather than a decision (see below).

## Do's and Don'ts

### Do

- Read the token, don't type the number. Every spacing, radius, size and opacity a component needs
  already has a name in `MaxTokens.kt`.
- Keep one card contract: `MaxCardSpec` radius, border, padding, icon container and title budget.
- Write a section title as `titleMedium` SemiBold, and put exactly one rank between it and a card title.
- Render an unknown value as `—` and a failed read as a failure with a rollback attempted.
- Reserve two title lines in a card so a row of cards aligns.
- Pair every tone with an icon and a word.
- Keep motion at or under `MaxDuration.deliberate` (360ms) and never loop it in the app.

### Don't

- Don't introduce a new corner radius, padding value or opacity literal for a single screen. That is
  precisely the drift this token layer exists to stop.
- Don't use a pill for a primary action. A pill means a status.
- Don't take Positive, Caution or Critical from the dynamic colour scheme — a decorative alert is a
  correctness bug here.
- Don't set labels or body copy in monospace.
- Don't lower `MaxCardSpec.minColumnWidth` to fit more cards in: truncating a title is worse than
  showing one column.
- Don't let colour be the only difference between two states.
- Don't add a drop shadow. Depth is a gradient plus a hairline.
- Don't animate anything forever in the app.

## Iteration Guide

The order that has produced every improvement in this layer so far:

1. **Measure first.** `python3 tools/design_tokens.py --assert` reports the literal radii, paddings,
   gaps and borders still in the tree, and `python3 tools/code_health.py --assert` reports the debt
   against a ceiling. A change that is argued rather than measured does not survive review here.
2. **Name before you change.** If a value appears more than a handful of times without a name, give it
   one at its current value first — zero visual change, and the next change becomes a one-line edit.
3. **Change the token, then regenerate.** Nothing downstream is edited by hand: the README panels come
   from `tools/gen_readme_assets.py`, and this document is checked against the token source.
4. **Verify against the gate you just changed.** `tools/design_doc.py --self-test` builds a tree with a
   known answer, because a gate that cannot fail proves nothing.
5. **Write down what cannot be measured.** Anything that needs hardware stays "not verified in this
   environment" — never "passes".

## Known Gaps

Measured, and stated rather than implied.

1. **`MaxMetricType` is dead.** `MaxMetricType` (`valueLarge` 34sp, `valueMedium` 22sp, `valueSmall`
   16sp) appears exactly once in the repository: its own definition. The scale actually in use is
   `MonoValueStyle*` (`theme/Type.kt` — 34sp / 16sp / 12sp), referenced from 18 files in 60 call sites.
   So the metric scale has two spellings, one of them unused, and `valueMedium` disagrees with its live
   counterpart (22sp against 16sp). Not removed here: deleting a token object is a code change that
   belongs in its own reviewed task, and the honest first step is to say so.
2. **`MaxTextRole` is a thin veneer.** `theme/MaxTypography.kt` defines four semantic roles
   (`description`, `metadata`, `status`, `liveValue`) but is referenced from 5 files with 8 call sites,
   while the Material 3 roles are called directly 149 (`bodySmall`), 74 (`bodyMedium`), 65
   (`titleMedium`), 65 (`labelSmall`) times. The semantic layer is an intention, not yet the contract.
3. **Nine screens still build their own `Scaffold`** (and nine files define their own `TopAppBar`), so
   page chrome is shared by convention rather than by construction. Migrating them is a task of its own;
   it is not attempted here because it would rewrite finished screens without a device to see them on.
4. **Only the hero banner has a light variant.** The other eight README panels are dark-only and will
   render dark panels on a light GitHub theme. The panels carry their own background and border so it
   reads as a deliberate plate, but a full light set does not exist.
5. **Hairline borders are below 3:1** (the 1dp edge measures 1.33:1 against the panel). That is
   deliberate and bounded: the border is never the only carrier of grouping — spacing and the gradient
   are the primary ones — so the low contrast does not hide an affordance.
6. **Colour contrast is measured for the design tokens, not for every rendered combination.** The six
   tone values are checked against both surfaces; arbitrary `alpha` compositions over gradients are not,
   and a new tone-derived surface should be measured before it ships.
