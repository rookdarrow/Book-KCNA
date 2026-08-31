Verified against `draft-v1.md` on disk. Emitting the stage artifact to stdout (per the executor convention that removes `Write` so the orchestrator captures stage output atomically).

```markdown
# Question-Quality Audit — Chapter 16

## Summary

- Chapter type: content
- Total questions inspected: 39
  - 🧭 Soundings questions: 8
  - ☆ Taking Your Bearings questions: 16 (across 3 checkpoints)
  - Practice questions: 15
- Question budget compliance: **met** (8 / 16 / 15 exactly, total 39 = `total_this_chapter`)
- Weak distractors (WARN): **5**
- Trap answers that don't target real misconceptions (WARN): **2** (both also counted above)
- Missing or incomplete why-wrong explanations (FAIL): **0** — all 31 multiple-choice questions explain all three wrong options
- Retrieval-practice spacing: **compliant** — 4 of 16 checkpoint questions = 25.0%, exactly the arc-outline ceiling
- Soundings spoiler check: **clean** (0 of 8 reveal a ★ Fixed Point; the one watched edge held)

**Two findings outside the template's summary rows, both material:**

- **Checkpoint revision prompts absent at all three checkpoints (FAIL).** No 0–2 scoring guidance anywhere in the chapter's checkpoints. Detail in "Checkpoint self-correction structure" below.
- **Three near-duplicate question pairs (WARN).** Practice Q12, Q13 and Q14 restate Taking Your Bearings 2.5, 2.3 and 3.1 with cosmetic rewording — 3 of 15 Practice slots, 20% of that budget, spent re-asking questions the reader answered earlier in the same chapter.

---

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 16 | 16 | met |
| Taking Your Bearings (checkpoints) | ≥2 (outline plans 3: 6+5+5) | 3 (6+5+5) | met |
| Practice Questions | 15 | 15 | met |
| **Chapter total** | **39** | **39** | **met** |

Per-checkpoint distribution matches the outline exactly: TYB 1 = 6 (L418–516), TYB 2 = 5 (L657–740), TYB 3 = 5 (L842–924). Every checkpoint clears the skill's ≥5-question floor.

Note on format: Soundings (L47–61) are short-answer, not multiple choice. That is within the skill's Part 11 structure, which shows plain numbered stems with rationale-carrying answers. Distractor analysis therefore does not apply to them, and the spoiler table below is the only Soundings analysis in this audit.

---

## Soundings spoiler check

The chapter marks four ★ Fixed Points: L308 (a container cannot be added to a running Pod), L352 (`--copy-to` makes a copy; the original is untouched), L532 (a Service with no endpoints is correct and selecting nothing — two causes, two files), L641 (a working `port-forward` beside a failing Service localizes rather than clears).

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 (L47) | Scope test — Running/Ready/confined, still wrong (Ch 13 §1) | no | Stem and answer stay entirely inside the Ch 13 prior. No chapter Fixed Point named. |
| 2 (L49) | Init sequence halts on non-zero exit (Ch 5 §3) | no | Ch 5 model only. |
| 3 (L51) | Running, 0/1 Ready → endpoint membership (Ch 5 §7, Ch 9 §4) | **no — watched edge held** | This is the risk the outline flagged. FP L532 is the *pairing* of two causes. Q3's answer (L70) says only "Readiness gates endpoint membership: a Pod that is not ready is not a valid target." It does not mention selector mismatch, does not enumerate two causes, and does not ask the reader to choose between them. The outline's constraint — "drafting must not let Q3's answer text enumerate both" — is honored verbatim. |
| 4 | `port` vs `targetPort` (Ch 9 §3) | no | Shipped Ch 9 field definition; not a Fixed Point here. |
| 5 | Service DNS name shape (Ch 9 §7) | no | Shape only, no failure mode. |
| 6 | StatefulSet stable identity (Ch 6 §6) | no | Ch 6 prior. §6's material is a ⚠ Navigational Hazard, not a ★. |
| 7 | PVC survives replica deletion (Ch 11 §6) | no | Decay probe as designed. §6's surviving-PVC content is a Hazard (L780), not a ★ Fixed Point, so the rule does not bite. |
| 8 | Minimal image, no `/bin/sh`, `exec -- sh` (Ch 2 §2) | no | Generation-effect setup working exactly as specified. Establishes the *problem*; the answer (L80) stops at "an image contains exactly what was put into it." No mention of ephemeral containers, `kubectl debug`, or adding a container — so FP L308 is intact. |

**Rubric check:** present and complete. All three branches at L82/L84/L86, and the 0–2 branch names a specific section (`Chapter 13 §1`) rather than a chapter. **Pass.**

**Answer-disclosure check:** `<details>` / `<summary>Answers + reading strategy</summary>` at L63–64. **Pass.**

One design note, not a defect: Soundings Q7's answer (L78) states the `Retain` default that TYB 3 Q2 later tests as a `[retrieval: ch11]` item. Skill Part 11 rule 1 explicitly designs Soundings and Bearings to pre/post-test the same material, so this is the intended pattern, not leakage.

---

## Checkpoint self-correction structure

**FAIL — no revision prompt at any checkpoint.**

All three checkpoints close with a `**Checkpoint: You've Now Mastered**` progress marker (L506, L731, L915) and a forward pointer. None carries scoring guidance for a reader who did badly. The only 0–2 branch in the entire chapter is the Soundings rubric at L86.

