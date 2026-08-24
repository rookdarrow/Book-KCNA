Write permission wasn't granted for the diagnostics path. That's consistent with the pipeline's design (per CLAUDE.md, `Write` is deliberately removed from `--allowed-tools` so stage output flows through stdout for atomic capture), so I'm emitting the artifact here rather than retrying the write.

---

# Question-Quality Audit — Chapter 6

<!-- Line citations are against `draft-v1.md` as it exists on disk after the voicing stage rewrote it (127,750 bytes / 1,254 lines, 2026-08-24 11:34). The truncated 4,050-byte artifact described in the draft's AUTHOR-REVIEW header is preserved as `draft-v1-prevoice.md`; it is NOT the file cited here. -->

## Summary

- Chapter type: **content**
- Total questions inspected: **42**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **15** (across 3 checkpoints, 5 each)
  - Practice questions: **19**
- Question budget compliance: **met** (42/42, exact match to outline frontmatter)
- Weak distractors (WARN): **9 options across 8 questions**
- Trap answers that don't target real misconceptions (WARN): **0**
- Missing or incomplete why-wrong explanations (FAIL): **0**
- Retrieval-practice spacing: **compliant** (20.6% combined; 20.0% Bearings-only)
- Soundings spoiler check: **clean** — no question stem reveals a ★ Fixed Point (1 answer-key WARN)

### Headline findings

The chapter's answer-key discipline is the strongest of any audited so far in this book: **all 23 multiple-choice items carry complete per-option why-wrong treatment**, with no exceptions. Zero FAILs.

Three issues are worth acting on before this ships:

