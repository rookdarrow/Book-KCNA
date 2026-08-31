The audit is complete. Here is the stage output for `diagnostics/theming-density.md`:

```markdown
# Theming-Density Audit — Chapter 18

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~15,900**
- Overt nautical/celestial metaphors outside branded markers: **14**
- Density: **0.9 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Counting method.** Raw whitespace-token count of `draft-v1.md` is 19,137. Removed: 7 fenced
figure blocks (1,205 words), all table rows (1,237), HTML comment lines — figure anchors and the
three AUTHOR-REVIEW notes (256), `[source: …]` citation tags (167 occurrences, ~306 tokens), and
markdown syntax tokens counted as words — `---` rules, `>` blockquote marks, list dashes, `✓`
marks, heading hashes (~340). Result ≈ 15,900, ±2%. Cross-bearing tags were left *in* the count;
they are inline prose convention, not apparatus, and excluding them moves density by under 0.02.

**Two qualifiers on the count.** First, 10 of the 14 are the same figure — the chapter's
"instruments" conceit. Distinct metaphor families present: navigational instruments (10),
sounding/depth (1), line/rope (1), chart/map (1), open water (1). Second, **there are zero
celestial metaphors in the chapter.** No stars, no fixed bodies, no lodestar outside the publisher
attribution. The brand's celestial half is entirely unused here.

If you count body prose only and exclude the two headings that carry the instruments figure, the
count is 12 and the density is 0.8 per 1000. Either way the chapter sits below the band.

---

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~1 | "Chapter 18: Reading the Instruments" | nautical — navigational instruments | acceptable — conforms to the book's chapter-title convention (Ch 3 *The Ship's Company*, Ch 11 *Below the Waterline*, Ch 17 *The Fleet and Its Charts*) |
| ~45 | "*Before reading, take depth.*" | nautical — sounding / depth | acceptable — tightest possible gloss on the Soundings marker. See note below on convention drift |
| ~104 | "you will have four instruments for it and a clear sense of which one to reach for" | nautical — instruments | acceptable |
| ~125 | "**Choose** the right instrument for a question, instead of reaching for the one you happen to know" | nautical — instruments | acceptable |
| ~146 | "A monitoring system is an instrument built to answer a fixed set of questions very well" | nautical — instruments | acceptable — the figure's best load-bearing use; it does analytical work rather than decoration |
| ~249 | "three instruments and the thing that ties them together… the string running through them" | nautical — line / rope | acceptable — light, and consonant with the 🪢 glyph it sits under |
| ~768 | "§6 — Lines From Everywhere" | pun (log lines / ship's lines) | **not counted** — primary sense is literal; functional per rule 4 |
| ~879 | "Six sections of instruments. Here is the question they exist to answer." | nautical — instruments | acceptable |
| ~1050 | "§8 — One Question, Four Instruments" | nautical — instruments | acceptable |
| ~1052 | "You have four instruments now." | nautical — instruments | acceptable |
| ~1060 | "you have three instruments pointed at three different things" | nautical — instruments | **repetitive** — fifth appearance of the figure inside eleven lines; see below |
| ~1109 | "The instruments follow from that. The dashboards follow from the instruments." | nautical — instruments | acceptable |
| ~1442 | "A map of where the weight actually is, checked against your own Soundings and Bearings history" | navigational — chart / map | acceptable — light; "map" is close to dead-metaphor English |
| ~1444 | "Chapter 19 is where you take your bearings before the last stretch of open water." | nautical — open water | acceptable in isolation; see stacking note |
| ~1446 | "The instruments do not tell you where you are. They tell you what you can find out." | nautical — instruments / position-fixing | acceptable — the strongest single beat in the chapter, and the only place the figure is stated rather than assumed |

**Not counted, and why.** The chapter's dominant figurative register is *financial*, not nautical:
"Chapter 17 ended by handing you a bill" (~96), "This is the chapter where the bill arrives" (~100),
"handed you a bill" (~1107), "This chapter is the payment" (~1109). That is a well-run sustained
metaphor, but it is outside this audit's budget. Also excluded as functional vocabulary: every
occurrence of *instrument/instrumentation* in the OpenTelemetry technical sense (~198, ~206, ~208,
~535, ~543, ~677, ~687, ~689, ~921, and throughout the Q&A), *route* (~1111), *thread* (~605),
*signal* (the OTel term, ~180 occurrences), and all cross-bearing tags.

---

## Overcooked passages

**One mild cluster: lines ~1444–1447 (The Voyage Ahead close + closing epigraph).**

> "You have the instruments. Chapter 19 is where you take your bearings before the last stretch
> of open water."
>
> > *"The instruments do not tell you where you are. They tell you what you can find out."*
> > — Lodestar Ledgers

Three navigational figures in about forty words — instruments, take-your-bearings, open water —
inside a section already named *The Voyage Ahead* and immediately followed by a nautical epigraph.
This is the chapter's send-off, so a beat is earned, and the epigraph is genuinely good. But
"take your bearings" is the weakest of the three: it recycles a branded marker name as a verb in
the same sentence that the chapter tells the reader to check their "Soundings and Bearings history"
two lines earlier. **Recommend trimming that one clause** and letting "the last stretch of open
water" carry the passage into the epigraph.

**One repetition flag: lines ~1050–1060.** The instruments figure appears in the §8 heading, then
at ~1052 ("You have four instruments now"), then again at ~1060 ("three instruments pointed at
three different things"), then twice more at ~1109. Not overcooked by density — it is the synthesis
section restating its own frame, which is legitimate — but ~1060 is the one instance that adds
nothing the heading and ~1052 have not already established. Optional trim.

Nothing else in the chapter stacks. There is no passage where a second metaphor arrives before the
first has cleared.

---

## Underseasoned passages

Three stretches exceed 800 words with zero thematic texture. Together they are about 12,900 of the
chapter's ~15,900 words — roughly 81% of the body prose carries no theming at all.

| Lines | Content | Approx. prose words | Metaphors |
|---|---|---|---|
| ~250–878 | §2 "Why baggage counts" → end of §6 (§3, Checkpoint 1, §4, §5, Checkpoint 2, §6) | **~7,700** | 0 |
| ~880–1049 | §7 in full + Checkpoint 3 | ~2,050 | 0 |
| ~1114–1441 | Exam Alert, 17 Practice Questions + explanations, Chapter Summary, 🏆 Safe Harbor | ~3,150 | 0 |

The first of these is the finding that matters. **Lines ~250–878 is the chapter's entire technical
core — Prometheus, tracing, cluster logging — and it runs roughly 7,700 words without a single
thematic touch.** By contrast, lines 1–249 carry six of the fourteen in about 2,800 words, which is
2.1 per 1000 and comfortably inside the band. The chapter is not uniformly thin; it front-loads its
theming into the opening and its closing, and the middle sixty percent is untextured.

The third stretch is defensible on its face: assessment apparatus is the wrong place for figurative
language, and its absence there is correct. The exception inside it is **🏆 Safe Harbor (~1426–1432)**,
which is a brand moment — the last one in the book's content chapters — and whose prose carries no
texture at all beyond the marker name.

**Three low-cost sites, if the author wants to reach the band.** Adding four to six beats across the
middle would put the chapter at roughly 1.2 per 1000, the low edge of the band, without touching
its analytical register:

1. **§4's pull model (~455–481).** "Which way the arrow points" is already a spatial figure doing
   the work; it wants one navigational turn and does not get one. The section is the chapter's
   densest exam surface and its driest prose.
2. **§5's opening wall (~587–595).** Seven services, seven complete logs, nothing joining them —
   this is a lost-position problem described without once using the vocabulary of lost position.
   The `🪢` line-and-knot register at ~249 was set up for exactly this and is never paid off.
3. **The word *signal* itself.** KCNA is a Communications Officer book, the chapter's central noun
   is "signal," and the chapter never once plays on it. That is a free, fully in-register beat sitting
   unused for 15,900 words.

**Calibration.** Shipped Ch 17 (*The Fleet and Its Charts*) is also lean in body prose — its theming
lives in the chapter title, section titles, and markers rather than in paragraphs. So Ch 18 is
*consistent with the book as shipped*, and the book as shipped appears to sit under the 1–3 band in
prose. Treat this as a chapter-level flag with a book-level cause; do not inject sixteen metaphors
into Ch 18 to hit an arithmetic target while its neighbours sit at 0.5.

**One convention note, not a density finding.** Line ~45 opens Soundings with "*Before reading, take
depth.*" Shipped Ch 17 opens the same marker with plain instructional prose ("Before reading this
chapter, try these questions. Your score determines how to approach the content…"). The Ch 18
version is better and more on-brand, but it is a divergence — worth resolving one way or the other
in a book-wide sweep rather than leaving two Soundings openers in one volume.

---

## Pirate-vocabulary check

Structural linter catches these too, but double-check:

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / maties | 0 | — |
| ye (as pronoun) | 0 | — |
| arr / arrr | 0 | — |
| avast | 0 | — |
| belay | 0 | — |
| aye | 0 | — |
| scallywag | 0 | — |
| landlubber / lubber | 0 | — |
| booty / plunder / doubloon | 0 | — |
| swashbuckling / buccaneer | 0 | — |
| yo-ho / shiver me / walk the plank / jolly roger | 0 | — |
| grog / hearties / cap'n | 0 | — |

**Clean.** No caricature register anywhere in the chapter. The voice holds the seasoned-navigator
line throughout — the problem is the opposite of caricature.
```

**Bottom line:** Ch 18 is at 0.9 metaphors per 1,000 words against a 1–3 band — underseasoned, with 10 of its 14 instances being one repeated figure ("instruments") and zero celestial imagery. The theming is front-loaded and back-loaded; the ~7,700-word technical core (§2 tail through §6) has none. Pirate check is clean, and the only overcooking is a three-figure stack in the closing forty words.