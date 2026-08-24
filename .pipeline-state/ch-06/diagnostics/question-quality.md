# Question-Quality Audit — Chapter 6

## Source artifact note (read first)

**`draft-voice.md` does not exist, and `draft-v1.md` is a truncated fragment.**

- `draft-v1.md` is 253 lines / 24 KB and **begins mid-word** (`ognition exam can ask about…`). It contains only the chapter tail: the back half of the Exam Alert, the full Practice Questions block with answer key, the Chapter Summary, The Voyage Ahead, and Safe Harbor. It carries **no Soundings and no Bearings checkpoints at all.**
- `draft-v1-prevoice.md` is 1,213 lines / 119 KB and is the complete chapter.
- The sibling `diagnostics/structural.md` was run against the truncated file and reports 8 FAILs (`Chapter Title: missing`, `Fixed Point: found 0`, `Dead Reckoning: found 0`, `Taking Your Bearings: found 0`, …). **Every one of those is an artifact of the truncation, not a defect in the chapter** — all of those elements are present in the complete draft. The three diagnostics that started at 08:24 alongside this one (fact-accuracy, curriculum-alignment, theming-density) will have consumed the same truncated input and should be re-run.

**This audit was therefore run against `draft-v1-prevoice.md`.** The overlapping region was compared between the two artifacts — the Exam Alert tail, all 19 Practice question stems and option sets, and the answer-key entries — and is identical. The voice pass did not alter any question. Soundings and Bearings could only be read from the prevoice text; if the voice stage is re-run and changes question wording, the Soundings spoiler check and the Bearings why-wrong findings below need re-verifying.

---

## Summary

- Chapter type: **content**
- Total questions inspected: **42**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **15** (across **3** checkpoints, 5 / 5 / 5)
  - Practice questions: **19**
- Question budget compliance: **met** (exactly, in every category)
- Weak distractors (WARN): **4**
- Trap answers that don't target real misconceptions (WARN): **3**
- Missing or incomplete why-wrong explanations (FAIL): **2**
- Questions with multiple defensible correct answers (FAIL): **1** *(added to the template — this is the most severe finding in the chapter)*
- Retrieval-practice spacing: **compliant** (20.6% against a 20% target)
- Soundings spoiler check: **clean** — 0 of 8 questions reveal a ★ Fixed Point
- Soundings rubric present: **yes** (6+ / 3–5 / 0–2, with a targeted 0–2 branch)
- Soundings answers in `<details>`: **yes**
- Checkpoint revision prompts (score-banded): **absent from all 3 checkpoints — WARN**

The chapter's question architecture is strong. Trap fidelity is unusually good: distractors are drawn from documented confusions rather than invented for symmetry, and the answer keys mostly name the misconception rather than just marking the option wrong. Practice Q12 (liveness-vs-readiness), Q13 (`Recreate` as a legitimate choice), and Bearings #3 Q1 (three distinct wrong-reasonings including a "right answer, wrong reason") are exemplary. The findings below are concentrated in six Practice items and one chapter-level omission.

---

## Question-budget compliance

Compared against `question_budget` in outline frontmatter:

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 15 | 15 | met |
| Taking Your Bearings (checkpoints) | ≥2 | 3 | met |
| Practice Questions | 19 | 19 | met |
| **Chapter total** | **42** | **42** | **met** |

The outline raised Bearings from B4's allocation of 10 to 15 across three checkpoints (§ Open questions #8). The draft honors that. All three checkpoints carry exactly 5, placed after §3, §5 and §8 as planned.

**One distribution drift, non-blocking.** The outline's Practice block plan is §1–§3 = 6, §4–§5 = 6, §6–§7 = 5, §8 = 2. By content the actual split is 6 / **7** / **4** / 2, because **Q13** (the exclusive-lock / `Recreate` question) sits in the §6–§7 block position but is §4 material. Totals are correct and every exam-priority topic is covered, so this is cosmetic — except that it interacts with the trap-#21 gap below, and the fix for that gap also repairs the split.

