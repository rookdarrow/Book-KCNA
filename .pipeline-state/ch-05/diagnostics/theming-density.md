Analysis complete. Emitting the report to stdout for the orchestrator to capture into `diagnostics/theming-density.md`.

---

# Theming-Density Audit — Chapter 5

> **Artifact note.** The stage prompt referenced `draft-voice.md`, which does not exist at audit time: the orchestrator swaps the voice-stage output into the canonical slot and backs up the prior draft as `draft-v1-prevoice.md`. This audit reads the voiced draft at `.pipeline-state/ch-05/draft-v1.md` (1,195 lines, 109,592 bytes). Line numbers below refer to that file.

> **Counting-method caveat.** This stage ran without Bash/Write permissions, so the mechanical token count used for Chapter 4 could not be reproduced. The denominator below is a segment-by-segment estimate from a full read of all 1,195 lines, with fenced blocks, tables, HTML comments, and `[source: …]` tags (81 of them) excluded. Margin is roughly ±10%. **The verdict does not depend on the precision:** with 3 metaphors, the chapter would have to be under 3,000 words to reach the band floor, and it is unambiguously five times that.

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~15,000** (estimated)
- Overt nautical/celestial metaphors outside branded markers: **3**
- Density: **0.2 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned** — by a wide margin, and the widest yet measured in this book

**Counted by discrete image rather than by device**, the closing quote contributes two images ("vessel," "at sea"), giving 4 images and a density of **0.27 per 1000**. Still far below band. The verdict is stable under either counting rule.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~1 | "Chapter 5: **The Smallest Vessel**" | nautical — vessel | acceptable, and the best idea in the chapter's theming. A vessel *contains* and is *the thing that is crewed, addressed, and berthed* — which is precisely the Pod-wraps-containers point. It does real teaching work. |
| ~181 | "§2 — More Than One Container **Aboard**" | nautical — shipboard | acceptable, light. The only in-body echo of the title anywhere in 1,195 lines. |
| ~1187 | "A **vessel** that cannot be repaired **at sea** must be a vessel you are willing to lose. Build accordingly — and keep the plans." | nautical — vessel / sea | acceptable, and the strongest single beat in the chapter. Ties disposability (§4) back to the title conceit. |

**Borderline, not counted:**

| Line | Passage | Why not counted |
|---|---|---|
| ~34 | "That is the natural **seam**." | Sewing/geology register. A ship's seam exists, but the word isn't distinctively nautical in this use. |
| ~183 | "A Pod can **hold** more than one container." | Plain verb. Faintly evokes a ship's hold only because the adjacent heading says "Aboard" — not a deliberate figure. |
| ~196 | "A **log-shipping** agent" | Standard technical term (log shipping). Functional vocabulary per Rule 4. |
| ~123, ~131, ~851 | "the wrapper," "load-bearing fact," "load-bearing wall" | Architectural register, not nautical. |
| all `cross-bearing` tags | *[cross-bearing: see Ch N §M]* | Branded convention, LOCKED 2026-04-19. Excluded per Rule 1. |

**Excluded as branded markers (Rule 1):** 🧭 Soundings (and the three "Soundings question N" callbacks at ~210, ~563, ~638), ☆ Taking Your Bearings ×3, ★ Fixed Point ×5, ⚠ Navigational Hazards ×2, — Dead Reckoning ×2, 🏆 Safe Harbor, ☀️ Zenith, The Voyage Ahead, 🗺️→🌊→🌅, ⚓ Worth Securing ×3, 🪝 Snag ×3, 🔭 Closer Look ×2, 🪢 Mnemonic ×2. Marker discipline is clean throughout — correct symbols, correct names, no drift.

**Celestial metaphors: zero.** No `star`, `North Star`, `lodestar`, `celestial`, `constellation`, `orbit`, `sky`, `firmament`, or `horizon` in body prose. The only celestial content is the branded `☀️ Zenith` and the `🌅` in the Voyage Progress strip. "Lodestar Ledgers" at ~41 is the publisher attribution on the epigraph — a brand name, not a figure of speech.

## Overcooked passages

**None.** There is no stacking anywhere in the chapter. The three touches are maximally dispersed — line 1, line 181, and line 1187 — which is the opposite failure mode.

**No clichés found.** Targeted scan for `chart a course`, `set sail`, `smooth sailing`, `all hands`, `batten down`, `weather the storm`, `uncharted waters`, `steady as she goes`, `anchors aweigh`, `rough seas`, `learn the ropes`, `tight ship`, `rising tide`, `sea change`, `navigate the` returned **zero matches**. What theming exists is bespoke. That remains the chapter's strength on this axis, as it was in Chapter 4.

## Underseasoned passages

Two gaps dominate, and the second is the largest texture-free run measured in this book so far.

| Range | Approx. words | What's in it | Note |
|---|---|---|---|
| **L182–L1186** | **~9,500** (excl. question bank) | §2 body, §3, Bearings #1, §4, §5, Bearings #2, §6, §7, §8, Bearings #3, **§9 Zenith**, Exam Alert, Chapter Summary, The Voyage Ahead | **The chapter's entire teaching body carries no thematic texture at all.** Every section that does the actual instructional work — including §5, the declared centerpiece, and §9, the synthesis — is metaphor-free. |
| L2–L180 | ~2,400 | Attention Budget, Soundings, Why This Chapter Matters, What You'll Learn, **all of §1** | The title lands on line 1 and is then dropped for 180 lines. §1 establishes the shared-context idea — the exact concept the "vessel" image exists to carry — and never reaches for it. |

