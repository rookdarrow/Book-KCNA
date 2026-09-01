---
title: "Glossary — KCNA"
subtitle: "Terms and Acronyms"
tagline: "Study less. Pass once."
publisher: "Lodestar Ledgers"
edition: "First Edition"
exam_version: "KCNA curriculum effective 2025-11-24 (4 domains: 44/28/16/12)"
---

# Glossary

Every term the book uses in a load-bearing way, plus the ones you will meet in the wild and want a one-line answer for. Skim it, or `Ctrl+F` it. Entries name the chapter that owns the idea, so a term you cannot place sends you somewhere specific rather than back to the beginning.

Where a word means two different things in this material — and several do — both senses appear together, because the collision is the thing worth knowing. Those are marked **⚠ two senses**.

---

## A

**ABAC (Attribute-Based Access Control)** — An authorization mode that grants access through policies combining attributes. Kubernetes supports it; RBAC is the one the curriculum teaches and essentially every cluster uses. (Ch 12)

**Access mode** — A PersistentVolume/PersistentVolumeClaim field describing **how many nodes** may mount a volume and in what mode: `ReadWriteOnce` (RWO), `ReadOnlyMany` (ROX), `ReadWriteMany` (RWX), `ReadWriteOncePod` (RWOP). Node-count semantics, not permission semantics. (Ch 11)

**Addon** — Optional cluster software that is not part of the core control plane: CoreDNS, a CNI plugin, metrics-server, an Ingress controller. Kubernetes runs without most of them, badly. (Ch 3)

**Admission controller** — A plugin in the API server that intercepts a request after authentication and authorization but before persistence. It can validate (yes/no) or mutate (yes, in modified form). The third of the three API access gates. (Ch 8)

**Admission webhook** — An admission controller implemented outside the API server and called over HTTP. **Validating** webhooks accept or reject; **mutating** webhooks may also modify the object. (Ch 8, Ch 12)

**Aggregation layer** — The API-server mechanism that lets an extension server serve an additional API group, as metrics-server does for the Metrics API. Distinct from CRDs, which extend the API server in place. (Ch 17)

**Alertmanager** — The Prometheus component that handles alerts: deduplicating, grouping, and routing them to receivers. Prometheus evaluates rules; Alertmanager decides who hears about it. (Ch 18)

**Ambient mode** — A service-mesh data-plane arrangement using a per-node L4 proxy and optionally a per-namespace L7 proxy, instead of a sidecar in every Pod. (Ch 17)

**Annotation** — Key/value metadata on an object that **nothing selects on**. For tools, humans, and controllers that look things up by name. Contrast **label**. (Ch 4)

**API group** — A collection of related resource kinds. The core group is `""` (Pods, Services, ConfigMaps); `apps` holds Deployments and StatefulSets; `rbac.authorization.k8s.io` holds Roles and bindings. (Ch 4)

**API server (kube-apiserver)** — The control-plane component that serves the Kubernetes API. The only component that writes to etcd, and the only way into the cluster. (Ch 3)

**APIService** — An object registering an extension server to serve a particular API group through the aggregation layer. (Ch 17, Ch 18)

**Argo CD** — A declarative GitOps continuous-delivery tool. A controller inside the cluster watches a Git repository and reconciles the cluster toward it. (Ch 15)

**Attestation** — A signed statement about an artifact — how it was built, what it contains, who approved it. Provenance is one kind. (Ch 12)

**Autoscaling** — Adjusting capacity automatically. **Horizontal** adds replicas (HPA, KEDA); **vertical** resizes existing ones (VPA); **cluster** autoscaling adds and removes nodes (Cluster Autoscaler, Karpenter). (Ch 6, Ch 17)

---

## B

**Baggage** — An OpenTelemetry signal: contextual key/value data propagated alongside a trace so downstream services can read it. The signal candidates most reliably forget. (Ch 18)

**Base (Kustomize)** — A directory of valid, applicable manifests that overlays patch. Contrast a Helm **template**, which is not a manifest until values are applied. (Ch 14)

**Binding** — **⚠ two senses.** (1) The scheduler's act of writing a chosen node onto a Pod. (2) The association of a PersistentVolumeClaim with a PersistentVolume. A **RoleBinding** is a third, unrelated object. (Ch 7, Ch 11, Ch 12)

**Blue/green deployment** — Running the old and new versions side by side and switching traffic between them at once. Contrast **canary**, which shifts a fraction at a time. (Ch 15)

---

## C

**Canary deployment** — Exposing a subset of users to a new version while the rest continue on the old one, then widening if it holds. (Ch 15)

**cgroup (control group)** — The Linux kernel feature that limits and accounts for a process's resource use. What makes a container's CPU and memory limits real. (Ch 2)

**Chart** — Helm's packaging format: a directory of files describing a related set of Kubernetes resources. The **package**, not an installation of it. (Ch 14)