---

## Soundings spoiler check

The chapter teaches seven ★ Fixed Points:

| FP | Section | Content |
|---|---|---|
| FP1 | §1 | Chain is Deployment → ReplicaSet → Pod; Deployment holds template + update policy, ReplicaSet holds the count |
| FP2 | §3 | A controller's Pods are the Pods matching its selector; membership is a query, not a list |
| FP3 | §4 | `RollingUpdate` is the default; `maxSurge` / `maxUnavailable` both default to 25%; `Recreate` kills all old Pods first |
| FP4 | §5 | A revision is created if and only if `.spec.template` changes |
| FP5 | §6 | The deciding property is interchangeability, not disk |
| FP6 | §7 | DaemonSet = one Pod per matching node, no replica count; Job = to completion once; CronJob = creates Jobs on a schedule |
| FP7 | §8 | Custom resource alone stores data; custom resource + custom controller = operator pattern |

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | What must be written down in advance to restore a dead process | **no** | Stem names nothing Kubernetes-specific. FP1's teaching is the *layering* — which object holds the count vs. the template. The general instinct ("a count and a recipe") is the ramp, not the answer. |
| 2 | Replacing a running service without losing reachability | **no** | Stem asks the reader to describe tools they already use. FP3 is the two named bounds and their numeric defaults; nothing here approaches them. |
| 3 | List-of-names vs. rule-about-a-property | **no** — closest call in the set | Stem is a clean trade-off framing. The `<details>` answer says *"a rule stays current but can match things you didn't expect,"* which is FP2's hazard half in fully generic form — no controller, no Pod, no selector. Post-attempt disclosure preserves the pretesting effect. Acceptable. |
| 4 | Swapping a primary and a replica in a two-member database | **no** (but see WARN below) | Never names StatefulSet or Kubernetes. Answer reaches "not substitutable," which is the *problem* FP5 names a resource for, not the Fixed Point itself. |
| 5 | Log agent on every machine, including future ones | **no** | Stem explicitly contrasts with "run six copies" but names no resource. The answer's *"the count is an output of the rule, not an input to it"* is FP6's conceptual core minus the resource name — at the boundary, but it is disclosed only after the attempt, and skill Part 11 rule 3 scopes the prohibition to **question stems**. Clean. |
| 6 | Init system: web server vs. nightly backup script | **no** | systemd `service`/`oneshot` framing. Never reaches Job/CronJob or once-vs-schedule. |
| 7 | *[retrieval: ch3]* Two states a control loop compares | **no** | Tests Chapter 3's material, not Chapter 6's. FP-free by construction. |
| 8 | *[retrieval: ch5]* Node dies; what did Ch 5 say happens | **no** | The reader retrieves a *question* ("who creates the replacement?"), which is exactly the cliffhanger §1 collects. Nothing about FP1's layering is given away. |

**Verdict: clean.** No Soundings question reveals a Fixed Point. The rubric is present and correctly banded, the 0–2 branch carries the targeted instruction the outline specified (*"if questions 7 and 8 were among your misses, re-read Chapter 3 §6 and Chapter 5 §4 before starting §2"*), and answers are inside a `<details>` collapsible.

---

## Per-question findings

### P14: "A StatefulSet's Pods are also selected by labels. What does the selector *not* tell you about them?"

**Issue: FAIL — three of the four options are defensible correct answers.** Skill Part 10B lists *"ambiguous questions with multiple defensible answers"* under **undesirable** difficulty, explicitly distinguished from the desirable kind. This question is that failure mode.

**Distractor analysis:**
- A) Which Pods belong to the StatefulSet — the selector **does** tell you this. The only genuinely wrong option.
- B) That the Pods are not interchangeable with one another — keyed correct. The selector does not tell you this. ✓
- C) How many Pods the StatefulSet maintains — the selector also does not tell you this. **Defensibly correct.**
- D) Which namespace the Pods are in — the selector also does not tell you this. **Defensibly correct.**

