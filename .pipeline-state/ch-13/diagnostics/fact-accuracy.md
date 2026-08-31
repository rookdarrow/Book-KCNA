# Fact-Accuracy Audit — Chapter 13

**Mode detected: STANDARD.** The `Cached sources` section carries 26 populated snapshots, and the draft carries `[source:` tags on 88 lines (≈102 individual citation instances). Untagged factual claims are therefore FAIL, not advisory.

**Draft audited:** `draft-v1.md` (135,125 bytes, 1,533 lines). `draft-v2.md` was not available; line numbers below are against `draft-v1.md`.

**Tag resolution check:** all 20 distinct snapshot names cited by the draft exist in the supplied corpus. There are **no dangling tags**. Three bundled snapshots are never cited: `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31`, `k8s-docs-kubectl-overview-2026-08-23`, `k8s-docs-pod-security-admission-2026-08-31` — see WARN 14, because two of the FAILs below would be closed by citing them.

## Summary

- Total factual claims inspected: **147**
- Tagged claims verified: **94**
- Tagged claims unverifiable (source tag points to a snapshot truncated at exactly the needed passage): **5**
- **Untagged factual claims (FAIL): 17** (13 unsupported by any cached snapshot; 4 supported by a cached snapshot but missing the tag)
- **Contradicted claims (FAIL): 4**
- Minor discrepancies (WARN): **14**

The single highest-severity finding is **FAIL-U1**: `CreateContainerConfigError` appears in **13 places** including a Fixed Point, two graded items and the Chapter Summary, and **appears in no cached snapshot in this corpus**. The next is **FAIL-C1**: the chapter's kernel-versus-kubelet "two enforcers" discrimination — an Exam Alert item — is contradicted by the one snapshot that attributes the kill.

---

## FAIL — Untagged factual claims

### Group A — untagged AND unsupported by any cached snapshot (research gaps)

### FAIL-U1. Lines 221, 282, 303–317, 327, 455, 504–506, 1192, 1219, 1258, 1308, 1336, 1413, 1498: `CreateContainerConfigError`

Representative excerpt, L307: *"If a referenced ConfigMap does not exist, or a referenced Secret does not exist, or a named key inside one of them is missing, the kubelet cannot finish assembling the container. It stops, and reports `CreateContainerConfigError`."*

And L282, inside a table the draft introduces as *"the `Waiting` reasons that matter for the never-started family, **from the documented reason table** [source: k8s-docs-pod-failure-signatures-2026-08-31]"*:

| `CreateContainerConfigError` | The container's configuration cannot be assembled. | A referenced ConfigMap or Secret |

**Why it's a factual claim:** it asserts the existence of a specific Kubernetes-emitted `Reason` string, its trigger conditions, and its position in the container start-up sequence.

**The problem:** searched all 26 snapshots — the string `CreateContainerConfigError` appears in **none** of them. The reason table in `k8s-docs-pod-failure-signatures-2026-08-31` lists fourteen reasons (`ContainerCreating`, `ImagePullBackOff`, `ImageInspectError`, `ErrImageNeverPull`, `ErrImagePull`, `ErrContainerStatusUnknown`, `PodInitializing`, `DockerDaemonNotAvailable`, `DockerContainerError`, `OOMKilled`, `ContainerCannotRun`, `TransitioningReason`, `DeadlineExceeded`, `ContainerWaitingReason`) and this is not one of them. The row at L282 is therefore presented as sourced *from a table it is not in* — see FAIL-C4.

**Blast radius:** the signature is one of the nine the ☀️ Zenith is built on (L1192), it carries a ★ Fixed Point (L327), and it is the correct answer to Bearings 1 Q1 (L455/L504) and Practice Q4 (L1308/L1413), and the diagnosis in Practice Q8 (L1336). It cannot be cut; it must be sourced.

**Fix:** open a research gap in the research-manifest for a snapshot that documents `CreateContainerConfigError`. The rendered kubernetes.io reason table does not carry it; the likely authoritative home is the kubelet source (`pkg/kubelet/kuberuntime`) or the ConfigMap/Secret consumption docs (`https://kubernetes.io/docs/concepts/configuration/configmap/`, "the kubelet reports an error if the ConfigMap doesn't exist"). Until a snapshot lands, every occurrence above is unsourced. Also unsourced and dependent on the same gap: L1441 *"Kubernetes does not validate that a referenced Secret exists at admission time."*

### FAIL-U2. Line 388: "The retention window is on the order of an hour by default, not days."

Repeated at L1507 (Chapter Summary): *"Retention is on the order of an hour."*

