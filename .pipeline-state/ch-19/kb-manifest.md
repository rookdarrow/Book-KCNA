I read the existing KB tree, the binding scaffolding, the shipped chapters and the source corpus before writing. Six of my checks changed the picture — including two the integration report got wrong in the chapter's favour, and two new duplicate-slug pairs nobody has flagged. Leading with those.

---

# Knowledge-Base Manifest — KCNA Chapter 19

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-31

> **Greenfield notice, re-verified this run.** `Book-KCNA/knowledge-base/` **still does not exist on disk.** Eighteen manifests exist (`ch-01`…`ch-18`); none has been applied. Chapter 19 adds the nineteenth.
>
> **Ordering contract, inherited from Ch 12–18.** **APPEND** for the three shared registers and for every shard that already exists; **WRITE** only for slugs that collide with nothing. Every proposed Ch 19 slug was checked against the emitted-block enumeration across `ch-01`–`ch-18`. **Two collisions found and deliberately not created** — see ⚑ C4.
>
> **What is different about this chapter.** Ch 19 owns no new technical vocabulary — the B7 ledger says so explicitly at `term-ownership.md:616` ("Ch 19 owns no new technical vocabulary. It owns the reader-facing apparatus of the final review"). So the glossary harvest is six apparatus terms, not forty, and the concept layer is mostly **appends that add a discriminator to a shard that already has a definition.** That is the whole shape of a synthesis chapter's KB contribution.

---

## ⚑ Findings that change what downstream stages should do

### ⚑ C0. The draft's consolidated research-gap block is a false alarm, and the integration report is right — but its corpus figure is wrong too

`draft-v2.md` §2 opens a six-item AUTHOR-REVIEW block asking for six research passes, on the premise of "this chapter's 31-file corpus." Integration correctly rejected the block and gave the corpus as 199 files.

**Both numbers are wrong. `Book-KCNA/sources/` holds 303 `.md` files as of this run.** I counted them. Every one of the six requested fetches is already cached, verified by filename:

| Draft's requested fetch | Cached as |
|---|---|
| 1. RBAC reference | `k8s-docs-rbac-2026-08-23` · `k8s-docs-rbac-depth-2026-08-31` · `k8s-docs-rbac-good-practices-2026-08-31` |
| 2. NetworkPolicy concept | `k8s-docs-network-policies-2026-08-23` · `k8s-docs-network-policies-depth-2026-08-24` |
| 3. Ingress concept | `k8s-docs-ingress-2026-08-23` · `k8s-docs-ingress-controllers-2026-08-24` · `k8s-docs-ingress-depth-2026-08-24` |
| 4. Pod lifecycle | `k8s-docs-pod-lifecycle-2026-08-23` |
| 5. CNCF maturity levels | `cncf-project-maturity-levels-2026-08-23` |
| 6. ConfigMap/Secret, Helm charts, OTel traces | `k8s-docs-configmap-2026-08-23` · `k8s-docs-secret-2026-08-23` · `helm-charts-2026-08-31` · `opentelemetry-signals-2026-08-23` |

**Delete the block.** The remedy is integration's: add cross-bearings to the §2 rows that lack them, under the book-level ruling ratified at the Ch 18 gate. The one item in that block that is *not* discharged is the `restartPolicy` Deployment clause — see ⚑ C1.

### ⚑ C1. CONFIRMED by direct search — the `restartPolicy` Deployment clause is genuinely untaught

Integration's Contradiction 3 says §2's Domain 1 row asserts something no chapter teaches: *"a Deployment's Pod template cannot use `Never` at all; the API requires `Always` there."*

I searched every shipped chapter for `restartPolicy`. **28 occurrences, across Ch 5, Ch 6 and Ch 16. Not one states the Deployment-side restriction.** What is taught:

- **Ch 5** owns the field completely — Pod-level scope (`ch05:638`, `:646`, `:710`, `:1107`), the three values, the backoff schedule, and a Chapter Summary row at `:1442`. All sourced to `k8s-docs-pod-lifecycle-2026-08-23`.
- **Ch 6 `:906`** teaches only the *Job* converse: "a Job's Pod template may only use a `restartPolicy` of `Never` or `OnFailure`" `[source: k8s-docs-job-2026-08-24]`. The Deployment side is never stated.

**One correction to the integration report, in the chapter's favour.** Integration treats the whole row as suspect. The row's *other* clause — that a Job whose Pod template sets `Never` still gets a replacement Pod from the Job controller — **is taught and sourced**: `ch06:902`, "the Job will start a new Pod if the first one fails or is deleted" `[source: k8s-docs-job-2026-08-24]`. So the surgery is narrower than it looked: **cut the final sentence only.** The row survives intact, illustrating container-vs-Pod scope with the Job case, which is exactly what the fact-accuracy stage recommended.

### ⚑ C2. CONFIRMED against shipped text — Ch 1's provenance passage, with the exact lines

Integration's Contradiction 2 is the highest-consequence finding in the gate and every part of it checks out. Verified verbatim:

| Ch 1 | Text |
|---|---|
| `:202` | "The question count is published nowhere: not on the exam page, not in the FAQ, not in the CNCF curriculum." |
| `:204` | "…a question count that **travels on repetition alone**." |
| `:341` | *(graded answer key)* "The question count is not on the exam page — **or anywhere else the certifying body writes**." |
| `:554` | *(Chapter Summary)* "The question count (**published nowhere**)" |

`provenance-kcna-60-questions-2026-08-31.md` supersedes the 08-23 file, states "THAT STATEMENT IS FALSE and must not be relied on by any drafting or revision stage," and names the figure's publication point: the LF T&C DOCS page *Multiple Choice Exams: Important Instructions* — *"The multiple-choice exam is delivered online and consists of 60\* multiple-choice questions."* Its "distinction that survives" section is precisely the framing Ch 19 §3's ⚓ Worth Securing already ships, so **Ch 1 can adopt Ch 19's language rather than invent new.**

**Do not touch `ch01:211–213`.** The ⚠ hazard there — pace by proportion, not by question number — remains correct and is what Ch 19 §3's ★ Fixed Point implements.

**Confirmed too: `ch01:215` emits `*[cross-bearing: see Ch 20 §1 — how the mock exam is sized, and why]*`.** The skeleton forbids `Ch 20 §N` pointers. The *same sentence* also carries the now-false "commonly-reported format" framing, so one edit repairs both.

### ⚑ C3. The headword divergence is worse than a naming preference — the KB slug already sides against the chapter

Integration flags that Ch 19 says **thread** where the ledger says **cross-cutting theme** and shipped `ch18:1721` says "Nine **cross-cutting themes** traced through twenty chapters." Both verified.

What integration did not notice: **the Ch 19 outline's own `kb_tags.concepts` names the slug `cross-cutting-themes`** — the ledger's form, not the chapter's. So if the author ratifies "thread" as reader-facing, the knowledge base, the ledger and Ch 18's handoff all say one thing and the chapter says another.

