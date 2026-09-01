---
title: "The Lodestar — KCNA"
subtitle: "Back-of-Book Reference"
tagline: "Study less. Pass once."
publisher: "Lodestar Ledgers"
edition: "First Edition"
exam_version: "KCNA curriculum effective 2025-11-24 (4 domains: 44/28/16/12)"
---

# The Lodestar — KCNA

*One page. Read it the week before. Work it in the last hour. Then close it.*

This is a **distillation, not a summary**. There are no chapter recaps here, no explanations, no worked examples, and no context — every line assumes you have read the chapter it came from. If you cannot reconstruct a chapter from its lines here, you have not found a defect in this page. You have found a chapter to go back to. *[cross-bearing: see Ch 19 §5 — using The Lodestar]*

**How to work it in the last hour.** Two passes, about twenty minutes each, with a break between. **First pass — drill:** cover the right-hand column of the discriminator blocks and the hazard block, work down, mark every hesitation. Do not look anything up; the point is to *find* soft spots, not fix them. **Second pass — lookup:** read the marked items and the number blocks, once, calmly. Then stop. Whatever is not in your head by then will not arrive in the next twenty minutes, and a third pass costs composure and buys nothing.

---

## 1. The exam's published shape — *lookup*

| Fact | Value | Where it is published |
|---|---|---|
| Duration | **90 minutes**, timer cannot be paused | KCNA exam page **and** candidate handbook |
| Questions | **60**, multiple choice | Candidate handbook, "Multiple Choice Exams: Important Instructions" |
| Passing score | **75%** | Candidate handbook, MC exam FAQ |
| Format | Online, proctored, multiple choice | KCNA exam page |
| Attempts | Two included · 12-month eligibility · valid 2 years | KCNA exam page |
| Prerequisites | None | KCNA exam page |

**The provenance point, because it is the one people get wrong.** All three numbers are published by the Linux Foundation — but for multiple-choice exams **as a class**, in the candidate handbook, not on the KCNA product page most candidates read. They are official. They are just not where you would look. *[cross-bearing: see Ch 1 § Ninety Minutes: The Exam as Published]*

### Domain weights

| # | Domain | Weight | Chapters |
|---|---|---|---|
| 1 | Kubernetes Fundamentals | **44%** | 2–8 |
| 2 | Container Orchestration | **28%** | 9–13 |
| 3 | Cloud Native Application Delivery | **16%** | 14–16 |
| 4 | Cloud Native Architecture | **12%** | 17–18 |

The 2025-11-24 revision **doubled** Application Delivery from 8% to 16% and folded the old standalone Observability domain into Cloud Native Architecture. Material written against the five-domain blueprint under-serves D3 badly. *[cross-bearing: see Ch 1 § What Changed, and What It Costs You]*

---

## 2. Exam-day pacing — *memorize; there is no scratch paper*

> **★ Read the question count off the screen. Divide the clock by it. Reach the end of the paper at roughly 60% of your total time, and hold the remaining 40% in reserve.**

On 90 minutes that is the end of the first pass at about the **54-minute mark**, with ~36 minutes left. You do not need the count in advance — you read it, you divide, you go.

- **Don't know it?** Answer anyway, then mark it. A blank scores zero with certainty; no wrong-answer penalty is published in either direction.
- **The failure mode this guards against** is spending four minutes on question nine.
- **Check the console on the tutorial screen**, before the clock matters: is there a flag/mark control, and will it let you move backward? Thirty seconds of checking buys you the shape of the next ninety minutes.

---

## 3. The four hazards where intuition is wrong — *drill*

| The intuition | What is actually true |
|---|---|
| `ReadWriteOnce` means one Pod | It means one **node**. Multiple Pods *on that node* can share it. `ReadWriteOncePod` is the one that means one Pod |
| `storageClassName: ""` is the same as omitting it | `""` means **no class** — bind only to a PV that also has none. Omitting it means "whatever the cluster's default behavior is" |
| A second default IngressClass is ambiguous | It is worse: it **removes** the default, and the Ingress can no longer be created at all |
| Phase `Running` means working | It means bound, containers created, at least one running **or starting or restarting**. A crash-looping Pod reports `Running` |

---

## 4. The version-skew numbers — *lookup, but read it twice*