**Why it's a factual claim:** it states a default duration for an API-server flag.

**The problem:** the cited snapshot `k8s-apiserver-event-ttl-and-toleration-defaults-2026-08-31` is transcribed only as far as the `## --event-ttl` heading — the value row is absent. The chapter's own AUTHOR-REVIEW comment at L386 says: *"the default duration value is not in the cached text. Per outline Open Question 4, no number may be written from memory here. The prose below states the shape rather than a figure."* The prose below it then states a figure ("on the order of an hour... not days"). The guardrail names itself and is then breached in the next sentence.

**Fix:** either re-fetch `kube-apiserver.md` far enough to capture the `--event-ttl` row and cite it as a dated illustration, or cut to a genuinely shape-only formulation ("the window is bounded and short — read the flag on your own cluster rather than assuming"). Do not ship the current sentence.

### FAIL-U3. Line 967: "Kubernetes ships roughly three minor releases a year"

**Why it's a factual claim:** it states a vendor release cadence.

**The problem:** the sentence's tagged portion (`"release branches for the most recent three minor releases"` / `"approximately 1 year of patch support"`) is verbatim-correct against `k8s-version-skew-policy-2026-08-31`. The cadence clause preceding it is not: that snapshot says nothing about releases per year, and no other snapshot does either. The tag at the end of the sentence gives the cadence claim borrowed authority it does not have.

**Fix:** open a research gap for the Kubernetes release cadence (`https://kubernetes.io/releases/release/` — "Kubernetes Releases" / release-cycle page), or delete the clause. The argument in the paragraph survives without it.

### FAIL-U4. Line 1040: "`kubeadm`, `kind`, and bare self-hosted clusters generally do not."

**Why it's a factual claim:** it names three specific distributions/tools and asserts what each ships by default.

**The problem:** the tagged half of the sentence quotes `k8s-docs-resource-metrics-pipeline-2026-08-23` correctly — *"a cluster addon component (not deployed by default in all distributions)"* — which is exactly as far as the corpus goes. The per-distribution breakdown that follows, and *"Managed platforms often install it for you,"* are unsourced.

**Fix:** cut to the sourced formulation ("some distributions install it, many do not"), or open a research gap for the metrics-server project README, which states the installation requirement directly.

### FAIL-U5. Lines 374, 376, 378, 1329, 1431: `ProgressDeadlineExceeded`, and "Six different underlying causes"

L374: *"A Deployment that stalls reports `ProgressDeadlineExceeded`, a condition which says the rollout did not finish in time... **Six different underlying causes produce that identical condition.**"*

**Why it's a factual claim:** it names a Deployment condition string and then quantifies its causes.

**The problem:** no Deployment/rollout snapshot is in this chapter's corpus. The condition name, the `progressDeadlineSeconds` mechanism (L1433), and above all the count "six" are unsourced. A specific cardinality is the kind of claim a reader will carry into an exam.

**Fix:** open a research gap for `https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#failed-deployment`, which lists the documented causes; cite the count from it or drop the number and say "several." The worked example at L376 and Practice Q7 both depend on this.

### FAIL-U6. Lines 235, 528: admission refusal leaves no Pod object, and the refusal lands on the ReplicaSet

L235: *"If a Pod was rejected at admission, by Pod Security Admission, by a validating webhook, by a quota, **there is no Pod object to describe.** The API server refused the write."*
L237 (🪝 Snag): *"the reason is on the **ReplicaSet**, not on any Pod. `kubectl describe replicaset <name>` is where the refusal message is."*
L528 (Bearings 1 Q4 answer): same claim as the keyed correct answer.

**Why it's a factual claim:** it asserts API-server write semantics and the specific object on which a controller's create failure is recorded.

**The problem:** `k8s-docs-pod-security-admission-2026-08-31` is in the corpus and is never cited; even so, it documents the `enforce`/`audit`/`warn` modes, not the "no object is created" consequence. Validating webhooks and ResourceQuota have no snapshot at all. This is the top branch of the §2 signature map (L221) and the keyed answer to a graded item.

**Fix:** open a research gap for PSA enforcement outcomes and for ReplicaSet status conditions (`FailedCreate`). At minimum, cite `k8s-docs-pod-security-admission-2026-08-31` for the PSA half of the enumeration.

### FAIL-U7. Line 319: "Init containers run to completion, in order, before any app container starts"

**Why it's a factual claim:** it states init-container execution semantics.

**The problem:** `PodInitializing` itself is legitimately sourced (it is in the reason table in `k8s-docs-pod-failure-signatures-2026-08-31`), but the ordering-and-completion semantics are not in any snapshot.

