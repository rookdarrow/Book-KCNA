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

### Search by keyword, then look at the shapes

Before any format-specific check, run:

```bash
python ../certcomp/scripts/variant_scan.py --book kcna --preset markers
python ../certcomp/scripts/variant_scan.py --book kcna --preset figures --case
```

**Searching for a format is how a format audit goes wrong.** Every false count in this book
came from assuming a shape and then trusting the number:

| searched for | missed | consequence |
|---|---|---|
| `**Fixed Point` | `★ **Fixed Point` | "5 chapters missing it" — all had it |
| `**1.**` | `**Q1.**` | 8 chapters reported zero questions |
| `<!--.*?-->` | bodies containing `-->` | a 313,777-char runaway `<pre>` |
| `source_ascii: \|` | `source_ascii: \|2` | 21 figures silently dropped |
| `<!-- FIGURE:` | ids living only in frontmatter | "21 anchors missing" — wrong question |

`variant_scan` searches the **word**, clusters the surrounding shapes, and flags minority
forms. Its first run found four forms of one marker: `> **★ Fixed Point**` (26),
`> ★ **Fixed Point**` (19), `> ★ **Fixed Point:**` (8), `★ **Fixed Point:**` (3).

When a count looks wrong, **search for the identifier, not the syntax**. `<!-- FIGURE:`
said 21 anchors were missing; searching `ch02-fig05-imagepullpolicy-decision` showed the ids
sitting in frontmatter, which is a different finding entirely.

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

**Cross-check the Attention Budget table against the headings, both ways.** Two checkpoint rows,
each sitting where its checkpoint sits; the "Total time" header equals the row sum; the
"Recommended" split names a section (`after §5`), never a checkpoint number.
`scripts/normalize_kcna.py` (certcomp) rebuilds the table, frontmatter budgets and marker forms;
`scripts/chapter_checks.py --chapter N` is the pre-read report.

**Cross-check the Attention Budget table against the headings, both ways.** Every `§N` row
names a heading that exists, every `##` section has a row, and every checkpoint row is a
checkpoint that still exists. The 2026-09-03 checkpoint merge deleted 33 sections from 16
chapters and left every table untouched; the tables were the only place the loss was visible,
and nobody was reading them. A `§` list with a gap (`1 2 3 4 5 8`) is a finding, not a style.

## B. Branded markers

Required with a per-chapter minimum: `☆` Taking Your Bearings (2), `★` Fixed Point (1),
`—` Dead Reckoning (1). Expected: `🧭` Soundings, `⚠` Navigational Hazards.
Optional: `🏆` Safe Harbor, `☀️` Zenith, `⚓` Worth Securing, `🪝` Snag, `🔭` Closer Look,
`🪢` Mnemonic, Logbook Entry, Extended Analogy.

- The marker must be the **marker form** (`**Dead Reckoning:**`), not a prose mention. Ch 2
  fails on exactly this: it references "§6 Dead Reckoning" inside a table and has no block.
- Difficulty indicators are `⚪` Foundation, `🔵` Standard, `🟡` Advanced, `🔴` Expert. Every
  `§N` heading carries one (a synthesis section may carry `☀️` instead). Heading form is
  glyph-first: `## ⚪ §1 — Title` (decided 2026-09-04; chapters 1–4 were converted).
- Fixed Point token: `★ **Fixed Point:**` — the contract's documented form, on its own line or
  opening a blockquote (decided 2026-09-04; the four earlier variants were normalized).
- Voyage Progress strip: exactly `🗺️ Chart → **🌊 Passage** → 🌅 Dawn` with the current stage
  bold (Chart = Ch 1, Passage = Ch 2–18, Dawn = Ch 19–20), placed after the Safe Harbor block.
  Any trailing sentence goes on its own italic line below it. Chapter 20 carries none.
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
- **Question numbering**: house format is `**1.**` for checkpoints and practice questions,
  including their answer keys (`**1 — B.**`, `**1. Answer: B.**`). Soundings blocks use a plain
  ordered list (`1.`) for questions and answers. (Normalized 2026-09-04; `**Q1.**` is gone.)
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

## H. Figures, ASCII placeholders and icons

- **Every anchor resolves to exactly one of**: an applied image, or a raw ``` ASCII
  placeholder (correct while the figure is still `pending`), never both. Both means the
  reader sees the diagram twice and print pays for it twice. Current state is clean: 86
  anchors, 78 image, 7 ASCII, 0 both.
- **Anchor vs frontmatter.** A `figure_anchor:` entry in the chapter's YAML with no
  `<!-- FIGURE: -->` in the body is a figure with nowhere to land. 21 ids are in this state.
- Alt text describes the RENDER, not the ASCII fallback and not the anchor id — the 2026-09-04
  audits found a dozen alts written against the fallback's shape (fan-out vs cascade, "in a
  row" vs vertical). Keep the in-chapter alt and `figures/<anchor>.alt.txt` identical. Alt text
  was generated outside the voice pass; British spellings are normalized by the central script,
  but a spelling baked into the SVG/PNG needs a regeneration.
- **The caption claims what the figure shows.** `ch15-fig06` stacked its phases vertically
  while the spec called for left-to-right — accurate caption, wrong render.
- Portrait figures (aspect < 0.75) render nearly full-page in print; note any taller than 3:4.
- **ASCII-FALLBACK comment bodies** must not contain `-->`. Art arrows (`0 -> N   -->`) close
  the comment early and orphan the terminator.
- **Marker and difficulty emoji must never sit inside a fenced code block.** Substitution
  skips fences, so the emoji survives to the EPUB and Kindle renders an empty box. 21 marker
  icons are rendered to `markers/` and substituted at build time; check the chapter's markers
  are in that set.
- **Glyphs**: only the `stack` and `pipeline` figure families carry Lucide glyphs, and every
  glyph must be registered in `certcomp-diagrams/assets/glyph-ledger.yaml` with exactly one
  meaning. Any other family should be glyph-free.

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
