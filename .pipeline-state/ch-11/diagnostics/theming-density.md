Counts are in. Emitting the stage document to stdout per pipeline convention (`Write` is outside this stage's contract; the orchestrator captures stdout).

---

# Theming-Density Audit — Chapter 11

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~19,900**
  - File total 21,658 words; less 888 words in markdown table rows (57 rows); less ~898 words inside the 8 fenced blocks (128 box-glyph figure lines + 23 YAML lines).
- Overt nautical/celestial metaphors outside branded markers: **8**
- Density: **0.4 per 1,000 words**
- Target band: 1–3 per 1,000 words
- Status: **underseasoned**

**Counting convention used:** the `Extended Analogy` sidebar (lines 107–113) is counted as **one** sustained figure rather than tallying each nautical noun inside it. It is a sanctioned container type whose entire function is extended metaphor. If you instead counted its internal figures separately (hold, crew rotation, shipper's claim, quartermaster, terms-of-arrangement), the total rises to 12 and the density to 0.6 per 1,000. **The verdict is the same under either convention** — the chapter does not approach the bottom of the band on any counting rule.

---

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 5 | "Chapter 11: Below the Waterline" | nautical — ship structure | **excellent** — load-bearing; names the §1 lifetime ladder's vertical register and is paid off by line 107 |
| 39 | "The cargo does not belong to the crew. It was aboard before this watch, and it will be aboard after." | nautical — cargo/watch | **excellent** — epigraph states the chapter's thesis (storage outlives the Pod) without naming the subject |
| 107–113 | "Think of the ship's hold, below the waterline… A shipper files a claim against space in the hold. A quartermaster decides which part of the hold satisfies it." | nautical — cargo/hold (sustained) | **acceptable** — dense, but it is an Extended Analogy sidebar and every term maps to a real object (hold→PV, shipper's claim→PVC, quartermaster→binding loop, terms of the arrangement→reclaim policy). See vocabulary note below re: *quartermaster*. |
| 439 | "**Voyage Progress: you are through the harbor and into open water.**" | nautical — passage | **cliché, thin** — "into open water" is stock. The branded strip 🗺️→🌊→🌅 carries the function on its own; the gloss adds phrasing, not meaning. Trim or make it specific to the §2→§3 transition. |
| 569 | "This is the third sighting of the same light." | nautical/celestial — navigational light | **excellent** — the chapter's best figure. Turns Ch 10's "an object without its component does nothing" into something a reader can count, and it is doing pedagogy, not decoration. |
| 861 | "### The fourth sighting" | nautical — navigational light | **acceptable** — sustains the 569 figure at heading level |
| 871 | "That is the same light, the fourth time." | nautical — navigational light | **acceptable** — closes the thread cleanly |
| 1373 | "The hold is inventoried by people who never sail. That is not a failure of the arrangement. That is the arrangement." | nautical — cargo/hold | **excellent** — returns the line-107 analogy as an aphorism; earns its place |

**Considered and not counted** (rule 4 — functional language, not deliberate figure):

- Line 190, "An escape hatch is precisely what it is, and escape hatches open both ways." — `escape hatch` is quoted from the Kubernetes documentation at line 188 and is a dead idiom in English. The author extends a source's phrase rather than reaching for the register.
- Lines 296, 319, 406, 1095 — "watches for new PVCs", "the reversal to watch for", "the component that watches for it". Control-loop vocabulary; no figurative intent.
- "Cross-bearing", "Soundings", "Taking Your Bearings", "Fixed Point", "Navigational Hazards", "Dead Reckoning", "Safe Harbor", "Zenith", "Worth Securing", "Snag", "Closer Look", "Mnemonic", "The Voyage Ahead" — branded markers and the locked margin-icon/sidebar set. Excluded per rule 1.

---

## Overcooked passages

**None.**

The only place overt metaphors stack is lines 107–113, and that is a sanctioned `Extended Analogy` sidebar doing four distinct concept mappings in four sentences. It is dense by design and by contract. No trim recommended.

Worth noting as a *distribution* problem rather than an overcooking one: **five of the eight metaphors fall in the first 113 lines (~8% of the chapter), and one more in the last three lines.** The chapter opens theme-heavy, then abandons the register almost entirely. A reader who samples §2 through §6 in isolation would not identify this as a Lodestar Ledgers chapter from its prose texture alone — only from its markers.

---

## Underseasoned passages

Two stretches well past the 800-word flag threshold carry zero thematic texture outside branded markers:

| Lines | Span | Approx. words | Content |
|---|---|---|---|
| 114–438 | Extended Analogy → Voyage Progress | ~5,100 | What You'll Learn, all of §1 (the lifetime ladder and every volume type), all of §2 (PV/PVC/binding/phases), and Taking Your Bearings #1 |
| 872–1372 | "the same light, the fourth time" → Safe Harbor | ~7,900 | §6 (StatefulSet pairing), **§7 in full**, Exam Alert, all 17 Practice Questions, Chapter Summary, The Voyage Ahead |

Two shorter gaps for completeness: lines 440–568 (~2,000 words, §3 through the provisioning figure) and 572–860 (~4,550 words, §4 access modes and reclaim policies plus Taking Your Bearings #2).

**The one that matters is §7.** Lines 1080–1110 are the ☀️ Zenith synthesis section — the chapter's designated payoff — and they contain no nautical or celestial figure at all. The synthesis lands on "records of intent outlive the things that act on them" and "one idea wearing different clothes." Both are good sentences; neither is in register. The chapter title, the epigraph, and the closing quote all point at the same idea in the brand's own vocabulary, and §7 is the natural place to collect them, but it reaches for abstraction instead. **Recommend one figure in §7 that closes the loop back to the hold** — the material is already there at lines 39 and 1373, sitting on either side of it.

Secondary recommendation: **§4 is the highest-yield section in the chapter (four of seven exam traps) and has zero texture across ~4,500 words.** The "same light" figure at 569 demonstrates that this author can carry a metaphor that does pedagogical work. One comparable figure in §4 — attached to the reclaim-policy inheritance chain, where the decision is made by someone who left the ship before you boarded — would raise the density and reinforce the chapter's actual argument at the same time.

Adding roughly **12–20 further metaphor touches** would bring the chapter to the bottom of the band (1.0/1,000). Reaching the middle would take ~40, which is more than this material wants. **Target the low end of the band and place the additions in §4, §6, and §7**, not evenly.

---

## Pirate-vocabulary check

Swept a 22-term lexicon against the full draft (case-insensitive, word-boundary anchored): `ahoy`, `matey`/`maties`, `arrr+`, `avast`, `scallywag`/`scalawag`, `booty`, `landlubber`, `lubber`, `hearties`, `shiver`, `plunder`, `swab`, `yo-ho`, `belay`, `savvy`, `doubloon`, `jolly roger`, `walk the plank`, `buccaneer`, `corsair`, `pieces of eight`, `ye`.

| Term | Occurrences | Action |
|---|---|---|
| *(all 22 terms)* | 0 | — |

**Clean.** No caricature register anywhere in the chapter. Zero hits on the full sweep, including `ye` as pronoun.

---

## Vocabulary note — one term worth a second look

Line 111 uses **"A quartermaster decides which part of the hold satisfies it."** *The Quartermaster* is a locked narrator role family (cloud platform / shared infrastructure — Azure AZ-900 and future cloud certs; ratified 2026-04-19). KCNA's role family is *The Communications Officer*.

The usage here is a lowercase common noun inside an analogy, not a narrator reference, so it is not drift as written. But it puts a role-family name in a non-role-family book, and the brand-visual-element ceiling reflection warns that each named element adds drift surface. **"The quartermaster decides which part of the hold satisfies it" reads identically as "the cargo officer decides…" or simply "someone decides…"** — and the analogy loses nothing. Recommend the substitution as cheap insurance. Flagging for the reviewer rather than asserting it as a fault; this is a brand-consistency call above this audit's pay grade.