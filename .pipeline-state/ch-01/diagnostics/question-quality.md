Audited. Note on inputs before the artifact: the prompt's `draft-voice.md` was unavailable because Stage 4 wrote its output back into `draft-v1.md` (preserving the pre-voice copy as `draft-v1-prevoice.md`) while `pipeline_state.yaml` records `output_path: draft-voice.md`. I audited `draft-v1.md`, whose mtime matches Stage 4's completion timestamp. That path mismatch is flagged in the artifact.

# Question-Quality Audit — Chapter 1

**Input audited:** `.pipeline-state/ch-01/draft-v1.md` (Stage 4 voiced output; see path note below)

> ⚠ **Pipeline defect, non-blocking for this audit.** This stage was handed `draft-voice.md`, which does not exist on disk. Stage 4 (`voice_pass`) mutated `draft-v1.md` in place and preserved the pre-voice text as `draft-v1-prevoice.md`, but `pipeline_state.yaml` records its `output_path` as `...\ch-01\draft-voice.md`. Every downstream diagnostic stage reading from state will be handed a missing file. `draft-v1.md` mtime (04:04:03Z) matches Stage 4's `completed_at` exactly, so the voiced draft was located and audited in full. Fix the Stage 4 `output_path` registration before Chapter 2 runs.
>
> Secondary: `diagnostics/structural.md` reports `0 fail, 0 warn, 0 pass` on this draft. Zero *passes* means the structural linter evaluated no checks at all, so it provides no independent corroboration of the marker and checkpoint counts below. Counts here were taken by hand from the draft.

## Summary

- Chapter type: **orientation**
- Total questions inspected: **10**
  - 🧭 Soundings questions: **5**
  - ☆ Taking Your Bearings questions: **5** (across **2** checkpoints — 3 + 2)
  - Practice questions: **0** (orientation-exempt)
- Question budget compliance: **met** (10/10, every category exact)
- Weak distractors (WARN): **4 options across 3 questions**
- Trap answers that don't target real misconceptions (WARN): **2**
- Missing or incomplete why-wrong explanations (FAIL): **0** — all 15 wrong options across all 5 checkpoint questions carry an explanation
- Retrieval-practice spacing: **compliant** (0% target, 0% actual — Ch 1 excluded from the retrieval schedule per [B3])
- Soundings spoiler check: **clean** against Chapter 1's ★ Fixed Point — 0 spoilers. Two cross-chapter over-disclosures flagged as WARN.
- **Soundings rubric: present but unscoreable as written (WARN, high).** Q5 has no right answer; the rubric bands assume 5 scoreable items.

The chapter is in good shape. There are no FAILs. The two items worth an author decision before the gate are the Soundings scoring arithmetic and the untested §4 claim.

## Question-budget compliance

Against `question_budget` in outline frontmatter:

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 5 | 5 | **met** |
| Taking Your Bearings (total) | 5 | 5 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 | 2 | **met** |
| Practice Questions | 0 | 0 | **met** (orientation-exempt) |
| **Chapter total** | **10** | **10** | **met** |

Checkpoint distribution (3 after §3, 2 after §6) matches the outline's plan exactly. The skill's ≥10-Bearings figure is a content-chapter baseline and correctly does not bind here.

## Soundings spoiler check

Chapter 1 declares exactly one ★ Fixed Point (draft-v1.md:142–144): *the four domains and their weights — 44 / 28 / 16 / 12*. Nothing in any Soundings stem or answer names a domain, a weight, or the four-domain structure.

