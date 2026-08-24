# Fact-Accuracy Audit — Chapter 3

**Mode detected: STANDARD.** The `sources/` directory contains 87 snapshots and the draft carries 88 inline `[source: ...]` tags. Untagged factual claims are therefore FAIL, not advisory.

**Input actually audited:** `.pipeline-state/ch-03/draft-v1.md` (1078 lines, post-voice). The stage prompt's `draft-v2.md` and `draft-voice.md` both resolve to `[file not available]` — neither exists for ch-03. `draft-v1.md` is the current head of the chapter (voice stage wrote it at 03:24, preserving `draft-v1-prevoice.md`). All line numbers below refer to `draft-v1.md`.

## Summary

- Total factual claims inspected: 109
- Tagged claims verified: 84
- Tagged claims unverifiable (source tag points to missing/empty snapshot): 0 — all 7 snapshots the draft cites are present in the cache
- **Untagged factual claims (FAIL): 11**
- **Contradicted / mis-cited claims (FAIL): 4**
- Minor discrepancies (WARN): 10

Tag distribution: `k8s-docs-cluster-architecture` ×36, `k8s-docs-controllers` ×17, `k8s-docs-overview` ×16, `k8s-docs-components` ×9, `k8s-history-ten-years` ×8, `k8s-docs-containers` ×1, `cncf-who-we-are` ×1.

---

## ⛔ BLOCKING PIPELINE NOTE — read before acting on findings 3, 4, 8, 10

**The Chapter 3 research pass fetched five new snapshots that never reached `sources/`.**

`.pipeline-state/ch-03/research-manifest.md` (written 03:12, *before* the drafting stage ran at 03:12–03:18) emits five new snapshots in harvest format:

| Manifest ref | Filename it declares | In `sources/`? |
|---|---|---|
| A1 | `k8s-docs-control-plane-node-communication-2026-08-24.md` | **NO** |
| A2 | `k8s-docs-cluster-addons-2026-08-24.md` | **NO** |
| A3 | `k8s-docs-etcd-access-control-2026-08-24.md` | **NO** |
| A4 | `k8s-docs-dns-cluster-addon-2026-08-24.md` | **NO** |
| A5 | `etcd-io-what-is-etcd-2026-08-24.md` | **NO** |

`ls sources/` returns 87 files, **all dated `-2026-08-23`, zero dated `-2026-08-24`**. `harvest_research_snapshots()` did not extract them. Consequently the draft cites zero 08-24 snapshots, and the manifest's three explicit drafting instructions (Gaps G-A, G-C; Notes for the author #1, #2) were not applied.

Two downstream consequences the revision stage must handle:

1. The `AUTHOR-REVIEW` at line 490 says *"Stage 2 must fetch kubernetes.io/docs/concepts/architecture/control-plane-node-communication/"*. **Stage 2 did fetch it.** The comment is stale; the material exists in the manifest but not in the cache.
2. Per this audit's rules ("trust only the cached snapshots"), every claim resting on A1/A3/A4 is scored **unverifiable-in-cache** below, not "correct." Re-running harvest (or hand-writing the five files from the manifest's fenced blocks) converts most of them to PASS without a re-fetch.

---

## FAIL — Untagged factual claims

### Line 262: "etcd is the only stateful component in the cluster. Every other component can be killed, restarted, replaced, or scaled out, and the cluster carries on."

**Why it's a factual claim:** An architectural exclusivity assertion about component statefulness. No cached snapshot states it. `k8s-docs-cluster-architecture-2026-08-23` says only *"Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data."* The claim is also loosely false as written — the kubelet maintains local state and the container runtime maintains an image cache on node disk, which the same snapshot set describes elsewhere (`k8s-docs-images-2026-08-23`: kubelet "has a container image with that exact digest cached locally").
**Recurrence:** Chapter Summary line 1051 — "**The only stateful component.**"
**Fix:** Narrow to what is sourced — *etcd is the cluster's backing store; every other component's state can be reconstructed from it* — or reframe as an explicit author gloss. Do not present as documented fact. Both instances must move together.

### Line 488 (figure caption), 496, 577, 584, 1060: "only the API server reaches etcd" / "None of them has a private channel to another component"