**Fix:** open a research gap for `https://kubernetes.io/docs/concepts/workloads/pods/init-containers/`, or defer wholly to the existing Ch 5 §3 cross-bearing and state only what the reason table supports.

### FAIL-U8. Line 265: "A Pod that mounts a PVC cannot be scheduled until that claim binds"

**Why it's a factual claim:** it asserts a scheduling precondition.

**The problem:** no storage snapshot is in this chapter's corpus. This is presented as a named member of the `Pending` cause family.

**Fix:** open a research gap for `https://kubernetes.io/docs/concepts/storage/persistent-volumes/` (or the `WaitForFirstConsumer` binding-mode docs, which complicate the claim — a `WaitForFirstConsumer` PVC binds *because of* scheduling, not before it). Verify direction before re-asserting.

### FAIL-U9. Lines 124, 200, 305, 614, 1048, 1258, 1285: claims about what the KCNA exam favors

- L124: *"Failure signatures are the most likely troubleshooting material on the KCNA exam"* and *"which is the shape the exam actually favors"*
- L200: *"the one the exam reaches for most often"*
- L305: *"This one is a favorite on exams"*
- L614: *"and the exam knows it"*
- L1048: *"One scope note that the exam likes"*
- L1258: *"the discrimination the exam reaches for most"*
- L1285: *"which is the shape the exam favors"*

**Why it's a factual claim:** each asserts the content distribution or item style of a third-party certification exam.

**The problem:** `cncf-kcna-curriculum-pdf-2026-08-23` publishes competency names and four domain weights and nothing else. The chapter's own AUTHOR-REVIEW at L6 concedes this: *"CNCF publishes no sub-competency weights (B1 gap G33, B2 disclosure #1)."* The metadata disclaimer at L10 is scrupulous about the 28%; these seven sentences then make unhedged frequency and item-style claims that rest on nothing in the corpus.

**Fix:** no source can close this — CNCF publishes no item statistics. Convert each to an explicitly authored judgement ("in my experience," "this chapter treats it as high-value because…") in the same register as the L10 disclaimer, or cut. The disclaimer at L10 loses its force if the rest of the chapter asserts exam behavior freely.

### FAIL-U10. Lines 135, 368, 440: `kubectl events --for pod/<pod-name>`

**Why it's a factual claim:** it asserts the existence and flag surface of a `kubectl` subcommand, taught as a step in the chapter's spine mnemonic (S-P-C-E-L) and printed inside a figure.

**The problem:** the corpus's own manifest flags this. `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31` carries `closes_gap: "B1 gap G1 -- the kubectl command surface. Partial: see manifest Gaps, item 1 (**kubectl events is NOT covered**)."` The chapter then teaches it anyway, untagged. `k8s-docs-kubectl-overview-2026-08-23` lists twelve operations and `events` is not among them.

**Fix:** open a research gap for `https://kubernetes.io/docs/reference/kubectl/generated/kubectl_events/`. Note the `--for` selector syntax specifically — that is the part being taught.

### FAIL-U11. Lines 1287, 1397, 1400: invented scheduler event and predicate strings

L1287: *"`0/6 nodes are available: 6 node(s) had untolerated taint {workload: gpu}`"* — presented as literal `kubectl describe pod` output in a graded item.
L1400: *"A request-versus-capacity failure produces a different predicate message (`Insufficient cpu`, `Insufficient memory`)."*

**Why it's a factual claim:** these are reproduced as verbatim product output, and Q1's entire discrimination turns on the reader parsing the string.

**The problem:** no snapshot in the corpus contains any scheduler event text. `k8s-docs-debug-pods-2026-08-23` establishes that the scheduler writes such messages — *"there should be messages from the scheduler about why it can not schedule your pod"* — but never quotes one. The strings above are plausible reconstructions, not transcriptions.

**Fix:** open a research gap for scheduler event message formats, or restate the question so the event is paraphrased rather than quoted (*"a scheduler event reporting that all six nodes carried an untolerated taint"*), which preserves the graded discrimination without asserting a literal string.

### FAIL-U12. Line 1423: "CPU is throttled at its limit; memory is not."

**Why it's a factual claim:** it asserts differential enforcement behavior for two resource types, as a distractor explanation in a graded item.

**The problem:** unsourced. `k8s-docs-pod-qos-2026-08-24` says only *"Any Container exceeding a resource limit will be killed and restarted by the kubelet"* — which, read literally, applies to both resource types and does not distinguish them. Nothing in the corpus documents CPU throttling.

**Fix:** open a research gap for `https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/` ("CPU is a compressible resource"), or delete the sentence — distractor D can be dismissed on the sourced grounds already given.

