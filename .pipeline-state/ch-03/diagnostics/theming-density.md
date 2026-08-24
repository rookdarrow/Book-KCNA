Write access to the book tree isn't granted in this session, so per the pipeline's stdout-capture design (`Write` is deliberately outside `--allowed-tools`), here is the stage output for the orchestrator to persist to `.pipeline-state/ch-03/diagnostics/theming-density.md`:

---

# Theming-Density Audit — Chapter 3

**Book:** KCNA · **Chapter:** 3, "The Ship's Company" · **Source:** `.pipeline-state/ch-03/draft-v1.md` (voiced draft, 1,077 lines)

## Summary

- Total word count (body prose only, excluding code blocks and tables): **≈13,400**
- Overt nautical/celestial metaphors outside branded markers: **7**
- Density: **0.5 per 1000 words**
- Target band: 1–3 per 1000 words
- Status: **underseasoned**

**Counting method.** `wc -w` on the whole file gives 14,761. Subtracted: four fenced ASCII diagrams (~290 words), four markdown tables totalling 50 lines (~830 words), and three `AUTHOR-REVIEW` / four `FIGURE` HTML comments (~260 words). Remainder ≈13,400. The subtractions are line-counted and word-estimated, so treat the denominator as ±3%; it does not change the verdict.

**Two readings of the numerator, both worth seeing.** The Extended Analogy at L647–655 is one sustained figure developed across five paragraphs. Counted as a single deliberate metaphor (the reading used above), the chapter scores 7 → **0.5/1000**. Decomposed into its constituent images (wardroom, the sea, helmsman/compass/ordered course, lookout/horizon, engineer/gauge, ratings, the vessel on course, the voyage), the chapter scores ~14 → **1.0/1000**, which lands on the floor of the band. Either way the chapter sits at or below the bottom of the target, and every reading above 0.5 depends entirely on one sidebar.

**Zero celestial metaphors.** No stars, North Star, lodestar, constellation, orbit, or sky imagery appears in body prose. `☀️ Zenith` (L745) and `🌅` in the Voyage Progress strips are branded markers and excluded. The chapter's theming is 100% nautical.

## Catalog of metaphors

| Line (approx) | Passage excerpt | Metaphor category | Verdict |
|---|---|---|---|
| 1 | "Chapter 3: The Ship's Company" | nautical — crew/company | acceptable — apt; components-as-crew is the chapter's controlling idea |
| 2 | "Everyone aboard has one job, and none of them is 'be in charge'" | nautical — crew/company | acceptable — carries the thesis, not decoration |
| 337 | "☆ Taking Your Bearings: **The Ship's Company**" | nautical — crew/company | acceptable, but an echo — third deployment of the same image, and the marker is already branded |
| 647–655 | "A ship's company is not a workflow … the sea does not consult it … The helmsman's standing order is a heading … The lookout's standing order is a horizon … No one aboard is running the voyage." | nautical — extended analogy (sustained) | **earns its place** — sanctioned `Extended Analogy` sidebar; L655 supplies its own justification; the helmsman image is doubly apt given Kubernetes' etymology |
| 773 | "It keeps the containers it already knows about running, because that was never an instruction. **It was a standing comparison.**" | nautical — callback to "standing orders" | strong — the analogy paying off inside technical prose; best-integrated instance in the chapter |
| 1070 | "You've met the crew and you know how they coordinate." | nautical — crew/company | acceptable — closes the frame opened by the title |
| 1078 | "*The vessel arrives on course not because someone executed a plan, but because a hundred small corrections were made continuously…*" | nautical — reprise of the analogy | acceptable as a closing quote (see consistency note below) |

### Considered and not counted

