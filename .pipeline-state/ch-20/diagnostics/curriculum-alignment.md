All tallies verified against the file. The research manifest's "No curriculum gaps" line is decisive — it removes Rule 3's escape hatch for every finding below.

Per the pipeline contract in CLAUDE.md (`Write` is removed from `--allowed-tools` so stage output flows through stdout for atomic capture), here is `diagnostics/curriculum-alignment.md`:

---

# Curriculum-Alignment Audit — KCNA Chapter 20

**Draft audited:** `.pipeline-state/ch-20/draft-v1.md` (1250 lines, 68KB). Line references are to that file.
**Authority:** `cncf-curriculum-kcna-readme-2026-08-31.md` (domain weights) and `cncf-kcna-curriculum-pdf-2026-08-23.md` (competency enumeration). The latter was **not** in this stage's packed source set; I read it from `../Book-KCNA/sources/` rather than treat the competency IDs as unverifiable. It confirms all thirteen IDs the outline uses.

**Method note.** For a `mock_exam` chapter, "coverage" is not prose about an objective — it is *items tagged to it*, because the answer-key tag is what drives the score sheet and routes a wrong answer back to a page. So coverage = item count, and depth = item count against published weight, plus the cognitive level at which the item assesses. All counts below are transcribed from the 59 answer-key tag lines (618–1193) and verified twice; item 42 has no walkthrough and is counted at the value its own AUTHOR-REVIEW note (line 1033) specifies, `D1.4 · Ch 2 §6 · 🔵`.

**Headline:** the domain distribution does not match the CNCF blueprint. D3 is under-weighted by 3 items (−4.3 pp), D4 over-weighted by 2 (+3.0 pp), and **D4.3 has zero items** against an outline promise of 2. Two of those three exceed skill Part 16's ±2 pp tolerance.

---

## Objectives the outline claims to cover

Descriptions are verbatim competency names from the curriculum PDF (line 13–16). CNCF publishes weights at **domain** level only; there are no published competency sub-weights, so the per-competency targets in the depth section are the book's own (B4-derived), clearly marked.

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.1 | Kubernetes Core Concepts | YES — 15 items | appropriate |
| D1.2 | Administration | YES — 5 items | over-covered (+2 vs plan) |
| D1.3 | Scheduling | **partial — 1 item** | **shallow** |
| D1.4 | Containerization | YES — 5 items (incl. orphaned 42) | appropriate |
| D2.1 | Networking | YES — 5 items | under-covered (−2 vs plan) |
| D2.2 | Security | YES — 5 items | over-covered (+1 vs plan) |
| D2.3 | Troubleshooting | YES — 5 items | over-covered (+2 vs plan) |
| D2.4 | Storage | YES — 3 items | appropriate |
| D3.1 | Application Delivery | YES — 6 items | under-covered (−1 vs plan) |
| D3.2 | Debugging | **partial — 1 item** | **shallow** |
| D4.1 | Observability | YES — 3 items | appropriate |
| D4.2 | Cloud Native Ecosystem and Principles | YES — 6 items | **over-covered (+4 vs plan)** |
| D4.3 | Cloud Native Community and Collaboration | **NO — 0 items** | **—** |

**D4.3 is the hard failure.** The outline committed to 2 items ("Ch 17's four items split 2 D4.2 / 2 D4.3, which is B2's promised disproportionate representation for Community and Collaboration"). All six Ch 17-sourced items — 9, 21, 44, 55, 58, 59 — are tagged D4.2. The competency B1 identifies as the one technically-strong candidates most reliably under-study is the one competency this instrument cannot measure at all. A reader with a total D4.3 blind spot scores identically to one who has mastered it.

This is **not** shielded by Rule 3. The research manifest states flatly at line 396: *"No curriculum gaps — All thirteen competencies are sourced by the existing 303-snapshot library."* The corpus carries `cncf-charter-governance-bodies`, `cncf-code-of-conduct`, `cncf-mentoring-and-community-groups`, `cncf-tags-current-structure`, `cncf-toc-and-tags`, and `cncf-who-we-are`. The sources for D4.3 are cached and unused.

