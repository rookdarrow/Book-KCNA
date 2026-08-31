Read the draft at `C:\dev\lodestar\Book-KCNA\.pipeline-state\ch-14\draft-v1.md` (1,088 lines). Audit follows.

```markdown
# Theming-Density Audit — Chapter 14

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~13,300**
- Overt nautical/celestial metaphors outside branded markers: **6**
- Density: **0.5 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Counting method.** Raw file is 16,229 words. Deducted: 7 fenced blocks (162 lines,
724 tokens — the five FIGURE diagrams, the zenith diagram, and the template/render
snippet in §2), 54 table lines (1,030 words), inline `[source: …]` tags (322 words),
and inline `*[cross-bearing: …]*` pointers (428 words). Remainder ≈ 13,300 words of
body prose, which includes Soundings, Practice Questions, and all answer explanations.

**Excluded by rule 1** (structural terminology, always acceptable, not counted):
🧭 Soundings (L42), ☆ Taking Your Bearings ×2 (L482, L733), ★ Fixed Point ×5 (L215,
L337, L400, L442, L554), ⚠ Navigational Hazards ×2 (L414, L710), ☀️ Zenith §7 heading
(L796) and summary row (L1067), 🏆 Safe Harbor (L1071), The Voyage Ahead (L1079),
Logbook Entry (L115), Extended Analogy (L424), ⚓ Worth Securing ×2 (L310, L351),
🪝 Snag ×3 (L203, L302, L452), 🔭 Closer Look (L625), 🪢 Mnemonic ×2 (L412, L478),
and ~40 `*[cross-bearing: …]*` pointers.

**Excluded by rule 4** (vocabulary overlap, not figures of speech): "Helm" wherever it
names the product; "chart" wherever it denotes the Helm artifact; "manifest" (Kubernetes
/OCI term); "drift" (config drift, industry term); "watches a repository" (L318 ×2,
L398) describing a GitOps agent's actual behavior.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~1 | "Chapter 14: Packing for the Voyage" (chapter title) | nautical — journey/provisioning | acceptable — the title does literal work; the chapter is about packaging |
| ~3 | "A chart is not a release, and templates are not the point" (subtitle) | nautical — pun on Helm's "chart" | acceptable — the double meaning is free, and the sentence is the chapter's thesis |
| ~101 | "That is a directory with instructions attached, and the instructions are a note somebody left for the next watch." | nautical — watch-standing | acceptable — strongest beat in the chapter; the figure carries the argument (a README *is* a handoff artifact) rather than decorating it |
| ~199 | "…which is a poor thing to require of somebody taking over the watch." | nautical — watch-standing | acceptable, with a caveat: second deployment of the same figure 98 lines later. Same argument, so the echo reads deliberate, but it means the chapter has one nautical *idea*, used twice, not two |
| ~213 | "Helm calls its packaging format a **chart**, which is a convenient word for a book like this one." | nautical — brand-aware wink | acceptable — the chapter's one explicit theming beat, and it is a good one: dry, one clause, no dwelling |
| ~1089 | "The chart is what you meant. The cluster is what happened. The interesting question is who keeps them the same." (closing quote) | nautical — chart pun | acceptable — the pun does real semantic work (chart = intent) rather than being ornament |

**Borderline, not counted:**

| Line | Passage | Why not counted |
|---|---|---|
| ~800 | "You have been comparing them at the wrong altitude." | Abstraction-level idiom in general English. The celestial resonance of "altitude" (angular height of a body) is coincidental, not authored. Flagged because this is the cheapest available site for an in-register turn — see below. |
| ~1083 | "Afterward, nothing watches." | Reads functional. Sits close enough to the two counted watch-standing figures that it picks up faint thematic colour, but on its own it is plain description. |
| ~818–820 | "The mechanisms could not be more different. / The destination is the same one. / The destination is the point." | Journey figure, but inside the fenced `ch14-zenith-package-not-template` diagram, so excluded from the prose word count and from the density figure. Worth noting: it is the only journey language in the chapter's back half. |

## Overcooked passages

**None.** No passage in this chapter stacks two or more overt metaphors. There is no
mixed-register collision, no extended nautical conceit, and nothing that reads as
performance. The chapter's two figurative set pieces — the Logbook Entry at L115 (the
`deployment-prod-final-v2-USE-THIS-ONE.yaml` directory) and the Extended Analogy at
L424 (package/installation/history on an administered machine) — are both *non-nautical*
by construction, drawn from the reader's own working life. That is a defensible choice
and it is why the overcooked column is empty.

## Underseasoned passages

The chapter is thematically front-loaded. Five of the six metaphors land in the first
213 lines; after L213 there is exactly one, and it is the closing quote at L1089.

| Span | Approx. body words | Overt metaphors | Notes |
|---|---|---|---|
| L214–481 (§2 body, §3, §4) | ~3,240 | 0 | Includes the chapter's central section (§3, Chart/Release/Revision) and its Extended Analogy — all of it in plain register |
| L482–795 (☆ TYB 1, §5, §6, ☆ TYB 2) | ~4,010 | 0 | The longest barren stretch. Spans both checkpoints, all of Kustomize, and the whole decision section |
| L796–1088 (§7, Exam Alert, 17 Practice Questions + answers, Chapter Summary, Safe Harbor, The Voyage Ahead) | ~3,560 | 0 | The ☀️ Zenith section itself — the chapter's designated synthesis moment — carries no thematic texture at all; the only journey language nearby is inside a fenced figure |

**Cumulative: ~10,800 consecutive words of body prose with zero thematic texture** —
roughly 81% of the chapter — broken only by the epigraph-style closing quote.

Assessment: the individual metaphors here are *good*. Each of the six earns its place,
none is cliché, none is caricature, and the watch-standing figure at L101 is the kind
of beat the brand exists to produce. The problem is distribution, not quality. A reader
who opens at §3 and reads to the Chapter Summary — which is how a cert guide is
actually read on a second pass — encounters nothing that identifies this as a Lodestar
book except the branded markers, and rule 1 says markers do not count. The chapter
reads as competent technical prose wearing brand furniture.

**Sites where a beat would be in-register and load-bearing** (offered as sites, not
prescribed prose; three or four of these would bring the chapter to ~0.8–1.0/1000 and
into the low end of the band without touching the density of the front half):

- **~L398–410, §3, "The word that means two things."** The section turns on two
  mechanisms sharing one English word at different scopes. A single celestial or
  positional figure — one clause, on the difference between fixing a whole position and
  fixing one landmark — would be exactly on-brand and would do explanatory work.
- **~L568, §5, "the base is not edited, the base is not copied."** The base/overlay
  relation is a fixed-reference-plus-declared-offset structure. That is what the brand's
  whole navigational register is *about*, and the section currently describes it in
  pure software vocabulary.
- **~L720–730, §6, "The four, closed."** The recapitulation table is followed by a
  paragraph on reading your own situation. A brief bearing-taking figure here would be
  in-register and would close the section's arc.
- **~L798–806, §7 (☀️ Zenith).** The designated synthesis section is the single most
  conspicuous gap. "You have been comparing them at the wrong altitude" (L800) is
  already reaching for a spatial figure and stopping short; committing it to the
  celestial register would cost one clause and would give the Zenith moment the
  atmosphere its marker promises.
- **~L1073–1075 (🏆 Safe Harbor) and ~L1081–1087 (The Voyage Ahead).** Both sections
  carry branded headings and then decline to follow through in the prose beneath them.
  This is the pattern that makes the back half read texture-less: the furniture is
  thematic and the contents are not.

One correction to make while adding: the watch-standing figure is used twice (L101,
L199) for the same argument. If beats are added elsewhere, consider whether L199 should
vary rather than repeat — or keep it deliberately as a callback, but decide rather than
inherit.

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
| grog / rum / parley / scurvy | 0 | — |

Clean. Zero pirate-register vocabulary.

**Cliché sweep (rule 2)** — also clean. Zero occurrences of: chart a course, set sail,
smooth sailing, uncharted waters, weather the storm, batten down, all hands, know/learn
the ropes, tip of the iceberg, sea change, steady as she goes, on the horizon, in the
same boat, rough seas, loose cannon, turn the tide, rising tide, safe passage, plain
sailing, guiding star, north star, true north, dead in the water.

The six metaphors that are present are all authored rather than inherited. Whatever
this chapter needs, it is not a trim.
```

**Bottom line:** Ch 14 is at **0.5 overt metaphors per 1,000 words against a 1–3 band — underseasoned**, and the shortfall is a distribution problem, not a quality one. Five of six beats land before line 213; ~10,800 consecutive words after that (including the ☀️ Zenith synthesis section, 🏆 Safe Harbor, and The Voyage Ahead) carry branded headings over prose with no thematic texture underneath. Nothing is overcooked, no clichés, no pirate vocabulary. I flagged five specific insertion sites and one repeated figure (watch-standing, L101 and L199) to decide about.