`diagnostics/theming-density.md`:

```markdown
# Theming-Density Audit — Chapter 13

*Line numbers cite `.pipeline-state/ch-13/draft-v1.md` (1,533 lines). `draft-voice.md` does not exist at this stage.*

## Summary

- Total word count (body prose only, excluding code blocks and tables): **18,254**
- Overt nautical/celestial metaphors outside branded markers: **6**
- Density: **0.3 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Measurement method.** Raw file total is 20,704 words. Excluded: 1,351 words in pipe tables, 697 words in fenced blocks (671 content + 26 fence markers across 13 blocks), 402 words in HTML comments (`AUTHOR-REVIEW` notes and `FIGURE` anchors). Remainder = 18,254.

**The verdict is robust to counting convention.** The Extended Analogy at L815–823 is counted as one sustained unit; counting its seven nautical terms individually, and admitting all three borderline items below, gives at most 15 metaphors = **0.8 per 1000**. Still under the band floor. There is no reading of this chapter that puts it inside 1–3.

**To reach the band floor of 1.0** this chapter would need roughly 18 overt metaphors — twelve more than it has. See the recommendation under *Underseasoned passages*; hitting mid-band (~37) is not recommended and would overcook it.

## Catalog of metaphors

| Line | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 394 | "A log that nobody keeps is a passage nobody can reconstruct." | nautical — ship's log / sea passage | acceptable — keep. Genuine double meaning on *log*; lands the ephemerality argument in one clause. |
| 685 | "…it makes you the first thing thrown overboard, because the kubelet has no reason to believe you need anything." | nautical — jettison | acceptable — keep. Concrete, does real work: jettison order *is* eviction order. |
| 771 | "A compass that reads north in every direction is telling you about the compass." | navigational — instrument failure | acceptable — strongest in the chapter. Makes systemic observer-error concrete; not a cliché. |
| 815–823 | "`kubectl` is the harbormaster's ledger… `crictl` is the individual ship's own log, kept aboard, written by the crew… the officer who was supposed to send the report and did not." | nautical — sustained (7 terms) | acceptable — sanctioned `Extended Analogy` sidebar; the chapter's only sustained figure, and it earns the space because the three-layer disagreement is hard to hold otherwise. See register note below. |
| 945 | "You are debugging your instrument, not the water." | navigational — instrument vs. observed world | acceptable — keep. Tight, closes the paragraph, no ornament. |
| 1232 | "Instruments change; the way you fix a position does not." | navigational — taking a fix | acceptable — keep. Thesis line, and *fix a position* deliberately rhymes with the ★ Fixed Point two paragraphs later. Resonance, not collision. |

**Clichés found: none.** Grep across the full cliché set (`chart a course`, `set sail`, `smooth sailing`, `uncharted waters`, `all hands`, `weather the storm`, `even keel`, `steady as`, `adrift`, `batten`) returns zero. Every hit on `port`/`tack`/`mast`/`horizon` is substring noise (`report`, `stack`, `Mastered`, `HorizontalPodAutoscaler`).

**Overwrought passages: none.** No metaphor in this chapter is doing decorative work.

### Borderline — inspected, not counted

| Line | Passage | Why not counted |
|---|---|---|
| 295 | "…gets `IfNotPresent` by default and **rides out** the same registry outage without noticing." | Dead idiom. Nautical in origin, general English in use; not a deliberate figure (rule 4). |
| 647 | "…they are two **altitudes** of the same event." | General spatial metaphor for levels of abstraction. Not distinctly nautical/celestial. |
| 659 | "So an eviction **wave** usually means…" | Standard ops vocabulary (cf. *crime wave*). Functional, not figurative. |

**Marker-hygiene note (minor, not a density finding).** *Hazard* appears twice as ordinary prose in §6 — "That silence is the whole hazard" (L949-ish) and "There is a forward hazard too." Neither is a metaphor, but both sit within a few hundred words of ⚠ Navigational Hazards blocks and slightly dilute the marker's signal. Revision stage may prefer *trap* or *risk* in one of the two.

**Register note on L815–823.** The Extended Analogy is the one place the chapter commits to an era, and it commits to age-of-sail (harbormaster, vessel, crew, ship's log). Per `style-decisions.md` 2026-04-20, per-book era placement varies and the Communications Officer family's other book (CKA) is placed in the early-interstellar register. This is a register-consistency question for the author, not a density problem — the analogy itself is good. Confirm KCNA's placement in `illustrator-brief.md` before revision; if KCNA sits with CKA, the same analogy works verbatim with *dockmaster's manifest / the ship's own log / the signals officer*.

## Overcooked passages

**None.** No passage in this chapter stacks two or more overt metaphors.

The chapter's only cluster is §5, which carries two (L771 compass, L815–823 Extended Analogy). They are separated by the entire `crictl` explanation and the layer-stack figure — roughly 600 words and a section break in reading experience. That is spacing, not stacking. No trim recommended anywhere.

## Underseasoned passages

Four metaphor-free stretches, all far over the 800-word flag threshold:

| Range | Approx. prose words | Content |
|---|---|---|
| L1–393 | ~5,350 | Metadata, Attention Budget, 🧭 Soundings + answers, Why This Chapter Matters, What You'll Learn, **§1 entire**, **§2 entire**, §3 opening |
| L395–684 | ~3,180 | §3 remainder, Checkpoint 1 + answers, §4 opening through `CrashLoopBackOff` |
| L946–1231 | ~3,280 | §6 remainder, **§7 entire**, Checkpoint 3 + answers, §8 opening |
| L1233–1533 | ~3,180 | §8 close, Exam Alert, all 15 Practice Questions + answers, Chapter Summary, The Voyage Ahead |

**The chapter does not read as texture-less**, and this matters for how the finding should be acted on. Branded apparatus is dense: 39 marker/sidebar/margin-icon instances and 37 `cross-bearing` pointers. The reader meets brand furniture constantly. What is absent is *prose* texture — the voice never picks up the register between the markers, except in §5, §6 and §8.

**Where additions are warranted (three stretches):**

1. **Why This Chapter Matters (L100–127)** — the highest-attention passage in the chapter and completely bare. This is where the method-versus-glossary argument is made, and it is the natural home for the chapter's one big image. The material offers it: an experienced operator narrowing by elimination is doing exactly what a navigator does with successive bearings.
2. **§1's fixed order (L174–197)** — "Scope → phase → conditions → events → logs." The argument for why the order is not arbitrary is currently made purely mechanically. One figure would carry it.
3. **§2's `Pending` subsection (L237–263)** — a Pod held indefinitely because no node is feasible, with nothing quietly relaxing the constraints on its behalf, is the most evocative fact in the chapter and is currently rendered flat.

Secondary: **§7 (L979–1077)** — "nobody installed the component that would collect this" is a strong image going unused across ~2,000 words.

**Where additions are NOT warranted — do not sprinkle here.** The L1233–1533 stretch is assessment and reference apparatus: Exam Alert, fifteen graded questions with answer keys, and the Chapter Summary table. Clinical is correct in graded and reference text, and the same applies to the 🧭 Soundings answer key and the three checkpoint answer keys inside the earlier ranges. Their bareness is a deliberate register choice, not a defect. Flagging them here only so the revision stage does not "fix" them.

**Recommendation.** Eight to twelve targeted additions across the three named stretches lands the chapter at roughly 0.8–1.0 per 1000 — at or just under the band floor, and proportionate for a diagnostic chapter whose subject matter is procedural. Closing the remaining gap to mid-band would require metaphor in the graded material, which would cost more than it buys. Recorded as an author decision rather than absorbed silently.

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / maties | 0 | — |
| ye (as pronoun) | 0 | — |
| avast | 0 | — |
| arrr / aye | 0 | — |
| landlubber | 0 | — |
| scallywag | 0 | — |
| swashbuckling | 0 | — |
| booty / plunder | 0 | — |
| buccaneer | 0 | — |
| walk the plank | 0 | — |
| shiver me / me hearties | 0 | — |
| thee / thou | 0 | — |

Clean. No caricature register anywhere in the chapter.
```

**Headline:** 6 metaphors across 18,254 words = **0.3 per 1000**, against a 1–3 target — underseasoned, and robustly so (even the most generous count reaches only 0.8). Nothing is overcooked, no clichés, no pirate vocabulary; the six that exist are all good, and four of them are clustered in §5–§6 and §8. The gap is the first ~5,350 words (front matter through §2, the chapter's largest teaching section) plus §7. I've flagged the assessment apparatus as deliberately clinical so the revision stage doesn't add texture to graded questions, and raised one register question: the Extended Analogy at L815–823 is the only place the chapter picks an era, and it picks age-of-sail, which may not match KCNA's placement alongside CKA.