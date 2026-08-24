```markdown
---
chapter: 1
chapter_type: "orientation"
title: "Taking Departure"
subtitle: "Ninety minutes, four domains, and a curriculum that moved"
exam_domain: "None — orientation chapter, no domain objectives"
domain_weight_pct: 0
complexity: "mixed"
novelty: "moderate"
prereq_factor: "light"

# --- Section plan (no word budgets) ---
# Length is content-driven. Arc-outline depth band for this chapter: "focused" —
# an orientation chapter earns its keep by being short enough to actually read
# before Chapter 2. That is a relative planning signal, NOT a target.
sections:
  - name: "What the KCNA Is, and Who It's For"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Ninety Minutes: The Exam as Published"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "The Curriculum That Moved Under Everyone's Feet"
    objectives: []
    requires_figure: true
    figure_anchor: "ch01-fig01-blueprint-change-2025"
    checkpoint_after: true
  - name: "The Phrase We Haven't Defined Yet"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "How This Book Is Built"
    objectives: []
    requires_figure: true
    figure_anchor: "ch01-fig02-book-map-parts-to-domains"
    checkpoint_after: false
  - name: "Three Ways to Read This Book"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true

# --- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ---
soundings_planned:
  question_count: 5
  topics:
    - "container-vs-virtual-machine intuition"
    - "what Kubernetes is (orchestrator vs runtime)"
    - "who governs Kubernetes (CNCF / Linux Foundation / vendor)"
    - "what 'cloud native' is commonly assumed to mean"
    - "prior exposure to declarative configuration tooling"

# --- Skill v5.3 Part 8: practice-question budget (from B4 via arc-outline) ---
question_budget:
  soundings: 5
  taking_your_bearings: 5              # across 2 checkpoints (3 + 2)
  practice_questions: 0                # orientation type — exempt per structural contract
  total_this_chapter: 10

# --- Concept / objective / command tagging ---
kb_tags:
  objectives: []
  concepts:
    - "kcna-exam-format"
    - "domain-weights-44-28-16-12"
    - "blueprint-change-2025-11-24"
    - "published-vs-commonly-reported"
    - "cncf-certification-ladder"
    - "cloud-native-framing"
    - "branded-markers"
    - "spaced-retrieval"
    - "reading-paths"
  commands: []

figures_planned:
  - "ch01-fig01-blueprint-change-2025"
  - "ch01-fig02-book-map-parts-to-domains"
---

# Chapter 1 Outline — Taking Departure

## Chapter-type note (read first)

`chapter_type: orientation`. Per `structural-contract.yaml`, this chapter is **exempt** from:

- `## Why This Chapter Matters` (exempt: orientation)
- `## What You'll Learn` (exempt: orientation)
- `## Exam Alert` / `## Practice Questions` (exempt: orientation)

It is **not** exempt from anything else. Drafting must still deliver:

| Required element | Status | Where it lands |
|---|---|---|
| `# Chapter 1: Taking Departure` | required | top |
| `## *"witty subtitle"*` | required | line 2 |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph, 5 questions |
| `## ☆ Taking Your Bearings` ×2 | **required, min 2** | after §3 and after §6 |
| `★ Fixed Point` ×1 min | **required** | §3 (the four domains and weights) |
| `**Dead Reckoning:**` ×1 min | **required** | §2 (the published exam facts, flat) |
| `⚠ Navigational Hazards` ×1 min | expected | §2 (unpublished figures treated as fact) |
| `## Chapter Summary` | required | table, near end |
| `## The Voyage Ahead` | required | closing — name locked 2026-04-19 |

Sections 1–6 below are the body sections. Because `## Why This Chapter Matters` is exempt, §1 does the arousal/identity work that section would otherwise carry — the drafting stage should not re-add the branded heading, but it should still open a curiosity gap and frame the reader as someone entering a profession, not someone cramming for a test.

**No Zenith figure.** Part 18.10 requires exactly one dramatic synthesis illustration per *content* chapter; orientation chapters are outside that rule, and the arc outline lists no `ch01-zenith-*` stub. Do not invent one.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 1 — Taking Departure". Carried forward without modification:

- **Covers**: exam mechanics and format; the 2025-11-24 blueprint change and what it invalidates; the three required weight-allocation disclosures; how to use this book; the cloud-native framing planted for harvest in Ch 17; the CNCF certification ladder positioned relative to CKA/CKAD/CKS.
- **Prerequisites**: none. Assumes general IT literacy and zero Kubernetes exposure.
- **Retrieval targets**: none. **[B3]** Ch 1 is excluded from the retrieval schedule entirely, and no item anywhere in the book tests exam mechanics.
- **Question budget**: 5 Soundings · 5 Bearings · 0 Practice · 10 total.
- **Figures**: `ch01-fig01-blueprint-change-2025`, `ch01-fig02-book-map-parts-to-domains`.
- **Depth band**: focused.

**Reader positioning** (from the commission record): Communications Officer role family, **junior tier** — the associate rung beneath CKA's senior comms officer, peer tier to Network+. Voice is the single unified brand voice; only the atmospheric register and the reader's rank differ. The reader is being *rated*, not yet given a watch of their own.

---

## 1. Why This Chapter Matters

*Exempt for `orientation` — no `## Why This Chapter Matters` heading in the draft.* The equivalent work is folded into §1 and is specified there. Planning notes for that fold:

The curiosity gap for this chapter is not "what is Kubernetes" — it's **"why does most of the KCNA prep material on the internet describe a different exam than the one you are going to sit?"** That question is answerable, load-bearing, specific to this book, and resolves in §3. Open it in §1, hold it through §2, pay it off at `ch01-fig01`.

The identity frame is that a reader finishing this book is not someone who memorized 60 answers; they are someone who can look at an unfamiliar cloud native tool and correctly guess what layer it plugs into and what it must therefore be doing. That is the actual competence the four domains are trying to measure, and it is worth saying out loud in Chapter 1 so that the reader knows what they are being asked to become.

The stakes are honest and modest — this is a $250, 90-minute, beginner-level, no-prerequisite credential with a two-year validity. Do not inflate them. The brand's ethical guardrails forbid manufactured urgency, and the reader is an adult professional who can tell.

---

## 2. What You'll Learn

*Exempt for `orientation` — no `## What You'll Learn` heading in the draft.* Retained here as the planner's statement of chapter outcomes, for the audit stages:

- Describe the KCNA's published format, duration, eligibility, and validity — and distinguish those from the figures that are only commonly reported.
- Name the four current exam domains and their weights, and state what each one absorbed or shed on 2025-11-24.
- Detect, in third-party prep material, whether it targets the current four-domain blueprint or the retired five-domain one.
- Locate any chapter of this book on the exam blueprint, and any exam domain in this book.
- Choose a reading path calibrated to your own starting point.

---

## 3. Soundings plan

**5 questions** (orientation baseline per skill Part 8 and `branded-terms.yaml`). All five test **priors the reader brings from general IT literacy** — which is the correct prerequisite set for Chapter 1, since there is no earlier chapter to source from. **[B3]** Soundings are excluded from the retrieval budget; here there is nothing to retrieve anyway.

| # | Topic (not wording) | Prerequisite / intuition tested | Why it is useful as a pre-test |
|---|---|---|---|
| 1 | The boundary between a container and a virtual machine | General virtualization literacy; whether the reader knows a container shares the host kernel | Directly calibrates Ch 2, the heaviest chapter in the book. A reader who misses this should be told to budget extra time there, before they hit it |
| 2 | What Kubernetes *is* — orchestrator vs container runtime | Whether the reader has absorbed the very common conflation of "Kubernetes" with "the thing that runs containers" | The conflation, if uncorrected, quietly corrupts Ch 2 and Ch 3. Surfacing it before reading means the CRI boundary in Ch 3 lands against an existing (wrong) model rather than into a vacuum |
| 3 | Who governs Kubernetes — vendor, foundation, or company | Institutional literacy about open-source governance | B1 flags D4.3 (community and collaboration) as the competency technically-strong candidates most reliably under-study. This question tells such a reader, on page one, that they have a gap — five chapters before Ch 17 has to fix it |
| 4 | What "cloud native" is commonly assumed to mean | The near-universal prior that it means "runs in a public cloud" | Sets up §4's plant. The reader who answers wrongly here is exactly the reader who needs Ch 17's definition to land as a correction rather than as a vocabulary item |
| 5 | Prior exposure to declarative configuration (Terraform, Ansible, CloudFormation, or similar) | Whether the reader already holds the declarative/imperative distinction under some other name | Calibrates Ch 4 and Ch 15. A reader who has written Terraform gets a large head start on "you file a declaration"; a reader who hasn't needs Ch 4 read slowly |

