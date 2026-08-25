The Write tool is blocked here — which is expected: per `CLAUDE.md`, `Write` was deliberately removed from the executor's `--allowed-tools` so stage output flows through stdout for the orchestrator to capture atomically. Emitting the artifact as stage output below.

**Method notes:** audited `.pipeline-state/ch-10/draft-v1.md` (1,401 lines). Prose word count derived as `wc -w` (18,062) minus fenced code blocks (791), table rows (1,179), and HTML comment lines (234) = **15,858**.

---

```markdown
# Theming-Density Audit — Chapter 10

Audited file: `.pipeline-state/ch-10/draft-v1.md` (1,401 lines). `draft-voice.md` does not exist at
this stage; all line references below are against `draft-v1.md`.

## Summary

- Total word count (body prose only, excluding code blocks and tables): **15,858**
- Overt nautical/celestial metaphors outside branded markers: **13** (across 10 passages)
- Density: **0.8 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Counting method (so this is reproducible).** Raw `wc -w` on the file = 18,062. Excluded: fenced
code blocks including their fence lines (13 blocks, 791 words); markdown table rows, i.e. lines
beginning `|` (68 lines, 1,179 words); HTML comment lines, i.e. FIGURE anchors and AUTHOR-REVIEW
notes (7 lines, 234 words). 18,062 − 791 − 1,179 − 234 = 15,858. Inline `[source: …]` tags were
*not* excluded; they add roughly 2% and do not move the verdict.

**Counting unit.** One count per distinct metaphorical figure, not per sentence and not per nautical
noun. "Three sightings of the same light … a landmark" is one continuous image and counts once;
"one fires a flare; the other is an uncharted rock" is an explicit two-part contrast and counts
twice.

**Sensitivity.** Two of the thirteen are soft (`~158` "the wall", `~789` "get under way" — see
verdicts). Dropping both gives 11 figures and 0.69 per 1000. The chapter is below band on either
count, so the verdict does not turn on those judgement calls.

**Celestial specifically: zero.** No stars, no North Star, no lodestar-as-figure, no constellation,
no sun/zenith imagery anywhere in body prose outside branded markers. The entire budget is spent on
the nautical half of the register. Not a defect — rule 3 puts both in one budget — but worth noting,
because the KCNA book's era placement is early-interstellar and the celestial register is the one
that travels best there.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~146 | "Keep this boundary on your **chart**." | nautical — chart / navigation | acceptable — light, one beat, does real work (the layer boundary is load-bearing through §6) |
| ~158 | "North-south goes through **the wall**; east-west stays inside it." | nautical — harbour wall (soft) | borderline — reads as generic fortification; only becomes nautical retroactively via ~168. Counted, but carries almost no thematic charge |
| ~168 | "The addresses Chapter 9 gave you work beautifully **inside the harbour wall**, and mean nothing beyond it." | nautical — harbour | acceptable — earns its place as §1's closing payoff; the figure *is* the argument |
| ~362 | "**DNS is the chart that gets you into the harbour.**" | nautical — chart / harbour | trim — weaker half of a stacked pair, and re-spends the "chart" figure already used at ~146. See Overcooked |
| ~362 | "Virtual hosting is **the harbourmaster deciding which berth you take** once you are inside it." | nautical — harbour personnel / berthing | acceptable, and the half to keep — "sorting traffic that has already arrived" maps to a harbourmaster precisely |
| ~423 | "**Three sightings of the same light**, and you stop calling it a coincidence and start calling it **a landmark**." | nautical — navigation fix | acceptable — one continuous image; carries the "three instances → a rule" move that §8 later cashes |
| ~454 | "**Same chart, different pilot.**" | nautical — chart / pilotage | acceptable — terse, fresh, exactly sized to a 🪝 Snag. But third use of "chart" (see repetition note) |
| ~569 | "**A light has been hung on the new channel**; the old one has not been closed." | nautical — navigation light / channel marking | acceptable — strongest figure in the chapter; it encodes `frozen ≠ deprecated` structurally, not decoratively. Do not touch |
| ~789 | "One piece of housekeeping before we **get under way**" | nautical — dead idiom | borderline — ordinary English, not a deliberate figure. Counted for completeness; contributes no texture |
| ~987 | "One failure **fires a flare**;" | nautical — distress signal | acceptable — half of a load-bearing contrast |
| ~987 | "the other is **an uncharted rock**, and nothing on the surface says it is there." | nautical — navigational hazard | acceptable — the chapter's central asymmetry (loud failure vs silent failure) made concrete. Best-earned figure after ~569 |
| ~1123 | "**A chart drawn perfectly is still a chart.**" | nautical — chart | acceptable in function; but this is the fourth and fifth "chart" (see repetition note) |
| ~1123 | "Somebody has to **stand the watch**." | nautical — watchkeeping | acceptable — clean closing beat, and it is the one figure that names the *component* rather than the object |

### Excluded as branded markers (not counted)

Per rule 1. Listed so a later pass does not mistake these for texture the chapter already has:

🧭 Soundings · ☆ Taking Your Bearings ×3 · ★ Fixed Point (×10) · ⚠ Navigational Hazards ×3 ·
— Dead Reckoning ×1 · 🏆 Safe Harbor · ☀️ Zenith · 🗺️→🌊→🌅 Voyage Progress and its
"*Part III: passage*" gloss · `## The Voyage Ahead` · ⚓ Worth Securing ×4 · 🪝 Snag ×4 ·
🔭 Closer Look ×2 · 🪢 Mnemonic ×3 · `*[cross-bearing: …]*` ×31 · the epigraph attribution
"— Lodestar Ledgers".

