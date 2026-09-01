# Chapter 20: Full Mock Exam

## *"Ninety minutes. No notes. Find out."*

---

## Instructions

You have reached the last chapter, and it is the only one that does not teach you anything.

Nineteen chapters have explained. This one measures. There is no Soundings block here, no Fixed Points, no callouts in the margin — a diagnostic instrument that keeps interrupting itself with encouragement is not a diagnostic instrument. The voice comes back in the walkthroughs, after the clock stops.

**Dead Reckoning:** The Linux Foundation publishes both of the numbers this instrument is built around, in its candidate handbook, for multiple-choice exams as a class. The multiple-choice exam "consists of 60* multiple-choice questions" and candidates "have 90* minutes to complete" it `[source: lf-mc-exam-important-instructions-2026-08-31]`. The asterisks resolve to a footnote naming CNPA — a different exam, with 85 questions and 120 minutes — not to a hedge about the class figures. KCNA belongs to that class: the Linux Foundation's own exam-code table lists KCNA in the multiple-choice column, alongside KCSA and LFCA, with CKA and CKAD in the performance-based column beside it `[source: lf-exam-user-interface-exam-codes-2026-08-31]`. Neither figure appears on the KCNA product page, which is exactly the provenance lesson Chapter 1 spent a section on — *[cross-bearing: see Ch 1 § Ninety Minutes: The Exam as Published]*.

So: **sixty questions, ninety minutes.**

### What this instrument is, and is not

It is sized to the published count and weighted to the published blueprint — 44% Kubernetes Fundamentals, 28% Container Orchestration, 16% Cloud Native Application Delivery, 12% Cloud Native Architecture `[source: cncf-curriculum-kcna-readme-2026-08-31]`. Twenty-six questions, seventeen, ten, and seven.

It was written by Lodestar Ledgers. It is not a leaked exam, not a reconstruction of one, and not a prediction of your score. Every question here is answerable from material this book taught, which is a property no real exam has.

What it predicts is *readiness*, and it does that through the per-domain breakdown at the end rather than through the total. Hold that thought until you get there; it is the reason this chapter exists at all.

### Conditions worth reproducing

One sitting. No notes, no cluster, no documentation, no search. Ninety minutes on a timer you can see.

A reader who looks things up is measuring how good this book's index is. That is a fine thing to measure, but it is not the thing you came here for.

### How the real console behaves

The Linux Foundation documents the multiple-choice exam interface in its candidate handbook. You move between items with Previous and Next; you can flag an item for later review; flagged items are highlighted on a Review Screen, and you can return to one and change your answer. When you reach the final item you are prompted to review, and the Review Screen carries the Finish Exam button. A Pause Exam function exists, and using it does not stop the timer `[source: lf-examui-multiple-choice-2026-08-31]`.

On paper here you can obviously do all of that and more. The behavior that matters — flag, move on, come back — is available to you in both places, and Chapter 19 owns what to do with it: *[cross-bearing: see Ch 19 §3 — pacing and time discipline]*.

That section also owns the pacing rule, which is stated as a fraction of the clock rather than as seconds per question, and for a reason worth remembering rather than re-deriving. Finish the first pass at roughly 60% of the time — **54 minutes of the 90** — and keep about 36 in reserve for the flagged items and the second look.

### One thing the real exam will not give you

Your score report arrives within 24 hours, by email and on the Portal. It tells you whether you passed. It does not tell you which domain you were weak in: the Linux Foundation states plainly that it "does not report performance on individual items and will not honor requests for more detailed information" `[source: lf-exam-scoring-and-notification-2026-08-31]`.

That is the whole argument for the score sheet at the end of this chapter. The per-domain breakdown you are about to generate is not a convenience duplicating something the real exam hands you afterward. It is the only domain-level diagnostic available to you anywhere in this preparation, and it is available only before the exam, which is the only time it can change anything.

### The answers

They are in the block after the exam, headed **Mock Exam Answers & Walkthroughs**. Do not read ahead into it. Every question there carries the correct answer, an explanation of why each of the three wrong options is wrong, the domain it belongs to, and a pointer back to the section that taught it.

When you are ready, start the clock.

---

## Exam

**1.** A container and a virtual machine both run an application in isolation from the host's other workloads. Which statement correctly distinguishes them?

A. A container runs its own kernel; a virtual machine shares the host's kernel
B. A container is a host process given an isolated view of the system and shares the host's kernel; a virtual machine runs its own kernel on virtualized hardware
C. A container cannot be resource-limited; a virtual machine can
D. A container requires a hypervisor; a virtual machine requires a container runtime

---

**2.** Which Kubernetes component is the only one that writes to cluster state?

A. kube-scheduler
B. kubelet
C. kube-apiserver
D. kube-controller-manager

---

**3.** A Deployment's `.spec.replicas` is set to 5. An administrator manually deletes one of the five Pods. What happens next, and which component is responsible?

A. Nothing; the Deployment records desired state but does not act on it
B. The ReplicaSet controller observes four Pods against a desired five and creates a replacement
C. The scheduler detects the shortfall and schedules a replacement directly
D. The kubelet on the node where the Pod ran recreates it from its local cache

---

**4.** A Pod manifest sets a container's memory request to `256Mi` and its memory limit to `512Mi`. Which QoS class does the Pod receive, assuming this is its only container?

A. Guaranteed
B. Burstable
C. BestEffort
D. The QoS class is determined by the Pod's priority class, not by its resources

---

**5.** An image is referenced as `registry.example.com/team/api:v2`. The same tag is later pushed again, pointing at different content. Which statement is true?

A. Tags are immutable; the second push would be rejected
B. The tag is a mutable pointer, so `:v2` now resolves to different content; a digest reference would not have changed
C. Both pushes are retained under `:v2` and the registry serves whichever is closer
D. The digest changes to match the new content, so digest references also follow the update

---

**6.** Which statement about a Kubernetes Namespace is correct?

A. It provides kernel-level isolation between the processes of different namespaces
B. It is a scope for names, and some resource kinds exist outside it entirely
C. Every Kubernetes resource kind is namespaced
D. It is the same mechanism as the Linux namespaces that isolate a container

---

**7.** A CNI plugin has not been installed on a freshly bootstrapped cluster. What is the most likely observed symptom?

A. The API server refuses to start
B. Pods are created but remain in `Pending`, and cluster networking does not function
C. Pods run normally but cannot reach the internet
D. Services are created but have no ClusterIP assigned

---

**8.** A Service of type `ClusterIP` selects Pods with the label `app: web`. Three Pods carry that label; one of them is failing its readiness probe. How many endpoints does the Service have?

A. Three — readiness affects restarts, not endpoints
B. Two — a Pod that is not ready is removed from the Service's endpoints
C. Zero — one unready Pod invalidates the whole EndpointSlice
D. Three, but traffic to the unready Pod is silently dropped by kube-proxy

---

**9.** Which of the following is the CNCF's stated purpose for the KCNA-level tier of certification, as reflected in the curriculum's own description?

A. To certify production cluster administrators
B. To provide a beginner-friendly option for learning about the Kubernetes community and the cloud native ecosystem
C. To replace the CKA for candidates who prefer multiple-choice formats
D. To certify security specialists working with Kubernetes

---

**10.** A `helm rollback` and a `kubectl rollout undo` both move a workload backward. Which statement correctly distinguishes them?

