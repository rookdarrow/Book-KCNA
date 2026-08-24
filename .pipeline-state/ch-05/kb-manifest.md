I have everything I need. Two things I verified that change what this stage can claim:

1. **`Book-KCNA/knowledge-base/` still does not exist.** Chapters 1, 3, and 4 all composed write blocks; none reached disk. Chapter 4's Stage 14 diagnosed why — `=== WRITE` appears exactly once in `certcomp`, in the prompt that asks for it. No parser consumes these blocks. That is still true.
2. **Chapter 5's research stage materialized zero snapshots.** `sources/` holds 115 files — the identical count Chapter 4 reported. All five snapshots the chapter needs are preserved in full inside `research-manifest.md` at lines 76, 210, 293, 361, 434. Both materializers are below.

---

# Knowledge-Base Manifest — KCNA Chapter 5

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 5 — The Smallest Vessel
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-24

**Inputs consulted:** the finalized chapter; `ch-05/integration.md` (Stage 13, 261 lines); `ch-05/outline.md` frontmatter (`kb_tags` — 71 concepts, 3 commands); `ch-05/research-manifest.md` (554 lines); `ch-05/diagnostics/{structural,fact-accuracy,curriculum-alignment,question-quality,theming-density}.md`; `ch-04/kb-manifest.md`, `ch-03/kb-manifest.md`, `ch-01/kb-manifest.md`; `Book-KCNA/sources/` (115 files, enumerated); the four published chapters.

## ⚑ Gate status — one closed, three carried, one new

**✅ Closed at Chapter 5: the fact-accuracy gate is real again.** Chapter 4 shipped with *no* audit (Stage 6 received `[file not available]` and inspected zero claims). Chapter 5's Stage 6 ran against `draft-v1.md` and inspected **148 claims — 81 tagged-and-verified, 17 untagged FAIL, 3 contradicted FAIL, 17 WARN.** More importantly, **all three contradicted claims were then actually remediated in the finalized chapter**, which I verified line by line:

| Finding | Stage 6 verdict | Finalized chapter |
|---|---|---|
| **C1** — worked overlay showing `phase: Running` + `Reason: ImagePullBackOff` | FAIL, "the one artifact that teaches the opposite of §5's centerpiece" | **Fixed** — neutral `<restart backoff>` placeholder |
| **C2** — "debugging init containers is a named skill in the exam curriculum" | FAIL — the curriculum names four domains and twelve competencies, nothing finer | **Fixed** — now "falls under **Troubleshooting**, one of the twelve named KCNA competencies" + source tag |
| **C3** — Bearings #2 A1, "doesn't contradict **any part** of that" | FAIL — true for post-creation waits, false for pre-creation | **Fixed** — stem names the reason; answer adds the discriminating half |
| **O1** — `grpc` success criterion "reports serving" | WARN, over-tagged | **Fixed** — softened to "the gRPC health check passes" |

This is the first chapter in the book where a blocking fact-accuracy finding was raised *and* discharged. It is worth saying so plainly.

Carried forward, unresolved:

