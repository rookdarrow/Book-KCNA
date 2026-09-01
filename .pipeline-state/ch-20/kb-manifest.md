Write access to `Book-KCNA` isn't granted and this session is non-interactive, so I can't put the files on disk. That is the same block that left `book-outline/retrieval-architecture.md` holding an apology instead of its artifact — I won't repeat that. The manifest below carries **complete file contents** in the WRITE blocks, so the writes apply mechanically once the path is granted.

# Knowledge-Base Manifest — KCNA Chapter 20

## Status of the knowledge base itself

`Book-KCNA/knowledge-base/` **does not exist**. Every file below is a creation, not an update. No stage-14 write was ever applied for Chapters 1–19 — which is why the stage-13 integration report ran with `[no knowledge-base shards tagged]` and had to verify everything against the B6/B7 contracts instead.

Two causes, both verified, both outside this stage's remit to fix:

1. **No write-back parser exists.** The prompt states "the orchestrator will parse these and perform the writes." Grepping `pipeline/` for `=== WRITE`, `=== APPEND`, `post_process`, and `writeback` returns only the prompt template itself. `stages.py:224-234` defines `kb_update` with `output="{ch}/kb-manifest.md"` and no post-processing hook. The blocks have never been applied for any chapter of any book.
2. **The book path is not writable** from the stage subprocess, so a stage cannot apply them itself either.

Because nothing exists yet, I have emitted **all blocks as `WRITE` with full contents** rather than `APPEND`. `WRITE` is idempotent; an `APPEND` block re-applied after a parser is added would duplicate every row.

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**Zero definitional entries.** Chapter 20 is `chapter_type: mock_exam` — it introduces no concepts and defines none. Rule 5 forbids paraphrasing a definition into existence, and answer-key prose adjudicates rather than defines. The integration report concurs.

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| *(none)* | — | — |

Three terms are recorded as **flagged debts, without definitions** — earlier-chapter debts that Ch 20 surfaces by using them in scored items:

| Term | Ch 20 use | Owner | Severity |
|---|---|---|---|
| **SIG** | Item 53 **D** — the *correct answer*, bare, while TOC/TAG/Steering Committee are expanded around it | Ch 8 first-use debt; Ch 17 §8 owns the material | High — fix in place |
| **63-character limit** | Item 51 **C**, distractor | Untaught anywhere | Low — cut the clause |
| **process namespace** | Item 55 **B**, distractor | No B7 row; Ch 5 §2 owns the adjacent idiom | Lowest — add a B7 row, don't edit the item |

## Concept shards added/updated at `Book-KCNA/knowledge-base/concepts/`

- `concepts/kcna-exam-format-and-console.md` — **created**

One shard qualifies under the ≥200-word threshold. Chapter 20's Instructions give roughly 700 words of sustained, fully-sourced exposition on the exam's published form — question count, time limit, console behaviour, and score reporting. This is genuine treatment, not assessment, and no other chapter owns it correctly.

**Rule 6 flag — loud, and it concerns shipped text, not a shard.** There is no prior shard to contradict, so this is not canon drift. But the shard records a live contradiction I verified directly:

> `chapter-19-bearings-before-landfall.md:624` (**shipped**, not merely drafted) states: *"The Linux Foundation does not publish how its multiple-choice exam console behaves"* — and cites four sources as confirming that absence.

The source snapshot `lf-examui-multiple-choice-2026-08-31.md` names that exact sentence and says it "must be corrected before Ch 19 ships." It shipped anyway. The snapshot's own header records that the page "was NOT among those six" pages Ch 19's research swept, and that the parent exam-code page routes KCNA to it by name. Ch 20's framing is the sourced one; the correction runs **Ch 19 → Ch 20, never the reverse**. Ch 20 also emits a cross-bearing *into* Ch 19 §3, so until Ch 19 is fixed the mock sends the reader to a page that contradicts the one they just left.

## Voice-exemplar candidates nominated

Nominated only — not written to `voice-exemplars.md` (rule 1). All five sit in the **Instructions** section, which the truncation does not touch, so they are safe to ratify before the chapter's tail is restored.