A. They are aliases; Helm delegates to `kubectl rollout undo`
B. `helm rollback` restores a previous release revision of the whole chart; `kubectl rollout undo` reverts a single Deployment to a previous ReplicaSet
C. `kubectl rollout undo` works on Helm-installed workloads; `helm rollback` does not
D. `helm rollback` operates on the Deployment's revision history stored in `revisionHistoryLimit`

---

**11.** Which statement about a StatefulSet is the reason it exists as a separate workload kind from a Deployment?

A. Only a StatefulSet can mount a PersistentVolumeClaim
B. It gives each replica a stable ordinal identity and a stable network name that survive rescheduling
C. It schedules replicas one per node
D. Only a StatefulSet supports rolling updates

---

**12.** ```yaml
apiVersion: v1
kind: Pod
metadata:
  name: check
spec:
  containers:
    - name: app
      image: example/app:1.0
```

The Pod above is applied and stays in `Pending`. Which of the following is a plausible cause?

A. The image tag does not exist in the registry
B. No node has sufficient allocatable resources or otherwise passes the scheduler's filters
C. The container's process exited immediately on startup
D. The container was killed for exceeding its memory limit

---

**13.** In the four-layer cloud native security model, which layer is the outermost — the one whose compromise undermines every layer inside it?

A. Code
B. Container
C. Cluster
D. Cloud

---

**14.** An operator applies a NetworkPolicy that allows ingress to Pods labeled `app: db` from Pods labeled `app: api`, and a second NetworkPolicy that denies ingress from `app: batch`. What is the effect?

A. Both are honored; `app: batch` is explicitly blocked
B. NetworkPolicy has no deny rules; the second policy cannot be expressed, and selection alone makes the target default-deny for anything not allowed
C. The second policy overrides the first
D. The policies conflict and neither takes effect

---

**15.** A container reads its database password from a file mounted from a Secret. Which statement about that Secret is accurate?

A. The value is encrypted by default in etcd
B. The value is base64-encoded, which is an encoding and not protection; encryption at rest is a separate configuration
C. base64 encoding makes the value unreadable to anyone with etcd access
D. Secrets cannot be mounted as files, only injected as environment variables

---

**16.** Which of the following is the correct order of the three gates every request to the API server passes through?

A. Admission, authentication, authorization
B. Authentication, admission, authorization
C. Authentication, authorization, admission
D. Authorization, authentication, admission

---

**17.** A `kubectl get pods` shows a Pod with status `CrashLoopBackOff` and eleven restarts. Which command retrieves the output of the container run that most recently failed?

A. `kubectl logs <pod>`
B. `kubectl logs <pod> --previous`
C. `kubectl describe pod <pod>`
D. `kubectl events --for pod/<pod>`

---

**18.** Which statement describes GitOps as distinct from a conventional CI/CD pipeline?

A. GitOps requires the cluster's credentials to be held by the build system
B. An agent inside the cluster pulls desired state from a repository and reconciles continuously, rather than an external system pushing changes in
C. GitOps applies manifests only on merge, never continuously
D. GitOps replaces declarative manifests with imperative deployment scripts

---

**19.** A Pod's container is terminated and the container state's `Reason` reads `OOMKilled`. What does this indicate?

A. The node ran out of memory and the kubelet evicted the Pod
B. The container exceeded its own memory limit and was terminated by the kernel
C. The container's liveness probe failed
D. The scheduler could not find a node with enough memory

---

**20.** What does an Ingress object accomplish on a cluster where no Ingress controller is installed?

A. It routes traffic using kube-proxy as a fallback
B. Nothing; the object is accepted and stored, but no component acts on it
C. It is rejected by the API server as invalid
D. It automatically provisions a cloud load balancer

---

**21.** Which of these is the durable, testable fact about the CNCF project maturity levels?

A. The current list of Graduated projects
B. The ordered progression from Sandbox through Incubating to Graduated, and what each level signals
C. The number of projects at each level
D. The date each project graduated

---

**22.** An init container in a Pod exits with a non-zero status. What happens?

A. The Pod's application containers start anyway; init failures are advisory
B. The Pod does not proceed to its application containers; the init container is retried according to the Pod's `restartPolicy`
C. The Pod is deleted and rescheduled on a different node
D. The next init container in the list runs, and the failure is recorded as an event

---

**23.** A cluster administrator wants to take a node out of service for maintenance without losing the workloads running on it. Which sequence is correct?

A. `kubectl drain` then `kubectl cordon`
B. `kubectl cordon` then `kubectl drain`
C. `kubectl delete node` then re-register it
D. `kubectl taint node ... NoExecute` then `kubectl uncordon`

---

**24.** Which statement about the relationship between a Deployment, a ReplicaSet, and a Pod is correct?

A. A Deployment creates Pods directly; the ReplicaSet is a status record
B. A Deployment manages ReplicaSets, and each ReplicaSet manages a set of Pods; a rolling update creates a new ReplicaSet
C. A ReplicaSet manages Deployments, which manage Pods
D. A Deployment and a ReplicaSet are the same object under two API versions

---

**25.** Which of the following best describes an operator in the Kubernetes sense?

A. A human administrator with cluster-admin permissions
B. A controller that manages a custom resource, encoding operational knowledge about an application into a reconciliation loop
C. A CLI plugin that extends `kubectl`
D. A webhook that mutates objects at admission time

---

**26.** A PersistentVolumeClaim requests `ReadWriteOnce`. What does this constrain?

A. Only one Pod in the cluster may ever use the volume
B. The volume may be mounted read-write by Pods on a single node
C. The volume may be read but not written after the first write
D. Only one container within a Pod may mount it

---

**27.** Which of the following is true of `kubectl top pods` on a cluster where nothing beyond the core control plane has been installed?

A. It works; the API server aggregates resource usage by default
B. It fails, because the metrics pipeline depends on metrics-server, which is an addon and not installed by default
C. It works, but only reports CPU and not memory
D. It fails, because `kubectl top` requires Prometheus

---

**28.** In a Helm chart, what is the role of `values.yaml`?

A. It is the rendered manifest that Helm applies to the cluster
B. It supplies the default parameter values that the chart's templates consume, and which a user may override at install time
C. It declares the chart's name, version, and dependencies
D. It contains the CustomResourceDefinitions the chart installs

---

**29.** A Pod has a liveness probe and a readiness probe, both HTTP GETs against different paths. The readiness probe begins failing while the liveness probe continues to succeed. What happens?

A. The container is restarted
B. The Pod is removed from its Services' endpoints but the container keeps running
C. The Pod is evicted from the node
D. Both probes must fail before any action is taken

---

**30.** Which describes the relationship between the four golden signals and the RED method?

A. They are the same four measures under different names
B. They are complementary framings of what to measure; the golden signals are latency, traffic, errors, and saturation, while RED covers rate, errors, and duration
C. RED replaced the golden signals when OpenTelemetry was standardized
D. The golden signals apply to infrastructure and RED applies only to databases

---

**31.** A taint is applied to a node with the effect `NoExecute`. What is the consequence for a running Pod on that node that does not tolerate the taint?

A. Nothing; `NoExecute` affects only future scheduling
B. The Pod is evicted
C. The Pod continues running but is marked `NotReady`
D. The Pod is restarted in place with the toleration added automatically

---

**32.** A container image is built `FROM` a base image and adds two layers. A second image is built from the same base and adds one different layer. What does the registry store?

A. Two complete, independent copies of both images
B. The shared base layers once, plus each image's distinct layers
C. Only the most recently pushed image; the older one is garbage collected
D. A single merged image with all layers from both

---

**33.** Which statement about Kubernetes version skew is accurate?