**Chart repository** — A remote location charts are fetched from. **⚠** Not to be confused with a chart's own `charts/` directory, which holds vendored subcharts. (Ch 14)

**`Chart.yaml`** — A chart's required metadata file. Carries `apiVersion`, `name` and `version` as required fields, and `appVersion` — the version of the *application* the chart installs — as an optional one, explicitly unrelated to `version`. (Ch 14)

**CI/CD** — Continuous Integration and Continuous Delivery/Deployment. A pipeline that builds, tests, and ships. In the **push** model it holds cluster credentials and reaches in; GitOps inverts that. (Ch 15)

**Cilium** — A CNI plugin providing a flat Layer 3 network with an eBPF data plane. A CNCF graduated project. (Ch 9)

**Cloud native** — Per the CNCF definition, an approach building and running scalable applications in modern, dynamic environments, exemplified by containers, service meshes, microservices, immutable infrastructure and declarative APIs. Never hyphenated. (Ch 17)

**CloudEvents** — A CNCF specification for describing event data in a common way, so an event from one system is intelligible to another without a bespoke adapter. (Ch 17)

**Cluster Autoscaler** — Adds and removes **nodes** in response to unschedulable Pods and underused capacity. Contrast HPA/VPA, which change workloads. (Ch 17)

**ClusterIP** — The default Service type. Exposes the Service on a cluster-internal virtual IP, reachable only from inside the cluster. (Ch 9)

**ClusterRole / ClusterRoleBinding** — RBAC objects that are not namespaced. A ClusterRole may be bound cluster-wide (ClusterRoleBinding) or into one namespace (RoleBinding). (Ch 12)

**CNI (Container Network Interface)** — The interface a network plugin implements to provide Pod networking. **A CNI plugin is required to implement the Kubernetes network model**; the container runtime loads it. (Ch 9)

**ConfigMap** — An object holding non-confidential configuration as key/value data, consumed as environment variables or mounted as a volume. (Ch 4)

**Container** — A runnable unit packaging an application with its dependencies, isolated by kernel features rather than by a separate operating system. Contrast a **virtual machine**. (Ch 2)

**containerd** — A container runtime implementing CRI. A CNCF graduated project. (Ch 2)

**Container runtime** — The software that runs containers on a node. The kubelet talks to it through CRI. (Ch 2, Ch 3)

**Context (kubeconfig)** — One named bundle of cluster, user and namespace. The **current context** is the one `kubectl` uses when you do not say otherwise. (Ch 8)

**Control loop** — A non-terminating loop that regulates a system: observe current state, compare against desired state, act to close the gap. The animating idea of Kubernetes. (Ch 3)

**Control plane** — **⚠ two senses.** (1) The cluster's: API server, etcd, scheduler, controller manager. (2) A service mesh's: the component configuring the mesh's proxies. Never use the bare phrase where both are in play. (Ch 3, Ch 17)

**Controller** — A control loop that watches one or more resource types and works to bring current state closer to the desired state recorded in `.spec`. (Ch 3)

**Controller manager (kube-controller-manager)** — The control-plane component running the built-in controllers as a single binary. (Ch 3)

**CoreDNS** — The cluster DNS addon that serves Service and Pod records. (Ch 9)

**CrashLoopBackOff** — A container that starts, exits, and is restarted, with the kubelet backing off between attempts. The Pod's **phase** is still `Running`. (Ch 13)

**CRD (CustomResourceDefinition)** — An object that adds a new resource kind to the API. Storage is all you get: nothing acts on those objects unless a controller is watching for them. (Ch 6)

**`crds/`** — A Helm chart directory whose CustomResourceDefinitions are installed before the templates render, because a chart shipping custom resources must define them before objects use them. (Ch 14)

**CRI (Container Runtime Interface)** — The interface standardizing the boundary between the kubelet and the container runtime, which is what makes runtimes interchangeable. (Ch 2)

**CRI-O** — A lightweight container runtime implementing CRI. (Ch 2)

**`crictl`** — A CLI for talking to a CRI-compatible runtime directly on a node. Useful when the cluster's own view is the thing in doubt. (Ch 13)

**CronJob** — An object that creates **Jobs** on a schedule. The factory; the Job is the product. (Ch 6)

**`CSIDriver`** — An object describing a CSI driver installed in the cluster, so Kubernetes knows how to interact with it. (Ch 11)

**CSI (Container Storage Interface)** — The interface a storage driver implements to provide volumes. The third of the four pluggable interfaces. (Ch 11)

---

## D

**DaemonSet** — A controller ensuring a copy of a Pod runs on every eligible node, tracked as nodes join and leave. Its Pods automatically tolerate the unschedulable taint, so they keep running on cordoned nodes. (Ch 6)

**Dead Reckoning** — A branded marker in this book: a facts-only block, stated without interpretation.