### FAIL-U13. Line 1046: an HPA "will report unknown metrics"

**Why it's a factual claim:** it asserts a specific observable HPA status output on a cluster without metrics-server. Repeated as the keyed answer C in Bearings 3 Q3 (L1085-ish, "reports unknown metrics").

**The problem:** the dependency itself is properly sourced (`k8s-docs-resource-metrics-pipeline-2026-08-31`: *"The HorizontalPodAutoscaler (HPA) and VerticalPodAutoscaler (VPA) use data from the metrics API"*). What the HPA object *displays* when the API is absent is not.

**Fix:** open a research gap for the HPA docs, or soften to the sourced form: the HPA is created, its metric source is absent, and it does not scale.

### Group B — untagged but supported by a snapshot already in the corpus (add the tag)

### FAIL-U14. Line 1066: "a node-level logging agent, typically run as a DaemonSet so that exactly one lands on each node"

**Fix:** tag it. `k8s-docs-logging-architecture-2026-08-23` says: *"Use a node-level logging agent that runs on every node (typically a DaemonSet) and pushes logs to a backend."* Note the snapshot supports "runs on every node," not "exactly one lands on each node" — adopt the source's phrasing. This also respects the `ledger_guardrail` (one clause plus a pointer, Ch 18 §6 owns it).

### FAIL-U15. Line 72 (Soundings, answer 1): "The five Pod phases are `Pending`, `Running`, `Succeeded`, `Failed`, `Unknown`"

**Fix:** tag `[source: k8s-docs-pod-failure-signatures-2026-08-31]`, which carries the full phase table verbatim.

### FAIL-U16. Line 84 (Soundings, answer 7): "Without `-c`, the command has to guess, and on a multi-container Pod it will refuse or pick the first container"

**Fix:** the `-c` requirement is sourced — `k8s-docs-logging-architecture-2026-08-23`: *"for a multi-container Pod use `-c <container>`"* — so tag that. The *behavior when omitted* ("refuse or pick the first") is not in any snapshot and the hedge conceals a likely inaccuracy: modern `kubectl` defaults to the first container and prints a `Defaulted container` notice rather than refusing. Cut the "refuse" branch or source it.

### FAIL-U17. Line 86 (Soundings, answer 8) and L1005-ish (§7): the Ingress object is created and inert

**Fix:** this is a Ch 10 retrieval item and Ch 10's snapshot set is not bundled here, so no tag in this corpus closes it. Either re-inject the Ingress-controller snapshot into this chapter's source set, or restate as an explicit callback to Ch 10 §3 rather than a fresh assertion.

---

## FAIL — Contradicted claims

### FAIL-C1. Lines 624, 643, 651, 875, 1262, 1419, and Chapter Summary L1516: the kernel as the OOM killer

**Tag:** `[source: k8s-docs-pod-qos-2026-08-24]` (L875, L1419)

**Snapshot says:** *"Any Container exceeding a resource limit will be **killed and restarted by the kubelet** without affecting other Containers in that Pod."*

**Draft says:**
- L643: *"The **kernel's cgroup enforcement kills the process**; the kubelet observes a terminated container with reason `OOMKilled`."*
- L624 (figure): *"Kernel cgroup enforcement kills / that one process"*
- L651: *"It is a kernel concept, not a Kubernetes one; Kubernetes is only reporting what the kernel did."*
- L1262 (Exam Alert item 3): *"Different killer (**kernel cgroup enforcement versus the kubelet**)"*
- L1419 (Practice Q5 answer): *"Exceeding a memory *limit* is kernel cgroup enforcement"* — immediately followed by the pod-qos quote that says the kubelet does it.
- L1516 (Chapter Summary): *"**Kernel killed it.**"*

The word `kernel` and the word `cgroup` appear in **zero** of the 26 snapshots. The only sourced statement of agency attributes the kill to the kubelet, and L1419 places the contradiction inside a single sentence: the draft asserts kernel enforcement and then quotes the source saying kubelet.

This matters more than an attribution nicety because the chapter builds a graded discrimination on it. The ⚠ Navigational Hazards at L667 teaches *"Two mechanisms. **Two enforcers, the kernel and the kubelet.**"* and Exam Alert item 3 promotes it to a high-priority topic. If a reader is examined on "who kills an over-limit container," the sourced answer and the taught answer differ.