- **Chapter 2 still never ran Stages 13–14.** Four chapters on, its terms have no glossary entries. Chapter 5 leans on Ch 2 for **four** retrieval items (Soundings Q8, Bearings #2 Q4, Practice Q20, Practice Q22) — more than any previous chapter — and `ImagePullBackOff`, first surfaced at ch2 §6, receives its actual definition here because Ch 2 has no ledger to hold it.
- **Chapter 4 still has no fact-accuracy audit.** Stage 6's Chapter 5 report says so explicitly and recommends a re-run. That outranks everything in Chapter 4's manifest.
- **Chapter 3's guardrail #8 remediation is open** (six unverifiable exam-frequency assertions). Relevant because Chapter 5 reintroduces the same construction — see the ethical-guardrail section, where I record a **divergence from Stage 13's read**.

New at Chapter 5:

- **⚑ The research stage wrote nothing to `sources/`.** 115 files before, 115 after. Five snapshots were fetched and their full bodies preserved in `research-manifest.md`, but none was written to disk. This is the direct cause of every untagged BLOCKING claim in the chapter, of the cut QoS material, and of the absent graceful-termination material. It is a *stage plumbing* failure, not a drafting choice, and the drafting stage handled it correctly by refusing to fabricate tags.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**57 terms contributed — 46 defined · 2 partial · 9 reserved · 5 status corrections to existing rows.**

Stage 13's coverage table counted **24** terms needing entries. My count is higher because I split the five Pod phases and three container states into their own rows rather than collapsing them. That is deliberate and Rule 5 requires it: **the quantifiers are the load-bearing part** — `Running` needs *all* containers created and *at least one* running; `Succeeded` and `Failed` both need *all* containers terminated. A single collapsed row would force a paraphrase, and the chapter's own Summary calls dropping an "all" the way readers get the phase wrong.

Appended as a Chapter 5 section rather than merged into the A–Z, following Chapter 4's precedent and for the same reason: this file is append-only under the current pipeline, and re-transcribing prior chapters' prose to preserve one alphabet is exactly the drift Rule 5 forbids.

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **Pod** ★ | "a Kubernetes object that represents a set of one or more running containers on your cluster" | Chapter 5 §1 — **closes the book's longest-standing gap** |
| **Pod IP** | "Each Pod gets its own unique cluster-wide IP address. A Pod has a private network namespace which is shared by all of the containers within it" | Chapter 5 §1 |
| **`localhost` communication** | "Processes running in different containers in the same Pod can communicate with each other over `localhost`" | Chapter 5 §1 |
| **PodSpec** | "the `spec` field of a Pod" — ⚑ authorial gloss, entailed but not verbatim in any snapshot | Chapter 5 §1 — **closes Chapter 3's reservation** |
| **init container** | "run before the app containers, in the order they are declared, and each must run to completion successfully before the next one starts" — ⚑ **UNSOURCED** | Chapter 5 §3 |
| **Pod phase** | one of `Pending`, `Running`, `Succeeded`, `Failed`, `Unknown`; Pod-scoped, in `status` | Chapter 5 §5 |
| **container state** | one of `Waiting`, `Running`, `Terminated`; per-container | Chapter 5 §5 |
| **`restartPolicy`** | "`Always` (the default), `OnFailure`, and `Never`… applies to all containers in the Pod" | Chapter 5 §5 |
| **ServiceAccount** | "a type of non-human account that, in Kubernetes, provides a distinct identity in a Kubernetes cluster" | Chapter 5 §6 — **closes Chapter 4's `Ch 5 (planted)` half** |
| **`livenessProbe`** | fails → "the kubelet kills the container," then restart policy applies | Chapter 5 §7 |
| **`readinessProbe`** | fails → "the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod" | Chapter 5 §7 |
| **`startupProbe`** | while configured and not yet succeeded, "all other probes are disabled" | Chapter 5 §7 |
| **resource request** | "the kube-scheduler uses this information to decide which node to place the Pod on" | Chapter 5 §8 |
| **resource limit** | "the kubelet enforces those limits so that the running container is not allowed to use more of that resource than the limit you set" | Chapter 5 §8 |
| *(32 further defined rows — full text in the append block)* | | |

### Rule 6 — canon conflicts, recorded not resolved

**No contradictions found.** I checked Chapter 5 against every shard it could plausibly collide with — `spec.md`, `status.md`, `control-loop.md`, `secret.md`, `namespace.md`, `label-selector.md`, `api-server-hub.md`, `node-components.md`. Chapter 5 is consistent with all of them. Three results worth recording, one of them a near-miss:

1. **✅ `status.md`'s Chapter 5 obligation is DISCHARGED.** The shard records Chapter 4's stated reuse plan — *"Chapter 5 reads it against a Pod's phase."* Chapter 5 §5 does exactly that, and Bearings #2 Q5 grades it (`status` carries `phase`; the system writes it; setting it yourself is a category error). **First of that shard's three downstream reuses to land.**
2. **✅ `secret.md` / `kubernetes.io/service-account-token` — consistent, no drift.** Chapter 4's glossary already recorded this type as *"a legacy long-lived"* form superseded by TokenRequest. Chapter 5 §6 repeats the same framing with the same source. Flagged as *checked and clean* because a legacy/current status is precisely where definitional drift shows up first.
3. **⚑ Near-miss worth an author note — the kubelet is `control-loop.md`'s *uncommon* shape, and Chapter 5 doesn't say so.** The shard's canonical Fixed Point reads: a controller *"usually acts by asking the API server to change something, **not by doing the thing itself**."* Chapter 5's Bearings #1 A5 calls the kubelet "Chapter 3's control-loop pattern operating at Pod scope" — correct, but the kubelet is Chapter 3's **direct control** case, the one Chapter 3 explicitly labelled *uncommon*. Not a contradiction; Chapter 3 documented both shapes. But a reader who meets the kubelet as the canonical example inherits a blurred model, and Chapter 13's whole method rests on it. **One clause fixes it.**

### ⚑ The escalation this stage exists to catch: `reconciliation` is now used in a graded answer key and has still never been defined

Chapter 3 made the reader a promise: *"when later chapters say **reconciliation**, this closing-the-gap work is exactly what the word names."* Both `control-loop.md` and `status.md` carry the gap as an open flag.

- **Chapter 4** was the first later chapter. It used the word family three times and never named the term.
- **Chapter 5** is the second. It uses the word family twice — and this time **both uses are inside the assessment surface**: Bearings #1 A5 (*"a description of a reconciliation loop with a PodSpec as its input"*) and Practice Q21's correct answer (*"The kubelet runs a reconciliation loop…"*).

The book is now grading readers on a word it promised to define and hasn't. That is a materially worse state than Chapter 4 left it in, and it will not self-correct — B3 runs the theme through Ch 6, 11, 15, and 17. **One appositive at Chapter 3's ★ Fixed Point closes it.** Rule 5 forbids my inventing the sentence here.

### ⚑ §N reservation collisions — Convention 5 broken a second time

Chapter 3's ledger proposed *"no `§N` in cross-bearings that point into undrafted chapters."* Chapter 4 broke it fifteen times; **Chapter 5 pins §-numbers into eleven undrafted chapters, seventeen times.** Never ratified, so this is a governance decision rather than a defect — but it is the direct cause of the collisions Stage 13 found, and the count is growing chapter over chapter. Recorded in the ledger:

| Reservation | Claimants | Status |
|---|---|---|
| **Ch 9 §1** | Ch 2 (*CNI and pod networking*) · **Ch 5** (*why a Service is necessary*) | ⚑ **HARD COLLISION.** Ch 2 has precedence and the arc outline's ordering supports it. Blocking before Ch 9 drafts. |
| **Ch 17 §2 / §3** | Ch 5 (autoscaling / mesh data plane) vs Ch 2's published `Ch 17 §4` | ⚑ Probable ordering conflict — outline puts both at §5+, and autoscaling *after* mesh |
| **Ch 6 §3** | Ch 1 · Ch 2 · Ch 4 — three topics | ⚑ Three-deep, carried from Chapter 4. **Ch 5 correctly avoided it** by pointing StatefulSet at no section at all |
| **Ch 12 §2** | Ch 2 (supply chain) · Ch 4 (access control) · **Ch 5** (SAs as RBAC subjects) | ⚑ Now three-deep |

---

## Concept shards added at `Book-KCNA/knowledge-base/concepts/{slug}.md`

**Twelve created.** Every slug is drawn from `outline.md`'s `kb_tags.concepts` so context-packer lookups round-trip, following Chapter 4's precedent.

- `concepts/pod.md` — **created** (§1, §9; the definition, the unit of scheduling, the seven-consequence synthesis) — **the book's most-deferred term, finally home**
- `concepts/pod-shared-context.md` — **created** (§1; one IP, `localhost`, shared volumes) — *Chapter 9's entire premise retrieves this*
- `concepts/multi-container-pod.md` — **created** (§2; the two-mechanism test, sidecar folded in)
- `concepts/init-container.md` — **created** (§3) — ⚑ **entirely unsourced; see the flag inside the shard**
- `concepts/pod-lifetime.md` — **created** (§4; scheduled once, replaced never, UID)
- `concepts/pod-phase.md` — **created** (§5; five values, verbatim, quantifiers intact)
- `concepts/container-state.md` — **created** (§5; three values + `Reason`)
- `concepts/restart-policy.md` — **created** (§5; scope, values, backoff schedule)
- `concepts/serviceaccount.md` — **created** (§6; identity only — Ch 12 owns authorization)
- `concepts/probe.md` — **created** (§7; all three types + four mechanisms in one shard)
- `concepts/resource-request.md` — **created** (§8)
- `concepts/resource-limit.md` — **created** (§8; carries the CPU-throttle / memory-OOM asymmetry)

**Deliberate structural choices, with reasons.** `probe.md` holds all three probe types rather than splitting into `liveness-probe.md` / `readiness-probe.md` / `startup-probe.md`, because the *discrimination between their failure behaviors* is the pedagogy — three separate shards would let the one fact that matters fall between them. Conversely `resource-request.md` and `resource-limit.md` **are** split, mirroring Chapter 4's `spec.md` / `status.md` precedent for a two-term contrast where each half has a distinct owning component.

**Not created, with reasons.** `smallest-deployable-unit` — a one-sentence thesis, folded into `pod.md` as its Zenith section rather than fragmented. `sidecar-container` — folded into `multi-container-pod.md`; its actual *mechanism* is unsourced, so a dedicated shard would be mostly a flag. `pod-ip`, `localhost-communication`, `pod-network-namespace`, `co-located-co-scheduled` — all four are one fact viewed from four sides, held together in `pod-shared-context.md`. `qos-class` and its three children — **cannot be created**; the material was cut for lack of a snapshot and writing a shard from memory is exactly what Open question #2 forbids. `pod-termination` — same, absent from the chapter. **No `commands/` shards**: the three `kubectl` verbs in `kb_tags` appear in the chapter only as deferrals to Chapters 13 and 16, which follows Chapter 4's precedent of leaving the command surface to Chapter 8.

---

## Voice-exemplar candidates nominated

**Not written to `voice-exemplars.md`** — Rule 1. Nominations only, for author ratification.

| Function | Excerpt | Recommendation |
|---|---|---|
| **why-wrong explanation** | *(Bearings #2 A4, distractor "State: `ImagePullBackOff`")* "If you wrote the right string in the wrong slot, you have the fact and not yet the taxonomy… It is also **the most self-concealing miss in the chapter, because the correct string appears in your answer and it *looks* right.**" | **Strongest in the chapter, and a genuinely new move for the series.** It diagnoses *why a reader won't catch their own error* rather than merely marking it wrong. Nominate as the canonical why-wrong exemplar. |
| **☀️ Zenith** | "A hull is not cargo. The vessel is the thing that gets a berth, an address, and a name on the manifest; the crates in the hold get none of those, and they go wherever the hull goes. That's it. That's the whole design." | **Strong.** Four sentences carrying a nine-section synthesis, and the metaphor is load-bearing rather than decorative — every noun maps (berth → node, address → Pod IP, manifest → API server). |
| **★ Fixed Point** | "**Phase is Pod-scoped; state is per-container.** And `Running` does not mean working — a crash-looping Pod reports the phase `Running`, because `Running` includes containers that are starting or restarting." | **Strong.** Rule first, consequence second, mechanism third. Structurally identical to Chapter 4's `spec`/`status` Fixed Point, which is now a series signature. |
| **⚓ Worth Securing** | "If two containers don't need `localhost` or a shared volume, they don't need to be one Pod. That's the whole test. Everything else — 'they belong to the same team,' 'they're part of the same product,' 'it's simpler to deploy' — is not a coupling requirement, it's a naming convention." | **Strong.** Models §18.14 scope discipline exactly, and the closing reframe does the work a paragraph of argument would. |
| **🔭 Closer Look** | "The **five-minute cap** is a floor on how bad things can get… The **ten-minute reset** is a forgiveness window… **Cap plus forgiveness.** Neither number is magic, but the *shape* — bounded penalty, earned amnesty — is a pattern you'll see again in distributed systems." | **Strong.** Converts two arbitrary constants into one transferable idea. Best available exemplar of the 🔭 register. |
| **Dead Reckoning** | "A Pod with three containers has one phase and three states. These are different fields with different vocabularies at different scopes. They are not interchangeable." | **Strong.** Facts-only register done correctly — the arithmetic sentence carries more than any restatement would, with zero framing. |
| **chapter-opening / curiosity gap** | "You already know this word. You've seen it since Chapter 2, where it arrived with an IOU attached… In the meantime, most readers form the obvious assumption. **Pod is Kubernetes' word for container.** It isn't, and the way it isn't matters more than a vocabulary quibble." | **Strong.** Names the reader's likely wrong model out loud, then spends the chapter dismantling it. Pairs with the Zenith as bookends. |
| **epistemic honesty / structural framing** | "A reader who leaves here able to recite five phase names but unable to say why the Pod has an IP and the container does not will re-learn this chapter four more times, each time under worse conditions. **That's not a threat; it's just how the book is built.**" | **Strong.** Disarms its own stakes claim in six words. This is the brand's confident-not-coercive line drawn precisely. |
| **closing epigraph (original)** | "A vessel that cannot be repaired at sea must be a vessel you are willing to lose. Build accordingly — and keep the plans." | **Strong.** Original Lodestar quote; earns its place because §4 already established replace-don't-repair as an engineering conviction, so the epigraph lands as summary rather than ornament. |
| **desirable difficulty** | *(Bearings #2 A3)* "If you got it, you're holding a level of detail most candidates skip. If you didn't, notice that you only needed two facts… **Both outcomes are fine here; the struggle is doing the encoding work.**" | **Moderate–strong.** Textbook Part 10B execution. Marked moderate only because the first clause carries a population claim (see below). |

**⚑ One repetition risk the author should rule on before Chapter 6.** Chapter 4's Stage 14 nominated a 🪝 Snag ending *"usually at two in the morning, while trying to make a stuck object look healthy."* Chapter 5 opens with *"a terminal at two in the morning with a pager still buzzing"* and §7 adds *"at three in the morning."* **Three small-hours beats across two consecutive chapters.** The register is right and skill v5.7 licenses it — but a signature repeated on schedule becomes a tic, and it is cheapest to diversify now, at chapter five of twenty, than at chapter twelve.

**Deliberately not nominated:** every line carrying an unsourced prevalence or exam-frequency claim — *"the easiest carry-over error to make," "Readers consistently assume," "the probe people most often reverse," "Practitioners find this genuinely surprising the first time," "the part most people don't know," "This is the part the exam cares about," "both of those breadths are tested," "That's what gets tested."* Chapter 3's guardrail #8 remediation is still open, and promoting this register would ratify it into brand canon before the author has ruled. Same reasoning Chapters 3 and 4 applied.

---

## Objective coverage log

Chapter 5 covers **D1.1 — Kubernetes Core Concepts** at **deep** depth. D1.1 remains **in progress**: B2 assigns it four consecutive chapters (3–6), and Chapter 5 delivers the workload layer.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.1 | Chapter 3 *(cluster layer)* | deep | 2026-08-24 |
| D1.1 | Chapter 4 *(object layer)* | deep | 2026-08-24 |
| **D1.1** | **Chapter 5** *(workload layer)* | **deep** | **2026-08-24** |

### ⚑ A book-level number nobody is tracking: the authored allocations are approaching the domain ceiling

Kubernetes Fundamentals is **44%** of the published exam. The four chapters that sit inside it have now claimed, each in a differently-worded metadata line:

| Chapter | Claimed allocation |
|---|---|
| Ch 2 — Containerization | ~9% |
| Ch 3 — Cluster architecture | ~6% |
| Ch 4 — Objects | ~6% |
| **Ch 5 — Pods** | **7%** |
| **Subtotal** | **28% of 44%** |

That leaves **16 percentage points for Chapter 6 alone** — which would make it, by the book's own accounting, larger than Chapters 3, 4, and 5 combined. Either the allocations need rebalancing or Chapter 6's is going to have to be authored to fit a residue rather than derived from its content. **This is cheapest to settle before Chapter 6 drafts**, and it is the concrete reason Stage 13's T4 (conform the metadata line to Chapter 2's disclosed form) is worth doing rather than deferring: four chapters now publish an authored number, only one of them discloses that it is authored.

### Chapter 5 — D1.1 coverage detail

| Sub-topic | Depth |
|---|---|
| Pod as the unit of scheduling; the definition itself | **deep — closes a four-chapter gap** |
| Shared network namespace, Pod IP, `localhost`, shared volumes | **deep — Chapter 9's premise originates here** |
| Multi-container Pods; the two-mechanism test; sidecar | moderate |
| Init containers: ordering, run-to-completion, failure | moderate — ⚑ **unsourced** |
| Pod lifetime; scheduled once; replaced with a new UID | deep — **discharges Chapter 4's forward commitment #3** |
| Pod phase (5 values) vs container state (3 values) | **deep — the chapter's centerpiece; Chapter 13's method depends on it** |
| `restartPolicy` scope, values, exponential backoff | deep |
| ServiceAccount as Pod identity; `default`; no permissions | moderate — **closes Chapter 4's `Ch 5 (planted)` half** |
| Probes: three types, four mechanisms, three failure behaviors | **deep — pays Chapter 3's "and healthy" debt** |
| Requests vs limits; CPU throttling vs reactive OOM kill; units | **deep — four later chapters retrieve it** |
| **QoS classes** (Guaranteed / Burstable / BestEffort) | ⚑ **ABSENT — outline-mandated, cut for lack of a snapshot** |
| **Graceful termination** (`terminationGracePeriodSeconds`, TERM→KILL) | ⚑ **ABSENT — `kb_tags` claims `pod-termination`** |
| `pod-template` | deferred to Ch 6 — correct; the tag is aspirational |
| `kubectl` command surface | deliberately deferred to Ch 13 / Ch 16 |

**Two outline-contract shortfalls, both traceable to the same plumbing failure.** QoS is named in the arc outline's *Covers*, its *Key concepts introduced*, and the `ch05-fig05` figure anchor — and the chapter assesses **zero** QoS items while shipping a figure with a deliberately empty strip. Graceful termination is claimed by `kb_tags`. Neither is a drafting defect: both snapshots were fetched and neither was written to `sources/`. Both close with a materialization and a short paragraph.

### ⚑ Ethical-guardrail status — Chapter 5, and a divergence from Stage 13

| Chapter | Guardrail #8 (frequency claims) | Note |
|---|---|---|
| Ch 1 | pass | |
| Ch 2 | pass | models the compliant phrasing |
| Ch 3 | **FAIL — open** | six unverifiable exam-frequency assertions |
| Ch 4 | BORDERLINE | five practitioner-prevalence superlatives |
| **Ch 5** | **BORDERLINE — four exam-frequency assertions + prevalence superlatives** | **see below** |

Stage 13 recorded guardrail #8 as **pass**, on the grounds that "the chapter makes no unhedged frequency claims" and that the subtitle's *"worth points"* is the only soft one, defended structurally in §9. The subtitle reading is right. The general claim is not — four unhedged assertions about **exam behavior** are present in the finalized text:

1. §3 — "**This is the part the exam cares about.**"
2. §5 — "Both of them are broader than their names suggest, and **both of those breadths are tested**."
3. §7 — "the definition matters less than the consequence of failure. **That's what gets tested.**"
4. Bearings #1 A1 — "**It will cost you points here** and it will make Chapter 9 incomprehensible."

These are mild, and the underlying judgments are very likely correct — but they are unsourced claims about what an exam does, which is Chapter 3's specific flagged failure mode, and Chapter 4 had avoided it cleanly. Recording the divergence rather than inheriting the "pass," because Chapter 3's remediation is still open and a second chapter drifting back into the construction is the signal the author needs. **Hedging all four costs about six words.** Author call; not marked failing.

Everything else on the Part 14 checklist passes and several items pass unusually well: no statistics of any kind appear in the chapter, every number is a sourced mechanism value, the two Dead Reckoning blocks and §7's explicit refusal to teach probe tuning handle the Order/Truth balance correctly, and the v5.7 subject-dignity guardrail is clean — every wry beat lands on the practitioner, none on anyone harmed by a failure.

---

## Retrieval-practice ledger

**8 tagged in-budget items · graded pool 38 (15 Bearings + 23 Practice) · rate = 21.1%.** B3's rung for Chapter 5 is **20%. Cleared.** Two further tagged items sit in Soundings, excluded from the budget by B3 but doing the spacing work anyway.

**Chapter 5 is the first chapter to draw from three predecessors.** Chapter 4 drew from two; Chapter 3 from one.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| `spec` / `status`; which reports what is true now | ch 4 §2 | **ch 5** — Soundings Q7 *(excluded from budget)* |
| `ImagePullBackOff`; reported as a container in **Waiting** | ch 2 §6 | **ch 5** — Soundings Q8 *(excluded from budget)* |
| the kubelet ensures PodSpec containers are running and healthy | ch 3 §3 | **ch 5** — Bearings #1 Q5 |
| `ImagePullBackOff` as a container-status `Reason` | ch 2 §6 | **ch 5** — Bearings #2 Q4 |
| which of `spec`/`status` carries `phase`; who writes it | ch 4 §2 | **ch 5** — Bearings #2 Q5 |
| labels as identifying attributes in `metadata`, selectable | ch 4 §5 | **ch 5** — Practice Q5 |
| `kubernetes.io/service-account-token` as legacy; TokenRequest since v1.22 | ch 4 §4 | **ch 5** — Practice Q13 |
| container immutability as a design principle | ch 2 §2 | **ch 5** — Practice Q20 |
| the control loop; kubelet as reconciliation | ch 3 §6 | **ch 5** — Practice Q21 |
| image-pull failure gating the init sequence | ch 2 §6 | **ch 5** — Practice Q22 |

**Quality notes, all favourable.** Practice Q22 is the strongest interleaving item the book has produced: it borrows Q9's *own* reasoning as its trap, so a reader who learned Q9 correctly is actively pulled toward the wrong answer, and the discriminator is one word (*created*). Practice Q13 is genuine retrieval rather than new material wearing a tag — Chapter 4 publishes the v1.22/TokenRequest fact itself. Bearings #1 Q5 is the chapter's cleanest seam: it takes Chapter 3's kubelet sentence, which contained two undefined nouns, and cashes both at once.

**⚑ One prescribed anchor only partially hit.** The outline names three retrieval anchors; two land exactly. The first — *"`imagePullPolicy` (Ch 2) as a cause of a container state"* — lands in its neighbourhood but **never names `imagePullPolicy`**, which is the field Ch 2 §6 spent its length on. Practice Q20's distractor D says "images are re-pulled on every restart," which is an `imagePullPolicy` fact in all but name. **Naming it there costs one word** and hits the anchor precisely.

### Cross-cutting themes — three land at Chapter 5, two for the first time

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **The control loop** (B3 headline) | Ch 3 §6 | Ch 4 · ✅ **Ch 5 — unplanned** | Ch 6, **Ch 11 (still unbeared)**, Ch 15, Ch 17 |
| **Namespaced vs cluster-scoped** | Ch 4 §3 | ✅ **Ch 5 §6 — FIRST retrieval, unplanned** | Ch 12 §3, Ch 10, Ch 11 |
| **Labels/selectors as the universal join** | Ch 4 §5 | ✅ **Ch 5 Practice Q5 — FIRST retrieval, unplanned** | Ch 6, Ch 7, Ch 9, Ch 10 |
| **The absent-component pattern** | Ch 3 §4, named | — *(still zero)* | Ch 10 ×2, Ch 13, Ch 17 |
| **"Kubernetes defines an interface, the ecosystem implements it"** | Ch 2 §4, named | ⚑ still zero named recurrences | Ch 9 (CNI), Ch 11 (CSI), Ch 17 §4 |

**All three of Chapter 5's theme retrievals were unplanned** — `control-loop.md`'s obligations table has no Chapter 5 row, and Chapter 4 beared the two new themes to Chapters 6, 7, 9, 10, and 12, not to 5. Chapter 5 picked them up anyway, at the natural moment, without being told to. That is the behaviour B3 was designed to produce, and it is the first evidence the theme architecture works without explicit bearings.

**⚑ Both new themes are still retrieved by paraphrase, not by name.** Chapter 5 §6 does the namespaced/cluster-scoped work in prose ("Chapter 4 taught you the namespaced-versus-cluster-scoped boundary; here it is doing work rather than being recited") without using either canonical retrieval string. Chapter 4's ledger fixed those strings precisely so five downstream chapters wouldn't each invent a paraphrase. **The decision deadline stands: a coined name must be chosen before Chapter 10 drafts.**

### Forward commitments — one discharged, one overdue, four new

| # | Commitment | Status |
|---|---|---|
| 1 | Ch 13 must carry a Ch 8 retrieval item (version skew) | **OPEN** — untouched at Ch 5 |
| 2 | Ch 11 must retrieve the control loop | ⚑ **OPEN, now three chapters overdue.** Chapter 5 bears to Ch 11 **twice** (§1 volume types; the proposed projected-volumes fix) and **neither carries the loop.** Ch 3, Ch 4, and Ch 5 have each passed it forward |
| 3 | Ch 5 must retrieve the UID rule | ✅ **DISCHARGED.** §4's ⚓ Worth Securing quotes Chapter 4's UID definition **verbatim with its source tag**, and Practice Q6's distractor D rebuttal turns it into a discriminator. Satisfies the wording exactly — retrieved, not re-derived. *Recorded precisely: it lands in prose and an untagged rebuttal, not as a `[retrieval: ch4]` graded item* |
| 4 | Ch 12 must **derive** the RBAC 2×2 from the namespaced boundary | **OPEN** |
| 5 | **Ch 9 must retrieve the Pod IP / shared namespace** | **NEW.** §1 tells the reader outright that "the entire argument for why Services must exist rests on the Pod having an IP that changes when the Pod is replaced." That is a published promise |
| 6 | **Ch 13's method must be "read the phase before you read the logs"** | **NEW.** Chapter 5 publishes that exact string **twice** as Chapter 13's method, and Chapter 4 published a third variant. Ch 13 must use the phrasing, not a paraphrase |
| 7 | **Ch 6 must open on "if Pods are designed to be replaced, who does the replacing?"** | **NEW.** Chapter 5's Voyage Ahead hands Chapter 6 its opening question and its thesis |
| 8 | **Ch 7, 13, 17, 18 must each retrieve requests/limits** | **NEW, and the largest single obligation in the book.** §8 tells the reader "four later chapters retrieve it by name" and names all four. Four separate chapters now owe a specific retrieval |

---

## Operator notes

1. **The write path is still broken, and this is the fourth manifest to say so.** Nothing in `certcomp` parses `=== WRITE` / `=== APPEND`. Chapter 4 supplied a materializer; it has not been run. An updated one covering ch-01 → ch-05 is below.
2. **Recovery order is load-bearing.** ch-01 → ch-03 → ch-04 → ch-05. Chapters 1 and 3 emit *full* `glossary.md`, `objective-coverage.md`, and `retrieval-log.md`; Chapters 4 and 5 emit *appends*. Running out of order silently discards the later chapters.
3. **⚑ Run the snapshot materializer first, before anything else.** Five snapshots sit fully preserved in `ch-05/research-manifest.md` and absent from `sources/`. They gate: five untagged claim clusters, the QoS section, the graceful-termination paragraph, a ★ Fixed Point, a 🪢 Mnemonic, four Bearings items, and three Practice questions — two of which (Q10 distractor C, Q17) have **correct answers resting on untagged claims**. This is the single highest-value action available and it costs one script run.
4. **Chapter 4 still has no fact-accuracy audit.** Chapter 5's Stage 6 says so and recommends the re-run. It also identifies the root cause for both chapters: Stage 6's declared input is `draft-v2.md`, which does not exist at that point in the graph. **Correct Stage 6's input resolution to `draft-v1.md`** and both chapters are fixed at the source.
5. **Chapter 2 has now been unaudited for four chapters** while four chapters retrieve from it. It is the oldest open item in the book.
6. **Append-only has a cost, stated plainly.** Five rows in earlier chapters' tables need *editing*, not appending — `Pod`, `PodSpec`, `ServiceAccount`, `TokenRequest API`, and `projected volume`. They are recorded in the append block under "Status changes to existing rows" for the reconcile pass.

### Materializer A — recover the five missing snapshots (run this first)

```python
# save as certcomp/tools/materialize_ch05_sources.py
import re, sys
from pathlib import Path
sys.stdout.reconfigure(encoding="utf-8")

BOOK = Path(r"C:\dev\lodestar\Book-KCNA")
MAN  = BOOK / ".pipeline-state" / "ch-05" / "research-manifest.md"

BLOCK = re.compile(
    r"<summary><code>[^<]*?sources/(?P<name>[^<]+?\.md)</code></summary>\s*"
    r"```markdown\r?\n(?P<body>.*?)^```",
    re.MULTILINE | re.DOTALL)

out = BOOK / "sources"
for m in BLOCK.finditer(MAN.read_text(encoding="utf-8")):
    tgt = out / m.group("name")
    if tgt.exists():
        print(f"SKIP (present): {tgt.name}"); continue
    tgt.write_text(m.group("body"), encoding="utf-8", newline="\n")
    print(f"WROTE {tgt.name}  ({len(m.group('body'))} bytes)")
# expected: k8s-docs-pods, -init-containers, -pod-qos, -sidecar-containers,
#           -pod-termination  (all -2026-08-24.md)
```

### Materializer B — replay the KB blocks (unchanged from Chapter 4, plus ch-05)

```python
# save as certcomp/tools/replay_kb_blocks.py
import re, sys
from pathlib import Path
sys.stdout.reconfigure(encoding="utf-8")

BOOK = Path(r"C:\dev\lodestar\Book-KCNA")
MANIFESTS = [BOOK / ".pipeline-state" / c / "kb-manifest.md"
             for c in ("ch-01", "ch-03", "ch-04", "ch-05")]   # order is load-bearing

WRITE  = re.compile(r"^=== WRITE (?P<p>.+?) ===\r?\n(?P<b>.*?)^=== END WRITE ===\r?$",
                    re.MULTILINE | re.DOTALL)
APPEND = re.compile(r"^=== APPEND (?P<p>.+?) ===\r?\n(?P<b>.*?)^=== END APPEND ===\r?$",
                    re.MULTILINE | re.DOTALL)

for man in MANIFESTS:
    if not man.exists():
        print(f"SKIP (absent): {man}"); continue
    text = man.read_text(encoding="utf-8")
    for rx, mode in ((WRITE, "w"), (APPEND, "a")):
        for m in rx.finditer(text):
            tgt = Path(m.group("p").strip().replace("/", "\\")).resolve()
            tgt.parent.mkdir(parents=True, exist_ok=True)
            body = m.group("b")
            if not body.endswith("\n"):
                body += "\n"
            with open(tgt, mode, encoding="utf-8", newline="\n") as fh:
                fh.write(body)
            print(f"{'WROTE ' if mode=='w' else 'APPEND'} {tgt.relative_to(BOOK)}")
```

---

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 5 additions — The Smallest Vessel (2026-08-24)

**Appended, not merged.** This file is append-only under the current pipeline. Book
assembly merges alphabets mechanically.

Terms contributed: **57** — 46 defined · 2 partial · 9 reserved · 5 status corrections.

## ⚑ Status changes to EXISTING rows above (apply at reconcile — cannot be done by append)

| Row | Current text | Correction | Evidence |
|---|---|---|---|
| Tier 3 · **Pod** | "⚑ **GAP** — used ~40× (Ch 3) / ~80× (Ch 4), never defined" | **CLOSED — defined at Ch 5 §1** | The shipped chapter. This was the book's longest-standing open term, carried across four chapters. |
| Tier 3 · **PodSpec** | reserved → Ch 5 (confirmed by outcome at Ch 4) | **CLOSED — defined at Ch 5 §1** ⚑ as an authorial gloss, not a sourced quotation. See Tier 2. | The shipped chapter |
| Tier 3 · **ServiceAccount** | "Ch 5 (planted) / Ch 12 (full)" | **Ch 5 half CLOSED — defined at Ch 5 §6** (identity). Ch 12 retains authorization/RBAC. | Ch 5 §6, four sourced facts |
| Tier 3 · **TokenRequest API** | reserved → Ch 12 | **SURFACED at Ch 5 §6** (one sentence, sourced). Full treatment still Ch 12. | Ch 5 §6 |
| Tier 3 · **`Lease`** | corrected to Ch 8 at Chapter 4 | **CONFIRMED.** Chapter 5 does not mention Lease, as expected under the Ch 8 assignment. | The shipped chapter |

---

## Tier 1 — Defined at Chapter 5 (prose inherited verbatim)

### B

**backoff reset (container restart)** — "Once a container has executed for **10 minutes
without any problems**, the kubelet resets the restart backoff timer for that container."
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §5)
> The chapter's gloss, worth keeping: the five-minute cap is "a floor on how bad things can
> get"; the ten-minute reset is "a forgiveness window." **Cap plus forgiveness.**

### C

**co-located and co-scheduled** — containers in a Pod are "co-located and co-scheduled to
run on the same node." [source: k8s-docs-containers-2026-08-23] (Ch 5 §1; phrase first
surfaced Ch 2, which has no glossary section)