1. **Two Practice slots are spent re-asking Bearings items** (Q3 ≡ Bearings #1 item 3; Q7 ⊂ Bearings #2 item 1). Same facts, same option propositions, same chapter. This is channel redundancy under skill Part 7, not spacing.
2. **Q17 is ambiguous** — three of its four options are defensible readings of the stem. Skill Part 10B names this as an *undesirable* difficulty.
3. **Six taught concepts are never tested**, including two with exam-shaped default-plus-consequence structure (`revisionHistoryLimit`, HPA). The two redundant Practice slots above are the obvious place to put them.

---

## Question-budget compliance

Compared against `question_budget` in outline frontmatter (`soundings: 8`, `taking_your_bearings: 15`, `practice_questions: 19`, `total_this_chapter: 42`).

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 15 | 15 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 | 3 | **met** |
| Taking Your Bearings (per checkpoint) | ≥5 | 5 / 5 / 5 | **met** |
| Practice Questions | 19 | 19 | **met** |
| **Chapter total** | **42** | **42** | **met** |

The outline's Open Question #8 raised Bearings from B4's allocated 10 to 15. The draft honors the raise and distributes it evenly across three checkpoints, matching the shape shipped by Chapters 3, 4 and 5. No action.

### Format-mix observation (WARN, not a budget failure)

| Block | Multiple-choice | Open-response |
|---|---|---|
| Soundings | 0 | 8 |
| Taking Your Bearings | 4 | 11 |
| Practice Questions | 19 | 0 |

**11 of 15 Bearings items carry no distractors at all.** Skill Part 11 illustrates trap-answer design using a ☆ Taking Your Bearings item specifically, so there is a stated expectation that checkpoints carry trap answers — and 73% of this chapter's checkpoint questions structurally cannot.

This is defensible: open retrieval is stronger than recognition under Bjork (skill Part 10B), and the 19 all-MC Practice questions supply the recognition practice a recognition exam needs. But it does mean the misconception-detection function of the checkpoints rests on only four items. **Recommendation:** convert two open Bearings items to MC — Bearings #2 item 3 (Recreate) and Bearings #3 item 5 (where the operator's controller runs) are the two whose wrong answers are most enumerable and most worth trapping. That moves the split to 6/9 without touching the budget.

---

## Soundings spoiler check

**Fixed Point inventory** (the baseline this check runs against) — 6 total, at draft-v1.md lines 165, 268, 483, 644, 739, 789:

| # | Section | Fixed Point content |
|---|---|---|
| FP1 | §1 (L165) | Chain is Deployment → ReplicaSet → Pod; Deployment owns template + strategy, ReplicaSet owns and enforces count |
| FP2 | §3 (L268) | Membership is a query, not a list; template labels must satisfy selector or the API rejects |
| FP3 | §5 (L483) | Revision created iff `.spec.template` changes; scaling does not create one |
| FP4 | §6 (L644) | Distinguishing property is interchangeability, not disk |
| FP5 | §7 (L739) | DaemonSet = one Pod per eligible node, count is a consequence; Job runs to completion once; CronJob creates Jobs on a schedule |
| FP6 | §8 (L789) | Custom resource alone stores data; CR + custom controller = operator pattern |

> **Note for the structural linter, not a finding of this audit:** the outline specifies ★ Fixed Points in §1, §3, §4, §5, §6, §7. The draft places them in §1, §3, §5, §6, §7, §8 — the count is right (6) but **§4 has no Fixed Point** and §8 has an unplanned one. §4 is the chapter's designated high-attention section and the one whose content (`RollingUpdate` default, both bounds at 25%, `Recreate` semantics) the Exam Alert ranks 6th. It is stated in the Dead Reckoning block instead. Flagging because the spoiler check's baseline depends on the inventory; adjudication belongs to `structural.md`.

**Per-question check** (draft-v1.md L49–L100):

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | What must be written down in advance to restore a dead process | **no** | Answer gives "the count and the recipe" — FP1's teaching is the *layering* (which object owns which), which the answer never touches. Names no resource. |
| 2 | Replacing a running service while it stays reachable | **no** | Answer is overlap-shaped and generic. §4 carries no Fixed Point; the bounds and defaults are nowhere in the stem or key. |
| 3 | List-vs-rule identification, and what each costs | **no** | Stem is abstract ("a group of things"). Answer states the generic trade-off; FP2's actual content — API rejection of selector/template mismatch — is absent. |
| 4 | Two-member database, what breaks if you swap the members | **no** | Surfaces non-interchangeability as a *problem* without naming StatefulSet or stating FP4's decision rule. Best-designed item in the block; correctly walks the reader toward the disk misconception so §6 can correct it. |
| 5 | Agent on every machine including next Tuesday's | **borderline — WARN** | See below. |
| 6 | Init system: service that shouldn't exit vs script that should | **no** | Answer stops at "exiting is failure / exiting is success." Neither Job/CronJob nor FP5's once-vs-schedule split appears. |
| 7 | `[retrieval: ch3]` The two states a control loop compares | **no** | Retrieval of Ch 3 material by design. §2 carries no Fixed Point. |
| 8 | `[retrieval: ch5]` Node dies — what did Ch 5 say, and what was left open | **no** | The reader retrieves a *question*, not an answer. Exemplary pre-test construction. |

### WARN — Soundings Q5 answer key states FP5's DaemonSet clause

**Location:** stem at L61; answer in the `<details>` block.

The stem is clean. The answer is not:

> "Express it as a property of the machine, not as a number. 'One agent per host' rather than 'six agents.' **The count is then whatever the fleet size happens to be, including next Tuesday's.**"

Set against FP5 (L739): *"DaemonSet: one Pod per eligible node, added automatically as nodes join. The count is a consequence of the cluster, not a setting."*

The bolded sentence is FP5's DaemonSet clause in all but the resource name — both halves of it (count-as-consequence, and automatic-on-join). It also pre-empts trap #22, which §7's Navigational Hazards block and Bearings #3 item 2 both exist to defuse.

Skill Part 11 rule 3 governs *stems*, so this is not a FAIL. But the same Part specifies Soundings answers as "1-line rationale each," and this one runs three sentences doing teaching work. The pre-test loses some of its diagnostic value when the answer key hands back the chapter's conclusion.

**Recommended fix:** trim to the framing and drop the gloss —

> "Express it as a property of the machine, not as a number: 'one agent per host' rather than 'six agents.'"

That preserves the calibration signal (did the reader reach for per-host or for a count?) without stating the consequence §7 is there to teach.

### Rubric and disclosure checks

- **Reading-strategy rubric:** present. 6+ / 3–5 / 0–2, all three branches, with the outline-specified 0–2 instruction ("if questions 7 and 8 were among your misses, re-read Chapter 3 §6 and Chapter 5 §4 before you start §2"). **PASS.**
- **Answer disclosure:** answers are inside a `<details><summary>Answers + reading strategy</summary>` collapsible. **PASS.**
- **Self-scoring reliability (minor):** the rubric requires the reader to land in a numeric bucket, but 5 of 8 answers give no grading criterion. Q2 and Q5 do it well ("Any overlap-based answer is correct"); Q1, Q3, Q4, Q6, Q7 leave the reader to judge whether their prose answer counts. **Recommendation:** add a one-clause "count it right if you said…" to those five. Low cost, and the rubric's whole function depends on the count being honest.

---

## Per-question findings

### Q Practice 3: "You submit a Deployment manifest whose `.spec.selector` does not match `.spec.template.metadata.labels`. What happens?"

**Location:** L998–L1003. Duplicate of **Bearings #1 item 3** (L310–L315).

**Issue:** Same fact, same four propositions, reworded. Not spacing — both sit inside Chapter 6, one checkpoint apart.

| | Bearings #1 item 3 | Practice Q3 |
|---|---|---|
| Runaway population | A | A |
| API rejects (correct) | C | B |
| Selector silently rewritten | D | C |
| Created but zero replicas | B | D |

**Distractor analysis (Q3):**
- A) Pod-creation loop it cannot terminate — **plausible; the *right* intuition landing on the wrong answer.** Excellent, and the key says so explicitly.
- B) API rejects — correct.
- C) Kubernetes copies template labels into the selector — plausible to a "Kubernetes repairs my intent" model.
- D) Created with zero replicas — plausible to a no-op-controller model.

