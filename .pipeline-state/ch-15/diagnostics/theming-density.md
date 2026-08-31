Read the draft at `C:\dev\lodestar\Book-KCNA\.pipeline-state\ch-15\draft-v1.md` (1,314 lines). Audit follows.

```markdown
# Theming-Density Audit — Chapter 15

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~16,500**
- Overt nautical/celestial metaphors outside branded markers: **6**
- Density: **0.4 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Counting method.** Raw file is 19,722 words. Deducted: 7 fenced blocks (166 lines,
808 words — the six FIGURE diagrams plus the zenith diagram), 75 table lines (1,249
words), 11 HTML-comment lines (331 words — 7 FIGURE anchors and 4 AUTHOR-REVIEW notes),
169 inline `[source: …]` tags (338 words), and 48 inline `*[cross-bearing: …]*` pointers
(502 words). Remainder ≈ 16,494 words of body prose, which includes Soundings, all three
Taking Your Bearings checkpoints, the 21 Practice Questions, and every answer explanation.

**Excluded by rule 1** (structural terminology, always acceptable, not counted):
🧭 Soundings (L16, L46), ☆ Taking Your Bearings ×3 (L331, L705, L903, plus four
Attention-Budget rows), ★ Fixed Point ×5 (L237, L251, L546, L600, L1029), ⚠ Navigational
Hazards ×2 (L516, L689), — Dead Reckoning (L125), ☀️ Zenith as the §7 marker (L954) and
summary row (L1298), 🏆 Safe Harbor (L1045), The Voyage Ahead (L1302), Logbook Entry
(L448), ⚓ Worth Securing ×3 (L317, L568, L877), 🪝 Snag ×4 (L205, L402, L578, L671),
🔭 Closer Look ×3 (L327, L510, L899), 🪢 Mnemonic ×2 (L227, L592), and 48
`*[cross-bearing: …]*` pointers.

**Excluded by rule 4** (vocabulary overlap, not authored figures) — this chapter has an
unusual amount of it, and separating it out is most of the work:

| Vocabulary | Where | Why not counted |
|---|---|---|
| "chart" / "charts" | L103, L572, L576 ×3, L871 ×2, L1084, L1150, L1225, L1290 | The Helm packaging artifact. Ten occurrences, all literal. Distinct from the title/epigraph/§7 figure, which is the navigator's chart. |
| "sync wave", "wave 0", "negative waves" | §5 throughout, and Q19/TYB3 answers | `argocd.argoproj.io/sync-wave` is Argo CD's own annotation name. The single largest source of nautical-*sounding* text in the chapter, and none of it is authored. |
| "watch" / "watches" / "watch-based" | L530 (§4 heading), L548, L1005, L1285 | The literal Kubernetes watch mechanism, and the literal thing an agent does to a repository. |
| "under way", "fleet" | L327, L362 | Inside cross-bearing pointers quoting Ch 6 §4's section title. |
| "load-bearing" | L50, L390, L695 | Structural-engineering idiom, not nautical. |
| "helm" | L666, L1263 | The product name, matched by the cliché sweep for "at the helm". False positives both. |
| "blast radius" | L442, L740, L1132, L1207, L1286 | Established industry security term, and not nautical/celestial in any case. |

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~1 | "The Chart Is the Truth" (chapter title) | nautical — chart / navigation | acceptable — the figure *is* the chapter's thesis, and §7 pays it off explicitly rather than leaving it as ornament |
| ~39 | "The chart is what you meant. The cluster is what happened. The interesting question is who keeps them the same." (epigraph) | nautical — chart | acceptable as a figure. Flagged for reuse, not for theming: L42's AUTHOR-REVIEW already records that this is Ch 14's closing quote verbatim, so a reader met it eight pages ago |
| ~103, ~109 | "Afterward, nothing keeps watch." → "A ReplicaSet keeps watch. The scheduler keeps watch. The node controller keeps watch." | nautical — watch-standing | acceptable, and the chapter's best beat. Counted once: one figure, deployed as complaint (L103) then four-beat answer (L109). The repetition is anaphora doing argumentative work, not a stack |
| ~121 | "so one back-bearing rather than a repetition" | nautical — navigation (taking a bearing) | acceptable, with a caveat — see below |
| ~247 | "Chapter 6 taught you the mechanics of replacing a running fleet" | nautical — fleet | acceptable — one clause, does not dwell, and the section immediately returns to plain register |
| ~1035, ~1037 | "The chart is the truth, but not because a file is inherently authoritative. Files are only ever claims." → "The chart is the truth because **something is continuously making it true.**" | nautical — chart | acceptable — the payoff, and the only thematic texture anywhere in the chapter's back 60% |

**Caveat on ~121 (`back-bearing`).** The figure is good and in register, but the word sits
one prefix away from `cross-bearing`, which is a *branded* convention in this book with a
fixed bracketed-italic format — and L121 carries an actual `*[cross-bearing: …]*` pointer
in the same sentence. A reader who has learned the convention may parse "back-bearing" as
a variant marker rather than as prose. Either is survivable; it should be a decision rather
than an accident.

**Borderline, not counted:**

| Line | Passage | Why not counted |
|---|---|---|
| ~568 | "anchor them to Chapter 4" | Dead-metaphor English ("anchor" = fix firmly), excluded under rule 4. Noting it because it sits directly beneath the ⚓ glyph, which reactivates the maritime sense — if the pun was authored it is a good one, and it is the only place in the chapter where marker and prose reinforce each other. |
| ~261 | "the release watches itself" | Mild personification of metric-driven rollback. Picks up faint colour from the L103/L109 watch figure, but on its own it is plain description. |
| ~592 | "how much you want the ground under your production cluster to shift" | Geological, not nautical. |
| ~946 | "If that came back clean, keep it loaded." | Ordnance register. Not nautical (and not celestial), so out of this budget — but see the register note below. |

**Celestial category: zero.** The words `zenith`, `star`, `north`, `celestial`, `dawn`,
`sky`, `orbit`, `meridian`, `altitude` and their relatives appear nowhere in body prose.
`zenith` occurs twice: once in the figure-anchor slug at L968
(`ch15-zenith-control-loop-pointed-at-a-repo`) and once as the branded marker name in the
Chapter Summary at L1298. Both excluded. The whole 6-metaphor budget is nautical.

## Overcooked passages

**None.** No passage stacks two or more distinct overt metaphors, there is no mixed-register
collision inside a sentence, and nothing reads as performance or caricature.

The closest thing to a density spike is L103–L121, which carries three figures (watch,
watch-anaphora, back-bearing) in nineteen lines — roughly 1.7 per 1,000 words locally,
which is *inside* the target band, not above it. The four-fold "keeps watch" repetition at
L109 is the only construction that could be read as overcooked, and it should not be: the
repetition is the argument (Kubernetes is structurally a collection of watchers), and it is
what makes §7's payoff legible 900 lines later. Leave it.

The chapter's two big figurative set pieces — the Logbook Entry at L448 (the Friday
`kubectl edit` that reverts six weeks later) and the extended push/pull contrast at
L408–L446 — are both *non-nautical* by construction, drawn from the reader's working life.
That is the same defensible choice Ch 14 made, and it is why this column is empty.

## Underseasoned passages

Five of the six metaphors land in the first 247 lines — the front 19% of the chapter.
After L247 there is exactly one, and it is the §7 chart payoff.

| Span | Approx. body words | Overt metaphors | Notes |
|---|---|---|---|
| L122–L246 (§1, Twelve Factors) | ~1,460 | 0 | Entire section, including all four developed factors |
| **L248–L1034** | **~9,800** | **0** | The chapter's whole middle. §2's body, ☆ TYB 1, §3 (the central push/pull argument), §4 (Argo CD, the longest section), ☆ TYB 2, §5, §6, ☆ TYB 3, and the first two-thirds of §7 — including the Zenith substitution itself and the four-principles re-read |
| L1038–L1314 | ~3,550 | 0 | 🏆 Safe Harbor, Exam Alert, all 21 Practice Questions and their answers, the Chapter Summary, The Voyage Ahead, and the closing quote |

**The single barren stretch at L248–L1034 is ~9,800 consecutive words — 59% of the chapter's
body prose.** Counting the tail as well, ~13,350 words (81%) sit after the last front-loaded
beat, broken only by the two-paragraph chart payoff at L1035–L1037.

This is the same distribution pathology Ch 14 was flagged for, and it is worse here, not
better: Ch 14 ran 0.5/1000 with ~10,800 barren words; Ch 15 runs 0.4/1000 with ~9,800 in
one span and ~13,350 total. Two consecutive chapters failing the same way is a book-level
signal, not a chapter-level one.

**One thing this chapter does better than Ch 14, and it should be said.** Ch 14's audit
found the ☀️ Zenith section itself carrying no thematic texture at all. Here the Zenith
section *does* land its beat — L1035–L1037 is the chart figure resolving, and it is the
strongest single passage in the chapter. The synthesis moment has the atmosphere its marker
promises. The gap is everywhere else.

**Sites where a beat would be in-register and load-bearing** (offered as sites, not
prescribed prose; three or four would bring the chapter to roughly 0.6–0.7/1000 — still
below band, but the band is not reachable at this length without changing the drafting
habit rather than patching this file):

- **~L440–L446, §3, the four consequences.** "Where the credentials sit," "what a
  compromise gets," "what happens between deploys," "what 'the truth' means." This is the
  chapter's central argument in four beats and it is entirely plain. The watch-standing
  figure from L103/L109 is *exactly* what "what happens between deploys" is about, and
  bringing it back here would close a loop the chapter opens and then drops for 900 lines.
- **~L582–L592, §4, branch / tag / pinned commit.** Three degrees of how much the target is
  allowed to move under you. That is a fixed-reference problem, which is what the brand's
  navigational register exists for. The 🪢 Mnemonic at L592 already reaches for it ("the
  ground under your production cluster to shift") and lands on geology instead.
- **~L891–L897, §6, more than one cluster.** One control point versus per-cluster agents,
  and the trade between a unified view and isolation. A fleet-versus-single-vessel figure
  would be in register, would do explanatory work, and would pay off the lone "fleet" at
  L247 that currently stands alone.
- **~L1304–L1312, The Voyage Ahead.** Branded heading, no follow-through beneath it — the
  same pattern Ch 14 was flagged for at the same location. The content is strong (the
  `Synced`-and-wrong handoff into Ch 16) and it is written in pure plain register.

## A register note (not counted, offered because it explains the number)

The chapter is not texture-*less*. Its dominant figurative register is **ledger and
commerce**, and it is used far more heavily than the nautical one:

> L101 "left you holding a package and a complaint" · L103 "It has **bought** you less than
> it should have" · L119 "The stakes here were **banked** in Chapter 1 … Chapter 14
> **cashed** the first half" · L275 "What you **buy** is the ability to test" · L496 "Hold
> that thought; §7 **collects** on it" · L657 "Chapter 14 **spent** the first" · L936,
> L1263 "Any of these consequences **earns credit**" · L1195 "Gradual **buys** time"

Eight-plus instances against six nautical ones. This is not drift into a banned register —
"Lodestar **Ledgers**" makes accounting arguably the house's second language, and none of it
is cliché or caricature. But it is not what the 1–3/1000 band measures, and it is probably
why the chapter reads as textured while auditing at 0.4. If the register is deliberate it
belongs in `style-decisions.md`; if it is not, it is the habit that is displacing the
nautical beats the band is asking for.

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / mateys / hearties | 0 | — |
| ye (as pronoun) | 0 | — |
| avast / arrr / yarr / aye | 0 | — |
| landlubber / swashbuckler / buccaneer / scallywag | 0 | — |
| booty / plunder / treasure map / pieces of eight | 0 | — |
| shiver me timbers / yo-ho / jolly roger / walk the plank | 0 | — |
| grog / parley / scurvy | 0 | — |

Clean. Zero pirate-register vocabulary.

**Cliché sweep (rule 2)** — also clean. Zero occurrences of: chart a course, set sail,
smooth sailing, uncharted waters, weather the storm, batten down, all hands, know/learn the
ropes, tip of the iceberg, sea change, steady as she goes, on the horizon, in the same boat,
rough seas, loose cannon, turn the tide, rising tide, safe passage, plain sailing, guiding
star, north star, true north, dead in the water, at the helm, rock the boat, miss the boat,
ship has sailed, sink or swim. The sweep's only two hits were "the Helm" as a product name
(L666, L1263).

All six metaphors present are authored rather than inherited. This chapter does not need a
trim anywhere.
```

