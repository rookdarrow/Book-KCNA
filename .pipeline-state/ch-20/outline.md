All artifacts read. One finding changes the plan materially, so I'll lead with it.

The B6 skeleton's Ch 20 block descriptions were written 2026-08-25 and are **stale on the two facts the chapter is built around**. They say the question count is "commonly reported, not published" and that the rubric "does not state a pass mark as fact — the 75% figure is unpublished." Both were superseded by the 2026-08-31 provenance work, and shipped Ch 1 plus drafted Ch 19 §3 now state the opposite with sources. Drafting the skeleton's version would contradict a shipped chapter and repeat a sentence the snapshot explicitly lists as false.

---

Research complete. Three findings changed the plan: the two stale skeleton constraints above, a per-chapter question blueprint derivable from B4 rather than guessable, and a ratified ruling that makes the 60-item answer key's citation burden tractable.

```yaml
---
chapter: 20
chapter_type: "mock_exam"
title: "Full Mock Exam"
subtitle: "Ninety minutes. No notes. Find out."
exam_domain: "All four domains — full-length assessment, no new objectives"
domain_weight_pct: 0
complexity: "mixed"
novelty: "familiar"
prereq_factor: "heavy"

# --- Section plan (no word budgets) ---
# THESE ARE BLOCKS, NOT NUMBERED SECTIONS. Per the B6 skeleton, Ch 20 has no
# §N anchors, deliberately. Nothing anywhere in the book may emit
# *[cross-bearing: see Ch 20 §N — …]*. Address this chapter by name only.
# `checkpoint_after` is false throughout: mock_exam is exempt from ☆ Taking
# Your Bearings, and a checkpoint inside a timed instrument would break it.
sections:
  - name: "Instructions"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Exam"
    objectives: ["D1.1", "D1.2", "D1.3", "D1.4", "D2.1", "D2.2", "D2.3", "D2.4", "D3.1", "D3.2", "D4.1", "D4.2", "D4.3"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Mock Exam Answers & Walkthroughs"
    objectives: ["D1.1", "D1.2", "D1.3", "D1.4", "D2.1", "D2.2", "D2.3", "D2.4", "D3.1", "D3.2", "D4.1", "D4.2", "D4.3"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Scoring Rubric"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false

# --- Skill v5.3 Part 11: Soundings ---
# 0 per B4 ("Soundings: 8 per content chapter; 5 per orientation/synthesis;
# 0 per mock_exam") and per the structural contract's mock_exam exemption.
soundings_planned:
  question_count: 0
  topics: []

# --- Skill v5.3 Part 8: practice-question budget (from B4 length-budget.md) ---
question_budget:
  soundings: 0
  taking_your_bearings: 0
  practice_questions: 60
  total_this_chapter: 60

kb_tags:
  objectives: ["D1.1", "D1.2", "D1.3", "D1.4", "D2.1", "D2.2", "D2.3", "D2.4", "D3.1", "D3.2", "D4.1", "D4.2", "D4.3"]
  concepts:
    - "mock-exam-calibration"
    - "domain-weighted-assessment"
    - "per-domain-score-sheet"
    - "distractor-from-trap-inventory"
    - "exam-pacing"
    - "confusion-pair-discrimination"
  commands:
    - "kubectl-get"
    - "kubectl-describe"
    - "kubectl-logs"
    - "kubectl-events"
    - "kubectl-exec"
    - "kubectl-debug"
    - "kubectl-port-forward"
    - "kubectl-top"
    - "kubectl-apply"
    - "kubectl-rollout-undo"
    - "kubectl-scale"
    - "kubectl-drain"
    - "helm-install"
    - "helm-rollback"
    - "crictl"

figures_planned: []
---
```

## 1. Why This Chapter Matters — *planning note, not a drafted section*

`mock_exam` is exempt from `## Why This Chapter Matters` in the structural contract, and the Instructions block carries the function. This note exists to orient drafting, not to be written.

The reader has finished nineteen chapters and two of them — 18 and 19 — told them they were nearly ready. This chapter is where that claim gets tested rather than asserted. Its value is not the score; it is the **per-domain** score, which is the only instrument in the book capable of showing the reader a hole they do not know they have. A candidate can be strong across three domains, weak in one, land a respectable total, and fail the real exam on the strength of the domain they never looked at. D4.3 Community and Collaboration is the standing example: B1 names it the competency technically-strong candidates most reliably under-study, and B2's stated mitigation is disproportionate representation here.