---

## Objectives covered in the draft but NOT in the outline

**1. Item 9 (line 127) tests the credential, not the curriculum — drift.**

> "Which of the following is the CNCF's stated purpose for the KCNA-level tier of certification, as reflected in the curriculum's own description?"

The correct answer is a quotation *about the certification*. Neither D4.2 ("Ecosystem and Principles") nor D4.3 ("Community and Collaboration") covers the purpose of an exam tier; this is Ch 1 material. It contradicts the outline's own Block 2 rule — *"No question tests exam mechanics… The mock tests the curriculum, not itself"* — and B3 excludes exam mechanics from retrieval entirely. Under Rule 1 this is drift, not a pass. Its distractor set (CKA/CKAD/CKS scoping) is legitimate ecosystem knowledge and could be salvaged into a genuine D4.2 or D4.3 item, but the stem as written must go.

**2. Item 33 (line 354), version skew, is at the scope boundary — author judgment.** Tagged `D1.2 · Ch 8 §6 · 🟡`. Version-skew policy is CKA-depth administration. The curriculum PDF names the competency "Administration" with no sub-detail, so the snapshot cannot adjudicate it and I am not calling it drift. Flagging only so the author can confirm associate-tier intent.

**3. Apparatus exposition drifts into Ch 19's owned territory — outline non-compliance, not curricular drift.** The outline's Block 1 spec says of both the console mechanics and the pacing rule: *"Ch 19 §3 owns this and the drafting must point rather than restate"* and *"Point, don't re-derive."* The draft restates both — the full Previous/Next/flag/Review-Screen mechanic at lines 31–37, and the 60%/54-minutes-of-90 rule at line 37 — and *then* cross-bears. Both blocks are `objectives: []` apparatus, so no objective is harmed, but the duplication is real.

**4. Positive finding — do not regress this.** The outline's Block 1 instructed the draft to write that real-console navigation is *"undocumented, confirmed absent across four official pages."* That instruction is stale, and `provenance-kcna-exam-interface-2026-08-31.md` lists that exact sentence as one that must not be written. **The draft correctly ignored the outline and drafted to the corrected evidence** (lines 31–37, citing `lf-examui-multiple-choice-2026-08-31`). Same for the 60/75 figures at lines 11–15. The revision stage must not "restore outline fidelity" here.

---

## Depth mismatches

### Domain level — against the published CNCF blueprint (authoritative)

| Objective | Exam weight | Items | Draft depth | Mismatch |
|---|---|---|---|---|
| D1 Kubernetes Fundamentals | 44% | 26 | 43.3% | OK (−0.7 pp) |
| D2 Container Orchestration | 28% | 18 | 30.0% | **over-covered (+2.0 pp)** |
| D3 Cloud Native Application Delivery | 16% | 7 | 11.7% | **under-covered (−4.3 pp)** |
| D4 Cloud Native Architecture | 12% | 9 | 15.0% | **over-covered (+3.0 pp)** |

D3 and D4 both breach skill Part 16's ±2 pp tolerance; D2 sits exactly on it. The outline's own table (26/17/10/7) is correct and matches the blueprint — **the draft did not execute it**. A reader whose weakness is application delivery is under-measured by 30%, in the domain that is 16% of the real exam.

### Competency level — against the book's own B4-derived targets

CNCF publishes no competency sub-weights. Targets below are the outline's roll-up, not CNCF's.