This is required by two independent authorities:

- **Skill Part 11, "Revision Prompts":** checkpoints that reveal gaps must provide clear guidance, with a specific section reference for low scorers. The Part 15 chapter template carries `[If scored 0-2: revision prompt with specific section reference]` inside the checkpoint block.
- **This chapter's own outline, §5:** "Every checkpoint carries trap answers targeting the misconceptions tabulated in the Exam Alert, why-wrong explanations for **all** options, and a revision prompt naming a **section** for 0–2 scorers." The first two are delivered in full. The third is absent.

The gap matters more here than in an average chapter, because this chapter sits at the 25% retrieval ceiling: a reader failing TYB 2 is most likely failing on Ch 9 and Ch 5 material, and the correct remediation points *backward out of this chapter*, which is exactly what a revision prompt would say and nothing else in the draft does.

**Recommended fix — add after each answer key, before the "You've Now Mastered" block:**

- **TYB 1 (insert ~L504):** 0–2 → re-read §2 and §3 before continuing; if question 1 was among the misses, re-read Ch 13 §1 first, because §4 onward assumes the boundary is settled.
- **TYB 2 (insert ~L729):** 0–2 → re-read §4, then Ch 9 §4 ("the list behind the name"). Name Ch 9 §3 specifically if question 2 was missed.
- **TYB 3 (insert ~L913):** 0–2 → re-read §6, then Ch 11 §6 for the retention policy.

---

## Per-question findings

### Q[TYB 3] 4 (L867): "A bug appears only when the application runs in the cluster. The failing code path reads a value that a mutating admission webhook injects into the Pod. Is a local reproduction useful?"

**Issue:** Option D is a giveaway. Its stated justification is transparently false, and the answer key says so outright ("wrong on its facts. Local machines run containers fine"). A distractor whose *reason* no reader believes is not a distractor — it is a fourth slot spent. D also shares the correct verdict ("No") with B, which is a legitimate right-answer/wrong-reason design **only** when the wrong reason is tempting. Here it is not, so the question effectively runs as a three-option item.

**Distractor analysis:**
- A) Yes — copy the injected value into a local environment variable and run it locally — **plausible to a real misconception**, and the strongest option in the set: it feels like rigor, and the answer key's correction ("tests your belief, not the system") is the lesson §7 exists to teach.
- B) Correct.
- C) Yes — mutating webhooks run identically against local processes — **plausible**; targets a genuine gap in the admission mental model for readers who have not internalized that webhooks live in the API-server request path.
- D) No — but only because local machines cannot run containers — **implausible.** No reader holds this belief.

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** replace D with a "No" whose reason is tempting and wrong for an identifiable reason. Suggested: *"No — mutating webhooks apply non-deterministically, so the injected value differs on each admission and cannot be pinned down for a local run."* That targets a real gap (webhook determinism), keeps the verdict split 2-Yes/2-No, and stays inside Ch 8 §2's shipped material.

---

### Q[TYB 1] 3 (L436): "Why do ephemeral containers exist as a separate API mechanism rather than as an ordinary edit to a Pod's spec?"

**Issue:** Option A targets no misconception anyone holds. It appears to exist for symmetry — four options, three wrong.

