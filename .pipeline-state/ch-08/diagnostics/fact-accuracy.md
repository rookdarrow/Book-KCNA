# Fact-Accuracy Audit — Chapter 8

**Mode detected: STANDARD.** The draft carries `[source: ...]` tags throughout (84 tag instances), and the cached-source section is populated with 32 snapshots. Untagged factual claims are therefore FAIL, not advisory.

**Locator convention.** This audit ran against the assembled `draft-v2.md` text supplied to the stage, which does not carry stable line numbering through the harness. Every finding is anchored by section + subsection + a verbatim excerpt, which is greppable. Where the draft's own `AUTHOR-REVIEW` comments already sit on a claim, that is noted.

---

## Summary

- Total factual claims inspected: **188**
- Tagged claim instances verified: **84**
- Tagged claims unverifiable (tag points to a missing/empty snapshot): **0**
- **Untagged factual claims (FAIL): 43 instances across 14 entries**
- **Contradicted claims (FAIL): 2**
- Minor discrepancies (WARN): **11**

---

## ⚠ Corpus change since the last audit — read this first

**The snapshots the draft's `AUTHOR-REVIEW` comments describe as "landed but unwritten" are present in this chapter's referenced source set now.** Thirteen of the fourteen blocking or near-blocking gaps recorded in draft-v2's inline comments are closable by tagging, with **no new fetch required**. The comments themselves are now stale and several make claims that are false against the current corpus — e.g. the metadata-line comment asserting that "the string 'Kubernetes Fundamentals' appears in NO cached snapshot in this chapter's referenced set," and the §2 comment asserting that "`sources/` contains none of them." Both are wrong as of this pass. The revision stage should treat the inline comments as a to-do list, not as a description of the evidence.

Newly available in this chapter's set:

| Snapshot | Closes |
|---|---|
| `cncf-kcna-curriculum-pdf-2026-08-23`, `cncf-kcna-certification-page-2026-08-23` | metadata line: domain name, domain count, 44% |
| `k8s-docs-controlling-access-2026-08-24` | §2 gate ordering, mutation, persistence order, 401/403, reads bypass admission, RBAC as an authorization module |
| `k8s-docs-admission-controllers-2026-08-24` | ResourceQuota / LimitRanger / NodeRestriction as admission plugins |
| `k8s-docs-resource-quotas-2026-08-24`, `k8s-docs-limit-range-2026-08-24` | all of §3's scope, defaulting and rejection claims |
| `k8s-docs-node-status-2026-08-24` | Capacity vs Allocatable definitions; **`cordon` writes `.spec`**; `node-monitor-grace-period` default |
| `k8s-docs-reserve-compute-resources-2026-08-24` | why Capacity and Allocatable differ (the unpaid Chapter 7 promise) |
| `k8s-docs-taints-tolerations-2026-08-23` | `NoSchedule` effect semantics (Soundings A5, Bearings #2 item 1) |
| `k8s-docs-audit-2026-08-24` | what auditing records, and that it lives inside kube-apiserver |
| `k8s-docs-safely-drain-node-2026-08-24`, `k8s-docs-api-eviction-2026-08-24`, `k8s-docs-kubectl-cordon-2026-08-24` | drain/evict/uncordon corroboration |
| `k8s-docs-resource-management-2026-08-23` | "requests are what the scheduler filters on" (Practice Q7) |

**Only one gap in this chapter is genuinely unclosable from the cached corpus:** the managed-vs-self-hosted duty split (entry 3 below). Everything else is a tagging job.

---

## FAIL — Untagged factual claims

### 1. Metadata line — "Domain: Kubernetes Fundamentals — 44% of the exam" and "its four domains"

**Excerpt:** `**Domain: Kubernetes Fundamentals — 44% of the exam · Competency: Cluster Administration — ~5% (authored allocation)...**` and `CNCF publishes weights for its four domains and not for the competencies within them.`

**Why it's a factual claim:** three separate assertions of published vendor exam structure — a domain name, a domain count, and a weighting percentage. This is the most consequential category of claim a certification study guide makes.

**Instances:** 3.

**Fix:** All three are now verifiable and should be tagged to `[source: cncf-kcna-curriculum-pdf-2026-08-23]` (which carries "44% – Kubernetes Fundamentals" and enumerates exactly four domains: 44/28/16/12) and/or `[source: cncf-kcna-certification-page-2026-08-23]` (which carries the same four-domain weight line). Tag the **name, the count and the percentage**, not just the percentage. The "no per-competency weights" observation is supportable as a structural reading of the curriculum PDF — the domains carry percentages and the competencies inside them do not — but frame it as an observation about the published document rather than as a quoted claim, since no source sentence says it. Delete the stale `AUTHOR-REVIEW` comment above the line.

### 2. Soundings answer 5 — "`NoSchedule` governs new placements only"

**Excerpt:** `**Nothing.** \`NoSchedule\` governs new placements only, which raises an obvious follow-up question that §4 answers.`

**Why it's a factual claim:** states the runtime semantics of a documented taint effect.

**Instances:** 2 (this answer and Bearings #2 item 1's answer, which asserts the same semantics).

**Fix:** Tag both to `[source: k8s-docs-taints-tolerations-2026-08-23]`, which is now in this chapter's set and states verbatim: *"NoSchedule — no new Pods will be scheduled on the tainted node unless they have a matching toleration. Pods currently running on the node are not evicted."* The existing inline comment's diagnosis was correct (the reference list was the problem, not the prose); the reference list is now fixed.

### 3. Soundings answer 8 — the five-duty managed/self-hosted list

**Excerpt:** `**Common correct answers: patching and upgrades; backups; hardware replacement; capacity planning; certificate rotation.** Any two of these is a pass.`

**Why it's a factual claim:** enumerates which operational duties transfer to a commercial provider — an assertion about third-party vendor responsibility models.

**Instances:** 1 (plus the narrowed §5 paragraph and Practice Q13, both of which now depend on the same unsourced axis — see CONTRADICTED entry 2).

**Fix:** **This is the chapter's one genuine research gap.** `k8s-docs-setup-tooling-2026-08-23` licenses only the existence of a split ("consider which aspects of operating a Kubernetes cluster (or abstractions) you want to manage yourself and which you prefer to hand off to a provider"); it does not enumerate sides, and kubernetes.io does not document commercial providers' responsibility models, so no fetch from that tree closes it. Either **open a research gap in the research-manifest for a vendor-neutral shared-responsibility source**, or narrow the answer key to "any operational duty that moves when a provider runs the control plane; which ones move is a per-provider question." Do not ship the five-item list as an answer key.

### 4. §2 — the sequential-gate semantics (largest cluster)

**Excerpts:**
- `Admission controllers see a request that has already been authenticated and authorized, and act on it before it is written down.`
- `> ★ **Fixed Point:** Authentication, then authorization, then admission. ... it is the only one of the three that can change your request instead of refusing it.`
- Figure 8.2 caption: `Gates one and two have one way out other than forward: refusal. Gate three has two.`
- Bearings #1 A3 and A4; Practice Q2, Q3, Q4 keys; Exam Alert items 1 and 2; Chapter Summary rows "The three gates" and "Admission's distinction".

**Why it's a factual claim:** asserts (i) that a request passes three checks in a fixed order, (ii) that admission runs after authorization and before persistence, and (iii) that admission modules may mutate rather than only accept/reject. All three are checkable statements about API server behaviour.

**Instances:** 19.

**Fix:** Tag against `[source: k8s-docs-controlling-access-2026-08-24]`, which closes all three outright:
- ordering — *"When a request reaches the API, it goes through several stages"*, plus the snapshot's `[STRUCTURAL]` observation that the page presents Transport security → Authentication → Authorization → Admission control → Auditing as sequential sections. **Cite the structural observation; do not quote the stage order as a source sentence** — the snapshot marks it as not-quotable prose.
- persistence order — *"Once a request passes all admission controllers, it is validated using the validation routines for the corresponding API object, and then written to the object store."*
- mutation — *"Admission Control modules are software modules that can modify or reject requests"* and *"admission controllers can also set complex defaults for fields."*

Two free upgrades available from the same snapshot: the quorum contrast (*"if any module authorizes the request, then the request can proceed. If all of the modules deny the request, then the request is denied (HTTP status code 403)"* vs *"Unlike Authentication and Authorization modules, if any admission controller module rejects, the request is immediately rejected"*), and *"Admission controllers do not act on requests that merely read objects."*

### 5. §2 Navigational Hazards — "admission has no opinion about your identity"

**Excerpt:** `**Authorization has no opinion about the contents of your request; admission has no opinion about your identity.**`

**Why it's a factual claim:** asserts a limit on what admission controllers can see.

**Instances:** 1.

**Fix:** The first half is supportable (`controlling-access`: authorization needs *"the username of the requester, the requested action, and the object affected"*; admission *"can access the contents of the object that is being created or modified"*). **The second half is supported by no snapshot and is stronger than the sources warrant** — nothing in the corpus says admission ignores identity. Replace the symmetry with the sourced quorum contrast from entry 4, which is a sharper hazard and is fully attested: authorization is any-module-approves, admission is any-module-rejects. Note that Practice Q4's explanation ("quota is not an identity-scoped check") is fine as written and is supported by `resource-quotas` — that claim is about ResourceQuota specifically, not about admission generally.

### 6. §2 — "RBAC ... is a mechanism that lives at this gate"

**Excerpt:** `it is a mechanism that lives at this gate, and it has opinions about identities and verbs, not about the contents of your YAML.`

**Instances:** 1.

**Fix:** Tag to `[source: k8s-docs-controlling-access-2026-08-24]`: *"Kubernetes supports multiple authorization modules, such as ABAC mode, RBAC Mode, and Webhook mode."* This also restores the clause draft-v1 carried and draft-v2 cut ("RBAC is one authorizer among several") — it is now sourced and can go back if wanted.

### 7. §2 / §3 — ResourceQuota and LimitRange "take effect at this gate"

**Excerpts:** `ResourceQuota is one of the API resources used to configure a cluster [source: ...], and it takes effect at this gate rather than through a separate subsystem.` and §3's closing `both of these mechanisms take effect at the admission gate. Neither is a separate subsystem with its own enforcement path.` and Practice Q4's `Quota enforcement happens at the admission gate`.

**Instances:** 3.

**Fix:** Tag to `[source: k8s-docs-admission-controllers-2026-08-24]` — *"ResourceQuota -- This admission controller will observe the incoming request and ensure that it does not violate any of the constraints enumerated in the ResourceQuota object"* and *"LimitRanger -- This admission controller will observe the incoming request and ensure that it does not violate any of the constraints enumerated in the LimitRange object."* Corroborated by `resource-quotas` (*"It is enabled when the API server `--enable-admission-plugins=` flag has `ResourceQuota` as one of its arguments"*) and `limit-range` (*"the LimitRange admission controller applies default request and limit values"*). This is load-bearing for §8's spine claim, so it should not stay untagged.

### 8. §2 — what auditing does

**Excerpt:** `auditing exists, it is part of securing a cluster, and it is what tells you afterwards what happened.`

**Instances:** 2 (this and the Chapter Summary row).

**Fix:** Tag to `[source: k8s-docs-audit-2026-08-24]`: *"Kubernetes auditing provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster."* The same snapshot supplies one clause that costs nothing and restates this chapter's spine a fourth time: *"Audit records begin their lifecycle inside the kube-apiserver component."* Keep stages, levels and backends out — above budget, and the snapshot confirms the level definitions were not verbatim-captured.

### 9. §3 — all scope, counting and defaulting claims

**Excerpts:**
- `A quota is a ceiling on a **namespace, in aggregate**: the team's total, not any one Pod's numbers.`
- `which is a constraint on **individual objects**, and a mechanism that has to be able to act on a manifest that says nothing at all.`
- `The quota counts the namespace's total. The LimitRange counts one object's numbers.`
- `The quota may refuse it. The LimitRange may fill it in.`
- `> ★ **Fixed Point:** **ResourceQuota counts the namespace. LimitRange constrains the object.**`
- Figure 8.3's `min ≤ … ≤ max` bound and `REJECTED` panel; Bearings #1 A5; Practice Q5 and Q6 keys; Exam Alert item 8; two Chapter Summary rows.

**Instances:** 12.

**Fix:** All closable, and this section can now be *strengthened* rather than merely tagged:
- aggregate scope — `[source: k8s-docs-resource-quotas-2026-08-24]`: *"A resource quota, defined by a ResourceQuota object, provides constraints that limit aggregate resource consumption per namespace."*
- per-object scope — `[source: k8s-docs-limit-range-2026-08-24]`: *"A LimitRange is a policy to constrain the resource allocations (limits and requests) that you can specify for each applicable object kind (such as Pod or PersistentVolumeClaim) in a namespace."*
- the `min ≤ … ≤ max` bound in Figure 8.3 — *"Enforce minimum and maximum compute resources usage per Pod or Container in a namespace."* **The figure was right and the prose was thin; bring the prose up, do not cut the figure down.**
- rejection — *"If creating or updating a resource violates a quota constraint, the control plane rejects that request with HTTP status code `403 Forbidden`."*
- **the section's single most examinable sourced fact, currently absent** — *"If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients, **must** specify either `requests` or `limits` for that resource, for every new Pod you submit."* This also settles the internal inconsistency the previous audit flagged in the §3 Worth Securing callout, in favour of "the quota refuses it."
- defaulting — *"Set default request/limit for compute resources in a namespace and automatically inject them to Containers at runtime"* and *"LimitRange validations occur only at Pod admission stage, not on running Pods."*

Scope guard unchanged: do **not** take quota scopes, scope selectors, priority-class quota, or the full countable-resource roster. Per the snapshot's own extraction note, the compute/storage/object-count resource names are **[NAMES ONLY]** — do not quote the table row descriptions.

### 10. §4 — "Capacity and Allocatable are two different numbers ... the second is the one the scheduler uses"

**Excerpt:** `Capacity and Allocatable are two different numbers on the same Node object, and the second is the one the scheduler uses.`

**Instances:** 2 (this and the Chapter Summary "Allocatable" row).

**Fix:** `[source: k8s-docs-node-status-2026-08-24]` now **defines Capacity**, which no earlier snapshot did: *"The fields in the capacity block indicate the total amount of resources that a Node has. The allocatable block indicates the amount of resources on a Node that is available to be consumed by normal Pods."* Combined with `k8s-docs-reserve-compute-resources-2026-08-24` (*"Pods can consume all the available capacity on a node by default. This is an issue because nodes typically run quite a few system daemons that power the OS and Kubernetes itself"*, plus `kubeReserved` and `systemReserved`), the **unpaid Chapter 7 promise can now be discharged in two sentences.**

**Hard constraint, re-confirmed by both snapshots:** there is still no textual statement or equation relating Capacity, the reservations and Allocatable — the relationship is published only as `node-capacity.svg` with no text equivalent. **Do not state an arithmetic relationship, in numbers or in words.** The draft-v1 phrasing "what is left after the node's own overheads are set aside" was correctly cut and must not return.

### 11. §8 and Bearings #2 item 1 — the cordon → taint → scheduler causal link

**Excerpts:**
- §8: `It is a write through the API server, and the scheduler then does what the scheduler always does: it checks taints when it makes scheduling decisions [source: k8s-docs-taints-tolerations-depth-2026-08-24], finds the node marked unschedulable, and places nothing there.`
- Bearings #2 item 1 stem: `You cordon a node. Chapter 7 taught you a built-in taint ... Name that taint`

**Why it's a factual claim:** the juxtaposition asserts a mechanism — that what `cordon` writes is the thing the scheduler's taint check reads.

**Instances:** 3 (§8 paragraph, Bearings #2 item 1 stem + key, Practice Q10 key).

**Fix, partial — and this is the chapter's highest-leverage single sentence:** `[source: k8s-docs-node-status-2026-08-24]` states verbatim *"`SchedulingDisabled` is not a Condition in the Kubernetes API; instead, cordoned nodes are marked Unschedulable in their spec."* That converts "cordon writes a field on a Node object" and the spec-vs-status framing from inference to sourced claim, and restores Practice Q10's original (better) spec-vs-status item along with its `[retrieval: ch4]` tag — which also fixes the retrieval-percentage shortfall the draft's own accounting comment records (6/34 = 17.6%, below the 20% floor; restoring Q10 returns it to 20.6%).

**Still not sourced:** no cached sentence connects `.spec.unschedulable` to the `node.kubernetes.io/unschedulable` *taint*. Three separate facts are cached — cordon marks the node Unschedulable in spec [node-status]; a built-in `node.kubernetes.io/unschedulable:NoSchedule` taint exists and DaemonSet Pods tolerate it [daemonset]; the scheduler checks taints [taints-depth] — and `taints-depth` attributes automatic taint creation to node *conditions*, which unschedulability is not. **Recommended framing:** state the sourced spec write, then the sourced taint's existence and effect, and let the reader see the shape without the chapter asserting the link. Bearings #2 item 1 should ask the reader to name the built-in taint whose effect matches, not imply that `cordon` applies it.

### 12. Practice Q7 — "requests are the number the scheduler filters on"

**Excerpt:** `Chapter 5 established that requests are the number the scheduler filters on`

**Instances:** 1.

**Fix:** The draft's inline comment marks this unverifiable. **It is verifiable** — `k8s-docs-resource-management-2026-08-23` is in this chapter's set and states: *"When you specify the resource request for containers in a Pod, the kube-scheduler uses this information to decide which node to place the Pod on."* Tag it and delete the comment. The Allocatable half of the explanation was already sourced. Q7's key (B) is sound.

### 13. Practice Q13 — "Taking etcd backups is a control-plane duty"

**Excerpt:** `Taking etcd backups is a control-plane duty`

**Instances:** 1. (The companion half of the same key is separately **contradicted** — see CONTRADICTED entry 2.)

**Fix:** Derivable but untagged. `k8s-docs-etcd-access-control-2026-08-24` establishes etcd as the control plane's backing store reachable ideally only by the API server, and `k8s-docs-etcd-backup-2026-08-23` names the disaster scenario as "losing all control plane nodes." Tag against both, or reframe as the book's architectural reasoning.

### 14. The Voyage Ahead — Pod disposability

**Excerpt:** `Pods are, by design, disposable: a controller may replace one at any moment, and the replacement is a different Pod.`

**Why it's a factual claim:** asserts controller replacement semantics.

**Instances:** 1.

**Fix:** No snapshot in this chapter's set covers workload-controller replacement semantics. This is Chapter 6 material recapped forward. Either tag against Chapter 6's referenced snapshot set (which the integration stage can verify), or attribute it explicitly to Chapter 6 in-prose ("Chapter 6 established that…"), which is the cheaper fix and matches how the chapter handles other backward references.

---

## FAIL — Contradicted claims

### 1. Figure 8.3 and its caption — "(no namespace boundary)" for LimitRange

**Location:** §3, `<!-- FIGURE: ch08-fig05-quota-vs-limitrange -->` right-hand panel label and the caption below it.

**Tag:** untagged (the figure carries no source tag; the surrounding prose is tagged to `k8s-docs-cloud-native-security-2026-08-23`, which does not address scope).

**Snapshot says** (`k8s-docs-limit-range-2026-08-24`): *"A LimitRange is a policy to constrain the resource allocations (limits and requests) that you can specify for each applicable object kind (such as Pod or PersistentVolumeClaim) **in a namespace**."* And: *"Kubernetes constrains resource allocations to Pods **in a particular namespace** whenever there is at least one LimitRange object in that namespace."*

**Draft says:** figure label `LimitRange / (no namespace boundary)`; caption: *"On the right, there is no namespace boundary at all — the constraints sit on individual Pods."*

**Why this matters beyond pedantry:** a LimitRange **is a namespaced object with a namespace boundary**; it applies only to objects in its own namespace. The chapter contradicts itself four paragraphs later: *"ResourceQuota and LimitRange are namespaced objects."* A reader who takes the figure at face value will answer a KCNA-style "is a LimitRange namespaced or cluster-scoped?" item wrongly — and the figure is the artefact the chapter tells them to trust ("the two failure modes are the proof").

**Recommended fix:** Draw the namespace boundary on **both** panels and move the discrimination to what is actually being counted: left panel, one aggregate total for the namespace, fifth Pod rejected at the cap; right panel, same namespace boundary, per-object `min ≤ … ≤ max` bounds on each Pod, fifth Pod accepted with defaults injected. Rewrite the caption to say the panels fail differently *within the same scope*, which is the true and sharper discrimination. Note that this is a figure-content change, not an anchor change — `ch08-fig05-quota-vs-limitrange` must be preserved verbatim as the join key to `image-specs.md`, and the corresponding spec entry needs the same correction in the same sweep.

### 2. Practice Q13, correct answer C's rationale — who sets ResourceQuotas

**Location:** Practice Questions, answer key for Q13.

**Tag:** untagged.

**Snapshot says** (`k8s-docs-resource-quotas-2026-08-24`): *"**A cluster administrator** creates at least one ResourceQuota for each namespace."* And (`k8s-docs-limit-range-2026-08-24`): *"**The administrator** creates a LimitRange in a namespace."*

**Draft says:** *"Taking etcd backups is a control-plane duty; setting a namespace's ResourceQuotas is a workload-side concern that belongs to whoever runs the workloads, on either team."* And in distractor B's rebuttal: *"which is right about images and requests but names no control-plane duty at all."*

**Why this matters:** the question's keyed answer turns on ResourceQuota administration sitting with the *workload team*. Both newly-present snapshots attribute it to the *cluster administrator* — i.e. to exactly the side the key excludes. The item is now keyed against its own sources, and a well-prepared candidate reading the documentation would pick differently. This is a live correctness defect in an exam-simulation item, not a phrasing quibble.

**Recommended fix:** Replace the "does not" half of option C with a duty the sources unambiguously place outside control-plane operation. The cleanest available pair, both fully sourced: **taking etcd backups** (control-plane duty) versus **choosing container images / declaring a Pod's resource requests** (`k8s-docs-resource-quotas-2026-08-24`: *"Users create resources (pods, services, etc.) in the namespace"*; `k8s-docs-resource-management-2026-08-23` on requests as a Pod-spec author's declaration). Rewrite distractor B accordingly so it remains a genuine four-way discrimination rather than collapsing into the new key. Note that the previous rewrite of Q13 correctly removed the unsourceable managed-vs-self-hosted axis; this finding is about the axis that replaced it.

---

## WARN — Minor discrepancies

1. **Citation staleness on the node conditions table (§4).** The conditions table, the three-valued `Ready` description, and the status-field list are tagged to `[source: k8s-docs-nodes-2026-08-23]`. That snapshot carries a `supersedes_note`: *"As of 2026-08-24 the concept page no longer carries that table -- it links out to this reference page. Chapter 8 sec.4 should cite THIS file"* — i.e. `k8s-docs-node-status-2026-08-24`. The **content is unchanged and correct**; only the citation points at a page that no longer carries it. Retag conditions, Capacity/Allocatable and Info to the node-status reference; keep the 08-23 nodes snapshot for registration, cordon/drain/uncordon, heartbeats and the node controller.

2. **The status-field list reads as exhaustive and is now one short.** §4: *"A Node's status contains Addresses (…); Conditions; Capacity and Allocatable; and Info…"* The current reference page lists five: *"Addresses * Conditions * Capacity and Allocatable * Info * Declared Features."* Declared Features is correctly out of scope (above associate tier, in no CNCF competency list), but the sentence should read "contains, among other fields" rather than implying a closed set.

3. **`node-monitor-grace-period` now has a documented default.** §4 states *"This book will not give you a number for it."* `k8s-docs-node-status-2026-08-24` documents *"default is 50 seconds."* The outline's standing instruction permits this **as a dated illustration, never as a rule.** Optional; the examinable fact is unchanged either way. If added, `SchedulingDisabled is not a Condition in the Kubernetes API` from the same snapshot is a ready-made Snag for the same subsection.

4. **Practice Q8's rebuttal of option A rests on an unasserted mechanism.** The key says drain-then-cordon *"would drain a node that is still accepting new Pods."* `k8s-docs-safely-drain-node-2026-08-24` carries an explicit warning: *"No sentence on this page states that `kubectl drain` cordons the node as part of its operation… **Chapter 8 must not claim it from this source.**"* The same page then instructs *"you need to run `kubectl uncordon <node name>` afterwards"*, which cuts against the draft's assumption. Neither direction is assertable. **Recommended fix:** rebut A on sequence logic that is sourced — cordon is documented as *"a preparatory step before a node reboot or other maintenance"* — rather than on a claim about what drain does or does not do to schedulability.

5. **The three-gate model omits a stage the source enumerates.** `k8s-docs-controlling-access-2026-08-24` presents five stages, opening with **Transport security** before Authentication. The chapter's compression to "three gates and a logbook" is defensible pedagogy and the TLS material is covered inside gate one, but a candidate could meet an item on the fuller stage list. One clause acknowledging that the project's own page begins with transport security would close the gap at negligible cost.

6. **`po` remains unattested.** Figure 8.1's callout `pod = pods = po`. The singular/plural/abbreviated *rule* is sourced; the specific abbreviation string is in no snapshot. Low risk. Either accept it as an instantiation or substitute a form the corpus attests.

7. **`kubectl scale deployment/web --replicas=5` uses a syntax the cached grammar does not document.** The prose example uses the `TYPE/NAME` slash form; Figure 8.1 silently normalises the same command into separate TYPE and NAME columns. `k8s-docs-kubectl-overview-2026-08-23` documents only `kubectl [command] [TYPE] [NAME] [flags]`. In a section whose entire point is the four-slot grammar, the mismatch between the prose example and the figure is worth resolving — use `kubectl scale deployment web --replicas=5` in both, or note the slash form as an equivalent the snapshot does not cover.

8. **"`kubectl explain` … queries the API's own documentation"** (§1 Worth Securing) asserts a mechanism. The snapshot supports only *"Get documentation of various resources (pods, nodes, services, etc.)"*. The pedagogical point survives as "returns documentation for a resource type rather than your cluster's contents"; drop "queries the API's own documentation" unless a `kubectl explain` reference page is fetched.

9. **"a container runtime must already be present on those nodes"** (§5). The snapshot establishes the requirement (*"A container runtime (containerd or CRI-O) must be installed on every node"*) but not the ordering relative to `kubeadm`. Delete "already"; the sourced form carries the same weight, and the previous narrowing pass left the word behind.

10. **§6's rationale for `kubectl`'s symmetric window is authored, not documented.** *"`kubectl` is a **user tool that addresses the cluster from outside** … so its compatibility window is about human convenience."* No snapshot gives a reason for any skew rule. The reasoning is sound and pedagogically valuable; mark it as the book's explanation rather than as documented rationale. Same applies to Bearings #3 A2 and Practice Q15's explanation. The upgrade-order derivation in the same section is handled correctly — it is explicitly framed as falling out of the tagged rule, and no cached source states an upgrade order.

11. **Two different API server ports now sit in the corpus.** §2 says *"a secure HTTPS port, typically 443"* [control-plane-node-communication] — faithful to its tag. `k8s-docs-controlling-access-2026-08-24` says *"the Kubernetes API server listens on port 6443 on the first non-localhost network interface."* No contradiction as written, but if §2 is expanded during the controlling-access retag, do not mix the two figures in one sentence.

Also noted, non-blocking: §3's absolute negative *"There is no ResourceQuota that limits how many Nodes a group may consume"* is a sound derivation from two tagged facts (quota is per-namespace; Nodes are cluster-scoped) rather than a quoted claim. It is correct — every countable resource the quota snapshot lists is namespaced — but it is a derivation and reads as a citation. Keep the derivation visible in the prose, which it currently is.

---

## PASS — Verified claims (sampled)

**§1 — kubectl grammar.** Four-slot form; `create`/`get`/`describe`/`delete` as command examples; TYPE as resource type; name-omitted-means-all; flags override defaults and environment variables; types case-insensitive and singular/plural/abbreviated; names case-sensitive. All verbatim in `k8s-docs-kubectl-overview-2026-08-23`. Full verb table (11 entries) matches the snapshot's Operations list, including `scale`'s "replication controller / deployment" phrasing and `rollout`'s three valid resource types. Kubeconfig precedence (`$HOME/.kube/config`, `KUBECONFIG`, `--kubeconfig`) verbatim; the flag-beats-environment conclusion is a transparent application of the snapshot's own general rule and the draft says so. In-cluster detection (two env vars + token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`, "all three found", ServiceAccount namespace unless `--namespace`) verbatim. `kubectl cordon $NODENAME` and its effect verbatim from `k8s-docs-nodes-2026-08-23`, now additionally corroborated by `k8s-docs-kubectl-cordon-2026-08-24` (*"Mark node as unschedulable"*, `kubectl cordon NODE`) — worth adding as a second tag, since that snapshot exists precisely to instantiate this section's grammar.

**§2 — attested portions.** The documentation's securing-a-cluster list and its relative ordering, including Auditing sitting further down among other entries — accurate to `k8s-docs-cluster-administration-2026-08-23`. Extension-point taxonomy naming authentication, authorization and dynamic admission control — accurate to `k8s-docs-extending-kubernetes-2026-08-23`. HTTPS port typically 443 with client authentication; node provisioning with the cluster root certificate and client certificates; kubelet TLS bootstrapping; ServiceAccount root-certificate-and-bearer-token injection; "one or more forms of authorization should be enabled, especially if anonymous requests or service account tokens are allowed" — all accurate to `k8s-docs-control-plane-node-communication-2026-08-24`. Authentication-and-authorization-as-a-pair — accurate to `k8s-docs-cloud-native-security-2026-08-23`. NodeRestriction's `node-restriction.kubernetes.io/` prefix rule — accurate to `k8s-docs-assign-pod-node-2026-08-23`, corroborated by the admission-controllers reference. Pod Security Admission as the built-in enforcer — accurate to `k8s-docs-pod-security-standards-2026-08-23`. Webhook synchronous-HTTP-plus-point-of-failure — accurate to extending-kubernetes. Hub-and-spoke closing paragraph — verbatim.

**§4.** Both node registration paths, `metadata.name` validation, healthy-node eligibility, DNS-subdomain-and-unique naming; cordon/drain/uncordon; all five conditions and the three `Ready` values; `kubectl describe node <name>`; both heartbeat forms and the `kube-node-lease` Lease objects; the node controller's three jobs including API-initiated eviction — all accurate to `k8s-docs-nodes-2026-08-23` (subject to WARN 1's retag). DaemonSet tolerating an unschedulable node — nodes snapshot — plus the `node.kubernetes.io/unschedulable` / `NoSchedule` toleration row — verbatim from `k8s-docs-daemonset-2026-08-24`. Control-loop definition (read `.spec`, do things, update `.status`) — verbatim from extending-kubernetes. Both Allocatable sentences — verbatim from `k8s-docs-node-allocatable-2026-08-24`. Chapter 4's Lease pointer — accurate to `k8s-docs-namespaces-2026-08-23`.

**§3 hinge.** Namespaced-vs-cluster-scoped, including the StorageClass/Nodes/PersistentVolumes examples — verbatim from `k8s-docs-namespaces-2026-08-23`. This is the one part of §3 that was fully sourced before this pass and remains so.

**§5.** All five planning questions match `k8s-docs-cluster-administration-2026-08-23`. minikube, kind ("Kubernetes IN Docker", Docker containers as nodes), managed/turnkey services, kubeadm as officially supported for creating clusters and joining nodes, k3s as lightweight, container runtime (containerd or CRI-O) required on every node, kubectl as the CLI for any cluster — all verbatim from `k8s-docs-setup-tooling-2026-08-23`. CRI as the interface for alternative runtimes, and scheduler plugins/profiles as a scheduling extension point — extending-kubernetes.

**§6 — the whole skew table, row by row.** HA kube-apiserver within one minor; kubelet not-newer / three-older / `<1.25` two-older, with the 1.36 → 1.36/1.35/1.34/1.33 example; kube-proxy not-newer-than-apiserver, three-older, and three older-or-newer than its co-located kubelet; controller-manager/scheduler/cloud-controller-manager not-newer, expected-to-match, one-older for live upgrades; kubectl one minor either direction with the 1.37/1.36/1.35 example — **all five rows and both worked examples verbatim** from `k8s-version-skew-policy-2026-08-23`. Semantic-versioning `x.y.z`; three maintained release branches; backporting by severity and feasibility — same snapshot. One year of patch support for 1.19+, nine months for 1.18 and older; three minor releases per year since 2021 at roughly fifteen weeks, SIG Release, monthly patch cuts; and the dated 1.36/1.35/1.34 roster, correctly presented as a snapshot-time illustration — all `k8s-releases-cadence-2026-08-23`. Figure 8.5 is consistent with the table, and its note that the HA rule is a mutual bound rather than a bar relative to the API server is correct.

**§7.** etcd as *"a consistent and highly-available key value store used as Kubernetes' backing store for all cluster data"* and *"Access to etcd is equivalent to root permission in the cluster so ideally only the API server should have access to it"* — verbatim from `k8s-docs-etcd-access-control-2026-08-24`. All objects stored in etcd; periodic backup for disaster scenarios including losing all control plane nodes; `etcdctl snapshot save backup.db`; volume snapshot as the second method; the four TLS flags; snapshot contains all state, keep encrypted, store outside the control plane nodes; `etcdutl snapshot restore` operating on data files with control-plane restart afterwards — all verbatim from `k8s-docs-etcd-backup-2026-08-23`. The section's restraint on etcd TLS configuration is correct and should be preserved: that guidance was explicitly not verbatim-verified in the cached fetch.

**§8.** *"The scheduler checks taints, not node conditions, when it makes scheduling decisions"* — verbatim from `k8s-docs-taints-tolerations-depth-2026-08-24` (the surrounding causal link is the subject of FAIL entry 11).

**Practice Q17 explanation** deserves specific credit: *"no cached documentation attributes automatic encryption to either utility"* states the evidentiary position rather than asserting a negative fact. That is the correct pattern for a distractor rebuttal in this pipeline, and it is the model the other keys flagged above should follow.