# Theming-Density Audit — Chapter 7

**Chapter:** KCNA Ch 7 — *Assigning the Berth*
**Audited file:** `.pipeline-state/ch-07/draft-v1.md` (1,123 lines)
**Status:** underseasoned — approximately one third of the target floor

> **Input note.** The prompt's `{{draft_voice}}` slot resolved to `[file not available: draft-voice.md]`. That is expected pipeline behaviour, not a missing artifact: `apply_voice_swap()` (`pipeline/orchestrator.py:250`) renames `draft-voice.md` into the canonical `draft-v1.md` slot after Stage 4 completes, keeping the un-voiced text as `draft-v1-prevoice.md`. This audit ran against `draft-v1.md`, which *is* the voiced draft (mtime 10:07, matching the Stage 4 progress log). `context_packer.py:216` maps `draft_voice → draft-voice.md`, so every downstream stage that requests the voiced draft by that key gets an empty substitution — worth fixing at the packer, not per-stage.

## Summary

- **Total word count** (body prose only; excludes fenced code/figure blocks, markdown table rows, `<!-- AUTHOR-REVIEW -->` editorial comments, and inline `[source: …]` citation tags): **~13,760**
  - Derivation: 16,079 raw − 1,105 table rows − 668 fenced-block words − 319 editorial-comment words − ~232 citation-tag tokens
- **Overt nautical/celestial metaphors outside branded markers: 6** (5 in reader-facing prose, 1 in a figure label)
- **Density: 0.4 per 1,000 words** (0.36 counting prose only)
- **Target band: 1–3 per 1,000 words**
- **Status: underseasoned** — the chapter would need roughly 14 instances to reach the floor and carries 6

Five of the six instances are a single recurring conceit (*berth*), and all five sit in **structural positions** — title, two section headings, epigraph, closing quote. The body prose itself is very nearly texture-free.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| ~1 | "Chapter 7: **Assigning the Berth**" | nautical — berthing/mooring | acceptable — opens the conceit; specific, not cliché |
| ~36 | "The hard part of assigning **a berth** is not choosing well. It is that you only choose once." | nautical — berthing | acceptable — epigraph carries the chapter's actual thesis (irreversibility), not decoration |
| ~318 | "§3 — Asking for a Particular **Berth**" | nautical — berthing | acceptable |
| ~410 | "§4 — When the **Berth Refuses** You" | nautical — berthing, personified | acceptable — the personification is doing real pedagogical work; it previews the taint/toleration direction inversion |
| ~458 | "Pod C: already **aboard**, no toleration" | nautical — shipboard | acceptable — figure label; the only in-register touch anywhere inside §4's 1,798 words |
| ~1119 | "You cannot move **a berth** once it is assigned. You can only be careful about what you said before it was." | nautical — berthing | acceptable — closes the frame opened at line 1 |

**Assessed and deliberately not counted:**

| Line (approx) | Passage | Why not counted |
|---|---|---|
| ~55 | "Some machines in your **fleet**" | Functional vocabulary. "Fleet" is standard infrastructure idiom (server fleet, fleet management), not a deliberate figure of speech — rule 4. |
| ~838 | anchor slug `ch07-zenith-berth-assignment` | Machine-readable figure ID, never rendered to the reader. |
| ~610 | "§5 **changes altitude**" | A live figure of speech, but aeronautical — outside the nautical/celestial budget. See register note below. |
| ~726, ~744 | "the **seat** is pluggable" | Furniture register. |
| ~870 | "wearing a specialised **hat**" | Clothing register. |
| throughout | 🧭 Soundings · ☆ Taking Your Bearings · ★ Fixed Point · ⚠ Navigational Hazards · — Dead Reckoning · ☀️ Zenith · 🏆 Safe Harbor · 🗺️→🌊→🌅 · ⚓ Worth Securing · 🪝 Snag · 🔭 Closer Look · 🪢 Mnemonic · Logbook Entry · *[cross-bearing: …]* · "The Voyage Ahead" | Branded structural terminology — excluded per rule 1. All are correctly named and correctly paired with their symbols; no drift ("Shoals Ahead", "Landfall", `⚓→★→🏆`) detected. |

## Overcooked passages

**None.** There is no passage in this chapter where two or more overt metaphors stack. The six instances are separated by 300–4,000 words each. No cliché nautical phrasing is present either — a targeted scan for *chart a course, set sail, smooth sailing, weather the storm, uncharted waters, stay the course, even keel, rising tide, sink or swim, full steam, all hands, batten down, north star, guiding star, shipshape* returned zero matches.

