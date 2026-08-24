# Theming-Density Audit — Chapter 6

**Chapter:** `Fleets, Not Vessels` — Book-KCNA
**Source audited:** `.pipeline-state/ch-06/draft-v1.md` (1,254 lines, 127,750 bytes). All line references below are against that file.
**Note:** `draft-voice.md` does not exist at this stage. `draft-v1-prevoice.md` (4,050 bytes) is the truncated stdout capture and was not audited.

## Summary

- Total word count (body prose only, excluding code blocks and tables): **≈16,900**
- Overt nautical/celestial metaphors outside branded markers: **15**
- Density: **0.9 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned** (marginally below band)

**Method for the denominator.** `wc -w` on the whole file returns 19,315 tokens. Removed: 9 fenced blocks (518 words, lines 138–161, 205–220, 230–233, 392–398, 407–421, 432–445, 619–640, 715–733, 900–925); 4 tables (919 words, lines 17–31, 495–502, 960–968, 1195–1216); 13 HTML comments (≈521 words, of which 7 are AUTHOR-REVIEW notes and 6 are FIGURE anchors); 142 inline `[source: …]` tags (≈284 tokens); ≈200 markdown/marker glyph tokens (`>`, `---`, `✓`, `☐`, difficulty and marker symbols at line start). Result ≈16,873, reported as ≈16,900. Treat as ±3%.

**Second denominator worth having.** Roughly 3,400 of those words are reference apparatus where thematic texture is neither expected nor wanted — Exam Alert, the 19 Practice Questions with their answer explanations, and the Chapter Summary table's surrounding prose (lines 942–1219). Against narrative prose only (≈13,500 words), density is **1.1 per 1000** — inside the band, at its low edge. Both numbers are honest; the second is the more useful editorial signal, and the gap between them is itself the finding: this chapter's theming lives almost entirely at its structural seams.