**Recommended fix:** the draft's claim is defensible in practice, but nothing in this corpus supports it, and one snapshot opposes it. Either (a) open a research gap for `https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#how-pods-with-resource-limits-are-run` or the OOM-kill behavior docs and re-source the whole discrimination, or (b) rebuild the OOMKilled/Evicted contrast on the axes the corpus *does* support — **scope** (one container vs. the whole Pod) and **trigger** (this Pod's own limit vs. the node's pressure) — and drop "killer" as an axis. Option (b) is the safe ship; it loses one of four axes in the L621 figure and one clause in the Exam Alert, and costs the chapter nothing else.

### FAIL-C2. Line 1264 (Exam Alert item 4): "no cluster ships one by default"

**Tag:** the claim is untagged here; the §7 body it summarizes is tagged `[source: k8s-docs-resource-metrics-pipeline-2026-08-23]`.

**Snapshot says:** metrics-server *"is a cluster addon component (**not deployed by default in all distributions**)."*

**Draft says:** *"**`kubectl top` requires metrics-server, and no cluster ships one by default.**"*

"Not deployed by default in all distributions" means *some distributions do deploy it*. "No cluster ships one" is the universal negation of that. The draft contradicts itself as well: L1040 says *"Managed platforms often install it for you."* An Exam Alert is the highest-recall surface in the chapter, and this is the version a reader memorizes.

**Recommended fix:** rewrite L1264 as *"`kubectl top` requires metrics-server, which many distributions do not install by default."* The ★ Fixed Point at L1043 has the same problem in milder form (*"an addon that a stock cluster does not have"*) — align both to the source.

### FAIL-C3. Line 991: "A stock Kubernetes cluster collects no usage metrics at all"

**Tag:** untagged at L991; the paragraph it opens is sourced from `k8s-docs-resource-metrics-pipeline-2026-08-31` fourteen lines later.

**Snapshot says:** *"**cAdvisor**: Daemon for collecting, aggregating and exposing container metrics **included in Kubelet**."* and *"**kubelet**: Node agent for managing container resources. Resource metrics are accessible using the `/metrics/resource` and `/stats` kubelet API endpoints."*

**Draft says:** *"**A stock Kubernetes cluster collects no usage metrics at all**, because the component that would collect them is not installed."*

Per the snapshot the collection happens — cAdvisor is inside the kubelet binary on every node, and the kubelet already exposes the results. What is missing is the *aggregator and API extension*. The draft's own figure caption at L1038 gets this exactly right (*"The measurements exist; nothing is publishing them"*) and its §7 walk-up says cAdvisor is *"part of the kubelet binary, on every node, always. Nobody installs it."* The thesis sentence contradicts both.

**Recommended fix:** *"A stock Kubernetes cluster **publishes** no usage metrics at all — the measurements are being taken on every node, and nothing is aggregating them into an API you can query."* One word, and the section's own argument gets stronger.

### FAIL-C4. Lines 1130–1141 (Bearings 3, answer 2): the answer key is labelled C and concludes B

**Tag:** `[source: k8s-version-skew-policy-2026-08-31]`

**Snapshot says:** *"`kube-apiserver` is at **1.37**; `kubelet` is supported at **1.37**, **1.36**, **1.35**, and **1.34**"*

**Draft says:** the answer opens **"2. C."** (L1130), then at L1134 *"Wait — that example lists 1.34 as the oldest, not 1.33"*, then at L1136 *"So the correct answer is **B**, not C,"* then keys the option list to B.

The answer label and the answer disagree. Option C as written (*"Supported — the kubelet may be up to three minor versions older, and 1.33 is three behind"*) asserts that 1.33 is three minors behind 1.37, which the snapshot's own example refutes: three behind 1.37 is 1.34.

The AUTHOR-REVIEW at L1143 already routes this to the revision stage as a *house-form* problem. It is more than that: as it stands the item is a **wrong answer key**, and a reader who checks only the bolded letter learns the off-by-one error the question exists to trap.

**Recommended fix:** relabel the answer **B**, delete L1134 and L1136 entirely, and fold the arithmetic into B's explanation: *"Three minor versions older than 1.37 is 1.34, which the documented example confirms. 1.33 is four behind and outside the window."* Then reword option C so it no longer states the arithmetic that the key must refute — e.g. *"Supported — 1.33 is within the three-version window."* The underlying fact and citation are correct; only the key and the option wording need work.

---

## WARN — Minor discrepancies

1. **L643 — "documented in the container-state reason table"** (`k8s-docs-pod-failure-signatures-2026-08-31`). The quote *"The container ran out of memory"* is verbatim, but the snapshot places `OOMKilled` in the **`Waiting` Reason** table. The draft frames it as a **`Terminated`** reason (*"the kubelet observes a terminated container with reason `OOMKilled`"*; Bearings 2 Q1 at L847 says *"last state shows `Terminated` with `Reason: OOMKilled`"*). Practically true; not what the cited table says. Either soften the framing or source the `Terminated`-state placement separately.