The *berth* conceit specifically earns its keep rather than reading as brand tax: a berth is a real assigned position at a real physical location that you cannot change once allotted, which is precisely the exam-critical fact the chapter is built on ("a Pod is scheduled once in its lifetime"). The metaphor and the mechanism are load-bearing on each other. That is the pattern to preserve.

## Underseasoned passages

This is the chapter's actual finding. Four stretches well over the 800-word threshold carry zero on-brand thematic texture:

| Lines | Span | Words | On-brand touches |
|---|---|---|---|
| ~550–826 | ☆ Bearings #2 → end of ☆ Bearings #3 (spans **all** of §5 and §6) | **4,002** | 0 |
| ~94–316 | Why This Chapter Matters → end of ☆ Bearings #1 (spans **all** of §1 and §2) | **3,445** | 0 |
| ~874–1069 | Exam Alert + Practice Questions | **3,009** | 0 |
| ~41–92 | 🧭 Soundings + answers | **873** | 0 ("fleet" is functional) |

Two qualifications, so the revision stage weights this correctly:

1. **The Exam Alert / Practice Questions stretch (~3,009 words) should stay dry.** Assessment and reference material is the wrong place for figurative language — a metaphor inside a distractor is a comprehension hazard. Do not season this stretch. Excluding it, the reader-facing narrative body is ~10,750 words carrying 6 metaphors: **0.56 per 1,000**, still well under the floor.

2. **The chapter is not texture-*less*; its texture is in the wrong register.** §2 runs a sustained and genuinely good extended metaphor — *booking*, *ledger*, *balance*, "read that again with an accountant's eye", "sixteen booked out of sixteen", "the scheduler books; it does not measure". It is the most vivid writing in the chapter and it is doing the heaviest teaching. It is simply an **accounting** metaphor, not a nautical/celestial one, so it contributes nothing to this budget. The same is true of "changes altitude", "the seat is pluggable", and "wearing a specialised hat" — the authorial instinct to reach for figuration is clearly present and firing; it is just reaching outside the brand register.

**Recommended remedy — 4 to 6 additions, not 8.** Aim for the low end of the 1–3 band (~1.0/1,000 ≈ 11–14 instances total) rather than the middle. This chapter's material is dense discrimination work, and the existing frame is strong enough that heavy seasoning would read as applied rather than native. Highest-value placements, in priority order:

- **§4 body (~1,798 words, currently one figure label).** Lowest-risk target by a wide margin: the register is *already live* here in the prose — "the node's refusal", "an exemption from that refusal", "keep everyone else off", "pulls the right work on". Extending berth/harbour vocabulary one or two beats into the taint/toleration explanation costs nothing in precision because the personification is already doing the work.
- **§1's "The decision is irreversible" (~lines 183–191).** This is the thesis paragraph of the whole chapter and the epigraph's berth line is sitting three hundred words above it, unclaimed. One touch connecting them would make the frame feel authored rather than bolted on.
- **The Logbook Entry (~lines 530–541).** A narrative sidebar is the most natural home for register in the entire chapter, and this one — eight GPU nodes, a team, a four-month wait — currently has none.
- **§5's opening failure scene (~lines 618–624)** — "Two replicas … Both land on the same node." One in-register beat here would land, since the loss being described (redundancy) is intuitively spatial.

**Two cautions for the revision stage:**

- **Do not season §5's `topologyKey` material.** "Domain", "zone", "region" and "node" are being carefully distinguished as a variable versus its values, and that is explicitly the hard idea in the section (flagged 🟡 for exactly this reason). Harbour/berth/anchorage vocabulary layered on top would collide with the technical taxonomy and cost more comprehension than it buys.
- **Do not convert §2's accounting metaphor to nautical.** It works, it is memorable, and "ledger" is not off-brand in any case — the publisher is *Lodestar **Ledgers***, and a ship's ledger is a log, not an anachronism. Raising density should mean *adding* in dry stretches, not *replacing* the one extended metaphor that is already succeeding. (Whether the accounting register should be formally ratified as brand-adjacent is a `style-decisions.md` question, not this audit's call.)

## Pirate-vocabulary check

Zero occurrences. Clean.

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / mateys | 0 | — |
| ye (as pronoun) | 0 | — |
| avast | 0 | — |
| arrr | 0 | — |
| scallywag | 0 | — |
| landlubber | 0 | — |
| hearties | 0 | — |
| booty / plunder | 0 | — |
| swab / bilge | 0 | — |
| grog / doubloon | 0 | — |
| thee / thy / hath | 0 | — |

Register is correct throughout: seasoned navigator, calm and precise, with the wry beats present but sparing ("and they're printed on the front of this chapter", "nobody is going to tell you when you get it wrong", "plausible-sounding nonsense"). No caricature drift, no aetheric/fantasy drift, no cutesy-mascot drift.