**Rubric (5-question scale, adapted from the standard 8-question rubric):**

- **4–5 right** — you arrive with the platform priors this book assumes. Read Ch 2 and Ch 3 at normal pace; the calibration in §6 will point you at the chapters where your gaps actually are.
- **2–3 right** — the expected starting point for this credential. Read at normal pace throughout; the book is built for you.
- **0–1 right** — read carefully, and give Ch 2 and Ch 3 a session of their own. Nothing here is beyond you; the vocabulary is just new, and the book introduces every term before it uses it.

**Fixed-Point spoiler check — passes.** Chapter 1's Fixed Point candidates are (a) the four domains and their weights and (b) the published-vs-commonly-reported distinction. None of the five Soundings questions touches either. Nor do they give away Ch 2's container/VM Fixed Point (Q1 *pre-tests* the reader's prior; the answer key states the correct distinction in one line and cross-bears to Ch 2 rather than teaching it), Ch 3's control loop, or Ch 17's CNCF definition (Q4 asks what the phrase is *commonly assumed* to mean and, in the answer key, declines to give the real definition — it names Ch 17 as where the reader will get it).

⚠ **Answer-key discipline for the drafting stage:** the `<details>` block gives a one-line rationale per question and *stops*. On Q1, Q4, and Q5 in particular, the temptation to teach the correct answer properly will be strong. Don't. Those are other chapters' Fixed Points, and spending them here costs the payoff twice.

---

## 4. Section plan

### §1 — ⚪ What the KCNA Is, and Who It's For

Establish the credential: beginner level, no prerequisites, aimed at demonstrating foundational knowledge of Kubernetes and the wider cloud native ecosystem. Position it against the hands-on credentials — KCNA is multiple-choice and conceptual, and this is a *design* decision, not a lesser version of CKA: the exam is testing whether you can discriminate between plausible alternatives, which is a different skill from typing the right command under time pressure. Open the chapter's curiosity gap here (why does most available prep describe a different exam?) and hold it. Close the section by naming what this book deliberately is not — it is not a kubectl drill book, and CKA is named as the next voyage rather than as a competitor.

- **Objectives**: none (orientation)
- **Concepts introduced**: `kcna-exam-format`, `cncf-certification-ladder`
- **Sources**: `lf-kcna-exam-page-2026-08-23.md`
- **Figure**: none
- **Checkpoint after**: no
- **Markers planned**: none required; a `> ⚓ **Worth Securing:**` on "conceptual exam, conceptual study method" fits naturally here
- **Cross-bearings**: forward to Ch 17 for the CNCF certification ladder in full; a standing pointer to Book-CKA as the next voyage
- ⚠ **Research constraint**: state only what the cached snapshot supports. The snapshot confirms beginner level, no prerequisites, and the KCNA's own positioning. It does **not** enumerate the current CNCF/LF certification roster. Say "the hands-on Kubernetes credentials — CKA, CKAD, CKS" only if Stage 2 returns a snapshot naming them as current; otherwise reduce this to a forward pointer and let Ch 17 carry it (gap G31).

### §2 — ⚪ Ninety Minutes: The Exam as Published

The mechanics, stated flat: online and proctored, multiple-choice, 90 minutes, no prerequisites, a 12-month eligibility window, two attempts included, certification valid for two years, and the three price tiers. Then the disclosure that makes this book different from its competitors: **the Linux Foundation does not publish a question count or a passing score.** The widely-circulated 60 questions and 75% pass mark are third-party reports, and this book will treat them as such every time they appear — including in Chapter 20, whose mock is sized to the commonly-reported format and framed as a calibrated instrument, not as a match to a published count.

- **Objectives**: none
- **Concepts introduced**: `kcna-exam-format`, `published-vs-commonly-reported`
- **Sources**: `lf-kcna-exam-page-2026-08-23.md` (all mechanics, and the explicit not-stated note)
- **Figure**: none — this is a table, and a table is the right instrument. Do not commission a figure for tabular facts (Part 18.9: illustration is a pedagogical decision, and there is no spatial or temporal structure here)
- **Checkpoint after**: no
- **Markers planned**:
  - `> **Dead Reckoning:**` — **satisfies the chapter's required Dead Reckoning block.** The published facts, no metaphor, no framing. This is the single best home for it in the chapter: the material is literally a facts-only list, and the marker's function is exactly that
  - `> ⚠ **Navigational Hazards**` — **satisfies the chapter's ⚠ minimum.** The hazard is not the exam; it is treating an unpublished number as a published one, then building a pacing strategy on it
  - `> 🔭 **Closer Look:**` optional, on why a certifying body might decline to publish a passing score
- **Carries**: B2 weight-allocation **disclosure #2**
- **Cross-bearings**: forward to Ch 20 (the mock's sizing rationale), forward to Ch 19 (exam-day pacing)

### §3 — 🔵 The Curriculum That Moved Under Everyone's Feet

The chapter's payload, and the resolution of §1's curiosity gap. The KCNA blueprint was restructured effective no earlier than 2025-11-24: five domains became four. Cloud Native Observability, formerly an 8% standalone domain, was folded into Cloud Native Architecture. Container Orchestration rose from 22% to 28%. Cloud Native Application Delivery **doubled**, from 8% to 16% — the single largest proportional change, and the one that most third-party material serves worst. Kubernetes Fundamentals eased from 46% to 44%. Present the current four domains with their weights and their named competencies, then show the delta, then say plainly what it means for the reader's other study materials: a guide organized around five domains with a standalone observability chapter is describing the retired blueprint, and its weighting is wrong even where its facts are right.

- **Objectives**: none directly — but this section is the map of every objective in the book
- **Concepts introduced**: `domain-weights-44-28-16-12`, `blueprint-change-2025-11-24`
- **Sources**: `lf-kcna-program-changes-2026-08-23.md` (the change notice and the retired weights), `lf-kcna-exam-page-2026-08-23.md` (current domains and competencies), `cncf-kcna-curriculum-pdf-2026-08-23.md` (competency names)
- **Figure**: **`ch01-fig01-blueprint-change-2025`** — required
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `**★ Fixed Point:**` — **satisfies the chapter's required Fixed Point.** The four domains and their weights: 44 / 28 / 16 / 12. This is the one thing from Chapter 1 that the reader should be able to recite cold, because it is the index to everything else
  - `> 🪢 **Mnemonic:**` optional, for holding 44/28/16/12 — but only if a genuinely good one exists. A forced mnemonic is worse than none
- **Carries**: B2 weight-allocation **disclosure #3**
- **Cross-bearings**: forward to Ch 18 (observability is no longer standalone — say so where the reader will feel it), forward to Ch 14–16 (the doubled domain)

### §4 — ⚪ The Phrase We Haven't Defined Yet

Short by design. The book has now used "cloud native" several times without defining it, and the reader should be told that this is deliberate. The phrase is doing real technical work — it names a set of characteristics, not a hosting location — and the CNCF has a published definition with named characteristics. That definition lands in Chapter 17, after the reader has met the machinery it describes, because a definition of cloud native read on page ten is vocabulary and the same definition read on page four hundred is a summary of everything they now know. What Chapter 1 leaves the reader with is the *question*, held open, plus the correction of the one prior that would block it later: cloud native does not mean "runs in a public cloud."

- **Objectives**: none — this is the plant that D4.2 harvests in Ch 17
- **Concepts introduced**: `cloud-native-framing` (framing only — **not** the definition)
- **Sources**: none needed. This section deliberately makes no citable factual claim about the CNCF definition, because it deliberately does not state it. If drafting finds itself reaching for `cncf-cloud-native-definition-2026-08-23.md`, the section has drifted into Ch 17's territory — cut back
- **Figure**: none
- **Checkpoint after**: no
- **Markers planned**: none required. A `> **Extended Analogy:**` sidebar is *permitted* here and nowhere else in this chapter — the "you are being handed a chart whose legend is on the last page" framing, if it can be written without preciousness. Optional; cut it if it reads as theme-dressing
- **Cross-bearings**: forward to Ch 17 §"the cloud native definition and its characteristics" — this is the single most important forward cross-bearing in the chapter, and Ch 17 must carry the reciprocal back-bearing to here
- ⚠ **Drift risk, flagged for the audit stage**: this section's whole value is what it withholds. The pressure to define the term properly will be considerable. Chapter 17's opening depends on the reader arriving with the question still open

### §5 — ⚪ How This Book Is Built

The instrument panel. Six parts, twenty chapters; Parts II through V map one-to-one onto the four domains, so progress through the book is legible as progress through the blueprint. Introduce the branded markers the reader will meet — 🧭 Soundings, ☆ Taking Your Bearings, ★ Fixed Point, ⚠ Navigational Hazards, — Dead Reckoning, 🏆 Safe Harbor, ☀️ Zenith — and the four difficulty indicators, and the four margin glyphs, and the cross-bearing convention, each in one line. Explain the two mechanisms readers most often misread as padding: the pre-chapter Soundings (a calibration instrument, not a quiz you can fail) and the deliberate practice of testing earlier chapters' material inside later chapters' checkpoints (spaced retrieval — it will feel like the book forgot you already covered that; it didn't). Name the book-level artifacts: `the-lodestar.md`, the glossary, and the Chapter 20 mock.

- **Objectives**: none
- **Concepts introduced**: `branded-markers`, `spaced-retrieval`
- **Sources**: none — this is book-internal
- **Figure**: **`ch01-fig02-book-map-parts-to-domains`** — required
- **Checkpoint after**: no
- **Markers planned**: the marker legend itself. **Presentation constraint:** the legend must be a table or list that *names* the markers, not a series of live marker blocks. A `★ Fixed Point` used as an example inside a legend still counts toward the linter's `inline_pattern` matches, which is harmless, but a legend written as seven consecutive real callout blocks reads as parody. One table, one line each
- **Carries**: B2 weight-allocation **disclosure #1** — the per-chapter percentages in this book are authored judgment derived from concept count and prerequisite load; CNCF publishes weights at the domain level only. State it here, where the Parts-to-domains map makes the claim visible
- **Cross-bearings**: forward to Ch 19 (where The Lodestar is walked through), forward to Ch 20

### §6 — ⚪ Three Ways to Read This Book

Calibration, using the Soundings result the reader now has. Three paths: **no Kubernetes exposure** (linear, Ch 2 and Ch 3 in their own sessions, don't skip the Soundings); **operations background, new to Kubernetes** (linear, but Ch 2's container material may be skimmable — check the Soundings score first); **developer who has deployed to a cluster someone else runs** (Ch 2, 4, 5, 6 will feel familiar and are not; the gaps are almost always Ch 8, Ch 12, and Ch 17, and Ch 17's D4.3 community material is the one most reliably under-studied by exactly this reader). Give an honest study-time frame rather than a marketing one. Close by handing the reader the departure: the next chapter starts with a shipping container, and the reason is not decorative.

- **Objectives**: none
- **Concepts introduced**: `reading-paths`
- **Sources**: none
- **Figure**: none
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2**
- **Markers planned**:
  - `> **Logbook Entry:**` — **the chapter's one sidebar.** The candidate who studied from a 2024 guide and walked in expecting a standalone observability domain. Subject-dignity check: the beat is aimed at the practitioner's own experience (studying the wrong blueprint), not at anyone harmed by a failure. Passes
  - `🏆 Safe Harbor` at the chapter close — expected marker, min 0, but an orientation chapter that ends without acknowledging the reader finished it wastes the one cheap competence signal available this early
  - `> 🪝 **Snag:**` optional — "your Soundings score is a reading strategy, not a verdict"
- **Cross-bearings**: forward to Ch 2 (the departure), forward to Ch 8/Ch 12/Ch 17 (the developer path's named gaps)

---

## 5. Taking Your Bearings checkpoints

Two checkpoints, **5 questions total** — the orientation-chapter budget from B4 (5 Soundings · 5 Bearings · 0 Practice), matching the skill's own CAPM worked example for an orientation chapter. The contract's `minimum_per_chapter: 2` applies to the *number of ☆ blocks* and is satisfied; the skill's ≥10-questions figure is a **content**-chapter baseline and does not bind here.

**Retrieval-practice content: none.** Chapter 1 has no earlier chapter to draw from, and **[B3]** excludes Ch 1 from the retrieval schedule entirely. The spacing ramp begins at Ch 3 (10%).

### ☆ Taking Your Bearings #1 — after §3

- **Topic**: the exam as published, and the blueprint change
- **Count**: 3
- **Retrieval from earlier chapters**: 0% (n/a)
- **Question design**:
  1. Domain identification — given a topic, name the domain it now lives in. Best candidate is observability, since the answer differs between the current and retired blueprints and the discrimination is the point
  2. Published vs commonly reported — given a set of exam facts, identify which one the Linux Foundation does not publish. This tests a judgment habit the book will rely on for twenty chapters, not a trivium
  3. The four weights, applied — e.g. which domain deserves the largest share of study time, and why the answer is not the same as "which domain has the most chapters." Trap answers should target the retired 46/22/16/8/8 weighting specifically
- **Trap-answer targets**: the retired five-domain structure; the assumption that 60 questions and 75% are published; the assumption that chapter count tracks exam weight exactly (it doesn't — max deviation 2.8 points, and the book says so)
- **Why-wrong explanations**: required for every option, per the contract and the ethical checklist

### ☆ Taking Your Bearings #2 — after §6

- **Topic**: how to use the book's instruments
- **Count**: 2
- **Retrieval from earlier chapters**: 0% (n/a)
- **Question design**:
  1. Instrument function — what a low Soundings score means and what the reader should do about it. The trap answer is "it means you should reread Chapter 1"; the right answer is that it is a pacing instruction for the chapter ahead
  2. Spaced retrieval — why Chapter 13's checkpoint will ask about Chapter 8's material. The trap answer is "because the book is repetitive"; the right answer names retrieval practice and is the reader's inoculation against skipping those questions for the next nineteen chapters
- ⚓ Both questions are metacognitive rather than factual. That is deliberate for an orientation chapter and consistent with the CAPM Ch 1 precedent — there is no domain content yet to test, and the two habits above are the ones that determine whether the rest of the book works

**Note on [B3]'s "no item anywhere tests exam mechanics."** That exclusion governs the *retrieval schedule* and the practice/mock question pools — no Bearings item in Ch 2–18, no end-of-chapter Practice question, and no mock question may test Ch 1 mechanics. Chapter 1's own checkpoints are in-chapter comprehension, not retrieval, and the chapter cannot satisfy its required two ☆ blocks without them. The design above further reduces the tension: neither checkpoint asks the reader to recall a price, a duration, or an eligibility window. Flagged in § Open questions for reviewer override.

---

## 6. Exam Alert plan

**Skipped — `orientation` is exempt** from the `## Exam Alert` / `## Practice Questions` requirement per `structural-contract.yaml`.

The exam-facing content that would live in an Exam Alert is instead distributed to where it belongs: the ⚠ Navigational Hazards block in §2 (unpublished figures treated as fact), and the ★ Fixed Point in §3 (the four weights). Chapter 19 carries the book's consolidated exam-day material, and Chapter 1 should not pre-empt it.

---

## 7. Practice Questions plan

**Target count: 0.** Orientation type — exempt. The arc outline's budget for this chapter is 5 Soundings · 5 Bearings · 0 Practice · **10 total**, and the book clears the 300-question floor by a wide margin (715 planned) without asking Chapter 1 to contribute.

Do not add practice questions here to "help the reader get started." There is no domain content in this chapter to test, and questions about exam mechanics are explicitly excluded from every pool in the book.

---

## 8. Required figures

Two figures. Both are stubs for Stage 10 `yaml-figure-spec` extraction and the sibling `certcomp-diagrams` pipeline. `diagram_enforcement.enabled` is `false` for this book, so the linter will not check for rendered artifacts yet.

### `ch01-fig01-blueprint-change-2025`

- **Purpose**: resolve the chapter's curiosity gap visually, and give the reader a durable mental image of the delta so they can audit any other study material against it at a glance.
- **Content**: a two-column before/after comparison. Left: the retired five-domain blueprint (Kubernetes Fundamentals 46 · Container Orchestration 22 · Cloud Native Architecture 16 · Cloud Native Observability 8 · Cloud Native Application Delivery 8). Right: the current four (Kubernetes Fundamentals 44 · Container Orchestration 28 · Cloud Native Application Delivery 16 · Cloud Native Architecture 12). Connector showing Observability folding into Cloud Native Architecture; emphasis on the two movements that matter — Application Delivery doubling, Container Orchestration rising six points.
- **Label budget**: ~11 labels (9 domain names + 2 column headers). Above the ~7-label comfort threshold in Part 18.12, but the structure is a paired list rather than a network, so working-memory load is low. Flag for the figure reviewer; if it reads as crowded, drop the weights into the adjacent prose table and keep only names and connectors in the figure.
- **Grayscale**: the before/after distinction must survive grayscale. Encode it with position and connector direction, not with color alone.
- **Copyright clearance**: `own_interpretation` — the weights are published facts; the visual arrangement is ours.

### `ch01-fig02-book-map-parts-to-domains`

- **Purpose**: give the reader a single image that answers both "where am I" and "what is this worth on the exam," reusable as a mental index for the whole book.
- **Content**: six Parts as bands, with chapter number ranges, mapped to the four domains and their weights. Parts I and VI shown carrying zero weight, which is itself informative. Should visibly encode that Parts II–V map one-to-one onto the domains.
- **Label budget**: high if every chapter title is included — **use chapter numbers and Part names only**, not twenty titles. The table of contents does titles; this figure does structure.
- **Reuse**: this figure is a candidate for re-presentation in Ch 19's cross-domain integration map. Design it knowing that; if `ch19-fig01` can be built as a filled-in version of this one, the reader gets a "you have now covered all of this" beat for free at the end of the book.
- **Copyright clearance**: `own_interpretation`.

---

## 9. Open questions for the author

1. **The certification-ladder claim in §1.** The cached exam-page snapshot supports KCNA's own positioning (beginner, no prerequisites) but does not enumerate the current CNCF/LF certification roster. Gap **G31** (adjacent certifications) is routed to Ch 17. Options: (a) Stage 2 fetches an LF certification-catalog snapshot and §1 names the ladder with a source tag; (b) §1 names only CKA as the hands-on next step, since the commission record already establishes Book-CKA as a sibling, and defers the rest to Ch 17. **Recommendation: (b)**, unless the research stage returns the catalog cheaply. Do not name KCSA, CKAD, or CKS from memory.

2. **Epigraph.** Not drafted here, per the no-prose constraint. Two directions, in the skill's Part 15 order of preference: a historical navigation or preparation quote (departure, taking bearings before you need them), or an original Lodestar epigraph about sailing with an out-of-date chart — which would rhyme with §3 and is the stronger fit, but originals should be used sparingly and this is the book's first page. Author's call.

3. **Chapter 1's Bearings vs. [B3]'s "no item anywhere tests exam mechanics."** Read above as governing the retrieval schedule and the practice/mock pools, not the orientation chapter's own required checkpoints — which cannot be dropped without failing the contract's `minimum_per_chapter: 2`. The two checkpoints as designed test discrimination and study method rather than mechanics trivia. Flagged for override if the intended reading was stricter.

4. **Does §4 survive audit?** A section whose value is what it withholds is unusual, and both the drafting stage and the fact-accuracy audit may read it as incomplete. Confirm the plant-and-harvest structure is intended before drafting, and consider adding a note to Ch 17's outline so its author knows the question was left open on purpose.

5. **Front matter overlap.** Per the arc outline, Chapter 1 "carries the three B2 disclosures into front matter." `00-front-matter.md` is a separate artifact. Which file states each disclosure canonically, and how much repetition is acceptable? **Proposal:** front matter states all three tersely as publisher's disclosures; Chapter 1 states each one *in the place where the reader needs it* (#2 in §2, #3 in §3, #1 in §5) with more context. That is content redundancy across different framings — good redundancy per skill Part 7 — but the two files must not contradict each other, and the reconcile pass should check.

6. **The `KCNA_Curriculum.pdf` typo** ("Could Native Community and Collaboration"). The arc outline routes it to the blueprint appendix, not this chapter. Confirmed as excluded from Chapter 1 — noted here only so drafting doesn't rediscover it and put it in §3.

7. **Freshness of the pricing figures.** `lf-kcna-exam-page-2026-08-23.md` was cached 2026-08-23. Prices and the THRIVE-ONE bundle are the most volatile facts in §2 and the least load-bearing. Consider stating the exam-only price with its snapshot date and describing the bundles without figures, so the chapter doesn't age badly on a detail that costs the reader nothing.

8. **Gap G37 (LFS250 syllabus) is still open** and is the arc outline's first open item. It does not gate this chapter — Chapter 1 covers no objectives — but if it surfaces an authoritative question count, §2's disclosure language and Chapter 20's framing both change. Chapter 1 can be drafted now; §2 should be re-read after G37 closes.
```