A. All cluster components must run identical versions
B. Supported component versions may differ within a defined window; a kubelet may run behind the API server by a bounded number of minor versions
C. The kubelet must always be ahead of the API server
D. Version skew applies only to the `kubectl` client

---

**34.** What distinguishes a headless Service from a standard ClusterIP Service?

A. A headless Service has no selector
B. A headless Service sets `clusterIP: None` and returns the Pod addresses directly in DNS rather than a single virtual IP
C. A headless Service cannot be used with StatefulSets
D. A headless Service is only reachable from outside the cluster

---

**35.** An organization wants configuration that varies between staging and production without maintaining two copies of the manifests, and prefers not to use templating. Which tool matches?

A. Helm
B. Kustomize, using a base and per-environment overlays
C. Argo CD sync waves
D. A ConfigMap generator in Helm

---

**36.** A Pod that mounts an `emptyDir` volume is deleted and its controller recreates it on the same node. What happens to the data in the volume?

A. It persists; `emptyDir` is bound to the node
B. It is lost; an `emptyDir` volume's lifetime is the Pod's
C. It persists if the Pod has the same name
D. It is migrated to the new Pod automatically

---

**37.** Which statement about RBAC in Kubernetes is correct?

A. RBAC rules can both grant and deny; a deny rule overrides a grant
B. RBAC is purely additive — permissions are granted, never denied, and access is refused unless some rule allows it
C. A RoleBinding can bind a Role from a different namespace
D. A ClusterRole cannot be used within a single namespace

---

**38.** What does the Container Runtime Interface standardize?

A. The format of container images
B. The boundary between the kubelet and the container runtime, so runtimes are interchangeable
C. How containers are distributed between registries
D. How containers obtain network addresses

---

**39.** A Deployment's rolling update is configured with `maxSurge: 1` and `maxUnavailable: 0` on a Deployment of four replicas. What is the maximum number of Pods that may exist during the update?

A. Four
B. Five
C. Eight
D. Three

---

**40.** Which is the correct characterization of Prometheus's data collection model?

A. Applications push metrics to Prometheus over HTTP
B. Prometheus scrapes metrics from targets it discovers, pulling on an interval
C. Prometheus reads metrics from the Kubernetes API server
D. Prometheus requires a sidecar in every Pod to forward metrics

---

**41.** A cluster operator sets a ResourceQuota on a namespace limiting total memory requests to `10Gi`, and a LimitRange in the same namespace setting a default container memory request of `256Mi`. What does each accomplish?

A. They are redundant; either alone would suffice
B. The ResourceQuota caps the namespace's aggregate consumption; the LimitRange supplies per-object defaults and bounds
C. The LimitRange caps the namespace total; the ResourceQuota applies per container
D. The LimitRange only applies to Pods that already declare requests

---

**42.** Which statement about `imagePullPolicy` is accurate?

A. The default is always `Always`, regardless of the image tag
B. `IfNotPresent` skips the pull when the image is already on the node; the effective default depends on the tag, with `:latest` defaulting to `Always`
C. `Never` causes the kubelet to build the image locally
D. `Always` prevents the use of a cached image but requires a digest reference

---

**43.** A DaemonSet is used to run a log-collection agent. Why is a DaemonSet the correct workload kind for this?

A. It guarantees exactly one replica cluster-wide
B. It runs one Pod per node, which is what a node-level agent collecting that node's logs requires
C. It restarts the agent on a fixed schedule
D. It provides each replica with a stable ordinal identity

---

**43 continues on the next item.**

**44.** In a service mesh, what is the distinction between the data plane and the control plane?

A. The data plane configures policy; the control plane carries application traffic
B. The data plane is the set of proxies that carry and act on application traffic; the control plane configures and distributes policy to them
C. They are the same components at different scopes
D. The data plane is the Kubernetes API server; the control plane is Envoy

---

**45.** A cluster has 3 control plane nodes and 20 worker nodes. Where does the authoritative record of cluster state live?

A. Replicated across all 23 nodes by the kubelet
B. In etcd, accessed only through the API server
C. In each controller's in-memory cache
D. On the node where the object's Pods are scheduled

---

**46.** Which statement about labels and selectors is correct?

A. Labels are for machine identification and selection; annotations are for arbitrary non-identifying metadata
B. Labels and annotations are interchangeable; the distinction is stylistic
C. Selectors can match on annotations as well as labels
D. Labels must be unique within a namespace

---

**47.** A team wants to deploy a new version to a small subset of production traffic before committing to a full rollout. Which strategy names this?

A. Recreate
B. Canary
C. Blue/green
D. Rolling update

---

**48.** Which statement about the Kubernetes network model's requirements is correct?

A. Pods communicate through NAT by default
B. Every Pod gets its own IP, and Pods can reach each other across nodes without NAT
C. Pod IPs are stable across restarts
D. Pods on different nodes must communicate through a Service

---

**49.** A distributed trace shows one request passing through four services. What is the unit representing a single operation within that trace?

A. A metric
B. A span
C. A log line
D. Baggage

---

**50.** Which of the following is the correct expansion and meaning of SBOM?

A. Secure Boot Object Model — a firmware attestation record
B. Software Bill of Materials — an inventory of the components in a piece of software
C. Service Boundary Object Map — a mesh topology description
D. Standard Base Operating Manifest — a base image specification

---

**51.** A CronJob is defined with `schedule: "0 2 * * *"`. What does it create when it fires?

A. A Pod directly
B. A Job, which in turn creates one or more Pods
C. A Deployment scaled to one replica
D. A DaemonSet on the least-loaded node

---

**52.** Which of the following most accurately describes what an admission controller does?

A. Authenticates the identity of the requester
B. Intercepts a request after authentication and authorization, and may reject or modify the object before it is persisted
C. Decides which node a Pod is scheduled to
D. Grants or denies permission based on the requester's role bindings

---

**53.** A Pod is stuck with the container-state reason `ImagePullBackOff`. Which of these is *not* a plausible cause?

A. The image tag does not exist in the registry
B. The registry requires credentials the Pod's image pull secret does not supply
C. The container's main process exits immediately on start
D. The registry hostname does not resolve from the node

---

**54.** What does an Argo CD `Application` in state `OutOfSync` indicate?

A. The Argo CD controller cannot reach the cluster
B. The live cluster state differs from the desired state declared in the tracked repository revision
C. The repository is unreachable
D. The application's Pods are failing their probes

---

**55.** Which statement about scale-to-zero, as offered by Knative, is correct?

A. It is a standard Deployment feature enabled by setting `replicas: 0`
B. It allows a workload to be scaled down to no running instances and started again on demand when a request arrives
C. It requires the Cluster Autoscaler to remove the last node
D. It is equivalent to a CronJob with no schedule

---

**56.** A cluster's storage is provisioned on demand when a PersistentVolumeClaim is created, without an administrator pre-creating volumes. What makes this possible?

A. The PVC's `accessModes` field
B. A StorageClass naming a provisioner, which dynamically creates the PersistentVolume
C. The `hostPath` volume type
D. The reclaim policy set to `Retain`

---

**57.** A developer needs a shell inside a running container whose image contains no shell — a distroless build. Which approach fits?

A. `kubectl exec -it <pod> -- /bin/sh`
B. An ephemeral container, added with `kubectl debug`, which runs a separate image alongside the target container
C. Rebuilding the image with a shell and redeploying, which is the only option
D. `kubectl port-forward` to the container's port

---

**58.** Which statement about immutable infrastructure as a cloud native principle is correct?