2. **L629 (figure) — "Reason: Evicted"** as a paired reason string. `k8s-docs-node-pressure-eviction-2026-08-31` documents the *phase* (*"the kubelet sets the phase for the selected pods to `Failed`"*) but no `Reason: Evicted` string, and it is absent from the reason table. Repeated in Practice Q5 distractor A (L1317). Low risk, but it is printed as literal API content.

3. **L805–806 — `crictl ps` / `crictl logs <id>`.** `k8s-docs-crictl-2026-08-31` declares `crictl-ps` and `crictl-logs` in its `concepts_covered`, but the transcription stops at the `/etc/crictl.yaml` configuration section — neither command appears in the verbatim body. Every other crictl claim in §5 is verbatim-clean; these two command forms and the gloss *"containers the runtime is actually running"* are not verifiable from the cached text. Classified unverifiable rather than FAIL because the snapshot's own frontmatter asserts coverage; re-transcribe the "General usage" command examples to close it.

4. **L386–388 — `--event-ttl`.** The tag legitimately supports *that the flag exists and governs event retention* (the snapshot title and heading say so); it supports nothing about the value. Unverifiable rather than contradicted. See FAIL-U2 for the value.

5. **L741 — "The kubelet is running and reporting a problem."** `k8s-docs-node-status-2026-08-24` supports the `Ready=False` semantics quoted alongside it, but does not identify the kubelet as the writer. `k8s-docs-node-controller-heartbeats-2026-08-31` supports it indirectly (*"Updates to the `.status` of a Node"* as a node heartbeat form). Add that second tag; the `False`-vs-`Unknown` discrimination at L747 is the section's exam payload and should rest on both.

6. **L1509 (Chapter Summary) — "implemented as a default 300-second toleration on `NoExecute` node taints."** Two facts are separately sourced: the node controller's 5-minute wait (`k8s-docs-node-controller-heartbeats-2026-08-31`) and the automatic `tolerationSeconds=300` on `not-ready`/`unreachable` (`k8s-docs-taints-tolerations-depth-2026-08-24`). No snapshot states that the former **is** the latter. The §5 body at L769 hedges appropriately (*"the same machinery from Chapter 7"*); the summary row hardens the inference into a mechanism. The heartbeats snapshot's own `closes_gap` note says *"It is taint-based"* — that is authored manifest metadata, not source text. Soften the summary row to match the body.

7. **L965 — "a peer of the other four sections."** `k8s-docs-troubleshooting-overview-2026-08-31` says the guide *"has four sections"* and lists them, then states the known-issues line separately. The source does not present it as a fifth peer section. Minor overstatement in service of a good point; rephrase to "the same page's closing instruction."

8. **L104 — "That instinct is right about a third of the time. The other two thirds..."** A statistic-shaped estimate with no source and no possible source. It reads as measured. Rephrase qualitatively ("sometimes right, and wrong in the three most common failure shapes — which the next three paragraphs walk through") so the chapter's opening is not its least defensible sentence.

9. **L407, L415, L1352, L1451 — `kubectl logs --all-containers`.** `-c` and `--previous` are both sourced (`k8s-docs-logging-architecture-2026-08-23`). `--all-containers` appears in no snapshot. It is also a graded distractor (Practice Q10 option A, dismissed at L1451). Low factual risk; add it to the kubectl-surface research gap in FAIL-U10.

10. **L341, L431, L435, L359, L462, L1298 — the `kubectl` output surface generally.** `kubectl config current-context`, `kubectl get pod -o wide`, and the semantics of the `RESTARTS`, `READY` and `STATUS` columns are all untagged. Individually minor; collectively they carry the ⚓ Worth Securing at L359 (*"The restart count... is a diagnosis all by itself"*), the Practice Q2 correct answer (L1298) and the §3 triage figure. **Root cause:** the one snapshot bundled to cover this — `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31` — is transcribed only as far as its first heading (`## Interacting with running Pods`) and contains no command lines at all, despite `closes_gap: "B1 gap G1 -- the kubectl command surface."` **Re-transcribing that one snapshot would close items 9, 10 and much of FAIL-U10 at once**; it is the highest-leverage single fetch in this audit.

11. **L647 — "If a container is OOM-killed repeatedly, you will see it as `CrashLoopBackOff`."** A sound inference from two sourced facts (restart-on-limit-exceeded; backoff on repeated restarts), but stated as observed behavior. Acceptable as authored synthesis; flagged so the revision stage marks it as reasoning rather than citation.

