# Fact-Accuracy Audit — Chapter 6

## ⚠ INPUT SUBSTITUTION — READ BEFORE CONSUMING THIS REPORT

**Mode detected: STANDARD** (the audited draft carries 162 `[source: ...]` tags; the source cache is fully populated).

**But the stage's declared input did not exist, and the substitute I audited is not the file the next stage will edit.** Recorded here because the revision stage must resolve this before applying any fix below.

| Declared input | State |
|---|---|
| `.pipeline-state/ch-06/draft-v2.md` | **Does not exist.** Chapter 6 has not reached the revision stage; no `draft-v2*` file is present. |
| `.pipeline-state/ch-06/draft-voice.md` | **Does not exist.** This book's voice stage writes `draft-vN.md` and backs up `draft-vN-prevoice.md`; it never produces `draft-voice.md`. |
| `.pipeline-state/ch-06/draft-v1.md` | **Present but truncated — 253 lines, 24 KB.** Begins mid-word (`ognition exam can ask about…`). Contains only the chapter's tail, from the Exam Alert block onward. |
| `.pipeline-state/ch-06/draft-v1-prevoice.md` | **Intact — 1,213 lines, 119 KB.** Full chapter, all nine sections, 162 source tags. **This is what I audited.** |

The truncation is independently corroborated by this chapter's own structural linter run (`diagnostics/structural.md`, 8 fail / 4 warn against `draft-v1.md`): it reports Chapter Title, Witty Subtitle, Attention Budget, Why This Chapter Matters, Soundings, Fixed Point, Dead Reckoning and Taking Your Bearings all **missing**. Every one of those is present in `draft-v1-prevoice.md`. The chapter is not malformed; the voice stage's stdout capture lost the first ~960 lines. This is the same failure class as commits `c358a92` and `821f1ef`.

**Consequences for this report:**

1. All line numbers below refer to **`draft-v1-prevoice.md`**, not to `draft-v1.md`.
2. Findings against material in lines 1–955 **cannot be applied to `draft-v1.md`** — that text is not in the file. The voice-swap output must be regenerated first.
3. The voice swap is a light-touch pass in this book (ch-05: 109,606 → 109,592 bytes, ~0.01% delta), so the pre-voice text is a faithful proxy for *facts and source tags*. It is not a proxy for prose. No voice judgments are made here.

---

## Summary

- Total factual claims inspected: **≈185** — 162 carrying `[source: ...]` tags, plus ~23 untagged assertions about external authorities, vendor behavior, or third-party tooling
- Tagged claims verified against cache: **160**
- Tagged claims unverifiable (tag points to missing/empty snapshot): **0** — all 25 distinct snapshots referenced exist in the cache; **zero dangling tags**
- **Untagged factual claims (FAIL): 7**
- **Contradicted claims (FAIL): 2**
- Minor discrepancies (WARN): **9**

Two of the three findings with the highest consequence were **pre-flagged by this chapter's own research manifest** (Notes 1 and 3) and by Chapter 1's kb-manifest. One of those pre-flagged corrections was adopted by the draft (the 13/8 rounding fix — see PASS); two were not.

---

## FAIL — Contradicted claims

### Line 104: "CNCF publishes four domain weights and twelve named competencies with no sub-weights"

**Tag:** `[source: cncf-kcna-curriculum-pdf-2026-08-23]`

**Snapshot says** (enumerating the curriculum in full):

> "44% – Kubernetes Fundamentals: Kubernetes Core Concepts; Administration; Scheduling; Containerization
> 28% – Container Orchestration: Networking; Security; Troubleshooting; Storage
> 16% – Cloud Native Application Delivery: Application Delivery; Debugging
> 12% – Cloud Native Architecture: Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration"

That is 4 + 4 + 2 + 3 = **thirteen** named competencies. The same thirteen are enumerated identically in `lf-kcna-exam-page-2026-08-23.md` and `lf-kcna-program-changes-2026-08-23.md`. No cached source states twelve.

**Draft says:** "twelve named competencies"

**This is a known, previously-diagnosed error that has now reached reader-facing prose.** `ch-01/kb-manifest.md` line 94 already recorded it:

> "**Competency count: 13, not 12.** B2 says '12 competencies' and 'twelve named competencies' twice. The cached CNCF curriculum snapshot enumerates 4 + 4 + 2 + 3 = **13**… **Chapter 1 is correct; the ratified outline is wrong** — correcting B2 is an author action outside this stage's write scope."

The wrong figure lives in the ratified book artifact `book-outline/chapter-lineup.md` line 11 and propagated from there into `ch-06/outline.md` line 792 and then into this draft. Chapter 5 carries it too, but only inside an `AUTHOR-REVIEW` HTML comment. **Chapter 6 line 104 is the first occurrence in shipped body prose** — it sits in "Why This Chapter Matters," one paragraph after the domain-weight disclosure, which is precisely the sentence a reader will trust.

**Recommended fix:** change "twelve named competencies" → "thirteen named competencies" at line 104. Then escalate the book-level correction to `book-outline/chapter-lineup.md` line 11, per the ch-01 integration note ("Correct B2 to thirteen before Chapter 19's synthesis"); until that lands, every subsequent chapter's outline will re-seed the error.

---

### Line 1189 (Chapter Summary table, Job row): "**Job** | Runs to completion, once. Reaches `Succeeded` or `Failed`"

**Tag:** none (summary table row).

**Snapshot says** (`k8s-docs-job-2026-08-24.md`, on finished Jobs):

> "Another way to clean up finished Jobs (either `Complete` or `Failed`) automatically is to use a TTL mechanism…"

And `k8s-docs-pod-lifecycle-2026-08-23.md`, on **Pod** phases:

> "Succeeded — All containers in the Pod have terminated in success, and will not be restarted."

**Draft says:** the *Job* "Reaches `Succeeded` or `Failed`."

`Succeeded`/`Failed` are **Pod phases**. A Job's own terminal terms are `Complete`/`Failed` (Job conditions). The summary row attributes the Pod vocabulary to the Job object.

This is the exact hazard the chapter's research manifest raised in advance — **Notes for the author, note 3**:

> "the Job page's own terms for a finished Job are **`Complete` or `Failed`** (Job conditions), while `Succeeded`/`Failed` are **Pod phases**… the draft should not write 'the Job reaches `Succeeded`.'"

The body prose (§7, line 706) and Practice Question 16 both handle this correctly — Q16 asks "Which **Pod phase** does it reach," and its answer key is right. Only the summary table slips, and the summary table is the chapter's memorization surface.

**Recommended fix:** rewrite the row as `Runs to completion, once. Its Pods reach phase `Succeeded` or `Failed`` — or, to teach both vocabularies: `Its Pods reach phase `Succeeded`; the Job itself gets condition `Complete``.

---

## FAIL — Untagged factual claims

### Lines 303, 1137, 1179: "neither one reports an error" / "there is no such validation" / "No error is reported"

**Why it's a factual claim:** it asserts a specific negative about Kubernetes API behavior — that overlapping controller selectors produce no diagnostic. It appears three times, and is load-bearing in all three: the §3 🪝 Snag, the keyed rationale for Practice Question 5 ("**A** is the answer people hope for; there is no such validation"), and the Chapter Summary row for "Overlapping selectors."

**What the cache does support:** `k8s-docs-replicaset-2026-08-24.md` warns "Be careful not to overlap with the selectors of other controllers, lest they try to adopt this Pod," and documents immediate acquisition and immediate termination. It documents the *hazard*. It says nothing about whether an error, event, or warning is emitted — and no other cached snapshot does either. This is an argument from documentary silence stated as a positive fact about system behavior.

**Fix:** either (a) soften to what the docs license — "the docs document no validation against overlapping selectors, and the symptom presents as flapping rather than as a rejected object" — or (b) open a research gap for `kubernetes.io/docs/concepts/workloads/controllers/replicaset/` events/status reporting and re-tag. Note that Practice Question 5's *keyed answer* depends on this, so leaving it unresolved leaves an answer key resting on an uncited negative.

### Line 460: "a Pod with no readiness probe is ready as soon as its containers are running, whether or not the application inside can serve anything"

**Why it's a factual claim:** it states the default readiness semantics for a probe-less container — a specific, checkable vendor behavior, and the hinge of §4's argument that omitting a readiness probe means opting out of rollout safety.

