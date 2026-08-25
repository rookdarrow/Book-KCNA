Analysis complete. Every nautical/celestial hit in the file resolved to a branded marker or the publisher name; the phrasal sweep and pirate sweep both returned zero. Here is the audit artifact.

---

# Theming-Density Audit — Chapter 9

**Book:** KCNA · **Chapter:** 9 — *Every Pod Has an Address* · **Source:** `.pipeline-state/ch-09/draft-v1.md` (1,401 lines)

## Summary

- Total word count (body prose only, excluding code blocks and tables): **16,890**
- Overt nautical/celestial metaphors outside branded markers: **0**
- Density: **0.0 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Word-count derivation** (whole file 19,120 words):

| Deduction | Words |
|---|---|
| Table rows (`^\|`) | −1,062 |
| HTML comments (FIGURE anchors + AUTHOR-REVIEW notes) | −293 |
| ASCII-figure lines carrying box-drawing glyphs | −764 |
| Plain-text lines inside fences (captions, `kubectl` block) | ≈−111 |
| **Body prose** | **16,890** |

At 16,890 words the target band implies **17–51** overt metaphors. The chapter has none. This is not a marginal miss — it is a floor breach by the entire budget.

**The distinction that matters most for remediation:** the *page* is not texture-less. The chapter carries **88 branded-marker and cross-bearing surfaces** (28 of them cross-bearings), which is dense brand furniture by any measure. What carries zero brand texture is the **prose itself**. Every figure of speech in this chapter is drawn from outside the nautical/celestial register. So the fix is not "add theming" — it is "let a handful of the existing figures be brand-register figures instead of generic ones."

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| — | *(no qualifying instances)* | — | — |

Every lexical hit in the sweep resolved to structural terminology, not prose metaphor:

| Line | Surface | Ruling |
|---|---|---|
| 39, 1402 | `— Lodestar Ledgers` (epigraph attributions) | Publisher name — not a metaphor |
| 43, 168 | `🧭 Soundings` | Branded marker |
| 82, 1005, 1008, 297, 778 | `⚠ Navigational Hazards` | Branded marker |
| 104, 818 | `— Dead Reckoning` | Branded marker |
| 923, 950, 964, 1377 | `☀️ Zenith` (incl. figure-anchor slug) | Branded marker |
| 1381 | `🏆 Safe Harbor` | Branded marker |
| 1385, 1389 | `Voyage Progress` / `The Voyage Ahead` | Branded marker / contract section name |
| 1297 | "plausible-**sounding** answer" | Functional vocabulary (Rule 4) |
| 59, 192, 196, 403, 1014 | "**ships** with no networking implementation", "Kubernetes **ships** the network" | Standard software idiom, not nautical figure (Rule 4) |
| 463, 974 | "**destination**", "crosses that **boundary**" | Functional networking/spatial vocabulary (Rule 4) |
| 952, 1383 | "**arrived** at properly", "You **arrived** at this chapter" | Generic idiom; voyage-adjacent but not a deliberate figure |

**Figurative language that *is* present, in non-brand registers** (listed so the revision stage does not re-derive it — these are the swap candidates, not defects):

| Line | Passage | Register |
|---|---|---|
| 289–309, 376, 960, 1366 | "the type **ladder**", "each **rung**", "the three that **stack**" | Architectural — the chapter's dominant recurring figure |
| 295 | "It is a DNS alias **wearing a Service's clothes**." | Costume / disguise |
| 326 | "### The **ceiling**" | Architectural |
| 469 | "The selector **proposes**; readiness **disposes**." | Proverb allusion |
| 536 | "it's a **coin flip**" | Gambling |
| 548 | "the quiet **workhorse** of migrations" | Equine |
| 715 | "a good **inoculation** against reading kube-proxy as load-bearing" | Medical + architectural |
| 972 | "they do it by ***offering a door***" | Architectural |

## Overcooked passages

**None.** No passage in this chapter stacks multiple overt metaphors, because no passage contains one. There is nothing to trim on this axis, and no cliché exposure — the sweep for `chart a course`, `set sail`, `smooth sailing`, `weather the storm`, `true north`, `guiding star`, `stay the course`, `uncharted`, `dead in the water`, and 40 further stock phrases returned zero hits.

