Draft located and audited. The context packer looked for `draft-voice.md`; Stage 4 had already swapped that into `draft-v1.md` (pre-voice backed up as `draft-v1-prevoice.md`), so the voiced draft was there under the post-swap name.

```markdown
# Theming-Density Audit — Chapter 1

**Book:** KCNA · **Chapter:** 1, "Taking Departure" · **Chapter type:** orientation

## Audit inputs

Source read: `.pipeline-state/ch-01/draft-v1.md` (42,384 bytes, 481 lines). The context
pack requested `draft-voice.md`, which no longer exists — `orchestrator.py:173-189` swaps
the voiced draft into `draft-v1.md` after Stage 4 and backs the pre-voice copy up as
`draft-v1-prevoice.md`. `context_packer.py:282` still looks for the pre-swap name, so this
stage receives "[file not available]" on every chapter that has passed Stage 4. Packer
bug, not a missing artifact. Audit ran against the correct file.

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~5,780**
- Overt nautical/celestial metaphors outside branded markers: **8**
- Density: **1.4 per 1,000 words**
- Target band: 1–3 per 1,000 words
- Status: **within band** (lower third)

### Counting method (matters here — state it so the number is checkable)

Denominator: `wc -w` total of 6,629, minus fenced-block content (~143), table rows (~646),
horizontal rules (~23), blockquote `>` markers (~28), and HTML/figure-comment tokens (~11).
Estimate carries roughly ±100.

Numerator: **a sustained conceit inside one container counts as one instance.** The epigraph,
the Extended Analogy sidebar, and the closing quote each develop a single figure across several
sentences; the nautical vocabulary inside them (legend, seabed, anchorage, cable) is the figure
working, not additional figures. Counting every overt nautical noun separately would yield 22
instances and a density of 3.8/1,000 — nominally "overcooked" — but that would be an artifact of
the counting rule, since the reader experiences three figures, not twenty-two. Both numbers are
recorded so a reviewer can disagree with the convention without re-reading the chapter.

Excluded as branded/structural, per Rule 1: 🧭 Soundings, ☆ Taking Your Bearings, ★ Fixed Point,
⚠ Navigational Hazards, — Dead Reckoning, 🏆 Safe Harbor, ⚓ Worth Securing, 🪝 Snag, 🔭 Closer Look,
🪢 Mnemonic, `[cross-bearing: …]`, the 🗺️→🌊→🌅 progress strip, "The Voyage Ahead" section name,
"Logbook Entry"/"Extended Analogy" sidebar headers, `the-lodestar.md`, and "Lodestar Ledgers" as
publisher attribution.

Excluded as functional, per Rule 4: "Helm" (the tool, §3); "vessel" in the Chapter 2 preview
(intermodal containers literally stack on ships — that passage is subject matter, and the
etymological source of the software term, not brand theming); "instrument" used in the plain
sense of a measuring device (L128, L425, L457).

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~1 | "Taking Departure" (chapter title) | nautical — navigation | acceptable — technically exact (taking departure = fixing position off a known landmark on leaving the coast), and the epigraph immediately cashes it |
| ~34 | "Take your departure while the landmarks are still in sight. The open sea is no place to discover your chart is wrong." | nautical — navigation / charts (sustained conceit) | acceptable — epigraph slot; states the chapter's actual thesis (stale blueprint = wrong chart) rather than decorating it |
| ~94 | "the Certified Kubernetes Administrator is the next voyage" | nautical — voyage | acceptable — one word, load-bearing, marks a real progression |
| ~183 | "that plan came off the old chart" | nautical — charts | acceptable — economical; four words carrying the section's whole argument |
| ~244 | "you may be studying from the old chart, or thinking in its terms" | nautical — charts | **repeat — recommend neutralizing** (see below) |
| ~289–293 | Extended Analogy: "a chart whose legend is printed on the last page" → seabed marks, rocky bottom / poor holding, anchoring once, the cable grinding | nautical — charts + anchoring (sustained conceit) | acceptable — sanctioned sidebar type; 1 of 2 sidebars in-chapter, inside the 1–3 target; justifies the deferred "cloud native" definition better than an assertion would |
| ~299 | "The instrument panel." | nautical-adjacent — instruments | borderline acceptable — see tic note below |
| ~482 | "A chart is only as good as the survey behind it. Check the date in the corner before you trust the depths." | nautical — charts (sustained conceit) | acceptable — closing quote slot; lands the thesis |

Also present but not counted (inside a fenced figure, therefore outside the prose denominator):
Part VI is named **"Departure"** at ~L315, echoing the chapter title. Structural label, on-brand,
no action.

## Overcooked passages

No passage stacks multiple independent metaphors. The three sustained conceits sit in their
designated containers and are separated by roughly 2,000 words each. Nothing needs trimming for
density.

One genuine finding, which is repetition rather than stacking:

**The same figure runs twice inside §3–checkpoint-1, ~1,000 words apart, doing the same
rhetorical job.**

- ~L183 — "If you were planning to spend a fifth of your study time on Prometheus, that plan
  came off the old chart."
- ~L244 — "If you picked A, you may be studying from the old chart, or thinking in its terms."

Both map *retired blueprint → old chart*. The second adds nothing the first didn't establish,
and near-identical phrasing at that distance reads as a verbal habit rather than a chosen image.

Recommend keeping ~L183 (fresher, more surprising, better placed) and neutralizing ~L244 to
"you may be studying from the retired blueprint, or thinking in its terms." That is also the
more precise wording — §3 names it "the retired blueprint" throughout — and it drops density to
1.2/1,000, still inside the band.

**Motif concentration (note, no action required).** Five of the eight counted instances are the
*same image*: chart. The chapter spends nearly its whole metaphor budget on one figure. Within a
chapter whose entire argument is "your chart is out of date," that is coherence rather than
poverty, and the bookending (title → epigraph → Part VI name → closing quote) is deliberate.
Flagging it only so the pattern is visible if Chapters 2–3 also default to charts, at which point
it becomes a book-level tic. Worth a check at reconciliation.

**Secondary tic — "instrument" (5 occurrences).** L23 (attention-budget row), L128 "a calibrated
practice instrument", L299 "The instrument panel.", L396 heading suffix "Using the Instruments",
L425 "the answers are part of the instrument", L457 "A pacing instrument, not a quiz". Only L299
is a true metaphor and is counted as such; the rest are the plain-English sense and correctly
excluded under Rule 4. But the word is doing double duty — plain measuring-device and
navigational-instrument echo — often enough to register. No single instance is wrong. If one goes,
L128 ("a calibrated practice instrument" → "a calibrated practice exam") is the most disposable.

## Underseasoned passages

Three stretches exceed 800 words with no authored metaphor. Branded markers appear throughout all
three, so none of them reads as flat on the page — the texture is structural rather than authored.

| Range | Approx. words | Content | Assessment |
|---|---|---|---|
| ~L39–92 | ~1,150 | Soundings block + §1 opening | Fine. Soundings is a diagnostic instrument; metaphor there would obstruct it. |
| ~L96–182 | ~1,450 | §2 "Ninety Minutes" + §3 opening | Fine, and partly mandatory — §2 is built around a **Dead Reckoning** block, which is *defined* as metaphor-free. |
| **~L300–481** | **~2,000** | §5 "How This Book Is Built" (after "The instrument panel"), §6 "Three Ways to Read This Book", checkpoint 2, Chapter Summary | **Longest dry stretch in the chapter.** Also the most mechanical content in it — marker tables, part-to-domain map, reading paths. Metaphor sits poorly on a reference table, and the marker tables themselves are saturated with nautical vocabulary at the surface. |

**Overall verdict: the chapter does not feel texture-less.** The opening (title, epigraph, §1) and
the close (Safe Harbor, Voyage Progress, The Voyage Ahead, closing quote) carry the register, and
the Extended Analogy sits at the midpoint. Distribution is bookended rather than even, which is a
legitimate shape for an orientation chapter.

If the author wants to lift density off the band's lower edge, §6 "Three Ways to Read This Book"
is the one natural site — three reader profiles choosing three routes through the same water is a
figure the section already implies and never states. Optional, and worth at most one sentence.
This is offered as placement guidance only; prose quality is not this audit's call.

## Pirate-vocabulary check

Full-file case-insensitive scan. Zero hits across the whole banned register.

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / mateys | 0 | — |
| ye (as pronoun) | 0 | — |
| avast | 0 | — |
| arr / arrr | 0 | — |
| aye / nay | 0 | — |
| hearties / me hearty | 0 | — |
| landlubber / lubber | 0 | — |
| scallywag | 0 | — |
| scurvy | 0 | — |
| booty / doubloon / plunder / treasure | 0 | — |
| buccaneer / pirate / swashbuckling | 0 | — |
| jolly roger / walk the plank / X marks | 0 | — |
| grog / cutlass / bilge / keelhaul / scupper | 0 | — |
| thee / thou / thy / 'tis | 0 | — |

Register holds. The chapter reads as a working navigator, not a costume.

## Verdict

**Within band at 1.4/1,000.** One recommended edit (~L244, de-duplicate the "old chart" figure),
one optional trim (~L128, "instrument"), one book-level pattern to watch at reconciliation
(chart-motif concentration). No overcooking. No pirate drift.
```