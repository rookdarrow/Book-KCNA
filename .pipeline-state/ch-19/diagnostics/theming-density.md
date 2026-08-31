Audit complete. The counting and grepping were run against `draft-v1.md` directly, so the line numbers below are exact.

```markdown
# Theming-Density Audit — Chapter 19

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~10,070**
- Overt nautical/celestial metaphors outside branded markers: **5**
- Density: **0.50 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

Method: `draft-v1.md` is 939 lines / 14,759 raw tokens. Excluding 113 table rows, the
three fenced ASCII figure blocks (L116–133, L304–333, L538–553), and the four HTML
comments leaves ~10,070 alphabetic word tokens of body prose. Blockquote callouts,
`<details>` answer blocks, and practice-question prose are counted as body prose.

The chapter is at roughly half the floor of the band. This is a placement finding more
than a count finding: all five metaphors sit at structural hinges (title, epigraph, two
section openers, closing quote) and none appear in the ~9,800 words between them. The
chapter does not read as texture-less, because a navigational-*instrument* register runs
through it (see "Borderline" below) — but that register is vocabulary, not figure of
speech, and it does not count toward the band.

One drift finding that is not a density issue is recorded under Pirate-vocabulary check:
the chapter title revives a retired marker name.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 1 | "Bearings Before Landfall" (chapter title) | nautical — navigation / arrival | **flag — retired marker vocabulary**; see Pirate-vocabulary check |
| 34 | "The chart does not tell you where you are. Two bearings on two landmarks tell you where you are. The chart only tells you what you are looking at." | nautical — navigation (extended; chart / bearings / landmarks as one conceit) | acceptable — strongest in the chapter; sets up §2's discriminator argument rather than decorating it |
| 297 | "Two landmarks that have merged into one on your chart cannot fix a position." | nautical — navigation | acceptable — load-bearing; it *is* the argument for why §2 supplies discriminators instead of paired definitions, and it pays off the epigraph |
| 561 | "The stretch of water you most enjoy sailing is rarely the one that puts you on the rocks." | nautical — sailing / hazard | acceptable, weakest of the five — "on the rocks" is a dead idiom, rescued only because the sentence around it is literally about sailing. Watch it; do not add a second like it |
| 940 | "Every navigator makes the same passage twice: once on the chart, and once on the water. The chart passage is the one that decides how the other goes." | nautical — navigation (extended) | acceptable — earns the closing position, and the two-passages figure does real work pointing at Ch 20 |

### Borderline — inspected, not counted

| Line(s) | Passage | Why not counted |
|---|---|---|
| 249, 280, 289, 372, 829, 932 | "the wrong instrument" / "which instrument is even applicable" / "the most common instrument error" / "it is not a chapter — it is the instrument" | Used in the plain diagnostic-tool sense (rule 4: functional language). Against a Communications Officer narrator it reads as navigational-instrument register, and it is the chapter's main source of low-grade texture — but it is vocabulary overlap, not figure of speech. L932 is the closest to deliberate |
| 353 | "Every rule is anchored to `kube-apiserver`" | Fully conventionalized dead metaphor in technical English. Mild collision with ⚓ Worth Securing, which is the icon on that same block's neighbour at L505 |
| 610 | "`the-lodestar.md` ships with this book" | Software-release English, not nautical theming |
| 384, 468 | "`OutOfSync` = drift, not error" | Technical GitOps term |
| 652, 926 | "to calibrate" / "Everything from here is calibration" | Instrument register, functional sense |

### Structural terminology excluded by rule 1 (not counted)

🧭 Soundings (L14, 39, 74, 569) · ☆ Taking Your Bearings (L16, 18, 241, 443, 569) ·
★ Fixed Point (L90, 166, 497) · ⚠ Navigational Hazards (L30, 427) · — Dead Reckoning
(L90, 563) · ☀️ Zenith (L107, as §1's marker) · 🏆 Safe Harbor (L920) · The Voyage Ahead
(L930) · ⚓ Worth Securing (L232, 505) · 🪝 Snag (L176, 592) · 🔭 Closer Look (L353) ·
🪢 Mnemonic (L145, 441) · Logbook Entry (L688) · every `*[cross-bearing: …]*` ·
The Lodestar / `the-lodestar.md` (L21, 100, 608, 640, 642, 678) · "Lodestar Ledgers" as
epigraph attribution (L35).

## Overcooked passages

**None.** No passage stacks multiple independent metaphors. The two extended figures
(L34, L940) each run three images, but both are one coherent conceit rather than a stack,
and both resolve into a point. Nothing here needs trimming.

The single closest thing to over-seasoning is the **title** (L1): two pieces of marker
vocabulary in five words. That is flagged as drift, not as density.

## Underseasoned passages

Two stretches far over the 800-word flag threshold carry zero counted metaphors:

**L36–L296 (~3,340 words) — Soundings, Why This Chapter Matters, What You'll Learn, all
of §1, and the first checkpoint.** Runs from the epigraph to the §2 opener with no
thematic texture. §1 is the chapter's conceptual centre — it argues that the book is nine
patterns rather than eighteen chapters — and it opens (L109–111) on pure abstract
argument: "The exam blueprint cuts across those ideas at right angles. So we cut the other
way now." That is the chapter's most natural home for one image, and the strongest
candidate for the first addition.

**L562–L917 (~4,550 words) — §4, §5, §6, Exam Alert, Practice Questions, Chapter
Summary.** The longest dry stretch in the chapter: from the §4 opener to the closing
quote, only structural markers carry the register. Two sub-locations are worth naming:

- **§3 "Ninety Minutes" (L487–L555, ~1,100 words)** — sits inside the first dry stretch's
  tail and is the most thematically available section in the chapter (running a fixed
  passage against an unpausable clock) while containing not one image. Caution: the
  obvious phrasings here are exactly what the linter's cliché rule forbids —
  `chart a course`, `set sail`, `weather the storm` are all FAIL-on-sight at L307 of
  `structural-contract.yaml`.
- **🏆 Safe Harbor (L920–L926)** — the chapter's emotional close, and entirely literal
  ("axis", "shape", "load", "calibration"). It sits under a marker that promises the
  register and does not deliver it, then hands straight to the closing quote, which does.

**Recommendation: add 3–5 metaphors, not more.** Five additions would land the chapter at
~1.0/1000 — the floor of the band, which is the right target for a synthesis chapter that
is mostly tables and exam logistics. Suggested placements, in priority order: §1 opener
(L109–111); §3, in "The three ways candidates run out of time" (L527–535); Safe Harbor
(L922–926); §6 "The morning" (L684–686), where the pre-departure register is available.
Do not add anything to §2 — it is 1,900 words of discriminator drill and texture would
work against the "work these actively" instruction at L301.

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / me hearties | 0 | — |
| ye (as pronoun) | 0 | — |
| arr / yarr / avast | 0 | — |
| scurvy / landlubber / plunder / booty | 0 | — |
| shiver me timbers / davy jones / walk the plank | 0 | — |
| smooth sailing / weather the storm / all hands on deck | 0 | — |
| chart a course / set sail / batten down the hatches | 0 | — |
| uncharted waters / plain sailing | 0 | — |
| **Landfall** (retired marker name) | **1 — L1, chapter title** | **flag for author decision** |

Clean on every pattern in `structural-contract.yaml` `forbidden_patterns` (L302–309) —
both the pirate-caricature rule and the nautical-cliché rule. No stock phrase survives
anywhere in the chapter.

**The one finding: the chapter title is "Bearings Before Landfall" (L1).**

`style-decisions.md` [LOCKED 2026-04-20] renames `🌅 Landfall` → `☀️ Zenith` and states:
*"Any future 'Landfall' in drafts is drift."* The chapter uses Zenith correctly as §1's
marker at L107, so the title revives a retired name the body has already retired — which
is precisely the collision the rename existed to prevent.

Secondary, milder: "Bearings" is live marker vocabulary (`☆ Taking Your Bearings`, used
twice in this chapter at L241 and L443, and again in the reader-facing table header at
L571). A title built entirely from marker names — one retired, one active — reads as
theme-dressing rather than a title.

**This is not caught mechanically.** `forbidden_patterns` has no rule for retired marker
names; the linter checks pirate vocabulary and nautical clichés only. This audit is the
only gate that sees it. Retitling is the author's call — the register is right, the
vocabulary is not. Options that keep the sense (fix your position before arrival) without
reusing marker names: *"The Second Passage"*, which the closing quote at L940 already
sets up, or *"Two Landmarks"*, which pays off both the epigraph and §2's opening line.
```

**The one thing worth your decision:** the chapter title reuses `Landfall`, retired as a marker name on 2026-04-20 with "any future 'Landfall' in drafts is drift" in the ledger — and the linter has no rule that catches it. Everything else is a density shortfall (0.5/1000 against a 1–3 band), which is fixable with three to five additions at named hinge points rather than any rewriting.