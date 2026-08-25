## Ch 1 — Taking Departure  [SHIPPED]

| § | Title | Owns |
|---|---|---|
| (none) | What the KCNA Is, and Who It's For | the credential's audience; what KCNA certifies and does not; prerequisites assumed |
| (none) | Ninety Minutes: The Exam as Published | published exam facts (90 minutes, online proctored, multiple choice); the commonly-reported-vs-published boundary; the 60-question and 75% disclosures |
| (none) | The Curriculum That Moved Under Everyone's Feet | the 2025-11-24 blueprint change; the four domains and 44/28/16/12; what the old five-domain material invalidates; the three weight-allocation disclosures |
| (none) | The Phrase We Haven't Defined Yet | "cloud native" planted, deliberately undefined; the forward pointer to Ch 17 §1 |
| (none) | How This Book Is Built | the branded markers; Parts-to-domains mapping; Soundings/Bearings/Practice architecture; cross-bearing convention |
| (none) | Three Ways to Read This Book | the three reading paths; calibration by Soundings score; how to use The Lodestar |

> ⚑ CONFLICT: **Ch 1's sections carry no `§N` numbers.** Every other chapter in the book numbers its content sections; Ch 1 does not. Consequence: no chapter may emit `*[cross-bearing: see Ch 1 §N — …]*`, because no such anchor exists. One published pointer has already had to improvise around this — `chapter-02-cargo-in-standard-crates.md:243` emits `*[cross-bearing: see Ch 1 §Soundings A2 — orchestrator versus runtime]*`, using a non-numeric section token. **Recommended edit (author's call):** number Ch 1's six content sections §1–§6 in the shipped order above, then retarget the Ch 2 pointer to `Ch 1 §1`. Until that happens, downstream chapters must address Ch 1 by heading name only. The topic ownership above is stable either way.

---

## Ch 2 — Cargo in Standard Crates  [SHIPPED]

| § | Title | Owns |
|---|---|---|
| §1 | What a Container Actually Is | containers vs VMs; namespaces and cgroups as the isolation primitives; the process-not-machine framing |
| §2 | What's Inside an Image | image layers; the union filesystem; the writable container layer; image immutability |
| §3 | Registries, Tags, and Digests | registries; the image reference grammar; tags as mutable pointers; digests as identity; OCI distribution spec |
| §4 | The Container Runtime Interface | CRI as the kubelet↔runtime boundary; containerd; CRI-O; dockershim removal. **First of the four pluggable interfaces** |
| §5 | The Open Container Initiative | the OCI three-spec split (runtime, image, distribution); runC; what standardization actually bought |
| §6 | When Kubernetes Pulls, and When It Doesn't | `imagePullPolicy` values and defaults; the `:latest` interaction; image pull secrets |
| §7 | Not All Isolation Is Equal: RuntimeClass | RuntimeClass; sandboxed runtimes (gVisor, Kata); when default isolation is insufficient |
| §8 | The Crate, Not the Cargo | chapter synthesis; the standardization argument |

---

## Ch 3 — The Ship's Company  [SHIPPED]

| § | Title | Owns |
|---|---|---|
| §1 | How the Cluster Got the Shape It Has | the three deployment eras; Kubernetes origin and history; what Kubernetes is and is not |
| §2 | The Control Plane | kube-apiserver; etcd; kube-scheduler; kube-controller-manager; cloud-controller-manager |
| §3 | Node Components in Context | kubelet; kube-proxy; the container runtime on the node; node registration |
| §4 | Addons, and What Else Is Optional | the addon concept; DNS, dashboard, network plugins as addons; shipped-by-default vs not |
| §5 | The Only Door In | the API server as sole mutator of cluster state; the request path; why nothing bypasses it |
| §6 | Controllers and the Control Loop | **the control loop** — desired state, current state, reconciliation; the controller pattern. **Definition home for cross-cutting theme 1** |
| §7 | Nobody Is in Charge | chapter synthesis; distributed responsibility as the architectural thesis |

---

## Ch 4 — Records of Intent  [SHIPPED]

| § | Title | Owns |
|---|---|---|
| §1 | You File a Declaration | declarative vs imperative; the object as an artifact of intent; `kubectl apply` semantics. **Definition home for cross-cutting theme 4** |
| §2 | The Anatomy of a Record | `apiVersion`/`kind`/`metadata`/`spec`; **spec vs status**; manifests; the `data`-instead-of-`spec` exception |
| §3 | Where a Name Lives | namespaces; the four initial namespaces; **namespaced vs cluster-scoped**. **Definition home for cross-cutting theme 2** |
| §4 | Configuration Kept Outside the Image | ConfigMaps; Secrets (definition, types, contrast); base64 ≠ encryption stated here, hardening deferred to Ch 12 §4 |
| §5 | The Universal Join | labels; annotations; equality-based and set-based selectors. **Definition home for cross-cutting theme 5** |
| §6 | A Declaration, Not an Order | chapter synthesis; intent as the durable artifact |

---

## Ch 5 — The Smallest Vessel  [SHIPPED]