**Why-wrong explanation status:** present and specific for all three wrong options. No defect in the item itself.

**Recommended fix:** the item is well built; the problem is that it is the *second* copy. Keep Bearings #1 item 3 (it follows §3 immediately and carries the generation-effect payoff) and re-cut Q3 to a fact currently untested. Best candidate: **`revisionHistoryLimit`** — the §5 default of 10, and the consequence that setting it to 0 removes the ability to undo. Suggested stem: *"You set `.spec.revisionHistoryLimit: 0` on a Deployment to stop old ReplicaSets accumulating. What have you given up?"* Distractors write themselves from real beliefs (nothing / only rollbacks past the previous one / the ability to undo the next rollout at all / pause-and-resume).

---

### Q Practice 7: "A Deployment has ten replicas and default strategy settings. What is the maximum total number of Pods (old plus new) that may exist at any instant during a rolling update?"

**Location:** L1034–L1040. Overlaps **Bearings #2 item 1** (L543–L549).

**Issue:** Bearings #2 item 1 asks for ceiling *and* floor at ten replicas with defaults (13 and 8). Q7 asks for the ceiling only, at ten replicas with defaults (13). Identical scenario, identical arithmetic, identical answer — a strict subset.

Q8 immediately after does the same computation at **six** replicas, which is exactly the right variation and shows the author knew how to vary it. Q7 is the slot that didn't get varied.

**Distractor analysis:**
- A) 10 — no surge at all. Thin; requires believing `maxSurge` defaults to 0, which the chapter states three times.
- B) 12 — **the money distractor.** Rounds surge down instead of up; also the number the outline itself carried before the source check corrected it. Genuinely tempting.
- C) 13 — correct.
- D) 15 — 50% surge. Defensible misremembering.

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** vary the stem so it tests something the reader hasn't just computed. Either (a) use explicit non-default values — *"`maxSurge: 0`, `maxUnavailable: 1`, eight replicas"* — which also tests the "neither may be 0 if the other is 0" rule the draft states in §4 and never assesses; or (b) invert it: give the observed ceiling and floor and ask for the replica count. Option (a) is preferred; it closes a real gap.

---

### Q Practice 17: "A StatefulSet's Pods, like a Deployment's, are found by a label selector. Given that, what does the selector *not* tell you about a StatefulSet's Pods?"

**Location:** L1124–L1130.

**Issue:** **Three of four options are defensible answers to the stem as written.** Skill Part 10B lists "ambiguous questions with multiple defensible answers" among *undesirable* difficulties — the item is hard for the wrong reason.

**Distractor analysis:**
- A) Which namespace they are in — the key rebuts with "namespace scoping is inherent to the query." Reasonable, but a reader can note that a selector expression itself carries no namespace; the namespace comes from the *request*, not the selector. Arguably true.
- B) Which of them is which — **intended correct**, and the pedagogically valuable answer.
- C) Whether they are running — the key rebuts with "readiness is on the Pod's status, which the selector leads you to." **This rebuttal defeats B by the same logic:** identity is on the Pod's metadata, which the selector also leads you to. The two options are not distinguished by the reasoning the key offers.
- D) How many there should be — the key concedes it "is not something the selector was ever going to tell you either." That is an admission the option is *also correct*.

The key's treatment of C and D reads as rationalization rather than refutation, which is the signature of an item whose stem doesn't isolate its answer.

**Why-wrong explanation status:** present for all three, but **C and D are not actually refuted** — they are conceded and then set aside.

**Recommended fix:** re-stem so the discrimination is mechanical rather than interpretive. Suggested replacement:

> **Q17.** 🟡 A StatefulSet's Pods all match its label selector, exactly as a Deployment's do. A StatefulSet nevertheless guarantees something about its Pods that no selector could express. What is it, and what carries it?
>
> A) That they are all running — carried by the readiness probe
> B) That each Pod keeps a stable ordinal identity and hostname across rescheduling — carried by the Pod's ordinal and derived name, not by the selector
> C) That there are exactly `.spec.replicas` of them — carried by the selector's match count
> D) That they share a namespace — carried by the selector's scope

This keeps the concept, makes B uniquely correct, and turns C and D into genuinely wrong claims that can be refuted rather than conceded. It also picks up the per-Pod name label the draft mentions in §6 and nothing currently tests.