| Objective | Target | Actual | Δ |
|---|---|---|---|
| D1.1 Core Concepts | 15 | 15 | 0 ✓ |
| D1.2 Administration | 3 | 5 | +2 |
| D1.3 Scheduling | 3 | 1 | **−2** |
| D1.4 Containerization | 5 | 5 | 0 ✓ |
| D2.1 Networking | 7 | 5 | **−2** |
| D2.2 Security | 4 | 5 | +1 |
| D2.3 Troubleshooting | 3 | 5 | +2 |
| D2.4 Storage | 3 | 3 | 0 ✓ |
| D3.1 Application Delivery | 7 | 6 | −1 |
| D3.2 Debugging | 3 | 1 | **−2** |
| D4.1 Observability | 3 | 3 | 0 ✓ |
| D4.2 Ecosystem and Principles | 2 | 6 | **+4** |
| D4.3 Community and Collaboration | 2 | 0 | **−2** |

**D1.3 Scheduling at one item is the quietest serious gap.** Scheduling is one of four competencies inside the 44% domain, and Ch 7 carries 17 practice questions in B4. It is represented here by item 31 alone (NoExecute taint). Nothing tests nodeSelector, affinity/anti-affinity, resource-based filtering, or the scheduler's filter/score phases. Item 31 is also **absent from every row of the score sheet** (see below), so as shipped, D1.3 is not merely thin — it is unscorable.

**D2.1 Networking at 5 against 7** traces to Ch 10 supplying 2 items instead of 3, and item 14 (NetworkPolicy, line 747) being tagged D2.2 though its owning section Ch 10 §6 is a networking section.

### Cognitive level — the instrument is measurably easier than calibrated

| Difficulty | Planned | Actual | Δ |
|---|---|---|---|
| ⚪ Foundation | 9 | 17 | **+8** |
| 🔵 Standard | 36 | 32 | −4 |
| 🟡 Advanced | 13 | 11 | −2 |
| 🔴 Expert | 2 | **0** | −2 |

Foundation items are nearly double plan and no Expert item exists. This is a depth finding with consequence, not a bookkeeping one: the Scoring Rubric interprets the reader's raw score against the published 75% standard (line ~1223), so an instrument skewed easy inflates confidence at precisely the point the chapter exists to give an honest reading. Rule 2 — over-coverage flagged as loudly as under.

**Assessment form.** The outline planned 8 manifest/output-reading items concentrated in D1.1 and D2.1. The draft contains **one** (item 12, the YAML block at lines 154–163 — the only fenced block in the entire exam). D1.1 and D2.1 are therefore assessed almost entirely through prose recognition. Reading a manifest is a real assessed skill under Core Concepts; at 1/8 of plan, the draft measures recall where it intended to measure interpretation.

### Score-sheet arithmetic — and a misdiagnosis in the draft's own note

The AUTHOR-REVIEW comment at line 1219 says the maxima are correct "so the item lists are what need fixing." **That is half right and the half it gets wrong matters.** The lists do contain bookkeeping errors, but correcting them cannot reconcile to 26/17/10/7, because the underlying item composition is off-blueprint. Both must be fixed.

Bookkeeping errors, verified:

- Items **9, 12, 48** appear in both the D1 row (1213) and their true rows. Answer key is authoritative: 9 = D4.2, 12 = D2.3, 48 = D2.1. Remove all three from D1.
- Item **31** (D1.3) appears in **no row**. Add to D1.
- Item **50** (D2.2) is missing from the D2 row (1214). Add to D2.
- Item **42** is listed in D1 but has no walkthrough (gap at line 1023, between 41 and 43).

Corrected lists **as drafted** (bookkeeping only, composition untouched):

| Domain | Corrected items | Count | Stated max |
|---|---|---|---|
| D1 | 1,2,3,4,5,6,11,16,22,23,24,25,29,31,32,33,38,39,41,42,43,45,46,51,52,60 | 26 | 26 ✓ |
| D2 | 7,8,12,13,14,15,17,19,20,26,27,34,36,37,48,50,53,56 | 18 | 17 ✗ |
| D3 | 10,18,28,35,47,54,57 | 7 | 10 ✗ |
| D4 | 9,21,30,40,44,49,55,58,59 | 9 | 7 ✗ |

### Routing defects in the answer-key tags

The tag line is what routes a wrong answer back to a page; a wrong pointer defeats the score sheet's entire remediation function.