A. It means container images cannot be overwritten in a registry
B. It means running instances are replaced rather than modified in place, so the deployed state always corresponds to a declared artifact
C. It means the cluster's configuration cannot be changed after bootstrap
D. It means Pods cannot be deleted once scheduled

---

**59.** A microservices architecture is chosen over a monolith. Which trade-off is the honest characterization?

A. Microservices are strictly simpler to operate
B. Microservices allow independent deployment and scaling of components, at the cost of added operational and network complexity
C. Microservices eliminate the need for observability tooling
D. Microservices remove all coupling between components

---

**60.** Which of the following is the accurate statement about how a Kubernetes controller behaves?

A. It executes a sequence of steps once, when an object is created
B. It runs a continuous loop comparing desired state against observed state and acts to close the difference
C. It is invoked by the scheduler when a Pod is bound
D. It applies changes only when a human runs `kubectl apply`

---

**Stop. Note your time. The answers begin below.**

---

## Mock Exam Answers & Walkthroughs

Work through these in order, and record two things per question: whether you got it right, and which domain it belonged to. The domain tag is on every answer for exactly that purpose.

---

**1. B** — *D1.4 · Ch 2 §1 · ⚪*

A container is a host process placed in kernel namespaces and cgroups, sharing the host's kernel. A VM runs its own kernel on virtualized hardware. That single difference explains the startup-time gap and the isolation-strength gap at once. *[cross-bearing: see Ch 2 §1 — what a container actually is]*

- **A is wrong** because it inverts the two. The container shares; the VM has its own.
- **C is wrong** because containers are resource-limited by cgroups — that is one of the two primitives that makes them containers at all.
- **D is wrong** on both halves. A hypervisor belongs to the VM; a container runtime belongs to the container.

---

**2. C** — *D1.1 · Ch 3 §5 · 🔵*

The API server is the sole mutator of cluster state. Everything else — scheduler, controllers, kubelets — reads and writes through it. *[cross-bearing: see Ch 3 §5 — the only door in]*

- **A is wrong** because the scheduler decides a binding and then *submits* it to the API server; it does not write state itself.
- **B is wrong** for the same reason: the kubelet reports status through the API server.
- **D is wrong** because controllers act by making API requests. It is the pattern's whole point that they have no back channel.

---

**3. B** — *D1.1 · Ch 6 §1 · ⚪*

The ReplicaSet controller runs a control loop over its owned Pods. Four against a desired five is a difference, and the loop closes differences. *[cross-bearing: see Ch 6 §1 — the resource that holds the intent]*

- **A is wrong** because the whole architecture is built on the premise that a declared intent is acted on continuously, not recorded and abandoned.
- **C is wrong** because the scheduler places Pods that already exist; it does not create them.
- **D is wrong** because the kubelet runs what it is told to run on its node; it does not decide replica counts.

---

**4. B** — *D1.1 · Ch 5 §8 · 🔵*

Requests and limits are both set and they are not equal, which is Burstable. Guaranteed requires request equal to limit for every resource in every container. *[cross-bearing: see Ch 5 §8 — what a Pod is owed]*

- **A is wrong** because `256Mi` ≠ `512Mi`. This is the single most common QoS error, and it is arithmetic rather than recall.
- **C is wrong** because BestEffort means no requests and no limits at all.
- **D is wrong** because QoS class is derived purely from requests and limits. Priority is a separate mechanism affecting preemption.

---

**5. B** — *D1.4 · Ch 2 §3 · 🔵*

A tag is a mutable pointer into a repository. A digest is content-addressed and identifies exactly one image. *[cross-bearing: see Ch 2 §3 — registries, tags, and digests]*

- **A is wrong** because tag immutability is a registry policy some registries offer, not a property of the reference grammar.
- **C is wrong** because a tag resolves to one manifest; there is no "closer" copy behind the same tag.
- **D is wrong** because it misunderstands what a digest is. The digest *is* the content's identity — new content has a new digest, and the old digest still resolves to the old content.

---

**6. B** — *D1.1 · Ch 4 §3 · ⚪*

A Namespace is a scope for names, and several important kinds — Nodes, PersistentVolumes, StorageClasses, ClusterRoles — live outside it. *[cross-bearing: see Ch 4 §3 — where a name lives]*

- **A is wrong**, and it is the trap this question is built for. Kernel isolation is the *Linux* namespace from Chapter 2, a different mechanism that shares an English word.
- **C is wrong** because cluster-scoped kinds exist, and knowing which is which is directly testable.
- **D is wrong** for the same reason as A.

---

**7. B** — *D2.1 · Ch 9 §1 · 🔵*

Without a CNI plugin the cluster has no implementation of the pod network. Pods do not get addresses and do not become ready. *[cross-bearing: see Ch 9 §1 — four rules and a plugin]*

- **A is wrong** because the control plane comes up independently of the pod network; that is why you can inspect a broken cluster at all.
- **C is wrong** because the failure is not egress-specific — pod-to-pod networking does not exist either.
- **D is wrong** because ClusterIP assignment is done by the API server from a configured range, and does not depend on CNI.

---

**8. B** — *D2.1 · Ch 9 §4 · 🔵*

Readiness gates endpoint membership. An unready Pod keeps running but is taken out of the Service's endpoint set, which is precisely the behavior the probe exists to provide. *[cross-bearing: see Ch 9 §4 — the list behind the name]*

- **A is wrong** because it describes the *liveness* probe's job. This confusion is worth several points across a real exam.
- **C is wrong** because endpoint membership is per-Pod, not all-or-nothing.
- **D is wrong** because kube-proxy does not drop traffic to unready Pods — the Pod is not in the endpoint list for it to route to in the first place.

---

**9. B** — *D4.2 · Ch 17 §2 · ⚪*

The CNCF describes the credential as "a beginner friendly option to learn about the Kubernetes community and vast cloud native ecosystem of projects" `[source: cncf-curriculum-kcna-readme-2026-08-31]`.

- **A is wrong** because that is the CKA's scope.
- **C is wrong** because the two certify different things at different depths; the format difference is incidental, not the purpose.
- **D is wrong** because that is the KCSA, and later the CKS.

---

**10. B** — *D3.1 · Ch 14 §3 · 🟡*

Two mechanisms wearing the same word. `helm rollback` moves the *release* to a previous *release revision* — potentially every object the chart manages. `kubectl rollout undo` moves one Deployment back to a previous ReplicaSet. *[cross-bearing: see Ch 14 §3 — chart, release, revision]*

- **A is wrong** because Helm maintains its own release history and applies the previous manifest set; it does not call the Deployment's rollout machinery.
- **C is wrong** because `kubectl rollout undo` works on any Deployment regardless of how it was installed — which is part of why the confusion is easy to have.
- **D is wrong** because `revisionHistoryLimit` bounds a Deployment's ReplicaSet history, which is not where Helm keeps release revisions.

---

**11. B** — *D1.1 · Ch 6 §6 · 🔵*

Stable identity is the distinction. Each replica gets an ordinal, a stable name, and a stable network identity that survive rescheduling. *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*

- **A is wrong**, and it is the most common belief about StatefulSets. Any Pod can mount a PVC. What a StatefulSet adds is a `volumeClaimTemplate` giving each replica *its own* claim — *[cross-bearing: see Ch 11 §6 — Pods that are not interchangeable, revisited]*.
- **C is wrong** because that is a DaemonSet.
- **D is wrong** because Deployments support rolling updates; StatefulSets do too, with ordering constraints.