| Function | Excerpt | Recommendation |
|---|---|---|
| chapter-opening | "You have reached the last chapter, and it is the only one that does not teach you anything. Nineteen chapters have explained. This one measures. There is no Soundings block here, no Fixed Points, no callouts in the margin: a diagnostic instrument that keeps interrupting itself with encouragement is not a diagnostic instrument." | **Strong.** Calm, confident, zero theming excess; earns a structural decision instead of announcing it. |
| ethical disclosure | "It was written by Lodestar Ledgers. It is not a leaked exam, not a reconstruction of one, and not a prediction of your score. What it gives you is a fix on your own position, taken from your own answers." | **Strong.** Nautical register at exactly the right density — one metaphor, load-bearing. Discharges guardrail 5 with nothing to gain commercially. |
| wry beat / subject dignity | "A reader who looks things up is measuring how good this book's index is. That is a fine thing to measure, but it is not the thing you came here for." | **Strong.** Aimed at the practitioner, never at anyone harmed — the v5.7 Part 14 #9 test, passed cleanly. |
| Dead Reckoning (provenance) | "The asterisks lead to a footnote naming CNPA, a different exam with 85 questions and 120 minutes; they are not a hedge about the class figures." | **Moderate–strong.** Model of the book's provenance discipline. Note: the block uses bold-led prose, not the skill's `> **Dead Reckoning:**` blockquote form — fix before promoting. |
| non-disclosure discipline | "Four options and one right answer is a reasonable authoring choice. Do not read it as a disclosure." | **Moderate.** Compact instance of separating an authoring choice from a published fact. |

## Objective coverage log

Appended as full-file creation. Chapter 20 is **not** first coverage for any objective — it is assessment. "First covered in" is taken from the B2 chapter lineup's authoritative competency mapping, not inferred from Ch 20's tags.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.1 Kubernetes Core Concepts | Chapter 3 | deep | Chapter 20 |
| D1.2 Administration | Chapter 8 | deep | Chapter 20 |
| D1.3 Scheduling | Chapter 7 | deep | Chapter 20 |
| D1.4 Containerization | Chapter 2 | deep | Chapter 20 |
| D2.1 Networking | Chapter 9 | deep | Chapter 20 |
| D2.2 Security | Chapter 12 | deep | Chapter 20 |
| D2.3 Troubleshooting | Chapter 13 | deep | Chapter 20 |
| D2.4 Storage | Chapter 11 | deep | Chapter 20 |
| D3.1 Application Delivery | Chapter 14 | deep | Chapter 20 |
| D3.2 Debugging | Chapter 16 | deep | Chapter 20 |
| D4.1 Observability | Chapter 18 | deep | Chapter 20 |
| D4.2 Cloud Native Ecosystem and Principles | Chapter 17 | deep | Chapter 20 |
| D4.3 Cloud Native Community and Collaboration | Chapter 17 | deep | Chapter 20 |

**Discrepancy found, flagged not resolved:** that is **13** competencies. `chapter-lineup.md:7` records B1's input as "4 domains, **12** competencies." Counting the curriculum PDF snapshot gives 4 + 4 + 2 + 3 = 13, and the book's own D-numbering runs to `D4.3` — which Chapter 20 uses in item 15. The "12" looks like a miscount in the B1 summary line, but B1 may have merged two deliberately. **Verify at B1 before anyone quotes the figure in front matter.**

## Retrieval-practice ledger

Chapter 20 is the book's largest single retrieval event: **42 confirmed items** drawing on all eighteen content chapters, plus **18 provisional** whose stems exist but whose walkthroughs are missing. Full rows are in the WRITE block below. Summary:

- **Section tags: 42/42 correct.** Every tag names a section that, per B6, actually owns the material — independently re-checked here against `shipped-sections.md`, the mechanical extract of the real headings.
- **Domain distribution is already correct and must not be adjusted.** Confirmed 42 give D1 18 · D2 13 · D3 6 · D4 5; the 18 missing items are exactly D1 8 · D2 4 · D3 4 · D4 2, landing on the published 26/17/10/7. Reweighting during restoration would break a correct instrument.
- **B3's four "must not be retrieved" prohibitions all hold**, with one now stale: B3 forbade retrieving "the unpublished 60-question figure," but `lf-mc-exam-important-instructions-2026-08-31` publishes it and Ch 20 sources it correctly. The prohibition predates the snapshot. The companion 75% passing figure needs the same re-check against the 2026-08-31 snapshots before anyone re-applies B3's rule to the Scoring Rubric.
- **B3's spacing floor** (from Ch 8 on, at least one item ≥4 chapters back) is satisfied many times over.
- **Cross-cutting theme coverage** is logged separately, including the "an object without its component does nothing" pattern — invoked four times in Ch 20 but **named zero times**, which is the integration report's binding-convention violation.

---

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===
# KCNA — Pipeline Glossary Ledger

