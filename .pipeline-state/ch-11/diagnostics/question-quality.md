I can't write files in this session — the harness holds this stage to stdout, as the pipeline intends. Emitting the document (target path: `../Book-KCNA/.pipeline-state/ch-11/diagnostics/question-quality.md`).

---

# Question-Quality Audit — Chapter 11

## Summary

- Chapter type: **content**
- Total questions inspected: **40**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **15** (across **3** checkpoints of 5)
  - Practice questions: **17**
- Question budget compliance: **met** (all four categories exact)
- Weak distractors (WARN): **6** — 5 individual options plus 1 question whose entire option set is defeated by a format tell
- Trap answers that don't target real misconceptions (WARN): **0** — all nine named traps (B1 #63–69 plus the two sourced additions) appear as distractors and every one maps to a documented misconception
- Missing or incomplete why-wrong explanations (FAIL): **2** (P4, P8)
- Retrieval-practice spacing: **compliant** — Bearings 20.0% (3/15), Practice 17.6% (3/17), combined 18.8% (6/32); ≥4-back floor met on 5 of 6 items
- Soundings spoiler check: **clean** — 0 of 8 stems reveal a ★ Fixed Point

Two structural findings sit outside the FAIL/WARN counts and are the highest-value edits in this report: **B3.5 is answerable from option form alone**, and the **Practice Question distribution under-serves §2** — the section carrying the blueprint's explicitly named three-way distinction received 2 of 17 items against an outline target of 4, while §1 received 5 against a target of 3.

---

## Question-budget compliance

Compared to `question_budget` in outline frontmatter:

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 15 | 15 | met |
| Taking Your Bearings (checkpoints) | ≥2 (outline: 3) | 3 | met |
| Practice Questions | 17 | 17 | met |
| **Chapter total** | **40** | **40** | **met** |

Checkpoint placement matches the outline exactly: after §2, §4, §6. Each checkpoint carries 5 questions, satisfying skill Part 8's "≥5 per checkpoint" floor. Bearings #2 carries the required Part 10B challenge labelling ("⚠️ These questions are intentionally challenging"), with struggle normalisation and a follow-on achievable win (§5) as the skill specifies.

All three checkpoints close with a differentiated revision prompt naming a specific section and a re-reading time estimate. Bearings #2's prompt is the strongest in the chapter — it branches on *which* question was missed ("If only question 3 went wrong, the gap is §3's `WaitForFirstConsumer` subsection rather than §4"), which is the self-correction design working as intended.

---

## Soundings spoiler check

The chapter's seven ★ Fixed Points, against which each stem was checked: (1) three lifetimes / two boundaries; (2) PV is supply, PVC is demand, Pods reference claims; (3) dynamic provisioning requires two conditions; (4) RWO counts nodes, RWOP counts Pods; (5) dynamic volumes inherit the class's reclaim policy, defaulting to `Delete`; (6) CSI is a cross-orchestrator published contract closing a set of four; (7) a StatefulSet's PVCs outlive the Pod and the StatefulSet.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| S1 | Container writable layer after crash+restart (Ch 2 §2, Ch 5 §4) | **no** | Discloses rung one only, which Ch 2 taught and graded. The ladder's *count* and its second boundary — the distinctive content of FP1 — are absent from the stem. |
| S2 | The two things a Pod's containers share (Ch 5 §1) | **no** | Verbatim Ch 5 retrieval. Says only that one of the two "is what this entire chapter is about," which is a scope pointer, not a claim. |
| S3 | PV namespaced or cluster-scoped, and how to settle it (Ch 4 §3) | **no** | Names `PersistentVolume` but asks *only* about scope, which Ch 4 taught, graded, and put in its Chapter Summary. No hint of the supply/demand split (FP2). |
| S4 | StatefulSet non-interchangeability + what Ch 6 deferred (Ch 6 §6) | **no** | The answer previews the five deferred verbs, but shipped `chapter-06` line 862 already stated them in those exact terms. Nothing new disclosed; FP7's survival rule is not touched. |
| S5 | Who creates a LUN vs who requests one (general prior) | **no** — *nearest approach* | Answer says "That separation is the entire point of the arrangement," which is FP2's *shape*. But it is posed entirely outside Kubernetes and names no API object, so it builds the prior without pre-empting the claim. This is the intended generation-effect design. |
| S6 | Name the pluggable interfaces met so far (Ch 2 §4, Ch 6 §8, Ch 9 §1) | **no** — *closest stem in the set* | Stem: *"say what each one hands to somebody outside the Kubernetes project."* That phrasing carries the general shape of FP6. It clears because shipped `chapter-10` line 1866 already told the reader verbatim: *"you will meet the last of the four pluggable interfaces… Chapter 11 brings CSI, at storage, and that closes the set."* This is arrived knowledge by definition. FP6's distinctive content — that CSI is *cross-orchestrator*, not a Kubernetes feature — is nowhere in the stem or answer. |
| S7 | Delete a VM, does the disk go? Does it depend on provisioning history? (general prior) | **no** — *near approach* | Establishes that provisioning history determines deletion behaviour, which is FP5's intuition, without naming `Retain`, `Delete`, StorageClass, or inheritance. |
| S8 | Two machines mounting one block device read-write (general prior) | **no** | Establishes the physical constraint that makes RWO sensible while deliberately withholding the unit. FP4's revelation (nodes, not Pods) still lands unspoiled in §4. |