**Register.** All 15 instances are nautical. Zero celestial metaphors appear outside branded markers (☀️ Zenith and the 🗺️→🌊→🌅 progression are markers and excluded). The register is age-of-sail — harbor pilot, deck, aground, berth — which is consistent with the sibling chapter titles in this book (*Taking Departure*, *The Ship's Company*, *The Smallest Vessel*, *Assigning the Berth*), so this is coherence, not drift.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 3 | "Chapter 6: Fleets, Not Vessels" | nautical — fleet/vessel | acceptable — the chapter's controlling figure, and it does real conceptual work (many-vs-one) |
| 4 | "*Nobody sails one Pod*" | nautical — sailing | acceptable — original construction, not a stock phrase |
| 44 | "A standing order outlives the watch that received it." | naval — watchkeeping | acceptable — earns its epigraph slot; "standing order" becomes the chapter's through-line |
| 294 | "It is two standing orders written about the same crew." | naval — standing orders / crew | acceptable — the strongest single beat in the chapter; lands the overlapping-selector failure in one image |
| 361 | "☐ How a running fleet gets replaced with a different one" | nautical — fleet | acceptable — light, checkpoint scaffolding |
| 366 | "§4 — Changing the Fleet Under Way" | nautical — under way | acceptable — "under way" is precise here (mid-passage), not decorative |
| 541 | "Five questions on changing the fleet…" | nautical — fleet | acceptable — light, echoes the §4 heading |
| 652 | "A Deployment's Pods are a watch rotation. Any qualified hand can stand any watch; the roster says 'three on deck'… when someone goes below you send up whoever is next." | nautical — watch rotation (Extended Analogy ¶1) | acceptable — sanctioned sidebar form; see Overcooked note below |
| 654 | "A StatefulSet's Pods are a pilot who knows this harbor… the chart of this specific approach… the same soundings, and the same name on the manifest, or the ship goes aground" | nautical — pilotage (Extended Analogy ¶2) | acceptable with one edit — see marker-collision note |
| 656 | "treat interchangeable crew as irreplaceable… treat irreplaceable crew as interchangeable and you lose data" | nautical — crew (Extended Analogy ¶3) | acceptable — closes the analogy on the pedagogical point |
| 893 | "## ☀️ §9 — Nobody Sails One Pod" | nautical — sailing (title callback) | acceptable — deliberate return, not repetition-by-accident |
| 941 | "Which returns you to the title. Nobody sails one Pod, not because a single Pod is forbidden…" | nautical — sailing (title callback) | acceptable — the third and final strike of the motif; the chapter has earned it by here |
| 1230 | "You know how a fleet is described. Next you find out how a berth is assigned." | nautical — fleet + berth | acceptable — hands off to Ch 7's own title (*Assigning the Berth*) |
| 1232 | "Finding the water to carry it out is the other half of the work." | nautical — sounding/depth | acceptable — fresh, not stock, and the "standing order" callback ties the two epigraphs together |
| 1230/1232 | (counted separately above: "berth" and "finding the water") | — | — |

**Not counted — functional language, per rule 4:**

| Line | Passage | Why excluded |
|---|---|---|
| 61 | "a log-collection agent has to run on every machine in your fleet" | "fleet of machines" is industry-standard ops vocabulary, not a figure |
| 80 | "whatever the fleet size happens to be" | same |
| 183 | "writing a bare Pod manifest" | Kubernetes term of art |
| 187, 830 | "a Helm chart's job", "why Helm charts have a `crds/` directory" | product name |
| 292, 686, 935, 1189 | "Somebody ships a second workload", "plugins ship as DaemonSets", "the loops Kubernetes ships" | standard software usage |
| 20, 84, 193, 1136 | "A Loop You Can Watch Working", "keeps watching", "a controller that watches `Certificate` objects" | literal observation; `watch` is also a Kubernetes API verb |
| 1239 | "Take the measure of what changed." | general English idiom, no nautical specificity |

**Not counted — inside tables (excluded from the denominator, listed for completeness):** line 23 (`§4 — Changing the Fleet Under Way`) and line 30 (`§9 — Nobody Sails One Pod`) in the Attention Budget table are section-title references, already counted at their headings.

**Not counted — branded markers:** 🧭 Soundings, ☆ Taking Your Bearings ×3, ★ Fixed Point ×5, ⚠ Navigational Hazards ×2, — Dead Reckoning, 🏆 Safe Harbor, ☀️ Zenith, 🗺️→🌊→🌅 Voyage Progress ×2, ⚓ Worth Securing ×3, 🪝 Snag ×4, 🔭 Closer Look, 🪢 Mnemonic, Logbook Entry, Extended Analogy header, `The Voyage Ahead`, and the 40+ `*[cross-bearing: …]*` pointers. All structural terminology.

## Overcooked passages

**Only one candidate, and it is not a defect.**

**Lines 652–656 — the Extended Analogy (watch rotation vs. harbor pilot).** ≈15 distinct nautical terms in ≈230 words: *watch rotation, stand any watch, hand, roster, on deck, goes below, send up, pilot, harbor, chart, approach, relieved, soundings, manifest, ship, aground, crew*. Local density ≈65 per 1,000 — roughly 70× the chapter average.

Verdict: **acceptable, do not trim.** `Extended Analogy` is a locked sidebar type (style-decisions, 2026-04-19) whose whole function is long-form metaphor, and the brand permits 1–3 sidebars per content chapter combined; this chapter has two (Logbook Entry at 290–296, Extended Analogy at 652–656). Sustained density is the form working as designed, and the analogy is carrying the chapter's hardest distinction (interchangeable vs. identity-bearing Pods) rather than decorating it.

Two small edits recommended, both marker-collision rather than density:

- **Line 654, "the same soundings"** — collides with the branded marker `🧭 Soundings`, which appears in this same chapter at line 49 and is referenced again at lines 606 and 897. Lowercase in-prose use of a branded term is drift surface. Suggest **"the same depths"** or **"the same tide tables"**; both keep the pilotage register without shadowing the marker.
- **Line 654, "chart" used twice** ("the chart of this specific approach" … "given the same chart") — also shadows `🗺️ Chart` in the Voyage Progress strip, which appears at lines 593 and 1255. The repetition is doing emphasis work, so if only one edit is made, make the `soundings` one; but varying the second instance to **"the same approach notes"** would remove both problems at once.

**Lines 1230–1232 — the chapter close.** Three figures ("how a fleet is described", "how a berth is assigned", "Finding the water to carry it out") in ≈50 words. Local density is high, but this is a deliberate closing cadence at a chapter seam, the "standing order" callback pays off the opening epigraph, and "berth" is a direct handoff to Ch 7's title. **Leave as is.**

No cliché nautical constructions found. Specifically absent: *chart a course, set sail, smooth sailing, all hands, batten down, uncharted waters, even keel, weather the storm, sink or swim, rising tide, tip of the iceberg*.

## Underseasoned passages

Four stretches of >800 words carry **zero** thematic texture. Together they account for ≈13,200 of ≈16,900 words — **78% of the chapter**.

| Lines | Span | Words (approx) | Assessment |
|---|---|---|---|
| 45–293 | Soundings + answers, Why This Chapter Matters, What You'll Learn, §1, §2, most of §3 | ≈3,900 | **Flag.** This is the chapter's opening 23% and it runs from the epigraph (44) to the Logbook Entry (294) with nothing in between. "Why This Chapter Matters" and the §1 reframe ("the Pod you spent all of Chapter 5 learning is an object you will almost never create directly") are the two highest-leverage passages in the chapter for a thematic beat, and both are bare. |
| 367–540 | §4 in full, §5 in full | ≈2,270 | **Flag.** The densest teaching in the chapter — rolling updates, the two bounds, revisions and rollback — and the only figure in 174 lines is the section heading itself. §4's "what makes it safe" turn (455–465) and §5's "Same loop. Same mechanics. Opposite direction." (522) are both natural landing spots. |
| 657–892 | §6 close, §7 in full, §8 in full, Taking Your Bearings #3 | ≈3,860 | **Flag — largest gap.** Immediately after the chapter's one Extended Analogy, texture drops to zero for 236 lines. §7's DaemonSet ("one per node, and you never revisit it when the cluster grows") and §8's closing turn ("the thing that extends Kubernetes is itself deployed *by* Kubernetes") are both strong candidates. |
| 942–1219 | Exam Alert, 19 Practice Questions + answers, Chapter Summary | ≈3,400 | **Do not flag.** Reference apparatus. Theming here would read as padding and would work against the recall function. This span is the main reason the full-chapter denominator drags density below band. |

**Recommendation.** The chapter is not texture-less in feel — its seams are well seasoned, and the Extended Analogy is genuinely good — but its interior is bare enough that a reader who opens at §4 and reads to §8 encounters no brand voice at all for ~6,100 words. Adding **four to six** light single-clause touches, distributed across the three flagged gaps, would bring full-chapter density to ≈1.2–1.3 per 1,000 and narrative-only density to ≈1.5 per 1,000 — comfortably mid-band without approaching the caricature line. Suggested anchor points, in priority order:

1. **§4, around line 455–465** — the "gradual is not the same as safe" turn. A single figure about a relief crew coming aboard before the old one is dismissed would carry `maxSurge`/`maxUnavailable` at almost no word cost.
2. **§8, around line 820–824** — "the thing that extends Kubernetes is itself deployed *by* Kubernetes."
3. **Why This Chapter Matters, around line 100–104** — the newcomer-vs-practitioner contrast ("Practitioners write down the count and the template and go home") is one clause away from a standing-order beat that would set up the epigraph's payoff at line 1232.
4. **§7, around line 680–686** — the DaemonSet "you never revisit it when the cluster grows" observation.

Nothing here is required. The skill permits selective use, and 0.9 is a near miss rather than a failure. But the distribution is lopsided enough that the fix is placement, not volume.

## Pirate-vocabulary check

Structural linter catches these too; double-checked here against the full file including code blocks and comments.

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / mateys | 0 | — |
| ye (as pronoun) | 0 | — |
| yer | 0 | — |
| avast | 0 | — |
| arr / arrr | 0 | — |
| landlubber / lubber | 0 | — |
| scallywag | 0 | — |
| booty / plunder | 0 | — |
| buccaneer | 0 | — |
| doubloon / pieces of eight | 0 | — |
| grog | 0 | — |
| savvy (as interjection) | 0 | — |
| shiver me / walk the plank / jolly roger | 0 | — |
| cap'n | 0 | — |

**Clean.** No caricature register anywhere in the chapter. The nautical vocabulary that is present (*watch, roster, deck, pilot, harbor, soundings, manifest, aground, berth, standing order*) is working-seamanship register, which is the locked brand voice.

## Findings for downstream stages

Out of scope for this audit, surfaced because they were encountered while reading:

- **Marker collision, line 654** — lowercase "soundings" and "chart" in the Extended Analogy shadow the branded `🧭 Soundings` and `🗺️ Chart` elements. Edit recommended above. This belongs to the structural linter's branded-terms check as well as here.
- **Not a theming issue but noted:** five `<!-- AUTHOR-REVIEW -->` comments (lines 1, 9, 266, 404, 670, 690, 767) remain embedded and must be resolved before publication. Two of them (670, 767) request one-token cross-bearing edits in `chapter-01` and `chapter-02` that cannot be made from inside this draft.