## ⚪ §2 — The Address That Doesn't Last

Your frontend Pod has the database Pod's address. It works. Requests go out, responses come back, everything is fine.

Then the database Deployment gets a new image tag and performs a rolling update. Every database Pod is replaced. And Chapter 6 was precise about what "replaced" means: Kubernetes does not repair a Pod and hand it back — a Pod is never rescheduled to a different node; it is replaced by a new, near-identical Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23]. A different Pod. Which, per §1's first rule, has a different address.

The frontend is now holding a valid-looking address for something that does not exist. Nothing malfunctioned. The system did precisely what it was designed to do, and the design broke the client.

*[cross-bearing: see Ch 6 §4 — rolling updates and Pod replacement]*, and *[cross-bearing: see Ch 5 §3 — Pod ephemerality]*, where you were told in as many words that this fact is the premise of Chapter 9. Here it is, being used.

Generalize it, in the documentation's own framing, because the exam's framing of Services descends from this paragraph:

> If some set of Pods (call them "backends") provides functionality to other Pods (call them "frontends") inside your cluster, how do the frontends find out and keep track of which IP address to connect to? [source: k8s-docs-service-2026-08-23]

The set of Pods running at one moment can be different from the set running a moment later [source: k8s-docs-service-2026-08-23]. That is the problem. Notice what it is *not*: it is not a failure mode, not a bug, not a degraded state to be recovered from. It is the normal condition of a system that replaces workloads freely.

A chart names the harbour, never the ships riding in it. That is exactly why the chart is still good next season.

The answer is an object.

A **Service** is a method for exposing a network application that is running as one or more Pods in your cluster. Each Service object defines a **logical set of endpoints** — usually those endpoints are Pods — along with a policy about how to make those Pods accessible [source: k8s-docs-service-2026-08-23]. The Service API lets you provide a **stable, long-lived** IP address or hostname for a service implemented by one or more backend Pods, where the individual Pods making up the service can change over time [source: k8s-docs-network-model-2026-08-23].

Read that last clause again. *Where the individual Pods making up the service can change over time.* The churn is not an inconvenience the Service copes with. The churn is the condition the Service exists for.

★ **Fixed Point:** A Service is a stable, long-lived address for a set of Pods **that is expected to change**. It is not a workaround for churn; it is the abstraction that makes churn a non-event.

How does a Service know which Pods? By a **selector**. Services most commonly abstract access to Kubernetes Pods thanks to the selector [source: k8s-docs-service-2026-08-23] — a query over labels, which is exactly what Chapter 4 told you a selector is, and exactly the mechanism Chapter 6 said a ReplicaSet uses to find its Pods. *[cross-bearing: see Ch 4 §7 — labels and selectors]*. Naming it now and leaving the machinery for §4 is the honest split, because Chapter 4 already told you a Service selects its backends this way. What §4 adds is where the query's answer gets *written down*.

And one fact about defaults, because it is cheap and it is examinable: **ClusterIP** exposes the Service on a cluster-internal IP, making it reachable only from within the cluster, and **it is the default that is used if you don't explicitly specify a type** [source: k8s-docs-service-2026-08-23]. §3 opens there and builds outward.

Before you go on, the correction that is worth more than anything else in this section:

> ⚓ **Worth Securing:** "A Service is a load balancer" is the most durable wrong model in Kubernetes networking, and it is wrong in a specific and useful way. A load balancer is *a thing that runs*: a process, on a machine, receiving your traffic and forwarding it. A Service is a **declaration that gets reconciled** — an object, in exactly the sense Chapter 4 established, stating that a set of Pods should be reachable at a stable address. Whether anything is listening, whether any Pod matches, whether traffic goes anywhere at all: none of that is the Service's doing, and none of it changes whether the Service exists. Almost every confusing thing in the next four sections follows from that distinction.

*[cross-bearing: see Ch 4 §4 — spec and status; a Service is an object like any other]*

---