Research complete. Every Ch 2–18 section shipped exactly as the skeleton planned, so all cross-bearing targets resolve. Three findings changed the plan: the canonical theme-3 phrase, the Ch 1 Bearings precedent (3+2, not 2×5), and a missing book-level artifact that §5 depends on.

---

```yaml
---
chapter: 19
chapter_type: "synthesis"
title: "Bearings Before Landfall"
subtitle: "Everything that connects, and the traps that don't"
exam_domain: "All four domains — synthesis, no new objectives"
domain_weight_pct: 0
complexity: "mixed"
novelty: "familiar"
prereq_factor: "heavy"

# --- Section plan (no word budgets) ---
# Section numbers are BINDING. §3 and §5 are pinned by published cross-bearings
# already shipped in chapter-01-taking-departure.md (lines 215 and 452).
sections:
  - name: "Nine Threads Through Twenty Chapters"
    objectives: ["D1.1", "D1.2", "D1.3", "D1.4", "D2.1", "D2.2", "D2.3", "D2.4", "D3.1", "D3.2", "D4.1", "D4.2", "D4.3"]
    requires_figure: true
    figure_anchor: "ch19-fig01-cross-domain-integration-map"
    checkpoint_after: true
  - name: "The Pairs That Cost Points"
    objectives: ["D1.1", "D1.2", "D1.3", "D1.4", "D2.1", "D2.2", "D2.3", "D2.4", "D3.1", "D3.2", "D4.1", "D4.2", "D4.3"]
    requires_figure: true
    figure_anchor: "ch19-fig02-confusion-pair-matrix"
    checkpoint_after: true
  - name: "Ninety Minutes"
    objectives: []
    requires_figure: true
    figure_anchor: "ch19-fig03-exam-day-pacing"
    checkpoint_after: false
  - name: "Where the Weight Actually Is"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Using The Lodestar"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "The Week Before"
    objectives: []
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false

# --- Skill v5.3 Part 11 + style-decisions [LOCKED 2026-04-19] ---
# Synthesis-chapter Soundings is an EXAM-READINESS instrument, not a topic-priors
# diagnostic. Five free-response self-assessment prompts; readiness-tier rubric.
soundings_planned:
  question_count: 5
  topics:
    - "Full-length timed attempt: has the reader sat one, and at what margin"
    - "Weakest domain: can the reader name it and state a plan to close it"
    - "Cold discrimination: can the reader state one named confusion pair's discriminator without looking"
    - "Theme coverage: can the reader name the book's cross-cutting patterns unprompted"
    - "Own error patterns: can the reader name their recurring failure mode from practice attempts"

# --- Skill v5.3 Part 8: practice-question budget (from B4 length-budget.md) ---
question_budget:
  soundings: 5
  taking_your_bearings: 5              # across 2 checkpoints (3 + 2) — see note
  practice_questions: 10
  total_this_chapter: 20

kb_tags:
  objectives: ["D1.1", "D1.2", "D1.3", "D1.4", "D2.1", "D2.2", "D2.3", "D2.4", "D3.1", "D3.2", "D4.1", "D4.2", "D4.3"]
  concepts:
    - "cross-cutting-themes"
    - "absent-component-pattern"
    - "confusion-pair-matrix"
    - "discriminating-question"
    - "exam-pacing"
    - "domain-weight-allocation"
    - "the-lodestar"
  commands: []

figures_planned:
  - "ch19-fig01-cross-domain-integration-map"
  - "ch19-fig02-confusion-pair-matrix"
  - "ch19-fig03-exam-day-pacing"
---
```

## 1. Why This Chapter Matters

The reader has finished eighteen chapters organized by domain, because that is how the exam is organized. But that is not how the material is *shaped*. The control loop is not a Chapter 3 fact — it is the thing Chapter 6 instantiates, Chapter 11 re-uses, Chapter 15 points at a Git repository, and Chapter 17 collects. A reader who learned it as a Chapter 3 fact will miss it when it appears in a Chapter 15 question. This chapter re-cuts the book along the nine threads that actually run through it, so the reader sees the material a second time in a different shape.

Identity frame: this is the shift from *having studied* to *being ready*. Practitioners do not hold nine hundred facts; they hold a small number of patterns and derive the facts. The RBAC four-way matrix is the clearest case — candidates memorize four rows, and practitioners derive them from a distinction the book settled back in Chapter 4. One of those two readers forgets under time pressure.

