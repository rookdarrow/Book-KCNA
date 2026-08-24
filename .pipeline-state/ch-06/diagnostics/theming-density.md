I located the chapter and audited it. One thing you need to know before the numbers: **the voiced draft is truncated on disk.**

- `ch-06/draft-v1.md` (the voice-swap output) is **254 lines / 3,810 words** and begins mid-word — `"ognition exam can ask about in a single sentence"`.
- `ch-06/draft-v1-prevoice.md` is **1,214 lines / 17,859 words** and is complete.
- Those 254 lines correspond exactly to prevoice lines **961–1214**. The voice stage's stdout capture lost the first ~79% of the chapter.

I verified the surviving overlap is theming-neutral (the voice pass made em-dash→colon/period punctuation changes only; both metaphors in that range survive unchanged), so I ran the audit against `draft-v1-prevoice.md` as a sound proxy. Flagging the truncation for repair regardless — Stage 9 is not the right place to fix it.

---

```markdown
# Theming-Density Audit — Chapter 6

**Source audited:** `.pipeline-state/ch-06/draft-v1-prevoice.md` (1,214 lines).
**Why not the voiced draft:** `draft-v1.md` is truncated to its last 254 lines (prevoice
961–1214), starting mid-word. The surviving overlap differs from prevoice only in
punctuation (em-dash → colon/period) and contains the same two metaphors in the same
places, so prevoice is theming-equivalent. **Re-run this audit after the voice stage is
re-materialized.**

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~16,500**
  *(17,859 raw `wc -w`, less ~509 words of fenced ASCII figures/terminal output, ~628
  words of table rows, ~160 words of HTML comments and FIGURE anchors. Estimated by
  inspection — mechanical counting was unavailable in this environment. ±150.)*
- Overt nautical/celestial metaphors outside branded markers: **12** counted
  (**15** catalogued, minus 2 Attention-Budget table echoes of headings and 1 functional usage)
- Density: **0.7 per 1000 words** (0.9 if the echoes and borderline usage are counted)
- Target band: 1–3 per 1000 words
- Status: **underseasoned** — below the floor on either count

## Catalog of metaphors

Line numbers refer to `draft-v1-prevoice.md`.

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 1 | "Chapter 6: **Fleets, Not Vessels**" | nautical — fleet/vessel | acceptable — the chapter's controlling metaphor, and it does real work (a fleet is a count + a template) |
| 2 | *"Nobody sails one Pod"* | nautical — sailing | acceptable — sets up §9's payoff |
| 18 | Attention Budget row: "§4 — Changing the Fleet **Under Way**" | nautical — under way | not counted (table row echoing the §4 heading) |
| 25 | Attention Budget row: "§9 — Nobody **Sails** One Pod" | nautical — sailing | not counted (table row echoing the subtitle) |
| 38 | "A **fleet** is not a number of **ships**. It is an intention, expressed in **ships**." | nautical — fleet/ships | acceptable — epigraph; densest single line but it *is* the chapter's thesis |
| 57 | Soundings Q5: "has to run on every machine in your **fleet**" | nautical — fleet | not counted — "fleet of machines" is standard industry usage (Rule 4) |
| 363 | §4 heading: "Changing the Fleet **Under Way**" | nautical — under way | acceptable — not cliché, and "under way" carries the exact sense (changing while serving traffic) |
| 365 | "Everything so far has been about **holding a fleet steady**." | nautical — seamanship | acceptable |
| 472 | "Section 4 changed **the fleet**." | nautical — fleet | acceptable — motif callback, one word |
| 541 | Bearings #2 intro: "Five questions on changing **the fleet**" | nautical — fleet | acceptable — motif callback |
| 660–668 | **Extended Analogy:** "two ways of **crewing a vessel** … any **bosun's mate** can stand any **watch** … the **pilot** who knows this **harbour** … the **chart** she's been annotating" | nautical — crew/seamanship (sustained) | acceptable — see note below |
| 906 | §9 heading: "Nobody **Sails** One Pod" | nautical — sailing | acceptable |
| 953 | "**Nobody sails one Pod** — not because a single Pod is forbidden, but because a single Pod is a statement about *right now*." | nautical — sailing | acceptable — the title cashed out; the best-earned metaphor in the chapter |
| 1205 | *"…and **the sea** does not always have room where you wanted it."* | nautical — sea | acceptable — closing quote, single touch |
| 1211 | "You came in able to read a Pod and left able to **author a fleet**." | nautical — fleet | acceptable |

**Celestial metaphors: zero.** No stars, lodestar, North Star, bearings-as-figure,
horizon, or constellation imagery anywhere in the body prose. The only occurrence of
"Lodestar" (line 39) is the epigraph's publisher attribution, not a figure of speech.

**Clichés: zero.** No "chart a course," "set sail," "smooth sailing," "uncharted
waters," "weather the storm," "tight ship," "even keel," "dead in the water," or "the
stars align." This chapter is clean on the cliché axis — notably so.

**Deliberately not flagged** (Rule 4 — vocabulary overlap, not figure of speech):

| Line(s) | Term | Why it's functional |
|---|---|---|
| 189, 533, 838 | "Helm chart", "Charts ship CRDs" | product name + software-distribution verb |
| 692, 838 | "Networking plugins **ship** as DaemonSets" | "ship" = release/distribute |
| 15, 193, 195, 1115 | "A Loop You Can **Watch** Working", "Both **watch** a resource" | plain observation; also the literal Kubernetes watch verb |
| 199, 228, 303, 412, 564, 714, 978, 1181 | "**line** that up", "one-**line** warning", "above the **line**" | idiom / graph axis / text line |
| 371 | "of **course** you'd need somewhere…" | discourse marker |

## Overcooked passages

**None requiring a trim.** Two local concentrations were examined and both clear:

1. **Front matter, lines 1–39 (~400 words): 5 occurrences (~12/1,000 locally).**
   Title, subtitle, two Attention-Budget echoes, and the epigraph. This is the chapter's
   framing apparatus, where theming is structurally expected and the reader has not yet
   started reading prose. Not a trim candidate.

2. **Extended Analogy, lines 660–668 (~230 words): ~8 nautical lexical items
   (~35/1,000 locally).** This is by far the densest passage in the chapter and it is
   the *right* density. It's a sanctioned sidebar type (`style-decisions.md`,
   [LOCKED 2026-04-19], target 1–3 per content chapter — this chapter has exactly one),
   it is a genuine explanatory analogy rather than decoration (interchangeable crew vs.
   the pilot who knows *this* harbour maps precisely onto Deployment vs. StatefulSet),
   and it contains no cliché. It also handles the gendered-pronoun guidance correctly —
   the pilot is "she," a character in an anecdote, not the narrator. **Leave as written.**

## Underseasoned passages

This is where the chapter's actual problem is. Two stretches over 800 words carry zero
thematic texture, and the first of them is the chapter's entire teaching spine:

1. **Lines ~96–362 — "Why This Chapter Matters" through the end of Taking Your
   Bearings #1. ~4,300 words. Zero overt metaphors.** The single occurrence in this
   range (line 57, "your fleet") is functional usage. The reader meets the epigraph's
   fleet-of-ships thesis on line 38 and then does not encounter the register again until
   line 363. That gap spans the ownership chain, the visible control loop, and
   selector-based membership — the three ideas the chapter is built on.

2. **Lines ~682–902 — §7 through the end of Taking Your Bearings #3. ~3,000 words.
   Zero overt metaphors.** Covers DaemonSet/Job/CronJob, the decision tree, and the
   whole CRD-and-operator abstraction jump.

3. *(Not flagged.)* Lines ~957–1194, Exam Alert through the answer key, ~3,900 words,
   zero. A question bank with no theming is correct, not underseasoned.

**Assessment.** The chapter is not texture-*less* — the fleet motif is coherent, it is
placed at the structural joints (title → epigraph → §4 → §9 → Safe Harbor), and §9 pays
off the subtitle with real force. What's missing is any touch between the joints. The
seasoning is all at the seams and none in the body, which is why the number lands below
the band despite the chapter reading as on-brand at open and close.

**If a pass is made** (this is a judgment call, not a lint failure — the skill permits
selective use, and thin-but-clean is a far better failure mode than overcooked): the two
dry stretches would each take one touch, placed where the register would carry meaning
rather than decorate. Candidates:

- **§2, around line 245** ("Self-healing and scaling are the same operation"). The
  strongest under-used opening in the chapter — a watch that does one thing whether the
  gap opened because you asked for more or because one was lost.
- **§8, around line 832** ("It is not privileged infrastructure. It is a workload,
  exactly like yours"). The operator-is-just-a-Deployment beat wants one line of register
  to land its deflation.

Two touches would put the count at 14/16,500 = 0.85 counted, ~1.0 including the echoes —
at the floor rather than under it. Three would be comfortably inside the band. More than
three risks the opposite problem in a chapter whose current restraint is a genuine asset.

**Off-register note** (outside this audit's budget — neither is nautical or celestial, so
neither counts toward density; recorded because both are metaphors reaching outside the
brand register in a chapter that is already thin on register texture):

| Line | Passage | Register |
|---|---|---|
| 529 | "The Deployment doesn't have a special **reverse gear**. It has one **gear**, and rollback points it at an older template." | vehicular |
| 247 | "It stays true **at this altitude**" | aviation |

Line 529 is the more notable of the two: it's a well-turned, load-bearing metaphor sitting
in a chapter that reaches for sails everywhere else. Worth a look at revision — a maritime
equivalent exists and would cost nothing.

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / maties | 0 | — |
| ye (as pronoun) | 0 | — |
| avast | 0 | — |
| arr / arrr | 0 | — |
| landlubber | 0 | — |
| swashbuckling | 0 | — |
| booty / plunder | 0 | — |
| scallywag | 0 | — |
| shiver me timbers | 0 | — |
| walk the plank | 0 | — |
| hearties | 0 | — |
| buccaneer / cutlass / jolly roger | 0 | — |

Clean. No caricature register anywhere in the chapter.
```

---

**Two things for the runner, outside the audit itself:**

1. **`ch-06/draft-v1.md` needs re-materializing.** It is missing prevoice lines 1–961. The full voiced output may be recoverable from `.draft-voice.md.progress.log` (766 KB of token-level NDJSON, preserved) without re-running the stage. Every downstream Stage-9-and-later diagnostic reading `draft-v1.md` — `curriculum-alignment`, `fact-accuracy`, `question-quality`, all of which have live heartbeats right now — is auditing 21% of the chapter. Worth checking their outputs before trusting them.

2. **The chapter carries two `AUTHOR-REVIEW` comments** (lines 696, 778) already flagged by the drafting stage — one on the unsourced "DaemonSet has no `replicas` field" claim (research gap G-6A), one on stale cross-bearings in shipped Chapters 1 and 2 pointing at §3 where this chapter's ordering puts §6 and §8. Not my remit, but they're unresolved.