12. **L661 — "API-initiated eviction, the mechanism behind `kubectl drain`."** `k8s-docs-node-pressure-eviction-2026-08-31` establishes that the two eviction kinds differ (*"Node-pressure eviction is not the same as API-initiated eviction"*) but never connects API-initiated eviction to `drain`. `k8s-docs-node-status-2026-08-24` covers cordon, not drain. The distinction the Closer Look draws is sourced; the `drain` attribution is not.

13. **L815 — "`journalctl -u kubelet` on a systemd host."** Unsourced. Low risk (generic Linux, and the draft explicitly marks it as past KCNA scope), but it is a concrete command presented as the next diagnostic step.

14. **Coverage note — three bundled snapshots are never cited.** `k8s-docs-kubectl-overview-2026-08-23` (would support the `kubectl` syntax and operations claims in §3), `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31` (truncated — see item 10), and `k8s-docs-pod-security-admission-2026-08-31` (would partially support FAIL-U6's PSA clause at L235). Two FAILs and one WARN above are cheaper to close than they look.

---

## PASS — Verified claims

Sampled across all sections; each checked word-for-word against the named snapshot.

| Line | Claim | Snapshot | Result |
|---|---|---|---|
| 4 | Container Orchestration published weight 28% | `cncf-kcna-curriculum-pdf-2026-08-23` | ✅ *"28% – Container Orchestration: Networking; Security; Troubleshooting; Storage."* The L10 disclaimer correctly declines to sub-divide it. |
| 76 | No tag → `:latest` → default policy `Always`; kubelet queries the registry each launch | `k8s-docs-images-2026-08-23` | ✅ all three parts verbatim |
| 78 | Two-container spec → `Burstable` | `k8s-docs-pod-qos-2026-08-24` | ✅ correctly fails `Guaranteed` (B has no limits; A's limits ≠ requests) and passes `Burstable` |
| 82 | API server 1.37 → oldest supported kubelet 1.34 | `k8s-version-skew-policy-2026-08-31` | ✅ matches the documented example exactly |
| 149, 151 | The two-audience split, both guides quoted | `k8s-docs-debug-pods-2026-08-31`, `k8s-docs-debug-cluster-2026-08-31` | ✅ both verbatim |
| 245, 247, 263 | `Pending` = not schedulable; read the scheduler's messages; capacity and `hostPort` causes | `k8s-docs-debug-pods-2026-08-23` | ✅ four quotations, all verbatim |
| 276–281 | `Waiting` reason rows: `ContainerCreating`, `ErrImagePull`, `ImagePullBackOff`, `ImageInspectError`, `ErrImageNeverPull`, `PodInitializing` | `k8s-docs-pod-failure-signatures-2026-08-31` | ✅ six of seven rows verbatim (the seventh is FAIL-U1) |
| 289 | `ImagePullBackOff` retry cap: *"compiled-in limit of 300 seconds (5 minutes)"* | `k8s-docs-images-2026-08-23` | ✅ verbatim |
| 291 | Cause list and the three-check sequence | `k8s-docs-images-2026-08-23`, `k8s-docs-debug-pods-2026-08-23` | ✅ verbatim |
| 299 | `Always` resolves to a digest and reuses the local cache if it matches | `k8s-docs-images-2026-08-23` | ✅ verbatim |
| 333 | `kubectl` setup/version check as first move | `k8s-docs-troubleshoot-kubectl-2026-08-31` | ✅ verbatim, and stays inside the snapshot's `partial_note` boundary |
| 349, 357 | *"The first step in debugging a Pod is taking a look at it"*; *"Are they all Running? Have there been recent restarts?"* | `k8s-docs-debug-pods-2026-08-31/-23` | ✅ verbatim |
| 411, 419, 421 | `-c` for multi-container; `--previous` reads a previous instantiation; kubelet keeps **one** terminated container | `k8s-docs-logging-architecture-2026-08-23` | ✅ all verbatim; the ★ Fixed Point at L417 is fully supported |
| 592 | The four-step restart sequence (initial crash → backoff → CrashLoopBackOff → reset) | `k8s-docs-container-restart-backoff-2026-08-31` | ✅ verbatim block quote |
| 599 | Backoff curve 10s/20s/40s, capped at 300s, **reset after 10 minutes** | `k8s-docs-container-restart-backoff-2026-08-31` | ✅ verbatim — and correctly takes **10 minutes**, honoring the snapshot's `conflict_note` that rejects the rendered page's "5 minutes" as a transcription error. Consistent at L1500 in the Chapter Summary. Good catch by the drafting stage. |
| 605 | Causes: *"application errors, configuration errors, resource constraints, failing health checks, or probe failures"* | `k8s-docs-container-restart-backoff-2026-08-31` | ✅ verbatim |
| 611 | Default `restartPolicy` is `Always`; exit 0 under `Always` still restarts | `k8s-docs-container-restart-backoff-2026-08-31` | ✅ supported by both the prose and the exit-code table |
| 655–665 | Node-pressure eviction: definition, monitored resources, phase `Failed`, controller replacement, self-healing, PDB/grace-period non-respect, API-initiated distinction | `k8s-docs-node-pressure-eviction-2026-08-31` | ✅ seven quotations, all verbatim |
| 673, 677 | Eviction order BestEffort → Burstable → Guaranteed; *"only Pods exceeding resource requests are candidates"* | `k8s-docs-pod-qos-2026-08-24` | ✅ verbatim; the ⚠ Hazards at L679 and 🪝 Snag at L687 both rest on it correctly |
| 695, 701 | Liveness failure → kill + restart policy; readiness failure → endpoints controller removes the Pod IP | `k8s-docs-pod-lifecycle-2026-08-23` | ✅ verbatim; the ★ Fixed Point at L705 is fully supported |
| 737–745 | Node-condition table, all six rows | `k8s-docs-node-status-2026-08-24` | ✅ each row's meaning matches, including `Unknown` = *"not heard from the node in the last `node-monitor-grace-period`"*. The chapter correctly declines to restate the 50-second default (sec.5 guardrail). |
| 755–777 | Two heartbeat forms; node controller sets `Ready=Unknown`; 5-minute wait; `NoExecute` taints for node problems; automatic `tolerationSeconds=300`; eviction rate limits; all-zones-unhealthy stand-down | `k8s-docs-node-controller-heartbeats-2026-08-31`, `k8s-docs-taints-tolerations-depth-2026-08-24` | ✅ all verbatim |
| 779, 781 | Node death → Pods marked for deletion after a timeout; a UID is never rescheduled | `k8s-docs-pod-failure-signatures-2026-08-31` | ✅ verbatim |
| 799–819 | `crictl` definition, stable since v1.11, Linux + CRI requirement, endpoint configuration and the known-endpoints performance note | `k8s-docs-crictl-2026-08-31` | ✅ five quotations, all verbatim (command forms excepted — WARN 3) |
| 947–961 | Skew: kubectl ±1 minor; kubelet ≤3 older, never newer; the persistently-3-behind upgrade block; `kubectl version` / runtime version in a bug report | `k8s-version-skew-policy-2026-08-31`, `k8s-docs-troubleshooting-overview-2026-08-31` | ✅ verbatim |
| 965 | *"You should also check the known issues for the release you're using."* | `k8s-docs-troubleshooting-overview-2026-08-31` | ✅ verbatim, and the GitHub-releases pointer matches the snapshot's link note |
| 1022–1032 | cAdvisor / kubelet / metrics-server / Metrics API definitions | `k8s-docs-resource-metrics-pipeline-2026-08-31` | ✅ four definitions, all verbatim; the figure at L1005 matches the snapshot's stated flow |
| 1046, 1048 | HPA and VPA consume the Metrics API; metrics-server is *"meant only for autoscaling purposes"* | `k8s-docs-resource-metrics-pipeline-2026-08-31/-23` | ✅ verbatim |
| 1056–1064 | `kubectl logs` routed to the kubelet reading a file; only the latest file; `containerLogMaxSize` 10Mi / `containerLogMaxFiles` 5; evicted Pod's logs go with it; Kubernetes provides no native log storage | `k8s-docs-logging-architecture-2026-08-23/-31` | ✅ five quotations, all verbatim. The ⚠ Hazards at L1068 is fully supported. |
| 1414, 1455, 1459 | Practice Q4/Q11/Q13 answer keys | as tagged | ✅ each key matches its snapshot (Q4's *cause* depends on FAIL-U1; its *reasoning* is sound) |

**Overall:** the tagged half of this chapter is unusually clean — 94 of 99 tagged claims verify verbatim, no tag points at a missing snapshot, and the drafting stage correctly resolved the one documented source conflict (the 10-minute backoff reset). The failures cluster in exactly the two places the outline predicted they would: material the corpus does not cover (`CreateContainerConfigError`, the kubectl command surface, Deployment rollout conditions, admission-refusal semantics) and material the outline barred from memory that got written from memory anyway (the `--event-ttl` default). Closing FAIL-U1 and re-transcribing the kubectl cheatsheet snapshot would resolve roughly half of everything above.