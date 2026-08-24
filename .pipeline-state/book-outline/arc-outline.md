---
book: Kubernetes and Cloud Native Associate
exam_code: KCNA
exam_authority: CNCF / Linux Foundation
curriculum_version: KCNA curriculum effective 2025-11-24 (4 domains: 44/28/16/12)
total_chapters: 20
total_target_words: null   # word budgets retired 2026-04-24 (style-decisions.md § "Length Budgets"); length is content-driven
book_key: kcna
stage: B5 — Outline Assembly
date: 2026-08-23
inputs: [B1 domain-analysis.md, B2 chapter-lineup.md, B3 retrieval-architecture.md (degraded — see § Input provenance), B4 length-budget.md]
---

# Arc Outline — Kubernetes and Cloud Native Associate

## Input provenance (read before consuming this file)

Three of four upstream artifacts are intact. One is not, and downstream stages need to know which.

| Stage | Artifact | State |
|---|---|---|
| B1 | `domain-analysis.md` | Intact (consumed indirectly — B2 encodes its conclusions) |
| B2 | `chapter-lineup.md` | **Intact and authoritative.** Titles, subtitles, objectives, prerequisites, weights, Part structure, and Zenith designations in this file are B2 verbatim or B2-derived |
| B3 | `retrieval-architecture.md` | **Degraded.** The file on disk contains B3's tool-permission failure message, not B3's document. The orchestrator captured stdout verbatim, and B3's stdout was a request for write access rather than the artifact. What survives is the ~19-line summary of conclusions embedded in that message |
| B4 | `length-budget.md` | Intact, with a cosmetic defect — the artifact begins with a stdout preamble and wraps its body in a ` ```markdown ` fence. Content is unaffected |

**Consequence for this file.** Every retrieval figure that B3 stated explicitly — the per-chapter percentages, the five 25%-ceiling chapters, the Ch 1 exclusion, the Soundings exclusion, the ≥4-chapters-back spacing floor, three of the nine cross-cutting themes, the version-skew decay fix, and the four do-not-retrieve items — is carried forward verbatim and marked `[B3]`. The remaining **six cross-cutting themes are reconstructed** from B2's dependency graph and cross-bearing pairs, and are marked `[B5-reconstructed]`. They are defensible and load-bearing, but they are not B3's list. If B3 is re-run, reconcile § "Cross-cutting retrieval themes" against its output before drafting Ch 5 onward.

**Also flagged:** B3 and B4 disagree on the early spacing ramp. B3 says Ch 3 = 10%, Ch 4 = 15%, then 20–25%. B4's restatement says Ch 4–5 ≈ 10%, Ch 6–8 ≈ 15%, Ch 9–13 ≈ 20%. B3 is the dedicated stage and its schedule is adopted here; B4's table is a generic restatement of the skill's Part 10 example and is superseded.

**Stage-hygiene note for the orchestrator:** stdout *is* the artifact. A stage that calls `Write` instead of emitting to stdout destroys its own output (B3), and a stage that wraps its body in commentary or a fence embeds that wrapper in the artifact (B4). This file emits raw markdown and nothing else.

---

## Book architecture

Twenty chapters in six Parts. Parts II–V map one-to-one onto the four published exam domains, so the reader's progress through the book is legible as progress through the blueprint — which matters unusually much for this exam, because the blueprint changed on 2025-11-24 and a large body of third-party prep still targets the old five-domain shape.

| Part | Theme | Chapters | Domain | Weight |
|---|---|---|---|---|
| **I — Taking Departure** | What KCNA is, what changed, how to read this book | 1 | — | 0% |
| **II — Ship, Cargo, and Company** | Containers, the cluster, the objects that describe it, the components that run it | 2–8 | D1 Kubernetes Fundamentals | **44%** |
| **III — Underway** | Keeping workloads reachable, stored, secured, diagnosable | 9–13 | D2 Container Orchestration | **28%** |
| **IV — Dispatches** | Getting software from a repository into a cluster, and finding out why it didn't work | 14–16 | D3 Cloud Native Application Delivery | **16%** |
| **V — The Wider Sea** | The patterns, the foundation, the instruments | 17–18 | D4 Cloud Native Architecture | **12%** |
| **VI — Making Port** | Synthesis, exam-day strategy, the full mock | 19–20 | — | 0% |

Seventeen content chapters carry 100% of exam weight. Content-chapter distribution: D1 7 (41.2%) · D2 5 (29.4%) · D3 3 (17.6%) · D4 2 (11.8%). Maximum count deviation from published weight: 2.8 points.

**The spine.** The book has one structural argument, stated three times at increasing altitude: *the control loop*. Chapter 3 introduces it as the animating idea of the cluster. Chapter 6 instantiates it in the workload controllers. Chapter 15 generalizes it to a Git repository — and that recognition, not a fifth list to memorize, is the book's **primary Zenith**. The whole of Part IV's ordering (packaging → delivery → debugging) exists to set that beat up: Argo CD consumes Helm charts, so Helm must land first.

The **secondary Zenith** is Chapter 17's extension-points synthesis, where CRI (Ch 2), CNI (Ch 9), CSI (Ch 11), and CRDs (Ch 6) resolve into a single pluggability story with back-bearings to all four.

**Ordering principles inherited from B2**, all dependency-driven:

- **Containers first, not last.** D1.4 is a quarter of the largest domain but the deepest root in the graph. Deferring OCI to a back chapter forces the reader to accept "container" as an undefined primitive for two hundred pages.
- **Core Concepts is the trunk and gets four consecutive chapters (3–6):** cluster → objects → Pod → controllers, each a hard prerequisite for the next.
- **Administration closes Part II rather than opening it.** The three API access gates, node lifecycle, and version skew read as arbitrary rules until the reader knows what a control plane, an object, and a node are. Placing it last converts a list of facts into a set of consequences.
- **Networking splits across two chapters** because "how do Pods find each other" (Ch 9) and "how does the outside world get in, and how do you stop it" (Ch 10) are different cognitive modes. Merging them would bury the Ingress-is-frozen-but-not-deprecated distinction in the back half of the book's only oversized chapter.
- **Security (Ch 12) is a synthesis chapter in disguise** and therefore comes after networking and storage: RBAC needs namespaces and cluster-scoped resources, Secret hardening needs etcd and RBAC, Pod Security Standards need `securityContext` and the Ch 8 admission gate.
- **Troubleshooting is one arc across two chapters.** The exam splits platform scope (Ch 13, D2.3) from application scope (Ch 16, D3.2); the reader's mental model should not be split. Reciprocal cross-bearings bind them.
- **One deliberate forward reference: StatefulSet.** It appears in Ch 6 with its sibling workload resources, five chapters before PersistentVolumes are defined, because it belongs taxonomically with Deployment and DaemonSet. Ch 6 teaches *why it is different*; Ch 11 closes the loop with the PV pairing.

**Length.** No chapter in this book carries a word target. Budgets were retired 2026-04-24; chapters are whatever length the material requires. The **depth band** given per chapter below is a planning signal for the Stage 1 section planner — a statement of relative heft derived from exam weight and prerequisite load — not a budget, and nothing downstream should enforce it.

**Question budget** (from B4): 715 questions against a 300 floor — 146 Soundings, 180 Bearings, 319 chapter Practice, 10 synthesis, 60 mock. Per-chapter figures appear in each entry below. Note that Bearings counts are *minimums to exceed*, not targets to hit; Ch 8, Ch 12, and Ch 17 each carry enough unrelated conceptual arcs to warrant three checkpoints and 12–15 Bearings.

---

## Chapter-by-chapter

### Chapter 1 — Taking Departure

- **Subtitle**: *"Ninety minutes, four domains, and a curriculum that moved under everyone's feet"*
- **Purpose**: orientation (chapter_type: `orientation`)
- **Covers**: No domain objectives. Exam mechanics and format; the 2025-11-24 blueprint change and what it invalidates; the three required weight-allocation disclosures; how to use this book; the cloud-native framing planted for harvest in Ch 17; the CNCF certification ladder positioned relative to CKA/CKAD/CKS
- **Prerequisites**: None. Assumes general IT literacy and no Kubernetes exposure
- **Target length**: Content-driven, no word target. **Depth band: focused** — orientation chapters earn their keep by being short enough to actually read before Chapter 2
- **Retrieval targets**: None. **[B3]** Ch 1 is excluded from the retrieval schedule entirely, and no item anywhere in the book tests exam mechanics
- **Key concepts introduced**: The four domains and their weights (44/28/16/12); what changed from the five-domain blueprint; "commonly reported" vs published exam facts; the reader's own calibration path through the book
- **Required figures (anchor stubs)**: `ch01-fig01-blueprint-change-2025`, `ch01-fig02-book-map-parts-to-domains`
- **Question budget**: 5 Soundings · 5 Bearings · 0 Practice · **10 total**
- **Notes**: Orientation type — exempt from *Why This Chapter Matters* and end-of-chapter Practice Questions per the structural contract. Carries the three B2 disclosures into front matter. The `KCNA_Curriculum.pdf` typo ("Could Native Community and Collaboration") belongs in the blueprint appendix, not here.

---

### Chapter 2 — Cargo in Standard Crates

- **Subtitle**: *"Why the shipping container beat the ship"*
- **Purpose**: domain — D1.4 Containerization (chapter_type: `content`)
- **Covers**: **D1.4** — containers vs VMs; images, layers, tags vs digests; registries; `imagePullPolicy`; immutability; OCI runtime/image/distribution specs; runC; CRI; containerd; CRI-O; RuntimeClass; image build practices
- **Prerequisites**: None beyond Ch 1. First content chapter by design — it is the deepest root in the dependency graph
- **Target length**: Content-driven, no word target. **Depth band: heavy** — largest single weight allocation (9 points), deepest prerequisite, and the most new research (B1 gap G29 found cached sources cover only the runtime and OCI-spec halves)
- **Retrieval targets**: None — first content chapter
- **Key concepts introduced**: The container/VM boundary; image immutability and why a tag is not an identity; the OCI three-spec split; the kubelet → CRI → containerd → runC chain; `imagePullPolicy` defaults and the `:latest` interaction
- **Required figures (anchor stubs)**: `ch02-fig01-vm-vs-container-stack`, `ch02-fig02-image-layers-and-digests`, `ch02-fig03-oci-three-specs`, `ch02-fig04-cri-runtime-chain`, `ch02-fig05-imagepullpolicy-decision`, `ch02-zenith-standard-crate`
- **Question budget**: 8 Soundings · 10 Bearings · 25 Practice · **43 total**
- **Notes**: Blocking gaps G29 (build practices, layers, tags vs digests, registries, Buildpacks) and G30 (sandboxed runtimes, RuntimeClass motivation) must close before drafting. CRI planted here is the first of the four pluggable interfaces that resolve in Ch 17.

---

### Chapter 3 — The Ship's Company

- **Subtitle**: *"Everyone aboard has one job, and none of them is 'be in charge'"*
- **Purpose**: domain — D1.1 Kubernetes Fundamentals / cluster architecture (chapter_type: `content`)
- **Covers**: **D1.1** — deployment eras; what Kubernetes is and is not; control-plane components (kube-apiserver, etcd, kube-scheduler, kube-controller-manager, cloud-controller-manager); node components (kubelet, kube-proxy, container runtime); addons; controllers; **the control loop**; desired vs current state; Kubernetes origin and history
- **Prerequisites**: Ch 2 — containers, container runtime, CRI
- **Target length**: Content-driven, no word target. **Depth band: standard-plus** — 6 points, but it opens the book's structural spine and the control-loop treatment must be strong enough to carry five later callbacks
- **Retrieval targets**: **10%** **[B3]** — the schedule's opening rung, drawn entirely from Ch 2. Anchors: the CRI boundary (which component actually talks to the runtime), image immutability, container-vs-VM
- **Key concepts introduced**: **The control loop** (desired state, current state, reconciliation) — the single most reused idea in the book; the control-plane/node split; why no component is "in charge"; etcd as the state of record
- **Required figures (anchor stubs)**: `ch03-fig01-control-plane-and-node-components`, `ch03-fig02-control-loop-desired-vs-current`, `ch03-fig03-deployment-eras-timeline`, `ch03-fig04-request-path-through-apiserver`, `ch03-zenith-nobody-is-in-charge`
- **Question budget**: 8 Soundings · 10 Bearings · 19 Practice · **37 total**
- **Notes**: `ch03-fig02` is the book's most reused figure — Ch 6, Ch 15, and Ch 17 all call back to its shape. Design it once, deliberately, for re-presentation at three later altitudes.

---

### Chapter 4 — Records of Intent

- **Subtitle**: *"You don't give Kubernetes orders. You file a declaration."*
- **Purpose**: domain — D1.1 Kubernetes Fundamentals / objects and configuration (chapter_type: `content`)
- **Covers**: **D1.1** — objects; spec/status; manifests; `apiVersion`/`kind`/`metadata`/`spec`; `kubectl apply`; labels; selectors (equality and set-based); annotations; namespaces; initial namespaces; **namespaced vs cluster-scoped**; ConfigMaps; Secrets (definition and contrast)
- **Prerequisites**: Ch 3 — control loop, kube-apiserver, etcd as state of record
- **Target length**: Content-driven, no word target. **Depth band: standard-plus** — 6 points, but two of the book's nine cross-cutting themes originate here (namespaced-vs-cluster-scoped; labels/selectors as the universal join)
- **Retrieval targets**: **15%** **[B3]** — from Ch 2–3. Anchors: the control loop (what does the controller compare `spec` against?), image references inside a Pod spec, the apiserver's role in `apply`
- **Key concepts introduced**: Declarative desired state as an artifact, not a command; `spec` vs `status` as the control loop's two halves; labels and selectors as the mechanism that joins nearly every object pair in Kubernetes; the namespaced/cluster-scoped boundary; ConfigMap vs Secret (and that Secrets are only base64-encoded)
- **Required figures (anchor stubs)**: `ch04-fig01-object-anatomy-spec-status`, `ch04-fig02-apply-round-trip`, `ch04-fig03-labels-selectors-join`, `ch04-fig04-namespaced-vs-cluster-scoped`, `ch04-fig05-configmap-secret-contrast`, `ch04-zenith-declaration-not-order`
- **Question budget**: 8 Soundings · 10 Bearings · 19 Practice · **37 total**
- **Notes**: Cached coverage is sufficient — no blocking gaps. `ch04-fig04` is load-bearing for Ch 12: **[B3]** the RBAC four-way matrix (Role/ClusterRole × RoleBinding/ClusterRoleBinding) should be *derived* from this boundary in Ch 12, not memorized as a table. Forward cross-bearing to Ch 15 (ConfigMap/Secret as twelve-factor factor III).

---

### Chapter 5 — The Smallest Vessel

- **Subtitle**: *"A Pod is not a container, and that distinction is worth points"*
- **Purpose**: domain — D1.1 Kubernetes Fundamentals / Pods (chapter_type: `content`)
- **Covers**: **D1.1** — the Pod concept and shared network namespace; multi-container and init containers; Pod phases; container states; `restartPolicy`; restart backoff; liveness/readiness/startup probes and probe mechanisms; resource requests and limits; QoS classes; ServiceAccount as Pod identity (planted)
- **Prerequisites**: Ch 2 (containers, images), Ch 4 (object anatomy, labels)
- **Target length**: Content-driven, no word target. **Depth band: substantial** — 7 points, and requests/limits introduced here feed four later chapters
- **Retrieval targets**: **20%** **[B3]** — from Ch 2–4. Anchors: `imagePullPolicy` (Ch 2) as a cause of a container state; spec/status (Ch 4) read against Pod phase; labels (Ch 4) on a Pod
- **Key concepts introduced**: The Pod as the smallest deployable unit and why the shared network namespace is the reason; Pod phase vs container state (the distinction Ch 13 depends on); the three probes and what each actually does on failure; **requests vs limits** and the QoS classes they produce
- **Required figures (anchor stubs)**: `ch05-fig01-pod-shared-network-namespace`, `ch05-fig02-pod-phases-and-container-states`, `ch05-fig03-init-containers-sequence`, `ch05-fig04-three-probes-compared`, `ch05-fig05-requests-limits-qos-classes`, `ch05-zenith-smallest-deployable-unit`
- **Question budget**: 8 Soundings · 10 Bearings · 21 Practice · **39 total**
- **Notes**: Blocking gaps G3 (requests, limits, QoS classes) and G7 (ServiceAccounts) must close first. ServiceAccount is *planted only* — full treatment is Ch 12. `ch05-fig05` is retrieved in Ch 7 (scheduling), Ch 13 (OOMKilled/Evicted), Ch 17 (autoscaling), and Ch 18 (metrics).

---

### Chapter 6 — Fleets, Not Vessels

- **Subtitle**: *"Nobody sails one Pod"*
- **Purpose**: domain — D1.1 Kubernetes Fundamentals / workload resources (chapter_type: `content`)
- **Covers**: **D1.1** — ReplicaSet; Deployment; rolling update; `maxSurge`/`maxUnavailable`; Recreate; revisions; rollout history; rollback; pause/resume; StatefulSet (introduced with siblings); DaemonSet; Job; CronJob; `kubectl scale`; the HPA concept; custom resources and the operator pattern (definition)
- **Prerequisites**: Ch 4 (objects, selectors), Ch 5 (Pod, probes, requests)
- **Target length**: Content-driven, no word target. **Depth band: standard-plus** — 6 points, but this is the control loop's first instantiation and closes Part II's trunk
- **Retrieval targets**: **20%** **[B3]** — from Ch 3–5. Anchors: the control loop (Ch 3) now visible in a named controller; selectors (Ch 4) as the ReplicaSet→Pod join; probes (Ch 5) as what makes a rolling update safe
- **Key concepts introduced**: Ownership chain Deployment → ReplicaSet → Pod; rolling-update *mechanics* (strategy vocabulary is deliberately deferred to Ch 15); the workload-resource decision tree; StatefulSet identity vs Deployment interchangeability; CRDs and the operator pattern as "the control loop, extended"
- **Required figures (anchor stubs)**: `ch06-fig01-deployment-replicaset-pod-ownership`, `ch06-fig02-rolling-update-maxsurge-maxunavailable`, `ch06-fig03-recreate-vs-rolling`, `ch06-fig04-workload-resource-decision-tree`, `ch06-fig05-statefulset-vs-deployment-identity`, `ch06-zenith-control-loop-instantiated`
- **Question budget**: 8 Soundings · 10 Bearings · 19 Practice · **37 total**
- **Notes**: Blocking gaps G8 (update mechanics, rollout, rollback) and G10 (CRDs, operator pattern). **The book's one deliberate forward reference lands here** — StatefulSet is taught at the level of *why it is different*, with a forward cross-bearing to Ch 11 for the PV pairing. This placement defuses B1 trap #21 ("Deployment vs StatefulSet is about whether the app writes to disk") at the point the distinction is actually drawn.

---

### Chapter 7 — Assigning the Berth

- **Subtitle**: *"Filter, score, bind — and then a coin flip"*
- **Purpose**: domain — D1.3 Scheduling (chapter_type: `content`)
- **Covers**: **D1.3** — scheduling overview; feasible nodes; filtering; scoring; binding; random tie-break; unschedulable Pods; node labels; `nodeSelector`; node affinity (required vs preferred); pod affinity/anti-affinity; taints and tolerations (NoSchedule / PreferNoSchedule / NoExecute); `nodeName`; topology spread; scheduling policies vs profiles
- **Prerequisites**: Ch 5 (Pod, requests/limits), Ch 6 (workload resources creating Pods)
- **Target length**: Content-driven, no word target. **Depth band: standard** — 5 points, procedural material with a clean three-step spine
- **Retrieval targets**: **20%** **[B3]** — from Ch 4–6. Anchors: labels (Ch 4) now doing node selection rather than Pod selection; requests (Ch 5) as the filter input; the controller (Ch 6) that produced the unscheduled Pod
- **Key concepts introduced**: Filter → score → bind, and that ties break randomly; the `nodeSelector`/affinity gradient from blunt to expressive; taints and tolerations as the *node's* veto rather than the Pod's request; why "unschedulable" is a Pending Pod, not an error
- **Required figures (anchor stubs)**: `ch07-fig01-filter-score-bind`, `ch07-fig02-nodeselector-vs-affinity`, `ch07-fig03-taints-tolerations-effects`, `ch07-fig04-pod-affinity-anti-affinity-topology`, `ch07-zenith-berth-assignment`
- **Question budget**: 8 Soundings · 10 Bearings · 17 Practice · **35 total**
- **Notes**: Blocking gaps G4 (taints/tolerations, affinity, `nodeSelector`, topology spread) and G3. **[B3] Decay risk — thin downstream presence.** Scheduling is otherwise never revisited. Two named anchors are mandatory: Ch 13 (Pending as a scheduling-failure signature) and Ch 17 (Cluster Autoscaler reacting to unschedulable Pods). Do not let these drop.

---

### Chapter 8 — Standing the Watch

- **Subtitle**: *"The commands you'll actually type, and the versions that will bite you"*
- **Purpose**: domain — D1.2 Cluster administration (chapter_type: `content`)
- **Covers**: **D1.2** — kubectl syntax and verbs; kubeconfig; in-cluster auth; cluster planning axes; managed vs self-hosted; bootstrap tooling (kubeadm, minikube, kind, k3s); **the three API access gates** (authentication → authorization → admission); auditing; ResourceQuota and LimitRange; node lifecycle (cordon/drain/uncordon, node conditions, leases); semantic versioning; supported releases; **version skew**; release cadence; etcd backup
- **Prerequisites**: Ch 3 (control plane), Ch 4 (objects, namespaces), Ch 7 (nodes as scheduling targets)
- **Target length**: Content-driven, no word target. **Depth band: standard** — 5 points, but four unrelated conceptual arcs
- **Retrieval targets**: **20%** **[B3]**, from Ch 3–7, **with the ≥4-back spacing floor now active** — at least one item must come from Ch 2–4. Anchors: the OCI/CRI boundary (Ch 2) or the control loop (Ch 3) as the ≥4-back item; namespaces (Ch 4) under ResourceQuota; node conditions against scheduling (Ch 7)
- **Key concepts introduced**: The kubectl verb-resource grammar; **the three gates in order** — authn, then authz, then admission; the version-skew window and the three-supported-minors rule; cordon vs drain; ResourceQuota (namespace total) vs LimitRange (per-object default)
- **Required figures (anchor stubs)**: `ch08-fig01-kubectl-verb-resource-grammar`, `ch08-fig02-three-api-gates`, `ch08-fig03-version-skew-window`, `ch08-fig04-node-lifecycle-cordon-drain`, `ch08-fig05-quota-vs-limitrange`, `ch08-zenith-consequences-not-rules`
- **Question budget**: 8 Soundings · **12–15 Bearings** (three checkpoints — four unrelated arcs) · 17 Practice · **37–40 total**
- **Notes**: Blocking gaps G1 (kubectl command surface), G26 (node lifecycle), G27 (etcd backup), G28 (bootstrap tooling). **[B3] The book's worst decay problem lives here.** The version-skew block is the densest pure-recall material in the book, taught at the 40% mark and otherwise never revisited before exam day. The fix is scheduled and non-negotiable: **version skew is retrieved in Ch 13** (as a troubleshooting cause) and **release cadence in Ch 17** (where the three-supported-minors rule and the ~3/year cadence explain each other). The admission gate is retrieved in Ch 12 (Pod Security Admission).

---

### Chapter 9 — Every Pod Has an Address

- **Subtitle**: *"Flat networks, stable names, and the abstraction that makes churn survivable"*
- **Purpose**: domain — D2.1 Container orchestration / networking (chapter_type: `content`)
- **Covers**: **D2.1** — the Kubernetes network model; Pod IP and shared namespace; CNI; Service; ClusterIP; NodePort; LoadBalancer; ExternalName; headless Services; Services without selectors; EndpointSlice; the service proxy; kube-proxy modes; CoreDNS; Service and Pod DNS records; FQDN
- **Prerequisites**: Ch 4 (labels, selectors), Ch 5 (Pod network namespace), Ch 6 (Pod churn under controllers)
- **Target length**: Content-driven, no word target. **Depth band: substantial** — 7 points, largest and most prerequisite-hungry of D2's competencies
- **Retrieval targets**: **20%** **[B3]**, from Ch 5–8, ≥4-back floor satisfied by Ch 5 (Pod shared network namespace — exactly four back). Additional anchors: selectors (Ch 4) now joining Service→Pod; ReplicaSet churn (Ch 6) as the reason a stable name is needed
- **Key concepts introduced**: The four rules of the flat network model; the Service-type ladder (ClusterIP → NodePort → LoadBalancer) as strictly additive layers; EndpointSlice as the selector's output; headless Services and when a stable name is *not* wanted; the DNS record shapes for Services and Pods
- **Required figures (anchor stubs)**: `ch09-fig01-network-model-four-rules`, `ch09-fig02-service-types-ladder`, `ch09-fig03-service-endpointslice-selector-path`, `ch09-fig04-kube-proxy-modes`, `ch09-fig05-dns-record-shapes`, `ch09-zenith-stable-name-over-churn`
- **Question budget**: 8 Soundings · 10 Bearings · 21 Practice · **39 total**
- **Notes**: Blocking gaps G11 (CNI), G13 (CoreDNS, DNS for Services and Pods), G24 (kube-proxy modes). CNI planted here is the second of the four pluggable interfaces resolving in Ch 17.

---

### Chapter 10 — Traffic from Beyond the Cluster

- **Subtitle**: *"Ingress is frozen, Gateway is the future, and neither does anything without a controller"*
- **Purpose**: domain — D2.1 (+ D2.2 boundary) / external exposure and network policy (chapter_type: `content`)
- **Covers**: **D2.1** — Ingress; Ingress controllers; TLS termination; name-based virtual hosting; simple fanout; edge router; the Ingress freeze and the Gateway recommendation; Gateway API (GatewayClass / Gateway / HTTPRoute, role-oriented design, request flow); NetworkPolicy (ingress and egress isolation, selectors, ipBlock, additive semantics, plugin dependency, the out-of-scope list)
- **Prerequisites**: Ch 9 — Service, ClusterIP, LoadBalancer, DNS
- **Target length**: Content-driven, no word target. **Depth band: standard** — 5 points
- **Retrieval targets**: **20%** **[B3]**, from Ch 6–9, ≥4-back floor satisfied by Ch 4 (labels/selectors, now selecting NetworkPolicy subjects) or Ch 5 (Pod IP). Additional anchor: the Service-type ladder (Ch 9) against what Ingress actually replaces
- **Key concepts introduced**: Ingress as L7 routing in front of Services, not a Service type; **frozen ≠ deprecated** — one of the most precise facts in the curriculum; the Gateway API role split (infrastructure / cluster operator / application developer); NetworkPolicy as **additive allow-only with no deny rule**, and that it does nothing on a CNI that doesn't implement it
- **Required figures (anchor stubs)**: `ch10-fig01-ingress-vs-service-loadbalancer`, `ch10-fig02-ingress-fanout-and-name-based-hosts`, `ch10-fig03-gateway-api-role-split`, `ch10-fig04-networkpolicy-additive-selectors`, `ch10-zenith-nothing-without-a-controller`
- **Question budget**: 8 Soundings · 10 Bearings · 17 Practice · **35 total**
- **Notes**: Blocking gap G25 (Gateway API detail). **NetworkPolicy is taught once, here** — Ch 12 cross-bears in rather than duplicating. `ch10-zenith` is the named home of cross-cutting theme #3, "the object exists but nothing happens without the component"; name the pattern here so Ch 13 and Ch 17 can retrieve it by name.

---

### Chapter 11 — Below the Waterline

- **Subtitle**: *"Storage outlives the Pod that asked for it"*
- **Purpose**: domain — D2.4 Container orchestration / storage (chapter_type: `content`)
- **Covers**: **D2.4** — volume types (emptyDir, hostPath, configMap/secret, projected, ephemeral); PersistentVolume; PersistentVolumeClaim; StorageClass; static vs dynamic provisioning; binding; reclaim policies (Retain/Delete/Recycle); access modes (RWO/ROX/RWX/RWOP); CSI; StatefulSet + PV pairing (loop closed from Ch 6)
- **Prerequisites**: Ch 4 (objects, ConfigMap/Secret as volume sources), Ch 5 (Pod volumes), Ch 6 (StatefulSet, introduced)
- **Target length**: Content-driven, no word target. **Depth band: standard** — 5 points
- **Retrieval targets**: **20%** **[B3]**, from Ch 6–10, ≥4-back floor satisfied by Ch 6 (StatefulSet — five back) and Ch 5 (Pod volume mounts). Additional anchor: ConfigMap/Secret (Ch 4) as volume types the reader already met as objects
- **Key concepts introduced**: The volume lifetime ladder (container → Pod → cluster); the PV/PVC/StorageClass triangle and who creates what; static vs dynamic provisioning; access modes as node-count semantics, not permission semantics; reclaim policy as what happens *after* the claim is gone
- **Required figures (anchor stubs)**: `ch11-fig01-volume-lifetime-ladder`, `ch11-fig02-pv-pvc-storageclass-binding`, `ch11-fig03-static-vs-dynamic-provisioning`, `ch11-fig04-access-modes-and-reclaim-policies`, `ch11-fig05-statefulset-pvc-pairing`, `ch11-zenith-outliving-the-pod`
- **Question budget**: 8 Soundings · 10 Bearings · 17 Practice · **35 total**
- **Notes**: Blocking gaps G11 (CSI), G12 (volume types other than PV/PVC). **Closes the book's one deliberate forward reference** — `ch11-fig05` is the back half of the Ch 6 StatefulSet cross-bearing and must be built as a reciprocal pair with `ch06-fig05`. CSI planted here is the third pluggable interface resolving in Ch 17.

---

### Chapter 12 — Locks, Keys, and Watchstanders

- **Subtitle**: *"RBAC has no deny rule, and Secrets aren't encrypted"*
- **Purpose**: domain — D2.2 Container orchestration / security (chapter_type: `content`)
- **Covers**: **D2.2** — the cloud native security lifecycle phases (develop / distribute / deploy / runtime) and the 4Cs framing; RBAC (Role, ClusterRole, RoleBinding, ClusterRoleBinding, additive permissions, binding immutability, default roles); ServiceAccounts and TokenRequest; Secret types and hardening; encryption at rest; Pod Security Standards and Pod Security Admission; `securityContext`; supply-chain security (scanning, signing, SBOM, in-toto, TUF, Harbor); policy engines (OPA, Kyverno, Falco); sandboxed runtimes
- **Prerequisites**: Ch 4 (namespaces, namespaced vs cluster-scoped, Secrets), Ch 5 (ServiceAccount as Pod identity, planted), Ch 8 (the admission gate), Ch 10 (NetworkPolicy)
- **Target length**: Content-driven, no word target. **Depth band: substantial** — 7 points, and a synthesis chapter in disguise with seven distinct arcs
- **Retrieval targets**: **20%** **[B3]**, from Ch 7–11, ≥4-back floor satisfied by Ch 4 (namespaced vs cluster-scoped) and Ch 8 (admission gate). Additional anchors: NetworkPolicy (Ch 10) cross-beared as the network half of the security story; ServiceAccount (Ch 5) collected from its planting
- **Key concepts introduced**: The 4Cs and the four lifecycle phases; **RBAC as additive-only with no deny rule**; the four-way Role/Binding matrix *derived* from Ch 4's namespaced/cluster-scoped boundary; ServiceAccount → token → API identity; Secrets are base64, not encrypted, and what encryption at rest actually adds; the three Pod Security Standard levels and the three admission modes
- **Required figures (anchor stubs)**: `ch12-fig01-4cs-and-lifecycle-phases`, `ch12-fig02-rbac-four-way-matrix`, `ch12-fig03-serviceaccount-token-flow`, `ch12-fig04-pod-security-standards-levels`, `ch12-fig05-supply-chain-checkpoints`, `ch12-zenith-additive-never-deny`
- **Question budget**: 8 Soundings · **12–15 Bearings** (three checkpoints) · 21 Practice · **41–44 total**
- **Notes**: Blocking gaps G5 (PSS/PSA, `securityContext`), G6 (4Cs), G7, G22 (supply chain), G23 (policy engines). **[B3]** `ch12-fig02` must be *derived* from `ch04-fig04`, not presented as a memorization table — this is the payoff for cross-cutting theme #2. Pair `ch12-zenith` with Ch 10's NetworkPolicy additive semantics: two systems, one rule, no deny.

---

### Chapter 13 — When the Cluster Won't Answer

- **Subtitle**: *"Read the phase before you read the logs"*
- **Purpose**: domain — D2.3 Container orchestration / troubleshooting, platform scope (chapter_type: `content`)
- **Covers**: **D2.3** — the two-audience split; Pod failure signatures (Pending, CrashLoopBackOff, ImagePullBackOff, ErrImagePull, OOMKilled, Evicted, CreateContainerConfigError); events; `kubectl describe` / `events` / `logs --previous`; node health and conditions; crictl; the resource metrics pipeline and metrics-server; `kubectl top`; cluster log architecture; known issues
- **Prerequisites**: Ch 5 (Pod phases, container states, requests/limits), Ch 7 (scheduling failure), Ch 9 (Service/DNS resolution), Ch 11 (volume mount failure)
- **Target length**: Content-driven, no word target. **Depth band: focused** — 4 points, but unusually high retrieval load; the chapter is mostly *applied* prior material
- **Retrieval targets**: **25% — ceiling** **[B3]**, from all previous. Retrieval *is* this chapter's method, not a tax on it. Mandatory named anchors: **version skew (Ch 8) as a troubleshooting cause** — the primary fix for the Ch 8 decay problem; **Pending → scheduling filters and taints (Ch 7)** — the primary fix for the Ch 7 decay problem; OOMKilled/Evicted → requests and limits (Ch 5); ImagePullBackOff → `imagePullPolicy`, tags vs digests, registry auth (Ch 2); phase vs container state (Ch 5); `kubectl top` → metrics-server as an instance of "nothing happens without the component" (Ch 10, by name)
- **Key concepts introduced**: The two-audience split (platform scope vs application scope); the failure-signature map as a lookup from symptom to cause; **read the phase before the logs**; events as the first-class diagnostic surface; the resource metrics pipeline and why `kubectl top` fails on a bare cluster
- **Required figures (anchor stubs)**: `ch13-fig01-two-audience-split`, `ch13-fig02-pod-failure-signature-map`, `ch13-fig03-phase-before-logs-flow`, `ch13-fig04-metrics-pipeline-and-metrics-server`, `ch13-zenith-read-the-phase-first`
- **Question budget**: 8 Soundings · 10 Bearings · 15 Practice · **33 total**
- **Notes**: Blocking gaps G1 and **G2 (Pod failure signatures by name — B1's highest-risk single gap)**. Opens the two-chapter troubleshooting arc; closes by handing off to Ch 16 ("if the platform is healthy and your app still isn't"). `ch13-fig04` is retrieved twice — Ch 17 (metrics-server as autoscaler input) and Ch 18 (metrics pipeline vs monitoring).

---

### Chapter 14 — Packing for the Voyage

- **Subtitle**: *"A chart is not a release, and templates are not the point"*
- **Purpose**: domain — D3.1 Cloud native application delivery / packaging (chapter_type: `content`)
- **Covers**: **D3.1** — from raw manifests to packages; Helm (chart structure, `Chart.yaml`, `values.yaml`, `templates/`, `charts/`, `crds/`, chart repositories, releases, upgrade and rollback); Kustomize (base and overlay); when each fits; CRDs shipped as chart content
- **Prerequisites**: Ch 4 (manifests, `kubectl apply`), Ch 6 (workload resources, rollback)
- **Target length**: Content-driven, no word target. **Depth band: standard** — 5 points
- **Retrieval targets**: **20%** **[B3]**, from Ch 9–13, ≥4-back floor satisfied by Ch 4 (object anatomy, `apply`) and Ch 6 (workload resources, revision/rollback). Additional anchor: Ch 6 rollback vs Helm rollback — different mechanisms, same word
- **Key concepts introduced**: Package vs manifest vs release vs revision — four words readers routinely collapse into one; Helm chart anatomy; templating as a means, not the point; Kustomize base/overlay as the no-templating alternative; why CRDs get their own chart directory
- **Required figures (anchor stubs)**: `ch14-fig01-manifest-to-package-progression`, `ch14-fig02-helm-chart-anatomy`, `ch14-fig03-release-vs-chart-vs-revision`, `ch14-fig04-kustomize-base-overlay`, `ch14-zenith-package-not-template`
- **Question budget**: 8 Soundings · 10 Bearings · 17 Practice · **35 total**
- **Notes**: Blocking gap G19 (Kustomize). **[B3] Decay risk — thin downstream presence.** Named anchors are mandatory in **Ch 15** (Argo CD's manifest sources include Helm charts — the reason Helm is taught first) and **Ch 17** (CRDs shipped as chart content, feeding the operator/extensibility synthesis).

---

### Chapter 15 — The Chart Is the Truth

- **Subtitle**: *"GitOps is the control loop you already learned, pointed at a repository"*
- **Purpose**: domain — D3.1 Cloud native application delivery / GitOps and delivery (chapter_type: `content`)
- **Covers**: **D3.1** — the twelve-factor app; deployment strategies (rolling, Recreate, blue/green, canary, A/B); CI/CD vs GitOps; the four OpenGitOps principles; Argo CD (controller model, Git as source of truth, OutOfSync, sync, tracking branches/tags/commits, PreSync/Sync/PostSync hooks, drift detection, rollback); Flux; multi-cluster delivery
- **Prerequisites**: Ch 3 (the control loop), Ch 6 (controllers, rolling update mechanics), Ch 14 (Helm charts as a manifest source)
- **Target length**: Content-driven, no word target. **Depth band: substantial** — 7 points, and it carries the book's primary Zenith
- **Retrieval targets**: **25% — ceiling** **[B3]**, from all previous. ≥4-back floor satisfied several times over. Mandatory anchors: **the control loop (Ch 3)** — the retrieval that *is* the Zenith; rolling-update mechanics (Ch 6) now given strategy vocabulary; Helm charts (Ch 14) as Argo's input; ConfigMap/Secret (Ch 4) as twelve-factor factor III; drift detection against `spec`/`status` (Ch 4)
- **Key concepts introduced**: The twelve factors that actually matter in Kubernetes; the strategy vocabulary (blue/green, canary, A/B) attached to Argo's sync hooks that give it mechanism; **push CI/CD vs pull GitOps**; the four OpenGitOps principles as a restatement of reconciliation; OutOfSync as `status ≠ spec` where spec lives in Git
- **Required figures (anchor stubs)**: `ch15-fig01-twelve-factor-in-kubernetes`, `ch15-fig02-deployment-strategies-compared`, `ch15-fig03-cicd-push-vs-gitops-pull`, `ch15-fig04-argocd-sync-states-and-hooks`, `ch15-fig05-opengitops-four-principles`, `ch15-zenith-control-loop-pointed-at-a-repo`
- **Question budget**: 8 Soundings · 10 Bearings · 21 Practice · **39 total**
- **Notes**: Blocking gaps G9 (deployment strategy vocabulary), G18 (Flux). **PRIMARY ZENITH.** `ch15-zenith` must visually re-present `ch03-fig02` with Git substituted for etcd as the desired-state store — the recognition is the payoff, and it fails if the two figures don't rhyme. This is the strongest synthesis opportunity in the book and the reason Part IV is ordered packaging → delivery → debugging.

---

### Chapter 16 — Your Application, Their Cluster

- **Subtitle**: *"Four questions that separate 'my code is broken' from 'the platform is broken'"*
- **Purpose**: domain — D3.2 Cloud native application delivery / debugging, application scope (chapter_type: `content`)
- **Covers**: **D3.2** — the application-scope triage flow; `kubectl debug` and ephemeral containers; init-container debugging; `exec`; `port-forward`; debugging Services and StatefulSets from the application side; local development and debugging; the handoff boundary with Ch 13
- **Prerequisites**: Ch 5 (Pod, init containers, probes), Ch 9 (Service, DNS), Ch 13 (platform-scope triage, the handoff)
- **Target length**: Content-driven, no word target. **Depth band: focused** — 4 points, high retrieval load
- **Retrieval targets**: **25% — ceiling** **[B3]**, from all previous. Mandatory anchors: the Ch 13 handoff, retrieved as the chapter's opening move; Pod phases and probes (Ch 5); Service→EndpointSlice→Pod path (Ch 9) as the "is my Service even selecting anything" check; StatefulSet identity (Ch 6) and its PVC pairing (Ch 11)
- **Key concepts introduced**: The four triage questions; ephemeral containers and why you cannot just add a container to a running Pod; `port-forward` as a diagnostic that deliberately bypasses the Service path; the scope boundary — what is yours to fix and what is the platform's
- **Required figures (anchor stubs)**: `ch16-fig01-application-scope-triage`, `ch16-fig02-ephemeral-container-debug`, `ch16-fig03-portforward-vs-service-path`, `ch16-zenith-mine-or-the-platforms`
- **Question budget**: 8 Soundings · 10 Bearings · 15 Practice · **33 total**
- **Notes**: Blocking gaps G1, G2. Closes the two-chapter troubleshooting arc opened in Ch 13. **Build the reciprocal cross-bearings deliberately** — Ch 13 hands off, Ch 16 opens by handing back. B1 sequencing implication #7: the exam splits these across domains, the reader's mental model must not be split.

---

### Chapter 17 — The Fleet and Its Charts

- **Subtitle**: *"Meshes, functions, autoscalers, and the foundation that keeps the map"*
- **Purpose**: domain — D4.2 + D4.3 Cloud native architecture, community and collaboration (chapter_type: `content`)
- **Covers**: **D4.2 + D4.3** — the CNCF cloud native definition v1.1 and its characteristics; loose coupling; microservices; immutable infrastructure; declarative APIs; **the extension-points synthesis** (CRI/CNI/CSI, CRDs, API aggregation, admission webhooks, device plugins, operators); service mesh (data vs control plane, Envoy, mTLS and zero trust, sidecar vs ambient); serverless and Knative (Serving, Eventing, Functions, scale to zero); the autoscaling landscape (VPA, KEDA, Cluster Autoscaler, Karpenter); CNCF maturity levels; the graduated roster as dated data; the CNCF Landscape; Governing Board / TOC / TAGs / End User TAB; Kubernetes SIGs / Working Groups / Committees / Steering; the contributor ladder; KEPs; release cadence; KubeCon; the Code of Conduct; the CNCF certification ladder
- **Prerequisites**: Ch 2 (CRI), Ch 6 (CRDs, operator pattern, HPA concept), Ch 9 (CNI), Ch 12 (mTLS, zero trust, policy engines), Ch 14 (charts as operator delivery), Ch 15 (declarative delivery)
- **Target length**: Content-driven, no word target. **Depth band: substantial** — 7 points, two competencies, six distinct arcs, and the secondary Zenith
- **Retrieval targets**: **25% — ceiling** **[B3]**, from all previous. Mandatory anchors: **CRI (Ch 2), CNI (Ch 9), CSI (Ch 11), CRDs (Ch 6)** — the four-way retrieval that *is* the secondary Zenith; **release cadence paired with version skew (Ch 8)** — the second fix for the Ch 8 decay problem, where the three-supported-minors rule and the ~3/year cadence explain each other; **unschedulable Pods (Ch 7)** as Cluster Autoscaler's trigger — the second fix for the Ch 7 decay problem; **metrics-server (Ch 13)** as HPA's input; **VPA not shipped by default** retrieved by name as "the object exists but nothing happens without the component" (Ch 10); Helm-delivered CRDs (Ch 14)
- **Key concepts introduced**: The CNCF cloud native definition and its named characteristics; extensibility as one story rather than four acronyms; mesh data plane vs control plane, and sidecar vs ambient; scale-to-zero; the autoscaler landscape and which axis each scales; **CNCF maturity levels** (Sandbox / Incubating / Graduated); CNCF and Kubernetes governance structures; the contributor ladder and KEPs
- **Required figures (anchor stubs)**: `ch17-fig01-cloud-native-definition-characteristics`, `ch17-fig02-extension-points-map`, `ch17-fig03-mesh-data-vs-control-plane`, `ch17-fig04-autoscaler-landscape`, `ch17-fig05-cncf-maturity-levels`, `ch17-fig06-cncf-and-k8s-governance`, `ch17-zenith-one-pluggability-story`
- **Question budget**: 8 Soundings · **12–15 Bearings** (three checkpoints) · 21 Practice · **41–44 total**
- **Notes**: Blocking gaps G10, G11, G14 (Kubernetes origin and history), G15 (CNCF Landscape), G16 (contributor ladder, KEPs, release cadence), G17 (Code of Conduct, events, participation paths), G31 (adjacent certifications), G32 (verify FinOps/cost is still in scope). **SECONDARY ZENITH** — `ch17-fig02` and `ch17-zenith` are the same synthesis at two altitudes; back-bear to all four interface chapters explicitly. **D4.3 gets its own numbered sections, its own Fixed Points, and its own Soundings coverage inside this chapter** — B1 warns it is the competency technically-strong candidates most reliably under-study, and the mitigation is explicit treatment rather than a separate chapter. **[B3] Do not retrieve the dated graduated-project roster; retrieve the maturity levels instead.**

---

### Chapter 18 — Reading the Instruments

- **Subtitle**: *"Four signals, one question: is the service doing what users expect?"*
- **Purpose**: domain — D4.1 Cloud native architecture / observability (chapter_type: `content`)
- **Covers**: **D4.1** — observability vs monitoring; unknown unknowns; instrumentation; telemetry; the four OpenTelemetry signals (traces, metrics, logs, baggage); spans and root spans; distributed tracing; Prometheus (pull model, time series, PromQL, exporters, Pushgateway, Alertmanager, client libraries, service discovery, fit and non-fit); metrics-server vs monitoring; logging architecture and node-level agents; Fluentd / Fluent Bit; Jaeger; Grafana; reliability; SLI; SLO; the golden signals
- **Prerequisites**: Ch 13 (the resource metrics pipeline, cluster log architecture), Ch 17 (microservices, service mesh — traces need a multi-service mental model)
- **Target length**: Content-driven, no word target. **Depth band: standard** — 5 points
- **Retrieval targets**: **25% — ceiling** **[B3]** — last content chapter, most accumulated decay, so the schedule closes at the ceiling. Draws from all previous. Mandatory anchors: **metrics-server vs a monitoring system (Ch 13)** — the distinction the exam actually tests; probes (Ch 5) as health-checking that is *not* observability; requests/limits (Ch 5) as the numbers metrics report against; mesh telemetry (Ch 17); node-level log agents as DaemonSets (Ch 6)
- **Key concepts introduced**: Observability vs monitoring, framed as unknown unknowns vs known unknowns; the four OpenTelemetry signals; spans, root spans, and trace propagation across services; the Prometheus **pull** model and where it does and does not fit; SLI vs SLO; the golden signals
- **Required figures (anchor stubs)**: `ch18-fig01-monitoring-vs-observability`, `ch18-fig02-otel-four-signals`, `ch18-fig03-trace-spans-across-services`, `ch18-fig04-prometheus-pull-architecture`, `ch18-fig05-sli-slo-golden-signals`, `ch18-zenith-instruments-answer-one-question`
- **Question budget**: 8 Soundings · 10 Bearings · 17 Practice · **35 total**
- **Notes**: Blocking gaps G20 (Grafana, Fluentd/Fluent Bit, Jaeger), G21 (golden signals, RED, USE). **Observability is no longer a standalone domain** in the 2025-11-24 blueprint — it sits inside D4 here. Readers arriving with pre-2025 material will expect an 8% standalone domain; say so. B1 sequencing implication #8: reversing Ch 17 and Ch 18 would make this material pure vocabulary drill.

---

### Chapter 19 — Bearings Before Landfall

- **Subtitle**: *"Everything that connects, and the traps that don't"*
- **Purpose**: synthesis (chapter_type: `synthesis`)
- **Covers**: No new objectives. Cross-domain integration map; the top confusion pairs; exam-day pacing; The Lodestar walkthrough; what to do the week before
- **Prerequisites**: Ch 2–18, all
- **Target length**: Content-driven, no word target. **Depth band: standard** — synthesis density, no new material
- **Retrieval targets**: **~100%** **[B3]** — the chapter is retrieval by definition. All nine cross-cutting themes are surfaced by name here, and every confusion pair from B1's trap inventory that survived to publication gets a discriminating question
- **Key concepts introduced**: None new. Reorganizes the book along the nine cross-cutting themes rather than along the four domains, so the reader sees the material a second time in a different shape
- **Required figures (anchor stubs)**: `ch19-fig01-cross-domain-integration-map`, `ch19-fig02-confusion-pair-matrix`, `ch19-fig03-exam-day-pacing`
- **Question budget**: 5 Soundings · 5 Bearings · 10 Practice (cross-domain by construction) · **20 total**
- **Notes**: Synthesis type — Soundings optional per the structural contract, but retained here at 5. **D4.3 gets disproportionate representation** per B2, compensating for its under-study risk. This chapter is where `the-lodestar.md` is walked through; the file itself is a book-level required artifact, not a chapter.

---

### Chapter 20 — Full Mock Exam

- **Subtitle**: *"Ninety minutes. No notes. Find out."*
- **Purpose**: synthesis / assessment (chapter_type: `mock_exam`)
- **Covers**: No new objectives. Full-length calibrated mock weighted to 44/28/16/12, with worked answers and a scoring rubric
- **Prerequisites**: Ch 2–18, all
- **Target length**: Content-driven, no word target. **Depth band: set by question count, not prose** — 60 questions plus full worked answers
- **Retrieval targets**: All domains, weighted. Not a spacing target — the mock is the terminal assessment
- **Key concepts introduced**: None
- **Required figures (anchor stubs)**: `ch20-fig01-score-rubric-bands`
- **Question budget**: 0 Soundings · 0 Bearings · **60 Practice** · **60 total**. Domain split: D1 26 · D2 17 · D3 10 · D4 7 (all within ±0.7 pp of published weights)
- **Notes**: `mock_exam` type — exempt from standard chapter structure, branded markers, and the Zenith requirement per the structural contract. **KCNA is multiple-choice, not performance-based** — the mock is a written instrument, not a task walkthrough. **[B3 / B2 disclosure #2] The 60-question size and the 90-minute budget are not equally sourced.** Ninety minutes is published by the Linux Foundation; 60 questions is *commonly reported* and must be framed as a calibrated instrument sized to the commonly reported format, never as a match to a published count. Neither the 60-question figure nor the 75% pass mark may be used as a retrieval target anywhere in the book. If gap G37 (the LFS250 syllabus fetch) surfaces an authoritative count, only this chapter's size changes — the domain proportions and the per-chapter budgets are independent of it.

---

## Cross-cutting retrieval themes

Nine themes are retrieved by name across the book. **[B3]** established the count and specified the first three; the remaining six are **[B5-reconstructed]** from B2's dependency graph and cross-bearing pairs, and should be reconciled if B3 is re-run.

| # | Theme | Chapter path | Source |
|---|---|---|---|
| 1 | **The control loop** — desired state, current state, reconciliation | 3 → 4 → 6 → 11 → 15 → 17 | **[B3]** |
| 2 | **Namespaced vs cluster-scoped** — *derives* the RBAC four-way matrix instead of memorizing it | 4 → 8 → 12 | **[B3]** |
| 3 | **"The object exists but nothing happens without the component"** — Ingress without a controller, NetworkPolicy on an unsupporting CNI, `kubectl top` without metrics-server, VPA not shipped by default | 10 → 13 → 17 | **[B3]** |
| 4 | **Declarative desired state vs imperative command** | 4 → 6 → 14 → 15 | [B5-reconstructed] |
| 5 | **Labels and selectors as the universal join** — ReplicaSet→Pod, Service→Pod, NetworkPolicy→Pod; and the contrast that RBAC uses subjects, not selectors | 4 → 6 → 7 → 9 → 10 → 12 | [B5-reconstructed] |
| 6 | **Pluggable interfaces** — CRI, CNI, CSI, CRDs as one extensibility story | 2 → 9 → 11 → 6 → 17 | [B5-reconstructed] |
| 7 | **Identity** — ServiceAccount as the thread from Pod to API to delivery agent | 5 → 12 → 15 | [B5-reconstructed] |
| 8 | **Requests and limits** — the numbers that reappear everywhere | 5 → 7 → 13 → 17 → 18 | [B5-reconstructed] |
| 9 | **Additive, allow-only, no deny** — RBAC and NetworkPolicy share one semantic | 10 → 12 | [B5-reconstructed] |

Theme 3 is a *pattern*, not a fact. **[B3]** Name it once in Ch 10 and retrieve it by name afterward; that converts four separate gotchas into one rule.

### Do not retrieve **[B3]**

Four things are excluded from the retrieval schedule entirely:

1. **Ch 1 exam mechanics.** No item anywhere tests them.
2. **The dated graduated-project roster.** Retrieve the maturity *levels* instead — the roster changes between printing and exam day.
3. **The 60-question and 75% figures.** Unpublished and commonly-reported; retrieving them would teach them as fact.
4. **Any `[inferred]` trap framed as exam frequency.** Fourteen of B1's 114 traps are `[inferred]` rather than `[source]`. Those may be described as "easy to confuse," never "frequently tested" — Ethical Guardrail #8.

---

## Cross-chapter callback map

Retrieval percentage per chapter, with source range and the mandatory named anchors. Percentages are **[B3]**; the ≥4-back column enforces B3's spacing floor, active from Ch 8 onward.

| Ch | % | Draws from | Mandatory named anchors | ≥4-back item |
|---|---|---|---|---|
| 1 | — | — | *excluded from schedule* | — |
| 2 | — | — | *first content chapter* | — |
| 3 | 10% | 2 | CRI boundary; image immutability | n/a |
| 4 | 15% | 2–3 | Control loop; apiserver in `apply` | n/a |
| 5 | 20% | 2–4 | `imagePullPolicy`; spec/status vs Pod phase | n/a |
| 6 | 20% | 3–5 | Control loop → named controller; selectors; probes | n/a |
| 7 | 20% | 4–6 | Node labels; requests as filter input | n/a |
| 8 | 20% | 3–7 | Namespaces under ResourceQuota; node conditions | **Ch 2 CRI or Ch 3 control loop** |
| 9 | 20% | 5–8 | Selectors → Service; controller churn | **Ch 5 Pod network namespace** |
| 10 | 20% | 6–9 | Service-type ladder; what Ingress replaces | **Ch 4 labels/selectors** |
| 11 | 20% | 6–10 | StatefulSet loop closed; ConfigMap/Secret as volumes | **Ch 5 Pod volumes / Ch 6 StatefulSet** |
| 12 | 20% | 7–11 | NetworkPolicy cross-beared; ServiceAccount collected | **Ch 4 namespaced/cluster-scoped; Ch 8 admission gate** |
| 13 | **25%** | all | **Version skew (Ch 8)**; **Pending → scheduling (Ch 7)**; OOMKilled → limits (Ch 5); ImagePullBackOff (Ch 2); `kubectl top` → theme 3 | Ch 2, 5, 7, 8 |
| 14 | 20% | 9–13 | Ch 6 rollback vs Helm rollback | **Ch 4 `apply`; Ch 6 workload resources** |
| 15 | **25%** | all | **Control loop (Ch 3) — the Zenith**; rolling-update mechanics (Ch 6); Helm as Argo input (Ch 14); ConfigMap/Secret as factor III (Ch 4) | Ch 3, 4, 6 |
| 16 | **25%** | all | Ch 13 handoff; Pod phases (Ch 5); Service→EndpointSlice (Ch 9); StatefulSet+PVC (Ch 6, 11) | Ch 5, 6, 9 |
| 17 | **25%** | all | **CRI/CNI/CSI/CRDs (2, 9, 11, 6) — the Zenith**; **release cadence + version skew (Ch 8)**; **unschedulable → CA (Ch 7)**; metrics-server (Ch 13); VPA → theme 3 | Ch 2, 6, 7, 8, 9, 11 |
| 18 | **25%** | all | metrics-server vs monitoring (Ch 13); probes ≠ observability (Ch 5); log agents as DaemonSets (Ch 6); mesh telemetry (Ch 17) | Ch 5, 6, 13 |
| 19 | ~100% | all | All nine themes by name; every surviving confusion pair | all |
| 20 | weighted | all | Terminal assessment | all |

### Reciprocal cross-bearing pairs to build deliberately

Six pairs must be built as pairs — each half written knowing the other exists, per B2:

| Pair | Relationship |
|---|---|
| Ch 6 ↔ Ch 11 | StatefulSet introduced / PV pairing completed — the book's one deliberate forward reference |
| Ch 10 ↔ Ch 12 | NetworkPolicy taught once in Ch 10; Ch 12 cross-bears in as the network half of security |
| Ch 13 ↔ Ch 16 | Troubleshooting handoff — platform scope hands off, application scope hands back |
| Ch 4 → Ch 15 | ConfigMap/Secret as twelve-factor factor III |
| Ch 3 → Ch 6 → Ch 15 | The control-loop spine, three beats |
| Ch 13 → Ch 17 and Ch 13 → Ch 18 | metrics-server as autoscaler input; metrics pipeline vs monitoring |

### Decay fixes — do not drop

Three chapters teach dense material that is otherwise never revisited. **[B3]** identified these and placed the anchors; drafting must honor them.

| At risk | Why | Where it is retrieved |
|---|---|---|
| **Ch 8 version skew** | Densest pure-recall block in the book, taught at the 40% mark | Ch 13 (as a troubleshooting cause) **and** Ch 17 (release cadence + three-supported-minors, which explain each other) |
| **Ch 7 scheduling** | Thin downstream presence | Ch 13 (Pending as a scheduling-failure signature) **and** Ch 17 (Cluster Autoscaler reacting to unschedulable Pods) |
| **Ch 14 Helm** | Thin downstream presence | Ch 15 (charts as Argo's manifest source) **and** Ch 17 (CRDs shipped as chart content) |

### Soundings do the spacing work for free **[B3]**

Soundings are **excluded from the retrieval budget** but perform retrieval anyway. Skill Part 11 requires Soundings questions be answerable from prerequisites — which in this book *means earlier chapters*. Counting them against the 20–25% target would distort their calibration purpose. **The drafting instruction is therefore: source each chapter's Soundings from B2's Prerequisites column**, which makes every Soundings block a spaced retrieval event at no cost to the schedule.

---

## Open items carried into drafting

1. **Re-run B3 or accept the reconstruction.** Six of nine cross-cutting themes here are B5-reconstructed. They are defensible, but they are not B3's list.
2. **Fetch the LFS250 syllabus (G37) before anything else.** It is the closest artifact to a detailed CNCF objective list. If it changes the weighting, the per-chapter percentages in B2 — and therefore every Practice Qs figure in B4 and every depth band here — should be revised before drafting. The chapter *sequence* is dependency-driven and would not change.
3. **Seventeen blocking gaps remain open**, routed per chapter in B2 § "Gap routing." Highest-risk single gap is **G2** (Pod failure signatures by name), which gates Ch 13 and Ch 16.
4. **B4 flagged a skill defect.** Part 8's practice-question formula returns a negative pool (−86) for this book, because fixed baselines alone (326) exceed `300 − mock_size`. It should be restated as a floor-check plus a weight-proportional allocation. KCNA is the first book in the catalog to trip it; any book with ≥13 content chapters and a mock under ~100 questions will trip it too.
5. **Diagram enforcement is off** for this book (`diagram_enforcement.enabled: false`). The figure anchors above are stubs for the Stage 10 image-spec extraction and the sibling `certcomp-diagrams` pipeline; flip the gate only after that book's diagram retro completes.

---

## Handoff to chapter pipeline

This arc outline is the authoritative input to `python pipeline/orchestrator.py --run --book kcna --chapter N`. Each chapter's planning stage (stage 1) reads this file and expands its chapter entry into a full outline with section plan.

Stage 1 consumes, per chapter: **Covers** (objective mapping), **Prerequisites** (both the chapter refs and the named concepts), **Key concepts introduced** (Fixed Point candidates), **Retrieval targets** (the spacing contract — percentage *and* named anchors, both binding), **Required figures** (anchor stubs, to be expanded into `yaml-figure-spec` blocks at Stage 10), and **Question budget** (Soundings / Bearings / Practice, where Bearings is a minimum to exceed).

Stage 1 must **not** derive a word target from the **Target length** field. The depth band is a relative planning signal only; word budgets were retired 2026-04-24 and no downstream stage enforces them.