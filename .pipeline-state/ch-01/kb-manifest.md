I have everything I need: the KB directory doesn't exist yet (Chapter 1 creates it), B2 gives me the chapter-of-definition mapping, and the cached curriculum snapshot confirms the competency enumeration.

# Knowledge-Base Manifest — KCNA Chapter 1

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 1 — Taking Departure
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-24
**KB state before this stage:** `Book-KCNA/knowledge-base/` **did not exist.** Chapter 1 is the first chapter through Stage 14, so every file below is a first creation. There are no prior shards, and therefore **no shard-contradiction risk under Rule 6** — but three contradictions against *ratified book-outline artifacts* are carried forward loudly into the shards (see "Canon conflicts" below).

**Inputs consulted:** finalized `draft-v2.md`, `integration.md` (Stage 13), `ch-01/outline.md` frontmatter (`kb_tags`), `book-outline/chapter-lineup.md` (B2, ratified), `book-outline/retrieval-architecture.md` (B3 — stage-failure notice, see operator note), `sources/lf-kcna-exam-page-2026-08-23.md`, `sources/cncf-kcna-curriculum-pdf-2026-08-23.md`.

> **Naming clarification, worth locking now:** `knowledge-base/glossary.md` (this file) is the *pipeline's accumulating working ledger* — it tracks which terms are surfaced, defined, or reserved, and by which chapter. It is **not** the shipped `glossary.md` at the book root that `structural-contract.yaml` requires under skill Part 16. The published artifact is generated from this ledger at book assembly, once every term has a real definition. Keeping them separate is what makes reserved stubs safe to write.

---

## Glossary entries added to `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md`

**35 terms surfaced · 10 defined from chapter text · 4 convention locks · 19 reserved · 2 optional.**

Rule 5 constrains this hard. Chapter 1 is orientation: it *names* roughly twenty Kubernetes terms it never defines. Writing definitions for those would mean paraphrasing cached sources or inventing — both are definitional drift. So the ledger has three tiers, and only tier 1 carries prose.

### Tier 1 — defined from Chapter 1 text (verbatim, no paraphrase)

| Term | Definition (verbatim from chapter) | Chapter of definition |
|---|---|---|
| **CKA (Certified Kubernetes Administrator)** | "a genuinely hands-on exam taken in a live terminal" — *partial; contrast only* | Ch 1 (partial) / Ch 17 §4 (full, in the certification ladder) |
| **cloud native** | "describes characteristics of how a system is built and operated" — and "it does **not** mean 'runs in a public cloud.' The CNCF's own definition covers workloads deployed across public, private, and hybrid environments." *Deferring entry — see note below.* | **Ch 17 §1** |
| **CNCF (Cloud Native Computing Foundation)** | The body that hosts Kubernetes; "part of the nonprofit **Linux Foundation**" | Ch 1 §1 |
| **container** | "a process on the host that has been given an isolated view of the system"; shares "the host's **operating system kernel**" | Ch 1 Soundings A1 (partial) / **Ch 2 §1** (full) |
| **container runtime** | "A separate **container runtime** on each machine does the work of actually starting the containers" | Ch 1 Soundings A2 (partial) / **Ch 2** (full) |
| **KCNA (Kubernetes and Cloud Native Associate)** | "the usual entry point to the cloud native certification family"; the Linux Foundation "describes it as demonstrating 'a user's foundational knowledge and skills in Kubernetes and the wider cloud native ecosystem'" | Ch 1 §1 |
| **Linux Foundation, The** | The nonprofit that publishes the exam and of which CNCF is part | Ch 1 §1 (partial) |
| **orchestrator / container orchestration** | "Kubernetes is an **orchestrator** — it decides what should run where" | Ch 1 Soundings A2 (partial) / **Ch 3** (full) |
| **The Lodestar** | "a single page holding the exam-critical facts, distinctions, and traps, distilled from the whole book" | Ch 1 §5 |
| **virtual machine** | "A virtual machine boots its own operating system on virtualized hardware" — *contrast only* | Ch 1 Soundings A1 (partial) / **Ch 2 §1** (full) |

**⚠ The `container` entry inherits an open `AUTHOR-REVIEW` flag.** The chapter says "operating system kernel"; the cached snapshot `k8s-docs-overview-2026-08-23` says containers share "the Operating System (OS) among the applications." The chapter's wording is more precise and more standard, but it is a sharpening, not a quotation. **Whatever the author settles in Chapter 1 propagates into Chapter 2's full definition** — the glossary entry is marked provisional so Ch 2's Stage 14 doesn't lock the sharpened form by accident.

**On the `cloud native` deferring entry.** Stage 13 referred this for author decision and did not default it, because a normal alphabetized glossary entry hands the reader exactly what §4 spends a whole section withholding. I have implemented Stage 13's **first-listed** option — the deferring entry — because it is buildable entirely from Chapter 1's own text (the negative claim is stated outright in §4 and again in QC2.3), it preserves the pedagogical device, and it reads as a pointer rather than a dodge. **This is reversible and flagged for ratification**, not treated as settled. If the author prefers the full entry, only this one row changes.

### Tier 2 — convention locks (Stage 13 recommendations; *not* chapter definitions)

These four terms are used precisely throughout Chapter 1 but never explicitly defined. Stage 13 recommends locking the conventions here because Chapter 1 sets canon for nineteen more chapters and Chapters 19–20 reason about these repeatedly. Marked as conventions, not definitions, so nothing masquerades as inherited prose.

| Term | Proposed convention | Rationale |
|---|---|---|
| **blueprint** | The domain-and-weight *structure* the CNCF curriculum describes | Chapter body uses it this way 11×; only the subtitle and §3 heading diverge, and those are rhetorical |
| **curriculum** | The CNCF-published *document* (`KCNA_Curriculum.pdf`) | Pairs with the above; B2 uses both terms interchangeably and will drift without this |
| **competency** | A named topic *inside* a domain (13 of them) | Load-bearing for the whole book; Chapter 1 already uses it precisely |
| **domain** | One of the four weighted blocks (44 / 28 / 16 / 12) | As above |

### Tier 3 — reserved terms (surfaced in Ch 1, defined later; **no definition written**)

Chapter of definition assigned from B2, per Stage 13's recommended rule: **cite the chapter of definition, not first mention.** Otherwise a third of the glossary points at the orientation chapter, which teaches none of it.

| Term | Defining chapter (B2) | | Term | Defining chapter (B2) |
|---|---|---|---|---|
| CNCF Cloud Native Definition v1.1 | Ch 17 | | OpenTelemetry | Ch 18 |
| Container Runtime Interface (CRI) | Ch 2 | | Pod | Ch 5 |
| declarative vs imperative | Ch 4 | | Prometheus | Ch 18 |
| deployment strategy | Ch 6 (mechanics) / Ch 15 (vocabulary) | | PromQL | Ch 18 |
| exporter | Ch 18 | | scheduler / scheduling | Ch 7 |
| GitOps | Ch 15 | | scrape (pull) model | Ch 18 |
| Helm | Ch 14 | | Service | Ch 9 |
| `kubectl` | Ch 8 | | StatefulSet | **Ch 6** (introduced) / Ch 11 (completed) |
| metrics | Ch 18 | | traces | Ch 18 |
| observability | Ch 18 | | | |

**Optional (product names, author call):** LFS250, THRIVE-ONE.
**Excluded, deliberately:** Terraform / Ansible / CloudFormation (external tools, not exam terms); branded markers and difficulty indicators (brand-level — they live in `branded-terms.yaml`, not a per-book glossary).

---

## Concept shards added at `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/{slug}.md`

Seven of the outline's nine `kb_tags.concepts` clear the ≥200-word threshold. Slugs match the outline's tags exactly so the tagging round-trips.