**container state** — "Each container in a Pod is in one of three states": `Waiting`,
`Running`, `Terminated`. Per-container, not per-Pod.
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §5)
> ★ Fixed Point wording, recorded as the canonical retrieval string:
> **"Phase is Pod-scoped; state is per-container."**

**container state — `Waiting`** — "the container is still running the operations it
requires in order to complete start up: pulling the container image, applying Secret data.
A **`Reason`** field summarizes *why* it's waiting."
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §5)

**container state — `Running`** — "the container is executing without issues. A
`startedAt` timestamp is recorded." [source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §5)

**container state — `Terminated`** — "the container began execution and then either ran to
completion or failed. A reason, an exit code, and start and finish times are recorded."
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §5)

**CPU throttling** — "When a container approaches its cpu limit, the kernel will restrict
access to the CPU corresponding to the container's limit. Thus, a cpu limit is a **hard
limit the kernel enforces**." [source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)
> Observable consequence the chapter states: "Exceed your CPU limit and you get slow." The
> container keeps running; **neither the Pod phase nor the container state changes.**

**CPU unit / millicpu** — "1 CPU unit is equivalent to 1 physical CPU core, or 1 virtual
core," depending on whether the node is a physical host or a VM. Fractional requests are
allowed; `0.1` is equivalent to `100m`, "one hundred millicpu." CPU "is always specified as
an absolute amount, never as a relative amount" — `500m` is the same computing power on a
single-core or a 48-core machine. "Kubernetes doesn't allow CPU resources finer than `1m`."
[source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)

### E

**extended resources** — beyond `cpu`, `memory`, `ephemeral-storage` and
`hugepages-<size>`, clusters "can additionally provide **extended resources**, custom-named
resources typically exposed by device plugins."
[source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)
> Chapter scope note, inherited: "Know that they exist; you will not be asked to reason
> about them."

### I

**`ImagePullBackOff`** — a container-status **`Reason`**, not a state. "That status means a
container could not start because Kubernetes could not pull a container image, an invalid
image name or a private registry with no `imagePullSecret` being the usual causes. The
`BackOff` part indicates that Kubernetes will keep trying, with an increasing back-off
delay, **up to a compiled-in limit of 300 seconds (five minutes)**."
[source: k8s-docs-images-2026-08-23] (Ch 5 §5 — **first surfaced Ch 2 §6, which has no
glossary section because Chapter 2 never ran Stages 13–14**)
> ⚑ Two "five minutes" live fifteen lines apart in §5 and the chapter never distinguishes
> them: this **image-pull** 300 s cap, and the **container-restart** backoff cap. Different
> mechanisms, same number. Stage 13 recommends one clarifying clause.
> The canonical three-field reading: phase `Pending` · state `Waiting` · `Reason`
> `ImagePullBackOff`. **Only the third is actionable.**

**init container** — "Init containers run before the app containers, in the order they are
declared, and each must run to completion successfully before the next one starts. Only
when all of them have succeeded does the kubelet start the Pod's app containers."
⚑ **UNSOURCED — no snapshot on disk.** (Ch 5 §3)
> ⚑ **BLOCKING.** `k8s-docs-init-containers-2026-08-24.md` was fetched and never
> materialized; its full body is at `ch-05/research-manifest.md` line 210. Recoverable
> close to verbatim: *"Init containers always run to completion. Each init container must
> complete successfully before the next one starts."*
> ★ Fixed Point wording: **"In order, to completion, all of them, then the app."**

**init container — failure behavior** — "If an init container fails, the kubelet restarts
it, and the Pod's `restartPolicy` governs whether it gets retried at all." With the default
policy the Pod "never progresses to its app containers"; with `Never` the Pod "fails
outright." ⚑ **UNSOURCED — same gap.** (Ch 5 §3)
> ⚑ **CORRECTION REQUIRED ON MATERIALIZATION.** The retrieved text states that a Pod
> `restartPolicy` of `Always` causes init containers to use **`OnFailure`** — so this is
> *not* straight inheritance. The `Never` case as written is correct. Practice Q10's
> distractor-C rebuttal depends on this resolution.

**init container — probes excluded** — classic init containers do not carry `lifecycle`,
`livenessProbe`, `readinessProbe`, or `startupProbe` fields. ⚑ **UNSOURCED — same gap**, and
the retrieved text requires the qualifier **"Regular** init containers (in other words:
excluding sidecar containers)". (Ch 5 §3)

### L

**`livenessProbe`** — asks "is the container running?" If it fails, "**the kubelet kills the
container**, and the container is then subject to its restart policy."
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §7)

**`localhost` communication** — "Processes running in different containers in the same Pod
can communicate with each other over `localhost`."
[source: k8s-docs-network-model-2026-08-23] (Ch 5 §1)
> One of the **two** mechanisms that make containers in one Pod tightly coupled. The other
> is a shared volume. The chapter's test: "If two containers don't need `localhost` or a
> shared volume, they don't need to be one Pod."

### M

**memory units** — measured in bytes; expressible "as a plain integer or with quantity
suffixes, in either decimal form (`k`, `M`, `G`, and up) or the power-of-two equivalents
(`Ki`, `Mi`, `Gi`, and up)."
[source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)

**memory suffix `m` vs `M`** ⚠ — "**`M` means megabytes. `m` means millibytes.**… a request
of `400m` of memory is a request for **0.4 bytes**."
[source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)
> The chapter's framing, worth keeping: `m` is "perfectly correct — and extremely common —
> for CPU… The suffix isn't wrong; it's wrong *for memory*. Habit carries it across, and
> nothing in the manifest will stop you."

**multi-container Pod — the two-mechanism test** — containers belong in one Pod only if
they need (1) to reach each other over `localhost`, sharing the Pod's network namespace
[source: k8s-docs-network-model-2026-08-23], or (2) to read and write the same files,
sharing a volume [source: k8s-docs-volumes-2026-08-23]. (Ch 5 §2)
> ⚓ Worth Securing, verbatim: "Everything else — 'they belong to the same team,' 'they're
> part of the same product,' 'it's simpler to deploy' — is not a coupling requirement,
> it's a naming convention."

### O

**OOM kill (memory limit enforcement)** — "Memory limits are enforced by the kernel with out
of memory (OOM) kills. When a container uses more than its memory limit, the kernel may
terminate it. However, **terminations only happen when the kernel detects memory pressure.**
Thus, a container that over allocates memory may not be immediately killed; **memory limits
are enforced reactively**." [source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)
> The word to hold onto is *reactively* — "it's why memory problems in Kubernetes have a
> reputation for being hard to reproduce: the trigger for the kill isn't your container's
> behavior alone, it's the node's aggregate pressure."
> ⚑ The **status string** `OOMKilled` is **not** defined here and must not be. Chapter 13
> owns it; Chapter 5 bears forward correctly.

### P

**Pod** ★ — "A Pod is a Kubernetes object that represents a set of one or more running
containers on your cluster." [source: k8s-docs-workloads-2026-08-23] It is the unit
Kubernetes schedules: "the scheduler watches for newly created **Pods** with no assigned
node and finds a node for each one" [source: k8s-docs-kube-scheduler-2026-08-23]. Its
containers are "co-located and co-scheduled" on one node
[source: k8s-docs-containers-2026-08-23]. (Ch 5 §1)
> **CLOSES the book's longest-standing gap** — reserved at Ch 1 §1, promised at Ch 2 §1,
> used ~40× undefined in Ch 3 and ~80× in Ch 4.
> ★ Fixed Point: **"The Pod, not the container, is the unit of scheduling. A Pod gets one
> IP address, shared by every container inside it, and those containers reach each other
> over `localhost`."**
> ⚑ The phrase **"smallest deployable unit"** (§9 title, Summary row, Zenith anchor slug)
> is **not in any cached snapshot.** Recoverable verbatim from the pending
> `k8s-docs-pods-2026-08-24.md` (research-manifest line 76): *"Pods are the smallest
> deployable units of computing that you can create and manage in Kubernetes."*