**Not flagged:** L887–L1144 (~3,200 words, Practice Questions and answer explanations). A question bank should be texture-free; adding metaphor there would be a defect, not a fix.

### The structural cause

**The chapter contains zero `Logbook Entry` and zero `Extended Analogy` sidebars.** The style ledger (LOCKED 2026-04-19) sets a combined frequency target of 1–3 per content chapter. Chapter 4 had one Extended Analogy, and that single sidebar carried most of its (already thin) thematic load. Chapter 5 has neither. The brand's formal vehicle for sustained metaphor is simply absent, which is the mechanical reason the chapter reads texture-less rather than merely light.

### Highest-value insertion points, in order

1. **§9 / Zenith (L815–853).** The synthesis states: *"the unit of scheduling wraps containers instead of being one."* That **is** the vessel image — a hull is not cargo; the ship is the thing that is crewed, addressed, and berthed, and the boxes in the hold are not. The chapter's own title conceit resolves exactly here and is left entirely unspoken. This is the single best insertion point in the chapter, and it is nearly free: the argument is already made, it just isn't imaged.
2. **§1 (L129–137).** "The Pod is the shared context, and the containers live inside it." This is where the title's promise should first be paid, and where one hull / one berth / one address is most naturally earned. Currently the end of a ~2,400-word texture-free run-up.
3. **§4 (L347–351).** "Replace, don't repair" is *already* the closing quote's idea, delivered 840 lines earlier in flat prose. One light touch here would make the L1187 quote read as a payoff rather than an image arriving from nowhere at the last line of the chapter.
4. **§7 (L582–590).** Readiness-versus-liveness maps cleanly onto watch-standing — being stood down from a watch versus being relieved of duty. Optional, but the book's role family is the Communications Officer and this is the chapter's most natural fit for that register.

### Scale-of-fix note — flagging a tension, not resolving it

Three or four added touches would bring the chapter to roughly **0.4–0.5 per 1,000**. That is a real improvement and still **below the ratified 1–3 band**. Reaching the band floor at this length requires ~15 overt metaphors, i.e. **+12 over current**. Forcing twelve insertions into a 15,000-word technical chapter risks precisely the caricature failure mode the guidance exists to prevent, so I am not recommending it.

Worth surfacing to the style ledger rather than deciding here: the 1–3/1000 band was locked 2026-04-18 against CAPM Ch 1, a much shorter orientation chapter. Applied to 15,000-word content chapters, band compliance means 15–45 overt metaphors per chapter. Chapters 4 and 5 have both landed at ~0.2–0.4 despite clean voice passes, which suggests the band may be miscalibrated for long content chapters rather than that two consecutive chapters were drafted carelessly. A `[DECIDE]` entry would be appropriate.

### One low-cost, high-yield conversion

The chapter's most conspicuous repeated figure is **musical, not nautical**: `Movement one` / `Movement two` / `Movement three` in §5 (L363, L375, L416) and `Movement one` through `Movement four` in §8 (L642, L660, L675, L704) — **7 instances**.

Renaming these to **`Leg`** (a leg of a passage) is in-register, collides with no branded marker, and is a one-word substitution requiring no prose surgery. It alone would take the chapter from 3 metaphors to 10 (**~0.67 per 1,000**); combined with recommendations 1–3 above, roughly **0.9 per 1,000** — at the band's doorstep with minimal risk.

Do **not** use "Passage" for this — it collides with 🌊 Passage in the Voyage Progress strip.

### Cross-chapter observation

Chapter 4's audit noted that its only consistent figurative register was **financial** rather than nautical. Chapter 5 repeats the pattern in a different key. The chapter is not figuratively flat — it is richly figurative in registers that aren't the brand's:

- **musical** — "Movement one/two/three/four" ×7
- **debt / obligation** — "What a Pod Is Owed" (L636), "worth banking" (L204), "§7 pays it" (L171), "the published promises this chapter collects" (L88), "comes due" (L359) ×5
- **architectural** — "load-bearing fact" (L131), "load-bearing work" (L551), "load-bearing wall" (L851) ×3
- **carceral** — "serving its backoff delay" (L460), "bounded penalty, earned amnesty" (L442)
- **dramaturgical** — "The readiness behavior is a forward plant" (L630)

That is ~18 deliberate figures of speech in registers outside the brand, against 3 inside it. This is now a **two-chapter pattern**, and it is the more actionable finding than the raw density number: the voice stage is producing vivid prose, but its metaphor instinct is not reaching for the brand's vocabulary. Recommend escalating to the voice pass as a systematic note rather than treating it as a per-chapter cleanup.

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / hearties | 0 | — |
| ye (as pronoun) | 0 | — |
| avast | 0 | — |
| arr / yarr | 0 | — |
| savvy | 0 | — |
| landlubber / lubber | 0 | — |
| scallywag | 0 | — |
| booty / plunder / pillage | 0 | — |
| bilge | 0 | — |
| swab | 0 | — |
| doubloon | 0 | — |
| buccaneer / corsair | 0 | — |
| belay | 0 | — |
| grog / cap'n / jolly roger | 0 | — |

Clean. No caricature register anywhere in the chapter.