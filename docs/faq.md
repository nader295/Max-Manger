# FAQ

Short answers to the questions that come up most. Where an answer has a limit, the limit is in it.

---

### Does it need root?

Yes. MaxManager is a **systemless module** for Magisk or KernelSU: the app drives the kernel through a
root bridge behind a single arbiter, and the daemons run as system-side processes. The module is what
makes the control plane possible; the app alone is not the product.

### Will it work on my phone?

Probably — but **you do not have to guess**. MaxManager resolves capabilities per interface before
showing anything: a control your device does not expose never appears as a switch that does nothing.
Open it and read the map; that answer is about *your* phone, which is better than any list.

The seven capability states, and which one claims success, are in
[compatibility.md](compatibility.md#what-supported-means-here).

### Is Max AI on by default?

No. Nothing self-enables. Manual control is the default state, and Max AI, Max Atlas and the per-app
engines are things you switch on. When you do, the safety layer still has absolute priority.

### What does "Max AI" actually do — is it a chatbot?

No, and it is not a table of magic values either. It is a decision loop that acts on the controls Atlas
found on *your* device: choose an objective, pick the smallest sufficient change, check safety, execute
through the normal write path, then **measure what happened** before crediting anything. Read
[max-ai.md](max-ai.md).

### Why does an unknown value show as `status_unknown` instead of `0`?

Because `0` is a claim. This project forbids fabricated telemetry: when it does not know, it says so
rather than showing a plausible-looking zero. A blank-looking field is more honest than a wrong number.

### Why is there no benchmark table?

Because a delta measured on one device with one workload is not a claim about yours. Publishing one and
generalising it is the most common lie in this category of software, so what is measured is stated as
measured and everything else is left out. See [verification.md](verification.md).

### What happens if something goes wrong?

Three independent layers:

1. Values are **read back** after being written; a mismatch is surfaced and a rollback is attempted.
2. A drift guard re-checks later, because a setting can silently revert.
3. The installer **disables itself** if the module fails to reach a stable boot twice in a row — that is
   code in `post-fs-data.sh`, not a promise in a document.

### Will it break my phone / void my warranty?

The module is systemless: nothing in `/system` is modified permanently, and uninstalling removes the
overlay and the links. It also refuses to write the hardware's own protection — **thermal trip points
are on a never-touch list**, on every device, with no profile able to override them.

That said: rooting itself is your decision and your responsibility, and any tool that writes kernel
interfaces deserves care. Take a backup of your boot image before you flash anything, as with any root
module.

### Does it send my data anywhere?

No telemetry, no analytics, no silent upload. The diagnostic report is **built locally and minimized**,
and it leaves your device only if you hand the file over yourself. The screenshot folder in this
repository is public, which is why you are asked to check your own screenshots before sharing them.

### I flashed it and something looks wrong. What do I send?

The device, the ROM, the root manager, and what the app showed. If the app said `status_unknown`, say
that too — it is a fact about your device, not a mistake on your part. For ROM-side integration, the
single most useful attachment is `dmesg | grep -i avc` right after boot.

### Can I use it in my ROM?

Yes — there is an integration kit in the repository (`android/aosp/`) with the init service, the Soong
build, the SELinux policy and the privileged permission allowlist. **But MaxManager is proprietary
software**: integration is with the copyright holder's written permission, and
[LICENSE](../LICENSE) grants no right otherwise. Ask first — the contact is in
[Support](../README.md#support). The technical path is in [rom-integration.md](rom-integration.md),
including two mismatches we found in our own kit and did not paper over.

### Why is the licence proprietary if the repo is public?

A public repository is not the same thing as an open-source project. MaxManager is closed-source
software whose repository serves as its product page, its ROM-integration kit and its engineering
record. Third-party components keep **their own** licences and are listed individually in
[THIRD_PARTY_NOTICES.md](../THIRD_PARTY_NOTICES.md).

### Can I contribute code?

Not in this form — the repository is not a contribution surface. Bug reports, device compatibility
reports and integration findings are genuinely welcome and are the fastest way to make it work on more
hardware. See [Support](../README.md#support).

### Why are the engineering notes in Arabic?

Because that is the language the maintainer works in. `docs/ai/` is the project's own working record —
decisions, handoffs, the validation contract, the review protocol — kept public on purpose, including
the attempts that failed. It is not a user manual and it is not translated. The product documentation
you are reading is in English and Arabic.
