---
chapter: 20
title: "Full Mock Exam"
chapter_type: mock_exam
exam: "KCNA"
exam_version: "CNCF curriculum effective 2025-11-24"
---

<!-- AUTHOR-REVIEW: YAML frontmatter added this pass. The stage-11 structural audit on draft-v1
     reported 8 FAILs and 5 WARNs for missing Attention Budget, Soundings, Why This Chapter Matters,
     Taking Your Bearings, Exam Alert, Chapter Summary, Road Ahead, and the ☆/★/⚠/🧭 markers. Every
     one of those rules carries `exempt_chapter_types: [mock_exam]` in structural-contract.yaml, so
     the findings were an artifact of the linter having no chapter_type to read — draft-v1 shipped
     without frontmatter. Confirm structural_lint reads chapter_type from the draft's own frontmatter
     and not only from the outline in pipeline state; if it reads only the outline, this block is
     harmless but the audit will keep failing until the outline is the input. Do NOT resolve those
     findings by adding Soundings or Bearings to a scored instrument. -->

# Chapter 20: Full Mock Exam

## *"Ninety minutes. No notes. Find out."*

---

## Instructions

You have reached the last chapter, and it is the only one that does not teach you anything.

Nineteen chapters have explained. This one measures. There is no Soundings block here, no Fixed Points, no callouts in the margin: a diagnostic instrument that keeps interrupting itself with encouragement is not a diagnostic instrument. The voice comes back in the walkthroughs, after the clock stops.

**Dead Reckoning:** The Linux Foundation publishes both of the numbers this instrument is built around, in its candidate handbook, for multiple-choice exams as a class. The multiple-choice exam "consists of 60* multiple-choice questions" and candidates "have 90* minutes to complete" it `[source: lf-mc-exam-important-instructions-2026-08-31]`. The asterisks lead to a footnote naming CNPA, a different exam with 85 questions and 120 minutes. They are not a hedge about the class figures. KCNA belongs to that class: the Linux Foundation's own exam-code table puts KCNA in the multiple-choice column beside KCSA and LFCA, with CKA and CKAD in the performance-based column `[source: lf-exam-user-interface-exam-codes-2026-08-31]`. Neither number appears on the KCNA product page `[source: provenance-kcna-60-questions-2026-08-31]`. That is the provenance lesson Chapter 1 spent a section on. *[cross-bearing: see Ch 1 § Ninety Minutes: The Exam as Published]*

So: **sixty questions, ninety minutes.**

### What this instrument is, and is not

It is sized to the published count and weighted to the published blueprint: 44% Kubernetes Fundamentals, 28% Container Orchestration, 16% Cloud Native Application Delivery, 12% Cloud Native Architecture `[source: cncf-curriculum-kcna-readme-2026-08-31]`. Twenty-six questions, seventeen, ten, and seven.

It was written by Lodestar Ledgers. It is not a leaked exam, not a reconstruction of one, and not a prediction of your score. What it gives you is a fix on your own position, taken from your own answers.

One shape here is this book's construction rather than a published figure. Every item below offers four options with one correct answer. The Linux Foundation does not publish how many options its multiple-choice items carry, whether any item is multi-select, whether unscored pretest items are mixed in, or whether a wrong answer costs anything `[source: lf-examui-multiple-choice-2026-08-31]`. Four options and one right answer is a reasonable authoring choice. Do not read it as a disclosure.

### Conditions worth reproducing

One sitting. No notes, no cluster, no documentation, no search. Ninety minutes on a timer you can see.

A reader who looks things up is measuring how good this book's index is. That is a fine thing to measure, but it is not the thing you came here for.

### How the real console behaves

The Linux Foundation documents the multiple-choice exam interface in its candidate handbook. You move between items with Previous and Next; you can flag an item for later review; flagged items are highlighted on a Review Screen, and you can return to one and change your answer. When you reach the final item you are prompted to review, and the Review Screen carries the Finish Exam button. A Pause Exam function exists, and using it does not stop the timer `[source: lf-examui-multiple-choice-2026-08-31]`.

On paper you can do all of that and more. Flag, move on, come back — and finish the first pass at roughly 54 of the 90 minutes, keeping the rest for the flagged items. Chapter 19 owns the reasoning behind that split and what to do with the second pass; this chapter only asks you to run it. *[cross-bearing: see Ch 19 §3 — pacing and time discipline]*

<!-- AUTHOR-REVIEW: Ch 19 §3 currently contains a sentence the corpus lists as false —
     ch-19/draft-v2.md line 541, "The Linux Foundation does not publish how its multiple-choice exam
     console behaves." See provenance-kcna-exam-interface-2026-08-31. Chapter 20's framing above is
     the correct one and is sourced. When the two chapters are harmonised, move Ch 19 to Ch 20's
     framing, never the reverse. The B6 skeleton's Ch 20 entry has already been corrected; its Ch 19
     entry has not been checked. -->

### One thing the real exam will not give you

Your score report arrives within 24 hours, by email and on the Portal. It reports the outcome. It does not tell you which domain you were weak in: the Linux Foundation states plainly that it "does not report performance on individual items and will not honor requests for more detailed information" `[source: lf-exam-scoring-and-notification-2026-08-31]`.

That is the whole argument for the score sheet at the end of this chapter. The per-domain breakdown you are about to generate is not a convenience duplicating something the real exam hands you afterward. It is the only domain-level diagnostic available to you anywhere in this preparation, and it is available only before the exam, which is the only time it can change anything.

### The answers

They are in the block after the exam, headed **Mock Exam Answers & Walkthroughs**. Do not read ahead into it. Every question there carries the correct answer, an explanation of why the wrong options are wrong, the domain it belongs to, and a pointer back to the section that taught it.

When you are ready, start the clock.

---

## Exam

**1.** A container and a virtual machine both run an application in isolation from the host's other workloads. Which statement correctly distinguishes them?

A. A container runs its own kernel on virtualized hardware; a virtual machine shares the host's kernel with other workloads
B. A container's resource ceiling is set by a hypervisor; a virtual machine's is set by cgroups on the host
C. A container is a host process sharing the host's kernel; a virtual machine runs its own kernel on virtualized hardware
D. A container needs a hypervisor before it can start; a virtual machine needs a container runtime before it can start

---

**2.** A cluster has been bootstrapped, but no CNI plugin has been installed. What is the most likely observed symptom?

A. The API server refuses to start until a pod network has been configured
B. Pods are created but stay `Pending`, and pod networking does not function
C. Pods run normally but cannot reach any destination outside the cluster
D. Services are created, but the API server assigns none of them a ClusterIP

---

**3.** Which Kubernetes component is the only one that writes to cluster state?

A. kube-scheduler, which records each of its binding decisions directly
B. kubelet, which reports the status of its own node directly
C. kube-controller-manager, which writes the results of every reconciliation
D. kube-apiserver, which every other component reaches state through

---

**4.** In a Helm chart, what is the role of `values.yaml`?

A. It supplies the chart's default parameters, which templates consume and a user may override
B. It is the rendered manifest set that Helm submits to the cluster at install time
C. It declares the chart's name, version, and dependency list for the repository index
D. It holds the CustomResourceDefinitions the chart must install before its other objects

---

**5.** Which statement about a Kubernetes Namespace is correct?

