# Chapter Lineup — KCNA

**Book:** Kubernetes and Cloud Native Associate
**Exam:** KCNA (CNCF / The Linux Foundation), curriculum effective 2025-11-24
**Stage:** B2 — Chapter Lineup
**Date:** 2026-08-23
**Input:** Stage B1 domain analysis (4 domains, 12 competencies, 114 traps, 37 gaps)

**Shape:** 20 chapters — 1 orientation, **17 content chapters** carrying 100% of exam weight, 1 synthesis, 1 mock exam.

Objective identifiers (`D1.1`, `D2.3`, …) are the **Lodestar convention established in B1**. CNCF publishes four domains and twelve named competencies with no numbering and no sub-weights (B1 §G33, §G36). Per-chapter weight figures below are **authored judgment**, not published data, and must be disclosed as such in front matter.

---

## Part structure

| Part | Theme | Chapters | Exam domain(s) | Weight |
|---|---|---|---|---|
| **I — Taking Departure** | What KCNA is, what changed, and how to read this book | 1 | — (orientation) | 0% |
| **II — Ship, Cargo, and Company** | Containers, the cluster, the objects that describe it, and the components that run it | 2–8 | D1 Kubernetes Fundamentals | **44%** |
| **III — Underway** | Keeping workloads reachable, stored, secured, and diagnosable | 9–13 | D2 Container Orchestration | **28%** |
| **IV — Dispatches** | Getting software from a repository into a cluster, and finding out why it didn't work | 14–16 | D3 Cloud Native Application Delivery | **16%** |
| **V — The Wider Sea** | The patterns, the foundation, and the instruments | 17–18 | D4 Cloud Native Architecture | **12%** |
| **VI — Making Port** | Synthesis, exam-day strategy, and the full mock | 19–20 | — (synthesis / assessment) | 0% |

Content-chapter distribution: D1 **7 of 17 (41.2%)** · D2 **5 (29.4%)** · D3 **3 (17.6%)** · D4 **2 (11.8%)**. Target: 44 / 28 / 16 / 12. Maximum count deviation: 2.8 points.

---

## Chapters

