## Exam Alert! 🚨

**High-Priority Topics**

1. **Every Pod gets a unique cluster-wide IP**, and all Pods reach all Pods **without NAT and without proxies** — same node or across nodes [source: k8s-docs-network-model-2026-08-23].
2. **The Pod holds the IP; its containers share it** and communicate over `localhost` [source: k8s-docs-pods-2026-08-24].
3. **ClusterIP is the default** Service type, and is reachable only from inside the cluster [source: k8s-docs-service-2026-08-23].
4. **NodePort also allocates a cluster IP** — the documentation is explicit that Kubernetes sets one up "the same as if you had requested a Service of type: ClusterIP" [source: k8s-docs-service-2026-08-23].
5. **Kubernetes does not provide a load balancer.** You supply one, or integrate with a cloud provider [source: k8s-docs-service-2026-08-23].
6. **ExternalName is a CNAME with no proxying of any kind** [source: k8s-docs-service-2026-08-23].
7. **`clusterIP: None` is deliberate** — DNS returns the Pod addresses directly [source: k8s-docs-service-2026-08-23].
8. **A Service without a selector is a supported pattern**, backed by manually managed EndpointSlices [source: k8s-docs-service-2026-08-23].
9. **`<service>.<namespace>.svc.<cluster-domain>`**, and a **bare name resolves in the local namespace only** [source: k8s-docs-dns-pod-service-2026-08-23] [source: k8s-docs-namespaces-2026-08-23].
10. **kube-proxy implements the virtual IP for every type except ExternalName**; **iptables is the default mode** [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].
11. **A Pod must be Ready to be an endpoint** [source: k8s-docs-pod-lifecycle-2026-08-23].
12. **Kubernetes defines the network model; a CNI network plugin implements it** [source: k8s-docs-extending-kubernetes-2026-08-23].

<!-- AUTHOR-REVIEW: two items narrowed relative to draft-v1, both awaiting fetches that §1 and §3 are also waiting on.

     (a) Item 4 previously read "the types are additive", which generalises the rule to LoadBalancer. The cached Service
     snapshot documents the cluster-IP allocation for NodePort only ("To make the node port available, Kubernetes sets up
     a cluster IP address, the same as if you had requested a Service of type: ClusterIP"); its LoadBalancer entry is a
     single sentence about external exposure and says nothing about the rungs beneath it. The general form is very likely
     correct but is not in the corpus. Restore it once the `type: LoadBalancer` subsection of
     kubernetes.io/docs/concepts/services-networking/service/ is cached in full. Same fetch resolves the "waits
     indefinitely" claim in §3.

     (b) Item 12 previously read "and implements none of it". The cited snapshot supports the positive half — CNI is
     listed among Kubernetes' infrastructure extension points "to implement pod networking" — but states no exclusive
     negative. This now mirrors §1's Fixed Point wording exactly, which is the form §1 already holds itself to. Restore
     the stronger claim, and the stronger normative form ("a CNI plugin is required"), when the network-plugins page
     fetch lands. The Dead Reckoning block in "Why This Chapter Matters" carries the same overreach and needs the same
     treatment. -->

---

**Common Traps** — every one of these is a documented mistake with a specific correct answer, which is to say every one is a hazard somebody has already run onto and marked. Don't let the wrong version be the one that's fresh when you sit down.

| The trap | The correction | Where it's defused |
|---|---|---|
| "Pods need NAT or a proxy to reach Pods on other nodes" | Direct, no NAT, no proxy — that's rule 3 | §1, Bearings #1 item 1 |
| "Each container in a Pod gets its own IP" | The **Pod** has the address; containers share it | §1 Snag, Bearings #1 item 2 |
| "NodePort replaces ClusterIP" | NodePort **also** allocates a cluster IP | §3 Fixed Point, Bearings #1 item 3 |
| "LoadBalancer means Kubernetes provides a load balancer" | It provides none. You supply one | §3 Fixed Point, Bearings #1 item 5 |
| "ExternalName proxies traffic" | CNAME only. No proxying of any kind | §3 Navigational Hazards, Bearings #1 item 5 |
| "A headless Service is a broken Service" | `clusterIP: None` is a value somebody typed | §5 Fixed Point, Bearings #2 item 4 |
| "A Service without a selector is invalid" | Supported pattern, used for external backends | §5, Bearings #2 item 5 |
| "A bare service name works across namespaces" | Local namespace only — and it may succeed *wrongly* | §7 Navigational Hazards, Bearings #3 item 4 |
| "Something is listening on the cluster IP" | Nothing is. It's a forwarding rule, not a socket | §6 Worth Securing, Bearings #3 item 2 |
| "kube-proxy is required" | Optional, if the plugin does equivalent forwarding | §6 Closer Look, Bearings #3 item 3 |
| "Headless Services have no DNS record" | Same name form; different answer | §7, Bearings #3 item 5 |
| "A Service with no endpoints is broken" | Correct Service; selector matches nothing, or Pods not Ready | §4 Snag, Bearings #2 item 3 |
| "A terminating Pod leaves the Service instantly" | Retained with `ready: false`, so traffic drains | §4 Closer Look |
| "Kubernetes ships the network" | It defines the *requirements*; a CNI plugin implements them | §1 Fixed Point |

**The most valuable one on that list** is "something is listening on the cluster IP." It has one clean correct answer, and that answer follows directly from what kube-proxy is documented to do — configure the node to *capture* traffic addressed to the Service's cluster IP and port, and *redirect* that traffic to one of the Service's endpoints [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Capture-and-redirect requires nothing bound to that address, which is exactly why nothing is bound to it. Believing the wrong version makes roughly half of Kubernetes networking incomprehensible — including several things Chapter 10 will assume you understand.

---