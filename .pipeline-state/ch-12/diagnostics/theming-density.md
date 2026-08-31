Analysis complete. Here is the deliverable.

```markdown
# Theming-Density Audit — Chapter 12

Audited file: `.pipeline-state/ch-12/draft-v1.md` (1,763 lines). `draft-voice.md` does not
exist at this stage; all line numbers below are against `draft-v1.md`.

## Summary

- Total word count (body prose only, excluding code blocks and tables): **~24,800**
- Overt nautical/celestial metaphors outside branded markers: **11**
- Density: **0.44 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Word-count derivation.** 28,143 whitespace tokens in the file, less 923 in the seven fenced
figure blocks (194–229, 294–328, 399–446, 877–928, 1005–1009, 1064–1090, 1338–1369), less
1,418 in table rows, less 309 in the six `<!-- FIGURE -->` / five `<!-- AUTHOR-REVIEW -->`
comments = 25,493. Netting out the citation apparatus (184 `[source: …]` tags and 38
`*[cross-bearing: …]*` pointers, ~650 tokens) gives ~24,800 words of actual prose. At the
1-per-1000 floor the chapter would want ~25 instances; it has 11.

**The distribution matters more than the total.** Eight of the eleven instances sit in two
passages — the Extended Analogy sidebar (118–124) and one sentence at 1092. Everything
between them, §1 through §6 plus two checkpoints, is ~14,700 words with no thematic texture
at all.

## Catalog of metaphors

| Line | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 1 | "Chapter 12: Locks, Keys, and **Watchstanders**" | nautical — shipboard watch | acceptable — series title convention, and it is the promise the sidebar keeps |
| 118 | "A **ship** carries locks, keys, and watchstanders, and the reason all three exist is that no one of them does the others' work." | nautical — vessel | acceptable — Extended Analogy thesis sentence; does real structural work (three panels → §2, §4, §8) |
| 120 | "a piece of metal that proves you are the person the **quartermaster** issued it to" | nautical — shipboard role | acceptable |
| 120 | "the **ship's manifest** of who holds which key, kept somewhere else entirely" | nautical — shipboard records | acceptable — earns its place; the manifest/RBAC-binding parallel is load-bearing, not decoration |
| 124 | "A **lookout at the masthead** has no authority to alter course." | nautical — watchkeeping | acceptable |
| 124 | "has no authority to **alter course**" | nautical — navigation | acceptable — literal shipboard usage, not the "chart a course" cliché |
| 124 | "one of them **stands on deck** and tells you what already happened" | nautical — shipboard | acceptable |
| 1092 | "Admission is the cluster's **gangway**: the one place it gets to inspect the cargo before it comes aboard." | nautical — ship access | acceptable — the strongest single figure in the chapter; it explains a section-ordering decision |
| 1092 | "inspect the **cargo** before it comes **aboard**" | nautical — cargo handling | acceptable — same sentence, same figure |
| 1188 | "## §8 — Rules That **Watch**" | nautical — ship's watch (puns on the Kubernetes `watch` verb) | acceptable — mild, and it collects the sidebar's third panel |
| 1241 | "This is the **watch at the masthead**, and it pays to be precise about what that is worth." | nautical — watchkeeping | acceptable — closes the Falco-detects-not-prevents argument on the image that opened it |

### Considered and not counted

Recorded so a later pass does not re-litigate them.

- **"ship / ships / shipped" in the software-release sense** — lines 14, 112, 116, 492, 614,
  800, 1055 (§7 title "Trusting What You Ship"), 1393, 1415. Vocabulary overlap, not figure
  of speech (rule 4). The §7 title is a free pun the brand gets without spending anything.
- **"strongbox" (122) and "did not ship with a lock fitted" (614, 620)** — genuine sustained
  callbacks to the sidebar, but the imagery is generic-security, not nautical or celestial.
  Not counted; worth knowing they are the chapter's only cross-section conceit that survives.
- **"Helm charts" (1393)** — product name. **"port" (784, 932)** — technical.
- **"watch" as the Kubernetes API verb** — 458, 640, 696, 980; and "**Watch** what you
  assign" (834), ordinary English imperative.
- **"bearing"** — 30 of 33 occurrences are the `*[cross-bearing: …]*` convention; the rest are
  "load-bearing" (962) and "bearing the token" (313, inside a figure).
- **Cross-bearing pointers quoting other chapters' section titles** — "when the berth refuses
  you" (158, 830), "three gates and a logbook" (82, 267, 846, 1211). Structural apparatus
  citing Ch 7 and Ch 8; the metaphor was authored there, not here.
- **Branded markers, excluded by rule 1** — 🧭 Soundings (51), ☆ Taking Your Bearings (23, 27,
  31, 551, 974, 1259), — Dead Reckoning (116, 375, 941), ★ Fixed Point, ⚠ Navigational
  Hazards, ☀️ Zenith (1325, 1373), 🏆 Safe Harbor (1754), The Voyage Ahead (35, 1738), the
  Voyage Progress strip "Chart, passage, dawn: 🗺️ → 🌊 → 🌅" (1762), and the margin icons
  ⚓ Worth Securing / 🪝 Snag / 🔭 Closer Look / 🪢 Mnemonic.

## Overcooked passages

**None.**

The only passage with high local density is the Extended Analogy at 118–124: six instances in
~330 words, ~18 per 1000 locally. That is not overcooking. `style-decisions.md`
[LOCKED 2026-04-19] defines Extended Analogy as the brand's long-form-metaphor sidebar; a
sustained figure is the format's entire function, and the local rate should not be measured
against a whole-chapter band. The sidebar is also disciplined: three panels, each mapping to a
named Kubernetes confusion (key ≠ permission, strongbox ≠ safe, watch ≠ prevention), each paid
off later in the chapter. Nothing in it is ornament.

Line 1092 stacks gangway / cargo / aboard, but that is one coherent image in one sentence, not
three metaphors competing. Leave it.

## Underseasoned passages

Three stretches over 800 words carry zero thematic texture. The middle one is the finding.

| Lines | Content | Prose words | Texture |
|---|---|---|---|
| 2–117 | subtitle → Attention Budget → 🧭 Soundings → Why This Chapter Matters (up to the sidebar) | ~1,850 | none |
| **125–1091** | **§1 Four Layers and Four Phases → §2 Who You Are → §3 What You May Do → ☆ Bearings #1 → §4 Secrets → §5 What a Pod May Do to Its Node → §6 Three Levels, Three Modes → ☆ Bearings #2** | **~14,700** | **none** |
| 1242–1763 | §8 close → ☆ Bearings #3 → §9 Additive, Never Deny → Exam Alert → Practice Questions → Chapter Summary → The Voyage Ahead → 🏆 Safe Harbor | ~6,500 | none outside branded markers |

The 14,700-word stretch is the problem. It is 59% of the chapter, it contains the material the
chapter exists for, and it reads as competent technical prose with the brand switched off. A
reader who opened at §3 and closed at §6 would have no way to tell which publisher's book they
were holding.

Two qualifications, so this is not read as a call to sprinkle:

- **The last three stretches are not equally at fault.** Practice Questions (1462–1656),
  Answers (1657–1702) and the Chapter Summary table (1703–1736) should stay texture-free;
  metaphor in a distractor or a summary row is noise. Exclude those ~4,000 words and the tail
  gap is ~2,500, which is ordinary.
- **The chapter already owns the fix.** It does not need new imagery. The Extended Analogy set
  up three panels and then abandoned two of them: the *key* panel is about ServiceAccounts and
  §2 never returns to it; the *strongbox* panel is about Secrets and §4 touches it once, in
  passing, at 620. Only the *watch* panel gets paid off (1188, 1241), and that pairing is the
  best-textured part of the chapter — which is the evidence that the technique works here.

**Recommended, in priority order** — eight to ten short callbacks, one sentence each, at seams
where the conceit is already true:

1. **§2, near line 237 or 267** — the "a key opens nothing until the manifest says it does"
   beat. §2's entire argument *is* the sidebar's first panel; it is currently stated in
   abstract terms only. Highest value, lowest cost. Put it in the body prose, not inside the
   ★ Fixed Point at 261–265 — Fixed Points stay flat.
2. **§4, near line 672** ("Encryption at rest, and what it buys") — the strongbox finally
   getting a lock fitted, and the honest accounting that a lock on the box does nothing about
   who is handed the box. The chapter makes exactly this argument and makes it bare.
3. **§9, near line 1381 or 1417** — the synthesis section has no texture at all outside the
   ☀️ Zenith marker. One image for "a rule whose meaning depends on rules you have not read"
   would close the chapter in register rather than in the abstract.
4. **§5, near line 749** ("The default position") — the workload-to-host boundary is the one
   axis with no image attached anywhere in the chapter.
5. **§6, near line 950** ("The namespace as a control surface") — optional; skip if 1–4 land.

Landing 1–5 would put the chapter near 0.7–0.8 per 1000 — still under the band, and that is
the right place to stop. Reaching 1.0 mechanically would mean ~14 more instances than the
material wants, and a padded chapter is a worse failure than a spare one. Flag the residual
gap to the author as a judgment call rather than closing it by volume.

## Pirate-vocabulary check

Checked against the full `forbidden_patterns` list in `structural-contract.yaml` (both the
FAIL-level "Pirate caricature vocabulary" pattern and the `expected`-level "Nautical cliche"
pattern), plus a wider sweep.

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / me hearties | 0 | — |
| ye (as pronoun) / ye be / yer | 0 | — |
| yarr / arr / avast | 0 | — |
| scurvy / landlubber / plunder | 0 | — |
| shiver me timbers / davy jones / walk the plank | 0 | — |
| buccaneer / corsair / swashbuckling / doubloon / grog / cutlass / jolly roger / scallywag | 0 | — |
| smooth sailing | 0 | — |
| weather the storm | 0 | — |
| all hands on deck | 0 | — |
| chart a course | 0 | — |
| set sail | 0 | — |
| batten down the hatches | 0 | — |
| uncharted waters | 0 | — |
| plain sailing | 0 | — |
| stay the course / on the horizon / north star / full steam ahead / tip of the iceberg | 0 | — |

Clean on both patterns. Note that the chapter's one navigation phrase, "alter course" (124),
is deliberately *not* "chart a course" — it is literal shipboard usage in a passage about a
lookout who cannot give that order. It reads as register, not as theme-dressing, and should
not be swept up by a future tightening of the cliché pattern.
```