**Rubric check: PASS.** The 6+ / 3–5 / 0–2 reading-strategy rubric is present and complete. The 0–2 branch correctly implements the outline's PREREQ NOTE, naming three *sections* rather than three chapters — "That is three sections, not three chapters" — which is the right call given this chapter's dependency shape.

**Answer disclosure: PASS.** Answers are inside `<details><summary>Click for answers + reading strategy</summary>`.

**Two observations, neither a finding:**

The Soundings are **open-ended short-answer** while all 32 other questions are four-option multiple choice. The skill's Part 11 template is format-agnostic, and the outline designed them this way deliberately, so this is not a violation. But the rubric branches on an integer score, and six of the eight questions are compound (two clauses each — S1, S3, S4, S6, S7, S8). A reader who answers one clause of S1 correctly must self-adjudicate whether that counts as "right," and the reading strategy they select depends on that judgment. If a future retro wants a cheap improvement, scoring guidance ("count a question right only if both halves are right") would cost one sentence.

Second: Part 11 specifies "answers with 1-line rationale each." S5, S7, and S8 run three to four sentences. They read well and they carry the prior-building work the outline wanted, but they teach rather than score, which slightly dilutes the pre-test function.

---

## Per-question findings

### QB3.5: "Which of the following is *not* one of the four pluggable interfaces this book has now collected, and which chapter introduced the one you would substitute for it?"

**Issue:** The correct option is identifiable from its **form alone**, with zero domain knowledge. This is the most serious question-architecture defect in the chapter.

**Distractor analysis:**
- A) `CRI — Chapter 2` — true statement, correctly attributed; functions only as filler
- B) `CNI — Chapter 9` — true statement, correctly attributed; filler
- C) `CSI — Chapter 11` — true statement, correctly attributed; filler
- D) `CIS — none; the fourth is CRDs, introduced in Chapter 6` — **contains its own answer, and is the only option that breaks the `<ACRONYM> — Chapter <N>` pattern**

Three independent tells point at D before any reasoning: it is the only option whose text says "none"; it is the only one that answers the stem's *second* clause; and "CIS" is a transposition of "CSI," which option C already lists. A test-wise reader with no Kubernetes knowledge scores this correctly every time.

The two-part stem is itself part of the problem — because only the correct option can answer "which chapter introduced the one you would substitute," the question's own structure forces the tell.

**Why-wrong explanation status:**
- Present but lumped: "A, B, and C are all genuine members and are correctly attributed." Adequate for a NOT-question in isolation, but with the format tell it corrects nothing.

**Recommended fix:** Rebuild with uniform option form so the wrongness lives in content, not shape. Vary the *boundary* rather than the acronym:

> Which pairing is wrong?
> A) CRI — the container runtime — Chapter 2
> B) CNI — the network — Chapter 9
> C) CSI — storage — Chapter 11
> D) CRD — the container runtime — Chapter 6

Every option now has identical form; D is wrong on the boundary while carrying the right acronym and chapter, and CRI/CRD confusion is a real and common slip. Note that P12 already tests the four-interface *pattern* well, so this slot is free to test set membership specifically without redundancy.

Keep the rebuilt item **untagged** for retrieval. §5 explicitly teaches "you hold all four," making it chapter material; tagging it would push Bearings retrieval to 26.7%, over the skill's Part 10 ceiling.

---

### QP4: "Which pair correctly describes the scoping of these two objects?"

**Issue:** Why-wrong explanations are lumped and vague. **FAIL** against rule 3.

**Distractor analysis:**
- A) `PV namespaced; PVC namespaced` — plausible to a reader who generalises "most things are namespaced"
- B) correct
- C) `PV cluster-scoped; PVC cluster-scoped` — **the strongest distractor in the question and the one that gets no treatment.** A reader who correctly remembers PV is cluster-scoped and assumes the claim follows its supply is exactly the target reader here
- D) `PV namespaced; PVC cluster-scoped` — the exhaustive-2×2 fourth cell; weakest option, though the key does address it

