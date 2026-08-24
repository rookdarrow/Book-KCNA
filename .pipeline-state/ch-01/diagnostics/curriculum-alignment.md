`Write` is gated in this stage (as CLAUDE.md documents — stage output flows through stdout for atomic capture by the orchestrator). Emitting the artifact below, following the same convention the research stage used.

---

**Harness note.** `Write` to the diagnostics path was denied, so this stage's output is stdout. Two input resolutions were needed first: (1) `draft-voice.md` does not exist — the voice stage wrote back to `draft-v1.md`, with `draft-v1-prevoice.md` as the backup; that is the file audited. (2) Auditing against `sources/` revealed that the research stage's corrected snapshots were never written to disk, which changes the finding materially. Detail in the Gaps section.

---

# Curriculum-Alignment Audit — KCNA Chapter 1

**Draft audited:** `.pipeline-state/ch-01/draft-v1.md` (voiced output).
**Authority:** cached snapshots in `../Book-KCNA/sources/` (84 files, all `fetched_at 2026-08-23`), cross-read against `.pipeline-state/ch-01/research-manifest.md`.
**Chapter type:** `orientation` · `exam_domain: None` · `domain_weight_pct: 0`.

**Verdict: PASS on objective coverage, with one blocking gap-handling failure inherited from the research stage.** The chapter claims zero exam objectives and correctly covers zero. Every *current*-blueprint fact validates cleanly against the cached snapshots. The failure is in §3's *retired*-blueprint column, which the research manifest explicitly ruled un-draftable and the draft drafted anyway.

---

## Objectives the outline claims to cover

The outline claims **none**. `exam_domain: "None — orientation chapter, no domain objectives"`, `domain_weight_pct: 0`, `kb_tags.objectives: []`, and all six body sections carry `objectives: []`.

This is correct against the authority. The KCNA blueprint (`lf-kcna-exam-page-2026-08-23`, `cncf-kcna-curriculum-pdf-2026-08-23`) defines four domains and eleven competencies, and **none is about exam mechanics, blueprint history, or study method.** An orientation chapter is by construction out-of-blueprint. There is no objective for it to under-cover.

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| — | *No objective claimed by the outline* | n/a | n/a |

**Coverage of the outline's own stated outcomes** (outline §2, retained there "for the audit stages") — not exam objectives, but what the chapter promised:

| Outline outcome | Delivered? | Where |
|---|---|---|
| Describe published format/duration/eligibility/validity; distinguish from commonly-reported figures | **partial** | §2 (lines 104–130) — mechanics correct; published/unpublished split mis-drawn. See Gap 2 |
| Name the four domains + weights; state what each absorbed or shed on 2025-11-24 | **partial** | §3 (lines 142–189) — current column correct and sourced; retired column unsourced. See Gap 1 |
| Detect whether third-party material targets current or retired blueprint | YES | §3 (lines 195–199), a genuinely operational 15-second test |
| Locate any chapter on the blueprint and any domain in the book | YES | §5 `ch01-fig02` (lines 302–319) |
| Choose a reading path calibrated to your starting point | YES | §6 (lines 376–384) |

---

## Objectives covered in the draft but NOT in the outline

All four instances sit in the **Soundings answer key and §4** — precisely where the outline predicted the pressure and posted a warning (*"the temptation to teach the correct answer properly will be strong. Don't. Those are other chapters' Fixed Points, and spending them here costs the payoff twice."*). Three of four held.

