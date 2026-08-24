All filesystem writes are blocked in this sandbox — including to the primary working directory. That matches this repo's documented stage design (CLAUDE.md: `Write` removed from `--allowed-tools` so "stage output flows through stdout where the orchestrator captures it atomically"). So stdout is my only output channel: the manifest below is the artifact, with the snapshot bodies embedded ready to be written.

Research is complete, and it turned up three findings that change Chapter 1 before it can be drafted.

---

# Research Manifest — KCNA Chapter 1

> **Harness note.** This stage could not write files: `Write` is gated and
> `Set-Content` to `Book-KCNA/sources/`, `Book-KCNA/.pipeline-state/`, and even
> `certcomp/` were all blocked by the sandbox. The four new snapshots and two
> corrected snapshots are reproduced in full in **Appendix A** and need to be
> written to `../Book-KCNA/sources/` before Stage 3 runs.

## Existing snapshots reusable for Chapter 1

The book-outline stage already cached 87 snapshots on 2026-08-23. Chapter 1 needs six of them; four are usable as-is, two need correction.

| Snapshot | Authority | Concepts | Status |
|---|---|---|---|
| `lf-kcna-exam-page-2026-08-23.md` | Linux Foundation (exam page) | `kcna-exam-format`, `domain-weights-44-28-16-12`, `published-vs-commonly-reported` | **REPLACE** — App. A1 |
| `lf-kcna-program-changes-2026-08-23.md` | Linux Foundation (program changes) | `blueprint-change-2025-11-24` | **REPLACE** — App. A2 (misattribution) |
| `cncf-kcna-curriculum-pdf-2026-08-23.md` | CNCF `cncf/curriculum` | `domain-weights-44-28-16-12` | OK as-is |
| `lf-cloud-native-certification-catalog-2026-08-23.md` | Linux Foundation catalog | `cncf-certification-ladder` | OK; corroborated |
| `lf-lfs250-course-outline-2026-08-23.md` | Linux Foundation (LFS250) | G37 | OK as-is |
| `cncf-cloud-native-definition-2026-08-23.md` | CNCF | `cloud-native-framing` | Present but **§4 must not use it** (by design) |

## New snapshots (Appendix A)

| Snapshot | Authority | Concepts |
|---|---|---|
| `lf-mc-exam-faq-2026-08-23.md` | LF T&C DOCS candidate handbook | `published-vs-commonly-reported`, `kcna-exam-format` |
| `cncf-kcna-certification-page-2026-08-23.md` | CNCF (cncf.io) | `cncf-certification-ladder`, `kcna-exam-format` |
| `cncf-curriculum-repo-kcna-versions-2026-08-23.md` | CNCF `cncf/curriculum` git history | `blueprint-change-2025-11-24` |
| `provenance-kcna-60-questions-2026-08-23.md` | **NOT authoritative** — evidence *about* a third-party claim | `published-vs-commonly-reported` |

---

## Corrections required before drafting

### 1. §2's central disclosure is half wrong — the passing score IS published

The outline says the book's differentiator is that "**the Linux Foundation does not publish a question count or a passing score.**" The first half holds. The second half does not.

The Linux Foundation's own candidate-facing handbook states verbatim:

> "A score of 75% or above must be earned to pass the Multiple Choice Exam."

— `docs.linuxfoundation.org/tc-docs/certification/faq-mc`

That is the LF's official documentation, not a third-party report. KCNA is a multiple-choice exam by the exam page's own words, so the 75% figure is published and applies. The same page also publishes the 90-minute duration and names CNPA as the sole timing exception.

**The accurate, and still distinctive, framing:** the two numbers have *different* provenance. The passing score is published — just in the candidate handbook rather than on the exam page most candidates read. The question count is published nowhere. That is a sharper and more defensible §2 than the current one, and the ⚠ Navigational Hazards block survives intact: the hazard is still treating an unpublished number as published, now with a worked example of a number that *is* published and a number that isn't sitting side by side.