The register shift matters and should be deliberate. Nineteen chapters have been a navigator explaining. This chapter is the instrument itself — quiet, unadorned, no commentary. The voice returns in the walkthroughs and the rubric.

## 2. What You'll Learn — *planning note, not a drafted section*

Also exempt. The Instructions block states what the instrument does and does not measure; no `## What You'll Learn` heading is drafted.

## 3. Soundings plan

**Zero questions. Confirmed correct, not an oversight.**

Three independent authorities agree: B4 allocates 0 Soundings to `mock_exam`; `branded-terms.yaml` gives question counts for content, orientation, and synthesis chapters only; and the structural contract lists `mock_exam` under `exempt_chapter_types` for the 🧭 Soundings marker.

The pedagogy agrees too. Soundings is a *pre-test that calibrates reading strategy* — its whole output is a rubric telling the reader to skim, read normally, or read carefully. There is no reading strategy to calibrate here, and a diagnostic in front of a diagnostic measures nothing new. Ch 19's Soundings already did the readiness self-assessment this chapter would otherwise duplicate, in its ratified exam-readiness form.

No Fixed Points can be spoiled, because a `mock_exam` chapter teaches none.

## 4. Block plan

Four blocks, in this order, matching skill Part 16 and the B6 skeleton exactly. **No `§N` numbering. No difficulty indicators in headings** — a difficulty glyph on a question is a hint, and hints do not belong in a timed instrument. Difficulty is tracked in the blueprint and surfaced only in the answer key.

---

### Block 1 — `## Instructions`

Sets the clock, the rules, and the honest limits of the instrument. Short — half a page, not two.

Must cover:

- **Time budget: 90 minutes, 60 questions.** Both figures are published by the Linux Foundation in the candidate handbook for multiple-choice exams as a class, of which the KCNA is one. Cite `[source: lf-mc-exam-important-instructions-2026-08-31]`. The asterisk on the handbook's "60\*" is a CNPA carve-out, not a hedge — do not read it as one.
- **Phrasing discipline, non-negotiable.** The snapshot lists two sentences as false and they must not appear in any form: *"The Linux Foundation does not publish a question count"* and *"The KCNA exam page states the exam has 60 questions."* The true and useful statement is that both figures live in the handbook rather than on the product page most candidates read — which is exactly the distinction shipped Ch 1 spends a section and a graded Practice item establishing.
- **What this instrument is.** Sized and weighted to the published blueprint; written by Lodestar, not by CNCF; not a leaked or reconstructed exam. It predicts readiness, it does not predict a score.
- **Navigation asymmetry, stated plainly.** In this book the reader can move freely — skip, return, change answers. Whether the real console permits any of that is **undocumented**, confirmed absent across four official pages. Ch 19 §3 owns this and the drafting must point rather than restate: *[cross-bearing: see Ch 19 §3 — pacing and time discipline]*.
- **The pacing rule, retrieved not redefined.** First pass ends at roughly 60% of the clock — 54 minutes of 90 — leaving about 36 in reserve. Ch 19 §3 owns the rule and the reasoning for stating it as a fraction rather than seconds-per-question. Point, don't re-derive.
- **Conditions worth reproducing:** one sitting, no notes, no cluster, no search. The reader who looks things up gets a measurement of the book's index, not of themselves.
- **Where the answers are**, and an explicit instruction not to read ahead into them.

Objectives: none. This block is apparatus.

---

### Block 2 — `## Exam`

Sixty questions. One continuous run. **No mid-exam commentary of any kind** — no branded markers, no callouts, no cross-bearings (a pointer to the owning chapter is an answer key), no encouragement between items, no section breaks by domain.

Composition rules the drafting stage must hold:

- **Interleaved, never domain-blocked.** Real exams interleave, and blocking by domain hands the reader a scope hint per item. Interleaving is also the skill's own Part 10 mechanism for improving discrimination and transfer, which is precisely what this instrument measures.
- **Single-best-answer, four options.** No source documents multi-select, partial credit, or unscored pretest items for this exam — see Open Questions. Default to the one form the sources do attest and do not assert it is the only form the real exam uses.
- **Stems are self-contained.** A question may include a short YAML manifest, a command, or command output in a fenced block. It may **not** include an ASCII structure diagram: the structural contract requires a `FIGURE:` anchor on every such block, and a figure anchor inside a question stem would need a rendered figure, an image-spec entry, and would visually flag that item. Manifests and terminal output are code, not diagrams, and need no anchor.
- **No question tests exam mechanics.** Question count, passing standard, duration, price, eligibility window, renewal terms, and the blueprint change are all Ch 1 material, which B3 excludes from retrieval entirely. The mock tests the curriculum, not itself.
- **No question depends on the dated graduated-project roster.** B1 trap 99 and B3 both rule this out; test the maturity *levels* and their order instead, which is the durable fact.