**Distractor analysis:**
- A) Because ephemeral containers need a different container runtime — **implausible / fabricated for symmetry.** "Different runtime" is not a belief readers arrive with; nothing in Chapters 1–15 would seed it.
- B) Correct.
- C) Because ephemeral containers are scheduled to a different node — **plausible**; targets a real confusion about whether a debug container is external to the Pod, which is precisely the model the Fixed Point at L308 has to displace.
- D) Because RBAC cannot grant `update` on Pods — **plausible**; the "this must be a permissions constraint" reading is a genuine and common misread, and the answer key names it correctly as architectural-not-authorization.

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** replace A with a distractor drawn from the real restriction set the section teaches at L328–338 — e.g. *"Because ephemeral containers must be declared before the Pod is scheduled, so the API needs them separately."* That is tempting to a reader who half-remembers the immutability point and inverts its direction, and it fails for a stateable reason (the whole point is that they are added *after* creation).

---

### Q[TYB 2] 5 (L689): "A client Pod in namespace `frontend` calls `http://api/` and gets no response. The Service `api` exists in namespace `payments`, with a populated endpoint list."

**Issue:** Options A and C occupy the same conceptual slot. Both are empty-endpoint-list causes, and the stem states the list is populated, so a single inference eliminates both at once. The answer key confirms it, grouping them: *"A and C are wrong for the same reason."* The question runs as a three-option item.

**Distractor analysis:**
- A) The Service selector does not match its Pods — **duplicate meaning with C** (both eliminated by "populated endpoint list").
- B) Correct.
- C) The Pods behind `api` are not Ready — **duplicate meaning with A.**
- D) `port` and `targetPort` are mismatched — **plausible and well-chosen**; survives the stem, and is discriminated by signature (refused connection to a real target vs. a name that resolves elsewhere), which is the skill the section teaches.

**Why-wrong explanation status:** present and specific — A and C are grouped but the shared reason is named exactly, and D gets its own signature-based explanation. No FAIL.

**Recommended fix:** replace **A** with an option that survives the populated-list fact and occupies a distinct misconception slot. Suggested: *"Services are not reachable across namespace boundaries without an Ingress."* That targets a genuinely common novice belief (namespaces as network boundaries), is not eliminated by anything in the stem, and its why-wrong writes itself against Ch 9 §7.

---

### Q[Practice] 11 (L1062): "A Service's endpoint list is fully populated with three ready Pods. Requests to the Service time out."

**Issue:** Same architecture as TYB 2 Q5 — options A and B are both upstream empty-list causes, both eliminated by "fully populated," and the answer key groups them. Weaker as a finding than TYB 2 Q5, because here the upstream/downstream split *is* the tested skill and seeing both upstream causes excluded together carries some pedagogical weight. Still, two of four options collapse.

**Distractor analysis:**
- A) A selector/label mismatch — **duplicate meaning with B.**
- B) Readiness holding Pods out of the list — **duplicate meaning with A.**
- C) Correct.
- D) The EndpointSlice controller has stopped reconciling — **plausible**; the platform-blame reflex §1 exists to break, and the why-wrong handles it well ("would leave a stale or empty list, not a correct one").

**Why-wrong explanation status:** present and specific.

**Recommended fix (lower priority than the four above):** keep one of A/B, and replace the other with break point 4 — *"The client is resolving a DNS name that does not point at this Service."* That gives the reader all four of §4's break points in one option set, which is the section's own framing, and only one of them is eliminated by the stem.

---

### Q[TYB 3] 3 (L860): "A StatefulSet's Pods run normally, but the replicas cannot discover each other... All Pods are `Running` and `Ready`."

**Issue:** Option A is eliminated by an explicit clause in the stem and targets no residual misconception. Milder than the cases above — only one option is lost, not two.

**Distractor analysis:**
- A) The readiness probe definitions — **implausible given the stem**, which states every Pod is `Ready`. The answer key's whole explanation is "the stem says every Pod is `Ready`."
- B) Correct.
- C) The `port`/`targetPort` pairing on the workload's ClusterIP Service — **plausible**; targets the real confusion between client-facing routing and peer-to-peer discovery.
- D) The PersistentVolumeClaims for each ordinal — **plausible**; targets "StatefulSet problem, therefore storage," which is a genuine reflex this chapter creates in §6 and should test the reader's ability to resist.