This also revises Chapter 20's framing (mock sized to a commonly-reported format) and the ☆ Bearings #1 question 2, whose designed answer — "identify which one the Linux Foundation does not publish" — currently has two defensible answers. Narrow it to question count.

### 2. `lf-kcna-program-changes` attributes weights the page does not contain

The cached snapshot states the retired five-domain weights (46/22/16/8/8) inside its summary of the program-changes page. Targeted re-fetch confirms **the page does not display the previous domain structure or weights at all.** It says only:

> "The KCNA domains (i.e. Fundamentals, Container Orchestration etc.) will remain mostly unchanged except that observability will be rolled under Cloud Native Architecture."

A downstream fact-accuracy audit checking §3's retired weights against this snapshot would validate them against text the authority never wrote. Corrected snapshot in A2.

The re-fetch did recover genuinely useful new material the old snapshot missed — the rule for which blueprint a candidate gets:

> "It does NOT matter if the exam reservation happens to be for a first attempt or a retake, nor does it matter on what date you completed the exam purchase. The only date that matters is the date you sit for the exam."

That belongs in §3 and is exactly the reader-facing consequence the section is about.

### 3. `ch01-fig01`'s entire left column is unsourced

**This is the significant gap.** The retired blueprint (Kubernetes Fundamentals 46 · Container Orchestration 22 · Cloud Native Architecture 16 · Cloud Native Observability 8 · Cloud Native Application Delivery 8) is the left half of the chapter's required figure and the substance of §3's delta — and I could not source it authoritatively.

What I established:

- The LF program-changes page does not contain it (finding 2).
- The current CNCF curriculum PDF does not contain it — it documents only the new blueprint.
- I located the authoritative archived original. CNCF commit `308c903` ("Archiving exam curriculum", zuzannapn, 2025-11-24) moved the pre-change PDF to **`old-versions/KCNA_Curriculum old.pdf`** in `github.com/cncf/curriculum`, alongside commit `06702fe` ("KCNA Exam Curriculum") the same day, which installed the four-domain replacement. The repo README confirms "Old versions remain available."
- **I could not extract that PDF's text.** WebFetch returns the 152 KB binary; the Read tool rejects `.bin`; Bash/Python network fetch and all local writes are blocked in this sandbox; GitHub's blob viewer errors out; `web.archive.org` is blocked to WebFetch.

Corroboration exists but is **not acceptable under this stage's sourcing rules**: the CNCF-hosted post of 2024-10-23 lists 46/22/16/8/8, but its byline reads "Community post originally published on Medium by Giorgi Keratishvili" — a guest contribution, not CNCF publication. Several third-party GitHub study guides agree.

**Recommendation.** Do not draft the retired weights from the corroboration above. A two-minute manual step closes this properly: open `https://github.com/cncf/curriculum/raw/master/old-versions/KCNA_Curriculum%20old.pdf`, and paste its domain list into a snapshot named `cncf-kcna-curriculum-retired-2026-08-23.md`. Until then, §3 can state the *structural* change (five domains to four, observability folded into Cloud Native Architecture) from the LF page, but **not the retired percentages**, and `ch01-fig01` cannot be specced.

---

## Gaps

| Gap | Status | Effect on Chapter 1 |
|---|---|---|
| **Retired five-domain weights** | **OPEN — blocking `ch01-fig01`** | Exact retrieval path in finding 3. Highest priority. |
| **Published question count** | **OPEN — and this is the answer** | Absent from the exam page, the MC FAQ, the general certification FAQ, the exam-results handbook page, the CNCF KCNA page, and the LFS250 outline. Six authoritative sources checked, none states it. This is now well-evidenced, not merely unfound — §2's claim is strong. |
| **G37 — LFS250 syllabus** | **Partially closed** | The course outline surfaces no question count. Per outline Open Question #8, §2's disclosure language does **not** need to change on this account. |
| **G31 / Open Question #1 — cert ladder** | **CLOSED** | See below. |
| Scoring methodology / cut-score derivation | Open, non-blocking | Not published. §2's optional 🔭 Closer Look on why a body might decline to publish should stay speculative and brief. |