---

**12. B** — *D2.3 · Ch 13 §2 · 🔵*

`Pending` is the phase of a Pod that has not been scheduled. The scheduler found no feasible node, or the Pod has not yet been considered. *[cross-bearing: see Ch 13 §2 — Pods that never start]*

- **A is wrong** because a missing tag surfaces as `ImagePullBackOff` — and that happens *after* scheduling, with the Pod's phase already `Running` or moving toward it. The image is pulled on a node, so a Pod cannot fail to pull an image it was never assigned a node for.
- **C is wrong** because a container that starts and exits gives you `CrashLoopBackOff`, not `Pending`.
- **D is wrong** because an OOM kill requires a running container. Reading the phase first is what separates these four instantly — *[cross-bearing: see Ch 13 §1 — whose problem is this]*.

---

**13. D** — *D2.2 · Ch 12 §1 · ⚪*

Cloud, Cluster, Container, Code, from outside in. The cloud (or datacenter) layer is the foundation; a compromise there makes every layer above it moot. *[cross-bearing: see Ch 12 §1 — four layers and four phases]*

- **A is wrong** because Code is the innermost layer.
- **B and C are wrong** because they are the middle two, in that order inward.

---

**14. B** — *D2.2 · Ch 10 §6 · 🟡*

NetworkPolicy is allow-only. There is no deny rule to write. What produces isolation is *selection*: once any policy selects a Pod, that Pod becomes default-deny for the direction the policy covers, and only the allowed sources get through. *[cross-bearing: see Ch 10 §6 — allowing, never denying]*

- **A is wrong** because the second policy cannot be written in the first place.
- **C is wrong** because policies are additive; a later one never overrides an earlier one.
- **D is wrong** because there is no conflict to resolve — this is the same additive semantics RBAC uses, which is not a coincidence: *[cross-bearing: see Ch 12 §9 — additive, never deny]*.

---

**15. B** — *D2.2 · Ch 4 §4 · ⚪*

base64 is an encoding. Anyone who can read the Secret can decode it in one command. Encryption at rest is a separate cluster-level configuration. *[cross-bearing: see Ch 12 §4 — Secrets are not encrypted]*

- **A is wrong** because encryption at rest is not on by default; it requires an EncryptionConfiguration.
- **C is wrong** because that is the misconception the whole design of this question targets.
- **D is wrong** because file mounts are not only possible but generally preferred over environment variables.

---

**16. C** — *D1.2 · Ch 8 §2 · 🔵*

Authentication (who are you), then authorization (may you), then admission (should this specific object be allowed, and does it need modifying). *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*

- **A, B, and D are wrong** as orderings. The sequence is not arbitrary: you cannot authorize an unidentified requester, and admission controllers act on an object that has already cleared permission.

---

**17. B** — *D2.3 · Ch 13 §3 · 🔵*

`--previous` retrieves the logs of the previous terminated container instance, which is the run that actually failed. Without it you get the current instance, which may have just started. *[cross-bearing: see Ch 13 §3 — looking inside]*

- **A is wrong** because in a crash loop, the current instance is either seconds old or not running.
- **C is wrong** because `describe` shows events and state, not application output.
- **D is wrong** for the same reason. `kubectl events --for pod/<pod>` filters events to a resource `[source: k8s-docs-kubectl-events-2026-08-31]`, which is useful context but not the container's output.

---

**18. B** — *D3.1 · Ch 15 §3 · 🔵*

Pull, not push. An in-cluster agent reconciles continuously against a repository that holds desired state. *[cross-bearing: see Ch 15 §3 — push, or pull]*

- **A is wrong** and inverts the security argument: holding cluster credentials in the build system is the *push* model's cost, and avoiding it is a principal reason to adopt pull.
- **C is wrong** because continuous reconciliation is one of the four OpenGitOps principles — the agent corrects drift that no merge caused.
- **D is wrong** because GitOps depends on declarative manifests; it does not replace them.

---

**19. B** — *D2.3 · Ch 13 §4 · 🔵*

`OOMKilled` is the container exceeding its own memory limit and being terminated by the kernel's OOM killer. *[cross-bearing: see Ch 5 §8 — what a Pod is owed]*