| Line | Passage | Why not counted |
|---|---|---|
| 202 | "The brand you're reading did not pick the maritime register to be cute about it. The subject arrived that way." | Not a metaphor — a meta-comment *about* the theming. See note below. |
| 202, 1048 | "the Greek word for helmsman or pilot" | Sourced etymological fact, not a figure of speech |
| 469 | "Not a chain of command. A hub." | Functional — standard vocabulary for a hierarchical architecture (Rule 4) |
| 1024 | "until you've **anchored** the real pair" | Borderline. Nautical word doing figurative work, but reads as standard cognitive-science "anchoring" vocabulary in a pedagogy sentence. Excluded under Rule 4; flag if a reviewer disagrees. |
| 459, 803 | "is not **shipped** by default" / "Does not **ship** middleware" | Functional — software-release vocabulary |
| 498–514, 601, 1060 | "watching, not telling," "anything watching," "watches the API server" | Functional — the chapter's core *technical* claim, not lookout imagery |
| 787 | "🏆 Safe Harbor reached" | Branded marker (Rule 1) |
| 414, 587, 739 | "🗺️/🌊/🌅 Chapter 3 · Voyage Progress" | Branded marker (Rule 1) |
| 39, 17–22, 118+, 438, 1068 | Soundings, Taking Your Bearings, cross-bearing tags, Navigational Hazards, The Voyage Ahead | Branded markers and conventions (Rule 1) |

## Overcooked passages

**None.** No passage stacks multiple overt metaphors where one would do.

The one candidate — the Extended Analogy at L647–655 — is explicitly *not* overcooked. It is the sanctioned container for exactly this kind of density (`Extended Analogy` sidebar, locked 2026-04-19, 1–3 per content chapter; this chapter uses one), the metaphors inside it are all facets of a single coherent figure rather than a pile-up of unrelated images, and L655 states why the analogy belongs in a sidebar rather than in the prose. Leave it alone.

**Cliché check: clean.** No "chart a course," "set sail," "smooth sailing," "uncharted waters," "weather the storm," "all hands," "even keel," "batten down," or "steady as she goes" anywhere in the chapter. "Arrives on course" (L653, L1078) is the closest call, and it survives because the helmsman is literally comparing a compass to an ordered course two sentences earlier — it's operating machinery in the analogy, not ornament. This is a notably disciplined result for a chapter whose title is a nautical metaphor.

## Underseasoned passages

Four runs exceed 800 words with zero thematic texture. Two of them are defensible; two are the reason for the verdict.

| Range | Content | ≈Words | Assessment |
|---|---|---|---|
| L36–L336 | Epigraph, Soundings, Why This Chapter Matters, What You'll Learn, §1, §2, §3 | **≈5,300** | **The problem.** The longest bare run in the chapter, and it spans the whole component census. Title and subtitle set up a ship's-company frame at L1–2, then the frame vanishes for 5,300 words and does not return until the checkpoint heading at L337 reuses the title verbatim. |
| L338–L646 | §4, §5, checkpoint #2, §6 opening through the ★ Fixed Point | **≈4,900** | **The problem.** Includes §5 ("The Only Door In"), the chapter's structural pivot, which is entirely texture-free. |
| L656–L772 | §6 desired-vs-current, checkpoint #3, §7 opening | ≈1,300 | Acceptable — bounded on both sides by the analogy (L647–655) and its callback (L773). |
| L774–L1069 | Exam Alert, 19 Practice Questions + answers, Chapter Summary | ≈3,300 | **Expected and correct.** Assessment apparatus. Do not add texture here; metaphor in answer explanations degrades them. |

**Does the chapter feel texture-less overall? No — but not because of its metaphors.** Three mitigating facts a reviewer should weigh before acting:

1. **Branded-marker density is high.** Three `☆ Taking Your Bearings` checkpoints, three Voyage Progress strips, three `★ Fixed Point` blocks, `🧭 Soundings`, `☀️ Zenith`, `🏆 Safe Harbor`, `— Dead Reckoning`, and eleven margin icons (⚓ ×4, 🪝 ×2, 🔭 ×2, 🪢 ×1, ⚠ ×3). The *felt* brand texture is well above what the metaphor count implies. Markers correctly don't count for this audit, but they do count for the reader.
2. **The subject supplies its own nautical anchor.** Kubernetes means helmsman. L202 is right that the register wasn't imposed.
3. **The scarcity is partly principled.** §5 and §6 are the chapter's load-bearing technical sections, and they're written in deliberately plain, high-precision prose. That's a defensible trade, not an oversight.