| § | Title | Owns |
|---|---|---|
| §1 | The Pod as the Unit of Scheduling | the Pod concept; the shared network namespace; shared volumes; why the Pod and not the container |
| §2 | More Than One Container Aboard | multi-container Pods; sidecar/adapter/ambassador shapes; when a second container is justified |
| §3 | Everything That Must Happen First | init containers; the init sequence; ordering and completion semantics |
| §4 | Scheduled Once, Replaced Never | Pod immutability of placement; Pods as cattle; `restartPolicy`; restart backoff |
| §5 | Pod Phases and Container States | **Pod phase vs container state** — the distinction Ch 13 is built on; the five phases; Waiting/Running/Terminated and their reasons |
| §6 | A Pod's Identity | ServiceAccount as Pod identity; the `default` ServiceAccount; TokenRequest and projected token volumes (planted; permissions deferred to Ch 12 §2–§3) |
| §7 | Three Probes, Three Jobs | liveness, readiness, startup probes; probe mechanisms (exec, HTTP, TCP, gRPC); what each does on failure |
| §8 | What a Pod Is Owed | **requests vs limits**; QoS classes (Guaranteed, Burstable, BestEffort). **Definition home for cross-cutting theme 8** |
| §9 | The Smallest Deployable Unit | chapter synthesis (Zenith) |

---

## Ch 6 — Fleets, Not Vessels  [SHIPPED]

| § | Title | Owns |
|---|---|---|
| §1 | The Resource That Holds the Intent | ReplicaSet; Deployment; the Deployment→ReplicaSet→Pod ownership chain |
| §2 | A Loop You Can Watch Working | the control loop instantiated in a named controller; `.spec.replicas`; **`kubectl scale`**; **the HPA concept in one sentence** (landscape deferred to Ch 17 §7) |
| §3 | How a Controller Knows Its Own | selectors as the controller→Pod join; `ownerReferences`; adoption and orphaning; selector immutability |
| §4 | Changing the Fleet Under Way | **rolling-update mechanics** — `maxSurge`, `maxUnavailable`, Recreate; pause/resume (strategy *vocabulary* deferred to Ch 15 §2) |
| §5 | Every Rollout Is a Revision | revisions; rollout history; **`kubectl rollout undo`** (distinct from Helm rollback — see Ch 14 §3) |
| §6 | When Pods Are Not Interchangeable | StatefulSet; stable ordinal identity; why identity, not disk-writing, is the distinction. **The book's one deliberate forward reference** — PV pairing completed at Ch 11 §6 |
| §7 | One Per Node, and Work That Ends | DaemonSet; Job; CronJob; completion and parallelism semantics |
| §8 | The Control Loop, Extended | custom resources; CRDs; the operator pattern. **Fourth of the four pluggable interfaces** |
| §9 | Nobody Sails One Pod | chapter synthesis (Zenith) |

---

## Ch 7 — Assigning the Berth  [SHIPPED]

| § | Title | Owns |
|---|---|---|
| §1 | One Decision, Made Once | scheduling overview; **filter → score → bind**; the random tie-break; binding as a one-time decision |
| §2 | What Makes a Node Feasible | feasible nodes; the filter phase; requests as filter input; Allocatable; **unschedulable Pods sit in Pending** |
| §3 | Asking for a Particular Berth | node labels; `nodeSelector`; node affinity, required vs preferred; the bluntness-to-expressiveness gradient |
| §4 | When the Berth Refuses You | taints and tolerations; NoSchedule / PreferNoSchedule / NoExecute; the node's veto vs the Pod's request |
| §5 | Placing Pods Relative to Each Other | pod affinity and anti-affinity; topology keys; topology spread constraints |
| §6 | Overruling the Scheduler, and Replacing It | `nodeName` as the bypass; scheduling policies vs profiles; scheduler plugins; multiple schedulers |
| §7 | Everything Is a Filter or a Score | chapter synthesis (Zenith) |

---

## Ch 8 — Standing the Watch  [SHIPPED]

| § | Title | Owns |
|---|---|---|
| §1 | The Grammar of a Command | kubectl verb-resource-name syntax; the verb surface; output formats; kubeconfig; contexts; in-cluster auth |
| §2 | Three Gates and a Logbook | **authentication → authorization → admission**, in order; admission controllers and webhooks; auditing |
| §3 | Dividing a Shared Cluster | ResourceQuota (namespace total) vs LimitRange (per-object default); the interaction with requests/limits |
| §4 | Taking a Node Out of Service | cordon / drain / uncordon; node conditions; node leases; PodDisruptionBudget interaction |
| §5 | Who Owns the Control Plane | managed vs self-hosted; cluster planning axes; bootstrap tooling (kubeadm, minikube, kind, k3s) |
| §6 | Versions That Are Allowed to Disagree | semantic versioning; **the version-skew window**; supported releases and the three-minor rule; release cadence stated, explained at Ch 17 §8. **Decay-risk block — retrieved at Ch 13 §6 and Ch 17 §8** |
| §7 | The One Backup That Matters | etcd backup and restore; why etcd is the only stateful thing that matters |
| §8 | Rules, or Consequences | chapter synthesis (Zenith) |

