```markdown
# Theming-Density Audit — Chapter 8

*Source: `../Book-KCNA/.pipeline-state/ch-08/draft-v1.md` (1,132 lines). `draft-voice.md` does not exist at this stage; all line numbers cite draft-v1.md.*

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~15,760**
- Overt nautical/celestial metaphors outside branded markers: **9**
- Density: **0.57 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Secondary density, narrative prose only:** the chapter carries ~6,420 words of assessment apparatus (Soundings 814 · Bearings #1 743 · #2 827 · #3 985 · Exam Alert ~230 · Practice Questions 2,817), which is deliberately un-themed exam register. Against narrative prose alone (~9,340 words) the density is **0.96 per 1000** — still below band, but only marginally. Both denominators land the chapter on the same side of the line, so the verdict does not depend on which one you prefer.

**The finding in one sentence:** nothing in this chapter is overcooked, nothing is cliché, and the nine metaphors present are all well-earned — but they are distributed into the first 45% of the chapter and the last 20 lines, leaving ~9,300 words in between with zero thematic texture.

### Counting method

An "instance" is one deliberate figure of speech, not one nautical noun. The Extended Analogy at lines 265–269 is counted **once** despite running ~230 words and using nine maritime nouns; counting it as nine would misrepresent the texture the reader experiences. Raw token counts for the chapter's five load-bearing nautical nouns (`watch` / `ship` / `harbour` / `aboard` / `cargo`) total 15 occurrences, of which 6 are inside branded markers or are technical Kubernetes vocabulary (`the scheduler's watch`, l.970).

Word-count derivation: 18,105 raw words − 1,438 (86 markdown table rows) − 611 (13 HTML comment lines: 6 FIGURE anchors, 7 AUTHOR-REVIEW blocks) − ~300 (6 fenced ASCII diagram blocks, 67 content lines) = ~15,760.

---

## Catalog of metaphors

| Line | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 1 | "Standing the Watch" (chapter title) | nautical — watchkeeping | acceptable — the chapter's subject genuinely *is* watchkeeping duty; the title sets a motif the chapter then pays off at l.1116 |
| 42 | "A watch is not a task you finish. It is a stretch of time during which the ship is your responsibility, and the log records what you did about it." | nautical — watchkeeping / logbook | acceptable — house epigraph, sustained figure, does definitional work rather than decoration |
| 104 | "practitioners on watch think in terms of what they can take out of service safely" | nautical — watchkeeping | acceptable — the only place the title's conceit enters body prose; one use, load-bearing |
| 216, 285 | §2 title "Three Gates and a Logbook"; subheading "And a logbook" | nautical — logbook | acceptable — the section-title metaphor names the auditing material, which is the one thing in §2 with no other handle on it |
| 265–269 | Extended Analogy: harbour, vessel, pilot boat, harbourmaster, berth allocations, cargo, customs officer, crates, dock | nautical — harbour operations | acceptable, and the strongest metaphor in the chapter — it is the only place the mutate-vs-reject distinction gets a concrete image, and it sits in the ratified `Extended Analogy` sidebar, which is precisely the sanctioned container for long-form metaphor |
| 436 | "`cordon` stops arrivals and touches nothing already aboard. `drain` clears what is aboard." | nautical — "aboard" for on-node | acceptable — inside a Fixed Point, but the figure itself is prose; compresses the chapter's headline distinction into one preposition |
| 453 | "The three Pods aboard the cordoned node are still running" | nautical — "aboard" for on-node | acceptable — second use of the l.436 conceit, consistent rather than repetitive |
| 1116 | "Part II is complete. Ship, cargo, and company: the container, the cluster, the objects, the Pod, the controllers, the placement, and now the watch." | nautical — ship's inventory | acceptable — closes the title's motif and summarises Part II's arc in one figure; see stacking note below |
| 1132 | "The chart tells you where the harbours are. It does not tell you how the water moves between them — and the water is what you are actually sailing on." | nautical — chart / water | acceptable — "chart" and "sailing" are stock furniture, but the second clause does real forward-pointing work (static topology vs. the networking medium of Part III), which is what redeems it from cliché |

