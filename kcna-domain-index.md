---
title: "Domain-to-Chapter Index — KCNA"
subtitle: "Back-of-Book Reference"
tagline: "Study less. Pass once."
publisher: "Lodestar Ledgers"
edition: "First Edition"
exam_version: "KCNA curriculum effective 2025-11-24 (4 domains: 44/28/16/12)"
---

# Domain-to-Chapter Index

A cross-reference from the published KCNA curriculum to the chapters that cover it. Use it two ways: to allocate study time in proportion to domain weight, and — when a mock exam shows you weak in one domain — to find the chapters that answer for it without re-reading the book.

**On the numbers below.** CNCF publishes four domains with weights, and names the competencies inside them. It publishes **no sub-weights and no topic list**. The per-chapter percentages in this book are authored judgment derived from concept count and prerequisite load; they are marked as such wherever they appear, and they are not a claim about how many questions you will see.

| Domain | Weight | Competencies | Chapters |
|---|---|---|---|
| **1 — Kubernetes Fundamentals** | **44%** | Core Concepts · Administration · Scheduling · Containerization | 2–8 |
| **2 — Container Orchestration** | **28%** | Networking · Security · Troubleshooting · Storage | 9–13 |
| **3 — Cloud Native Application Delivery** | **16%** | Application Delivery · Debugging | 14–16 |
| **4 — Cloud Native Architecture** | **12%** | Observability · Cloud Native Ecosystem and Principles · Cloud Native Community and Collaboration | 17–18 |

---

## Domain 1 — Kubernetes Fundamentals (44%)

### Containerization (Chapter 2 · ~9%)

| Topic | Chapter |
|---|---|
| Containers versus virtual machines; what isolation actually is | 2 §1 |
| Image anatomy, layers, copy-on-write | 2 §2 |
| Registries; tags versus digests; immutability | 2 §3 |
| Container Runtime Interface (CRI); containerd, CRI-O | 2 §4 |
| Open Container Initiative — image, runtime, distribution specs; runC | 2 §5 |
| `imagePullPolicy` and the tag-conditional default | 2 §6 |
| Sandboxed runtimes and RuntimeClass | 2 §7 |
| Build practices | 2 §2, 2 §8 |

### Kubernetes Core Concepts (Chapters 3–6 · ~25%)

| Topic | Chapter |
|---|---|
| Deployment eras; what Kubernetes is and is not; origin and history | 3 §1 |
| Control-plane components | 3 §2 |
| Node components | 3 §3 |
| Addons | 3 §4 |
| The API server as the only door in | 3 §5 |
| Controllers, the control loop, desired versus current state | 3 §6 |
| Objects; `spec` and `status`; manifests and required fields | 4 §1, 4 §2 |
| Namespaces; namespaced versus cluster-scoped; initial namespaces | 4 §3 |
| ConfigMaps and Secrets | 4 §4 |
| Labels, selectors (equality and set-based), annotations | 4 §5 |
| `kubectl apply` and declarative management | 4 §1, 4 §6 |
| The Pod; shared network namespace | 5 §1 |
| Multi-container Pods; init containers; sidecars | 5 §2, 5 §3 |
| Pod replacement and ephemerality | 5 §4 |
| Pod phases and container states; `restartPolicy`; restart backoff | 5 §5 |
| ServiceAccount as Pod identity | 5 §6 |
| Liveness, readiness and startup probes | 5 §7 |
| Resource requests and limits; QoS classes; graceful termination | 5 §8 |
| ReplicaSet; ownership and adoption | 6 §1, 6 §3 |
| Deployment; rolling update; `maxSurge`/`maxUnavailable`; Recreate | 6 §4 |
| Revisions, rollout history, rollback, pause and resume | 6 §5 |
| StatefulSet (identity) | 6 §6 |
| DaemonSet; Job; CronJob | 6 §7 |
| Custom resources, CRDs, the operator pattern | 6 §8 |
| Manual scaling; the HPA concept | 6 §2 |

### Scheduling (Chapter 7 · ~5%)

| Topic | Chapter |
|---|---|
| Filter, score, bind; the random tie-break | 7 §1 |
| Feasible nodes; unschedulable Pods; Capacity and Allocatable | 7 §2 |
| Node labels; `nodeSelector`; node affinity (required and preferred) | 7 §3 |
| Taints and tolerations — `NoSchedule`, `PreferNoSchedule`, `NoExecute` | 7 §4 |
| Pod affinity and anti-affinity; topology spread constraints | 7 §5 |
| `nodeName`; scheduling policies versus profiles; PriorityClass | 7 §6 |

### Administration (Chapter 8 · ~5%)