**Why-wrong explanation status:**
- **Present but vague.** Verbatim: *"A, C, and D each get at least one half wrong. D inverts both."* A and C receive no individual correction. "Gets at least one half wrong" does not tell a reader which half, or why they believed it.

**Recommended fix:** Replace the lumped line with three specific rebuttals, and make C's the substantive one, since it is the only wrong answer a reader arrives at by reasoning rather than by guessing:

> - **A is wrong** on the PV: a PersistentVolume is a cluster resource *"just like a node is a cluster resource"* — it belongs to no namespace because it belongs to no team.
> - **C is wrong** on the PVC, and it is the most reasonable wrong answer here: having correctly placed the PV at cluster scope, it assumes the claim follows its supply. It does not. *Claims must exist in the same namespace as the Pod using the claim.* Demand is owned by whoever owns the namespace; supply is owned by the cluster. That is the supply/demand split expressed in the API's scoping.
> - **D is wrong** on both halves; it inverts the relationship entirely.

---

### QP8: "A cluster administrator creates a StorageClass whose `provisioner` field references a CSI driver that has not been installed…"

**Issue:** Two of three distractors receive a label-level rebuttal instead of a behaviour-level one. **FAIL** against rule 3.

**Distractor analysis:**
- A) correct — absent-component pattern, claim remains unbound
- B) `eventual-consistency pattern; the claim binds after a reconciliation delay` — **genuinely strong.** Kubernetes *is* eventually consistent and the reader has spent ten chapters watching control loops converge; "it'll bind eventually" is a well-motivated wrong answer
- C) `admission-rejection pattern; the StorageClass is rejected at creation` — plausible; the key handles it properly
- D) `default-fallback pattern; the claim falls back to the default StorageClass` — plausible; a reader who has just learned about default classes may expect graceful degradation

**Why-wrong explanation status:**
- **Present but incomplete.** Verbatim: *"B, C, and D are all invented patterns. C in particular is worth rejecting explicitly: the API server validates schema, not the existence of running components."* Only C gets a behaviour-level rebuttal. For B and D, "invented pattern" rejects the *label* while leaving the *described behaviour* uncorrected — and the behaviour is what the reader actually believed.

**Recommended fix:** Rebut the behaviours:

> - **B is wrong** because there is no retry that ends in a bind. *Claims will remain unbound indefinitely if a matching volume does not exist* — the binder is a control loop, and a loop reconciling toward a volume that nothing will ever create converges on waiting. This is not a delay; it is the terminal state.
> - **D is wrong** because a claim that names a class does not fall back. The default applies only to a claim with **no** `storageClassName` field; naming a class is a commitment to that class.

---

### QB2.3: "A StorageClass sets `volumeBindingMode: WaitForFirstConsumer`… the Pod requests 64Gi of memory and no node has that much allocatable."

**Issue:** Two of three distractors are non-tempting, reducing the chapter's best storage/scheduling integration item toward a two-option question.

**Distractor analysis:**
- A) `PVC Bound, Pod Pending` — **strong.** This is `Immediate` mode's behaviour, precisely what `WaitForFirstConsumer` exists to prevent. Any reader who half-learned the mode picks this
- B) correct
- C) `PVC Bound, Pod Running on a node that exceeds its allocatable capacity` — **weak.** This contradicts Ch 7's filter phase, which is the very material the question retrieval-tests. A reader who knows filtering eliminates it instantly; a reader who doesn't picks A, not C
- D) `PVC Failed, Pod Failed — an unschedulable Pod causes its claim to fail reclamation` — **weak.** The attached justification is self-defeating: reclamation concerns a volume whose claim was deleted, and this Pod never started. The clause signals "throwaway" to any careful reader

**Why-wrong explanation status:**
- **Present and specific** for all three. The key is not the problem here; the options are.

**Recommended fix:** Replace C and D with wrong answers a reader could reach by reasoning:

> C) PVC `Bound`, Pod `Pending` — the volume provisions in the zone with the most free capacity, and the Pod waits for a node there
> D) PVC `Bound`, Pod `Pending` — `WaitForFirstConsumer` delays only *binding*, not provisioning; the volume is created immediately and binds when the Pod is created

Both are wrong for reasons the section teaches, and both require the reader to hold what the mode actually delays. C and D as written are eliminable without either.

---

### QB1.2: "Where was `/tmp/scratch.log` written, and is it still there?" — option D

**Issue:** Weak distractor.