| # | Title (working) | Subtitle (working) | Part | Covers objectives | Prerequisites | Exam weight % |
|---|---|---|---|---|---|---|
| 1 | Taking Departure | *"Ninety minutes, four domains, and a curriculum that moved under everyone's feet"* | I | — (exam mechanics; cloud native framing planted for Ch 17) | — | 0 |
| 2 | Cargo in Standard Crates | *"Why the shipping container beat the ship"* | II | **D1.4** — containers vs VMs, images, layers, tags vs digests, registries, `imagePullPolicy`, immutability, OCI runtime/image/distribution specs, runC, CRI, containerd, CRI-O, RuntimeClass, build practices | — | 9 |
| 3 | The Ship's Company | *"Everyone aboard has one job, and none of them is 'be in charge'"* | II | **D1.1** — deployment eras, what Kubernetes is and is not, control-plane components, node components, addons, controllers, the control loop, desired vs current state, Kubernetes origin and history | 2 | 6 |
| 4 | Records of Intent | *"You don't give Kubernetes orders. You file a declaration."* | II | **D1.1** — objects, spec/status, manifests, `apiVersion`/`kind`/`metadata`/`spec`, `kubectl apply`, labels, selectors (equality and set-based), annotations, namespaces, initial namespaces, namespaced vs cluster-scoped, ConfigMaps, Secrets (definition and contrast) | 3 | 6 |
| 5 | The Smallest Vessel | *"A Pod is not a container, and that distinction is worth points"* | II | **D1.1** — Pod concept and network namespace, multi-container and init containers, Pod phases, container states, `restartPolicy`, restart backoff, liveness/readiness/startup probes, probe mechanisms, resource requests and limits, QoS classes, ServiceAccount as Pod identity (planted) | 2, 4 | 7 |
| 6 | Fleets, Not Vessels | *"Nobody sails one Pod"* | II | **D1.1** — ReplicaSet, Deployment, rolling update, `maxSurge`/`maxUnavailable`, Recreate, revisions, rollout history, rollback, pause/resume, StatefulSet (introduced with siblings), DaemonSet, Job, CronJob, `kubectl scale`, HPA concept, custom resources and the operator pattern (definition) | 4, 5 | 6 |
| 7 | Assigning the Berth | *"Filter, score, bind — and then a coin flip"* | II | **D1.3** — scheduling overview, feasible nodes, filtering, scoring, binding, random tie-break, unschedulable Pods, node labels, `nodeSelector`, node affinity (required vs preferred), pod affinity/anti-affinity, taints and tolerations (NoSchedule / PreferNoSchedule / NoExecute), `nodeName`, topology spread, scheduling policies vs profiles | 5, 6 | 5 |
| 8 | Standing the Watch | *"The commands you'll actually type, and the versions that will bite you"* | II | **D1.2** — kubectl syntax and verbs, kubeconfig, in-cluster auth, cluster planning axes, managed vs self-hosted, bootstrap tooling (kubeadm, minikube, kind, k3s), API access gates (authentication → authorization → admission), auditing, ResourceQuota and LimitRange, node lifecycle (cordon/drain/uncordon, node conditions, leases), semantic versioning, supported releases, version skew, release cadence, etcd backup | 3, 4, 7 | 5 |
| 9 | Every Pod Has an Address | *"Flat networks, stable names, and the abstraction that makes churn survivable"* | III | **D2.1** — the Kubernetes network model, Pod IP and shared namespace, CNI, Service, ClusterIP, NodePort, LoadBalancer, ExternalName, headless Services, Services without selectors, EndpointSlice, service proxy, kube-proxy modes, CoreDNS, Service and Pod DNS records, FQDN | 4, 5, 6 | 7 |
| 10 | Traffic from Beyond the Cluster | *"Ingress is frozen, Gateway is the future, and neither does anything without a controller"* | III | **D2.1** (+ **D2.2** boundary) — Ingress, Ingress controllers, TLS termination, name-based virtual hosting, simple fanout, edge router, Ingress freeze and the Gateway recommendation, Gateway API (GatewayClass / Gateway / HTTPRoute, role-oriented design, request flow), NetworkPolicy (ingress and egress isolation, selectors, ipBlock, additive semantics, plugin dependency, out-of-scope list) | 9 | 5 |
| 11 | Below the Waterline | *"Storage outlives the Pod that asked for it"* | III | **D2.4** — volume types (emptyDir, hostPath, configMap/secret, projected, ephemeral), PersistentVolume, PersistentVolumeClaim, StorageClass, static vs dynamic provisioning, binding, reclaim policies (Retain/Delete/Recycle), access modes (RWO/ROX/RWX/RWOP), CSI, StatefulSet + PV pairing (loop closed from Ch 6) | 4, 5, 6 | 5 |
| 12 | Locks, Keys, and Watchstanders | *"RBAC has no deny rule, and Secrets aren't encrypted"* | III | **D2.2** — cloud native security lifecycle phases (develop/distribute/deploy/runtime) and the 4Cs framing, RBAC (Role, ClusterRole, RoleBinding, ClusterRoleBinding, additive permissions, binding immutability, default roles), ServiceAccounts and TokenRequest, Secret types and hardening, encryption at rest, Pod Security Standards and Pod Security Admission, `securityContext`, supply-chain security (scanning, signing, SBOM, in-toto, TUF, Harbor), policy engines (OPA, Kyverno, Falco), sandboxed runtimes | 4, 5, 8, 10 | 7 |
| 13 | When the Cluster Won't Answer | *"Read the phase before you read the logs"* | III | **D2.3** — the two-audience split, Pod failure signatures (Pending, CrashLoopBackOff, ImagePullBackOff, ErrImagePull, OOMKilled, Evicted, CreateContainerConfigError), events, `kubectl describe`/`events`/`logs --previous`, node health and conditions, crictl, the resource metrics pipeline and metrics-server, `kubectl top`, cluster log architecture, known issues | 5, 7, 9, 11 | 4 |
| 14 | Packing for the Voyage | *"A chart is not a release, and templates are not the point"* | IV | **D3.1** — from raw manifests to packages, Helm (chart structure, `Chart.yaml`, `values.yaml`, `templates/`, `charts/`, `crds/`, chart repositories, releases, upgrade and rollback), Kustomize (base and overlay), when each fits, CRDs shipped as chart content | 4, 6 | 5 |
| 15 | The Chart Is the Truth | *"GitOps is the control loop you already learned, pointed at a repository"* | IV | **D3.1** — the twelve-factor app, deployment strategies (rolling, Recreate, blue/green, canary, A/B), CI/CD vs GitOps, the four OpenGitOps principles, Argo CD (controller model, Git as source of truth, OutOfSync, sync, tracking branches/tags/commits, PreSync/Sync/PostSync hooks, drift detection, rollback), Flux, multi-cluster delivery | 3, 6, 14 | 7 |
| 16 | Your Application, Their Cluster | *"Four questions that separate 'my code is broken' from 'the platform is broken'"* | IV | **D3.2** — application-scope triage flow, `kubectl debug` and ephemeral containers, init-container debugging, `exec`, `port-forward`, debugging Services and StatefulSets from the application side, local development and debugging, handoff boundary with Ch 13 | 5, 9, 13 | 4 |
| 17 | The Fleet and Its Charts | *"Meshes, functions, autoscalers, and the foundation that keeps the map"* | V | **D4.2 + D4.3** — CNCF cloud native definition v1.1 and its characteristics, loose coupling, microservices, immutable infrastructure, declarative APIs, extension points synthesis (CRI/CNI/CSI, CRDs, API aggregation, admission webhooks, device plugins, operators), service mesh (data vs control plane, Envoy, mTLS and zero trust, sidecar vs ambient), serverless and Knative (Serving, Eventing, Functions, scale to zero), the autoscaling landscape (VPA, KEDA, Cluster Autoscaler, Karpenter), CNCF maturity levels, the graduated roster as dated data, the CNCF Landscape, Governing Board / TOC / TAGs / End User TAB, Kubernetes SIGs / Working Groups / Committees / Steering, contributor ladder, KEPs, release cadence, KubeCon, Code of Conduct, the CNCF certification ladder | 2, 6, 9, 12, 14, 15 | 7 |
| 18 | Reading the Instruments | *"Four signals, one question: is the service doing what users expect?"* | V | **D4.1** — observability vs monitoring, unknown unknowns, instrumentation, telemetry, the four OpenTelemetry signals (traces, metrics, logs, baggage), spans and root spans, distributed tracing, Prometheus (pull model, time series, PromQL, exporters, Pushgateway, Alertmanager, client libraries, service discovery, fit and non-fit), metrics-server vs monitoring, logging architecture and node-level agents, Fluentd/Fluent Bit, Jaeger, Grafana, reliability, SLI, SLO, golden signals | 13, 17 | 5 |
| 19 | Bearings Before Landfall | *"Everything that connects, and the traps that don't"* | VI | — (synthesis: cross-domain integration map, the top confusion pairs, exam-day pacing, The Lodestar walkthrough, what to do the week before) | 2–18 | 0 |
| 20 | Full Mock Exam | *"Ninety minutes. No notes. Find out."* | VI | — (assessment: full-length calibrated mock, weighted to 44/28/16/12, with worked answers and scoring rubric) | 2–18 | 0 |