The answer key concedes the problem rather than resolving it: *"**C** is `.spec.replicas`. **D** is `metadata.namespace`."* Both sentences confirm that C and D name things the selector does not express — which is what the stem asked for. A careful reader who picks C or D has answered the question as written and will be marked wrong.

**Why-wrong explanation status:** present and specific — but the specificity is what exposes the defect.

**Recommended fix:** rewrite the stem to demand a discriminating property, and replace C and D with claims the selector genuinely *does* express. This also closes the `matchLabels`/`matchExpressions` coverage gap flagged below:

> **14.** *[interleaved: §3 + §6]* A StatefulSet's Pods are selected by labels, exactly as a Deployment's are. Which of these is true of a StatefulSet's Pods but **cannot be expressed in the selector**?
>
> A) That they belong to this StatefulSet rather than some other controller
> B) That each holds a persistent identity and is not interchangeable with the others ✓
> C) That they carry the labels set in `.spec.template.metadata.labels`
> D) That they satisfy both `matchLabels` and `matchExpressions` when both are specified

A, C and D are all selector-expressible; B is the property that lives in the resource kind, not the labels — which is the point the interleave exists to make.

---

### P7: "A Deployment has `replicas: 8` and default strategy settings. What is the maximum total number of Pods and the minimum available?"

**Issue: WARN — options A and B assert the identical cluster state.** The discriminating clause is inert at the chosen replica count.

**Distractor analysis:**
- A) 10 max, 6 min — keyed correct ✓
- B) 10 max, 6 min — with both values rounded up — **same numbers as A.** Differs only by an appended claim about procedure.
- C) 8 max, 6 min — plausible: forgets surge headroom entirely. Good distractor.
- D) 10 max, 8 min — plausible: transposes the two bounds. The chapter's designated trap; it belongs here.

At `replicas: 8`, 25% is exactly 2 in both directions. **Nothing rounds.** A reader who computes correctly arrives at 10/6 and finds two options stating it, then has to adjudicate a rationale about a rounding operation the scenario never performs. The answer key acknowledges this — *"(With 8 replicas both values are whole, so rounding doesn't bite, which is why **B**'s 'both rounded up' is wrong as a rule even though its numbers happen to match…)"* — which is a defence of the key, not a repair of the question.

**Why-wrong explanation status:** present and specific for C and D; for B it is present but circular.

**Recommended fix:** change the replica count so rounding actually bites and every option is numerically distinct. Do **not** use 10 — Bearings #2 Q1 already uses 10 replicas and yields 13/8, and reusing it makes the Practice item a duplicate. Use 6:

> **7.** A Deployment has `replicas: 6` and default strategy settings. During a rolling update, what is the maximum total number of Pods, and the minimum that must be available?
>
> A) 8 max, 5 min ✓ *(surge 1.5 → up = 2; unavailable 1.5 → down = 1)*
> B) 7 max, 5 min *(rounds surge down)*
> C) 8 max, 4 min *(rounds unavailable up)*
> D) 7 max, 4 min *(transposes both roundings)*

Every option now maps to a distinct, identifiable arithmetic error, and the item tests the rounding asymmetry it was designed to test.

---

### P6: "Which of these is the correct reason a Deployment's `.spec.template.metadata.labels` must match its `.spec.selector`?"

**Issue: WARN (weak distractor) + FAIL (incomplete why-wrong).**

**Distractor analysis:**
- A) So that `kubectl get pods --show-labels` renders consistently — **implausible.** No reader holds a belief about a display flag driving an API validation rule. This reduces the item to three options.
- B) So that the scheduler can find a node for the Pods — **plausible to a real and common misconception**: conflating a workload's `.spec.selector` with the Pod template's `nodeSelector`. The chapter itself introduces `nodeSelector` in §7, so the confusion is live in this exact chapter.
- C) Because the controller finds its Pods by querying for the selector, so Pods it creates must satisfy that query — keyed correct ✓
- D) Because the API server uses labels to assign owner references — plausible: conflates the two membership mechanisms §3 deliberately separates. Good distractor.