- `concepts/kcna-exam-format.md` — **created** (§1 + §2 Dead Reckoning)
- `concepts/published-vs-commonly-reported.md` — **created** (§2 + ⚠ Hazard + QC1.2) — *carries an unresolved AUTHOR-REVIEW*
- `concepts/blueprint-change-2025-11-24.md` — **created** (§3) — *carries a contested-provenance flag*
- `concepts/domain-weights-44-28-16-12.md` — **created** (§3 ★ Fixed Point + §5 disclosure)
- `concepts/cloud-native-framing.md` — **created** (§4 + Extended Analogy + QC2.3)
- `concepts/spaced-retrieval.md` — **created** (§5 + QC2.2) — *encodes a hard Ch 13 ← Ch 8 contract*
- `concepts/reading-paths.md` — **created** (§6 + Logbook Entry + QC2.1)

**Not created, with reasons:**
- `cncf-certification-ladder` — Chapter 1 gives it three sentences and explicitly defers to Ch 17 §4. Below threshold; glossary row only. **Ch 17's Stage 14 creates this shard.**
- `branded-markers` — brand-level canon, already authoritative in `knowledge-base/voice/branded-terms.yaml`. Duplicating it per-book invites drift. Chapter 1's §5 legend is a *reader-facing rendering* of that canon, not a second source of truth.

### Canon conflicts carried into the shards (Rule 6)

No existing shard was overwritten — none existed. But three ratified-canon conflicts are recorded **inside the shards themselves**, loudly, because Chapters 19 and 20 will read these shards and would otherwise inherit the wrong figure silently:

1. **Retired blueprint weights (46 / 22 / 16 / 8 / 8) have contested provenance.** The fact-accuracy audit verified them verbatim against `lf-kcna-program-changes-2026-08-23`; the curriculum-alignment audit reports that snapshot is stale and a correction was cached but never written to `sources/`. Both cannot be right. `blueprint-change-2025-11-24.md` opens with this in a fenced warning block and marks every derived figure — the −2 / +6 / ×2 annotations, the "under-serve by roughly half" test, `ch01-fig01`'s left column — as blocked pending resolution. **The structural claim (five domains → four, Observability folded into Architecture) is independently sourced and survives either way**, so the shard separates the two cleanly.
2. **Competency count: 13, not 12.** B2 says "12 competencies" and "twelve named competencies" twice. The cached CNCF curriculum snapshot enumerates 4 + 4 + 2 + 3 = **13**, and B1's own `D1.1`–`D4.3` identifier scheme yields 13 identifiers. `objective-coverage.md` is seeded with all thirteen and records the discrepancy at the top. **Chapter 1 is correct; the ratified outline is wrong** — correcting B2 is an author action outside this stage's write scope.
3. **`ch01-fig02` Part names diverge from B2's ratified titles**, and label Part VI "Departure" while Chapter 1 is itself "Taking Departure" (B2's Part I). Recorded in `reading-paths.md` as a blocking figure-spec fix, since the shard describes the book's own structure.

---

## Voice-exemplar candidates nominated

**Not written to `voice-exemplars.md`** — Rule 1. Nominations only; the author promotes to LOCKED. Note that the current exemplar file is anchored on CAPM Ch 1, and this is the first KCNA chapter, so a promotion here also tests whether the unified voice holds across role families (Navigator → Communications Officer).

| Function | Excerpt | Recommendation |
|---|---|---|
| **chapter-opening / curiosity gap** | "Here is a question worth carrying for the next few pages: **why does so much of the KCNA study material online describe a different exam than the one you are going to sit?** … Not a slightly different exam. A structurally different one … The material isn't fraudulent and its authors aren't careless. Something moved underneath them." | **Strong.** Opens a gap, sets stakes, and refuses to strawman competitors in the same breath — the hardest of the three to do at once. |
| **Extended Analogy** | "You have been handed a chart whose legend is printed on the last page. … Sail the water first. Anchor once on rocky bottom and spend a night listening to the cable grind. Then turn to the legend, and the mark doesn't teach you anything. It *names* something your hands already know." | **Strongest in the chapter.** Maritime register doing real pedagogical work, not decoration; justifies a structural decision rather than ornamenting one. Best available exemplar of §18.15 sidebar craft. |
| **Dead Reckoning** | "The KCNA is an online, proctored, multiple-choice exam. Duration is 90 minutes. There are no prerequisites. Registration includes a 12-month eligibility window … Pricing at the time this book's sources were captured (2026-08-23)…" | **Strong.** Textbook facts-only register: no metaphor, no framing, and it dates its own volatile figures inline. |
| **⚠ Navigational Hazards** | "The hazard here is not the exam. It's the habit of treating a widely-repeated number as a published one. … 'A quarter of the way through the questions when a quarter of my time is gone' survives any question count. 'Question 15 at the 22-minute mark' does not." | **Strong.** Names the hazard, shows the failure mode, hands over a correction that costs nothing. Model for the marker. |
| **why-wrong explanation** | "**D is wrong**, and it's the trap §3 sets by accident. A domain that doubled from a small base is still small. Growth rate is not exam share … Sixteen does not outrank forty-four." | **Strong.** Diagnoses the *reasoning* error, not just the answer, and admits the chapter set the trap itself. |
| **⚓ Worth Securing (inline callout)** | "A conceptual exam deserves a conceptual study method. … you will not pass this exam by drilling `kubectl` commands, and you can fail it while typing them fluently. Study for discrimination: for every concept, ask 'what is the thing this is most often confused with, and what's the difference?'" | **Moderate–strong.** Good §18.14 length discipline; first inline-glyph exemplar in the series if promoted. |
| **cliffhanger / The Voyage Ahead** | "The intermodal shipping container changed global trade not by being a better box, but by being a box that cranes, truck beds, railcars, and ships' holds could all agree to handle identically. The contents stopped mattering to the infrastructure." | **Moderate.** Excellent as prose. Hold until Ch 2's research pass caches the intermodal-history source — the passage currently carries an open `AUTHOR-REVIEW` for exactly this. |
| **Logbook Entry** | "A colleague of mine sat the KCNA earlier this year having studied hard from a course recorded in 2024. … Ten minutes of a ninety-minute exam spent recalibrating is over a tenth of your time, and it goes at exactly the moment your composure matters most." | **Conditional — do not promote yet.** Stage 13 referred the first-person-anecdote posture for author decision (Part 14: real story vs. fabricated scenario). This is the book's first Logbook Entry, so whichever framing is chosen becomes canon for nineteen chapters. Promote *after* that call, not before — promoting it would silently ratify the posture. |
| **honest-register / study time** | "Anyone quoting you a precise number ('Pass in 14 days!') is selling something … This is not a credential you grind. It's one you understand." | **Conditional.** Last sentence is excellent. The first imputes motive rather than describing an error — Stage 13 flagged it. Promote the closing pair only, or promote after rewording. |

---

## Objective coverage log

`objective-coverage.md` — **created.** Chapter 1 covers **no objectives** (orientation, 0% weight, `objectives: []` in frontmatter). Rather than write a single empty row, the ledger is seeded with all **13** competency identifiers and their planned home chapters from B2, so it is useful the moment Chapter 2 runs.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| — (none) | Chapter 1 | n/a — orientation chapter, no domain objectives | 2026-08-24 |

Full 13-row registry with planned homes is in the write block below.

---

## Retrieval-practice ledger

`retrieval-log.md` — **created.** Chapter 1 contains **zero retrieval items, which is correct**: B3 excludes Ch 1 from the retrieval schedule entirely (orientation, 0% weight), and the ramp begins at Ch 3 drawing 10% from Ch 2.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| *(none — Ch 1 is excluded from the retrieval schedule by design)* | — | — |

Two forward-looking entries **are** recorded, because Chapter 1 makes a bindable promise in prose:

| Commitment | Source | Status |
|---|---|---|
| **Ch 13's checkpoint must carry a Ch 8 retrieval item** (version skew, as a troubleshooting cause) | Ch 1 §5 states it in plain text; QC2.2 makes the pairing a whole question; B3 schedules it deliberately | **Binding contract — open.** If Ch 13 ships without it, Chapter 1 has told the reader something false about the book, in the section teaching them to trust the mechanism. |
| **★ `44 / 28 / 16 / 12` is designated must-memorize but is never retrieval-tested** | B3 lists "Ch 1 mechanics" among four things that must not be retrieved | **Open — author decision.** Stage 13's cheapest resolution: let Ch 19 retrieve the weights *instrumentally* (allocate remaining study time across domains) rather than as trivia, which stays inside B3's exclusion. |

---

## Operator notes (not chapter defects, not fixed by this stage)

1. **`book-outline/retrieval-architecture.md` is a stage-failure notice, not the B3 artifact.** Verified on disk: the file contains a permission-denied message plus a prose summary. Every subsequent chapter's retrieval planning will read it. I transcribed the summary into `retrieval-log.md` under a loud **PROVISIONAL** fence rather than presenting it as canon — but **re-run B3 with write access before Chapter 3**, which is where the schedule actually starts.
2. **Outline frontmatter is stale and this stage did not correct it** (outside write scope): `question_budget` still reads `taking_your_bearings: 5` / `total_this_chapter: 10`; the finalized chapter carries **6** across 3 + 3, total **11**. The book-level question-budget rollup will read low until amended.
3. **`kb_tags.commands: []` is stale** — `kubectl` surfaces in Chapter 1 (named, not taught). The glossary reserves it against Ch 8. If a command index is ever built from those tags, Chapter 1's tag needs `kubectl` added.
4. **`diagnostics/structural.md` reports `0 fail, 0 warn, 0 pass`** — zero *passes* means the linter evaluated no checks, so this chapter has no independent structural corroboration. Both Stage 13's counts and this stage's were taken by hand.

---

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===
# KCNA — Knowledge-Base Glossary Ledger

**Working ledger, not the shipped artifact.** This file tracks which terms the book
surfaces, which chapter defines each one, and what definition was actually written.
The published `glossary.md` at the book root (required by skill Part 16, minimum 100
terms) is generated from this ledger at book assembly, once every reserved term has a
real definition.

**Conventions locked at Chapter 1** (per Stage 13 recommendation; author-ratifiable):

1. **Cross-reference cites the chapter of DEFINITION, not first mention.** Chapter 1
   names ~20 terms it never teaches. Citing first mention would point a third of the
   glossary at the orientation chapter.
2. **Reserved terms carry no prose.** A term surfaced but not defined gets a row and a
   defining chapter, nothing more. Paraphrasing a cached source into a definition the
   chapter never wrote is definitional drift, which is worse than no entry.
3. **`curriculum`** = the CNCF-published document (`KCNA_Curriculum.pdf`).
   **`blueprint`** = the domain-and-weight structure that document describes.

Last updated: 2026-08-24 (Chapter 1, Stage 14)
Terms tracked: 35 — 10 defined · 4 conventions · 19 reserved · 2 optional

---

## Tier 1 — Defined (prose inherited verbatim from chapter text)

### C

**CKA (Certified Kubernetes Administrator)** — "a genuinely hands-on exam taken in a
live terminal." *Partial: Chapter 1 defines it only by contrast with the KCNA's
multiple-choice format.* (Surfaced Ch 1 §1 · full treatment Ch 17 §4)

**cloud native** — "describes characteristics of how a system is built and operated."
It does **not** mean "runs in a public cloud": "The CNCF's own definition covers
workloads deployed across public, private, and hybrid environments."
*DEFERRING ENTRY — the positive definition, with each characteristic examined, is
Chapter 17 §1. Chapter 1 §4 deliberately withholds it for four hundred pages; this
entry preserves that device by carrying only the negative claim, which §4 states
outright anyway.* (Surfaced Ch 1 §1 · defined Ch 17 §1)
> ⚑ AUTHOR DECISION OPEN. Stage 13 referred the glossary-vs-§4 collision without
> defaulting it. Options were: (a) this deferring entry, (b) a full entry accepting
> the spoil, (c) omission. (a) is implemented. Reversible — only this entry changes.

**CNCF (Cloud Native Computing Foundation)** — the open-source foundation that hosts
Kubernetes; "part of the nonprofit **Linux Foundation**." (Ch 1 §1, Soundings A3)

**competency** — *convention, see Tier 2.*

**container** — "a process on the host that has been given an isolated view of the
system." Shares the host's **operating system kernel** with the host; contrast with a
virtual machine, which "boots its own operating system on virtualized hardware."
*Partial: Chapter 1 Soundings A1 gives the discriminating fact only.*
(Surfaced Ch 1 · full treatment Ch 2 §1)
> ⚑ PROVISIONAL WORDING. Open `AUTHOR-REVIEW` in the Ch 1 draft: the cached snapshot
> `k8s-docs-overview-2026-08-23` says containers share "the Operating System (OS)
> among the applications," not specifically the kernel. The chapter's "operating
> system kernel" is a sharpening — more precise and more standard, but not verbatim
> from the source. Chapter 2's Stage 14 must NOT lock the sharpened form until this
> is resolved.

**container runtime** — the component that "does the work of actually starting the
containers"; one runs on each machine, separate from the orchestrator.
*Partial.* (Surfaced Ch 1 Soundings A2 · full treatment Ch 2)

**curriculum** — *convention, see Tier 2.*

### D

**domain** — *convention, see Tier 2.*

### K

**KCNA (Kubernetes and Cloud Native Associate)** — "the usual entry point to the cloud
native certification family." The Linux Foundation "describes it as demonstrating 'a
user's foundational knowledge and skills in Kubernetes and the wider cloud native
ecosystem.'" Experience level: beginner. Prerequisites: none.
[source: lf-kcna-exam-page-2026-08-23] (Ch 1 §1)

### L

**Linux Foundation, The** — the nonprofit organization that publishes the KCNA exam and
of which CNCF is part. *Partial.* (Ch 1 §1)

**Lodestar, The** (book artifact) — "a single page holding the exam-critical facts,
distinctions, and traps, distilled from the whole book. It's the last thing to read
before the exam." Ships as `the-lodestar.md` at the book root. (Ch 1 §5)

### O

**orchestrator / container orchestration** — "Kubernetes is an **orchestrator** — it
decides what should run where." Distinct from the container runtime, which starts the
containers. *Partial.* (Surfaced Ch 1 Soundings A2 · full treatment Ch 3)

### V

**virtual machine** — "boots its own operating system on virtualized hardware."
*Partial: contrast with container only.* (Surfaced Ch 1 · full treatment Ch 2 §1)

---

## Tier 2 — Convention locks (NOT chapter definitions)

Used precisely throughout Chapter 1 but never explicitly defined there. Recorded as
conventions so nothing masquerades as inherited prose. Chapters 19 and 20 reason about
all four repeatedly and will diverge without them.

| Term | Convention | Status |
|---|---|---|
| **blueprint** | The domain-and-weight *structure* the CNCF curriculum describes | Proposed — Ch 1 body follows it 11×; subtitle and §3 heading say "curriculum" rhetorically |
| **curriculum** | The CNCF-published *document* (`KCNA_Curriculum.pdf`) | Proposed — pairs with the above |
| **competency** | A named topic *inside* a domain. There are **13** | Proposed — see `objective-coverage.md` for the count discrepancy against B2 |
| **domain** | One of the four weighted blocks: 44 / 28 / 16 / 12 | Proposed |