**Weight check:** 9+6+6+7+6+5+5 = **44** (D1) · 7+5+5+7+4 = **28** (D2) · 5+7+4 = **16** (D3) · 7+5 = **12** (D4) · total **100**.

---

## Rationale

### Why this ordering?

The order is the B1 dependency graph walked from its deepest root outward, with one deliberate exception (below).

**Containerization goes first, not last.** B1 sequencing implication #1 is emphatic about this: D1.4 is only a quarter of the largest domain, but it is the deepest root in the graph. Nothing about images, immutability, or the CRI/OCI split can be inferred later, and the *reason* Kubernetes exists — the container deployment era — is the book's opening arousal beat. Books that treat OCI as ecosystem trivia and defer it to a back chapter force the reader to accept "container" as an undefined primitive for two hundred pages.

**Core Concepts is the trunk, so it gets four consecutive chapters (3–6).** The chain is cluster → objects → Pod → controllers, in that order, because each link is a hard prerequisite for the next. Chapter 3 introduces the control loop as the animating idea of the whole system; Chapter 6 instantiates it in the workload controllers; Chapter 15 generalizes it to a Git repository. That three-beat callback is the book's spine, and it only works if the beats land in that order.

**Scheduling (Ch 7) sits immediately after workloads** because it needs Pod, Node, and resource requests and nothing whatsoever from D2. Keeping it inside Part II preserves D1 as one contiguous arc rather than scattering the largest domain across the book.