**What the cache supports:** `k8s-docs-pod-lifecycle-2026-08-23.md` defines `readinessProbe` and its failure behavior; `k8s-docs-pod-termination-2026-08-24.md` lists the `ContainersReady` and `Ready` conditions. Neither states what happens when no readiness probe is configured.

**Fix:** open a research gap for `kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/`, which carries the default-ready statement, then tag. Interim alternative: state it as the contrapositive of what *is* sourced — a Pod counts as available once ready, and with no readiness probe there is nothing for readiness to wait on.

### Line 78 (Soundings, answer 6): "systemd calls these `service` and `oneshot`"

**Why it's a factual claim:** it names specific identifiers in a third-party init system. No cached snapshot covers systemd — it is outside the source set entirely.

**Additionally imprecise:** `oneshot` is a value of `Type=`; `service` is a *unit suffix* (`.service`), not a `Type=` value. Both a long-running web server and a run-once backup script live in `.service` units; the pair that actually contrasts them is `Type=simple` (or `Type=exec`/`Type=notify`) versus `Type=oneshot`. As written, the sentence pairs a unit type with a `Type=` value as though they were siblings — and it is in a Soundings answer key, which is the reader's first calibration of whether the book is precise.

**Fix:** either change to "systemd calls these `Type=simple` and `Type=oneshot`," or drop the identifier-level specificity ("an init system treats the first as a service that should never exit and the second as a task that should"). The surrounding analogy needs no citation; only the named identifiers do.

### Line 812: "You will meet it again with Ingress — creating an Ingress resource has no effect without an Ingress controller to fulfill it"

**Why it's a factual claim:** it asserts vendor feature behavior. It sits in a four-item parallel list in which the third and fourth items (VPA, NetworkPolicy) *are* tagged — so the omission is inconsistent within a single block.

**The snapshot exists.** `k8s-docs-ingress-2026-08-23.md`: *"You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect."*

**Fix:** add `[source: k8s-docs-ingress-2026-08-23]`. One-token change.

### Line 812 (and restated at line 882): "`kubectl top`, which needs metrics-server deployed"

**Why it's a factual claim:** asserts a dependency between a CLI verb and an optional cluster component. Same untagged item in the same four-item list.

**The snapshot exists.** `k8s-docs-resource-metrics-pipeline-2026-08-23.md`: the metrics-server "implements the Metrics API… and provides access to CPU and memory usage for nodes and pods," "You can also view the resource metrics using the `kubectl top` command," and "It is a cluster addon component (not deployed by default in all distributions)."

**Fix:** add `[source: k8s-docs-resource-metrics-pipeline-2026-08-23]` at line 812. Line 882's restatement inherits it.

### Line 185: "You may occasionally meet **ReplicationController** in older tutorials and in `kubectl scale`'s own help text"

**Why it's a factual claim:** asserts the literal content of a shipped CLI's help output.

**The snapshot exists.** `k8s-docs-kubectl-overview-2026-08-23.md` documents the operation as: *"scale — Update the size of the specified replication controller / deployment."*

**Fix:** add `[source: k8s-docs-kubectl-overview-2026-08-23]`. The rest of the sentence's clauses are already tagged; this is the only unsupported one.

### Line 183: "A bare Pod is not replaced when its node fails — it is simply gone"

**Why it's a factual claim:** asserts what does *not* happen to an uncontrolled Pod on node failure. It closes the ⚓ Worth Securing block and is the block's actual payload; the preceding sentence is tagged but does not cover it.

**The snapshot exists**, and states it almost verbatim. `k8s-docs-replicaset-2026-08-24.md`: *"Unlike the case where a user directly created Pods, a ReplicaSet replaces Pods that are deleted or terminated for any reason, such as in the case of node failure or disruptive node maintenance, such as a kernel upgrade."*

**Fix:** add `[source: k8s-docs-replicaset-2026-08-24]`. Lowest-cost item in this section.

---

## WARN — Minor discrepancies

**1. Line 698 — the tag over-attributes. "A DaemonSet does not take a replica count… `[source: k8s-docs-daemonset-2026-08-24]`"**

The cited snapshot explicitly disclaims this sentence in its own closing note: *"no fetched sentence states explicitly that a DaemonSet has no `replicas` field; the Pod count follows from node eligibility… See research-manifest Gaps, G-6A."* The claim is true and soundly entailed — but the tag reads as though the snapshot says it, and it does not.