A. It isolates the processes belonging to different namespaces from one another at the kernel level
B. It is a scope for names, and some resource kinds exist outside it entirely
C. It applies to every Kubernetes resource kind, without exception
D. Deleting one leaves the objects inside it in place, belonging to no namespace

---

**6.** In the four-layer cloud native security model, which layer is the outermost — the one whose compromise undermines every layer inside it?

A. Code
B. Container
C. Cluster
D. Cloud

---

**7.** Which is the correct characterization of Prometheus's data collection model?

A. Applications push their metrics to Prometheus over HTTP as those metrics are produced
B. Prometheus subscribes to a stream that an OpenTelemetry Collector forwards to it
C. Prometheus scrapes metrics from targets it discovers, pulling on an interval
D. Prometheus reads application metrics from the Kubernetes API server's aggregation layer

---

**8.**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: report-worker
spec:
  containers:
    - name: worker
      image: example/worker:2.1
      resources:
        requests:
          cpu: "250m"
          memory: "256Mi"
        limits:
          cpu: "500m"
          memory: "512Mi"
```

Which QoS class does the Pod above receive?

A. Burstable
B. Guaranteed
C. BestEffort
D. Guaranteed for CPU and Burstable for memory

---

**9.** A Pod that mounts an `emptyDir` volume is deleted, and its controller recreates it on the same node. What happens to the data in the volume?

A. It persists, because an `emptyDir` volume is bound to the node rather than to the Pod
B. It is lost, because an `emptyDir` volume's lifetime is the Pod's
C. It persists, provided the replacement Pod is given the same name as the original
D. It is copied into the replacement Pod by the kubelet running on that node

---

**10.** Which statement about the relationship between a Deployment, a ReplicaSet, and a Pod is correct?

A. A Deployment creates Pods directly, and the ReplicaSet records what it created
B. A ReplicaSet manages Deployments, which in turn manage the individual Pods
C. A Deployment manages ReplicaSets, each of which manages a set of Pods
D. A Deployment and a ReplicaSet are one object exposed under two API versions

---

**11.** Which statement describes GitOps as distinct from a conventional CI/CD pipeline?

A. An agent inside the cluster pulls desired state from a repository and reconciles it continuously
B. The build system holds the cluster's credentials and applies manifests when a pipeline succeeds
C. Manifests are applied at merge time only, and are never reapplied to the cluster afterward
D. Declarative manifests are replaced by imperative deployment scripts that the agent executes

---

**12.**

```yaml
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

A. The image tag does not exist in the registry that the node would pull it from
B. The container's main process started and then exited immediately on startup
C. The container was terminated by the kernel for exceeding its memory limit
D. No node passes the scheduler's filters, so the Pod has not been bound to one

---

**13.** An image is referenced as `registry.example.com/team/api:v2`. The same tag is later pushed again, pointing at different content. Which statement is true?

A. Tags are immutable under the OCI distribution spec, so the second push is rejected
B. The tag now resolves to the new content; a digest reference would still resolve to the old
C. Both manifests are retained under `:v2`, and the registry serves whichever copy is nearer
D. The original digest is updated to match the new content, so digest references follow it

---

**14.** An operator applies a NetworkPolicy that allows ingress to Pods labeled `app: db` from Pods labeled `app: api`, and then writes a second NetworkPolicy intended to deny ingress from `app: batch`. What is the effect?

A. Both are honored, and traffic from `app: batch` is explicitly blocked at the target Pods
B. The second policy replaces the first, because policies are evaluated in creation order
C. NetworkPolicy has no deny rule; selection alone makes the target default-deny for anything not allowed
D. The two policies conflict, so the API server rejects the second one at admission

---

**15.** A project has just been accepted into the CNCF at the entry level of its maturity ladder, before it has been asked to demonstrate broad production adoption. Which level is it at, and which level follows?

A. Sandbox, and the next level is Incubating
B. Incubating, and the next level is Sandbox
C. Sandbox, and the next level is Graduated
D. Incubating, and the next level is Graduated

---

**16.** Which of the following is the correct order of the three gates every request to the API server passes through?

A. Admission, then authentication, then authorization
B. Authentication, then admission, then authorization
C. Authorization, then authentication, then admission
D. Authentication, then authorization, then admission

---

**17.**

```
$ kubectl get pods -l app=web
NAME                   READY   STATUS    RESTARTS   AGE
web-6d4f8b7c9d-2xk4p   1/1     Running   0          14m
web-6d4f8b7c9d-7hqnv   1/1     Running   0          14m
web-6d4f8b7c9d-lz8mt   0/1     Running   0          14m
```

A Service of type `ClusterIP` selects Pods with the label `app: web`. How many endpoints does the Service have?

A. Three, because all three Pods are in the `Running` phase
B. Zero, because one Pod that is not ready invalidates the whole EndpointSlice
C. Two, because a Pod that is not ready is removed from the Service's endpoints
D. Three, but kube-proxy silently drops the traffic it routes to the unready Pod

---

**18.** A `helm rollback` and a `kubectl rollout undo` both move a workload backward. Which statement correctly distinguishes them?

A. They are one operation, because Helm delegates the work to the Deployment's rollout machinery
B. `helm rollback` restores a previous release revision; `kubectl rollout undo` reverts one Deployment to a previous ReplicaSet
C. `kubectl rollout undo` works only on Helm-installed workloads, while `helm rollback` works on any
D. `helm rollback` reads the Deployment's own ReplicaSet history, bounded by `revisionHistoryLimit`

---

**19.** A cluster administrator wants to take a node out of service for maintenance without losing the workloads running on it. Which sequence is correct?

A. `kubectl cordon`, then `kubectl drain`
B. `kubectl drain`, then `kubectl cordon`
C. `kubectl delete node`, then re-register the node afterward
D. `kubectl taint node ... NoExecute`, then `kubectl uncordon`

---

**20.** A container reads its database password from a file mounted from a Secret. Which statement about that Secret is accurate?

A. The value is encrypted in etcd by default, so it is protected at rest without further work
B. base64 encoding renders the value unreadable to anyone who can read etcd directly
C. Secrets can only be injected as environment variables, and cannot be mounted as files
D. The value is base64-encoded, which is encoding and not protection; encryption at rest is configured separately

---

**21.** Which statement about a StatefulSet is the reason it exists as a workload kind separate from a Deployment?

A. Only a StatefulSet is able to mount a PersistentVolumeClaim into the Pods it manages
B. Only a StatefulSet supports rolling updates, rather than replacing every replica at once
C. It gives each replica a stable ordinal identity and network name that survive rescheduling
D. It places exactly one replica on each node, which is what stateful workloads require

---

**22.** A distributed trace shows one request passing through four services. What is the unit representing a single operation within that trace?

A. A metric, which records the operation's duration as a point in a time series
B. A span, which records one operation's start, end, and position in the trace
C. A log line, emitted by the service at the boundary of the operation
D. Baggage, which carries the operation's identity from one service to the next

---

**23.** An init container in a Pod exits with a non-zero status. What happens?

A. The Pod's application containers start anyway, because init failures are advisory only
B. The Pod is deleted and rescheduled onto a different node, where the init is retried
C. The next init container in the list runs, and the failure is recorded as an event
D. No application container starts; the init container is retried per the Pod's `restartPolicy`

---

**24.**

```
$ kubectl get pod payment-7c9f4d8b6-nq2vs
NAME                      READY   STATUS             RESTARTS       AGE
payment-7c9f4d8b6-nq2vs   0/1     CrashLoopBackOff   11 (22s ago)   38m
```