**Declarative API** — An API where you record the state you want and something else reconciles reality toward it. Contrast **imperative**, where you issue the steps. (Ch 4)

**Deployment** — A controller managing a ReplicaSet to run a stated number of interchangeable Pods, with rolling updates and revision history. (Ch 6)

**Desired state** — What you asked for, recorded in an object's `.spec`. Contrast **current state**, reported in `.status`. (Ch 3, Ch 4)

**Digest** — A content hash identifying an image immutably. Contrast a **tag**, which is a mutable pointer. (Ch 2)

**Distroless image** — A container image containing the application and its runtime dependencies and nothing else — no shell, no package manager. Excellent for security, awkward for `kubectl exec`, which is why ephemeral containers exist. (Ch 16)

**Drift** — A difference between the declared state in a repository and the actual state in the cluster. Argo CD reports it as `OutOfSync`, which is a status, not an error. (Ch 15)

---

## E

**eBPF** — A Linux kernel technology allowing sandboxed programs to run in kernel space, used by some CNI plugins as a data plane and by security tools such as Falco. (Ch 9, Ch 12)

**EndpointSlice** — An object listing the network endpoints backing a Service. The control plane creates them for any Service with a selector, and they reference **all** the Pods the selector matches — each endpoint carrying `ready` / `serving` / `terminating` conditions. (Ch 9)

**Endpoints (legacy object)** — The older object EndpointSlice replaced. You will meet it in `kubectl api-resources` output and in older material. This book teaches EndpointSlice. (Ch 9)

**Envoy** — A proxy commonly used as a service mesh's data plane. A CNCF graduated project. (Ch 17)

**Ephemeral container** — A container added to a **running** Pod for debugging. It exists because a Pod's container list is fixed at creation and cannot be changed. (Ch 16)

**etcd** — The consistent, distributed key-value store holding all cluster data. The only stateful component of the control plane. (Ch 3)

**Eviction** — The termination of a Pod by the kubelet or by the node controller, typically under resource pressure or after a node stops reporting. Shows as `Evicted`. (Ch 13)

**ExternalName** — A Service type mapping a name to an external hostname via a CNAME record. **⚠** Not a rung on the ClusterIP/NodePort/LoadBalancer ladder: no cluster IP, no endpoints, no proxying. (Ch 9)

---

## F

**Falco** — A CNCF runtime-security project that detects anomalous behavior at run time. (Ch 12)

**Finalizer** — A key on an object that blocks deletion until a controller has done its cleanup and removed the key. (Ch 11)

**Fixed Point** — A branded marker in this book: a must-memorize concept.

**Flannel** — A CNI plugin providing an overlay network. (Ch 9)

**Fluentd / Fluent Bit** — Log collectors, usually run as a DaemonSet. Fluentd is one word; Fluent Bit is two. Both are CNCF projects. (Ch 18)

**Flux** — A GitOps delivery agent, alternative to Argo CD. A CNCF graduated project. (Ch 15)

**FQDN (fully qualified domain name)** — A complete DNS name. In-cluster Services take the form `<service>.<namespace>.svc.<cluster-domain>`. (Ch 9)

---

## G

**Gateway API** — The role-oriented successor to Ingress, shipped as CRDs rather than built in. **GatewayClass** belongs to the infrastructure provider, **Gateway** to the cluster operator, **HTTPRoute** to the application developer. (Ch 10)

**GitOps** — An operating model where the desired state lives in Git and an agent continuously reconciles the cluster toward it. Its four OpenGitOps principles are: declarative, versioned and immutable, pulled automatically, continuously reconciled. (Ch 15)

**Golden signals** — Latency, traffic, errors, saturation. The four things worth watching on almost any service. (Ch 18)

**Grafana** — A visualization and dashboarding tool commonly paired with Prometheus. (Ch 18)

**Graduated** — The most mature CNCF project level. The ladder is Sandbox → Incubating → Graduated. **⚠** Which project sits at which level changes; the ordering is the durable fact. (Ch 17)

**gVisor** — A sandboxed container runtime providing stronger isolation than shared-kernel containers, selected via RuntimeClass. (Ch 2)

---

## H

**Harbor** — A CNCF registry project with vulnerability scanning and signing. (Ch 12)

**Headless Service** — A Service with `clusterIP: None`. Deliberate, not broken: DNS returns the Pod addresses directly instead of one virtual IP. Required by StatefulSets for per-Pod network identity. (Ch 9)

**Helm** — The package manager for Kubernetes. Charts are packages; installing one produces a **release**. (Ch 14)

**`hostPath`** — A volume type mounting a path from the node's filesystem. Ties data to one node, and a hazard in most cluster contexts. (Ch 11)

**HPA (HorizontalPodAutoscaler)** — A built-in controller that adjusts a workload's replica count based on observed metrics. Requires the Metrics API, hence metrics-server. (Ch 6, Ch 17)