**Pod — the design decision, in one line** — "The unit of scheduling wraps containers
instead of being one." (Ch 5 §9, authorial synthesis)
> Recorded as the canonical retrieval string for the chapter. Seven separate facts —
> Pod IP, `localhost`, `restartPolicy` scope, phase-vs-state scope, identity scope,
> scheduling scope, and what a Service selects — are consequences of it.

**Pod IP** — "Each Pod gets its own unique cluster-wide IP address. A Pod has a private
network namespace which is shared by all of the containers within it."
[source: k8s-docs-network-model-2026-08-23] (Ch 5 §1)
> 🪝 Snag, verbatim: "Each container in a Pod does **not** get its own IP address… This is
> the easiest carry-over error to make from single-container Docker experience."
> **Chapter 9's entire argument for why Services must exist rests on this.**

**Pod lifetime / ephemerality** — a Pod is created and assigned a UID; it is "**scheduled
once in its lifetime**" to a node, "where it remains until termination or deletion"; it is
"**never 'rescheduled' to a different node**"; if the node dies its Pods are "marked for
deletion after a timeout"; Pods "do not survive evictions due to lack of resources or node
maintenance." The documentation's summary: Pods are "relatively ephemeral (rather than
durable) entities." [source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §4)

**Pod replacement (and why "rescheduled" is wrong)** — a Pod is "replaced by a new,
near-identical Pod **with a different UID**."
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §4)
> **Discharges Chapter 4's forward commitment #3.** The chapter retrieves Chapter 4's UID
> definition verbatim — a UID is "intended to distinguish between historical occurrences of
> similar entities" [source: k8s-docs-names-and-uids-2026-08-24] — rather than re-deriving
> it. Same name, different UID, different object.
> 🪝 Snag: "Kubernetes does not move Pods. It replaces them."

**Pod phase** — a Pod-level field in `status` with five possible values.
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §5)
> A Pod with three containers has **one** phase and **three** states.

**Pod phase — `Pending`** — "the Pod has been accepted by the cluster, but one or more of
its containers has not been set up and made ready to run. This *includes* time spent
waiting to be scheduled **and** time spent downloading container images over the network."
[source: k8s-docs-pod-lifecycle-2026-08-23]

**Pod phase — `Running`** — "the Pod has been bound to a node, and **all** of the containers
have been created. **At least one** container is still running, **or is in the process of
starting or restarting**." [source: k8s-docs-pod-lifecycle-2026-08-23]
> ⚠ **The costliest misreading in the chapter: `Running` does not mean working. A
> crash-looping Pod reports the phase `Running`.** Chapter 13's diagnostic method depends
> on the reader not making this error.

**Pod phase — `Succeeded`** — "**all** containers in the Pod have terminated in success, and
will not be restarted." [source: k8s-docs-pod-lifecycle-2026-08-23]

**Pod phase — `Failed`** — "**all** containers have terminated, and at least one terminated
in failure: it either exited with non-zero status or was terminated by the system, and is
not set for automatic restarting." [source: k8s-docs-pod-lifecycle-2026-08-23]

**Pod phase — `Unknown`** — "for some reason the state of the Pod could not be obtained.
This typically occurs due to an error communicating with the node where the Pod should be
running." [source: k8s-docs-pod-lifecycle-2026-08-23]
> The chapter's discriminator, worth keeping: *"The cluster can't see it"* and *"the app
> can't stay up"* are different failures.

**Pod phase — the quantifiers** — `Running` needs **all** containers created and **at least
one** running; `Succeeded` and `Failed` both need **all** containers terminated. "Drop an
'all' and you get the phase wrong." (Ch 5 Chapter Summary)
> Recorded as its own row because Practice Q23 and Q22 both grade it and it is the single
> most compressible-and-therefore-most-lost part of §5.

**PodSpec** — "the `spec` field of a Pod." It is what you write; it lists the containers,
their images, and everything else in the chapter. ⚑ **Authorial gloss** — entailed by
[source: k8s-docs-cluster-architecture-2026-08-23] (which uses "PodSpecs" without defining
it) plus [source: k8s-docs-objects-2026-08-23] (which establishes `spec` generically), but
**not stated verbatim in any cached snapshot.** (Ch 5 §1)
> **CLOSES Chapter 3's reservation** — Ch 3 §3 used the noun undefined and beared it here.
> The pending `k8s-docs-pods-2026-08-24.md` carries `podspec` in its `concepts_covered`;
> tag after materialization, or keep as an explicit authorial gloss.

**probe** — "a diagnostic performed periodically by the kubelet on a container."
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §7)
> **Pays the second half of Chapter 3's debt** — the kubelet ensures containers are
> "running **and healthy**"; §1 handled *running*, §7 handles *healthy*.
> ⚑ A probe is **not** observability: "A probe answers a yes/no question for the kubelet's
> benefit and produces no history, no trend, and no measurement." Ch 18 owns that.

**probe mechanisms (the four)** — `exec` (success = exit status 0) · `httpGet` (success =
status code ≥ 200 and < 400) · `tcpSocket` (success = the port is open) · `grpc` (success =
the gRPC health check passes). [source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §7)
> ⚑ Two tagging notes. (a) The snapshot gives explicit criteria for the first three only;
> the `grpc` cell is authorial and was correctly softened from "reports serving" after
> Stage 6 flagged it as over-tagged. (b) **The orthogonality claim — "any probe type can use
> any mechanism" — is correct but nowhere asserted in the snapshot.** It is the entire
> answer to Practice Q17, whose three distractors all depend on it. Source it before a
> graded item rests on document layout.

**probe parameters (the five)** — `initialDelaySeconds`, `periodSeconds`, `timeoutSeconds`,
`successThreshold`, `failureThreshold`.
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §7)
> Deliberately shallow: "Choosing good values is a real engineering skill and it isn't what
> this exam is asking."

### R

**`readinessProbe`** — asks "is the container ready to respond to requests?" If it fails,
"**the endpoints controller removes the Pod's IP address from the endpoints of all Services
that match the Pod**." The container keeps running; nothing is killed or restarted.
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §7)
> ★ Fixed Point, the chapter's one-sentence discrimination: **"Liveness restarts, and does
> not remove from service. Readiness removes from service, and does not restart."**
> The chapter's framing: "Readiness stands a container down from the watch. Liveness
> relieves it of duty altogether."

**resource limit** — "When you specify a resource limit for a container, the kubelet
enforces those limits so that the running container is not allowed to use more of that
resource than the limit you set."
[source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)

**resource request** — "When you specify the resource request for containers in a Pod, the
**kube-scheduler** uses this information to decide which node to place the Pod on… The
kubelet also **reserves at least the request amount** of that system resource specifically
for that container to use." A request is a **floor**, not a ceiling: "if the node where a
Pod is running has enough of a resource available, it's possible — and allowed — for a
container to use more of that resource than its request specifies. However, a container is
not allowed to use more than its resource limit."
[source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)
> 🪢 Mnemonic: **"Requests are about placement. Limits are about containment. Scheduler
> places; kubelet contains."**

**resource types** — `cpu` (compute processing, base unit: cpu/core) and `memory` (RAM, base
unit: bytes) are the two specified constantly; `ephemeral-storage` and `hugepages-<size>`
(Linux only) exist and are specified the same way.
[source: k8s-docs-resource-management-2026-08-23] (Ch 5 §8)

**`restartPolicy`** — "The `spec` of a Pod has a `restartPolicy` field with possible values
**`Always` (the default)**, `OnFailure`, and `Never`. The `restartPolicy` applies to **all
containers in the Pod**." [source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §5)
> ⚠ It is **not** per-container. This is one of three traps sharing a single root cause:
> **reading a Pod-scoped signal as though it were container-scoped.**
> ⚑ The prior draft's absolute — "there is no way to configure one container to restart and
> another not to" — was **correctly dropped** rather than scoped, because sidecar containers
> are init containers carrying `restartPolicy: Always`. Do not restore it without the
> sidecar snapshot.

**restart backoff** — "After containers in a Pod exit, the kubelet restarts them with an
**exponential backoff delay — 10s, 20s, 40s, and so on — capped at five minutes.**"
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §5)

### S

**ServiceAccount** — "a type of non-human account that, in Kubernetes, provides a distinct
identity in a Kubernetes cluster." Application Pods use one to identify themselves to the
API server. [source: k8s-docs-service-accounts-2026-08-23] (Ch 5 §6)
> **CLOSES the `Ch 5 (planted)` half of Chapter 4's reservation.** Chapter 12 retains
> authorization, RBAC binding, token hardening, and the Pod-creation privilege-escalation
> path.

**ServiceAccount — namespaced, with a `default`** — "ServiceAccounts are namespaced, and
every namespace gets one named `default` upon creation."
[source: k8s-docs-service-accounts-2026-08-23] (Ch 5 §6)
> **First landed retrieval of Chapter 4's namespaced-vs-cluster-scoped theme.**

**ServiceAccount — automatic assignment** — "If you deploy a Pod in a namespace and don't
manually assign a ServiceAccount to it, Kubernetes assigns the `default` ServiceAccount for
that namespace to the Pod." [source: k8s-docs-service-accounts-2026-08-23] (Ch 5 §6)
> ⚓ Worth Securing, verbatim: **"Every Pod has an identity whether or not you gave it
> one."** There is no such thing as an anonymous Pod in a namespace.

**ServiceAccount — no permissions by default** — "The `default` service accounts get no
permissions by default" beyond "the default API discovery permissions Kubernetes grants to
all authenticated principals when RBAC is enabled."
[source: k8s-docs-service-accounts-2026-08-23] (Ch 5 §6)
> The two halves are independent: it **has** an identity (it can authenticate); it has
> almost no **authorization**.

**`spec.serviceAccountName`** — the field by which a ServiceAccount is assigned to a Pod.
[source: k8s-docs-service-accounts-2026-08-23] (Ch 5 §6)

**shared volume (Pod-scoped)** — containers in a Pod can share volumes; "all containers in a
Pod can read and write the same files in a shared `emptyDir` volume."
[source: k8s-docs-volumes-2026-08-23] (Ch 5 §1)
> Volume *types* and what makes a volume outlive the Pod are Chapter 11's.

**sidecar** — the helper container in a multi-container Pod, existing "to do something *for*
the main container" using one of the two coupling mechanisms. Documented instances: "a
sidecar container with a logging agent configured to pick up logs from an application
container" [source: k8s-docs-logging-architecture-2026-08-23]; a service mesh that "deploys
an Envoy proxy alongside each pod" [source: istio-service-mesh-2026-08-23]. (Ch 5 §2)
> ⚑ **The mechanism is absent.** Modern Kubernetes implements sidecars as **init containers
> with `restartPolicy: Always`**. The snapshot was fetched and never materialized
> (research-manifest line 361). Adopting it also scopes §5's `restartPolicy` claims
> correctly and licenses the word "regular" in §3's probes sentence.

**`startupProbe`** — asks "has the application within the container started?" While one "is
configured and has not yet succeeded, **all other probes are disabled**." If it fails, the
kubelet kills the container and applies the restart policy.
[source: k8s-docs-pod-lifecycle-2026-08-23] (Ch 5 §7)
> The suppression **is** the reason it exists: "Without it, a liveness probe would kill a
> slow-starting application before it ever finished starting, forever." The suppression
> lifts the moment it succeeds.

### W

**workload resource** — Kubernetes' built-in resources whose job is "to manage a set of Pods
on your behalf, making sure the right number of the right kind of Pod are running to match
the state you specified." "Higher-level controllers create the replacement Pods."
[source: k8s-docs-workloads-2026-08-23] [source: k8s-docs-pod-lifecycle-2026-08-23]
(Ch 5 §4)
> Named here only because Pod disposability **forces** it to exist: "The Pod cannot recreate
> itself; it's gone. Something outside it has to know that three replicas were wanted."
> Chapter 6 owns the treatment.

---

## Tier 2 — Partial at Chapter 5 (named, defining chapter elsewhere)

**TokenRequest API** — named in one sentence: "In Kubernetes v1.22 and later, Kubernetes
gets a **short-lived, automatically rotating token** using the TokenRequest API and mounts
it as a **projected volume**." [source: k8s-docs-service-accounts-2026-08-23] (Ch 5 §6)
→ **Full treatment: Ch 12.** Consistent with Chapter 4's glossary row; no drift.

**projected volume** — ⚑ **named, bolded, and never defined.** (Ch 5 §6)
→ **Ch 11.** This is the chapter's **only** deferred term without a cross-bearing — every
other one carries a pointer (`emptyDir` → Ch 11 §1, `kubectl logs -c` → Ch 13 §3, RBAC →
Ch 12 §2). An omission rather than a policy. **Fix: append
`*[cross-bearing: see Ch 11 §1 — projected volumes]*`.** Cheapest fix in the chapter.

---

## Tier 3 — Reserved by Chapter 5 (named, deferred, owner recorded)

| Term | Reserved to | Surfaced at | Bearing present? |
|---|---|---|---|
| `emptyDir` | Ch 11 §1 | Ch 5 §1 | ✅ |
| endpoints controller / Service endpoints | Ch 9 §4 | Ch 5 §7 | ✅ |
| `kubectl logs -c` (multi-container) | Ch 13 §3 | Ch 5 §2 | ✅ |
| `OOMKilled` / `Evicted` (status strings) | Ch 13 §4 | Ch 5 §8 | ✅ — mechanism taught here, string reserved there. Correct handling |
| RBAC / ServiceAccount authorization | Ch 12 §2 | Ch 5 §6 | ✅ — ⚑ but §2 is now three-deep claimed |
| service mesh data plane | Ch 17 | Ch 5 §2 | ⚑ §-number probably wrong; drop to chapter-level |
| **StatefulSet** | Ch 6 | Ch 5 §4 (🪝 Snag) | ⚑ **NO BEARING.** Correctly avoided pinning `Ch 6 §3`, which is triple-claimed — but add a chapter-level pointer or cut the clause |
| **QoS classes** (Guaranteed / Burstable / BestEffort) | ⚑ **NOWHERE — CUT** | — | ⚑ **Outline-mandated and absent.** See below |
| **graceful termination** | ⚑ **NOWHERE — ABSENT** | — | ⚑ `kb_tags` claims `pod-termination`. See below |
| **`CrashLoopBackOff`** | ⚑ **research gap** | — | ⚑ Appears in **no** cached snapshot. It is the natural label for §5's worked overlay and one sentence of prose; the neutral placeholder `<restart backoff>` stands in. Distinct from the five unmaterialized snapshots — this one was never fetched |