**Distractor analysis:**
- A) `image's read-only layers; still there` — plausible; conflates image layers with the container filesystem
- B) `writable layer; still there` — **the target misconception**, correct on location and wrong on lifetime. Exactly what the ladder exists to correct
- C) correct
- D) `To a Pod-scoped volume created implicitly by the kubelet; still there` — **weak.** No such mechanism exists, nothing in Chapters 1–10 suggests one, and a reader holding this belief has not been observed. It is symmetry filler

**Why-wrong explanation status:**
- **Present and specific** for all three ("the kubelet does not create implicit volumes. A volume exists because a PodSpec declared it").

**Recommended fix:** Swap D for a lifetime-boundary confusion that a reader could actually hold:

> D) To the container's writable layer; gone, because the *Pod* was replaced

Wrong on the event (the Pod was not replaced; the container restarted), which is the discrimination §1 spends its whole ladder building. That makes D a near-miss on the boundary rather than an invented mechanism.

---

### QB3.2: "A StorageClass names `ebs.csi.aws.com`; the driver has never been deployed…" — option B

**Issue:** Weak distractor.

**Distractor analysis:**
- A) `API server rejects the StorageClass at creation` — plausible; over-estimating admission validation is a real and common belief
- B) `The PVC binds to a placeholder PV and the Pod starts with an empty volume` — **weak.** There is no placeholder-PV mechanism anywhere in Kubernetes and no analogue in the reader's experience. Nothing in the chapter or its predecessors makes graceful-degradation-to-empty-volume imaginable
- C) correct
- D) `Kubernetes automatically installs the named CSI driver on first use` — acceptable. Managed clusters (GKE, EKS) genuinely do pre-install drivers, so "the cluster handles it" is a real field intuition

**Why-wrong explanation status:**
- **Present and specific** for all three.

**Recommended fix:** Replace B with a partial-success outcome that a reader could construct:

> B) The PVC binds to an existing `Available` PV of a different class, since the requested class cannot be satisfied

This targets the "binding is best-effort matching" misconception, which is trap 63's cousin and demonstrably real, rather than a fabricated fallback.

---

### QP6: "Which of the following is required for dynamic provisioning to occur when a PVC is created?" — option D

**Issue:** Weak distractor — off-axis.

**Distractor analysis:**
- A) correct — the two conditions
- B) `A matching PersistentVolume must already exist in the Available phase` — **strong.** This is static provisioning, and dynamic provisioning is specifically what happens when no such PV exists. Excellent inversion
- C) `The PVC must specify volumeName naming the PV to be created` — acceptable. `volumeName` is a real field and misusing it as a creation directive is believable for a reader who has seen it
- D) `The cluster must have Recycle enabled as the default reclaim policy` — **weak.** Reclaim policy governs what happens *after* a claim is deleted and has no bearing on whether provisioning occurs. The two concepts share no axis, so no coherent misconception produces this answer. The key concedes as much: *"unrelated and names a deprecated policy"*

**Why-wrong explanation status:**
- **Present and specific** for all three.

**Recommended fix:** Replace D with an on-axis wrong condition:

> D) The cluster must have exactly one StorageClass marked default, so the provisioner is unambiguous

This targets a real belief — that dynamic provisioning depends on a default existing — which the chapter refutes twice (an explicitly named class provisions without a default; a cluster with no default leaves the field unset rather than failing).

---

### QP10: "A StatefulSet named `db` has two replicas and one `volumeClaimTemplate` named `data`…" — option D

**Issue:** Weak distractor.

**Distractor analysis:**
- A) `One claim, data-db, shared by both Pods; deleted with the StatefulSet` — plausible; this is what a Deployment referencing a single PVC would produce, and Deployment-shaped thinking is the chapter's running discrimination target
- B) `Two claims, data-db-0 and data-db-1; both deleted with the StatefulSet` — **the target trap.** Naming right, survival wrong, which as the key correctly observes is "the more expensive half"
- C) correct
- D) `No claims until a Pod writes data, at which point one is created per write` — **weak.** Lazy-on-write PVC creation exists nowhere, and "one per write" is internally absurd. The key's rebuttal is simply "D is fabricated," which is the complete and correct explanation for an invented mechanism — the defect is the option, not the key

**Why-wrong explanation status:**
- **Present and specific** for A and B; adequate for D given the option's nature.

**Recommended fix:** Replace D with the generic-ephemeral confusion the chapter deliberately set up in §6's 🪝 Snag:

> D) Two claims, `data-db-0` and `data-db-1`; both are garbage-collected when their Pods are deleted

Two mechanisms in this chapter create one claim per Pod with **opposite** deletion behaviour. §6 explicitly contrasts them. This option makes that contrast load-bearing instead of leaving it as prose.