**HTTPRoute** — The Gateway API resource expressing application-level routing rules. Owned by the application developer. (Ch 10)

---

## I

**`imagePullPolicy`** — When the kubelet pulls an image: `Always`, `IfNotPresent`, or `Never`. The **default is conditional on the tag** — `IfNotPresent` normally, `Always` for `:latest` or an omitted tag. (Ch 2)

**`imagePullSecrets`** — A Pod or ServiceAccount field naming Secrets holding registry credentials, of type `kubernetes.io/dockerconfigjson`. (Ch 12)

**Immutable infrastructure** — Servers and containers that are replaced rather than modified in place. **⚠** Distinct from **image immutability**, which is about a digest identifying fixed content. (Ch 17)

**Incubating** — The middle CNCF project maturity level. (Ch 17)

**Ingress** — An API object defining HTTP/HTTPS routing rules into the cluster. **Frozen**, not deprecated: feature-complete and supported, receiving no new features, with Gateway API as the recommended successor. Does nothing without an Ingress controller. (Ch 10)

**Ingress controller** — The component that reads Ingress objects and implements them, usually with a load balancer or edge router. Not shipped by default; you install one. (Ch 10)

**IngressClass** — The object naming which controller should fulfill an Ingress, referenced by `ingressClassName`. **⚠** A second default IngressClass does not create ambiguity — it removes the default, and the Ingress can no longer be created. (Ch 10)

**`Init:N/M`** — A Pod status showing that init container *N* of *M* has completed. A Pod stuck here has an init container that has not finished. (Ch 16)

**Init container** — A container that runs to completion before the Pod's application containers start, in order. (Ch 5)

**in-toto** — A CNCF framework for securing a software supply chain by making the steps of its production verifiable. (Ch 12)

**iSCSI** — A protocol carrying SCSI storage commands over IP networks; one of the volume types a PersistentVolume may be backed by. (Ch 11)

---

## J

**Jaeger** — A CNCF distributed-tracing backend: it receives, stores and visualizes traces. Contrast **OpenTelemetry**, which produces them. (Ch 18)

**Job** — A controller running one or more Pods to completion. Its Pod template may use `restartPolicy` of `Never` or `OnFailure` only. (Ch 6)

---

## K

**Karpenter** — A node-provisioning autoscaler that adds and removes cluster capacity. (Ch 17)

**Kata Containers** — A sandboxed runtime running each container in a lightweight VM. (Ch 2)

**KCNA / KCSA / CKA / CKAD / CKS** — The CNCF certification ladder: Kubernetes and Cloud Native Associate, Kubernetes and Cloud Native Security Associate, Certified Kubernetes Administrator, Certified Kubernetes Application Developer, Certified Kubernetes Security Specialist. (Ch 17)

**KEDA (Kubernetes Event-Driven Autoscaling)** — A CNCF graduated project scaling workloads on event-source metrics such as queue depth. (Ch 17)

**KEP (Kubernetes Enhancement Proposal)** — The document and process through which a substantial change to Kubernetes is proposed, brought to the SIG that owns the area. (Ch 17)

**kind** — A tool running Kubernetes clusters in Docker containers, for local development and testing. (Ch 8)

**kubeadm** — The officially supported tool for bootstrapping a cluster: installing the control plane and joining nodes. (Ch 8)

**kubeconfig** — The file holding cluster addresses, credentials and contexts. `kubectl` looks for `$HOME/.kube/config`, overridable by `KUBECONFIG` or `--kubeconfig`. (Ch 8)

**kubectl** — The command-line client for the Kubernetes API. **⚠** Version skew: within **one** minor version of the API server, in **either** direction — the only component permitted to be newer. (Ch 8)

**kubelet** — The node agent that runs containers described for its node and reports node and Pod status. **⚠** Version skew: up to **three** minor versions older than the API server, and never newer. (Ch 3, Ch 8)

**kube-proxy** — The node component implementing the Service virtual-IP mechanism, by watching Services and EndpointSlices and programming node rules. Modes on Linux: **iptables (default)**, IPVS, nftables; on Windows, kernelspace. Optional — some CNI plugins do the work themselves. (Ch 9)

**Kubernetes network model** — The four requirements every implementation must satisfy: every Pod gets its own cluster-wide IP; Pods can reach all other Pods without NAT; node agents can reach Pods on their node; and Pods see their own address as others see it. (Ch 9)

**Kustomize** — A tool patching a shared base with per-environment overlays, without a templating language. Built into `kubectl` as `apply -k`. (Ch 14)

**Kyverno** — A CNCF policy engine whose policies are Kubernetes resources written in YAML and CEL. Contrast **OPA Gatekeeper**, which uses Rego. (Ch 12)

---

## L