---

## Ch 9 — Every Pod Has an Address  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Four Rules and Who Wires Them | the Kubernetes network model's four requirements; Pod IP as cluster-routable; NAT-free pod-to-pod; **CNI** as the pluggable implementation and what a CNI plugin does. **Second of the four pluggable interfaces**; shared network namespace refers to Ch 5 §1 |
| §2 | A Name That Outlives the Pod | the Service object; ClusterIP; the virtual IP; why controller-driven churn (Ch 6 §1) forces an indirection |
| §3 | Four Types, Stacked | ClusterIP → NodePort → LoadBalancer as strictly additive layers; ExternalName as the outlier that resolves rather than routes |
| §4 | Selecting the Backends | Service selector → EndpointSlice; Endpoints as the legacy form; **readiness gates endpoint membership** (probe definitions at Ch 5 §7); headless Services; Services without selectors and hand-written endpoints |
| §5 | How the Traffic Actually Gets There | the service proxy concept; kube-proxy modes (iptables, IPVS, nftables; userspace as historical); why the VIP has no process behind it |
| §6 | Finding It by Name | CoreDNS as the cluster DNS addon; Service A/AAAA/SRV records; Pod DNS records; FQDN shape; search domains and namespace-relative resolution |
| §7 | A Stable Name Over Churn | chapter synthesis (Zenith) |

*Published pointers honored: `Ch 9 §1 — CNI and pod networking`; `Ch 9 §4 — readiness and Service endpoint membership`. Both were emitted in shipped text before this skeleton existed and are immovable.*

---

## Ch 10 — Traffic from Beyond the Cluster  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Where LoadBalancer Runs Out | the cost and scaling limits of one LoadBalancer per Service; the edge-router concept; the L4/L7 boundary. Service types refer to Ch 9 §3 |
| §2 | Routing by Host and Path | the Ingress object; simple fanout; name-based virtual hosting; TLS termination; default backend; path types |
| §3 | The Object Is Not the Implementation | Ingress controllers; IngressClass; **names the pattern "the object exists but nothing happens without the component."** Definition home for cross-cutting theme 3 — Ch 13 §7 and Ch 17 §7 retrieve it *by name* rather than re-deriving it |
| §4 | Frozen, Not Deprecated | the Ingress feature freeze; **frozen ≠ deprecated**; what still gets fixed; the Gateway recommendation and what it does and does not oblige |
| §5 | Roles, Not Just Routes | Gateway API; GatewayClass / Gateway / HTTPRoute; the three-role split (infrastructure provider, cluster operator, application developer); request flow through the resources |
| §6 | Allowing, Never Denying | NetworkPolicy; ingress and egress isolation; `podSelector`, `namespaceSelector`, `ipBlock`; **additive allow-only semantics, no deny rule**; default-deny by selection. **Sole definition home for NetworkPolicy** — Ch 12 §9 refers, never redefines |
| §7 | What NetworkPolicy Cannot Do | the CNI-plugin dependency (a policy on an unsupporting plugin is silently inert); the published out-of-scope list (TLS, node-local traffic, policy targeting non-Pod endpoints) |
| §8 | Nothing Happens Without a Controller | chapter synthesis (Zenith) |

---

## Ch 11 — Below the Waterline  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Three Lifetimes, and the Volumes That Have Them | **the volume lifetime ladder** — container filesystem → Pod-scoped volume → cluster-scoped storage; `emptyDir`; `hostPath` and why it is a hazard; ConfigMap/Secret/projected as volume sources (the objects themselves are Ch 4 §4); generic ephemeral volumes; the `subPath` exception |
| §2 | The Claim and the Supply | PersistentVolume; PersistentVolumeClaim; the supply/demand split and who creates which; binding; PV phases (Available, Bound, Released, Failed) |
| §3 | Provisioning on Demand | StorageClass; static vs dynamic provisioning; the default StorageClass; provisioner and parameters; `volumeBindingMode` and WaitForFirstConsumer |
| §4 | Access Modes and What Happens After | RWO / ROX / RWX / RWOP as **node-count semantics, not permission semantics**; reclaim policies Retain / Delete / Recycle (Recycle as deprecated) |
| §5 | Who Actually Provides the Storage | CSI as the pluggable interface; in-tree-to-CSI migration; what a CSI driver installs. **Third of the four pluggable interfaces** |
| §6 | Pods That Are Not Interchangeable, Revisited | StatefulSet `volumeClaimTemplates`; per-replica PVC; PVC survival across replica rescheduling and deletion. **Closes the Ch 6 §6 forward reference** — reciprocal pair, neither half redefines the other |
| §7 | Outliving the Pod That Asked | chapter synthesis (Zenith) |

*Published pointer honored: `Ch 11 §1 — volume types and lifetimes`. This forced volume types and the lifetime ladder into a single section rather than the two the arc outline's figure list implies; `ch11-fig01-volume-lifetime-ladder` and the volume-type enumeration now share §1.*

---

