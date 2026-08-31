Measurements complete. Here is the Stage 9 deliverable.

**Note on delivery:** `Write` is gated in this session (as it is in the pipeline runner, where it is deliberately removed from `--allowed-tools`), so the artifact is emitted to stdout below for the orchestrator to capture to `diagnostics/theming-density.md`. The existing file at that path is the draft-v1 audit and should be overwritten.

```markdown
# Theming-Density Audit — Chapter 8

*Source: `../Book-KCNA/.pipeline-state/ch-08/draft-v2.md` (1,224 lines). `draft-voice.md` does not exist at this stage; all line numbers cite draft-v2.md.*

## Summary

- Total word count (body prose only, excluding code blocks and tables): **16,829**
- Overt nautical/celestial metaphors outside branded markers: **10**
- Density: **0.6 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Secondary density, narrative prose only.** The chapter carries **7,362 words** of assessment apparatus (Soundings 895 · Bearings #1 940 · Bearings #2 966 · Bearings #3 1,055 · Exam Alert 224 · Practice Questions + Answers 3,282) — deliberately un-themed exam register where theming would be actively wrong. Against narrative prose alone (**9,467 words**) the density is **1.1 per 1000**, which is *just inside* the band at its bottom edge.

**This is a change from draft-v1, and it matters.** The draft-v1 audit reported that both denominators landed the chapter on the same side of the line (0.57 / 0.96). Draft-v2 no longer does: the verdict now depends on which denominator you accept. Nothing thematic was added — the revision was fact-accuracy work, and the metaphor inventory is unchanged. The narrative denominator moved because ~300 words of unsourceable prose were cut from §5, §7 and the closing teaser, concentrating the same 10 metaphors into slightly less prose.

**The finding in one sentence:** nothing here is overcooked, nothing is cliché, and all 10 metaphors are well-earned — but they cluster at the chapter's two ends, leaving a **3,387-word span from §4's Figure 8.4 caption to §7's ⚓ callout with zero thematic texture**, which is the third of the chapter a reader spends most of their time in.

### Counting method

An **instance** is one deliberate deployment of a figure at one location. A figure sustained across contiguous sentences counts **once**: the Extended Analogy at L282–286 is one instance despite running ~230 words across nine maritime nouns, because counting it as nine would misrepresent the texture the reader actually experiences. Recurrences of the same figure separated by intervening material count separately (the "watch" figure at L1, L42, L108 and L1207 is four instances, not one).

Excluded from the count, per Rule 1 and Rule 4:
- **Branded markers and locked brand furniture:** 🧭 Soundings, ☆ Taking Your Bearings, ★ Fixed Point, ⚠ Navigational Hazards, — Dead Reckoning, 🏆 Safe Harbor, ☀️ Zenith, *The Voyage Ahead*, and the 20 `*[cross-bearing: …]*` pointers. These are structural terminology.
- **Technical Kubernetes vocabulary:** `cordon`, `drain`, "the scheduler's **watch**" (L1040, L1127), "**port** 443" (L241), "load-**bearing** sentence" (L316). Vocabulary overlap, not figure of speech.

If the two "logbook" headings (L225, L302) are folded into a single figure — the fold the draft-v1 audit used — the count is 9 and the densities are 0.5 / 1.0. **The verdict is underseasoned under either rule.**

## Catalog of metaphors

| Line | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 1 | "Chapter 8: **Standing the Watch**" | nautical — watchkeeping | acceptable — establishes the chapter's controlling figure, and the figure is genuinely apt (a watch is a *stretch of responsibility*, which is exactly the posture shift §"Why This Chapter Matters" describes) |
| 42–43 | "A watch is not a task you finish. It is a stretch of time during which **the ship is your responsibility, and the log records what you did about it.**" | nautical — watchkeeping + logkeeping | earns its place — the epigraph does double duty, seeding both the watch figure and the logbook figure that §2 collects at L302 |
| 108 | "**On watch,** you think in three questions: what can I take out of service safely, what can I stop other people doing, and what can I not get back." | nautical — watchkeeping | earns its place — the metaphor is load-bearing, not decorative; it organises the chapter's three-part spine in one clause |
| 225 | "§2 — Three Gates and **a Logbook**" | nautical — logkeeping | acceptable — pays off the epigraph and gives auditing a brand-register name without inventing a marker |
| 282–286 | "Think of a working commercial **harbour** rather than a locked building. A **vessel** arriving is met first by a **pilot boat** … the **harbourmaster** consults the **berth** allocations … the customs officer … may find something prohibited and turn the whole vessel around" | nautical — harbour/pilotage (sustained, ~230 words) | **strongest instance in the chapter** — see "Overcooked passages" for why this is not overcooked |
| 302 | "### And **a logbook**" | nautical — logkeeping | acceptable — recurrence of the L225 figure; the only thematic touch in a 77-line stretch, so it is doing work |
| 484 | "The three Pods **aboard** the cordoned node are still running" | nautical — stowage/complement | acceptable — light touch, and the ship-as-node mapping is the one the ⚠ Navigational Hazards at L486 depends on. (The same figure appears at L467 inside a ★ Fixed Point; excluded per Rule 1, counted once here.) |
| 785 | "A snapshot that lives only on the machines it exists to protect you against losing is not a backup. It is a copy that goes down with the original — **the maritime word for which is *ballast*, not *lifeboat*.**" | nautical — stowage/safety | **best-executed instance** — signposts itself ("the maritime word for which"), so the register never has to be guessed at, and the ballast/lifeboat opposition carries real information rather than atmosphere |
| 1207 | "Part II is complete. **Ship, cargo, and company:** the container, the cluster, the objects, the Pod, the controllers, the placement, and now the watch." | nautical — vessel/complement | earns its place — maps seven chapters onto three nautical nouns and closes the watch figure opened at L1 |
| 1225 | "**The chart tells you where the harbours are. It does not tell you how the water moves between them — and the water is what you are actually sailing on.**" | nautical — chartwork/pilotage | earns its place — the closing quote is a real argument (Part II = static placement, Part III = networking) in figurative dress, not ornament |

### Category distribution

| Category | Instances |
|---|---|
| Nautical | **10** |
| Celestial | **0** |

**Zero celestial metaphors outside branded markers.** The only celestial vocabulary anywhere in the chapter is the ☀️ Zenith marker at L888 and its figure anchor at L890; the word "horizon" in that same line sits inside the marker. `star`, `north star`, `lodestar`, `constellation`, `meridian`, `sextant` and `sun`/`moon`/`sky` return no non-marker hits — `Lodestar` appears once, at L43, as the publisher attribution on the epigraph.

This is not a defect against any locked decision (the ledger's 2026-04-18 entry sets one combined budget for both categories, not a ratio). It is worth recording because the chapter is a Communications Officer title and the brand world spans maritime through interstellar registers: a purely age-of-sail palette is a choice, and right now it is an unexamined one rather than a made one.

## Overcooked passages

**None.** No passage in the chapter stacks multiple distinct metaphors, and no metaphor is cliché.

Two passages were checked specifically because they are the chapter's densest and would be the obvious candidates:

- **L282–286, the Extended Analogy (~230 words, nine maritime nouns).** Not overcooked. It is **one** sustained figure, not a stack — every noun (pilot boat, harbourmaster, berth, crate, cargo, customs officer) belongs to a single coherent scene, and each maps to exactly one element of the three-gate model. It is also inside an `Extended Analogy` sidebar, the brand's locked container for exactly this (style-decisions, 2026-04-19), so the reader is told in advance that a long metaphor is coming and can skip it. The test that matters — does removing the metaphor cost the reader anything? — it passes: the customs officer is the only place in the chapter where admission's *third option* (proceed, altered) is given a concrete image, and that is the section's whole pedagogical point.

- **L1207 + L1225, the closing 20 lines.** Two metaphors in 412 words is **4.9 per 1000**, well above band *locally*. No action recommended. Chapter-closing furniture (Safe Harbor, The Voyage Ahead, the closing quote) is where brand voice is supposed to concentrate, and the two instances are 18 lines apart with un-themed prose between them. Flagged here only so the local spike is on the record and is not mistaken for drift if it is measured in isolation.

## Underseasoned passages

Four gaps exceed the 800-word flag threshold. Listed worst-first.

| Gap | Span | Body-prose words | Of which narrative | Assessment |
|---|---|---|---|---|
| **B** | L484 (Fig 8.4 caption) → L785 (ballast) — §4 back half, all §5, Bearings #2, all §6, §7 opening | 4,353 | **3,387** | **worst stretch in the chapter** |
| **C** | L785 → L1207 — §7 close, Bearings #3, §8, Exam Alert, Practice Questions, Summary | 5,795 | ~1,040 | acceptable — 82% is assessment apparatus, where texture is correctly absent |
| **A** | L302 → L484 — §2 close, all §3, Bearings #1, §4 opening | 2,277 | ~1,337 | flag |
| **§1** | L108 → L225 — Why-This-Chapter-Matters remainder, What You'll Learn, all of §1 | 1,427 | 1,427 | flag |

### Gap B is the finding

Within Gap B the reader crosses two contiguous narrative runs with no thematic texture at all:

- **L485–L603 (~1,747 words)** — §4's node conditions, heartbeats, the node controller as a control loop, Capacity/Allocatable, and the whole of §5.
- **L665–L784 (~1,640 words)** — the whole of §6 (version skew) and §7's opening.

Only Bearings #2 separates them, and Bearings #2 is un-themed by design. So the reader's experienced stretch is a single ~3,400-word desert covering **§5, §6 and the front of §7** — and §6 is, by the chapter's own account (L38), "the densest pure-recall block in this book."

That is the wrong place to have no voice. The skill's guidance is that theming is used *where it enhances engagement*; a dense pure-recall table section is precisely where engagement needs help most, and it currently gets none.

### Recommendation: two additions, not five

Bringing the body-prose density into band would need ~7 more instances, which would be over-correction and would risk the caricature the brand bans. Recommend **two**, both placed to break the longest run rather than to hit a number:

1. **§6, around the derivation at L667–L673** ("Nothing in the cluster may be newer than the API server it talks to"). One figure, one sentence. The material is already about a *fleet* whose parts must stay in step — the metaphor is sitting there unused. This is the highest-value single placement in the chapter: it puts texture at the exact point the reader is being asked to memorise five rows.
2. **§5, in "What ownership actually means" (L580–L592)** — the section is *about* custody and responsibility, which is the watch figure's native territory, and it currently reaches for a calendar instead. Note that the ⚓ Logbook Entry at L594 already carries the section's best writing without any nautical register at all, so the addition should complement it rather than compete.

Both additions land inside Gap B and would split it into three runs of roughly 900–1,400 words, none of which trips the 800-word flag as a *narrative* stretch. Resulting density: 12 / 16,829 = **0.7 per 1000** on body prose, 12 / 9,467 = **1.3 per 1000** on narrative prose — comfortably inside band on the narrative denominator and still conservatively short of the caricature line.

**Do not** add texture to Bearings #1/#2/#3, the Practice Questions, the Exam Alert, or the Chapter Summary. Those account for 7,362 of the chapter's 16,829 words and are correctly un-themed; theming them would be the actual drift risk here.

### One passage that is doing this correctly already

L1211–L1223, "The Voyage Ahead," runs ~250 words of genuinely un-themed prose under a branded heading and then lands the closing quote. That is the right shape: the brand furniture carries the register, the argument carries itself. Cited as the model for the two additions above.

## Pirate-vocabulary check

Structural linter catches these too; verified independently against draft-v2.

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / maties | 0 | — |
| ye (as pronoun) | 0 | — |
| arr / avast | 0 | — |
| scallywag / landlubber | 0 | — |
| booty / plunder | 0 | — |
| swashbuckling / buccaneer | 0 | — |
| yo-ho / shiver me / me hearties | 0 | — |
| walk the plank / jolly roger | 0 | — |

**Clean.** No pirate-caricature vocabulary of any kind.

### Cliché sweep (Rule 2)

| Phrase | Occurrences | Action |
|---|---|---|
| chart a course / charting a course | 0 | — |
| set sail / smooth sailing / sail through | 0 | — |
| weather the storm / stormy / tempest | 0 | — |
| uncharted waters / choppy waters / rough seas | 0 | — |
| rising tide / all hands / batten down | 0 | — |
| tip of the iceberg / full steam / even keel | 0 | — |
| drop anchor / anchor yourself | 0 | — |
| north star / guiding star / beacon in the | 0 | — |

**Clean.** One near-miss worth naming so it is not flagged in a later pass: **L1225 uses "chart" as a noun** — *"The chart tells you where the harbours are"* — which is the concrete instrument, not the dead idiom "chart a course." It passes. `Lodestar` at L43 is the publisher attribution, not a metaphor.

---

## Verdict

**Underseasoned**, at 0.6 per 1000 on body prose (1.1 on narrative prose, at the band's bottom edge).

Quality of what is present: **high**. Ten instances, zero clichés, zero pirate vocabulary, zero overcooking, one genuinely excellent self-signposting metaphor (L785) and one well-built sustained analogy (L282–286). This chapter's theming problem is distribution, not craft — the metaphors sit at the two ends and abandon the middle third, which is also the chapter's densest and least forgiving material.

**Recommended action:** two additions, §6 and §5, per the placements above. No removals. No rewrites.
```

**Three things worth surfacing from the run:**

- The verdict flipped denominators since draft-v1. On narrative prose alone the chapter is now at 1.1/1000 — technically *inside* band — because the fact-accuracy revision cut ~300 words of prose without touching a single metaphor. On body prose it remains clearly underseasoned at 0.6. I reported both rather than picking the flattering one.
- The chapter is **100% nautical, 0% celestial** outside branded markers. Not a contract violation, but for a Communications Officer title in a brand world that spans age-of-sail through interstellar, that looks like an unmade decision rather than a made one.
- The actionable defect is one **3,387-word span** covering §5, §6 and §7's opening with zero texture — and §6 is the chapter's own self-declared densest recall block. Two placed additions fix it; adding seven to hit the band arithmetically would push toward the caricature the contract bans.