Which command retrieves the output of the container run that most recently failed?

A. `kubectl logs payment-7c9f4d8b6-nq2vs --previous`
B. `kubectl logs payment-7c9f4d8b6-nq2vs`
C. `kubectl describe pod payment-7c9f4d8b6-nq2vs`
D. `kubectl events --for pod/payment-7c9f4d8b6-nq2vs`

---

**25.** A team wants to deploy a new version to a small subset of production traffic before committing to a full rollout. Which strategy names this?

A. Recreate, which stops every instance of the old version before starting the new one
B. Blue/green, which stands up a complete parallel environment and then cuts over to it
C. Canary, which sends a small share of production traffic to the new version first
D. Rolling update, which replaces the running instances one batch at a time

---

**26.**

```yaml
apiVersion: v1
kind: Node
metadata:
  name: node-07
spec:
  taints:
    - key: maintenance
      value: "true"
      effect: NoExecute
```

A Pod is already running on `node-07` and declares no tolerations. What is the consequence of the taint above?

A. Nothing, because the effect governs only scheduling decisions made after it is applied
B. The Pod is evicted from `node-07`
C. The Pod keeps running, and the node is marked `NotReady` until the taint is tolerated
D. The Pod is restarted in place, with a matching toleration added to it automatically

---

**27.** A PersistentVolumeClaim requests `ReadWriteOnce`. What does this constrain?

A. The volume may be mounted read-write by Pods on a single node
B. Exactly one Pod anywhere in the cluster may mount the volume at any time
C. The volume may be read by many Pods, but written only by the first to mount it
D. Only one container inside a given Pod may mount the volume read-write

---

**28.** In a Kubernetes object, what is the relationship between `spec` and `status`?

A. `spec` is written by the controller, and `status` is written by the user who submitted the object
B. Both are written by the user, and the API server validates that they agree before persisting
C. `status` is a copy of `spec` retained for rollback, and diverges from it only during an update
D. `spec` is the declared desired state; `status` is the observed state a controller reports

---

**29.** In a service mesh, what is the distinction between the data plane and the control plane?

A. The data plane distributes policy, and the control plane carries the application traffic
B. The data plane is the proxies carrying application traffic; the control plane configures them
C. They name the same components, described once at cluster scope and once at Pod scope
D. The data plane is the Kubernetes API server, and the control plane is the Envoy proxy

---

**30.** A container image is built `FROM` a base image and adds two layers. A second image is built from the same base and adds one different layer. What does the registry store?

A. Two complete and independent copies, one for each of the two images
B. Only the most recently pushed image; the older one is garbage collected
C. The shared base layers once, plus each image's distinct layers
D. A single merged image containing every layer from both of them

---

**31.** What does an Ingress object accomplish on a cluster where no Ingress controller is installed?

A. Nothing; the object is accepted and stored, and no component acts on it
B. Traffic is routed by kube-proxy, which falls back to the Ingress rules
C. The API server rejects the object as invalid when it is submitted
D. A cloud load balancer is provisioned automatically for the Ingress host

---

**32.** A developer needs a shell inside a running container whose image contains no shell — a distroless build. Which approach fits?

A. `kubectl exec -it <pod> -- /bin/sh`, which starts a shell in the target container
B. `kubectl port-forward` to the container's port, then connect to it from the workstation
C. Rebuild the image with a shell included and redeploy, which is the only available option
D. `kubectl debug`, which adds an ephemeral container running a different image alongside it

---

**33.** Which of the following best describes an operator in the Kubernetes sense?

A. A human administrator holding cluster-admin permissions across the whole cluster
B. A plugin that extends the `kubectl` client with additional subcommands and output
C. A controller for a custom resource, encoding operational knowledge in a reconciliation loop
D. A webhook that mutates objects at admission time on an application's behalf

---

**34.** What distinguishes a headless Service from a standard ClusterIP Service?

A. It sets `clusterIP: None`, so DNS returns the Pod addresses instead of one virtual IP
B. It carries no selector, so the addresses behind it must be maintained by hand
C. It cannot be paired with a StatefulSet, which requires one Service per replica
D. It is reachable only from outside the cluster, through each node's external address

---

**35.** A cluster has 3 control plane nodes and 20 worker nodes. Where does the authoritative record of cluster state live?

A. Replicated across all 23 nodes by the kubelet running on each of them
B. In each controller's in-memory cache, reconciled between the controllers
C. On whichever node the objects' Pods have been scheduled onto
D. In etcd, which only the API server reads from and writes to

---

**36.**

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: payments
  name: pod-reader
rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list"]
```

A ServiceAccount in `payments` is bound to the Role above by a RoleBinding in the same namespace. What may it do?

A. Get and list Pods in every namespace, since the rules name no namespace of their own
B. Get and list Pods in `payments`, and nothing else
C. Get, list, and delete Pods in `payments`, since read verbs imply the write verbs
D. Everything except delete Pods, since RBAC refuses only what a rule explicitly forbids

---

**37.** What does an Argo CD `Application` in state `OutOfSync` indicate?

A. The live cluster state differs from the desired state in the tracked repository revision
B. The Argo CD controller cannot reach the cluster's API server to compare the two states
C. The repository the Application tracks is unreachable, or its revision cannot be resolved
D. The application's Pods are running but are failing their configured readiness probes

---

**38.** A Pod has a liveness probe and a readiness probe, both HTTP GETs against different paths. The readiness probe begins failing while the liveness probe continues to succeed. What happens?

A. The container is restarted by the kubelet on the node where it is running
B. The Pod is evicted from the node and rescheduled somewhere with more headroom
C. The Pod is removed from its Services' endpoints, and the container keeps running
D. Nothing happens until both probes have failed their configured thresholds

---

**39.** Which describes the relationship between the four golden signals and the RED method?

A. They are the same four measures, published under two different names
B. RED superseded the golden signals when OpenTelemetry standardized its signals
C. RED is the client-side view of a service, and the golden signals the server-side view
D. Complementary framings: latency, traffic, errors, and saturation against rate, errors, and duration

---

**40.** A cluster operator sets a ResourceQuota on a namespace limiting total memory requests to `10Gi`, and a LimitRange in the same namespace setting a default container memory request of `256Mi`. What does each accomplish?

A. They are redundant; either one alone would bound the namespace's memory consumption
B. The quota caps the namespace's aggregate; the LimitRange supplies per-object defaults and bounds
C. The LimitRange caps the namespace's aggregate; the quota applies to each container in turn
D. The LimitRange applies only to Pods that already declare requests of their own

---

**41.** A Pod's container is terminated and the container state's `Reason` reads `OOMKilled`. What does this indicate?

A. The node came under memory pressure, and the kubelet evicted the Pod from it
B. The container's liveness probe failed, and the kubelet restarted the container
C. The scheduler could not find a node with enough allocatable memory for the Pod
D. The container exceeded its own memory limit and was terminated by the kernel

---

**42.** Which statement about `imagePullPolicy` is accurate?

A. `IfNotPresent` skips the pull when the image is already on the node; the effective default depends on the tag, with `:latest` defaulting to `Always`
B. The default is `Always` for every image, whatever tag the reference carries or omits
C. `Never` causes the kubelet to build the image on the node from a local build context
D. `Always` re-checks the registry on every start, and requires the image to be given by digest

---

**43.** A cluster's storage is provisioned on demand when a PersistentVolumeClaim is created, without an administrator pre-creating volumes. What makes this possible?

A. The claim's `accessModes` field, which selects between the provisioning modes
B. The `hostPath` volume type, which creates the directory on the node at first use
C. A StorageClass naming a provisioner, which creates the PersistentVolume dynamically
D. A reclaim policy of `Retain`, which preserves the volume so it can be reused

---

**44.** An organization wants configuration that varies between staging and production without maintaining two copies of the manifests, and prefers not to use a templating language. Which tool matches?

A. Helm, using a separate values file for each of the two environments
B. Kustomize, using a shared base and one overlay per environment
C. Argo CD sync waves, which order the objects applied to each environment
D. A ConfigMap generator in Helm, which emits per-environment ConfigMaps

---

**45.** The scheduler is placing a newly created Pod. Which sequence describes what it does?

A. It scores every node, discards the ones scoring below a threshold, and binds to one of the rest
B. It binds the Pod to a node, then filters and scores to confirm that the choice was feasible
C. It asks each kubelet whether it can accept the Pod, and binds to the first one that answers
D. It filters nodes down to the feasible ones, scores those, and binds the Pod to the highest scorer

---

**46.** The Gateway API splits responsibility for north-south traffic across three resource kinds, each aimed at a different role. Which mapping is correct?

A. GatewayClass to the infrastructure provider, Gateway to the cluster operator, HTTPRoute to the application developer
B. GatewayClass to the application developer, Gateway to the infrastructure provider, HTTPRoute to the cluster operator
C. All three are cluster-scoped, and all three are the cluster operator's alone to manage
D. HTTPRoute to the infrastructure provider, with Gateway and GatewayClass to the application developer

---

**47.** A microservices architecture is chosen over a monolith. Which trade-off is the honest characterization?

A. Decomposition reduces the system's total complexity, because each part is smaller than the whole
B. Service boundaries remove coupling between components, because each service owns its own data
C. Components can be deployed and scaled independently, at the cost of operational and network complexity
D. Independent deployment follows automatically once each service has its own repository and pipeline

---

**48.** A CronJob is defined with `schedule: "0 2 * * *"`. What does it create when it fires?

A. A Pod directly, labeled with the CronJob's name and the timestamp of the run
B. A Job, which in turn creates one or more Pods to run the work to completion
C. A Deployment scaled to a single replica, which is deleted when the work finishes
D. A DaemonSet on whichever node has the most allocatable capacity at that moment

---

**49.** An auditor needs to know which software components are present in a shipped image, so that a newly disclosed vulnerability can be checked against them. Which artifact answers that question directly?

A. The image's SBOM, an inventory of the components the image contains
B. A vulnerability scan report from the last time that image was scanned
C. A signed provenance attestation, recording how and where the image was built
D. The image's digest, which uniquely identifies the content that was shipped

---

**50.** `kubectl port-forward` to a Pod works and the application answers, but requests sent through the Pod's Service time out. What does that pair of results establish?

A. The application is unhealthy, and the Service is correctly declining to send it traffic
B. The cluster's CNI plugin is failing to pass traffic between nodes
C. The Service's ClusterIP has been reused by another Service in the same namespace
D. The application is reachable; the fault is on the Service path — selector, ports, or endpoints

---

**51.** Which statement about labels and selectors is correct?

A. They are interchangeable with annotations, and which to use is a matter of house style
B. Labels are for identification and selection; annotations carry metadata and are not selectable
C. Selectors can match on annotations when a label value would exceed the 63-character limit
D. Labels must be unique within a namespace, whereas annotations may repeat freely

---

**52.** A Pod in the namespace `orders` resolves the name `billing`. Which Service does that name reach, and why?

A. The `billing` Service in `default`, because unqualified names resolve in the default namespace
B. Nothing, because a Service name must be given fully qualified before cluster DNS resolves it
C. The `billing` Service in `orders`, because the Pod's search domains try its own namespace first
D. Whichever `billing` Service was created first, because cluster DNS resolves names cluster-wide

---

**53.** A contributor wants to propose a substantial change to a Kubernetes subsystem. Through which structure and document does that proposal proceed?

A. A pull request against the release branch, reviewed by the Steering Committee
B. An issue on the CNCF Landscape repository, triaged by the Technical Oversight Committee
C. A CNCF Technical Advisory Group charter, ratified by the Governing Board
D. A Kubernetes Enhancement Proposal, brought to the SIG that owns that subsystem

---

**54.** What does the Container Runtime Interface standardize?

A. The boundary between the kubelet and the container runtime, so runtimes are interchangeable
B. The on-disk format of a container image and the ordering of the layers inside it
C. The protocol by which registries distribute images to the nodes that pull them
D. The mechanism by which a container is given a network address on its node

---

**55.** Two containers run in one Pod. Which statement about what they share is correct?

A. They share a filesystem root, so a file written by one is visible to the other
B. They share a process namespace by default, so each can see the other's processes
C. They share a network namespace, so each reaches the other on `localhost`
D. They share one memory limit, so either may consume whatever the other leaves unused

---

**56.** The twelve-factor app says configuration belongs in the environment rather than in the build. Which Kubernetes practice implements that?

A. Baking each environment's settings into a separate image, one tag per environment
B. Supplying settings from ConfigMaps and Secrets, so one image runs in every environment
C. Mounting a `hostPath` volume holding the node's local copy of the settings file
D. Rebuilding and redeploying the application whenever a single setting has to change

---

**57.**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
```

What is the maximum number of Pods this Deployment may have in existence during a rolling update?

A. Four, because `maxUnavailable: 0` forbids the running count from changing at all
B. Eight, because the new ReplicaSet is created at full size beside the old one
C. Three, because one Pod is taken down before each replacement is created
D. Five, because `maxSurge: 1` permits one Pod above the desired count

---

**58.** A workload should run on nodes labeled `disk=ssd` where possible, but should still be scheduled when no such node is available. Which mechanism expresses that?

A. Node affinity with a `preferredDuringSchedulingIgnoredDuringExecution` rule
B. A `nodeSelector` naming the label, which the scheduler treats as a preference
C. A taint on every node lacking the label, with a matching toleration on the Pod
D. Node affinity with a `required` rule, which the scheduler relaxes when nothing matches

---

**59.**

```
$ kubectl get svc,endpointslice -l app=orders
NAME             TYPE        CLUSTER-IP      PORT(S)   AGE
service/orders   ClusterIP   10.96.140.22    80/TCP    6m

NAME                         ADDRESSTYPE   ENDPOINTS   AGE
endpointslice/orders-x8k2p   IPv4          <none>      6m

$ kubectl get pods -l app=order-api
NAME                       READY   STATUS    RESTARTS   AGE
order-api-5d7c9b4f-jm2wq   1/1     Running   0          6m
order-api-5d7c9b4f-t4nlv   1/1     Running   0          6m
```

Both Pods are ready, and the Service has no endpoints. What is the most likely cause?

A. The Pods' readiness probes pass, but their startup probes have not yet completed
B. The Service's selector does not match the labels the Pods actually carry
C. The Service's `targetPort` names a port the containers do not expose
D. No Ingress controller is installed, so the Service has nothing to route traffic for

---

**60.** Which of the following accurately describes how a Kubernetes controller behaves?