## Ch 12 — Locks, Keys, and Watchstanders  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Four Layers and Four Phases | the 4Cs (Cloud, Cluster, Container, Code); the cloud native security lifecycle phases (develop, distribute, deploy, runtime); how the two framings overlay |
| §2 | Who You Are | ServiceAccounts as the cluster's non-human identity; TokenRequest and projected tokens; the `default` ServiceAccount's near-zero permissions; **ServiceAccounts as the subjects RBAC binds to** (the binding model itself is §3); users and groups as external identities. Collects the Ch 5 §6 plant; authentication as a gate refers to Ch 8 §2 |
| §3 | What You May Do | RBAC: Role, ClusterRole, RoleBinding, ClusterRoleBinding; **the four-way matrix derived from Ch 4 §3's namespaced/cluster-scoped boundary, not memorized**; verbs and resources; aggregated ClusterRoles; default roles; binding immutability; **why RBAC names subjects instead of selecting them** (contrast with Ch 4 §5); **additive, no deny rule** |
| §4 | Secrets Are Not Encrypted | Secret types; base64 as encoding not protection; **encryption at rest** and EncryptionConfiguration; etcd as the reason it is a separate decision; hardening (RBAC on Secrets, least privilege, file mounts over env vars); external secret stores |
| §5 | What a Pod May Do to Its Node | `securityContext` at Pod and container scope; `runAsNonRoot`, `privileged`, capabilities, `readOnlyRootFilesystem`, seccomp, AppArmor; workload isolation refers to Ch 2 §7 for RuntimeClass and sandboxed runtimes |
| §6 | Three Levels, Three Modes | Pod Security Standards (privileged, baseline, restricted); Pod Security Admission (enforce, audit, warn); namespace labels as the control surface. Retrieves the admission gate from Ch 8 §2 |
| §7 | Trusting What You Ship | supply-chain security: image scanning, signing and attestation, SBOM, in-toto, TUF/Notary, Harbor; restricting who may pull what. Digests as the identity a signature binds refers to Ch 2 §3 |
| §8 | Rules That Watch | policy engines: OPA/Gatekeeper and Kyverno at admission time; Falco at runtime; how these relate to and exceed Pod Security Admission |
| §9 | Additive, Never Deny | chapter synthesis (Zenith); RBAC and NetworkPolicy as one shared semantic — refers to Ch 10 §6, does not restate it. **Cross-cutting theme 9 lands here** |

*Published pointer honored: `Ch 12 §2 — ServiceAccounts as RBAC subjects`.*

---

## Ch 13 — When the Cluster Won't Answer  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Whose Problem Is This, and What to Read First | **the two-audience split** (platform scope vs application scope); the ordered triage flow — scope, then phase, then conditions, then events, then logs; why the phase comes before the logs. Opens the two-chapter arc that Ch 16 §1 closes |
| §2 | Pods That Never Start | Pending; **ImagePullBackOff and ErrImagePull**; CreateContainerConfigError; ImageInspectError; init-container failures from the platform side. Retrieves Ch 7 §2 and §4 (Pending as a scheduling outcome — **Ch 7 decay-fix anchor**), Ch 2 §3 and §6 (image identity and pull policy), Ch 4 §4 (missing ConfigMap/Secret) |
| §3 | Looking Inside | `kubectl describe`; `kubectl events` and the event retention window; `kubectl logs`, `--previous`, `-c` and `--all-containers` for **multi-container Pods**; events as a first-class diagnostic surface |
| §4 | Pods That Start and Then Don't Stay | CrashLoopBackOff and its backoff curve; **OOMKilled**; **Evicted** and node-pressure eviction; the QoS class's role in eviction order. Retrieves Ch 5 §8 |
| §5 | When the Node Is the Problem | node conditions (Ready, MemoryPressure, DiskPressure, PIDPressure); kubelet health and node leases; **`crictl`, and why a node-level tool exists below the Kubernetes API**. Cordon and drain refer to Ch 8 §4 |
| §6 | Versions That Don't Agree | version skew as a cause of failures that are otherwise misdiagnosed; the symptom shapes of a skewed kubelet or client. **Primary decay-fix anchor for Ch 8 §6** — retrieves the rule, does not restate the table |
| §7 | Numbers Nobody Collects by Default | the resource metrics pipeline; metrics-server; `kubectl top` and why it fails on a bare cluster — **retrieved by name as cross-cutting theme 3, defined at Ch 10 §3**; cluster log architecture and node-level agents. **Definition home for metrics-server** — Ch 17 §7 and Ch 18 §3 refer |
| §8 | Read the Phase First | chapter synthesis (Zenith); the explicit handoff to Ch 16 §1 |

*Published pointers honored — four of them, the tightest constraint set in the book: `Ch 13 §2 — diagnosing ImagePullBackOff`, `Ch 13 §2 — diagnosing a Pod that will not start`, `Ch 13 §3 — reading logs from a multi-container Pod`, `Ch 13 §4 — OOMKilled and Evicted`, `Ch 13 §5 — crictl` / `debugging nodes with crictl`. These pins dictate the §2/§3/§4/§5 split above; the arc outline's single "failure signature map" section had to become two (§2 never-started, §4 started-then-died) with the command surface wedged between them at §3.*

