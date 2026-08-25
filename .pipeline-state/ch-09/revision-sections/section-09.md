## ☆ Taking Your Bearings #1

Five questions on the model and the abstraction — §1 through §3. Two of them reach back to earlier chapters.

1. ⚪ A Pod on `worker-3` sends a request to a Pod on `worker-11`. What does the receiving Pod see as the source address, and what two things does the network model guarantee are *not* involved?

2. ⚪ **[retrieval: ch5]** A Pod runs two containers. One listens on 8080. Can the other also listen on 8080? How does each reach the other? And how many IP addresses does the Pod have?

3. 🔵 You create a Service with `type: NodePort`. A colleague says, "so now it's only reachable from outside — we lost the internal address." What is wrong with that, and why?

4. 🔵 **[retrieval: ch6]** Chapter 6 walked a Deployment through a rolling update. State what happens to the Pod IP addresses during that update, and then say what a Service gives a client that the Pod IPs cannot.

5. 🔵 Two Services. One has `type: LoadBalancer` and, twenty minutes after creation, still has no external address. One has `type: ExternalName` pointing at `api.vendor.example`. For each: what is Kubernetes doing, and is anything broken?

---

**Answers with Explanations:**

**1. The sending Pod's own IP address. Not involved: NAT (address translation), and proxies.**

The model states it directly — Pods can communicate with each other directly, without the use of proxies or address translation [source: k8s-docs-network-model-2026-08-23] — and that the guarantee holds whether the Pods are on the same node or different nodes [source: k8s-docs-network-model-2026-08-23].

*Why the tempting wrong answers are wrong:*
- **"The sending node's IP"** would be correct in almost any non-Kubernetes cluster, which is exactly why it's the trap. Node-to-node forwarding with source rewriting is the normal arrangement elsewhere. It is forbidden here.
- **"A translated address from the pod network's NAT pool"** assumes cross-node traffic must be translated. It must not be. §1's third rule forbids address translation between Pods outright [source: k8s-docs-network-model-2026-08-23], and that prohibition binds every plugin equally — whatever a plugin does internally to carry a packet from one node to another, the receiver still sees the sender's own address. Reason from the rule, not from a guess about how any particular plugin moves the bytes.

**2. No — they share one port space. Over `localhost`. One address.**

Every container in a Pod shares the network namespace, including the IP address and network ports; within a Pod, containers share an IP address and port space and can find each other via `localhost` [source: k8s-docs-pods-2026-08-24].

*Why the wrong answers are wrong:*
- **"Yes, they each get their own port space"** is the single-container mental model most people arrive with. Two containers in one Pod compete for ports exactly as two processes on one host do.
- **"Two addresses, one per container"** is the single most common Kubernetes networking misconception. One Pod, one address per address family.

**3. Nothing was lost. Requesting NodePort also allocates a cluster IP.**

To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP` [source: k8s-docs-service-2026-08-23].

Say the rule at the level of the ladder rather than as a fact about NodePort, because the shape is what makes the types easy to hold: **a type that adds reachability keeps what the type beneath it already provided.** The documentation states that shape explicitly for NodePort over ClusterIP [source: k8s-docs-service-2026-08-23]. Hold it in that form and you carry one rule instead of three separate facts — and Chapter 10's argument for Ingress — "one external address per Service, and that does not scale" — becomes available to you without further work.

<!-- AUTHOR-REVIEW: This answer previously read "LoadBalancer implies NodePort implies ClusterIP." The cached Service snapshot documents additivity for NodePort over ClusterIP only; its LoadBalancer entry is a single sentence describing external exposure and saying nothing about cluster IPs or node ports. The claim is narrowed here to the documented rung, pending the targeted re-fetch of kubernetes.io/docs/concepts/services-networking/service/ capturing the `type: LoadBalancer` subsection in full (routed to Stage 2 by the fact-accuracy audit as its highest-priority gap). When it lands, restore the full three-rung statement here and in §3's Fixed Point in one pass, so the checkpoint bullet below and the figure caption stay in agreement.

The same fetch covers answer 5's "Indefinitely." That a provider-less LoadBalancer Service waits forever follows from the cached "Kubernetes does not directly offer a load balancing component," but no cached snapshot describes the observable pending state, so the wording is left as the book's own entailment rather than presented as documented. -->

**4. Every Pod is replaced, and each replacement has a different address. A Service gives the client one address that does not change while the set behind it does.**

A Pod is replaced by a new, near-identical Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23]; §1's first rule gives that new Pod its own address. The Service API provides a stable, long-lived IP address or hostname for a service implemented by one or more backend Pods, where the individual Pods making up the service can change over time [source: k8s-docs-network-model-2026-08-23].

If you answered something like "the client breaks, and it wouldn't have if it were using something that doesn't move" — you have written §2's opening for yourself, which is the ideal outcome for this item.

**5. LoadBalancer: waiting for an external load balancer that nothing is providing. ExternalName: working exactly as designed, as a CNAME with no proxying. Neither is broken.**

Kubernetes does not directly offer a load balancing component; you must provide one, or integrate with a cloud provider [source: k8s-docs-service-2026-08-23]. A cluster with no such integration has nothing to act on the request, so the Service waits. Indefinitely, and correctly.

ExternalName maps the Service to the contents of the `externalName` field by configuring cluster DNS to return a CNAME record; no proxying of any kind is set up [source: k8s-docs-service-2026-08-23]. There is nothing further for it to do.

*Why the tempting wrong answers are wrong:*
- **"The LoadBalancer Service failed to provision"** treats absence of a provider as failure. The declaration is correct; the actor is missing.
- **"The ExternalName Service is proxying traffic to the vendor"** is the trap. It is not in the path at all.

This is a genuinely reasonable thing to be surprised by. Most people meet `type: LoadBalancer` on a managed cluster where it just works, and the first bare-metal cluster is where the assumption surfaces. That's a normal way to learn it.

---

**Checkpoint: You've Now Mastered**

✓ The four rules of the Kubernetes network model, and who implements them
✓ Why a Pod IP is not something a client can hold on to
✓ Four Service types, how the ladder is built, and which one isn't a rung on it at all
✓ That Kubernetes ships no load balancer

Next: the Service has a name and an address — a mark that holds position while everything behind it is replaced. Now find out what *is* behind it, and what a Pod has to do to get on the list.

---