Stage 13 recommends stating the curriculum/blueprint pair once in front matter, and
adding the chapter-of-definition rule to `structural-contract.yaml` so the linter can
check it. Both are author actions; this stage does not modify either file.

---

## Tier 3 — Reserved (surfaced in Ch 1, defined later — NO definition written)

Defining chapters assigned from B2 (`chapter-lineup.md`, ratified).

| Term | Defining chapter | First surfaced |
|---|---|---|
| CNCF Cloud Native Definition v1.1 | Ch 17 | Ch 1 §4 |
| Container Runtime Interface (CRI) | Ch 2 | Ch 1 Soundings A2 (cross-bearing label) |
| declarative vs imperative | Ch 4 | Ch 1 Soundings Q5 |
| deployment strategy | Ch 6 (mechanics) / Ch 15 (vocabulary) | Ch 1 §3 |
| exporter | Ch 18 | Ch 1 §6 (Logbook Entry) |
| GitOps | Ch 15 | Ch 1 §3 |
| Helm | Ch 14 | Ch 1 §3 |
| `kubectl` | Ch 8 | Ch 1 §1 |
| metrics | Ch 18 | Ch 1 §3 |
| observability | Ch 18 | Ch 1 §3 |
| OpenTelemetry | Ch 18 | Ch 1 §3 |
| Pod | Ch 5 | Ch 1 §1 |
| Prometheus | Ch 18 | Ch 1 §3 |
| PromQL | Ch 18 | Ch 1 §6 (Logbook Entry) |
| scheduler / scheduling | Ch 7 | Ch 1 §1 |
| scrape (pull) model | Ch 18 | Ch 1 §6 (Logbook Entry) |
| Service | Ch 9 | Ch 1 §1 |
| StatefulSet | **Ch 6** (introduced) / Ch 11 (completed) | Ch 1 §5 (cross-bearing label) |
| traces | Ch 18 | Ch 1 §3 |

**Optional (product names — author call whether they belong in a published glossary):**
LFS250 (Ch 1 §2), THRIVE-ONE (Ch 1 §2).

**Deliberately excluded:**
- Terraform, Ansible, CloudFormation — external tools named for calibration in
  Soundings Q5; not KCNA exam terms.
- Branded markers (🧭 ☆ ★ ⚠ — 🏆 ☀️), inline glyphs (⚓ 🪝 🔭 🪢), sidebar types,
  cross-bearings, difficulty indicators (⚪🔵🟡🔴) — brand-level canon, authoritative in
  `knowledge-base/voice/branded-terms.yaml`. Chapter 1 §5's legend is a reader-facing
  rendering of that canon, not a second source of truth.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kcna-exam-format.md ===
# Concept: KCNA exam format

**Slug:** `kcna-exam-format`
**First taught:** Chapter 1 §1–§2
**Status:** established (dated figures)
**Sources:** `lf-kcna-exam-page-2026-08-23`, `lf-cloud-native-certification-catalog-2026-08-23`

## What Chapter 1 establishes

The published, verifiable facts about the exam, stated in a Dead Reckoning block so
they carry no framing:

- Online, proctored, **multiple-choice** exam
- Duration **90 minutes**
- **No prerequisites** — no required course, no logged hours, no prior certification,
  no attestation of experience
- Experience level: **beginner**
- Registration includes a **12-month eligibility window**, **two exam attempts**, and
  an exam preparation handbook
- Certification valid **2 years**
- Pricing as of 2026-08-23: **$250** exam only · **$299** with LFS250 · **$495** with
  THRIVE-ONE annual subscription

## The interpretive claims Chapter 1 attaches (these must not drift)

**The KCNA measures discrimination, not execution.** "The hands-on Kubernetes
certifications … measure whether you can *do* the thing. The KCNA measures whether you
can *discriminate*." This is the chapter's central framing for study method and it
governs how every subsequent chapter writes its questions: for every concept, name the
thing it is most often confused with.

**Two attempts is a structural feature, not a consolation prize.** "The second attempt
is part of what you bought … failing once costs you time and morale, not money."

**Two years of validity is honest, not stingy.** "Cloud native tooling moves fast
enough that a five-year credential would be a fiction."

**This book is explicitly not a `kubectl` drill book.** "There are commands in it,
because you cannot understand a Service without seeing how one is described, but the
commands are here to illuminate concepts, not to build reflexes."

## Downstream obligations

- **Volatility.** Pricing and bundle names are the most volatile facts in the book and
  the least load-bearing. Chapter 1 dates them inline and tells the reader to check the
  exam page. Any chapter restating a price must carry the same date stamp.
- **Ch 17 §4** owns the full certification ladder; Chapter 1 deliberately defers it.
- **Ch 19 §3** owns exam-day pacing; Chapter 1 defers it and only establishes the
  proportional-pacing rule (see `published-vs-commonly-reported`).
- **Ch 20** is sized to the commonly-reported format and must be framed as a calibrated
  instrument, never as a match to a published count.

## Contested / unresolved

None. Every fact in this shard is verbatim from the cached exam-page snapshot.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/published-vs-commonly-reported.md ===
# Concept: Published vs. commonly-reported exam facts

**Slug:** `published-vs-commonly-reported`
**First taught:** Chapter 1 §2 (+ ⚠ Navigational Hazards, QC1.2)
**Status:** ⚑ **CONTESTED — one open AUTHOR-REVIEW. Read before reusing.**
**Sources:** `lf-kcna-exam-page-2026-08-23`

## What Chapter 1 establishes

> The Linux Foundation's KCNA exam page **does not state a question count or a passing
> score.** The page states the format, the duration, the eligibility terms, the price,
> and the domain weights.

The widely-circulated "**60 questions, 75% to pass**" figures are **commonly reported by
third parties**, not stated where the certifying body describes this exam. Chapter 1
flags this every time either figure appears, and QC1.2 makes it a checkpoint question.

**The generalized habit is the chapter's real payload**, and it is more portable than
the fact: *"know which of your facts are published and which are inherited."*

## The hazard and its correction (verbatim — do not reword)

> A study plan built on "60 questions in 90 minutes" yields a pacing rule of 90 seconds
> per question, and that rule feels precise and authoritative. If the real count is
> different, the rule is wrong, and you find that out at minute forty of a ninety-minute
> exam, with a proctor watching and no way to reset.
>
> The correction costs nothing: pace by *proportion of elapsed time*, not by question
> number. "A quarter of the way through the questions when a quarter of my time is
> gone" survives any question count. "Question 15 at the 22-minute mark" does not.

## ⚑ CONTESTED PROVENANCE — unresolved

The curriculum-alignment audit reports that the Linux Foundation **does** publish a 75%
passing score for multiple-choice exams, in its multiple-choice candidate FAQ
(`docs.linuxfoundation.org/tc-docs/certification/faq-mc`), and that the research stage
cached a corrected snapshot which was never written to `sources/`. **No such snapshot
exists on disk**, so the claim cannot be verified.

Chapter 1 has been narrowed to what the cached exam-page snapshot supports verbatim
("not stated on this page"), which is true under either reading.

**If the FAQ snapshot lands**, rewrite to the two-provenance framing: the passing score
**is** published (75%, in a candidate FAQ most readers never open) while the question
count is published **nowhere**. That sharpens the hazard rather than weakening it.

**Do not resolve this from memory.** Any chapter reusing this concept inherits the
narrowed framing until the snapshot exists.

## Downstream obligations

- **B2 disclosure #2** requires this be stated up front and that Ch 20's mock be framed
  as a calibrated instrument.
- **B3 exclusion:** the unpublished 60-question/75% figures must **never** be retrieval-
  tested. Testing an inherited number as if it were a fact inverts the whole lesson.