**The sharper finding is monotony, not scarcity.** Five of the seven counted metaphors are the *same* metaphor — ship's company / crew / aboard — deployed at the title, subtitle, a checkpoint heading, the Extended Analogy, and the "Voyage Ahead" opener. The chapter has one image, used five times, mostly at structural positions rather than inside the prose that needs it. Adding volume without adding variety would make this worse.

**Recommendation — 3 light additions, placed inside prose, not at structural positions:**

- **L212, §2 opening** ("Start with the shape of the thing.") — the control-plane/node split is introduced completely bare. One image here would seed the ship's-company frame at the moment the census begins, so L337's callback lands as a return rather than a repeat.
- **L469, §5** ("Not a chain of command. A hub.") — the chapter's structural pivot and its most quotable line, currently unthemed. This is the highest-value single insertion point in the chapter.
- **L665, §6** ("A cluster that is never quite finished reconciling isn't malfunctioning…") — the "never reaches a stable state" idea is the chapter's most counterintuitive claim, and a vessel underway is a natural image for it. Would also pre-load the Extended Analogy 20 lines later.

Three additions bring the count to 10 (≈0.75/1000, or ≈1.3/1000 on the decomposed reading). That is a deliberate stop short of the band's midpoint: this chapter's technical density is high, its marker density is high, and pushing to 2–3/1000 would require padding §2/§3's component definitions, which are near-verbatim documentation and should stay that way. **Do not add texture to the Practice Questions, the answer explanations, or the Chapter Summary table.**

## Pirate-vocabulary check

| Term | Occurrences | Action |
|---|---|---|
| ahoy | 0 | — |
| matey / mateys | 0 | — |
| ye (as pronoun) | 0 | — |
| arr / yarr / avast | 0 | — |
| hearties / scallywag / landlubber | 0 | — |
| booty / plunder / doubloon / grog | 0 | — |
| swashbuckling / buccaneer / cutlass | 0 | — |
| "shiver me" / "walk the plank" / jolly roger | 0 | — |
| thee / thy / o'er / cap'n | 0 | — |

**Clean.** No caricature register anywhere in the chapter. The one place the draft could have slipped — the Extended Analogy's crew roles — stays in a professional naval register (helmsman, lookout, engineer, ratings, wardroom, standing orders) rather than a costume one.

## Notes for other stages

Out of scope for this audit, surfaced because both concern the metaphor's own text:

- **L653 vs L1078 — the chapter misquotes itself.** The Extended Analogy reads "a **few dozen** small corrections"; the closing quote presents itself as a quotation of that sentence but reads "a **hundred** small corrections." Same sentence, two numbers. Pick one.
- **L202 — meta-comment on the register.** "The brand you're reading did not pick the maritime register to be cute about it. The subject arrived that way." This is a fourth-wall break about brand construction, not a metaphor, so it isn't counted here. It's defensible given the helmsman etymology — but it's the only line in the chapter that steps outside the narrator's frame to discuss the brand as a brand. Worth a voice/register reviewer's eye, not this audit's.
- **Register era.** "Wardroom" and "ratings" are age-of-sail Royal Navy terms. KCNA sits in the Communications Officer family alongside CKA, which `illustrator-brief.md` places in the early-interstellar era. Both terms survive the translation to a fleet register, so this is an observation rather than a finding — but if KCNA's era placement is being fixed, the Extended Analogy is where it shows.

---

Two things worth flagging about the run itself: the prompt's inline copy of the voiced draft came through as `[file not available: draft-voice.md]`, so I resolved the draft from `pipeline_state.yaml` — the ch-03 voice stage wrote back to `draft-v1.md` (pre-voice preserved as `draft-v1-prevoice.md`), not to `draft-voice.md` as ch-01 did. And `Write`, `python`, and inline shell scripting were all blocked here, so the word counts are line-counted subtractions from `wc -w` rather than a scripted parse; the ±3% uncertainty doesn't move the verdict.