Stakes, stated honestly: this chapter adds nothing new. Everything in it was taught somewhere in Chapters 2–18. Its whole value is in the second pass — the discrimination that separates a reader who *recognizes* a term from one who can tell it from its neighbor with ninety seconds on the clock.

## 2. What You'll Learn

- **Trace** each of the book's nine cross-cutting themes through the chapters that build it, and name the pattern rather than the instances
- **Discriminate** between every confusion pair the book has flagged, using a one-line test rather than two competing definitions
- **Pace** a ninety-minute multiple-choice exam, including what to do with a question you cannot answer on first read
- **Allocate** remaining study time against published domain weights and your own checkpoint history, rather than against whatever feels least comfortable
- **Use** `the-lodestar.md` in the last hour before the exam, and know what it deliberately leaves out
- **Plan** the final week, including the parts of it that consist of not studying

## 3. Soundings plan

Synthesis type. Five free-response self-assessment prompts, per style-decisions.md [LOCKED 2026-04-19] — the reader is diagnosing **launch-readiness**, not priors. None are multiple-choice; the CAPM Ch 7 precedent quoted in the ledger is the shape to follow.

| # | Topic | What it tests | Why it earns its place |
|---|---|---|---|
| 1 | Timed full-length attempt | Whether the reader has ever sat the whole instrument under a clock, and at what margin | Pacing failure is invisible until you meet it. A reader who has only done untimed practice does not know their own rate. |
| 2 | Weakest-domain naming | Whether the reader can name their weakest of the four domains *and* say what they would do about it | Naming the weakness is the easy half; having a plan is the readiness signal. Feeds directly into §4. |
| 3 | Cold discrimination on one named pair | Retrieval of a discriminator, unprompted, for a pair the reader met chapters ago | The single best proxy for §2's whole content. If this one is shaky, §2 is the chapter's centre of gravity for this reader. |
| 4 | Unprompted theme recall | Whether the reader can name the book's recurring patterns without the list in front of them | Calibrates §1 exactly. A reader who names most of them should skim §1; one who names none should read it slowly. |
| 5 | Own error-pattern awareness | Whether the reader knows *how* they get questions wrong — misread stem, coin-flip between two, clock | Metacognitive, and the only one §3 can act on. Distinct from "which domain is weak." |

**Fixed-Point check — passes.** No prompt reveals a chapter Fixed Point, because this chapter has no new Fixed Points to reveal; both ★ callouts (§1 and §3) restate material already taught in Chapters 3–17. Prompts 3 and 4 *ask the reader to retrieve* rather than supplying an answer, and their `<details>` keys must confirm-and-point (`see §1` / `see §2`) rather than re-derive. Prompt 4's stem must not contain the theme-3 phrase.

**Rubric — readiness tiers, not reading pace:**

- **5 of 5:** Sit it. Use §5 and §6 as the plan and stop adding material.
- **3–4:** One to two more weeks. §4 tells you where they go.
- **0–2:** Four or more weeks, and §4 plus your own Bearings history tells you which chapters to re-read — not the whole book again.

## 4. Section plan

Heading form follows the Ch 5–18 shipped convention: `## <difficulty> §N — Title`.

---

### ☀️ §1 — Nine Threads Through Twenty Chapters

Traces the nine cross-cutting themes, each **named**, through its chapter path, so the reader sees the book cut by pattern instead of by domain. Owns no new material — every claim here is a retrieval from a shipped chapter, and the section must point rather than re-teach. Closes on the integration map.

The nine, with the paths drafting must honor (all §N targets verified against shipped text):

| # | Theme | Path | Provenance |
|---|---|---|---|
| 1 | The control loop — desired state, current state, reconciliation | Ch 3 §6 → Ch 4 §1 → Ch 6 §2 → Ch 11 §2 → Ch 15 §7 → Ch 17 §4 | B3 |
| 2 | Namespaced vs cluster-scoped — *derives* the RBAC matrix | Ch 4 §3 → Ch 8 §3 → Ch 12 §3 | B3 |
| 3 | **"An object without its component does nothing"** | Ch 3 §4 → Ch 10 §3 → Ch 11 §5 → Ch 13 §7 → Ch 17 §7 → Ch 18 | B3 |
| 4 | Declarative desired state vs imperative command | Ch 4 §1 → Ch 6 → Ch 14 → Ch 15 | B5-reconstructed |
| 5 | Labels and selectors as the universal join — and RBAC's contrast | Ch 4 §5 → Ch 6 §3 → Ch 7 §3 → Ch 9 §4 → Ch 10 §6 → Ch 12 §3 | B5-reconstructed |
| 6 | Pluggable interfaces — CRI, CNI, CSI, CRDs as one story | Ch 2 §4 → Ch 9 §1 → Ch 11 §5 → Ch 6 §8 → Ch 17 §4 | B5-reconstructed |
| 7 | Identity — ServiceAccount from Pod to API to delivery agent | Ch 5 §6 → Ch 12 §2 → Ch 15 §4 | B5-reconstructed |
| 8 | Requests and limits — the numbers that reappear everywhere | Ch 5 §8 → Ch 7 §2 → Ch 13 §4 → Ch 17 §7 → Ch 18 §3 | B5-reconstructed |
| 9 | Additive, allow-only, no deny — RBAC and NetworkPolicy share one semantic | Ch 10 §6 → Ch 12 §3 → Ch 12 §9 | B5-reconstructed |