---

### QP13: "A PVC is created with `storageClassName: \"\"` on a cluster that has a default StorageClass and no classless PersistentVolumes."

**Issue:** Near-verbatim duplicate of B2.5 — same fact, same cluster setup, functionally identical option set. Spends 1 of 17 Practice slots on zero added discrimination.

Side by side:

| | B2.5 | P13 |
|---|---|---|
| Setup | default class + working CSI provisioner, no classless PVs | default class, no classless PVs |
| A | default used, "empty means unspecified" | uses the default StorageClass |
| B | rejected as invalid | rejected as an invalid manifest |
| C | **correct** — opts out, stays unbound | **correct** — opts out, stays unbound |
| D | binds to any Available PV, "empty matches all" | binds to any Available PV, "empty class matches all" |

Skill Part 7 draws exactly this line: *same concept, different representations* is good redundancy; *same information, same channel* is not. Spacing a checkpoint fact into the Practice set is right — reproducing the question is not. Part 10B's desirable difficulty is **variation**, same concept in a different context.

**Recommended fix — one edit closing three problems at once.** Recast P13 as a §2 item testing **binding filters beyond capacity**, which is taught in §2's 🪝 Snag and is currently **untested anywhere in the chapter**:

> A cluster has one PersistentVolume: 100Gi, `Available`, `storageClassName: fast`, labelled `tier=production`. A user creates a 10Gi PVC in the same cluster requesting `storageClassName: fast` with a selector `matchLabels: {tier: staging}`. What happens?
>
> A) It binds — the PV satisfies both the capacity request and the class request
> B) It binds — label selectors filter Pods onto nodes, not claims onto volumes
> C) It remains unbound — a selector on a claim is an additional requirement, and all requirements are ANDed
> D) It binds, and the PV's `tier` label is updated to `staging` to reflect the new claimant

Correct: C. This preserves §2's highest-yield surface, closes a real coverage gap, and moves one item from the over-allocated §1/§3 group into the under-allocated §2 group (see below). Empty-string opt-out remains tested once, at B2.5, which is adequate for a trap already reinforced in the Exam Alert and Chapter Summary.

---

### Architecture note: Practice Question distribution vs. outline §7

Not a per-question defect, but the highest-leverage structural finding after B3.5.

| Section | Outline target | Actual | Delta |
|---|---|---|---|
| §1 volume types and lifetimes | 3 | 5 (P1, P5, P9, P14, P17) | **+2** |
| §2 PV / PVC / binding | **4** | **2** (P2, P4) | **−2** |
| §3 provisioning | 3 | 3 (P6, P13, +P8 partial) | 0 |
| §4 access modes and reclaim | 4 | 4 (P3, P7, P11, P15) | 0 |
| §5 CSI | 1 | 2 (P8, P12) | +1 |
| §6 StatefulSet pairing | 2 | 2 (P10, P16) | 0 |

The outline gave §2 the **highest single allocation** on explicit grounds: B1's domain analysis records that D2 expects the candidate to *"distinguish PV from PVC from StorageClass"* — the one three-way distinction named in the published expectation. In the shipped draft, §2 received the joint-smallest allocation.

Total §2 exposure is not thin overall — Bearings #1 devotes all five of its questions to §1/§2. But the end-of-chapter Practice set is the interleaved, exam-simulating surface, and it is where §2 is under-weighted. Recasting P13 per the fix above brings §2 to 3 of 17; converting one §1 item would bring it to target, though every §1 item currently earns its slot (P5 pays the `chapter-04:762` `subPath` debt, P9 plants Ch 12 §5, P17 carries the generic-ephemeral/StatefulSet discrimination). Recommendation: take the P13 recast, accept §2 at 3, and record the −1 as a deliberate deviation rather than converting a debt-paying §1 item.

**Interleaving itself is exemplary** and should not be disturbed. Section sequence across P1–P17 runs §1, §2, §3/4, §2, §1, §3, §4, §3/5, §1, §6, §4, §5, §3, §1, §4, §6, §1 — no two adjacent items share a section, and the outline's three named pairings are all present: an access-mode item beside a reclaim item (P7→P8→P9→…P11 adjacent to P12), a `subPath` item near the ConfigMap-update rule (P5), and items requiring §2 and §3 together (P6, P8).

---

### Borderline options — reviewed, no action required

Listed for completeness so a later stage does not re-flag them. Each was assessed against the bar *"could an identifiable reader select this?"* and cleared:

| Question | Option | Why it clears |
|---|---|---|
| B1.1 | D — gone after crash, present after delete | Exhaustive 2×2 fourth cell, and both halves map to real beliefs: "restart means fresh everything" plus "the Deployment restores the volume with the Pod" |
| B1.3 | D — Pod names both PV and PVC "so the binding can be verified" | Belt-and-braces reasoning is a real hedge for an unsure reader; the key's correction ("it has no field for a PV") is useful |
| B2.1 | D — RWO invalid for multi-Pod configs, PVC fails to bind | Over-reading "Once" as an API constraint is believable |
| B2.3 | D — PVC/Pod both `Failed` | Guessing `Failed` over `Pending` is real; only the appended justification is weak |
| B3.3 | D — StatefulSet in another namespace, PVCs cluster-scoped | Appears to contradict the stem, but a reader holding the PVC-is-cluster-scoped belief reads "same namespace" as irrelevant, so it does not self-eliminate for the target reader |
| P1 | C — `/etc/creds` empty until remounted manually | Treating mounted Secret content as Pod-local state is a real slip |
| P2 | D — write a CSIDriver object | Plausible object name for a reader who has just met CSI |
| P5 | D — ConfigMap `subPath` mounts error on update | Mounts genuinely can break; there is an analogue, unlike the fabricated-mechanism cases above |
| P8 | A's familiarity tell | A is the only option quoting a phrase the book has drilled four times. Mild, and arguably the intended recognition payoff Ch 10 set up |
| P11 | C — permitted if the mounts are in different namespaces | Namespace-as-isolation-boundary is a real mental model |
| P12 | D — all four shipped in one release, versioned together | Assuming the C\*I family arrived together is believable |

**Two questions deserve positive note** and should be preserved intact through any revision pass:

**B2.2** is the best-designed question in the chapter. Option A ("decided by the PVC, which defaults to `Retain`") is plausible *because §2 itself quotes a glossary source stating that a claim specifies "how it is reclaimed"* — the chapter builds its own trap from its own cited material. Option B applies a **true** fact (manual PVs default to `Retain`) to the wrong provisioning path. Option D reaches the **right outcome by the wrong reasoning**, and the key names this explicitly: *"Getting the outcome right for the wrong reason is still getting it wrong, and the exam will offer you that option."* Options C and D sharing an outcome while differing on mechanism is deliberate and correct — do not "fix" it as a duplicate.

**P15** option C (patch the PV's `claimRef` to null) is a technique practitioners genuinely use, defeated not by being false but by the stem's requirement that the old data be removed. Real-world plausibility defeated by careful reading of the stem is the desirable-difficulty target, done right.

---

## Retrieval-practice spacing

- Chapter 11 target: **20%** (outline / B3), within skill Part 10's 20–25% band for Ch 6+ and audit rule 4's 10–25%
- Actual, Taking Your Bearings: **20.0%** — 3 of 15
- Actual, Practice Questions: **17.6%** — 3 of 17 (outline called for "20% ≈ 3–4 items"; 3 delivered, at the low end of its own range)
- Actual, combined: **18.8%** — 6 of 32
- Status: **compliant**

| Item | Tag | Chapters back | ≥4-back floor | Anchor |
|---|---|---|---|---|
| B1.2 | `[retrieval: ch2]` | 9 | ✓ | Writable container layer |
| B2.3 | `[retrieval: ch7]` | 4 | ✓ | Feasible nodes / filter phase |
| B3.3 | `[retrieval: ch6]` | 5 | ✓ | StatefulSet identity |
| P4 | `[retrieval: ch4]` | 7 | ✓ | Namespaced vs cluster-scoped |
| P8 | `[retrieval: ch10]` | 1 | — | Absent-component pattern |
| P12 | `[retrieval: ch2]` | 9 | ✓ | The pluggable-interface set |

The single one-back item (P8) is **sanctioned by the outline**, which names "the absent-component pattern applied to a missing provisioner (Ch 10 §3 / Ch 3 §4)" as a Practice retrieval candidate and states the ≥4-back floor is "already satisfied twice in the Bearings." It is satisfied three times. No violation.

One counting ambiguity worth recording: **B3.5 is substantially cross-chapter** (it tests the Ch 2 / Ch 6 / Ch 9 interface count) but carries no retrieval tag. Leaving it untagged is correct — §5 teaches the set-closing as chapter material, and tagging it would put Bearings retrieval at 26.7%, over Part 10's ceiling. Recorded so a later stage does not read the untagged cross-chapter content as an omission.

**Recommended addition — one item, closing a retrieval gap and a coverage gap together.** Add a fourth Practice retrieval anchored on **Ch 5 §6, the projected ServiceAccount token volume** (six back, floor satisfied). This lifts Practice retrieval to 23.5% (4/17) and combined to 21.2% (7/32) — mid-band rather than at the floor — and simultaneously closes the highest-priority coverage gap below. Sketch:

> In Chapter 5, a Pod's ServiceAccount token appeared inside the container's filesystem without any `configMap` or `secret` volume being declared. Which volume type delivered it, and what else can that type carry?
>
> A) A `secret` volume; it can carry only Secret data
> B) A `projected` volume; it can map `secret`, `configMap`, `downwardAPI`, and `serviceAccountToken` sources into one directory
> C) A `hostPath` volume mounting the node's kubelet credentials directory
> D) A `generic ephemeral` volume provisioned by the ServiceAccount controller

