All anchors confirmed. Emitting the audit to stdout per the pipeline's stage-output convention (the orchestrator writes `diagnostics/question-quality.md`).

---

```markdown
# Question-Quality Audit — Chapter 20

## Summary

- Chapter type: **mock_exam**
- Total questions inspected: **60**
  - 🧭 Soundings questions: **0** (correct — `mock_exam` is exempt; budget target is 0)
  - ☆ Taking Your Bearings questions: **0** (across 0 checkpoints — correct; exempt)
  - Practice questions: **60**
- Question budget compliance: **met on stems (60/60); answer key short by 1**
- Weak distractors (WARN): **7 questions** individually, plus **1 systemic pattern affecting all 60**
- Trap answers that don't target real misconceptions (WARN): **2 confirmed, 1 borderline**
- Missing or incomplete why-wrong explanations (FAIL): **1 missing entirely; 4 grouped rather than per-option**
- Retrieval-practice spacing: **compliant (by construction)**
- Soundings spoiler check: **N/A — no Soundings block, correctly**

**Ship-blocking finding, stated first:** 55 of the 60 correct answers are option **B**. A reader who notices the pattern — and on a 60-item run with the key adjacent, they will — scores 55/60 without reading a single stem. Every per-domain sub-score on the Scoring Rubric becomes uninterpretable, which destroys the one artifact this chapter exists to produce. Detail in **Systemic finding 1**.

---

## Question-budget compliance

Compared against `question_budget` in outline frontmatter.

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 0 | 0 | met |
| Taking Your Bearings (total) | 0 | 0 | met |
| Taking Your Bearings (checkpoints) | ≥2 | 0 | **N/A — `mock_exam` exempt from the two-checkpoint minimum** |
| Practice Questions | 60 | 60 stems / 59 walkthroughs | met on stems; **key short by 1** |

The exam block (`draft-v1.md:53–609`) contains 60 stems numbered 1–60 with no gaps. The answer key (`draft-v1.md:612–1201`) contains 59 entries, jumping from item 41 (`:1013`) to item 43 (`:1023`). Item 42 has no walkthrough. This is already flagged by an in-draft `AUTHOR-REVIEW` comment at `:1025`, which also supplies the intended answer (B), tags (D1.4 · Ch 2 §6 · 🔵) and distractor refutations — so the fix is transcription, not authoring.

---

## Soundings spoiler check

No 🧭 Soundings block exists in this chapter. This is **correct and required**, not an omission:

- B4 allocates 0 Soundings to `mock_exam`.
- The structural contract lists `mock_exam` under `exempt_chapter_types` for the 🧭 marker.
- A `mock_exam` chapter teaches no ★ Fixed Points, so there is nothing available to spoil.

Rules 7, 8 and 9 (spoiler-freedom, the 6+/3–5/0–2 rubric, `<details>` answer disclosure) are therefore **not applicable**. Their absence is not a FAIL.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| — | — | — | No Soundings block; chapter type exempt |

---

## Systemic findings

These affect the instrument as a whole rather than individual items, and they outrank every per-question issue below.

### Systemic 1 — Answer-position collapse: 55 of 60 correct answers are B (**FAIL**)

Tallied from the answer-key headers across `draft-v1.md:618–1193`, plus item 42's intended answer from the review comment at `:1025`:

| Option | Count | Items |
|---|---|---|
| A | 1 | 46 |
| **B** | **55** | all others |
| C | 3 | 2, 16, 53 |
| D | 1 | 13 |

**Why this is disqualifying rather than untidy.** The chapter's stated purpose is the per-domain score sheet — the Instructions block argues at `draft-v1.md:45–49` that this breakdown is "the only domain-level diagnostic available to you anywhere in this preparation." A score reachable by answering B sixty times is not a measurement of anything. A reader who half-notices the pattern gets an inflated total *and* inflated sub-scores, and the chapter then routes them to "you are looking for a date" (`:1248`) on the strength of it. An instrument that over-predicts readiness is worse than no instrument.

**Recommended fix:** permute option order on roughly 40 items to land near 15/15/15/15. Two cautions:

1. The answer key is letter-keyed in both the header (`**1. B**`) and every refutation bullet (`- **A is wrong** because…`). Permuting by hand across 60 items will introduce mismatches. Do this with a script that rewrites stem order and key letters together, then verify by re-deriving the tally.
2. Position permutation alone is insufficient — see Systemic 2.

### Systemic 2 — The correct answer is systematically the longest and most hedged option (**FAIL**)

Independent of position, option B is in most items visibly longer, more qualified, and more nuanced than its three rivals, which are short and absolute. Representative:

- **Q1** (`:55`) — B is a two-clause distinction; A, C, D are one short absolute clause each.
- **Q14** (`:183`) — B runs 30+ words explaining default-deny semantics; A, C, D run under 10.
- **Q41** (`:426`) — B names both mechanisms and their scopes; distractors are single assertions.
- **Q59** (`:590`) — B is the only non-absolutist option; A, C, D use "strictly," "eliminate," "all."

Test-wise candidates are explicitly trained on "longest, most qualified answer is usually correct." This tell survives any position permutation, so it must be fixed separately: pad the distractors to comparable length and grammatical complexity, or trim the correct answer. Roughly 45 items need option-length rebalancing.

### Systemic 3 — Domain distribution breaches skill Part 16's ±2 pp tolerance (**FAIL**)

Tallied from the per-question domain tags in the answer key, which the in-draft review comment at `:1219` designates authoritative.

| Domain | Blueprint | Target items | Actual items | Actual % | Deviation | Status |
|---|---|---|---|---|---|---|
| D1 Kubernetes Fundamentals | 44% | 26 | 26 | 43.3% | −0.7 pp | pass |
| D2 Container Orchestration | 28% | 17 | 18 | 30.0% | +2.0 pp | at the limit |
| D3 Cloud Native App Delivery | 16% | 10 | **7** | 11.7% | **−4.3 pp** | **FAIL** |
| D4 Cloud Native Architecture | 12% | 7 | **9** | 15.0% | **+3.0 pp** | **FAIL** |

**This correction is larger than the in-draft `AUTHOR-REVIEW` comment at `:1219` implies.** That comment says "the maximums (26/17/10/7) are correct… so the item lists are what need fixing." For D1 and D2 that is true. For D3 and D4 it is not: the D3 row lists 7 items because only 7 D3 questions were written, and the D4 row lists 9 because 9 D4 questions were written. No edit to the score sheet can make 7 authored D3 items into 10. **Three questions must be converted from D4/D2 to D3** (natural candidates: two more D3.2 debugging items from Ch 16, one more D3.1 from Ch 15), and two D4.2 items retired.

### Systemic 4 — Three competencies are effectively un-diagnosable (**FAIL**)

Competency roll-up, actual versus the outline's planned allocation:

| Competency | Planned | Actual | Δ |
|---|---|---|---|
| D1.1 | 15 | 15 | 0 |
| D1.2 | 3 | 5 | +2 |
| **D1.3** Scheduling | 3 | **1** | **−2** |
| D1.4 | 5 | 5 | 0 |
| D2.1 | 7 | 5 | −2 |
| D2.2 | 4 | 5 | +1 |
| D2.3 | 3 | 5 | +2 |
| D2.4 | 3 | 3 | 0 |
| D3.1 | 7 | 6 | −1 |
| **D3.2** Debugging | 3 | **1** | **−2** |
| D4.1 | 3 | 3 | 0 |
| D4.2 | 2 | 6 | +4 |
| **D4.3** Community & Collaboration | 2 | **0** | **−2** |

Three failures here, in descending severity:

1. **D4.3 has zero items.** The outline promised two, and gave the reasoning: B1 identifies Community and Collaboration as the competency technically-strong candidates most reliably under-study, and B2's stated mitigation was *disproportionate* representation in the mock. The chapter delivers none. All six non-observability D4 items are tagged D4.2. Q9 (`:127`, KCNA's stated purpose) and Q21 (`:246`, CNCF maturity levels) are plausibly D4.3 material mis-tagged as D4.2 — so part of this fix may be re-tagging rather than authoring, but at least one genuinely new D4.3 item is needed either way.
2. **D1.3 has one item** (Q31, taints). One item is noise, not a measurement. A reader who misses it cannot distinguish "I don't know scheduling" from "I misread one question."
3. **D3.2 has one item** (Q57, ephemeral containers). Same problem.

### Systemic 5 — Per-chapter floor and ceiling violated

The outline set a floor of 3 and ceiling of 5 items per content chapter, with the stated property that "no chapter the reader studied goes unmeasured."

| Ch | Planned | Actual | Status |
|---|---|---|---|
| 2 | 5 | 5 | ✓ |
| 3 | 4 | 3 | −1 |
| 4 | 4 | 3 | −1 |
| 5 | 4 | 3 | −1 |
| **6** | 3 | **7** | **over ceiling by 2** |
| **7** | 3 | **1** | **under floor by 2** |
| 8 | 3 | 5 | at ceiling, over plan by 2 |
| 9 | 4 | 4 | ✓ |
| 10 | 3 | 2 | −1 |
| 11 | 3 | 3 | ✓ |
| 12 | 4 | 3 | −1 |
| 13 | 3 | 5 | at ceiling, over plan by 2 |
| 14 | 3 | 3 | ✓ |
| 15 | 4 | 3 | −1 |
| **16** | 3 | **1** | **under floor by 2** |
| **17** | 4 | **6** | **over ceiling by 1** |
| 18 | 3 | 3 | ✓ |

Ch 7 and Ch 16 are effectively unmeasured. Moving two items from Ch 6 and one from Ch 17 into Ch 16 also repairs the D3.2 shortfall in Systemic 4 and part of the D3 deficit in Systemic 3 — one edit, three findings.

### Systemic 6 — Interleaving rule violated

The outline specified: no two consecutive items from the same chapter; no three consecutive from the same domain.

| Violation | Location | Detail |
|---|---|---|
| Six consecutive D1 items | Q1–Q6 (`:55–:108`) | The exam opens domain-blocked, which the outline explicitly forbade because it hands the reader a scope hint |
| Four consecutive D1 | Q22–Q25 (`:255–:290`) | |
| Three consecutive D2 | Q13–Q15 (`:174–:200`) | |
| Three consecutive D1 | Q31–Q33 (`:336–:362`) | |
| Three consecutive D1 | Q41–Q43 (`:426–:452`) | |
| Same chapter consecutive | Q58, Q59 (`:581`, `:590`) | Both Ch 17 §3, both D4.2, both 🔵, adjacent |

Item 1 is ⚪, satisfying the "open easy" rule. The "distribute the four hardest items" rule is moot — see Systemic 7.

### Systemic 7 — Difficulty skews easier than designed

| Level | Planned | Actual |
|---|---|---|
| ⚪ Foundation | 9 | **17** |
| 🔵 Standard | 36 | 32 |
| 🟡 Advanced | 13 | 11 |
| 🔴 Expert | 2 | **0** |

Nearly double the planned Foundation count and no Expert items at all. Compounding Systemics 1 and 2, the instrument scores more generously than the real exam in three independent ways. For a readiness instrument this is the wrong direction of error.

### Systemic 8 — Stray numbering artifact

`draft-v1.md:453` emits `**43 continues on the next item.**` between items 43 and 44. It is not a question, not a continuation, and refers to nothing. Delete. (Flagged by the review comment at `:1025`; noted here because it sits in the exam block a reader sees under timed conditions, where an unexplained line costs composure.)

---

## Per-question findings

### Q6 (`draft-v1.md:100`): "Which statement about a Kubernetes Namespace is correct?"

**Issue:** Two distractors encode the identical misconception, reducing the item to three effective options.

**Distractor analysis:**
- A) *provides kernel-level isolation between processes of different namespaces* — plausible; targets Linux-namespace/K8s-namespace conflation
- B) *scope for names; some kinds exist outside it* — **correct**
- C) *every resource kind is namespaced* — plausible; targets the cluster-scoped blind spot
- D) *same mechanism as the Linux namespaces that isolate a container* — **duplicate of A.** Same misconception, restated

**Why-wrong explanation status:** present, but `:675` refutes D with "for the same reason as A," which confirms the duplication in the key itself.

**Recommended fix:** replace D with a distinct misconception — e.g. *"deleting a Namespace leaves its objects intact under no Namespace"* (targets the real and consequential belief that namespace deletion is non-cascading).

---

### Q50 (`draft-v1.md:509`): "Which of the following is the correct expansion and meaning of SBOM?"

**Issue:** Three fabricated distractors, admitted as such in the key. Trap fidelity failure under Rule 2.

**Distractor analysis:**
- A) *Secure Boot Object Model* — not a real term; targets no misconception
- B) *Software Bill of Materials* — **correct**
- C) *Service Boundary Object Map* — not a real term
- D) *Standard Base Operating Manifest* — not a real term

**Why-wrong explanation status:** present but grouped, and self-defeating. `:1101` reads: *"A, C, and D are wrong as expansions. They are constructed to be plausible; none is a real term."* It then hands over the elimination heuristic outright: *"the correct expansion is the only one describing an inventory."* A reader who has never encountered SBOM answers this correctly from the key's own reasoning.

**Recommended fix:** rebuild as a discrimination item against neighbours the book actually taught — SBOM versus image digest versus provenance attestation versus vulnerability scan report. All four are real, all four are Ch 12 §7 material, and confusing them is a genuine and common failure.

---

### Q21 (`draft-v1.md:246`): "Which of these is the durable, testable fact about the CNCF project maturity levels?"

**Issue:** Solvable by test-wiseness with zero subject knowledge. B is the only option describing a *concept*; A, C, D all describe *point-in-time data*. The odd-one-out structure gives it away.

**Distractor analysis:**
- A) *the current list of Graduated projects* — category: data
- B) *the ordered progression Sandbox → Incubating → Graduated* — **correct**; category: concept
- C) *the number of projects at each level* — category: data
- D) *the date each project graduated* — category: data

**Why-wrong explanation status:** grouped (`:819`), though the grouping is defensible here since all three share one category error.

**Additional note:** the stem asks what is *durable and testable* — a question about study strategy, not about CNCF governance. The outline's intent (B1 trap 99, B3) was to *test the levels and their order* rather than the roster. This item tests whether the reader knows which facts are worth memorising, which is not a D4.2 curriculum objective.

**Recommended fix:** rewrite to test the thing itself — *"A project has completed a public security audit, demonstrated production adoption by multiple organisations, and been approved by the TOC. Which maturity level has it reached?"* with the other three levels as distractors. Retains the durable fact, removes the category tell, converts a meta-question into a curriculum question.

---

### Q59 (`draft-v1.md:590`): "A microservices architecture is chosen over a monolith. Which trade-off is the honest characterization?"

**Issue:** All three distractors are absolutist and eliminable without domain knowledge — the sharpest single instance of Systemic 2.

**Distractor analysis:**
- A) *strictly simpler to operate* — "strictly" flags it
- B) *independent deployment and scaling, at the cost of operational and network complexity* — **correct**; the only hedged option
- C) *eliminate the need for observability tooling* — "eliminate" flags it
- D) *remove all coupling* — "all" flags it

**Why-wrong explanation status:** present and specific for all three (`:1187–:1191`). The explanations are fine; the options are not.

**Recommended fix:** replace with defensible-but-wrong positions a real practitioner might hold — e.g. *"Microservices reduce total system complexity by decomposing it"* (true-sounding, and the exact error the fallacy of decomposition produces).

---

### Q16 (`draft-v1.md:201`): "Correct order of the three gates"

**Issue:** Distractors are excellent — three genuine permutations, each tempting to a reader with the order muddled. The **why-wrong is the problem**.

**Why-wrong explanation status:** grouped, not per-option. `:771` reads in full: *"A, B, and D are wrong as orderings. The sequence is not arbitrary: you cannot authorize an unidentified requester, and admission controllers act on an object that has already cleared permission."*

A reader who chose A (admission first) gets a general principle, not a refutation of their specific ordering. Rule 3 and the outline's own Block 3 spec require per-distractor refutation.

**Recommended fix:** three bullets. A — admission cannot run first because it inspects an object whose submitter is unidentified and unauthorised. B — admission cannot precede authorisation because a mutating webhook would then modify an object the requester may not be permitted to create. D — authorisation cannot precede authentication because there is no identity to evaluate policy against.

---

### Q13 (`draft-v1.md:174`): "Four-layer cloud native security model — outermost layer"

**Issue:** Minor. Distractors are sound (all four real layer names; each tempting to a reader with the ordering unsettled). Why-wrong groups B and C at `:744`: *"B and C are wrong because they are the middle two, in that order inward."*

**Why-wrong explanation status:** present but grouped. The grouping does uniquely place both, so information is not lost — this is a style deviation from the per-option rule rather than a gap.

**Recommended fix:** split into two bullets. Low priority relative to everything above.

---

### Q30 (`draft-v1.md:327`) and Q46 (`draft-v1.md:473`): thin single distractors

- **Q30 D)** *"golden signals apply to infrastructure and RED applies only to databases"* — arbitrary rather than misconception-derived; no candidate believes this. Replace with *"RED is the client-side view and the golden signals the server-side view"* (a real and tempting mis-framing).
- **Q46 B)** *"labels and annotations are interchangeable; the distinction is stylistic"* — weak, and phrased as a dismissal a reader recognises as the wrong answer's voice. Replace with *"annotations can be used in selectors when labels would exceed the 63-character value limit"* — plausible, specific, and false.

Both have complete per-option why-wrong explanations. Distractor quality only.

---

### Questions with exemplary architecture (no action)

Worth recording so the fixes above don't disturb them: **Q12** (`:154`, four Pod-phase failure signatures, each distractor a distinct real confusion), **Q26** (`:291`, targets the RWO-means-one-Pod misconception directly), **Q57** (`:572`, A is the exact wrong instinct a practitioner has), **Q11** (`:145`, the key at `:723` correctly identifies A as the most common belief about StatefulSets), and **Q53** (`:536`) — whose grouped explanation is *correct by design*, since a negative stem requires explaining why the three non-answers are all plausible.

---

## Retrieval-practice spacing

- Chapter 20 target: 20–25% of checkpoint questions from earlier chapters
- Actual: **100% of all 60 questions draw on chapters 2–18**
- Tagged `[retrieval: chN]`: **0**
- Status: **compliant (by construction)**

The template's ratio is not computable here — there are no checkpoints, so the denominator is zero, and a mock exam is a pure retrieval event by definition. Coverage spans 17 prior chapters, far exceeding the spirit of Rule 4.

The absent `[retrieval: chN]` tags are **not a finding**. The answer key's `Ch N §M` tag on every walkthrough serves the same routing function and serves it better, since it resolves to a section rather than a chapter. No change recommended.

---

## Coverage vs concepts

A `mock_exam` introduces no concepts, so this section is adapted: it checks coverage of the outline's declared `kb_tags` rather than of newly-taught material. Competency coverage is reported in **Systemic 4** above.

### Commands declared in `kb_tags.commands`

| Command | Tested? |
|---|---|
| kubectl-get | yes — Q17 stem |
| kubectl-describe | **only as a distractor** (Q17 C) and in explanations; never a correct answer |
| kubectl-logs | yes — Q17 (correct answer, `--previous`) |
| kubectl-events | yes — Q17 D |
| kubectl-exec | yes — Q57 A |
| kubectl-debug | yes — Q57 (correct answer) |
| kubectl-port-forward | yes — Q57 D |
| kubectl-top | yes — Q27 stem |
| kubectl-apply | marginal — Q60 D only |
| kubectl-rollout-undo | yes — Q10 |
| kubectl-scale | **NO** |
| kubectl-drain | yes — Q23 |
| helm-install | marginal — Q28 references install-time override; no command tested |
| helm-rollback | yes — Q10 |
| crictl | **NO** |

Two declared commands are never tested. `crictl` is the more consequential omission: it is the tool a candidate reaches for when the kubelet is the suspect and `kubectl` cannot help, and Ch 13 teaches it as exactly that. A Ch 13 item is a natural home — though note Ch 13 is already at the ceiling with 5 items, so this trades against Systemic 5.

### Concepts declared in `kb_tags.concepts`

Five of six (`mock-exam-calibration`, `domain-weighted-assessment`, `per-domain-score-sheet`, `distractor-from-trap-inventory`, `exam-pacing`) are chapter *apparatus* or authoring machinery, not testable reader-facing content — and `exam-pacing` is correctly untested, since B3 excludes exam mechanics from retrieval. `confusion-pair-discrimination` is heavily exercised (Q8, Q12, Q19, Q29, Q34, Q53 among others). No action.

### Question-form mix versus the outline blueprint

| Form | Planned | Actual |
|---|---|---|
| Recall / identification | 15 | ~17 |
| Discrimination (confusion pair) | 22 | ~26 |
| Scenario / diagnostic | 15 | ~16 |
| **Manifest or output reading** | **8** | **1** (Q12 only) |

Only Q12 (`:154`) carries a fenced block. No item shows real command output — Q17 describes `kubectl get pods` output in prose rather than displaying it. Seven items short. This matters beyond bookkeeping: reading a manifest and reading `describe`/`get` output are distinct skills from recalling a definition, and the exam currently measures the second almost exclusively. Converting existing items is cheap — Q4 (QoS) and Q39 (surge arithmetic) both become stronger if the reader must extract the values from a manifest rather than being handed them in prose.

---

## Recommended fix order

1. **Permute answer positions** across ~40 items to reach ~15/15/15/15, by script, updating key headers and refutation letters together (Systemic 1).
2. **Rebalance option lengths** so the correct answer is not systematically longest (Systemic 2). Steps 1 and 2 together are the difference between a working instrument and a decorative one.
3. **Restore the Q42 walkthrough** from the review comment at `:1025`; delete the stray line at `:453`.
4. **Reallocate ~5 items** to fix D3/D4 (Systemic 3), D4.3/D1.3/D3.2 (Systemic 4), and the Ch 7 / Ch 16 floor (Systemic 5) — these overlap heavily; moving two Ch 6 items and one Ch 17 item into Ch 16 and Ch 7 addresses all three.
5. **Rebuild the score sheet item lists** from the corrected tags. Note Q31 and Q50 currently appear in **no row** (`:1213–:1216`), and Q9, Q12, Q48 appear in **two**, so a reader tallying by row counts 58 distinct items against a stated total of 60.
6. **Rewrite Q50 and Q59**; repair the Q16 why-wrong; replace Q6 option D, Q30 option D, Q46 option B.
7. **Re-sequence** to satisfy the interleaving rule, in particular breaking up the six-item D1 opening (Systemic 6).
8. Optional, lower value: add 2 🔴 items and convert two items to manifest-reading form (Systemics 7 and the form-mix shortfall).
```

---

**Audit complete.** Eight systemic findings and eleven per-question findings against a 60-item instrument.

The headline is not the missing item-42 walkthrough that the in-draft review comments already caught — it's that **55 of 60 correct answers are option B**, and the correct answer is also systematically the longest and most hedged option. Two independent test-wiseness tells stack, so a reader can score in the fifties without reading a stem, which makes every per-domain sub-score meaningless. Since the per-domain score sheet is the sole reason the chapter exists — the Instructions block argues it is the only domain-level diagnostic available anywhere in the book — this invalidates the instrument rather than blemishing it.

Two findings correct earlier in-draft notes rather than repeating them. The `AUTHOR-REVIEW` comment at `:1219` says the score-sheet maximums are right and only the item lists need fixing; that holds for D1 and D2, but D3 lists 7 items because only 7 D3 questions were written and D4 lists 9 because 9 were written, so three questions need reallocating, not just relabelling. And the outline's promised 2 items for D4.3 Community and Collaboration — the competency B1 flags as the most reliably under-studied — came out at zero.

Nothing was written to disk; per this repo's executor configuration the stage output above flows through stdout for the orchestrator to capture as `diagnostics/question-quality.md`.