### ⚑ QoS classes — the outline contract Chapter 5 does not meet

`arc-outline.md` lists QoS under Chapter 5's *Covers*, its *Key concepts introduced*, and
the `ch05-fig05-requests-limits-qos-classes` anchor; `image-specs.md` marks that figure
**BLOCKED**; `kb_tags` carries four QoS slugs. The chapter assesses **zero** QoS items and
ships the figure with a deliberately empty strip.

**The drafting stage was right to cut rather than write from memory** — Open question #2
forbids it, and a grep of all 115 snapshots returns nothing for any of the three class
names. `k8s-docs-pod-qos-2026-08-24` is preserved at research-manifest line 293.

**Guard when writing, inherited from the draft's own note and independently confirmed:** that
page contains a loose generalization — *"Any Container exceeding a resource limit will be
killed and restarted by the kubelet"* — which **contradicts** the more specific, verified
CPU-throttles / memory-OOM-kills asymmetry in §8. **Do not let it overwrite Leg two.** The
same page also carries the Pod-level aggregation rule §9's sixth bullet needs (*"The resource
request of a Pod is equal to the sum of the resource requests of its component Containers"*),
which the init-containers snapshot complicates for Pods declaring init containers. **Check
both before writing the aggregate claim.**

### ⚑ Graceful termination — the second outline contract not met

`terminationGracePeriodSeconds`, SIGTERM-then-SIGKILL, and `preStop` hooks are absent.
Research reported the material "now fully sourced: default grace period 30 seconds, preStop
hook, TERM then KILL"; the snapshot sits at research-manifest line 434.

Open question #5 specifies the altitude precisely — **"termination is a request with a
deadline, not an instant event"** — one short paragraph with the 30-second default and
TERM-then-KILL. **Do not teach `preStop` syntax**; it exceeds associate tier and §4 is
deliberately a low-cost section. Closing this also strengthens Chapter 15's twelve-factor
disposability callback.

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod.md ===
# Concept: The Pod

**Home:** Chapter 5 §1, §9 · **Competency:** D1.1 · **Status:** canonical
**Closes:** the book's longest-standing reserved term — held open across Chapters 1–4.

## Definition (verbatim)

> A Pod is a Kubernetes object that represents **a set of one or more running containers on
> your cluster.** [source: k8s-docs-workloads-2026-08-23]

It is the unit Kubernetes schedules: "the scheduler watches for newly created **Pods** with
no assigned node and finds a node for each one" [source: k8s-docs-kube-scheduler-2026-08-23].
Its containers are "co-located and co-scheduled to run on the same node"
[source: k8s-docs-containers-2026-08-23].

## ★ Fixed Point (verbatim — do not reword)

> **The Pod, not the container, is the unit of scheduling. A Pod gets one IP address, shared
> by every container inside it, and those containers reach each other over `localhost`.**

## The one decision the whole chapter is a consequence of

> **The unit of scheduling wraps containers instead of being one.**

This is the chapter's Zenith and its most valuable single sentence. Seven separate facts are
consequences of it, not seven facts to memorize:

| Consequence | Section |
|---|---|
| The Pod has the IP, not the container | §1 |
| Containers reach each other on `localhost` | §1, §2 |
| `restartPolicy` is Pod-level and applies to every container | §5 |
| Phase is Pod-level; state is per-container | §5 |
| Identity (ServiceAccount) attaches to the Pod | §6 |
| Requests are declared per container, but the scheduler places the Pod | §8 |
| Services will select Pods, not containers | §1 → Ch 9 |

The chapter's own test of the model: if "Pod is Kubernetes' word for container" were true,
**every one of those seven would be wrong.**

## What it costs

Stated plainly in §1 and worth preserving: "Everything in a Pod lands on one machine, scales
as one thing, and dies as one thing." The interesting question is therefore not *what* a Pod
is but *why the wrapper exists at all* — which `pod-shared-context.md` answers.

## The misconception this shard exists to kill

**"Pod is Kubernetes' word for container."** Chapter 2 planted the deferral; four chapters of
undefined use let the assumption harden. It is wrong about IP addresses, about what a Service
selects, about what `restartPolicy` applies to, about what a phase describes, and about what
gets replaced when something fails.

## ⚑ Source gap

The phrase **"smallest deployable unit"** — §9's title, a Chapter Summary row, and the Zenith
anchor slug — appears in **no cached snapshot.** It is recoverable verbatim from
`k8s-docs-pods-2026-08-24.md` (research-manifest line 76): *"Pods are the smallest deployable
units of computing that you can create and manage in Kubernetes."* Until materialized, §1's
prose deliberately claims only what kube-scheduler and workloads support.

The same snapshot carries the **"two main ways Pods are used"** framing that §2 relies on, and
a caution §2 should probably absorb: *"Grouping multiple co-located and co-managed containers
in a single Pod is a relatively advanced use case."*

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 6** | Answer "if Pods are designed to be replaced, who does the replacing?" — Chapter 5's Voyage Ahead hands this over as Chapter 6's opening question. Also: the reader has been told the Pod is "something you will almost never create directly" |
| **Ch 9** | **Retrieve the Pod IP.** §1 tells the reader the entire argument for Services rests on it |
| **Ch 13** | The diagnostic method, published here twice as *"read the phase before you read the logs"* |

## Related