| Topic | Chapter |
|---|---|
| `kubectl` syntax and verbs; kubeconfig and contexts; in-cluster auth | 8 §1 |
| The three API access gates — authentication, authorization, admission | 8 §2 |
| Auditing; ResourceQuota and LimitRange | 8 §3 |
| Node lifecycle — cordon, drain, uncordon; node conditions; leases | 8 §4 |
| Cluster planning; managed versus self-hosted; kubeadm, minikube, kind, k3s | 8 §5 |
| Semantic versioning; supported releases; version skew; release cadence | 8 §6 |
| etcd backup | 8 §7 |

---

## Domain 2 — Container Orchestration (28%)

### Networking (Chapters 9–10 · ~12%)

| Topic | Chapter |
|---|---|
| The Kubernetes network model; Pod IP; CNI | 9 §1 |
| Service and ClusterIP; the address that does not last | 9 §2 |
| Service types — ClusterIP, NodePort, LoadBalancer, ExternalName; port mechanics | 9 §3 |
| Selectors, EndpointSlice, readiness and endpoint membership | 9 §4 |
| Headless Services; Services without selectors | 9 §5 |
| The service proxy; kube-proxy modes | 9 §6 |
| CoreDNS; Service and Pod DNS records; FQDN and search domains | 9 §7 |
| Ingress; TLS termination; name-based virtual hosting; simple fanout | 10 §1, 10 §2 |
| Ingress controllers; IngressClass; the edge router | 10 §3 |
| The Ingress freeze and the Gateway API recommendation | 10 §4 |
| Gateway API — GatewayClass, Gateway, HTTPRoute; role-oriented design | 10 §5 |
| NetworkPolicy — ingress and egress isolation, selectors, `ipBlock`, additive semantics | 10 §6 |
| What NetworkPolicy cannot do; plugin dependency | 10 §7 |

### Storage (Chapter 11 · ~5%)

| Topic | Chapter |
|---|---|
| Volume types — `emptyDir`, `hostPath`, ConfigMap/Secret, projected, ephemeral | 11 §1 |
| PersistentVolume and PersistentVolumeClaim; binding; PV phases | 11 §2 |
| StorageClass; static versus dynamic provisioning; `volumeBindingMode` | 11 §3 |
| Access modes (RWO/ROX/RWX/RWOP); reclaim policies (Retain/Delete/Recycle) | 11 §4 |
| Container Storage Interface (CSI) | 11 §5 |
| StatefulSet storage pairing; `volumeClaimTemplates` | 11 §6 |

### Security (Chapter 12 · ~7%)

| Topic | Chapter |
|---|---|
| The 4Cs; the cloud native security lifecycle phases | 12 §1 |
| ServiceAccounts; TokenRequest; identity as an RBAC subject | 12 §2 |
| RBAC — Role, ClusterRole, RoleBinding, ClusterRoleBinding; additive permissions | 12 §3 |
| Secret types and hardening; encryption at rest | 12 §4 |
| `securityContext`; what a Pod may do to its node | 12 §5 |
| Pod Security Standards and Pod Security Admission | 12 §6 |
| Supply-chain security — scanning, signing, SBOM, in-toto, TUF, Harbor | 12 §7 |
| Policy engines — OPA, Kyverno, Falco | 12 §8 |
| NetworkPolicy as the network half of security | 12 §9 *(taught at 10 §6–§7)* |

### Troubleshooting (Chapter 13 · ~4%)

| Topic | Chapter |
|---|---|
| The two-audience split — platform scope versus application scope | 13 §1 |
| Pods that never start — `Pending`, `ImagePullBackOff`, `ErrImagePull`, `CreateContainerConfigError` | 13 §2 |
| `kubectl describe`, `events`, `logs --previous`; event retention | 13 §3 |
| Pods that start then fail — `CrashLoopBackOff`, `OOMKilled`, `Evicted` | 13 §4 |
| Node health and conditions; `crictl` | 13 §5 |
| Version-skew symptoms | 13 §6 |
| The resource metrics pipeline; metrics-server; `kubectl top` | 13 §7 |

---

## Domain 3 — Cloud Native Application Delivery (16%)

This domain **doubled** in the 2025-11-24 revision, from 8% to 16%. It is the largest proportional change on the blueprint, and material written against the retired five-domain blueprint under-serves it.

### Application Delivery (Chapters 14–15 · ~12%)