The prose *inside* a marker block is still prose and was audited normally — three of the thirteen
counted figures (~362, ~423, ~454) live inside ⚠/⚓/🪝 blocks.

## Overcooked passages

**One site, and only one.**

**~362 — the ⚠ Navigational Hazards block closing §2's DNS-vs-virtual-hosting distinction.**

> "…DNS is the chart that gets you into the harbour. Virtual hosting is the harbourmaster deciding
> which berth you take once you are inside it."

Four nautical nouns — *chart*, *harbour*, *harbourmaster*, *berth* — in two consecutive sentences,
inside a block already carrying branded nautical framing (⚠ Navigational Hazards). This is the only
place in the chapter where the register announces itself rather than working quietly.

**Recommend trimming to the essential one.** Cut the *chart/harbour* sentence and keep the
*harbourmaster/berth* sentence. Reasons: (a) the harbourmaster figure maps onto the actual mechanism
— sorting arrivals that are already inside — where "the chart that gets you in" is only restating
"DNS resolves first," which the preceding two paragraphs already said in plain prose; (b) "chart" is
the chapter's most over-used figure and this is its cheapest use. Trimming here costs one of the
thirteen figures and takes density to 0.76 — but the chapter's problem is distribution, not volume,
and the replacement belongs in §5–§7, not here.

### Repetition note (not density, but adjacent)

**"Chart" carries five of the thirteen figures** — ~146, ~362, ~454, and twice at ~1123. Within band
or not, one noun doing 38% of the thematic work reads as a tic rather than a register. Vary at least
one. ~454 ("same chart, different pilot") and ~1123 ("a chart drawn perfectly is still a chart") are
both good enough to keep; ~146 and ~362 are the candidates.

## Underseasoned passages

Six stretches over 800 prose words carry zero thematic texture. Word counts are prose-only, computed
the same way as the summary figure.

| Lines | Content | Prose words | Note |
|---|---|---|---|
| 1–145 | Front matter, Attention Budget, 🧭 Soundings (8 Q + answers + rubric), Why This Chapter Matters, What You'll Learn, §1 opening | 1,857 | Includes the chapter's thesis paragraph — *"The question is not did I write the object correctly. It is is anything watching this object."* — which is the rhetorical high point of the chapter and is entirely bare |
| 456–568 | Bearings #1 answers, Checkpoint, §4 through the freeze/deprecation split | 1,395 | Defensible — §4 is a word-level precision section where figures would blur the distinction |
| 570–788 | §5 Gateway API (roles, resources, cardinality, request flow) + Bearings #2 | 1,972 | Longest section of the API arc, zero figures |
| 790–986 | §6 NetworkPolicy through the isolation model, additivity, both-ends rule, default-deny construction | 2,281 | The chapter's highest-attention section (14 min, High) and the one section explicitly built to overturn a reader instinct. No thematic support at all |
| 988–1122 | §7 remainder (out-of-scope list, reasoning-to-the-dependency) + Bearings #3 + §8 opening | 2,112 | — |
| 1124–1401 | Exam Alert, Practice Questions (17 + answers), Chapter Summary, The Voyage Ahead | 3,150 | **Correct as-is.** Reference apparatus; bare is the right call. Do not add texture here |