**Bottom line:** Ch 15 audits at **0.4 overt metaphors per 1,000 words against a 1–3 band — underseasoned**, on ~16,500 words of body prose. Six figures, all nautical, all authored, none cliché, zero pirate vocabulary, nothing overcooked. Zero celestial metaphors anywhere.

Three things worth the author's attention beyond the number:

1. **Distribution, again.** Five of six beats land before L247; ~9,800 consecutive words (L248–L1034 — §3, §4, all three checkpoints, and most of §7) carry none, and ~13,350 words after L247 carry one. Ch 14 was flagged for the same pathology at 0.5/1000. Two chapters in a row is a book-level signal.
2. **The Zenith section improved.** Unlike Ch 14's, §7 lands its beat — the chart payoff at L1035–L1037 is the chapter's strongest passage. The gap is everywhere except there.
3. **A competing register.** The chapter runs eight-plus ledger/commerce figures (banked, cashed, spent, buys, collects, earns credit) against six nautical ones. Not banned, arguably on-brand for "Lodestar Ledgers," but undeclared — and it is plausibly what is displacing the beats the band asks for. Worth a `style-decisions.md` line either way.

I also flagged `back-bearing` (L121) as a decision to make rather than inherit: it sits one prefix from the branded `cross-bearing` convention and shares a sentence with an actual cross-bearing pointer.