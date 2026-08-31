# Term Ownership Ledger — KCNA

**Book:** Kubernetes and Cloud Native Associate
**Exam:** KCNA (CNCF / The Linux Foundation), curriculum effective 2025-11-24
**Stage:** B7 — Term Ownership
**Date:** 2026-08-24
**Inputs:** B1 domain analysis · B2 chapter lineup · B6 section skeleton · shipped text of Chapters 1–8

Chapters 1–8 are drafted and published. Their term ownership below is **recorded, not assigned** — every claim about a shipped chapter in this document was verified against the file, and where the shipped text and the B6 skeleton disagree, the shipped text wins and the disagreement is flagged `⚑`. Chapters 9–20 are unwritten; their ownership is assigned here and is binding on drafting.

---

## How to read this ledger

**`Defined by`** is the one place in the book where the term gets its full treatment. Exactly one chapter-and-section per concept. Where a word carries two genuinely different concepts (a Helm *revision* and a Deployment *revision*), the concepts are split into two rows and each row has one owner; see **Canonical forms** for the surface-form rules that keep them apart.

**`First appears`** is where the reader first meets the word, which is frequently not where it is defined. Unmarked chapter numbers are **verified in shipped text**. A `†` marks a **projected** first appearance derived from the B6 skeleton — Chapters 9–20 do not exist yet, so those are predictions the drafting stage should treat as the plan, not as fact.

**`Earlier chapters must`** is the instruction a drafting stage follows verbatim, and it takes exactly one of four values:

| Instruction | What it licenses |
|---|---|
| `define in place` | This chapter owns the term. Full treatment here. |
| `gloss in one clause + pointer` | One sentence of working meaning, then `*[cross-bearing: see Ch N §M — …]*`. The reader can proceed without the full definition. |
| `name only, always with a pointer` | The word may be used. It may not be explained. Never bare — a pointer accompanies every use. |
| `do not use before Ch N` | The word is unavailable. Rewrite around it. |

Where the instruction column reads `—`, no chapter earlier than the owner uses the term and nothing is required.

**`⚑`** marks a conflict between shipped text and the B6 skeleton, or between two shipped chapters. Every `⚑` carries a recommendation; none of them reassign a shipped chapter's ownership.

---

# Part 1 — The ledger

## Ch 1 — Taking Departure  [SHIPPED]