| Topic | Chapter |
|---|---|
| Why a folder of YAML stops working | 14 §1 |
| Helm chart structure — `Chart.yaml`, `values.yaml`, `templates/`, `charts/`, `crds/` | 14 §2 |
| Chart, release, revision; upgrade and rollback | 14 §3 |
| Chart repositories; `helm repo`, OCI registries as chart stores | 14 §4 |
| Kustomize — base and overlay; patching instead of templating | 14 §5 |
| When each fits | 14 §6 |
| The twelve-factor app | 15 §1 |
| Deployment strategies — rolling, Recreate, blue/green, canary, A/B | 15 §2 |
| CI/CD versus GitOps; push versus pull; the four OpenGitOps principles | 15 §3 |
| Argo CD — controller model, Git as source of truth, `OutOfSync`, drift, sync | 15 §4 |
| Sync ordering — phases and waves | 15 §5 |
| Flux; multi-cluster delivery | 15 §6 |

### Debugging (Chapter 16 · ~4%)

| Topic | Chapter |
|---|---|
| The handoff from platform scope; the four triage questions | 16 §1 |
| Debugging init containers | 16 §2 |
| `kubectl exec`; ephemeral containers; `kubectl debug`; distroless images | 16 §3 |
| Application-side Service debugging — selectors, empty EndpointSlice, `port` versus `targetPort` | 16 §4 |
| `port-forward` as a diagnostic that skips the Service path | 16 §5 |
| StatefulSet debugging from the application side | 16 §6 |
| Local development and debugging loops | 16 §7 |

---

## Domain 4 — Cloud Native Architecture (12%)

Observability was a **standalone domain** on the retired blueprint and is now a competency inside this one. If your other study material has an "Observability" domain, it is out of date.

### Cloud Native Ecosystem and Principles (Chapter 17 · ~5%)

| Topic | Chapter |
|---|---|
| The CNCF cloud native definition and its characteristics | 17 §1 |
| Project maturity — Sandbox, Incubating, Graduated; the CNCF Landscape | 17 §2 |
| Microservices; loose coupling; immutable infrastructure; declarative APIs | 17 §3 |
| The extension points collected — CRI, CNI, CSI, CRDs, aggregation, webhooks, device plugins | 17 §4 |
| Service mesh — data versus control plane, Envoy, mTLS, sidecar versus ambient mode | 17 §5 |
| Serverless and Knative — Serving, Eventing, Functions, scale to zero | 17 §6 |
| The autoscaling landscape — HPA, VPA, KEDA, Cluster Autoscaler, Karpenter | 17 §7 |

### Cloud Native Community and Collaboration (Chapter 17 · ~2%)

| Topic | Chapter |
|---|---|
| Governing Board, TOC, TAGs, End User TAB | 17 §8 |
| Kubernetes SIGs, Working Groups, Committees, Steering | 17 §8 |
| The contributor ladder; KEPs; release cadence | 17 §8 |
| KubeCon; the Code of Conduct; participation paths | 17 §8 |
| The CNCF certification ladder — KCNA, KCSA, CKA, CKAD, CKS | 17 §8 |

*This is the competency technically strong candidates most reliably under-study, which is why it has its own numbered section rather than a footnote.*

### Observability (Chapter 18 · ~5%)

| Topic | Chapter |
|---|---|
| Observability versus monitoring; unknown unknowns | 18 §1 |
| Instrumentation and telemetry | 18 §2 |
| The resource metrics pipeline; utilization versus requests | 18 §3 |
| OpenTelemetry — traces, metrics, logs, baggage; the Collector | 18 §4 |
| Spans, root spans, distributed tracing; Jaeger | 18 §5 |
| Prometheus — pull model, time series, PromQL, exporters, Pushgateway, Alertmanager | 18 §6 |
| Reliability, SLI, SLO, and the golden signals | 18 §7 |
| Logging architecture; node-level agents; Fluentd and Fluent Bit; Grafana | 18 §8 |

---

## Chapters that belong to no domain

| Chapter | What it is for |
|---|---|
| **1 — Taking Departure** | Exam mechanics, the 2025-11-24 blueprint change, and how to read this book |
| **19 — Bearings Before Landfall** | Synthesis: the cross-cutting threads, the confusion pairs, exam-day pacing, the final week |
| **20 — Full Mock Exam** | A calibrated 60-question mock weighted 26/17/10/7, with worked answers and a per-domain score sheet |

---

## Using this index after a mock

Chapter 20's score sheet gives you a per-domain tally. Read it **proportionally, not absolutely** — losing 3 of 7 in Domain 4 is a worse signal than losing 5 of 26 in Domain 1, even though the second number is larger.

Then come back here, find the domain, and work only the sections listed against the questions you missed. Re-reading a whole chapter to fix two wrong answers is the most common way candidates spend a week and move nothing.