- **Ch 19 §3** (pacing) and **Ch 20 §1** (mock sizing) both depend on this framing.
- Chapter 1's own quantifier claims — "repeated across dozens of study sites, videos,
  and forum threads," "widely and consistently reported" — are themselves **uncited**.
  Stage 13 flagged the irony directly. Either cache two or three representative
  third-party pages during a later research pass, or drop "dozens" and let the
  qualitative claim stand.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/blueprint-change-2025-11-24.md ===
# Concept: The 2025 blueprint restructure

**Slug:** `blueprint-change-2025-11-24`
**First taught:** Chapter 1 §3
**Status:** ⚑ **PARTIALLY CONTESTED — structural claim sound, retired weights disputed.**
**Sources:** `lf-kcna-program-changes-2026-08-23` (disputed), `lf-kcna-exam-page-2026-08-23`,
`cncf-kcna-curriculum-pdf-2026-08-23`
**Figure:** `ch01-fig01-blueprint-change-2025`

---

## ⚑ READ THIS FIRST — contested provenance

Two audits disagree and **both cannot be right**:

- The **fact-accuracy audit** verified the five retired weights (46 / 22 / 16 / 8 / 8)
  verbatim against the cached snapshot `lf-kcna-program-changes-2026-08-23`.
- The **curriculum-alignment audit** reports that snapshot is **stale** — that the
  retired percentages were never on the LF page, that a correction was cached, and that
  it could not be written to `sources/`.

**Blocked pending resolution** (do not reuse in any chapter until settled):
the five retired weights; `ch01-fig01`'s left column; the −2 / +6 / ×2 annotations; the
"under-serve Application Delivery by roughly half" test; the Logbook Entry's premise.

**Resolution path:** (a) retrieve the retired curriculum PDF from
`cncf/curriculum/old-versions/` and cache it as
`cncf-kcna-curriculum-retired-2026-08-23.md`, or (b) if that fails, cut all five
percentages and respec `ch01-fig01` as a one-sided "what moved" diagram.

**Do NOT source the weights from the CNCF-hosted Medium repost.** That is a syndicated
guest post — the exact diffusion mechanism §2 teaches readers to catch.

---

## What survives regardless (independently sourced — safe to reuse)

The **structural** claims are not in dispute:

- The blueprint was restructured, **effective no earlier than 2025-11-24**.
- **Five domains became four.**
- **Cloud Native Observability ceased to exist as a standalone domain.** It was folded
  in as a competency under **Cloud Native Architecture**, alongside Cloud Native
  Ecosystem and Principles, and Cloud Native Community and Collaboration.
- Observability content is **still examinable**. Nothing was removed; it was reorganized.
- The current four domains and weights are **44 / 28 / 16 / 12** (see
  `domain-weights-44-28-16-12`).

## The reader-facing test (the section's real payload)

**Count the domains.** Material organized around **five** domains, or carrying a
standalone "Cloud Native Observability" section presented as a domain in its own right,
was built for the retired blueprint.

> "That doesn't make its facts wrong; a Pod worked the same way in 2024. But its
> *weighting* is wrong, which makes its emphasis wrong, which makes its practice sets
> wrong … Use it for facts if you like. Don't use it to allocate your time."

This test is stated to take "about fifteen seconds of skimming" and is set up by the
chapter's opening curiosity gap.

## 🪝 The Snag worth preserving

Cloud Native Architecture appears in both blueprints at different weights, but it is
**not the same domain in a smaller hat**. It *gained* observability while *losing*
weight, so its remaining material is compressed harder than the number alone suggests.
Do not reason about it by comparing the two percentages.

## Missing reader-facing consequence (gap — do not add unsourced)

The curriculum-alignment audit recovered a consequence this section should carry and
currently does not: **the only date that determines which blueprint you are examined
against is the date you SIT the exam** — not the purchase date, not first-attempt-
versus-retake. This claim is **not present in any cached snapshot on disk.** Add it with
a citation once the corrected `lf-kcna-program-changes` snapshot lands.

## Downstream obligations

- **B2 disclosure #3** requires this be stated up front for readers arriving with older
  material.
- **Ch 14–16** (Application Delivery) carry the largest consequence of the restructure.
- **Ch 18 §1** teaches observability under the current blueprint and must not present
  it as a standalone domain.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/domain-weights-44-28-16-12.md ===
# Concept: The four domain weights — 44 / 28 / 16 / 12

**Slug:** `domain-weights-44-28-16-12`
**First taught:** Chapter 1 §3 (★ Fixed Point) + §5 (disclosure)
**Status:** established — the single most-repeated fact in the book
**Sources:** `lf-kcna-exam-page-2026-08-23`, `cncf-kcna-curriculum-pdf-2026-08-23`
**Figure:** `ch01-fig02-book-map-parts-to-domains`

## ★ Fixed Point (verbatim)

> **The current KCNA blueprint is four domains: Kubernetes Fundamentals 44%, Container
> Orchestration 28%, Cloud Native Application Delivery 16%, Cloud Native Architecture
> 12%.**

Chapter 1 designates this as the chapter's single ★ Fixed Point: "If you memorize one
thing from this chapter, memorize those four numbers. They are the index to everything
else."

## The 13 competencies

| Domain | Weight | Competencies |
|---|---|---|
| Kubernetes Fundamentals | 44% | Kubernetes Core Concepts; Administration; Scheduling; Containerization |
| Container Orchestration | 28% | Networking; Security; Troubleshooting; Storage |
| Cloud Native Application Delivery | 16% | Application Delivery; Debugging |
| Cloud Native Architecture | 12% | Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration |

**4 + 4 + 2 + 3 = 13.** See `objective-coverage.md` — the ratified B2 lineup says
"twelve," which is wrong.

## Canonical notation

**`44 / 28 / 16 / 12`** is the canonical shorthand (Stage 13 recommendation). The
middot form `44 · 28 · 16 · 12` is reserved for the 🪢 Mnemonic, where the visual
difference is doing work. Prose may write them as percentages in full.

## 🪢 The mnemonic (verbatim)

> The weights descend: **44 · 28 · 16 · 12**. Four numbers, each smaller than the last,
> no ties to confuse. … **44 and 28 together make 72%.** Kubernetes itself and its
> orchestration mechanics are nearly three-quarters of the exam. The remaining 28% is
> everything *around* Kubernetes: how you deliver to it, and the ecosystem it lives in.

## The two disclosures that must travel with the weights