**Binding constraints for drafting:**

- **★ Fixed Point** on theme 3, quoting **verbatim**: *an object without its component does nothing.* Verified at **28 occurrences across 7 chapters** (Ch 3, 6, 10, 11, 13, 17, 18). B7's errata records that a mis-quotation of this exact phrase already propagated from the ledger into shipped text once. Do not paraphrase it, and do not substitute the descriptive label "the absent-component pattern," which appears only 7 times and only in Ch 3/11/17.
- **No running ordinals.** Per the book-level convention ratified at the Ch 8 gate: name the pattern, say it is the same one, but never assert a count ("the sixth control loop," "the fourth time"). Chapter *paths* are fine — they are a closed set the reader can see. The only sanctioned control-loop count in the book is Ch 6's two-altitudes framing and Ch 15 §7's payoff.
- **Theme 6 must not re-open the interface-count reconciliation.** Ch 17 §4 already reconciled "CRDs" vs "API extensions" and the second-vs-third ordinal. Ch 19 inherits a reconciled reader; state the four, do not re-argue them.
- Themes 4–9 are `[B5-reconstructed]`, not B3's list. See Open Questions #3.

Concepts retrieved by name: control loop, namespaced/cluster-scoped, the absent-component phrase, declarative vs imperative, label selectors, the four pluggable interfaces, ServiceAccount identity, requests/limits/QoS, additive-no-deny.

**Figure:** `ch19-fig01-cross-domain-integration-map` · **Checkpoint 1 falls here.**

---

### 🟡 §2 — The Pairs That Cost Points

The chapter's centre of mass. A **discriminating question** for every confusion pair that survived from B1's 114-trap inventory to publication, plus the surface-form homonyms from the term ledger's Canonical Forms table. The section's method is uniform and must stay uniform: name the pair, give the *one-line test* that separates them, then the tell that shows up in a question stem. Never two competing definitions side by side — that is the failure mode this section exists to fix.

Pairs, grouped by home domain (B1 trap numbers in brackets):

- **D1 (Ch 2–8):** Pod phase vs container state [6, 7] · liveness/readiness/startup [10, 11] · labels vs annotations [15] · ConfigMap vs Secret [16, 60] · namespace vs labels for versioning [13, 14] · Deployment vs StatefulSet [21] · DaemonSet vs replica count [22] · Job vs CronJob [23] · OCI vs CRI [32, 33] · scheduler binds / kubelet starts [24, 25] · kubelet skew vs kubectl skew vs supported releases [27, 28, 29] · scheduled-once vs rescheduled [9] · restartPolicy scope [8]
- **D2 (Ch 9–13):** Service type ladder [37, 38, 39] · headless vs broken vs selectorless [40, 41] · Ingress object vs controller [42] (theme 3) · Ingress frozen vs deprecated [44] · NetworkPolicy default-open, additive, both-ends [48, 49, 50] · RBAC no-deny [53] · the four-way binding matrix [54, 55, 59] · view/edit/admin [57, 58] · PV vs PVC [64] · RWO vs RWOP [65] · Retain/Delete/Recycle [66, 67, 68] · `""` storage class [69] · Pending → don't reach for logs [70]
- **D3 (Ch 14–16):** chart vs release vs revision [79, 80] · `charts/` vs chart repository [81] · **Deployment rollback vs Helm rollback** (term ledger homonym; not a B1 trap) · GitOps push vs pull [73, 74, 75] · OutOfSync as drift, not error [76] · troubleshooting vs debugging scope [71, 87]
- **D4 (Ch 17–18):** mesh control plane vs cluster control plane [101] · sidecar vs ambient mode [102] · Serving vs Eventing [83] · maturity-level ordering [97] · TOC vs Governing Board [110] · SIG vs Working Group vs Committee [108, 109] · TAG vs SIG [112] · horizontal vs vertical [103] · HPA built-in vs VPA add-on [104] · workload vs node autoscaling [106] · observability vs monitoring [88] · span vs trace [90] · SLI vs SLO vs SLA [92] · Prometheus pull vs Pushgateway [93]
- **Surface-form homonyms** (term ledger Part 3): namespace · control plane · sandbox · revision · rollback · label · request · binding · release · Service · immutable · operator · volume · plugin