**Label** — **⚠ two senses.** (1) Kubernetes: key/value metadata that selectors query. (2) Prometheus: a dimension on a time series. In Kubernetes, labels are selectable and annotations are not. (Ch 4, Ch 18)

**LimitRange** — A namespaced policy setting **per-object** defaults and bounds for resource requests and limits. Contrast **ResourceQuota**, which caps the namespace's aggregate. (Ch 8)

**Liveness probe** — A probe whose failure **restarts** the container. Contrast readiness (removes from endpoints) and startup (suspends the other two while booting). (Ch 5)

**LoadBalancer** — The Service type requesting an external load balancer from the provider. Kubernetes provides no load balancer itself; without an integration the address stays pending indefinitely. (Ch 9)

**LUN (Logical Unit Number)** — In a traditional storage array, an addressable unit of storage. The pre-Kubernetes analogue of a PersistentVolume. (Ch 11)

---

## M

**Manifest** — **⚠ two senses.** (1) A YAML or JSON file describing a Kubernetes object. (2) In OCI, the document listing an image's layers and configuration. (Ch 2, Ch 4)

**`maxSurge` / `maxUnavailable`** — Deployment rolling-update bounds. `maxSurge` is how far above the desired replica count the total may go; `maxUnavailable` is how far below the ready count may fall. (Ch 6)

**Metrics API** — The API serving CPU and memory metrics for autoscaling and `kubectl top`. Requires an extension server — normally metrics-server — registered through the aggregation layer. (Ch 13, Ch 18)

**metrics-server** — The cluster addon collecting resource metrics from each kubelet and serving the Metrics API. **Not installed by default** in many distributions, which is why `kubectl top` so often fails. Meant for autoscaling, not monitoring. (Ch 13)

**Microservices** — An architecture decomposing an application into independently deployable services. The trade: independent deployment and scaling, at the cost of operational and network complexity. (Ch 17)

**minikube** — A tool running a local single-node cluster for learning and development. (Ch 8)

**Mirror Pod** — The API-server representation of a static Pod, so that `kubectl` can show it. (Ch 13)

**Monitoring** — Collecting, processing, aggregating and displaying real-time quantitative data about a system — questions you decided in advance to ask. Contrast **observability**. (Ch 18)

**Mutating admission webhook** — An admission webhook that may modify an object before persistence. (Ch 8, Ch 12)

---

## N

**Namespace** — **⚠ two senses.** (1) Linux kernel: an isolation primitive giving a process its own view of a resource. (2) Kubernetes: a scope for object names, quota and policy. (Ch 2, Ch 4)

**NAT (Network Address Translation)** — Rewriting addresses as packets traverse a boundary. The Kubernetes network model forbids it between Pods. (Ch 9)

**NetworkPolicy** — A namespaced object restricting Pod traffic at layer 3/4. **Additive and allow-only**: a Pod selected by no policy is fully open; a Pod selected by any policy is restricted to the union of what its policies permit. There is no deny rule, and it does nothing unless the network plugin implements it. (Ch 10)

**NFS (Network File System)** — A protocol for sharing filesystems over a network; a volume type supporting multiple simultaneous writers, and therefore `ReadWriteMany`. (Ch 11)

**Node** — A worker machine, virtual or physical, running the kubelet, a container runtime, and usually kube-proxy. (Ch 3)

**Node affinity** — A Pod's expression of preference or requirement for nodes carrying particular labels. `required…` filters; `preferred…` scores. Contrast **taints**, where the node does the refusing. (Ch 7)

**Node condition** — A node's self-reported status: `Ready`, `MemoryPressure`, `DiskPressure`, `PIDPressure`, `NetworkUnavailable`. **⚠** `Ready=False` means the node is reporting a problem; `Ready=Unknown` means it has stopped reporting at all. (Ch 8, Ch 13)

**NodePort** — A Service type exposing the Service on a static port on every node, drawn from `--service-node-port-range` (default **30000–32767**). It **adds** a cluster IP rather than replacing it. (Ch 9)

**`nodeSelector`** — The simplest node-selection field: a hard requirement that the node carry the given labels. (Ch 7)

---

## O

**Observability** — Being able to understand a system from the outside, and to ask questions of it you did not anticipate. Contrast **monitoring**. (Ch 18)

**OCI (Open Container Initiative)** — The body publishing the image, runtime and distribution specifications. **⚠** OCI standardizes the artifact and its execution; CRI standardizes the kubelet's conversation with a runtime. (Ch 2)

**OOMKilled** — The reason recorded when a container exceeds its memory limit and is terminated. The kernel does the killing; the kubelet observes and applies the `restartPolicy`. (Ch 5, Ch 13)

**OPA (Open Policy Agent)** — A CNCF policy engine; with Gatekeeper it enforces policy at admission, using the Rego language. (Ch 12)

**OpenTelemetry (OTel)** — The CNCF project providing APIs, SDKs and a Collector for producing telemetry. Its signals are **traces, metrics, logs and baggage**. Contrast Jaeger, a backend. (Ch 18)

