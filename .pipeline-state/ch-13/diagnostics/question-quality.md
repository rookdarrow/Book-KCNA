The Write tool isn't permitted for this stage — per the pipeline design, stage output flows through stdout so the orchestrator captures it atomically. Emitting the artifact:

```markdown
# Question-Quality Audit — Chapter 13

*Audited against `draft-v1.md` (135,125 bytes, 1,530 lines). All line citations are `draft-v1.md`.
`draft-voice.md` does not exist at this stage.*

## Summary

- Chapter type: **content**
- Total questions inspected: **39**
  - 🧭 Soundings questions: **8** (L53–67)
  - ☆ Taking Your Bearings questions: **16** (across **3** checkpoints — 6 / 5 / 5)
  - Practice questions: **15** (L1287–1391)
- Question budget compliance: **met** (39 of 39; every category exact)
- Weak distractors (WARN): **9**
- Trap answers that don't target real misconceptions (WARN): **1**
- Missing or incomplete why-wrong explanations (FAIL): **1** — TYB3 Q2 answer key states the wrong
  letter and its bullets are keyed to a different option than its header. One further key
  (Practice Q3) is complete in substance but not in house per-option form (WARN).
- Retrieval-practice spacing: **compliant** — 4 of 16 = **25.0%**, exactly the arc-outline ceiling.
  WARN on tag fidelity: 2 of the 4 tagged items are hybrids whose answers are partly chapter
  material, not earlier-chapter material.
- Soundings spoiler check: **clean** — no Soundings question stem or answer states any of the
  chapter's five ★ Fixed Points. One WARN: S Q5's *answer* discloses §5's exam-critical
  `False`-vs-`Unknown` discrimination.
- Soundings rubric: **present** (L88–94, all three branches, 0–2 branch names Ch 5 §5 by section).
- Soundings answer disclosure: **present** — `<details>` at L69, closed L96.
- Bearings revision prompts: **present on all three**, each naming a section (§2 / §4 / §7).

**Ship-blocking:** one item (TYB3 Q2). Everything else is WARN-level.

---

## Question-budget compliance

| Category | Target (outline `question_budget`) | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 16 | 16 | met |
| Taking Your Bearings (checkpoints) | ≥2 (outline plans 3, at 6+5+5) | 3, at 6+5+5 | met |
| Practice Questions | 15 | 15 | met |
| **Chapter total** | **39** | **39** | **met** |

The outline raised Bearings from B4's 10 to 16 specifically so retrieval could land at exactly 25%
across three checkpoints of ≥5. The draft honours that: 6 + 5 + 5, with 1 + 1 + 2 retrieval.

### Practice-question distribution vs the outline's per-section plan

The total is met, but the allocation drifted:

| Section | Outline plan | Actual | Delta | Items |
|---|---|---|---|---|
| §1 triage method / two-audience split | 1 | **0** | **−1** | — |
| §2 never started | 5 | 4 | −1 | Q1, Q3, Q4, Q8 |
| §3 commands and events | 2 | 4 | +2 | Q2, Q7, Q10, Q15 |
| §4 started then gone | 4 | 3 | −1 | Q5, Q6, Q9 |
| §5 node-level | 1 | 2 | +1 | Q11, Q12 |
| §6 skew and known issues | 1 | 1 | 0 | Q13 |
| §7 metrics and logs | 1 | 1 | 0 | Q14 |

§2 is the chapter's highest-risk section (B1 gap G2) and came in one item under its plan while §3
came in two over. More consequentially, §1 was allocated one item and received zero — see the
coverage table below, where `platform-scope-vs-application-scope` is the chapter's only untested
owned concept that the chapter's own §1 argues is the first move in any investigation.

**Interleave tags:** three present, as planned — Q7 `[interleaved: D1.1 workloads]`, Q8
`[interleaved: D2.2 security]`, Q13 `[interleaved: D1.3 scheduling]`. Q13's tag is **wrong**: the
question is about kubelet version skew against the API server, which is D2.3 / Ch 8 §6 material.
Nothing in it touches scheduling. Either retag it or replace it with the planned scheduling
interleave (the outline specified "one pairs a Pending Pod with a taint" — that is Q1, which
carries no tag at all).

---

## Soundings spoiler check

The chapter's five ★ Fixed Points, for reference:

| # | ★ Fixed Point | Line |
|---|---|---|
| FP1 | Every failure in §2 means no container ever executed | L325 |
| FP2 | On a crash-looping Pod, `kubectl logs` returns nothing; `--previous` reads the container that died | L419 |
| FP3 | Liveness failure restarts the container; readiness failure removes it from Service endpoints | L701 |
| FP4 | `kubectl top` requires metrics-server, which a stock cluster does not have | L1042 |
| FP5 | Read the phase before you read the logs | L1242 |

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 (L53) | `Reason` belongs to container state, not phase (Ch 5 §5) | **no** | Tests the taxonomy's existence. Never mentions reading order, so FP5 survives. |
| 2 (L55) | Is anything retrying a `Pending` Pod? (Ch 7 §2/§4) | **no** | Answer (L74) states `Pending` is a stable report. FP1's claim — *no container ever executed across the whole family* — is not stated. |
| 3 (L57) | `imagePullPolicy` default and `:latest` (Ch 2 §6) | **no** | Prior-chapter fact. Touches no Fixed Point. |
| 4 (L59) | Derive QoS class from requests/limits (Ch 5 §8) | **no** | Correctly stops at derivation. Does **not** ask about eviction order, per the outline's own constraint. FP3 untouched. |
| 5 (L61) | What `Ready=False` reports, and who wrote it (Ch 8 §4) | **no** — but see WARN | No Fixed Point involves node conditions. |
| 6 (L63) | Oldest supported kubelet against a 1.37 control plane (Ch 8 §6) | **no** | Deliberate decay probe. No Fixed Point covers skew. |
| 7 (L65) | Logs of one container in a three-container Pod (Ch 5 §2) | **no** | Stem and answer (L84) are constrained to `-c`. Neither mentions `--previous`, so **FP2 is intact** — this was the outline's tightest spoiler risk and the draft held it. |
| 8 (L67) | Ingress object with no Ingress controller (Ch 10 §3) | **no** | Uses an Ingress controller precisely so that **FP4 is not spoiled**. Neither `kubectl top` nor metrics-server appears. |

**Verdict: clean.** All eight are answerable from Ch 1–12 or general professional knowledge, none
requires chapter-only material, and no stem or answer states a Fixed Point.

> ⚠ **WARN — S Q5's answer leaks §5's exam-critical discrimination.**
> The answer at L80 reads: *"The kubelet reports node status; the node controller sets `Ready` to
> `Unknown` if it stops hearing from the node entirely."* The question only asked what `Ready=False`
> reports. §5 (L748–750) states that the `False` vs `Unknown` distinction is "the one to take to the
> exam," and **both** TYB2 Q3 and Practice Q11 depend on it. Handing the reader that discrimination
> in the pre-test answer key, before §5 argues it, weakens two graded items.
> **Fix:** truncate the L80 answer after the first clause — "`Ready=False` means the node is not
> healthy and is not accepting Pods; the kubelet is what reports node status." Drop the `Unknown`
> sentence and let §5 introduce it.

*Format note (not a finding):* all eight Soundings are open-response rather than multiple-choice,
so distractor analysis does not apply to them. This matches shipped house form — Ch 12's Soundings
(chapter-12, L389–403) are open-response too.

---

## Per-question findings

### Q[TYB3] 2: "Your control plane is at 1.37. You are asked whether a node running kubelet 1.33 is supported. What is the answer, and what is the rule?"

**Issue: FAIL — the answer key states the wrong letter.** The key at L1130 opens `**2. C.**`, then at
L1136 says *"So the correct answer is **B**, not C,"* and its bullets explain **B is correct** and
**C is wrong**. A reader who scores against the bold header marks a correct answer wrong. A reader
who reads the body gets the right fact from a key that visibly argues with itself, which is not the
house form for an answer key and undermines confidence in every other key in the chapter.

There is an `AUTHOR-REVIEW` comment at L1143 acknowledging this and deferring it to the revision
stage. Recording it here as a formal FAIL so it cannot ship unresolved: the answer key currently
states an incorrect answer.

**Distractor analysis (stem at L1089):**
- A) "the kubelet may be any version older than the API server" — **plausible**; targets the real
  belief that old kubelets are always tolerated. Good.
- B) "Not supported — at most three minor versions older, and 1.33 is four behind 1.37" — **the
  correct answer.**
- C) "Supported — up to three minor versions older, and 1.33 is three behind" — **the intended trap,
  and a good one.** It states the rule correctly and miscounts, which is exactly the off-by-one
  people make. The trap is sound; only the key is broken.
- D) "the kubelet must exactly match the API server's minor version" — **plausible**; a real belief
  among people who have only ever upgraded whole clusters at once.

**Why-wrong explanation status:** **present but keyed to the wrong option.** All four options are
explained, and the explanations are individually correct. The defect is the header letter and the
mid-answer self-correction at L1134–1136.

**Recommended fix:** rewrite as a clean key headed `**2. B.**`, opening on the source quote
(*"`kube-apiserver` is at 1.37; `kubelet` is supported at 1.37, 1.36, 1.35, and 1.34"*
[source: k8s-version-skew-policy-2026-08-31]) and stating the floor is 1.34, so 1.33 is outside the
window. Then explain C as the off-by-one without the key having to walk into it: *"C states the rule
correctly and then miscounts. Three minors below 1.37 is 1.34, not 1.33. This is the single most
common error in applying the skew window, which is why the option asserts the miscount out loud."*

---

### Q[TYB2] 4: "You run `kubectl get pods` on a node you suspect is broken and see nothing unexpected. You then run `crictl ps` on that node and find a container running that `kubectl` did not report."

**Issue: WARN — trap fidelity. This stem commits the exact error that Practice Q12 exists to catch.**

Practice Q12 (L1364) presents `kubectl get pods -o wide` showing two Pods and `crictl ps` showing
four containers, and its correct answer is **A**: the comparison is invalid because `crictl ps` lists
*containers* and `kubectl get pods` lists *Pods*. Its why-wrong for B (L1466) is explicit: *"You must
compare like with like before concluding there is a discrepancy at all. The genuine `crictl` signal
is a container the cluster has no record of, which requires matching Pod and container identities,
not counting rows."*

TYB2 Q4's stem asserts a container-level discrepancy discovered by comparing `crictl ps` against a
bare `kubectl get pods` — the Pod-level command, un-scoped to the node — and its correct answer C
draws precisely the conclusion Practice Q12 forbids from that comparison. A reader who has learned
Q12's lesson should answer TYB2 Q4 with "you cannot conclude that yet."

The two items are recoverable — Q4's stem *stipulates* that the container is unreported, which is a
stronger premise than Q12's row count — but the stem does not say how that was established, and it
names the wrong command for establishing it.

**Distractor analysis:**
- A) "`crictl` is showing stale data and should be ignored" — **plausible**; targets real distrust of
  node-level tools. Acceptable.
- B) "registered with the API server but hidden by a namespace filter" — **plausible and useful**;
  the key handles it honestly (L887) by conceding it is worth ruling out in practice. Good.
- C) correct.
- D) "The container belongs to a different cluster" — **implausible.** No misconception supports it;
  the key's own rebuttal (L889) is a one-line statement of fact. Reduces this to a three-option item.

**Why-wrong explanation status:** present and specific for A, B, D.

**Recommended fix:** two edits. (1) Tighten the stem so the identity match is explicit and the
command is the right one: *"...you run `kubectl get pods -o wide --all-namespaces` and confirm no
Pod on that node accounts for it. `crictl ps` lists a running container whose Pod appears nowhere in
the API."* (2) Replace D with a distractor targeting a real belief — e.g. *"The container is a
static Pod, which `kubectl` never displays"* (false: static Pods get mirror Pods in the API, and the
belief that they are invisible is genuinely common).

---

### Q[TYB3] 1: "`kubectl top nodes` returns an error on a cluster where every node is `Ready` and every workload is healthy."

**Issue:** WARN — two of three distractors are non-functional.

**Distractor analysis (stem at L1082):**
- A) "The nodes have insufficient permissions to report metrics" — **plausible**; RBAC-flavoured and
  targets a real confusion about what metrics-server needs. Keep.
- B) correct.
- C) "The `top` subcommand was removed in a recent Kubernetes release" — **implausible.** No reader
  holds this belief; the key's rebuttal (L1126) is "`kubectl top` is current and unremoved," which is
  an assertion rather than a correction of a misconception.
- D) "The nodes are under memory pressure and cannot compute their usage" — **self-contradicted by
  the stem**, which stipulates every node is `Ready` and every workload healthy. The key says so
  itself (L1127). A distractor the stem has already eliminated is not a distractor.

**Why-wrong explanation status:** present for all three, but A is the only one doing work.

**Recommended fix:** replace C and D with misconception-bearing options:
- for C: *"metrics-server is installed but has not finished its first scrape window"* — targets the
  real belief that the error is transient and will resolve on retry.
- for D: *"The cluster has no HorizontalPodAutoscaler, so the Metrics API is not activated"* —
  targets a genuine inversion of the §7 dependency (HPA depends on the Metrics API, not the reverse),
  and productively collides with TYB3 Q3.

---

### Q[Practice] 1: "`0/6 nodes are available: 6 node(s) had untolerated taint {workload: gpu}`"

**Issue:** WARN — one dead distractor; also the chapter's only Pending-plus-taint item carries no
interleave tag despite the outline planning it as one.

**Distractor analysis (stem at L1287):**
- A) "The cluster is out of capacity and needs more nodes" — **strong.** This is the chapter's named
  Navigational Hazard (capacity and taints look identical from outside) and the key flags it as the
  trap. Keep.
- B) correct.
- C) "resource requests exceed every node's allocatable capacity" — **plausible**; a reader who did
  not parse the event text lands here. Keep.
- D) "The scheduler is malfunctioning and should be restarted" — **implausible.** The stem quotes a
  coherent, informative scheduler event; concluding the scheduler is broken requires ignoring the
  text you were just handed. The key's rebuttal (L1400) even says the message *is* the scheduler
  functioning.

**Why-wrong explanation status:** present and specific for A, C, D.

**Recommended fix:** replace D with *"The Pod will be scheduled once the scheduler's next backoff
cycle retries it with the taint ignored"* — targets the Ch 7 decay misconception the Soundings Q2
probes and §2 corrects, and keeps the item four-way live. Also add `*[interleaved: D1.3 scheduling]*`
to this stem and retag Practice Q13 (see the budget section above).

---

### Q[Practice] 3: "Which of the following is *not* a plausible cause?" (`ImagePullBackOff`)

**Issue:** WARN — why-wrong explanation is complete in substance but not in house per-option form.

**Why-wrong explanation status:** **present but collapsed.** The key (L1409–1411) gives D a full
explanation, then handles the three non-answers in a single grouped line: *"A, B, C are all
documented causes,"* followed by two source quotes. The quotes do map onto all three (invalid image
name → A; private registry without an imagePullSecret → B; "have you pushed the image to the
registry?" → C), so the reader is not left without a reason. But on a NOT-question the reader's error
mode is *picking one of A/B/C*, and each of those needs its own named rebuttal — that is the whole
self-correction mechanism.

**Recommended fix:** split into three bullets keyed to the option letters, each carrying its own
source quote, matching every other key in the chapter.

---

### Weak-distractor summary (remaining items)

These are single-option defects that do not warrant a full block. Each reduces a four-option item to
an effective three:

| Item | Option | Text | Why it is non-functional | Suggested replacement |
|---|---|---|---|---|
| TYB1 Q2 (L462) | A | "restart counts are unreliable for `Waiting` containers" | Asserts a property of the tooling nobody believes; key rebuts by flat denial (L520) | "The container is being created and the count has not incremented yet" — targets the real belief that `ContainerCreating` and `ImagePullBackOff` are the same waiting state |
| P Q4 (L1308) | C | "An expired TLS certificate on the API server" | Would break far more than one container's config and cannot produce a per-container `Reason` | "The Pod's ServiceAccount was deleted" — genuinely adjacent to config assembly and a real cause of confusion |
| P Q9 (L1343) | D | "The restart count is a display artifact and carries no information" | No misconception supports it; the chapter has spent two sections arguing the opposite | "The Pod is `Ready` now, so the seven restarts must have been the platform, not the application" — targets a real inversion |
| P Q12 (L1364) | D | "The node belongs to two clusters simultaneously" | Structurally impossible; no reader considers it | "Some of those containers are the node's static Pods, which run outside any Deployment" — plausible and productively wrong |
| P Q14 (L1378) | D | "Adding a readiness probe to the workload" | Probes and usage metrics share no mechanism; nothing connects them | "Enabling the kubelet's `/metrics/resource` endpoint, which is off by default" — targets a real misreading of the §7 pipeline figure |
| P Q15 (L1385) | D | "Events are only written for successful operations" | Contradicted by every example in the chapter | "The Pod's events were garbage-collected when the Pod was deleted, so a surviving Pod always retains its events" — targets a real conflation of event TTL with object lifecycle |

Two further options are **marginal but defensible** and I am not counting them as findings:
P Q2 option D (`AGE`) — a reader may genuinely think a long-lived Pod implies it started; and
P Q10 option D (`kubectl describe pod`) — a reader may think `describe` surfaces log content.

### Trap answers verified as targeting real, common misconceptions (no action)

Recorded so the revision stage does not "fix" working traps:

- **TYB1 Q1 D** ("started and then exited with a configuration error") — the never-started /
  started-then-died confusion, the chapter's central discrimination.
- **TYB1 Q2 D** (`restartPolicy: Never`) — real inference from a zero restart count.
- **TYB1 Q4 A** ("in the Pods' events — find the Pod name first") — the reflex that produces
  `NotFound` and a false conclusion. This is the sharpest trap in the chapter.
- **TYB1 Q6 C** ("tags and digests are two spellings of the same identifier") — real.
- **TYB2 Q1 A/C** (eviction described as OOM kill) — the chapter's top confusion pair.
- **TYB2 Q5 D** (`Guaranteed` = exempt from eviction) — real, and the key correctly draws the
  last-versus-never distinction.
- **TYB3 Q3 A** ("the HPA object is rejected at creation") — real, and it is the exact inverse of
  Ch 10's named pattern.
- **P Q5 D** ("throttled to 256Mi and continues running") — the CPU-throttle / memory-kill
  confusion. Excellent.
- **P Q6 D** (`Guaranteed` evicted first) — real inversion.
- **P Q8 D** ("refused at admission because the Secret did not exist") — real, and it forces the
  reader to use the "is there a Pod object" branch.
- **P Q13 D** ("the kubelet will report an error event for each unimplemented field") — real, and
  the silence is precisely the hazard §6 argues.

---

## Retrieval-practice spacing

- Chapter 13 target: **20–25%** of checkpoint questions from earlier chapters (skill Part 10,
  "Chapter 6+"; the arc outline sets 25% as a ceiling, not a floor).
- Actual: **25.0%** — 4 of 16 questions tagged `[retrieval: chN]`.
- Status: **compliant**, sitting exactly on the ceiling as designed.

| Checkpoint | Qs | Retrieval | Local % | Tagged item |
|---|---|---|---|---|
| TYB 1 (after §3) | 6 | 1 | 16.7% | Q6 `[retrieval: ch2]` — tag vs digest |
| TYB 2 (after §5) | 5 | 1 | 20.0% | Q5 `[retrieval: ch5]` — QoS derivation |
| TYB 3 (after §7) | 5 | 2 | 40.0% | Q2 `[retrieval: ch8]` — skew window; Q3 `[retrieval: ch10]` — named-component pattern |
| **Chapter** | **16** | **4** | **25.0%** | |

TYB 3's local 40% is the outline's deliberate design (§6 and §7 are the book's decay-fix anchors for
Ch 8 and Ch 10, so the checkpoint after them is where the repair is verified). The chapter average is
the governing number and it is at the ceiling. No action.

> ⚠ **WARN — tag fidelity. Two of the four tagged items are hybrids.**
> The outline set a deliberately narrow definition and instructed the drafting stage to hold it:
> *"a retrieval question is one whose answer lives in an earlier chapter."* Measured strictly:
>
> - **TYB1 Q6** `[retrieval: ch2]` — **clean.** Answer is entirely Ch 2 §3.
> - **TYB3 Q2** `[retrieval: ch8]` — **clean.** Answer is entirely Ch 8 §6; §6 of this chapter
>   deliberately never restates the numbers.
> - **TYB2 Q5** `[retrieval: ch5]` — **hybrid.** The stem asks two things. QoS derivation is Ch 5 §8;
>   *"and what does that mean for eviction order"* is §4 of **this** chapter.
> - **TYB3 Q3** `[retrieval: ch10]` — **hybrid.** The pattern is Ch 10 §3; the metrics-server
>   dependency the pattern is applied to is §7 of **this** chapter.
>
> Strictly clean retrieval is therefore **2 of 16 = 12.5%**, which still clears the 10% floor but
> sits at the bottom of the band rather than the top. The chapter is not non-compliant — hybrids are
> the more pedagogically valuable form, and this chapter is by design mostly applied prior material —
> but the reported 25.0% overstates how much *purely* earlier-chapter retrieval is happening.
>
> **Recommended fix (cheap, preserves the 25% count):** split TYB2 Q5 into a clean retrieval stem —
> drop the eviction-order clause, ask only for the QoS class and the reason — and move the eviction
> consequence into the existing Practice Q6, which already owns eviction order. TYB3 Q3 is worth
> leaving as-is: the transfer *is* the point of that item, and mislabelling it would cost more than
> the tag's precision is worth. Note the residual hybrid in the outline's retro instead.

---

## Coverage vs concepts

Drawn from the outline's `kb_tags.concepts` and `kb_tags.commands`. "Tested" means the concept is
load-bearing in a question stem or in a correct answer — appearing only inside a why-wrong
explanation does not count, since the reader meets it after committing.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| platform-scope-vs-application-scope | **NO** — see below |
| triage-flow | yes (TYB1 Q3; P Q7) |
| pod-failure-signature-map | yes (implicitly across TYB1 Q1–Q5; P Q2) |
| pending-diagnosis | yes (TYB1 Q3; P Q1) |
| imagepullbackoff-diagnosis | yes (TYB1 Q2; P Q3) |
| errimagepull | yes (TYB1 Q2; P Q3) |
| createcontainerconfigerror | yes (TYB1 Q1; P Q4; P Q8) — three items, the chapter's heaviest concept |
| imageinspecterror | **NO** — appears only in the §2 reason table (L280) and the two figures |
| admission-rejection-versus-pod-failure | yes (TYB1 Q4; P Q8 option D) |
| kubernetes-events | yes (TYB1 Q3; P Q7; P Q15) |
| event-retention-window | yes (P Q15) |
| **crashloopbackoff** | **NO** — see below |
| **restart-backoff-curve** | **NO** — the 10s/20s/40s curve, the 300s cap, and the 10-minute reset are taught at L596–598 and tested nowhere |
| oomkilled-signature | yes (TYB2 Q1; P Q5) |
| evicted | yes (P Q6; TYB3 Q4) |
| node-pressure-eviction | yes (P Q6) |
| eviction-order-by-qos-class | yes (TYB2 Q5; P Q6) |
| probe-failure-signatures | **partial** — readiness is tested (TYB2 Q2); the **liveness half of FP3 is untested** |
| node-conditions-as-diagnostic | **partial** — `Unknown` is tested (TYB2 Q3; P Q11); the `False` vs `Unknown` discrimination §5 calls "the one to take to the exam" (L748) is never asked |
| kubelet-health | partial (TYB2 Q4, via the crictl route) |
| **node-lease-heartbeat** | **NO** — taught at L755, tested nowhere |
| node-death-handling | yes (TYB2 Q3; P Q11) |
| crictl | yes (TYB2 Q4; P Q12) |
| version-skew-symptoms | yes (TYB3 Q2; TYB3 Q5; P Q13) |
| **release-known-issues** | **NO** — §6 owns it as a named triage step (L965–969) and no item touches it |
| resource-metrics-pipeline | yes (TYB3 Q1; P Q14) |
| metrics-server | yes (TYB3 Q1; TYB3 Q3; P Q14) |
| kubectl-top | yes (TYB3 Q1; P Q14) |
| cluster-log-architecture | yes (TYB3 Q4) |

| Command introduced in chapter | Tested in a question? |
|---|---|
| kubectl-describe | yes (TYB1 Q3; P Q7) |
| **kubectl-events / kubectl-get-events** | **NO** — the commands appear at L368 and in the §3 figure; no item requires selecting them. P Q15 tests event *expiry*, not the command |
| kubectl-logs | yes (P Q10) |
| kubectl-logs-previous | yes (P Q10) |
| kubectl-get-pod-o-wide | partial — appears in P Q12's stem as given context, never as the answer |
| kubectl-top | yes (TYB3 Q1; P Q14) |
| crictl-ps | yes (TYB2 Q4; P Q12) |
| crictl-pods / crictl-logs / crictl-inspect | **NO** — `crictl logs` is taught at L800 and untested |

### The three gaps worth fixing before ship

**1. `CrashLoopBackOff` is untested, and it is Exam Alert high-priority topic #2.**
The string never appears in a question stem and is never a correct answer. It surfaces only inside
two why-wrong explanations (P Q2 option A at L1405; P Q3's answer at L1409), where the reader meets
it *after* committing. §4 spends its longest subsection (L579–610) on it, the Chapter Summary gives
it the longest row (L1500), the Exam Alert names it twice (L1260, L1270), and the ⚠ Navigational
Hazard at L604 calls the `ImagePullBackOff` / `CrashLoopBackOff` sibling confusion out explicitly —
and nothing asks the reader to demonstrate it. This is the single largest coverage hole in the
chapter.
**Fix:** add one item, most naturally in TYB2 (which currently runs 5 against TYB1's 6, so the
budget absorbs it at 17 — or swap it in for P Q9, which overlaps TYB2 Q2's territory). Suggested
stem: *"A Pod shows `CrashLoopBackOff`. Which of the following has definitely already succeeded?"*
with options covering the image pull, the config assembly, and the process launch (all correct,
combined in the key answer) against distractors asserting an image or scheduling failure. That tests
FP-adjacent reasoning rather than string recall, and it directly discharges the Exam Alert trap.

**2. `platform-scope-vs-application-scope` is untested, and §1 received zero of its one planned
Practice item.** §1 gives the boundary a mechanical test — *"If the Pod is `Running` and `Ready` and
the behavior is still wrong, you have crossed into application scope"* (L172) — the ☀️ §8 Zenith
turns on it (L1234–1240), and The Voyage Ahead hands the reader to Ch 16 on it. Nothing tests it.
**Fix:** restore the planned §1 Practice item. Suggested stem: *"A Pod is `Running`, `1/1 Ready`,
restart count 0, on a node reporting `Ready=True`. Users report it returns the wrong data. What is
your next move?"* — correct answer: the platform has finished its work, so this is application scope;
distractors reaching for `describe`, the events, and the node conditions each target the real habit
of continuing to interrogate the platform after it has answered.

**3. §6's `release-known-issues` and §5's `node-lease-heartbeat` are taught and untested.**
Lower stakes than the two above — both are single-paragraph concepts on an associate-tier exam — but
`release-known-issues` is one of only two concepts §6 owns, and §6 has exactly one Practice item
(Q13), which spends it on skew. If a fourth TYB3 slot opens, known-issues-as-a-triage-step is the
natural occupant; otherwise record both in the retro as accepted, deliberate non-coverage rather than
oversight.
```

---

**Headline for the gate:** budget is exact (39/39), Soundings spoiler check is clean against all five Fixed Points, retrieval sits at 25.0%. One ship-blocker — the TYB3 Q2 answer key is headed `C` but concludes `B`, so a reader scoring against the letter marks a correct answer wrong. Two coverage holes worth fixing: `CrashLoopBackOff` (Exam Alert priority #2) is never tested in any stem or correct answer, and §1's platform-vs-application boundary got zero of its one planned Practice item despite the Zenith turning on it.

Note: the Write tool was denied for `diagnostics/question-quality.md`, so the artifact is above rather than on disk. If the orchestrator doesn't capture stdout for this stage, grant the write and I'll persist it.