Objectives: all thirteen competencies.

---

### Block 3 — `## Mock Exam Answers & Walkthroughs`

Separated so the reader can attempt first without spoilers. Per question:

1. The correct answer.
2. Why it is correct.
3. **Why each of the three distractors is wrong** — individually, not as a group. This is the skill's Part 11 requirement and it is the block's whole pedagogical payload.
4. A tag line: `D2.1 · Ch 9 §4 · 🔵` — domain and competency, owning chapter and section, difficulty. This is what makes the score sheet in Block 4 work, and it is what routes a wrong answer back to a page.
5. A cross-bearing to the owning section.

**Citation discipline — the rule that makes this block tractable.** Every claim in this chapter is a *retrieved* claim; the mock introduces nothing. The book-level ruling ratified at the Ch 18 gate (2026-08-31) applies directly: a cross-bearing to the owning section discharges the `[source:]` obligation for a claim first taught and source-tagged in its owning chapter. Three conditions bind — the pointer must name the owning **section**, not the chapter at large; the retrieved claim must not be strengthened, sharpened, or given a number the owner did not source; and the rule does not cover a claim the owning chapter itself left untagged. If drafting finds itself wanting to state something no chapter taught, the question is wrong, not the rule.

**Distractor sourcing.** B1's 114-entry trap inventory is the primary well — it is already tagged `[source]` or `[inferred]` per entry, and a distractor built on a documented misconception is worth four built on plausible-sounding noise. Two constraints: an `[inferred]` trap may be described as "easy to confuse" but **never** as frequently tested or as something candidates commonly miss, per Ethical Guardrail #8 and B1's own instruction; and a distractor whose refutation requires a term the book never defines must be rebuilt from taught material, per the ruling established at the Ch 9 gate over eBPF.

---

### Block 4 — `## Scoring Rubric`

Three elements in order.

**(a) The per-domain score sheet.** A fill-in table: one row per domain, with the item numbers belonging to it, a box for the reader's raw score, the maximum, and a percentage. This is the chapter's highest-value artifact and the reason the answer key carries domain tags. A single total can hide a domain hole; four sub-scores cannot.

| Domain | Items | Your score | Out of |
|---|---|---|---|
| D1 Kubernetes Fundamentals | *(listed)* | ____ | 26 |
| D2 Container Orchestration | *(listed)* | ____ | 17 |
| D3 Cloud Native Application Delivery | *(listed)* | ____ | 10 |
| D4 Cloud Native Architecture | *(listed)* | ____ | 7 |

**(b) Band interpretation.** The Linux Foundation publishes a 75% passing standard for its multiple-choice exams, of which the KCNA is one `[source: lf-mc-exam-faq-2026-08-31]` — 45 of 60 here. State it as the published standard for the class; do not state it as a KCNA-page fact, and do not imply that clearing it on this instrument predicts clearing it on the real one.

| Band | Reading |
|---|---|
| 51–60 | Comfortable margin above the published standard |
| 45–50 | At or just above it, on a thin margin |
| 36–44 | Below it; targeted work, not a general re-read |
| ≤ 35 | Below it substantially; a second pass through the weak domains |

**(c) What to do after each outcome.** Routing, not exhortation. The instruction in every band is the same shape: work from the sub-scores, not the total. A reader at 47 with D2 at 9/17 has a networking-and-storage problem, not a readiness problem, and the fix is two chapters rather than eighteen. Point at Ch 19 §4 for the weight-versus-weakness allocation, which owns that reasoning: *[cross-bearing: see Ch 19 §4 — where the weight actually is]*.

Objectives: none. Apparatus.

## 5. Taking Your Bearings checkpoints

**None.** `mock_exam` is exempt from the ☆ marker and from the two-checkpoint minimum; B4 allocates zero. A checkpoint inside a timed 60-question instrument would destroy the thing being measured. Retrieval practice is not skipped — the entire chapter is a retrieval event drawing on all seventeen content chapters, which is beyond the 20–25% spacing target by construction.

## 6. Exam Alert plan