| Soundings Q # | Tests topic | Spoils Ch 1 Fixed Point? | Evidence |
|---|---|---|---|
| 1 | Container vs VM — kernel sharing | no | Stem and answer confined to the kernel boundary; one-line answer + `[cross-bearing: see Ch 2 §1]`. Does not touch domains or weights. |
| 2 | Kubernetes as orchestrator vs runtime | no — but see WARN below | Answer key runs two sentences and states the reconciliation loop. No Ch 1 Fixed-Point content. |
| 3 | Who governs Kubernetes | no | Answer names CNCF/Linux Foundation. Ch 17 territory, not Ch 1's Fixed Point. |
| 4 | What "cloud native" is *commonly assumed* to mean | no — exemplary | Answer states the wrong-but-common belief, explicitly declines the real definition, and defers: *"We'll come back to it in §4 below, and [cross-bearing: see Ch 17 §1]"*. This is exactly the plant-and-harvest discipline the outline specified. |
| 5 | Prior declarative-config exposure | no | Self-report calibration item; no factual content. |

**Verdict: clean.** Rule 7 satisfied. Two secondary observations:

**WARN — Q2's answer key over-teaches into Chapter 3.** The key reads: *"Kubernetes is an **orchestrator**: it decides what should run where, watches whether reality matches your declared intent, and corrects the difference."* The clause after the colon is a compressed statement of the reconciliation control loop, which the outline names as Chapter 3's Fixed Point. The outline's own answer-key discipline said one-line rationale and stop. **Recommended fix:** truncate to *"Not accurate. Kubernetes is an **orchestrator** — it decides what runs where. A separate **container runtime** on each machine actually starts the containers."* and let the cross-bearing carry the rest. The reconciliation clause is Chapter 3's payoff; spending it here costs it twice.

**WARN (minor) — Q3's answer key exceeds a pre-test rationale.** It carries two sourced facts beyond the answer (the 2015 Google donation, the contributor scale). Both belong to Ch 17's ecosystem material. Not a spoiler — Ch 17's Fixed Point is the CNCF *definition*, not the governance history — but it is more teaching than a pre-test key needs. Trim to the foundation name plus the cross-bearing if Ch 17 wants the donation story as its own beat.

**Answer disclosure (rule 9): PASS.** All five answers sit inside a `<details><summary>Answers + reading strategy</summary>` block (draft-v1.md:53–72).

**Rubric (rule 8): PRESENT, three bands, reading-strategy per band — but arithmetically broken.** See the finding below.

## Per-question findings

### Q🧭 Soundings (instrument-level): the rubric cannot be scored as written

**Issue:** Q5 is a self-report with no correct answer — the key says so outright: *"No right answer here; this one is calibration only."* But the rubric that follows bands on a five-point scale: **4–5 right** / **2–3 right** / **0–1 right**. Only four items are scoreable, so "5 right" is unreachable, and a reader who answers all four scoreable questions correctly scores 4/5 — landing at the *bottom* of the top band, reading as a near-miss when it is in fact a perfect result. A reader who gets two of four right cannot tell whether Q5 counts toward their 2.

Compounding it: the five items use four different response formats. Q1, Q2, Q4 are open-response; Q3 embeds three choices in the stem; Q5 is a yes/no self-report. Self-scoring an open-response set is already noisy — Q2 in particular is a two-part question (*"Is that accurate? If not, what does Kubernetes actually do, and what runs the containers?"*) with no partial-credit guidance — and the rubric bands are carrying more precision than the instrument can deliver.

**Distractor analysis:** n/a — the Soundings are open-response, so no distractors exist. Worth noting as a design consequence rather than a defect: §1 tells the reader the KCNA "measures whether you can *discriminate*" among four plausible statements, and §5 frames Soundings as calibration for that exam. An open-response Soundings cannot rehearse discrimination and cannot carry trap answers. Chapter 1 is the reader's first encounter with the instrument, so the format sets an expectation for the other nineteen chapters. Flagging for the author; it is a book-level format decision, not a Chapter 1 error.

**Why-wrong explanation status:** n/a (open-response; every item carries a correct-answer rationale, which is the applicable standard).

**Recommended fix:** cheapest option — restate the bands over the scoreable four and say so:

> *Q5 isn't scored; it's calibration. Of the four scored questions:*
> **3–4 right:** you arrive with the platform priors this book assumes…
> **1–2 right:** this is the expected starting point for this credential…
> **0 right:** read carefully, and give Chapters 2 and 3 a session of their own…