> **What this file is.** The pipeline's internal term ledger, written by stage 14
> (`kb_update`) and read back by later stages via `needs_kb_shards`. It is **not**
> the book's shipped glossary. The shipped glossary is a book-assembly artifact
> required by skill Part 16 (minimum 100 terms, alphabetical, chapter
> cross-references) and does not yet exist for this book.
>
> **Provenance warning — read before trusting this file's coverage.** This ledger
> was created at **Chapter 20**, the last chapter of the book. No stage-14 write
> was ever applied for Chapters 1-19, so **the terms those chapters introduced are
> not recorded here**. An empty or thin ledger means "never captured," not
> "nothing to capture." Do not treat absence from this file as evidence that a
> term is undefined in the book.
>
> Bootstrapped: 2026-08-31 - Source chapter: 20 (Full Mock Exam)

---

## Entries added by Chapter 20

**None.** Chapter 20 is a mock exam (`chapter_type: mock_exam`). It introduces no
concepts and defines none - its walkthroughs restate and adjudicate material the
content chapters already own. Per stage-14 rule 5 (entries inherit the chapter's
*exact* definition; do not paraphrase), there is nothing here to inherit, and
manufacturing definitions from answer-key prose would be definitional drift.

The stage-13 integration report reached the same conclusion independently:
*"Net for stage 14: zero new glossary entries are generated by this chapter."*

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| *(none)* | - | - |

---

## Flagged: terms reaching graded text without a lookup path

These are **not** glossary entries. They are debts inherited from earlier chapters
that Chapter 20 surfaces by using the term in a scored item. The B7 term-ownership
ledger's test is that *"a term used in question text or an answer key may not be
glossary-only, because a reader who meets it there has no place to look it up
mid-question."* All three fail that test. **No definition is recorded** - the fix
belongs in the owning chapter, not here.

| Term | Where Ch 20 uses it | Owning chapter | Status | Required fix |
|---|---|---|---|---|
| **SIG** | Item 53, option **D** - the *correct answer* - bare and unexpanded, while its three sibling options (TOC, TAG, Steering Committee) are all correctly expanded | Ch 8 (first unexpanded use, per B7); Ch 17 §8 owns the contributor/SIG material | **Open - highest severity of the three** | Expand in place at item 53 D: "...brought to the Special Interest Group (SIG) that owns that subsystem." Then give Ch 8 a first-use expansion. |
| **63-character limit** (label values) | Item 51, option **C**, a distractor | Untaught anywhere per B7 | **Open - low severity** | The option's wrongness does not depend on the number (selectors cannot match annotations *at all*), so the item is sound. The figure is decoration the reader cannot verify. Recommend cutting the clause when walkthrough 51 is written. |
| **process namespace** | Item 55, option **B**, a distractor | No B7 row exists; Ch 5 §1-§2 own the adjacent "shared network namespace" in the same bare style | **Open - lowest severity; not a defect** | Consistent with the book's existing usage. Add a B7 canonical-forms row under Ch 5 §2 rather than editing the item. |

---

## Restrictions honoured (verification record, not entries)

Chapter 20 was checked against every graded-use restriction in the B7 ledger's
Part 2, across 60 stems, 240 options, and 42 walkthroughs. All ten hold. Recorded
here so a retroactive sweep does not re-derive it:

`PodDisruptionBudget`/`PDB` (named by B7 for the Ch 20 mock specifically) -
`ABAC` - `eBPF` - `SRE` - `LTS` - `PSP` - `descheduler` -
`Endpoints` (legacy capitalised object) - static Pod / mirror Pod - `SLA`

`SLA` in particular was *predicted* by B7 to appear as a Ch 20 distractor and does
not, so Chapter 20 creates no pressure to resolve that orphan early - it can be
settled on Ch 18's own schedule.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kcna-exam-format-and-console.md ===
---
concept: kcna-exam-format-and-console
owned_by: "Chapter 20 (Instructions); contested by Chapter 19 §3 - see CONTRADICTION"
first_treatment: "Chapter 20"
objectives: []
status: "sourced; one live contradiction with shipped Ch 19 text"
recorded_by: "stage 14 (kb_update), 2026-08-31"
---

# The KCNA exam's published form, and the console it runs in

Roughly 700 words of sustained, fully-sourced exposition in Chapter 20's
Instructions section. Recorded as a shard because it is the book's **correct and
sourced** treatment of exam mechanics, and because Chapter 19 currently
contradicts it in shipped text. A future harmonisation pass needs this on record
so the correction runs in the right direction.

Unaffected by the Ch 20 truncation - the Instructions section is intact.

## The class-inheritance chain

Neither the question count nor the time limit appears on the KCNA product page
`[source: provenance-kcna-60-questions-2026-08-31]`. Both are inherited:

1. The Linux Foundation candidate handbook gives the figures for multiple-choice
   exams **as a class** - "60* multiple-choice questions," "90* minutes to
   complete" `[source: lf-mc-exam-important-instructions-2026-08-31]`.