**None.** `mock_exam` is exempt. Ch 19's Exam Alert and its §2 confusion-pair matrix carry this function for the reader; the walkthroughs in Block 3 carry the trap-level warnings item by item, where they land against a wrong answer the reader has just given. That is strictly better placement than a summary list.

## 7. Practice Questions plan — the sixty

The whole chapter. Three allocations, each derived rather than chosen.

### Domain distribution (from B4, verified)

| Domain | Blueprint | Items | Actual | Deviation |
|---|---|---|---|---|
| D1 Kubernetes Fundamentals | 44% | 26 | 43.3% | −0.7 pp |
| D2 Container Orchestration | 28% | 17 | 28.3% | +0.3 pp |
| D3 Cloud Native Application Delivery | 16% | 10 | 16.7% | +0.7 pp |
| D4 Cloud Native Architecture | 12% | 7 | 11.7% | −0.3 pp |
| **Total** | **100%** | **60** | | all within skill Part 16's ±2 pp |

### Per-chapter blueprint

B4 fixes the domain totals but not which chapter inside a domain supplies which item — and left unspecified, drafting will over-sample whatever is easiest to write questions about. Allocating each domain's items across its chapters **in proportion to that chapter's own B4 practice-question allocation** reuses a weighting the book already ratified, rather than inventing a second one.

| Ch | Chapter | Competency | B4 practice | Mock items |
|---|---|---|---|---|
| 2 | Cargo in Standard Crates | D1.4 Containerization | 25 | **5** |
| 3 | The Ship's Company | D1.1 Core Concepts | 19 | **4** |
| 4 | Records of Intent | D1.1 | 19 | **4** |
| 5 | The Smallest Vessel | D1.1 | 21 | **4** |
| 6 | Fleets, Not Vessels | D1.1 | 19 | **3** |
| 7 | Assigning the Berth | D1.3 Scheduling | 17 | **3** |
| 8 | Standing the Watch | D1.2 Administration | 17 | **3** |
| 9 | Every Pod Has an Address | D2.1 Networking | 21 | **4** |
| 10 | Traffic from Beyond the Cluster | D2.1 | 17 | **3** |
| 11 | Below the Waterline | D2.4 Storage | 17 | **3** |
| 12 | Locks, Keys, and Watchstanders | D2.2 Security | 21 | **4** |
| 13 | When the Cluster Won't Answer | D2.3 Troubleshooting | 15 | **3** |
| 14 | Packing for the Voyage | D3.1 App Delivery | 17 | **3** |
| 15 | The Chart Is the Truth | D3.1 | 21 | **4** |
| 16 | Your Application, Their Cluster | D3.2 Debugging | 15 | **3** |
| 17 | The Fleet and Its Charts | D4.2 + D4.3 | 21 | **4** |
| 18 | Reading the Instruments | D4.1 Observability | 17 | **3** |
| | | | | **60** ✓

Competency roll-up: D1.1 15 · D1.2 3 · D1.3 3 · D1.4 5 · D2.1 7 · D2.2 4 · D2.3 3 · D2.4 3 · D3.1 7 · D3.2 3 · D4.1 3 · D4.2 2 · D4.3 2.

Two properties worth keeping: **every content chapter is represented** (floor of 3, ceiling of 5), so no chapter the reader studied goes unmeasured; and **Ch 17's four items split 2 D4.2 / 2 D4.3**, which is B2's promised disproportionate representation for Community and Collaboration — B1 reads roughly 8 of D4's 12 points as observability-flavored, and a proportional allocation would have left D4.3 with one item or none.

### Question-form mix

B1 characterizes D1/D3 as comprehension, D2 as comprehension with diagnostic reasoning, and D4 as recall and recognition. The mix follows that:

| Form | Items | Concentrated in |
|---|---|---|
| Recall / identification | 15 | D4, some D1.4 |
| Discrimination (confusion pair) | 22 | across all four |
| Scenario / diagnostic | 15 | D2.3, D3.2, D2 generally |
| Manifest or output reading | 8 | D1.1, D2.1 |

### Difficulty distribution

CNCF publishes no difficulty mix, so this is author-calibrated judgment, which skill Part 16 permits and requires be labeled as such. Weighted toward the associate tier B1 describes: ⚪ 9 · 🔵 36 · 🟡 13 · 🔴 2. Recorded in the answer-key tags only — **never in the exam block**.

### Interleaving