**Administration (Ch 8) closes Part II** rather than opening it. `kubectl` is introduced operationally throughout Chapters 2–7 (you cannot teach objects without `kubectl apply`), but the full command surface, the three API access gates, node lifecycle, and version skew all read as arbitrary rules until the reader knows what a control plane, an object, and a node actually are. Placing Administration last converts a list of facts into a set of consequences.

**D2 opens with networking because networking is the largest and most prerequisite-hungry of its four competencies**, and it splits into two chapters for a reason: the Service abstraction (Ch 9) and external exposure plus policy (Ch 10) are different cognitive modes. Ch 9 is "how do Pods find each other"; Ch 10 is "how does the outside world get in, and how do you stop it." Merging them would produce the book's only genuinely oversized chapter and would bury the Ingress-is-frozen-but-not-deprecated distinction — one of the most precise facts in the whole curriculum — in the back half of a monster.

**Security (Ch 12) comes after networking and storage**, not before, because it is a synthesis chapter in disguise: RBAC needs namespaces and cluster-scoped resources, Secret hardening needs etcd and RBAC, Pod Security Standards need `securityContext` and the admission gate from Ch 8, and NetworkPolicy — taught once in Ch 10 — is cross-beared in as the network half of the security story rather than re-explained.

**Troubleshooting (Ch 13) closes Part III as the platform-side half of a two-chapter arc** whose application-side half is Chapter 16. B1 sequencing implication #7 argues that the exam splits these across domains but the reader's mental model should not be split. The lineup honors the exam's split (Ch 13 is D2.3, Ch 16 is D3.2) while binding the two with explicit reciprocal cross-bearings: Ch 13 ends by handing off "if the platform is healthy and your app still isn't, go to Ch 16"; Ch 16 opens by handing back.