2. The asterisks lead to a footnote naming **CNPA**, a different exam at 85
   questions and 120 minutes. They are an exception callout, not a hedge on the
   class figures.
3. The LF exam-code table places KCNA in the multiple-choice column beside KCSA
   and LFCA, with CKA and CKAD in the performance-based column
   `[source: lf-exam-user-interface-exam-codes-2026-08-31]`.

Therefore: **60 questions, 90 minutes.** Stated flatly, with the inheritance
disclosed rather than hidden.

## Domain weighting

44% Kubernetes Fundamentals - 28% Container Orchestration - 16% Cloud Native
Application Delivery - 12% Cloud Native Architecture
`[source: cncf-curriculum-kcna-readme-2026-08-31]`. Over 60 items: **26 / 17 / 10 / 7.**

Four independent CNCF/LF surfaces agree on the split, so it can be asserted
without hedging.

## Console behaviour - PUBLISHED

`[source: lf-examui-multiple-choice-2026-08-31]`, the handbook page the exam-code
table routes KCNA to by name:

1. Navigation is bidirectional (Previous / Next buttons).
2. An item can be flagged for later review.
3. Flagged items are highlighted on a Review Screen.
4. A candidate can return to a flagged item **and change the answer**.
5. A Review Exam prompt appears after the final item; the Review Screen carries
   the Finish Exam button.
6. The exam ends on timer expiry or on Finish Exam.
7. A **Pause Exam** function exists, and using it **does not stop the timer** - a
   break is available but is purchased with exam time.

## Score reporting - PUBLISHED, and it is what justifies the Ch 20 rubric

The score report arrives within 24 hours by email and on the Portal. It reports
the outcome only: the Linux Foundation "does not report performance on individual
items and will not honor requests for more detailed information"
`[source: lf-exam-scoring-and-notification-2026-08-31]`.

This is the entire argument for Chapter 20's per-domain score sheet. The
breakdown is not a convenience duplicating something the real exam supplies
afterward - it is **the only domain-level diagnostic available anywhere in the
preparation**, and it arrives before the exam, which is the only point at which it
can still change anything. Anyone tempted to trim the Scoring Rubric during
restoration should read that sentence first.

## NOT published - do not assert

- How many answer options a multiple-choice item carries.
- Whether any item is multi-select or "choose two."
- Whether unscored pretest items are mixed in.
- Whether a wrong answer carries a penalty.
- On-screen layout, button placement, or whether a question counter is displayed
  (these rest on two screenshots whose image bodies were not retrievable as text).

Chapter 20's four-options-one-answer shape is therefore **an authoring choice by
Lodestar Ledgers**, and the chapter says so outright: *"Do not read it as a
disclosure."* Preserve that disclaimer through any revision.

The handbook's phrase "update your answer" is singular. Suggestive of one
selection per item; **not dispositive**, and must not be cited as proof of a
single-best-answer format.

## CONTRADICTION - shipped text, unresolved

`chapter-19-bearings-before-landfall.md` line 624 states:

> "The Linux Foundation does not publish how its multiple-choice exam console
> behaves: whether you can skip a question, mark one for review, navigate back, or
> change an answer you have already given. That silence is not an oversight in this
> book's research; it is confirmed absent on four separate official pages..."

**This is false, and it is in the shipped chapter file, not merely in a draft.**

- The source snapshot itself names this exact sentence under a "FALSE, do not
  write" heading and records that it "must be corrected before Ch 19 ships." It
  shipped anyway.
- The snapshot's header notes the ExamUI page "was NOT among those six" pages Ch
  19's research swept - so the four-page corroboration Ch 19 cites is a survey
  that missed the page that answers the question.
- Ch 19's citation list makes this worse rather than better: it presents an
  incomplete sweep as positive evidence of absence.

**Direction of correction: Ch 19 -> Ch 20. Never the reverse.** Ch 20's framing is
sourced; Ch 19's is not.

**Scope warning.** Do not fix line 624 alone. The B6 skeleton's Ch 20 block already
carries a 2026-08-31 CORRECTION superseding a "NOT FOUND in any authoritative
source" finding; Ch 19's block has not been checked against it, and Ch 1 needed a
full provenance retrofit for the same root cause. Treat Ch 19 as requiring a sweep
of every provenance claim, not a one-line edit.

**Knock-on:** Chapter 20 emits `*[cross-bearing: see Ch 19 §3 - pacing and time
discipline]*`. The pointer resolves correctly (Ch 19 §3 is "Ninety Minutes"), but
until Ch 19 is fixed the mock exam sends the reader to a section that contradicts
the page they just left.

## Prescribed phrasings

