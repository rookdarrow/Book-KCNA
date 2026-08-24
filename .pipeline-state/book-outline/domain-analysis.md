# Domain Analysis — KCNA

**Book:** Kubernetes and Cloud Native Associate
**Exam:** KCNA (CNCF / The Linux Foundation)
**Curriculum version:** effective no earlier than 2025-11-24 (four-domain blueprint)
**Analysis date:** 2026-08-23
**Sources:** cached authoritative set (CNCF curriculum PDF, LF exam page, LF program-changes page, kubernetes.io docs, OCI, OpenGitOps, 12factor.net, Prometheus, OpenTelemetry, Istio, Helm, Argo CD, Knative, cncf/toc, kubernetes/community)

---

## Exam facts (established from sources)

| Fact | Value | Source authority |
|---|---|---|
| Format | Online, proctored, **multiple-choice** | LF exam page |
| Duration | 90 minutes | LF exam page |
| Experience level | Beginner; **no prerequisites** | LF exam page |
| Attempts included | 2 | LF exam page |
| Eligibility window | 12 months from purchase | LF exam page |
| Certification validity | 2 years | LF exam page |
| Domains | 4 (44 / 28 / 16 / 12) | LF exam page + CNCF curriculum PDF + LF program-changes |
| **Question count** | **Not published.** Third-party sources widely report 60; LF does not state it. | LF exam page explicitly notes this is unpublished |
| **Passing score** | **Not published.** Third-party sources widely report 75%; LF does not state it. | LF exam page explicitly notes this is unpublished |

**⚠ Authoring constraint:** the book must not assert 60 questions / 75% as fact. Where pacing guidance or the Mock Exam requires a question count, state the commonly-reported figure *as commonly reported*, cite that LF does not publish it, and frame Mock Exam sizing as a calibrated choice rather than a match to a published count. This directly engages Ethical Guardrail #1 (never create false beliefs about exam content) and #8 (distinguish "frequently tested" from "might be tested").

**Blueprint transition note.** The prior five-domain blueprint was Kubernetes Fundamentals 46% / Container Orchestration 22% / Cloud Native Architecture 16% / Cloud Native Observability 8% / Cloud Native Application Delivery 8%. Under the 2025-11-24 revision, Observability was folded into Cloud Native Architecture, Container Orchestration rose 22→28%, and Application Delivery rose 8→16%. Legacy study material sized to the old blueprint under-weights Application Delivery by half and treats Observability as a standalone domain. The book should note this explicitly in front matter — a large volume of third-party KCNA prep still targets the five-domain split.

---

## Domain inventory

Objective numbering below (D1.1, D1.2, …) is a **Lodestar convention**. CNCF publishes named competencies under each domain but does **not** number them and does **not** publish sub-competency weights. The `Weight %` column is stated only at domain level because that is the only level the sources state.

| Domain | Weight % | Objectives (competencies as published) | Expected depth | Notes |
|---|---|---|---|---|
| **D1 — Kubernetes Fundamentals** | **44%** | D1.1 Kubernetes Core Concepts · D1.2 Administration · D1.3 Scheduling · D1.4 Containerization | **Comprehension.** Name every control-plane and node component and state what it does; read a manifest and identify apiVersion/kind/metadata/spec; distinguish the workload resources by use case; describe the scheduler's two-step filter→score→bind flow. Not configuration-level: no hands-on, no YAML authoring under time pressure. | Largest domain by a wide margin — nearly half the exam. Sub-competency weights unpublished; allocate chapter weight by concept count and prerequisite load, not by guessing splits. Core Concepts is the load-bearing sub-competency: almost every other domain depends on it. |
| **D2 — Container Orchestration** | **28%** | D2.1 Networking · D2.2 Security · D2.3 Troubleshooting · D2.4 Storage | **Comprehension, with diagnostic reasoning.** Given a symptom, name the likely cause and the object to inspect. Distinguish the four Service types and when each applies; state the two NetworkPolicy isolation directions; distinguish PV from PVC from StorageClass; distinguish Role from ClusterRole and RoleBinding from ClusterRoleBinding. | Rose from 22% to 28% in the 2025-11-24 revision — the second-biggest weight and the biggest *increase* by absolute points alongside Application Delivery. Troubleshooting is the thinnest-covered competency in the cached sources (index-level only) and needs the most supplementary research. |
| **D3 — Cloud Native Application Delivery** | **16%** | D3.1 Application Delivery · D3.2 Debugging | **Comprehension.** State the four OpenGitOps principles; describe what a Helm chart contains and what a release is; explain what OutOfSync means in Argo CD; recognize the 12-factor principles by name and intent. Debugging: know which kubectl verb answers which question. | **Doubled** from 8% to 16% in the revision — the single largest proportional change. Legacy prep material badly under-serves this domain. D3.2 Debugging overlaps heavily with D2.3 Troubleshooting; treat the distinction as *application-scope* (D3.2) vs *cluster/platform-scope* (D2.3) and cross-bear between the chapters rather than duplicating. |
| **D4 — Cloud Native Architecture** | **12%** | D4.1 Observability · D4.2 Cloud Native Ecosystem and Principles · D4.3 Cloud Native Community and Collaboration | **Recall and recognition.** Name the three OpenTelemetry signal types plus Baggage; distinguish metric from log from span from trace; state the three CNCF maturity levels in order; distinguish SIG from Working Group from Committee; recite the CNCF cloud-native definition's characteristics. | Smallest domain but the highest *breadth-to-depth ratio* — lots of names, few mechanics. Absorbed the former standalone 8% Observability domain, so ~8 of these 12 points may still be observability-flavored, though CNCF does not publish that split. D4.3 is pure institutional knowledge and is the competency most likely to be under-studied by technically-strong candidates. |

**Domain-weight arithmetic check:** 44 + 28 + 16 + 12 = 100. All four weights are explicitly stated in three independent cached sources (CNCF curriculum PDF, LF exam page, LF program-changes page) and agree.

**Curriculum-text errata:** the CNCF-published KCNA_Curriculum.pdf contains the typo "**Could** Native Community and Collaboration" for the D4.3 competency. Correct reading is "Cloud". Worth a one-line footnote in the book's blueprint appendix — candidates who download the PDF will see it and wonder.

---

## Concept map

One-line definitions only. Grouped by domain and competency. Every entry below is attested in the cached sources; concepts I believe are examinable but *not* attested are listed in **Gaps in sources**, not here.

### D1.1 — Kubernetes Core Concepts

| Concept | One-line definition |
|---|---|
| Cluster | A control plane plus a set of worker machines (nodes) that run containerized applications. |
| Control plane | The components that make global decisions about the cluster and respond to cluster events. |
| Node (worker) | A machine that hosts the Pods forming the application workload; every cluster needs at least one. |
| kube-apiserver | The control-plane front end that exposes the Kubernetes HTTP API; scales horizontally by adding instances. |
| etcd | Consistent, highly-available key-value store used as the backing store for all cluster data. |
| kube-scheduler | Control-plane component that watches for unscheduled Pods and selects a node for each. |
| kube-controller-manager | Control-plane component running the built-in controller processes, compiled into one binary. |
| cloud-controller-manager | Optional control-plane component embedding cloud-provider-specific control logic; absent on-prem. |
| kubelet | Per-node agent ensuring the containers described in PodSpecs are running and healthy. |
| kube-proxy | Optional per-node network proxy maintaining the node network rules that implement Services. |
| Container runtime | Per-node software managing container execution and lifecycle (containerd, CRI-O, any CRI implementation). |
| Addons | Optional cluster extensions: DNS, Dashboard, container resource monitoring, cluster-level logging. |
| Kubernetes object | A persistent entity representing cluster state; a "record of intent". |
| spec | The nested field describing an object's **desired** state; you set it at creation. |
| status | The nested field describing an object's **current** state; supplied and updated by the system. |
| Manifest | A file (conventionally YAML) describing an object, applied with `kubectl apply -f`. |
| apiVersion / kind / metadata / spec | The four required fields of an object manifest. |
| Controller | A non-terminating control loop that watches state and drives current state toward desired state. |
| Control loop / reconciliation | The thermostat pattern: compare desired vs current, act to close the gap, repeat forever. |
| Control via API server | The common controller pattern: the controller tells the API server to create/remove objects rather than acting directly. |
| Direct control | The less common pattern where a controller communicates with a system *outside* the cluster (e.g. node provisioning). |
| Pod | A set of one or more running containers, co-located and co-scheduled on the same node. |
| Pod phase | Pending, Running, Succeeded, Failed, Unknown. |
| Container state | Waiting, Running, Terminated — a per-container state, distinct from Pod phase. |
| restartPolicy | Pod-level field: Always (default), OnFailure, Never; applies to all containers in the Pod. |
| Restart backoff | Exponential kubelet restart delay (10s, 20s, 40s …) capped at five minutes; resets after 10 minutes of clean running. |
| Liveness probe | Diagnostic indicating whether a container is running; failure kills the container per restart policy. |
| Readiness probe | Diagnostic indicating whether a container can serve requests; failure removes its IP from Service endpoints. |
| Startup probe | Diagnostic gating the other probes until the app has started; failure kills the container. |
| Probe mechanisms | exec, grpc, httpGet, tcpSocket. |
| Deployment | Workload resource for stateless applications where any Pod is interchangeable. |
| ReplicaSet | The controller a Deployment manages to hold a Pod count (replaces the legacy ReplicationController). |
| StatefulSet | Workload resource for related Pods that track state, typically each matched with a PersistentVolume. |
| DaemonSet | Workload resource scheduling one Pod per matching node, for node-local facilities. |
| Job | Workload resource defining a task that runs to completion once. |
| CronJob | Workload resource running a Job repeatedly on a schedule. |
| Namespace | A mechanism for isolating groups of resources within a single cluster; provides a scope for names. |
| Initial namespaces | default, kube-system, kube-public, kube-node-lease. |
| Namespaced vs cluster-scoped | Deployments/Services are namespaced; Nodes, PersistentVolumes, StorageClasses, and namespaces themselves are not. |
| Label | Key/value pair attached to an object to specify identifying attributes; the basis of grouping. |
| Annotation | Non-identifying metadata attached to an object; not usable for selection. |
| Label selector | The core grouping primitive; equality-based (`=`, `==`, `!=`) or set-based (`in`, `notin`, `exists`). |
| matchLabels / matchExpressions | Selector fields on newer resources; matchLabels is equivalent to matchExpressions with operator `In`. |
| ConfigMap | API object storing **non-confidential** key-value configuration data; max 1 MiB. |
| Secret | API object holding a small amount of sensitive data; **base64-encoded, not encrypted by default**. |
| Immutable ConfigMap/Secret | Since v1.19, a ConfigMap can be marked immutable; the flag cannot be reverted, only delete-and-recreate. |
| Deployment eras | Traditional (physical servers) → Virtualized (VMs) → Container (shared OS, lightweight, portable). |
| What Kubernetes provides | Service discovery/load balancing, storage orchestration, automated rollouts/rollbacks, automatic bin packing, self-healing, secret & config management, batch execution, horizontal scaling, IPv4/IPv6 dual-stack, extensibility. |
| What Kubernetes is not | Not a traditional all-inclusive PaaS; doesn't build source, doesn't provide middleware/databases, doesn't mandate logging or config languages, and is "not a mere orchestration system" — it's composable control loops, not a defined A→B→C workflow. |