The negative form ("no replica count" / "no `replicas` field to set") is asserted in **five** places: line 698, the §7 ★ Fixed Point (722), Bearings #3 answer 2 (870), Exam Alert priority 3 (963), Chapter Summary (1188), plus Practice Q15's explanation (1157). The draft's own `AUTHOR-REVIEW` comment at line 696 flags exactly this and defers it to revision — so this WARN is confirming an open author question, not raising a new one.

Manifest **G-6A**'s recommendation: *"phrase the Fixed Point as* the count is a consequence of how many nodes match*, which is directly sourced, rather than as* there is no `replicas` field*, which is true but uncited."* The Exam Alert line already carries both formulations ("with no replica count. The count is a consequence, not a setting"), so the sourced half is available verbatim.

**Fix:** keep the entailment framing at 698 and re-tag to the sourced sentences (`"The DaemonSet controller creates a Pod for each eligible node"` + the HPA page's `"Horizontal pod autoscaling does not apply to objects that can't be scaled (for example: a DaemonSet.)"`, both already cited elsewhere in the section), and lead with the consequence form in the Fixed Point.

**2. Lines 168 / 175 / 992 / 1129 — "The ReplicaSet holds the count" is a simplification the docs only half-support.**

`.spec.replicas` is a documented field on **both** objects. `k8s-docs-deployment-spec-fields-2026-08-24.md`: *"`.spec.replicas` is an optional field that specifies the number of desired Pods. It defaults to 1"* — that is the *Deployment* spec. `k8s-docs-replicaset-2026-08-24.md` documents the same field on the ReplicaSet.

The §1 ★ Fixed Point ("The ReplicaSet holds the replica count") states the pedagogical version without qualification. Practice Question 1 keys to B (the ReplicaSet) and its explanation *does* handle the tension well — "you *set* `replicas` on the Deployment, and the Deployment propagates it to the ReplicaSet it manages — but the object whose job is maintaining that many Pods is the ReplicaSet, and during a rollout there are two of them holding different numbers." That reasoning is correct and is the right teaching. The Fixed Point should not be more absolute than the answer key that defends it.

**Fix:** consider "the ReplicaSet is the object that *maintains* the count" in the Fixed Point, preserving the distinction the answer key already draws. (The "propagates it to the ReplicaSet" mechanism itself is entailed but not stated in cache — hedge or leave as the explanation's reasoning rather than a sourced claim.)

**3. Lines 104, 571, 972 — exam-frequency framing exceeds what the cache licenses.**

- Line 571: "this exact distinction is a **recognition-exam favourite**"
- Line 972: "**Common Traps** — these are **documented confusions**, not invented ones"
- Line 104: "the **three documented confusions** around it"

No cached source speaks to how often the KCNA tests anything, or to which confusions are common among candidates. The docs document the *distinctions*; they do not document that readers confuse them.

This book has an established precedent on exactly this point. `k8s-blog-dockershim-faq-2026-08-24.md` carries a standing framing constraint: *"trap #34 remains [inferred] AS TO EXAM FREQUENCY. Nothing on this page speaks to how often the exam tests it. Write 'easy to confuse', never 'frequently tested'."*

What **is** sourced and can carry the weight: the exam is *"an online, proctored, multiple-choice exam"* (`cncf-kcna-certification-page-2026-08-23`, `lf-kcna-exam-page-2026-08-23`). So "recognition exam" as a descriptor is fine and used correctly elsewhere. It is "favourite" and "documented confusions" that overreach.

**Fix:** "a recognition-exam favourite" → "exactly the shape a recognition item is built from" (which the chapter already uses well at line 478). "documented confusions" → "confusions the documentation goes out of its way to pre-empt," which is defensible — the ReplicaSet page's overlap warning and the StatefulSet page's "not interchangeable" sentence both read as pre-emptive.

**4. Line 10 — Attention Budget total does not match its own table.**

Header: "Total time: ~95 minutes." The table sums to **105** (12+7+12+6+16+11+6+9+8+12+6). Internal arithmetic, not a source matter, but it is a number a reader can add up.

**Fix:** ~105 minutes, or trim the table.

**5. Lines 812 / 882 — the "four gotchas" count is inconsistent between its two statements.**

Line 812 names **four** forward examples (Ingress, `kubectl top`, VPA, NetworkPolicy) then concludes "Four gotchas, one rule" — which makes five instances counting the CRD case being taught. Line 882 names **three** (Ingress, `kubectl top`, VPA) and also concludes "four gotchas," which is consistent if the CRD case is the fourth. The two passages count differently.

**Fix:** pick one roster and use it in both places. The line-882 version (three forward + the CRD case = four) is the cleaner claim.

**6. Lines 219–224 — sample `kubectl get pods` output omits the `RESTARTS` column.**

The block shows `NAME  READY  STATUS  AGE`. Real `kubectl get pods` emits `NAME  READY  STATUS  RESTARTS  AGE`. **Not verifiable from cache** — no cached snapshot documents `kubectl` table output formats — so this is flagged for author judgment, not asserted as an error. It matters slightly more than usual here because §2 is built entirely on the reader running these two commands and comparing.

**Fix (author's call):** add the column, or state that output is elided for clarity.

**7. Line 531 — "'rolling back' is largely a matter of scaling it back up while scaling the current one down."**

The mechanism is not stated in any cached source. What *is* sourced is that `revisionHistoryLimit` retains old ReplicaSets "to allow rollback" (`k8s-docs-deployment-spec-fields-2026-08-24`), which makes the described mechanism a reasonable inference. The hedge "largely" is doing appropriate work. Recorded so a later pass does not harden it into an unqualified claim.

**8. Line 706 — "for a Job those two phases are the entire scoreboard" has an ambiguous antecedent.**

The sentence is unambiguously about *Pod* phases in context (the preceding clause is "Chapter 5 taught you five Pod phases"), so this is not the same defect as the Chapter Summary row. But "for a Job those two phases" invites the Job/Pod conflation that manifest Note 3 warns about, in the one section where the conflation is live.

**Fix:** "for a Job's Pods, those two phases are the entire scoreboard."

**9. Line 523 — "`rollout undo` restores a previous *Pod template*."**

`k8s-docs-deployment-2026-08-23.md` says undo "rolls back to the previous revision." Given the same page's if-and-only-if rule (a revision exists iff `.spec.template` changed), revision ≡ template state, so the draft's restatement is sound. It is one inferential step past the source wording, in a ⚠ Navigational Hazards block whose whole point is precision. Recorded, no change required.

---

## PASS — Verified claims

Sampled coverage, weighted toward the numerically checkable and the exam-facing.

**Prior corrections confirmed adopted:**

- **Manifest Note 1 (the 13/8 rounding correction) was applied correctly.** The ratified outline specified "at most twelve Pods, at least eight available" for ten replicas; the manifest flagged 12 as wrong. The draft states **13 and 8** at line 407–408, the figure caption at 376–381 uses the same pair, and Bearings #2 item 1 (543, 557–565) keys to "thirteen may exist; eight must remain available." The old wrong value is preserved as a *distractor* with its misconception named ("rounds surge down"), which is what the manifest recommended. Verified against `k8s-docs-deployment-spec-fields-2026-08-24`: surge "rounding up," unavailable "rounding down."
- **Manifest Note 4 (`backoffLimit` 6-vs-4 transcription conflict): checked, not applicable.** The draft never mentions `backoffLimit`. Recorded so the conflict is not re-derived downstream, per the manifest's own request.

**Deployment mechanics — all exact:**

- `RollingUpdate` is the default `.spec.strategy.type`; `Recreate` is the alternative (394, 416, 446)
- `maxSurge` and `maxUnavailable` both default to 25%; opposite rounding directions; neither may be 0 if the other is 0 (398–401, 1143)
- The API reference's 30%/130%/70% worked example, quoted accurately (410)
- `minReadySeconds` defaults to 0; `progressDeadlineSeconds` defaults to 600 and surfaces `type: Progressing` / `status: "False"` / `reason: ProgressDeadlineExceeded`; "the controller keeps retrying" (446, 452, 462)
- Stuck-rollout causes, five of the six listed, introduced with "including" (462)
- `revisionHistoryLimit` retains 10 old ReplicaSets by default; zero means rollout cannot be undone (513)
- A revision is created **if and only if** `.spec.template` changes; scaling does not (476, 486, 521, 569, 1145)
- All six `kubectl rollout` subcommands, exact against `k8s-docs-kubectl-rollout-2026-08-24` (492–501); valid resource types "deployments, daemonsets and statefulsets" (490)
- Pause/resume motivation quoted accurately (505, 587)
- 8-replica arithmetic in Practice Q7: surge 2 → max 10, unavailable 2 → min 6 (1141)

**Selectors, ownership, adoption:**

- Selector-must-match-template-labels, sourced independently in all three resources (ReplicaSet, Deployment, DaemonSet) at line 273 — matching manifest Note 6
- `matchLabels` ≡ `matchExpressions` with operator `In`; ANDed when both present (267)
- `metadata.ownerReferences`; ownership as a mechanism distinct from labels/selectors, with the Service/EndpointSlice example (285, 287)
- Cascading deletion; `kubectl delete` removes dependent Pods by default (289)
- Immediate acquisition of unowned matching Pods, and immediate termination when over count (295, 299, 1133) — the "Non-Template Pod acquisitions" material the manifest recommended in Note 5

**Workload family:**

- StatefulSet: "same spec… not interchangeable"; ordinal 0..N-1; hostname `$(statefulset name)-$(ordinal)`; one PVC per `volumeClaimTemplate` entry bound for the Pod's lifecycle; sequential creation 0→N-1 and reverse termination; predecessors must be Running and Ready; Headless Service required and author-provided; volumes not deleted on scale-down (614–652, 674, 676)
- DaemonSet: node-add behavior; three typical uses; `nodeSelector`/affinity narrowing and the all-nodes default; scheduler binds after controller creation; auto-added tolerations for unschedulable / disk / memory pressure / not-ready (688–694)
- Job: run-to-completion; `restartPolicy` restricted to `Never` or `OnFailure` (702, 708)
- CronJob: one crontab line; `.spec.schedule` required; `0 3 * * 1` = weekly Monday 3 a.m.; `.spec.jobTemplate` shares the Job schema; approximate scheduling → Jobs should be idempotent (712–718). Reader-facing cron expressions verified: `0 2 * * *` = nightly 02:00 (876); `0 4 * * *` = daily → 7 firings/week (1104, 1161)
- Deployment-as-interchangeable, quoted exactly from the workloads overview (606)
- ReplicationController superseded; the set-based-selector difference (185)

**Extension and the operator pattern:**

- Resource / custom resource / dynamic registration / `kubectl` parity (784–786)
- CRD serves and stores; less flexible than aggregation (792, 836)
- "On their own, custom resources let you store and retrieve structured data" (800)
- Declarative-vs-imperative separation of responsibilities (802)
- Operator pattern = custom resource + custom controller; extends the cluster "without modifying the code of Kubernetes itself"; the six-item automation list; **the controller normally runs outside the control plane, for example as a Deployment** (818–830, 891, 1163, 1165)
- CRI / CNI / CSI / API-extension as published extension points (834)
- Helm charts carry a `crds/` directory (838)

**Cross-chapter retrievals:**

- Pod replacement with a different UID, never rescheduled (82, 226, 1135)
- `spec` = desired / `status` = current, including the docs' own three-replica example (1131)
- Readiness failure removes the Pod's address from matching Service endpoints; liveness (not readiness) kills and restarts (454, 579, 1151)
- Pod phases `Succeeded` / `Failed` defined correctly where they are attributed to Pods (706, 1159)
- Job controller tells the API server to create or remove Pods rather than running them (247, 704)
- HPA as API resource + controller adjusting scale to observed metrics; does not apply to DaemonSets; ReplicaSet is a valid HPA target (251, 698, 872)

**Metadata and disclosure:**

- The 6% domain weight is labeled "authored allocation — see front matter" at line 4 and disclosed again in body prose at 104. This is handled correctly and matches the pattern Chapters 2–5 established. Only the competency count inside that same disclosure is wrong (see FAIL).
- **Tag hygiene: 162 tags across 25 distinct snapshots, zero dangling.** Every referenced snapshot exists in the cache. No claim in this chapter is unverifiable for want of a source file.