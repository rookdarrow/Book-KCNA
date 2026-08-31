I read the actual `draft-v1.md` and measured it rather than estimating. Here is the audit document.

---

```markdown
# Theming-Density Audit — Chapter 16

Source: `../Book-KCNA/.pipeline-state/ch-16/draft-v1.md` (1,224 lines).
Line numbers cited against that file.

## Summary

- Total word count (body prose only, excluding code blocks and tables): **15,925**
  - Raw file: 17,881 words. Excluded: 7 fenced blocks (ASCII figures, kubectl
    commands, YAML, one error-output block) and all pipe-delimited table rows.
- Overt nautical/celestial metaphors outside branded markers: **1**
  - Generous count, admitting all four borderline dual-coded items below: **5**
- Density: **0.06 per 1,000 words** (0.31 generous)
- Target band: 1–3 per 1,000 words
- **Status: underseasoned** — by a wide margin. The band floor for a chapter of
  this length is 16 instances; the chapter has one.

Method note: a full nautical/celestial vocabulary sweep (58 terms — voyage, chart,
course, sail, harbor, anchor, star, lodestar, compass, tide, helm, crew, fleet,
shoal, reef, horizon, adrift, keel, rudder, wake, waters, vessel, deck, mast,
sextant, beacon, lighthouse, celestial, constellation, dawn, map, cargo, berth,
and the pirate set) returns **three hits in 1,224 lines**, two of which are branded
structure (`🏆 Safe Harbor reached`, line 922; `## The Voyage Ahead`, line 1214).

## Catalog of metaphors

| Line | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 647 | "You have not fixed anything. **You have halved the map.**" | celestial/nautical — cartography, navigation | **acceptable — and the best line in the chapter.** Earned, compact, lands the §5 elimination point better than the literal restatement would. Keep verbatim. |

That is the complete list. Borderline items considered and **not** counted, per
rule 4 (vocabulary overlap, not deliberate figure of speech):

| Line | Passage | Why not counted |
|---|---|---|
| 104 | "the person who **shipped** the thing" | Software-release vocabulary. Dual-coded with the brand register but functional first. |
| 806 / 25 | "§7 — Before You **Ship** It" | Same. |
| 326 | "this is an **instrument**, not a workload" | Literal — a diagnostic instrument. Faint navigational resonance only. |
| 1222 | "After that, **the instruments.**" | Refers to observability instrumentation (Ch 18). The sentence-fragment framing gives it a navigator's-console flavour, but the referent is literal. Closest thing in the chapter to a second thematic touch. |
| 934 / 1220 | "Different **altitude**" / "a change of **altitude**" | Zoom-level abstraction. Aviation-adjacent, not nautical or celestial. |
| — | `port`, `port-forward` (~40 occurrences) | Network port. Pure vocabulary collision; a naive counter would inflate this audit by 40. Explicitly not metaphors. |

## Overcooked passages

**None.** No passage in the chapter stacks two or more overt nautical/celestial
metaphors, and no cliché fired: `set sail`, `chart a course`, `smooth sailing`,
`weather the storm`, `all hands`, `batten down`, `uncharted`, `north star`,
`steady as she goes`, `on the horizon` — all zero occurrences.

The single densest figurative moment is line 647, which carries two figures in one
callout ("a **second road to the same house** … the mail arrives by the back road"
followed by "you have halved the map"). It reads fine because the first figure is
domestic/terrestrial and only the second is in the brand register, so they don't
compete. No trim recommended.

## Underseasoned passages

The chapter is one long dry stretch interrupted once, at line 647.

| Stretch | Approx. prose words | Overt metaphors |
|---|---|---|
| Line 1 → 646 (open, Soundings, §1–§4, first checkpoint, most of §5) | ~8,300 | 0 |
| Line 648 → 1224 (§6, §7, second/third checkpoints, Zenith §8, Exam Alert, 15 practice Qs, summary, The Voyage Ahead) | ~7,600 | 0 |

Both stretches are roughly ten times the 800-word flag threshold.