### D1.2 — Administration

| Concept | One-line definition |
|---|---|
| Cluster planning axes | Local vs multi-node HA; hosted vs self-managed; on-prem vs IaaS; bare metal vs VMs; user vs contributor. |
| Managed vs self-hosted | Hosted offerings (e.g. GKE) run the control plane for you; self-hosted means you own it. |
| Resource quota | Per-namespace mechanism for dividing cluster resources among users/teams. |
| Controlling access to the API | The three sequential gates: authentication, authorization, admission control. |
| Authentication | Establishing *who* is making the request (certificates, tokens, and other configured methods). |
| Authorization | Deciding whether the authenticated identity may perform the action (RBAC is one authorizer). |
| Admission controllers | Components that intercept validated API requests before persistence and may mutate or reject them. |
| Auditing | Recording the sequence of activities affecting the cluster. |
| TLS bootstrapping | The mechanism by which a kubelet obtains its client certificate to join the cluster. |
| Control-plane ↔ node communication | The trust and traffic paths between the API server and node components. |
| Semantic versioning | Kubernetes releases are `x.y.z` — major.minor.patch. |
| Supported versions | Release branches are maintained for the most recent **three** minor releases; 1.19+ receives ~1 year of patch support. |
| Version skew — kubelet | Must not be *newer* than kube-apiserver; may be up to **three** minor versions older. |
| Version skew — kube-proxy | Must not be newer than kube-apiserver; up to three minor versions older; up to three older *or newer* than its kubelet. |
| Version skew — controller-manager / scheduler / CCM | Must not be newer than the API servers they talk to; expected to match, may be one minor older to allow live upgrade. |
| Version skew — kubectl | Supported within **one** minor version older *or newer* than kube-apiserver. |
| Version skew — HA apiservers | Newest and oldest kube-apiserver instances must be within one minor version. |

### D1.3 — Scheduling

| Concept | One-line definition |
|---|---|
| Scheduling | Assigning a newly-created, unbound Pod to a suitable node. |
| kube-scheduler | The default scheduler, running as part of the control plane; replaceable with a custom scheduler. |
| Feasible node | A node that meets a Pod's scheduling requirements. |
| Filtering | Step 1 — eliminate nodes where the Pod cannot run (e.g. PodFitsResources checks available capacity). |
| Scoring | Step 2 — rank the surviving feasible nodes by the active scoring rules. |
| Binding | The scheduler notifying the API server of its node choice for the Pod. |
| Tie-breaking | If multiple nodes score equally, kube-scheduler picks one **at random**. |
| Unschedulable | If filtering leaves an empty list, the Pod stays unscheduled until the scheduler can place it. |
| Scheduling factors | Individual and collective resource requirements; hardware/software/policy constraints; affinity and anti-affinity; data locality; inter-workload interference; deadlines. |
| Scheduling Policies | The older configuration model: Predicates (filtering) and Priorities (scoring). |
| Scheduling Profiles | The plugin model: plugins implement stages including QueueSort, Filter, Score, Bind, Reserve, Permit; multiple profiles can run. |
| Direct node assignment | The API permits specifying a node at Pod creation — unusual, special cases only. |
| Pod scheduling is once-only | A Pod is scheduled once in its lifetime and is never rescheduled to a different node. |

### D1.4 — Containerization

| Concept | One-line definition |
|---|---|
| Container | A repeatable, standardized runtime unit that decouples an application from host infrastructure. |
| Container image | A ready-to-run package containing code, runtime, application and system libraries, and default settings. |
| Immutability | Containers are intended to be stateless and immutable — change means build a new image and recreate, never edit a running container. |
| Container vs VM | Containers relax isolation to share the host OS, making them lightweight; a VM includes a full guest OS. |
| CRI | The Container Runtime Interface — the Kubernetes-facing contract any runtime must implement. |
| containerd / CRI-O | Two CRI-conformant container runtimes supported by Kubernetes. |
| RuntimeClass | Pod-level field selecting a specific container runtime when a cluster runs more than one. |
| OCI | Open Container Initiative — open governance body creating industry standards for container formats and runtimes; founded June 2015 by Docker and others. |
| OCI runtime-spec | Specifies how to run a filesystem bundle unpacked on disk. |
| OCI image-spec | Defines the OCI Image Format: image manifest, filesystem layer serialization, image configuration. |
| OCI distribution-spec | Standardizes the API for distributing container images; reached v1.0 in May 2020. |
| runC | Docker's donated container runtime, the cornerstone of the OCI effort. |
| OCI flow | Download OCI Image → unpack into OCI Runtime filesystem bundle → run bundle with an OCI Runtime. |

### D2.1 — Networking

| Concept | One-line definition |
|---|---|
| Kubernetes network model | Every Pod gets a unique cluster-wide IP; all Pods can reach all Pods without NAT or proxies. |
| Pod network namespace | Each Pod has a private network namespace shared by all its containers, which talk over localhost. |
| Pod network / cluster network | The layer handling Pod-to-Pod communication across nodes. |
| Node-agent reachability | Agents on a node (kubelet, system daemons) can reach all Pods on that node. |
| Service | An abstraction providing a stable IP/hostname for a logical set of Pod endpoints that churn over time. |
| ClusterIP | Default Service type; exposes the Service on a cluster-internal IP, reachable only inside the cluster. |
| NodePort | Exposes the Service on each node's IP at a static port; also allocates a ClusterIP. |
| LoadBalancer | Exposes the Service externally via an external load balancer you or your cloud provider supplies. |
| ExternalName | Maps the Service to a DNS CNAME for an external hostname; **no proxying of any kind**. |
| Headless Service | `.spec.clusterIP: None`; DNS returns Pod addresses directly instead of a single virtual IP. |
| Service without selector | A Service backed by manually-managed EndpointSlices, abstracting non-Pod or off-cluster backends. |
| EndpointSlice | The object tracking which Pods currently back a Service; managed automatically by Kubernetes. |
| Service proxy | The implementation watching Services and EndpointSlices and programming the data plane to route traffic. |
| Ingress | An API exposing **HTTP and HTTPS** routes from outside the cluster to Services inside it. |
| Ingress controller | The component that actually fulfills an Ingress; creating an Ingress with no controller has **no effect**. |
| Ingress capabilities | Externally-reachable URLs, load balancing, TLS/SSL termination, name-based virtual hosting, simple fanout by URI. |
| Ingress is frozen | Generally available and covered by GA stability guarantees, but no longer developed; the project recommends **Gateway** instead. |
| Gateway API | The successor to Ingress; dynamic infrastructure provisioning and advanced traffic routing. |
| Edge router | The router enforcing the cluster's firewall policy — a cloud-managed gateway or physical hardware. |
| NetworkPolicy | Built-in API controlling L3/L4 traffic between Pods and between Pods and the outside world. |
| Service DNS | `<service-name>.<namespace>.svc.cluster.local`; a bare `<service-name>` resolves within the local namespace only. |

### D2.2 — Security