Ch 1's sections are unnumbered (B6 Collision #1), so every pointer into this chapter addresses it **by heading name**, never `Ch 1 §N`.

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| KCNA (Kubernetes and Cloud Native Associate) | Ch 1 § *What the KCNA Is* | Ch 1 | — |
| The Linux Foundation | Ch 1 § *What the KCNA Is* | Ch 1 | — |
| CNCF — **as exam sponsor and credential issuer** | Ch 1 § *What the KCNA Is* | Ch 1 | — |
| Exam domain | Ch 1 § *The Curriculum That Moved* | Ch 1 | — |
| Domain weight | Ch 1 § *The Curriculum That Moved* | Ch 1 | — |
| Blueprint (exam blueprint / curriculum) | Ch 1 § *The Curriculum That Moved* | Ch 1 | — |
| Online proctored exam | Ch 1 § *Ninety Minutes* | Ch 1 | — |
| "Commonly reported" vs "published" | Ch 1 § *Ninety Minutes* | Ch 1 | — |
| The Lodestar (the book's one-page reference) | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| 🧭 Soundings | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| ☆ Taking Your Bearings | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| ★ Fixed Point | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| ⚠ Navigational Hazards | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| — Dead Reckoning | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| 🏆 Safe Harbor | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| ☀️ Zenith | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| ⚓ Worth Securing · 🪝 Snag · 🔭 Closer Look · 🪢 Mnemonic | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| Logbook Entry · Extended Analogy (sidebars) | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| Cross-bearing | Ch 1 § *How This Book Is Built* | Ch 1 | — |
| Difficulty band (⚪🔵🟡🔴) | Ch 1 § *How This Book Is Built* | Ch 1 | — |

## Ch 2 — Cargo in Standard Crates  [SHIPPED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| Container | Ch 2 §1 | Ch 1 | name only, always with a pointer |
| Containerization | Ch 2 §1 | Ch 2 §1 | — |
| Virtual machine / VM | Ch 2 §1 (by contrast) | Ch 2 §1 | — |
| Hypervisor | Ch 2 §1 | Ch 2 §1 | — |
| Linux namespace (the kernel primitive) | Ch 2 §1 | Ch 2 §1 | — |
| cgroup (control group) | Ch 2 §1 | Ch 2 §1 | — |
| Process isolation | Ch 2 §1 | Ch 2 §1 | — |
| Container image | Ch 2 §2 | Ch 2 §1 | — |
| Image layer | Ch 2 §2 | Ch 2 §2 | — |
| Union filesystem / overlay filesystem | Ch 2 §2 | Ch 2 §2 | — |
| Writable container layer | Ch 2 §2 | Ch 2 §2 | — |
| Copy-on-write | Ch 2 §2 | Ch 2 §2 | — |
| Base image | Ch 2 §2 | Ch 2 §2 | — |
| Image immutability | Ch 2 §2 | Ch 2 §2 | — |
| Registry | Ch 2 §3 | Ch 2 §2 | — |
| Repository (image repository) | Ch 2 §3 | Ch 2 §3 | — |
| Image reference (the grammar) | Ch 2 §3 | Ch 2 §3 | — |
| Tag | Ch 2 §3 | Ch 2 §3 | — |
| `:latest` | Ch 2 §3 | Ch 2 §3 | — |
| Digest | Ch 2 §3 | Ch 2 §3 | — |
| CRI (Container Runtime Interface) | Ch 2 §4 | Ch 2 §4 | — |
| Container runtime | Ch 2 §4 | Ch 2 §1 | — |
| containerd | Ch 2 §4 | Ch 2 §4 | — |
| CRI-O | Ch 2 §4 | Ch 2 §4 | — |
| dockershim | Ch 2 §4 | Ch 2 §4 | — |
| Docker | Ch 2 §4 | Ch 2 §1 | — |
| OCI (Open Container Initiative) | Ch 2 §5 | Ch 2 §3 | — |
| OCI runtime spec · image spec · distribution spec | Ch 2 §5 | Ch 2 §3 | — |
| runC | Ch 2 §5 | Ch 2 §5 | — |
| `imagePullPolicy` (`Always`/`IfNotPresent`/`Never`) | Ch 2 §6 | Ch 2 §6 | — |
| Image pull secret | Ch 2 §6 | Ch 2 §6 | — |
| **`ImagePullBackOff` — the reason string and its taxonomic slot** | Ch 2 §6, completed at Ch 5 §5 | Ch 2 §6 | — · see ⚑2 |
| RuntimeClass | Ch 2 §7 | Ch 2 §7 | — |
| Sandboxed runtime | Ch 2 §7 | Ch 2 §7 | — |
| gVisor · Kata Containers | Ch 2 §7 | Ch 2 §7 | — |
| Interface-and-implementations pattern | Ch 2 §4 (named), collected at Ch 17 §4 | Ch 2 §4 | — |

## Ch 3 — The Ship's Company  [SHIPPED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| Bare-metal / virtualization / container deployment era | Ch 3 §1 | Ch 3 §1 | — |
| IaaS · PaaS · SaaS | Ch 3 §1 | Ch 3 §1 | — |
| Orchestration / orchestrator | Ch 3 §1 | Ch 1 | name only, always with a pointer |
| Kubernetes | Ch 3 §1 | Ch 1 | name only, always with a pointer |
| K8s (the abbreviation) | Ch 3 §1 | Ch 1 | — |
| Borg | Ch 3 §1 | Ch 3 §1 | — |
| Cluster | Ch 3 §1 | Ch 1 | name only, always with a pointer |
| Control plane — **the cluster's** | Ch 3 §2 | Ch 3 §2 | — · homonym, see Canonical forms |
| kube-apiserver / API server | Ch 3 §2 | Ch 3 §2 | — |
| etcd | Ch 3 §2 | Ch 3 §2 | — |
| kube-scheduler | Ch 3 §2 | Ch 3 §2 | — |
| kube-controller-manager | Ch 3 §2 | Ch 3 §2 | — |
| cloud-controller-manager | Ch 3 §2 | Ch 3 §2 | — |
| Node / worker node | Ch 3 §3 | Ch 2 §4 | gloss in one clause + pointer |
| kubelet | Ch 3 §3 | Ch 2 §4 | gloss in one clause + pointer |
| kube-proxy | Ch 3 §3 | Ch 3 §3 | — |
| Node registration | Ch 3 §3 | Ch 3 §3 | — |
| Addon (cluster addon) | Ch 3 §4 | Ch 3 §4 | — |
| Network plugin (**as an addon**; as an interface, Ch 9 §1) | Ch 3 §4 | Ch 3 §3 | — |
| Kubernetes Dashboard | Ch 3 §4 | Ch 3 §4 | — |
| The API server as sole mutator of cluster state | Ch 3 §5 | Ch 3 §2 | — |
| Watch (the API primitive) | Ch 3 §5 | Ch 3 §5 | — |
| **Control loop** | Ch 3 §6 | Ch 3 §6 | — |
| Controller | Ch 3 §6 | Ch 3 §2 | gloss in one clause + pointer |
| Reconciliation | Ch 3 §6 | Ch 3 §6 | — |
| Desired state · current state | Ch 3 §6 | Ch 3 §6 | — |
| Controller pattern | Ch 3 §6 | Ch 3 §6 | — |

## Ch 4 — Records of Intent  [SHIPPED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| Declarative | Ch 4 §1 | Ch 1 | name only, always with a pointer |
| Imperative | Ch 4 §1 (by contrast) | Ch 4 §1 | — |
| Object (Kubernetes object) | Ch 4 §1 | Ch 3 §5 | gloss in one clause + pointer |
| Resource / API resource | Ch 4 §1 | Ch 3 §5 | gloss in one clause + pointer |
| `kubectl apply` | Ch 4 §1 | Ch 4 §1 | — |
| Manifest | Ch 4 §2 | Ch 4 §1 | — |
| `apiVersion` · `kind` · `metadata` | Ch 4 §2 | Ch 4 §2 | — |
| API group · API version | Ch 4 §2 | Ch 4 §2 | — |
| **`spec` vs `status`** | Ch 4 §2 | Ch 3 §6 | gloss in one clause + pointer |
| `data` (the ConfigMap/Secret exception to `spec`) | Ch 4 §2 | Ch 4 §2 | — |
| Namespace — **the Kubernetes object** | Ch 4 §3 | Ch 3 §2 | gloss in one clause + pointer · homonym with Linux namespace, see Canonical forms |
| `default` · `kube-system` · `kube-public` · `kube-node-lease` | Ch 4 §3 | Ch 4 §3 | — |
| **Namespaced vs cluster-scoped** | Ch 4 §3 | Ch 4 §3 | — |
| ConfigMap | Ch 4 §4 | Ch 4 §4 | — |
| Secret (the object; hardening is Ch 12 §4) | Ch 4 §4 | Ch 2 §6 | name only, always with a pointer |
| Secret type | Ch 4 §4 | Ch 4 §4 | — |
| base64 (encoding, not protection) | Ch 4 §4 | Ch 4 §4 | — |
| `stringData` | Ch 4 §4 | Ch 4 §4 | — |
| **Label** — the Kubernetes label | Ch 4 §5 | Ch 4 §2 | — · homonym with Prometheus label, see Canonical forms |
| Annotation | Ch 4 §5 | Ch 4 §5 | — |
| **Label selector** | Ch 4 §5 | Ch 4 §5 | — |
| Equality-based selector · set-based selector | Ch 4 §5 | Ch 4 §5 | — |
| Field selector | Ch 4 §5 (name + scope only); glossary owns the definition | Ch 4 §5 | — |
| `ownerReferences` | Ch 6 §3 | Ch 4 §5 | name only, always with a pointer |

## Ch 5 — The Smallest Vessel  [SHIPPED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **Pod** | Ch 5 §1 | Ch 2 §4 | gloss in one clause + pointer |
| PodSpec | Ch 5 §1 | Ch 3 §3 | gloss in one clause + pointer |
| Shared network namespace (the Pod's) | Ch 5 §1 | Ch 5 §1 | — |
| Pod IP | Ch 9 §1 | Ch 5 §1 | gloss in one clause + pointer |
| Co-location / shared fate | Ch 5 §1 | Ch 5 §1 | — |
| Multi-container Pod | Ch 5 §2 | Ch 5 §1 | — |
| **Sidecar** (the Pod shape; the mesh proxy is Ch 17 §5) | Ch 5 §2 | Ch 5 §2 | — |
| Adapter · ambassador (container shapes) | Ch 5 §2 | Ch 5 §2 | — |
| Init container | Ch 5 §3 | Ch 5 §2 | — |
| `restartPolicy` (`Always`/`OnFailure`/`Never`) | Ch 5 §4 | Ch 5 §4 | — |
| Restart backoff (the exponential mechanism) | Ch 5 §4 | Ch 5 §4 | — |
| Cattle, not pets | Ch 5 §4 | Ch 5 §4 | — |
| **Pod phase** (`Pending`/`Running`/`Succeeded`/`Failed`/`Unknown`) | Ch 5 §5 | Ch 5 §4 | — |
| **Container state** (`Waiting`/`Running`/`Terminated`) | Ch 5 §5 | Ch 2 §6 | name only, always with a pointer |
| `Reason` (the container-state field) | Ch 5 §5 | Ch 2 §6 | name only, always with a pointer |
| `ImagePullBackOff` — **diagnosis** | Ch 13 §2 | Ch 2 §6 | name only, always with a pointer · ⚑2 |
| ServiceAccount — **the object and Pod identity** | Ch 5 §6 | Ch 3 §3 | name only, always with a pointer |
| `default` ServiceAccount | Ch 5 §6 | Ch 5 §6 | — |
| TokenRequest | Ch 5 §6 | Ch 5 §6 | — |
| Projected token volume | Ch 5 §6 | Ch 5 §6 | — |
| `automountServiceAccountToken` | Ch 5 §6 | Ch 5 §6 | — |
| Liveness probe | Ch 5 §7 | Ch 5 §5 | — |
| Readiness probe | Ch 5 §7 | Ch 5 §5 | — |
| Startup probe | Ch 5 §7 | Ch 5 §7 | — |
| Probe mechanism (`exec`, HTTP GET, TCP socket, gRPC) | Ch 5 §7 | Ch 5 §7 | — |
| **Resource request** | Ch 5 §8 | Ch 5 §8 | — · homonym with API request, see Canonical forms |
| **Resource limit** | Ch 5 §8 | Ch 5 §8 | — |
| QoS class (`Guaranteed`/`Burstable`/`BestEffort`) | Ch 5 §8 | Ch 5 §8 | — |
| Millicore · mebibyte (resource units) | Ch 5 §8 | Ch 5 §8 | — |
| CPU throttling | Ch 5 §8 | Ch 5 §8 | — |
| `OOMKilled` — **the mechanism** | Ch 5 §8 | Ch 5 §8 | — · diagnosis is Ch 13 §4, deferral already in shipped text |

## Ch 6 — Fleets, Not Vessels  [SHIPPED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| ReplicaSet | Ch 6 §1 | Ch 4 §5 | name only, always with a pointer |
| **Deployment** | Ch 6 §1 | Ch 2 | name only, always with a pointer |
| Ownership chain (Deployment → ReplicaSet → Pod) | Ch 6 §1 | Ch 6 §1 | — |
| `.spec.replicas` | Ch 6 §2 | Ch 6 §1 | — |
| `kubectl scale` | Ch 6 §2 | Ch 6 §2 | — |
| Horizontal scaling vs vertical scaling | Ch 6 §2 | Ch 6 §2 | — |
| HPA (HorizontalPodAutoscaler) — **the concept, one sentence** | Ch 6 §2 | Ch 3 | name only, always with a pointer |
| `ownerReferences` | Ch 6 §3 | Ch 4 §5 | name only, always with a pointer |
| Adoption · orphaning | Ch 6 §3 | Ch 6 §3 | — |
| Selector immutability | Ch 6 §3 | Ch 6 §3 | — |
| Cascading deletion | Ch 6 §3 | Ch 6 §3 | — |
| **Rolling update** — the mechanics | Ch 6 §4 | Ch 6 §4 | — · the *vocabulary* of strategies is Ch 15 §2 |
| `maxSurge` · `maxUnavailable` | Ch 6 §4 | Ch 6 §4 | — |
| `Recreate` strategy | Ch 6 §4 | Ch 6 §4 | — |
| Pause / resume rollout | Ch 6 §4 | Ch 6 §4 | — |
| **Revision — the Deployment sense** | Ch 6 §5 | Ch 6 §4 | — · homonym with Helm revision, see Canonical forms |
| Rollout history · `revisionHistoryLimit` | Ch 6 §5 | Ch 6 §5 | — |
| **`kubectl rollout undo`** | Ch 6 §5 | Ch 6 §5 | — · Helm rollback is a different mechanism, Ch 14 §3 |
| **StatefulSet — stable identity** | Ch 6 §6 | Ch 4 | name only, always with a pointer |
| Ordinal index | Ch 6 §6 | Ch 6 §6 | — |
| Stable network identity | Ch 6 §6 | Ch 6 §6 | — |
| DaemonSet | Ch 6 §7 | Ch 6 §7 | — |
| Job | Ch 6 §7 | Ch 3 §6 | name only, always with a pointer *(shipped Ch 3 already defers explicitly)* |
| CronJob · `schedule` | Ch 6 §7 | Ch 6 §7 | — |
| `completions` · `parallelism` · `backoffLimit` | Ch 6 §7 | Ch 6 §7 | — |
| Custom resource | Ch 6 §8 | Ch 6 §8 | — |
| **CRD (CustomResourceDefinition)** | Ch 6 §8 | Ch 2 §8 | name only, always with a pointer |
| **Operator pattern / operator** | Ch 6 §8 | Ch 6 §8 | — |

## Ch 7 — Assigning the Berth  [SHIPPED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| Scheduling | Ch 7 §1 | Ch 3 §2 | gloss in one clause + pointer |
| **Filter → score → bind** | Ch 7 §1 | Ch 7 §1 | — |
| **Binding — the scheduler's** | Ch 7 §1 | Ch 7 §1 | — · homonym with RoleBinding and PV binding, see Canonical forms |
| Random tie-break | Ch 7 §1 | Ch 7 §1 | — |
| Feasible node | Ch 7 §2 | Ch 7 §1 | — |
| Capacity · **Allocatable** | Ch 7 §2 | Ch 7 §2 | — |
| `Unschedulable` (the condition) | Ch 7 §2 | Ch 7 §2 | — |
| PriorityClass | Ch 7 §2 (name + scope only); glossary owns the definition | Ch 7 §2 | — · appears in the Ch 7 answer key, so **not** glossary-only |
| Preemption | Ch 7 §2 (name + scope only); glossary owns the definition | Ch 7 §2 | — · same constraint |
| Node label | Ch 7 §3 | Ch 4 §5 | — |
| `nodeSelector` | Ch 7 §3 | Ch 7 §3 | — |
| Node affinity | Ch 7 §3 | Ch 4 §5 | name only, always with a pointer |
| `requiredDuringSchedulingIgnoredDuringExecution` · `preferred…` | Ch 7 §3 | Ch 7 §3 | — |
| Taint | Ch 7 §4 | Ch 7 §4 | — |
| Toleration | Ch 7 §4 | Ch 7 §4 | — |
| `NoSchedule` · `PreferNoSchedule` · `NoExecute` | Ch 7 §4 | Ch 7 §4 | — |
| Pod affinity · pod anti-affinity | Ch 7 §5 | Ch 7 §5 | — |
| Topology key | Ch 7 §5 | Ch 7 §5 | — |
| `topologySpreadConstraints` · `maxSkew` | Ch 7 §5 | Ch 7 §5 | — |
| `nodeName` (the scheduler bypass) | Ch 7 §6 | Ch 7 §6 | — |
| Scheduling policy vs scheduling profile | Ch 7 §6 | Ch 7 §6 | — |
| Scheduler plugin | Ch 7 §6 | Ch 7 §6 | — |
| Multiple schedulers · `schedulerName` | Ch 7 §6 | Ch 7 §6 | — |

## Ch 8 — Standing the Watch  [SHIPPED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| kubectl | Ch 8 §1 | Ch 4 §1 | gloss in one clause + pointer |
| Verb (kubectl verb) | Ch 8 §1 | Ch 8 §1 | — |
| kubeconfig | Ch 8 §1 | Ch 8 §1 | — |
| Context (kubeconfig context) | Ch 8 §1 | Ch 8 §1 | — |
| In-cluster authentication | Ch 8 §1 | Ch 8 §1 | — |
| **Authentication → authorization → admission** (the three gates) | Ch 8 §2 | Ch 3 §5 | gloss in one clause + pointer |
| Admission controller | Ch 8 §2 | Ch 8 §2 | — |
| Mutating vs validating admission webhook | Ch 8 §2 | Ch 6 §8 | name only, always with a pointer |
| Audit / audit log / audit policy | Ch 8 §2 | Ch 8 §2 | — |
| ResourceQuota | Ch 8 §3 | Ch 8 §3 | — |
| LimitRange | Ch 8 §3 | Ch 8 §3 | — |
| `kubectl cordon` · `drain` · `uncordon` | Ch 8 §4 | Ch 8 §4 | — |
| **Node condition** (`Ready`, `MemoryPressure`, `DiskPressure`, `PIDPressure`, `NetworkUnavailable`) | **Ch 8 §4** | Ch 8 §4 | — · ⚑1 |
| Node lease | Ch 8 §4 | Ch 8 §4 | — |
| Managed vs self-hosted Kubernetes | Ch 8 §5 | Ch 8 §5 | — |
| kubeadm · minikube · kind · k3s | Ch 8 §5 | Ch 8 §5 | — |
| Semantic versioning / SemVer | Ch 8 §6 | Ch 8 §6 | — |
| **Version skew** | Ch 8 §6 | Ch 8 §6 | — |
| Supported releases / the three-minor rule | Ch 8 §6 | Ch 8 §6 | — |
| Release cadence | Ch 8 §6 (stated); **explained** at Ch 17 §8 | Ch 8 §6 | — |
| etcd backup · snapshot · restore | Ch 8 §7 | Ch 3 §2 | name only, always with a pointer |
| Pod Security Admission | Ch 12 §6 | Ch 8 §2 | name only, always with a pointer *(shipped Ch 8 already points forward)* |
| PodDisruptionBudget / PDB | **unowned** | — | see **Orphans** · ⚑3 |

## Ch 9 — Every Pod Has an Address  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| Kubernetes network model (the four requirements) | Ch 9 §1 | Ch 9 §1 † | — |
| Flat network | Ch 9 §1 | Ch 9 §1 † | — |
| **Pod IP** | Ch 9 §1 | Ch 5 §1 | gloss in one clause + pointer |
| NAT-free pod-to-pod traffic | Ch 9 §1 | Ch 9 §1 † | — |
| NAT (Network Address Translation) | Ch 9 §1 (gloss); glossary owns the expansion | Ch 9 §1 † | — |
| **CNI (Container Network Interface)** | Ch 9 §1 | Ch 2 §5 | name only, always with a pointer |
| CNI plugin | Ch 9 §1 | Ch 2 §5 | name only, always with a pointer |
| Calico · Cilium · Flannel (as CNI implementations) | Ch 9 §1 | Ch 9 §1 † | — |
| **Service** (the Kubernetes object) | **Ch 9 §2** | Ch 1 | name only, always with a pointer · ⚑5 |
| ClusterIP | Ch 9 §2 | Ch 9 §2 † | — |
| Virtual IP / VIP | Ch 9 §2 | Ch 9 §2 † | — |
| `port` · `targetPort` · `nodePort` | Ch 9 §3 | Ch 9 §3 † | — |
| NodePort | Ch 9 §3 | Ch 9 §3 † | — |
| LoadBalancer (Service type) | Ch 9 §3 | Ch 9 §3 † | — |
| ExternalName | Ch 9 §3 | Ch 9 §3 † | — |
| Service selector | Ch 9 §4 | Ch 4 §5 | name only, always with a pointer |
| **EndpointSlice** | Ch 9 §4 | Ch 3 §3 | name only, always with a pointer |
| Endpoints (the legacy object) | **orphan — see Part 2** | — | do not use; the *controller*'s two names are reconciled at Ch 9 §4 |
| Headless Service (`clusterIP: None`) | Ch 9 §5 | Ch 6 §6 | name only, always with a pointer |
| Service without selectors | Ch 9 §5 | Ch 9 §5 † | — |
| Readiness gating endpoint membership | Ch 9 §4 | Ch 5 §7 | gloss in one clause + pointer |
| Service proxy | Ch 9 §6 | Ch 3 §3 | gloss in one clause + pointer |
| kube-proxy modes (iptables · IPVS · nftables · userspace) | Ch 9 §6 | Ch 9 §6 † | — |
| **CoreDNS** | Ch 9 §7 | Ch 3 §4 | name only, always with a pointer |
| Cluster DNS | Ch 9 §7 | Ch 3 §4 | name only, always with a pointer |
| A / AAAA record · SRV record | Ch 9 §7 | Ch 9 §7 † | — |
| FQDN (fully qualified domain name) | Ch 9 §7 | Ch 4 §3 | name only, always with a pointer |
| `svc.cluster.local` · search domain | Ch 9 §7 | Ch 9 §7 † | — |
| Pod DNS record | Ch 9 §7 | Ch 9 §7 † | — |

## Ch 10 — Traffic from Beyond the Cluster  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| Edge router | Ch 10 §1 | Ch 10 §1 † | — |
| L4 vs L7 | Ch 10 §1 | Ch 10 §1 † | — |
| North-south vs east-west traffic | Ch 10 §1 | Ch 10 §1 † | — |
| **Ingress** (the object) | Ch 10 §2 | Ch 3 §4 | name only, always with a pointer |
| Ingress rule · host · path · `pathType` | Ch 10 §2 | Ch 10 §2 † | — |
| Simple fanout | Ch 10 §2 | Ch 10 §2 † | — |
| Name-based virtual hosting | Ch 10 §2 | Ch 10 §2 † | — |
| TLS termination | Ch 10 §2 | Ch 4 §4 | name only, always with a pointer |
| Default backend | Ch 10 §2 | Ch 10 §2 † | — |
| **Ingress controller** | Ch 10 §3 | Ch 10 §2 † | — |
| IngressClass | Ch 10 §3 | Ch 10 §3 † | — |
| **"An object without its component does nothing"** (the named pattern) | **Ch 3** coins the sentence; **Ch 10 §3** names it as a pattern | Ch 3 §4 † | quote it VERBATIM — this exact wording now appears 24× across Ch 3/6/10/11/13/17, including a graded Practice option |
| Feature freeze · **frozen ≠ deprecated** | Ch 10 §4 | Ch 10 §4 † | — |
| **Gateway API** | Ch 10 §5 | Ch 10 §4 † | — |
| GatewayClass · Gateway · HTTPRoute | Ch 10 §5 | Ch 10 §5 † | — |
| Role-oriented design (infrastructure provider / cluster operator / application developer) | Ch 10 §5 | Ch 10 §5 † | — |
| **NetworkPolicy** | **Ch 10 §6** | Ch 2 | name only, always with a pointer |
| `podSelector` · `namespaceSelector` · `ipBlock` | Ch 10 §6 | Ch 10 §6 † | — |
| CIDR notation | Ch 10 §6 (gloss); glossary owns the expansion | Ch 10 §6 † | — |
| Ingress rule vs egress rule (policy sense) | Ch 10 §6 | Ch 10 §6 † | — |
| **Additive allow-only semantics / no deny rule** | Ch 10 §6 | Ch 10 §6 † | — |
| Default-deny by selection | Ch 10 §6 | Ch 10 §6 † | — |
| Policy inertness on an unsupporting CNI plugin | Ch 10 §7 | Ch 10 §7 † | — |

## Ch 11 — Below the Waterline  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **Volume** (the Kubernetes volume) | Ch 11 §1 | Ch 4 §4 | gloss in one clause + pointer |
| **The volume lifetime ladder** | Ch 11 §1 | Ch 11 §1 † | — |
| `emptyDir` | Ch 11 §1 | Ch 5 §1 | name only, always with a pointer |
| `hostPath` (and why it is a hazard) | Ch 11 §1 | Ch 11 §1 † | — |
| `configMap` / `secret` volume source | Ch 11 §1 | Ch 4 §4 | gloss in one clause + pointer |
| Projected volume | Ch 11 §1 | Ch 5 §6 | name only, always with a pointer |
| Generic ephemeral volume | Ch 11 §1 | Ch 11 §1 † | — |
| `subPath` | Ch 11 §1 | Ch 11 §1 † | — |
| `downwardAPI` volume | Ch 11 §1 | Ch 11 §1 † | — |
| **PersistentVolume / PV** | Ch 11 §2 | Ch 4 §3 | name only, always with a pointer · ⚑6 |
| **PersistentVolumeClaim / PVC** | Ch 11 §2 | Ch 6 §6 | name only, always with a pointer |
| PV phase (`Available`/`Bound`/`Released`/`Failed`) | Ch 11 §2 | Ch 11 §2 † | — |
| Binding — **the PV/PVC sense** | Ch 11 §2 | Ch 11 §2 † | — · homonym, see Canonical forms |
| **StorageClass** | Ch 11 §3 | Ch 4 §3 | name only, always with a pointer · ⚑6 |
| Static vs dynamic provisioning | Ch 11 §3 | Ch 11 §3 † | — |
| Provisioner | Ch 11 §3 | Ch 11 §3 † | — |
| Default StorageClass | Ch 11 §3 | Ch 11 §3 † | — |
| `volumeBindingMode` · `WaitForFirstConsumer` | Ch 11 §3 | Ch 11 §3 † | — |
| **Access mode** — RWO · ROX · RWX · RWOP | Ch 11 §4 | Ch 11 §2 † | — |
| **Reclaim policy** — `Retain` · `Delete` · `Recycle` | Ch 11 §4 | Ch 11 §4 † | — |
| **CSI (Container Storage Interface)** | Ch 11 §5 | Ch 2 §5 | name only, always with a pointer |
| CSI driver | Ch 11 §5 | Ch 11 §5 † | — |
| In-tree volume plugin · CSI migration | Ch 11 §5 | Ch 11 §5 † | — |
| `volumeClaimTemplates` | Ch 11 §6 | Ch 6 §6 | name only, always with a pointer |

## Ch 12 — Locks, Keys, and Watchstanders  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **The 4Cs** (Cloud, Cluster, Container, Code) | Ch 12 §1 | Ch 12 §1 † | — |
| Cloud native security lifecycle (develop / distribute / deploy / runtime) | Ch 12 §1 | Ch 12 §1 † | — |
| ServiceAccount **as an RBAC subject** | Ch 12 §2 | Ch 5 §6 | — · the object itself is Ch 5 §6 |
| Subject (RBAC subject) | Ch 12 §2 | Ch 12 §2 † | — |
| User · group (as external identities) | Ch 12 §2 | Ch 8 §2 | name only, always with a pointer |
| Service account token | Ch 12 §2 | Ch 5 §6 | gloss in one clause + pointer |
| JWT · OIDC | Ch 12 §2 (name + scope only); glossary owns the definitions | Ch 8 §2 | name only, always with a pointer |
| **RBAC (Role-Based Access Control)** | **Ch 12 §3** | Ch 4 §4 | name only, always with a pointer · ⚑7 |
| Role · ClusterRole | Ch 12 §3 | Ch 12 §3 † | — |
| RoleBinding · ClusterRoleBinding | Ch 12 §3 | Ch 12 §3 † | — |
| Rule · verb · resource (RBAC sense) | Ch 12 §3 | Ch 12 §3 † | — |
| Aggregated ClusterRole | Ch 12 §3 | Ch 12 §3 † | — |
| Default role (`cluster-admin`, `admin`, `edit`, `view`) | Ch 12 §3 | Ch 12 §3 † | — |
| Least privilege | Ch 12 §3 | Ch 4 §4 | name only, always with a pointer |
| **Additive permissions / no deny rule** | Ch 12 §3 | Ch 12 §3 † | — |
| Binding immutability | Ch 12 §3 | Ch 12 §3 † | — |
| **Encryption at rest** · EncryptionConfiguration | Ch 12 §4 | Ch 3 §2 | name only, always with a pointer |
| Secret hardening | Ch 12 §4 | Ch 4 §4 | name only, always with a pointer |
| External secret store | Ch 12 §4 | Ch 4 §4 | name only, always with a pointer |
| **`securityContext`** (Pod and container scope) | Ch 12 §5 | Ch 12 §5 † | — |
| `runAsNonRoot` · `runAsUser` · `privileged` | Ch 12 §5 | Ch 12 §5 † | — |
| Linux capabilities | Ch 12 §5 | Ch 12 §5 † | — |
| `readOnlyRootFilesystem` · `allowPrivilegeEscalation` | Ch 12 §5 | Ch 12 §5 † | — |
| seccomp · AppArmor | Ch 12 §5 | Ch 12 §5 † | — |
| **Pod Security Standards** (`privileged`/`baseline`/`restricted`) | Ch 12 §6 | Ch 8 §2 | name only, always with a pointer |
| **Pod Security Admission** (`enforce`/`audit`/`warn`) | Ch 12 §6 | Ch 8 §2 | name only, always with a pointer |
| PodSecurityPolicy / PSP (**removed**) | Ch 12 §6 (one clause, as retired) | Ch 12 §6 † | — |
| Image scanning · CVE | Ch 12 §7 | Ch 2 | name only, always with a pointer |
| Image signing · attestation · provenance | Ch 12 §7 | Ch 12 §7 † | — |
| **SBOM (Software Bill of Materials)** | Ch 12 §7 | Ch 2 | name only, always with a pointer |
| in-toto · TUF · Notary | Ch 12 §7 | Ch 12 §7 † | — |
| Harbor | Ch 12 §7 | Ch 12 §7 † | — |
| Supply-chain security | Ch 12 §7 | Ch 2 | name only, always with a pointer |
| Policy engine | Ch 12 §8 | Ch 12 §8 † | — |
| OPA (Open Policy Agent) · Gatekeeper | Ch 12 §8 | Ch 12 §8 † | — |
| Kyverno | Ch 12 §8 | Ch 12 §8 † | — |
| Falco | Ch 12 §8 | Ch 12 §8 † | — |

## Ch 13 — When the Cluster Won't Answer  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **Platform scope vs application scope** (the two-audience split) | Ch 13 §1 | Ch 13 §1 † | — |
| Triage flow (scope → phase → conditions → events → logs) | Ch 13 §1 | Ch 13 §1 † | — |
| `ImagePullBackOff` — **diagnosis** | Ch 13 §2 | Ch 2 §6 | name only, always with a pointer · ⚑2 |
| `ErrImagePull` | Ch 13 §2 | Ch 13 §2 † | — |
| `CreateContainerConfigError` | Ch 13 §2 | Ch 13 §2 † | — |
| `ImageInspectError` · `ErrImageNeverPull` | Ch 13 §2 | Ch 13 §2 † | — |
| Event (the Kubernetes object) | Ch 13 §3 | Ch 8 §2 | gloss in one clause + pointer |
| Event retention window | Ch 13 §3 | Ch 13 §3 † | — |
| `kubectl describe` | Ch 13 §3 | Ch 8 §4 | — |
| `kubectl events` | Ch 13 §3 | Ch 13 §3 † | — |
| `kubectl logs` · `--previous` · `-c` · `--all-containers` | Ch 13 §3 | Ch 13 §3 † | — |
| **`CrashLoopBackOff`** | Ch 13 §4 | Ch 5 §4 | name only, always with a pointer |
| **`OOMKilled`** — the signature | Ch 13 §4 | Ch 5 §8 | — · Ch 5 §8 owns the mechanism and already defers |
| **`Evicted`** · node-pressure eviction | Ch 13 §4 | Ch 5 §8 | name only, always with a pointer |
| Eviction order by QoS class | Ch 13 §4 | Ch 5 §8 | gloss in one clause + pointer |
| Reading node conditions as a diagnostic | Ch 13 §5 | Ch 13 §5 † | — · the conditions themselves are **Ch 8 §4** · ⚑1 |
| kubelet health | Ch 13 §5 | Ch 13 §5 † | — |
| **`crictl`** | Ch 13 §5 | Ch 13 §5 † | — |
| Version-skew symptom shapes | Ch 13 §6 | Ch 13 §6 † | — · the rule is Ch 8 §6 |
| **Resource metrics pipeline** | Ch 13 §7 | Ch 13 §7 † | — |
| **metrics-server** | Ch 13 §7 | Ch 3 §4 | name only, always with a pointer |
| `kubectl top` | Ch 13 §7 | Ch 3 §4 | name only, always with a pointer |
| Cluster log architecture | Ch 13 §7 | Ch 13 §7 † | — |
| Node-level logging agent | **Ch 18 §6** | Ch 13 §7 † | gloss in one clause + pointer |

## Ch 14 — Packing for the Voyage  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **Helm** | Ch 14 §2 | Ch 1 | name only, always with a pointer |
| **Chart** | Ch 14 §2 | Ch 1 | name only, always with a pointer |
| `Chart.yaml` · `values.yaml` · `templates/` · `charts/` · `crds/` | Ch 14 §2 | Ch 14 §2 † | — |
| `NOTES.txt` · `_helpers.tpl` | Ch 14 §2 | Ch 14 §2 † | — |
| Subchart | Ch 14 §2 | Ch 14 §2 † | — |
| Go template (in the Helm sense) | Ch 14 §2 | Ch 14 §2 † | — |
| **Release** (Helm) | Ch 14 §3 | Ch 14 §2 † | — · homonym with Kubernetes release, see Canonical forms |
| **Revision — the Helm sense** | Ch 14 §3 | Ch 14 §3 † | — · homonym with Ch 6 §5, see Canonical forms |
| `helm install` · `helm upgrade` | Ch 14 §3 | Ch 14 §3 † | — |
| **`helm rollback`** (distinct mechanism from `kubectl rollout undo`) | Ch 14 §3 | Ch 14 §3 † | — |
| Chart repository | Ch 14 §4 | Ch 14 §4 † | — |
| OCI registry as a chart store | Ch 14 §4 | Ch 14 §4 † | — |
| Chart version vs `appVersion` | Ch 14 §4 | Ch 14 §4 † | — |
| **Kustomize** | Ch 14 §5 | Ch 14 §1 † | — |
| Base · overlay | Ch 14 §5 | Ch 14 §5 † | — |
| `kustomization.yaml` | Ch 14 §5 | Ch 14 §5 † | — |
| Strategic merge patch · JSON patch | Ch 14 §5 | Ch 14 §5 † | — |
| Generator (`configMapGenerator`, `secretGenerator`) | Ch 14 §5 | Ch 14 §5 † | — |
| `kubectl -k` | Ch 14 §5 | Ch 14 §5 † | — |
| Templating vs overlay (the decision) | Ch 14 §6 | Ch 14 §6 † | — |

## Ch 15 — The Chart Is the Truth  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **Twelve-factor app** | Ch 15 §1 | Ch 4 §4 | name only, always with a pointer |
| Factor III (config in the environment) | Ch 15 §1 | Ch 15 §1 † | — |
| **Deployment strategy** (the vocabulary) | Ch 15 §2 | Ch 6 §4 | — · mechanics stay at Ch 6 §4 |
| Blue/green deployment | Ch 15 §2 | Ch 15 §2 † | — |
| Canary deployment | Ch 15 §2 | Ch 15 §2 † | — |
| A/B testing (as a release strategy) | Ch 15 §2 | Ch 15 §2 † | — |
| CI (continuous integration) · CD (continuous delivery/deployment) · CI/CD | Ch 15 §3 | Ch 1 | name only, always with a pointer |
| Push-based delivery vs pull-based delivery | Ch 15 §3 | Ch 15 §3 † | — |
| **GitOps** | Ch 15 §3 | Ch 1 | name only, always with a pointer |
| **OpenGitOps and the four principles** | Ch 15 §3 | Ch 15 §3 † | — |
| Blast radius (of delivery credentials) | Ch 15 §3 | Ch 15 §3 † | — |
| **Argo CD** | Ch 15 §4 | Ch 15 §3 † | — |
| `Application` (the Argo CD custom resource) | Ch 15 §4 | Ch 15 §4 † | — |
| Source of truth | Ch 15 §4 | Ch 15 §3 † | — |
| `Synced` · **`OutOfSync`** | Ch 15 §4 | Ch 15 §4 † | — |
| Sync operation · self-heal | Ch 15 §4 | Ch 15 §4 † | — |
| Drift · drift detection | Ch 15 §4 | Ch 15 §4 † | — |
| Rollback by revert | Ch 15 §4 | Ch 15 §4 † | — |
| Sync hook (`PreSync`/`Sync`/`PostSync`) | Ch 15 §5 | Ch 15 §5 † | — |
| Sync wave | Ch 15 §5 | Ch 15 §5 † | — |
| **Flux** | Ch 15 §6 | Ch 15 §6 † | — |
| Flux controller set (source · kustomize · helm · notification) | Ch 15 §6 | Ch 15 §6 † | — |
| Multi-cluster delivery | Ch 15 §6 | Ch 15 §6 † | — |

## Ch 16 — Your Application, Their Cluster  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **The four triage questions** (running / healthy / reachable / configured) | Ch 16 §1 | Ch 16 §1 † | — |
| Init-container debugging | Ch 16 §2 | Ch 16 §2 † | — · the init sequence is Ch 5 §3 |
| `kubectl exec` | Ch 16 §3 | Ch 3 | name only, always with a pointer |
| **Distroless image** (and the debugging problem it creates) | Ch 16 §3 | Ch 2 | name only, always with a pointer |
| **Ephemeral container** | Ch 16 §3 | Ch 16 §3 † | — |
| **`kubectl debug`** · debug profile · `--copy-to` | Ch 16 §3 | Ch 16 §3 † | — |
| `kubectl debug node/` | Ch 16 §3 | Ch 16 §3 † | — |
| Selector/label mismatch (as a Service failure) | Ch 16 §4 | Ch 16 §4 † | — |
| Empty EndpointSlice (as a symptom) | Ch 16 §4 | Ch 16 §4 † | — |
| **`kubectl port-forward`** | Ch 16 §5 | Ch 3 | name only, always with a pointer |
| Local development loop | Ch 16 §7 | Ch 16 §7 † | — |

## Ch 17 — The Fleet and Its Charts  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **Cloud native** (CNCF definition v1.1, verbatim) | **Ch 17 §1** | Ch 1 | name only, always with a pointer · ⚑4 |
| The named characteristics of cloud native systems | Ch 17 §1 | Ch 17 §1 † | — |
| **CNCF — as an institution** | Ch 17 §1 | Ch 1 | name only, always with a pointer · the exam-sponsor sense is Ch 1 |
| **Project maturity level** (Sandbox · Incubating · Graduated · Archived) | Ch 17 §2 | Ch 17 §2 † | — · homonym with sandboxed runtime, see Canonical forms |
| CNCF project lifecycle | Ch 17 §2 | Ch 17 §2 † | — |
| Governing Board | Ch 17 §2 | Ch 17 §2 † | — |
| TOC (Technical Oversight Committee) | Ch 17 §2 | Ch 17 §2 † | — |
| TAG (Technical Advisory Group) | Ch 17 §2 | Ch 17 §2 † | — |
| End User TAB (Technical Advisory Board) | Ch 17 §2 | Ch 17 §2 † | — |
| CNCF Landscape | Ch 17 §2 | Ch 17 §2 † | — |
| **Microservices** | Ch 17 §3 | Ch 17 §3 † | — |
| Monolith | Ch 17 §3 | Ch 17 §3 † | — |
| **Loose coupling** | Ch 17 §3 | Ch 17 §3 † | — |
| **Immutable infrastructure** | Ch 17 §3 | Ch 17 §3 † | — · distinct from image immutability, Ch 2 §2 |
| Declarative API (as a cloud native characteristic) | Ch 17 §3 | Ch 4 §1 | — |
| **Extension point** | Ch 17 §4 | Ch 2 §4 | name only, always with a pointer |
| API aggregation / aggregation layer | Ch 17 §4 | Ch 17 §4 † | — |
| Device plugin | Ch 17 §4 | Ch 17 §4 † | — |
| **Service mesh** | Ch 17 §5 | Ch 5 §2 | name only, always with a pointer *(Ch 5 already points forward)* |
| **Data plane** | Ch 17 §5 | Ch 5 §2 | name only, always with a pointer |
| **Control plane — the mesh's** | Ch 17 §5 | Ch 17 §5 † | — · homonym with Ch 3 §2, see Canonical forms |
| Envoy | Ch 17 §5 | Ch 17 §5 † | — |
| Sidecar proxy | Ch 17 §5 | Ch 5 §2 | name only, always with a pointer |
| **mTLS (mutual TLS)** | Ch 17 §5 | Ch 4 | name only, always with a pointer |
| **Zero trust** | Ch 17 §5 | Ch 17 §5 † | — |
| Ambient mesh (sidecar-less) | Ch 17 §5 | Ch 17 §5 † | — |
| Istio · Linkerd | Ch 17 §5 | Ch 17 §5 † | — |
| **Serverless** | Ch 17 §6 | Ch 3 | name only, always with a pointer |
| FaaS (Functions as a Service) | Ch 17 §6 | Ch 17 §6 † | — |
| **Knative** · Serving · Eventing · Functions | Ch 17 §6 | Ch 17 §6 † | — |
| **Scale to zero** | Ch 17 §6 | Ch 17 §6 † | — |
| Autoscaling (the landscape) | Ch 17 §7 | Ch 6 §2 | — · the HPA concept is Ch 6 §2 |
| **VPA (VerticalPodAutoscaler)** | Ch 17 §7 | Ch 17 §7 † | — |
| **Cluster Autoscaler** | Ch 17 §7 | Ch 17 §7 † | — |
| **Karpenter** | Ch 17 §7 | Ch 17 §7 † | — |
| **KEDA** | Ch 17 §7 | Ch 17 §7 † | — |
| **SIG (Special Interest Group)** | Ch 17 §8 | Ch 8 §6 | name only, always with a pointer |
| Working Group · Committee · Steering Committee | Ch 17 §8 | Ch 17 §8 † | — |
| Contributor ladder | Ch 17 §8 | Ch 17 §8 † | — |
| **KEP (Kubernetes Enhancement Proposal)** | Ch 17 §8 | Ch 17 §8 † | — |
| SIG Release | Ch 17 §8 | Ch 17 §8 † | — |
| KubeCon + CloudNativeCon | Ch 17 §8 | Ch 17 §8 † | — |
| Code of Conduct | Ch 17 §8 | Ch 17 §8 † | — |
| **The CNCF certification ladder** (KCNA · KCSA · CKA · CKAD · CKS) | Ch 17 §8 | Ch 1 | name only, always with a pointer |

## Ch 18 — Reading the Instruments  [PLANNED]

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| **Observability** | Ch 18 §1 | Ch 1 | name only, always with a pointer |
| **Monitoring** | Ch 18 §1 | Ch 1 | name only, always with a pointer |
| Unknown unknowns vs known unknowns | Ch 18 §1 | Ch 18 §1 † | — |
| Instrumentation | Ch 18 §1 | Ch 18 §1 † | — |
| Telemetry | Ch 18 §1 | Ch 18 §1 † | — |
| **Health checking ≠ observability** | Ch 18 §1 | Ch 18 §1 † | — · probes are Ch 5 §7 |
| **OpenTelemetry / OTel** | Ch 18 §2 | Ch 18 §2 † | — |
| Signal (the OTel sense) | Ch 18 §2 | Ch 18 §2 † | — |
| Trace · metric · log · **baggage** | Ch 18 §2 | Ch 18 §2 † | — |
| OTel Collector | Ch 18 §2 | Ch 18 §2 † | — |
| Time series | Ch 18 §3 | Ch 18 §3 † | — |
| **Metric label** · cardinality | Ch 18 §3 | Ch 18 §3 † | — · homonym with Kubernetes label, see Canonical forms |
| **Utilization relative to requests** | Ch 18 §3 | Ch 18 §3 † | — |
| **metrics-server vs a monitoring system** | Ch 18 §3 | Ch 18 §3 † | — · metrics-server itself is Ch 13 §7 |
| **Prometheus** | Ch 18 §4 | Ch 1 | name only, always with a pointer |
| Pull / scrape model | Ch 18 §4 | Ch 18 §4 † | — |
| Service discovery (Prometheus sense) | Ch 18 §4 | Ch 18 §4 † | — |
| Exporter | Ch 18 §4 | Ch 18 §4 † | — |
| Client library (instrumentation) | Ch 18 §4 | Ch 18 §4 † | — |
| Pushgateway | Ch 18 §4 | Ch 18 §4 † | — |
| **PromQL** | Ch 18 §4 | Ch 18 §4 † | — |
| **Alertmanager** | Ch 18 §4 | Ch 18 §4 † | — |
| **Grafana** | Ch 18 §4 | Ch 18 §4 † | — |
| **Distributed tracing** | Ch 18 §5 | Ch 18 §2 † | — |
| **Span** · root span | Ch 18 §5 | Ch 18 §5 † | — |
| Trace ID · span ID | Ch 18 §5 | Ch 18 §5 † | — |
| Context propagation | Ch 18 §5 | Ch 18 §5 † | — |
| **Jaeger** | Ch 18 §5 | Ch 18 §5 † | — |
| **Node-level logging agent** | Ch 18 §6 | Ch 13 §7 † | gloss in one clause + pointer |
| **Fluentd** · **Fluent Bit** | Ch 18 §6 | Ch 18 §6 † | — |
| Sidecar logging pattern | Ch 18 §6 | Ch 18 §6 † | — |
| Log rotation | Ch 18 §6 | Ch 18 §6 † | — |
| Reliability | Ch 18 §7 | Ch 18 §7 † | — |
| **SLI (Service Level Indicator)** | Ch 18 §7 | Ch 18 §7 † | — |
| **SLO (Service Level Objective)** | Ch 18 §7 | Ch 18 §7 † | — |
| SLA (Service Level Agreement) | Ch 18 §7 (one clause, by contrast) | Ch 18 §7 † | — · see **Orphans** |
| Error budget | Ch 18 §7 | Ch 18 §7 † | — |
| **The four golden signals** (latency · traffic · errors · saturation) | Ch 18 §7 | Ch 18 §7 † | — |
| RED method · USE method | Ch 18 §7 | Ch 18 §7 † | — |

## Ch 19 — Bearings Before Landfall  [PLANNED]

Ch 19 owns no new technical vocabulary. It owns the reader-facing apparatus of the final review.

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| Cross-cutting theme (as an organizing device) | Ch 19 §1 | Ch 19 §1 † | — |
| Confusion pair | Ch 19 §2 | Ch 19 §2 † | — |
| Discriminating question | Ch 19 §2 | Ch 19 §2 † | — |
| Flagging and skipping (exam mechanics) | Ch 19 §3 | Ch 1 | gloss in one clause + pointer |
| The second pass | Ch 19 §3 | Ch 19 §3 † | — |
| Using The Lodestar | Ch 19 §5 | Ch 1 | — · the artifact itself is named in Ch 1 |

## Ambient technical vocabulary — no teaching chapter

These are assumed of an adult professional reader. No chapter defines them; the glossary carries an expansion where the term is an acronym. Any chapter may use them bare.

| Term | Defined by | First appears | Earlier chapters must |
|---|---|---|---|
| API (in the general sense) | glossary-only | Ch 1 | — |
| HTTP · HTTPS · TCP · UDP · IP | glossary-only | Ch 2 | — |
| DNS (**the protocol**; cluster DNS is Ch 9 §7) | glossary-only | Ch 3 §3 | — |
| TLS (**the protocol**; termination is Ch 10 §2, mTLS is Ch 17 §5) | glossary-only | Ch 4 | — |
| JSON · YAML | glossary-only | Ch 4 §2 | — |
| REST · gRPC | glossary-only | Ch 2 | — |
| CLI · shell | glossary-only | Ch 1 | — |
| CPU · RAM · GPU · SSD · I/O | glossary-only | Ch 2 §1 | — |
| OS · kernel · process · PID | glossary-only | Ch 2 §1 | — |
| Git · repository · branch · tag · commit | glossary-only | Ch 1 | — · Git *as source of truth* is Ch 15 §3 |
| UID · GUID | glossary-only | Ch 4 §2 | — |
| SSH | glossary-only | Ch 5 | — |
| Load balancing (**the general technique**) | glossary-only | Ch 3 §1 | — |

## Acronym register

An index of surface forms, not a second ownership claim. Every acronym the book uses appears here exactly once, pointing at the ledger row that owns it. **Every acronym is expanded on its first use in the book, without exception**, even where the expansion is obvious.

| Acronym | Expansion | Owning row |
|---|---|---|
| A/B | (not an acronym — A/B testing) | Ch 15 §2 |
| ABAC | Attribute-Based Access Control | glossary-only — see **Orphans** |
| API | Application Programming Interface | ambient |
| CA | Cluster Autoscaler | Ch 17 §7 |
| CD | Continuous Delivery / Continuous Deployment | Ch 15 §3 |
| CI | Continuous Integration | Ch 15 §3 |
| CIDR | Classless Inter-Domain Routing | Ch 10 §6 |
| CKA | Certified Kubernetes Administrator | Ch 17 §8 |
| CKAD | Certified Kubernetes Application Developer | Ch 17 §8 |
| CKS | Certified Kubernetes Security Specialist | Ch 17 §8 |
| CNCF | Cloud Native Computing Foundation | Ch 1 (sponsor) / Ch 17 §1 (institution) |
| CNI | Container Network Interface | Ch 9 §1 |
| CRD | CustomResourceDefinition | Ch 6 §8 |
| CRI | Container Runtime Interface | Ch 2 §4 |
| CRI-O | (a proper name, not an expansion) | Ch 2 §4 |
| CSI | Container Storage Interface | Ch 11 §5 |
| CVE | Common Vulnerabilities and Exposures | Ch 12 §7 |
| DNS | Domain Name System | ambient / Ch 9 §7 |
| FaaS | Functions as a Service | Ch 17 §6 |
| FQDN | Fully Qualified Domain Name | Ch 9 §7 |
| GPU | Graphics Processing Unit | ambient |
| HPA | HorizontalPodAutoscaler | Ch 6 §2 |
| IaaS | Infrastructure as a Service | Ch 3 §1 |
| IPVS | IP Virtual Server | Ch 9 §6 |
| JWT | JSON Web Token | Ch 12 §2 |
| K8s | Kubernetes (numeronym) | Ch 3 §1 |
| KCNA | Kubernetes and Cloud Native Associate | Ch 1 |
| KCSA | Kubernetes and Cloud Native Security Associate | Ch 17 §8 |
| KEDA | Kubernetes Event-Driven Autoscaling | Ch 17 §7 |
| KEP | Kubernetes Enhancement Proposal | Ch 17 §8 |
| L4 / L7 | OSI Layer 4 / Layer 7 | Ch 10 §1 |
| LTS | Long-Term Support | glossary-only — see **Orphans** |
| mTLS | mutual Transport Layer Security | Ch 17 §5 |
| NAT | Network Address Translation | Ch 9 §1 |
| OCI | Open Container Initiative | Ch 2 §5 |
| OIDC | OpenID Connect | Ch 12 §2 |
| OOM | Out Of Memory | Ch 13 §4 (via `OOMKilled`) |
| OPA | Open Policy Agent | Ch 12 §8 |
| OTel | OpenTelemetry | Ch 18 §2 |
| PaaS | Platform as a Service | Ch 3 §1 |
| PDB | PodDisruptionBudget | **unowned** — see **Orphans** |
| PromQL | Prometheus Query Language | Ch 18 §4 |
| PSA | Pod Security Admission | Ch 12 §6 |
| PSP | PodSecurityPolicy (removed in 1.25) | Ch 12 §6 |
| PSS | Pod Security Standards | Ch 12 §6 |
| PV | PersistentVolume | Ch 11 §2 |
| PVC | PersistentVolumeClaim | Ch 11 §2 |
| QoS | Quality of Service | Ch 5 §8 |
| RBAC | Role-Based Access Control | Ch 12 §3 |
| RED | Rate, Errors, Duration | Ch 18 §7 |
| REST | Representational State Transfer | ambient |
| ROX | ReadOnlyMany | Ch 11 §4 |
| RWO | ReadWriteOnce | Ch 11 §4 |
| RWOP | ReadWriteOncePod | Ch 11 §4 |
| RWX | ReadWriteMany | Ch 11 §4 |
| SaaS | Software as a Service | Ch 3 §1 |
| SBOM | Software Bill of Materials | Ch 12 §7 |
| SemVer | Semantic Versioning | Ch 8 §6 |
| SIG | Special Interest Group | Ch 17 §8 |
| SLA | Service Level Agreement | Ch 18 §7 |
| SLI | Service Level Indicator | Ch 18 §7 |
| SLO | Service Level Objective | Ch 18 §7 |
| SRE | Site Reliability Engineering | glossary-only — see **Orphans** |
| TAB | Technical Advisory Board | Ch 17 §2 |
| TAG | Technical Advisory Group | Ch 17 §2 |
| TLS | Transport Layer Security | ambient |
| TOC | Technical Oversight Committee | Ch 17 §2 |
| TUF | The Update Framework | Ch 12 §7 |
| USE | Utilization, Saturation, Errors | Ch 18 §7 |
| VIP | Virtual IP | Ch 9 §2 |
| VM | Virtual Machine | Ch 2 §1 |
| VPA | VerticalPodAutoscaler | Ch 17 §7 |
| WG | Working Group | Ch 17 §8 |

---

> **Acronym-register debt recorded 2026-08-30 (Ch 9 integration gate).** Four acronyms first
> appear in Ch 9 and are absent from the register below: **CNAME**, **BGP**, **eBPF**, and
> **IPVS** (registered, but unexpanded at its first appearance in the book, which is Ch 9 §6).
> Expand IPVS in place at Ch 9 §6 and add all four to the register at the glossary build.
> eBPF additionally needs its glossary entry written — Ch 9 now names it twice with a
> "see the glossary" pointer, and its Practice Q16 distractor was rebuilt from taught
> material so that no graded item depends on it, per this ledger's own ruling.

> **Register and ambient-tier debt recorded 2026-08-30 (Ch 10 integration gate).**
> **SNI** (Server Name Indication) and **OSI** (Open Systems Interconnection) are now expanded
> at their first use in Ch 10 — both had been reaching graded text unexpanded (SNI in a
> Soundings answer, OSI in a Practice stem) and neither has a register row. Add both, plus a
> glossary entry for SNI, at the glossary build.
> **reverse proxy** has 7 uses in Ch 10 including a Soundings answer, no owner, and no ambient
> tier. Defensible as ambient for this reader, but it currently sits in graded text with no
> lookup path: assign it to the ambient tier or give it a glossary entry. Lowest priority.

> **Glossary debt recorded 2026-08-30 (Ch 11 integration gate).** Six terms need entries at the glossary build: **NFS** (Network File System), **LUN** (Logical Unit Number), **iSCSI**, **EBS** (Elastic Block Store), **finalizer**, and **`CSIDriver`**. NFS, LUN and EBS are now expanded at first use in Ch 11; NFS in particular carries two graded Practice items (Q7, Q11) and had never been spelled out anywhere in the book. iSCSI appears only inside quoted documentation, so it needs a register row rather than an in-text expansion.

> ⛑ **BOOK-LEVEL CONVENTION, ratified 2026-08-30 at the Ch 8 gate: state the pattern, never the count.**
> Running ordinals across chapters have now caused two collisions in this book, both of which reached shipped text and had to be repaired at a later chapter's gate:
>
> - **Control loops.** Ch 8 said the node controller was "the sixth"; Ch 9 said kube-proxy was "the sixth" too. Worse, shipped Ch 6 closes by telling the reader they have seen the loop *twice* and that "the third time is the one that matters" — which is **Ch 15 §7, the book's designated primary Zenith**. A reader who had been counting to six would arrive at that Zenith with the recognition already spent. Both ordinals are now removed.
> - **Pluggable interfaces.** Ch 9 §8 called CNI "the second instance"; Ch 10 and Ch 11 count to three. Reconciled by a half-clause in Ch 10.
>
> **The rule for every chapter from 12 on:** name the pattern and say it is the same one, but do **not** assert a running ordinal ("the fourth time", "the sixth control loop", "you now have three of four") unless the count is fixed by a closed set the reader can see in front of them — the four pluggable interfaces, the four domains. Ch 6's two-altitudes framing and Ch 15 §7's payoff are the only sanctioned control-loop count in the book, and no chapter may add to it.

> **Glossary queue and stale rows recorded 2026-08-30 (Ch 8 gate).** Needed at the glossary build: mutating/validating admission webhook, CIDR (also expand in place at Ch 8 §4), kubelet TLS bootstrapping, hugepages, Eviction API. `context` is now defined in Ch 8 §1 and no longer owes one.
> Rows this ledger gets wrong, recorded so no later stage "corrects" a chapter toward them: **node registration** is not taught in Ch 3 — Ch 8 §4 is the de facto owner and should keep it; **`kubectl describe`** first appears in Ch 5, not Ch 8 §4; **mutating vs validating admission webhook** does not appear in Ch 6 at all (zero occurrences of "webhook"); **CIDR**'s first reader-facing use is Ch 8 §4, not Ch 10 §6.

> **Glossary debt recorded 2026-08-31 (Ch 13 gate).** **static Pod** and **mirror Pod** are absent from Ch 1-12 and first appear in Ch 13 Practice Q13's distractor D, where the answer key refutes it with a sourced quotation. **Ruling: the distractor stays.** This is not the Ch 9 eBPF case -- there the ledger had explicitly ruled the term out of graded text and the book defined it nowhere, so the distractor was rebuilt. Here the key teaches both terms inline with a source and targets a real belief about hidden containers. What they lack is a lookup path: add glossary entries for both at the glossary build, plus a register row. Also queued from this chapter: `crictl`, `ProgressDeadlineExceeded`.

> **Ledger errata found at the Ch 17 gate (2026-08-31).**
> - The absent-component pattern row carried the WRONG SENTENCE and the WRONG COINER. Ch 17
>   followed it faithfully, handing back the book's most-reinforced retrieval phrase in words
>   the reader had never seen. Chasing it found Ch 6 teaching the wrong wording too — inside
>   the very instruction "Name the pattern, because you will retrieve it by name." Row fixed;
>   Ch 6, Ch 13 and Ch 17 aligned; the phrase is now identical in all 24 uses. This is the
>   clearest case in the commission of a ledger defect propagating into shipped text.
> - `VPA | First appears Ch 17 §7` is wrong: VPA first appears in shipped Ch 3 (line 606) and
>   again in Ch 10 (lines 678, 1811).
> - Headword **"Ambient mesh (sidecar-less)" → "ambient mode"** — Istio's own documented term
>   and what the sources say. Ch 17 uses "ambient mode" 11× and is correct; the ledger was not.
> - The **FaaS** register row is orphaned.
> - **CKAD** and **CKS** are now expanded at Ch 17 §8. **SIG** is first used unexpanded at Ch 8
>   line 861 — a pre-existing Ch 8 debt. **CloudEvents** needs a glossary entry and register row.

> ⛑ **BOOK-LEVEL RULING, ratified 2026-08-31 at the Ch 18 gate: a cross-bearing to the owning chapter discharges the `[source:]` obligation for a retrieved claim.**
> Ch 18 §4's AUTHOR-REVIEW asked for this and correctly noted there is no later content chapter to defer it to. The rule, in three parts:
>
> 1. A claim **first taught and source-tagged in its owning chapter** may be retrieved elsewhere behind a `*[cross-bearing: see Ch N §M — …]*` pointer **without repeating the tag**. The pointer is the citation: it is traceable, and the owning section carries the snapshot. Re-tagging every retrieval would duplicate ~15 snapshots across the book and invite exactly the drift the ledger exists to prevent.
> 2. The pointer must name the **owning section**, not the chapter at large, and the retrieved claim **must not be strengthened** beyond what the owner sourced. A retrieval that sharpens, generalizes or adds a number is a new claim and needs its own tag.
> 3. This does **not** apply to a claim the owning chapter itself left untagged. Those stay gaps wherever they appear.
>
> Applies to the seven Kubernetes claims Ch 18 §4 raised (probe semantics, metrics-server scope, DaemonSet placement, scheduler placement, the CRI boundary, StatefulSet identity), all of which are owned and tagged in Ch 2/5/6/7 and correctly pointered here. **Fact-accuracy stages should stop re-raising this class.**

# Part 2 — Orphans

Ten terms have no owner, or an owner that the shipped text does not honor. Each carries a recommendation. Where a term reaches graded material, it is called out — **a term used in question text or an answer key may not be glossary-only**, because a reader who meets it there has no place to look it up mid-question.

### Endpoints (the legacy object) — **unowned, and correctly so**

Moved here from Ch 9 §4 at the 2026-08-30 integration gate. The ledger assigned the legacy
`Endpoints` object to Ch 9 §4 and the Canonical forms table reserved the capitalized form for
that section's contrast, but the shipped chapter never mentions it — and **no snapshot in the
168-file corpus describes it**. Writing the sentence would have meant asserting an unsourced
claim in a book whose every factual sentence carries a tag.

What the reader actually needs at associate tier is already there: Ch 9 §4 reconciles the
**controller**'s two documented names (*EndpointSlice controller* and the older *endpoints
controller*) explicitly, three times. That is the confusion the exam can reach. The legacy
*object* is a `kubectl api-resources` artifact, not blueprint material.

**Recommendation: leave unowned.** If a later pass wants it, it needs a fetch first — the
EndpointSlice concept page's own comparison to the Endpoints API — and one clause in Ch 9 §4,
not a section. Until then no chapter should use the capitalized bare form.

### ⚑3 — PodDisruptionBudget / PDB — **unowned**

The B6 skeleton assigns "PodDisruptionBudget interaction" to Ch 8 §4. The shipped Ch 8 contains **zero occurrences** of `PodDisruptionBudget`, `PDB`, or even the substring `disruption`. Ch 8 §4 teaches `cordon`/`drain`/`uncordon` and states that `kubectl drain` evicts the Pods, with nothing about what may block or shape that eviction.

**Recommendation: assign to Ch 8 §4 as a one-clause gloss, via a minimal retrofit.** The clause belongs where `drain` is taught — "a PodDisruptionBudget caps how many replicas a voluntary eviction may take down at once, which is why a drain can stall" — because that is the only place in the book where the reader has a question a PDB answers. Until that clause exists, the term is **not eligible for graded question text or an answer key anywhere in the book**, including the Ch 20 mock, and Ch 13 §4 must not reach for it when explaining `Evicted`.

Do not route this to the glossary alone. B1 does not list PDB among the blocking gaps, so this is not a coverage failure — it is a one-sentence hole created when the skeleton's plan for Ch 8 §4 outran what the chapter shipped.

### ⚑ SLA (Service Level Agreement) — **assign to Ch 18 §7**

Not named in the lineup or the skeleton; the skeleton gives Ch 18 §7 only SLI, SLO, error budgets, and the golden signals. SLA is the near-universal third member of that acronym family and the natural distractor in any SLI/SLO item.

**Recommendation: Ch 18 §7 owns it as a one-clause contrast** — the externally committed, contractual number, as against the internally chosen SLO and the measured SLI. **Not glossary-only:** it will appear in Ch 18 and Ch 20 answer keys as a wrong option, and a distractor the reader cannot look up is a badly built distractor.

### ABAC (Attribute-Based Access Control) — **glossary-only**

Kubernetes supports several authorization modes; RBAC is the one the curriculum teaches. ABAC has no teaching value here and is not on the exam blueprint.

**Recommendation: glossary-only.** Ch 12 §3 may name it in a single clause establishing that RBAC is *an* authorization mode rather than *the* authorization mechanism. It **must not** appear as a distractor unless that clause is written, because "authorization modes other than RBAC exist" is the only fact about it the book will have supplied.

### SRE (Site Reliability Engineering) — **glossary-only**

The provenance of SLIs, SLOs, error budgets, and the golden signals, but not itself an exam object.

**Recommendation: glossary-only.** Ch 18 §7 may attribute the golden signals to SRE practice in passing. Not eligible for graded text.

### LTS (Long-Term Support) — **glossary-only, with a hazard note**

Kubernetes has no LTS release. This is a live misconception for readers arriving from distributions that do, and it sits directly against Ch 8 §6's three-minor support window.

**Recommendation: glossary-only for the expansion; the *fact* belongs to Ch 8 §6** as a ⚠ Navigational Hazards line — "there is no Kubernetes LTS; support is three minor versions and roughly a year." Shipped Ch 8 §6 does not say this. If the retrofit is made, the fact becomes eligible for graded use; until then, no question may hinge on it.

### descheduler — **glossary-only**

Not in the curriculum. Ch 7 §6 covers overruling and replacing the scheduler without needing it.

**Recommendation: glossary-only, or omit.** Not eligible for graded text.

### eBPF — **glossary-only**

Reachable from three directions (CNI dataplanes at Ch 9 §1, kube-proxy alternatives at Ch 9 §6, Falco at Ch 12 §8) and owned by none of them. The curriculum does not require it.

**Recommendation: glossary-only.** Any of the three sections may name it as an implementation detail with a pointer to the glossary. Not eligible for graded text.

### PodSecurityPolicy / PSP — **assign to Ch 12 §6, as retired**

Removed in Kubernetes 1.25. It appears throughout the pre-2025 prep material B2's disclosure #3 warns readers about, which makes its *absence* the load-bearing fact.

**Recommendation: Ch 12 §6 owns a single clause naming it as removed and superseded by Pod Security Admission.** Eligible for graded use *only* as a wrong option in a Pod Security Admission item, never as a correct one.

### Kubernetes Dashboard — **owned, but thinly**

Ch 3 §4 names it as an addon example. Nothing downstream retrieves it.

**Recommendation: leave ownership at Ch 3 §4; no action.** Recorded here only so a later stage does not mistake its thinness for an orphan.

---

# Part 3 — Canonical forms

One headword per concept. Variants listed here are **sanctioned** — each is reserved for a stated purpose, and any surface form not listed is drift.

### Homonyms — the same word, two concepts

These are the pairs most likely to produce a reader who thinks they have met a term before. In every case, **the second appearance must explicitly mark itself as the other sense.**

| Headword | Sense A (owner) | Sense B (owner) | Rule |
|---|---|---|---|
| **namespace** | Linux namespace — the kernel isolation primitive (Ch 2 §1) | Namespace — the Kubernetes object (Ch 4 §3) | Sense A is always written **"Linux namespace"**, lowercase, never bare after Ch 2 §1. Sense B is capitalized **"Namespace"** when it means the object, lowercase "namespace" when it means the scope. Ch 4 §3 must open by disposing of the collision explicitly. |
| **control plane** | The cluster's control plane (Ch 3 §2) | A service mesh's control plane (Ch 17 §5) | Sense B is always **"the mesh's control plane"** or **"the service mesh control plane"** on first use in Ch 17 §5, and the section must say in one clause that this is a different control plane from Ch 3 §2's. Bare "control plane" always means sense A. |
| **sandbox** | Sandboxed runtime — gVisor, Kata (Ch 2 §7) | CNCF **Sandbox** — the maturity level (Ch 17 §2) | Sense A is **"sandboxed runtime"**, adjectival, never the bare noun. Sense B is capitalized **"Sandbox"** and always appears alongside at least one sibling level (Incubating, Graduated). A confusion-pair row in Ch 19 §2. |
| **revision** | Deployment revision (Ch 6 §5) | Helm release revision (Ch 14 §3) | Sense B is always **"release revision"** or **"Helm revision"**, never bare, and Ch 14 §3 owns the explicit contrast. |
| **rollback** | `kubectl rollout undo` (Ch 6 §5) | `helm rollback` (Ch 14 §3) | Never write bare "rollback" where either could be meant. Ch 14 §3 owns the statement that these are different mechanisms wearing the same word. A third sense — GitOps rollback-by-revert (Ch 15 §4) — is always written **"rollback by revert"**. |
| **label** | Kubernetes label (Ch 4 §5) | Prometheus metric label (Ch 18 §3) | Sense B is always **"metric label"** on first use in Ch 18 §3 and in any sentence where a Kubernetes object is also present. |
| **request** | Resource request (Ch 5 §8) | API request (Ch 8 §2) | Sense A is **"resource request"** in any sentence that also discusses the API server. Sense B is **"API request"** in any sentence that also discusses scheduling or QoS. Bare "request" is permitted only where the section's whole subject makes it unambiguous. |
| **binding** | Scheduler binding (Ch 7 §1) | PV/PVC binding (Ch 11 §2) | Neither may be written bare outside its own chapter. `RoleBinding`/`ClusterRoleBinding` (Ch 12 §3) are object names, always in code style, and are never shortened to "binding". |
| **release** | A Kubernetes release — a minor version (Ch 8 §6) | A Helm release — an installed chart instance (Ch 14 §3) | Sense B is **"Helm release"** on first use in each Ch 14/15 section. Sense A is "Kubernetes release" or "minor release". |
| **Service** | The Kubernetes Service object (Ch 9 §2) | A Knative Service (Ch 17 §6) | Sense B is always **"Knative Service"**, never bare. Generic English "service" (a running application) stays lowercase and is avoided wherever a Kubernetes Service is in the same paragraph. |
| **immutable** | Image immutability (Ch 2 §2) | Immutable infrastructure (Ch 17 §3) | Sense B is always the full two-word phrase **"immutable infrastructure"**. Ch 17 §3 back-bears to Ch 2 §2 rather than re-deriving. |
| **operator** | The operator pattern (Ch 6 §8) | A human operator | Never use "operator" for a person. Write "cluster administrator" or, in the Gateway API role split, **"cluster operator"** — which is a *role name*, always two words, and Ch 10 §5 must say so. |
| **volume** | The Kubernetes volume (Ch 11 §1) | A Docker volume | Sense B is not used. Where a contrast is needed, write "a Docker volume". |
| **plugin** | CNI plugin (Ch 9 §1) · scheduler plugin (Ch 7 §6) · admission plugin (Ch 8 §2) · device plugin (Ch 17 §4) | — | Never bare. Always qualified by its interface. |

### Headwords with sanctioned variants

| Headword | Sanctioned variants | Reserved for |
|---|---|---|
| **node controller** | `node controller` | The controller in kube-controller-manager. Lowercase, two words. **"Node controller" (capitalized) and "node lifecycle controller" are drift** — do not use either. |
| **admission controller** | `admission controller` · `admission plugin` · `admission webhook` | *Admission controller* is the headword and the general term. *Admission plugin* names a specific compiled-in one (`NodeRestriction`, `LimitRanger`) — use only when naming one. *Admission webhook* names the extensible out-of-process form, always qualified **mutating** or **validating**. Never treat the three as interchangeable in one sentence. |
| **Kubernetes** | `Kubernetes` · `K8s` | Spell it out everywhere in body prose. `K8s` appears only where the book is discussing the abbreviation itself (Ch 3 §1), in quoted material, or inside a URL or resource name. Never `k8s` lowercase in prose. |
| **cloud native** | `cloud native` | **Never hyphenated.** Matches the CNCF definition v1.1 that Ch 17 §1 quotes verbatim, including attributive use ("cloud native architecture"). ⚑ Shipped Chapters 1, 2, 3, 4, and 8 contain **16 hyphenated instances** of "cloud-native" alongside the unhyphenated form. **Recommended edit (author's call): a cosmetic sweep normalizing all of them to "cloud native."** Not load-bearing, but the book quotes the CNCF's own unhyphenated wording and should not disagree with itself two paragraphs later. |
| **Pod** | `Pod` · `pod` | Capitalized when it means the API object, which is nearly always. Lowercase only inside `kubectl` output, resource names, and the phrase "pod networking" (which is the CNI documentation's own wording). |
| **ServiceAccount** | `ServiceAccount` · `service account` | CamelCase for the object. Two lowercase words for the general idea of a non-human identity, and for the phrase "service account token". |
| **Secret** | `Secret` · `secret` | Capitalized for the Kubernetes object. Lowercase for the general noun ("a database secret"), which should be avoided near the object. |
| **StatefulSet · DaemonSet · ReplicaSet · CronJob · ConfigMap · EndpointSlice · StorageClass · PersistentVolume · PersistentVolumeClaim · RuntimeClass · NetworkPolicy · CustomResourceDefinition · LimitRange · ResourceQuota · PodDisruptionBudget · IngressClass · GatewayClass · HTTPRoute · PriorityClass** | exact CamelCase, unspaced | Object names are never spaced ("Stateful Set"), never lowercased in prose, and never pluralized inside the CamelCase ("StatefulSets" is correct; "StatefulsSet" and "Stateful Sets" are not). |
| **kubectl** | `kubectl` | Always lowercase, always code style, even sentence-initially — recast the sentence rather than capitalize. |
| **etcd** | `etcd` | Always lowercase, even sentence-initially. Recast rather than capitalize. |
| **CRI-O** | `CRI-O` | Exactly this. Not `CRIO`, not `cri-o`, not `CRI-o`. |
| **containerd** | `containerd` | Always lowercase, one word. |
| **runC** | `runC` | Lowercase r, capital C. Not `RunC`, not `runc` in prose (though `runc` is correct inside a command or path). |
| **Argo CD** | `Argo CD` | Two words, both capitalized. **Not `ArgoCD`, not `Argo-CD`.** The project's own form. |
| **Flux** | `Flux` | Not `FluxCD`. Where disambiguation from the older v1 is needed, write "Flux v2". |
| **Fluentd · Fluent Bit** | `Fluentd` · `Fluent Bit` | Fluentd is one word; Fluent Bit is two. This asymmetry is correct and is itself a plausible exam-adjacent detail. |
| **Gateway API** | `Gateway API` · `Gateway` | *Gateway API* names the whole project and specification. Bare *Gateway* names only the resource kind, always in a sentence where GatewayClass or HTTPRoute is also present. Never use bare "Gateway" to mean the API. |
| **Ingress** | `Ingress` · `ingress` | Capitalized for the object and the controller ("Ingress controller"). Lowercase for the direction of traffic in a NetworkPolicy ("ingress rules", "ingress isolation"). Ch 10 carries both senses in adjacent sections — §2 and §6 — and each must mark which it means. |
| **Endpoints** | `EndpointSlice` · `Endpoints` · `endpoints` | *EndpointSlice* is the current object and the default headword. *Endpoints* (capitalized, code style) names the legacy object, which no chapter now teaches — see the Part 2 orphan entry before using it anywhere. Lowercase *endpoints* means the backend addresses generally. |
| **twelve-factor app** | `twelve-factor app` | Hyphenated, spelled out. Not `12-factor`, not `12 Factor`. |
| **scale to zero** | `scale to zero` · `scale-to-zero` | Unhyphenated as a verb phrase ("Knative can scale to zero"), hyphenated only as a compound modifier ("scale-to-zero behavior"). |
| **worker node** | `node` · `worker node` | *Node* is the headword and covers both the object and the machine. *Worker node* is used only where the contrast with control-plane nodes is the point. **"Minion" is retired and must not appear.** |
| **container runtime** | `container runtime` · `runtime` | Spell out on first use in each chapter. Bare *runtime* is permitted afterward within the same section only, and never in a section that also discusses the OCI runtime spec. |
| **the four pluggable interfaces** | `the four pluggable interfaces` | The book's own phrase for CRI + CNI + CSI + CRDs. Ch 17 §4 owns it and the shipped Ch 2 §4 already points at that exact wording. Do not paraphrase it as "the four extension points" — the Kubernetes documentation's own list of extension points is longer, and Ch 17 §4 covers both. |
| **Taking Your Bearings** | `Taking Your Bearings` | Never "Bearings" alone in reader-facing text. "Bearings" is permitted in pipeline and planning documents only. |

---

## Summary of flags

| # | Flag | Where | Recommended action |
|---|---|---|---|
| ⚑1 | Node conditions are fully defined in shipped Ch 8 §4 (conditions table, `kubectl describe node`); the B6 skeleton also lists them under Ch 13 §5 | Ch 8 §4 ↔ Ch 13 §5 | Ownership stays at **Ch 8 §4**. Ch 13 §5 retrieves them as a diagnostic and must not restate the table. No edit to shipped text. |
| ⚑2 | `ImagePullBackOff` is substantively defined in shipped Ch 2 §6 and Ch 5 §5 (as a container-state `Reason`), not in Ch 13 | Ch 2 §6 / Ch 5 §5 ↔ Ch 13 §2 | Split stands: the **string and its taxonomic slot** are Ch 2 §6 + Ch 5 §5; **diagnosis** is Ch 13 §2. The published pointer already reads "diagnosing ImagePullBackOff," so no edit is needed — but Ch 13 §2 must not re-teach the phase/state taxonomy. |
| ⚑3 | PodDisruptionBudget is assigned to Ch 8 §4 by B6 and appears nowhere in shipped Ch 8 | Ch 8 §4 | One-clause retrofit at Ch 8 §4, or the term stays out of all graded material. Author's call. |
| ⚑4 | "Cloud native" is used 40× in Ch 1 and defined at Ch 17 §1 | Ch 1 → Ch 17 §1 | **By design** — Ch 1 § *The Phrase We Haven't Defined Yet* plants it deliberately. No action. |
| ⚑5 | "Service" is used 45× across Ch 1–8 before Ch 9 §2 defines it | Ch 1–8 → Ch 9 §2 | **Handled** — shipped Ch 3 §3 states outright that "Service is a Kubernetes object with its own chapter." Ch 9 §2 still owns it. No action. |
| ⚑6 | PersistentVolume and StorageClass appear in Ch 4 graded question text and a figure, seven chapters before Ch 11 defines them | Ch 4 §3 → Ch 11 §2–§3 | **Tolerable** — they are used purely as examples of cluster-scoped resources, and the question tests scope, not storage. No edit. Recorded so no later stage widens that use. |
| ⚑7 | RBAC appears in Ch 4 §4 (inside a sourced quote), Ch 5, Ch 6, and Ch 8 before Ch 12 §3 defines it | Ch 4–8 → Ch 12 §3 | All uses are name-only. Ch 12 §3 retains ownership. Verify during Ch 12 drafting that no earlier chapter has quietly defined a `Role` or a binding. |
| ⚑8 | 16 hyphenated "cloud-native" instances in shipped Ch 1, 2, 3, 4, 8, against the unhyphenated CNCF form the book will quote at Ch 17 §1 | Ch 1–8 | Cosmetic sweep to "cloud native". Author's call; not load-bearing. |

---

*Stage B7 complete. 19 chapters with owned vocabulary, plus an ambient tier and a 74-entry acronym register. Nine orphans routed: two assigned to a chapter, one requiring an author decision, six declared glossary-only with graded-use restrictions stated. Eight flags, none of which reassigns a shipped chapter's ownership. No term in the ledger has two owners; eleven words carry two concepts and are split with a sanctioned surface form for each.*