Worth recording explicitly: a chapter that scores 0.0 has *also* scored zero on the brand's primary failure mode. If the revision stage adds texture, the cliché floor is the thing to watch, not the ceiling.

## Underseasoned passages

Measured two ways, because the two answers differ sharply.

**Strict reading — stretches with zero prose metaphor:** the chapter is a single 16,890-word stretch. Every section qualifies.

**Practical reading — stretches with zero brand surface of any kind** (no marker, no cross-bearing, no metaphor):

| Range | Section | Words | Note |
|---|---|---|---|
| **1015–1376** | **Practice Questions + Answers with Explanations** | **3,735** | The dominant gap. 21 questions and their full explanations run without a single branded surface. ~22% of the chapter's prose. |
| 564–637 | ☆ Taking Your Bearings #2 body | 1,167 | Questions, answers, checkpoint |
| 339–408 | ☆ Taking Your Bearings #1 body | 974 | Questions, answers, checkpoint |

The Practice Questions block is the one flag I would carry forward. Three-and-a-half thousand words is long enough that a reader who opens the book there — which is exactly how a study guide gets used in the last week before an exam — encounters no signal that they are reading a Lodestar Ledgers book at all.

**Highest-leverage slots for the revision stage**, in order of cost-to-benefit. These are placement observations, not prose grades:

1. **Both epigraphs are non-thematic.** Line 38 (*"A name is a promise that survives the thing it named."*) and line 1401 (*"You do not need to know where a thing is. You need to know what to call it, and who keeps the answer current."*) are house-attributed, in-voice, and carry zero nautical/celestial imagery. These are the two cheapest slots in the chapter — they are already brand-attributed, already set apart, and changing them touches no technical content and no source tags.
2. **The recurring "ladder" figure (§3, five occurrences).** It is the chapter's load-bearing metaphor and it is architectural. A register-appropriate equivalent would convert five instances at once, which is roughly a third of the band floor from one decision.
3. **🏆 Safe Harbor prose (1381–1383)** and **The Voyage Ahead (1389–1399)** sit directly beneath branded markers that promise the register, then deliver flat technical summary.
4. **§8 / ☀️ Zenith (950–974)** is the chapter's synthesis beat and its strongest writing. It reaches for "a question does not have a location" — an abstract close where the brand register is natively available.

Recommend the revision stage target the low end of the band (≈17) via slots 1–3 rather than distributing 17 metaphors mechanically across a heavily source-tagged technical chapter. Forcing the count into §1, §4, §6 or the Practice Questions would introduce the cliché risk the chapter currently has none of.

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / mateys | 0 | — |
| ye (as pronoun) | 0 | — |
| arr / avast / aye | 0 | — |
| hearties / scallywag / landlubber | 0 | — |
| plunder / booty / doubloon / treasure | 0 | — |
| jolly roger / walk the plank / shiver me timbers | 0 | — |
| cap'n / swab / grog / buccaneer / corsair | 0 | — |
| marooned / cutlass / parley / scurvy / kraken / barnacle | 0 | — |

**Clean.** No caricature exposure.

---

## Notes for the next stage

- **Verdict is mechanical, and the tension is worth naming.** The 1–3/1000 band was ratified 2026-04-18 against CAPM Ch 1, an orientation chapter. Chapter 9 is a dense technical chapter with 30+ inline source tags and seven ASCII figures. The band is the band and I have applied it as written, but the gap between "0.0" and "underseasoned prose" is smaller here than the number implies — the chapter reads as in-voice (calm, precise, wry-sparing), it simply reads as in-voice *without imagery*.
- **Two AUTHOR-REVIEW comment blocks remain unresolved** (lines gating the "you must install a CNI plugin" claim, the `port`/`targetPort`/`nodePort` fields, and EndpointSlice internals). Not this audit's concern, but any revision pass touching §1, §3 or §4 will land next to them.
- Verification for this audit: three independent regex sweeps against `draft-v1.md` — lexical nautical/celestial (~90 terms), phrasal figures (~50 stock expressions), and pirate register (~30 terms). Full nautical/celestial hit list was 17 lines, all resolved to branded markers or the publisher name; both other sweeps returned no matches.