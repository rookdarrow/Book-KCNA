---
source_url: "https://kubernetes.io/docs/concepts/workloads/autoscaling/"
fetched_at: "2026-08-31T09:55:00-0400"
authority: "Kubernetes project (kubernetes.io/docs) — three pages, each attributed inline"
objectives_covered: ["D4.2"]
concepts_covered: ["vertical-pod-autoscaler", "keda-event-driven-autoscaling", "horizontal-vs-vertical-autoscaling", "cluster-autoscaler"]
---
# Autoscaling workloads, the VPA, and in-place resize — refreshed 2026-08-31

REFRESHES the version-dependent claims in `k8s-docs-autoscaling-2026-08-23.md`.
That snapshot's structural facts are unchanged; its VERSION NUMBER has moved and
its VPA-in-place claim is contradicted by two other official pages. Both are
recorded here. See the manifest's Notes 1.

## Source A — kubernetes.io/docs/concepts/workloads/autoscaling/ (verbatim)

### Vertical scaling

> "You can automatically scale a workload vertically using a
> VerticalPodAutoscaler (VPA). Unlike the HPA, the VPA doesn't come with
> Kubernetes by default, but is a an add-on that you or a cluster administrator
> may need to deploy before you can use it."

> "Once installed, it allows you to create CustomResourceDefinitions (CRDs) for
> your workloads which define _how_ and _when_ to scale the resources of the
> managed replicas."

> "Note: You will need to have the Metrics Server installed to your cluster for
> the VPA to work."

### In-place pod vertical scaling

> "Feature state: Stable since Kubernetes v1.35"

> "This is a stable feature in Kubernetes, and has been since version v1.35. It
> was first available in the v1.27 release. You can no longer disable or opt out
> of this feature or behavior (it is locked); if you explicitly set a value for
> the associated feature gate InPlacePodVerticalScaling, Kubernetes ignores it
> but does not report any error."

> "As of Kubernetes 1.37, VPA does not support resizing pods in-place, but this
> integration is being worked on."

*(The 2026-08-23 snapshot recorded this same sentence dated to v1.35. The claim
persists; only the version stamp has advanced.)*

### Event driven autoscaling

> "It is also possible to scale workloads based on events, for example using the
> _Kubernetes Event Driven Autoscaler_ (**KEDA**)."

> "KEDA is a CNCF-graduated project enabling you to scale your workloads based on
> the number of events to be processed, for example the amount of messages in a
> queue. There exists a wide range of adapters for different event sources to
> choose from."

### Autoscaling based on schedules

> "Another strategy for scaling your workloads is to **schedule** the scaling
> operations, for example in order to reduce resource consumption during off-peak
> hours."

> "Similar to event driven autoscaling, such behavior can be achieved using KEDA
> in conjunction with its `Cron` scaler. The `Cron` scaler allows you to define
> schedules (and time zones) for scaling your workloads in or out."

### Scaling cluster infrastructure

> "If scaling workloads isn't enough to meet your needs, you can also scale your
> cluster infrastructure itself."

> "Scaling the cluster infrastructure normally means adding or removing nodes."

## Source B — kubernetes.io/docs/concepts/workloads/autoscaling/vertical-pod-autoscale/ (verbatim)

> "In Kubernetes, a _VerticalPodAutoscaler_ automatically updates a workload
> management resource (such as a Deployment or StatefulSet), with the aim of
> automatically adjusting infrastructure resource requests and limits to match
> actual usage."

> "Unlike HorizontalPodAutoscaler, which is part of the core Kubernetes API, VPA
> must be installed separately in your cluster."

> "The VPA consists of three main components: The _recommender_, which analyzes
> resource usage and provides recommendations. The _updater_, that Pod resource
> requests either by evicting Pods or modifying them in place. And the VPA
> _admission controller_ webhook, which applies resource recommendations to new
> or recreated Pods."

Update modes listed on this page: `Off`, `Initial`, `Recreate`,
`InPlaceOrRecreate`, `InPlace`, `Auto` (deprecated).

## Source C — kubernetes.io/blog/2025/12/19/kubernetes-v1-35-in-place-pod-resize-ga/ (verbatim)

> "This release marks a major step: more than 6 years after its initial
> conception, the **In-Place Pod Resize** feature (also known as In-Place Pod
> Vertical Scaling), first introduced as alpha in Kubernetes v1.27, and graduated
> to beta in Kubernetes v1.33, is now **stable (GA)** in Kubernetes 1.35!"

> "In-Place Pod Resize makes CPU and memory requests and limits mutable, allowing
> you to adjust these resources within a running Pod, often without requiring a
> container restart."

> "Autoscalers are now empowered to adjust resources and with less impact. For
> example, Vertical Pod Autoscaler (VPA)'s `InPlaceOrRecreate` update mode, which
> leverages this feature, has graduated to beta. This allows resources to be
> adjusted automatically and seamlessly based on usage with minimal disruption."

---
⚠ SOURCE CONFLICT — see manifest Notes 1. Sources A, B and C are all
kubernetes.io and do not agree on whether VPA supports in-place resize. Trap #105
must be written to the conflict, not through it.