| Component | Rule |
|---|---|
| **kubelet** | Up to **three** minor versions older than kube-apiserver. **Never newer** |
| **`kubectl`** | Within **one** minor version, **either direction**. The only component permitted to be newer |
| **Supported releases** | **Three** supported minors · ~1 year of patch support · ~3 minor releases per year |

> ⚠ The kubelet rule and the `kubectl` rule are **different rules**, and candidates routinely apply the first to the second. *kubelet: three minors, older only. `kubectl`: one minor, either direction.* Not the same number, not the same shape.

---

## 5. The confusion-pair discriminators — *drill*

Cover the right column. Work down. Uncover. This is the block that repays a second pass.

### Domain 1 — Kubernetes Fundamentals

| Pair | The one-line test |
|---|---|
| Pod phase vs container state | Phase = the whole Pod's position in its lifecycle. State = one container, right now |
| liveness vs readiness vs startup | Liveness **restarts**. Readiness **removes from endpoints**, no restart. Startup **suspends the other two** while booting |
| labels vs annotations | Does anything *select* on it? Labels yes, annotations no |
| image tag vs digest | Mutable pointer, or identity? A tag can be moved; a digest cannot |
| ConfigMap vs Secret | Would you mind seeing it in a log? Secret is base64-**encoded**, not encrypted |
| namespace vs label | Namespace is a *scope* boundary. Label is a *selection* attribute |
| ResourceQuota vs LimitRange | Total, or default? Quota caps the namespace's aggregate. LimitRange sets per-object defaults |
| Deployment vs StatefulSet | Does replica 0 need to **be** replica 0? It is about **identity**, not disk |
| DaemonSet vs "replicas = node count" | DaemonSet tracks nodes joining and leaving. A number does not know what a node is |
| Job vs CronJob | CronJob is the factory; Job is the product |
| taints/tolerations vs node affinity | Who refuses? Taint = the **node** repels. Affinity = the **Pod** asks |
| OCI vs CRI | OCI = the artifact and its execution. CRI = the kubelet's API to a runtime |
| scheduler binds / kubelet starts | Scheduler decides and writes it down. Kubelet does the starting |
| scheduled once vs rescheduled | A Pod is bound **once** and never moved. "Rescheduling" is a *new* Pod |
| `restartPolicy` scope | Governs **containers within a Pod**, not the Pod object |

### Domain 2 — Container Orchestration

| Pair | The one-line test |
|---|---|
| ClusterIP / NodePort / LoadBalancer | Reachable from where? Each type **includes** the one beneath it |
| headless vs broken vs selectorless | Headless is `clusterIP: None` **on purpose**. Broken is a selector matching nothing |
| Ingress object vs controller | The record versus the thing that acts on it |
| Ingress frozen vs deprecated | **Frozen** = feature-complete, still supported. Deprecated would mean scheduled for removal. Ingress is frozen |
| NetworkPolicy default | Is this Pod selected by *any* policy? No → fully open. Yes → union of what its policies allow |
| NetworkPolicy needs both ends | A→B needs A's egress **and** B's ingress |
| RBAC has no deny | Permissions are the union of every binding naming you. Nothing subtracts |
| view / edit / admin | `view` reads (not Secrets). `edit` writes workloads. `admin` manages RBAC **within a namespace**. None is `cluster-admin` |
| PV vs PVC | Supply versus demand. A Pod references a **PVC**, never a PV |
| Retain / Delete / Recycle | Retain keeps it for manual reclamation. Delete removes both. **Recycle is deprecated** |
| empty slice vs slice that serves nothing | Empty list = **selector** problem. Listed but not ready = **readiness** problem |
| `Pending` → don't reach for logs | No containers yet, so nothing produced output. Read the phase, then events |

### Domain 3 — Cloud Native Application Delivery

| Pair | The one-line test |
|---|---|
| chart vs release vs revision | Chart = package. Release = one installed instance. Revision = a numbered version of that release |
| `charts/` vs chart repository | `charts/` is a **directory inside a chart** holding subcharts. A repository is a **remote place charts come from** |
| Kustomize overlay vs Helm template | Patch, or render? Kustomize patches a valid manifest. Helm renders one that was not a manifest until values arrived |
| `rollout undo` vs `helm rollback` | Whose history? A **Deployment's** revisions, or a **release's** |
| rolling / Recreate / blue-green / canary | What happens to the old version? Incremental / all stopped first / both then switch / a fraction |
| GitOps push vs pull | Where do the credentials live? Outside reaching in, or inside reaching out |
| `OutOfSync` = drift, not error | It reports a **difference**. That is a status, not a failure |
| platform vs application scope | Is the Pod running the way Kubernetes intended? If yes and the app misbehaves, it is the application |