**Why it's a factual claim:** A load-bearing architectural invariant, asserted five times, driving `ch03-fig04`, Bearings #2 Q4, and §7's Zenith. Untagged in every instance.
**Cache status:** Unverifiable. The supporting snapshot (A3) was not harvested.
**What the manifest actually found (Notes for the author #1) — and this changes the wording:**
- *"Components do not talk to each other directly"* — **strongly sourced.** A1 gives the quotable sentences: *"Kubernetes has a 'hub-and-spoke' API pattern. All API usage from nodes (or the pods they run) terminates at the API server. None of the other control plane components are designed to expose remote services."* §5 may state this flatly once A1 is in the cache.
- *"Only the API server talks to etcd"* — **sourced as a recommendation, not an invariant.** A3's exact sentence is *"Access to etcd is equivalent to root permission in the cluster so ideally only the API server should have access to it."* The word is *ideally*.

**Fix:** Harvest A1 and A3, then tag the first half to A1 and rewrite the second half from an absolute to the manifest's recommended framing — *the API server is the component that reads and writes etcd, and anything else with etcd access holds root-equivalent power.* All five instances, including the Chapter Summary row at line 1060 and the Bearings #2 Q4 distractor rationale at line 577, must be revised in step.

### Line 430: "three items in that set of twelve are marked optional in the documentation"

**Why it's a factual claim:** An assertion about what the cited authority explicitly marks, plus an arithmetic claim. Both are wrong.
**What the snapshot marks:** `k8s-docs-components-2026-08-23` prints "(optional)" on exactly two entries — `cloud-controller-manager` and `kube-proxy`. Addons are described as *"extend the functionality of Kubernetes"*; the word "optional" is never applied to them. The set of twelve is 8 components + 4 addons; "Addons" collapsed to a single item is not a member of that set, so "three of twelve" does not parse either.
**Internal contradiction:** Practice Q13 answer (line 1008) states correctly — *"kube-proxy and cloud-controller-manager are the two marked optional."* The chapter contradicts itself.
**Fix:** Rewrite to *"two of those twelve are marked optional in the documentation; a third kind of optionality — the addons as a class — is the book's own framing."* This preserves §4's three-reasons structure while keeping the ⚠ block's own advice at line 444 ("read the word 'optional' when the documentation prints it") honest.

### Line 500: "a tool called Argo CD sits outside the cluster watching a Git repository"

**Why it's a factual claim:** A statement about where a third-party CNCF project runs.
**In tension with cache:** `argocd-overview-2026-08-23` states *"Argo CD is implemented as a Kubernetes controller which continuously monitors running applications and compares the current, live state against the desired target state (as specified in the Git repo)."* Argo CD runs **in** the cluster; the **Git repository** is what sits outside.
**Fix:** *"…when a controller called Argo CD watches a Git repository that sits outside the cluster."* Tag to `argocd-overview-2026-08-23`. This forward reference will be re-read in Chapter 15; leaving it inverted plants an error the reconcile pass will have to unpick.

### Line 271: "the scheduler selects a node and records that choice. It does not start anything."

**Why it's a factual claim:** A component-boundary assertion that the chapter treats as high-value (it is the basis of Bearings #1 Q5, Bearings #2 Q4, and the Common Traps entry at line 812).
**Fix:** Tag to `k8s-docs-kube-scheduler-2026-08-23`, which states it directly: *"The scheduler then notifies the API server about this decision in a process called binding."* Note that this snapshot is cached, is named in the research manifest's own snapshot table as covering "kube-scheduler binding boundary," and **is cited nowhere in the draft.** Free precision.

### Line 773: "A kubelet whose control plane is unreachable doesn't sit waiting for orders. It keeps the containers it already knows about running"

**Why it's a factual claim:** A specific behavioral assertion about kubelet operation during a control-plane partition. It is the evidence for §7's "what this buys" argument.
**Cache status:** Unsupported. `k8s-docs-nodes-2026-08-23` covers only the control-plane side of an unreachable node (*"updating the Ready condition to Unknown when a node becomes unreachable, and triggering API-initiated eviction"*). No cached snapshot describes kubelet behavior when the API server is unreachable.
**Fix:** Either open a research gap for `kubernetes.io/docs/concepts/architecture/nodes/` node-lifecycle or the kubelet reference, or reframe as a consequence of the sourced claim rather than an observed behavior: the kubelet's job is a standing comparison against the PodSpecs it holds, not an instruction queue.

### Line 96: "CNCF publishes weights per domain, not per competency"

**Why it's a factual claim:** An assertion about the vendor's publication practice, and the load-bearing justification for the chapter's `~6%` disclosure at line 4.
**Fix:** Tag to `cncf-kcna-curriculum-pdf-2026-08-23` and/or `lf-kcna-exam-page-2026-08-23` — both publish four weighted domains (44/28/16/12) with competency *names* only and no sub-percentages. The research manifest confirms this at its Note #6 ("Open question #6 confirmed as a genuine, permanent gap"). The claim is correct; it just needs the tag. The `~6%` figure itself is properly disclosed as an authored estimate at lines 4 and 96 and is **not** a finding.

### Line 34–35 (epigraph): "Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration." — the Kubernetes documentation

**Why it's a factual claim:** A verbatim quotation attributed to a named authority, with no tag.
**Content verified:** matches `k8s-docs-overview-2026-08-23` exactly.
**Fix:** Add `[source: k8s-docs-overview-2026-08-23]`. Trivial, but the chapter tags this same sentence at lines 190, 759, 763, and 810 — the epigraph is the lone untagged instance.

### Line 321: "It's a separate project, swappable, and it existed before Kubernetes wanted it."

**Why it's a factual claim:** A dated priority claim about the container runtime relative to Kubernetes.
**Problem:** The referent is ambiguous and, on the reading the surrounding sentence invites (containerd, CRI-O — both named two sentences earlier), it is false. Both projects postdate Kubernetes' 2014 first commit, which the chapter itself dates at line 198. Container runtime *technology* predates Kubernetes (`k8s-history-ten-years-2026-08-23` dates Docker's introduction to March 2013), but that is not what the sentence says.
**Fix:** *"It's a separate project, swappable, and not authored by the Kubernetes project."* The architectural point — Kubernetes defines an interface rather than reimplementing — survives without the dating claim.