Sequence by a fixed rule so it is reproducible and auditable: no two consecutive items from the same chapter, no three consecutive from the same domain, and the four hardest items distributed rather than clustered at the end. Item 1 should be ⚪ or 🔵 — an opening 🔴 costs composure and measures nothing the reader will not be asked again.

## 8. Required figures

**None.** `figures_planned: []`.

A mock exam is an instrument, not an explanation; nothing here builds a schema that a diagram would build faster. The two tables (score sheet, band interpretation) are tables, not figures, and need no anchors.

**Caution for drafting.** The `figure_anchors` rule in the structural contract has no `mock_exam` exemption. Any fenced block that visually depicts structure will fail lint without a `<!-- FIGURE: ch20-figNN-slug -->` anchor. Keep fenced blocks to manifests, commands, and command output — all of which are code and need no anchor — and the chapter stays at zero figures cleanly.

## 9. Open questions for the author

**1. Two B6 skeleton constraints for this chapter are stale and must not be drafted as written.** *(Blocking — this is the one that needs a decision before drafting.)*

The skeleton, written 2026-08-25, instructs the Instructions block to disclose that "the question count is commonly reported" and the instrument is "sized to that report rather than matched to a published figure," and instructs the Scoring Rubric to avoid stating a pass mark because "the 75% figure is unpublished." The 2026-08-31 provenance work superseded both. Shipped Ch 1 (lines 202–204, 341–342, 553–554) and drafted Ch 19 §3 (lines 535, 537) now state — with sources, and with a graded Ch 1 Practice item turning on the distinction — that both figures are published in the Linux Foundation's candidate handbook for multiple-choice exams as a class, just not on the product page. The `lf-mc-exam-important-instructions-2026-08-31` snapshot lists "The Linux Foundation does not publish a question count" among sentences that must not be written.

Drafting the skeleton's version would put the book's final chapter in direct contradiction with its first and its second-to-last. **Recommendation: draft to the current evidence state as planned in Blocks 1 and 4 above, and amend the B6 skeleton's Ch 20 entry to match.** Confirming this is the author's call; the plan above assumes yes.

Note that B3's related exclusion still holds on its own merits and is unaffected: no mock item should *test* the 60/75 figures, because exam mechanics are Ch 1 material and excluded from retrieval. What changed is how the chapter may describe them, not whether it may examine them.

**2. Question format beyond single-best-answer is undocumented.** No cached source mentions multi-select, "choose two," partial credit, or unscored pretest items for this exam. The plan defaults to four-option single-best and says nothing about other forms. If the research stage can cache a Linux Foundation or PSI page documenting the multiple-choice interface, the Instructions block can be specific and Ch 19 §3's navigation hedge collapses at the same time — the two share a source. Worth one targeted fetch, since it would improve two chapters.

**3. Should the book's final page carry a branded marker?** The plan is marker-free throughout, on the grounds that `mock_exam` is exempt and the instrument register is the point. But Ch 20 is the last page of the book, and 🏆 Safe Harbor exists precisely to mark arrival. Argument for: the reader who finishes deserves the beat, and the marker is the brand's own vocabulary for it. Argument against: Safe Harbor means *chapter completion*, Ch 19 already closed the teaching, and a trophy attached to a score the reader may have just failed lands badly. **Recommendation: leave it out**, and let the rubric's closing routing paragraph carry the ending plainly. Reversible either way; flagging because it is a brand-surface decision, not a drafting one.

**4. `the-lodestar.md` does not exist yet.** Ch 19 §5 is a walkthrough of a book-level artifact that has not been written, and Ch 19's own outline flagged this. Ch 20 does not depend on it — the rubric routes to Ch 19 §4 and to chapters, not to The Lodestar — so this is **not blocking for this chapter**. Recording it because Ch 20 is the last chapter in the pipeline and the artifact is `expected` in the structural contract's `required_book_artifacts`; after this chapter ships, it and the glossary are what stand between the book and assembly.

**5. Chapter size will exceed the single-generation ceiling.** Sixty stems plus 240 individual distractor refutations plus apparatus lands somewhere near 20,000 words — past the ~120KB threshold at which the drafting stage starts returning partial documents that the length guard rejects. `pipeline/incremental_draft.py` is the intended path and `run_chapters.sh` invokes it automatically, but this chapter has no H2 sections in the ordinary sense, so the H2 split will produce four very uneven blocks with `## Exam` and `## Mock Exam Answers & Walkthroughs` carrying nearly all of it. Worth verifying the splitter handles that shape before the run, or drafting the answer key in domain batches by hand.