---

### Q Practice 19: "What does a custom controller written by a third party have in common with a built-in controller… and where does each of them run?"

**Location:** L1142–L1148.

**Issue:** **Answer-length tell.** The correct option is roughly three times the length of the mean distractor and is the only one that answers both halves of the two-part stem. A test-wise reader selects B without engaging the content.

| Option | Approx. words | Answers both halves of the stem? |
|---|---|---|
| A | 13 | partially |
| **B (correct)** | **45** | **yes** |
| C | 16 | partially |
| D | 8 | no |

**Distractor analysis:**
- A) Nothing structural; different API, privileged processes — plausible to a "custom code must be privileged to extend a platform" model. Real.
- B) Correct, and conspicuous.
- C) Both run inside the API server — **genuinely real.** Many practitioners believe controllers live in the API server rather than talking to it. Best distractor here.
- D) Both run on every node as DaemonSets — **filler.** No identifiable belief produces this; the chapter has just spent §7 establishing what a DaemonSet is for, and nothing in it suggests controllers.

**Why-wrong explanation status:** present and specific for all three, including D.

**Recommended fix:** two edits.
1. Balance lengths — trim B to *"Both follow the same control loop (read `.spec`, act, write `.status`), but built-ins ship inside the control plane while a custom controller normally runs as an ordinary Deployment"* and expand A, C, D to comparable length.
2. Replace D with a real misconception: *"Both are registered with the API server through a CustomResourceDefinition, which is what makes a controller discoverable"* — conflates the CRD (the noun) with the controller (the verb), which is the exact confusion FP6 and Bearings #3 item 4 exist to correct, and would interleave the two nicely.

---

### Q Practice 9: "Which of the following is the correct reason to choose `Recreate` over `RollingUpdate`?"

**Location:** L1052–L1058.

**Issue:** One fabricated distractor.

**Distractor analysis:**
- A) Faster, because Pods aren't replaced one at a time — **real rationalization**, and the one people actually offer. Strong.
- B) Correct (two versions cannot coexist).
- C) Preserves revision history, which `RollingUpdate` discards — **fabricated.** Nothing in the chapter, the source material, or field practice suggests `RollingUpdate` discards revision history; §5 establishes the opposite in plain terms (all history kept by default, ten deep). No reader holds this belief, so the option converts Q9 into a three-option item.
- D) Avoids the need for readiness probes — plausible to someone who thinks probes exist only to gate rollouts. Acceptable.

**Why-wrong explanation status:** present and specific for all three. C's rebuttal is correct but has nothing to correct.

**Recommended fix:** replace C with a *true-sounding, partially-true* claim, which is what makes a good trap here:

> C) It needs no spare capacity, because no surge Pods are ever created

That is materially true (`Recreate` does not surge) and is a real reason people reach for it on capacity-constrained clusters — but it is not the *correct* reason, because the availability cost dominates and a `maxSurge: 0` rolling update achieves the same thing without downtime. The why-wrong then teaches something instead of denying a claim nobody made.

---

### Q Practice 13: "Which of these workloads most clearly requires a StatefulSet rather than a Deployment?"

**Location:** L1088–L1094.

**Issue:** Options A and B are **duplicate in meaning** — both are "writes to disk but is nonetheless interchangeable," failing for the identical reason. The key confirms this by grouping them: *"A and B are both distractors built from the disk misconception."* One option slot is wasted.

**Distractor analysis:**
- A) Web front end caching rendered pages to local disk — disk misconception (trap #21). Real.
- B) Image-resizing service writing temp files — disk misconception. **Same misconception, second instance.**
- C) Correct.
- D) Batch importer writing to object storage — distinct: durable output, no identity. Good.

**Why-wrong explanation status:** present, but A and B are treated as one, which is the tell.

**Recommended fix:** re-cut B to target a *different* real error in the same decision:

> B) A message consumer that must never have two instances processing the queue simultaneously

This targets "singleton ⇒ StatefulSet," a distinct and common mistake with a different correct answer (Deployment with `replicas: 1`). It also interleaves against §7's decision tree rather than repeating §6's single criterion, and gives the key something new to say.

---

### Q Bearings #1 item 5: "What would it mean for one Pod to be selected by both a ReplicaSet and a Service at the same time?"

**Location:** stem L325, answer L348. Tagged `[retrieval: ch4]`.

**Issue (two, both about the tag rather than the item):**