**Why-wrong explanation status:** **present but vague.** D gets a specific, well-sourced correction. A and B are dismissed together in five words — *"**A** and **B** are unrelated to selector semantics."* For B that is a bare assertion where the reader needs the actual distinction: node placement is driven by `nodeSelector` / affinity **on the Pod template**, a differently-scoped field with a confusingly similar name, and the workload's `.spec.selector` never reaches the scheduler at all.

**Recommended fix:** replace A with a real misconception —

> A) Because the Deployment copies the selector into each Pod's `metadata.labels` when it creates them

— a genuine inversion (treating the selector as the *source* of the labels rather than a query over them), which §3's "membership is a query, not a list" exists to correct. Then extend the key: *"**B** confuses `.spec.selector` with `nodeSelector`. They are different fields at different scopes: the workload selector is how the controller finds its own Pods, and it is never consulted by the scheduler. Node placement is expressed inside the Pod template, by `nodeSelector` or affinity — which you'll meet in Chapter 7."*

---

### P8: "A Deployment sets `maxSurge: 0`. What must be true of `maxUnavailable`?"

**Issue: WARN (weak distractor) + FAIL (incomplete why-wrong).**

**Distractor analysis:**
- A) It must also be 0 — **plausible and well chosen.** The symmetry instinct. The key handles it well ("would deadlock the rollout, which is why it's prohibited").
- B) It must be greater than 0 — keyed correct ✓
- C) It is ignored when `maxSurge` is 0 — **plausible**: a reader may believe one bound supersedes the other, or that zeroing a field disables it rather than constraining it.
- D) It must be expressed as a percentage — **implausible.** §4 states plainly that both fields accept an absolute number or a percentage, and nothing in the chapter or the docs links the units of one bound to the value of the other. There is no misconception behind this option.

**Why-wrong explanation status:** **present but vague** for C and D — *"**C** and **D** invent behavior."* True of D, but not an explanation; and C deserves better, because the belief behind it is real.

**Recommended fix:** replace D —

> D) It must equal `.spec.replicas`, so that all Pods can be replaced at once

— a plausible over-reading of "no surge means the only way to make room is to remove Pods first." Then extend the key: *"**C** treats a bound set to zero as switched off. It isn't — zero is a real constraint, and the strictest one available: no Pod may be created above the desired count. The two fields are always both in force, which is exactly why they can't both be zero. **D** confuses a bound with a target: `maxUnavailable` caps how many Pods may be down; it does not prescribe how many should be."*

---

### P10: "You scaled a Deployment from 3 to 9 replicas, then later changed the image and immediately ran `kubectl rollout undo`. After the rollback completes, how many replicas are running?"

**Issue: WARN — one nonsensical distractor.** The item is otherwise one of the chapter's best; option A is the genuine, documented misconception and the key says so.

**Distractor analysis:**
- A) 3 — the rollback restores the state from before the scale — **the target misconception**, correctly identified in the key as "what most people expect."
- B) 9 — the replica count is not part of the Pod template — keyed correct ✓
- C) 6 — the rollback averages the two counts — **implausible.** No reader believes Kubernetes averages replica counts. Pure symmetry filler.
- D) Indeterminate, until you run `kubectl scale` — weak but defensible; a reader might think the count is left undefined.

**Why-wrong explanation status:** present and specific for A; *"**C** is invented"* is accurate, but the option should not exist.

**Recommended fix:** replace C with a technically tempting error grounded in §5's own material —

> C) 3 — the rollback scales the previous ReplicaSet back up, and that ReplicaSet still holds its old count

Key: *"**C** is the sharpest wrong answer, because the mechanism it describes is half right. Rollback does scale the previous ReplicaSet back up. But the Deployment propagates its own current `.spec.replicas` down to whichever ReplicaSet it is scaling — the count is held by the Deployment layer and pushed down, not stored per-revision. Revisions are a history of what your Pods are, not of how many."*

---

### P11: "Midway through a rolling update, `kubectl get rs` shows two ReplicaSets, one with 6 Pods and one with 5. Which is which, and why do two exist?"