**1. Domain-level only.** "The CNCF publishes weights at the domain level only. There is
no published per-competency or per-topic weighting." Every per-chapter emphasis figure
in this book is **authored judgment**, derived from concept count and prerequisite load,
and must be disclosed as such. (B2 disclosure #1; Ethical Guardrail #4.)

**2. Maximum divergence 2.8 points.** Part II holds 7 of 17 content chapters (41.2%)
against Kubernetes Fundamentals' 44%. The other three Parts land within 1.6 points.
**"Where chapter allocation and exam weight diverge … trust the weights."**

## How the weights are used (QC1.3 — the reasoning to preserve)

Correct allocation is **weight-proportional first, personal-weakness-adjusted second.**

Two errors Chapter 1 traps explicitly:
- **Chapter count is not exam share.** "Chapter count tracks *how much explaining a
  topic needs*, not *how many questions it generates*."
- **Growth rate is not exam share.** "A domain that doubled from a small base is still
  small … Sixteen does not outrank forty-four."

## Downstream obligations

- Every **Part opener** states its domain and weight.
- **`the-lodestar.md`** carries the quad.
- **Ch 19** synthesizes against it; **Ch 20** is weighted to it (±2 points per skill
  Part 16).
- **B3 exclusion:** Ch 1 mechanics must not be retrieval-tested, so this ★ Fixed Point
  is the one must-memorize fact never retrieved. Stage 13 referred this; the suggested
  resolution is a Ch 19 item that uses the weights *instrumentally* (allocate remaining
  study time) rather than testing them as trivia.

## Contested / unresolved

The **current** weights are solid — verbatim in two independent cached snapshots. Only
the **retired** weights are contested; see `blueprint-change-2025-11-24`.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cloud-native-framing.md ===
# Concept: The deferred "cloud native" definition

**Slug:** `cloud-native-framing`
**First taught:** Chapter 1 §4 (+ Extended Analogy, Soundings Q4, QC2.3)
**Status:** established — **structural device spanning Ch 1 → Ch 17**
**Sources:** `cncf-cloud-native-definition-2026-08-23`

## The device

Chapter 1 uses "cloud native" ~14 times, including in the credential's name and two of
four domain names, and **deliberately does not define it.** The positive definition —
the CNCF Cloud Native Definition v1.1, examined characteristic by characteristic — is
**Chapter 17 §1**.

The chapter tells the reader this is deliberate rather than letting them wonder:

> Why wait four hundred pages for a definition I could give you in a paragraph? Because
> those are two different experiences of the same sentence. Read on page ten, the
> definition is vocabulary … Read in Chapter 17, after you have met containers,
> orchestration, declarative APIs, services, and delivery pipelines in person, every
> clause lands as a description of something you now recognize.

**"It's the only thing this book asks you to carry that far."**

## What Chapter 1 DOES establish (the negative claim — safe to reuse)

**"Cloud native" does not mean "runs in a public cloud."**

- "The CNCF's own definition covers workloads deployed across public, private, and
  hybrid environments" [source: cncf-cloud-native-definition-2026-08-23]
- "A rack of hardware in your own building can be thoroughly cloud native, and renting
  cloud instances does not by itself make a system cloud native."
- QC2.3: "'Cloud native' describes characteristics of how a system is built and
  operated, not where it runs."
- It is "doing real technical work in those names. It is not decoration and it is not a
  synonym for 'modern.'"

The misconception is pre-tested in Soundings Q4 and corrected in QC2.3 — the same
concept, bracketed pre- and post-reading, which is the Soundings/Bearings pattern
working as designed.

## Three distractor errors worth preserving (QC2.3)

- **A** — the bare form: cloud native requires a public cloud. "The phrase contains the
  word 'cloud,' which does most of the misleading on its own."
- **B** — the halfway version: "conceding that location isn't the test, then smuggling
  it back in as 'well, *some* cloud services, surely.'"
- **D** — multi-cloud. "It appears nowhere in the definition."

## The Extended Analogy (nominated voice exemplar — preserve intact)

The chart whose legend is printed on the last page. "Sail the water first. Anchor once
on rocky bottom and spend a night listening to the cable grind. Then turn to the legend,
and the mark doesn't teach you anything. It *names* something your hands already know."

## Downstream obligations — binding

1. **No chapter between 2 and 16 may define "cloud native."** Doing so breaks a device
   Chapter 1 explicitly promised the reader and justified at length.
2. **Chapter 17 §1 must deliver the full CNCF definition, unabridged, characteristic by
   characteristic.** Chapter 1 promises exactly this, three times, in three separate
   cross-bearings. It is a commitment, not a preference.
3. **The glossary carries a deferring entry only** — negative claim, pointer to Ch 17.
   See `glossary.md`; this is flagged for author ratification.
4. B2 confirms the design: "Ch 1 plants the framing; Ch 17 … delivers the institutional
   material."
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/spaced-retrieval.md ===
# Concept: Spaced retrieval and the Soundings instrument

**Slug:** `spaced-retrieval`
**First taught:** Chapter 1 §5 ("Two mechanisms that look like padding and aren't") + QC2.1, QC2.2
**Status:** established — **carries one binding forward contract**
**Sources:** ⚑ **none cached** — see the citation gap below

## What Chapter 1 tells the reader

**Soundings are an instrument, not a quiz.** "Nothing is scored, recorded, or held
against you." Two stated purposes: pre-testing improves subsequent learning even when
answers are wrong, and "a score gives you something more useful than a grade: a reading
instruction. High score, skim. Low score, slow down."

QC2.1 hardens this: a low Soundings score is a **pacing instruction for the chapter
ahead**, never a verdict, and never a signal that earlier material was missed — "The
questions test *priors you brought with you*, not material the book has taught."

**Later chapters test earlier chapters' material, on purpose.**

> Chapter 13's checkpoint will ask you something from Chapter 8. This is going to feel,
> the first few times, like the book forgot it already covered that. It didn't.
> Retrieving a fact after you've had time to partly forget it strengthens the memory far
> more than rereading it would. … When you hit one of those questions and think *we did
> this already*, that thought is the mechanism working. Answer it anyway.

QC2.2 inoculates against the skip reflex: "It's the one structural feature of this book
most likely to be skipped by readers trying to be efficient, and skipping it costs the
most."

**Retrieval items are scheduled by spacing interval, not prerequisite relationship**
(QC2.2 distractor C). This matters: it is why a retrieval item may appear in a chapter
that does not depend on its source chapter.

## ⚑ BINDING CONTRACT — Ch 13 must carry a Ch 8 retrieval item

Chapter 1 §5 names the pairing **in plain reader-facing text**, and QC2.2 makes it the
subject of a whole question. Both are verified against ratified canon:

- B3 places Chapter 8's **version-skew** material into Chapter 13 as a troubleshooting
  cause — version skew is "the densest pure-recall material in the book, taught at the
  40% mark and otherwise never revisited before exam day."
- Ch 13 ← Ch 8 is exactly 5 chapters back, satisfying B3's spacing floor.
- QC2.2 distractor C asserts Ch 13 does not depend on Ch 8. **Accurate** — B2 lists
  Ch 13's prerequisites as 5, 7, 9, 11.

**If Chapter 13's checkpoint ships without a Chapter 8 retrieval item, Chapter 1 has
told the reader something false about the book, in the section whose entire purpose is
teaching them to trust the mechanism.** Tracked in `retrieval-log.md`.

## ⚑ CITATION GAP — open AUTHOR-REVIEW (book-level)

Both mechanisms make learning-science claims, and the retrieval paragraph explicitly
appeals to external research: **"That's a well-established effect."** No cached source
covers learning science.

This chapter spends §2 teaching readers to distinguish published facts from inherited
ones, then makes an unsourced appeal to research two sections later. Worth closing
rather than waiving.

**Open a BOOK-LEVEL research gap** (both mechanisms are book-wide — cache once, not per
chapter): Roediger & Karpicke (2006) on the testing effect; Richland, Kornell & Kao
(2009) on pretesting; Bjork on desirable difficulties.

**If the gap will not be filled,** downgrade "That's a well-established effect" to
authorial framing so it stops claiming external authority.

## Downstream obligations

- **Ch 3** is the first chapter carrying retrieval items (B3: 10%, drawing from Ch 2).
- **The `[retrieval: chN]` tag's rendered form is still unresolved** — reader-visible or
  draft-only annotation. Chapter 1 correctly carries none, but §5 describes the
  mechanism to readers in prose, so the decision has a reader-facing dimension.
  **Chapter 3 is the first chapter that needs it settled.**
- Every chapter's Soundings must be answerable from prerequisites (skill Part 11), which
  in this book means earlier chapters — making every Soundings block a free spaced-
  retrieval event. B3 excludes them from the budget deliberately, to protect their
  calibration purpose.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/reading-paths.md ===
# Concept: The three reading paths and the book's self-description

**Slug:** `reading-paths`
**First taught:** Chapter 1 §5–§6 (+ Logbook Entry, 🪝 Snag)
**Status:** established — **three items referred for author decision**
**Figure:** `ch01-fig02-book-map-parts-to-domains`

## Structural claim the whole book rests on

**Parts II–V map one-to-one onto the four exam domains.** "That isn't a coincidence of
organization; it's the point. 'I've finished Part III' and 'I've covered the Container
Orchestration domain' are the same statement."

Parts I and VI carry no exam weight — "which is itself worth knowing."

## The three paths (verbatim commitments)

**No Kubernetes exposure:** read linearly, no skipping. Give **Ch 2 and Ch 3 a study
session each**. "They carry the conceptual load everything else rests on, and rushing
them is a false economy that shows up six chapters later."

**From operations, new to Kubernetes:** read linearly, but check the Ch 2 Soundings
score first — container-fundamentals material is skimmable for this reader. Likely
blind spots: **Part IV's delivery tooling and Ch 17's ecosystem and community material.**

**Developer who has deployed to someone else's cluster:** Ch 2, 4, 5, 6 "will feel
familiar. They are not as familiar as they feel … confident partial knowledge is harder
to correct than no knowledge at all." Reliable gaps: **Ch 8, Ch 12, Ch 17.**

**🪝 Snag (verbatim):** "Your Soundings score is a reading strategy, not a verdict. A
1/8 on Chapter 9's Soundings means 'read Chapter 9 carefully' and nothing else. It is
not a prediction about the exam, and it is certainly not information about you."

## On study time — the honest register to preserve

"This is a beginner-level, ninety-minute, conceptual exam … a few weeks of consistent
evening study is a realistic frame. For someone already working around clusters,
considerably less. … the material is finite and well-bounded. **This is not a credential
you grind. It's one you understand.**"

## ⚑ Referred for author decision (three items)

**1. The Logbook Entry is presented as a real first-person anecdote** — "A colleague of
mine sat the KCNA earlier this year…" — stated as fact with specific detail. If real, no
issue. If authored illustration, it is a fabricated factual claim in a chapter whose §2
teaches readers to distinguish what is attested from what is merely repeated (Part 14
draws exactly this line).

Fix is framing, not deletion: "Here is a pattern worth expecting" or "Picture a
candidate who…" costs the passage almost nothing — its force comes from the mechanism it
illustrates, not from its being a specific person.

**This is the first Logbook Entry in the book, so whichever posture is chosen becomes
canon for nineteen more chapters.** Settle it here.

**2. An inferred trap hardened into a superlative fact.** "Chapter 17's community and
collaboration material is what technically strong candidates under-study most
consistently." This traces to B1 as the *analyst's judgment*, and B2 instructs
explicitly: "Inferred traps stay labelled as inferred … chapters must describe those as
'easy to confuse,' never 'frequently tested' — the distinction Ethical Guardrail #8
requires." Recommend hedging to authorial observation.

Also unhedged, twice: "the assumption almost everyone arrives with" (cloud native =
public cloud). Recommend settling **one hedging posture for reader-behavior claims
across the whole book**, since every chapter will make them.

**3. Two small competitor characterizations.** "Anyone quoting you a precise number
('Pass in 14 days!') is selling something" imputes motive rather than describing an
error; "the disclosure that separates this book from most of its competitors" is an
unverified comparative. Neither is a strawman and both are defensible, but Chapter 1
sets tone for the series.

## ⚑ Blocking figure conflict — `ch01-fig02` contradicts ratified B2 Part titles

The figure labels the Parts *Orientation / Kubernetes Fundamentals / Container
Orchestration / Application Delivery / Cloud Native Architecture / Departure*. **B2's
ratified titles** are:

| Part | Ratified title | Chapters | Domain | Weight |
|---|---|---|---|---|
| I | Taking Departure | 1 | — | 0% |
| II | Ship, Cargo, and Company | 2–8 | Kubernetes Fundamentals | 44% |
| III | Underway | 9–13 | Container Orchestration | 28% |
| IV | Dispatches | 14–16 | Cloud Native Application Delivery | 16% |
| V | The Wider Sea | 17–18 | Cloud Native Architecture | 12% |
| VI | Making Port | 19–20 | — | 0% |

These carry the **Communications Officer** role family's atmospheric register. Beyond the
divergence, the figure's labels have an internal problem: it calls Part **VI**
"Departure," while Chapter 1 is itself "Taking Departure" and B2's Part **I** carries
that name. A departure at the *end* of the voyage reads backwards — B2's Part VI is
"Making Port" for exactly that reason.

**Recommended fix:** print both (`II — Ship, Cargo, and Company · Kubernetes
Fundamentals · 44%`), since the figure's whole argument is that Parts map onto domains.
Requires a matching update in `image-specs.md` **before the diagram pipeline renders it.**

## Downstream obligations

- **Ch 17** must give D4.3 (Community and Collaboration) its own numbered sections,
  Fixed Points, and Soundings coverage — B2's stated mitigation for the under-study risk
  Chapter 1 names.
- **Ch 8, Ch 12, Ch 17** are named to the developer reader as reliable gaps and should
  be written knowing that reader was sent there.
- Every **Part opener** should state its domain and weight, per the one-to-one claim.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===
# KCNA — Objective Coverage Log

Tracks which exam competency each chapter covers, at what depth, and when it was last
reviewed. Seeded at Chapter 1 with the full competency registry so it is useful from
Chapter 2 onward.

**Identifier scheme:** `D<domain>.<competency>` — the Lodestar convention established in
B1. CNCF publishes four domains and thirteen named competencies with **no numbering and
no sub-weights**. Every per-chapter weight figure is authored judgment and must be
disclosed as such in front matter.

---

## ⚑ Competency count: 13, not 12

`chapter-lineup.md` (B2, ratified) states "12 competencies" and "twelve named
competencies," twice. **This is wrong.** The cached CNCF curriculum enumerates
4 + 4 + 2 + 3 = **13**, and B1's own `D1.1`–`D4.3` scheme yields 13 identifiers.
Chapter 1's domain table is correct.

**Correct B2 before Chapter 19's synthesis, the blueprint appendix, or the front-matter
disclosure inherits the wrong figure.** (Author action — outside Stage 14's write scope.)

Sources: `lf-kcna-exam-page-2026-08-23`, `cncf-kcna-curriculum-pdf-2026-08-23`.

---

## Coverage by chapter

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| — (none) | Chapter 1 | n/a — orientation chapter, 0% weight, `objectives: []` | 2026-08-24 |

Chapter 1 covers no exam objectives. It establishes exam mechanics, the 2025 blueprint
restructure, and the cloud-native framing that Chapter 17 later harvests. It does
**name** roughly twenty terms belonging to later competencies without teaching them —
those are tracked as reserved entries in `glossary.md`, not as coverage.

---

## Competency registry (13) — planned homes from B2

| ID | Competency | Domain (weight) | Planned chapter(s) | Status |
|---|---|---|---|---|
| D1.1 | Kubernetes Core Concepts | Kubernetes Fundamentals (44%) | Ch 3, 4, 5, 6 | not yet covered |
| D1.2 | Administration | Kubernetes Fundamentals (44%) | Ch 8 | not yet covered |
| D1.3 | Scheduling | Kubernetes Fundamentals (44%) | Ch 7 | not yet covered |
| D1.4 | Containerization | Kubernetes Fundamentals (44%) | Ch 2 | not yet covered |
| D2.1 | Networking | Container Orchestration (28%) | Ch 9, 10 | not yet covered |
| D2.2 | Security | Container Orchestration (28%) | Ch 12 (+ Ch 10 boundary) | not yet covered |
| D2.3 | Troubleshooting | Container Orchestration (28%) | Ch 13 | not yet covered |
| D2.4 | Storage | Container Orchestration (28%) | Ch 11 | not yet covered |
| D3.1 | Application Delivery | Cloud Native Application Delivery (16%) | Ch 14, 15 | not yet covered |
| D3.2 | Debugging | Cloud Native Application Delivery (16%) | Ch 16 | not yet covered |
| D4.1 | Observability | Cloud Native Architecture (12%) | Ch 18 | not yet covered |
| D4.2 | Cloud Native Ecosystem and Principles | Cloud Native Architecture (12%) | Ch 17 | not yet covered |
| D4.3 | Cloud Native Community and Collaboration | Cloud Native Architecture (12%) | Ch 17 | not yet covered |

**Note on D4.3:** B1 flags it as the competency technically-strong candidates most
reliably under-study. B2's mitigation is not a separate chapter but explicit treatment
inside Ch 17 — its own numbered sections, Fixed Points, and Soundings coverage — plus
disproportionate representation in the Ch 19 synthesis and the Ch 20 mock. Track that
this actually happens.

**Curriculum typo worth recording:** the CNCF-published `KCNA_Curriculum.pdf` contains
"Could Native Community and Collaboration" for D4.3. Candidates who download it will see
it. Belongs in the blueprint appendix.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===
# KCNA — Retrieval-Practice Ledger

Tracks which earlier-chapter topics have been retrieval-tested, and in which later
chapter. Also records forward commitments the prose has made to the reader, which are
binding contracts rather than preferences.

---

## Retrieval items by chapter

| Tested topic | Original chapter | Retested in |
|---|---|---|
| *(none — Chapter 1 is excluded from the retrieval schedule by design)* | — | — |

**Chapter 1: 0 retrieval items, which is correct.** B3 excludes Ch 1 entirely — the
skill's table assumes Ch 1 is a content chapter, but here it is orientation at 0%
weight. The ramp begins at **Ch 3 (10%, drawing from Ch 2)**. The question-quality audit
confirmed 0%/0% compliance.

---

## ⚑ Forward commitments — binding

| # | Commitment | Where stated | Status |
|---|---|---|---|
| 1 | **Chapter 13's checkpoint must carry a Chapter 8 retrieval item** (version skew, framed as a troubleshooting cause) | Ch 1 §5, in plain reader-facing prose; QC2.2 makes the pairing a whole question | **OPEN — verify at Ch 13 Stage 13** |

**Why #1 is a contract, not a preference.** Chapter 1 tells the reader the pairing by
name, then builds a checkpoint question around it whose distractor C asserts (correctly,
per B2) that Ch 13 does not *depend* on Ch 8. B3 schedules it deliberately: version skew
is "the densest pure-recall material in the book, taught at the 40% mark and otherwise
never revisited before exam day," and Ch 13 ← Ch 8 is exactly 5 chapters back, clearing
B3's spacing floor.

If Ch 13 ships without it, Chapter 1 has told the reader something false about the book,
in the section whose entire purpose is teaching them to trust the mechanism. **Flag this
in Chapter 13's chapter-state so it isn't lost fifteen chapters from now.**

---

## Open item — a ★ Fixed Point that is never retrieved

Chapter 1 designates `44 / 28 / 16 / 12` as its single ★ Fixed Point and tells the
reader to memorize it above everything else. B3 then excludes Ch 1 from retrieval
entirely and lists "Ch 1 mechanics" among four things that must *not* be retrieved
anywhere in the book.

Net effect: **the book's most emphatically flagged must-memorize fact is the one fact
never retrieval-tested.** Defensible — the weights are reinforced structurally (Parts
II–V are named for the domains, `the-lodestar.md` carries them, Ch 19 synthesizes
against them, Ch 20 is weighted to them) — but it sits oddly beside §5, where Chapter 1
spends four paragraphs selling retrieval as "the single highest-leverage thing this book
does structurally."

**Referred for author decision.** Cheapest resolution: let the weights be retrieved
*instrumentally* rather than as trivia — a Ch 19 item requiring the reader to allocate
remaining study time across domains uses the weights without testing them as facts, and
stays inside B3's exclusion.

---

## ⚑ PROVISIONAL — B3 schedule summary (NOT from the B3 artifact)

> **Provenance warning.** `book-outline/retrieval-architecture.md` on disk is a
> **stage-failure notice**, not the B3 document — the artifact was composed but a
> permission error prevented the write. What follows is transcribed from the prose
> summary embedded in that notice. It is detailed enough to have verified the Ch 13 ←
> Ch 8 contract above, but it is **second-hand and must not be treated as canon.**
>
> **Re-run B3 with write access to `.pipeline-state/` before Chapter 3**, which is where
> the schedule actually starts. Replace this block with the real artifact's figures.

**Spacing targets.** Ch 3 at 10%, Ch 4 at 15%, then 20–25% through Ch 18. Five chapters
sit at the 25% ceiling — Ch 13 and 16 (troubleshooting/debugging arc), Ch 15 and 17 (the
two Zeniths), Ch 18 (last content chapter, most accumulated decay).

**Three structural decisions:**
1. Ch 1 excluded from retrieval entirely (orientation, 0% weight). Ch 3's 10% draws from
   Ch 2; no item anywhere tests exam mechanics.
2. Soundings are excluded from the budget but do the work anyway — Part 11 requires they
   be answerable from prerequisites, which in this book means earlier chapters. Counting
   them would distort their calibration purpose. Drafting instruction: source Soundings
   from B2's Prerequisites column, making the spacing free.
3. **Spacing floor:** from Ch 8 on, at least one item must come from ≥4 chapters back.
   Without it the schedule degenerates into "test the previous chapter."

**Nine cross-cutting themes**, headed by the control loop (Ch 3 → 4 → 6 → 11 → 15 → 17)
and namespaced-vs-cluster-scoped (which *derives* the RBAC four-way matrix instead of
memorizing it). One is a pattern rather than a fact: **"the object exists but nothing
happens without the component"** — Ingress without a controller, NetworkPolicy on an
unsupporting CNI, `kubectl top` without metrics-server, VPA not shipped by default.
Naming it once and retrieving it by name turns four gotchas into one rule.

**Decay fixes:** Ch 8's version skew → retrieved in Ch 13 (as a troubleshooting cause);
release cadence → Ch 17 (where the three-supported-minors rule and the ~3/year cadence
explain each other). Ch 7 (scheduling) and Ch 14 (Helm) are similarly thin and get named
anchors.

**Four things that must NOT be retrieved:**
1. Ch 1 exam mechanics
2. The dated graduated-project roster (retrieve the maturity *levels* instead)
3. The unpublished 60-question / 75% figures
4. Any `[inferred]` trap framed as exam frequency

---

## Unresolved convention

**The `[retrieval: chN]` tag's rendered form** — reader-visible or draft-only annotation
— is still undecided. Chapter 1 correctly carries none, but §5 describes the mechanism
to readers in prose, so the decision has a reader-facing dimension. **Chapter 3 is the
first chapter that needs it settled.**
=== END WRITE ===
```

---

## Summary of what this stage did and did not do

**Wrote (10 files, all first creation):** the glossary ledger, 7 concept shards, the objective-coverage log, the retrieval ledger.

**Did not write, per Rules 1–4:** `voice-exemplars.md` (9 candidates nominated only), `style-decisions.md`, `structural-contract.yaml`, the skill.

**Did not silently resolve:** the retired-blueprint weight provenance, the passing-score FAQ snapshot, the learning-science citations, the Logbook-Entry anecdote posture, the `ch01-fig02` Part-name conflict, or the B2 competency miscount. All six are recorded as loud, fenced flags inside the shards that later chapters will read — because Chapters 19 and 20 consume this KB, and a quietly-inherited wrong figure is exactly the failure mode Chapter 1 spends its second section teaching readers to catch.

**One judgment call made under explicit assumption:** the `cloud native` glossary entry. Stage 13 referred it for author decision without defaulting; I implemented its first-listed option (the deferring entry, built entirely from Chapter 1's own text) rather than leave the book's title term absent from its glossary. Flagged as reversible — one row changes if the author prefers otherwise.