Correct: B. Distractor C is worth keeping — it is wrong, but the reason it is wrong (a Pod reading `/var/lib/kubelet` is the §1 hazard, not the token mechanism) reinforces the chapter's own security plant. The outline's "drawn from Ch 6–10" phrasing is non-strict — it also lists a Ch 4 candidate, and P4 already ships as Ch 4 retrieval.

---

## Coverage vs concepts

Every `kb_tags` concept and command from the outline frontmatter, plus taught-but-untagged material found in the draft.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| volume | yes (B1.1, P1) |
| volume-lifetime-ladder | yes (B1.1, B1.2, P1) |
| ephemeral-volume | yes (B1.1, P17) |
| persistent-volume-lifetime | yes (B1.1, P1) |
| emptydir | yes (B1.1, P1, P14) |
| emptydir-medium-memory | yes (P14) |
| emptydir-size-limit | **NO** |
| hostpath | yes (P9) |
| hostpath-type-field | **NO** |
| hostpath-security-risk | yes (P9) |
| configmap-volume | yes, indirectly (P5, via the `subPath` exception) |
| secret-volume | yes (P1) |
| secret-volume-tmpfs | **NO** |
| projected-volume | **NO** |
| downwardapi-volume | **NO** |
| generic-ephemeral-volume | yes (P17) |
| subpath | yes (P5) |
| subpath-no-updates | yes (P5) |
| nfs-volume | yes (P7, stem) |
| local-volume | yes (P9, correct answer and option D) |
| persistentvolume | yes (B1.3, B1.4, P2, P4) |
| persistentvolumeclaim | yes (B1.3, P2, P4) |
| supply-and-demand-split | yes (B1.3, P2, P4) |
| pods-consume-node-resources | no — framing analogy, not a testable fact (acceptable) |
| pvcs-consume-pv-resources | no — framing analogy (acceptable) |
| pv-lifecycle-independence | yes (B3.4, P16) |
| binding | yes (B1.4) |
| exclusive-one-to-one-binding | yes (B1.4) |
| unbound-claim | yes (B1.4, B3.2, P8, P13) |
| pv-phase | yes (B1.5) |
| released-not-available | yes (B1.5, B2.4, P15) |
| storageclass | yes (B2.2, P2, P3) |
| static-provisioning | **weak** — appears only as P6 option B; never tested as a named path |
| dynamic-provisioning | yes (P6) |
| provisioner | yes (B3.2, P8) |
| storageclass-parameters | **NO** |
| default-storageclass | yes (B2.2, P3, P13) |
| empty-storage-class-opt-out | yes (B2.5, P13 — the duplication) |
| volume-binding-mode | yes (B2.3) |
| wait-for-first-consumer | yes (B2.3) |
| access-mode | yes (B2.1, P7, P11) |
| readwriteonce | yes (B2.1, P7, P11) |
| readonlymany | yes (P7, P11) |
| readwritemany | yes (P7) |
| readwriteoncepod | yes (B2.1 key, P7 option D) |
| node-count-semantics | yes (B2.1) |
| reclaim-policy | yes (B2.2, B2.4, P3, P15) |
| retain | yes (B1.5, B2.4, P15) |
| delete | yes (B2.2, P3) |
| recycle-deprecated | yes, distractor-only (B2.4 C, P3 D, P15 D) — appropriate; recognising it as retired is the exam skill |
| inherited-reclaim-policy | yes (B2.2, P3) |
| csi | yes (B3.1, P12) |
| csi-driver | yes (B3.2, P8) — but see gap below on driver *architecture* |
| in-tree-volume-plugin | **NO** |
| csi-migration | **NO** — 🔭 Closer Look depth, explicitly above KCNA; acceptable |
| fourth-pluggable-interface | yes (P12); B3.5 defective |
| volumeclaimtemplates | yes (B3.3, P10) |
| per-replica-pvc | yes (B3.3, B3.4, P10, P16) |
| pvc-survives-deletion | yes (B3.3, P10) |
| absent-component-pattern | yes (B3.2, P8) |
| `kubectl get pv` | **NO** |
| `kubectl get pvc` | yes, as B3.3 stem framing only — not tested as a command |
| `kubectl get storageclass` | **NO** — named as a called-for action in §4's Fixed Point |
| `kubectl describe pvc` | **NO** |
| `kubectl api-resources` | yes (S3, open-ended) |
| *untagged:* binding filters beyond capacity (class match, label selector, `volumeName`) | **NO** |
| *untagged:* Storage Object in Use Protection / `pvc-protection` finalizer | **NO** |
| *untagged:* access mode does not enforce write protection | **NO** — appears only as B2.1 distractor C; never affirmed |
| *untagged:* one access mode at a time | yes (P11) |
| *untagged:* retroactive default-class assignment to waiting PVCs | **NO** |
| *untagged:* `persistentVolumeClaimRetentionPolicy` (`whenDeleted` / `whenScaled`) | **NO** — 🔭 Closer Look depth; acceptable |
| *untagged:* CSI driver deployment shape (Deployment + DaemonSet) | **NO** |
| *untagged:* generic-ephemeral PVC naming and collision | **NO** — 🔭 Closer Look depth; acceptable |
| *untagged:* node failure ≠ scale-down; PVC retained | yes (B3.4) |

