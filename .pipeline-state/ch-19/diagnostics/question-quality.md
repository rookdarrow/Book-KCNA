Analysis complete. Here is the stage output for `diagnostics/question-quality.md` (emitting to stdout per the executor convention rather than writing the file directly).

```markdown
# Question-Quality Audit — Chapter 19

## Summary

- Chapter type: **synthesis**
- Total questions inspected: **20**
  - 🧭 Soundings questions: **5**
  - ☆ Taking Your Bearings questions: **5** (across 2 checkpoints, 3 + 2)
  - Practice questions: **10**
- Question budget compliance: **met** (all four categories exact)
- Weak distractors (WARN): **4**
- Trap answers that don't target real misconceptions (WARN): **2**
- Missing or incomplete why-wrong explanations (FAIL): **0**
- Retrieval-practice spacing: **compliant** (100%, deliberately outside the 20–25% schedule per outline §5)
- Soundings spoiler check: **clean** — 0 of 5 questions reveal a ★ Fixed Point

**Two set-level construction defects outrank every per-question finding below and are recorded in their own section:** the practice-question answer key is `B` in 8 of 10 items, and the key is the longest option in 5 of 10. Both are mechanically fixable without touching content. Neither is visible from a per-question read, which is why they survived drafting.

---

## Question-budget compliance

Compared against `question_budget` in `outline.md:65-69`.

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 5 | 5 (`draft-v1.md:43-51`) | **met** |
| Taking Your Bearings (total) | 5 | 5 (`:245-249`, `:447-449`) | **met** |
| Taking Your Bearings (checkpoints) | ≥2 | 2 (`:241`, `:443`) | **met** |
| Practice Questions | 10 | 10 (`:725-812`) | **met** |
| **Chapter total** | **20** | **20** | **met** |

The 3+2 Bearings split falls below the skill's "≥5 questions per checkpoint" floor. This is the ratified non-content-chapter exception (outline §5, following the shipped Ch 1 precedent), not a defect. The structural contract's `minimum_per_chapter: 2` for ☆ instances is satisfied.

## Soundings spoiler check

The chapter has exactly two ★ Fixed Points: the absent-component phrase (`:166`) and the pacing rule (`:497`). Neither is referenced, paraphrased, or given away by any Soundings stem or key.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 (`:43`) | Timed full-length attempt taken? | no | Self-report. Key adds published 90-minute figure — context, not a ★. |
| 2 (`:45`) | Weakest domain + a plan | no | Self-report; key points to §4 without answering. |
| 3 (`:47`) | `ReadWriteOnce` cold retrieval | no — but see WARN below | Targets a ⚠ Navigational Hazard (`:429`), not a ★. |
| 4 (`:49`) | Unprompted theme recall | no | Stem correctly omits the theme-3 canonical phrase, as outline §3 required. Key confirms-and-points: "§1 supplies the list" (`:62`). |
| 5 (`:51`) | Own error-pattern awareness | no | Metacognitive; nothing to spoil. |

**Rubric check (rule 8): present, thresholds adapted — not a FAIL.** The block ends with a three-tier rubric at `:70-74`, but banded `5 of 5 / 3–4 / 0–2` rather than the skill's literal `6+ / 3–5 / 0–2`. This is the ratified synthesis-chapter variant (readiness tiers, not reading pace) from outline §3 citing style-decisions.md [LOCKED 2026-04-19], and a `6+` band is arithmetically unreachable on a 5-question instrument. Recording the deviation so the integration gate does not re-raise it.

**Answer disclosure (rule 9): clean.** `<details>` opens at `:53`, closes after the rubric. Readers can attempt before seeing answers.

---

## Per-question findings

### Q-Soundings 3 (`:47`, key `:60`): "a PersistentVolumeClaim requests `ReadWriteOnce`. State in one sentence what that constrains..."

**Issue:** The key fully re-derives the answer instead of confirming-and-pointing, in direct violation of the binding constraint in outline §3 ("Prompts 3 and 4 ... their `<details>` keys must confirm-and-point (`see §1` / `see §2`) rather than re-derive"). Prompt 4's key complies (`:62`); prompt 3's does not.

The consequence is concrete: the key at `:60` hands over one of the four ⚠ Navigational Hazards — "It does **not** mean one Pod; that is `ReadWriteOncePod`" — roughly 370 lines before the reader reaches the hazard block at `:429` that exists to teach it. A reader who opens the Soundings answers arrives at §2 with that hazard already spent. It is not a ★ spoiler, so it does not trip rule 7, but it degrades the pretesting effect on the single most-emphasised trap in the chapter.

Compounding: the cross-bearing at the end of the key points to **Ch 11 §4**, not to §2 of this chapter, so the reader is not even redirected to where the discrimination work happens.

**Why-wrong explanation status:** N/A (constructed-response self-assessment).

**Recommended fix:** Cut the derivation. Replace the key body with a confirm-and-point of the shape prompt 4 already uses — e.g. *"Access modes are node-count semantics, not permission semantics, and the distinction has a name. If you hesitated, §2's storage row and the ⚠ block are the centre of gravity for you — see §2."* Retain the Ch 11 §4 cross-bearing as a secondary pointer.

---

### Q-Bearings 3 (`:249`, key `:276-282`): "...name the cross-cutting thread that tells you which field to read instead."

**Issue — answerability defect.** §1 defines a closed, numbered set of **nine** cross-cutting threads (`:107-240`) and the chapter uses "thread" throughout as the controlled term for that set ("this is thread 3" `:342`; "thread 9 is soft" `:822`; "thread 8 arriving from the other direction" `:415`). The expected answer at `:280` is **"Pod phase versus container state (Ch 5 §5)"** — which is **not one of the nine threads.** It is a §2 confusion pair, listed in the D1 discriminator table at `:303`.

A reader who correctly restricts themselves to the chapter's own defined vocabulary cannot produce the expected answer. A reader who *does* answer from the nine would most defensibly say thread 8 (requests and limits) — which is exactly what P2's key invokes for the same `Pending` scenario at `:829` ("requests are the scheduler's filter input (thread 8)"). The chapter answers the same diagnostic question two different ways in two places.

This is the undesirable-difficulty failure the skill names in Part 10B: "ambiguous questions with multiple defensible answers."

**Why-wrong explanation status:** present and specific for the partial answer ("If you said 'logs would be empty,' you are right but incomplete") — the key is well built; only the stem's category word is wrong.

**Recommended fix:** Cheapest correct edit is one word in the stem — change "the cross-cutting thread" to **"the confusion pair"**, which matches `:280` exactly and matches §2's own terminology. If instead you want the item to test §1, retarget both stem and key to thread 8 and let the phase/state pair be the supporting detail.

---

### Q-Bearings 5 (`:449`, key `:465-473`): "You're handed a stem containing the word 'revision' and four options..."

**Issue (two, both minor):**

1. **Discriminator collision.** The key resolves "revision" with *"whose history?"* — the Deployment-vs-Helm homonym split from the table at `:420`. But §2's own figure row and D3 table give a *different* discriminator for chart/release/revision: *"Package, install, or version of it?"* (`:301`, `:383`). Both are correct for different splits, and the stem does not say which family it means. A reader answering with the §2 table's phrasing gets marked wrong by the key.
2. **Only Bearings item with no wrong-answer callout.** Q1, Q2, Q3 and Q4 each name a specific likely error and what it diagnoses ("If you answered 'the CRD is broken'…", "If you answered 'cluster-wide secret read access', you inverted the rule", "If you caught 'deprecated' but not 'traffic will break'…"). Q5's key has none. Since these five items are constructed-response, the key is the *only* place misconception detection can happen — see the note under set-level findings.

**Why-wrong explanation status:** present but incomplete — explains the correct discriminator thoroughly, identifies no error mode.

**Recommended fix:** Add one clause to the stem naming the family — "…a stem containing the word 'revision' where the ambiguity is *cross-tool*…" — and append a wrong-answer callout: *"If you reached for 'package, install, or version of it?', you resolved the three-way split inside Helm rather than the cross-tool homonym. Both discriminators are real; the stem tells you which is in play."*

---

### P2 (`:734`, key `:825-831`): "A Pod has been in `Pending` for ten minutes."

**Issue:** Option D is the weakest distractor in the item, and the weakness is repairable in the key rather than the option.

**Distractor analysis:**
- A) `kubectl logs` → `exec` → stdout — **plausible**; targets the reflexive-logs error the chapter calls "the most common instrument error" (`:398`). Strong.
- B) describe → events → capacity vs requests — **correct**.
- C) `kubectl top` → utilization vs limits — **plausible**; targets requests/limits collapse (thread 8) and doubles as an absent-component check (metrics-server). Strong.
- D) "Restart the kubelet on the target node, then re-check the phase" — **plausible but under-credited**. It does target a real, chapter-named misconception (the scheduler-binds / kubelet-starts pair, `:311`), but the key dismisses it in seven words — "there is no target node yet; that is the problem" — without naming the pair. As written it reads as the throwaway fourth option.

**Why-wrong explanation status:** present and specific for A and C; present but vague for D.

**Recommended fix:** Extend D's rationale to name the pair it catches: *"D is wrong because there is no target node yet — that is the problem. If you picked it, you have collapsed **scheduler binds / kubelet starts** (§2, D1 table): `Pending` means the scheduler has not decided, so no kubelet is involved to restart."*

---

### P4 (`:752`, key `:841-847`): "A `RoleBinding` in namespace `web` grants a `ClusterRole` called `pod-reader` to a ServiceAccount..."

**Issue — under-specified stem creates a duplicate-meaning distractor.** The stem never states which namespace the ServiceAccount lives in. Option D reads "Pods in `web`, plus Pods in the ServiceAccount's own namespace." If the reader assumes the ServiceAccount is in `web` — the only namespace the stem names, and the natural default — **D collapses into A**, and the item has two options meaning the same thing.

**Distractor analysis:**
- A) "Pods in `web` only — the RoleBinding constrains the ClusterRoleBinding" — **plausible**; targets the "narrower binding limits the broader one" error. The single best trap in the item.
- B) "Pods cluster-wide" — **correct**.
- C) "Nothing — the two bindings conflict and RBAC resolves conflicts by denying" — **plausible**; targets the firewall mental model, i.e. thread 9. Real and common.
- D) "Pods in `web`, plus Pods in the ServiceAccount's own namespace" — **duplicate meaning under the natural reading**, and under any other reading it invents a namespace-of-origin rule the book never mentions and no reader would have acquired. The key concedes this: "it invents a namespace-of-origin rule that does not exist" (`:847`). A distractor whose only defence is that it is made up is fabricated for symmetry.

**Why-wrong explanation status:** present and specific for A and C; present but built on an invented premise for D.

**Recommended fix:** Two edits. (1) Name the ServiceAccount's namespace in the stem — "…to a ServiceAccount in namespace `ci`" — which removes the collapse. (2) Replace D with a distractor drawn from a real taught error, e.g. **"Pods in every namespace except `web`, where the RoleBinding takes precedence"** — that targets precedence-thinking, which is the same misconception family as C but from the opposite direction, and it is genuinely tempting to a reader who has not internalised "additive, nothing subtracts."

---

### P6 (`:770`, key `:857-863`): "A PersistentVolume with `persistentVolumeReclaimPolicy: Retain` had its bound PVC deleted..."

**Issue:** Option D fails trap fidelity — it conjoins two mechanisms the book never relates, and the key's entire refutation is that they are unrelated.

**Distractor analysis:**
- A) "`Retain` volumes can only be bound once, ever" — **plausible**; an overreading of `Retain` that a reader could genuinely hold. Acceptable.
- B) "The PV is in `Released`, not `Available`…" — **correct**.
- C) "The new PVC needs `volumeName` set explicitly" — **plausible and good**; targets the belief that static binding is the remedy. A reader could act on this in the field and be surprised.
- D) "`Retain` requires the DefaultStorageClass admission plugin to be disabled" — **implausible / fabricated for symmetry.** The key's refutation is "reclaim policy and the DefaultStorageClass admission plugin are unrelated mechanisms" (`:863`) — which is the tell. There is no identifiable misconception that produces this answer; it is two remembered nouns bolted together.

**Why-wrong explanation status:** present and specific for A and C; present but non-diagnostic for D.

**Recommended fix:** Replace D with the `storageClassName: ""` hazard, which is currently taught (`:396`, `:433`) and **tested nowhere in the chapter**:

> D) The PV has `storageClassName: ""`, so it can only bind to a PVC that omits the field

That option is tempting to anyone who has half-absorbed the `""` rule, it is wrong for a statable reason (`""` binds only to a PVC that *also* sets `""`, not one that omits it), and it converts a dead slot into coverage for one of the four ⚠ hazards. This single edit closes a coverage gap and a distractor gap at once.

---

### P8 (`:788`, key `:873-879`): "A Deployment's Pods show phase `Running` and a readiness probe that is failing."

**Issue:** Option C is thin.

**Distractor analysis:**
- A) "The containers are restarted repeatedly" — **plausible, excellent**; liveness/readiness collapse is the D1 discrimination the chapter calls the most common (`:879`).
- B) "Removed from the Service's endpoints and receive no traffic, without restarting" — **correct**.
- C) "The Pods are evicted under node pressure ahead of other workloads" — **weak**. Requires believing probe results feed QoS class. The chapter teaches QoS as deriving from requests and limits (thread 8), and never suggests probes participate, so nothing in the reader's model produces this answer. It is the fourth option rather than a trap.
- D) "The Deployment's rollout is rolled back automatically" — **plausible**; targets the belief that `progressDeadlineSeconds` auto-reverts. Real.

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** Swap C for a readiness-adjacent error with a real source: **"The Pod is removed from the Service's endpoints and the container is restarted after the failure threshold"** — the half-right answer, which catches readers who have the endpoint effect but have also imported the restart from liveness. That discriminates more finely than A does, because it catches partial rather than total collapse.

---

### P9 (`:797`, key `:881-887`): "An organization wants to define who is responsible for approving a new project into the CNCF..."

**Issue (two):**

1. **Only practice item that fails the interleaving rule.** Outline §7 binds every practice item to "name at least two chapters in its answer key." P9's citation line reads "*Chapters: 17 §2 (governance), 17 §8 (institutional structure)*" — two *sections*, one chapter. All nine other items cite two or three distinct chapters. Since this is the sole D4.3 item (see set-level findings), it is also the item least able to afford being non-interleaved.
2. **Stem framing is slightly off-task.** "An organization wants to define who is responsible for approving a new project into the CNCF" — the organization is not defining CNCF's governance; CNCF's charter already has. The question is really "who does what," and the framing briefly obscures that. Minor, but it is the kind of stem friction Part 10B classes as undesirable difficulty.

**Distractor analysis (this part is strong — no changes needed):**
- A) TOC approves projects; Board decides budget — **correct**.
- B) Clean inversion — **plausible, the strongest trap**; catches a reader who has both bodies but not their remits.
- C) End User TAB approves projects; Board decides budget — **plausible**; one half correct, tests whether TAB's advisory role is understood. Good partial-knowledge discrimination.
- D) TAGs approve projects; TOC decides budget — **plausible**; targets the TAG/TOC/SIG confusion the chapter documents as having a real historical cause (`:411`).

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** Reframe the stem to a lookup task ("Which pairing correctly describes who approves a new project into the CNCF and who sets the foundation's budget?") and add a second chapter to the citation line — Ch 17's maturity-level material or the Ch 18 governance touchpoint — so the interleaving rule holds.

---

## Set-level construction findings

These are the two highest-value fixes in this audit. Both are invisible per-question and both are mechanical.

### 1. Answer-position bias — **B in 8 of 10 items**

| Item | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|---|---|---|---|
| **Key** | B | B | C | B | B | B | B | B | A | B |

Keys verified at `:817`, `:825`, `:833`, `:841`, `:849`, `:857`, `:865`, `:873`, `:881`, `:889`. Distribution: **B×8, C×1, A×1, D×0.**

A reader who notices this and answers `B` on every item they cannot resolve scores 80% without domain knowledge. That defeats the purpose of a practice set whose stated job (`:721`) is to be worked "under something like exam conditions." It also mis-calibrates the reader: a high score here will not reproduce on the mock in Ch 20, and §4 explicitly instructs the reader to allocate study time from measured scores — so a bias-inflated score routes their remaining hours wrongly.

**Recommended fix:** Re-order options so keys land roughly 2–3 per position, and place at least two at D. This is a pure reordering — no stem, option, or rationale text changes, though the key lines (`**1 — B.**` etc.) and the two in-key option references (`:822` "If you picked C"; `:847`) must be updated to match.

### 2. Length cue — key is the longest option in 5 of 10

Items **2, 6, 7, 8, 10**. In each, the correct answer is the longest option by a wide margin:

- P6: B is 19 words against A 8, C 7, D 9 (`:772-775`)
- P10: B is 21 words against A 13, C 10, D 14
- P2: B is ~18 against A 9, C 11, D 11
- P8: B is 14 against A 5, C 11, D 7
- P7: B is 21 against A 15, C 11, D 12

Test-wiseness heuristics ("the longest, most qualified option is usually right") score above chance on this set. Compounded with the position bias, a reader with no Kubernetes knowledge can pass. P1 and P4 run the opposite way (key is conspicuously the *shortest*), which is its own weaker cue.

**Recommended fix:** Trim the keyed options to option-length parity and move the qualifying detail into the rationale, where it belongs. P6-B is the clearest case: "The PV is `Released`, not `Available`" is sufficient as an option; the reclamation explanation is already in the key at `:859`.

### 3. Constructed-response Bearings carry all misconception detection in the key

All five ☆ items are free-response, so the checkpoints contain **zero trap answers**. This is the right format for a section whose method is "supply the discriminator, not the definition" (`:445`) — an MC item cannot test discriminator *production*. The design compensates correctly: four of five keys name a specific wrong answer and say what it diagnoses. Recording it so the integration gate does not read "0 trap answers in checkpoints" as a defect. The one gap is Bearings Q5, handled above.

### 4. No score-banded revision prompts at either checkpoint

Skill Part 11 specifies score-banded revision prompts ("If You Scored 0–2: … go back to X"). Both checkpoints close with a competence signal only (`:286-291`, `:477-481`). Per-question revision pointers *do* exist and are good — Bearings Q2 sends the reader to Ch 4 §3 (`:274`), P1's key sends them to Ch 10 §6 and Ch 12 §3 (`:822`) — so the function is served, just not banded. With 3- and 2-question checkpoints a full band is awkward.

**Recommended fix (low cost):** one line per checkpoint. After checkpoint 1: *"Missed any of the three? Each maps to a thread — Q1 to thread 3, Q2 to thread 2, Q3 to §2's D1 pairs. Re-read that thread before §2, not the whole section."*

### 5. Domain sequencing — two consecutive-domain collisions

Outline §7 binds "no two consecutive items draw on the same domain." Actual primary domains: **D2, D1, D1, D2, D3, D2, D3, D1, D4, D4**. Items 2–3 are both D1; items 9–10 are both D4. Per-domain totals match the outline exactly (D1×3, D2×3, D3×2, D4×2). Fixed by swapping item 3 with item 4 and item 9 with item 8 — and note that reordering also helps the position-bias fix, since it changes which items sit adjacent.

### 6. The deliberate D4.3 over-representation is half-delivered

Outline §7 specifies both D4 items come from **D4.3 Community and Collaboration**, as B2's compensation for the competency §4 identifies as reliably under-studied and highest-return (`:589-593`). Actual: **P9 is D4.3 governance ✓; P10 is VPA/autoscaling ✗** — architecture, not community.

The chapter therefore argues at `:599` that Community and Collaboration is the best use of the reader's next study hour, then gives it a single practice item out of twenty. That is a self-undercutting gap, and it is the coverage finding most likely to cost real points.

**Recommended fix:** P10 is a strong item (it is the only place the absent-component pattern is shown failing at a *different layer* — API rejection rather than silent no-op — which is genuinely instructive). Do not cut it. Instead retarget **P3** (version skew, currently D1, and the set's third D1 item) to a D4.3 item on SIG vs Working Group vs Committee — the distinction is taught at `:407`, has four clean derivable options (ongoing/time-bounded/closed-membership), and is named in Exam Alert item 5 (`:708`) yet tested nowhere.

---

## Retrieval-practice spacing

- **Chapter 19 target:** skill Part 10 sets 20–25% for Ch 6+. Outline §5 declares this chapter **~100% by construction and deliberately outside that schedule** — every item in a synthesis chapter is cross-chapter by definition.
- **Actual:** **100%** — 5 of 5 checkpoint questions carry `[retrieval: chN]` tags (`:245`, `:247`, `:249`, `:447`, `:449`), spanning Ch 3, 4, 5, 6, 7, 10, 12, 13, 14, 17.
- **Practice questions** use the parallel convention from outline §7 — a trailing italic chapter citation per key rather than an inline tag. 9 of 10 name two or more distinct chapters; P9 names one (see above).
- **Status: compliant.** No additions needed. The only spacing-adjacent defect is P9's single-chapter citation.

## Coverage vs concepts

Concepts from `outline.md` `kb_tags.concepts`, plus the chapter's own declared high-priority material.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| `cross-cutting-themes` (thread recognition) | yes (Bearings Q1, Q2; Sound. Q4; P1, P4, P7, P10) |
| `absent-component-pattern` (★ Fixed Point, `:166`) | yes — heavily (Bearings Q1; P1; P10) |
| `confusion-pair-matrix` | yes (Bearings Q4, Q5; P3, P5, P6, P8) |
| `discriminating-question` (produce the test, not the definition) | yes (Bearings Q4, Q5 — the only two items that test production rather than recognition) |
| `exam-pacing` (★ Fixed Point, `:497`) | **NO** — accepted by design |
| `domain-weight-allocation` | **NO** — accepted by design |
| `the-lodestar` | **NO** — accepted by design |
| Thread 1 — control loop | **NO** |
| Thread 2 — namespaced vs cluster-scoped | yes (Bearings Q2; P4) |
| Thread 3 — absent component | yes (Bearings Q1; P1; P10) |
| Thread 4 — declarative vs imperative | **NO** |
| Thread 5 — labels/selectors as universal join | **NO** |
| Thread 6 — the four pluggable interfaces | weak — P1 key cites CNI in passing only |
| Thread 7 — ServiceAccount identity | yes (P7) |
| Thread 8 — requests and limits | yes (P2) |
| Thread 9 — additive, allow-only, no deny | yes (P1 option C; P4) |
| ⚠ Hazard — `ReadWriteOnce` is a node, not a Pod | **pre-test only** (Sound. Q3, whose key discloses it) — no post-reading item |
| ⚠ Hazard — `storageClassName: ""` means no class | **NO** |
| ⚠ Hazard — a second default IngressClass is ambiguity | **NO** |
| ⚠ Hazard — `Running` is not "working" | yes (P8; P2 by contrast) |
| Version-skew numbers (Exam Alert #4) | yes (P3 — model item) |
| RBAC four-way matrix (Exam Alert #2) | yes (Bearings Q2; P4) |
| D4.3 Community & Collaboration (Exam Alert #5) | **partial — 1 item where outline specified 2** |
| Surface-form homonyms (13 in table, `:418-433`) | **2 of 13** — `revision`, `rollback` (Bearings Q5; P5) |

**Reading of this table.** The three §3–§5 gaps are ratified: outline §5 excludes exam mechanics and study planning from the checkpoints deliberately, both to avoid theatre and to stay clear of the do-not-retrieve rule. Worth stating the consequence anyway rather than leaving it implicit: **the ★ Fixed Point at `:497` is the only ★ in the book's final content chapter that the reader never gets to confirm by retrieval.** Soundings Q1 asks whether they have sat a timed attempt, but nothing tests whether the pacing *rule* stuck. If the author wants that closed without testing exam mechanics, a self-check line in §6's final-week plan ("state the pacing rule from memory; if you can't, it isn't executable and there's no scratch paper") does the job outside the question budget.

The substantive gaps are the two untested ⚠ hazards and threads 1, 4 and 5. Both are addressable inside the existing 10-item budget: the P6-D swap above covers `storageClassName: ""`, and retargeting one of the three thread-3 items (which is over-tested at 3 of 20) to thread 5 would pick up the RBAC-names-rather-than-selects asymmetry — which the draft itself flags at `:373` as "exactly the kind of 'why is this one different' detail that makes a good question," and then does not write.

---

## Priority of fixes

1. **Re-shuffle practice answer positions** (B×8 → ~2–3 per position). Highest impact, zero content risk.
2. **Trim the five long keyed options** to length parity with their distractors.
3. **Fix Bearings Q3's stem** — "cross-cutting thread" → "confusion pair" (one word; removes an unanswerable item).
4. **Swap P6-D** for the `storageClassName: ""` distractor — closes a hazard-coverage gap and a fabricated-distractor gap together.
5. **Specify the ServiceAccount's namespace in P4** and replace its D option.
6. **Retarget P3 to D4.3** to deliver the planned two-item Community and Collaboration weighting, and fix P9's single-chapter citation.
7. **Rewrite Soundings Q3's key** as confirm-and-point per the outline's binding constraint.
8. Low cost, do if touching the file anyway: extend P2-D's rationale; add a wrong-answer callout to Bearings Q5; add one revision-prompt line per checkpoint.

Items 1–2 and 8 are edits to the answer keys and option ordering only. Items 3–7 change question content and should be re-checked for fact accuracy by the Stage 9 pass, since 4 and 6 introduce new claims.
```

**Headline for the gate:** budget and why-wrong compliance are clean (20/20 questions, 0 missing rationales, no ★ Fixed Point spoilers), but the practice set has a mechanical construction defect that makes it gameable — the key is `B` in 8 of 10 items and the longest option in 5 of 10, so a test-wise reader scores ~80% without knowledge. That matters more than usual here because §4 instructs the reader to allocate their remaining study hours from these scores. Two content defects also warrant a fix before integration: Bearings Q3 asks the reader to name a "cross-cutting thread" and expects an answer that isn't one of the chapter's nine, and the outline's deliberate two-item D4.3 weighting shipped as one — in a chapter that argues D4.3 is the best use of the reader's next study hour.