*Section count note: 8 sections against 4 weight points is the book's highest section-to-weight ratio. It is correct here — the chapter's method is applied retrieval, and each signature family needs an addressable home because six shipped chapters already point into it.*

---

## Ch 14 — Packing for the Voyage  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Why a Folder of YAML Stops Working | the problem statement: environment variation, apply ordering, versioning, distribution; what `kubectl apply -f` (Ch 4 §1) does not solve |
| §2 | What a Chart Contains | Helm chart anatomy: `Chart.yaml`, `values.yaml`, `templates/`, `charts/` for subcharts, `crds/`, `NOTES.txt`, `_helpers.tpl`; templating as a means rather than the point |
| §3 | Chart, Release, Revision | **the four words readers collapse** — package, manifest, release, revision; `helm install` / `upgrade` / `rollback`; **Helm rollback vs Deployment rollback as different mechanisms wearing the same word** (Ch 6 §5) |
| §4 | Where Charts Come From | chart repositories; OCI registries as chart stores (ties to Ch 2 §3); `helm repo` and `helm pull`; chart version vs appVersion |
| §5 | Patching Instead of Templating | Kustomize; base and overlay; `kustomization.yaml`; strategic-merge and JSON patches; generators; `kubectl -k` as the built-in path |
| §6 | Which One, When | the templating-vs-overlay decision; using both together; **why charts have a `crds/` directory** and the ordering problem it solves (CRD definition is Ch 6 §8) |
| §7 | A Package, Not a Template | chapter synthesis (Zenith) |

*Decay-risk note (B3): Helm has thin downstream presence. The two mandatory anchors are Ch 15 §4 (charts as an Argo CD manifest source) and Ch 17 §4 (CRDs shipped as chart content). Neither may be dropped.*

---

## Ch 15 — The Chart Is the Truth  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Twelve Factors, and the Ones Kubernetes Already Solved | the twelve-factor app; **factor III (config in the environment)** tied back to Ch 4 §4; which factors the platform supplies and which remain the application's problem |
| §2 | Ways to Replace What's Running | **deployment strategy vocabulary** — rolling, Recreate, blue/green, canary, A/B — and the trade-off each makes. The *mechanics* of rolling and Recreate stay at Ch 6 §4; this section owns the names and the reasoning only |
| §3 | Push, or Pull | CI/CD as push; GitOps as pull; the credential and blast-radius consequences; **the four OpenGitOps principles** (declarative, versioned and immutable, pulled automatically, continuously reconciled) as the pull model's definition |
| §4 | An Agent That Watches a Repository | Argo CD: the Application custom resource; the controller model; tracking branches, tags, and commits; Synced vs OutOfSync; sync operations and self-heal; drift detection; rollback by revert; **the delivery agent's own identity — its ServiceAccount and the permissions it must hold** (identity model at Ch 12 §2–§3). Charts as a manifest source refers to Ch 14 §2 |
| §5 | Ordering the Sync | PreSync / Sync / PostSync hooks; sync waves; why ordering is a problem GitOps has that a single `kubectl apply` does not |
| §6 | The Other Agent, and More Than One Cluster | Flux and its controller set; the Argo/Flux comparison; multi-cluster delivery patterns and where the desired state lives for each |
| §7 | The Control Loop, Pointed at a Repository | **PRIMARY ZENITH.** Chapter synthesis; re-presents `ch03-fig02` with Git substituted for etcd as the desired-state store. Owns no new material — the payoff is recognition, and it fails if the figure does not visually rhyme with Ch 3 §6's |

*Published pointer honored: `Ch 15 §4 — the delivery agent's identity`. This pins Argo CD to §4, which pushed the four OpenGitOps principles up into §3 alongside push-vs-pull. That merge is defensible — the principles are the pull model's definition — but it means `ch15-fig05-opengitops-four-principles` renders inside §3, not in a section of its own.*

---

## Ch 16 — Your Application, Their Cluster  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Handed Back | receives the Ch 13 §8 handoff; **when the Pod is fine and the application isn't**; the scope boundary restated from the application side; **the four triage questions** that structure the chapter (is it running, is it healthy, is it reachable, is it configured) |
| §2 | When It Never Got Started | **debugging init containers** from the application side; reading the init sequence (defined at Ch 5 §3); `kubectl logs -c <init-container>`; ordering and non-idempotency mistakes; config errors visible at init |
| §3 | Getting Inside, and Adding What Isn't There | `kubectl exec` and `-c`; the distroless-image problem; ephemeral containers; `kubectl debug`, debug profiles, and `--copy-to`; `kubectl debug node/` |
| §4 | Is Anything Even Selected | application-side Service debugging: selector/label mismatch, empty EndpointSlice, `port` vs `targetPort`, readiness holding endpoints back, DNS name shape. Refers to Ch 9 §4 and §6; does not restate the Service model |
| §5 | Bypassing the Service on Purpose | `port-forward` as a diagnostic that deliberately skips the Service path; what a working port-forward plus a broken Service together prove |
| §6 | When Each Replica Is Its Own | StatefulSet debugging from the application side: ordinal identity, the per-replica PVC, headless-Service DNS names. Refers to Ch 6 §6 and Ch 11 §6 |
| §7 | Before You Ship It | local development and debugging loops; when to reproduce locally and when the reproduction is only valid in-cluster |
| §8 | Mine, or the Platform's | chapter synthesis (Zenith); closes the two-chapter arc |