**Recommended fix:** replace A with something the stem does not exclude — e.g. *"DNS negative caching from lookups issued before the peers existed."* That is real, taught in §6 at L796 with a direct source quote, currently untested anywhere, and it makes the question harder in a desirable way: the reader must choose between two correct-sounding DNS explanations and pick the structural one.

---

### Q[Practice] 13 (L1076) — duplicate of TYB 2 Q3 (L675)

**Issue:** Not a distractor problem — a **budget problem**. These are the same question.

| | TYB 2 Q3 (L675) | Practice Q13 (L1076) |
|---|---|---|
| Stem | "You port-forward directly to a Pod behind a failing Service and the application responds correctly. What have you established?" | "You port-forward to a Pod behind a failing Service and the application responds correctly on the forwarded port. What is the correct conclusion?" |
| A | app working, incident resolved | healthy, close the incident |
| B | **correct** — app serves, fault on Service path | **correct** — app serves, fault on Service path |
| C | Service fine, Pod unhealthy | Service fine, Pod probes misconfigured |
| D | Nothing — same path | inconclusive — same path |

Same scenario, same correct answer, same four concepts in the same order. Skill Part 7 classifies this as channel redundancy (same information, same channel), the kind that "bores alert readers and doesn't help struggling readers" — as against content redundancy, which requires a changed representation or context.

**Recommended fix:** keep TYB 2 Q3, re-aim Practice Q13 at §5 material that is currently untested. Two candidates, both taught in the section:
1. **The negative case** (L653): a port-forward that *also* fails exonerates the Service path and sends the investigation back inside the container to §3. Currently tested nowhere, and it is half of the section's inference.
2. **The port-number trap** in the ⚓ callout (L649): forwarding to 8080 when the Service's `targetPort` says 80 accidentally routes around break 3, and a successful forward on the right port beside a Service pointing at the wrong one *is* the `port`/`targetPort` signature. This is the subtlest thing §5 teaches and it is entirely untested.

Option 2 is the stronger choice — it interleaves §4 and §5, which is what an end-of-chapter Practice item should do that a mid-chapter checkpoint cannot.

---

### Q[Practice] 12 (L1069) — near-duplicate of TYB 2 Q5 (L689)

**Issue:** Same fact, same scenario shape, three of four options shared.

| | TYB 2 Q5 | Practice Q12 |
|---|---|---|
| Setup | client in `frontend` → `api` in `payments`, populated list | client in `web` → `cache` in `data`, populated list |
| Correct | short name resolves in client's namespace | short name resolves in client's namespace |
| Shared distractors | not Ready; `port`/`targetPort` | not Ready; `port`/`targetPort` |
| Differing distractor | selector mismatch | "Redis requires a headless Service" |

Practice Q12 is the better-built of the two — only one option is eliminated by the stem, and its D is a genuinely good domain distractor. But it is the third §4 item in a section allocated three, and it spends that slot on a fact already checkpointed.

**Recommended fix:** if TYB 2 Q5's option A is repaired as recommended above, the two questions diverge enough to keep both. If not, re-aim Q12 at §4 material that is untested — the `kubectl get endpointslices -l kubernetes.io/service-name=<name>` lookup form (L556), or `kubectl describe service` (see coverage gaps below). Prefer the latter: Exam Alert high-priority topic 1 (L965) names `describe service` explicitly and no question touches it.

---

### Q[Practice] 14 (L1083) — near-duplicate of TYB 3 Q1 (L846)

**Issue:** Softest of the three. Same scenario (one StatefulSet ordinal fails, is deleted, returns, fails identically; siblings healthy), same correct answer (the surviving PVC), and three of four distractor concepts shared (node fault, image, shared template). The concrete workload differs (`db-1` vs `queue-0`) and Practice Q14's option A ("the Pod template") is a genuinely new and good distractor that TYB 3 Q1 lacks.

**Recommended fix:** acceptable to keep if Q12 and Q13 are re-aimed — one repeated shape across a 39-question chapter is within the skill's variation allowance (Part 10B: "same concept, different contexts"). If a further slot is needed, re-aim at §6's untested material: the `Unknown`/`Terminating` replica blocking StatefulSet rollout progress (L762), which is sourced, exam-shaped, and currently absent from every question set.

---

### Borderline, no edit requested