### Priority coverage gaps

Ranked by consequence, with the Closer Look material excluded as legitimately above-exam depth.

1. **`projected-volume` — untested.** The highest-priority gap. §1 pays a published cross-bearing from `chapter-05` line 775, teaching that the token volume the reader already met is the same mechanism generalised. The reader is never asked to confirm the encoding. The recommended Ch 5 retrieval item above closes this and lifts Practice retrieval to mid-band in one edit.
2. **`secret-volume-tmpfs` — untested.** §1 teaches that Secret volumes are tmpfs-backed and never written to non-volatile storage, then the Voyage Ahead tells the reader outright: *"you already hold half of it"* for Ch 12 §4's file-mounts-over-environment-variables argument. The chapter asserts the reader holds it without ever checking.
3. **Binding filters beyond capacity — untested.** §2's 🪝 Snag teaches that class match, label selector (ANDed across `matchLabels` and `matchExpressions`), and `volumeName` are all binding filters, and that *"capacity is one filter among several."* B1.4 tests exclusivity but never the filters. The P13 recast above closes this.
4. **CSI driver architecture — untested.** `chapter-02` line 600 promised *"CSI and storage drivers"* — the word *drivers* was in the promise. §5 pays it in prose (controller Deployment plus per-node DaemonSet, and the recognition that a CSI driver is ordinary Kubernetes workloads) and no question verifies it. B3.1 tests what CSI *is*; nothing tests what a driver *is*.
5. **`hostpath-type-field`, `emptydir-size-limit`, `storageclass-parameters` — untested.** Each is taught with specifics (the `type` field's existence checks; `sizeLimit` against an unbounded default; `parameters` as an opaque provisioner passthrough shown in YAML). All three are low-frequency on a recall exam; recording them so a retro can judge rather than rediscover.
6. **`static-provisioning` as a named path — weak.** Tested only as P6's option B. The static/dynamic distinction is a §3 Fixed-Point neighbour and `ch11-fig03` is built entirely around it; no question asks the reader to identify which path a scenario is on.
7. **Command coverage — thin.** Three of five tagged commands are untested. Mitigating: KCNA is multiple-choice recall, not performance-based, and the outline lists commands as artifacts rather than as skills. Not worth a slot on its own, but `kubectl get storageclass` could ride along inside the recast §2 item's stem at zero cost, since §4's Fixed Point explicitly instructs the reader to run it.

---

## Verdict

Two FAILs (P4, P8), both narrow and both fixable by rewriting an answer-key line — neither requires touching a question. Six weak distractors, five of them single-option swaps. One question (B3.5) needs a rebuild because its correct answer is readable from option shape alone. One duplicate (P13) that, recast, closes the §2 practice shortfall and a coverage gap at the same time. One recommended addition (Ch 5 projected-volume retrieval) that closes the top coverage gap and moves retrieval off the band floor.

Budget compliance is exact on all four categories. Trap fidelity is clean across the board — all nine named traps present, all mapped to sourced misconceptions, none fabricated for symmetry. The Soundings pass the spoiler check with no stem disclosing a Fixed Point, and the two nearest approaches (S5, S6) clear on evidence rather than on charity: S6 restates only what shipped `chapter-10` already told the reader, which is arrived knowledge by definition.