### Domain 4 — Cloud Native Architecture

| Pair | The one-line test |
|---|---|
| mesh vs cluster control plane | The cluster's is kube-apiserver/etcd/scheduler/controller-manager. A mesh's configures proxies |
| sidecar vs ambient mode | Proxy per **Pod**, or per **node** |
| Knative Serving vs Eventing | Serving = HTTP request-driven, scale to zero. Eventing = asynchronous routing |
| maturity-level ordering | Sandbox → Incubating → Graduated. *Which project sits where is not a memorization target* |
| TOC vs Governing Board | Technical, or business? Board = marketing, business oversight, budget |
| End User TAB vs TOC | The TAB **advises** and voices end users. The TOC holds the technical vision |
| SIG vs Working Group vs Committee | SIGs are ongoing and own a topic. WGs are **time-bounded** and cross SIGs. Committees have closed membership |
| TAG vs SIG | TAGs are **CNCF-level** across projects. SIGs are **Kubernetes-project-level** |
| horizontal vs vertical scaling | More replicas, or bigger ones |
| HPA vs VPA | HPA is core API. **VPA is an add-on** you deploy |
| workload vs node autoscaling | HPA/VPA/KEDA change *workloads*. Cluster Autoscaler and Karpenter change the *cluster* |
| observability vs monitoring | New questions, or known ones |
| span vs trace | One unit of work, or the whole tree following one request |
| SLI vs SLO vs SLA | Measure, target, or consequence |
| Prometheus pull vs Pushgateway | Prometheus scrapes. The Pushgateway is for jobs that **cannot be scraped** |


### Surface-form homonyms — one word, two meanings

| Word | Sense A | Sense B |
|---|---|---|
| **namespace** | Linux kernel isolation primitive | Kubernetes scope object |
| **control plane** | The cluster's | A service mesh's |
| **sandbox** | Sandboxed runtime (gVisor, Kata) | CNCF Sandbox maturity level |
| **revision** | Deployment revision | Helm release revision |
| **rollback** | `kubectl rollout undo` | `helm rollback` — and rollback by revert |
| **label** | Kubernetes label | Prometheus metric label |
| **request** | Resource request | API request |
| **binding** | Scheduler binding | PV/PVC binding — and RoleBinding |
| **release** | A Kubernetes minor release | A Helm release |
| **Service** | The Kubernetes object | A Knative Service |
| **immutable** | Image immutability | Immutable infrastructure |
| **operator** | The operator pattern | "Cluster operator" as a Gateway API role |
| **volume** | A directory the containers share | A PersistentVolume with its own lifecycle |

---

## 6. Governance and institutional vocabulary — *lookup; the cheapest block to refresh*

This is the Domain 4 material most likely to have gone soft, and it is bounded — which is exactly why it is worth a pass.

| Body | What it does |
|---|---|
| **CNCF Governing Board** | Marketing, business oversight, budget decisions |
| **TOC** (Technical Oversight Committee) | Technical vision; project acceptance and lifecycle |
| **End User TAB** | The **voice of end users**; advisory, not governing |
| **TAG** | CNCF-level, coordinates interests **across projects** |
| **Kubernetes SIG** | Project-level, ongoing, owns a topic area |
| **Working Group** | **Time-bounded**, spans SIGs |
| **Committee** | Closed membership; does not always operate in public |
| **Steering Committee** | Kubernetes project governance |

- **Maturity levels:** Sandbox → Incubating → Graduated.
- **Proposing a change:** a **KEP**, brought to the SIG that owns the subsystem.
- **Release cadence:** three minor releases a year, roughly every fifteen weeks.
- **The certification ladder:** KCNA is pre-professional, feeding CKA (Certified Kubernetes Administrator), CKAD (Application Developer) and CKS (Security Specialist).


---

## 7. The one sentence to carry in

> **An object without its component does nothing.**

A `type: LoadBalancer` Service with no provider. A Service whose selector matches no Pods. An Ingress with no Ingress controller. A NetworkPolicy on a plugin that does not implement it. An HPA with no metrics-server. One rule, five instances, and the first instinct is always "something is misconfigured" when the answer is "something is not installed."

---

*Chart → Passage → Dawn. Close the book. Go and pass it.*
