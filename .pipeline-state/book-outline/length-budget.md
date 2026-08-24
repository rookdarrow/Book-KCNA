No prior `length-budget.md` exists in any book repo, so this is the first instance of the retired-word-budget format. Emitting to stdout for the orchestrator to capture.

---

```markdown
# Question Budget — KCNA

**Book:** Kubernetes and Cloud Native Associate
**Exam:** KCNA (CNCF / The Linux Foundation), curriculum effective 2025-11-24
**Stage:** B4 — Question Budget
**Date:** 2026-08-23
**Input:** Stage B2 chapter lineup (20 chapters — 1 orientation, 17 content, 1 synthesis, 1 mock)

> **Word-count budgets were retired 2026-04-24** (style-decisions.md § "Length Budgets").
> This file produces no word targets. Chapters and sections are whatever length the
> material requires. The filename is retained for pipeline compatibility only.

---

## Per-chapter question budget

Per skill v5.3 Part 8 "Practice-Question Budget":

- **Floor: 300 questions per book.**
- **Mock Exam** (final chapter): matches real exam size (or performance-task count for performance-based exams)
- **Soundings**: 8 per content chapter; 5 per orientation/synthesis; 0 per mock_exam
- **Taking Your Bearings**: minimum 10 per content chapter (across ≥2 checkpoints)
- **Practice Questions** (end-of-chapter): `(300 − mock_exam − soundings_total − bearings_total) × domain_weight_pct / 100`

### The formula returns a negative pool for this book — see § "Practice-question derivation"

```
mock_exam        = 60   (commonly reported; NOT published — see Caveats)
soundings_total  = 146  (17×8 content + 5 orientation + 5 synthesis)
bearings_total   = 180  (17×10 content + 5 orientation + 5 synthesis)