**Issue: WARN — the stem asks two things and the options answer one.**

**Distractor analysis:**
- A) The Deployment created a temporary copy; only one is real — plausible. Good.
- B) The old ReplicaSet is scaling down and the new one is scaling up; both exist because the Deployment layer manages both — keyed correct ✓
- C) One belongs to the Deployment and the other belongs to a Service — plausible: conflates selection with ownership. Good, and the key handles it well.
- D) The second was created by the scheduler to hold unschedulable Pods — plausible for a reader fuzzy on component responsibilities. Fine.

**Why-wrong explanation status:** present and specific throughout.

The defect is in the stem. *"Which is which"* asks the reader to map the counts 6 and 5 onto old and new. **No option supplies that mapping**, and it is not derivable — mid-rollout with default bounds, either ReplicaSet could hold either count. The reader is asked a question the option set cannot answer, then graded on the other half.

**Recommended fix:** delete the unanswerable half — *"Midway through a rolling update, `kubectl get rs` shows two ReplicaSets for the same Deployment, one with 6 Pods and one with 5. Why do two exist?"*

---

### Trap #21 has no Practice distractor (chapter-level WARN)

The outline requires that all three B1 traps appear **as selectable distractors** in the §6–§7 Practice block, *"not only in the Exam Alert"* — on the reasoning that documented misconceptions make better distractors than invented ones.

| B1 trap | Practice distractor? |
|---|---|
| #22 — DaemonSet to "run several copies" | **yes** — P15 options A and D |
| #23 — Job vs. CronJob | **yes** — P17 options A and C |
| #21 — "writes to disk ⇒ StatefulSet" | **no** |

Trap #21 is the chapter's **#2 exam-priority topic**. It is well handled in prose (§6 Snag, §6 Fixed Point, §7 Hazards, Exam Alert) and it gets three distinct why-wrong forms in Bearings #3 Q1 — but Bearings items are **open-response**, so the misconception never appears anywhere in the chapter as an option the reader can be tempted into selecting and then corrected on. P13's option D ("A StatefulSet, because locks imply state") is a cousin, not the disk form.

**Recommended fix — repairs the trap gap and the 6/7/4/2 block drift in one edit.** Move Q13 into the §4–§5 block (renumber to follow Q9), and add a §6 selection item in the vacated slot:

> **13.** A team runs a Redis cache at three replicas. Each Pod writes its working set to a local volume so it can warm-start after a restart. Any Pod can serve any request, and losing one costs nothing but a cold cache. Which resource, and why?
>
> A) StatefulSet — the Pods write to disk *(trap #21, in its exact common form)*
> B) Deployment — the Pods are interchangeable ✓
> C) DaemonSet — caches should be node-local so clients hit a nearby instance
> D) StatefulSet — a fixed replica count implies a fixed member list

Key for A: *"This is the misconception in its most common form, and it is worth meeting as a wrong answer rather than as a warning. Writing to disk is a fact about the application. Interchangeability is a fact about how the Pods must be managed, and only the second one selects a resource. If you destroyed any one of these Pods and built an identical replacement, nothing would care which one it was — so it's a Deployment, disk or no disk."*

---

### Soundings Q4 does not isolate the variable that §6 turns on (WARN, low severity)

> **4.** Consider a two-member database: one primary, one replica, each with its own data on disk. What actually breaks if you swap which machine is which — hostnames, storage, and all?

Not a spoiler, and the best-designed item in the block for surfacing non-interchangeability before the resource has a name. But the scenario pairs identity **with** on-disk data, so it does not distinguish them — and distinguishing exactly those two things is what FP5 exists to do. A reader who takes the pre-test can reasonably come away with *"data on disk ⇒ identity matters,"* which is trap #21, arriving one section before §6 has to argue against it.

**Recommended fix:** add a contrast case so the pre-test separates the variables it is priming:

> **4.** Consider two systems. The first is a two-member database — one primary, one replica, each with its own data on disk. The second is a pair of web servers that each cache rendered pages to local disk. In which one does it matter *which machine is which*, and what makes the difference?

Keeps the metacognitive work, keeps the Kubernetes vocabulary out, and lets §6's Fixed Point land as confirmation rather than correction.

---

### No score-banded revision prompts at any checkpoint (chapter-level WARN)

Skill Part 11 ("Revision Prompts") and Part 13 ("Micro-Progress After Checkpoints") call for score-banded guidance after a checkpoint, and the Ethical Checkpoint in Part 17 lists *"Revision prompts included for low checkpoint scores"* as a publish gate.

All three checkpoints close with a **"Checkpoint: You've Now Mastered"** competence block — which discharges the progress-visibility requirement — but none carries a score band. What exists instead is per-item correction embedded in the answer keys, and it is good: Bearings #1 Q2 (*"if your answer included the word 'restarted,' reread §2"*), #1 Q4 (*"if you wrote 'the number of Pods it created,' you've described a list rather than a query — see §3"*), #2 Q2 (*"**How'd you do?** If you answered 'two,' you're in the majority… Reread §5's hazards block"*). That last one also correctly discharges Part 10B's requirement to label and normalize a designated struggle item.

The self-correction machinery is present and per-item; only the aggregate band is missing. Add three lines per checkpoint:

> **5/5:** You own this section. Continue.
> **3–4:** Solid. Review the items you missed and their explanations, then continue — §4 builds directly on the ownership chain.
> **0–2:** Stop here and re-read §1 and §3 before going on. §4 is the chapter's densest section and it is unintelligible without the middle layer.

---

## Retrieval-practice spacing