### Line 448: "In practice almost every real cluster has it" (cluster DNS)

**Why it's a factual claim:** An empirical deployment-prevalence claim. Already carries an `AUTHOR-REVIEW` at line 450 acknowledging it is unsourced — **the acknowledgement does not discharge it.**
**Recurrence:** Line 570 — *"Cluster DNS in particular is present in essentially every working cluster."*
**Fix is already written and was not applied.** Research manifest Gap G-C harvested A4, which supplies the sourceable replacement: *"DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on."* Harvest A4, adopt the built-in/launched-automatically framing, and drop the prevalence claim. Then delete the stale AUTHOR-REVIEW.

### Line 260: "every component that reads from etcd through the API server gets the same answer as every other component"

**Why it's a factual claim:** A consistency-guarantee assertion presented as an unpacking of the documentation's word *"consistent."*
**Cache status:** Not sourceable. Research manifest Gap G-B checked `etcd.io/docs/v3.5/learning/why/` specifically for this and records **NOT PRESENT**: *"the recommended sentence 'every component reads the same answer'"* is explicitly listed as unsourceable.
**Fix:** Manifest's recommendation — write the gloss as plain-language explanation *clearly framed as explanation*, and cite A5 (`etcd-io-what-is-etcd-2026-08-24`) for *"strongly consistent."* The current paragraph opens with "Two words deserve unpacking," which is close, but the sentence itself reads as reported fact.

---

## FAIL — Contradicted / mis-cited claims

*Each entry below carries a `[source: ...]` tag whose snapshot does not contain the claim. Two are direct contradictions of the cited text; two attribute a claim to a snapshot that is silent on it.*

### Line 126: "they have relaxed isolation properties that let them share the operating system kernel among applications"

**Tag:** `[source: k8s-docs-overview-2026-08-23]`
**Snapshot says:** *"Containers are similar to VMs, but they have relaxed isolation properties to share the Operating System (OS) among the applications. Therefore, containers are considered lightweight."*
**Draft says:** "share the operating system **kernel** among applications"
**Severity: highest-priority finding in this audit.** The research manifest's Gap G-A addresses this claim by name and rules on it: *"The book's sharpening to 'kernel' is technically correct but is authorial precision, not documented fact. Chapter 3 §1 must therefore either quote 'Operating System (OS)' verbatim when citing, or make the sharpening visible as the book's own gloss. **It cannot be presented as what the documentation says.**"* The draft presents it as what the documentation says. G-A also records that a targeted search for a Kubernetes-authored sentence using "kernel" in this sense returned nothing.