**The finding, stated plainly: this chapter is not texture-less, it is texture-lopsided.** Ten
passages carry figures and several are genuinely good — ~569 and ~987 are exemplar-grade, encoding
the distinction rather than decorating it. But every one of them sits in §1–§4 or §8. The stretch
from L570 to L1122 — §5, §6, §7, two checkpoints, roughly **6,365 prose words, 40% of the
chapter** — contains exactly one figure, and it is the dead idiom "get under way."

That stretch is also where the chapter is hardest. §6 is flagged High attention, opens the second
session, and its stated job is to take away a firewall instinct the reader has held for a decade.
It is precisely where a figure buys the most and where the draft supplies none.

**Recommended additions: 4–8 figures, concentrated in §5–§7.** Reaching mid-band (2.0/1000) from
0.8 would take ~19 more; that is not the recommendation and would overcook the chapter. Getting into
band at all takes 3 more; 4–8 gets to ~1.1–1.3/1000 with the distribution repaired. Ranked slots:

1. **~866, §6 — the "collect the debt from Soundings question 4" paragraph.** The single best
   unclaimed slot in the chapter. "A Pod starts fully open in both directions, and becomes
   restricted only because some policy went looking for it and found it" is a reversal the reader
   is actively resisting, and it is stated in bare prose. A figure here earns its keep immediately.
2. **~920, §6 — the both-ends rule.** "Both the source's egress and the destination's ingress"
   is the rule the section says costs practitioners the most time. Two-signal / two-permission
   imagery is available and in-register.
3. **~110, Why This Chapter Matters.** The chapter's thesis. Currently the most figure-free
   high-value paragraph in the draft.
4. **~1000, §7 — the silent-failure passage** already has the flare/rock pair at ~987; a second
   beat is *not* needed. Skip unless 1–3 are declined.

**One caution on §5.** The obvious slot — the three-role split (infrastructure provider / cluster
operator / application developer) — maps temptingly onto shipboard division of responsibility, and
the brand's own seven-role architecture makes it feel natural. **Recommend against it.** The draft
already stops at ~599 and again at ~745 to warn that Gateway API's "cluster operator" is not the
operator pattern from Chapter 6. Introducing a third sense of *role* — a shipboard rank — into the
one paragraph already managing a two-way vocabulary collision would cost more than the texture is
worth. If §5 gets a figure, put it on the request flow (~700) instead.

## Pirate-vocabulary check

Structural linter catches these too, but double-checked:

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey | 0 | — |
| ye (as pronoun) | 0 | — |

Extended sweep, all zero: *arr, avast, aye, buccaneer, bilge, booty, corsair, cutlass, davy jones,
grog, hearties, jolly roger, lad/lads/lass, landlubber, mainsail, mutiny, parley, pieces of eight,
pirate, plunder, rum, salty, scallywag, scurvy, sea dog, shiver me, skipper, swab, swashbuckling,
treasure, walk the plank, yo-ho.*

Also checked and clear: **"captain," "crew," "first mate," "crow's nest"** — zero occurrences.
Absence of crew/captain vocabulary is consistent with the locked rule that the narrator is an
implied presence rather than a depicted character.

**Cliché check (rule 2): clean.** Neither *"chart a course"* nor *"set sail"* appears. The nearest
thing to a cliché is *"get under way"* at ~789, which is a dead idiom rather than a nautical set
phrase — it reads as ordinary English and would not be noticed as theming. No action required; it
simply should not be credited as texture when judging whether §6 has any.
```

---

**Headline for the revision stage:** 0.8/1000 — below the 1–3 band. The problem is distribution, not absence. §1–§4 and §8 are well seasoned (two figures, ~569 and ~987, are exemplar-grade); §5–§7 is ~6,365 prose words with one dead idiom. One overcooked site (~362, four nautical nouns in two sentences) and one repetition tic ("chart" carries 5 of 13 figures). Pirate vocabulary: clean, including an extended 32-term sweep.