**Governing ethical constraint.** Ethical Guardrail #8 and the retrieval architecture's do-not-retrieve list #4: any pair resting on an `[inferred]` trap is described as **"easy to confuse,"** never **"frequently tested."** The `[inferred]` set relevant here is **#33, #34, #70, #84, #85, #87, #112** — but see Open Questions #4, because the count is disputed and drafting must read the tag on each trap rather than trust a summary.

**⚠ Navigational Hazards** block lands here, collecting the pairs whose *wrong* answer is the intuitive one (RWO reading as one Pod; `""` reading as "use the default"; two default IngressClasses reading as more coverage).

**Figure:** `ch19-fig02-confusion-pair-matrix` · **Checkpoint 2 falls here.**

---

### ⚪ §3 — Ninety Minutes

**Pinned** — `chapter-01-taking-departure.md:215` emits `*[cross-bearing: see Ch 19 §3 — pacing and time discipline]*`. This section must sit at §3.

Owns exam-day pacing and time discipline: the first pass, flagging and skipping, the second pass, and what to do with a question that is unfamiliar rather than merely hard. Distinguishes the three reasons a candidate runs out of time (re-reading stems, refusing to flag, and re-litigating settled answers) because they have different fixes.

**The sourcing constraint that shapes this whole section.** Ninety minutes is *published* by the Linux Foundation. The question count is *commonly reported*, not published — Ch 1 already made that distinction to the reader, and the retrieval architecture's do-not-retrieve list forbids teaching either the 60-question figure or the 75% pass mark as fact. So the pacing arithmetic cannot be a fixed seconds-per-question number. The section must give a **rule that survives a different count**: read the count off the screen, divide, bank the first pass at roughly 60% of the clock, and reserve the remainder for flagged items. The commonly reported format may be used as a worked example, explicitly labelled as such.

**★ Fixed Point** on the pacing rule itself. **★** is warranted here despite this being strategy rather than fact — it is the one behavior the reader should be able to execute without thinking on the day.

**Figure:** `ch19-fig03-exam-day-pacing`.

---

### ⚪ §4 — Where the Weight Actually Is

Re-walks the published 44/28/16/12 split against the reader's *own* Soundings and Bearings history, so the allocation is personal rather than generic. Answers one question: where does the next block of study time buy the most?

**— Dead Reckoning** block here, stating the weights flat with no metaphor: D1 Kubernetes Fundamentals 44% (Ch 2–8) · D2 Container Orchestration 28% (Ch 9–13) · D3 Cloud Native Application Delivery 16% (Ch 14–16) · D4 Cloud Native Architecture 12% (Ch 17–18).

Two calls this section must make:

- **D4.3 Community and Collaboration is flagged as the reliably under-studied competency** (per B2). It is institutional, name-dense, feels unexaminable, and is where a reader who ran out of time stopped. Ch 17 §2 and §8 are its home.
- **The 2025-11-24 blueprint change is a study-allocation hazard, not just a fact.** D3 doubled from 8% to 16% and observability lost standalone-domain status. A reader working from third-party material bought before the change is mis-allocated by roughly a full domain [B1 trap 113].

**No figure — deliberate.** This section uses a reader-completed table (generation effect, skill Part 10). The reader fills in their own per-chapter checkpoint scores against the weight column; a pre-rendered figure would do the work for them and destroy the point.

---

### ⚪ §5 — Using The Lodestar

**Pinned** — `chapter-01-taking-departure.md:452` emits `*[cross-bearing: see Ch 19 §5 — using The Lodestar]*` and tells the reader in so many words that "Chapter 19 walks you through using it." This section must sit at §5 and must deliver that walkthrough.