| # | Objective touched | Location | Assessment |
|---|---|---|---|
| 1 | **D1 Containerization** — container shares host kernel | Soundings A1, line 56 | **Within tolerance.** Outline sanctioned "correct distinction in one line + cross-bear to Ch 2." Draft does exactly that. No action. |
| 2 | **D1 Core Concepts** — orchestrator vs. runtime, *plus the reconciliation loop* | Soundings A2, line 58 | **Drift — act.** Orchestrator-vs-runtime is sanctioned. But *"watches whether reality matches your declared intent, and corrects the difference"* is the control loop the outline reserves as **Ch 3's Fixed Point**. The outline's spoiler check asserts Q2 does *not* give this away; this answer key makes that false. |
| 3 | **D4 Community and Collaboration** — Kubernetes governance | Soundings A3, line 60 | **Drift — act.** Delivers CNCF + Linux Foundation + 2015 Google donation + contributor scale, with two source tags. Ch 17 / D4.3 payload. Compounding: **A3 is the only Soundings answer with no cross-bearing** — the reader who misses it gets the answer but no destination, inverting the question's design purpose. |
| 4 | **D4 Ecosystem and Principles** — scope of "cloud native" | §4, line 281 | **Borderline — author's call.** The negative correction is sanctioned. The two illustrations that follow — *"A rack of hardware in your own building can be thoroughly cloud native. A fleet of rented cloud instances can fail every characteristic of the term"* — are positive claims about the CNCF characteristics, in a section the manifest says "must not acquire any [sources]." Unsourced by design, therefore unverifiable downstream. |

**Not drift, explicitly cleared:** §3's naming of Prometheus, OpenTelemetry, GitOps, Helm (lines 183–185) are signposts to where weight moved, not coverage. §1's scheduler/Pod mention (line 90) illustrates question *form*.