1. **The stem supplies the retrieval target.** It opens *"Chapter 4 listed several things that use label selectors and told you a ReplicaSet was one of them"* — handing the reader the Chapter 4 fact rather than requiring them to produce it. Retrieval practice requires generation; a reminder is not a retrieval. The item is doing forward-setup work for Chapter 9, which is legitimate and valuable, but it is not spaced retrieval and the tag overstates it.
2. **No anticipated-wrong treatment.** The key is a clean exposition ending *"If you found this one hard, good."* The obvious wrong answer — that dual selection is a conflict, a double-ownership problem, or something that needs resolving — is never named, so a reader who held it leaves holding it. This is the item most likely to be missed in the checkpoint, and it has the least error-correction attached.

**Why-wrong explanation status:** *present but incomplete* — correct answer explained well, anticipated wrong answer absent.

**Recommended fix:**
- Cut the stem's first clause so the reader must retrieve unaided: *"In Chapter 9 you will meet a Service, which finds its backend Pods the same way a ReplicaSet does. What would it mean for one Pod to be selected by both at once?"*
- Append to the key: *"If you answered that this is a conflict, or that one of them must win, re-read §3's closing distinction. Ownership is exclusive; selection is not. A Pod can satisfy any number of independent queries, and none of them own it by doing so."*

This also matters because it is one of only three Bearings retrieval items — see the spacing section.

---

### Minor distractor findings (WARN, no structural change needed)

| Item | Location | Weak option | Assessment | Suggested replacement |
|---|---|---|---|---|
| Bearings #1 item 1 | L312 | D) "Deployment → Node → Pod. The Node holds the count." | **Filler.** No reader who finished Chapter 5 places a Node in the ownership chain or gives it a replica count. Reduces a load-bearing item to three options. | "Deployment → ReplicaSet → Pod. The Deployment holds both the count and the template; the ReplicaSet only watches." — targets the real half-understanding that the ReplicaSet is passive. |
| Bearings #2 item 1 | L548 | D) "12 and 7 — 25% applies jointly to the pair" | **Numbers don't follow from the stated misconception.** A shared 25% budget is a real belief, but it doesn't yield 12 and 7 by any arithmetic; a reader would have to hold the joint-budget belief *and* round inconsistently. The label is doing work the numbers don't support. | "12 and 8 — the 25% is a single budget split between surge and unavailability" — keeps the misconception, attaches numbers that a reader holding it would actually produce. |
| Practice Q5 | L1021 | D) "a new Pod that inherits the previous Pod's name and UID for continuity" | **Internally incoherent** — a new Pod inheriting both name and UID is definitionally the same Pod. Key rebuts with "UIDs are not reused," which is thin. | "A new Pod that reuses the old Pod's name but receives a new UID" — this is *true for StatefulSets* and false for the ReplicaSet case in the stem, making it a genuine trap that also interleaves against §6. |
| Practice Q14 | L1099 | A) "One Pod; three more nodes changes nothing" | Thin, though not baseless — reads "daemon" as "one daemon." Weakest of Q14's three, but the item is otherwise strong and C/D carry trap #22 properly. | Acceptable as-is; if edited, "One Pod per DaemonSet per namespace" is a closer near-miss. |
| Practice Q18 | L1135 | A) "A namespace annotation on the CRD" | **Invented.** No practitioner reaches for a namespace annotation when a CRD appears inert. | "RBAC permissions granting access to the new resource" — the real first thing people check when nothing happens, and wrong for an instructive reason (the object *was* retrievable, so access is not the issue). |

---

## Retrieval-practice spacing

- **Chapter 6 target:** 20–25% per skill Part 10 (Chapter 6+ → "20–25% from all previous"). Outline `[B3]` specifies **20%**, sourced from Chapters 3–5, allocated 3 Bearings + 4 Practice against a combined pool of 34.
- **Actual:** **7 of 34 = 20.6%** combined. Bearings-only: **3 of 15 = 20.0%**. Practice-only: 4 of 19 = 21.1%.
- **Status: compliant.** All three measures sit inside the band.

Chapter 1 is correctly excluded (outline `[B3]` bars it), and no retrieval item tests exam mechanics.

**Tagged items:**

| Location | Tag | Source chapter concept | Genuine retrieval? |
|---|---|---|---|
| Soundings 7 (L65) | `ch3` | Control loop: two states + action | yes — *outside the budget by design; Soundings sits apart from the retrieval allocation* |
| Soundings 8 (L67) | `ch5` | Pod replaced, not rescheduled | yes — *outside the budget; retrieves a question rather than an answer* |
| Bearings #1 item 4 (L323) | `ch3` | Control loop, instantiated for a ReplicaSet | **yes** — stem scaffolds ("two states and an action") without naming them |
| Bearings #1 item 5 (L325) | `ch4` | Label selectors as universal join | **weak** — stem supplies the Ch 4 fact; see per-question finding above |
| Bearings #2 item 4 (L554) | `ch5` | Readiness probes as release safety | **yes, but recency-loaded** — §4 taught this ~70 lines earlier, so the gap is short. It is the pinned Ch 5 payoff, so placement is correct; just note it is doing less spacing work than the tag implies |
| Practice Q2 (L989) | `ch4` | `spec` vs `status` | **yes** — clean, unassisted |
| Practice Q5 (L1016) | `ch5` | Replacement Pod, new UID | **yes** |
| Practice Q16 (L1115) | `ch5` | The five Pod phases | **yes** — and the strongest of the set; retrieves the two phases Ch 5 taught with no use case attached |
| Practice Q19 (L1142) | `ch3` | Control loop as a general shape | **yes** — correctly distinguished from Bearings #1 item 4 (generalization vs instantiation), per the outline's explicit instruction |