**Operator** — **⚠ two senses.** (1) The operator *pattern*: a custom resource plus a controller that acts on it, encoding operational knowledge. (2) "Cluster operator" as a **role name** in Gateway API. Never use the bare word for a person. (Ch 6, Ch 10)

**`OutOfSync`** — Argo CD's report that the cluster differs from the repository. A status describing drift, not an error. (Ch 15)

**Overlay (Kustomize)** — A directory patching a base for one environment. (Ch 14)

---

## P

**PersistentVolume (PV)** — A piece of storage in the cluster, provisioned by an administrator or dynamically by a StorageClass. Cluster-scoped: it belongs to no namespace. **Supply.** (Ch 11)

**PersistentVolumeClaim (PVC)** — A workload's request for storage. **Namespaced** — it must live in the same namespace as the Pod using it. **Demand.** A Pod references a PVC, never a PV directly. (Ch 11)

**Phase (Pod)** — A Pod's high-level position in its lifecycle: `Pending`, `Running`, `Succeeded`, `Failed`, `Unknown`. **⚠** `Running` means bound with at least one container running, starting **or restarting** — a crash-looping Pod reports `Running`. Contrast **container state**. (Ch 5)

**Pod** — The smallest deployable unit: one or more containers sharing a network namespace, an IP address and storage volumes. Not a container. (Ch 5)

**Pod Security Admission (PSA)** — The built-in admission controller enforcing the Pod Security Standards, configured per namespace by label. Its **modes** are `enforce`, `audit`, `warn`. (Ch 12)

**Pod Security Standards (PSS)** — Three cumulative policies: `privileged`, `baseline`, `restricted`. **⚠** Levels say what is checked; modes say what happens. Independent axes. (Ch 12)

**PodDisruptionBudget (PDB)** — A policy limiting how many replicas of a workload may be voluntarily disrupted at once, which a drain must respect. (Ch 8)

**`port` / `targetPort` / `nodePort`** — `port` is exposed by the Service; `targetPort` is on the container; `nodePort` is on every node. `targetPort` defaults to `port`, which is why the distinction is easy to miss. (Ch 9)

**Prometheus** — A CNCF monitoring system that **pulls** metrics by scraping targets, stores them as time series, and queries them with PromQL. (Ch 18)

**Provenance** — A verifiable record of how and where an artifact was built. The build-process half of supply-chain security; the **SBOM** is the components half. (Ch 12)

**Pushgateway** — A Prometheus intermediary for jobs that cannot be scraped — short-lived batch work. Not a general workaround for the pull model. (Ch 18)

---

## Q

**QoS class** — A Pod's quality-of-service classification, derived from its containers' requests and limits: `Guaranteed`, `Burstable`, `BestEffort`. Determines eviction order under node pressure. (Ch 5)

---

## R

**RBAC (role-based access control)** — The authorization mode regulating access by role. **Additive and allow-only**: permissions are the union of every binding naming you, and nothing subtracts. **⚠** After a binding is created you cannot change the Role it refers to. (Ch 12)

**Readiness probe** — A probe determining whether a container should receive traffic. Failure removes the endpoint from service **without restarting** the container. (Ch 5)

**Reclaim policy** — What happens to a PersistentVolume after its claim is deleted: `Retain` (kept for manual reclamation), `Delete` (object and backing storage removed), `Recycle` (**deprecated**). (Ch 11)

**Release (Helm)** — One installed instance of a chart, with a name. Installing the same chart twice gives two releases. **⚠** Distinct from a Kubernetes minor **release**. (Ch 14)

**ReplicaSet** — The controller maintaining a stated number of identical Pods. Normally managed by a Deployment rather than created directly. (Ch 6)

**Requests and limits** — A container's declared resource floor and ceiling. **Requests** are what the scheduler counts when placing a Pod; **limits** are what the kubelet and kernel enforce at run time. (Ch 5)

**ResourceQuota** — A namespaced policy capping **aggregate** consumption. Contrast **LimitRange**, which sets per-object defaults. (Ch 8)

**`restartPolicy`** — A Pod field governing restarts of **containers within the Pod**, not of the Pod object: `Always`, `OnFailure`, `Never`. (Ch 5)

**Revision** — **⚠ two senses.** (1) A Deployment's numbered rollout history entry. (2) A Helm release's numbered version. (Ch 6, Ch 14)

**Reverse proxy** — A server that accepts a client's request and forwards it to a backend on the client's behalf. What an Ingress controller is, mechanically. (Ch 10)

**Rollback** — **⚠ three senses.** `kubectl rollout undo` walks a Deployment's revisions; `helm rollback` returns a release to a revision; **rollback by revert** changes a commit and lets a GitOps agent reconcile. (Ch 6, Ch 14, Ch 15)