**Celestial metaphors: zero.** No stars, North Star, lodestar, constellation, zenith, meridian, sextant, or almanac outside branded markers. `☀️ Zenith` (l.822) and `— Dead Reckoning` (l.638) are structural terminology and excluded per Rule 1.

### Borderline — checked and not counted

| Line | Passage | Why not counted |
|---|---|---|
| 674 | "run one `kubectl` against a fleet of clusters" | Rule 4 — "fleet of X" is standard operations vocabulary, a dead metaphor with no figurative intent |
| 457 | "A cordon is a rope across a doorway" | Not nautical — this is a crowd-control / venue image, and it is doing functional explanation of the actual `cordon` command |
| 970 | "the scheduler's watch on unscheduled Pods" | Rule 4 — `watch` is the Kubernetes API primitive, vocabulary overlap only |
| 228, 1014 | "secure HTTPS port, typically 443"; "which port does it listen on" | Rule 4 — technical `port`, no maritime sense in play |
| 299 | "That is the load-bearing sentence" | Architectural dead metaphor, not nautical/celestial — outside this audit's budget |
| 547 | `Logbook Entry` sidebar (managed vs. self-hosted) | Branded sidebar type per Rule 1; its ~200 words of content contain no nautical figure at all |

---

## Overcooked passages

**None requiring a trim.**

One mild stacking note, recorded rather than actioned:

- **Lines 1110–1132 (chapter close, ~300 words).** Four thematic signals land in quick succession: the `🏆 Safe Harbor` marker (branded), "Ship, cargo, and company… and now the watch" (l.1116), the `The Voyage Ahead` heading (branded), and the closing quote's chart/harbours/water/sailing (l.1132). Two of the four are branded markers already carrying maritime weight, so the two prose metaphors land on top of them.

  This is the chapter's densest thematic stretch by a wide margin and it is still not overcooked — closes are the conventional place for a motif payoff, and both figures are doing work (l.1116 summarises Part II; l.1132 sets up Part III). If anything here were ever cut, l.1116 is the more expendable of the two, because `🏆 Safe Harbor` sitting directly above it already signals arrival. **Recommendation: leave both.** Flagged only so the retro knows this stretch was looked at deliberately.

The Extended Analogy at 265–269 is dense by design and is explicitly what the `Extended Analogy` sidebar exists for (`style-decisions.md` 2026-04-19: "long-form metaphor"). It is not a stacking violation. Its real significance for this audit is that it accounts for a large share of the chapter's total maritime word volume in a single 5-line block — which is what makes the distribution lumpy.

---

## Underseasoned passages

Two gaps exceed the 800-word threshold. The second is the chapter's substantive problem.

**Gap 1 — lines 286–435, ~2,100 words prose.** §2's close, all of §3 (ResourceQuota / LimitRange), and Bearings #1. Zero thematic texture. Minor on its own; noted because it immediately follows the chapter's richest passage, so the drop-off is abrupt.

**Gap 2 — lines 454–1115, ~9,300 words prose. This is the finding.** From Figure 8.4's caption (l.453) to the Safe Harbor close (l.1116) there is not one overt nautical or celestial metaphor. That stretch contains:

- §4's back half — node conditions, heartbeats, the node controller, Capacity/Allocatable
- §5 — Who Owns the Control Plane, including its `Logbook Entry` sidebar
- §6 — Versions That Are Allowed to Disagree (the chapter's densest section)
- §7 — The One Backup That Matters
- §8 — Rules, or Consequences (the synthesis section, including the `☀️ Zenith`)
- Bearings #2 and #3, Exam Alert, Practice Questions, Chapter Summary

Discounting the assessment apparatus inside that span (~4,860 words of Bearings/Exam Alert/Practice Questions, which are correctly un-themed), **~4,440 words of continuous narrative prose carry no thematic texture whatsoever.** That covers four consecutive body sections, including the synthesis section that is supposed to be the chapter's emotional payoff.

The chapter does not read as brand-less, because the branded markers keep firing throughout and they carry maritime weight on their own. But per Rule 1 those are structural furniture, not theming, and stripping them out reveals a long dry middle. The reader who reaches §8's Zenith has not seen a figure of speech in roughly forty minutes of reading.

**Candidate anchor points, if the revision wants to close the gap** (three to five light touches would bring the narrative-prose density to ~1.2–1.5/1000 without touching anything already in place):

- **§4, l.483–491** — heartbeats and the node controller. A watch-relief or roll-call figure would extend the title's motif into the section where it is most literally apt, and §4 is the only body section that already has the "aboard" conceit to build on.
- **§5, l.539–543** — "What ownership actually means." The managed/self-hosted split is the chapter's clearest owner-of-the-vessel question and currently has no figure at all.
- **§6, l.668–680** — the `kubectl` exception. The "outside the cluster, not a component inside it" distinction is exactly the kind of insider/outsider point a maritime figure handles well.
- **§7, l.716–730** — the etcd snapshot as both recovery and liability. The strongest available slot in the chapter: a single figure here would land on the one passage explicitly written to be *felt* rather than filed.
- **§8, l.822 vicinity** — the Zenith. Currently the synthesis moment is delivered in flat architectural register ("one door, and controllers behind it"), which is clear and correct but gives the chapter's peak no thematic lift.

---

## Pirate-vocabulary check

Structural linter catches these too; verified independently against draft-v1.md, case-insensitive, word-boundary anchored.

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / mateys | 0 | — |
| ye (as pronoun) | 0 | — |
| yer | 0 | — |
| arr / arrr / avast | 0 | — |
| aye | 0 | — |
| belay | 0 | — |
| landlubber / lubber | 0 | — |
| scallywag | 0 | — |
| buccaneer / pirate(s) | 0 | — |
| booty / plunder / doubloon / treasure | 0 | — |
| swashbuckling / swashbuckler | 0 | — |
| cutlass / galleon | 0 | — |
| grog / seadog / hearties / cap'n | 0 | — |
| marooned / walk the plank / jolly roger | 0 | — |
| shiver me timbers / yo-ho / parrot | 0 | — |

**Clean.** Zero caricature vocabulary. The register throughout is working-harbour and watchkeeping — commercial, professional, and dignified — which is exactly the "seasoned navigator, not a pirate caricature" target.

Cliché check (Rule 2) is also clean: **zero** instances of "chart a course," "set sail," "smooth sailing," "weather the storm," "all hands," "uncharted waters," "steady as she goes," or "navigate the tempest." The chapter's one use of `chart` (l.1132) is a literal instrument doing a real conceptual job, not the stock verb phrase.

---

## Recommendation

**Underseasoned — add, do not trim.** Every existing metaphor earns its place; none should be touched. The gap is distributional: the chapter front-loads its theming into the title, epigraph, §1–§2, and one Extended Analogy, then runs ~9,300 words without texture before a two-figure close.

Three to five light touches placed in §4–§8 (anchors listed above) would bring the chapter to ~1.2–1.5 per 1000 on the narrative-prose basis and into band, and would give the synthesis section a thematic register proportional to its function. No passage requires a reduction.

---

## Observation for the per-book retro — out of band

Flagged as a theming observation, not a finding, and outside this audit's remit to resolve:

The chapter's maritime register is **age-of-sail** throughout — harbour, pilot boat, harbourmaster, berth allocations, customs officer, crates, watch, log. Under the brand-world expansion (`style-decisions.md`, 2026-04-20) per-book era placement varies, and CKA — the other Communications Officer book — is placed at early interstellar. `illustrator-brief.md` records no era placement for KCNA (grep: no match). If KCNA is intended to sit alongside CKA in the interstellar register, the harbour analogy at 265–269 and the closing quote at 1132 are the two passages that would need re-registering, and both would survive the move intact (a docking authority and a chart of transit lanes are era-portable). Recommend the retro settle KCNA's era placement before Chapter 9, since Part III's networking material will want the same vocabulary.
```