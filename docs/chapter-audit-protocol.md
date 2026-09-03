# Chapter audit protocol — KCNA

One chapter per session, read in full, findings filed as beads. This exists because the
alternative — finding defects when a build breaks — has been demonstrably worse: the figure
pass surfaced 21 silently-dropped specs, a 313,777-character runaway `<pre>`, 98 broken image
links, 98 destroyed alt texts and three chapters missing a required marker, every one of them
discovered by something failing rather than by anyone looking.

A chapter is ~20,000 words. That fits in one session with room to read rather than skim.

## How to run one

```bash
cd C:/dev/lodestar/Book-KCNA
bd ready -l audit                 # take the lowest-numbered open chapter bead
bd update <id> --claim
python ../certcomp/pipeline/structural_lint.py --book kcna --chapter N
```

The linter runs **first, not instead**. It catches what has already been encoded; the read is
for what has not. Then work the checklist, file one bead per finding (`-l audit-finding`,
`--deps discovered-from:<id>`), and close with a verdict.

---

## A. Required structure

From `structural-contract.yaml`. Present, in order, correctly named:

| section | strictness |
|---|---|
| Chapter Title · Witty Subtitle · Attention Budget | required |
| Epigraph · Soundings · What You'll Learn | expected |
| Why This Chapter Matters | required |
| Taking Your Bearings | **required, min 2** |
| Exam Alert / Practice Questions | required |
| Chapter Summary · Closing / The Voyage Ahead | required |

**Checkpoints are now at exactly the minimum of 2.** There is no slack: removing one breaks
the contract.

## B. Branded markers

Required with a per-chapter minimum: `☆` Taking Your Bearings (2), `★` Fixed Point (1),
`—` Dead Reckoning (1). Expected: `🧭` Soundings, `⚠` Navigational Hazards.
Optional: `🏆` Safe Harbor, `☀️` Zenith, `⚓` Worth Securing, `🪝` Snag, `🔭` Closer Look,
`🪢` Mnemonic, Logbook Entry, Extended Analogy.

- The marker must be the **marker form** (`**Dead Reckoning:**`), not a prose mention. Ch 2
  fails on exactly this: it references "§6 Dead Reckoning" inside a table and has no block.
- Difficulty indicators are `⚪` Foundation, `🔵` Standard, `🟡` Advanced, `🔴` Expert. Check
  they are applied consistently — whether every section heading carries one is still an open
  `[DECIDE]`, so record which convention this chapter follows rather than "fixing" it.
- **No marker emoji inside a fenced code block.** Substitution skips fences, so the emoji
  survives to the EPUB and Kindle renders an empty box.

## C. Formatting

- **Headers**: `##` for `§N — Title` sections, `###` for subsections. No skipped levels
  (`##` → `####`). Section numbers run without gaps.
- **Lists**: `-` for bullets, not `*` or `+`. Ordered lists `1.` `2.`. Consistent indentation
  (2 or 4 spaces, not mixed). Blank line before a list that follows a paragraph, or the
  renderer swallows it.
- **Tables**: pipe tables with a header separator row. Wide tables need a scroll container in
  the EPUB — flag any wider than ~6 columns.
- **Code fences**: opening fence carries a language tag. Long lines wrap or are shortened;
  `check_reflow` fails on anything that overflows a 390px column.
- **Links**: never `](chapter-NN-slug.md)`. Source-file links do not exist inside the EPUB
  and produce RSC-007 errors that fail epubcheck, which KDP runs at upload.
- **Question numbering**: house format is `**1.**`. Eight chapters use `**Q1.**`.
- **Checkpoint closing**: `✓/☐ You've Now Mastered` list, or `<details>` scoring bands. Both
  exist in the book. Record which this chapter uses.
- **`source_ascii:`** blocks carry an explicit indicator (`|2`), never a bare `|`.
- **HTML comments**: no `-->` inside a comment body.

## D. Language

- US spelling outside verbatim quotations. Watch `labelled`, `colour`, `behaviour`, `centre`,
  `grey`, `recognise`, `emphasised`, `neighbours`. A British spelling inside a `[source:]`
  quote is **correct** — read the line before changing it.
- ~430 are flagged book-wide, concentrated in **figure alt text**, which was generated outside
  the voice pass and never went through it.
- No pirate caricature, no nautical cliché, no cartoon register.
- Narrator voice: seasoned navigator. Confident, calm, precise, warm, sparing wry beats.

## E. Terminology — the one most likely to be missed

The book has a **B7 Term Ownership Ledger** (`.pipeline-state/book-outline/term-ownership.md`)
naming which chapter *defines* each term, and what earlier chapters must do instead:
define / gloss+pointer / name+pointer / do not use.

- Does this chapter define terms it owns, and only gloss ones it does not?
- Does it use a term before its owning chapter, without a pointer?
- **Collisions**: a word meaning different things in different chapters. Ch 12 handles this
  well — it stops to say "binding" is now the third distinct sense in six chapters. Look for
  the cases that *don't* stop.
- Canonical casing and spelling of product names, per the ledger.

## F. Sourcing and cross-references

- Every factual claim carries `[source: …]`, and the named snapshot exists.
- Spot-check three claims against the snapshot text. Packing truncated eleven Kubernetes pages
  at their first code fence, so some tags point at passages absent from the packed corpus.
- Every `[cross-bearing: see Ch N §M]` resolves **and says what the pointer claims**. Ch 17
  has one disagreeing with two others about §1 vs §2.
- Vendor marks: name the exam and the administering body factually. Never imply endorsement,
  never use a logo. CKA's first cover named the wrong body entirely.

## G. Assessment integrity

- Every question has an answer, and the numbering matches after any renumbering.
- Distractors are plausible and unambiguously wrong; the keyed answer is unambiguously right.
- `[retrieval: chN]` tags point at chapters already read.
- Question difficulty spread is not all-easy or all-hard.

## H. Figures

- Alt text describes the figure, not the anchor id.
- **The caption claims what the figure shows.** `ch15-fig06` stacked its phases vertically
  while the spec called for left-to-right — accurate caption, wrong render.
- Portrait figures (aspect < 0.75) render nearly full-page in print; note any taller than 3:4.

## I. Scope — the judgment no tool can make

KCNA is 60 multiple-choice questions, 90 minutes, entry level. For each major section:
*would this be assessed, at this depth, on that exam?*

Flag material that is correct and well-written but pitched at CKA/CKAD depth. Record a verdict
of **tight / defensible / over-scoped**, naming the two or three sections that drive it. Do
not average across the chapter.

---

## What not to do

- Do not fix content while auditing. File the finding; fixing is a separate pass.
- Do not skim and declare clean. A chapter with no findings should say what was checked.
- Do not measure what you should read. Two scripted proxies were built for section I and both
  measured the book's scaffolding vocabulary instead of its concepts.