**Rolling update** — Replacing a workload's Pods incrementally, bounded by `maxSurge` and `maxUnavailable`, so the service stays available throughout. (Ch 6)

**Role / RoleBinding** — Namespaced RBAC objects: a Role holds permissions, a RoleBinding grants them to subjects within that namespace. (Ch 12)

**runC** — The reference OCI runtime that actually creates containers. (Ch 2)

**RuntimeClass** — An object selecting which runtime configuration a Pod uses, the mechanism by which sandboxed runtimes are chosen. (Ch 2)

---

## S

**Sandbox** — **⚠ two senses.** (1) A sandboxed **runtime** such as gVisor or Kata, giving stronger isolation. (2) The entry-level **CNCF maturity level**. (Ch 2, Ch 17)

**SBOM (Software Bill of Materials)** — A standardized inventory of the components an artifact contains. The two dominant standards are **SPDX** (Linux Foundation) and **CycloneDX** (OWASP). Answers "what is in this image," which a scan report from last week does not. (Ch 12)

**Scheduler (kube-scheduler)** — The control-plane component that assigns Pods to nodes: **filter** to the feasible nodes, **score** those, **bind** to the winner. It decides; the kubelet does the starting. (Ch 7)

**Secret** — An object holding confidential data. **⚠** Base64-**encoded**, not encrypted; encryption at rest is a separate cluster configuration. (Ch 4, Ch 12)

**Selector** — A query over labels. Equality-based or set-based. What a Service, a ReplicaSet and a NetworkPolicy each use to name a set of Pods. (Ch 4)

**Service** — **⚠ two senses.** (1) The Kubernetes object giving a set of Pods a stable address and name. (2) A **Knative Service**, always written in full. (Ch 9, Ch 17)

**ServiceAccount** — A Pod's identity to the API server, and an RBAC **subject**. Every namespace has a `default` one, which can do almost nothing. (Ch 5, Ch 12)

**Service mesh** — A layer handling service-to-service communication through proxies, with a **data plane** (the proxies) and a **control plane** (what configures them). Provides mTLS, retries, and traffic policy without application changes. (Ch 17)

**SIG (Special Interest Group)** — An ongoing Kubernetes group owning a topic area. Contrast a **Working Group** (time-bounded, spans SIGs) and a **Committee** (closed membership). (Ch 17)

**SLI / SLO / SLA** — A **service level indicator** is a measure; an **objective** is a target for it; an **agreement** is the external contract with consequences. Measure, target, consequence. (Ch 18)

**SNI (Server Name Indication)** — A TLS handshake extension carrying the requested hostname, letting one address serve several hostnames' certificates. (Ch 10)

**Span** — A single unit of work in a distributed trace. A **trace** is the tree of spans following one request; a **root span** is the first. (Ch 18)

**`spec` / `status`** — An object's two halves: `spec` is the desired state you write, `status` is the observed state the system reports. (Ch 4)

**Startup probe** — A probe that suspends liveness and readiness checks until an application has finished starting. (Ch 5)

**Static Pod** — A Pod managed directly by a kubelet from a file on the node, represented in the API by a **mirror Pod**. (Ch 13)

**StatefulSet** — A controller for Pods that are **not interchangeable**: stable ordinal names, ordered startup, and a per-replica PersistentVolumeClaim from a `volumeClaimTemplate`. Requires a headless Service for network identity. **⚠** The distinction from Deployment is *identity*, not "writes to disk." (Ch 6, Ch 11)

**StorageClass** — An object describing a class of storage and naming a provisioner, enabling dynamic provisioning. `volumeBindingMode` of `Immediate` binds on claim creation; `WaitForFirstConsumer` waits for a Pod, so the volume matches its scheduling constraints. (Ch 11)

**Subject (RBAC)** — Whatever a grant is made to: a user, a group, or a ServiceAccount. (Ch 12)

---

## T

**TAG (Technical Advisory Group)** — A CNCF-level group coordinating interests across projects. Contrast a Kubernetes **SIG**, which is project-level. (Ch 17)

**Taint / toleration** — A **taint** is a node repelling Pods by default (`NoSchedule`, `PreferNoSchedule`, `NoExecute`); a **toleration** is a Pod's permission to ignore it. The node refuses; affinity is the Pod asking. (Ch 7)

**Tag** — A mutable, human-readable pointer to an image. Can be moved to a different image tomorrow; a **digest** cannot. (Ch 2)

**TOC (Technical Oversight Committee)** — The CNCF body holding the technical vision and overseeing project lifecycle. Contrast the **Governing Board** (marketing, business oversight, budget) and the **End User TAB** (advisory voice of end users). (Ch 17)

**Tiller** — The cluster-side component Helm 2 used to hold release state and apply changes. Removed in Helm 3, which talks to the API server directly as the user. A frequent distractor. (Ch 14)