*Published pointers honored: `Ch 16 §1 — when the Pod is fine and the application isn't`; `Ch 16 §2 — debugging init containers`. The §2 pin moved init-container debugging ahead of the exec/ephemeral-container material, which is the reverse of the arc outline's implied order. It reads fine — never-started precedes running-but-wrong — but the figure `ch16-fig02-ephemeral-container-debug` now belongs to §3, not §2.*

---

## Ch 17 — The Fleet and Its Charts  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | What "Cloud Native" Actually Names | **the CNCF cloud native definition v1.1, verbatim, and its named characteristics**; what the CNCF is as an institution; collects the Ch 1 plant |
| §2 | Sandbox, Incubating, Graduated, and Who Decides | **CNCF project maturity levels and the project lifecycle**; **CNCF governance** — Governing Board, TOC, TAGs, End User TAB; the CNCF Landscape as a map. **The graduated roster is dated data; the levels are the durable fact and the only retrieval target** |
| §3 | Small Pieces, Replaced Whole | microservices; loose coupling; immutable infrastructure; declarative APIs; how the three reinforce each other. Back-bears Ch 4 §1 and Ch 2 §1–§2 |
| §4 | Every Place Kubernetes Lets You In | **the four pluggable interfaces, collected** — CRI (Ch 2 §4), CNI (Ch 9 §1), CSI (Ch 11 §5), CRDs and operators (Ch 6 §8) — plus API aggregation, admission webhooks (Ch 8 §2), device plugins, and scheduler plugins (Ch 7 §6). **Collects; does not redefine.** CRDs shipped as chart content refers to Ch 14 §6 |
| §5 | A Network That Knows What It's Carrying | service mesh; **data plane vs control plane**; Envoy; mTLS and zero trust (refers to Ch 12 §3–§4); sidecar vs ambient; what a mesh adds over Service (Ch 9) plus NetworkPolicy (Ch 10 §6) |
| §6 | Code Without a Server to Put It On | serverless; Knative Serving, Eventing, Functions; scale to zero; how a Knative Service relates to a Deployment |
| §7 | Four Things That Scale | **the autoscaling landscape** — HPA (concept at Ch 6 §2), VPA, Cluster Autoscaler, Karpenter, KEDA; the axis each one moves. metrics-server as HPA's input refers to Ch 13 §7; **Cluster Autoscaler reacting to unschedulable Pods — Ch 7 decay-fix anchor**; **VPA is an addon, not shipped by default — retrieved by name as cross-cutting theme 3** |
| §8 | How the Project Actually Runs, and How You'd Join | Kubernetes governance — SIGs, Working Groups, Committees, Steering Committee; the contributor ladder; KEPs; **SIG Release, the release cadence, and why ~3 releases a year and three supported minors explain each other — Ch 8 §6 decay-fix anchor**; KubeCon; the Code of Conduct; the CNCF certification ladder and adjacent credentials |
| §9 | One Pluggability Story | **SECONDARY ZENITH.** Chapter synthesis at a second altitude above §4; back-bears explicitly to all four interface chapters |

*Published pointers honored: `Ch 17 §1 — the CNCF cloud native definition and its characteristics`; `Ch 17 §2 — CNCF governance and project maturity` / `…and the project lifecycle`; `Ch 17 §4 — the four pluggable interfaces, collected`. One published pointer disagrees with these — see Collisions below.*

*Section count note: 9 sections is the book's joint-largest, and correct — this chapter carries two competencies (D4.2 and D4.3), six distinct arcs, and three Bearings checkpoints. §2 and §8 are D4.3's own numbered sections, satisfying B2's requirement that Community and Collaboration get explicit treatment rather than a footnote.*

---

## Ch 18 — Reading the Instruments  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | What You Can Ask, and What You Already Know | **observability vs monitoring**, framed as unknown unknowns vs known unknowns; instrumentation and telemetry as terms; **health checking is not observability** — probes (Ch 5 §7) explicitly excluded; **observability's status under the 2025-11-24 blueprint**, no longer a standalone domain |
| §2 | Four Signals | the four OpenTelemetry signals — traces, metrics, logs, baggage; what each answers and cannot answer; the OTel collector's role |
| §3 | Numbers Over Time | metrics as time series; labels and cardinality; **utilization relative to requests** (retrieves Ch 5 §8); **metrics-server vs a monitoring system** — the distinction the exam actually tests (metrics-server defined at Ch 13 §7) |
| §4 | Pulling, Not Being Pushed | Prometheus: the pull/scrape model; service discovery; exporters; client libraries; Pushgateway and its narrow correct use; PromQL; Alertmanager; Grafana as the dashboard layer; where Prometheus fits and where it does not |
| §5 | Following One Request | distributed tracing; spans and root spans; trace and span IDs; context propagation across services; Jaeger; mesh-generated telemetry refers to Ch 17 §5. Depends on the multi-service model built at Ch 17 §3 |
| §6 | Lines From Everywhere | cluster logging architecture; **node-level log collection agents as DaemonSets** (Ch 6 §7); Fluentd and Fluent Bit; sidecar logging; log rotation and why `kubectl logs` is not archival |
| §7 | Is the Service Doing What Users Expect | reliability; SLI and SLO; error budgets; **the four golden signals**; RED and USE as complementary framings |
| §8 | One Question, Four Instruments | chapter synthesis (Zenith) |