- **TYB 1 Q2 option D** (L434, `kubectl port-forward` against an init-stuck Pod): weakest option in its set, but defensible — "the app isn't responding, let me try to reach it" is a real novice move, and the question is testing high-priority topic 1 (verb-to-question mapping), which is better served by an option set drawn from all four verbs.
- **TYB 3 Q1 option D** (admission webhook rejecting one ordinal): the stem says the Pod *is* recreated and then fails, which excludes an admission refusal for a careful reader. Retained because it targets a real confusion between "refused" and "failed," and the why-wrong teaches that distinction explicitly.
- **TYB 1 Q1 ↔ Practice Q1** and **TYB 1 Q5 ↔ Practice Q4**: same underlying mechanism, but the asked-for output differs (diagnosis vs. next action; `mkdir` vs. `git clone` with a distinct option set). This is the desirable-variation pattern, not duplication.
- **TYB 2 Q1 ↔ Practice Q10**: the two empty-list causes tested from opposite directions, with different discriminating evidence in each stem. Deliberate and sound. The option pool is nearly identical between them, which is worth watching but not fixing — the reader still has to read the evidence to choose.

---

## Trap fidelity

All labeled traps were checked against the Exam Alert table (L971–984) and against the section prose. Every trap in the table is tested by at least one question, and every tested trap is a real misconception with a named mechanism in the draft:

| Trap (Exam Alert) | Tested at | Fidelity |
|---|---|---|
| `exec -- sh` works on any container | S8, TYB 1 Q6, P Q6 | real — sourced to the distroless quote at L296 |
| `kubectl debug` repairs the Pod | TYB 1 Q4, P Q7 | real |
| `--copy-to` = "debug the running Pod" | TYB 1 Q4 (option B) | real, and the best-built distractor in the chapter — it is the *other* debug shape, not an invention |
| working `port-forward` = app is fine | TYB 2 Q3, P Q13 | real |
| `port` vs `targetPort` | TYB 2 Q2, P Q11 | real |
| empty EndpointSlice = broken Service | TYB 2 Q1, P Q10, P Q11 (option D) | real |
| plain `kubectl logs` on an init-stuck Pod | TYB 1 Q2 | real |
| rescheduled StatefulSet replica returns empty | S7, TYB 3 Q1, TYB 3 Q2, P Q14 | real |
| RBAC ≠ admission for `kubectl debug` | P Q9 | real — discharges the Ch 12:1342 debt, and Q9's option A is well-built because it survives the stem's "you hold RBAC permission" clause by claiming the subresource needs *separate* grant |
| D3 Debugging vs D2 Troubleshooting | (not directly testable) | n/a — this is a meta-trap about exam tagging, correctly left to the Exam Alert prose |

**Fabricated-for-symmetry count: 2** — TYB 1 Q3 option A and TYB 3 Q4 option D, both detailed above. Everything else earns its slot.

---

## Retrieval-practice spacing