- CORRECT: "The Linux Foundation publishes the multiple-choice exam interface's
  behaviour in its candidate handbook, for the interface KCNA uses."
- CORRECT: "The Linux Foundation publishes both of the numbers... Neither number
  appears on the KCNA product page." (Chapter 20's actual wording.)
- FORBIDDEN: "The Linux Foundation does not publish how its multiple-choice exam
  console behaves."
- FORBIDDEN: "The KCNA exam page describes the exam interface."
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===
# KCNA — Objective Coverage Log

> Bootstrapped by stage 14 at **Chapter 20**, 2026-08-31. Rows for Chapters 1-19
> were never captured (no stage-14 write was ever applied); "First covered in" is
> therefore taken from the **B2 chapter lineup's** authoritative competency mapping
> rather than from prior entries in this file.
>
> **Numbering caveat.** The `D1.1` / `D2.3` identifiers are the **Lodestar
> convention established in B1**. CNCF publishes four domains and their named
> competencies with **no numbering and no sub-weights**
> `[source: cncf-kcna-curriculum-pdf-2026-08-23]`. Per-chapter weight figures in
> the lineup are authored judgment and must be disclosed as such in front matter -
> never presented as CNCF-published data.

## Coverage

Chapter 20 is a mock exam. It is **not first coverage for any objective**; it is
assessment. It appears only in "Last reviewed."

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.1 Kubernetes Core Concepts | Chapter 3 | deep | Chapter 20 |
| D1.2 Administration | Chapter 8 | deep | Chapter 20 |
| D1.3 Scheduling | Chapter 7 | deep | Chapter 20 |
| D1.4 Containerization | Chapter 2 | deep | Chapter 20 |
| D2.1 Networking | Chapter 9 | deep | Chapter 20 |
| D2.2 Security | Chapter 12 | deep | Chapter 20 |
| D2.3 Troubleshooting | Chapter 13 | deep | Chapter 20 |
| D2.4 Storage | Chapter 11 | deep | Chapter 20 |
| D3.1 Application Delivery | Chapter 14 | deep | Chapter 20 |
| D3.2 Debugging | Chapter 16 | deep | Chapter 20 |
| D4.1 Observability | Chapter 18 | deep | Chapter 20 |
| D4.2 Cloud Native Ecosystem and Principles | Chapter 17 | deep | Chapter 20 |
| D4.3 Cloud Native Community and Collaboration | Chapter 17 | deep | Chapter 20 |

Secondary teaching chapters (not first coverage): D1.1 also Ch 4, 5, 6 -
D2.1 also Ch 10 - D2.2 boundary material also Ch 10 - D3.1 also Ch 15.

## COUNT DISCREPANCY - verify at B1 before quoting

The table above has **13** competencies. `chapter-lineup.md:7` records the B1 input
as "4 domains, **12** competencies."

Counting the curriculum PDF snapshot gives 4 + 4 + 2 + 3 = 13, and the book's own
numbering runs to `D4.3` - which Chapter 20 uses as a live answer-key tag on item
15. The "12" looks like a miscount in the B1 summary line, but B1 may have merged
two competencies deliberately. **Resolve at B1. Do not print either figure in
front matter until it is settled.**

## Chapter 20 assessment coverage

Blueprint targets, from the published 44/28/16/12 weighting over 60 items
`[source: cncf-curriculum-kcna-readme-2026-08-31]`:
**D1 26 - D2 17 - D3 10 - D4 7.**

| Objective | Confirmed items (walkthrough present) | Provisional (stem only) | Total |
|---|---|---|---|
| D1.1 | 10 | 4 | 14 |
| D1.2 | 3 | 0 | 3 |
| D1.3 | 1 | 2 | 3 |
| D1.4 | 4 | 1 | 5 |
| **D1 total** | **18** | **8** | **26** |
| D2.1 | 5 | 2 | 7 |
| D2.2 | 3 | 1 | 4 |
| D2.3 | 3 | 0 | 3 |
| D2.4 | 2 | 1 | 3 |
| **D2 total** | **13** | **4** | **17** |
| D3.1 | 5 | 2 | 7 |
| D3.2 | 1 | 2 | 3 |
| **D3 total** | **6** | **4** | **10** |
| D4.1 | 3 | 0 | 3 |
| D4.2 | 1 | 1 | 2 |
| D4.3 | 1 | 1 | 2 |
| **D4 total** | **5** | **2** | **7** |
| **Book total** | **42** | **18** | **60** |

**The exam block's weighting is already correct. Do not adjust it.** Items 43-60
need walkthroughs written against their existing stems; they do not need
reweighting, resequencing, or substitution. Any change to the item set breaks a
distribution that currently lands exactly on the published blueprint.