**`[B3]` named-anchor placement — all three honored:**

| Named anchor | Required placement | Actual | Status |
|---|---|---|---|
| Control loop (Ch 3) visible in a named controller | Bearings #1 item 4 | Bearings #1 item 4 | ✓ |
| Selectors (Ch 4) as the ReplicaSet→Pod join | Bearings #1 item 5 | Bearings #1 item 5 | ✓ (item quality noted above) |
| Probes (Ch 5) as what makes a rolling update safe | Bearings #2 item 4 | Bearings #2 item 4 | ✓ |

**Recommended additions:** none required — the chapter is compliant. If Bearings #1 item 5's stem is tightened as recommended, the item becomes genuine retrieval and the Bearings-only rate becomes robust rather than nominal. No count change needed.

---

## Coverage vs concepts

Checked against `kb_tags.concepts` (52) and `kb_tags.commands` (10) in outline frontmatter. "Tested" means a question requires the reader to produce or discriminate the concept — not merely that the answer key cites it.

Key: **B**n.m = Bearings checkpoint n item m · **Q**n = Practice n

| Concept introduced in chapter | Tested in a question? |
|---|---|
| workload-resource | yes (B1.1, Q1) |
| deployment | yes (B1.1, B2.1, Q1, Q3, Q10) |
| replicaset | yes (B1.1, B1.2, B1.4, Q1, Q4) |
| replicationcontroller-legacy | **NO** |
| pod-template | yes (B1.1, B1.3, Q3) |
| podtemplatespec | yes (B2.2, Q10) |
| ownership-chain | yes (B1.1, Q1) |
| owner-reference | yes (Q6) |
| controller-adoption | yes (Q4) |
| orphaning | *not taught (out of scope per outline Open Q #3)* |
| cascading-deletion | yes (Q6) |
| replicas | yes (B1.4, Q2, Q14) |
| desired-replica-count | yes (B1.4, Q2) |
| manual-horizontal-scaling | yes (B2.2, Q10) |
| horizontal-scaling | yes (B2.2, Q10) |
| vertical-scaling | *not taught (deliberate, outline Open Q #4)* |
| horizontalpodautoscaler | **NO** |
| label-selector | yes (B1.3, B1.5, Q3, Q4, Q17) |
| matchlabels | **NO** |
| matchexpressions | **NO** |
| selector-template-agreement | yes (B1.3, Q3) |
| overlapping-selectors | **NO** |
| deployment-strategy | yes (B2.3, Q9) |
| rolling-update | yes (B2.1, Q7, Q8, Q12) |
| recreate-strategy | yes (B2.3, Q9) |
| maxsurge | yes (B2.1, Q7, Q8) |
| maxunavailable | yes (B2.1, Q7, Q8) |
| minreadyseconds | partial — the *availability gate* is tested (B2.4, Q12); the field itself is not |
| readiness-gated-rollout | yes (B2.4, Q12) |
| rollout | yes (B2.5, Q11) |
| revision | yes (B2.2, Q10, Q11) |
| rollout-history | yes (B2.2, Q10) |
| rollback | yes (Q11) |
| revision-history-limit | **NO** |
| pause-rollout | yes (B2.5) |
| resume-rollout | yes (B2.5) |
| stuck-rollout | yes (B2.4, Q12) |
| statefulset | yes (B3.1, Q13, Q17) |
| stable-pod-identity | yes (Q17) |
| pod-interchangeability | yes (B3.1, Q13) |
| daemonset | yes (B3.2, Q14) |
| node-local-facility | partial — the count property is tested (B3.2, Q14); the *purpose* (storage daemon / log agent / networking plugin) is not |
| job | yes (B3.3, Q15, Q16) |
| run-to-completion | yes (Q15, Q16) |
| cronjob | yes (B3.3, Q15) |
| cronjob-schedule | **NO** |
| custom-resource | yes (B3.4, Q18) |
| customresourcedefinition | yes (B3.4, Q18) |
| custom-controller | yes (B3.4, B3.5, Q18, Q19) |
| operator-pattern | yes (B3.5, Q19) |
| declarative-api | partial — appears in Q18's key, not in any stem or option |
| dynamic-registration | partial — appears in B3.4's rebuttal of option D, not tested directly |

| Command introduced in chapter | Tested in a question? |
|---|---|
| kubectl-get | yes (used as the observable in B1.2, Q14) |
| kubectl-describe | *not taught (deferred to Ch 13)* |
| kubectl-apply | yes (as context in B1.3, Q3) |
| kubectl-scale | partial — the *operation* is tested (B2.2), the verb is never named in a question |
| kubectl-rollout-status | **NO** |
| kubectl-rollout-history | yes (B2.2, Q10) |
| kubectl-rollout-undo | yes (Q11) |
| kubectl-rollout-pause | yes (B2.5) |
| kubectl-rollout-resume | yes (B2.5) |
| kubectl-delete | yes (B1.2, Q6) |

### Coverage gaps worth closing

Six taught concepts get no assessment. Ranked by cost:

1. **`revisionHistoryLimit`** — §5 teaches a specific default (10) and a specific consequence (setting 0 removes the ability to undo). Default-plus-consequence is the single most exam-shaped structure in the chapter, and it appears in the Chapter Summary as though it had been assessed. **Highest-value addition.**
2. **HorizontalPodAutoscaler** — taught in §2, listed in the Chapter Summary, cited in Q14's key as supporting evidence, never the object of a question. The outline deliberately caps HPA depth at one clause, so a single recognition item ("what writes `replicas` when it isn't you?") is proportionate and sufficient.
3. **Overlapping selectors** — §3 spends an entire Logbook Entry sidebar on the two-controllers-fighting failure and its signature. Q4 tests *adoption of a bare Pod*, which is adjacent but not the same mechanism. A whole sidebar with no retrieval path is the largest teach-without-test imbalance in the chapter.
4. **CronJob idempotency** — §7 flags, with emphasis, that a CronJob creates a Job *approximately* once per schedule and that "the Jobs you define should be idempotent." Operationally significant, source-backed, untested. The `.spec.schedule` five-field syntax is likewise only shown in B3.3's answer, never asked.
5. **`kubectl rollout status`** — the only verb in §5's six-row command table with no question behind it.
6. **ReplicationController** — one clause in §1 by design (outline Open Q #7). Untested is proportionate to how it is taught; **no action needed**, listed for completeness.

`matchLabels` / `matchExpressions` are Chapter 4 material retrieved in passing; leaving them untested here is correct — Chapter 4 owns their assessment.

### Where the additions fit

The chapter is exactly at budget (42/42), so additions must displace, not extend. The two redundant Practice items identified above are the natural slots, and the mapping is clean:

| Slot | Currently | Replace with | Closes |
|---|---|---|---|
| Q3 | duplicate of Bearings #1 item 3 | `revisionHistoryLimit` default + the undo consequence | gap 1 |
| Q7 | subset of Bearings #2 item 1 | non-default `maxSurge`/`maxUnavailable`, including the "neither may be 0 if the other is 0" rule | gap 5 partially, plus an untested stated rule |

That leaves HPA, overlapping selectors and CronJob idempotency still uncovered. Closing those requires either a budget raise or three further displacements; **recommendation is to take the two free slots now and raise the question with the author on the remaining three**, since the outline's Open Question #8 already anticipated that Stage 8 would cut weak items and the chapter has room under the book's 300-question floor.

---

## Trap fidelity

Every distractor that the answer key presents as targeting a known misconception was checked against the outline's B1 trap catalogue and the cached source material. **No fabricated traps found — 0 WARNs in this category.**

| Trap | Outline source | Where it appears as a distractor | Real? |
|---|---|---|---|
| #21 Deployment vs StatefulSet is about disk | B1 `[source]` | Q13 A/B, B3.1 | **yes** — documented |
| #22 DaemonSet to "run several copies" | B1 `[source]` | Q14 C, B3.2 | **yes** — documented |
| #23 Job vs CronJob confusion | B1 `[source]` | Q15 A/C, B3.3 | **yes** — documented |
| Scaling creates a revision | cached Deployment source | Q10 C, B2.2 | **yes** |
| `maxSurge`/`maxUnavailable` transposed | cached Deployment spec source | Q7 B, Q8 B/C/D, B2.1 A/C | **yes** |
| "`Recreate` is a mistake" | cached Deployment source | Q9 A | **yes** |
| "Installing a CRD makes something happen" | cached custom-resources source | Q18 B/C/D, B3.4 A/B/D | **yes** |

The outline's requirement that all three B1 traps appear as distractors in the §6–§7 Practice block *and not only in the Exam Alert* is **met** (Q13, Q14, Q15).

**Boundary note on the count.** The nine weak distractors reported in the Summary are weak on *plausibility*, not fidelity. In every case the answer key correctly presents them as simply false rather than as documented traps — so none is a mislabeled trap, and the fidelity count is properly 0. The two categories are kept separate deliberately; conflating them would overstate the severity of what are, in the main, filler-option problems.

---

## Why-wrong explanation status

**Multiple-choice items: 23 of 23 complete. Zero FAILs.**

| Block | MC items | Complete per-option why-wrong |
|---|---|---|
| Bearings #1 | items 1, 3 | 2 / 2 |
| Bearings #2 | item 1 | 1 / 1 |
| Bearings #3 | item 4 | 1 / 1 |
| Practice | Q1–Q19 | 19 / 19 |

Every wrong option is addressed, either individually or in an explicitly-flagged group where two options fail for one reason (Q2 A/B, Q5 A/C, Q13 A/B, Q14 C/D). The grouping is legitimate where the shared reason is stated — though at Q13 it doubles as the evidence that A and B are redundant.

Several keys go beyond the requirement in ways worth preserving: Q7 names its own most instructive wrong answer, Q3 and Bearings #1 item 3 both tell the reader that option A is "the *right* intuition" landing wrong, and Bearings #2 item 2 is explicitly labeled as a struggle item with the miss normalized (skill Part 10B). Q16's rebuttal of the invented `Completed` phase — noting that the word genuinely appears in `kubectl get pods` output as a container-state reason, which is *why* the distractor works — is the best single why-wrong in the chapter.

**Open-response items: 5 of 11 carry anticipated-wrong-answer treatment; 6 do not.**

Open items have no enumerated wrong answers, so this is not a FAIL against the skill's requirement. It is a self-correction gap: the skill's error-detection design assumes the key catches the misconception the reader actually held.

| Open item | Anticipated wrong answer addressed? |
|---|---|
| Bearings #1 item 2 | no — states the correct mechanism only |
| Bearings #1 item 4 | **yes** — "If your answer for current state was 'the number of Pods it created'…" |
| Bearings #1 item 5 | no — see per-question finding |
| Bearings #2 item 2 | **yes** — "If you answered 'one,' you are in good company…" |
| Bearings #2 item 3 | no |
| Bearings #2 item 4 | partial — "Users experience nothing" implicitly corrects "the service goes down" |
| Bearings #2 item 5 | partial — explains the cost of omitting `pause` |
| Bearings #3 item 1 | **yes** — names the wrong version and its failure in both directions |
| Bearings #3 item 2 | partial — explains the count without naming the belief |
| Bearings #3 item 3 | **yes** — "If your answer was 'a Job with a schedule on it'…" |
| Bearings #3 item 5 | no — the likely wrong answer ("in the control plane" / "as a static Pod") is never named |

**Recommendation:** add one anticipated-wrong clause to Bearings #1 item 2, Bearings #1 item 5 and Bearings #3 item 5. Item 5 of Bearings #3 is the priority — it is the 🟡 item the outline designates as the direct precursor to Chapter 15's recognition, and a reader who leaves believing the operator runs in the control plane will misread Chapter 15's central move.

---

## Verdict

**PASS with 3 actionable warnings.**

No FAIL conditions triggered: budget met exactly, Soundings clean of Fixed-Point spoilers, rubric and `<details>` disclosure both present, retrieval spacing compliant, and complete why-wrong coverage across every multiple-choice item in the chapter.

Ordered by value of fixing:

1. **Redundancy** — re-cut Practice Q3 and Q7 (each duplicates a Bearings item) into `revisionHistoryLimit` and a non-default-bounds item. Closes two coverage gaps at zero budget cost.
2. **Ambiguity** — re-stem Practice Q17 so its answer is unique; the current key concedes two distractors rather than refuting them.
3. **Distractor quality** — nine filler or incoherent options across eight questions, with Q9 C, Q19 D and Q5 D the three worth replacing outright. Suggested replacements are given inline above and are drawn from real misconceptions rather than invented for symmetry.

Two smaller items, both cheap: trim Soundings Q5's answer so it stops stating §7's Fixed Point, and add anticipated-wrong clauses to the three open Bearings items that lack them.

---

**Two notes on the run itself:**

- The audit ran against `draft-v1.md` on disk (1,254 lines), which I verified matches the voiced text supplied in the stage prompt — so the line citations above are live, not against the truncated `draft-v1-prevoice.md`.
- One out-of-scope observation surfaced and is flagged for `structural.md` rather than acted on here: the draft's six ★ Fixed Points sit in §1/§3/§5/§6/§7/§8, but the outline specifies §1/§3/§4/§5/§6/§7. The count is right; **§4 has none**, which matters because §4 owns the rolling-update defaults the Exam Alert ranks 6th. That content currently lives in §4's Dead Reckoning block instead.