*Published pointers honored: `Ch 18 §1 — health checking is not observability`; `Ch 18 §1 — observability under the current blueprint`; `Ch 18 §3 — utilization relative to requests`.*

---

## Ch 19 — Bearings Before Landfall  [PLANNED]

| § | Title | Owns |
|---|---|---|
| §1 | Nine Threads Through Twenty Chapters | the nine cross-cutting themes, each named and traced through its chapter path; the book re-seen by theme rather than by domain. Owns no new material |
| §2 | The Pairs That Cost Points | the confusion-pair matrix; a discriminating question for every surviving pair from the B1 trap inventory. `[inferred]` traps described as "easy to confuse," never as "frequently tested" |
| §3 | Ninety Minutes | **exam-day pacing and time discipline**; flagging and skipping; the second pass; what to do when a question is unfamiliar |
| §4 | Where the Weight Actually Is | the 44/28/16/12 map re-walked against the reader's own Soundings and Bearings history; where remaining study time buys the most; D4.3 flagged as the reliably under-studied competency |
| §5 | Using The Lodestar | walkthrough of `the-lodestar.md`; what each block is for; how to use it in the last hour. The file itself is a book-level artifact, not chapter content |
| §6 | The Week Before | a dated final-week plan; what to review, what to leave alone, what to do the night before |

*Published pointers honored: `Ch 19 §3 — pacing and time discipline`; `Ch 19 §5 — using The Lodestar`. Both pins are satisfied at their exact numbers; §4 sits between them, which is why "where the weight is" follows pacing rather than preceding it.*

*Synthesis type — Soundings optional per the structural contract, retained at 5 per the arc outline.*

---

## Ch 20 — Full Mock Exam  [PLANNED]

**This chapter has no numbered sections, deliberately.** `chapter_type: mock_exam` is exempt from standard chapter structure, branded markers, and the Zenith requirement. Its structure is fixed by skill Part 16 and consists of unnumbered blocks:

| Block | Owns |
|---|---|
| Instructions | time budget; pacing guidance; what the reader may and may not use; the calibration disclosure — 90 minutes is published, the question count is commonly reported, and this instrument is sized to that report rather than matched to a published figure |
| Exam | 60 questions, one continuous section, no mid-exam commentary. Domain split D1 26 · D2 17 · D3 10 · D4 7 |
| Mock Exam Answers & Walkthroughs | per-question correct answer, why it is correct, why each distractor is wrong; separated so the reader can attempt first |
| Scoring Rubric | band interpretation and what to do after each outcome. **Does not state a pass mark as fact** — the 75% figure is unpublished |

**Nothing anywhere in the book may emit `*[cross-bearing: see Ch 20 §N — …]*`.** Address this chapter by name only.

---

## Collisions and open numbering questions

**1. Ch 1 has no `§N` anchors at all.** Six content sections, none numbered. One shipped pointer already improvises around it (`chapter-02:243`, `see Ch 1 §Soundings A2`). No future chapter may assume `Ch 1 §N` resolves. Author decision required: number them §1–§6 in shipped order and retarget the Ch 2 pointer, or leave Ch 1 addressable by heading name only. Recorded as a CONFLICT under the Ch 1 block.

**2. One published Ch 17 pointer contradicts two others.** Shipped text contains all three of:

- `see Ch 17 §1 — the CNCF, its governance, and the cloud native definition`
- `see Ch 17 §2 — CNCF governance and project maturity`
- `see Ch 17 §2 — CNCF governance and the project lifecycle`