| Concept | One-line definition |
|---|---|
| RBAC | Role-based access control; authorization driven by the `rbac.authorization.k8s.io` API group, enabled via `--authorization-mode`. |
| Role | A namespaced set of permission rules; you must specify its namespace. |
| ClusterRole | A **non-namespaced** set of permission rules, usable cluster-wide or bound into individual namespaces. |
| RoleBinding | Grants a Role's (or a ClusterRole's) permissions to subjects **within one namespace**. |
| ClusterRoleBinding | Grants a ClusterRole's permissions **cluster-wide**. |
| Permissions are purely additive | RBAC has **no deny rules**; you cannot subtract a granted permission. |
| Binding immutability | After you create a binding you cannot change which Role/ClusterRole it refers to. |
| cluster-admin | Default ClusterRole granting super-user access to any action on any resource. |
| admin | Default ClusterRole for namespace admin via RoleBinding; can create roles and bindings in that namespace. |
| edit | Default ClusterRole for read/write on most namespace objects; **cannot** view or modify roles/bindings. |
| view | Default ClusterRole for read-only on most namespace objects; **cannot** see Secrets, roles, or bindings. |
| Secret storage default | Secrets are stored **unencrypted** in etcd by default; encryption at rest must be enabled explicitly. |
| Secret exposure paths | Anyone with API access, etcd access, or the ability to create a Pod (or Deployment) in a namespace can read that namespace's Secrets. |
| Secret hardening steps | Enable encryption at rest; least-privilege RBAC on Secrets; restrict Secret access to specific containers; consider external secret stores. |
| Secret types | Opaque (default), service-account-token, dockercfg, dockerconfigjson, basic-auth, ssh-auth, tls, bootstrap token. |
| ServiceAccount token modernization | Since v1.22 the recommended approach is short-lived, automatically rotating tokens via the TokenRequest API, not long-lived token Secrets. |
| NetworkPolicy as security control | Pod-scoped L3/L4 segmentation — the built-in mechanism for restricting east-west traffic. |
| Zero trust via service mesh | Workload identity plus mutual TLS plus policy, provided at the infrastructure layer without code changes. |
| Securing the kubelet | Control-plane↔node communication, TLS bootstrapping, kubelet authentication and authorization. |

### D2.3 — Troubleshooting