**TokenRequest** — The API through which short-lived, audience-scoped ServiceAccount tokens are issued, replacing long-lived token Secrets. (Ch 12)

**Topology spread constraints** — A Pod field distributing replicas across failure domains, bounded by `maxSkew`. (Ch 7)

**Trace** — The tree of spans following one request across services. One of OpenTelemetry's signals. (Ch 18)

**TUF (The Update Framework)** — A CNCF framework for securing software update systems. (Ch 12)

**Twelve-factor app** — A methodology for building services. Factor III, configuration in the environment, is what ConfigMaps and Secrets implement: one image, every environment. (Ch 15)

---

## V

**Validating admission webhook** — An admission webhook that accepts or rejects an object without modifying it. (Ch 8, Ch 12)

**Version skew** — The supported version differences between components. **kubelet:** up to three minors older than the API server, never newer. **`kubectl`:** within one minor, either direction. Three supported minor releases; roughly three releases a year. (Ch 8)

**Volume** — **⚠ two senses.** (1) A directory in a Pod spec that the Pod's containers share, living as long as the Pod. (2) A **PersistentVolume**, a cluster resource with its own lifecycle. (Ch 11)

**`volumeClaimTemplate`** — A StatefulSet field producing one PersistentVolumeClaim per replica, so each Pod keeps its own storage across rescheduling. (Ch 11)

**VPA (VerticalPodAutoscaler)** — Adjusts the resource requests of existing Pods. **⚠** Not part of core Kubernetes — an add-on you deploy. (Ch 17)

---

## W

**Waypoint proxy** — In ambient mode, the optional per-namespace Layer 7 proxy. (Ch 17)

**Working Group** — A **time-bounded** Kubernetes group spanning SIG boundaries. (Ch 17)

**Workload** — An application running on Kubernetes, expressed through a controller: Deployment, StatefulSet, DaemonSet, Job, CronJob. (Ch 6)

---

## Acronyms

| Acronym | Expansion |
|---|---|
| ABAC | Attribute-Based Access Control |
| API | Application Programming Interface |
| BGP | Border Gateway Protocol |
| CA | Cluster Autoscaler |
| CD | Continuous Delivery / Continuous Deployment |
| CEL | Common Expression Language |
| CI | Continuous Integration |
| CKA | Certified Kubernetes Administrator |
| CKAD | Certified Kubernetes Application Developer |
| CKS | Certified Kubernetes Security Specialist |
| CNAME | Canonical Name (DNS record) |
| CNCF | Cloud Native Computing Foundation |
| CNI | Container Network Interface |
| CRD | CustomResourceDefinition |
| CRI | Container Runtime Interface |
| CSI | Container Storage Interface |
| DNS | Domain Name System |
| eBPF | extended Berkeley Packet Filter |
| EBS | Elastic Block Store |
| FaaS | Functions as a Service |
| FQDN | Fully Qualified Domain Name |
| GUID | Globally Unique Identifier |
| HPA | HorizontalPodAutoscaler |
| iSCSI | Internet Small Computer Systems Interface |
| IPVS | IP Virtual Server |
| KCNA | Kubernetes and Cloud Native Associate |
| KCSA | Kubernetes and Cloud Native Security Associate |
| KEDA | Kubernetes Event-Driven Autoscaling |
| KEP | Kubernetes Enhancement Proposal |
| LTS | Long-Term Support |
| LUN | Logical Unit Number |
| mTLS | mutual Transport Layer Security |
| NAT | Network Address Translation |
| NFS | Network File System |
| OCI | Open Container Initiative |
| OIDC | OpenID Connect |
| OOM | Out Of Memory |
| OPA | Open Policy Agent |
| OSI | Open Systems Interconnection |
| OTel | OpenTelemetry |
| OWASP | Open Worldwide Application Security Project |
| PDB | PodDisruptionBudget |
| PSA | Pod Security Admission |
| PSS | Pod Security Standards |
| PV | PersistentVolume |
| PVC | PersistentVolumeClaim |
| QoS | Quality of Service |
| RBAC | Role-Based Access Control |
| ROX | ReadOnlyMany |
| RWO | ReadWriteOnce |
| RWOP | ReadWriteOncePod |
| RWX | ReadWriteMany |
| SBOM | Software Bill of Materials |
| SIG | Special Interest Group |
| SLA | Service Level Agreement |
| SLI | Service Level Indicator |
| SLO | Service Level Objective |
| SNI | Server Name Indication |
| SPDX | Software Package Data Exchange |
| SRE | Site Reliability Engineering |
| TAB | Technical Advisory Board |
| TAG | Technical Advisory Group |
| TLS | Transport Layer Security |
| TOC | Technical Oversight Committee |
| TUF | The Update Framework |
| VM | Virtual Machine |
| VPA | VerticalPodAutoscaler |
| WG | Working Group |