Difficulty spread across the 42 confirmed: Foundation 8 - Standard 25 -
Advanced 9 - Expert 0. The absence of Expert items is a deliberate choice for an
associate-tier credential, not a gap to fill when keying 43-60.
=== END WRITE ===
```

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===
# KCNA — Retrieval-Practice Ledger

> Which earlier-chapter topics have been retrieval-tested, and where.
> Bootstrapped by stage 14 at **Chapter 20**, 2026-08-31. Chapters 3-19 each
> carry their own retrieval load per the B3 schedule (Ch 3 at 10%, Ch 4 at 15%,
> 20-25% from Ch 5 on), but **none of it was ever logged** - no stage-14 write was
> applied before this one. This file therefore records Chapter 20 only. Absence of
> a topic here does not mean it was never retrieved.
>
> Chapter 20 is the book's largest single retrieval event: 60 items drawing on all
> eighteen content chapters.

## Confirmed — walkthrough present, section tag verified

All 42 section tags were re-verified against `shipped-sections.md`, the mechanical
extract of the real chapter headings. **42 of 42 resolve to a section that owns the
material.** No misdirected retrieval.

| Tested topic | Original chapter | Retested in | Ch 20 item |
|---|---|---|---|
| Container vs virtual machine (shared kernel vs own kernel) | ch 2 §1 | ch 20 | 1 |
| Cluster with no CNI plugin installed | ch 9 §1 | ch 20 | 2 |
| API server as the only writer of cluster state | ch 3 §5 | ch 20 | 3 |
| Helm `values.yaml` as default parameters | ch 14 §2 | ch 20 | 4 |
| Namespace as name scope; cluster-scoped kinds | ch 4 §3 | ch 20 | 5 |
| The 4Cs, and which layer is outermost | ch 12 §1 | ch 20 | 6 |
| Prometheus pull/scrape model | ch 18 §4 | ch 20 | 7 |
| QoS class computation from requests and limits | ch 5 §8 | ch 20 | 8 |
| `emptyDir` lifetime is the Pod's | ch 11 §1 | ch 20 | 9 |
| Deployment owns ReplicaSet owns Pod | ch 6 §1 | ch 20 | 10 |
| GitOps as pull-based in-cluster reconciliation | ch 15 §3 | ch 20 | 11 |
| `Pending` means unscheduled | ch 13 §2 | ch 20 | 12 |
| Mutable tag vs content-addressed digest | ch 2 §3 | ch 20 | 13 |
| NetworkPolicy is allow-only; selection creates default-deny | ch 10 §6 | ch 20 | 14 |
| CNCF maturity levels and their order | ch 17 §2 | ch 20 | 15 |
| Authentication then authorization then admission | ch 8 §2 | ch 20 | 16 |
| Readiness gates endpoint membership | ch 9 §4 | ch 20 | 17 |
| `helm rollback` vs `kubectl rollout undo` | ch 14 §3 | ch 20 | 18 |
| Cordon before drain | ch 8 §4 | ch 20 | 19 |
| Secrets are base64-encoded, not encrypted | ch 12 §4 | ch 20 | 20 |
| StatefulSet stable ordinal identity | ch 6 §6 | ch 20 | 21 |
| A span as the unit within a trace | ch 18 §5 | ch 20 | 22 |
| Init container failure halts the sequence | ch 5 §3 | ch 20 | 23 |
| `kubectl logs --previous` in a crash loop | ch 13 §3 | ch 20 | 24 |
| Canary vs blue/green vs rolling vs Recreate | ch 15 §2 | ch 20 | 25 |
| `NoExecute` evicts; `NoSchedule` does not | ch 7 §4 | ch 20 | 26 |
| `ReadWriteOnce` is node-count, not Pod-count | ch 11 §4 | ch 20 | 27 |
| `spec` declared vs `status` observed | ch 4 §2 | ch 20 | 28 |
| Mesh data plane vs mesh control plane | ch 17 §5 | ch 20 | 29 |
| Image layers are content-addressed and shared | ch 2 §2 | ch 20 | 30 |
| Ingress object without an Ingress controller | ch 10 §3 | ch 20 | 31 |
| `kubectl debug` / ephemeral containers on distroless | ch 16 §3 | ch 20 | 32 |
| Operator as controller for a custom resource | ch 6 §8 | ch 20 | 33 |
| Headless Service (`clusterIP: None`) | ch 9 §5 | ch 20 | 34 |
| etcd as authoritative state, reached only via API server | ch 3 §2 | ch 20 | 35 |
| Role + RoleBinding scope; verbs are enumerated | ch 12 §3 | ch 20 | 36 |
| Argo CD `OutOfSync` semantics | ch 15 §4 | ch 20 | 37 |
| Readiness failure vs liveness failure consequence | ch 5 §7 | ch 20 | 38 |
| Four golden signals vs RED | ch 18 §7 | ch 20 | 39 |
| ResourceQuota aggregate vs LimitRange per-object | ch 8 §3 | ch 20 | 40 |
| `OOMKilled` vs `Evicted` | ch 13 §4 | ch 20 | 41 |
| `imagePullPolicy` and its tag-conditional default | ch 2 §6 | ch 20 | 42 |

## Provisional — stem present, walkthrough missing

Items 43-60 exist in the exam block but have no answer key (see the chapter's
ship-blocking AUTHOR-REVIEW). Topics are read off the stems; **section targets are
inferred and marked provisional** - confirm each against B6 when the walkthroughs
are written.

| Tested topic | Original chapter (provisional) | Retested in | Ch 20 item |
|---|---|---|---|
| Dynamic provisioning via StorageClass and provisioner | ch 11 §3 | ch 20 | 43 |
| Kustomize base and overlay, without templating | ch 14 §5 | ch 20 | 44 |
| Scheduler: filter, score, bind | ch 7 §1 | ch 20 | 45 |
| Gateway API role split across three kinds | ch 10 §5 | ch 20 | 46 |
| Microservices trade-off, honestly stated | ch 17 §3 | ch 20 | 47 |
| CronJob creates a Job creates Pods | ch 6 §7 | ch 20 | 48 |
| SBOM as component inventory | ch 12 §7 | ch 20 | 49 |
| `port-forward` works but the Service path fails | ch 16 §5 | ch 20 | 50 |
| Labels select; annotations do not | ch 4 §5 | ch 20 | 51 |
| DNS search domains resolve the Pod's own namespace first | ch 9 §7 | ch 20 | 52 |
| KEP proposed to the owning SIG | ch 17 §8 | ch 20 | 53 |
| Container Runtime Interface as kubelet/runtime boundary | ch 2 §4 | ch 20 | 54 |
| Containers in one Pod share a network namespace | ch 5 §2 | ch 20 | 55 |
| Twelve-factor config from ConfigMaps and Secrets | ch 15 §1 | ch 20 | 56 |
| `maxSurge` / `maxUnavailable` during rolling update | ch 6 §4 | ch 20 | 57 |
| Node affinity `preferred...` vs `required...` | ch 7 §3 | ch 20 | 58 |
| Service selector does not match Pod labels | ch 16 §4 | ch 20 | 59 |
| Controller as continuous reconciliation loop | ch 3 §6 | ch 20 | 60 |

## Cross-cutting themes retrieved

B3 specified nine cross-cutting themes. Chapter 20's coverage of the named ones:

| Theme | Ch 20 items | Note |
|---|---|---|
| The control loop (Ch 3 -> 4 -> 6 -> 11 -> 15 -> 17) | 3, 11, 28, 33, 37, 60 | Retrieved six times across four chapters of origin - the primary Zenith's dependency, well served |
| Namespaced vs cluster-scoped | 5, 36 | Item 36 *derives* the RBAC scope rule from it rather than asking for recall, which is the intent |
| "An object without its component does nothing" | 2, 31, 43, and 31's option D | **Invoked four times, named zero times.** See defect below |
| Additive-never-deny (RBAC and NetworkPolicy share it) | 14, 36 | Item 14 closes to Ch 12 §9 explicitly - the two mechanisms retrieved as one rule |
| Version skew / release cadence decay fix | *none* | Ch 20 carries no version-skew item. B3 placed the anchors in Ch 13 and Ch 17; the mock does not reinforce them. Worth a deliberate decision when keying 43-60, though the distribution has no free slot |

### Defect: the pattern is invoked but never named

B3's rationale: *"Naming it once and retrieving it by name turns four gotchas into
one rule."* B7 states the requirement harder - quote it **VERBATIM**, because the
exact wording appears 24 times across Ch 3/6/10/11/13/17, including a graded
Practice option.

Walkthrough 31 opens with a paraphrase: *"The object exists; nothing happens
without the component."* In the chapter whose entire function is retrieval, that
hands back the book's most-reinforced retrieval phrase in words the reader has
never seen - the same failure B7's 2026-08-31 errata note documents for Ch 17 and
found propagating in Ch 6.

**Fix:** open walkthrough 31 with **"An object without its component does nothing."**
then keep the existing gloss. Consider naming it once more in walkthrough 43, where
the same pattern governs StorageClass and its provisioner; that would let the mock
land the pattern twice. Naming it in all four places would be over-reinforcement.

## B3 prohibitions — compliance

B3 specified four things that must **not** be retrieved.

| Prohibition | Status |
|---|---|
| Ch 1 exam mechanics | **Honoured.** Zero graded items test exam mechanics. The Instructions discuss them at length, but nothing is scored on them |
| The dated graduated-project roster | **Honoured, and reinforced.** Item 15 tests the maturity *levels and their order*; its walkthrough tells the reader outright that a memorised Graduated roster "is memorization with an expiry date on it" |
| The unpublished 60-question / 75% figures | **STALE PROHIBITION - re-check before re-applying.** The 60-question figure is now published and Ch 20 sources it correctly `[source: lf-mc-exam-important-instructions-2026-08-31]`. B3 predates that snapshot. The companion 75% passing figure needs the same re-check against the 2026-08-31 snapshots before anyone applies B3's rule to the missing Scoring Rubric |
| Any `[inferred]` trap framed as exam frequency | **One soft breach.** Walkthrough 38 A: *"the exam will test whether you can keep them apart"* - an unsourced claim about exam behaviour, in a chapter otherwise scrupulous about the distinction. Suggested: *"and keeping them apart is the whole of it."* The adjacent misconception-prevalence claims (items 8 B, 21 A) are claims about *readers*, not the exam, and sit inside the sanctioned register |

Spacing floor (from Ch 8 on, at least one item from >=4 chapters back):
**satisfied many times over** - Ch 20 draws on all eighteen content chapters.

## Instrument-validity finding — carry into any re-key

Not a retrieval defect, but it governs how items 43-60 must be restored, so it is
recorded here rather than lost in the integration report.

Draft-v1 keyed roughly 55 of 60 items to **B**. Draft-v2 correctly rewrote that,
balancing the totals (A 11 - B 10 - C 10 - D 11 across 42) but introducing two new
positional signatures:

1. **Every consecutive block of four contains each letter exactly once** - ten
   blocks, ten complete sets, zero exceptions. On a random key each block completes
   with probability ~0.094; ten in a row is ~5e-11.
2. **No letter ever repeats on consecutive items** - zero adjacent repeats across
   41 pairs, against ~10 expected on a random key.

A test-wise candidate who answers three items in a block confidently can deduce the
fourth without knowing the material. That inflates the score and, worse, corrupts
the per-domain breakdown - which exists precisely because the real exam never
supplies one `[source: lf-exam-scoring-and-notification-2026-08-31]`.

**Re-key after the tail is restored, not before**, so it is one relabeling pass:
generate a fresh 60-item key by unconstrained random assignment with only a global
balance target (15 +/- 2 per letter), **permitting** adjacent repeats and repeated
letters within a block - those are properties a real key has. Then permute each
stem's four options so the correct text moves to its new letter, and update the
walkthrough header letter and refutation bullets to match.

Verified safe: no option references another by letter, none is "all/none of the
above," and no distractor's wrongness depends on its position. The permutation is a
pure relabeling.
=== END WRITE ===
```

