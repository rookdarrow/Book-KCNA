Analysis complete. Emitting the stage artifact to stdout (the orchestrator writes `diagnostics/theming-density.md`; a live `.theming-density.md.heartbeat` is present, so I have not written the file myself).

---

```markdown
# Theming-Density Audit — Chapter 17

## Summary

- Total word count (body prose only, excluding code blocks and tables): **20,408**
  - Raw file: 23,261 words / 1,666 lines
  - Less 1,653 words in table rows (83 rows), 925 in the eight ASCII figure fences, 259 in HTML comments (2 AUTHOR-REVIEW notes + 8 FIGURE anchors), 16 fence markers
- Overt nautical/celestial metaphors outside branded markers: **20**
- Density: **0.98 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned (marginal — sitting on the floor of the band)**

**Second reading, because the headline number is misleading.** 7,449 words of this chapter (36.5%) are assessment apparatus — Soundings (707), three Taking Your Bearings blocks (1,032 / 1,266 / 1,165), and the 21-question Practice set with explanations (3,279). Metaphor is correctly near-absent there; an exam question written in figurative language is a defective exam question. Excluding it:

- Expository prose: **~12,959 words**, carrying **16** of the 20 metaphors → **1.23 per 1000 — within band**
- Assessment apparatus: ~7,449 words, 4 metaphors → 0.54 per 1000 (appropriate)

So the chapter is not thin where it teaches. It is thin *overall* because it is the longest chapter in the book and carries the heaviest question load. The corrective action is narrow and identified below (§6–§8), not general.

**Character of the theming.** This chapter runs essentially one figure — **map / chart / terrain** — nine times, plus a fleet bookend at the title and the last line. That is unusually disciplined rather than sparse: the metaphor is load-bearing (the CNCF Landscape genuinely is a chart of terrain, and the source says so in those words), it is never decorative, and it never competes with the technical claim next to it. No cliché. No pirate register. No celestial imagery at all outside the branded ☀️ Zenith marker.

---

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 1 | "Chapter 17: **The Fleet** and Its Charts" | nautical — fleet | acceptable — the chapter's subject genuinely is the multi-project ecosystem |
| 1 | "The Fleet and Its **Charts**" | nautical — cartography | acceptable — earned; §2's Landscape material is literally a chart |
| 3 | "the foundation that **keeps the map**" | nautical — cartography | acceptable — quiet pun on "foundation" (CNCF), doesn't announce itself |
| 84 | "see Ch 5 §2 — more than one container **aboard**" | nautical — shipboard | acceptable — inherited chapter title, cited not authored |
| 307 | "it is offering you **the old map**" | nautical — cartography | **strong.** A navigator-brand book calling a superseded TAG list "the old map" is exactly on-register and does pedagogical work |
| 313 | "### **The map of the terrain**" (heading) | nautical — cartography | acceptable — adopts the source's own image for the section it introduces |
| 315 | "the foundation's attempt to **chart the whole space**" | nautical — cartography | acceptable — verb used precisely, sits directly beside the quotation using the same image |
| 328 | "the governance structure and **the map** are the same structure" | nautical — cartography | acceptable — the figure is carrying an argument, not ornamenting one |
| 447 | "the Landscape, which **catalogs the terrain**" | nautical — cartography | acceptable — inside an answer explanation, appropriately flat |
| 520 | "you would see **both maps** side by side" | nautical — cartography | acceptable |
| 535 | "**Both maps are correct.** They are answering different questions." | nautical — cartography | **strong.** The chapter's central epistemic point delivered through the running figure |
| 565 | "That is **the map**. §9 says what it means." | nautical — cartography | acceptable — section-closing beat, one sentence, no elaboration |
| 687 | "see Ch 5 §2 — more than one container **aboard**" | nautical — shipboard | acceptable — inherited title, second citation |
| 822 | "the documentation's wider extension **map** beside it" | nautical — cartography | acceptable |
| 1364 | "the extension-points **map**, one altitude higher" | nautical — cartography | acceptable — figure caption, restrained |
| 1376 | "see Ch 2 §8 — **the crate, not the cargo**" | nautical — cargo | acceptable — inherited title |
| 1376 | "see Ch 6 §9 — nobody **sails** one pod" | nautical — sailing | acceptable — inherited title |
| 1423 | "whether a concept is **anchored** or merely adjacent" | nautical — ground tackle | acceptable — light, and consonant with the ⚓ margin icon without duplicating it |
| 1664 | "learning **the shape of the fleet**" | nautical — fleet | acceptable — closes the title's loop, 1,663 lines later |
| 1664 | "Next you learn to **read its instruments**." | navigation — instrumentation | **strong.** Double duty: the closing image *is* the handoff to Chapter 18's observability material |

### Borderline, deliberately not counted

| Line(s) | Passage | Why uncounted |
|---|---|---|
| 92, 571, 703, 1650 | "the **leg** from the Ingress to the Pod" | Standard network jargon (cf. "call leg"). The author plausibly chose it over "hop" for register, but it is not *overt* — rule 4 applies. Four occurrences; if theming is later increased, note this is already quietly doing work. |
| 108, 1364 | "It changes **altitude**" / "one altitude higher" | Aviation/zoom sense, not the celestial-navigation sense. See recommendation below. |
| 206 | "it is **cargo** cult" | Fixed idiom for a software anti-pattern, not a figure. Worth a note only because Chapter 2 is titled *Cargo in Standard Crates* — the echo is accidental and harmless. |
| 122 | "a release **train**" | Rail, and standard release-engineering jargon. |
| 1217 | "the **flagship** conference series" | Fully lexicalized dead metaphor. |
| 315 | "a map through the previously **uncharted terrain**" / "a particularly **well-traveled path**" | Verbatim CNCF quotation. Contributes texture to the reader's experience but is not the book's spend. |
| 827 | "you are in **the passage**" | Gloss on the 🗺️→🌊→🌅 Voyage Progress marker, using the marker's own locked vocabulary. Branded, not authored metaphor. |

### Branded markers present and correctly excluded

🧭 Soundings · ☆ Taking Your Bearings (×3) · ★ Fixed Point (×7) · ⚠ Navigational Hazards (×4) · — Dead Reckoning · 🏆 Safe Harbor · ☀️ Zenith (§9) · 🗺️→🌊→🌅 Voyage Progress · The Voyage Ahead · ⚓ Worth Securing (×5) · 🪝 Snag (×5) · 🔭 Closer Look (×5) · 🪢 Mnemonic (×4) · Logbook Entry · cross-bearing (×30). All structural terminology per `branded-terms.yaml` and style-decisions 2026-04-19. None counted.

---

## Overcooked passages

**None requiring a trim.**

The densest local patch is §2's *"The map of the terrain"* subsection (L313–328, ~350 words): heading at 313, "chart the whole space" at 315, the quoted "uncharted terrain"/"well-traveled path" at 315, and "the map are the same structure" at 328 — locally ~8.5 per 1000. Under a mechanical reading that is over-dense. It is not a defect: the passage is introducing a CNCF artifact whose own repository describes it in exactly this vocabulary, so the surrounding prose is matching the source rather than dressing it. Leave as written.

Second-densest is L1664, two images in one sentence pair ("the shape of the fleet" / "read its instruments"). This is the chapter's only flourish, it lands on the last line before the closing quote, and the second image doubles as the Chapter 18 handoff. Leave as written.

L1376 puts two nautically-titled cross-bearings in one line ("the crate, not the cargo", "nobody sails one pod") within a four-pointer run. Mild stacking, but both are citations of other chapters' titles, not figures composed here. No action.

---

## Underseasoned passages

Stretches over 800 words with zero thematic texture, longest first:

| Lines | Span | Words | Note |
|---|---|---|---|
| **823–1363** | §6 Serverless, §7 Autoscaling, §8 Community, TYB 3, §9 opening | **~6,830** | **The one real finding.** Three full sections and 540 lines with no thematic beat whatsoever. §9 is the ☀️ Zenith — the chapter's synthesis moment — and it reaches its "one story" payoff (L1370, L1374, L1378) on entirely literal language. |
| 1424–1663 | Practice answers → Exam Alert → Summary → Safe Harbor → Voyage Ahead | ~3,838 | Mostly assessment and tabular summary; appropriately flat. The Safe Harbor prose (L1648–1650) and Voyage Ahead (L1656–1662) are the exceptions — 400 words of genuine closing prose that carry nothing until the final line. |
| 85–306 | Soundings answers, Why This Chapter Matters, What You'll Learn, §1 entire, §2 opening | ~3,406 | Includes ~1,900 words of expository opening. *Why This Chapter Matters* is the chapter's most rhetorically shaped prose and is entirely literal. |
| 329–446 | §3 entire + TYB 1 questions | ~1,615 | §3's closing argument ("Small pieces, replaced whole… described rather than commanded", L376–382) is the best-written passage in the chapter and is texture-free. |
| 566–686 | §5 first half (service mesh definition, the two planes) | ~1,223 | Dense technical vocabulary; flatness is defensible here. |

Also worth recording: **all nine section titles are theme-free** — "What 'Cloud Native' Actually Names", "Small Pieces, Replaced Whole", "Every Place Kubernetes Lets You In", "A Network That Knows What It's Carrying", "Code Without a Server to Put It On", "Four Things That Scale", "One Pluggability Story". They are good titles, and it is a legitimate authorial choice. But it means the chapter's entire theming budget is spent in the title, the §2 Landscape passage, and the last sentence.

### Recommendation, scoped

Do **not** distribute metaphors evenly, and do not put any into the question-and-answer apparatus. If the author wants this chapter inside the band on the whole-chapter number, the cheapest and most defensible spend is **three to five beats across L823–1363**, which would lift the chapter to ~1.2/1000 and the expository half to ~1.5/1000 — comfortably mid-band, still well short of theme-dressing.

Two specific openings, offered as observations rather than prescriptions:

1. **§9 (L1330–1378) is the strongest candidate.** It is the Zenith section, its whole function is recognition, and its argument is already spatial ("collapsed into the single relation they were always instances of"). One image at the §9 close would be the highest-value single addition in the chapter.

2. **"Altitude" (L108, L1364) is a missed celestial beat.** In celestial navigation *altitude* is a term of art — the angular height of a body above the horizon, the thing a sextant measures. The chapter uses it twice, both times in the flat modern zoom sense ("It changes altitude", "one altitude higher"). The word is already on the page and already repeated; it would cost nothing to let one of the two carry its navigational meaning. This would also give the chapter its only celestial reference outside the ☀️ Zenith marker, which is currently a gap: the brand is nautical **and** celestial, and this chapter is 100% nautical.

---

## Pirate-vocabulary check

Verified against the exact `forbidden_patterns` regexes in `knowledge-base/voice/structural-contract.yaml` (L302–309), case-insensitive, across the whole file.

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey | 0 | — |
| ye (as pronoun) / "ye be" | 0 | — |
| yarr / arr | 0 | — |
| scurvy | 0 | — |
| landlubber | 0 | — |
| plunder | 0 | — |
| avast | 0 | — |
| shiver me timbers | 0 | — |
| davy jones | 0 | — |
| walk the plank | 0 | — |
| me hearties | 0 | — |

**Nautical cliché check** (same contract block, `strictness: expected`):

| Term | Occurrences | Action |
|---|---|---|
| smooth sailing | 0 | — |
| weather the storm | 0 | — |
| all hands on deck | 0 | — |
| chart a course for/to | 0 | — |
| set sail for/towards | 0 | — |
| batten down the hatches | 0 | — |
| uncharted waters | 0 | — |
| plain sailing | 0 | — |

Also checked and absent: "on the horizon", "choppy/troubled waters", "navigate the waters", "tip of the iceberg", "rising tide", "turn the tide", "steady as she goes", "full steam".

**Clean.** Note for the record that L315 contains "uncharted **terrain**" — that is the CNCF Landscape repository's own wording inside a `[source:]` quotation, and it is not the banned "uncharted waters". Do not let a later stage "correct" it.
```