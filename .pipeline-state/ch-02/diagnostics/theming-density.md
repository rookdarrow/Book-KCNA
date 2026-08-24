Audit complete. Emitting the stage document to stdout per the pipeline contract (`Write` is deliberately outside `--allowed-tools`; the orchestrator captures stage output atomically).

```markdown
# Theming-Density Audit — Chapter 2 (KCNA: "Cargo in Standard Crates")

## Summary

- Total word count (body prose only, excluding code blocks, tables, and HTML comments): **≈13,830**
  - Of which assessment apparatus (🧭 Soundings, 3× ☆ Taking Your Bearings, Practice Questions): ≈6,235
  - **Narrative prose only: ≈7,600**
- Overt nautical/celestial metaphors outside branded markers: **8**
- Density: **0.6 per 1000 words** (whole chapter) / **1.1 per 1000 words** (narrative prose only)
- Target band: 1–3 per 1000 words
- Status: **underseasoned — and, more importantly, severely clustered**

Both readings matter. Measured against all body prose the chapter sits well below band. Measured against narrative prose only — excluding question banks, where dryness is correct — it lands on the band's lower edge. Either way the distribution is the real finding: **7 of the 8 instances sit in the chapter's frame (title, subtitle, epigraph) or in §8**, leaving one metaphor across §2–§7.

Zero celestial metaphors of any kind. The nautical payload is entirely one conceit: the intermodal shipping crate.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~1 | "Cargo in Standard Crates" (chapter title) | nautical — cargo/shipping | acceptable — controlling metaphor, well chosen |
| ~2 | "Why the shipping container beat the ship" (subtitle) | nautical — shipping | acceptable — states the chapter's thesis, not decoration |
| ~35 | "The crate outlives the ship. Standardize the crate." (epigraph) | nautical — shipping | acceptable |
| ~178 | "Kernel below, everything above it in the crate." | nautical — cargo | acceptable — the one mid-chapter touch, and it does real work |
| ~707 | "The Crate, Not the Cargo" (§8 heading) | nautical — cargo | acceptable |
| ~711 | "Nobody at the crane has an opinion about what is inside." | nautical — port/cargo handling | acceptable, but see Overcooked (duplicates the Extended Analogy) |
| ~719 | "Kubernetes never needed to know what is in the crate … It knows the shape of the fitting." | nautical — cargo | acceptable — the Zenith payoff, earns its place |
| ~724–732 | Extended Analogy: ship's hold, barrels, sacks, cranes, terminal, port authority | nautical — sustained/extended | acceptable as a sanctioned form; trim internally |

**Counting rule used:** the ⚠ Extended Analogy sidebar is counted as **one** instance rather than per-sentence. It is a ratified brand element whose defined purpose is long-form metaphor (`style-decisions.md`, LOCKED 2026-04-19), so scoring it per-image would penalize a structure the brand mandates. Its internal density is reported separately below so the author can recount on a different basis if they disagree.

### Excluded as branded structural terminology (Rule 1)

Not counted: 🧭 Soundings, ☆ Taking Your Bearings (×3), ★ Fixed Point (×3), ⚠ Navigational Hazards (×2), — Dead Reckoning, 🏆 Safe Harbor, ☀️ Zenith, 🗺️→🌊→🌅 Voyage Progress, "The Voyage Ahead", ⚓ Worth Securing (×4), 🪝 Snag (×3), 🔭 Closer Look (×3), 🪢 Mnemonic, Logbook Entry, Extended Analogy header — **43 marker instances** — plus **20 `[cross-bearing: …]`** references and the "Lodestar Ledgers" epigraph attribution.

### Excluded as functional language or idiom (Rule 4)

| Line (approx) | Passage | Why not counted |
|---|---|---|
| ~97 | "place it on a map in about ten seconds" | generic conceptual-map idiom, not a deliberate navigational figure |
| ~113 | "how practitioners actually navigate this ecosystem" | functional sense of *navigate* |
| ~176 | "A shipped kernel would have to be booted" | *ship* as software-delivery idiom |
| ~396 | "the node agent Kubernetes ships" (Figure 2-3 label) | same idiom; also diagram text |
| ~483 | 🪢 Mnemonic: "Build it, ship it, run it" | standard software idiom. Mild brand resonance, no flag |
| ~245, ~1035 | "a port number", `[registry[:port]/]` | technical term, zero metaphorical content |
| ~676, ~971 | "has no bearing on pull policy" / "no bearing on which specifications" | ordinary English idiom — but see note below |
| ~722 | Figure 2-6 note: "crates moving between incompatible carriers … 20th-century dockside" | author-facing production/commissioning apparatus, not reader prose |

> **Minor collision worth the author's eye:** "has no bearing on" appears twice (~676, ~971) inside answer explanations, in a chapter that also uses ☆ **Taking Your Bearings** three times as a section name. The idiom is innocent and neither instance reads as thematic, but if a light copy pass is happening anyway, "has no effect on" / "is irrelevant to" removes the flicker at zero cost.

## Overcooked passages

**§8, lines ~707–735 — ≈820 words carrying 4 of the chapter's 8 instances (local density ≈4.9 per 1000).**

Locally above band, which is defensible for a synthesis payoff section and consistent with how ☀️ Zenith is meant to land. Not a drift problem. There is, however, one genuine redundancy inside it:

- **Lines ~711 and ~726–728 tell the same story twice.** The §8 opening prose gives the intermodal-container history ("Wooden crates were fine boxes… Nobody at the crane has an opinion about what is inside"), and then the Extended Analogy re-tells it at ~600 words with the pre-standard hold, the barrels and sacks, and the crane designer. The second telling is better and does more work.
- **Recommendation — trim, don't cut.** Reduce line ~711 to its thesis (the industry standardized the *interface*, not the box) and let the Extended Analogy carry the historical scene-setting. That removes ~80–100 words of duplicated imagery, keeps all four metaphor instances, and tightens the run-up to the Zenith. No other passage in the chapter stacks metaphors densely enough to warrant trimming.

## Underseasoned passages

**Lines ~179–706 — ≈8,073 words (≈7,400 excluding tables, ASCII diagrams, and author-review comments) with zero overt thematic texture.** That is roughly **9× the 800-word flag threshold**, and it spans the majority of the chapter's teaching content: the remainder of §2, §3 (registries/tags/digests), ☆ Bearings #1, §4 (CRI), §5 (OCI), ☆ Bearings #2, §6 (pull policy), §7 (RuntimeClass), ☆ Bearings #3.

Lines ~736–1069 (Exam Alert, Practice Questions, Chapter Summary, The Voyage Ahead — ≈4,400 words) also carry none. **Not flagged:** that region is question bank and reference apparatus, where flat, unfigured prose is correct and metaphor would actively harm precision.

**Countervailing factor, stated so this isn't over-corrected.** The chapter does not *read* as texture-less, because the register is carried at the terminology layer instead of the metaphor layer: 43 branded-marker instances and 20 `[cross-bearing: …]` references are distributed evenly across exactly the stretch flagged above. A reader moving through §3–§7 meets Soundings, Bearings, Fixed Point, Navigational Hazards, Worth Securing, Snag, Closer Look, Mnemonic, Dead Reckoning and cross-bearings continuously. The brand voice is present; overt figures of speech are what's absent.

**Recommendation — at most two light touches, placed deliberately.**

1. **A section transition in the §4–§5 span.** The socket/interface material is where the crate conceit is most available and least forced — a single sentence tying the CRI socket to the standardized corner fitting would plant §8's payoff 300 lines earlier and make the Zenith read as recognition rather than as a new idea. The chapter already gestures at this ("It is a socket, and the socket is the product," ~389) in purely mechanical terms.
2. **Optionally one at the §6→§7 seam**, where the prose turns from structure to behavior.

**Do not add texture inside §6 or §7's rule statements.** Those sections carry the four conditional `imagePullPolicy` defaults and the RuntimeClass mechanism — the chapter's most precision-critical material, where the skill's "selectively, where it enhances engagement and sounds natural" guidance argues for leaving the prose flat. Two additions bring narrative-prose density to ≈1.3 per 1000 and close the longest gap without touching anything load-bearing.

**Also note:** the closing quote (~1069, *"Standardize the fitting, and you stop needing to know what's inside…"*) carries no nautical vocabulary at all. It works — "fitting" inherits the crate frame from §8 — but it is the one place a single word would restore the register at zero risk, if the author wants a third touch.

## Pirate-vocabulary check

Full lexical sweep of the raw file. **All clear — zero hits.**

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey | 0 | — |
| ye (as pronoun) | 0 | — |
| arr / avast | 0 | — |
| booty / plunder | 0 | — |
| scallywag / landlubber | 0 | — |
| swashbuckling / buccaneer | 0 | — |
| cutlass / grog | 0 | — |
| yo-ho / "shiver me" / "me hearties" | 0 | — |

No cliché nautical constructions either — the sweep found no "chart a course", "set sail", "smooth sailing", "navigate the waters", "weather the storm", "all hands", "uncharted", "North Star", or "guiding star". The one conceit the chapter does use (intermodal containerization) is historically load-bearing for the subject rather than ornamental: "container" in the Kubernetes sense descends from exactly this metaphor, so the chapter is explaining its own vocabulary rather than decorating it.
```

**Bottom line:** no drift, no caricature, no cliché — the failure mode here is the opposite one. The chapter is underseasoned at 0.6/1000 across all body prose (1.1/1000 counting narrative prose alone), with 7 of 8 instances confined to the frame and §8, and a ~7,400-word stretch from §2 through §7 carrying none. Two things to act on: trim the duplicated intermodal history at line ~711 in favour of the stronger Extended Analogy, and plant one crate/fitting touch in the §4–§5 span so §8's Zenith reads as recognition.

One process note worth flagging: the stage prompt received `[file not available: draft-voice.md]`. The voice stage writes back over `draft-v1.md` and preserves `draft-v1-prevoice.md`, so there is no `draft-voice.md` on disk — I audited `draft-v1.md` (timestamp matches the voice stage's completion). If other Stage 9+ diagnostics interpolate the same `draft-voice.md` path, they are all being handed an empty input and the orchestrator's path mapping needs a look.