| Concept | One-line definition |
|---|---|
| Two audiences | *Debugging your application* (you deployed code that isn't working) vs *debugging your cluster* (the platform is unhappy). |
| Troubleshooting Applications | Debugging Pods, Services, StatefulSets; determining Pod failure reasons; debugging init containers and running Pods. |
| Troubleshooting Clusters | Troubleshooting kubectl, the resource metrics pipeline, monitoring tools, node health, crictl, auditing, local service debugging. |
| Resource metrics pipeline | metrics-server collecting and aggregating resource usage from kubelets, feeding `kubectl top` and autoscaling. |
| Logging architecture | How Kubernetes handles cluster and application logs; native patterns and integration points for log systems. |
| kubectl debug | The built-in diagnostic command for debugging workloads. |
| crictl | The CRI-level tool for debugging nodes below the Kubernetes API. |
| Known issues | Release-specific known-issue lists are part of the troubleshooting path. |
| Pod phase as first signal | Pending vs Running vs Failed narrows the failure to scheduling, image pull, startup, or exit. |
| Container Waiting `Reason` | The field summarizing *why* a container has not yet started (image pull, Secret application, etc.). |
| Probe failure signatures | Liveness failure → restart loop; readiness failure → Pod silently removed from Service endpoints. |
| Node lease heartbeats | kube-node-lease Lease objects let the kubelet report liveness so the control plane can detect node failure. |
| Node death handling | Pods on a dead node are marked for deletion after a timeout; higher-level controllers create replacements. |

### D2.4 — Storage

| Concept | One-line definition |
|---|---|
| PersistentVolume (PV) | A piece of cluster storage, admin-provisioned or dynamically provisioned; a cluster resource like a node. |
| PV lifecycle independence | A PV's lifecycle is independent of any individual Pod that uses it. |
| PersistentVolumeClaim (PVC) | A user's *request* for storage — a specific size and access mode. |
| Pods:PVCs :: node resources:Pods | Pods consume node resources; PVCs consume PV resources. |
| StorageClass | The resource letting admins offer PV varieties (performance tiers etc.) without exposing implementation. |
| Static provisioning | An admin pre-creates PVs carrying real storage details. |
| Dynamic provisioning | The cluster creates a PV on demand for a PVC that requests a StorageClass configured for it. |
| Disabling dynamic provisioning | A claim requesting storage class `""` opts itself out of dynamic provisioning. |
| Binding | A control loop matches a new PVC to a PV and binds them; binds are **exclusive and one-to-one**. |
| Unbound claims | A PVC with no matching volume stays unbound indefinitely, binding later if a match appears. |
| Using | A Pod references a PVC in its `volumes` block; the cluster mounts the bound volume. |
| Reclaiming | What happens to the PV after its claim is deleted, governed by the reclaim policy. |
| Retain | PV persists in "released" state with data intact; requires manual admin reclamation. |
| Delete | Removes both the PV object and the backing storage asset; the **default for dynamically-provisioned volumes** (inherited from the StorageClass). |
| Recycle | Deprecated reclaim policy. |
| ReadWriteOnce (RWO) | Mountable read-write by a **single node** — multiple Pods on that same node may still share it. |
| ReadOnlyMany (ROX) | Mountable read-only by many nodes. |
| ReadWriteMany (RWX) | Mountable read-write by many nodes. |
| ReadWriteOncePod (RWOP) | Mountable read-write by exactly **one Pod** cluster-wide. |
| StatefulSet + PV | The pairing that gives stateful workloads durable per-Pod storage. |

### D3.1 — Application Delivery

| Concept | One-line definition |
|---|---|
| GitOps | A set of principles for operating and managing software systems with a declarative desired state under version control. |
| OpenGitOps | The CNCF sandbox project publishing the standards, practices, and education for GitOps adoption. |
| Principle 1 — Declarative | The desired state must be expressed declaratively. |
| Principle 2 — Versioned and Immutable | Desired state is stored so as to enforce immutability and versioning, retaining complete history. |
| Principle 3 — Pulled Automatically | Software agents automatically pull the desired-state declarations from the source. |
| Principle 4 — Continuously Reconciled | Software agents continuously observe actual state and attempt to apply desired state. |
| Argo CD | A declarative GitOps continuous-delivery tool for Kubernetes, implemented as a Kubernetes controller. |
| Source of truth | Argo CD treats the Git repository as the source of truth for desired application state. |
| OutOfSync | Argo CD's status for a deployed application whose live state deviates from the Git target state. |
| Sync | Bringing live state back to target state — automatically or manually. |
| Argo CD manifest sources | Kustomize applications, Helm charts, Jsonnet, plain YAML/JSON directories, or a custom config-management plugin. |
| Tracking targets | Argo CD can track a branch, a tag, or a pinned Git commit. |
| Argo CD features | Multi-cluster deployment, SSO, multi-tenancy/RBAC, rollback to any committed config, health-status analysis, drift detection and visualization, web UI, CLI, webhooks, PreSync/Sync/PostSync hooks for blue-green and canary, audit trails, Prometheus metrics, Helm parameter overrides. |
| Helm | The CNCF-graduated Kubernetes package manager. |
| Chart | Helm's packaging format — a collection of files describing a related set of Kubernetes resources. |
| Chart.yaml | The YAML file carrying the chart's own metadata. |
| values.yaml | The chart's default configuration values. |
| templates/ | The directory of templates that, combined with values, generate valid Kubernetes manifests. |
| charts/ | The directory holding charts this chart depends on. |
| crds/ | The chart directory for Custom Resource Definitions. |
| Chart repository | An HTTP server housing packaged charts, managed with `helm repo` commands. |
| Release | An installed instance of a chart in a cluster; one chart can produce many independently-upgradable releases. |
| Knative | A Kubernetes-based platform of middleware components for building and running serverless workloads. |
| Knative Serving | HTTP-triggered autoscaling container runtime managing stateless HTTP services, including **scale to zero**. |
| Knative Eventing | CloudEvents-over-HTTP asynchronous routing layer decoupling event producers from consumers. |
| Knative Functions | A simplified build-and-deploy experience for stateless functions built on Serving and Eventing. |
| Knative implementation | Serving and Eventing are implemented as Kubernetes CRDs on top of the Pod abstraction. |
| Twelve-Factor App | A methodology for SaaS apps emphasizing declarative setup, clean OS contract, portability, dev/prod parity, and scale-out. |
| The twelve factors | I Codebase · II Dependencies · III Config · IV Backing services · V Build, release, run · VI Processes · VII Port binding · VIII Concurrency · IX Disposability · X Dev/prod parity · XI Logs · XII Admin processes. |
| Config in the environment | Factor III — the principle Kubernetes ConfigMaps and Secrets implement. |
| Stateless processes | Factor VI — the principle that makes Deployments and horizontal scaling work. |
| Logs as event streams | Factor XI — the principle behind cluster-level log aggregation. |
| Disposability | Factor IX — fast startup and graceful shutdown, matching Pod ephemerality. |
| ConfigMap for portability | Decoupling environment-specific configuration from the container image so applications are portable. |
| ConfigMap consumption paths | Container command/args; environment variables; read-only volume file; the Kubernetes API from inside the Pod. |
| ConfigMap live updates | Only the API-reading path lets an application subscribe to ConfigMap changes; the other three are applied by the kubelet at container launch. |

### D3.2 — Debugging

Shares its concept set with **D2.3 Troubleshooting** above, scoped to the application side: Troubleshooting Applications, determining Pod failure reasons, init-container and running-Pod debugging, `kubectl debug`, and developing/debugging services locally.

### D4.1 — Observability

| Concept | One-line definition |
|---|---|
| Observability | Understanding a system from the outside — asking questions about it without knowing its internals, including "unknown unknowns". |
| Instrumentation | Application code emitting signals; properly instrumented means no new instrumentation is needed to troubleshoot. |
| Telemetry | Data emitted from a system about its behavior. |
| Signals (OpenTelemetry) | Traces, Metrics, Logs, and Baggage. |
| Trace | A record of the path a request takes through a multi-service architecture; made of one or more spans. |
| Span | A unit of work or operation, carrying name, timing, structured log messages, and attributes. |
| Root span | The first span in a trace, representing the request start-to-finish. |
| Log | A timestamped message from a service; not necessarily tied to a request, and far more useful correlated with a span. |
| Metric | An aggregation over a period of time of numeric data about infrastructure or an application. |
| Baggage | Contextual information passed between signals. |
| Reliability | The question "is the service doing what users expect it to be doing?" |
| SLI | Service Level Indicator — a measurement of service behavior; a good one measures from the user's perspective. |
| SLO | Service Level Objective — how reliability is communicated, attaching SLIs to business value. |
| Prometheus | An open-source systems monitoring and alerting toolkit; the **second** project hosted by CNCF, after Kubernetes (joined 2016). |
| Time series | Prometheus stores metrics with the timestamp of recording plus optional key-value labels. |
| Multi-dimensional data model | Time series identified by metric name plus key/value label pairs. |
| PromQL | Prometheus's query language for exploiting that dimensionality. |
| Pull model | Prometheus scrapes metrics over HTTP; each server is standalone with no distributed-storage dependency. |
| Pushgateway | The intermediary supporting short-lived jobs that cannot be scraped. |
| Exporters | Special-purpose adapters exposing metrics for third-party services (HAProxy, StatsD, Graphite …). |
| Alertmanager | The Prometheus component handling alerts. |
| Client libraries | Libraries for instrumenting application code. |
| Service discovery | How Prometheus finds scrape targets, versus static configuration. |
| Prometheus fit | Excellent for numeric time series and dynamic service-oriented architectures; **not** appropriate where 100% accuracy is required (e.g. per-request billing). |
| Reliability over completeness | Prometheus's explicit design tradeoff — a standalone server you can trust when other infrastructure is broken. |

### D4.2 — Cloud Native Ecosystem and Principles

| Concept | One-line definition |
|---|---|
| Cloud native (CNCF definition v1.1) | Practices empowering organizations to develop, build, and deploy workloads across public/private/hybrid cloud to meet needs at scale, programmatically and repeatably. |
| Cloud-native characteristics | Loosely coupled systems that interoperate securely, resiliently, manageably, sustainably, and observably. |
| Cloud-native technologies (non-exhaustive) | Containers, service meshes, multi-tenancy, microservices, immutable infrastructure, serverless, declarative APIs. |
| The payoff | Robust automation plus loose coupling lets engineers make high-impact changes frequently and predictably with minimal toil. |
| CNCF mission | Drive adoption by fostering an ecosystem of open-source, vendor-neutral projects; democratize state-of-the-art patterns. |
| CNCF and the Linux Foundation | CNCF is part of The Linux Foundation, a nonprofit. |
| Cloud-native stack (CNCF framing) | Deploy applications as microservices, package each part into its own container, dynamically orchestrate containers to optimize resource utilization. |
| Microservices | Loosely coupled, distributed, elastic services, each independently deployable. |
| Immutable infrastructure | Infrastructure replaced rather than modified in place. |
| Declarative API | An API you target with a description of desired state rather than a sequence of commands. |
| Service mesh | An infrastructure layer giving applications zero-trust security, observability, and advanced traffic management **without code changes**. |
| Data plane | The proxies that mediate and control all network communication between services. |
| Control plane | The layer that manages and configures those proxies. |
| Envoy | The industry-standard proxy used by Istio in both data-plane modes. |
| Sidecar mode | An Envoy proxy deployed alongside each Pod. |
| Ambient mode | Per-node Layer 4 proxies plus optional per-namespace Envoy proxies. |
| Mesh capabilities | Workload identity and mutual TLS; telemetry integrating with Prometheus/Grafana; traffic routing for A/B testing and canary deployments. |
| Serverless | Running workloads without managing servers; Knative is the CNCF-graduated Kubernetes implementation. |
| Scale to zero | Reducing a workload's replica count to zero when idle — a defining serverless behavior. |
| Autoscaling — horizontal | Changing the **number of replicas**. |
| Autoscaling — vertical | Adjusting the **resources available** to replicas. |
| HorizontalPodAutoscaler (HPA) | API resource plus controller periodically adjusting replica count to match observed utilization such as CPU or memory. |
| VerticalPodAutoscaler (VPA) | An **add-on, not included by default**, that automatically scales workload resources. |
| In-place pod vertical scaling | Stable as of Kubernetes v1.35; VPA does not yet support it directly. |
| Cluster Proportional Autoscaler | Scales replica counts based on the number of schedulable nodes and cores (e.g. for cluster DNS). |
| KEDA | CNCF-graduated Kubernetes Event Driven Autoscaler, scaling on events such as queue depth; its Cron scaler handles schedule-based scaling. |
| Node autoscaling | Adding or removing **nodes** to scale cluster infrastructure (Cluster Autoscaler, Karpenter). |
| Manual scaling | Horizontal via `kubectl` replica change; vertical via patching the resource definition. |
| Project maturity — Sandbox | Experimental projects not yet widely tested in production; bleeding edge. |
| Project maturity — Incubating | Used successfully in production by a small number of users, with a healthy contributor pool. |
| Project maturity — Graduated | Stable, widely adopted, production-ready, attracting thousands of contributors. |
| Maturity progression | Projects enter at Sandbox and may progress through Incubating to Graduated per the TOC's project-lifecycle criteria. |
| Graduation criteria location | Defined in the CNCF TOC's project-lifecycle documentation (github.com/cncf/toc), **not** on the projects page. |
| Graduated projects (2026-08-23 snapshot) | Argo, Buildpacks, cert-manager, Cilium, CloudEvents, containerd, CoreDNS, CRI-O, Crossplane, CubeFS, Dapr, Dragonfly, Envoy, etcd, Falco, Fluentd, Flux, Harbor, Helm, in-toto, Istio, Jaeger, KEDA, Knative, KubeEdge, Kubeflow, Kubernetes, Kyverno, Linkerd, OPA, OpenTelemetry, Prometheus, Rook, SPIFFE, SPIRE, TUF, TiKV, Vitess. |
| Early CNCF stack components | Kubernetes, Fluentd, Linkerd, Prometheus, OpenTracing, gRPC (as named in the CNCF curriculum PDF). |

### D4.3 — Cloud Native Community and Collaboration

| Concept | One-line definition |
|---|---|
| CNCF TOC | The Technical Oversight Committee — the technical governing body of the CNCF. |
| TOC responsibilities | Define and maintain technical vision and principles; approve new projects within the Governing Board's scope; create a conceptual architecture; align, remove, or archive projects; accept end-user TAB feedback and map it to projects; align interfaces and establish common practices. |
| Governing Board | The body that sets the scope within which the TOC approves projects. |
| End user Technical Advisory Board | The body whose feedback the TOC accepts and maps to projects. |
| TAGs | Technical Advisory Groups — TOC-aligned groups organized by technical area. |
| Current TAGs (post-2025 restructure) | Developer Experience; Infrastructure; Operational Resilience; Security and Compliance; Workloads Foundation. |
| Former TAGs (pre-2025) | App Delivery, Contributor Strategy, Environmental Sustainability, Network, Observability, Runtime, Security, Storage. |
| Kubernetes community principles | Open; Welcoming and respectful (Code of Conduct); Transparent and accessible (work done in public); Merit (contributions judged on technical merit and alignment). |
| SIG | Special Interest Group — the primary organizational unit of the Kubernetes project, focused on a specific topic. |
| SIG orientations | Vertical (Network, Storage, Node), horizontal (Scalability, Architecture), or project-support (Testing, Release, Docs). |
| SIG chairs | At least one, ideally two per SIG; organizers and facilitators responsible for SIG operation and cross-SIG coordination. |
| Subproject | The unit of work division inside a SIG, with designated owners serving as technical leaders. |
| Working Group | A group facilitating discussion on topics that **cross SIG lines**; short-lived or spanning multiple SIGs. |
| Committee | A **closed-membership** group formed by the steering committee for topics requiring discretion (Security, Code of Conduct); has a charter and chairs and reports to steering. |
| Steering Committee | Holds overall Kubernetes project governance. |
| Contributor roles | Member, reviewer, approver — defined in the separate community-membership document. |
| Multi-company membership | Each SIG comprises members from multiple companies and organizations. |

---

## Dependency graph

Read this as: *a concept on the right must be taught before the concept on the left.* Use it to sequence chapters; edges crossing domain boundaries are the ones that constrain ordering hardest.

### Tier 0 — Root concepts (no prerequisites)

`Traditional → Virtualized → Container deployment eras` · `Container` · `Container image` · `Immutability` · `Cluster` · `Control plane / worker node split` · `Declarative vs imperative` · `Cloud-native definition`

### Tier 1 — Depends only on Tier 0

| Concept | Requires |
|---|---|
| OCI specs (runtime / image / distribution) | Container image, Container |
| runC, containerd, CRI-O | Container, OCI runtime-spec |
| CRI | Container runtime, kubelet (soft) |
| Kubernetes object · spec/status | Declarative, Cluster |
| Manifest · apiVersion/kind/metadata/spec | Kubernetes object |
| Control-plane components (apiserver, etcd, scheduler, controller-manager, CCM) | Control plane |
| Node components (kubelet, kube-proxy, runtime) | Worker node, Container runtime |
| Pod | Container, Node |
| Twelve-factor app | Cloud-native definition |

### Tier 2 — Depends on Tier 1

| Concept | Requires |
|---|---|
| Controller / control loop / reconciliation | spec/status, kube-controller-manager |
| Pod phase · container state · restartPolicy | Pod, kubelet |
| Probes (liveness / readiness / startup) | Pod, container state, kubelet |
| Label · annotation · label selector | Kubernetes object, metadata |
| Namespace | Kubernetes object, cluster-scoped vs namespaced |
| ConfigMap · Secret | Kubernetes object, Pod, 12-factor III |
| Scheduling: filter → score → bind | kube-scheduler, Pod, Node |
| Kubernetes network model (Pod IP, no NAT) | Pod, Node |

### Tier 3 — Depends on Tier 2

| Concept | Requires |
|---|---|
| ReplicaSet · Deployment | Controller, Pod, label selector |
| StatefulSet | Deployment, Pod, PersistentVolume |
| DaemonSet | Controller, Node, Pod |
| Job · CronJob | Controller, Pod, restartPolicy, Pod phase Succeeded/Failed |
| Service (all four types) | Pod IP, label selector, network model |
| EndpointSlice | Service, label selector, readiness probe |
| Service DNS FQDN | Service, Namespace |
| RBAC (Role / ClusterRole / bindings) | Namespace, namespaced-vs-cluster-scoped, API access model |
| PersistentVolume · PersistentVolumeClaim | Kubernetes object, Pod volumes, cluster-scoped resources |
| Resource quota | Namespace |
| Version skew policy | Control-plane and node components, semantic versioning |

### Tier 4 — Depends on Tier 3

| Concept | Requires |
|---|---|
| Ingress · Ingress controller | Service (ClusterIP), HTTP routing, controller pattern |
| Gateway API | Ingress (as the thing it supersedes) |
| NetworkPolicy | Pod, label selector, Namespace, network model, CNI plugin support |
| StorageClass · dynamic provisioning · reclaim policy | PV, PVC, binding |
| Access modes (RWO / ROX / RWX / RWOP) | PV, PVC, Node |
| Secret hardening (encryption at rest, least-privilege RBAC) | Secret, RBAC, etcd |
| HPA | Deployment/ReplicaSet, metrics pipeline |
| VPA · in-place resize | HPA (contrast), resource requests |
| Cluster autoscaling (Cluster Autoscaler, Karpenter) | Node, scheduling, unschedulable Pods |
| Troubleshooting workflow | Pod phase, container state, probes, Service/EndpointSlice, events |

### Tier 5 — Depends on Tier 4

| Concept | Requires |
|---|---|
| Helm chart · values · templates · release | Manifest, Deployment/Service, templating idea |
| GitOps four principles | Declarative, controller/reconciliation, immutability, version control |
| Argo CD · OutOfSync · sync | GitOps principles, controller pattern, Helm/Kustomize/plain YAML |
| Service mesh (data plane / control plane, mTLS, sidecar vs ambient) | Pod, Service, Envoy proxy concept, control-plane/data-plane framing |
| Knative Serving / Eventing / scale-to-zero | CRD concept, Deployment, HPA, Pod |
| KEDA event-driven autoscaling | HPA, external event sources |
| Observability signals (traces, metrics, logs, baggage) | Instrumentation, distributed system, microservices |
| Prometheus (pull model, PromQL, exporters, Alertmanager) | Metrics, time series, Service discovery |
| SLI / SLO / reliability | Metrics, user perspective |

### Tier 6 — Ecosystem and institutional (low technical prerequisite, high name-density)

`CNCF maturity levels` · `Graduated project roster` · `TOC` · `TAGs` · `Governing Board` · `End user TAB` · `Kubernetes SIGs / WGs / Committees / Steering` · `Community principles` · `Contributor roles`

These have almost no technical prerequisites and can be placed anywhere in the book. **Recommendation:** split them — put the cloud-native *definition* and the *why* of CNCF early (it frames everything), and defer the maturity levels, project roster, and governance bodies to a late chapter, where the reader can attach project names to concepts they now understand. Teaching the graduated-project list before the reader knows what a service mesh or a CD controller *is* produces rote memorization with nothing to hang on.

### Sequencing implications

1. **Containerization (D1.4) must precede everything.** It is only ~1/4 of the largest domain but it is the deepest root in the graph. Do not save it for late just because OCI feels like ecosystem trivia.
2. **Core Concepts (D1.1) is the trunk.** Objects/spec/status → controllers → Pod → workload resources → labels/namespaces. Every other domain hangs off this chain. Budget accordingly.
3. **Scheduling (D1.3) needs Pod and Node but nothing from D2.** It can go immediately after Core Concepts, keeping D1 contiguous.
4. **Storage (D2.4) must precede StatefulSet's full treatment.** Either introduce StatefulSet lightly in the workloads chapter and return to it after PV/PVC, or place storage before the deep workloads pass. The former is better for the reader — StatefulSet belongs with its siblings.
5. **Service must precede Ingress must precede Gateway API.** A strict chain, and the frozen-Ingress fact only lands once the reader knows what Ingress does.
6. **NetworkPolicy sits in both D2.1 and D2.2.** Teach it once, in Networking, and cross-bear from the Security chapter. Duplicating it costs words and creates two slightly-divergent explanations.
7. **Troubleshooting (D2.3) and Debugging (D3.2) should be one teaching arc split across two chapters** by scope: platform-side symptoms in the D2 chapter, application-side workflow in the D3 chapter, with explicit cross-bearings both ways. The exam splits them across domains; the reader's mental model should not be split.
8. **Observability (D4.1) needs microservices and distributed systems framing first.** Traces are meaningless without a multi-service mental model. Place it after the service mesh / microservices material, not before.
9. **GitOps needs the controller/reconciliation pattern.** The four OpenGitOps principles are a restatement of the Kubernetes control loop applied to Git. Teaching them after Tier 2 controllers turns D3 from memorization into a Zenith moment — this is the strongest synthesis opportunity in the book, and the D3 chapter should be built around it.

---

## Known traps

Each entry is tagged **[source]** where the trap is explicitly flagged or directly implied by a cached authoritative source, or **[inferred]** where it comes from the structure of the material and known candidate-confusion patterns. Inferred traps must be verified against practice material before a chapter asserts "candidates commonly miss this" — Ethical Guardrail #8 requires distinguishing *frequently tested* from *might be tested*, and the book should describe inferred traps as "easy to confuse" rather than claiming exam frequency data we do not have.

### D1 — Kubernetes Fundamentals

| # | Trap | Correct understanding | Tag |
|---|---|---|---|
| 1 | "kube-proxy is required on every node." | kube-proxy is explicitly **optional**. A network plugin that implements Service packet forwarding itself makes it unnecessary. | [source] |
| 2 | "Every cluster has a cloud-controller-manager." | CCM is optional and absent when running on-prem or on a local learning cluster. | [source] |
| 3 | "The controller-manager runs one process per controller." | Logically separate, but all compiled into a **single binary running in a single process**. | [source] |
| 4 | "Kubernetes is an orchestrator that runs A then B then C." | Kubernetes explicitly rejects this framing — it is a set of independent, composable control processes continuously driving toward desired state; it "eliminates the need for orchestration." | [source] |
| 5 | "Kubernetes is a PaaS." | It is **not** a traditional all-inclusive PaaS; it doesn't build source, doesn't ship middleware/databases/caches, doesn't mandate logging or a config language. | [source] |
| 6 | Confusing **Pod phase** with **container state**. | Phase (Pending/Running/Succeeded/Failed/Unknown) is Pod-level; state (Waiting/Running/Terminated) is per-container. A Pod can be `Running` with a container in `Waiting`. | [source] |
| 7 | "`Running` means the app is working." | Running means the Pod is bound and containers created, with at least one running **or starting or restarting**. A crash-looping Pod can report Running. | [source] |
| 8 | "restartPolicy can be set per container." | It is a **Pod-level** field and applies to all containers in the Pod. | [source] |
| 9 | Assuming a failed Pod is rescheduled to a healthy node. | A Pod is scheduled **once in its lifetime** and is never rescheduled. It is *replaced* by a new, near-identical Pod with a different UID, by a higher-level controller. | [source] |
| 10 | "Liveness and readiness do the same thing." | Liveness failure → kubelet kills the container and applies restart policy. Readiness failure → the Pod's IP is removed from Service endpoints; **the container keeps running**. | [source] |
| 11 | Forgetting that a startup probe **disables** the other probes. | While a startupProbe is configured and not yet succeeding, all other probes are disabled. | [source] |
| 12 | "Restart backoff grows forever." | It is capped at five minutes, and resets after a container runs cleanly for 10 minutes. | [source] |
| 13 | Using a Namespace to separate two versions of the same software. | The docs explicitly say not to — use **labels** to distinguish resources within one namespace. Namespaces are for many users/teams/projects. | [source] |
| 14 | "Everything lives in a namespace." | Nodes, PersistentVolumes, StorageClasses — and namespace objects themselves — are not namespaced. | [source] |
| 15 | Confusing **labels** with **annotations**. | Labels are identifying and selectable; annotations are non-identifying metadata and cannot be selected on. | [source] |
| 16 | "ConfigMaps are for config, Secrets are for secure config." | A ConfigMap provides **no secrecy or encryption**; a Secret provides base64 encoding and *still* no encryption at rest by default. The difference is intent and handling, not cryptography. | [source] |
| 17 | Assuming a ConfigMap change propagates to a running container. | Only the fourth consumption path (reading the API from inside the Pod) supports subscribing to updates. For env vars, args, and mounted files the kubelet applies data **at container launch**. | [source] |
| 18 | "Immutable ConfigMaps can be un-marked." | Once marked immutable, the flag cannot be reverted and the data cannot be mutated — delete and recreate only. | [source] |
| 19 | Missing the ConfigMap size ceiling. | 1 MiB. Larger settings need a volume, database, or file service. | [source] |
| 20 | Assuming a ConfigMap can be referenced across namespaces. | The Pod and the ConfigMap **must be in the same namespace**. | [source] |
| 21 | "Deployment vs StatefulSet is about whether the app writes to disk." | The distinguishing property is whether Pods are **interchangeable**. StatefulSet is for related Pods that track state and typically pair each Pod with a PV. | [source] |
| 22 | Reaching for a DaemonSet to "run several copies." | DaemonSet means **one Pod per matching node**, added automatically as nodes join — a node-local facility, not a replica count. | [source] |
| 23 | Job vs CronJob confusion. | Job = runs to completion **once**. CronJob = runs the same Job repeatedly on a schedule. | [source] |
| 24 | "The scheduler places the Pod on the node." | The scheduler **filters, scores, and then notifies the API server (binding)**; the kubelet on the chosen node actually starts the containers. | [source] |
| 25 | "The scheduler picks the single best node deterministically." | Among equally-scored nodes it selects one **at random**. | [source] |
| 26 | Assuming an unschedulable Pod errors out. | It remains `Pending` indefinitely until the scheduler can place it. | [source] |
| 27 | "kubelet must match the API server version." | kubelet may be up to **three** minor versions older; it must simply never be **newer**. | [source] |
| 28 | Applying the kubelet skew rule to kubectl. | kubectl is supported within **one** minor version in **either** direction — the only component permitted to be newer. | [source] |
| 29 | "Kubernetes supports the last two minor releases." | Release branches are maintained for the most recent **three** minor releases. | [source] |
| 30 | "A container image includes the OS kernel." | It includes code, runtime, application and system libraries, and default settings. Containers **share the host OS**; that's the VM contrast. | [source] |
| 31 | "You patch a running container." | Containers are intended to be stateless and immutable — build a new image and recreate. | [source] |
| 32 | "OCI is a runtime." | OCI is a **governance structure publishing three specifications** (runtime-spec, image-spec, distribution-spec). runC is a runtime donated *to* OCI. | [source] |
| 33 | Conflating OCI (image/runtime format standards) with CRI (the Kubernetes↔runtime interface). | Different layers: CRI is how Kubernetes talks to a runtime; OCI is how images are formatted, distributed, and bundles executed. | [inferred] |
| 34 | "Docker is the container runtime Kubernetes uses." | Kubernetes supports containerd, CRI-O, and any CRI implementation. RuntimeClass selects among them when more than one is present. | [inferred] |

### D2 — Container Orchestration

| # | Trap | Correct understanding | Tag |
|---|---|---|---|
| 35 | "Pods need NAT or a proxy to reach Pods on other nodes." | The network model requires direct Pod-to-Pod communication **without NAT**, on the same node or across nodes. | [source] |
| 36 | "Each container in a Pod gets its own IP." | The **Pod** gets one IP; all containers in it share the network namespace and talk over `localhost`. | [source] |
| 37 | "NodePort replaces ClusterIP." | Requesting NodePort **also** allocates a cluster IP, exactly as if you'd asked for ClusterIP. | [source] |
| 38 | "LoadBalancer means Kubernetes provides a load balancer." | Kubernetes does **not** offer a load-balancing component; you supply one or integrate with a cloud provider. | [source] |
| 39 | "ExternalName proxies traffic." | It configures a DNS **CNAME** and sets up **no proxying of any kind**. | [source] |
| 40 | Thinking a headless Service is a broken Service. | `clusterIP: None` is deliberate — DNS returns Pod addresses directly instead of one virtual IP, for when you don't want load balancing. | [source] |
| 41 | "A Service without a selector is invalid." | It's a supported pattern for abstracting external databases, other-namespace services, or migrating workloads, using manually-managed EndpointSlices. | [source] |
| 42 | "Creating an Ingress object exposes the app." | Without an **Ingress controller**, creating an Ingress resource has **no effect**. | [source] |
| 43 | "Ingress can expose any protocol." | Ingress handles **HTTP and HTTPS only**. Other protocols need NodePort or LoadBalancer. | [source] |
| 44 | "Ingress is deprecated / being removed." | It is **frozen**, not deprecated: GA, covered by stability guarantees, with no plans for removal — but no further development. The project *recommends* Gateway for new work. Both halves matter. | [source] |
| 45 | "All Ingress controllers behave identically." | Ideally all fit the reference spec; in reality they operate slightly differently. | [source] |
| 46 | Using a bare service name across namespaces. | A bare `<service-name>` resolves within the **local** namespace; cross-namespace requires the FQDN `<svc>.<ns>.svc.cluster.local`. | [source] |
| 47 | "Creating a NetworkPolicy secures the cluster." | Policies are implemented **by the network plugin**. With a CNI that doesn't support NetworkPolicy, the resource has **no effect** — a silent security failure. | [source] |
| 48 | "A Pod with no NetworkPolicy is closed by default." | Default is **non-isolated** in both directions: all ingress and all egress allowed. | [source] |
| 49 | "One NetworkPolicy can deny traffic another allows." | Policies are **purely additive and never conflict**. There is no deny rule. | [source] |
| 50 | Forgetting that both ends must permit the connection. | The source Pod's **egress** policy and the destination Pod's **ingress** policy must both allow it. | [source] |
| 51 | Assuming NetworkPolicy can block node-local traffic or self-traffic. | Traffic to and from the node where a Pod runs is **always allowed**, and a Pod cannot block access to itself. | [source] |
| 52 | Expecting NetworkPolicy to do TLS, name-based service targeting, logging, or explicit deny. | All explicitly out of scope for the current NetworkPolicy API. | [source] |
| 53 | "RBAC has deny rules." | Permissions are **purely additive**; there are no deny rules. Removing access means removing the grant. | [source] |
| 54 | "ClusterRole is only for cluster-scoped resources." | A ClusterRole can define permissions on namespaced resources and be bound into individual namespaces via a RoleBinding, granted across all namespaces via a ClusterRoleBinding, **or** cover cluster-scoped resources. | [source] |
| 55 | The four-way Role/ClusterRole × RoleBinding/ClusterRoleBinding matrix. | The **binding** type determines scope of the grant. RoleBinding + ClusterRole = permissions of that ClusterRole, limited to the binding's namespace. | [source] |
| 56 | "You can retarget a binding to a different role." | After creation you **cannot change** the Role/ClusterRole a binding refers to. | [source] |
| 57 | "The `view` role can read Secrets." | `view` explicitly **does not allow viewing Secrets**, nor roles or bindings. | [source] |
| 58 | "`edit` can manage RBAC in its namespace." | `edit` cannot view or modify roles or role bindings; `admin` can. | [source] |
| 59 | "cluster-admin always means the whole cluster." | In a **RoleBinding**, cluster-admin grants full control only within that binding's namespace. | [source] |
| 60 | "Secrets are encrypted." | Stored **unencrypted** in etcd by default. Encryption at rest is opt-in. | [source] |
| 61 | Missing the Pod-creation privilege-escalation path. | Anyone authorized to create a Pod in a namespace — including indirectly, via a Deployment — can read **any** Secret in that namespace. | [source] |
| 62 | "ServiceAccount token Secrets are the current best practice." | Since v1.22 the recommendation is short-lived, auto-rotating tokens via the **TokenRequest API**; the token Secret type is a legacy long-lived credential. | [source] |
| 63 | "A PVC binds to any PV that's big enough." | Binding is **exclusive and one-to-one**; an unmatched PVC stays unbound **indefinitely**, binding later only if a match appears. | [source] |
| 64 | Reversing PV and PVC. | PV = the **supply** (a piece of cluster storage). PVC = the **demand** (a user's request). Pods reference PVCs, never PVs. | [source] |
| 65 | "ReadWriteOnce means one Pod." | RWO means one **node** — multiple Pods on that same node can still access it. **ReadWriteOncePod** is the one-Pod-cluster-wide mode. | [source] |
| 66 | "Deleting a PVC always keeps the data." | Dynamically-provisioned volumes inherit the StorageClass reclaim policy, which **defaults to Delete** — removing both the PV object and the backing storage asset. | [source] |
| 67 | "Retain means the PV is immediately reusable." | The PV becomes `released`, not `available`; the prior claimant's data remains and an admin must manually reclaim it. | [source] |
| 68 | Expecting `Recycle` to be a live option. | Deprecated. | [source] |
| 69 | "Requesting storage class `""` uses the default class." | The empty string **disables dynamic provisioning** for that claim. | [source] |
| 70 | Jumping to `kubectl logs` for a Pod stuck in `Pending`. | Pending means it hasn't been scheduled or its image hasn't pulled — there are no container logs yet. Inspect events and scheduling instead. | [inferred] |
| 71 | Treating "debugging the application" and "debugging the cluster" as one activity. | The docs split them deliberately by audience; the diagnostic paths and tools differ. | [source] |
| 72 | Expecting `kubectl top` to work without metrics-server. | `kubectl top` and autoscaling depend on the **resource metrics pipeline** (metrics-server) collecting from kubelets. | [source] |

### D3 — Cloud Native Application Delivery

| # | Trap | Correct understanding | Tag |
|---|---|---|---|
| 73 | "GitOps means running CI from Git." | GitOps is four specific principles about *desired state*: declarative, versioned and immutable, **pulled** automatically, continuously reconciled. CI is not part of the definition. | [source] |
| 74 | Missing "**pulled**" — assuming a pipeline pushes to the cluster. | Principle 3 is explicit: agents **pull** desired-state declarations from the source. Push-based CD is not GitOps. | [source] |
| 75 | Treating reconciliation as one-shot at deploy time. | Principle 4 is **continuous** observation and application, indefinitely. | [source] |
| 76 | "OutOfSync means the sync failed." | OutOfSync means **live state deviates from the Git target state** — including because a human changed something in the cluster. It is a drift signal, not an error. | [source] |
| 77 | "Argo CD only deploys plain YAML." | It supports Kustomize, Helm, Jsonnet, plain YAML/JSON directories, and custom config-management plugins. | [source] |
| 78 | "Argo CD can only track a branch." | It can track branches, tags, or a **pinned Git commit**. | [source] |
| 79 | "Helm is a templating engine." | Helm is a packaging system: chart (the package) → values (configuration) → templates (which render manifests) → **release** (an installed instance). | [source] |
| 80 | Confusing **chart** with **release**. | One chart can be installed many times; each install is a separately-named release, independently upgradable and rollback-able. | [source] |
| 81 | Confusing `charts/` with a chart repository. | `charts/` is a directory of **dependency** charts inside a chart. A chart repository is an **HTTP server** housing packaged charts, managed with `helm repo`. | [source] |
| 82 | "Knative is a Kubernetes replacement." | Knative is Kubernetes-based, builds on the Pod abstraction, and is implemented as **CRDs**. | [source] |
| 83 | Confusing Knative Serving with Eventing. | Serving = HTTP-triggered autoscaling container runtime with scale-to-zero. Eventing = CloudEvents-over-HTTP **asynchronous** routing. | [source] |
| 84 | Treating "serverless" as "no containers." | Knative serverless workloads are containers on Pods; the serverless property is the lifecycle (scale to zero, request-driven), not the absence of containers. | [inferred] |
| 85 | Reciting twelve-factor as twelve unrelated rules. | The factors cluster: III/IV are configuration and dependency externalization; VI/VIII/IX are the stateless-disposable-scale-out triad Kubernetes assumes; XI is why log aggregation works; X is why containers exist. | [inferred] |
| 86 | "Factor III means use a config file." | Store config **in the environment** — this is precisely what ConfigMaps and Secrets injected as env vars implement. | [source] |
| 87 | Treating D3.2 Debugging as identical to D2.3 Troubleshooting. | The exam splits them; the split is roughly application-scope vs cluster-scope. A question tagged to one may still test the other's tooling. | [inferred] |

### D4 — Cloud Native Architecture

| # | Trap | Correct understanding | Tag |
|---|---|---|---|
| 88 | "Observability is monitoring with better dashboards." | Observability is the ability to ask **new** questions of a system from the outside — handling "unknown unknowns" — not just watching pre-defined indicators. | [source] |
| 89 | Naming three OpenTelemetry signals. | There are **four**: traces, metrics, logs, and **Baggage** (contextual information passed between signals). Baggage is the one candidates drop. | [source] |
| 90 | Confusing **span** with **trace**. | A span is one unit of work. A trace is the whole request path, made of one or more spans, beginning with a **root span**. | [source] |
| 91 | "Logs are the richest observability signal." | Logs typically **lack contextual information** and are "not extremely useful for tracking code execution on their own"; they become useful inside a span or correlated with a trace. | [source] |
| 92 | Confusing **SLI** with **SLO**. | SLI = the **measurement** of service behavior, ideally from the user's perspective. SLO = the **objective**, how reliability is communicated by attaching SLIs to business value. | [source] |
| 93 | "Prometheus pushes metrics." | Prometheus **pulls** (scrapes) over HTTP. Pushing is supported only via the **Pushgateway** intermediary, for short-lived jobs. | [source] |
| 94 | "Prometheus is a good billing system." | Explicitly not: if you need 100% accuracy, such as per-request billing, Prometheus is the wrong choice — it trades completeness for reliability. | [source] |
| 95 | "Prometheus needs distributed storage / clustered backends." | Each server is **standalone and autonomous**, deliberately, so it works when the rest of your infrastructure is broken. | [source] |
| 96 | "Prometheus was the first CNCF project." | Kubernetes was first; Prometheus was the **second**, joining in 2016. | [source] |
| 97 | Ordering the maturity levels wrong. | **Sandbox → Incubating → Graduated.** Sandbox = experimental/bleeding edge; Incubating = production use by a small number of users; Graduated = stable, widely adopted, production-ready. | [source] |
| 98 | Assuming graduation criteria are on the projects page. | They live in the **TOC's project-lifecycle documentation** (github.com/cncf/toc). | [source] |
| 99 | Guessing at a project's maturity level. | The roster changes. The graduated list captured 2026-08-23 is a snapshot; any book statement should be dated and framed as "as of". | [source] |
| 100 | "A service mesh requires changing application code." | The defining property is delivering zero-trust security, observability, and traffic management **without code changes**. | [source] |
| 101 | Confusing mesh **data plane** with **control plane**. | Data plane = the proxies mediating service-to-service traffic. Control plane = what manages and configures those proxies. Same vocabulary as Kubernetes' own split, different layer — a genuine collision point. | [source] |
| 102 | "Service mesh means sidecars." | Istio supports **sidecar mode** (per-Pod Envoy) and **ambient mode** (per-node L4 proxies plus optional per-namespace Envoy). Both use Envoy. | [source] |
| 103 | Confusing horizontal with vertical scaling. | Horizontal = change the **number of replicas**. Vertical = change the **resources per replica**. | [source] |
| 104 | "VPA ships with Kubernetes." | VPA is an **add-on, not included by default**. HPA is a built-in API resource and controller. | [source] |
| 105 | "In-place vertical resize means VPA now works in place." | In-place pod vertical scaling is stable as of v1.35, but **VPA does not yet support it directly**. | [source] |
| 106 | Confusing Pod autoscaling with node autoscaling. | HPA/VPA/KEDA scale **workloads**. Cluster Autoscaler and Karpenter scale the **node pool**. | [source] |
| 107 | "KEDA is a CPU-based autoscaler." | KEDA is **event-driven** — queue depth and similar external signals — and also provides schedule-based scaling via its Cron scaler. | [source] |
| 108 | Confusing **SIG** with **Working Group**. | SIGs are the primary, durable organizational unit focused on a topic. Working Groups are for topics that **cross SIG lines** and are short-lived. | [source] |
| 109 | Assuming all Kubernetes community groups are open. | **Committees** do not have open membership and do not always operate in the open; they're formed by the steering committee for topics requiring discretion (Security, Code of Conduct). | [source] |
| 110 | Confusing the CNCF **TOC** with the **Governing Board**. | The Governing Board sets the scope; the TOC approves projects **within** that scope and owns technical vision, architecture, and project lifecycle. | [source] |
| 111 | Using the pre-2025 TAG list. | TAGs were **restructured in 2025**. Current: Developer Experience, Infrastructure, Operational Resilience, Security and Compliance, Workloads Foundation. The old list (App Delivery, Contributor Strategy, Environmental Sustainability, Network, Observability, Runtime, Security, Storage) appears throughout older study material. | [source] |
| 112 | Confusing CNCF **TAGs** with Kubernetes **SIGs**. | TAGs are CNCF-wide, TOC-aligned. SIGs are internal to the Kubernetes project. Different organizations, similar-sounding function. | [inferred] |
| 113 | Studying to the five-domain blueprint. | Observability is no longer a standalone domain, Container Orchestration rose to 28%, and Application Delivery **doubled** to 16%. Much third-party prep still targets the old split. | [source] |
| 114 | Treating the CNCF cloud-native technology list as exhaustive. | The definition explicitly says "this list is non-exhaustive." | [source] |

---

## Gaps in sources

Topics that the four published competency lists plainly imply, or that a beginner-level Kubernetes exam near-certainly reaches, but which the cached source set **does not cover in sufficient depth to draft from**. Each needs additional research before the chapter pipeline runs on the affected chapter.

### Blocking — high confidence these are examinable, and cached coverage is absent or index-level only

| # | Gap | Affected competency | Suggested authority to fetch |
|---|---|---|---|
| G1 | **`kubectl` command surface.** The entire book depends on `kubectl get / describe / logs / exec / events / apply / top / port-forward / debug`, and no cached source documents them. | D1.2, D2.3, D3.2 | kubernetes.io/docs/reference/kubectl/ + the kubectl cheat sheet |
| G2 | **Pod failure signatures by name.** CrashLoopBackOff, ImagePullBackOff, ErrImagePull, OOMKilled, Evicted, CreateContainerConfigError. Not one appears in the cached set, and these are the single most likely troubleshooting question material. | D2.3, D3.2 | kubernetes.io/docs/tasks/debug/debug-application/debug-pods/ |
| G3 | **Resource requests and limits, and QoS classes** (Guaranteed / Burstable / BestEffort). Referenced obliquely (PodFitsResources, "tell Kubernetes how much CPU and memory") but never defined. Prerequisite for scheduling, autoscaling, and OOMKilled. | D1.3, D1.1, D2.3 | kubernetes.io/docs/concepts/configuration/manage-resources-containers/ |
| G4 | **Taints and tolerations; node affinity/anti-affinity; nodeSelector; topology spread constraints.** The scheduling source names "affinity and anti-affinity specifications" as a factor but never explains them. This is a substantial fraction of D1.3 with zero cached coverage. | D1.3 | kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ and .../taint-and-toleration/ |
| G5 | **Pod Security Standards and Pod Security Admission** (privileged / baseline / restricted) and `securityContext`. The single most conspicuous D2.2 absence — cached security coverage is RBAC and Secrets only. | D2.2 | kubernetes.io/docs/concepts/security/pod-security-standards/ and .../pod-security-admission/ |
| G6 | **The 4Cs of Cloud Native Security** (Cloud, Cluster, Container, Code). Standard KCNA-level security framing; entirely absent. | D2.2 | kubernetes.io/docs/concepts/security/overview/ |
| G7 | **ServiceAccounts as a concept.** Referenced in RBAC subjects, Secret types, and the ServiceAccount controller, but never defined as the Pod identity mechanism. | D2.2, D1.1 | kubernetes.io/docs/concepts/security/service-accounts/ |
| G8 | **Deployment update mechanics.** Rolling update strategy, `maxSurge`/`maxUnavailable`, `Recreate`, rollout status, revision history, rollback. D3 doubled in weight and this is its most operationally central topic; the cached Argo CD source mentions blue/green and canary only in passing. | D3.1, D1.1 | kubernetes.io/docs/concepts/workloads/controllers/deployment/ |
| G9 | **Deployment strategy vocabulary**: rolling, blue/green, canary, A/B. Named across Argo CD and Istio sources but nowhere defined or contrasted. | D3.1 | Argo Rollouts docs and/or kubernetes.io deployment strategies material |
| G10 | **CRDs, the operator pattern, and API extension.** Knative "implemented as CRDs" and Argo CD "implemented as a Kubernetes controller" both presuppose it; Kubernetes' "designed for extensibility" claim depends on it. Never defined. | D1.1, D4.2, D3.1 | kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/ and .../operator/ |
| G11 | **CNI, CSI, and CRI as the three pluggable interfaces.** CRI is covered; CNI is implied ("network plugin"); CSI is entirely absent. The three-interface story is core cloud-native-architecture framing. | D2.1, D2.4, D1.4, D4.2 | kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/ + the CNI and CSI specs |
| G12 | **Volume types other than PV/PVC**: emptyDir, hostPath, configMap/secret volumes, projected, ephemeral. A large share of real Pod storage and not covered. | D2.4 | kubernetes.io/docs/concepts/storage/volumes/ |
| G13 | **CoreDNS and DNS for Services and Pods.** The FQDN format is covered via the namespaces page, but CoreDNS as the cluster DNS addon, and Pod DNS records, are not. | D2.1 | kubernetes.io/docs/concepts/services-networking/dns-pod-service/ |
| G14 | **Kubernetes history and origin**: Borg, Google's 2014 open-sourcing, donation as CNCF's first project, the Go implementation, the name's etymology. Standard KCNA ecosystem material; the cached set never states it. | D4.2 | kubernetes.io/docs/concepts/overview/ history material + CNCF history |
| G15 | **CNCF Landscape**: what it is, how it's organized, and the trail-map framing. Named nowhere in the cached set despite being a canonical KCNA reference. | D4.2 | landscape.cncf.io + CNCF documentation |
| G16 | **Contributor ladder and KEPs.** The Kubernetes governance source explicitly defers member/reviewer/approver to a separate document, which is not cached. Kubernetes Enhancement Proposals and the ~3-per-year release cadence are absent entirely. | D4.3 | kubernetes/community membership doc; kubernetes/enhancements KEP process; kubernetes/sig-release cadence |
| G17 | **CNCF Code of Conduct, community events, and participation paths**: KubeCon, community groups, Ambassadors, LFX mentorship, Slack/mailing lists/community meetings, membership tiers. D4.3 is "Community **and Collaboration**" and the collaboration half is uncovered. | D4.3 | cncf.io community pages; CNCF Code of Conduct |

### Secondary — likely examinable, cached coverage thin, lower risk

| # | Gap | Affected competency | Note |
|---|---|---|---|
| G18 | **Flux** as the other graduated GitOps engine. Appears only as a name in the graduated-projects roster; Argo CD gets a full source. A KCNA question contrasting the two is plausible. | D3.1 | fluxcd.io docs |
| G19 | **Kustomize.** Named inside the Argo CD and Helm-adjacent material as a manifest source, never explained. Overlay/base model is worth one paragraph. | D3.1 | kubectl kustomize docs |
| G20 | **Grafana, Fluentd/Fluent Bit, Jaeger** as the concrete visualization / logging / tracing implementations. Prometheus mentions Grafana; Fluentd and Jaeger appear only in the graduated roster. Observability questions often name-drop these. | D4.1 | Project docs |
| G21 | **Golden signals / RED / USE methods.** Standard observability framing; absent. | D4.1 | Google SRE book or OpenTelemetry adjacent material |
| G22 | **Supply-chain security**: SBOM, image signing, sigstore, in-toto, TUF, Harbor, image scanning. in-toto, TUF, and Harbor appear only in the graduated roster; the concepts are unexplained. | D2.2, D1.4 | Project docs; CNCF software supply chain best practices |
| G23 | **Policy engines**: OPA/Gatekeeper, Kyverno, Falco. Roster-only mentions. Falco (runtime security) in particular is a common KCNA name-recognition target. | D2.2 | Project docs |
| G24 | **kube-proxy modes** (iptables, IPVS, nftables). kube-proxy's role is covered; its implementation modes are not. | D2.1 | kubernetes.io/docs/reference/networking/virtual-ips/ |
| G25 | **Gateway API detail.** Recommended over Ingress by the project, but the cached sources give it one sentence. Given that recommendation, the exam may test its existence and basic role. | D2.1 | gateway-api.sigs.k8s.io |
| G26 | **Node lifecycle operations**: cordon, drain, uncordon; node conditions (Ready, MemoryPressure, DiskPressure, PIDPressure); eviction. Node leases are covered; the operations are not. | D1.2, D2.3 | kubernetes.io/docs/concepts/architecture/nodes/ |
| G27 | **etcd backup and restore.** The architecture source says "make sure you have a back up plan" and stops there. | D1.2 | kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/ |
| G28 | **Cluster bootstrap tooling**: kubeadm, minikube, kind, k3s. The cluster-administration page asks planning questions and links out; nothing cached answers them. | D1.2 | kubernetes.io/docs/setup/ |
| G29 | **Container image build practices**: layers, tags vs digests, multi-stage builds, base-image selection, registries, Buildpacks. D1.4 Containerization is 1/4 of the 44% domain and the cached set covers only the runtime and OCI-spec halves. | D1.4 | OCI image-spec detail; buildpacks.io; general container-build documentation |
| G30 | **Sandboxed and alternative runtimes**: gVisor, Kata Containers, and what RuntimeClass is actually used *for*. RuntimeClass is defined; its motivating use case is not. | D1.4, D2.2 | kubernetes.io/docs/concepts/containers/runtime-class/ |
| G31 | **Adjacent CNCF certifications and personas**: KCSA, CKA, CKAD, CKS, and where KCNA sits. Useful for the book's front matter and "road ahead" framing even if not directly examinable. | Front matter | training.linuxfoundation.org certification catalog |
| G32 | **Cost management / FinOps** (OpenCost, KubeCost). Was adjacent to the old Observability domain; whether it survives into the new D4 is unclear from the sources. | D4.1/D4.2 | opencost.io; CNCF FinOps material — **and** verify against the current curriculum whether it's still in scope |

### Structural gaps — cannot be closed by research

| # | Gap | Impact |
|---|---|---|
| G33 | **Sub-competency weights are unpublished.** CNCF states domain weights only. There is no authoritative basis for allocating the 44% of D1 across Core Concepts / Administration / Scheduling / Containerization. | Chapter-weight allocation within a domain must be authored judgment, documented as such in the outline. Do not present a derived split as if CNCF published it. |
| G34 | **Question count and passing score are unpublished.** LF explicitly does not state them. | Mock Exam sizing and all exam-day pacing guidance must be framed as calibrated estimate, with the commonly-reported 60/75% cited as commonly reported. |
| G35 | **No official sample questions in the cached set.** No published item bank, no disclosed difficulty mix, no question-type breakdown beyond "multiple-choice." | Difficulty calibration (⚪🔵🟡🔴) and trap-answer design are author judgment. The **[inferred]** traps above cannot be described as "frequently tested" without evidence — describe them as "easy to confuse" instead. |
| G36 | **Curriculum text is a competency list, not an objective list.** Unlike CompTIA or PMI blueprints, CNCF publishes four domains and twelve named competencies with no sub-bullets. There is no authoritative enumeration of *which* Kubernetes concepts fall under "Kubernetes Core Concepts." | The concept map above is derived from authoritative *documentation* mapped onto the competency names, not from a published objective list. State this in the book's blueprint appendix so readers understand why the coverage map looks different from a CompTIA-style guide. |
| G37 | **The LFS250 course syllabus is not cached.** LF sells "exam + LFS250 course" as a bundle, which makes the LFS250 syllabus the closest thing to an unofficial detailed objective list. | Fetching it would substantially reduce G33 and G36 uncertainty. Recommend adding it to the source set before Stage B2. |

---

## Recommendations for the next stage

1. **Close G1–G17 before any chapter drafting.** Seventeen blocking gaps is a lot, but they cluster into about eight fetch targets on kubernetes.io plus three CNCF/community pages. This is one focused research pass, not a campaign.
2. **Fetch the LFS250 syllabus (G37) first.** It is the highest-leverage single artifact available — it is the closest thing to a detailed objective list CNCF/LF produces, and it would materially firm up the sub-competency weighting judgment that G33 otherwise leaves to guesswork.
3. **Front-matter must carry three disclosures**: the 2025-11-24 blueprint change and what it invalidates in older prep material; that question count and passing score are unpublished; and that sub-competency weights are unpublished, so chapter weighting is authored judgment. All three are Ethical Guardrail obligations, not optional courtesies.
4. **Build the D3 chapter around the GitOps-as-control-loop synthesis.** The four OpenGitOps principles restate the Kubernetes reconciliation pattern applied to Git. A reader who has met controllers in D1 will experience this as a genuine ☀️ Zenith rather than a fifth list to memorize — and D3 doubling in weight makes it worth the investment.
5. **Treat the graduated-project roster as dated data.** Any chapter listing graduated projects must state the snapshot date and frame the list as "as of," since the roster changes between the book's writing and the reader's exam.

---

*Stage B1 complete. 4 domains, 12 competencies, 114 traps catalogued, 37 gaps flagged (17 blocking, 15 secondary, 5 structural).*