The skeleton puts the definition at §1 and governance at §2, satisfying the majority. The first pointer lands a governance-seeking reader one section early. Adjacent sections make this survivable, but it is a real defect in shipped text. **Recommended edit (author's call):** retarget that single pointer to `Ch 17 §2`, or broaden it to `Ch 17 §1–§2`. Do not move governance into §1 — two pointers outvote one, and §1 is already the busiest anchor in the chapter.

**3. Heading-format drift among shipped chapters.** Ch 2, 3, and 4 write `## §N — <difficulty> Title`. Ch 5, 6, 7, and 8 write `## <difficulty> §N — Title`. The numbering is unaffected and nothing needs renumbering, but the mechanical extractor handles the two forms differently (it strips the difficulty glyph from one and keeps it in the other), which is why the input to this stage looked inconsistent. **Recommendation for Ch 9–19: adopt the Ch 5–8 form** — it is the majority, it is the more recent, and it puts the difficulty glyph where a reader scanning the left margin finds it first.

**4. Zenith-marking drift among shipped chapters.** Ch 5 §9, Ch 6 §9, and Ch 7 §7 mark the closing synthesis section `☀️`. Ch 2 §8, Ch 3 §7, Ch 4 §6, and Ch 8 §8 mark theirs with an ordinary difficulty glyph. All seven *are* the chapter's Zenith. **Recommendation for Ch 9–19: use `☀️` on the closing section.** Retrofitting Ch 2/3/4/8 is a separate cosmetic sweep, not this stage's call.

**5. Pinned section numbers — the binding constraint on everything above.** Shipped chapters emitted 19 forward cross-bearings carrying explicit `§N` targets into chapters that did not yet exist. Those numbers are now immovable and dictated several splits in this skeleton:

| Pin | Effect on the design |
|---|---|
| Ch 9 §1 — CNI and pod networking | CNI merged into §1 with the network model rather than getting its own section |
| Ch 9 §4 — readiness and Service endpoint membership | §4 must be the EndpointSlice/readiness section, so the Service-type ladder moved to §3 |
| Ch 11 §1 — volume types and lifetimes | volume types and the lifetime ladder forced into one section |
| Ch 12 §2 — ServiceAccounts as RBAC subjects | identity at §2, permission model at §3 |
| Ch 13 §2, §3, §4, §5 | the signature map split into never-started (§2) and started-then-died (§4), with the command surface at §3 and node-level at §5 |
| Ch 15 §4 — the delivery agent's identity | Argo CD pinned to §4, pushing the OpenGitOps principles up into §3 |
| Ch 16 §1, §2 | init-container debugging ahead of exec/ephemeral containers |
| Ch 17 §1, §2, §4 | definition, governance+maturity, and the collected interfaces at fixed slots |
| Ch 18 §1, §3 | the observability/health distinction at §1; utilization-vs-requests at §3 |
| Ch 19 §3, §5 | pacing at §3, The Lodestar at §5 |

All 19 pins are satisfied. Any later revision to Ch 9–19 numbering must re-check this list first.

**6. All back-pointers into shipped chapters currently resolve.** Every `see Ch 2–8 §N` reference in shipped text targets a section that exists. No broken back-references. The only unresolvable form in the book is the Ch 1 case in item 1.

**7. Topics with a single owner and named referrers.** These are the pairs most likely to be re-taught by accident:

| Topic | Sole owner | Refers, never redefines |
|---|---|---|
| The control loop | Ch 3 §6 | Ch 6 §2, Ch 11 §2, Ch 15 §7, Ch 17 §4 |
| Namespaced vs cluster-scoped | Ch 4 §3 | Ch 8 §3, Ch 12 §3 |
| Labels and selectors | Ch 4 §5 | Ch 6 §3, Ch 7 §3, Ch 9 §4, Ch 10 §6, Ch 16 §4 |
| Requests, limits, QoS | Ch 5 §8 | Ch 7 §2, Ch 13 §4, Ch 17 §7, Ch 18 §3 |
| ServiceAccount identity | Ch 5 §6 (object) / Ch 12 §2 (as RBAC subject) | Ch 15 §4 |
| Rolling-update mechanics | Ch 6 §4 | Ch 15 §2 owns the strategy *vocabulary* only |
| Rollback | Ch 6 §5 (`kubectl rollout undo`) | Ch 14 §3 owns Helm rollback and the name collision |
| StatefulSet | Ch 6 §6 (identity) / Ch 11 §6 (storage pairing) | Ch 16 §6 |
| Version skew | Ch 8 §6 | Ch 13 §6, Ch 17 §8 |
| CRI / CNI / CSI / CRDs | Ch 2 §4 / Ch 9 §1 / Ch 11 §5 / Ch 6 §8 | Ch 17 §4 collects all four |
| NetworkPolicy | Ch 10 §6–§7 | Ch 12 §9 |
| "Object exists, nothing happens without the component" | Ch 10 §3 (named as a pattern) | Ch 13 §7, Ch 17 §7 — retrieved *by name* |
| metrics-server and the metrics pipeline | Ch 13 §7 | Ch 17 §7, Ch 18 §3 |
| Troubleshooting scope | Ch 13 (platform) / Ch 16 (application) | reciprocal handoff at Ch 13 §8 ↔ Ch 16 §1 |
| Autoscaling | Ch 6 §2 (HPA concept) / Ch 17 §7 (landscape) | Ch 13 §7 |

**8. Section counts that deviate from what the arc outline implies.** Two, both deliberate and both explained under their blocks: Ch 13 runs 8 sections against 4 weight points because four pinned anchors forced the signature map into two sections plus a command section; Ch 17 runs 9 sections because it carries two competencies and D4.3 requires its own numbered treatment. Neither should be compressed to chase a count.

**9. Ch 20 has no section numbers.** Restated here so no later stage assumes otherwise.