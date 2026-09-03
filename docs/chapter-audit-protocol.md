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
bd ready -l audit          # take the lowest-numbered open chapter bead
bd update <id> --claim
```

Read the whole chapter. Not a grep, not a sample — the whole thing. Then work the checklist
below, file one bead per finding (`-l audit-finding`, linked with `--deps discovered-from:<id>`),
and close the chapter bead with a one-paragraph verdict.

The linter runs first, not instead:

```bash
python ../certcomp/pipeline/structural_lint.py --book kcna --chapter N
```

It catches what has already been encoded. The read is for what has not.

## Checklist

**1. Format consistency.** Four variants were found by accident, so assume more.
- Question numbering: house format is `**1.**`. Eight chapters use `**Q1.**`.
- Checkpoint closing: `✓/☐ You've Now Mastered` list, or `<details>` scoring bands. Both
  exist. Note which this chapter uses.
- `source_ascii:` blocks carry an explicit indicator (`|2`), never a bare `|`.
- HTML comments: no `-->` inside a comment body.

**2. Structure.**
- Required branded markers present (Dead Reckoning is the one currently missing in ch 2, 8, 10).
- `§N` anchors exist and are numbered without gaps.
- Every `[cross-bearing: see Ch N §M]` resolves to a section that exists and says what the
  pointer claims. Ch 17 has one disagreeing with two others about §1 vs §2.

**3. Sourcing.**
- Every factual claim carries a `[source: …]` tag, and the tag names a snapshot that exists.
- Spot-check three claims against their snapshot. Packing truncated eleven Kubernetes pages
  at their first code fence, so some tags point at passages that are not in the packed corpus.

**4. Voice.**
- US spelling outside verbatim quotations. ~430 British spellings are flagged book-wide,
  concentrated in figure alt text, which was generated outside the voice pass.
- No pirate caricature, no nautical cliché, no cartoon register.

**5. Figures.**
- Alt text describes the figure, not the anchor id.
- The figure teaches what its caption claims.
- Portrait figures (aspect < 0.75) render nearly full-page in print; note any that are
  taller than 3:4.

**6. Scope — the judgment the tools cannot make.**
This is the reason a person reads the chapter. KCNA is 60 multiple-choice questions in 90
minutes, entry level. For each major section ask: *would this be assessed, at this depth, on
that exam?* Flag material that is correct and well-written but pitched at CKA/CKAD depth.

Record a verdict: **tight / defensible / over-scoped**, with the two or three sections that
drive it. Do not average across the chapter — name specific sections.

## What not to do

- Do not fix content while auditing. File the finding; fixing is a separate pass with its
  own review.
- Do not skim and declare clean. A chapter that produces no findings should say what was
  checked and why it passed.
- Do not measure what you should read. Two scripted proxies were built for the scope
  question and both measured the book's scaffolding vocabulary instead of its concepts.