- **Chapter 6 target:** 20% of the Bearings + Practice pool, drawn from **Chapters 3–5 only** (Chapter 1 excluded by the outline; no item may test exam mechanics)
- **Actual: 20.6% — 7 of 34 items**, all correctly tagged `[retrieval: chN]`
- **Status: compliant** (also inside skill Part 10's 20–25% band for Ch 6+)

| Item | Tag | Retrieves |
|---|---|---|
| Bearings #1 Q4 | `[retrieval: ch3]` | The control loop's two states + action, filled in for a ReplicaSet |
| Bearings #1 Q5 | `[retrieval: ch4]` | Selectors as a shared join — one Pod selected by a ReplicaSet and a Service at once |
| Bearings #2 Q4 | `[retrieval: ch5]` | Readiness probes as the release-safety mechanism |
| Practice 2 | `[retrieval: ch4]` | `spec` vs `status` on a workload resource |
| Practice 4 | `[retrieval: ch5]` | Pod disposability and the new UID |
| Practice 16 | `[retrieval: ch5]` | Pod phases `Succeeded` / `Failed`, finally given a use case |
| Practice 18 | `[retrieval: ch3]` | The control loop as a general shape, vs. kube-controller-manager's built-ins |

All three of B3's named anchors landed in their designated sections. Bearings #1 carries 2 of the 3 checkpoint retrievals (40% for that checkpoint), which the outline anticipated and justified: both anchors belong to §2 and §3 and nowhere else. The chapter-level rate is what governs, and it is on target.

The two Chapter 3 retrievals are correctly **differentiated** rather than duplicated — Bearings #1 Q4 asks the reader to instantiate the loop for a ReplicaSet using the real field name; Practice 18 asks what generalizes across all controllers. That is the outline's stated intent, executed.

Soundings Q7 and Q8 also do retrieval work (Ch 3, Ch 5) but sit outside the retrieval budget by design, per the outline.

**No additions needed.**

---

## Coverage vs concepts

Every concept in the outline's `kb_tags.concepts` that the draft actually introduces, checked against all 42 questions. `B{n}.{q}` = Bearings checkpoint *n* item *q*; `P{n}` = Practice question *n*; `S{n}` = Soundings.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| workload-resource | yes (B1.1, P1) |
| deployment | yes (P1, P9, P11, B1.1) |
| replicaset | yes (P1, P3, P11, B1.4) |
| replicationcontroller-legacy | **NO** |
| pod-template | yes (P1 D, P6, B1.1) |
| podtemplatespec | yes (P9, P11) |
| ownership-chain | yes (B1.1, P1, P11) |
| owner-reference | **weak** — distractor only (P6 D); implied by P3's "bare, unowned Pod" |
| controller-adoption | yes (P3) |
| orphaning | **NO** |
| cascading-deletion | **NO** |
| replicas | yes (P1, P7, P15 D) |
| desired-replica-count | yes (B1.4) |
| manual-horizontal-scaling | yes (B2.2, P10) |
| horizontal-scaling | yes (B2.2, P10) |
| horizontalpodautoscaler | **NO** — appears in answer keys (P15, B3.2) but in no stem or option |
| label-selector | yes (P3, P5, P6, P14, B1.3, B1.5) |
| matchlabels | **NO** |
| matchexpressions | **NO** |
| selector-template-agreement | yes (P6, B1.3) |
| overlapping-selectors | yes (P5, B1.5 by contrast) |
| deployment-strategy | yes (P7, P13) |
| rolling-update | yes (P7, P11, P12, B2.1) |
| recreate-strategy | yes (P13, B2.3) |
| maxsurge | yes (P7, P8, B2.1) |
| maxunavailable | yes (P7, P8, P12, B2.1) |
| minreadyseconds | **NO** — in the §4 Dead Reckoning and the P12 answer key, but in no stem or option |
| readiness-gated-rollout | yes (P12, B2.4) |
| rollout | yes (P9, P11, B2.5) |
| revision | yes (P9, P10, B2.2) |
| rollout-history | yes (B2.2, P10) |
| rollback | yes (P10, B2.2) |
| revision-history-limit | **weak** — distractor only (P9 D), with a specific why-wrong |
| pause-rollout | yes (B2.5) |
| resume-rollout | yes (B2.5) |
| stuck-rollout | yes (P12, B2.4) |
| statefulset | yes (P14, B3.1) |
| stable-pod-identity | **NO** — see note below |
| pod-interchangeability | yes (P14, B3.1) |
| daemonset | yes (P15, B3.2) |
| node-local-facility | **NO** — primed in S5 only |
| job | yes (P16, P17, B3.3) |
| run-to-completion | yes (P16, P17) |
| cronjob | yes (P17, B3.3) |
| cronjob-schedule | yes (P17 stem: `0 4 * * *`) |
| custom-resource | yes (B3.4, P18, P19) |
| customresourcedefinition | yes (B3.4, P19 D) |
| custom-controller | yes (P18, B3.4) |
| operator-pattern | yes (P19, B3.5) |
| declarative-api | yes (P18) |
| dynamic-registration | **NO** |

Commands (`kb_tags.commands`):

| Command | Tested? |
|---|---|
| `kubectl get` | yes (P2, P11, B3.4 stems) |
| `kubectl scale` | **weak** — named only in P10 option D; the scaling *action* is tested in B2.2 and P10 |
| `kubectl rollout status` | **NO** — appears in §5's verb table only |
| `kubectl rollout history` | yes (B2.2, P10 stems) |
| `kubectl rollout undo` | yes (P10 stem) |
| `kubectl rollout pause` | yes (B2.5) |
| `kubectl rollout resume` | yes (B2.5) |
| `kubectl delete` | yes (B1.2 stem) |
| `kubectl apply` | *not introduced in the draft — exclude* |
| `kubectl describe` | *not introduced in the draft — exclude* |

`vertical-scaling` is tagged in the outline but deliberately **not introduced** (§ Open questions #4 holds it for Ch 17). Correctly absent from both draft and questions; excluded above.

### The one coverage gap worth acting on

**`stable-pod-identity`.** §6 spends a substantial block on the three parts of a StatefulSet's identity — ordinal index 0…N-1, hostname `$(statefulset name)-$(ordinal)` producing `web-0` / `web-1` / `web-2` on every reschedule, and per-Pod PVC binding — plus ordered creation and reverse-order termination. It is drawn in `ch06-fig05`. **Not one question touches any of it.** Every StatefulSet item (P14, B3.1) tests only the interchangeability *principle*. Ordinal naming is concrete, mechanically checkable, and exactly the shape a recognition exam asks about; leaving it untested means the reader never confirms encoding on the most testable half of §6.

**Recommended addition** — fold into the §6–§7 block, or extend Bearings #3 Q1 with a second part:

> A StatefulSet named `db` has `replicas: 3`. Pod `db-1` is deleted. What is the replacement's name, and what does it attach to?
>
> A) A new generated name, and a freshly provisioned volume
> B) `db-1`, and the same PersistentVolumeClaim the deleted Pod was using ✓
> C) `db-3`, because ordinals only ever increase
> D) `db-1`, but with a new volume — storage is recreated with the Pod

