# Max AI — deciding what should change now

Max AI is the decision engine. It replaced three scattered components (a recommender, a predictor and a
learner) with one loop whose every step is either a real measurement or an explicit decision:

```
detect → decide → safety check → execute → measure the result → reward what actually happened
```

## The principles it is built on

These are not aspirations in a document; each one is visible in the code.

| Principle | What it means in practice |
| --- | --- |
| **Off by default, manual control** | Nothing self-enables. Turning it on is your action, and manual control is the default state. |
| **Only discovered knobs are vocabulary** | The engine's vocabulary is the hardware controls Atlas actually found — not a list of commands it hopes exist. |
| **One owner per knob** | A shared ownership ledger decides who holds a control (safety, per-app policy, manual, AI). There is no global mode and no queue of pending tweaks racing each other. |
| **Global performance profile stays manual** | The performance/balanced/eco profile is a manual baseline applied through the module service; it never becomes an instruction to the engine. |
| **Safety outranks everything, always** | The safety layer has absolute priority in the arbiter — including while the engine is off. |
| **No decision without execution, no reward without measurement** | Every decision goes through the single arbiter and its result is then measured. A predicted win that did not happen earns nothing. |

## Where each part lives

| Part | What it does |
| --- | --- |
| `Objective` | An objective is **weights, not a fixed profile** — performance, balanced and eco are three points in the same space, not three sets of constants |
| `MinimalPlanner` | The **smallest sufficient intervention** (a design decision, not an optimization): change one thing that is enough, instead of distributing a change across eight strings |
| `ControlRegistry` | The canonical vocabulary — the real knobs discovered on this device, keyed so that two layers can never invent two keys for one control |
| `ControlOutcomeModel` | The learning core, pure Kotlin over measured outcomes |
| `ResponseModel` | Predicts what a knob will do **before** trying it, so the engine does not have to learn everything by trial |
| `TrustModel` + `CredibilityStore` | The layer that says *"I know what I do not know"* — a source that has been wrong is not trusted equally |
| `DynamicIntentLearner` | Learns user patterns (for example: games between 3pm and 7pm) |
| `MaxAiCadence` | **When** to reconsider: the engine does not think on a fixed timer, it thinks when there is a reason to |
| `CoalescingCycleRunner` | Serializes evaluation and shares a generation: a burst of triggers produces one follow-up, not one replay per caller |
| `SafetyEngine` + `SafetyGovernor` + `PredictiveSafety` | The safety layer with absolute priority, including a predictor that fails safe |
| `MaxAiThermalCurve` | A ceiling that scales with how far over the line the device is — not two fixed thresholds |
| `MaxAiThermalBudget` | How long the device sustained full performance before it had to be dropped — a *capability* number, not another status readout |
| `MemoryStall` | Memory **stall** pressure, because a nearly-full-but-idle device and a stalling device need opposite answers |
| `MaxAiEpisode` · `MaxAiJournal` · `MaxAiJournalCodec` | The decision ledger: every cycle stored as a complete, measured episode, with a typed and versioned encoding |
| `MaxAiInsights` | What the engine actually learned, turned into verdicts that can be displayed — all pure functions over measured data |
| `CpuCeilingKnobs` | The per-policy CPU ceiling expressed as a real control through the same arbitration path, not a private write |

## What it will not do

- **It will not touch a never-touch interface.** Thermal trip points and their relatives are refused
  before planning, before routing and before any transaction is built — see
  [max-atlas.md](max-atlas.md).
- **It will not claim a win it did not measure.** Success requires a verified write; a command that was
  merely sent is not a result.
- **It will not invent telemetry.** Where a value is unknown the app says `status_unknown`; it never
  shows a plausible-looking zero.
- **It will not hide a failure.** Outcomes are recorded in their real states, including the rolled-back
  ones.

## Why the ledger matters

Most of what looks like "AI" in tuning apps is a table of rules and a promise. The interesting part
here is not the loop — it is the **record** of it: what the engine wanted, what it changed, what the
device did afterwards, whether the change held, and what it learned from the difference. That record is
what you can read in the app, and it is what makes the behaviour reviewable instead of mystical.