- **Item 15** (line 757) is tagged `D2.2 · Ch 4 §4` but its walkthrough cross-bears to **Ch 12 §4** for the claim. A Security-competency item routes the reader to a Core Concepts section.
- **Item 14** (line 747) is tagged `D2.2` with owning section `Ch 10 §6`, a networking section the blueprint assigns to D2.1.

### Interleaving — secondary, but it affects measurement validity

The outline required no two consecutive items from one chapter and no three consecutive from one domain. Violations:

- **Items 1–6 are six consecutive D1 items.** This is exactly the domain-blocked opening the outline forbade, and it hands the reader a scope hint across the first tenth of the exam.
- Further runs: 12–15 (four D2), 22–25 (four D1), 31–33 (three D1), 41–43 (three D1).
- Consecutive same-chapter: **7–8** (both Ch 9), **24–25** (both Ch 6), **58–59** (both Ch 17 **§3** — same section, adjacent).
- Item 1 is ⚪, satisfying the opening-difficulty rule ✓.

---

## Gaps the research stage flagged

The manifest's five gaps (lines 370–394) are all exam-mechanics gaps; it records **no curriculum gaps**. Handling:

| Gap | Handled correctly? | Evidence |
|---|---|---|
| G1 — single-best vs multi-select UNPUBLISHED | **YES** | Instructions block is silent on item format. Manifest ratified silence as the right call; the draft does not upgrade the authoring choice into a claim. |
| G2 — number of options per item UNPUBLISHED | **YES** | Four-option form used throughout without any statement that the real exam uses four. |
| G3 — unscored/pretest items UNPUBLISHED | **YES** | No mention anywhere. |
| G4 — penalty for wrong answers UNPUBLISHED | **YES** | The banned premise ("no penalty for a wrong answer") appears nowhere. Guessing advice is absent rather than unsourced. |
| G5 — whether check-in consumes exam time | **YES (n/a)** | Ch 20 does not depend on it; not raised. |

Also correctly discharged from the manifest's author notes:

- **Note 5** — the Pause Exam mechanic ("does not stop the timer") is present at line 37 with the right citation. ✓
- **Note 6** — the ExamUI page's malformed prose is paraphrased, not quoted. ✓
- **Note 3 / Open Question 1** — Blocks 1 and 4 drafted to current evidence, citing `lf-mc-exam-important-instructions-2026-08-31` and `lf-mc-exam-faq-2026-08-31`. ✓
- **B1 trap 99 / B3** — item 21 correctly tests the *maturity levels* rather than the dated Graduated roster, and its rationale tells the reader outright that memorising a roster is misdirected effort. ✓ Exemplary handling; keep.

**Two open dependencies, neither a Ch 20 defect:**

1. **Ch 19 §3 must be corrected before either chapter ships.** `ch-19/draft-v2.md:541` asserts the LF does not publish console behaviour — a sentence the corpus lists as false. Ch 20's Instructions block cross-bears into that section twice (lines 35, 37). Ch 20 is right and Ch 19 is wrong; shipping as-is reproduces the contradiction Open Question 1 was raised to prevent.
2. **The B6 skeleton's Ch 20 entry is stale** and still instructs future stages to call the 60/75 figures unpublished. Amend it, or a later retroactive sweep will reintroduce the error.

---

## Recommended fixes

Ordered by severity. Fixes 1–5 close the arithmetic to exactly 60 items at 26/17/10/7.

**1. Cover D4.3 — write 2 Cloud Native Community and Collaboration items.** Zero coverage of a claimed objective, with sources cached and unused. Draw from `cncf-charter-governance-bodies`, `cncf-tags-current-structure` / `cncf-toc-and-tags` (TOC and TAG structure), `cncf-code-of-conduct`, or `cncf-mentoring-and-community-groups` (contributor pathways). Tag `D4.3 · Ch 17 §<n>`. This is the single highest-value fix: it restores B2's promised disproportionate representation for the competency B1 names as most reliably under-studied.