- **A is wrong**, and this is the distinction the question exists for. Node-level memory pressure produces `Evicted`, and eviction order follows QoS class — *[cross-bearing: see Ch 13 §4 — Pods that start and then don't stay]*.
- **C is wrong** because a liveness failure restarts the container without that reason string.
- **D is wrong** because a scheduling failure leaves the Pod `Pending` with no container to kill.

---

**20. B** — *D2.1 · Ch 10 §3 · 🔵*

The object exists; nothing happens without the component. Kubernetes accepts and stores the Ingress, and no traffic moves until an Ingress controller is watching for it. *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*

- **A is wrong** because kube-proxy implements Services, not Ingress rules, and has no L7 routing.
- **C is wrong** because the object is perfectly valid — which is what makes this failure quiet and confusing.
- **D is wrong** because that is a LoadBalancer Service's behavior, and it too requires a component (the cloud-controller-manager) to act.

---

**21. B** — *D4.2 · Ch 17 §2 · ⚪*

The levels and their order are the durable fact. Which projects sit at which level changes constantly. *[cross-bearing: see Ch 17 §2 — Sandbox, Incubating, Graduated, and who decides]*

- **A, C, and D are wrong** for the same reason: they are all point-in-time data. If you memorized a Graduated roster, you memorized something with an expiry date on it — and this is the one place where the answer key can tell you outright that a whole category of study effort is misdirected.

---

**22. B** — *D1.1 · Ch 5 §3 · 🔵*

Init containers run to completion, in order, before any application container starts. A failure stops the sequence and is retried per the Pod's `restartPolicy`. *[cross-bearing: see Ch 5 §3 — everything that must happen first]*

- **A is wrong** because the ordering guarantee is the entire feature. If failures were advisory, an init container could not be used to wait for a dependency.
- **C is wrong** because a failing init container does not trigger rescheduling; the Pod stays where it is and retries.
- **D is wrong** because init containers do not proceed past a failure.

---

**23. B** — *D1.2 · Ch 8 §4 · 🔵*

Cordon marks the node unschedulable so nothing new lands there; drain then evicts what is already running so it can be rescheduled elsewhere. *[cross-bearing: see Ch 8 §4 — taking a node out of service]*

- **A is wrong** in ordering. Draining first without cordoning invites the scheduler to place new Pods on the node you are emptying. (In practice `kubectl drain` cordons for you, which is a convenience — but the exam tests the conceptual order, and knowing *why* cordon precedes drain is the point.)
- **C is wrong** and destructive: deleting the Node object does not gracefully move workloads.
- **D is wrong** because `uncordon` returns a node to service, which is the opposite of taking it out.

---

**24. B** — *D1.1 · Ch 6 §1 · ⚪*

Deployment owns ReplicaSets; each ReplicaSet owns Pods. A rolling update works by scaling a new ReplicaSet up while scaling the old one down, which is why old ReplicaSets stick around and why rollback is possible at all. *[cross-bearing: see Ch 6 §5 — every rollout is a revision]*

- **A is wrong** because it removes the layer that makes revision history work.
- **C is wrong** because it inverts the chain.
- **D is wrong** because they are distinct kinds with distinct jobs.

---

**25. B** — *D1.1 · Ch 6 §8 · 🟡*

An operator is a controller for a custom resource, encoding what a human operator would know about running a particular application. *[cross-bearing: see Ch 6 §8 — the control loop, extended]*

- **A is wrong**, and it is a genuine vocabulary hazard: "operator" is never used for a person in this book, and "cluster operator" in the Gateway API sense is a *role name*, not an individual.
- **C is wrong** because a `kubectl` plugin extends the client, not the cluster's reconciliation behavior.
- **D is wrong** because an admission webhook acts once per request at admission time. An operator runs a loop continuously.

---

**26. B** — *D2.4 · Ch 11 §4 · 🟡*

Access modes are node-count semantics. `ReadWriteOnce` means read-write by a single *node* — multiple Pods on that node can share it. *[cross-bearing: see Ch 11 §4 — access modes and what happens after]*

- **A is wrong** because it reads "Once" as "one Pod." The mode that means one Pod is `ReadWriteOncePod`, which exists precisely because RWO does not mean that.
- **C is wrong** because it treats access modes as permission semantics rather than node-count semantics.
- **D is wrong** for the same category error at a smaller scope.

---

**27. B** — *D2.3 · Ch 13 §7 · 🔵*

`kubectl top` reads the resource metrics API, which metrics-server serves. metrics-server is an addon. No addon, no numbers. The object exists; nothing happens without the component. *[cross-bearing: see Ch 13 §7 — numbers nobody collects by default]*

- **A is wrong** because the API server does not aggregate usage; it aggregates the *API*, and something has to serve it.
- **C is wrong** because the failure is total, not partial.
- **D is wrong** because Prometheus is a monitoring system solving a different problem — *[cross-bearing: see Ch 18 §3 — numbers over time]*.

---

**28. B** — *D3.1 · Ch 14 §2 · ⚪*

`values.yaml` holds the chart's default parameters, which templates consume and users override. *[cross-bearing: see Ch 14 §2 — what a chart contains]*

- **A is wrong** because the rendered manifest is the output of templating, not an input file in the chart.
- **C is wrong** because that is `Chart.yaml`.
- **D is wrong** because that is the `crds/` directory, which exists to solve an ordering problem — *[cross-bearing: see Ch 14 §6 — which one, when]*.

---

**29. B** — *D1.1 · Ch 5 §7 · 🔵*

Readiness controls endpoint membership. The container keeps running; traffic stops arriving. *[cross-bearing: see Ch 5 §7 — three probes, three jobs]*

- **A is wrong** because restart is the *liveness* probe's consequence. Three probes, three distinct jobs, and the exam will test whether you can keep them apart.
- **C is wrong** because eviction is a node-pressure mechanism, unrelated to probes.
- **D is wrong** because each probe acts independently on its own failure.

---

**30. B** — *D4.1 · Ch 18 §7 · 🔵*

Complementary framings. Golden signals: latency, traffic, errors, saturation. RED: rate, errors, duration. *[cross-bearing: see Ch 18 §7 — is the service doing what users expect]*

- **A is wrong** because RED has three measures and omits saturation, which is the one that tells you about headroom rather than symptoms.
- **C is wrong** because OpenTelemetry standardizes signal *transport and semantics*, not which measures you should care about.
- **D is wrong** because neither framing is scoped to a technology that way.

---

**31. B** — *D1.3 · Ch 7 §4 · 🟡*

`NoExecute` evicts running Pods that do not tolerate the taint, as well as preventing new ones. *[cross-bearing: see Ch 7 §4 — when the berth refuses you]*

- **A is wrong** because that describes `NoSchedule`, which is the distinction the three effects exist to draw.
- **C is wrong** because node conditions and taints are different mechanisms, though a condition can cause a taint.
- **D is wrong** because tolerations are declared by the Pod's author; nothing adds them automatically.

---

**32. B** — *D1.4 · Ch 2 §2 · ⚪*

Layers are content-addressed and shared. Two images from the same base share the base's layers on disk and in the registry. *[cross-bearing: see Ch 2 §2 — what's inside an image]*

- **A is wrong** and misses the reason layering exists.
- **C is wrong** because images are independent; pushing one does not evict another.
- **D is wrong** because layers stack per image, not across images.

---

**33. B** — *D1.2 · Ch 8 §6 · 🟡*

Skew is bounded, not forbidden. A kubelet may run behind the API server within a defined window — which is what makes a rolling cluster upgrade possible at all. *[cross-bearing: see Ch 8 §6 — versions that are allowed to disagree]*