A. It runs a sequence of steps once, at the moment the object it manages is created
B. It is invoked by the scheduler once a Pod has been bound to a particular node
C. It loops continuously, comparing desired state against observed and closing the difference
D. It applies its changes only when an administrator runs `kubectl apply` against the cluster

---

**Stop. Note your time. The answers begin below.**

---

## Mock Exam Answers & Walkthroughs

Work through these in order, and record two things per question: whether you got it right, and which domain it belonged to. The domain tag is on every answer for exactly that purpose.

---

**1. C** — *D1.4 · Ch 2 §1 · ⚪*

A container is a host process placed in kernel namespaces and cgroups, sharing the host's kernel. A VM runs its own kernel on virtualized hardware. That single difference explains the startup-time gap and the isolation-strength gap at once. *[cross-bearing: see Ch 2 §1 — what a container actually is]*

- **A is wrong** because it inverts the two. The container shares the kernel; the VM has its own.
- **B is wrong** because a container's ceiling comes from cgroups on the host, and a VM's from the hypervisor's allocation. It swaps the mechanisms.
- **D is wrong** on both halves. A hypervisor belongs to the VM; a container runtime belongs to the container.

---

**2. B** — *D2.1 · Ch 9 §1 · 🔵*

Without a CNI plugin the cluster has no implementation of the pod network. Pods do not get addresses and do not become ready. *[cross-bearing: see Ch 9 §1 — four rules and a plugin]*

- **A is wrong** because the control plane comes up independently of the pod network. That is why you can inspect a broken cluster at all.
- **C is wrong** because the failure is not egress-specific; pod-to-pod networking does not exist either.
- **D is wrong** because ClusterIP assignment is done by the API server from a configured range, and does not depend on CNI.

---

**3. D** — *D1.1 · Ch 3 §5 · 🔵*

The API server is the sole mutator of cluster state. Everything else — scheduler, controllers, kubelets — reads and writes through it. *[cross-bearing: see Ch 3 §5 — the only door in]*

- **A is wrong** because the scheduler decides a binding and then *submits* it to the API server; it does not write state itself.
- **B is wrong** for the same reason: the kubelet reports its node's status through the API server.
- **C is wrong** because controllers act by making API requests. It is the pattern's whole point that they have no back channel.

---

**4. A** — *D3.1 · Ch 14 §2 · ⚪*

`values.yaml` holds the chart's default parameters, which templates consume and users override. *[cross-bearing: see Ch 14 §2 — what a chart contains]*

- **B is wrong** because the rendered manifest is the output of templating, not an input file in the chart.
- **C is wrong** because name, version, and dependencies live in `Chart.yaml`.
- **D is wrong** because CustomResourceDefinitions live in the `crds/` directory, which exists to solve an ordering problem. *[cross-bearing: see Ch 14 §6 — which one, when]*

---

**5. B** — *D1.1 · Ch 4 §3 · ⚪*

A Namespace is a scope for names, and several important kinds live outside it: Nodes, PersistentVolumes, StorageClasses, ClusterRoles. *[cross-bearing: see Ch 4 §3 — where a name lives]*

- **A is wrong**, and it is the trap this question is built for. Kernel isolation is the *Linux* namespace from Chapter 2, a different mechanism that shares an English word.
- **C is wrong** because cluster-scoped kinds exist, and knowing which is which is directly testable.
- **D is wrong** because namespace deletion cascades: the objects inside are deleted with it. There is no orphaned state left behind, which is exactly why deleting a namespace is not a reversible tidying-up.

---

**6. D** — *D2.2 · Ch 12 §1 · ⚪*

Cloud, Cluster, Container, Code, from outside in. The cloud (or datacenter) layer is the foundation; a compromise there makes every layer above it moot. *[cross-bearing: see Ch 12 §1 — four layers and four phases]*

- **A is wrong** because Code is the innermost layer, the one every other layer sits outside of.
- **B is wrong** because Container is the second-innermost, one step out from Code.
- **C is wrong** because Cluster is the third, sitting inside Cloud rather than outside it.

<!-- AUTHOR-REVIEW: this item asserts the composition and ordering of a named external model (the
     4Cs of Cloud Native Security, from the Kubernetes documentation) with no [source:] tag. The
     ordering is load-bearing — a reader who learns it backwards fails the real question. The
     cross-bearing to Ch 12 §1 suggests Ch 12 owns and sourced it; if Ch 12's fact-accuracy
     diagnostic cleared it against a cached snapshot, name that snapshot here. If it did not, open a
     research gap for the Kubernetes docs page on the 4C's of Cloud Native Security and tag both the
     stem's premise and this walkthrough. -->

---

**7. C** — *D4.1 · Ch 18 §4 · 🔵*

Prometheus pulls. It discovers targets and scrapes their metrics endpoints on an interval. *[cross-bearing: see Ch 18 §4 — pulling, not being pushed]*

- **A is wrong** as the general model. Pushgateway exists for the narrow case of jobs too short-lived to be scraped, and using it generally is an anti-pattern.
- **B is wrong** because an OTel Collector can *export* to Prometheus, but the transfer is still a scrape of the collector; Prometheus does not subscribe to a stream.
- **D is wrong** because the API server is one scrape target among many, not the source of application metrics.

---

**8. A** — *D1.1 · Ch 5 §8 · 🔵*

Requests and limits are both set, and they are not equal, which is Burstable. Guaranteed requires request equal to limit for every resource in every container. *[cross-bearing: see Ch 5 §8 — what a Pod is owed]*

- **B is wrong** because `250m` ≠ `500m` and `256Mi` ≠ `512Mi`. This is the single most common QoS error, and it is arithmetic rather than recall.
- **C is wrong** because BestEffort means no requests and no limits at all, which this manifest plainly has.
- **D is wrong** because QoS is a property of the Pod, computed once across every resource in every container. There is no per-resource QoS class.

---

**9. B** — *D2.4 · Ch 11 §1 · ⚪*

An `emptyDir` lives and dies with the Pod. Same node makes no difference; a new Pod gets a new empty directory. *[cross-bearing: see Ch 11 §1 — three lifetimes, and the volumes that have them]*

- **A is wrong** because node-scoped persistence is what `hostPath` does, and it is a hazard for exactly the reasons that chapter gives.
- **C is wrong** because Pod name has no bearing on volume lifetime. Per-replica persistence requires a PVC.
- **D is wrong** because nothing copies or migrates an `emptyDir`; the kubelet deletes it when the Pod is removed.

---

**10. C** — *D1.1 · Ch 6 §1 · ⚪*

Deployment owns ReplicaSets; each ReplicaSet owns Pods. A rolling update works by scaling a new ReplicaSet up while scaling the old one down, which is why old ReplicaSets stick around and why rollback is possible at all. *[cross-bearing: see Ch 6 §5 — every rollout is a revision]*

- **A is wrong** because it removes the layer that makes revision history work.
- **B is wrong** because it inverts the ownership chain; a ReplicaSet has no knowledge of Deployments.
- **D is wrong** because they are distinct kinds with distinct jobs, both in `apps/v1`.

---

**11. A** — *D3.1 · Ch 15 §3 · 🔵*

Pull, not push. An in-cluster agent reconciles continuously against a repository that holds desired state. *[cross-bearing: see Ch 15 §3 — push, or pull]*