**2. Retire item 9 (line 127).** Tests the credential rather than the curriculum; violates the outline's Block 2 rule and B3's exclusion. Its CKA/CKAD/CKS distractor material can be rebuilt as a D4.2 ecosystem item if the author wants to keep it. D4.2 → 5.

**3. Retire 2 more D4.2 items to reach the 12% weight.** Take one of the adjacent Ch 17 §3 pair — **58 or 59** (same section, consecutive, redundant construct) — and one of {21, 44, 55}. With fix 1 this lands D4 at 7: D4.1 3 · D4.2 2 · D4.3 2.

**4. Retire item 53 (line 536), keep item 12.** Both are Ch 13 §2 and test the same Pending / ImagePullBackOff / CrashLoopBackOff discrimination from two sides. Keep 12 specifically because it is the exam's only manifest-reading item. D2 → 17 ✓.

**5. Add 3 D3 items into the freed slots.** Two × **D3.2 Debugging** sourced to Ch 16 (target 3, actual 1 — Ch 16 has 15 B4 practice questions and one mock item), one × **D3.1** sourced to Ch 15 (target 4, actual 3). D3 → 10 ✓. Net across fixes 2–5: −1 D2, −2 D4, +3 D3, D1 unchanged at 26.

**6. Restore item 42's walkthrough and delete the stray line 453.** The draft's own note at line 1033 specifies the content: answer B, `D1.4 · Ch 2 §6 · 🔵`, with the three distractor refutations already written out. Delete `**43 continues on the next item.**` at line 453. Renumber nothing.

**7. Rebuild the score-sheet rows (line 1213–1216) from the answer-key tags after fixes 1–6, and delete the AUTHOR-REVIEW comment at 1219.** Its premise is wrong — the maxima and the composition were both off, not just the lists. Ensure item **31** appears; as drafted it is in no row and therefore unscorable.

**8. Rebalance D1.3 Scheduling from 1 item to 3.** Convert 2 of the 5 Ch 8 items (D1.2, target 3) into Ch 7 scheduling items — nodeSelector/affinity, or the scheduler's filter-and-score phases. Domain total unaffected; this is an internal D1 correction.

**9. Rebalance D2.1 from 5 to 6.** Retag item 14 (line 747) from `D2.2` to `D2.1` — its owning section Ch 10 §6 is a networking section and the blueprint assigns Ch 10 to D2.1. Boundary call (NetworkPolicy is genuinely both), but it moves both competencies toward target. Then convert one of the remaining Ch 13 items to a Ch 10 item to reach D2.1 7 / D2.3 3.

**10. Fix item 15's owning section** (line 757): `D2.2 · Ch 4 §4` → `D2.2 · Ch 12 §4`, matching the section its own walkthrough cross-bears to.

**11. Raise the difficulty floor.** Convert ~8 ⚪ items to 🔵 by deepening the stems, and author the 2 planned 🔴 items. As drafted the instrument reads easier than the outline calibrated, which biases the reader's readiness signal optimistic against a rubric anchored to the published 75% standard.

**12. Convert ~7 prose items to manifest/output-reading form** in D1.1 and D2.1, per the outline's planned 8. Manifests and command output are code and need no `FIGURE:` anchor, so this stays at zero figures cleanly — but keep ASCII structure diagrams out, since the contract has no `mock_exam` exemption for figure anchors.

**13. Reorder for interleaving.** Break the D1 run at items 1–6 first; then the runs at 12–15, 22–25, 31–33, 41–43, and the same-chapter adjacencies at 7–8, 24–25, 58–59. Keep item 1 at ⚪/🔵. Structural rather than curricular — sequence after the composition fixes, or the work is done twice.

**14. Trim the restated apparatus** at lines 31–37 back to a pointer, per the outline's "point, don't re-derive." **Preserve the corrected console and 60/75 facts** — the draft is right and the B6 skeleton is stale. Amend the skeleton's Ch 20 entry rather than the chapter.