### Open Question #1 resolves to option (a)

The outline recommended option (b) — name only CKA and defer — "unless the research stage returns the catalog cheaply." It did. CNCF's own KCNA page states verbatim:

> "The KCNA exam is intended to prepare candidates to work with cloud native technologies and pursue further CNCF credentials, including CKA, CKAD, and CKS."

and describes KCNA as "a pre-professional certification designed for candidates interested in advancing to the professional level." The CNCF certifications hub adds that KCNA "lays the groundwork for further CNCF certifications like CKA, CKAD, and CKS," and confirms CKA/CKAD/CKS are performance-based while KCNA is "online and multiple-choice."

**§1 may now name CKA, CKAD, and CKS with a source tag** — the "hands-on Kubernetes credentials" phrasing the outline wanted is fully supported, including the multiple-choice-vs-performance-based contrast §1 builds its "design decision, not a lesser version" argument on. KCSA still should not be named from memory; it is in the LF catalog snapshot but plays no role in §1's argument.

---

## Notes for the author

**Pricing (Open Question #7).** Confirmed current as of 2026-08-23: $250 exam only, $495 with THRIVE-ONE, $299 with LFS250. One discrepancy worth knowing: CNCF's page says "$250 and includes one free retake" while the LF page says "Two exam attempts" — consistent, differently worded. Your instinct to state the exam-only price with its snapshot date and describe the bundles without figures is sound; the bundle names are the volatile part.

**Two-year validity** appears on the LF exam page only. The general certification FAQ does not state a validity period, so cite the exam page.

**The 60-question figure's provenance is itself a story for §2.** The most authoritative-*looking* home for it is a post on cncf.io — which turns out to be a syndicated community guest post. That is a precise, fair, checkable illustration of how an unpublished number acquires the appearance of authority, and it is aimed at the diffusion mechanism rather than at the author. Subject-dignity check passes. Snapshot A4 preserves the byline as evidence; it is marked non-authoritative and must never be cited as fact.

**Curriculum version confirmed.** The commission's "effective 2025-11-24" is exact — both CNCF commits land on 2025-11-24, matching the LF's "no earlier than November 24, 2025."

**Minor catalog discrepancy, not Chapter 1's problem.** The cached LF catalog snapshot files ICA under intermediate/performance-based; the CNCF hub lists it among associates while describing it as "performance-based." Route to Ch 17 with G31.

**Unchanged.** §4 correctly needs no sources and must not acquire any. §5 and §6 are book-internal. Outline Open Questions #2–#6 are author/editorial calls that research does not bear on.

---

## Appendix A — snapshot files to write

### A1 · `lf-kcna-exam-page-2026-08-23.md` (replaces existing)

```markdown
---
source_url: "https://training.linuxfoundation.org/certification/kubernetes-cloud-native-associate/"
fetched_at: "2026-08-23T23:50:00-0400"
authority: "The Linux Foundation (Training & Certification) — official exam product page"
objectives_covered: []
concepts_covered: ["kcna-exam-format", "domain-weights-44-28-16-12", "published-vs-commonly-reported", "cncf-certification-ladder"]
---

# Kubernetes and Cloud Native Associate (KCNA) — Linux Foundation official exam page

> Re-fetched and expanded 2026-08-23T23:50 for Chapter 1. Supersedes the thinner
> capture taken at 22:30 the same day. All quoted strings are verbatim.

## What the exam demonstrates

"The Kubernetes and Cloud Native Associate (KCNA) exam demonstrates a user's foundational knowledge and skills in Kubernetes and the wider cloud native ecosystem."

## Experience level and prerequisites

Experience Level: "Beginner"
Prerequisites: "There are no prerequisites for this exam."

## Exam details

Format: "This exam is an online, proctored, multiple-choice exam."
Duration: "90 minutes"

Pricing tiers:
- "Certification exam only – $250"
- "Certification exam + THRIVE-ONE Annual Subscription... – $495"
- "Certification exam + Kubernetes and Cloud Native Essentials (LFS250) course – $299"

Eligibility and attempts:
- "12-months to schedule & take the exam"
- "Two exam attempts"

Validity: "Certification Valid for 2 Years"

## Domains and competencies

- "Kubernetes Fundamentals 44%" — Kubernetes Core Concepts; Administration; Scheduling; Containerization
- "Container Orchestration 28%" — Networking; Security; Troubleshooting; Storage
- "Cloud Native Application Delivery 16%" — Application Delivery; Debugging
- "Cloud Native Architecture 12%" — Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration

## What this page does NOT state

Confirmed by targeted re-fetch on 2026-08-23:
- No question count stated.
- No passing score stated.

WARNING — do not generalize this. This snapshot supports only the narrow claim
that the exam product page omits both figures. The passing score IS published by
the Linux Foundation elsewhere: see lf-mc-exam-faq-2026-08-23.md (75%). The
question count remains unlocated in any authoritative LF or CNCF source.
```

### A2 · `lf-kcna-program-changes-2026-08-23.md` (replaces existing — removes misattribution)

```markdown
---
source_url: "https://training.linuxfoundation.org/kcna-program-changes/"
fetched_at: "2026-08-23T23:50:00-0400"
authority: "The Linux Foundation (Training & Certification) — KCNA program changes notice"
objectives_covered: []
concepts_covered: ["blueprint-change-2025-11-24", "domain-weights-44-28-16-12"]
---

# KCNA Program Changes — Linux Foundation

> CORRECTION 2026-08-23: the previous capture of this page listed the retired
> five-domain weights (46/22/16/8/8) as if sourced here. Targeted re-fetch
> confirms THE PAGE DOES NOT DISPLAY THE PREVIOUS DOMAIN STRUCTURE OR WEIGHTS.
> Those figures have been removed from this snapshot. For the retired weights
> see cncf-curriculum-repo-kcna-versions-2026-08-23.md — currently an OPEN GAP.

## Announcement

"The Kubernetes and Cloud Native Associate (KCNA) exam will be updated no earlier than November 24, 2025."

## What changed

"The KCNA domains (i.e. Fundamentals, Container Orchestration etc.) will remain mostly unchanged except that observability will be rolled under Cloud Native Architecture."

## Which blueprint a candidate is tested on

"Any KCNA exam taken after the updated release will test on the new set of Domains and Competencies."

"It does NOT matter if the exam reservation happens to be for a first attempt or a retake, nor does it matter on what date you completed the exam purchase. The only date that matters is the date you sit for the exam."

## Rationale

"These updates are part of our ongoing efforts to ensure that a Kubernetes and Cloud Native Associate (KCNA) has the most updated skills, knowledge, and competence needed in the industry."

## Updated domains and competencies

- "Kubernetes Fundamentals – 44%": Kubernetes Core Concepts; Administration; Scheduling; Containerization
- "Container Orchestration – 28%": Networking; Security; Troubleshooting; Storage
- "Cloud Native Application Delivery – 16%": Application Delivery; Debugging
- "Cloud Native Architecture – 12%": Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration

## Not stated on this page

No question count, no passing score, no duration, and no retired-blueprint weights.
```

### A3 · `lf-mc-exam-faq-2026-08-23.md` (new)

```markdown
---
source_url: "https://docs.linuxfoundation.org/tc-docs/certification/faq-mc"
fetched_at: "2026-08-23T23:50:00-0400"
authority: "The Linux Foundation — official candidate-facing T&C DOCS, 'Multiple Choice Exams: Frequently Asked Questions'"
objectives_covered: []
concepts_covered: ["kcna-exam-format", "published-vs-commonly-reported"]
---

# Multiple Choice Exams: FAQ — Linux Foundation T&C DOCS

> THIS SNAPSHOT CHANGES A LOAD-BEARING CHAPTER 1 CLAIM. See the Ch 1 research
> manifest, "Corrections required before drafting", finding 1.

Official Linux Foundation candidate handbook documentation, not a third-party
site. Governs the LF's multiple-choice exams as a class. The KCNA exam page
calls KCNA "an online, proctored, multiple-choice exam", placing it in this class.

## Passing score — PUBLISHED

"A score of 75% or above must be earned to pass the Multiple Choice Exam."

## Duration — PUBLISHED

"Candidates are allowed 90 minutes to complete Multiple Choice Exams, with the exception of CNPA. CNPA candidates are allowed 120 minutes to complete the exam."

## Question count — NOT PUBLISHED

Confirmed absent on targeted fetch 2026-08-23. No statement of how many
questions an exam contains, and none that the number varies by exam.

## Scoring methodology — NOT PUBLISHED

No mention of scaled scoring, cut scores, or psychometric standard setting.

## Scope caveat

The FAQ is titled for multiple-choice exams generally and does not enumerate
which exams it covers. CNPA is named as a timing exception; the renewal section
references KCNA, KCSA, and CKA/CKAD/CKS re: the CARE program.

Supported phrasings:
- CORRECT: "The Linux Foundation publishes a 75% passing standard for its
  multiple-choice exams, of which the KCNA is one."
- FALSE, do not write: "The Linux Foundation does not publish a passing score."
- FALSE, do not write: "The KCNA exam page states the passing score is 75%."
  (It is in the candidate handbook, not on the exam page.)
```

### A4 · `cncf-kcna-certification-page-2026-08-23.md` (new)

```markdown
---
source_url: "https://www.cncf.io/training/certification/kcna/"
fetched_at: "2026-08-23T23:50:00-0400"
authority: "Cloud Native Computing Foundation (cncf.io) — official KCNA certification page"
objectives_covered: []
concepts_covered: ["cncf-certification-ladder", "kcna-exam-format", "domain-weights-44-28-16-12"]
---

# Kubernetes and Cloud Native Associate (KCNA) — CNCF

## Description and audience

"The Kubernetes and Cloud Native Associate (KCNA) exam demonstrates a user's foundational knowledge and skills in Kubernetes and the wider cloud native ecosystem."

"The KCNA is a pre-professional certification designed for candidates interested in advancing to the professional level through a demonstrated understanding of kubernetes foundational knowledge and skills. This certification is ideal for students learning about or candidates interested in working with cloud native technologies."

## Format and cost

"This exam is an online, proctored, multiple-choice exam."
Cost: "$250 and includes one free retake."

## Certification ladder

"The KCNA exam is intended to prepare candidates to work with cloud native technologies and pursue further CNCF credentials, including CKA, CKAD, and CKS."

Corroborated at https://www.cncf.io/training/certification/ : KCNA "lays the
groundwork for further CNCF certifications like CKA, CKAD, and CKS." That page
describes KCNA as "online and multiple-choice", CKA as a "performance-based exam
where candidates interact with the command line to solve real-world challenges",
CKAD as a "hands-on, command-line environment", and CKS as "performance-based".

## Domains

Kubernetes Fundamentals 44% · Container Orchestration 28% ·
Cloud Native Application Delivery 16% · Cloud Native Architecture 12%

## Not stated on this page

Duration, question count, passing score, validity period, prerequisites.
```

### A5 · `cncf-curriculum-repo-kcna-versions-2026-08-23.md` (new)

```markdown
---
source_url: "https://github.com/cncf/curriculum/commits/master/KCNA_Curriculum.pdf"
fetched_at: "2026-08-23T23:50:00-0400"
authority: "Cloud Native Computing Foundation — cncf/curriculum repository, version control history"
objectives_covered: []
concepts_covered: ["blueprint-change-2025-11-24"]
---

# CNCF curriculum repository — KCNA curriculum version history

Primary-source provenance for the KCNA blueprint change. The cncf/curriculum
repo is CNCF's official publication channel for exam curricula; its README
states "Old versions remain available."

## Commit history for KCNA_Curriculum.pdf

- 06702fe — "KCNA Exam Curriculum" — zuzannapn — Nov 24, 2025
- 308c903 — "Archiving exam curriculum" — zuzannapn — Nov 24, 2025
- 4461347 — "KCNA Exam Curriculum" — caitmulholland — Nov 19, 2021
- a25cd84 — "archive old KCNA" — caitmulholland — Nov 19, 2021
- f7c6c89 — "KCNA Curriculum - Coming Q4 2021" — caitmulholland — Oct 11, 2021

The two 2025-11-24 commits are the blueprint change. This independently confirms
the effective date given on the LF program-changes page ("no earlier than
November 24, 2025").

## Where the retired five-domain curriculum lives

Commit 308c903 moved the pre-change PDF to:

    old-versions/KCNA_Curriculum old.pdf     (152 KB)

Raw URL:
https://github.com/cncf/curriculum/raw/master/old-versions/KCNA_Curriculum%20old.pdf

## OPEN GAP — text not extracted

The retired domain weights are NOT recorded in this snapshot because the
research stage could not extract the PDF's text (binary not readable by the
available tools; sandbox blocked local download; GitHub's blob viewer errored).

DO NOT draft the retired weights from memory or from third-party study guides.
Retrieve the PDF above and record its domain list in
cncf-kcna-curriculum-retired-2026-08-23.md first.
```

### A6 · `provenance-kcna-60-questions-2026-08-23.md` (new — evidence, NOT fact)

```markdown
---
source_url: "https://www.cncf.io/blog/2024/10/23/how-to-ace-kcna-kubernetes-and-cloud-native-associate-exam/"
fetched_at: "2026-08-23T23:50:00-0400"
authority: "NOT AUTHORITATIVE — community guest post syndicated onto the CNCF blog. Retained solely as evidence of what third parties claim."
objectives_covered: []
concepts_covered: ["published-vs-commonly-reported"]
---

# Provenance of the "60 questions / 75%" figures

> DO NOT CITE THE CONTENTS OF THIS FILE AS FACT. This snapshot exists to
> document WHERE a widely-repeated claim comes from, which is itself the
> subject of Chapter 1 §2. It is not a source for the claim's truth.

## The claim, as it appears

"You'll have 90 minutes to answer 60 questions" and "the passing score is >75%"

The same post states the pre-change five-domain blueprint as:
"Kubernetes Fundamentals 46% / Container Orchestration 22% / Cloud Native
Architecture 16% / Cloud Native Observability 8% / Cloud Native Application
Delivery 8%"

## Why this is not authoritative

The byline reads: "Community post originally published on Medium by Giorgi
Keratishvili". It is a syndicated community contribution hosted on cncf.io, not
a CNCF publication. Hosting on the authority's domain is what lends the figures
their apparent authority.

## Cross-check against authoritative sources (all fetched 2026-08-23)

- 90 minutes — CONFIRMED published (LF exam page; LF MC FAQ).
- 75% passing score — CONFIRMED published (LF MC FAQ, for MC exams as a class).
- 60 questions — NOT FOUND in any authoritative source. Checked and absent from:
  the LF KCNA exam page; the LF MC exam FAQ; the LF general certification FAQ;
  the LF exam-results handbook page; the CNCF KCNA page; the LFS250 outline.
- 46/22/16/8/8 — NOT independently sourced. See
  cncf-curriculum-repo-kcna-versions-2026-08-23.md (open gap).
```

---

**One item needs your decision before Stage 3.** Everything else is settled, but the retired five-domain weights need a two-minute manual retrieval (the raw URL in A5) — without them, `ch01-fig01` has no left column and §3 can describe the restructure but not quantify it. If you'd rather not block on it, the alternative is to draft §3 on the structural change only and spec the figure as a one-sided "what moved" diagram, but that gives up the before/after comparison the section was designed around.