in-chapter practice pool = 300 − 60 − 146 − 180 = −86
```

The fixed baselines alone total **326** questions, clearing the 300 floor before a
single end-of-chapter Practice Question is written. B2 anticipated this
("306 from fixed baselines alone… cleared with substantial headroom"). Because 300
is a **floor, not a cap** — and the skill's own CAPM worked example lands at 351 —
the literal subtraction is not the operative rule here. The derivation used instead
is stated below and is weight-proportional in exactly the way the formula intends.

### Budget table

| # | Title | Type | Weight % | Soundings | Bearings | Practice Qs | Total |
|---|---|---|---|---|---|---|---|
| 1 | Taking Departure | orientation | — | 5 | 5 | 0 | 10 |
| 2 | Cargo in Standard Crates | content | 9 | 8 | 10 | 25 | 43 |
| 3 | The Ship's Company | content | 6 | 8 | 10 | 19 | 37 |
| 4 | Records of Intent | content | 6 | 8 | 10 | 19 | 37 |
| 5 | The Smallest Vessel | content | 7 | 8 | 10 | 21 | 39 |
| 6 | Fleets, Not Vessels | content | 6 | 8 | 10 | 19 | 37 |
| 7 | Assigning the Berth | content | 5 | 8 | 10 | 17 | 35 |
| 8 | Standing the Watch | content | 5 | 8 | 10 | 17 | 35 |
| 9 | Every Pod Has an Address | content | 7 | 8 | 10 | 21 | 39 |
| 10 | Traffic from Beyond the Cluster | content | 5 | 8 | 10 | 17 | 35 |
| 11 | Below the Waterline | content | 5 | 8 | 10 | 17 | 35 |
| 12 | Locks, Keys, and Watchstanders | content | 7 | 8 | 10 | 21 | 39 |
| 13 | When the Cluster Won't Answer | content | 4 | 8 | 10 | 15 | 33 |
| 14 | Packing for the Voyage | content | 5 | 8 | 10 | 17 | 35 |
| 15 | The Chart Is the Truth | content | 7 | 8 | 10 | 21 | 39 |
| 16 | Your Application, Their Cluster | content | 4 | 8 | 10 | 15 | 33 |
| 17 | The Fleet and Its Charts | content | 7 | 8 | 10 | 21 | 39 |
| 18 | Reading the Instruments | content | 5 | 8 | 10 | 17 | 35 |
| 19 | Bearings Before Landfall | synthesis | — | 5 | 5 | 10 | 20 |
| 20 | Full Mock Exam | mock_exam | — | 0 | 0 | 60 | 60 |
| **Total** | | | **100** | **146** | **180** | **389** | **715** |

---

## Practice-question derivation

Per-chapter Practice Questions are set by a weight-monotonic base formula bounded to
the skill's own per-chapter Practice Questions range (Part 15 chapter template:
"15-25 questions with interleaved topics"):

```
practice_qs(chapter) = 15 + 2 × (chapter_weight_pct − 4)
```

The lowest-weighted content chapter (4%) lands on the template's floor of 15; the
highest (9%) lands on its ceiling of 25. Nothing is clipped.

| Weight % | Practice Qs | Chapters |
|---|---|---|
| 4 | 15 | 13, 16 |
| 5 | 17 | 7, 8, 10, 11, 14, 18 |
| 6 | 19 | 3, 4, 6 |
| 7 | 21 | 5, 9, 12, 15, 17 |
| 9 | 25 | 2 |

**Content-chapter practice total:** 25 + 19 + 19 + 21 + 19 + 17 + 17 + 21 + 17 + 17 + 21 + 15 + 17 + 21 + 15 + 21 + 17 = **319**

### The derivation reproduces the published domain weights

The point of the skill's formula is that end-of-chapter practice volume tracks
domain weight. This derivation satisfies that to within 1.1 points on every domain:

| Domain | Published weight | Practice Qs | Share of practice pool | Deviation |
|---|---|---|---|---|
| D1 Kubernetes Fundamentals (Ch 2–8) | 44% | 137 | 42.9% | −1.1 |
| D2 Container Orchestration (Ch 9–13) | 28% | 91 | 28.5% | +0.5 |
| D3 Cloud Native Application Delivery (Ch 14–16) | 16% | 53 | 16.6% | +0.6 |
| D4 Cloud Native Architecture (Ch 17–18) | 12% | 38 | 11.9% | −0.1 |
| | **100%** | **319** | **100%** | |

Arithmetic check — D1: 25+19+19+21+19+17+17 = 137 · D2: 21+17+17+21+15 = 91 ·
D3: 17+21+15 = 53 · D4: 21+17 = 38 · 137+91+53+38 = **319**. ✓

---

## Mock Exam composition (Ch 20)

KCNA is a **multiple-choice exam, not performance-based** — it is the CNCF's
associate-tier written credential, distinct from the performance-based CKA/CKAD/CKS.
The mock is therefore a full-length multiple-choice instrument, not a task walkthrough.

Domain distribution, weighted to the 2025-11-24 blueprint and held inside the skill's
±2 percentage-point tolerance:

| Domain | Target weight | Mock Qs | Actual share | Deviation |
|---|---|---|---|---|
| D1 Kubernetes Fundamentals | 44% | 26 | 43.3% | −0.7 pp |
| D2 Container Orchestration | 28% | 17 | 28.3% | +0.3 pp |
| D3 Cloud Native Application Delivery | 16% | 10 | 16.7% | +0.7 pp |
| D4 Cloud Native Architecture | 12% | 7 | 11.7% | −0.3 pp |
| **Total** | **100%** | **60** | **100%** | |

Arithmetic check: 26 + 17 + 10 + 7 = **60**. ✓

Time budget stated in-chapter: **90 minutes**, matching the published exam duration
(the one exam-mechanics figure the Linux Foundation *does* publish).

---

## Totals

- **Total content chapters:** 17 (Ch 2–18)
- **Total chapters:** 20 (1 orientation, 17 content, 1 synthesis, 1 mock exam)
- **Soundings:** 146 — (17 × 8) + (2 × 5) = 136 + 10
- **Taking Your Bearings:** 180 — (17 × 10) + (2 × 5) = 170 + 10
- **Practice Questions:** 389 — 319 content + 10 synthesis + 60 mock
- **Grand total:** 146 + 180 + 389 = **715 questions**
- **Against the 300-question floor:** cleared by **415 questions (238% of floor)**

Fixed baselines alone (Soundings + Bearings, 326) clear the floor without any
end-of-chapter practice. This is headroom by design: the Stage 8 question-quality
audit is expected to cut weak items, and a book that only just meets the floor
pre-audit falls below it post-audit.

### Bearings minimums are minimums

The table records **10** Bearings per content chapter because that is the skill's
floor, distributed across ≥2 checkpoints of ≥5 each. Chapters carrying more than one
major conceptual arc will run 3 checkpoints and land at 12–15. Outlines should treat
the 10 as a contract to exceed, not a target to hit. Chapters where this is most
likely, based on the B2 objective loads:

- **Ch 8** (kubectl surface / API gates / node lifecycle / version skew — four unrelated arcs)
- **Ch 12** (security lifecycle / RBAC / ServiceAccounts / Secrets / PSS / supply chain / policy engines)
- **Ch 17** (cloud native definition / extension points / mesh / serverless / autoscaling / CNCF governance)

### Retrieval-practice spacing draws from this budget, not on top of it

Per skill Part 10, 20–25% of later checkpoints test earlier content. Those questions
are **allocated within** each chapter's Bearings and Practice counts above, not added
to them. Schedule for this book:

| Chapter range | Share of questions drawn from earlier chapters |
|---|---|
| Ch 4–5 | ~10% (from Ch 2–3) |
| Ch 6–8 | ~15% (from Ch 2–5) |
| Ch 9–13 | ~20% (from Ch 2–8) |
| Ch 14–18 | 20–25% (from all previous) |
| Ch 19 | ~100% — the synthesis chapter's 20 questions are cross-domain by definition |

---

## Caveats

- **No content chapter lands at 0 Practice Questions.** The minimum is 15 (Ch 13, Ch 16),
  which is the skill's own per-chapter floor. No redistribution is required.
- **The literal formula returns −86 and is not usable for this book.** It is written for
  books whose mock exam consumes most of the 300 floor (CAPM's 150-question mock leaves
  150). KCNA's 60-question mock is small relative to a 17-content-chapter lineup, so the
  fixed baselines overshoot the floor on their own. The derivation in
  § "Practice-question derivation" is substituted; it preserves the formula's *intent*
  (practice volume ∝ domain weight, verified to within 1.1 points on all four domains)
  while bounding per-chapter counts to the skill's stated 15–25 range. **Flagged for
  skill maintenance:** Part 8's formula should be restated as a floor-check plus a
  weight-proportional allocation, since the subtraction goes negative for any book with
  ≥13 content chapters and a mock under ~100 questions.
- **Mock exam size (60) is *commonly reported*, not published.** The Linux Foundation does
  not publish KCNA's question count or passing score (B1 gap G34; B2 disclosure #2).
  Chapter 20 must frame itself as a **calibrated instrument sized to the commonly
  reported 60-question / 90-minute format**, never as a match to a published count.
  If the LFS250 syllabus fetch (G37) surfaces an authoritative count, revise this file
  before Ch 20 drafts — the mock's *domain proportions* would not change, only its size.
- **Per-chapter weight percentages are authored judgment, not CNCF data** (B1 gap G33;
  B2 disclosure #1). CNCF publishes four domain weights and no sub-competency weights.
  Every Practice Qs figure in this file inherits that uncertainty. If G37 revises the
  per-chapter weights, re-run this stage — the derivation is a pure function of them.
- **The 2025-11-24 blueprint change affects question sourcing, not just counts**
  (B2 disclosure #3). Observability is no longer a standalone domain; D2 rose 22→28%
  and D3 doubled 8→16%. Practice questions harvested from pre-2025 third-party material
  will be mis-weighted. Ch 14–16 (D3) in particular need originally authored items —
  53 of them — because the old blueprint under-served that domain.
- **14 of B1's 114 traps are `[inferred]`, not `[source]`.** Trap-answer distractors built
  on those must be described as "easy to confuse," never "frequently tested," per
  Ethical Guardrail #8. This constrains question *framing*, not question *count*.
- **This file no longer produces or enforces word targets.** Length is content-driven
  (decision 2026-04-24). Any downstream stage still reading `words_target` or
  `calculated_length_words` from this file will find neither.

---

*Stage B4 complete. 715 questions budgeted against a 300 floor — 146 Soundings,
180 Bearings, 319 chapter Practice, 10 synthesis, 60 mock. Practice allocation
reproduces published domain weights to within 1.1 points. Formula override documented
and flagged for skill maintenance.*
```

---

**Two things worth your attention before B5:**

1. **The skill's Part 8 formula is broken for this book shape** — it returns a negative practice pool (−86) for any book with enough content chapters that `8+10` baselines exceed `300 − mock_size`. KCNA is the first book in the catalog to trip it. I substituted a weight-proportional derivation that verifiably reproduces the 44/28/16/12 split, but the formula itself should be restated in the skill as *floor-check plus allocation* rather than *subtraction*.

2. **The mock exam's 60-question size is the only soft number here.** If the LFS250 syllabus fetch (B1 gap G37) turns up an authoritative count, only Chapter 20's size changes — the per-chapter budget is independent of it under this derivation.