**The AUTHOR-REVIEW at line 128 rests on a false premise — verified.** It asserts Chapter 1 sharpened to "kernel," instructs the reader to "Confirm Chapter 2 resolved the same way," and adopts "kernel" on that assumption. Actual state of the two shipped chapters:

- `chapter-01-taking-departure.md:142` — uses **"operating system kernel"**, and carries its own unresolved `AUTHOR-REVIEW` at line 140 flagging exactly this ("Accept the sharpening or soften to match the source").
- `chapter-02-cargo-in-standard-crates.md:279` — uses **"share the operating system among the applications"**, matching the snapshot. Reinforced at lines 1148 and 1263 ("share the OS among the applications").

**Chapter 2 resolved the opposite way.** The book is now 2–1 split on its most-quoted sentence, which is precisely the divergence line 128 predicted the reconcile pass would surface.
**Recommended fix:** Adopt Chapter 2's resolution — quote "operating system" when citing, and if the kernel-level precision is wanted, add it as a visibly authorial sentence with no tag attached. Then raise the divergence for Chapter 1 §Soundings A1, which is the remaining outlier. Do not resolve this chapter in isolation.

### Line 569 (Bearings #2 Q3 answer): "Addons extend the functionality of Kubernetes and are implemented using Kubernetes resources"

**Tag:** `[source: k8s-docs-components-2026-08-23]`
**Snapshot says, in full:** *"## Addons — extend the functionality of Kubernetes · **DNS** — For cluster-wide DNS resolution. · **Web UI (Dashboard)** — For cluster management via a web interface. · **Container Resource Monitoring** — For collecting and storing container metrics. · **Cluster-level Logging** — For saving container logs to a central log store."*
**Draft says:** "…and are implemented using Kubernetes resources"
**The snapshot contains no implementation detail at all.** The first half of the sentence is verbatim; the second half is attributed to a snapshot that never makes the claim. Answer option B at line 544 is worded the same way, so the *keyed correct answer* to Q3 currently rests on unsourced text.
**Recurrences:** Line 426 (untagged) — "They're cluster extensions, implemented using ordinary Kubernetes resources"; line 436 table row; line 571 — "Addons run as ordinary workloads and can land anywhere the cluster schedules them."
**Recommended fix:** Harvest A2 (`k8s-docs-cluster-addons-2026-08-24`), which is the correct source for addon material. Note A2 as transcribed in the manifest states *"Add-ons extend the functionality of Kubernetes"* and lists concrete addons — it still does not state "implemented using Kubernetes resources." Either locate that sentence or rewrite Q3's answer key and option B around what A2 does support. **Do not ship a keyed answer on an unsourced clause.**

### Line 399 (Bearings #1 Q5 answer): "it does so by talking to a CRI implementation such as containerd or CRI-O"

**Tag:** `[source: k8s-docs-cluster-architecture-2026-08-23]`
**Snapshot says (kubelet entry):** *"An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod."* Snapshot says (container runtime entry): *"Kubernetes supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI (Container Runtime Interface)."*
**Draft says:** the kubelet reaches the runtime *through CRI*.
**The cited snapshot never connects the two.** It names the kubelet and it names CRI, but the linkage — that CRI is the interface the kubelet speaks — is the reader's inference, and here it is the keyed answer to a `[retrieval: ch2]` item.
**Recommended fix:** Chapter 2 already solved this. `chapter-02-cargo-in-standard-crates.md:551` cites `k8s-docs-extending-kubernetes-2026-08-23` for the CRI parenthetical, and line 539 double-tags `k8s-docs-containers` + `k8s-docs-cluster-architecture`. Mirror that: add `[source: k8s-docs-extending-kubernetes-2026-08-23]` to line 399. Cached, zero re-fetch.

### Line 333 (Dead Reckoning block): single tag covering nine component descriptions