C targets "ordinals are a counter"; D targets exactly the misreading `ch06-fig05` is drawn to prevent (storage belongs to the identity, not to the Pod).

The remaining NOs are acceptable at associate tier and none needs action: `replicationcontroller-legacy` is a one-clause recognition item the chapter explicitly declines to develop; `orphaning` and `cascading-deletion` are named as the associate-tier fact with the machinery deliberately held back; `matchLabels` / `matchExpressions` are Chapter 4's to test (and the P14 rewrite above picks up `matchExpressions` for free); `minReadySeconds`, `dynamic-registration` and `node-local-facility` are supporting detail rather than testable claims; `kubectl rollout status` is a verb the chapter names but teaches no behavior for. `horizontalpodautoscaler` is the borderline one — §2 gives it one sentence and hands the topic to Ch 13 and Ch 17, so leaving it untested here is consistent with the scope boundary.

---

## Recommended edit list, in priority order

| # | Item | Severity | Edit |
|---|---|---|---|
| 1 | P14 | **FAIL** | Rewrite stem + options C/D — three defensible answers as written |
| 2 | P7 | WARN | Change `replicas: 8` → `6` and redistribute option values; A and B currently assert the same state |
| 3 | P6 | FAIL (why-wrong) | Replace implausible option A; expand B's why-wrong to name the `nodeSelector` conflation |
| 4 | P8 | FAIL (why-wrong) | Replace implausible option D; expand C's why-wrong to name the "zero disables the bound" belief |
| 5 | §6–§7 block | WARN | Move Q13 to the §4–§5 block; add a trap-#21 selection item in its place (restores the 6/6/5/2 split) |
| 6 | Bearings ×3 | WARN | Add score-banded revision prompts (5/5 · 3–4 · 0–2) after each "You've Now Mastered" block |
| 7 | Coverage | WARN | Add one `stable-pod-identity` item — ordinal naming and PVC reattachment are untested |
| 8 | P10 | WARN | Replace the "averages the two counts" distractor with the old-ReplicaSet-holds-its-count error |
| 9 | P11 | WARN | Drop "Which is which, and" from the stem — the options cannot discharge it |
| 10 | Soundings 4 | WARN (low) | Add a contrast case so the pre-test separates on-disk data from Pod identity |

None of these is a re-outline trigger. The budget is met exactly in every category, retrieval spacing is compliant, and the Soundings block is clean. Items 1–4 are option-set surgery on four Practice questions; the rest are additive.

---

**Note to the orchestrator:** I could not write this to `diagnostics/question-quality.md` — the `Write` tool was denied, consistent with `Write` being removed from `--allowed-tools` so stage output flows through stdout. The report above is the stage output. Separately, **`draft-voice.md` is missing and `draft-v1.md` is a truncated 24 KB fragment of a 119 KB chapter** — the voice-stage harvest captured only the tail. `diagnostics/structural.md` already ran against that fragment and its 8 FAILs are spurious. Re-run the voice stage (or restore `draft-v1.md` from `draft-v1-prevoice.md`) before re-running structural, fact-accuracy, curriculum-alignment, and theming-density.