- **B is wrong** because it describes the push model precisely — and it inverts the security argument. Holding cluster credentials in the build system is the push model's cost, and avoiding it is a principal reason to adopt pull.
- **C is wrong** because continuous reconciliation is one of the OpenGitOps principles. The agent corrects drift that no merge caused.
- **D is wrong** because GitOps depends on declarative manifests; it does not replace them with scripts.

<!-- AUTHOR-REVIEW: draft-v1 wrote "one of the four OpenGitOps principles". The cardinality claim is
     the fragile part and no OpenGitOps snapshot is in this corpus, so the count has been dropped
     here. Open a research gap for the OpenGitOps Principles (opengitops.dev); once cached, restore
     "four" and tag it. Note the B6 skeleton assigns the four principles to Ch 15 §3, so Ch 15 may
     already carry a snapshot — check there before opening a new gap. -->

---

**12. D** — *D2.3 · Ch 13 §2 · 🔵*

`Pending` is the phase of a Pod that has not been scheduled. The scheduler found no feasible node, or the Pod has not yet been considered. *[cross-bearing: see Ch 13 §2 — Pods that never start]*

- **A is wrong** because a missing tag surfaces as `ImagePullBackOff`, which happens *after* scheduling. The image is pulled on a node, so a Pod cannot fail to pull an image it was never assigned a node for.
- **B is wrong** because a container that starts and exits gives you `CrashLoopBackOff`, not `Pending`.
- **C is wrong** because an OOM kill requires a running container. Reading the phase first is what separates these four instantly. *[cross-bearing: see Ch 13 §1 — whose problem is this]*

---

**13. B** — *D1.4 · Ch 2 §3 · 🔵*

A tag is a mutable pointer into a repository. A digest is content-addressed and identifies exactly one image. *[cross-bearing: see Ch 2 §3 — registries, tags, and digests]*

- **A is wrong** because tag immutability is a registry policy some registries offer, not a property of the reference grammar.
- **C is wrong** because a tag resolves to one manifest; there is no "nearer" copy behind the same tag.
- **D is wrong** because it misunderstands what a digest is. The digest *is* the content's identity: new content has a new digest, and the old digest still resolves to the old content.

---

**14. C** — *D2.1 · Ch 10 §6 · 🟡*

NetworkPolicy is allow-only. There is no deny rule to write. What produces isolation is *selection*: once any policy selects a Pod, that Pod becomes default-deny for the direction the policy covers, and only the allowed sources get through. *[cross-bearing: see Ch 10 §6 — allowing, never denying]*

- **A is wrong** because the second policy cannot be written in the first place, so there is nothing to honor.
- **B is wrong** because policies are additive and unordered; a later one never overrides an earlier one.
- **D is wrong** because there is no conflict to detect, and nothing for admission to reject. This is the same additive semantics RBAC uses, which is not a coincidence. *[cross-bearing: see Ch 12 §9 — additive, never deny]*

---

**15. A** — *D4.3 · Ch 17 §2 · 🔵*

Sandbox, Incubating, Graduated, in that order. Sandbox is the entry point; Incubating and then Graduated each raise the bar on adoption, governance, and sustainability. *[cross-bearing: see Ch 17 §2 — Sandbox, Incubating, Graduated, and who decides]*

- **B is wrong** because it reverses the first two levels. Incubating is the middle rung, not the entry point.
- **C is wrong** because it skips Incubating. A project does not go from Sandbox straight to Graduated.
- **D is wrong** on both halves: it names the wrong entry level and the wrong successor.

Worth carrying into the real exam: the *levels and their order* are the durable fact. Which projects sit at which level changes constantly, and a memorized Graduated roster is memorization with an expiry date on it.

<!-- AUTHOR-REVIEW: two provenance gaps in this item, both needing a fetch rather than a rewrite.
     (1) The maturity levels and their ordering are asserted with no [source:] tag;
     cncf-curriculum-kcna-readme-2026-08-31 covers domain weights only and does not reach them. Open
     a research gap for the CNCF project maturity levels / graduation criteria document. This one is
     worth caching rather than softening — the item's whole force depends on the ordering being right.
     (2) The stem's premise that the entry level carries no production-adoption requirement is a
     claim about admission criteria and needs the same snapshot. If the snapshot does not support it,
     cut the clause and let the stem read "at the entry level of its maturity ladder". -->

---

**16. D** — *D1.2 · Ch 8 §2 · 🔵*

Authentication (who are you), then authorization (may you), then admission (should this specific object be allowed, and does it need modifying). *[cross-bearing: see Ch 8 §2 — three gates and a logbook]*

- **A is wrong** because admission cannot run first: it inspects an object whose submitter has not been identified and whose permission has not been checked. There is nothing yet to admit.
- **B is wrong** because admission cannot precede authorization. A mutating webhook would otherwise modify an object the requester may turn out to have no permission to create.
- **C is wrong** because authorization cannot precede authentication. Policy is evaluated against an identity, and there is no identity yet.

---

**17. C** — *D2.1 · Ch 9 §4 · 🔵*

Readiness gates endpoint membership. `web-...-lz8mt` shows `0/1` ready, so it keeps running but is taken out of the Service's endpoint set — precisely the behavior the probe exists to provide. Two endpoints. *[cross-bearing: see Ch 9 §4 — the list behind the name]*

- **A is wrong** because it reads the `STATUS` column and ignores `READY`. `Running` is the phase; readiness is a separate condition, and it is the one endpoints follow.
- **B is wrong** because endpoint membership is per-Pod, not all-or-nothing. The other two Pods remain addressable.
- **D is wrong** because kube-proxy does not drop traffic to unready Pods. The Pod is not in the endpoint list for it to route to in the first place.

---

**18. B** — *D3.1 · Ch 14 §3 · 🟡*

Two mechanisms wearing the same word. `helm rollback` moves the *release* to a previous *release revision*, potentially every object the chart manages. `kubectl rollout undo` moves one Deployment back to a previous ReplicaSet. *[cross-bearing: see Ch 14 §3 — chart, release, revision]*

- **A is wrong** because Helm maintains its own release history and applies the previous manifest set; it does not call the Deployment's rollout machinery.
- **C is wrong** because `kubectl rollout undo` works on any Deployment regardless of how it was installed, which is part of why the confusion is easy to have.
- **D is wrong** because `revisionHistoryLimit` bounds a Deployment's ReplicaSet history, which is not where Helm keeps release revisions.

---

**19. A** — *D1.2 · Ch 8 §4 · 🔵*

Cordon marks the node unschedulable so nothing new lands there; drain then evicts what is already running so it can be rescheduled elsewhere. *[cross-bearing: see Ch 8 §4 — taking a node out of service]*

- **B is wrong** in ordering. Draining first without cordoning invites the scheduler to place new Pods on the node you are emptying. (In practice `kubectl drain` cordons for you. The exam tests the conceptual order, and knowing *why* cordon precedes drain is the point.)
- **C is wrong**, and destructive: deleting the Node object does not gracefully move the workloads off it first.
- **D is wrong** because `uncordon` returns a node to service, which is the opposite of taking it out.

---

**20. D** — *D2.2 · Ch 12 §4 · 🔵*

base64 is an encoding. Anyone who can read the Secret can decode it in one command. Encryption at rest is a separate cluster-level configuration. *[cross-bearing: see Ch 12 §4 — Secrets are not encrypted]*