**Tag:** `[source: k8s-docs-components-2026-08-23]` (one tag, end of block)
**Snapshot says:** the components page gives one-line summaries only — e.g. *"kube-controller-manager — Runs controllers to implement Kubernetes API behavior"* and *"kube-proxy (optional) — Maintains network rules on nodes to implement Services."*
**Draft says:** "kube-controller-manager … runs controller processes **in a single binary**" and "kube-proxy runs on every node **unless something else does its job**."
**Both italicized details come from `k8s-docs-cluster-architecture-2026-08-23`, not from the tagged snapshot.** Dead Reckoning is the chapter's facts-only block; a reader auditing it against the cited page will not find two of its nine sentences.
**Recommended fix:** Add `[source: k8s-docs-cluster-architecture-2026-08-23]` alongside, exactly as the ★ Fixed Point at line 331 already does correctly.

---

## WARN — Minor discrepancies

1. **Line 204 (Closer Look):** *"Omega was its research successor, an attempt to rethink the architecture with lessons learned"* — tagged `k8s-history-ten-years-2026-08-23`, which says only *"the Borg system (and its research successor Omega)."* "Borg was the production system" is a fair inference from "research successor"; "an attempt to rethink the architecture with lessons learned" is not in the snapshot at all. Cut the second clause or mark it as the book's reading.

2. **Line 488 figure caption + `ch03-fig04` scope.** Research manifest Note #2 flags this as *"the most consequential finding in this pass"*: A1 documents two real control-plane→node paths the figure omits — API server→kubelet (pod logs, `kubectl attach`, port-forwarding) and API server→node/pod/service via proxy. The current caption's three enumerated absences (scheduler→kubelet, node↔node, non-apiserver→etcd) do not directly contradict this, but §5's broader "None of them has a private channel to another component" (line 496) does. Manifest recommendation: scope the figure and §5 explicitly to the **state/API path**, and add one sentence acknowledging the API server opens connections to kubelets for logs and exec, cross-beared to Ch 13. Chapter 13's debugging material will otherwise contradict this figure.

3. **Line 496:** *"the controller-manager running its dozen controllers"* — the snapshot says *"There are many different types of controllers"* and names four. "Dozen" asserts a count no source gives. Use "its many controllers."

4. **Line 246:** *"starting up a new Pod when a workload's replica count is unsatisfied"* — snapshot: *"starting up a new pod when a **Deployment's replicas field** is unsatisfied."* The generalization is defensible (Deployment is not introduced until Ch 6) but drifts from the cited wording. Consider "when a controller's declared replica count is unsatisfied."

5. **Lines 653 vs 1078 — self-quotation drift.** The Extended Analogy at line 653 reads *"a few dozen small corrections were made continuously."* The chapter's closing pull-quote at line 1078 quotes it back as *"a hundred small corrections."* A quotation should match its own source seventeen pages earlier. Pick one number.

6. **Line 305 / Practice Q9-B (line 993):** *"won't report it"* / *"there's no reporting path for containers the kubelet doesn't manage."* The snapshot supports only *"The kubelet doesn't manage containers which were not created by Kubernetes."* "Doesn't manage" is the sourced claim; "no reporting path exists" is a stronger, unsourced mechanism claim, and it is a keyed distractor rationale. Soften to what "doesn't manage" entails.

7. **Line 490 — stale AUTHOR-REVIEW.** Instructs Stage 2 to fetch `control-plane-node-communication`. Stage 2 fetched it (manifest A1). Once A1 is harvested, replace this comment with the tags; do not let it ship as a live blocking note.

8. **Line 128 — AUTHOR-REVIEW premise falsified.** See the line 126 finding: Chapter 2 resolved the opposite way (`chapter-02:279`). Rewrite or delete rather than carrying the instruction forward a fourth time.

9. **Chapter Summary (lines 1044–1064) carries zero source tags** across 19 rows. Most rows restate body claims that *are* tagged, so this is a formatting observation rather than a fresh error — with two exceptions that restate FAIL-level claims and must move when their body instances do: line 1051 ("The only stateful component") and line 1060 ("Only the API server reaches etcd").