Alternative, if the five-point scale is wanted: convert Q5 into a scoreable declarative/imperative discrimination item (*"Which of these describes what a Terraform file does?"*), which also gives the Soundings one item in the exam's own format.

### QC1.2: "Which of the following about the KCNA is **not** published by the Linux Foundation on the exam page?"

**Issue:** Three of four options are true-fact recall rather than misconception traps, and the question's most valuable discriminative target never appears as an option.

**Distractor analysis:**
- A) The exam duration — **implausible as a trap.** Published, and stated in bold in the Dead Reckoning block eight paragraphs earlier. No misconception attaches to it.
- B) The number of exam attempts included — **implausible as a trap.** Same; §2 gives it its own bolded paragraph.
- C) The passing score — correct.
- D) The four domain weights — **implausible as a trap.** Published, and about to be made the chapter's Fixed Point.

The question therefore reduces to "which of these four did the chapter *not* list as published," which is recall, not discrimination. Meanwhile §2 and the ⚠ Navigational Hazards block treat **the 60-question figure** as at least as dangerous as the 75% figure — the pacing hazard is built entirely on question count — yet the count appears only in the answer body (*"Neither is the question count"*), never as an option the reader has to reject. The reader is never made to confront the more consequential of the two inherited numbers.

**Why-wrong explanation status:** present but thin. A, B, and D each get a single clause (*"A is wrong — 90 minutes is published"*). Factually complete, but they perform no error correction because no error was available to make. The trailing paragraph on "75% to pass" is the strongest part of the answer and is doing work the options should have done.

**Recommended fix:** invert the stem so both inherited figures become distractors and every wrong answer targets a documented misconception:

> **Which of the following about the KCNA *is* published by the Linux Foundation?**
> A) The number of questions on the exam
> B) The passing score
> C) The four domain weights ✓
> D) The recommended number of study hours

A and B are then the two figures the internet reports as fact — exactly the misconception §2 exists to correct — and D catches the reader who assumes a certifying body prescribes preparation time. The existing answer prose transfers almost unchanged.

### QC1.3, option D: "Prioritize Cloud Native Architecture, since it contains the most named competencies"

**Issue:** The option's stated premise is false against the chapter's own table, printed ~85 lines earlier, and the answer key silently contradicts it.

**Distractor analysis:**
- A) Allocate by chapter count, "since chapter count reflects difficulty" — **plausible and worth keeping.** The book itself discloses that chapter allocation deviates from exam weight, so the reader has grounds to be tempted. One softness: the answer key partly *concedes* the premise (*"Chapter count tracks how much explaining a topic needs"* ≈ difficulty), so the option is wrong because the premise doesn't license the conclusion, not because it's false. The explanation handles this adequately; no change needed.
- B) Weight-proportional, then adjust for personal weakness — correct.
- C) Even split across four domains — **plausible.** A real naive strategy, and the explanation quantifies why it fails. Good.
- D) Prioritize Cloud Native Architecture, "since it contains the most named competencies" — **false premise.** The chapter's competency table gives Kubernetes Fundamentals four (Core Concepts, Administration, Scheduling, Containerization), Container Orchestration four (Networking, Security, Troubleshooting, Storage), Cloud Native Architecture **three**, Application Delivery two. Cloud Native Architecture does not have the most; it is tied for fewest-but-one. A reader who checks the table eliminates D on arithmetic without engaging the concept, which is the definition of a dead distractor. The answer key then states *"Cloud Native Architecture has three named competencies"* — correcting the option's premise without acknowledging the option asserted otherwise, which reads as an editorial slip rather than a trap.

**Why-wrong explanation status:** present and specific for all three. D's explanation is internally sound but disagrees with the option it explains.

**Recommended fix:** replace D with the misconception §3 actually induces — confusing *rate of change* with *share of exam*:

> D) Prioritize Cloud Native Application Delivery, since it doubled in the 2025 restructure