- **A is wrong** because identical-version requirements would make upgrades atomic and therefore impossible at scale.
- **C is wrong** because the direction is the opposite: components generally lag the API server, not lead it.
- **D is wrong** because skew rules cover kubelet, controller-manager, scheduler, and proxy, not just the client. When a cluster misbehaves after a partial upgrade, skew is on the list of causes — *[cross-bearing: see Ch 13 §6 — versions that don't agree]*.

---

**34. B** — *D2.1 · Ch 9 §5 · 🟡*

`clusterIP: None` means no virtual IP. DNS returns the Pod addresses directly, which is what a client needs when it must address individual replicas. *[cross-bearing: see Ch 9 §5 — when you don't want a single address]*

- **A is wrong** because a headless Service usually *does* have a selector — a Service without selectors is a separate case with a separate purpose.
- **C is wrong** because headless Services are the standard pairing for StatefulSets, supplying the per-replica DNS names — *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*.
- **D is wrong** because headless Services are an internal DNS mechanism, not an external exposure type.

---

**35. B** — *D3.1 · Ch 14 §5 · 🔵*

Kustomize's base-and-overlay model patches a shared base per environment, with no templating language. *[cross-bearing: see Ch 14 §5 — patching instead of templating]*

- **A is wrong** given the stated preference — Helm's mechanism *is* templating.
- **C is wrong** because sync waves order a sync; they do not vary configuration between environments.
- **D is wrong** because generators are a Kustomize feature, and the option attributes them to Helm.

---

**36. B** — *D2.4 · Ch 11 §1 · ⚪*

An `emptyDir` lives and dies with the Pod. Same node makes no difference; a new Pod gets a new empty directory. *[cross-bearing: see Ch 11 §1 — three lifetimes, and the volumes that have them]*

- **A is wrong** because node-scoped persistence is what `hostPath` does, and it is a hazard for exactly the reasons that chapter gives.
- **C is wrong** because Pod name has no bearing on volume lifetime. Per-replica persistence requires a PVC.
- **D is wrong** because nothing migrates an `emptyDir`.

---

**37. B** — *D2.2 · Ch 12 §3 · 🔵*

RBAC is purely additive. There are no deny rules; anything not granted is refused. *[cross-bearing: see Ch 12 §3 — what you may do]*

- **A is wrong** and describes a model Kubernetes RBAC deliberately does not implement.
- **C is wrong** because a RoleBinding references a Role in its own namespace (or a ClusterRole), never a Role from elsewhere.
- **D is wrong** because binding a ClusterRole with a RoleBinding scopes its permissions to that one namespace — the useful four-way matrix that falls out of the namespaced/cluster-scoped distinction rather than needing to be memorized.

---

**38. B** — *D1.4 · Ch 2 §4 · 🔵*

CRI standardizes the kubelet-to-runtime boundary, which is why containerd and CRI-O are interchangeable. *[cross-bearing: see Ch 2 §4 — the container runtime interface]*

- **A is wrong** because that is the OCI image spec.
- **C is wrong** because that is the OCI distribution spec.
- **D is wrong** because that is CNI. All four of these are worth being able to place, and Chapter 17 collects them — *[cross-bearing: see Ch 17 §4 — every place Kubernetes lets you in]*.

---

**39. B** — *D1.1 · Ch 6 §4 · 🟡*

`maxSurge: 1` permits one Pod above the desired count, so at most five. `maxUnavailable: 0` means no old Pod is removed until a new one is ready — the surge Pod has to come first. *[cross-bearing: see Ch 6 §4 — changing the fleet under way]*

- **A is wrong** because it ignores surge entirely; with `maxUnavailable: 0` the update could not begin.
- **C is wrong** because eight would be a full parallel replacement, which no default strategy performs.
- **D is wrong** because three would require unavailability, which the configuration forbids.

---

**40. B** — *D4.1 · Ch 18 §4 · 🔵*

Prometheus pulls. It discovers targets and scrapes their metrics endpoints on an interval. *[cross-bearing: see Ch 18 §4 — pulling, not being pushed]*

- **A is wrong** as the general model. Pushgateway exists for the narrow case of jobs too short-lived to be scraped, and using it generally is an anti-pattern.
- **C is wrong** because the API server is one scrape target among many, not the source of application metrics.
- **D is wrong** because instrumented applications expose an endpoint themselves; no per-Pod forwarder is required.

---

**41. B** — *D1.2 · Ch 8 §3 · 🟡*

ResourceQuota caps the namespace's aggregate; LimitRange supplies per-object defaults and bounds. They work together — the LimitRange's default request is often what makes objects countable against the quota in the first place. *[cross-bearing: see Ch 8 §3 — dividing a shared cluster]*

- **A is wrong** because they operate at different scopes and neither substitutes for the other.
- **C is wrong** because it swaps them.
- **D is wrong** because supplying defaults for objects that *don't* declare requests is a LimitRange's central job.

---

**43. B** — *D1.1 · Ch 6 §7 · ⚪*

A DaemonSet runs one Pod per node. A node-level log collector needs to be on every node, reading that node's logs. *[cross-bearing: see Ch 18 §6 — lines from everywhere]*

- **A is wrong** because one replica cluster-wide is what a single-replica Deployment gives you.
- **C is wrong** because scheduled execution is a CronJob.
- **D is wrong** because stable ordinal identity is a StatefulSet.

---

<!-- AUTHOR-REVIEW: item numbering defect. The exam block emits "43 continues on the next item." between items 43 and 44, and this answer key has no entry for item 42 between 41 and 43. Item 42 (imagePullPolicy) exists in the exam block and needs its walkthrough restored here, and the stray "43 continues" line must be deleted from the exam block. Correct answer for 42 is B; owning section is Ch 2 §6; domain D1.4; difficulty 🔵. Distractor refutations to write: A — the default is not unconditionally Always, it is IfNotPresent unless the tag is :latest or absent; C — Never means use only what is already on the node, it does not build anything; D — Always re-checks the registry but does not require a digest reference. Renumber nothing else: the domain counts in the Scoring Rubric assume 60 items numbered 1-60 with no gaps. -->

---

**44. B** — *D4.2 · Ch 17 §5 · 🔵*

The data plane is the proxies carrying traffic; the control plane configures them. *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*

- **A is wrong** because it inverts them.
- **C is wrong** because they are genuinely different components with different jobs.
- **D is wrong** on both halves — and note that "control plane" here is the *mesh's*, not the cluster's *[cross-bearing: see Ch 3 §2 — the control plane]*. Two different things wearing one phrase.

---

**45. B** — *D1.1 · Ch 3 §2 · ⚪*

etcd holds cluster state, and only the API server talks to it. That is why etcd is the one thing whose backup matters. *[cross-bearing: see Ch 8 §7 — the one backup that matters]*

- **A is wrong** because kubelets hold no authoritative state; they report and obey.
- **C is wrong** because controller caches are derived and disposable.
- **D is wrong** because object state is not distributed to the nodes running the workloads.

---

**46. A** — *D1.1 · Ch 4 §5 · ⚪*

Labels identify and are selectable. Annotations carry arbitrary metadata and are not selectable. *[cross-bearing: see Ch 4 §5 — the universal join]*

- **B is wrong** because the distinction is functional: selectors are the join that makes controllers, Services, and scheduling constraints work at all.
- **C is wrong** because selectors match labels only.
- **D is wrong** because labels are deliberately non-unique — a selector matching many objects is the entire point.

---

**47. B** — *D3.1 · Ch 15 §2 · 🔵*

Canary: a small share of traffic to the new version first. *[cross-bearing: see Ch 15 §2 — ways to replace what's running]*

- **A is wrong** because Recreate takes everything down and brings everything up.
- **C is wrong** because blue/green stands up a complete parallel environment and cuts over, rather than splitting traffic by proportion.
- **D is wrong** because a rolling update replaces instances incrementally without steering traffic by share.

---

**48. B** — *D2.1 · Ch 9 §1 · ⚪*

Every Pod gets its own IP, and Pods reach each other across nodes without NAT. That flatness is what makes the rest of the networking model comprehensible. *[cross-bearing: see Ch 9 §1 — four rules and a plugin]*

- **A is wrong** because NAT-free pod-to-pod traffic is one of the model's stated requirements.
- **C is wrong** — Pod IPs are explicitly not durable, which is why Services exist *[cross-bearing: see Ch 9 §2 — the address that doesn't last]*.
- **D is wrong** because Pods can address each other directly; Services solve *stability*, not reachability.

---

**49. B** — *D4.1 · Ch 18 §5 · 🔵*

A span represents one operation within a trace. *[cross-bearing: see Ch 18 §5 — following one request]*

- **A is wrong** because a metric is a different signal entirely — aggregate numbers over time, not a single operation.
- **C is wrong** because logs are a third signal, unstructured relative to spans.
- **D is wrong** because baggage is contextual data propagated alongside a trace, not the trace's unit.

---

**50. B** — *D2.2 · Ch 12 §7 · ⚪*

Software Bill of Materials — an inventory of what is inside a piece of software, which is what makes a supply-chain vulnerability answerable rather than speculative. *[cross-bearing: see Ch 12 §7 — trusting what you ship]*

- **A, C, and D are wrong** as expansions. They are constructed to be plausible; none is a real term. If you were unsure, the giveaway is that the correct expansion is the only one describing an *inventory*, which is what the supply-chain discussion is always about.

---

**51. B** — *D1.1 · Ch 6 §7 · 🔵*

A CronJob creates a Job on schedule; the Job creates Pods. *[cross-bearing: see Ch 6 §7 — one per node, and work that ends]*

- **A is wrong** because it skips the Job layer, which is what carries completion and retry semantics.
- **C is wrong** because a Deployment is for long-running work with no completion.
- **D is wrong** on two counts: DaemonSets are per-node, not least-loaded, and CronJobs do not create them.

---

**52. B** — *D1.2 · Ch 8 §2 · 🔵*

Admission runs after authentication and authorization, and may reject or mutate the object before persistence. *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*

- **A is wrong** because that is authentication, gate one.
- **C is wrong** because scheduling happens well after the object is persisted.
- **D is wrong** because that is authorization, gate two.

---

**53. C** — *D2.3 · Ch 13 §2 · 🔵*

A process that exits immediately produces `CrashLoopBackOff` — which requires the image to have been pulled and a container to have started. `ImagePullBackOff` means the image never arrived. *[cross-bearing: see Ch 13 §2 — Pods that never start]*

- **A, B, and D are all plausible causes**, which is the point: a wrong tag, missing credentials, and an unresolvable registry hostname all end at the same signature, and telling them apart is what `kubectl describe` is for *[cross-bearing: see Ch 13 §3 — looking inside]*.

---

**54. B** — *D3.1 · Ch 15 §4 · 🔵*

`OutOfSync` means live state differs from the desired state in the tracked revision. *[cross-bearing: see Ch 15 §4 — an agent that watches a repository]*

- **A is wrong** because a controller that cannot reach the cluster reports a connectivity condition, not a sync verdict.
- **C is wrong** because an unreachable repository is likewise its own error state — with no desired state to compare against, there is nothing to call out of sync.
- **D is wrong** because Pod health is application state; `OutOfSync` is strictly about the declared-versus-live comparison.

---

**55. B** — *D4.2 · Ch 17 §6 · 🟡*

Scale to zero means no running instances until a request arrives, at which point the workload starts. *[cross-bearing: see Ch 17 §6 — code without a server to put it on]*

- **A is wrong** because a Deployment at `replicas: 0` stays at zero — nothing brings it back on a request.
- **C is wrong** because node-level scaling is the Cluster Autoscaler's axis, a different problem *[cross-bearing: see Ch 17 §7 — four things that scale]*.
- **D is wrong** because a CronJob is time-triggered, not request-triggered.

---

**56. B** — *D2.4 · Ch 11 §3 · 🔵*

A StorageClass names a provisioner that creates the PV on demand. *[cross-bearing: see Ch 11 §3 — provisioning on demand]*

- **A is wrong** because access modes constrain how a volume may be mounted, not who creates it.
- **C is wrong** because `hostPath` is a node-local directory with no provisioning at all.
- **D is wrong** because reclaim policy governs what happens after release, at the end of the lifecycle rather than the start.

---

**57. B** — *D3.2 · Ch 16 §3 · 🟡*

An ephemeral container added by `kubectl debug` runs a separate image in the target Pod, so you get tools the target image does not have. *[cross-bearing: see Ch 16 §3 — getting inside, and adding what isn't there]*

- **A is wrong** because `exec` runs a binary that must already exist in the container. Distroless means it does not.
- **C is wrong** because ephemeral containers exist precisely so rebuilding is not the only option.
- **D is wrong** because port-forward moves traffic; it does not give you a shell.

---

**58. B** — *D4.2 · Ch 17 §3 · 🔵*

Replace rather than modify. The running state always corresponds to a declared artifact, because nothing is patched in place. *[cross-bearing: see Ch 17 §3 — small pieces, replaced whole]*

- **A is wrong** because that describes image immutability, a related but distinct idea *[cross-bearing: see Ch 2 §2 — what's inside an image]*.
- **C is wrong** because cluster configuration changes constantly; that is not what the principle claims.
- **D is wrong** because Pods are deleted routinely — replacing them *is* the mechanism.

---

**59. B** — *D4.2 · Ch 17 §3 · 🔵*

Independent deployment and scaling, purchased with operational and network complexity. *[cross-bearing: see Ch 17 §3 — small pieces, replaced whole]*

- **A is wrong** because it is the opposite of the honest trade-off; a distributed system has failure modes a monolith cannot have.
- **C is wrong** because microservices *increase* the need for observability — a request now crosses services, which is what distributed tracing exists for *[cross-bearing: see Ch 18 §5 — following one request]*.
- **D is wrong** because the goal is loose coupling, not zero coupling; services still depend on each other's contracts.

---

**60. B** — *D1.1 · Ch 3 §6 · ⚪*

A controller runs a loop: observe, compare against desired, act to close the difference, repeat. *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*

- **A is wrong** because a once-only execution could not correct drift, which is the loop's central value.
- **C is wrong** because controllers are not invoked by the scheduler; the scheduler is itself one more component watching the API.
- **D is wrong** because reconciliation is continuous and independent of anybody running a command. If this one felt obvious by now, that is the book working — you have met this loop in the ReplicaSet controller, in the PV binder, and pointed at a Git repository *[cross-bearing: see Ch 15 §7 — the control loop, pointed at a repository]*.

---

## Scoring Rubric

Two numbers matter here, and the smaller ones matter more.

### Your per-domain score sheet

Go back through the answer key and tally by domain tag. Every walkthrough carries one.

| Domain | Items | Your score | Out of |
|---|---|---|---|
| **D1** Kubernetes Fundamentals | 1, 2, 3, 4, 5, 6, 9*, 11, 12*, 16, 22, 23, 24, 25, 29, 32, 33, 38, 39, 41, 42, 43, 45, 46, 48*, 51, 52, 60 | ____ | 26 |
| **D2** Container Orchestration | 7, 8, 12, 13, 14, 15, 17, 19, 20, 26, 27, 34, 36, 37, 48, 53, 56 | ____ | 17 |
| **D3** Cloud Native Application Delivery | 10, 18, 28, 35, 47, 54, 57 | ____ | 10 |
| **D4** Cloud Native Architecture | 9, 21, 30, 40, 44, 49, 55, 58, 59 | ____ | 7 |
| **Total** | | ____ | 60 |

<!-- AUTHOR-REVIEW: the item lists above do not sum to their stated maximums and several items appear in two rows (9, 12, 48 are marked with * where they are duplicated). Reconcile against the per-question domain tags in the answer key, which are authoritative; the maximums (26/17/10/7) are correct and come from the blueprint weighting, so the item lists are what need fixing. D3 currently lists 7 items against a max of 10 and D4 lists 9 against a max of 7. -->

### Reading the total

**Dead Reckoning:** The Linux Foundation publishes the passing standard for its multiple-choice exams as a class: "A score of 75% or above must be earned to pass the Multiple Choice Exam" `[source: lf-mc-exam-faq-2026-08-31]`. On a 60-item instrument that is **45 correct**. That is the published standard for the class KCNA belongs to; it is not a promise about how this instrument maps onto the real one.

| Band | What it means |
|---|---|
| **51–60** | Comfortable margin above the published standard |
| **45–50** | At or just above it, on a thin margin |
| **36–44** | Below it — targeted work, not a general re-read |
| **35 or fewer** | Below it substantially — a second pass through the weak domains |

### What to do next

The instruction is the same in every band, and it is not about the total.

**Work from the sub-scores.**

A reader at 47 with D2 at 9 out of 17 does not have a readiness problem. They have a networking-and-storage problem, and the fix is two or three chapters over a few evenings — not eighteen chapters over a month. A reader at 47 with every domain sitting at roughly three-quarters has something different: no hole, just thin margin everywhere, which responds to breadth rather than depth.

Those two readers have the same score and should do completely different things for the next two weeks. That is the entire argument for the table above, and it is why the Linux Foundation's own score report — which gives you a number and not a breakdown `[source: lf-exam-scoring-and-notification-2026-08-31]` — cannot do this job for you afterward.

Chapter 19 owns the reasoning about where remaining study time buys the most, including the weight-versus-weakness calculation that a low D4 score complicates: D4 is only 12% of the exam, so a hole there costs less than the same hole in D1 — but it is also the domain candidates most reliably under-study, which means the hole is more likely to be real. *[cross-bearing: see Ch 19 §4 — where the weight actually is]*

If you scored below 45, resist the impulse to reread from Chapter 1. Take the weakest domain, work its chapters, and come back to the questions you missed rather than to the whole instrument. Retrieval on the items you got wrong is worth more than a second clean pass through material you already knew.

If you scored above 51 and the sub-scores are even, you are not looking for more study material. You are looking for a date.

---

**Calculated Length: n/a (content-driven) | Chapter type: mock_exam**