Walks `the-lodestar.md` block by block: what each block is for, which are lookup and which are drill, and how to use it in the last hour. Also states what it deliberately omits — it is a distillation, not a summary, and a reader who cannot reconstruct a chapter from it has not found a defect.

**⛑ This section is currently blocked.** `the-lodestar.md` does not exist in the Book-KCNA repo. See Open Questions #1 — this is the one item that can stop drafting.

---

### ⚪ §6 — The Week Before

A dated final-week plan: what to review, what to leave alone, and what to do the night before. Includes the case for *not* studying in the last twenty-four hours, and the specific failure of trying to learn new material late — which is where D4.3 typically gets crammed and typically does not stick.

**Logbook Entry** sidebar fits naturally here (the week-before experience as lived, not prescribed). Closes with **🏆 Safe Harbor**, then the chapter's `## The Voyage Ahead` hands off to the mock.

**Ch 20 must be addressed by name only** — it has no numbered sections, and nothing in the book may emit `*[cross-bearing: see Ch 20 §N — …]*`.

## 5. Taking Your Bearings checkpoints

Two checkpoints, 5 questions total (3 + 2), matching B4's budget for this chapter exactly and following the **shipped Ch 1 precedent** — the book's only other non-content chapter also carries 5 Bearings split 3+2 across two checkpoints. The skill's "≥5 questions per checkpoint" floor is written for content chapters; the book has already decided otherwise for non-content chapters and shipped it. The structural contract's `minimum_per_chapter: 2` (two ☆ instances) is satisfied.

| # | Placement | Topic | Qs | Retrieval share |
|---|---|---|---|---|
| 1 | After §1 | **The Threads** — name the pattern, given instances from chapters the reader must connect | 3 | 100% |
| 2 | After §2 | **The Pairs** — supply the discriminator, not the definition | 2 | 100% |

Retrieval share is **~100% by construction** — this is a synthesis chapter and every item is cross-chapter by definition, which is why it sits outside the 20–25% schedule.

**Both checkpoints land in the §1–§2 half deliberately.** §3–§6 are strategy and advice; quizzing a reader on their own study plan is theatre. It also keeps Ch 19 clear of the do-not-retrieve rule against testing exam mechanics.

## 6. Exam Alert plan

Kept short — §2 is already the trap section, and duplicating it here would be channel redundancy (skill Part 7).

**High-priority:**
1. The absent-component pattern, quoted in its canonical form — it converts four separate gotchas into one rule
2. The RBAC four-way matrix, *derived* from namespaced-vs-cluster-scoped rather than memorized
3. Additive, allow-only, no deny — one semantic shared by RBAC and NetworkPolicy
4. The version-skew numbers (kubelet three back, kubectl one either way, three supported minors)
5. D4.3 institutional vocabulary — the highest ratio of exam presence to study time in the book

**Common traps to name:** the four pairs where the intuitive answer is the wrong one (RWO as one Pod; `""` as "default class"; a second default IngressClass as wider coverage; `Running` as "the app works").

## 7. Practice Questions plan

**10 questions**, cross-domain by construction. Primary-domain tagging is approximate — most items deliberately require two chapters to answer, which is the point.

| Domain | Items | Sourced from |
|---|---|---|
| D1 | 3 | Ch 2–8 — one on themes 1/2, one on the skew rules, one on a D1 confusion pair |
| D2 | 3 | Ch 9–13 — one theme-3 instance, one RBAC matrix derivation, one storage pair |
| D3 | 2 | Ch 14–16 — the rollback homonym; GitOps pull-not-push |
| D4 | 2 | Ch 17–18 — **both from D4.3**, per the deliberate over-representation |

D4 at 20% against a published 12% is intentional and is *not* a violation of the ±2pp tolerance — that tolerance governs the Ch 20 mock, not chapter practice sections. The tilt is B2's compensation for D4.3's under-study risk.

**Interleaving strategy:** every item names at least two chapters in its answer key, and no two consecutive items draw on the same domain. Trap answers are built from §2's pair matrix so that a wrong answer diagnoses *which* pair the reader has collapsed.

**Excluded from all 10, per the do-not-retrieve list:** exam mechanics, the dated graduated-project roster (test maturity *levels*), and the 60-question / 75% figures.

## 8. Required figures