- Chapter 16 target: **25%** of checkpoint questions from earlier chapters (skill Part 10 gives 20–25% for Chapter 6+; the arc outline sets 25% as a ceiling and this chapter's outline targets the ceiling exactly)
- Actual: **25.0%** (4 of 16 questions tagged `[retrieval: chN]`)
- Status: **compliant, at ceiling**

| Checkpoint | Retrieval items | Local % |
|---|---|---|
| TYB 1 | Q6 `[retrieval: ch2]` (L457) | 16.7% |
| TYB 2 | Q2 `[retrieval: ch9]` (L668), Q4 `[retrieval: ch5]` (L682) | 40.0% |
| TYB 3 | Q2 `[retrieval: ch11]` (L853) | 20.0% |

TYB 2's local 40% is the deliberate concentration the outline specified ("§4 and §5 are the sections where this chapter's method depends most completely on shipped Ch 9 facts, and this is where the repair gets verified"). The chapter average is the governing figure and it lands exactly on target.

The outline's narrow definition of retrieval — a question whose *answer* lives in an earlier chapter, not one that merely leans on earlier material — is correctly applied. TYB 2 Q1 and Q5 both depend heavily on Ch 9's Service model but are chapter questions, and they are correctly left untagged. Had the draft tagged loosely, this chapter would have scored near 90% retrieval and the number would have meant nothing.

**WARN — Practice-section retrieval items are untagged.** The outline requires: "Retrieval-practice items carry the same 25% ceiling as the Bearings and **count separately from them**; at least three Practice items should draw their *answer* from Ch 5, Ch 9 or Ch 11." No Practice question carries a `[retrieval: chN]` tag, so nothing can be counted mechanically.

Two Practice items qualify substantively already:
- **Q12** (L1069) — the answer is Ch 9 §7's short-name resolution rule
- **Q14** (L1083) — the answer is Ch 11 §6's PVC survival

That is 2 of 15 = 13.3%, under the ceiling, so the fix is tagging rather than rewriting. **Recommended:** tag Q12 `[retrieval: ch9]` and Q14 `[retrieval: ch11]`, and if a third is wanted, re-aim one item at Ch 5 §7's readiness semantics — currently the only one of the three named chapters with no Practice-section representation. (If Q12 is re-aimed per the duplication finding above, retag whichever replacement carries a shipped-chapter answer.)

---

## Coverage vs concepts

Checked against `kb_tags.concepts` and `kb_tags.commands` in the outline frontmatter.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| application-scope-triage | yes (TYB 1.1, P Q1, P Q2) |
| four-triage-questions | **thin** — named in P Q1 option B only; no question requires the *order*, which §1's ⚓ callout (L180) argues is the whole value |
| scope-handoff-boundary | yes (TYB 1.1, P Q2) |
| init-container-debugging | yes (TYB 1.2, P Q3) |
| init-container-ordering-and-idempotency | yes — ordering (P Q5), idempotency (TYB 1.5, P Q4) |
| config-errors-visible-at-init | **NO** |
| distroless-image-debugging | yes (S8, TYB 1.6, P Q6) |
| ephemeral-containers | yes (TYB 1.3, P Q7, P Q9) |
| debug-profiles | **NO** |
| debug-copy-to | yes (TYB 1.4, P Q8) |
| debug-node | **NO** — appears only as a distractor (P Q8 option C) |
| service-selector-mismatch | yes (P Q10 correct; TYB 2.1 distractor) |
| empty-endpointslice-as-symptom | yes (TYB 2.1, P Q10, P Q11) |
| port-versus-targetport | yes (TYB 2.2, P Q11) |
| readiness-gating-endpoints | yes (TYB 2.1, TYB 2.4) |
| service-dns-name-shape | yes (S5, TYB 2.5, P Q12) |
| port-forward-as-diagnostic | yes (TYB 2.3, P Q13) |
| service-path-versus-api-path | **thin** — tested only as a distractor (TYB 2.3 D, P Q13 D); never as the thing a correct answer turns on |
| statefulset-application-debugging | yes (TYB 3.1, TYB 3.3, P Q14) |
| per-replica-pvc-debugging | yes (TYB 3.1, TYB 3.2, P Q14) |
| headless-service-dns-names | yes (TYB 3.3) |
| local-development-loop | **thin** — the proxy pattern (§7, L826–834), which is the section's central recommendation, is tested nowhere; only the *dividing line* is tested |
| in-cluster-only-reproduction | yes (TYB 3.4, TYB 3.5, P Q15) |

| Command introduced in chapter | Tested in a question? |
|---|---|
| kubectl-logs-c-init-container | yes (TYB 1.2) |
| kubectl-exec | yes (TYB 1.6, P Q6) |
| kubectl-debug | yes (TYB 1.3, TYB 1.4, P Q6, P Q7, P Q8, P Q9) |
| kubectl-debug-copy-to | yes (TYB 1.4, P Q8) |
| kubectl-debug-node | **NO** |
| kubectl-port-forward | yes (TYB 2.3, P Q13) |
| kubectl-get-endpointslices | yes (TYB 2.1, P Q10) |
| kubectl-describe-service | **NO** |

### The four gaps, ranked

1. **`kubectl debug node/` (§3, L362–374) — untested, and the Exam Alert promises it.** High-priority topic 3 (L969) states: *"`kubectl debug` has three shapes... Each answers a different question and they are not interchangeable."* Two of the three shapes are tested as correct answers (ephemeral inject: TYB 1.3, P Q9; `--copy-to`: TYB 1.4, P Q8). The third appears only as a wrong option in P Q8. A reader can pass every question in this chapter while believing `node/` is always the wrong answer — which is the precise inverse of what §3 teaches, since the section frames it as legitimately correct *when you have crossed the scope boundary*. **Recommend one Practice item** where `debug node/` is the right call and the point is the scope crossing, not the syntax.

2. **`kubectl describe service` (§4, L566) — untested, and the Exam Alert names it.** High-priority topic 1 (L965) lists it beside `get endpointslices` as the pair that answers "whether anything is even selected." Only one of the pair is tested. Cheap to close, and Practice Q12's slot is already flagged for re-aiming.

3. **Config errors visible at init (§2, L232–236) — untested.** One of the three named ways an init container is wrong; the other two (ordering, idempotency) each get two questions. The section makes a specific pedagogical point here — a config error *caught* at init is the good case, loud and self-describing, while the same error *past* init becomes §3's much harder problem. That contrast connects the chapter's two answers to "is it configured" and nothing tests it. P Q15 tests the §3 half only. **Recommend one item** on the init-visible half, ideally one that forces the reader to place the same class of bug at the right stage.

4. **`--profile` / debug profiles (§3, L386–390) — untested.** Flagged as a gap with a caveat: the draft's own `AUTHOR-REVIEW` at L388 records that two cached snapshots disagree on the profile list and the default, and the outline's Open Question 4 directs the drafting stage to soften rather than assert. Given that, leaving the *list* untested is defensible and probably correct. But the **shape** is safe to test and is not source-conflicted: a profile is a privilege preset, and asking for more privilege than the namespace allows is what triggers the admission refusal P Q9 already tests. **Recommend** a stem that turns on that relationship rather than on profile names. If the fact-accuracy audit resolves the source conflict, revisit.

### Secondary, untagged material introduced and untested

Listed for the revision stage's judgment rather than as findings — none is in `kb_tags`, and all three are presented as optional depth:

- **Termination messages / `/dev/termination-log`** (§2, L250–252) — introduced in body prose plus a 🔭 Closer Look. Optional-depth framing makes leaving it untested reasonable.
- **`Unknown`/`Terminating` replicas blocking StatefulSet progress** (§6, L762) — sourced, exam-shaped, and the best available replacement if P Q14 is re-aimed.
- **The §5 port-number trap** (⚓ callout, L649) — the subtlest inference in the chapter, and the strongest candidate for the re-aimed P Q13 (see that finding).

---

## What is working

Recorded so the revision stage does not "fix" it:

- **Why-wrong completeness is exemplary.** 31 multiple-choice questions, 93 wrong options, 0 unexplained. The three grouped explanations (TYB 2 Q5 A+C, TYB 3 Q5 A+C+D, P Q11 A+B) each name every option's individual reason inside the grouping, so they satisfy the skill's self-correction requirement despite the compression.
- **Several why-wrong explanations teach signature discrimination rather than just negating.** TYB 1 Q5 option A ("a PV reattachment failure... would produce a different signature — the Pod stuck on volume mounting, with events saying so"), P Q14 option A, and P Q12 option C all model the reasoning the chapter exists to instill. This is above the house standard.
- **The half-true option is used well and sparingly.** TYB 2 Q2 option D (`containerPort` is informational, but `targetPort` is not independent of the listening port) and P Q15 option A (copying the *declared* value tests your assumption) are the two best-constructed distractors in the chapter, because in both cases the reader's error survives into practice if uncorrected.
- **P Q6 option D** (`kubectl cp` also requires `tar` in the image) teaches a fact the body prose never states and that a reader would otherwise discover the hard way. Distractor as instruction, done correctly.
- **The Soundings held its one watched edge.** Q3 could easily have enumerated both empty-list causes and spoiled the L532 Fixed Point. It did not.
```

**The audit in brief:** budgets are met exactly (8/16/15 = 39), retrieval spacing lands on 25.0% precisely at the ceiling, the Soundings is spoiler-clean including the edge the outline flagged, and why-wrong coverage is complete across all 93 wrong options — no FAIL on the template's own criteria.

Two findings need drafting attention. **All three checkpoints are missing their 0–2 revision prompts**, which the skill's Part 11 and this chapter's own outline both mandate — that's the one FAIL, and it matters more here than usual because a reader failing TYB 2 needs to be sent back to Ch 9, which nothing currently does. And **three Practice items (Q12, Q13, Q14) are reworded restatements of checkpoint questions** — Q13 is verbatim-equivalent to TYB 2 Q3 — spending 20% of the Practice budget on repetition while `debug node/`, `describe service`, and the config-error-at-init case go untested despite two of the three being named in the Exam Alert's high-priority topics.