10. **Line 397 (Bearings #1 Q4-D rationale):** *"image layers live in a registry and on node disks, not in etcd."* Untagged; loosely supported by `k8s-docs-images-2026-08-23` (push to a registry; kubelet caches locally). Low risk, but it is a keyed distractor rationale — tag it.

---

## PASS — Verified claims (sampled, for coverage evidence)

**§1 — deployment eras and capability lists (`k8s-docs-overview-2026-08-23`)**
- L122 traditional era: no resource boundaries, one-app-per-server solution, didn't scale, expensive — verbatim match.
- L124 virtualized era: multiple VMs on one physical CPU, isolation, "each VM is a full machine running all the components, including its own operating system" — verbatim match.
- L158–171 capability table: all **ten** published capabilities present and correctly paraphrased (service discovery, storage orchestration, rollouts/rollbacks, bin packing, self-healing, secret/config management, batch execution, horizontal scaling, IPv4/IPv6 dual-stack, extensibility).
- L177–186 "what Kubernetes is not": all six bullets match, including the PaaS framing and the Spark/MySQL/Ceph examples.
- L759 block quote — checked character-by-character against the snapshot's orchestration passage. **Exact**, minus the leading "Additionally,". Correctly reproduced at L763 and L802.

**§1 — origin (`k8s-history-ten-years-2026-08-23`)**
- L198: June 6th 2014, 250 files, 47,501 lines of Go/bash/markdown — exact.
- L200: Solomon Hykes, PyCon, March 2013, five-minute lightning talk, "The future of Linux Containers"; DockerCon June 2014; v1.0 July 2015; CNCF's first project — all exact.
- L202: Greek for helmsman or pilot; K8s numeronym, eight letters — exact.
- L200: "CNCF is part of the nonprofit Linux Foundation" `[cncf-who-we-are-2026-08-23]` — exact.

**§2–§3 — the component census (`k8s-docs-cluster-architecture-2026-08-23`, `k8s-docs-components-2026-08-23`)**
- L214 cluster shape, "at least one worker node," HA control plane — verbatim.
- L250 kube-apiserver front end + horizontal scaling; L516 restates it correctly.
- L258 etcd one-line role and the backup advisory — verbatim.
- L269 kube-scheduler description including the full factor list; Practice Q7 (L983) correctly enumerates it and correctly excludes node-name ordering.
- L277 kube-controller-manager, including all four named controllers (Node, Job, EndpointSlice, ServiceAccount) and the logically-separate/single-binary/single-process sentence. Reproduced correctly at L279, L390, L801, L809.
- L283 cloud-controller-manager, including the on-premises/laptop absence. Reproduced correctly at L435, L564, L808, L1013.
- L299 kubelet, including "doesn't manage containers which were not created by Kubernetes."
- L311 kube-proxy, including the full network-plugin optionality condition. Reproduced correctly at L434, L559, L807, L1013.
- L319 container runtime and the containerd/CRI-O/CRI list.
- L424 addon list: DNS, Web UI (Dashboard), Container Resource Monitoring, Cluster-level Logging — exact.
- L1008 (Practice Q13): "kube-proxy and cloud-controller-manager are the two marked optional" — **correct**, and the correct count.

**§6 — the control loop (`k8s-docs-controllers-2026-08-23`)** — the chapter's highest-value section is also its cleanest.
- L597 thermostat passage — verbatim.
- L601 "controllers are control loops that watch the state of your cluster…" — verbatim.
- L625 controller pattern, including "more commonly … send messages to the API server that have useful side effects."
- L629 Job controller: "does not run any Pods or containers itself," "tells the API server to create or remove Pods," "other components in the control plane act on the new information" — verbatim.
- L635 direct control, including the Node-provisioning example and desired-state-from-the-API-server detail.
- L639 Job marked Finished — verbatim.
- L661 never-stable-state passage — verbatim, and correctly restated in Bearings #3 Q4 (L726) and Summary L1063.

**Retrieval item**
- L1036 (Practice Q19, `[retrieval: ch2]`): immutability and rebuild-then-recreate `[k8s-docs-containers-2026-08-23]` — verbatim match, correctly tagged.

**Cross-chapter quotation**
- L194 quotes Chapter 1 as *"Kubernetes is an orchestrator — it decides what should run where."* Verified against `chapter-01-taking-departure.md:144` — **exact match.** The §1→§7 Snag/payoff structure is built on an accurate self-citation.