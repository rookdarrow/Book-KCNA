Analysis complete. Emitting the report to stdout for the orchestrator to capture into `diagnostics/theming-density.md`.

---

# Theming-Density Audit — Chapter 4

> **Artifact note.** The stage prompt referenced `draft-voice.md`, which no longer exists at audit time: `orchestrator.py:209–228` swaps the voice-stage output into the canonical slot and backs up the prior draft as `draft-v1-prevoice.md`. This audit reads the voiced draft at `.pipeline-state/ch-04/draft-v1.md` (1,095 lines). Line numbers below refer to that file.

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~13,300**
- Overt nautical/celestial metaphors outside branded markers: **5**
- Density: **0.4 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Counting method.** Whitespace-token count over the whole file (15,392), minus fenced blocks (525 + 18 fence markers), markdown tables (820), HTML comments (260), YAML frontmatter (35), inline `[source: …]` tags (~234 across 117 in-prose tags), and markdown scaffolding tokens (64 blockquote markers, 89 bullet/checkmark markers) → **13,347**. Margin is roughly ±3%; the verdict is stable anywhere in the 10,000–14,000 range.

**Counting rule for sustained devices.** The `Extended Analogy` at L155–161 is counted as **one** metaphor, not as its ~8 constituent images. Counted the other way (each discrete nautical image scored separately), the chapter has 12 metaphors and a density of **0.9 per 1000** — still below band. The verdict does not depend on which rule you prefer.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~155–161 | "Think about the papers a vessel files before departure… A declaration lodged with the harbormaster is not an instruction to anyone… The record outranks the moment it was written." | nautical — harbor / ship's papers | acceptable (sustained, sanctioned sidebar; carries the chapter's core conceit) |
| ~278 | "The four top-level fields you now know are the map. `kubectl explain` is how you read the territory inside `spec`" | nautical — cartography | acceptable, light |
| ~344 | "Two ships on two different registries can carry the same name, and neither registry has to care." | nautical — vessels / registry | acceptable (does real explanatory work on namespace scoping) |
| ~460 | "A Secret is a strongbox stowed in the same hold as everything else. The lock is Chapter 12's; this chapter is only telling you the box did not ship with one fitted." | nautical — stowage / cargo hold | acceptable |
| ~589 | "A label is closer to a signal flag than to a filing category. The flag means whatever your fleet agreed it means; the machinery that reads it only cares that it is flying." | nautical — signals / fleet | acceptable (genuinely clarifying — maps to "labels imply no semantics to the core system") |

**Borderline, not counted:**

| Line | Passage | Why not counted |
|---|---|---|
| ~757–760 | "No hand receives an instruction. Every hand reads the record" | "hand" in the crew sense is very light, and the text sits inside a fenced figure (excluded from the denominator) |
| ~1079 | "You have crossed from *watching the system* to *writing to it*" | adjacent to the branded Voyage Progress strip; "crossed" reads as near-functional |
| ~410 | "one plant, deliberately shallow" | depth-of-treatment, not soundings |
| ~141 | "in front of the one door Chapter 3 showed you" | architectural, not nautical |
| ~107, ~244 | "arrived from imperative tooling" | functional vocabulary per Rule 4 |

**Celestial metaphors: zero.** No `star`, `North Star`, `lodestar`, `celestial`, `constellation`, `orbit`, `sky`, or `firmament` anywhere in body prose. The only celestial content in the chapter is the branded `☀️ Zenith` marker and the `🌅` in the Voyage Progress strip, both of which are structural and excluded by Rule 1.

## Overcooked passages

**None.**

The one locally dense passage is the `Extended Analogy` at L155–161: roughly 8 nautical images in ~230 words, a local rate of ~35 per 1,000. This is dense **by design, not overcooked** — `Extended Analogy` is a formal sidebar type whose entire function is a sustained long-form metaphor, and every beat in it maps to a real mechanism (harbormaster → API server; independent parties consulting the record → controllers watching; "the hold changes, not the paper" → reconciliation direction). No trimming recommended.