- **A is wrong** because encryption at rest is not on by default; it requires an EncryptionConfiguration on the API server.
- **B is wrong** because that is the misconception this whole item targets. Decoding base64 requires no key and no privilege beyond reading the value.
- **C is wrong** because file mounts are not only possible but generally preferred over environment variables, which leak into process listings and crash dumps.

---

**21. C** — *D1.1 · Ch 6 §6 · 🔵*

Stable identity is the distinction. Each replica gets an ordinal, a stable name, and a stable network identity that survive rescheduling. *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*

- **A is wrong**, and it is the most common belief about StatefulSets. Any Pod can mount a PVC. What a StatefulSet adds is a `volumeClaimTemplate` giving each replica *its own* claim. *[cross-bearing: see Ch 11 §6 — Pods that are not interchangeable, revisited]*
- **B is wrong** because Deployments support rolling updates too; StatefulSets add ordering constraints to theirs, but they did not invent the capability.
- **D is wrong** because one replica per node is a DaemonSet, a different kind with a different purpose.

---

**22. B** — *D4.1 · Ch 18 §5 · 🔵*

A span represents one operation within a trace, carrying its own start, end, and place in the tree. *[cross-bearing: see Ch 18 §5 — following one request]*

- **A is wrong** because a metric is a different signal entirely: aggregate numbers over time, with no identity tying them to one request.
- **C is wrong** because logs are a third signal. A log line may reference a trace, but it is not the trace's unit of structure.
- **D is wrong** because baggage is contextual data propagated alongside a trace, not a unit within it.

---

**23. D** — *D1.1 · Ch 5 §3 · 🔵*

Init containers run to completion, in order, before any application container starts. A failure stops the sequence and is retried per the Pod's `restartPolicy`. *[cross-bearing: see Ch 5 §3 — everything that must happen first]*

- **A is wrong** because the ordering guarantee is the entire feature. If failures were advisory, an init container could not be used to wait for a dependency.
- **B is wrong** because a failing init container does not trigger rescheduling; the Pod stays where it is and retries in place.
- **C is wrong** because init containers do not proceed past a failure. The sequence halts on the one that failed.

---

**24. A** — *D2.3 · Ch 13 §3 · 🔵*

`--previous` retrieves the logs of the previous terminated container instance, which — with eleven restarts and the most recent 22 seconds ago — is the run that actually failed. *[cross-bearing: see Ch 13 §3 — looking inside]*

- **B is wrong** because in a crash loop the current instance is either seconds old or not running at all. You get an empty stream or the first lines of a fresh start.
- **C is wrong** because `describe` shows events, conditions, and state transitions — useful context, but not the container's own output.
- **D is wrong** for the same reason. `kubectl events --for pod/<pod>` filters events to a resource `[source: k8s-docs-kubectl-events-2026-08-31]`, which tells you what the cluster did, not what the process printed.

<!-- AUTHOR-REVIEW: the claim about `kubectl logs --previous` is untagged, while the sibling
     `kubectl events` claim in the same walkthrough is tagged — inconsistent within one item. The
     natural tag is k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31, whose concepts_covered
     lists `kubectl-logs-previous`. BUT the body of that snapshot as packed for this stage ends at
     the heading "## Interacting with running Pods" with no command lines beneath it, so the flag's
     documented wording could not be verified. Confirm the file on disk carries the line before
     tagging; if it is genuinely truncated, that is a corpus defect to raise rather than paper over. -->

---

**25. C** — *D3.1 · Ch 15 §2 · 🔵*

