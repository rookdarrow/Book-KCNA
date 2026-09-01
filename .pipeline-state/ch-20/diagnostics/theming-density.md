I could not run scripts (both Bash and PowerShell were declined), but Grep and a single `Measure-Object` call went through, so the counts below are measured against `draft-v1.md` rather than estimated by eye.

```markdown
# Theming-Density Audit — Chapter 20

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~10,800**
  (11,201 words in file, less ~159 in the two rubric tables, ~12 in the single YAML fence
  at item 12, and ~230 in the two `AUTHOR-REVIEW` HTML comments)
- Overt nautical/celestial metaphors outside branded markers: **5**
  (of which **4 are inherited** — quoted section titles from other chapters carried inside
  `cross-bearing` pointers — and **1 is authored in this chapter**)
- Density: **0.46 per 1000 words** (authored-only: **0.09 per 1000 words**)
- Target band: 1–3 per 1000 words
- Status: **underseasoned** — but see the note below; this is very likely correct for this chapter

**Note on chapter type.** This is `chapter_type: mock_exam`, and the chapter argues its own
case for the absence at line 11: *"There is no Soundings block here, no Fixed Points, no
callouts in the margin: a diagnostic instrument that keeps interrupting itself with
encouragement is not a diagnostic instrument."* That is a defensible design decision, and the
recommendation section below does **not** ask for metaphors to be added to the exam block or
the answer key. The band miss is reported because the audit is mechanical, not because the
chapter should be seasoned to hit it.

The denominator is also doing most of the damage. Roughly 9,600 of the ~10,800 words are the
60-item exam block and the 59 answer walkthroughs — instrument text, where texture is a defect.
Measured against only the chapter's framing prose (Instructions, lines 7–52, plus Scoring
Rubric, lines 1203–1245, ≈ 1,190 words), density is **0.84 per 1000** — just under band, and a
single additional light beat would put it inside.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~769 | "*[cross-bearing: see Ch 8 §2 — three gates and **a logbook**]*" | nautical — ship's log | acceptable (inherited: Ch 8 §2 title) |
| ~915 | "*[cross-bearing: see Ch 7 §4 — when the **berth** refuses you]*" | nautical — mooring | acceptable (inherited: Ch 7 §4 title) |
| ~995 | "*[cross-bearing: see Ch 6 §4 — changing the **fleet under way**]*" | nautical — fleet / sailing | acceptable (inherited: Ch 6 §4 title) |
| ~1117 | "*[cross-bearing: see Ch 8 §2 — three gates and **a logbook**]*" | nautical — ship's log | acceptable (inherited; second occurrence of the same title) |
| ~1240 | "Those two readers have the same score and should **steer** completely differently for the next two weeks." | nautical/celestial — navigation | acceptable — the one authored beat in the chapter, and it lands on the chapter's thesis |

**On the inherited four.** All four are the *titles of other chapters' sections*, quoted verbatim
inside `cross-bearing` pointers. The `cross-bearing` convention itself is structural terminology
and is excluded per Rule 1; the title text inside it is not, so it is counted. But nothing should
be changed here on their account — rewriting a pointer so it disagrees with the section it points
at would break the mechanical `Ch N §M` verification the integration stage runs. If "the berth
refuses you" or "changing the fleet under way" is too much, that is a Ch 7 / Ch 6 finding, not a
Ch 20 one.

**Non-findings, recorded so the next pass does not re-raise them:**

- `Lodestar Ledgers` (line 21) — publisher name, not a figure of speech.
- `Dead Reckoning` (lines 13, 1223) and `Soundings` / `Fixed Points` (line 11) — branded markers,
  excluded by Rule 1. Line 11 *names* two markers in order to say they are absent; still excluded.
- `cross-bearing` (~70 occurrences) — locked structural convention, excluded by Rule 1.
- "without **steering** traffic by share" (line 1073) — functional. Traffic steering is standard
  progressive-delivery vocabulary; excluded by Rule 4.
- `chart` (lines 136–141, 309–314, 374–377, 710, 885, 889, 957–959) — Helm chart, the product
  name. No nautical intent. Excluded by Rule 4.
- "trusting what you **ship**" (line 1099, Ch 12 §7 title) — dead metaphor from software-release
  idiom, not maritime register. Excluded by Rule 4.
- "**cordon** ... **drain**" (line 835) — `kubectl` subcommand names. Excluded by Rule 4.

## Overcooked passages

**None.** No passage stacks two or more overt metaphors. The maximum density anywhere in the
chapter is one metaphor per paragraph, and only at four widely separated points.

Cliché sweep is also clean: zero hits for *chart a course*, *set sail*, *smooth sailing*,
*navigate the waters*, *stay the course*, *all hands*, *uncharted*, *weather the storm*,
*rising tide*, *North Star*, *the stars align*. This chapter has no cliché problem — the
opposite, if anything.

## Underseasoned passages

Three contiguous stretches exceed 800 words with zero thematic texture:

| Lines | Section | ~Words | Assessment |
|---|---|---|---|
| 53–610 | `## Exam` — all 60 items | ~4,900 | **Correct as written. Do not season.** Metaphor inside a timed diagnostic instrument is noise the reader has to parse under clock pressure. Adding texture here would be a defect. |
| 612–768 | Answers 1–15 | ~1,575 | Acceptable. Walkthroughs are deliberately terse — answer, why, three refutations. Texture would dilute the refutations, which are the pedagogical payload. |
| 1117–1240 | Answers 52–60 plus rubric intro | ~1,050 | Acceptable, same reasoning. |

The longest single texture-free run is lines 53–768 (~6,475 words), which is the exam block plus
the first quarter of the answer key.

**The one place worth a look** is the Instructions section (lines 7–52, ~740 words) — under the
800-word flag threshold, so not formally flagged, but it is the chapter's main authorial-voice
moment and carries zero metaphors. It is where the brand voice would normally be audible: it
explains what the instrument is, what conditions to reproduce, and why the per-domain sheet exists.
The prose there is strong and does not read flat — it earns its effect through structure and
plain statement rather than figure ("It was written by Lodestar Ledgers. It is not a leaked exam,
not a reconstruction of one, and not a prediction of your score.").

**Recommendation:** optional, and at most one beat. If the revision stage wants the chapter inside
band on its framing prose, the natural site is line 43 — *"That is the whole argument for the score
sheet at the end of this chapter"* — or line 45's "The answers" preamble. One light navigational
figure there would bring framing-prose density to ~1.7 per 1000 and cost the instrument nothing,
because it sits before the clock starts. Do not add anything after line 53 and before line 1203.

Adding nothing at all is also a defensible outcome for a `mock_exam` chapter, and the audit does
not treat the band miss as a blocker.

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey | 0 | — |
| ye (as pronoun) | 0 | — |
| avast | 0 | — |
| landlubber | 0 | — |
| shipmate | 0 | — |
| buccaneer / scallywag / hearties | 0 | — |
| plunder / booty / grog / swab / scupper | 0 | — |

Clean. No caricature register anywhere in the chapter.

## Out-of-scope observations (not theming; forwarded, not graded)

Two defects are already recorded in-file as `AUTHOR-REVIEW` comments and are owned by other
stages — noted here only so they are not mistaken for something this audit passed over:

- Item 42's walkthrough is missing from the answer key (comment at ~line 1190), and the exam block
  carries a stray *"43 continues on the next item."* line at ~line 466.
- The Scoring Rubric's per-domain item lists do not sum to their stated maximums, and items 9, 12,
  and 48 appear in two rows each (comment at ~line 1219).
```