**Does the chapter therefore feel texture-less overall? Partly — and the diagnosis
matters more than the count.** The chapter is not brand-less. It carries 73 branded
structural instances (42 cross-bearings, plus Soundings, three Taking Your Bearings,
three Fixed Points, two Navigational Hazards, one Dead Reckoning, Safe Harbor,
Zenith, and 11 margin icons — ⚓ ×5, 🪝 ×4, 🔭 ×3, 🪢 ×2). Structurally it is one of
the most on-brand chapters in the book. What it lacks is *voice-level* texture: the
prose itself never once reaches for the brand's register.

Three further observations, all actionable at revision:

1. **The chapter does reach for figurative language — just in the wrong register.**
   Every deliberate figure in it is domestic or terrestrial: "a tool you hand
   **through the window**, not a room you add to the house" (328); "keep breaks 1–2
   and 3–4 in separate **mental boxes**" (594); "a second **road** to the same house"
   (647); "eliminate the most **ground** first" (115, 142). This is the cheapest
   route to the band — converting two or three of these to nautical/celestial
   equivalents costs zero added words and no new prose.

2. **The chapter's structural hinges are all bare.** Every one is a natural site
   for a single-clause touch, and every one currently passes without: the §1 opener
   (126), the §2/§3/§4/§6/§7 openers (184, 256, 518, 742, 806), the three checkpoint
   closers (418ff, 657ff, 842ff), the Zenith at 926–957, and the authored closing
   aphorism at 1224 ("The boundary is not a wall between two teams. It is the line
   that tells each of them where to look") — which is the chapter's most quotable
   line and carries no thematic register at all. Ten hinge sites plus two or three
   register conversions lands the chapter at roughly 12–16 instances, i.e. at or
   near the band floor, without adding a paragraph anywhere.

3. **Series consistency, flagged not decided (outside this audit's remit).** Peer
   chapters in this book carry nautical titles — "The Ship's Company" (3), "The
   Smallest Vessel" (5), "Fleets, Not Vessels" (6), "Below the Waterline" (11),
   "Packing for the Voyage" (14), "The Chart Is the Truth" (15). Chapter 16's title
   and subtitle ("Your Application, Their Cluster" / "Four questions that separate
   your bug from theirs") are entirely non-thematic, as is its paired Chapter 13.
   So the Part IV pair carries no thematic identity at the title level either, which
   compounds the prose-level absence rather than offsetting it.

**Counter-consideration the revision stage should weigh:** this is a debugging
chapter built around a scope boundary, and its rhetorical mode is deliberately
Dead-Reckoning-ish — plain, mechanical, facts-first. That is a defensible reason for
restraint and an argument against mechanically manufacturing 16 metaphors to satisfy
an arithmetic band. The recommendation is the band floor reached through hinge
placement and register conversion, not a quota applied to body prose. Over-correction
here trades an underseasoned chapter for an overcooked one, which is the worse
failure.

## Pirate-vocabulary check

Clean. Verified by full-file regex sweep; all counts are literal, not sampled.

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / hearties | 0 | — |
| ye (as pronoun) | 0 | — |
| aye / arrr / avast | 0 | — |
| landlubber / shipmate / seadog | 0 | — |
| buccaneer / corsair / swashbuckl* | 0 | — |
| plunder / booty / treasure | 0 | — |
| grog / scurvy / bilge / cutlass | 0 | — |
| jolly roger / walk the plank | 0 | — |

Cliché sweep (rule 2), also all zero: `set sail`, `chart a course`, `smooth sailing`,
`all hands`, `batten down`, `weather the storm`, `rough seas`, `uncharted`,
`north star`, `guiding star`, `steady as she goes`, `steer`, `tempest`, `storm`.
```

---

Two notes on execution:

- **The file was not written.** `diagnostics/theming-density.md` requires the Write tool, which is not permitted in this session (the write to a scratch path was declined, and the pipeline's executor strips `Write` from `--allowed-tools` by design so stage output flows through stdout). The document above is the complete stage output for the orchestrator to capture. If you want it on disk instead, grant write access and I'll place it at `../Book-KCNA/.pipeline-state/ch-16/diagnostics/theming-density.md`.
- **Word count is measured, not estimated** — 15,925 prose words after excluding 7 fenced blocks and all table rows from a 17,881-word file. The metaphor count comes from a 58-term vocabulary sweep across all 1,224 lines, which returned three hits, two of them branded structure.