[[pod-shared-context]] · [[pod-phase]] · [[pod-lifetime]] · [[multi-container-pod]] ·
[[kubernetes-object]] · [[spec]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-shared-context.md ===
# Concept: The Pod's shared context — one IP, one namespace, shared volumes

**Home:** Chapter 5 §1 · **Competency:** D1.1 · **Status:** canonical
**Depth here:** the load-bearing fact of Chapter 5, and the premise of Chapter 9.

## Definition (verbatim)

> **Each Pod gets its own unique cluster-wide IP address. A Pod has a private network
> namespace which is shared by all of the containers within it. Processes running in
> different containers in the same Pod can communicate with each other over `localhost`.**
> [source: k8s-docs-network-model-2026-08-23]

## Why this forces the Pod to exist — read it as an argument, not a feature list

Chapter 5's derivation, preserved because it is the reason the Pod is not arbitrary:

1. Suppose you want two containers to behave the way two processes on one host behave —
   reachable instantly, no service discovery, no network hop, neither needing the other's
   address.
2. There is **exactly one** way to give them that: put them in the same network namespace.
3. A network namespace cannot be handed out per-container-but-shared while still calling the
   container an independent schedulable thing.
4. Therefore the moment two containers share a network namespace they must be placed
   together, started together, and torn down together. **They have become one unit.**

> **The Pod is the shared context, and the containers live inside it.** Not a container with
> extra fields.

## The second half: storage

Containers in a Pod can share volumes — "all containers in a Pod can read and write the same
files in a shared `emptyDir` volume" [source: k8s-docs-volumes-2026-08-23]. Named here and
left; volume *types* and lifetimes are Chapter 11's.

## The two coupling mechanisms — the whole test

There are exactly two, and together they are the decision rule for multi-container Pods:

1. **`localhost`** — shared network namespace [source: k8s-docs-network-model-2026-08-23]
2. **A shared volume** — the same files [source: k8s-docs-volumes-2026-08-23]

See `multi-container-pod.md`.

## Figure

`ch05-fig01-pod-shared-network-namespace` — the IP is drawn **bound to the Pod boundary, not
to either container.** The chapter states outright that "that placement is the pedagogy, not
decoration." Any redraw must preserve it.

## 🪝 The misconception (verbatim)

> Each container in a Pod does **not** get its own IP address. The Pod gets one; all its
> containers share it. This is the easiest carry-over error to make from single-container
> Docker experience, where "one container, one IP" was a safe assumption.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 9** | **The premise.** The argument for why Services must exist rests on the Pod having an IP *that changes when the Pod is replaced.* ⚑ Chapter 5 pins this at `Ch 9 §1`, which **collides** with Chapter 2's published `Ch 9 §1 — CNI and pod networking`. Ch 2 has precedence |
| **Ch 7** | `httpGet` probes target *the Pod's* IP — the fact resurfaces where readers don't expect it |

## Related

[[pod]] · [[multi-container-pod]] · [[probe]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/multi-container-pod.md ===
# Concept: Multi-container Pods and the sidecar

**Home:** Chapter 5 §2 · **Competency:** D1.1 · **Status:** canonical *(mechanism incomplete)*

## The default

Overwhelmingly the most common shape is **one container per Pod** — the Pod as a thin wrapper
around a single container. That is the default to reach for.

⚑ The "two main ways Pods are used" framing is **not in the cached source set.** Recoverable
close to verbatim from `k8s-docs-pods-2026-08-24.md` (research-manifest line 76): *"Pods in a
Kubernetes cluster are used in two main ways… The 'one-container-per-Pod' model is the most
common Kubernetes use case."* That snapshot also carries a caution this section should absorb:
*"Grouping multiple co-located and co-managed containers in a single Pod is a relatively
advanced use case."*

## The decision rule — the whole test

Two containers belong in one Pod **only** if they need one of exactly two mechanisms:

1. **They reach each other over `localhost`** [source: k8s-docs-network-model-2026-08-23]
2. **They read and write the same files** [source: k8s-docs-volumes-2026-08-23]

> ⚓ **Worth Securing (verbatim):** If two containers don't need `localhost` or a shared
> volume, they don't need to be one Pod. That's the whole test. Everything else — "they belong
> to the same team," "they're part of the same product," "it's simpler to deploy" — is not a
> coupling requirement, it's a naming convention.

## The sidecar

The helper container that exists to do something *for* the main container, using one of those
two mechanisms. Documented instances:

- **Log shipping** — "a sidecar container with a logging agent configured to pick up logs from
  an application container" [source: k8s-docs-logging-architecture-2026-08-23]
- **Proxying** — a service mesh "deploys an Envoy proxy alongside each pod"
  [source: istio-service-mesh-2026-08-23]
- **Credential refresh** — a helper rewriting a token file the app reads

## ⚑ The mechanism is missing

Modern Kubernetes implements sidecar containers as **init containers with
`restartPolicy: Always`.** The research stage retrieved
`k8s-docs-sidecar-containers-2026-08-24.md` and reported the mechanism "established plainly";
the snapshot was never materialized (research-manifest line 361).

**Adopting it does three things at once:** names the mechanism here in one clause; licenses
the word "regular" in §3's probes-exclusion sentence; and correctly scopes §5's
`restartPolicy` claims. The curriculum audit recommends **ADOPT**.

## 🪝 The misconception (verbatim)

> A Pod is not a small virtual machine. The instinct to put a web server, a database, and a
> cache into one Pod because "they're one application" is exactly what §1's co-scheduling
> guarantee makes *possible* — and exactly what makes it a mistake. Everything in a Pod scales
> together, fails together, and is replaced together… **Three components with three different
> scaling profiles want three Pods.**

## Not the Docker-era doctrine

§2 explicitly declines to endorse "one process per Pod." Multi-container Pods are a supported,
useful pattern. The test isn't *how many* processes; it's whether `localhost` or a shared
volume is genuinely **needed**.

## Practical consequence banked for Chapter 13

Once a Pod holds more than one container, several commands stop being unambiguous:
`kubectl logs <pod>` prints *a container's* logs, and a multi-container Pod requires
`-c <container>` [source: k8s-docs-logging-architecture-2026-08-23]. Ch 13 owns the method.

## Related

[[pod-shared-context]] · [[init-container]] · [[restart-policy]] · [[pod]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/init-container.md ===
# Concept: Init containers

**Home:** Chapter 5 §3 · **Competency:** D1.1 · **Status:** ⚑ **UNSOURCED — BLOCKING**

## ⚑ Read this first

**Every semantic claim in this shard is untagged.** No primary source in the cached set covers
init containers. `kubernetes.io/docs/concepts/workloads/pods/init-containers/` **was** fetched
by the research stage; its snapshot `k8s-docs-init-containers-2026-08-24.md` was never
materialized into `sources/` because that stage had no filesystem write access. **Its full
text is preserved at `ch-05/research-manifest.md` line 210.**

Stage 6 rated this BLOCKING (findings U1, U2, U3). What is currently untagged in the shipped
chapter: the ordering rule, run-to-completion, the failure behavior, the probes exclusion, the
★ Fixed Point, the 🪢 Mnemonic, Bearings #1 items 3 and 4, and **Practice questions 4, 10,
and 22.**

## The contract (as the chapter states it — untagged)

> Init containers run before the app containers, **in the order they are declared**, and each
> must **run to completion successfully** before the next one starts. Only when **all** of them
> have succeeded does the kubelet start the Pod's app containers.

**Recoverable close to verbatim:** *"Init containers always run to completion. Each init
container must complete successfully before the next one starts."* And for the app containers:
*"Once preconditions are met, all of the app containers in a Pod can start in parallel."*

## The contrast that carries the section

- **Init containers: sequential.** One at a time, each waiting on the previous successful exit.
- **App containers: parallel.** All start together once the init sequence completes.

## ⚑ TWO CORRECTIONS required on materialization

1. **The restart behavior is NOT straight inheritance.** The retrieved text states: *"if the
   Pod restartPolicy is set to Always, the init containers use restartPolicy OnFailure."* The
   chapter currently implies plain inheritance. The `Never` case as written **is** correct.
   **Practice Q10's distractor-C rebuttal depends on this** — as written it rejects C on the
   grounds of the *total* exemption C claims, which stays true either way, but the underlying
   claim must not assert identical treatment.
2. **The probes sentence needs the word "regular."** *"Regular init containers (in other words:
   excluding sidecar containers) do not support the lifecycle, livenessProbe, readinessProbe,
   or startupProbe fields."*

## The one axis that generates everything else

> **Init containers are expected to exit; app containers are expected to keep running.**

That single difference explains the sequencing (a thing that exits can be waited on), the
success criterion (exit status 0), and the probe exclusion (probes answer questions about a
long-running process).

## ★ Fixed Point / 🪢 Mnemonic (both currently untagged)

> **In order, to completion, all of them, then the app.**

## Figure

`ch05-fig03-init-containers-sequence` — two tracks, success and failure. The failure track's
teaching point is that app containers are **NEVER STARTED**, not partially started.

## Cross-section dependency, stated openly

§3 leans on `restartPolicy`, which §5 defines. The chapter names the dependency rather than
pretending the sections are independent. Preserve that.

## Related

[[restart-policy]] · [[pod-phase]] · [[multi-container-pod]] · [[pod]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-lifetime.md ===
# Concept: Pod lifetime — scheduled once, replaced never

**Home:** Chapter 5 §4 · **Competency:** D1.1 · **Status:** canonical
**Discharges:** Chapter 4's forward commitment #3 (Ch 5 must retrieve the UID rule).

## The lifetime, in order (all verbatim)

- A Pod is **created** and assigned a unique **UID**.
- It is **scheduled once in its lifetime** to a specific node, "where it remains until
  termination or deletion."
- It is **never "rescheduled" to a different node.** Instead it is "replaced by a new,
  near-identical Pod **with a different UID**."
- If the node dies, its Pods are "marked for deletion after a timeout."
- Pods "do not survive evictions due to lack of resources or node maintenance."

[source: k8s-docs-pod-lifecycle-2026-08-23]

The documentation's own summary: Pods are **"relatively ephemeral (rather than durable)
entities."**

## 🪝 The misconception (verbatim)

> A Pod on a failed node is **not rescheduled onto a healthy node.** It is deleted, and
> something creates a new one. The word "rescheduled" implies the same object moving, which
> will lead you to the wrong answer on questions about UIDs, about identity, and about why
> StatefulSets are different. **Kubernetes does not move Pods. It replaces them.**

## The Chapter 4 retrieval — done correctly

§4 quotes Chapter 4's UID definition **verbatim with its source tag** rather than re-deriving
it: a UID is "intended to distinguish between historical occurrences of similar entities"
[source: k8s-docs-names-and-uids-2026-08-24]. Same name, different UID, different object.

**This discharges Chapter 4's forward commitment #3.** Recorded precisely: it lands in prose
and in Practice Q6's distractor-D rebuttal, not as a `[retrieval: ch4]`-tagged graded item.
The commitment's wording — "retrieve `metadata.uid` explicitly rather than re-deriving it" —
is fully satisfied.

## Why this forces a workload resource to exist

The reason this short section exists at all. If the thing that runs your application is
designed to be **replaced rather than repaired**, something else must hold the intent that
survives the replacement. The Pod cannot recreate itself; it's gone. Workload resources
"manage a set of Pods on your behalf, making sure the right number of the right kind of Pod
are running to match the state you specified" [source: k8s-docs-workloads-2026-08-23], and
"higher-level controllers create the replacement Pods"
[source: k8s-docs-pod-lifecycle-2026-08-23]. **That is Chapter 6's premise.**

## The same conviction, one level up

Chapter 2 taught that containers are immutable — you don't change a running container, you
build a new image and recreate it [source: k8s-docs-containers-2026-08-23]. A Pod is that
instinct at the next layer. **Replace, don't repair: at the image layer and at the Pod layer
both.** The chapter is explicit that noticing it is the *same* conviction expressed twice is
worth more than memorizing either instance. Practice Q20 grades exactly this.

## ⚑ Missing: graceful termination

`terminationGracePeriodSeconds`, SIGTERM-then-SIGKILL, and `preStop` are absent, though
`kb_tags` claims `pod-termination`. Snapshot retrieved, never materialized
(research-manifest line 434). Open question #5 specifies the altitude: **"termination is a
request with a deadline, not an instant event"** — one short paragraph, the 30-second default,
TERM then KILL. **Do not teach `preStop` syntax.** Closing this strengthens Chapter 15's
twelve-factor disposability callback.

## Related

[[pod]] · [[pod-phase]] · [[restart-policy]] · [[kubernetes-object]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-phase.md ===
# Concept: Pod phase

**Home:** Chapter 5 §5 · **Competency:** D1.1 · **Status:** canonical
**Depth here:** the chapter's centerpiece and the foundation of Chapter 13's method.
**Discharges:** `status.md`'s recorded plan — "Chapter 5 reads it against a Pod's phase."

## Definition

A Pod-level field in `status` with **five** possible values
[source: k8s-docs-pod-lifecycle-2026-08-23]:

| Phase | Verbatim |
|---|---|
| **`Pending`** | "the Pod has been accepted by the cluster, but one or more of its containers has not been set up and made ready to run." Includes time waiting to be scheduled **and** time downloading images over the network |
| **`Running`** | "the Pod has been bound to a node, and **all** of the containers have been created. **At least one** container is still running, **or is in the process of starting or restarting**" |
| **`Succeeded`** | "**all** containers in the Pod have terminated in success, and will not be restarted" |
| **`Failed`** | "**all** containers have terminated, and at least one terminated in failure… and is not set for automatic restarting" |
| **`Unknown`** | "the state of the Pod could not be obtained. This typically occurs due to an error communicating with the node" |

## ★ Fixed Point (verbatim — do not reword)

> **Phase is Pod-scoped; state is per-container.** And `Running` does not mean working — a
> crash-looping Pod reports the phase `Running`, because `Running` includes containers that
> are starting or restarting.

## The quantifiers are the fact

Recorded separately because they are what readers compress away, and both Practice Q22 and
Q23 grade them:

- `Running` → **all** created, **at least one** running/starting/restarting
- `Succeeded` and `Failed` → **all** terminated

**"Drop an 'all' and you get the phase wrong."**

## ⚠ The three traps, and their single root cause

All three are **reading a Pod-scoped signal as though it were container-scoped.** Fix the
cause and all three close:

1. **Phase is not state.** "The Pod is Waiting" is not a sentence Kubernetes can produce;
   "the container is Pending" is equally impossible.
2. **`Running` does not mean working.** The costliest misreading in the chapter.
3. **`restartPolicy` is not per-container.**

## The discriminator worth more than any single answer

Same state name, different reason, **different phase**:

| Scenario | Container state | Phase |
|---|---|---|
| Container created, crashed, serving backoff | `Waiting` | **`Running`** |
| Container blocked on an image pull (never created) | `Waiting` | **`Pending`** |

`Running` requires that **all** containers have been created. A container that cannot pull its
image has not been created. This is why the §5 figure's worked overlay uses a *post-creation*
waiting reason.

## ⚑ Figure correction already applied — do not regress it

`ch05-fig02-pod-phases-and-container-states`'s worked overlay originally showed
`phase: Running` against `Reason: ImagePullBackOff`, which contradicts the cached definition
of `Running` and the chapter's own table. Stage 6 rated it a FAIL and "the one artifact in the
chapter that teaches the opposite of §5's centerpiece." **It has been fixed** to a neutral
`<restart backoff>` placeholder. The natural label is `CrashLoopBackOff`, which appears in **no
cached snapshot** — a research gap distinct from the five unmaterialized files. Replace the
placeholder only once a source for container status reasons is fetched.

Note also: container states are drawn **inside** the Pod in that figure because that is the
actual relationship. "If you find yourself picturing them side by side… the figure has failed
and so has the model."

## The boundary this section holds

§5 owns the **vocabulary**; Chapter 13 owns the **method**. No `kubectl describe` walkthrough,
no event stream. The reason the boundary is worth holding is stated in the chapter: Chapter
13's method is *"read the phase before you read the logs,"* and that instruction is worthless
to a reader who doesn't already own the vocabulary.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 13** | The entire diagnostic method. **Must use the published string** *"read the phase before you read the logs"* — Chapter 5 publishes it twice, Chapter 4 a third variant |
| **Ch 16** | Application-scope triage — the Pod is fine and the application isn't |

## Related

[[container-state]] · [[restart-policy]] · [[status]] · [[spec]] · [[pod]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/container-state.md ===
# Concept: Container state

**Home:** Chapter 5 §5 · **Competency:** D1.1 · **Status:** canonical

## Definition

Each **container** in a Pod is in one of three states
[source: k8s-docs-pod-lifecycle-2026-08-23]:

| State | Verbatim | Carries |
|---|---|---|
| **`Waiting`** | "still running the operations it requires in order to complete start up: pulling the container image, applying Secret data" | a **`Reason`** field summarizing *why* |
| **`Running`** | "executing without issues" | a `startedAt` timestamp |
| **`Terminated`** | "began execution and then either ran to completion or failed" | a reason, an **exit code**, start and finish times |

## Why a state tells you more than a phase

> A phase is one word. A container state comes with a `Reason`, or an exit code, or a
> timestamp: the specifics of *what*, not just *which*.

**A Pod with three containers has one phase and three states.**

## The three-field reading — the shape to remember

Worked on `ImagePullBackOff` [source: k8s-docs-images-2026-08-23]:

| Signal | Value | Scope |
|---|---|---|
| Pod phase | `Pending` | Pod |
| Container state | `Waiting` | Container |
| Container `Reason` | `ImagePullBackOff` | Container |

"The phase tells you the Pod hasn't gotten going. The state tells you which container. The
`Reason` tells you why. **Three fields, three levels of specificity, and only the third one is
actionable.**"

## ⚑ The most self-concealing error in the chapter

Answering **"state: `ImagePullBackOff`"**. The three states are `Waiting`, `Running`,
`Terminated` and nothing else is ever one of them. `ImagePullBackOff` is a **`Reason`**.

The chapter's diagnosis is worth preserving verbatim as a teaching move: *"If you wrote the
right string in the wrong slot, you have the fact and not yet the taxonomy… It is also the
most self-concealing miss in the chapter, because the correct string appears in your answer
and it looks right."*

## ⚑ Vocabulary gap: `CrashLoopBackOff`

The counterpart `Reason` for a container that **has** been created, has failed, and is serving
its backoff appears in **no cached snapshot.** It is needed in two places (the §5 figure
overlay and one sentence of prose) and is currently a placeholder. **Open a research fetch**
for container status reasons — candidates: the Pod-lifecycle container-states section, or the
Pod API reference `ContainerStateWaiting`.

## Related

[[pod-phase]] · [[restart-policy]] · [[probe]] · [[resource-limit]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/restart-policy.md ===
# Concept: `restartPolicy` and the restart backoff

**Home:** Chapter 5 §5 · **Competency:** D1.1 · **Status:** canonical

## Definition (verbatim)

> The `spec` of a Pod has a `restartPolicy` field with possible values **`Always` (the
> default)**, `OnFailure`, and `Never`. **The `restartPolicy` applies to all containers in the
> Pod.** [source: k8s-docs-pod-lifecycle-2026-08-23]

It is set once, on the Pod. That is trap #3 of §5's hazards block stated as a fact.

## The backoff schedule (verbatim)

> After containers in a Pod exit, the kubelet restarts them with an **exponential backoff
> delay — 10s, 20s, 40s, and so on — capped at five minutes.** Once a container has executed
> for **10 minutes without any problems**, the kubelet resets the restart backoff timer for
> that container. [source: k8s-docs-pod-lifecycle-2026-08-23]

## 🔭 Why those two numbers — the transferable part

> The **five-minute cap** is a floor on how bad things can get: no matter how long a container
> has been failing, you never wait more than five minutes to find out whether the next attempt
> works. The **ten-minute reset** is a forgiveness window… **Cap plus forgiveness.** Neither
> number is magic, but the *shape* — bounded penalty, earned amnesty — is a pattern you'll see
> again in distributed systems.

## ⚑ Two scope caveats — do not restore the absolute

The prior draft asserted "there is no way to configure one container to restart and another
not to." **That absolute was correctly dropped**, not scoped, for two reasons:

1. It is unverifiable against the cache.
2. **Sidecar containers are init containers carrying `restartPolicy: Always`** — so
   per-container restart behavior *does* exist via that mechanism.

Further: the retrieved init-containers text states that a Pod policy of `Always` causes init
containers to use **`OnFailure`**. So *"applies to all containers"* is true of the **field's
scope** but **not of the resulting behavior in every case.** Both snapshots must be
materialized before the absolute is restored in any form.

## ⚑ The other "five minutes" in the same section

`ImagePullBackOff` retries "up to a compiled-in limit of 300 seconds (five minutes)"
[source: k8s-docs-images-2026-08-23] — a **separate** backoff governing *pulls*, not
*restarts*, fifteen lines away in §5. The chapter never distinguishes them and a reader will
reasonably conclude they are one cap. **One clause fixes it.**

## Where it becomes visible

A **liveness probe** failure hands the container to exactly this machinery — which is why §5
precedes §7. See `probe.md`.

## Related

[[pod-phase]] · [[container-state]] · [[probe]] · [[init-container]] · [[pod-lifetime]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/serviceaccount.md ===
# Concept: ServiceAccount — a Pod's identity

**Home:** Chapter 5 §6 · **Competency:** D1.1 · **Status:** canonical *(identity only)*
**Scope boundary:** Chapter 12 owns authorization, RBAC binding, and token hardening.
**Closes:** the `Ch 5 (planted)` half of Chapter 4's reservation.

## Definition (verbatim)

> A service account is **a type of non-human account that, in Kubernetes, provides a distinct
> identity in a Kubernetes cluster.** [source: k8s-docs-service-accounts-2026-08-23]

Application Pods use one to identify themselves to the API server.

## Four facts, and then the chapter stops

1. **Namespaced, with a `default`.** "ServiceAccounts are namespaced, and every namespace gets
   one named `default` upon creation."
2. **Automatic assignment.** "If you deploy a Pod in a namespace and don't manually assign a
   ServiceAccount to it, Kubernetes assigns the `default` ServiceAccount for that namespace to
   the Pod."
3. **No permissions by default.** "The `default` service accounts get no permissions by
   default" beyond the API discovery permissions granted to all authenticated principals when
   RBAC is enabled.
4. **Assigned via `spec.serviceAccountName`.**

All four: [source: k8s-docs-service-accounts-2026-08-23]

## ⚓ Worth Securing (verbatim)

> **Every Pod has an identity whether or not you gave it one.** Practitioners find this
> genuinely surprising the first time — the mental model of "I didn't configure
> authentication, so there isn't any" is wrong. There is an identity, it's the namespace's
> `default`, it can authenticate to the API server, and it can do almost nothing.

**The two halves are independent and both are graded:** it *has* an identity (authentication);
it has almost no *authorization*.

## The credential, in one sentence

> In Kubernetes v1.22 and later, Kubernetes gets a **short-lived, automatically rotating
> token** using the TokenRequest API and mounts it as a **projected volume**. Long-lived
> ServiceAccount token Secrets don't expire or rotate and are not recommended.
> [source: k8s-docs-service-accounts-2026-08-23]

The `kubernetes.io/service-account-token` type still exists; it's the legacy form
[source: k8s-docs-secret-2026-08-23]. **Consistent with Chapter 4's glossary row — checked,
no drift.**

⚑ **`projected volume` is named here and never defined,** and it is the chapter's only
deferred term without a cross-bearing. Add
`*[cross-bearing: see Ch 11 §1 — projected volumes]*`.

## Theme retrieval landed here

Fact One is the **first landed retrieval of Chapter 4's namespaced-vs-cluster-scoped theme**,
and it was unplanned — Chapter 4 beared that theme to Chapters 10, 11, and 12, not to 5. The
chapter's own framing: "here it is doing work rather than being recited." ⚑ It does **not** use
Chapter 4's canonical retrieval string (*"Not everything lives in a namespace"*).

## Related

[[secret]] · [[namespace]] · [[cluster-scoped-resource]] · [[pod]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/probe.md ===
# Concept: Probes — three types, four mechanisms, three failure behaviors

**Home:** Chapter 5 §7 · **Competency:** D1.1 · **Status:** canonical
**Pays:** the second half of Chapter 3's debt — the kubelet ensures containers are "running
**and healthy**." §1 handled *running*.

**Held in one shard on purpose.** The three probe types are split across
`kb_tags` as `liveness-probe`, `readiness-probe`, `startup-probe`, but the examinable fact is
the **discrimination between their failure behaviors**. Three separate shards would let the
one thing that matters fall between them.

## Definition (verbatim)

> A probe is **a diagnostic performed periodically by the kubelet on a container.**
> [source: k8s-docs-pod-lifecycle-2026-08-23]

## The two axes are orthogonal — keep them in separate compartments

The **mechanism** is *how the question is asked*. The **type** is *what the answer is used
for*. "Keep them in separate compartments and this section is easy. Merge them and you'll be
trying to memorize twelve things instead of seven."

### The four mechanisms [source: k8s-docs-pod-lifecycle-2026-08-23]

| Mechanism | Success means |
|---|---|
| `exec` | Exit status 0 |
| `httpGet` | Status code ≥ 200 and < 400 |
| `tcpSocket` | The port is open |
| `grpc` | The gRPC health check passes ⚑ authorial — snapshot says only "grpc (gRPC health check)" |

`httpGet` goes to **the Pod's** IP, not the container's — §1's fact resurfacing.

⚑ **The orthogonality claim itself — "any probe type can use any mechanism" — is correct but
nowhere asserted in the snapshot.** It is inferred from adjacent sentences, and it is the
entire answer to **Practice Q17**, whose three distractors all depend on it. Source it before
a graded item rests on document layout. *(Q17 is the audit's identified cut candidate if the
21-question outline budget must hold exactly.)*

### The three types, by consequence of failure

| Type | Asks | On failure | Does **not** |
|---|---|---|---|
| **`livenessProbe`** | Is the container running? | **kubelet kills the container** → restart policy applies | remove it from Service endpoints |
| **`readinessProbe`** | Can it respond to requests? | **Pod IP removed from the endpoints of all matching Services** | kill or restart anything — the container keeps running |
| **`startupProbe`** | Has the application started? | kubelet kills the container → restart policy | run alongside the others — it **suppresses** them until it succeeds |

[source: k8s-docs-pod-lifecycle-2026-08-23]

## ★ Fixed Point (verbatim)

> **Liveness failure → the kubelet kills the container** (restart policy then applies).
> **Readiness failure → the Pod's IP is removed from the endpoints of all matching Services;
> nothing is restarted.** **Startup probe configured → all other probes are disabled until it
> succeeds.**

The one-sentence form, if only one survives: *"Liveness restarts, and does not remove from
service. Readiness removes from service, and does not restart."*

The chapter's image: **"Readiness stands a container down from the watch. Liveness relieves it
of duty altogether."**

## 🪝 The startup-probe misconception

> Configuring a startup probe **disables** the liveness and readiness probes until it
> succeeds. Readers consistently assume all three run in parallel from the moment the
> container starts. They don't — and that suppression is the startup probe's entire reason for
> existing. Without it, a liveness probe would kill a slow-starting application before it ever
> finished starting, forever.

The suppression **lifts** the moment it succeeds. A startup probe that permanently disabled the
other two would leave you with no health checking at all.

## Parameters — deliberately shallow

`initialDelaySeconds`, `periodSeconds`, `timeoutSeconds`, `successThreshold`,
`failureThreshold` [source: k8s-docs-pod-lifecycle-2026-08-23]. "Choosing good values is a real
engineering skill and it isn't what this exam is asking."

## What a probe is not

**Observability.** "A probe answers a yes/no question for the kubelet's benefit and produces no
history, no trend, and no measurement." Chapter 18 owns that distinction.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| **Ch 9** | Readiness **is** the mechanism that removes a Pod from Service endpoints — the forward plant |
| **Ch 6** | Probes are what make a rolling update safe: a Pod that never reports ready never receives traffic |
| **Ch 18** | Health checking is not observability |

## Related

[[pod-shared-context]] · [[restart-policy]] · [[container-state]] · [[pod-phase]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-request.md ===
# Concept: Resource request — what the scheduler reads

**Home:** Chapter 5 §8 · **Competency:** D1.1 · **Status:** canonical
**Forward reach:** the longest in the book — four later chapters retrieve it by name.

## Definition (verbatim)

> When you specify the resource request for containers in a Pod, **the kube-scheduler uses
> this information to decide which node to place the Pod on**… The kubelet also **reserves at
> least the request amount** of that system resource specifically for that container to use.
> [source: k8s-docs-resource-management-2026-08-23]

## A request is a floor, not a ceiling

> If the node where a Pod is running has enough of a resource available, it's **possible — and
> allowed —** for a container to use more of that resource than its request specifies. However,
> a container is not allowed to use more than its resource limit.
> [source: k8s-docs-resource-management-2026-08-23]

Exceeding your request on a node with spare capacity is **normal, expected behavior, not a
violation of anything.** Bearings #3 Q4 grades exactly this.

## 🪢 Mnemonic (verbatim)

> **Requests are about placement. Limits are about containment.** Scheduler places; kubelet
> contains.

## Units

**CPU.** "1 CPU unit is equivalent to 1 physical CPU core, or 1 virtual core." Fractional
requests allowed; `0.1` ≡ `100m` ("one hundred millicpu"). CPU "is always specified as an
**absolute amount, never as a relative amount**" — `500m` is the same computing power on a
single-core or a 48-core machine, which makes a CPU request **portable across node types by
construction.** Floor on precision: "Kubernetes doesn't allow CPU resources finer than `1m`."

**Memory.** In bytes; plain integer or suffixes, decimal (`k`, `M`, `G`) or power-of-two
(`Ki`, `Mi`, `Gi`). In practice `Mi` and `Gi`.

All: [source: k8s-docs-resource-management-2026-08-23]

## ⚠ The `m` / `M` trap

> **`M` means megabytes. `m` means millibytes.** A request of `400m` of memory is a request for
> **0.4 bytes.** [source: k8s-docs-resource-management-2026-08-23]

`m` is correct and idiomatic **for CPU**. It is wrong **for memory**. "Habit carries it across,
and nothing in the manifest will stop you." One keystroke, nine orders of magnitude — the most
mechanically checkable gotcha in the chapter.

## Resource types

`cpu` and `memory` are specified constantly; `ephemeral-storage` and `hugepages-<size>` (Linux
only) exist and are specified the same way; clusters can provide **extended resources**,
"custom-named resources typically exposed by device plugins."
[source: k8s-docs-resource-management-2026-08-23]

## ⚑ Pod-level aggregation is NOT claimed here

§9's synthesis bullet was **correctly reworded** away from asserting that a Pod's request is
the sum of its containers' requests — that rule is not in
`k8s-docs-resource-management-2026-08-23`. It **is** recoverable from the pending
`k8s-docs-pod-qos-2026-08-24.md`: *"The resource request of a Pod is equal to the sum of the
resource requests of its component Containers."* **The init-containers snapshot complicates it
for Pods declaring init containers — check both before writing the aggregate claim.**

## Downstream obligations — all four are published promises to the reader

| Chapter | Obligation |
|---|---|
| **Ch 7** | Requests as the scheduler's filtering step |
| **Ch 13** | What the system reports when a Pod is killed for using too much |
| **Ch 17** | The baseline autoscalers compare observed usage against |
| **Ch 18** | The denominator when monitoring reports "utilization" |

§8 tells the reader outright: "Two numbers in a Pod spec; four later chapters."

## Related

[[resource-limit]] · [[pod]] · [[spec]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-limit.md ===
# Concept: Resource limit — what the kubelet enforces

**Home:** Chapter 5 §8 · **Competency:** D1.1 · **Status:** canonical

## Definition (verbatim)

> When you specify a resource limit for a container, **the kubelet enforces those limits** so
> that the running container is not allowed to use more of that resource than the limit you
> set. [source: k8s-docs-resource-management-2026-08-23]

## Two words, two components

| | **Request** | **Limit** |
|---|---|---|
| Who reads it | **kube-scheduler** — to choose a node | **kubelet** (with the kernel) — to enforce at runtime |
| What it means | *Reserve at least this much for me* | *Never let me exceed this* |
| When it acts | At placement time, once | Continuously, while the container runs |

## ★ The asymmetry — the part most people don't know

**CPU limits throttle.**
> When a container approaches its cpu limit, the kernel will restrict access to the CPU
> corresponding to the container's limit. Thus, a cpu limit is a **hard limit the kernel
> enforces.** [source: k8s-docs-resource-management-2026-08-23]

**Memory limits kill, reactively.**
> When a container uses more than its memory limit, the kernel may terminate it. However,
> **terminations only happen when the kernel detects memory pressure.** Thus, a container that
> over allocates memory may not be immediately killed; **memory limits are enforced
> reactively.** [source: k8s-docs-resource-management-2026-08-23]

## What an operator actually observes

- **Exceed CPU → you get slow.** The container keeps running. **Neither the Pod phase nor the
  container state changes.** This is the failure mode that hides from every signal §5 taught.
- **Exceed memory → you eventually get dead.** But not necessarily *when* you exceed it — the
  container reaches `Terminated` with a reason and exit code, possibly hours later, at a moment
  correlating with something else entirely on the node.

That word *reactively* "is why memory problems in Kubernetes have a reputation for being hard
to reproduce: the trigger for the kill isn't your container's behavior alone, it's the node's
aggregate pressure."

## ⚑ The status string is NOT defined here

`OOMKilled` belongs to **Chapter 13**, and Chapter 5 bears forward correctly — it teaches the
*mechanism* and reserves the *string*. File the glossary entry under Chapter 13 so Stage 14
does not cross-reference it to the wrong chapter.

## ⚑ BLOCKED: QoS classes

§8 has **no Leg four.** Guaranteed / Burstable / BestEffort, their derivation from how requests
and limits were filled in, and the node-pressure eviction ordering are all absent, and
`ch05-fig05-requests-limits-qos-classes` ships with a deliberately empty lower strip. The
chapter assesses **zero** QoS items against four outline-tagged QoS concepts.

**The cut was correct** — a grep of all 115 snapshots returns nothing for any of the three
class names, and Open question #2 forbids writing from memory.
`k8s-docs-pod-qos-2026-08-24.md` is preserved at research-manifest line 293.

**Two guards when writing it:**
1. That page's loose generalization — *"Any Container exceeding a resource limit will be killed
   and restarted by the kubelet"* — **contradicts the verified asymmetry above.** Do not let it
   overwrite this shard.
2. **Do not name a `status.qosClass` field** — the manifest confirms the source's prose does
   not.

Add 2–3 assessment items when the section lands.

## Related

[[resource-request]] · [[container-state]] · [[pod-phase]] · [[restart-policy]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 5 update (2026-08-24)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.1** | Chapter 3 *(cluster layer)* | deep | 2026-08-24 |
| **D1.1** | Chapter 4 *(object layer)* | deep | 2026-08-24 |
| **D1.1** | **Chapter 5** *(workload layer)* | **deep** | **2026-08-24** |

**Registry row change:** `D1.1 | Kubernetes Core Concepts | Ch 3, 4, 5, 6` →
status becomes **"in progress — Ch 3, 4, and 5 covered 2026-08-24"**.

### Chapter 5 — D1.1 coverage detail

`kb_tags.objectives: ["D1.1"]`; all nine sections carry `objectives: ["D1.1"]`.

| Sub-topic | Depth |
|---|---|
| Pod as the unit of scheduling; the definition itself | **deep — closes a four-chapter gap** |
| Shared network namespace, Pod IP, `localhost`, shared volumes | **deep — Ch 9's premise originates here** |
| Multi-container Pods; the two-mechanism test; sidecar | moderate — ⚑ mechanism unsourced |
| Init containers: ordering, run-to-completion, failure | moderate — ⚑ **entirely unsourced** |
| Pod lifetime; scheduled once; replaced with a new UID | deep — **discharges Ch 4 commitment #3** |
| Pod phase vs container state | **deep — the centerpiece; Ch 13's method depends on it** |
| `restartPolicy` scope, values, exponential backoff | deep |
| ServiceAccount as Pod identity | moderate — **closes Ch 4's `Ch 5 (planted)` half** |
| Probes: three types, four mechanisms, three failure behaviors | **deep — pays Ch 3's "and healthy" debt** |
| Requests vs limits; CPU throttle vs reactive OOM; units | **deep — four later chapters retrieve it** |
| **QoS classes** | ⚑ **ABSENT — outline-mandated, cut for lack of a snapshot** |
| **Graceful termination** | ⚑ **ABSENT — `kb_tags` claims `pod-termination`** |
| `pod-template` | deferred to Ch 6 — correct; the tag is aspirational |
| `kubectl` command surface | deliberately deferred to Ch 13 / Ch 16 |

---

## ⚑ Book-level: the authored allocations are approaching the domain ceiling

Kubernetes Fundamentals is **44%** of the published exam. Four chapters sit inside it and each
publishes an authored allocation in a differently-worded metadata line:

| Chapter | Claimed | Metadata form |
|---|---|---|
| Ch 2 | ~9% | **the only one that discloses "authored allocation" inline and source-tags it** |
| Ch 3 | ~6% | "authored estimate" |
| Ch 4 | ~6% | no caveat at all |
| **Ch 5** | **7%** | "This book's allocation" — no caveat, no tag |
| **Subtotal** | **28% of 44%** | |

That leaves **16 points for Chapter 6 alone** — larger than Chapters 3, 4, and 5 combined.
Either the allocations need rebalancing or Chapter 6's will have to be authored to fit a
residue rather than derived from its content. **Settle before Chapter 6 drafts.**

This is also the concrete reason to act on Stage 13's T4 rather than defer it: four chapters
publish an authored number and **one** of them tells the reader it is authored. Chapter 1
committed the book to that disclosure in prose. **Conform Ch 5 to Chapter 2's shape; flag
Ch 3 and Ch 4 for `reconcile.py`.** Note the competency separator also drifts three ways
(`— competency: X` / `— X` / `(X)`); pick one.

---

## ⚑ Ethical-guardrail status — Chapter 5

| Chapter | Guardrail #8 | Note |
|---|---|---|
| Ch 1 | pass | |
| Ch 2 | pass | models the compliant phrasing |
| Ch 3 | **FAIL — open** | six unverifiable exam-frequency assertions |
| Ch 4 | BORDERLINE | five practitioner-prevalence superlatives |
| **Ch 5** | **BORDERLINE** | **four exam-frequency assertions + prevalence superlatives** |

**This diverges from Stage 13, which recorded a pass.** Stage 13's reasoning — that the
subtitle's "worth points" is the only soft claim and is defended structurally in §9 — is
correct about the subtitle. It is not correct that the chapter carries no unhedged frequency
claims. Four assertions about **exam behavior** are present in the finalized text:

1. §3 — "**This is the part the exam cares about.**"
2. §5 — "**both of those breadths are tested**"
3. §7 — "the consequence of failure. **That's what gets tested**"
4. Bearings #1 A1 — "**It will cost you points here**"

Plus the practitioner-prevalence register Chapter 4 was flagged for: "Readers consistently
assume," "the probe people most often reverse," "Practitioners find this genuinely surprising
the first time," "the part most people don't know," "the easiest carry-over error to make."

These are mild and the underlying judgments are very likely right. But they are unsourced
claims about what an exam does — **Chapter 3's specific flagged failure mode, which Chapter 4
had cleanly avoided.** A second chapter drifting back into the construction while Chapter 3's
remediation is still open is the signal worth having. **Hedging all four costs about six
words.** Author call; not marked failing.

**Everything else on the Part 14 checklist passes, several unusually well:**

- **No statistics of any kind.** No invented pass rates, no "73% of breaches." Every number is
  a sourced mechanism value (300 s, 10s/20s/40s, 5-minute cap, 10-minute reset, HTTP
  ≥200/<400, v1.22, the `1m` floor).
- **Subject dignity (v5.7): clean.** Every wry beat lands on the practitioner. None lands on
  anyone harmed by a failure.
- **Simplification acknowledged.** Two Dead Reckoning blocks; §7 explicitly declines to teach
  probe tuning and says why; §8 names the minor resource types and stops; §5 states outright
  that "the phase cannot tell you that."
- **No strawmanning.** §2's rebuttal of "one process per Pod" engages the doctrine on the
  merits and declines the opposite absolutism.

**⚑ The condition on the "authority claims" pass.** Five load-bearing claim clusters are stated
confidently in prose while carrying no source tag, flagged only in HTML comments the reader
never sees: init-container semantics (§3), the "two main ways" framing (§2), "smallest
deployable unit" (§9), the PodSpec identity (§1), and probe-type/mechanism orthogonality (§7).
Against guardrail #4 — *never claim certainty where legitimate uncertainty exists* — **an
invisible comment is not a hedge to the reader.** The draft handled this correctly by not
fabricating tags. **This item passes on the condition that the five snapshots are materialized
and the claims tagged before publication.** If any cannot be, the affected prose must be
softened to an explicit authorial gloss, and the two graded items whose correct answers depend
on untagged claims — **Practice Q17 and Practice Q10's distractor-C rebuttal** — must be
reworked or cut.

---

## ✅ Gate status — the one that improved

**Chapter 5 has a real fact-accuracy audit, and its blocking findings were remediated.**
Stage 6 inspected 148 claims (81 tagged-and-verified, 17 untagged FAIL, 3 contradicted FAIL,
17 WARN) and all three contradicted claims plus one over-tagging WARN were fixed in the
finalized chapter. **This is the first chapter in the book where a blocking fact-accuracy
finding was raised and discharged.**

Structural: **0 fail / 0 warn / 30 pass.**

⚑ **Chapter 4 still has no audit at all**, and Chapter 5's Stage 6 identifies the shared root
cause: Stage 6's declared input is `draft-v2.md`, which does not exist at that point in the
graph. **Correct the Stage 6 input resolution to `draft-v1.md`** and both chapters are fixed
at the source.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 5 update (2026-08-24)

**8 tagged in-budget items · graded pool 38 (15 Bearings + 23 Practice) · rate = 21.1%.**
B3's rung for Chapter 5 is **20%. Cleared.** Two further tagged items sit in Soundings,
excluded from the budget by B3.

**Chapter 5 is the first chapter to draw from three predecessors.** Ch 4 drew from two, Ch 3
from one.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| `spec` / `status`; which reports what is true now | ch 4 §2 | **ch 5** — Soundings Q7 *(excluded from budget)* |
| `ImagePullBackOff`; reported as a container in **Waiting** | ch 2 §6 | **ch 5** — Soundings Q8 *(excluded from budget)* |
| the kubelet ensures PodSpec containers are running and healthy | ch 3 §3 | **ch 5** — Bearings #1 Q5 |
| `ImagePullBackOff` as a container-status `Reason` | ch 2 §6 | **ch 5** — Bearings #2 Q4 |
| which of `spec`/`status` carries `phase`; who writes it | ch 4 §2 | **ch 5** — Bearings #2 Q5 |
| labels as identifying attributes in `metadata`, selectable | ch 4 §5 | **ch 5** — Practice Q5 |
| `kubernetes.io/service-account-token` as legacy; TokenRequest since v1.22 | ch 4 §4 | **ch 5** — Practice Q13 |
| container immutability as a design principle | ch 2 §2 | **ch 5** — Practice Q20 |
| the control loop; kubelet as reconciliation | ch 3 §6 | **ch 5** — Practice Q21 |
| image-pull failure gating the init sequence | ch 2 §6 | **ch 5** — Practice Q22 |

**Notes on quality, all favourable:**

- **Practice Q22 is the strongest interleaving item the book has produced.** It borrows
  **Q9's own reasoning** as its trap — correct there, wrong here — and the discriminator is a
  single word (*created*). "Same rule, opposite outcome."
- **Bearings #1 Q5 is the cleanest cross-chapter seam so far.** Chapter 3's kubelet sentence
  contained two undefined nouns; this item cashes both at once and reveals the sentence was
  "all along, a description of a reconciliation loop with a PodSpec as its input."
- **Practice Q13 is genuine retrieval**, not new material wearing a tag — Chapter 4 publishes
  the v1.22/TokenRequest fact itself.
- **Q6's distractor D is unusually good**: it accepts that the Pod doesn't move but still
  assumes the *object* survives — the residual half of the misconception D6 tests.

**⚑ One prescribed anchor only partially hit.** The outline names three retrieval anchors; two
land exactly (Bearings #2 Q5; Practice Q5). The first — *"`imagePullPolicy` (Ch 2) as a cause
of a container state"* — lands in its neighbourhood but **never names `imagePullPolicy`**, the
field Ch 2 §6 spent its length on. Practice Q20's distractor D ("images are re-pulled on every
restart") is an `imagePullPolicy` fact in all but name. **Naming it there costs one word.**

**⚑ Retrieval tags absent from the answer keys.** Chapter 4 repeats the tag in its answers;
Chapter 5 tags only the stems. Repeating it tells a reader who missed the item *which chapter
to go back to* — the whole point of the tag. Match Chapter 4.

---

## Cross-cutting themes — status after Chapter 5

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **The control loop** (B3 headline) | Ch 3 §6 | Ch 4 · ✅ **Ch 5 — unplanned** | Ch 6, **Ch 11 (still unbeared)**, Ch 15, Ch 17 |
| **Namespaced vs cluster-scoped** | Ch 4 §3 | ✅ **Ch 5 §6 — FIRST retrieval, unplanned** | Ch 12 §3, Ch 10, Ch 11 |
| **Labels/selectors as the universal join** | Ch 4 §5 | ✅ **Ch 5 Practice Q5 — FIRST retrieval, unplanned** | Ch 6, Ch 7, Ch 9, Ch 10 |
| **The absent-component pattern** | Ch 3 §4, named | — *(still zero, two chapters on)* | Ch 10 ×2, Ch 13, Ch 17 |
| **"Kubernetes defines an interface, the ecosystem implements it"** | Ch 2 §4, named | ⚑ still zero named recurrences | Ch 9 (CNI), Ch 11 (CSI), Ch 17 §4 |

**All three of Chapter 5's theme retrievals were unplanned.** `control-loop.md`'s obligations
table has no Chapter 5 row; Chapter 4 beared the two new themes to Chapters 6, 7, 9, 10, and 12,
not to 5. Chapter 5 picked them up anyway, at the natural moment, without being told to. **That
is the first evidence the theme architecture works without explicit bearings** — and it is a
better signal than Chapter 4's discharged obligation, because nothing instructed it.

**⚑ Both new themes are still retrieved by paraphrase, not by name.** §6 does the
namespaced/cluster-scoped work in prose without using either canonical retrieval string. The
strings were fixed at Chapter 4 precisely so five downstream chapters wouldn't each invent a
paraphrase — and the first downstream chapter invented one. **The decision deadline stands: a
coined name must be chosen before Chapter 10 drafts,** the first chapter needing both themes at
once.

**⚑ The `reconciliation` gap has crossed into the assessment surface.** Chapter 3 promised the
reader that later chapters saying "reconciliation" would mean closing-the-gap work. Chapter 4
described the behavior three times and never named it. **Chapter 5 now uses the word in two
graded answers** — Bearings #1 A5 and Practice Q21's correct answer. The book is grading
readers on a word it promised to define and hasn't, and B3 runs the theme through Ch 6, 11, 15,
and 17. **One appositive at Chapter 3's ★ Fixed Point closes it.**

---

## Forward commitments — status

| # | Commitment | Status |
|---|---|---|
| 1 | Ch 13 must carry a Ch 8 retrieval item (version skew) | **OPEN** — untouched at Ch 5 |
| 2 | Ch 11 must retrieve the control loop | ⚑ **OPEN, three chapters overdue.** Chapter 5 bears to Ch 11 **twice** and neither carries the loop. Ch 3, Ch 4, and Ch 5 have each passed it forward |
| 3 | Ch 5 must retrieve the UID rule | ✅ **DISCHARGED.** §4's ⚓ Worth Securing quotes Chapter 4's UID definition verbatim with its source tag; Practice Q6's distractor-D rebuttal makes it a discriminator. *Lands in prose and an untagged rebuttal, not as a `[retrieval: ch4]` graded item — which still satisfies the wording exactly* |
| 4 | Ch 12 must **derive** the RBAC 2×2 from the namespaced boundary | **OPEN** |
| 5 | **Ch 9 must retrieve the Pod IP / shared network namespace** | **NEW.** §1 tells the reader the entire argument for Services rests on it. A published promise |
| 6 | **Ch 13's method must be "read the phase before you read the logs"** | **NEW.** Chapter 5 publishes that exact string twice; Chapter 4 a third variant. Ch 13 must use the phrasing, not a paraphrase |
| 7 | **Ch 6 must open on "if Pods are designed to be replaced, who does the replacing?"** | **NEW.** Chapter 5's Voyage Ahead hands over the opening question *and* tells the reader the Pod is "something you will almost never create directly" |
| 8 | **Ch 7, 13, 17, 18 must each retrieve requests/limits** | **NEW — the largest single obligation in the book.** §8 tells the reader "four later chapters retrieve it by name" and names all four |

---

## ⚑ §N reservations — Convention 5 broken a second time, collisions now three-deep

Chapter 3's ledger proposed *"no `§N` in cross-bearings that point into undrafted chapters."*
Chapter 4 broke it 15 times; **Chapter 5 pins §-numbers into eleven undrafted chapters, 17
times.** Never ratified — a governance decision, not a defect — but the count grows each
chapter and it is the direct cause of the collisions below.

| Reservation | Claimants | Status |
|---|---|---|
| **Ch 9 §1** | Ch 2 (*CNI and pod networking*) · **Ch 5** (*why a Service is necessary*) | ⚑ **HARD COLLISION — blocking before Ch 9 drafts.** Ch 2 has precedence and the arc outline's ordering (network model → Pod IP → CNI → Service) supports it. Move Ch 5 to §2 or §3 |
| **Ch 17 §2 / §3** | Ch 5 (autoscaling / mesh) vs Ch 2's published **Ch 17 §4** | ⚑ Probable ordering conflict — the outline puts both at §5+, and autoscaling **after** mesh. **Drop to chapter-level** until Ch 17 is outlined *(a sanctioned form; Ch 3 already uses it)* |
| **Ch 12 §2** | Ch 2 (supply chain) · Ch 4 (access control) · **Ch 5** (SAs as RBAC subjects) | ⚑ Three-deep. §3 is likelier for Ch 5's claim |
| **Ch 6 §3** | Ch 1 · Ch 2 · Ch 4 | ⚑ Three-deep, carried from Ch 4. **Ch 5 correctly avoided it** — its StatefulSet mention pins no section at all |
| Ch 11 §1, Ch 13 §2/§3/§4, Ch 15 §4, Ch 16 §1/§2, Ch 18 §1/§3, Ch 6 §1, Ch 7 §2, Ch 9 §4 | Ch 5 | ✅ verified compatible with published claims and the outline |

## ⚑ Two figure-anchor notes closed as NOT defects

Both of the draft's own AUTHOR-REVIEWs on figure anchors would, if acted on, make Chapter 5
**less** consistent with the book. Recorded here so the next stage does not re-raise them:

1. **`ch05-zenith-smallest-deployable-unit` is not malformed.** `arc-outline.md` prescribes
   `chNN-zenith-<slug>` for **every** chapter's Zenith figure, and **Chapter 2 already shipped
   `ch02-zenith-standard-crate` in published prose.** Renaming would make Chapter 5 the only
   deviating chapter and break the pattern for fifteen undrafted ones. **Keep the anchor**; add
   `chNN-zenith-<slug>` to the structural contract as a sanctioned second form so the linter
   stops flagging it; strike the rename proposal at `image-specs.md` line 558.
2. **The figure numbering is not out of order relative to its contract.** The five `figMM` slugs
   are prescribed verbatim by `arc-outline.md`, and **Chapter 2 shipped with the same property**
   (`ch02-fig04` appears before `ch02-fig03`). The anchors are the join key into
   `image-specs.md`. **The draft was right to preserve them unrenamed.**

## Convention status

`[retrieval: chN]` tags render **reader-visible, bold-bracketed in the stem**. Three chapters
of consistent practice (Ch 3, 4, 5). ⚑ Chapter 5 breaks the *answer-key* half of Chapter 4's
practice. **Still OBSERVED PRACTICE pending author ratification — and the window to change it
cheaply has effectively closed.**

=== END APPEND ===

---

**The three things worth your attention, in order.**

1. **Run Materializer A.** Five snapshots sit fully preserved in `ch-05/research-manifest.md` and absent from `sources/`. One script run unblocks five untagged claim clusters, the QoS section, the graceful-termination paragraph, a ★ Fixed Point, a 🪢 Mnemonic, four Bearings items, and three Practice questions — two of which have correct answers currently resting on untagged claims. Chapter 5's research stage wrote nothing: `sources/` is still 115 files, the same count Chapter 4 reported.

2. **Correct Stage 6's input resolution to `draft-v1.md`.** That single fix explains both Chapter 4's missing audit and Chapter 5's audit having to improvise its input. Chapter 5's audit is the good news here — it ran, found three contradicted claims including a figure that taught the opposite of §5's centerpiece, and all three were remediated before the chapter finalized. That is the gate working for the first time.

3. **Chapter 5 closed the book's longest-standing gap — `Pod` — and opened four new forward commitments.** The Pod was reserved at Chapter 1, promised at Chapter 2, and used roughly 120 times undefined across Chapters 3 and 4. It is defined now, along with `PodSpec` and the Chapter 5 half of `ServiceAccount`. Against that: `reconciliation` has now crossed from undefined-but-described into **undefined-but-graded**, and Chapter 11's control-loop retrieval is three chapters overdue with no chapter having anchored it.

One thing I did not do: I did not write the knowledge-base files or replay Chapters 1, 3, and 4. Replaying them is an author decision about canon ordering — Chapters 1 and 3 emit full-file writes while 4 and 5 emit appends, so running them out of order silently discards the later chapters' contributions. Both scripts are above and are safe to run in the stated order.