---

## What needs your decision

**Four things, in severity order. Only the first is mine to hand back.**

1. **The stage-14 write path is dead for every book.** No parser for these blocks exists anywhere in `pipeline/`, and the book directory isn't writable from the stage subprocess. Both need fixing or stage 14 is decorative — it has produced a manifest for every chapter of every book and applied nothing. The same permission block is why `book-outline/retrieval-architecture.md` contains a written apology where its artifact should be; that file should be regenerated once the path is granted.

2. **Chapter 19 is shipped with a false sourced claim.** Line 624 asserts the LF doesn't publish its exam console behaviour and cites four pages as proof of absence — but the page that documents it wasn't among them, and its snapshot explicitly flags this sentence as needing correction before Ch 19 ships. Correct Ch 19 to Ch 20's framing, and sweep the chapter rather than editing one line: Ch 1 needed a full provenance retrofit for the same root cause.

3. **Chapter 20 cannot ship** — 18 of 60 items have no answer and the Scoring Rubric is absent, while the Instructions promise both. Already covered in the draft's own block and the integration report; the retrieval log now adds the constraint that the *re-key must happen after restoration*, and that the exam block's weighting is already correct and must not be touched.

4. **The competency count is off by one somewhere.** B1 says 12; the curriculum PDF and the book's own `D4.3` tag both say 13. Settle it at B1 before either number reaches front matter.

The chapter's own work was strong where it wasn't truncated: 54 cross-bearings resolving without a defect, ten B7 graded-use restrictions honoured across 240 options, and a voluntary disclosure that its four-option shape is an authoring choice rather than a published fact — which is why five of the nominations above come from a single section.