**Part IV runs packaging → delivery → debugging** so that the GitOps chapter arrives with Helm already in hand (Argo CD's manifest sources include Helm charts, so teaching Argo first would be teaching a consumer before its input) and with the controller pattern four chapters behind it.

**Part V runs patterns → instruments.** B1 sequencing implication #8 is explicit: traces are meaningless without a multi-service mental model. Chapter 17 establishes microservices, service mesh, and the data-plane/control-plane distinction; Chapter 18 then has somewhere to put a distributed trace. Reversing these would make the OpenTelemetry material pure vocabulary drill.

**The one deliberate exception: StatefulSet.** It appears in Chapter 6 with its sibling workload resources, six chapters before PersistentVolumes are defined. B1 flagged this and recommended exactly this resolution — StatefulSet belongs taxonomically with Deployment and DaemonSet, and separating it to satisfy a storage prerequisite would damage the more important comparison. Chapter 6 therefore teaches StatefulSet at the level of *why it is different* (Pods are not interchangeable; each is paired with durable storage) and carries a forward cross-bearing; Chapter 11 closes the loop with the PV pairing once PVC and access modes exist. The trap this defuses — "Deployment vs StatefulSet is about whether the app writes to disk" (B1 trap #21) — is addressed in Ch 6, where the distinction is actually being drawn.

### Why these Parts?

Parts II–V map one-to-one onto the four published exam domains. This is not the only defensible cut, but it is the right one for a beginner exam whose blueprint just changed: a reader who has been studying against five-domain material needs the new four-domain shape to be structurally visible, not merely mentioned in front matter. Every Part opener can state its domain weight and what it is responsible for, and the reader's progress through the book is legible as progress through the blueprint.

Parts I and VI bracket the weighted material and carry no domain weight. Part I ("Taking Departure") does exam intelligence, the 2025-11-24 blueprint change, and the cloud-native framing that Chapter 17 later harvests. Part VI does synthesis and assessment.

The Part titles carry the **Communications Officer** role family's atmospheric register — signals, dispatches, watches, standing off and making port — while the prose voice remains the single unified Lodestar voice. Differentiation is visual and atmospheric only, per the locked architectural rule.

### Where are the prerequisite dependencies honored?

Every edge B1 flagged as ordering-constraining is satisfied, and the Prerequisites column above is the machine-checkable record. The load-bearing ones:

| B1 constraint | How the lineup honors it |
|---|---|
| Containerization precedes everything | Ch 2 is the first content chapter |
| Objects/spec/status → controllers → Pod → workload resources | Ch 3 → 4 → 5 → 6, consecutive |
| Scheduling needs Pod and Node, nothing from D2 | Ch 7, inside Part II |
| Requests/limits precede scheduling and OOMKilled | Introduced Ch 5, applied Ch 7, diagnosed Ch 13 |
| Service → Ingress → Gateway API, strictly | Ch 9 → Ch 10, in that sequence within Ch 10 |
| NetworkPolicy taught once | Full treatment Ch 10; Ch 12 cross-bears in rather than duplicating |
| Storage precedes StatefulSet's *full* treatment | Ch 6 introduces, Ch 11 completes, cross-beared both ways |
| Troubleshooting and Debugging as one arc, two chapters | Ch 13 (platform scope) and Ch 16 (application scope), reciprocal cross-bearings |
| Observability after microservices and service mesh | Ch 17 → Ch 18 |
| GitOps needs the controller/reconciliation pattern | Ch 3 introduces, Ch 6 instantiates, Ch 15 generalizes |
| Cloud-native *why* early, maturity/roster/governance late | Ch 1 plants the framing; Ch 17, second-to-last content chapter, delivers the institutional material |
| ServiceAccount needed by RBAC subjects and Secret types | Planted in Ch 5 as Pod identity; full treatment Ch 12 |
| CRDs/operators needed by Argo CD and Knative | Defined in Ch 6 as the controller pattern extended; full extensibility synthesis in Ch 17 |

Two concepts are deliberately split across chapters along their own dual source-tagging rather than forced into one home:

- **Autoscaling.** Manual scaling and the HPA concept sit in Ch 6 (D1.1, where Deployment lives); the landscape — VPA as an add-on, KEDA, Cluster Autoscaler, Karpenter, scale-to-zero — sits in Ch 17 (D4.2). The `kubectl top` / metrics-server dependency is established in Ch 13, which Ch 17 back-bears to.
- **Deployment strategy.** Rolling-update *mechanics* (`maxSurge`, `maxUnavailable`, Recreate, rollback) are Ch 6, because they are Deployment fields. Strategy *vocabulary* (blue/green, canary, A/B) is Ch 15, because that is where Argo's sync hooks give it something to attach to.

### Where does the most-weighted domain get the most chapter volume?

D1 at 44% receives **7 of 17 content chapters (41.2%)** and **44 of 100 weight points**, and Part II is by a wide margin the longest stretch of the book — seven consecutive chapters, roughly a third more than the next-largest Part. Within D1, Containerization draws the single largest chapter allocation (9 points) because it is the deepest prerequisite and because B1's gap analysis (G29) found the cached sources cover only its runtime and OCI-spec halves, meaning it also carries the most new research.

The full picture, count against weight:

| Domain | Published weight | Content chapters | Count share | Weight points allocated |
|---|---|---|---|---|
| D1 Kubernetes Fundamentals | 44% | 7 | 41.2% | 44 |
| D2 Container Orchestration | 28% | 5 | 29.4% | 28 |
| D3 Cloud Native Application Delivery | 16% | 3 | 17.6% | 16 |
| D4 Cloud Native Architecture | 12% | 2 | 11.8% | 12 |

Maximum count deviation is 2.8 points (D1, slightly under-counted); weight-point allocation is exact by construction. D1 is under-counted in chapters and over-weighted per chapter, which is the correct direction: its chapters are the book's meatiest, and splitting Core Concepts into an eighth chapter to chase the count would fragment the trunk.

**D3 is deliberately given three chapters rather than the two its 16% would minimally justify.** B1 flagged this as the single largest proportional change in the 2025-11-24 revision — Application Delivery doubled from 8% to 16% — and noted that a large volume of third-party prep still targets the old blueprint and badly under-serves it. Three chapters at 17.6% of the count is the lineup's way of saying that out loud.

**D4 is given two chapters rather than three** despite having three competencies, because splitting Community and Collaboration into its own chapter would push D4 to 17.6% of the count against a 12% weight — the largest distortion in any candidate lineup considered. D4.3 is instead the second half of Chapter 17, paired with the CNCF ecosystem material it institutionally belongs to. B1 correctly warns that D4.3 is the competency technically-strong candidates most reliably under-study; the mitigation is not a separate chapter but explicit treatment — its own numbered sections, its own Fixed Points, and its own Soundings coverage — inside Ch 17, plus disproportionate representation in the Ch 19 synthesis and the Ch 20 mock.

---

## Weight-allocation disclosure (carries into front matter)

Three disclosures are **required**, not optional, and all three trace to B1 structural gaps and the skill's Ethical Guardrails:

1. **Sub-competency weights are unpublished (G33).** CNCF states domain weights only. Every per-chapter percentage in this lineup is authored judgment derived from concept count and prerequisite load. The book must not present these as CNCF-published figures.
2. **Question count and passing score are unpublished (G34).** The Linux Foundation explicitly does not state them. The widely-reported 60 questions and 75% pass mark must be cited *as commonly reported*, and Chapter 20's mock must be framed as a calibrated instrument rather than a match to a published count.
3. **The 2025-11-24 blueprint change invalidates a large body of existing prep material (B1 trap #113).** Observability is no longer a standalone domain, Container Orchestration rose 22→28%, and Application Delivery doubled 8→16%. Readers arriving with older material need this stated up front.

A fourth, smaller note belongs in the blueprint appendix: the CNCF-published `KCNA_Curriculum.pdf` contains the typo "Could Native Community and Collaboration." Candidates who download it will see it and wonder.

---

## Gap routing (Stage B1 blocking gaps → chapters)

Seventeen blocking gaps must close before drafting. They route to chapters as follows, so the research pass can be scoped per chapter rather than per gap:

| Chapter | Blocking gaps to close first |
|---|---|
| Ch 2 Containerization | G29 (image build practices, layers, tags vs digests, registries, Buildpacks), G30 (sandboxed runtimes, RuntimeClass motivation) |
| Ch 4 Objects & configuration | — (cached coverage sufficient) |
| Ch 5 Pods | G3 (requests, limits, QoS classes), G7 (ServiceAccounts) |
| Ch 6 Workload controllers | G8 (Deployment update mechanics, rollout, rollback), G10 (CRDs, operator pattern) |
| Ch 7 Scheduling | G4 (taints/tolerations, node and pod affinity, `nodeSelector`, topology spread), G3 |
| Ch 8 Administration | G1 (kubectl command surface), G26 (node lifecycle, cordon/drain, conditions), G27 (etcd backup), G28 (bootstrap tooling) |
| Ch 9 Networking I | G11 (CNI), G13 (CoreDNS, DNS for Services and Pods), G24 (kube-proxy modes) |
| Ch 10 Networking II | G25 (Gateway API detail) |
| Ch 11 Storage | G11 (CSI), G12 (volume types other than PV/PVC) |
| Ch 12 Security | G5 (Pod Security Standards and Admission, `securityContext`), G6 (4Cs framing), G7, G22 (supply chain), G23 (policy engines) |
| Ch 13 Troubleshooting | G1, G2 (Pod failure signatures by name — highest-risk single gap) |
| Ch 14 Packaging | G19 (Kustomize) |
| Ch 15 GitOps & delivery | G9 (deployment strategy vocabulary), G18 (Flux) |
| Ch 16 Debugging | G1, G2 |
| Ch 17 Architecture & ecosystem | G10, G11, G14 (Kubernetes origin and history), G15 (CNCF Landscape), G16 (contributor ladder, KEPs, release cadence), G17 (Code of Conduct, events, participation paths), G31 (adjacent certifications), G32 (verify FinOps/cost is still in scope) |
| Ch 18 Observability | G20 (Grafana, Fluentd/Fluent Bit, Jaeger), G21 (golden signals, RED, USE) |

**Fetch the LFS250 syllabus (G37) before anything else.** It is the closest artifact to a detailed CNCF objective list and would materially firm up the per-chapter weight judgment that G33 and G36 otherwise leave to authored estimate. If it changes the weighting, this lineup's per-chapter percentages should be revised before drafting begins — the chapter *sequence* is dependency-driven and would not change.

---

## Notes for downstream stages

- **Primary Zenith:** Chapter 15. The four OpenGitOps principles are the Kubernetes control loop restated against a Git repository. A reader who met controllers in Ch 3, watched them work in Ch 6, and then sees the same shape again in Ch 15 experiences recognition rather than a fifth list to memorize. B1 identifies this as the strongest synthesis opportunity in the book; the whole Part IV ordering exists to set it up.
- **Secondary Zenith:** Chapter 17's extension-points synthesis — CRI (Ch 2), CNI (Ch 9), CSI (Ch 11), and CRDs (Ch 6) resolving into one pluggability story, with back-bearings to all four.
- **Reciprocal cross-bearing pairs to build deliberately:** Ch 6 ↔ Ch 11 (StatefulSet/PV), Ch 10 ↔ Ch 12 (NetworkPolicy), Ch 13 ↔ Ch 16 (troubleshooting/debugging handoff), Ch 4 → Ch 15 (ConfigMap/Secret as twelve-factor III), Ch 3 → Ch 6 → Ch 15 (the control-loop spine), Ch 13 → Ch 17 (metrics-server as autoscaler input) and Ch 13 → Ch 18 (metrics pipeline vs monitoring).
- **Practice-question budget:** 17 content chapters × (8 Soundings + 10 minimum Bearings) = 306 from fixed baselines alone, before per-chapter Practice Questions or the mock. The 300-question floor is cleared with substantial headroom for cutting weak items at audit.
- **Inferred traps stay labelled as inferred.** B1 marks 14 of its 114 traps `[inferred]` rather than `[source]`. Until practice material verifies them, chapters must describe those as "easy to confuse," never "frequently tested" — the distinction Ethical Guardrail #8 requires.

---

*Stage B2 complete. 20 chapters — 1 orientation, 17 content (44/28/16/12), 1 synthesis, 1 mock exam. 6 Parts. All B1 sequencing constraints satisfied; StatefulSet is the single deliberate forward reference, resolved by cross-bearing per B1's own recommendation.*