My recommendation, and the shard is written to support either outcome: **keep the slug at `cross-cutting-themes.md` regardless** (it is the ledger's headword and the KB is a machine index, not reader-facing prose), and record both surface forms inside the shard so a later stage does not read the mismatch as drift. Then the author's only decision is the reader-facing word, and it costs one word in `ch18:1721` either way.

Same ruling for **discriminator** vs the ledger's **discriminating question** (`term-ownership.md:622`), which `ch18:1721` renders as "a question that discriminates between them."

### ⚑ C4. Two slug collisions, both declined

The outline's `kb_tags.concepts` names seven slugs. Two already have homes:

- **`absent-component-pattern`** — exists as `absent-component-pattern.md`, written at ch-03 and appended by ch-09, 10, 11, 12, 13, 14, 15, 17, 18. Ch 19 **appends**; no new slug.
- **`domain-weight-allocation`** — would sit beside `domain-weights-44-28-16-12.md` (ch-01, appended by ch-14, 15, 17, 18), holding the same 44/28/16/12 figures. Creating it reproduces the ⚑ I2 shape at the chapter that has the *least* claim to the territory. **Not created.** §4's allocation method — the build-your-own table, the priority order, the Community-and-Collaboration arithmetic — appends to the existing shard.

Five new slugs remain, all collision-free: `cross-cutting-themes` · `confusion-pair-matrix` · `discriminating-question` · `exam-pacing` · `the-lodestar`.

**Why `confusion-pair-matrix` and `discriminating-question` are two files and not one.** The Ch 18 precedent consolidates when the discrimination *is* the content. Here the ledger carries **two rows with two separate owners** (`:621`, `:622`), because one is a catalogue and the other is a method claim — *a discriminator is a procedure, and procedures survive pressure.* Two ledger concepts, two shards. They cross-link heavily so no later stage reads them as a ⚑ I2 split.

### ⚑ C5. Two NEW duplicate-slug pairs, previously unflagged — the ⚑ I2 fault is threefold, not single

⚑ I2 has been carried since ch-11 as one duplicate pair. Enumerating every emitted block this run, **there are three:**

| Pair | Written at | Both appended by |
|---|---|---|
| `pluggable-interface-pattern.md` / `pluggable-interfaces.md` | ch-02 / ch-11 | ch-13, ch-14, ch-15, ch-16 **← known (⚑ I2)** |
| `serviceaccount.md` / `serviceaccounts-and-identity.md` | ch-05 / ch-12 | **ch-15 appends to both** ← **NEW** |
| `cluster-scoped-resource.md` / `namespaced-vs-cluster-scoped.md` | ch-04 / ch-08 | **ch-08 writes one and appends the other** ← **NEW** |

Chapter 19 is where this stops being cosmetic, because threads 2 and 7 are exactly these two concepts and a synthesis chapter appending to both halves of a split would entrench it permanently. **Ch 19 appends to one side of each and declines the other:** `namespaced-vs-cluster-scoped.md` (the discrimination shard, per the `tag-vs-digest.md` / `oomkilled-vs-evicted.md` precedent) and `serviceaccounts-and-identity.md` (the ch-12 shard that owns identity as a concept rather than the object). `pluggable-interface-pattern.md` gets thread 6; `pluggable-interfaces.md` still gets nothing.

### ⚑ C6. The three fidelity repairs, verified against shipped text — all three confirmed

- **`Running` drops "or restarting."** `ch05:573` defines it as "at least one container is still running, **or is in the process of starting or restarting**," and the next line tells the reader both `Pending` and `Running` "are broader than their names suggest, and both of those breadths are tested." Ch 19 says "running or starting" in all three places. Two words, three insertions.
- **The second-default-IngressClass hazard is softer than what Ch 10 taught.** `ch10:720` is emphatic and sourced: a second default "does not widen the net — it **removes** it, and the Ingress **can no longer be created at all**"; `:724`, "They take away the one chance it had, because the cluster now has no way to choose" `[source: k8s-docs-ingress-depth-2026-08-24]`. Ch 19's "an ambiguous configuration, not a redundant one" states the cause and drops the consequence — on one of only four hazards the reader is told to drill. No research needed.
- **Two §2 rows lack the cross-bearing that would discharge their source obligation.** Confirmed against `shipped-sections.md`: **Ch 5 §7 is titled "Three Probes, Three Jobs"** and **Ch 10 §4 is titled "Frozen, Not Deprecated."** Both owners exist and are precisely on point; Ch 19's probe row and frozen/deprecated row point at neither.

### ⚑ C7. `the-lodestar.md` — BLOCKING, and Ch 1 has already sold it

Re-verified by directory listing: `Book-KCNA/` root holds nineteen chapter files, `README.md`, `sources/`, `.pipeline-state/`. **No `the-lodestar.md`.**

`ch01:452` names it to the reader — *"a single page holding the exam-critical facts, distinctions, and traps, distilled from the whole book. It's the last thing to read before the exam. Chapter 19 walks you through using it"* — and emits `*[cross-bearing: see Ch 19 §5 — using The Lodestar]*`. The B7 ledger corroborates at `:625` ("the artifact itself is named in Ch 1"). §5 cannot be cut, deferred, or reshaped around the absence.

I have created `concepts/the-lodestar.md` anyway, and deliberately: it records §5's six blocks as the **contract the artifact must satisfy**, which is the thing needed to write the file. It is labelled as describing an unwritten artifact so no stage mistakes it for a description of something on disk.

### ⚑ C8. B7 ledger obligations — checked row by row

All six Ch 19 rows (`term-ownership.md:620–625`) are discharged by the draft, with one erratum:

- **`:620` Cross-cutting theme**, `:621` Confusion pair, `:622` Discriminating question, `:624` The second pass — all defined in-chapter at the owning section. ✓
- **`:625` Using The Lodestar** — defined at §5; Ch 1's naming honored. ✓
- **`:623` Flagging and skipping — the ledger row is wrong.** It records "First appears **Ch 1** · gloss in one clause + pointer." I searched Ch 1 for every form of *flag* and *skip*: the hits are Soundings-skipping (`:444`), chapter-skipping (`:462`), a Practice option (`:491`), retrieval-skipping (`:525`, `:542`) and one use of *flags* meaning "calls out" (`:215`). **Ch 1 never glosses flagging as exam mechanics.** Its only pointer is `*[cross-bearing: see Ch 19 §3 — pacing and time discipline]*`. Ch 19 §3 is the first appearance.

  The useful consequence, which integration spotted and I confirm: **because there is no Ch 1 promise, §3's hedge contradicts nothing.** The chapter is free to say the console's navigation behavior is unpublished — which it does, naming four official pages verified silent — without breaking an earlier commitment.

- **The `volume` homonym pair Ch 19 ships is not the one the ledger sanctions.** `term-ownership.md:886` defines the pair as *Kubernetes volume vs **Docker volume***, with the ruling "Sense B is not used." Ch 19's homonym table instead pairs **Pod-spec volume (Ch 11 §1) vs PersistentVolume (Ch 11 §2)**. That is a *better* pair for this reader — both senses are owned, both are examinable, and the Docker sense is banned — but it is unsanctioned. **Add it to Canonical forms** rather than leaving one chapter to invent a homonym.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

Ch 19 introduces **no new exam vocabulary by design**, so this is the smallest glossary harvest in the commission. Three tiers.

### Tier 1 — the six B7-owned apparatus terms (`term-ownership.md:620–625`)

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **Cross-cutting theme** *(the chapter writes "thread")* | An idea Kubernetes applies repeatedly across subsystems, which the exam blueprint cuts across at right angles. "The book is nine patterns with instances, not eighteen chapters with facts." ⚑ Surface-form divergence — see ⚑ C3 | Chapter 19 §1 |
| **Confusion pair** | Two adjacent concepts a reader has filed as one thing. Points are lost to *collapse*: "when both appear as options the reader has no way to separate them and picks by feel" | Chapter 19 §2 |
| **Discriminating question** *(the chapter writes "discriminator")* | The one-line test that separates a confusion pair, given instead of two competing definitions. "Definitions side by side is what caused the collapse in the first place; a discriminator is a *procedure*, and procedures survive pressure." ⚑ Surface-form divergence — see ⚑ C3 | Chapter 19 §2 |
| **Flagging and skipping** | Marking a question for later return. ⚑ **Deliberately hedged:** the Linux Foundation publishes nothing about its multiple-choice console's navigation, confirmed absent on four official pages. The chapter tells the reader to establish it on the tutorial screen. ⚑ Ledger erratum — see ⚑ C8 | **Chapter 19 §3**, not Ch 1 |
| **The second pass** | The reserve period spent on marked questions, in the order marked. Governed by one rule: "Change an answer only when you can say why" | Chapter 19 §3 |
| **The Lodestar** | "This book's one-page reference, living at the repository root: the concentrated form of everything worth having in front of you in the hour before you sit down, and nothing else." "A **distillation, not a summary**" — no chapter recaps, no explanations, no context. ⚑ **The artifact does not exist** — see ⚑ C7 | Chapter 19 §5; named Chapter 1 |

### Tier 2 — carried glossary debts, neither created by Ch 19

| Term | Status | First appearance |
|---|---|---|
| **waypoint proxy** | **9 occurrences in shipped Ch 17**, 1 here inside a quotation; **no ledger row exists** — I searched `term-ownership.md` and there is none. Ch 17 §5's sourced definition is available verbatim and is used below. *(Integration reported 11 occurrences; measured, it is 9.)* | Chapter 17 §5 |
| **CloudEvents** | Queued at the Ch 17 gate, still open. ⚠ **Cannot be given an inherited definition: no chapter defines it.** All 6 shipped occurrences use it attributively ("a CloudEvents-over-HTTP asynchronous routing layer"). Rule 5 forbids paraphrase, so the entry records the gap rather than inventing a definition | Chapter 17 §6 |

### Tier 3 — a sanctioned label variant, not a new term

**`absent-component pattern`** — the shorthand label for the sentence *An object without its component does nothing*. Established in shipped Ch 3, 10, 11 and 17; Ch 19 uses it four times. The Canonical-forms row currently sanctions only the sentence. Add the label as a variant so no later linter reads it as drift.

---

## Concept shards at `Book-KCNA/knowledge-base/concepts/{slug}.md`

**Five created, twenty amended by append, two deliberately not created (⚑ C4).**

The append rule I applied, stated so it is not re-litigated: a synthesis chapter appends to a shard only when it adds a **discriminator, a thread membership, or a fidelity correction** — something the shard does not already have. Restating a definition the shard already carries is duplication, and Ch 19's whole premise is that it contains nothing new.

### Created

| Slug | § | Note |
|---|---|---|
| `cross-cutting-themes.md` | §1 | ★ the nine threads with their verified chapter paths; carries the ⚑ C3 surface-form ruling and the ⚑ C4 count dispute |
| `confusion-pair-matrix.md` | §2 | the catalogue: 23 discriminator rows across four domains, plus the 13 homonyms and the four hazards |
| `discriminating-question.md` | §2 | ★ the method claim — why a procedure beats two definitions. Separate from the catalogue per the ledger's two rows (⚑ C4) |
| `exam-pacing.md` | §3 | ★ the 60/40 rule, stated so it survives an unknown question count; carries the unpublished-console hedge |
| `the-lodestar.md` | §5 | ⚑ **describes an artifact that does not exist.** Written as the contract for building it (⚑ C7) |

### Not created — ⚑ C4

`absent-component-pattern` (exists, ch-03) · `domain-weight-allocation` (folds into `domain-weights-44-28-16-12.md`)

### Amended by append (20)

**Thread shards (9).** `control-loop.md` · `namespaced-vs-cluster-scoped.md` ⚑ · `absent-component-pattern.md` · `declarative-configuration.md` · `label-selector.md` · `pluggable-interface-pattern.md` ⚑ · `serviceaccounts-and-identity.md` ⚑ · `resource-request.md` · `additive-never-deny.md`

**Discriminator and fidelity shards (9).** `pod-phase.md` ⚑⚑ *(the "or restarting" repair)* · `probe.md` ⚑ *(missing cross-bearing)* · `ingress-freeze.md` ⚑⚑ *(the softened hazard)* · `access-modes.md` · `pv-phases.md` · `storageclass-and-provisioning.md` · `helm-rollback-versus-rollout-undo.md` · `restart-policy.md` ⚑⚑ *(the untaught clause)* · `version-skew.md`

**Exam-apparatus shards (2).** `domain-weights-44-28-16-12.md` ⚑ *(absorbs the declined slug)* · `blueprint-change-2025-11-24.md`

**⚑ DO NOT APPEND:** `pluggable-interfaces.md` · `cluster-scoped-resource.md` · `serviceaccount.md`. All three are the wrong half of a duplicate pair (⚑ C5). Merge at the replay.

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Pricing your own chapter honestly** | "Here is what this chapter is honestly worth, stated plainly so you can decide how much time to give it: **it contains nothing new.** Every fact in it was taught somewhere in Chapters 2 through 18. Its entire value is the second pass… Recognizing that 'ReadWriteOnce' is a term you have met is worth zero points. Being able to say what it constrains, and what its neighbor constrains, with ninety seconds on the clock, is worth all of them." | **Strong candidate.** A review chapter that opens by telling the reader it adds nothing, then earns the time anyway by naming the exact conversion it performs. The catalog has no exemplar of a chapter arguing for its own necessity from a position of weakness. |
| **A rubric that changes what it measures** | "**Readiness tiers — this rubric reads differently from every other chapter's.** You are not choosing a reading pace. You are estimating a date. … **0–2 — four or more weeks, and not a re-read.** Rereading the book front to back is the least efficient thing you could do with four weeks." | **Strong candidate.** The Soundings apparatus repurposed at the book's end, with the change announced rather than smuggled. Skill Part 11's metacognitive instrument turned into a scheduling instrument. |
| **The register carrying explanatory load** | "A coastline surveyed on a north–south run and the same coastline surveyed east–west produce two charts that do not look much alike, and a navigator wants both." | **Strong candidate.** Four lines of maritime register doing the entire justification for why a synthesis chapter exists. Companion to Ch 18's cross-bearing passage and Ch 17's "altitude is not a metaphor for importance." |
| **Naming a failure mode before the reader meets it** | "Around day four, you will probably have a bad session… the conclusion that will arrive uninvited is that you have been fooling yourself and you are not ready. This is common enough to be worth naming in advance, and it is worth much less as a signal than it feels like. What is usually happening is that you have moved from recognition practice to retrieval practice, and retrieval is harder. **Recognition was always the easier task and it was always flattering you.**" | **Strong candidate.** Skill Part 10B's desirable-difficulties principle delivered as reassurance rather than instruction, in a Logbook Entry. Subject dignity executed cleanly — the wry beat lands on the practitioner's self-deception, never on their competence. |
| **Refusing a frequency claim and arguing anyway** | "Here is the argument for spending an hour there, stated as arithmetic rather than as a claim about how often it is tested. … What makes it worth the hour is not its share but its *shape*: the material is finite and bounded. … An hour covers a large fraction of the whole competency." | **Strong candidate.** Guardrail 8 executed as rhetoric instead of omission. Most guides would assert "this is heavily tested"; this declines to, states why it declines, and then produces a *stronger* argument from bounded surface area. Best single instance of Part 14 in the commission. |
| **Degrading gracefully in the face of missing evidence** | "The Linux Foundation does not publish how its multiple-choice exam console behaves… That silence is not an oversight in this book's research; it is confirmed absent on four separate official pages… So establish it yourself, on the tutorial screen, before the clock matters. … Either way the failure mode the rule guards against is identical." | **Strong candidate.** Guardrail 4 at section scale: names the uncertainty, shows the work behind it, then restructures the advice so it is executable under either branch. The alternative — a memorized procedure that turns out to be unavailable — is explicitly reasoned about. |
| **Closing by naming what the reader is carrying** | "You are not carrying nine hundred facts, and you were never going to. You are carrying nine patterns, a set of discriminators, four weights, and one pacing rule — **a load small enough to hand up on deck in the dark**, which is the entire reason this chapter re-cut the book instead of summarizing it." | **Moderate to strong.** Safe Harbor stating the chapter's method as its result. Held at moderate only because the image depends on the register being already established by eighteen chapters. |
| **Dead Reckoning as a triage instruction** | "> **Dead Reckoning:** This is a review chapter. Sections 1 and 2 re-present taught material in a new organization. Sections 3 through 6 are exam strategy and study scheduling, not technical content. There are two ★ Fixed Points and both restate things you already learned. **If you are short on time, §2 is the section that moves your score.**" | **Moderate.** A Dead Reckoning block that tells a hurried reader which section to skip to — including which of the chapter's own Fixed Points are redundant. Useful precedent for any synthesis or capstone chapter. |

---

## Objective coverage log

Ch 19 is a synthesis chapter. `domain_weight_pct: 0`, `exam_domain: "All four domains — synthesis, no new objectives."` **It first-covers nothing.** All thirteen competencies are revisited at review depth.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.1 – D1.4 | Chapters 2–8 | review | 2026-08-31 |
| D2.1 – D2.4 | Chapters 9–13 | review | 2026-08-31 |
| D3.1 – D3.2 | Chapters 14–16 | review | 2026-08-31 |
| D4.1 – D4.3 | Chapters 17–18 | review | 2026-08-31 |

**The domain→chapter mapping is editorial and the chapter says so.** §4's Dead Reckoning separates the published weights (44/28/16/12, `[source: cncf-curriculum-kcna-readme-2026-08-31]`) from the chapter grouping, which is "how *this book* laid the material out, not something CNCF publishes." That distinction should survive into any reconciliation pass.

**Frontmatter to write at materialisation:** `chapter: 19` · `chapter_type: "synthesis"` · `title: "Bearings Before Landfall"` *(pending the ⚑ C9 retitle decision)* · `domain_weight_pct: 0` · `objectives: []` with all thirteen as review.

---

## Retrieval-practice ledger

Retrieval density is **100% by construction** — every graded item in a synthesis chapter is cross-chapter. Recorded for completeness, not as a compliance measurement, since skill Part 10's 20–25% band does not apply to a chapter whose entire function is retrieval.

**Five tagged checkpoint items**, all verified against `section-skeleton.md`:

| Tested topic | Original chapter | Retested in |
|---|---|---|
| absent-component pattern (CRD with no operator) | ch 3 §4 (coined) · ch 10 §3 (named) · ch 6 §8 · ch 13 §7 · ch 17 §7 | ch 19 Bearings 1 Q1 **[tagged]** |
| RBAC binding scope derived from namespacing | ch 4 §3 · ch 12 §3 | ch 19 Bearings 1 Q2 **[tagged]** |
| `Pending` means no container, so no logs | ch 5 §5 · ch 7 §2 · ch 13 §2 | ch 19 Bearings 1 Q3 **[tagged]** |
| Ingress frozen, not deprecated | ch 10 §4 | ch 19 Bearings 2 Q4 **[tagged]** |
| revision / rollback homonym | ch 6 §5 · ch 14 §3 | ch 19 Bearings 2 Q5 **[tagged]** |

**Ten Practice items, each with a verified chapter attribution:**

| # | Tested topic | Original chapters |
|---|---|---|
| 1 | `Pending` triage order; requests as scheduler filter input | ch 5 · 7 · 13 |
| 2 | NetworkPolicy inert on a non-implementing CNI | ch 10 · 9 |
| 3 | version skew — three numbers, three axes | ch 8 · 13 |
| 4 | CNCF TOC vs Governing Board | ch 1 · 17 §2 |
| 5 | RBAC additive; no precedence because no deny | ch 4 · 12 |
| 6 | readiness removes from endpoints, does not restart | ch 5 · 9 |
| 7 | `helm rollback` scope vs `rollout undo` | ch 6 · 14 |
| 8 | PV `Released` ≠ `Available` under `Retain` | ch 11 · 13 |
| 9 | Working Group: time-bounded, crosses SIG lines | ch 17 §8 · 2 / 9 / 11 |
| 10 | GitOps pull model as an identity argument | ch 5 · 12 · 15 |

**Distinct chapters drawn on: sixteen of eighteen.** Only Ch 1 and Ch 3 appear solely as supporting attributions rather than as a graded item's primary target — appropriate, since Ch 1 is orientation and Ch 3's control loop is tested through its instances.

**⚑ The B3 retrieval architecture that was supposed to specify this chapter is still an 18-line permissions-failure message.** See ⚑ I3. Ch 19 was built by exactly the audit B3 never produced, and the density figures above are therefore measured, not planned against a spec.

---

## Infrastructure flags — the knowledge base itself

**⚑ I0 — CRITICAL, still live, scope still incomplete.** Re-verified: `k8s-docs-logging-architecture-2026-08-31.md` is still **24 lines**, still ends at *"To fetch the logs, use the `kubectl logs` command, as follows:"*, and its frontmatter still claims to carry facts it does not. **Ch 19's own corpus is clean** — I measured all seventeen load-bearing `2026-08-31` captures (LF exam pages, version skew, autoscaling, CNCF charter and TAGs, SIG list, SRE book, Pushgateway, Istio ambient, Helm rollback, curriculum README): 16–112 lines, none showing the signature. `helm-rollback-cli-2026-08-31.md` is only 16 lines but is a complete CLI reference page ending cleanly, not a truncation. **The chapters 08–12 and 14–15 sweep Ch 18 requested remains outstanding** and I did not perform it — line count alone is not the signature and the check requires reading tails, which is a research-stage job.

**⚑ I1 — HIGH, unchanged, now nineteen chapters expensive.** Re-enumerated. `ch-01` emits **WRITE** for all three registers (correct — it creates them). `ch-03`, `ch-10` and `ch-11` also emit **WRITE**, which is destructive on replay. `ch-06` emits **no `glossary.md` block at all** — only `objective-coverage.md` and `retrieval-log.md`. Chapter 19 adds only APPENDs. **Convert the three WRITE blocks to APPENDs before any replay.**

**⚑ I2 — MEDIUM → HIGH, scope revised upward. See ⚑ C5.** Three duplicate pairs, not one. Chapter 19 appends to one side of each and declines the other three slugs. Merge all three at the replay.

**⚑ I3 — MEDIUM → BLOCKING, and the deadline has passed.** `book-outline/retrieval-architecture.md` is **18 lines**, re-measured this run: a permissions-failure message plus the stage's own summary. Ch 18 flagged it as "now blocking Ch 19 directly" and asked for a re-run "before Ch 19 drafts." **Ch 19 drafted anyway.** The chapter is sound — its retrieval load is measured above and is heavier than any spec would have asked for — but Ch 20's mock exam is the last artifact B3 governs, and it is the one where a missing retrieval architecture actually costs something. **Re-run before Ch 20 drafts.**

**⚑ I6 — HIGH, unchanged.** No `statefulset.md` exists. `statefulset-storage.md` (ch-11) is the only StatefulSet shard in the tree, and it covers `volumeClaimTemplates`, not ordinal identity. **Ch 19 §2's Deployment-vs-StatefulSet row grades on identity** ("Does replica 0 need to *be* replica 0?"), which is Ch 6 §6 material with no shard. Third consecutive chapter to flag it. **Create from shipped Ch 6 §6 at the replay.**

**⚑ I7 — HIGH, unchanged.** `ch-16/kb-manifest.md` documents 21 new shards and 16 appends and emits **exactly three blocks** — re-counted this run. Ch 16's entire concept layer is unwritten. *(For contrast, verified this run: `ch-18` documents 25 + 16 + 3 and emits **44** blocks. Ch 18 is complete; Ch 16 is the outlier.)*

**⚑ I8 — LOW, unchanged.** `ch-15/kb-manifest.md:2605` still reads `` === APPEND C:\dev\lodestar\cert``` ``, immediately followed by the correct duplicate at `:2606`. A naive parser fails or writes a garbage path. **Delete line 2605.**

**⚑ I10 — LOW, unchanged.** `k8s-docs-logging-architecture-2026-08-23.md` still carries `objectives_covered: ["D4 Observability", "D2 Troubleshooting"]` in the retired blueprint's vocabulary. Retag to `["D4.1", "D2.3"]`.

**⚑ I11 — LOW, new.** The corpus figures circulating in this chapter's own paperwork are both wrong: the draft says 31 files, integration says 199, and `sources/` holds **303**. Neither error is load-bearing, but the draft's figure is what its false research-gap block rests on (⚑ C0), so it is worth correcting where it appears rather than leaving a plausible number in a comment.

---

## Recommended actions, ranked

1. **Retrofit shipped Ch 1's provenance passage (⚑ C2).** Highest value in the gate: `ch01:341` is a *graded answer key* teaching the reader something false. Adopt Ch 19 §3's ⚓ framing — the lesson changes from *whether* the authority publishes to *where*. While in `:215`, retarget the forbidden `Ch 20 §1` pointer to address Ch 20 by name, and drop "commonly-reported format." **This also unblocks Ch 20's Instructions and Scoring Rubric**, whose skeleton instructions are now stale.
2. **Write `the-lodestar.md` (⚑ C7).** Ch 1 has promised it by name. `concepts/the-lodestar.md` below records the contract; reconcile §5's six block names against the file once it exists and restore §5's opening to present tense.
3. **Cut one sentence from the `restartPolicy` row (⚑ C1)** — the Deployment clause only. The Job clause is taught and sourced; leave it.
4. **Apply the three fidelity repairs (⚑ C6).** Insert "or restarting" three times; adopt Ch 10's actual second-default consequence; add the two missing cross-bearings (Ch 5 §7, Ch 10 §4). All are edits against material already on disk.
5. **Delete the §2 research-gap block (⚑ C0)** once the cross-bearings are in. Six research passes are not needed; all six sources are cached.
6. **Decide the chapter count (⚑ C3 / integration 4).** Three-way disagreement — skeleton "Twenty," `ch18:1721` "twenty," Ch 19 §1 "Eighteen." Two of the three must move together. Cheapest: keep Ch 19, edit the skeleton, change one word in Ch 18.
7. **Decide the title (integration 1).** "Landfall" is a retired marker name, exposed only in the H1. "Two Landmarks" pays off both the epigraph and §2's opening line.
8. **Ratify the headwords (⚑ C3)** — thread / cross-cutting theme, discriminator / discriminating question. The KB slugs follow the ledger regardless; only the reader-facing word is open, and it costs one word in `ch18:1721`.
9. **Ledger errata to enter at the glossary build:** correct `:623` Flagging and skipping to first-appear Ch 19 §3 (⚑ C8) · add the Pod-spec-volume / PersistentVolume homonym to Canonical forms · add `absent-component pattern` as a sanctioned label variant · create rows for `waypoint proxy` and `CloudEvents`.
10. **Infrastructure, before any replay:** ⚑ I3 (re-run B3 **before Ch 20**) · ⚑ I7 (re-emit Ch 16's shards) · ⚑ I8 (delete `ch-15:2605`) · ⚑ I1 (WRITE→APPEND ×3, plus Ch 6's missing glossary block) · ⚑ I2 (merge **three** duplicate pairs, ⚑ C5) · ⚑ I6 (create `statefulset.md`) · ⚑ I0 (sweep chapters 08–12, 14–15) · ⚑ I10 (retag).
11. **Still genuinely open, correctly:** the retired-blueprint weights (`old-versions/KCNA_Curriculum old.pdf`), which §4's AUTHOR-REVIEW correctly declines to draft from memory and which Ch 20 will want too; and the LF multiple-choice console's navigation behavior, which §3 correctly degrades around rather than guessing at.

---

Below are the write intentions: three registers, then the twenty shard appends, then the five new shards.

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

# Chapter 19 additions (2026-08-31)

Chapter 19 is a synthesis chapter and introduces NO new exam vocabulary by design.
The B7 ledger states it outright (term-ownership.md:616): "Ch 19 owns no new
technical vocabulary. It owns the reader-facing apparatus of the final review."

Six apparatus terms follow, plus two carried debts neither created nor owned here.

## A

**Absent-component pattern** — The shorthand label for the pattern whose canonical
sentence is *An object without its component does nothing*. ⚑ REGISTER ERRATUM: the
Canonical-forms row currently sanctions only the sentence, but the label is
established in shipped Ch 3, Ch 10, Ch 11 and Ch 17 and is used four times in
Ch 19. Add it as a sanctioned variant so no later linter reads it as drift.
(Sentence coined Chapter 3 §4; named as a pattern Chapter 10 §3)

## C

**CloudEvents** — ⚠ NO DEFINITION EXISTS IN THIS BOOK. All six shipped occurrences
(Chapter 17 §6) use the term attributively, inside or adjacent to a quotation:
Knative Eventing is "a CloudEvents-over-HTTP asynchronous routing layer"
[source: knative-overview-2026-08-23]. Chapter 19 §2's Domain 4 table adds a
seventh use, also inside that quotation.

Rule 5 forbids paraphrase, and there is nothing here to inherit. This entry
therefore records the GAP rather than inventing a definition. Two ways to close it,
author's pick: (a) a one-clause gloss at Ch 17 §6's first use, which the acronym
register's own standard would require of any term reaching graded text; or (b) an
author-supplied definition entered here directly. Queued at the Chapter 17 gate and
re-recorded at Chapter 18; still open. (Chapter 17 §6)

**Confusion pair** — Two adjacent concepts a reader has filed as one thing. The
failure they produce is *collapse*: "when both appear as options the reader has no
way to separate them and picks by feel." Chapter 19 §2 catalogues 23 pairs across
the four domains, plus 13 surface-form homonyms and four hazards where the
intuitive reading is the wrong one. See **discriminating question**. (Chapter 19 §2)

**Cross-cutting theme** — An idea Kubernetes applies repeatedly across subsystems,
which the exam blueprint cuts across at right angles. Chapter 19 §1 names nine and
traces each through the chapters that build it. The reader-facing payoff: "The book
is nine patterns with instances, not eighteen chapters with facts."

⚑ SURFACE-FORM DIVERGENCE. The ledger headword (term-ownership.md:620) and shipped
Chapter 18's handoff (ch18:1721, "Nine cross-cutting themes traced through twenty
chapters") both use "cross-cutting theme." Chapter 19 uses "thread" everywhere
except one line in What You'll Learn. The KB slug is cross-cutting-themes.md, which
follows the ledger. Ratify one form; the concept shard supports either.
(Chapter 19 §1)

## D

**Discriminating question** *(the chapter writes "discriminator")* — The one-line
test that separates a confusion pair, supplied in place of two competing
definitions. The method claim, stated in the chapter: "Definitions side by side is
what caused the collapse in the first place; a discriminator is a *procedure*, and
procedures survive pressure."

⚑ SURFACE-FORM DIVERGENCE, same shape as **cross-cutting theme**. The ledger
(term-ownership.md:622) says "discriminating question"; ch18:1721 says "a question
that discriminates between them"; Chapter 19 says "discriminator."
(Chapter 19 §2)

## F

**Flagging and skipping** — Marking a question during a timed exam for return in the
reserve period.

⚠ DELIBERATELY HEDGED, AND THE HEDGE IS CORRECT. The Linux Foundation does not
publish how its multiple-choice exam console behaves — whether a question can be
skipped, marked, navigated back to, or an answer changed. Chapter 19 §3 confirms
that silence on four separate official pages
[source: lf-mc-exam-important-instructions-2026-08-31]
[source: lf-mc-exam-faq-2026-08-31]
[source: lf-exam-rules-and-policies-2026-08-31]
[source: lf-handbook2-taking-the-exam-2026-08-31]
and instructs the reader to establish it on the tutorial screen before the clock
matters. The pacing rule is written to work under either branch.

⚑ LEDGER ERRATUM. term-ownership.md:623 records "First appears Ch 1 · gloss in one
clause + pointer." Chapter 1 does not gloss it. Every "skip" in Chapter 1 concerns
skipping Soundings (:444), chapters (:462), or retrieval questions (:525, :542);
its only relevant pointer is *[cross-bearing: see Ch 19 §3 — pacing and time
discipline]* at :215. Chapter 19 §3 is the first appearance. Useful consequence:
because there is no Ch 1 promise, §3's hedge contradicts nothing.
(Chapter 19 §3)

## L

**The Lodestar (`the-lodestar.md`)** — "This book's one-page reference, living at the
repository root: the concentrated form of everything worth having in front of you in
the hour before you sit down, and nothing else." A "distillation, not a summary" —
no chapter recaps, no explanations, no worked examples, no context; every line
assumes the chapter it came from has been read.

Its diagnostic property, stated in the chapter: "if you cannot reconstruct a chapter
from its Lodestar lines, you have not found a defect in the Lodestar. You have found
a chapter you need to go back to."

⚑ BLOCKING: THE ARTIFACT DOES NOT EXIST. Verified this run — Book-KCNA/ holds no
the-lodestar.md. Chapter 1 :452 already promises it to the reader by name and emits
*[cross-bearing: see Ch 19 §5 — using The Lodestar]*, so §5 cannot be cut or
deferred. The six block names in §5 are provisional and become factual claims about
a shipped artifact the moment the file is written. See concepts/the-lodestar.md for
the contract. (Chapter 19 §5; named Chapter 1)

## S

**The second pass** — The reserve period of a timed exam, spent on marked questions
in the order they were marked. Two things have changed since first sight: later
questions sometimes disambiguate earlier ones, and first-pass momentum has lifted,
so the full discriminator procedure is affordable. Governed by one rule: "Change an
answer only when you can say why." A statable reason is evidence; "it feels wrong
now" is fatigue wearing the costume of insight. (Chapter 19 §3)

## W

**Waypoint proxy** — In Istio's ambient mode, the optional per-namespace Layer 7
proxy. It "is a deployment of the Envoy proxy; the same engine that Istio uses for
its sidecar data plane mode" [source: istio-ambient-mode-2026-08-31]. The
discrimination it supports: ambient removes *sidecars*, not Envoy. The per-node L4
proxy is ztunnel; the per-namespace L7 waypoint is Envoy.

⚑ REGISTER GAP. Nine occurrences in shipped Chapter 17, one in Chapter 19 §2's
Domain 4 table, and NO ROW EXISTS in term-ownership.md — I searched. Needs both a
register row (owner: Ch 17 §5) and this entry. Carried forward from the Chapter 17
gate; not created by Chapter 19. (Chapter 17 §5)

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

## Chapter 19 (2026-08-31)

Chapter 19 is a SYNTHESIS chapter. It first-covers nothing. All thirteen
competencies are revisited at review depth.

  chapter_type: "synthesis"
  domain_weight_pct: 0
  exam_domain: "All four domains — synthesis, no new objectives"

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.1 - D1.4 | Chapters 2-8 | review | 2026-08-31 |
| D2.1 - D2.4 | Chapters 9-13 | review | 2026-08-31 |
| D3.1 - D3.2 | Chapters 14-16 | review | 2026-08-31 |
| D4.1 - D4.3 | Chapters 17-18 | review | 2026-08-31 |

### The domain-to-chapter mapping is editorial, and the chapter says so

§4's Dead Reckoning separates two things that later stages have conflated before:

- PUBLISHED: the domain weights 44 / 28 / 16 / 12
  [source: cncf-curriculum-kcna-readme-2026-08-31], which agree exactly with the
  Linux Foundation exam page and the curriculum PDF.
- EDITORIAL: which chapters carry which domain. D1 = Ch 2-8, D2 = Ch 9-13,
  D3 = Ch 14-16, D4 = Ch 17-18. This is "how *this book* laid the material out,
  not something CNCF publishes."

Preserve that distinction in any reconciliation pass. A reconciler that treats the
chapter grouping as published will produce a drift report against a boundary CNCF
never drew.

### Frontmatter to write at materialisation

  chapter: 19
  chapter_type: "synthesis"
  title: "Bearings Before Landfall"     # pending the retitle decision, see below
  domain_weight_pct: 0
  objectives: []                        # all thirteen as review, none first-covered

⚑ The title reuses "Landfall," retired as a branded-marker name
[LOCKED 2026-04-20] with the note "any future 'Landfall' in drafts is drift."
Reader-facing exposure is the H1 alone; the body uses ☀️ Zenith correctly at §1.
The structural linter has no rule for retired marker NAMES, so no automated gate
sees this. Author decision. "Two Landmarks" pays off both the epigraph and §2's
opening line.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

## Chapter 19 (2026-08-31)

Retrieval density is 100% BY CONSTRUCTION. Every graded item in this chapter is
cross-chapter, which is what a synthesis chapter is. Skill Part 10's 20-25% band
does not apply and no compliance measurement is recorded against it.

Recorded here so Chapter 20's mock-exam weighting can see which chapters have
already been retrieval-tested at the book's end, and how recently.

### Tagged checkpoint items (5 of 5 - every Bearings question)

| Tested topic | Original chapter | Retested in |
|---|---|---|
| absent-component pattern (CRD with no operator) | ch 3 §4 coined · ch 10 §3 named · ch 6 §8 · ch 13 §7 · ch 17 §7 | ch 19 Bearings 1 Q1 |
| RBAC binding scope derived from namespacing | ch 4 §3 · ch 12 §3 | ch 19 Bearings 1 Q2 |
| Pending means no container, so no logs | ch 5 §5 · ch 7 §2 · ch 13 §2 | ch 19 Bearings 1 Q3 |
| Ingress frozen, not deprecated | ch 10 §4 | ch 19 Bearings 2 Q4 |
| revision / rollback homonym | ch 6 §5 · ch 14 §3 | ch 19 Bearings 2 Q5 |

All five tags verified against section-skeleton.md. Ch 10 §4 is titled "Frozen, Not
Deprecated" and Ch 5 §5 owns phase-versus-container-state, so both point at the
owning section rather than the chapter.

### Practice items (10 of 10 - all cross-domain)

| # | Tested topic | Original chapters |
|---|---|---|
| 1 | Pending triage order; requests as scheduler filter input | ch 5 · 7 · 13 |
| 2 | NetworkPolicy inert on a non-implementing CNI | ch 10 · 9 |
| 3 | version skew - three numbers on three axes | ch 8 · 13 |
| 4 | CNCF TOC vs Governing Board | ch 1 · 17 §2 |
| 5 | RBAC additive; no precedence because no deny | ch 4 · 12 |
| 6 | readiness removes from endpoints, does not restart | ch 5 · 9 |
| 7 | helm rollback scope vs rollout undo | ch 6 · 14 |
| 8 | PV Released is not Available under Retain | ch 11 · 13 |
| 9 | Working Group: time bounded, crosses SIG lines | ch 17 §8 · 2 / 9 / 11 |
| 10 | GitOps pull model as an identity argument | ch 5 · 12 · 15 |

### Coverage across the book

Sixteen of eighteen content chapters are drawn on as a graded item's primary
target. Ch 1 and Ch 3 appear only as supporting attributions - appropriate, since
Ch 1 is orientation and Ch 3's control loop is tested through its instances rather
than directly.

Distractor construction is unusually disciplined and worth recording, because
Ch 20 should reuse the technique:

- Q3's three wrong options are each off by exactly one increment on a DIFFERENT
  axis, so the discrimination tested is which axis the rule applies to, not
  arithmetic. The answer key says so explicitly.
- Q6's option B has the endpoint effect RIGHT and then imports the restart from
  liveness. A partial collapse is harder to catch than a total one, which is why
  the item exists.
- Q8's option D inverts one of the four hazards rather than contradicting it.

### The four threads that carry the graded load

Recorded because it is the most useful single fact for weighting Ch 20:

  thread 3 (absent component) - Bearings Q1, Practice Q2
  thread 9 (additive, no deny) - Practice Q2 distractor, Practice Q5
  thread 2 (namespaced vs cluster-scoped) - Bearings Q2, Practice Q5
  thread 7 (identity) - Practice Q10

Threads 1, 4, 5 and 6 are taught in §1 and NOT graded anywhere in this chapter.
If Ch 20 wants them, it must build them itself.

### ⚑ B3 never specified this chapter

book-outline/retrieval-architecture.md is still 18 lines of permissions-failure
message plus the stage's own summary - re-measured this run. Chapter 18 flagged
this as "now blocking Ch 19 directly" and asked for a re-run before Ch 19 drafted.
Ch 19 drafted anyway.

The chapter is sound; its retrieval load is measured above and is heavier than any
spec would have required. But Ch 20's mock exam is the last artifact B3 governs and
the one where a missing retrieval architecture actually costs something.

RE-RUN B3 BEFORE CHAPTER 20 DRAFTS.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

## Chapter 19 update (2026-08-31) — thread 1, and the retrieval handle

Ch 19 §1 names this the single most reused idea in the system and traces it as
thread 1. Adds no mechanism; adds a compression and a path.

THE COMPRESSION (Ch 19 §1, 🪢 Mnemonic):

  Desired, observed, act.

  "If you can say those three words about any Kubernetes component, you have found
  its control loop."

THE VERIFIED PATH, six nodes:

  Ch 3 §6  defines it
  Ch 4 §1  supplies the artifact the loop reads — the declared object
  Ch 6 §2  instantiates it in a watchable controller, .spec.replicas as desired state
  Ch 11 §2 applies it to storage — a claim is a desired state, binding is reconciliation
  Ch 15 §7 points the loop at a Git repository instead of etcd
  Ch 17 §4 collects it as the thing every extension point extends

WHY Ch 15 §7 IS THE PAYOFF, stated so a later stage does not re-explain it:
nothing changes except WHERE THE DESIRED STATE LIVES. The loop is identical.
Substituting Git for etcd is not a new mechanism, which is precisely why the GitOps
section could re-present Chapter 3's figure and expect it to land.

See [[control-loop-pointed-at-a-repository]], [[cross-cutting-themes]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/namespaced-vs-cluster-scoped.md ===

## Chapter 19 update (2026-08-31) — thread 2, and the derivation that replaces a memorized table

⚑⚑ SLUG RULING. cluster-scoped-resource.md (ch-04) and this file (ch-08) are one
concept under two slugs — the same fault as pluggable-interface-pattern /
pluggable-interfaces, previously unflagged. Chapter 19 appends HERE ONLY, because
this is the discrimination shard and the discrimination is what §1 uses. Do not
append the same content to cluster-scoped-resource.md. Merge at the replay.
See the manifest's ⚑ C5.

THE LOAD THIS DISTINCTION CARRIES. Ch 19 §1 thread 2 shows one Chapter 4
distinction deriving the entire RBAC four-way binding matrix, three chapters later,
in material that looks unrelated on the surface:

  Ch 4 §3  defines it
  Ch 8 §3  builds ResourceQuota (a namespace total) and LimitRange (a per-object
           default) on it
  Ch 12 §3 derives the binding matrix from it

THE DERIVATION RULE — two sentences that replace four memorized rows:

  1. A binding can never grant more scope than it has itself.
  2. A namespaced Role can never escape its namespace.

Both follow from Chapter 4. Everything in the matrix falls out:

  RoleBinding + Role                 -> the Role's permissions, in that namespace
  RoleBinding + ClusterRole          -> the ClusterRole's permissions, but only in
                                        the binding's namespace
  ClusterRoleBinding + Role          -> NOT VALID
  ClusterRoleBinding + ClusterRole   -> cluster-wide

THE PRACTICE PATTERN the derivation exposes (Ch 19 Bearings 1 Q2 answer key):
define a ClusterRole once, bind it per-namespace with RoleBindings, and you get
consistent permission sets without duplicating Role definitions.

THE FAILURE MODE the checkpoint tests for: answering "cluster-wide" inverts the
rule. The scope of the GRANT is set by the BINDING, not by the role.

See [[rbac]], [[additive-never-deny]], [[cross-cutting-themes]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

## Chapter 19 update (2026-08-31) — thread 3, the inverse, and two symptom shapes

Ch 19 §1 calls this "the pattern the book has hammered hardest, and the one most
likely to be worth points on the day," and makes it a ★ Fixed Point. The canonical
sentence is unchanged and byte-identical across all shipped uses:

  An object without its component does nothing.

THE FULL PATH, verified against the skeleton — six nodes, one rule doing the work
of five separate gotchas:

  Ch 3 §4  coins the phrase, at addons, because "optional component" is where the
           reader first learns parts of the cluster are not automatically present
  Ch 10 §3 names it as a pattern, at the Ingress-object-vs-controller split
  Ch 11 §5 CSI drivers
  Ch 13 §7 kubectl top on a bare cluster
  Ch 17 §7 the VerticalPodAutoscaler
  Ch 18    the whole observability stack

TWO THINGS CHAPTER 19 ADDS.

1. THE INVERSE, which is less often taught (Ch 19 §1, 🪝 Snag): a component with no
   object also does nothing visible. An Ingress controller in a cluster with no
   Ingress resources is IDLE, NOT BROKEN. Question stems sometimes present the
   idle-controller case to see whether both directions have been internalised.

2. THE PATTERN FAILS AT DIFFERENT LAYERS, and the symptom shape differs (Ch 19 §2,
   Domain 4 HPA/VPA row):

   - With Ingress: the object is ACCEPTED and nothing happens. Silent no-op.
   - With VPA: the API REJECTS THE KIND OUTRIGHT, because without the add-on the
     CRD does not exist.

   Same pattern, two symptom shapes. A stem describing "cannot create the object"
   and a stem describing "created it, nothing happened" are both this pattern.

THE FIRST-QUESTION HEURISTIC: when a question describes an object that EXISTS and a
behavior that is NOT HAPPENING, reach for this before diagnosing the object.

⚑ REGISTER ERRATUM. The label "absent-component pattern" is used four times in
Ch 19 and is established in shipped Ch 3, 10, 11 and 17, but Canonical forms
sanctions only the sentence. Add the label as a variant.

See [[cross-cutting-themes]], [[pluggable-interface-pattern]], [[ingress-freeze]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/declarative-configuration.md ===

## Chapter 19 update (2026-08-31) — thread 4

Ch 19 §1 traces this as thread 4 and states the framing that makes GitOps follow
from it rather than be bolted onto it.

  Ch 4 §1  defines it
  Ch 6     a declared replica count meets a controller
  Ch 14    declarations packaged for distribution — charts and overlays
  Ch 15    the declaration placed in version control; the repository as truth

THE PAYOFF, stated so no later chapter re-argues it: "GitOps is not a new idea
bolted onto Kubernetes. It is what you get when you take Chapter 4 seriously and
ask where the declaration ought to live."

THE CLARIFICATION Ch 19 adds about imperative commands: kubectl scale and
kubectl create are conveniences that WRITE A DECLARATION ON YOUR BEHALF. They are
not a second, competing model.

See [[control-loop]], [[gitops]], [[cross-cutting-themes]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/label-selector.md ===

## Chapter 19 update (2026-08-31) — thread 5, and the exception that proves it

Ch 19 §1: "Kubernetes has almost no foreign keys. What it has instead is labels on
objects and selectors that match them, and nearly every relationship in the system
is expressed that way."

THE PATH, seven nodes:

  Ch 4 §5  defines labels and selectors
  Ch 6 §3  controller-to-Pod join, plus ownerReferences
  Ch 7 §3  node labels for nodeSelector and affinity
  Ch 9 §4  a Service's selector building EndpointSlice membership
  Ch 10 §6 podSelector and namespaceSelector for NetworkPolicy
  Ch 16 §4 the join FAILING from the application side — a selector matching nothing
           produces an empty EndpointSlice
  Ch 12 §3 the contrast

THE CONTRAST IS THE EXAMINABLE PART, and it is easy to miss:

  RBAC DOES NOT SELECT. RBAC NAMES.

A RoleBinding lists its subjects explicitly; it does not match them by label. The
asymmetry is deliberate and the reason is the thing to hold: permission granted by
label match would mean ANYONE WHO CAN SET A LABEL CAN ESCALATE PRIVILEGE.

That is exactly the "why is this one different" shape that makes a good question.

⚑ Ch 16 §4's membership in this thread was added at Ch 19's revision and is not in
the figure spec ch19-fig01-cross-domain-integration-map as originally written. The
spec's AUTHOR-REVIEW item 2 (Ch 16 rendering as an empty row) is closed by it.
Total marks in the grid are 41, not the 40 the spec records. Re-sync the spec.

See [[rbac]], [[cross-cutting-themes]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pluggable-interface-pattern.md ===

## Chapter 19 update (2026-08-31) — thread 6, and its interlock with thread 3

⚑ Appending HERE and not to pluggable-interfaces.md. ⚑ I2's merge-to-stub still
stands; Ch 19 is a synthesis chapter and appending to both halves of a split would
entrench it permanently.

Ch 19 §1 thread 6 collects the canonical four:

  CRI  — Container Runtime Interface — running containers      — Ch 2 §4
  CNI  — Container Network Interface — Pod networking          — Ch 9 §1
  CSI  — Container Storage Interface — providing storage       — Ch 11 §5
  CRDs and operators — extending the API itself                — Ch 6 §8

Ch 17 §4 collects all four and situates them alongside the wider extension surface:
API aggregation, admission webhooks, device plugins, scheduler plugins. The fourth
slot is named both ways in the wild ("API extensions"); Chapter 17 reconciled the
two and Chapter 19 inherits that reconciliation rather than re-opening it.

THE INTERLOCK, which is the thing Ch 19 adds:

  Every pluggable interface CREATES an object-without-component hazard, because
  "Kubernetes defines the interface" always implies "somebody else installs the
  implementation."

Thread 6 and thread 3 are therefore not independent. A stem about a pluggable
interface is very often an absent-component stem wearing different clothes.

A RELATED SURFACE-FORM RULE from Ch 19 §2: **plugin is never used bare in this
book.** It is always qualified — CNI plugin, scheduler plugin, admission plugin,
device plugin. An option that says "the plugin" without saying which is not telling
you enough to answer, and that is usually deliberate.

See [[absent-component-pattern]], [[one-pluggability-story]], [[cross-cutting-themes]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/serviceaccounts-and-identity.md ===

## Chapter 19 update (2026-08-31) — thread 7, and why the blast-radius argument is an identity argument

⚑⚑ SLUG RULING. serviceaccount.md (ch-05) and this file (ch-12) are one concept
under two slugs — a second, previously unflagged instance of the ⚑ I2 fault.
ch-15 appends to BOTH, which is how it went unnoticed. Chapter 19 appends HERE
ONLY, because this shard owns identity as a concept rather than the object. Merge
at the replay. See the manifest's ⚑ C5.

Ch 19 §1 thread 7: "Everything that talks to the API server has an identity, and in
this cluster non-human identity means ServiceAccount."

  Ch 5 §6  the ServiceAccount as the Pod's identity; the default account carries
           near-zero permissions
  Ch 12 §2 it becomes the subject RBAC binds to
  Ch 15 §4 the delivery agent — a Pod like any other, therefore with a
           ServiceAccount, needing exactly the permissions its syncing requires

THE POINT CHAPTER 19 ADDS, and the reason this thread matters more than it looks:

  The GitOps blast-radius argument in Chapter 15 depends ENTIRELY on this thread.
  A pull-based agent holds cluster credentials INSIDE the cluster; a push-based CI
  system holds them OUTSIDE. That is an IDENTITY argument, not a networking one.

Graded at Ch 19 Practice Q10, where three of the four distractors fail on identity
rather than on GitOps mechanics — including option C, "the agent needs no
ServiceAccount," which is wrong because EVERY Pod has one.

See [[rbac]], [[gitops]], [[cross-cutting-themes]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-request.md ===

## Chapter 19 update (2026-08-31) — thread 8, two numbers and five consequences

Ch 19 §1 thread 8 traces requests and limits through five subsystems. The value is
the count: a question can enter this thread AT ANY OF THE FIVE POINTS, so the
retrieval handle is the trace, not any one node.

  Ch 5 §8  defines requests, limits, and the QoS classes they produce
  Ch 7 §2  requests become the scheduler's FILTER INPUT — which is why an
           over-requested Pod sits in Pending
  Ch 13 §4 QoS class becomes the EVICTION ORDERING under node pressure
  Ch 17 §7 they become the thing the VerticalPodAutoscaler ADJUSTS
  Ch 18 §3 they become the DENOMINATOR for utilization

"Two numbers, five consequences. This is a thread worth being able to trace out
loud."

THE OTHER DIRECTION, from Ch 19 §2's Domain 4 table: node autoscaling is triggered
by Pods that "can't be scheduled on existing Nodes"
[source: k8s-docs-node-autoscaling-2026-08-31] — which is thread 8 arriving from
the cluster side rather than the workload side.

Graded at Ch 19 Practice Q1, where the correct triage compares REQUESTS to node
Allocatable, and the wrong answers reach for logs, top, or a kubelet restart.

See [[pod-phase]], [[cross-cutting-themes]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/additive-never-deny.md ===

## Chapter 19 update (2026-08-31) — thread 9, and the rule for "how do I stop this"

Ch 19 §1 thread 9. RBAC and NetworkPolicy were built by different SIGs for
different problems and share ONE semantic exactly:

  Both are purely additive. Neither has a deny rule.

  RBAC: permissions accumulate across every binding that names you. Nothing
        subtracts.
  NetworkPolicy: a Pod no policy selects is fully open; a Pod any policy selects is
        restricted to the UNION of what its policies allow; there is no rule that
        says "block this."

  Ch 10 §6 establishes it for NetworkPolicy
  Ch 12 §3 establishes it for RBAC
  Ch 12 §9 names them as one shared semantic

THE ACTIONABLE RULE Ch 19 adds (⚓ Worth Securing) — the form a question actually
takes is "how do I STOP something," and the answer is never a deny rule:

  RBAC          -> REMOVE THE GRANT
  NetworkPolicy -> SELECT THE POD with a policy that does not allow it
                   (restricts by SELECTION, not by denial)

"An option offering a deny verb is testing whether you have imported firewall
intuitions into a system that has none."

THE SECOND-ORDER CONSEQUENCE, from Ch 19 Practice Q5's answer key, which is the
sharpest statement of it in the book: RBAC HAS NO PRECEDENCE BECAUSE IT HAS NO
DENY. With nothing that subtracts, there is nothing for precedence to arbitrate.
A narrower binding does not limit a broader one, and there are no conflicts to
resolve. Q5's options B and C are both built on imagining a precedence rule.

See [[rbac]], [[network-policy]], [[cross-cutting-themes]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-phase.md ===

## Chapter 19 update (2026-08-31) — the discriminator, and ⚑ a fidelity repair

THE DISCRIMINATOR (Ch 19 §2, Domain 1, first row):

  "Lifecycle, or one container?"

  Phase describes the whole Pod's position in its lifecycle. State describes one
  container right now.

  THE TELL: a stem that says a Pod is Running and something is still broken is
  testing this. Running is a LIFECYCLE POSITION, NOT A HEALTH VERDICT.

Also one of the four ⚠ hazards where intuition is wrong, and the source of the
book's most-repeated instrument error: a Pending Pod has no containers, so
kubectl logs asks the kubelet on a node that does not exist for output that was
never produced. Read the phase, then describe for events. Graded at Ch 19
Bearings 1 Q3 and Practice Q1.

⚑⚑ FIDELITY REPAIR REQUIRED — Ch 19 STATES THIS DEFINITION LESS FULLY THAN Ch 5 DID

Shipped Ch 5 §5 (ch05:573) defines the phase as:

  "the Pod has been bound to a node, and all of the containers have been created.
   At least one container is still running, OR IS IN THE PROCESS OF STARTING OR
   RESTARTING."
   [source: k8s-docs-pod-lifecycle-2026-08-23]

and builds a ★ Fixed Point on the restarting case: a crash-looping Pod reports the
phase Running. Ch 5 then tells the reader outright that both Pending and Running
"are broader than their names suggest, and both of those breadths are tested."

Ch 19 says "at least one is running or starting" in ALL THREE places it states the
definition — the §2 Domain 1 row, the ⚠ Navigational Hazards block, and the Chapter
Summary. That technically EXCLUDES THE CRASHLOOPBACKOFF CASE, which is the hazard's
whole point.

Two-word insertion, three times. Restore "or restarting."

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/probe.md ===

## Chapter 19 update (2026-08-31) — three discriminators, and ⚑ a missing pointer

THE DISCRIMINATOR (Ch 19 §2, Domain 1):

  "Restart it, or stop sending traffic?"

  liveness fails  -> RESTARTS the container
  readiness fails -> REMOVES IT FROM SERVICE ENDPOINTS, no restart
  startup         -> SUSPENDS THE OTHER TWO until the app has finished booting

  THE TELLS: a slow-starting app being killed repeatedly is a STARTUP-probe
  question. Traffic reaching a not-yet-ready Pod is a READINESS question.

Graded at Ch 19 Practice Q6, whose option B is the finest discrimination in the
item set: it gets the ENDPOINT EFFECT RIGHT and then imports the RESTART from
liveness. A partial collapse is harder to catch than a total one.

⚑ MISSING CROSS-BEARING. Ch 19's probe row carries no pointer, and the owner is
exact: SHIPPED CH 5 §7, titled "Three Probes, Three Jobs." Under the book-level
ruling ratified at the Ch 18 gate, a cross-bearing to the owning section discharges
the [source:] obligation for a retrieved claim. Adding it retires this row from the
draft's §2 research-gap block at zero research cost.

See [[pod-phase]], [[service-types]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/ingress-freeze.md ===

## Chapter 19 update (2026-08-31) — the discriminator, and ⚑ a weakened hazard

THE DISCRIMINATOR (Ch 19 §2, Domain 2; graded at Bearings 2 Q4):

  "Frozen means no new features. Deprecated means an end date."

  FROZEN     = feature-complete and still supported; the API is stable, it keeps
               working, new development happens in Gateway API instead.
  DEPRECATED = scheduled for removal with a migration deadline.

  Ingress is FROZEN. An option saying it is deprecated or removed is wrong.

THE SECOND HALF, which Ch 19's checkpoint makes explicit and which is the part a
planning stem tests: BECAUSE Ingress is not deprecated, THERE IS NO UPGRADE AT
WHICH TRAFFIC BREAKS. Migrating to Gateway API is a choice made for its
capabilities — the role-oriented design and richer routing — not a deadline being
met. A reader who catches "deprecated" but not "traffic will break" has half the
item.

⚑⚑ FIDELITY REPAIR REQUIRED — the second-default-IngressClass hazard is softer in
Ch 19 than what Ch 10 taught

Ch 19 says two defaults is "an ambiguous configuration, not a redundant one."
Shipped Ch 10 gives the actual consequence, twice, sourced:

  ch10:720 — a second default "does not widen the net — it REMOVES it, and the
             Ingress CAN NO LONGER BE CREATED AT ALL"
  ch10:724 — "They take away the one chance it had, because the cluster now has no
             way to choose"
  [source: k8s-docs-ingress-depth-2026-08-24]

Ch 19 states the CAUSE and drops the CONSEQUENCE, on one of only four hazards the
reader is explicitly told to drill. Ch 10 has the sourced sentence; no research is
needed. Adopt Ch 10's outcome.

Note also Ch 10's own framing, worth preserving if the hazard is rewritten: this
failure and the absent-controller failure are the same failure in the end — an
object that never reaches a controller — but this one fails AT THE MOMENT YOU APPLY
IT and the other applies cleanly and then quietly does nothing. Only one of them
tells you.

See [[ingress]], [[ingress-controller]], [[gateway-api]], [[absent-component-pattern]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/access-modes.md ===

## Chapter 19 update (2026-08-31) — the discriminator and the mnemonic

THE DISCRIMINATOR (Ch 19 §2, Domain 2):

  "One node, or one Pod?"

  ReadWriteOnce (RWO)     = read-write by A SINGLE NODE. Multiple Pods ON THAT NODE
                            can share it.
  ReadWriteOncePod (RWOP) = read-write by A SINGLE POD, CLUSTER-WIDE.
  [source: k8s-docs-persistent-volumes-depth-2026-08-25]

One of the four ⚠ hazards where the intuitive reading is wrong, and the strongest
of them: "The English is genuinely misleading, which is why ReadWriteOncePod exists
to name the other case explicitly."

Stated the other way, which is the version that survives pressure: ACCESS MODES ARE
NODE-COUNT SEMANTICS, NOT PERMISSION SEMANTICS. Ch 19's Soundings Q3 asks the
reader to state what RWO constrains AND what it does not, precisely because the
second half is where the collapse lives.

THE MNEMONIC covering all four hazards (Ch 19 §2, 🪢):

  Once is a node, empty is nothing, one default only, Running is not working.

See [[persistentvolume-and-claim]], [[pv-phases]], [[storageclass-and-provisioning]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pv-phases.md ===

## Chapter 19 update (2026-08-31) — the discriminator

THE DISCRIMINATOR (Ch 19 §2, Domain 2, 🪝 Snag):

  Released is not Available.

When a PVC is deleted, its PV moves to Released: the claim is gone but the previous
claimant's data is still there, so the volume is NOT free for a new claim
[source: k8s-docs-persistent-volumes-depth-2026-08-25]. Under Retain, an
administrator reclaims it by hand.

  THE TELL: a stem describing a PV that "should be reusable but isn't" is usually
  here.

WHY THAT IS THE POINT AND NOT A BUG, from Ch 19 Practice Q8's answer key:
reclaiming is a manual, deliberate act, and that is the entire purpose of Retain —
IT PROTECTS DATA BY REFUSING TO SILENTLY RECYCLE.

Q8's distractors are worth recording because each fails differently: "can only be
bound once" (wrong — it can be reused after manual reclamation); "must set
volumeName" (volumeName binds a PVC to a NAMED PV but does not change the PV's
PHASE, and a Released volume still will not bind); and an inversion of the
storageClassName hazard.

See [[access-modes]], [[reclaim-policies]], [[storageclass-and-provisioning]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/storageclass-and-provisioning.md ===

## Chapter 19 update (2026-08-31) — the discriminator, and the inversion trap

THE DISCRIMINATOR (Ch 19 §2, Domain 2):

  storageClassName: ""  = explicitly NO CLASS. Bind only to a PV that also has no
                          class. An explicit opt-OUT.
  field OMITTED         = "whatever the cluster's default behavior is," which
                          depends on whether the DefaultStorageClass admission
                          plugin is on.
  [source: k8s-docs-persistent-volumes-depth-2026-08-25]

One of the four ⚠ hazards. Reading "" as "use the default" gets it EXACTLY
BACKWARDS: omitting the field is the thing that engages default behavior.

THE INVERSION TRAP Ch 19 Practice Q8 builds on it, which is worth recording because
it is a second-order use of the same hazard: option D says a PV with
storageClassName: "" binds only to a PVC that OMITS the field. It does not — it
binds only to a PVC that ALSO EXPLICITLY SETS "". The distractor inverts the hazard
rather than contradicting it, which is why it repays a careful read.

See [[access-modes]], [[pv-phases]], [[reclaim-policies]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/helm-rollback-versus-rollout-undo.md ===

## Chapter 19 update (2026-08-31) — one question resolves both halves of the homonym

THE DISCRIMINATOR (Ch 19 §2, Domain 3; graded at Bearings 2 Q5 and Practice Q7):

  "Whose history is being rewound?"

  kubectl rollout undo -> walks a DEPLOYMENT's revision history, inside Kubernetes
  helm rollback        -> takes "the name of a release" and "a revision (version)
                          number" and rolls THAT RELEASE back to that revision
                          [source: helm-rollback-cli-2026-08-31]

Different histories, different scopes, same English word. The scope differs by an
order of magnitude: a release may contain a dozen Kubernetes objects.

WHAT CH 19 ADDS — the same question resolves BOTH halves of the collision:

  For "revision": whose history?
  For "rollback": whose history is being rewound?

  THE FASTEST TELL: a release name plus a number is Helm. A Deployment plus
  ReplicaSets is rollout undo. A commit is GitOps.

THE THIRD SENSE, held in reserve: GitOps ROLLBACK BY REVERT — undo the commit and
let the agent reconcile. Ch 15 always writes it out in full precisely because the
bare word is overloaded.

⚑ A DISTINCTION WORTH PRESERVING, from Bearings 2 Q5's answer key. The Helm-internal
discriminator ("package, install, or version of it?") separates chart / release /
revision FROM EACH OTHER. This row's discriminator separates Helm FROM Kubernetes.
Both are correct; the stem tells you which ambiguity is in play, and reading the
stem for that is the actual skill. Do not consolidate the two discriminators.

See [[helm-release-revision]], [[helm-release]], [[gitops]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/restart-policy.md ===

## Chapter 19 update (2026-08-31) — the scope discriminator, and ⚑ ONE UNTAUGHT CLAIM

THE DISCRIMINATOR (Ch 19 §2, Domain 1, last row):

  restartPolicy governs CONTAINERS WITHIN A POD, not the Pod object.

  A Job whose Pod template sets restartPolicy: Never will still get a REPLACEMENT
  POD from the Job controller when the first one fails. The policy stopped the
  container from restarting IN PLACE; it did not stop the workload from being
  retried.

  THE TRAP: reading "Never" as "this workload will not come back."

Both halves of that are taught and sourced. Ch 5 §5 owns the field — Pod-level
scope, the three values, the backoff schedule
[source: k8s-docs-pod-lifecycle-2026-08-23]. Ch 6 §7 supplies the replacement
behavior: "the Job will start a new Pod if the first one fails or is deleted"
[source: k8s-docs-job-2026-08-24], and Ch 6 also teaches the Job-side restriction
to Never or OnFailure.

⚑⚑ ONE CLAIM IN THIS ROW HAS NO OWNER AND NO SOURCE

Ch 19's row closes with: "Note also that a Deployment's Pod template cannot use
Never at all; the API requires Always there."

I searched all eighteen shipped chapters for restartPolicy — 28 occurrences across
Ch 5, Ch 6 and Ch 16. NOT ONE STATES THE DEPLOYMENT-SIDE RESTRICTION. Ch 6 :906
teaches only the Job converse. The claim is untaught, unsourced, and has no ledger
row.

It also breaks a promise the chapter makes to the reader in bold — "it contains
nothing new. Every fact in it was taught somewhere in Chapters 2 through 18" — and
one shipped Ch 18 makes on the way in: "Chapter 19 does not add material."

CONTEXT THAT CHANGES THE FIX. The fact-accuracy stage flagged draft-v1's version of
this row as describing a configuration that cannot exist; the revision stage
answered by ADDING this sentence. That resolved a factual defect and created an
integration one. DO NOT REVERT.

RECOMMENDED: cut the final sentence only. The row survives intact and illustrates
container-vs-Pod scope with the Job case, which is what the fact-accuracy stage
recommended and which stays entirely inside taught material. The alternative —
keeping it, sourcing it, and giving it an owner — also requires softening both
"nothing new" claims.

See [[pod-phase]], [[probe]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/version-skew.md ===

## Chapter 19 update (2026-08-31) — three numbers, and the structure that holds them

THE DISCRIMINATOR (Ch 19 §2, Domain 1): THREE DIFFERENT NUMBERS ON THREE DIFFERENT
AXES. Read which component is named before reaching for a number.

  kubelet           up to THREE minor versions older than kube-apiserver, never newer
  kubectl           within ONE minor version either direction
  supported releases the most recent THREE minor releases
  [source: k8s-version-skew-policy-2026-08-31]

THE STRUCTURE THAT MAKES THEM RECALLABLE (Ch 19 §2, 🔭 Closer Look) — this is what
Ch 19 adds, and it converts three memorized numbers into one rule plus one
exception:

  EVERY RULE IS ANCHORED TO kube-apiserver. Every component EXCEPT kubectl must be
  NO NEWER than it — which is why the upgrade order is control plane first.

  kubectl is the ONLY component allowed to be newer, because it is a client you run
  from your laptop and the project accepts you may have upgraded it casually.

GRADED AT Ch 19 PRACTICE Q3, and the item's shape is worth recording for Ch 20:
every distractor is off by EXACTLY ONE on a DIFFERENT AXIS. When a numeric item's
options differ by a single increment on separate dimensions, the discrimination
being tested is WHICH DIMENSION THE RULE APPLIES TO, not the arithmetic.

See [[version-skew-symptoms]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/domain-weights-44-28-16-12.md ===

## Chapter 19 update (2026-08-31) — the allocation method

⚑ SLUG RULING. The Ch 19 outline nominated `domain-weight-allocation` as a new
concept. NOT CREATED. It would sit beside this file holding the same figures, which
is the ⚑ I2 shape at the chapter with the least claim to the territory. §4's
allocation method appends here instead. See the manifest's ⚑ C4.

THE WEIGHTS, unchanged and re-confirmed: 44 / 28 / 16 / 12
[source: cncf-curriculum-kcna-readme-2026-08-31] — CNCF's own curriculum
repository, agreeing exactly with the LF exam page and the curriculum PDF.

⚠ THE CHAPTER MAPPING IS EDITORIAL AND CH 19 SAYS SO. D1 = Ch 2-8, D2 = Ch 9-13,
D3 = Ch 14-16, D4 = Ch 17-18 is "how *this book* laid the material out, not
something CNCF publishes." A reconciler that treats it as published will report
drift against a boundary CNCF never drew.

### The allocation method (Ch 19 §4)

The premise: "Study time is not fungible with comfort. The hours you most want to
spend are usually on material you already know."

The instrument is a table THE READER FILLS IN — domain, weight, chapters, their own
worst Bearings score in that range, which chapter, hours already spent — followed by
one question:

  "Is the domain where you scored worst the domain where you have spent the most
   hours?"

"If the answer is no, and for most readers it is no, that gap is your study plan."
The chapter is explicit that this beats any general advice BECAUSE IT IS MEASURED ON
THE READER.

### The priority order

  1. Worst-scoring chapter in Domain 1 — 44%, so a weak chapter there costs more
     than a weak chapter anywhere else, arithmetically
  2. Community and Collaboration, if never deliberately studied — see below
  3. §2 of Ch 19, worked ACTIVELY rather than read
  4. Worst-scoring chapter in Domain 2 — 28%, second-largest surface
  5. A timed full-length attempt, if never sat — pacing is a distinct skill and is
     invisible until you meet the clock

  NOT on the list: re-reading chapters you scored well on. "It feels like studying.
  It is not."

### The Community-and-Collaboration argument, stated as arithmetic

⚑ WORTH PRESERVING VERBATIM IN SPIRIT — this is the book's cleanest execution of
ethical guardrail 8. Ch 19 REFUSES to claim the competency is frequently tested,
says so out loud ("stated as arithmetic rather than as a claim about how often it
is tested"), and argues from BOUNDED SURFACE AREA instead:

  Cloud Native Architecture is 12%, split across three competencies, so Community
  and Collaboration is roughly a twenty-fifth of the paper. What makes it worth an
  hour is not its share but its SHAPE — governance bodies and remits, SIG vs WG vs
  Committee, the project lifecycle, the maturity levels. Finite and bounded. An
  hour covers a large fraction of the whole competency. An hour added to a Domain 1
  topic already scoring well covers a much smaller fraction of a much larger
  surface, at a much lower marginal return.

Do not let a later stage "strengthen" this into a frequency claim.

See [[blueprint-change-2025-11-24]], [[cncf-project-maturity-levels]].

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/blueprint-change-2025-11-24.md ===

## Chapter 19 update (2026-08-31) — reframed as a study-allocation hazard

Ch 19 §4 stops treating the 2025-11-24 change as a historical fact and makes it an
active hazard about the READER'S OWN MATERIALS:

  "Third-party study material produced before that date allocates its coverage
   against a blueprint that no longer exists. If your practice questions came from
   a bank that still treats observability as a domain in its own right, your sense
   of where the points are is wrong."

THE TELL (Ch 19 §4, 🪝 Snag) — a checkable test, not a blanket dismissal:

  Check the copyright date on every non-CNCF resource. Look at WHERE OBSERVABILITY
  SITS. If your material lists it as a DOMAIN IN ITS OWN RIGHT, with its own
  weight, rather than as a COMPETENCY UNDER CLOUD NATIVE ARCHITECTURE, that
  material predates the change.

THE RULE FOR WHICH BLUEPRINT APPLIES, and it is unambiguous: "Any KCNA exam taken
after the updated release will test on the new set of Domains and Competencies,"
and "The only date that matters is the date you sit for the exam"
[source: lf-kcna-program-changes-2026-08-23]. Not purchase date, not first attempt,
not retake status.

⚑ WHAT CH 19 DELIBERATELY DOES NOT SAY, and the revision was right to strip it

draft-v1 stated the retired blueprint had FIVE DOMAINS and named the retired domain
"Cloud Native Observability." Both were removed. The only corpus source for either
is provenance-kcna-60-questions-2026-08-23, which is headed "DO NOT CITE THE
CONTENTS OF THIS FILE AS FACT," and cncf-curriculum-repo-kcna-versions-2026-08-23
records the retired weights as an explicit OPEN GAP with the instruction "DO NOT
draft the retired weights from memory or from third-party study guides."

The tell above rests ONLY on what is sourced: that observability MOVED under Cloud
Native Architecture.

OPEN AND CHEAP TO CLOSE, and Ch 20 will want it too: retrieve
`old-versions/KCNA_Curriculum old.pdf` (raw URL is in the versions snapshot) and
cache the retired domain list.

See [[domain-weights-44-28-16-12]].

=== END APPEND ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cross-cutting-themes.md ===

# Cross-cutting themes (the nine threads)

**Owner:** Chapter 19 §1 · **Type:** book apparatus, not exam vocabulary
**Ledger row:** term-ownership.md:620

## What it is

An idea Kubernetes applies repeatedly across subsystems, which the exam blueprint
cuts across at right angles. Ch 19 §1's premise:

  "A book organized by exam domain serves the exam, not the material. Kubernetes
   did not grow four domains. It grew a handful of ideas that got applied over and
   over, in different subsystems, by different SIGs, across a decade."

The reader-facing payoff, from the Chapter Summary: **the book is nine patterns
with instances, not eighteen chapters with facts.**

The instruction the section gives, which is the actual skill: "Do not memorize the
paths. The paths are here so you can CHECK your recall, not so you can recite them.
What you want is the ability to hear a question stem and think: *this is thread 3*."

## ⚑ Surface-form divergence — unratified

| Where | Form used |
|---|---|
| B7 ledger (term-ownership.md:620) | **cross-cutting theme** |
| Shipped Ch 18 handoff (ch18:1721) | **cross-cutting themes** |
| Ch 19 body, all nine subheads | **thread** |
| Ch 19 What You'll Learn (once) | cross-cutting themes |
| THIS SLUG | cross-cutting-themes |

A reader crossing the Ch 18 -> Ch 19 boundary meets a renamed concept with no
bridge. The slug follows the ledger deliberately: the KB is a machine index, not
reader-facing prose, so it should not move with an unratified stylistic choice.
Ratify the reader-facing word; the shard supports either. If "thread" wins, one
word in ch18:1721 must change.

Same shape applies to [[discriminating-question]].

## ⚑ The chapter count is a three-way disagreement

  section-skeleton.md   "Nine Threads Through TWENTY Chapters"
  shipped ch18:1721     "Nine cross-cutting themes traced through TWENTY chapters"
  Ch 19 §1 as drafted   "Nine Threads Through EIGHTEEN Chapters"

Ch 19 is right on the merits — the threads terminate at Ch 18 (seventeen chapters
traced), and the book has eighteen content chapters before this one. But correcting
only the skeleton leaves shipped Ch 18 promising a number the next page
contradicts. TWO OF THE THREE MUST MOVE TOGETHER.

## The nine threads, with verified paths

Tiers are a reading aid, not doctrine.

STRUCTURAL — how the cluster is built

  1. THE CONTROL LOOP. Desired state, current state, reconciliation.
     Ch 3 §6 -> 4 §1 -> 6 §2 -> 11 §2 -> 15 §7 -> 17 §4. See [[control-loop]].

  2. NAMESPACED VS CLUSTER-SCOPED.
     Ch 4 §3 -> 8 §3 -> 12 §3. Derives the whole RBAC binding matrix.
     See [[namespaced-vs-cluster-scoped]].

  3. AN OBJECT WITHOUT ITS COMPONENT DOES NOTHING. ★ Fixed Point.
     Ch 3 §4 -> 10 §3 -> 11 §5 -> 13 §7 -> 17 §7 -> 18.
     See [[absent-component-pattern]].

INTERFACE — how the parts are joined and extended

  4. DECLARATIVE DESIRED STATE VS IMPERATIVE COMMAND.
     Ch 4 §1 -> 6 -> 14 -> 15. See [[declarative-configuration]].

  5. LABELS AND SELECTORS AS THE UNIVERSAL JOIN.
     Ch 4 §5 -> 6 §3 -> 7 §3 -> 9 §4 -> 10 §6 -> 16 §4 -> 12 §3 (the contrast).
     See [[label-selector]].

  6. THE PLUGGABLE INTERFACES. CRI / CNI / CSI / CRDs, collected at Ch 17 §4.
     See [[pluggable-interface-pattern]].

POLICY — what is permitted

  7. IDENTITY, FROM POD TO API TO DELIVERY AGENT.
     Ch 5 §6 -> 12 §2 -> 15 §4. See [[serviceaccounts-and-identity]].

  8. REQUESTS AND LIMITS. Two numbers, five subsystems.
     Ch 5 §8 -> 7 §2 -> 13 §4 -> 17 §7 -> 18 §3. See [[resource-request]].

  9. ADDITIVE, ALLOW-ONLY, NO DENY.
     Ch 10 §6 -> 12 §3 -> 12 §9. See [[additive-never-deny]].

## Density, and what it implies

Threads 1, 3 and 5 touch the most chapters (six or more each) and are
correspondingly the most likely to appear in a question whose stem NEVER NAMES
THEM.

⚑ FIGURE SPEC DESYNC. The grid in ch19-fig01-cross-domain-integration-map was
rebuilt at revision from the nine prose paths, not traced from draft-v1's ASCII,
which was not column-aligned and disagreed with the prose in four places. Two
consequences the spec must absorb: the density sentence now names threads 1, 3 and
5 (resolving the spec's AUTHOR-REVIEW item 1), and thread 5 now includes Ch 16 §4,
which closes item 2 — Ch 16 no longer renders as an empty row. TOTAL MARKS ARE 41,
NOT THE 40 THE SPEC RECORDS. Re-sync.

## What is graded, and what is not

Only four of the nine carry a graded item in this chapter: 3, 9, 2 and 7. Threads
1, 4, 5 and 6 are taught in §1 and tested nowhere in Ch 19. If Chapter 20 wants
them, it must build them itself.

=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/confusion-pair-matrix.md ===

# Confusion pair matrix

**Owner:** Chapter 19 §2 · **Type:** book apparatus, not exam vocabulary
**Ledger row:** term-ownership.md:621

## The diagnosis

  "Most lost points on a multiple-choice exam are not lost to ignorance. They are
   lost to COLLAPSE: two adjacent concepts filed as one thing, so that when both
   appear as options the reader has no way to separate them and picks by feel."

The remedy is [[discriminating-question]] — a procedure, not a definition. This
file is the CATALOGUE; that one is the METHOD. Two ledger rows with two owners, so
two shards. They are cross-linked heavily on purpose: this is NOT the ⚑ I2
duplicate-slug shape.

## The working instruction, which is not optional

  "Work these actively. Cover the right column, read the pair, say the
   discriminator out loud, then check. Reading this section passively will feel
   productive and will do nothing."

§4 ranks working §2 actively THIRD in the reader's remaining study hours, above
their weakest Domain 2 chapter, on the reasoning that "discrimination failures are
cheap to fix and expensive to leave."

## Structure

23 pairs on the compressed card, more in the four full tables underneath, plus a
13-row surface-form homonym table and four hazards. Each row is: THE ONE-LINE TEST,
then THE TELL that shows it up in a stem. Never two competing definitions side by
side.

## The compressed card — the highest-value pairs, sized for one drill pass

  D1  Pod phase / container state  -> "Lifecycle, or one container?"
  D1  liveness / readiness         -> "Restart it, or stop sending traffic?"
  D1  labels / annotations         -> "Does anything select on it?"
  D1  ConfigMap / Secret           -> "Would you mind this in a log?"
  D1  Deployment / StatefulSet     -> "Does replica 0 need to BE replica 0?"
  D1  OCI / CRI                    -> "Artifact format, or kubelet's API?"

  D2  ClusterIP/NodePort/LB        -> "Reachable from where?"
  D2  Ingress object / controller  -> "The record, or the thing that acts?"
  D2  NetworkPolicy default        -> "Is this Pod selected by any policy?"
  D2  Role / ClusterRole binding   -> "What scope is the BINDING?"
  D2  PV / PVC                     -> "Supply, or demand?"
  D2  RWO / RWOP                   -> "One node, or one Pod?"

  D3  chart / release / revision   -> "Package, install, or version of it?"
  D3  rollout undo / helm rollback -> "Whose history is being rewound?"
  D3  push / pull delivery         -> "Where do the credentials live?"
  D3  OutOfSync                    -> "Difference, or failure?"

  D4  mesh CP / cluster CP         -> "Whose control plane?"
  D4  sidecar / ambient            -> "Proxy per Pod, or per node?"
  D4  HPA / VPA                    -> "More replicas, or bigger ones?"
  D4  observability / monitoring   -> "New questions, or known ones?"
  D4  span / trace                 -> "One hop, or the whole journey?"
  D4  SLI / SLO / SLA              -> "Measure, target, or consequence?"
  D4  TOC / Governing Board        -> "Technical, or business?"

## The four hazards where intuition is actively wrong

Ch 19 rates these "worth more attention than the rest of this section combined,
because intuition will actively work against you and confidence will feel high."

  1. ReadWriteOnce is a NODE, not a Pod. See [[access-modes]].
  2. storageClassName: "" means NO CLASS, not "the default".
     See [[storageclass-and-provisioning]].
  3. A second default IngressClass REMOVES coverage. See [[ingress-freeze]].
     ⚑ Ch 19 understates this; Ch 10 has the stronger sourced form.
  4. Running is not "the application works." See [[pod-phase]].
     ⚑ Ch 19's wording drops "or restarting" — see that shard.

  🪢 Once is a node, empty is nothing, one default only, Running is not working.

## The 13 surface-form homonyms

namespace · control plane · sandbox · revision · rollback · label · request ·
binding · release · Service · immutable · operator · volume

  "When one of these appears in a stem, the first move is to establish WHICH SENSE,
   because half the options will be constructed from the other one."

Plus one word that is not a homonym but behaves like one: PLUGIN is never used bare
in this book — always CNI plugin, scheduler plugin, admission plugin, device
plugin. An option saying "the plugin" is not telling you enough to answer, and that
is usually deliberate.

⚑ THE `volume` ROW IS UNSANCTIONED. Ch 19 pairs Pod-spec volume (Ch 11 §1) with
PersistentVolume (Ch 11 §2). The ledger's Canonical-forms row (term-ownership.md:886)
defines the pair as Kubernetes volume vs DOCKER volume, with "Sense B is not used."
Ch 19's pair is BETTER for this reader — both senses are owned, both are examinable,
the Docker sense is banned — but it should be added to Canonical forms rather than
left to one chapter to invent.

## What §2 needs before it ships

Two rows lack the cross-bearing that would discharge their source obligation under
the book-level ruling from the Ch 18 gate. Both owners exist and are exact:

  the probe row              -> Ch 5 §7, "Three Probes, Three Jobs"
  the frozen/deprecated row  -> Ch 10 §4, "Frozen, Not Deprecated"

Adding them retires most of the draft's own §2 research-gap block at zero cost.
The block itself is a false alarm — all six sources it asks for are cached; the
corpus is 303 files, not the 31 the block assumes.

See [[discriminating-question]], [[exam-pacing]], [[the-lodestar]].

=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/discriminating-question.md ===

# Discriminating question (the discriminator)

**Owner:** Chapter 19 §2 · **Type:** book apparatus, not exam vocabulary
**Ledger row:** term-ownership.md:622

## The method claim

  "For each pair: THE ONE-LINE TEST THAT SEPARATES THEM, then THE TELL that shows
   it up in a stem. Never two competing definitions side by side. Definitions side
   by side is what caused the collapse in the first place; A DISCRIMINATOR IS A
   PROCEDURE, and procedures survive pressure."

That sentence is the whole concept. Two definitions held next to each other require
the reader to compare under time pressure; a discriminator asks ONE QUESTION whose
answer selects. The first degrades with fatigue; the second does not.

The checkpoint enforces it: "Supply the DISCRIMINATOR, not the definition. If your
answer reads like a dictionary entry, it will not survive the clock."

## ⚑ Surface-form divergence — unratified

  B7 ledger (term-ownership.md:622)  discriminating question
  Shipped ch18:1721                  "a question that discriminates between them"
  Ch 19 body throughout              discriminator
  THIS SLUG                          discriminating-question

Same shape and same ruling as [[cross-cutting-themes]]: the slug follows the
ledger; the reader-facing word is the author's to ratify.

## Choosing the right discriminator for the stem in front of you

The skill Ch 19 actually tests is not reciting a discriminator but knowing WHICH
AMBIGUITY IS IN PLAY. Bearings 2 Q5 is built entirely on this, and its answer key
is the clearest statement in the book:

  "package, install, or version of it?"  separates chart / release / revision FROM
                                        EACH OTHER. Internal to Helm.
  "whose history is being rewound?"      separates Helm FROM Kubernetes. Cross-tool.

  "Both discriminators are correct; the stem tells you which one is in play, and
   reading the stem for that is the actual skill."

DO NOT let a later stage consolidate the two. They answer different questions.

## Why this is a separate shard from the catalogue

[[confusion-pair-matrix]] is the catalogue of 23 pairs. This file is the method
claim. The ledger carries them as two rows with two owners, so two shards. This is
NOT the ⚑ I2 duplicate-slug shape — that fault is one concept under two slugs, and
these are two concepts that cite each other.

Recorded explicitly so no later manifest "merges" them.

## Frequency and decay

§6 names discrimination as "the thing that goes soft fastest and comes back
quickest, which is what makes it the best use of a short daily block" — twenty
minutes a day in the final week, worked aloud against a covered column.

[[the-lodestar]]'s discriminator block is the compressed drill form of the same
material.

=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/exam-pacing.md ===

# Exam pacing (the ninety minutes)

**Owner:** Chapter 19 §3 · **Type:** exam strategy, not technical content
**Ledger rows:** term-ownership.md:623 (flagging and skipping), :624 (the second pass)

## The three published facts that shape everything

  90 MINUTES for the Linux Foundation's multiple-choice exams
  [source: lf-mc-exam-faq-2026-08-31], on the KCNA exam page
  [source: lf-kcna-exam-page-2026-08-23] and in the candidate handbook
  [source: lf-mc-exam-important-instructions-2026-08-31].

  THE TIMER CANNOT BE PAUSED. "The system does not offer a way to pause the exam
  timer or to add time back to the exam during connection loss events"
  [source: lf-handbook2-taking-the-exam-2026-08-31]. Not for a bathroom break, not
  for a dropped connection.

  THERE IS NO SCRATCH PAPER. "Candidate is not allowed to write or enter input on
  anything (whether paper, electronic device, etc.) outside of the Exam console
  screen" [source: lf-exam-rules-and-policies-2026-08-31].

That third fact is load-bearing for the design of the rule: WHATEVER PLAN THE
READER USES HAS TO BE EXECUTABLE FROM MEMORY.

## ★ The rule

  Read the question count off the screen. Divide the clock by it. Reach the end of
  the paper at roughly 60% of your total time, and hold the remaining 40% in
  reserve.

  On 90 minutes: first pass ends around 54 minutes, ~36 minutes in reserve.

STATED AS A RULE, NOT A SECONDS-PER-QUESTION NUMBER, ON PURPOSE. The LF publishes a
60-question format for MC exams as a class, in the candidate handbook
[source: lf-mc-exam-important-instructions-2026-08-31] — 60 in 90 is 90 seconds
apiece, ~54 seconds on the first pass. But THE RULE SURVIVES A DIFFERENT COUNT AND
THE ARITHMETIC DOES NOT.

## ⚑ The provenance point, and what it costs upstream

Ch 19's ⚓ Worth Securing states the 60 and the 75% ARE published — in the
handbook, for MC exams as a class, not on the product page. That is correct
[source: provenance-kcna-60-questions-2026-08-31].

SHIPPED CHAPTER 1 SAYS THE OPPOSITE, in four places, two of them graded (ch01:202,
:204, :341, :554). Ch 1 needs a retrofit and can adopt Ch 19's framing — the lesson
changes from WHETHER the authority publishes to WHERE. Ch 1's own hazard at
:211-213 (pace by proportion, not by question number) stays correct and is exactly
what this rule implements; do not touch it.

## ⚑ The console's behavior is unpublished, and §3 degrades gracefully

The LF publishes nothing about whether its MC console lets you skip, mark for
review, navigate back, or change an answer. Ch 19 confirms that absence on four
official pages, each of which documents the exam in detail and says nothing about
navigation.

So the reader establishes it on the TUTORIAL SCREEN, before the clock matters, and
the reserve means one of two things:

  CAN navigate back  -> the reserve is a genuine SECOND PASS, marked questions in
                        the order marked
  CANNOT             -> the reserve is a MARGIN: extra time affordable on a hard
                        question IN PLACE, spent as you go

Either way the failure mode guarded against is identical, and it is the one that
actually costs people the exam: SPENDING FOUR MINUTES ON QUESTION NINE.

This is the chapter's highest-value missing snapshot. If an LF or PSI BRIDGE source
documenting the MC interface is located and cached, the subsection collapses to two
sentences and the ★ Fixed Point can name the flag control directly. Until then the
hedge stands — there is no scratch paper to fall back on, and a memorized procedure
that turns out to be unavailable is worse than no procedure.

## The first pass — three categories

  KNOW IT       Answer, move. DO NOT RE-READ TO CONFIRM. Confirmation on a question
                you knew is the single largest source of time leakage and almost
                never changes the answer.
  CAN GET IT    Two options survive. Give it twenty seconds. If it resolves, answer
                and move. If not, pick the likelier, mark, move.
  DON'T KNOW IT ANSWER ANYWAY, reasoned rather than blind: a blank scores zero with
                certainty, and the LF publishes no wrong-answer penalty in either
                direction. Certain zero vs uncertain penalty -> answer. Then mark
                and move IMMEDIATELY.

  Always leave an answer even when marking. A marked question with an answer is one
  you can improve; a marked blank is one you can lose to the clock.

## The second pass

Marked questions, in the order marked. Two things have changed: later questions
sometimes disambiguate earlier ones, and first-pass momentum has lifted, so the full
[[discriminating-question]] procedure is affordable.

  CHANGE AN ANSWER ONLY WHEN YOU CAN SAY WHY. "A reason you can state out loud is
  evidence. 'It feels wrong now' is usually fatigue wearing the costume of insight."

## The three ways candidates run out of time

Separated because the fixes differ:

  RE-READING STEMS                  -> read once, then go to the options; the
                                       options usually clarify the stem
  REFUSING TO LEAVE ONE UNRESOLVED  -> marking is not giving up; it is waiting
                                       until the fix is possible
  RE-LITIGATING SETTLED ANSWERS     -> the reserve is for marked questions only

## Closed book — and the CKA advice does not transfer

"Candidates are NOT PERMITTED to access tools, resources or external sites when
taking the Linux Foundation Multiple Choice OR SkillCred Exams"
[source: lf-certification-resources-allowed-2026-08-31]. The kubernetes.io-open-in-
a-tab allowance is real but applies only to the PERFORMANCE-BASED exams
[source: lf-certification-resources-allowed-2026-08-31]. It does not transfer to
KCNA.

See [[the-lodestar]], [[confusion-pair-matrix]], [[domain-weights-44-28-16-12]].

=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/the-lodestar.md ===

# The Lodestar (`the-lodestar.md`)

**Owner:** Chapter 19 §5 · **Named to the reader:** Chapter 1
**Ledger row:** term-ownership.md:625

## ⚑⚑ BLOCKING — THIS SHARD DESCRIBES AN ARTIFACT THAT DOES NOT EXIST

Verified 2026-08-31: `Book-KCNA/` contains nineteen chapter files, README.md,
sources/ and .pipeline-state/. THERE IS NO the-lodestar.md.

This is worse than a missing deliverable, because CHAPTER 1 HAS ALREADY SOLD IT.
ch01:452 names it to the reader —

  "**`the-lodestar.md`** — a single page holding the exam-critical facts,
   distinctions, and traps, distilled from the whole book. It's the last thing to
   read before the exam. Chapter 19 walks you through using it."

— and emits *[cross-bearing: see Ch 19 §5 — using The Lodestar]*. So §5 CANNOT BE
CUT, DEFERRED, OR RESHAPED AROUND THE ABSENCE.

This file therefore records §5 as THE CONTRACT THE ARTIFACT MUST SATISFY, which is
the thing needed to write it. The six block names below are PROVISIONAL. They
become factual claims about a shipped artifact the moment the file exists, and must
be reconciled against it.

Ch 19 §5's opening sentence was softened at revision from the present-tense "ships
with this book" to a description of what the file is FOR, so the chapter does not
assert a shipped artifact that has not shipped. RESTORE THE STRONGER PHRASING once
the file exists.

## What it is

  "This book's one-page reference, living at the repository root: the concentrated
   form of everything worth having in front of you in the hour before you sit down,
   and nothing else."

  "A DISTILLATION, NOT A SUMMARY." No chapter recaps, no explanations, no worked
  examples, no context. Every line assumes you have read the chapter it came from.

Brand context (skill Part 16, style-decisions.md [LOCKED 2026-04-19]): the
functional analog to a For Dummies tear-out card, named for the brand's namesake
reference star, REQUIRED for every Lodestar book.

## The six blocks §5 declares, each typed as DRILL or LOOKUP

  1. DOMAIN WEIGHTS AND THE EXAM'S PUBLISHED SHAPE — 44/28/16/12, 90 minutes, the
     handbook-published count and passing standard.  LOOKUP.
  2. THE CONFUSION-PAIR DISCRIMINATORS — the pair and its one-line test, nothing
     else. DRILL. "The block that repays a second pass."
  3. THE FOUR HAZARDS — Once is a node, empty is nothing, one default only, Running
     is not working. Four lines. DRILL.
  4. THE VERSION-SKEW NUMBERS — kubelet three back, kubectl one either way, three
     supported minors. LOOKUP, "but read it twice."
  5. EXAM-DAY PACING — the §3 rule in one line, because it must be executable from
     memory and there is no scratch paper.
  6. GOVERNANCE AND INSTITUTIONAL VOCABULARY — Board/TOC, the End User TAB's
     advisory role, SIG/WG/Committee, maturity levels. "The Domain 4 material most
     likely to have gone soft, and the cheapest to refresh because it is bounded."

Skill Part 16 additionally requires exam-critical FORMULAS with interpretation
rules; KCNA has none, which is why §5's block list has no formula entry. Note that
divergence when reconciling against the shipped file.

## How §5 says to use it in the last hour

  FIRST PASS — DRILL, ~20 min. Cover the answers. Work the discriminator and hazard
  blocks. Mark where you hesitate. DO NOT LOOK ANYTHING UP; the point is to find
  soft spots, not fix them.

  Break.

  SECOND PASS — LOOKUP, ~20 min. Read the marked items and the number blocks. Once,
  calmly. Then CLOSE IT.

  "Whatever is not in your head at that point is not going to arrive in the next
   twenty minutes, and the marginal value of a third pass is negative: it costs you
   composure and buys you nothing."

## The diagnostic property — worth preserving verbatim in spirit

  "If you cannot reconstruct a chapter from its Lodestar lines, YOU HAVE NOT FOUND
   A DEFECT IN THE LODESTAR. You have found a chapter you need to go back to."

Used as a final-week instrument: a Lodestar line that means nothing names a chapter
to re-read. In the last hour it is too late to act on, which is why §6 comes first
in the reader's timeline even though it comes second in the chapter.

## Production constraints (skill Part 16)

  - Single file at the book repo root: `the-lodestar.md`
  - Mostly tabular for density
  - One print page or one tablet screen; past two pages it is not distilled
  - NO NEW CONTENT — every fact derived from chapter material
  - Cross-bearings back to the owning chapter for each item

See [[confusion-pair-matrix]], [[exam-pacing]], [[access-modes]],
[[storageclass-and-provisioning]], [[ingress-freeze]], [[pod-phase]],
[[version-skew]], [[domain-weights-44-28-16-12]].

=== END WRITE ===
```