**Structural withholding — working as designed.** §4 does **not** state the CNCF definition; the plant-and-harvest structure the outline worried about (Open Question #4) survives intact. The Extended Analogy is used in the one section that permits it and nowhere else. This was the hardest thing the chapter had to do and it did it.

---

## Depth mismatches

**Weight-proportional analysis does not apply** — every topic here carries 0% exam weight. The honest analog is the outline's declared depth band (`focused`) and per-section plan.

| Content area | Exam weight | Outline plan | Draft depth | Mismatch |
|---|---|---|---|---|
| §1 What the KCNA is | 0% | ⚪ brief, open curiosity gap | proportionate | OK |
| §2 Published mechanics | 0% | ⚪ flat facts + one hazard | proportionate | OK |
| §2 Pricing detail | 0% | exam-only price + bundles without figures (Open Q#7; manifest concurs) | all three tiers, stated **three times** (lines 104, 112, 449) | **over-covered** |
| §3 Blueprint change | 0% | 🔵 chapter payload | correctly the densest section | OK |
| §4 "Cloud native" plant | 0% | "short by design" | ~430 words incl. 3-para analogy | slightly over, acceptable |
| §5 Book mechanics | 0% | ⚪ instrument panel | proportionate | OK |
| §6 Reading paths | 0% | ⚪ calibration | proportionate | OK |

**1. Runs long against its own band.** 6,629 words. The `focused` band is justified as "short enough to actually read before Chapter 2." At ~200 wpm the prose alone is ~33 min, before 10 questions, two answer-key blocks, and two figures. Realistic completion ~45–50 min, not the 35 claimed. Not a correctness defect — dense rather than padded — but the self-report under-states it.

**2. The Attention Budget table doesn't sum to its own total.** Nine section rows (lines 15–23) total **39 minutes**; header (line 11) says **~35**. Straight arithmetic error, independent of finding 1.

**Under-covered: nothing.**

---

## Gaps the research stage flagged

**Root cause — a pipeline integrity failure, not a drafting failure.** The research stage could not write files (sandbox blocked `Write`; manifest lines 1, 9–13). It emitted six snapshots to stdout — two *corrections*, four *new* — and asked for them to be written before Stage 3. **They never were.** Verified on disk:

- `lf-kcna-exam-page-2026-08-23.md` — still `fetched_at: 22:30`, not the corrected `23:50` re-fetch.
- `lf-kcna-program-changes-2026-08-23.md` — still `22:30`, and **still contains the misattributed `46%` retired weights** the correction was written to remove.
- `lf-mc-exam-faq-*`, `cncf-kcna-certification-page-*`, `cncf-curriculum-repo-kcna-versions-*`, `provenance-kcna-60-questions-*`, `cncf-kcna-curriculum-retired-*` — **all absent.**

The drafting stage read a stale, known-bad snapshot set and drafted faithfully from it. Its citations *do* validate against the files as they currently sit. **Fixing the prose without fixing `sources/` will regress on the next run.**

| Gap | Manifest status | Draft handling | Verdict |
|---|---|---|---|
| Retired five-domain weights | **OPEN — blocking `ch01-fig01`** | Drafted in full | **NOT handled — blocking** |
| Passing score is published (75%) | **Correction #1 — claim reversed** | Pre-correction framing retained | **NOT handled** |
| Question count | **CLOSED in the book's favour** | Handled correctly | **OK** |
| G31 — cert ladder | **CLOSED, resolves to option (a)** | Took option (b) | **Under-used** |
| G37 — LFS250 syllabus | Partially closed, no effect | Correctly unaffected | **OK** |
| Scoring methodology | Open, non-blocking | Not raised | **OK — and fortunate** |

### Gap 1 — retired blueprint weights: drafted against an explicit prohibition

The manifest (finding 3) wrote: *"**DO NOT draft the retired weights from memory or from third-party study guides**"* and *"§3 can state the structural change … but **not the retired percentages**, and `ch01-fig01` cannot be specced."*

The draft states all five (line 159), attributed to `lf-kcna-program-changes-2026-08-23` — the exact snapshot the manifest corrected *because the LF page never contained them*. The unsourced figures propagate through six further constructions: `ch01-fig01`'s entire left column and its −2/+6/×2 annotations (163–177); the three "what changed" claims (183–189); the 🪝 Snag on 16→12 (191); the "under-serve Application Delivery by roughly half" test (197); the Logbook Entry's whole premise (386–392); the Summary row (452).

Only the *structural* half of §3 is currently supportable: five domains → four, observability folded into Cloud Native Architecture. Both directly quotable from the LF page.

The manifest also recovered material §3 should have and doesn't: **the only date that matters is the date you sit the exam** (not purchase date, not first-attempt-vs-retake). That is the reader-facing consequence §3 exists to deliver.

### Gap 2 — the passing score: the draft asserts the reverse of the finding

Manifest finding 1 establishes the LF *does* publish it, verbatim: *"A score of 75% or above must be earned to pass the Multiple Choice Exam"* (`docs.linuxfoundation.org/tc-docs/certification/faq-mc`). Snapshot A3 lists the exact sentence to avoid: *"FALSE, do not write: 'The Linux Foundation does not publish a passing score.'"*

The draft writes materially that sentence three times — line 116 (bolded, the section's load-bearing claim), line 118, line 254.

**Owning stage:** fact-accuracy. Logged here because it determines whether the draft handled a research finding correctly, and it does not.

**Two things survive and should not be touched.** ☆ Bearings #1 Q2 (line 222) was narrowed to *"not published … **on the exam page**"* — exactly the disambiguation the manifest asked for, making C uniquely correct. Stem and explanation (line 248) are sound. And the manifest's framing is *better* than the draft's: the two numbers have **different provenance** — one published in a handbook most candidates never read, one published nowhere. The ⚠ Navigational Hazards block survives and gains a worked contrast.

### Gap 3 — question count: correctly handled
Six authoritative sources checked, none states it. Not merely unrefuted but positively well-evidenced. No change.

### Gap 4 — G31 cert ladder: closed, under-used
The outline recommended option (b) *"unless the research stage returns the catalog cheaply."* It did: CNCF's KCNA page states KCNA prepares candidates to *"pursue further CNCF credentials, including CKA, CKAD, and CKS,"* and supplies the multiple-choice-vs-performance-based contrast §1's "design decision, not a lesser version" argument rests on. §1 names only CKA (line 94). Not an error — the CKA citation is sound — but the trigger for option (a) was met. Author's call. **KCSA still must not be named here.**

### Gap 5 — scoring methodology: correctly avoided
The outline offered an optional 🔭 Closer Look on "why a body might decline to publish a passing score." The draft repurposed its Closer Look to pricing volatility instead. Given Gap 2, that speculation would have rested on a false premise.

---

## Recommended fixes

**Fix 0 gates 1 and 2** — do it first or the rest regresses.

**0. Land the research stage's snapshots before revising prose.** Write Appendix A of `research-manifest.md` to `../Book-KCNA/sources/`: replace A1 `lf-kcna-exam-page` and A2 `lf-kcna-program-changes`; add A3 `lf-mc-exam-faq`, A4 `cncf-kcna-certification-page`, A5 `cncf-curriculum-repo-kcna-versions`, A6 `provenance-kcna-60-questions`. A6 is evidence, **never** a citable source. Then retrieve `https://github.com/cncf/curriculum/raw/master/old-versions/KCNA_Curriculum%20old.pdf` and record its domain list as `cncf-kcna-curriculum-retired-2026-08-23.md`. That is the two-minute manual action the manifest asked for, and the only thing standing between §3 and correctness.

**1. §3 + `ch01-fig01` — resolve the retired column (blocking).** If fix 0's PDF retrieval succeeds, re-cite lines 159, 183–189, 191, 197, 452 to the new snapshot and the figure stands as drawn. If not, rewrite §3 to the structural change only, drop all five percentages and the −2/+6/×2 annotations, and respec `ch01-fig01` as the one-sided "what moved" diagram the manifest names as fallback. The Logbook Entry's premise survives qualitatively without the 8%/16% figures. **Do not** source the weights from the CNCF-hosted Medium repost — it is a syndicated guest post, precisely the diffusion mechanism §2 teaches readers to catch.

**2. §2 — re-cut the published/unpublished split (lines 116, 118, 254).** Replace with the two-provenance framing: the passing score **is** published — 75%, in the LF's multiple-choice candidate FAQ, not on the exam page most candidates read; the question count is published **nowhere**, across six authoritative sources. Cite A3. The hazard sharpens rather than weakens. Leave ☆ Bearings #1 Q2 and its explanation alone.

**3. §3 — add the sit-date rule.** Insert after line 189: neither purchase date nor first-attempt-vs-retake matters; only the date you sit. Cite A2.

**4. Soundings A2 (line 58) — stop short of the control loop.** Cut *"watches whether reality matches your declared intent, and corrects the difference."* Keep orchestrator-vs-runtime and the Ch 3 cross-bearing.

**5. Soundings A3 (line 60) — trim to calibration, add the missing cross-bearing.** Keep the one-line answer. Cut the 2015 Google donation and contributor-scale figures — Ch 17's D4.3 material, and the competency B1 flags as most under-studied, so it should arrive fresh. Add `*[cross-bearing: see Ch 17 §2 — CNCF governance and the project lifecycle]*`; this is the only answer in the set without one, and routing the reader forward is the question's whole purpose.

**6. §2 — collapse the pricing repetition.** State $250 exam-only with its snapshot date; name the two bundles without figures. Drop tier prices from Dead Reckoning (104) and the Summary row (449); keep the 🔭 Closer Look on volatility (112).

**7. Attention Budget — fix the arithmetic and the band.** Rows sum to 39, header says ~35. Reconcile, and raise the total to ~45 min to account for the questions and answer-key blocks the reading estimate omits.

**8. §4 (line 281) — author's call on the two illustrations.** Either soften to the negative correction alone ("it is not a statement about *where* the system runs"), or accept as authored framing and note the exemption for fact-accuracy. Recommend softening — the section's power is what it withholds, and these sentences edge toward the definition.

**9. Optional — state the deviation (line 258).** The draft says "a small margin." The outline's figure is **max 2.8 points**, and it checks out: across 17 content chapters, Part II is 41.2% vs 44% (−2.8), Part III 29.4% vs 28%, Part IV 17.6% vs 16%, Part V 11.8% vs 12%. Stating 2.8 makes the disclosure checkable — the habit §2 spends a page building.

---

Two things worth surfacing beyond the artifact itself:

- **The chapter's objective coverage is not the problem** — it claims zero objectives and covers zero, which is correct for an orientation chapter. Every current-blueprint fact validates against the cached snapshots, and the derived arithmetic (44+28=72, 16%≈1-in-6, the 2.8-point deviation) all checks out.
- **The real defect is upstream.** The research stage found that the LF *does* publish the 75% passing score and that the retired 46/22/16/8/8 weights are unsourced — then couldn't write those corrections to disk. Stage 3 drafted from the stale snapshots in good faith. Fixing only the prose leaves the bad snapshots in place for the next run, which is why fix 0 gates the rest.