Canary: a small share of production traffic to the new version first, with the rest still on the old one. *[cross-bearing: see Ch 15 §2 — ways to replace what's running]*

- **A is wrong** because Recreate takes everything down and brings everything up, which is the opposite of a graduated exposure.
- **B is wrong** because blue/green stands up a complete parallelenvironment and cuts over to it wholesale, rather than splitting traffic by proportion.
- **D is wrong** because a rolling update replaces instances incrementally without steering any particular share of traffic to the new version.

---

**26. B** — *D1.3 · Ch 7 §4 · 🟡*

`NoExecute` evicts running Pods that do not tolerate the taint, as well as preventing new ones from landing. The Pod on `node-07` declares no tolerations, so it goes. *[cross-bearing: see Ch 7 §4 — when the berth refuses you]*

- **A is wrong** because that describes `NoSchedule`, which affects only future placement. The distinction between the three effects is exactly what this manifest is testing.
- **C is wrong** because node conditions and taints are different mechanisms. A condition can cause a taint; a taint does not set a condition.
- **D is wrong** because tolerations are declared by the Pod's author. Nothing adds one on the Pod's behalf.

---

**27. A** — *D2.4 · Ch 11 §4 · 🟡*

Access modes are node-count semantics. `ReadWriteOnce` means read-write by a single *node*; multiple Pods on that node can share the volume. *[cross-bearing: see Ch 11 §4 — access modes and what happens after]*

- **B is wrong** because it reads "Once" as "one Pod." The mode that means one Pod is `ReadWriteOncePod`, which exists precisely because RWO does not mean that.
- **C is wrong** because it treats the mode as permission semantics — who may write — rather than as a constraint on how many nodes may mount it.
- **D is wrong** for the same category error at a smaller scope. Containers within one Pod are already on one node, so the mode has nothing to say about them.

---

**28. D** — *D1.1 · Ch 4 §2 · 🔵*

`spec` is the declaration a user files; `status` is what a controller observes and reports back. Every control loop in the cluster is the gap between those two fields being closed. *[cross-bearing: see Ch 4 §2 — the anatomy of a record]*

- **A is wrong** because it swaps the writers. A user who edits `status` is writing into a field the controller owns and will overwrite.
- **B is wrong** because the API server does not require them to agree — a newly created object has a `spec` and an empty or absent `status`, and that disagreement is the work queue.
- **C is wrong** because rollback history lives in revisions on the workload object, not in `status`. *[cross-bearing: see Ch 6 §5 — every rollout is a revision]*

---

**29. B** — *D4.2 · Ch 17 §5 · 🔵*

The data plane is the proxies carrying traffic; the control plane configures them and distributes policy. *[cross-bearing: see Ch 17 §5 — a network that knows what it's carrying]*

- **A is wrong** because it inverts them. The plane that carries the packets is the data plane, by definition.
- **C is wrong** because they are genuinely different components with different jobs, not one thing viewed at two scopes.
- **D is wrong** on both halves. Note also that "control plane" here is the *mesh's*, not the cluster's — two different things wearing one phrase. *[cross-bearing: see Ch 3 §2 — the control plane]*

---

**30. C** — *D1.4 · Ch 2 §2 · ⚪*

Layers are content-addressed and shared. Two images from the same base share the base's layers on disk and in the registry. *[cross-bearing: see Ch 2 §2 — what's inside an image]*

- **A is wrong**, and it misses the reason layering exists at all. Independent copies would make a registry of similar images ruinously large.
- **B is wrong** because images are independent objects; pushing one does not evict another that happens to share its base.
- **D is wrong** because layers stack within one image. There is no merge across images.

---

**31. A** — *D2.1 · Ch 10 §3 · 🔵*

The object exists; nothing happens without the component. Kubernetes accepts and stores the Ingress, and no traffic moves until an Ingress controller is watching for it. *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*

- **B is wrong** because kube-proxy implements Services, not Ingress rules, and has no L7 routing to fall back to.
- **C is wrong** because the object is valid, which is what makes this failure quiet and confusing. Nothing warns you.
- **D is wrong** because that is a LoadBalancer Service's behavior — and it too requires a component, the cloud-controller-manager, to act.

---

**32. D** — *D3.2 · Ch 16 §3 · 🟡*

An ephemeral container added by `kubectl debug` runs a separate image inside the target Pod, so you get tools the target image does not have. *[cross-bearing: see Ch 16 §3 — getting inside, and adding what isn't there]*

- **A is wrong** because `exec` runs a binary that must already exist in the container. Distroless means it does not.
- **B is wrong** because port-forward moves traffic to a port. It gives you the application's interface, not a shell.
- **C is wrong** because ephemeral containers exist precisely so that rebuilding is not the only option — and rebuilding changes the thing you were trying to observe.

---

**33. C** — *D1.1 · Ch 6 §8 · 🟡*

An operator is a controller for a custom resource, encoding what a human operator would know about running a particular application. *[cross-bearing: see Ch 6 §8 — the control loop, extended]*

- **A is wrong**, and it is a genuine vocabulary hazard: "operator" is never used for a person in this book. Where the Gateway API says "cluster operator" it means a *role name*, not an individual. *[cross-bearing: see Ch 10 §5 — roles, not just routes]*
- **B is wrong** because a `kubectl` plugin extends the client on your workstation, not the cluster's reconciliation behavior.
- **D is wrong** because an admission webhook acts once per request, at admission time. An operator runs a loop continuously, long after the object was persisted.

---

**34. A** — *D2.1 · Ch 9 §5 · 🟡*

`clusterIP: None` means no virtual IP. DNS returns the Pod addresses directly, which is what a client needs when it must address individual replicas. *[cross-bearing: see Ch 9 §5 — when you don't want a single address]*

- **B is wrong** because a headless Service usually *does* have a selector. A Service without selectors is a separate case with a separate purpose.
- **C is wrong** because headless Services are the standard pairing for StatefulSets, supplying exactly the per-replica DNS names those workloads need. *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*
- **D is wrong** because headless Services are an internal DNS mechanism. Nothing about them exposes anything externally.

---

**35. D** — *D1.1 · Ch 3 §2 · ⚪*

etcd holds cluster state, and only the API server talks to it. That is why etcd is the one thing whose backup matters. *[cross-bearing: see Ch 8 §7 — the one backup that matters]*

- **A is wrong** because kubelets hold no authoritative state; they report and obey.
- **B is wrong** because controller caches are derived from watches and are disposable. Losing one costs a resync, not data.
- **C is wrong** because object state is not distributed to the nodes running the workloads. A node knows about its own Pods, not about the cluster.

---

**36. B** — *D2.2 · Ch 12 §3 · 🔵*

A Role is namespaced, and a RoleBinding grants it within that namespace only. The rule lists two verbs on one resource, so that is exactly the access granted: get and list Pods in `payments`. *[cross-bearing: see Ch 12 §3 — what you may do]*

- **A is wrong** because a Role's scope comes from its own `metadata.namespace`, not from what its rules mention. Cluster-wide access would require a ClusterRole bound with a ClusterRoleBinding.
- **C is wrong** because RBAC verbs are enumerated, never implied. `delete` is absent, so `delete` is refused.
- **D is wrong** because it inverts the model. RBAC is purely additive: there are no deny rules, and anything not granted is refused. *[cross-bearing: see Ch 12 §9 — additive, never deny]*

---

**37. A** — *D3.1 · Ch 15 §4 · 🔵*

`OutOfSync` means live state differs from the desired state in the tracked revision. *[cross-bearing: see Ch 15 §4 — an agent that watches a repository]*

- **B is wrong** because a controller that cannot reach the cluster reports a connectivity condition. It cannot make a sync verdict at all without seeing live state.
- **C is wrong** because an unreachable repository is likewise its own error state. With no desired state to compare against, there is nothing to call out of sync.
- **D is wrong** because Pod health is application state. `OutOfSync` is strictly about the declared-versus-live comparison, and a perfectly healthy application can be out of sync.

---

**38. C** — *D1.1 · Ch 5 §7 · 🔵*

Readiness controls endpoint membership. The container keeps running; traffic stops arriving. *[cross-bearing: see Ch 5 §7 — three probes, three jobs]*

- **A is wrong** because restart is the *liveness* probe's consequence. Three probes, three distinct jobs, and the exam will test whether you can keep them apart.
- **B is wrong** because eviction is a node-pressure mechanism, unrelated to probe results.
- **D is wrong** because each probe acts independently on its own failure. There is no combined threshold.

---

**39. D** — *D4.1 · Ch 18 §7 · 🔵*

Complementary framings. Golden signals: latency, traffic, errors, saturation. RED: rate, errors, duration. *[cross-bearing: see Ch 18 §7 — is the service doing what users expect]*

- **A is wrong** because RED has three measures and omits saturation — the one that tells you about headroom rather than symptoms.
- **B is wrong** because OpenTelemetry standardizes signal *transport and semantics*, not which measures you should care about. Neither framing was retired.
- **C is wrong** because both framings are written from the service's own perspective. RED's rate, errors, and duration are measured at the service, not at its callers.

---

**40. B** — *D1.2 · Ch 8 §3 · 🟡*

ResourceQuota caps the namespace's aggregate; LimitRange supplies per-object defaults and bounds. They work together: the LimitRange's default request is often what makes objects countable against the quota in the first place. *[cross-bearing: see Ch 8 §3 — dividing a shared cluster]*

- **A is wrong** because they operate at different scopes and neither substitutes for the other. A quota alone cannot stop one Pod claiming the whole `10Gi`.
- **C is wrong** because it swaps them. Nothing about a LimitRange sums across the namespace.
- **D is wrong** because supplying defaults for objects that *don't* declare requests is a LimitRange's central job.

---

**41. D** — *D2.3 · Ch 13 §4 · 🔵*

`OOMKilled` is the container exceeding its own memory limit and being terminated by the kernel's OOM killer. *[cross-bearing: see Ch 5 §8 — what a Pod is owed]*

- **A is wrong**, and this is the distinction the question exists for. Node-level memory pressure produces `Evicted`, and eviction order follows QoS class. *[cross-bearing: see Ch 13 §4 — Pods that start and then don't stay]*
- **B is wrong** because a liveness failure restarts the container without that reason string; you would see the restart count climb with a different cause.
- **C is wrong** because a scheduling failure leaves the Pod `Pending`, with no container running for anything to kill.

---

**42. A** — *D1.4 · Ch 2 §6 · 🟡*

`IfNotPresent` uses the copy already on the node when there is one. The effective default is not fixed: it is `IfNotPresent` for a normal tag, and `Always` when the reference is `:latest` or carries no tag at all. *[cross-bearing: see Ch 2 §6 — when Kubernetes pulls, and when it doesn't]*

- **B is wrong** because the default is conditional on the tag, which is exactly the detail this item tests. Assuming an unconditional `Always` is how people convince themselves a stale image is impossible.
- **C is wrong** because `Never` means use only what is already on the node, and fail if nothing is there. The kubelet builds nothing.
- **D is wrong** because `Always` re-checks the registry on every container start but places no requirement on how the image is referenced. A digest reference is a separate, stronger guarantee.