One minor note inside it: *"this is the draft, this is where we are bound"* uses "draft" in the ship's-draught sense, in a book whose pipeline and prose both use "draft" to mean a manuscript. The pun is invisible to a reader but is a small ambiguity; "this is what she draws" or simply cutting the clause would remove it. Cosmetic, not a density issue.

**No clichés found.** Targeted scan for `chart a course`, `set sail`, `smooth sailing`, `all hands`, `batten down`, `weather the storm`, `uncharted waters`, `rough seas`, `steady as she goes`, `anchors aweigh`, `navigate the` returned zero matches. Every metaphor in the chapter is bespoke rather than stock — this is the chapter's clear strength on this axis.

## Underseasoned passages

The chapter front-loads nearly all of its thematic texture into one sidebar in §1, then runs roughly 11,000 words on four light touches. Stretches over 800 words with zero thematic texture:

| Range | Approx. words | What's in it | Note |
|---|---|---|---|
| L591–818 | ~2,900 | remainder of §5, Bearings #3, **all of §6**, Exam Alert | **Most conspicuous gap.** §6 "A Declaration, Not an Order" is the chapter's synthesis and climax, and contains no image at all. Its `☀️ Zenith` callout is branded but its prose is metaphor-free. |
| L13–154 | ~2,300 | title block, Attention Budget, Soundings, Why This Chapter Matters, §1 up to the sidebar | Runs texture-free until the Extended Analogy lands at L155. |
| L462–588 | ~1,700 | Secret hardening, types table, side-by-side, Navigational Hazards, Bearings #2 | Between the strongbox touch (L460) and the signal-flag touch (L589). |
| L163–277 | ~1,400 | §2 "The Anatomy of a Record" | The chapter's most important teaching section — the `spec`/`status` authorship boundary — carries no image until the light map/territory touch at L278. |

**Not flagged:** L819–1051 (~2,900 words, Practice Questions and answer explanations). A question bank should be texture-free; adding metaphor there would be a defect, not a fix.

**Overall verdict: the chapter does read texture-less in brand terms**, and the fix is small. Three to five light touches placed in the dry stretches would bring density to roughly 0.7–0.9 per 1,000 counted as devices, or comfortably into band counted by discrete image. Highest-value placements, in order:

1. **§6 (L730–787)** — one image closing the loop back to the harbormaster analogy from §1. The chapter opens by filing papers and ends by explaining that nobody was ever given an order; that arc currently completes in flat prose. This is the single best insertion point in the chapter.
2. **§2, around the authorship boundary (L228–245)** — the `spec`/`status` asymmetry is the most reused idea in the book and has no image attached to it.
3. **§4 opening (L418–425)** — the "one image, two environments" problem is a natural fit for a light touch and currently sits in a 1,700-word dry run.

**Observation, not a defect:** the chapter's only *consistent* figurative register is financial, not nautical — "Chapter 3 owed you something. This is where it comes due" (L169), "That last sentence is a promissory note. Chapter 12 collects on it" (L387), "That is §3 collecting rent one section later" (L434). Three instances of a debt/obligation family against five nautical instances. These are outside the nautical/celestial budget and are not violations, but they explain why the chapter reads as texture-*less* on brand while not being literally metaphor-free: the texture is there, it just isn't the brand's. Worth a look at the voice pass. Converting even one of the three to the maritime register would serve both this audit and voice consistency.

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey | 0 | — |
| ye (as pronoun) | 0 | — |
| avast | 0 | — |
| arr / yarr | 0 | — |
| savvy | 0 | — |
| landlubber | 0 | — |
| scallywag | 0 | — |
| booty | 0 | — |
| plunder | 0 | — |
| bilge | 0 | — |
| swab | 0 | — |
| doubloon | 0 | — |
| buccaneer / corsair | 0 | — |
| hearties | 0 | — |
| belay | 0 | — |

Clean. No caricature register anywhere in the chapter.