| Anchor | Purpose | Content |
|---|---|---|
| `ch19-fig01-cross-domain-integration-map` | Theme 1 payoff — the book re-seen by pattern instead of domain | Nine labelled threads running horizontally across a chapter axis (2→18), each thread touching only the chapters that build it. Chapters on one axis, themes on the other; density shows where the book concentrates. Must stay under ~7 visual groupings per skill Part 18.12 — consider banding the nine threads into three visual tiers rather than nine equal lines. |
| `ch19-fig02-confusion-pair-matrix` | §2's navigation aid | Two-column pair matrix — left the pair, right the one-line discriminator. **Not** a definition table. Must be legible at 400px and in grayscale; likely needs splitting into per-domain panels rather than one long table. |
| `ch19-fig03-exam-day-pacing` | §3's rule made spatial | Ninety-minute timeline showing first pass, flag budget, second pass, and reserve. Must render the per-question rate as a *derived* quantity, not a hard number — the count is unpublished. |

No `ch19-zenith-*` anchor. The book's two designated Zeniths are Ch 15 §7 (primary) and Ch 17 §9 (secondary), both shipped; Ch 19 must not compete with them.

## 9. Open questions for the author

1. **`the-lodestar.md` does not exist — this blocks §5.** The file is absent from the Book-KCNA repo, along with `glossary.md`, front matter, and `00-table-of-contents.md`. §5 is pinned by a published pointer *and* Ch 1 tells the reader outright that "Chapter 19 walks you through using it," so the section cannot be cut or deferred. Two paths: (a) produce `the-lodestar.md` before Ch 19 drafts, so §5 walks a real file; or (b) draft §5 against a specified block structure and reconcile after. **(a) is strongly preferable** — a walkthrough written against a hypothetical file will not match the file that eventually ships, and the mismatch lands in the reader's last hour of study.

2. **Theme 3's retrieval name is inconsistent in shipped text.** The canonical phrase *an object without its component does nothing* appears 28 times across Ch 3, 6, 10, 11, 13, 18 and once in Ch 17. The descriptive label *the absent-component pattern* appears 7 times, only in Ch 3, 11, 17. Ch 19 §1 will use the canonical phrase. Worth deciding whether Ch 10 §3 — the pattern's designated naming home per the arc outline — should also carry the label in a one-clause retrofit, so the two names are reconciled where the reader first meets them rather than in the final review.

3. **Six of the nine themes are reconstructed, not authored.** `retrieval-architecture.md` (the B3 artifact) is **not stage output** — it is a permission-failure notice recording that B3 could not write to the book repo, followed by a prose summary. B5 carried three themes forward verbatim from that summary and reconstructed themes 4–9 from B2's dependency graph. §1 will present all nine as canonical, which is the right reader experience but overstates their provenance. Either accept the reconstruction on the record, or re-run B3 and reconcile before §1 drafts. The three B3-sourced themes (1, 2, 3) are the ones with downstream shipped dependencies, so the risk is contained.

4. **The `[inferred]` trap count is disputed.** B4 and B5 both state 14 of 114 traps are `[inferred]`; the D1–D4 trap tables in `domain-analysis.md` tag **7** (#33, #34, #70, #84, #85, #87, #112). Since §2 is built entirely on that inventory and the tag governs whether a pair may be called "frequently tested," drafting must read the tag on each trap it uses rather than trusting either number. Flagging so the discrepancy is a known quantity, not a surprise at the integration gate.

5. **☀️ on §1's heading rather than the closing section — confirm.** Ch 17 §9 and Ch 18 §8 both mark the *closing* section ☀️, and the section skeleton recommends that convention for Ch 9–19. Ch 19 inverts it: the recognition beat is §1 (the book re-seen by theme), and §6 is a scheduling section that would be mismarked by a Zenith glyph. The proposal is `## ☀️ §1 — Nine Threads Through Twenty Chapters` with §6 taking an ordinary difficulty glyph. Deliberate, but it is a visible break from the two preceding chapters.

6. **Recorded, no action needed:** Ch 1 carries no `§N` anchors, so §1/§4/§5 must address it by heading name. Ch 20 has no sections and is addressed by name only. Both constraints are already in the skeleton; noting them here so the drafting stage does not generate an unresolvable pointer under time pressure.

---

**Verification note.** All 19 published forward cross-bearings resolve — I extracted the shipped section headings for Ch 1–18 and every `§N` this outline references exists with the planned content. Only two inbound pointers target Ch 19 (`§3 — pacing and time discipline`, `§5 — using The Lodestar`), both from Ch 1, and both land at their pinned numbers.

This is stage output; per the executor convention it should be captured to `../Book-KCNA/.pipeline-state/ch-19/outline.md` rather than written by me directly.