That is genuinely tempting immediately after a section whose emotional emphasis is "App Delivery doubled," it is checkably wrong (16% is still the second-smallest domain), and its why-wrong writes itself: *a domain that doubled from a small base is still small; growth rate is not exam share, and 16% does not outrank 44%.* It also inoculates against a misallocation §3 could plausibly cause, which is better trap fidelity than the current option offers.

### QC2.1, option D: "Move on to Chapter 10, since Chapter 9 clearly isn't landing"

**Issue:** Filler distractor. No reader scoring 1/8 on a *pre-*reading diagnostic concludes they should skip the chapter they have not yet read — the option is internally incoherent with its own stem, since "isn't landing" presupposes reading that hasn't happened. The answer key effectively concedes this: *"D is wrong and would be a genuine error"* — language that describes a mistake nobody is making rather than a temptation being defused.

**Distractor analysis:**
- A) Reread Chapter 1 — **plausible and correctly identified as the trap.** Readers do read a low diagnostic as "I missed something upstream." Good.
- B) Skip the Soundings answers, return after reading — **plausible.** Deferring an answer key is a real reader behavior, and the explanation makes a substantive case (the rubric and cross-bearings live in the key). Good.
- C) Read carefully and slowly — correct.
- D) Move on to Chapter 10 — **implausible; see above.**

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** replace D with the misconception the §6 🪝 Snag exists to correct — treating the score as information about the reader rather than as an instruction about the chapter:

> D) Read Chapter 9 at normal pace — a Soundings score reflects what you knew beforehand, so it says nothing about how to read the chapter

That is defensible-sounding, it is the exact confusion the Snag addresses, and its why-wrong closes the loop: *the score says nothing about your ability, but it says a great deal about the gap between what you brought and what the chapter assumes — which is precisely a pacing instruction.*

### Questions with no findings

QC1.1 (where observability lives), QC2.2 (why Ch 13 tests Ch 8). Both clean. QC1.1 is the strongest question in the chapter: all three distractors target distinct, real misconceptions — the retired blueprint (A), the practical adjacency of observability and troubleshooting (C), and "the domain is gone, so the topic is gone" (D) — and each why-wrong corrects a different error. QC2.2's option C (prerequisite-checking rather than spacing) is a genuinely tempting reading and its correction teaches something the reader will need for nineteen chapters.

## Retrieval-practice spacing

- Chapter 1 target: **0%** — no earlier chapter exists, and the arc outline's [B3] excludes Chapter 1 from the retrieval schedule entirely. The spacing ramp begins at Ch 3 (10%).
- Actual: **0%** (0 of 5 checkpoint questions tagged `[retrieval: chN]`)
- Status: **compliant**
- Recommended additions if short: none. Adding retrieval items here would be a defect, not an improvement.

**Forward-looking note for Stage 8 on Chapters 3+:** no question in this chapter is tagged with the `[retrieval: chN]` convention, so the tag's rendered form is not yet established anywhere in the book. Chapter 3 will be the first chapter that needs it. Whether the tag is reader-visible or a draft-only annotation stripped before publication is unresolved in both the outline and the structural contract — worth settling before Chapter 3 drafts, since this audit checks for it mechanically.

**[B3] compliance check:** the exclusion states no item *anywhere* in the book may test exam mechanics. Both Chapter 1 checkpoints stay inside it — neither asks the reader to recall a price, a duration, an eligibility window, or an attempt count as a fact. QC1.2 comes closest, since its options enumerate mechanics, but what it tests is the published/inherited distinction, not the values. The outline flagged this tension for reviewer override; as drafted, no override is needed.

## Coverage vs concepts

Against `kb_tags.concepts` in outline frontmatter:

| Concept introduced in chapter | Tested in a question? |
|---|---|
| `kcna-exam-format` | yes (C1.2) |
| `domain-weights-44-28-16-12` | yes (C1.3, and C1.1 indirectly) |
| `blueprint-change-2025-11-24` | yes (C1.1 — the relocation; the date itself is untested, correctly, as it is exam mechanics under [B3]) |
| `published-vs-commonly-reported` | yes (C1.2) |
| `cncf-certification-ladder` | **no** — acceptable. §1 names CKA and explicitly defers the family to Ch 17; the concept is *named*, not taught, so there is nothing yet to confirm encoding of. |
| `cloud-native-framing` | **NO — the one gap that matters.** See below. |
| `branded-markers` | **no** — acceptable. §5 is a reference legend; testing it would be book trivia, not learning. |
| `spaced-retrieval` | yes (C2.2) |
| `reading-paths` | partial (C2.1 tests what to do with a score; the three paths themselves are untested — acceptable, they are reader-selected, not recalled) |

### The `cloud-native-framing` gap

§4 makes exactly one assertion the reader is asked to carry forward, and it is stated in bold: **"cloud native" does not mean "runs in a public cloud."** Nothing in either checkpoint tests it.

This matters more than an ordinary coverage miss because §4's entire architecture is a plant harvested four hundred pages later. The section deliberately withholds the definition and asks the reader to hold a question open until Ch 17. Soundings Q4 *pre*-tests the misconception, which establishes that the author considers it live and near-universal — but a pre-test with no post-test is exactly the configuration that leaves a misconception uncorrected. The reader arrives believing "cloud native = public cloud," reads one paragraph telling them it isn't, and is never asked to retrieve that. If the negative claim doesn't encode, Ch 17's opening lands against the original wrong prior anyway and the four-hundred-page plant returns nothing.

Testing the *negative* does not spoil Ch 17, which owns the positive definition. It is the one part of §4 that can be safely examined.

**The obstacle is budget, not design.** Bearings is at 5/5. Adding a sixth puts the chapter at over-by-1. Three options, in order of preference:

1. **Add one question to Checkpoint #1 and amend the outline** — `question_budget.taking_your_bearings: 5 → 6`, `total_this_chapter: 10 → 11`. Honest, and the book clears the 300-question floor by a wide margin (715 planned), so nothing downstream is disturbed. A workable item: *"Your company runs Kubernetes on hardware in its own data centre, with no public-cloud footprint. Can the platform be described as cloud native?"* — distractors targeting "no, cloud native requires a public cloud" (the universal prior), "no, unless it uses managed services" (the halfway version), and "only if it's multi-cloud" (the buzzword conflation).
2. **Swap it in for QC1.2** if that question is rebuilt anyway per the finding above, holding Bearings at 5. Costs the published/inherited check, which is load-bearing for twenty chapters. Not recommended.
3. **Ship the gap deliberately**, with a note in Ch 17's outline that its opening must not assume the negative claim survived. Defensible, but it makes Ch 17 do work Chapter 1 could have done for one question.

**Recommendation: option 1.**

## Gate summary

| Severity | Count | Items |
|---|---|---|
| FAIL | 0 | — |
| WARN (high) | 2 | Soundings rubric unscoreable (Q5); `cloud-native-framing` untested |
| WARN | 4 | QC1.2 distractors A/B/D are recall-only and omit the question-count trap; QC1.3-D false premise; QC2.1-D filler; Soundings Q2 answer key spends Ch 3's control loop |
| WARN (minor) | 1 | Soundings Q3 answer key over-teaches Ch 17 governance detail |
| Non-blocking, operator | 2 | Stage 4 `output_path` points at a nonexistent `draft-voice.md`; structural lint reported 0 passes |

No finding blocks the gate on question architecture grounds. The chapter's strongest questions (QC1.1, QC2.2) are genuinely good — distractors that map to distinct real errors, why-wrong prose that corrects rather than announces. The weaknesses cluster in a predictable place: the fourth distractor, where symmetry pressure produced two options nobody would pick (QC1.3-D, QC2.1-D) and one question built from true statements instead of tempting ones (QC1.2). All four fixes above are single-option edits.