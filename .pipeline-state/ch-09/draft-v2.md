" | CNAME only. No proxying of any kind | §3 Navigational Hazards, Bearings #1 item 5 |
| "A headless Service is a broken Service" | `clusterIP: None` is a value somebody typed | §5 Fixed Point, Bearings #2 item 4 |
| "A Service without a selector is invalid" | Supported pattern, used for external backends | §5, Bearings #2 item 5 |
| "A bare service name works across namespaces" | Local namespace only — and it may succeed *wrongly* | §7 Navigational Hazards, Bearings #3 item 4 |
| "Something is listening on the cluster IP" | Nothing is. It's a forwarding rule, not a socket | §6 Worth Securing, Bearings #3 item 2 |
| "kube-proxy is required" | Optional, if the plugin does equivalent forwarding | §6 Closer Look, Bearings #3 item 3 |
| "Headless Services have no DNS record" | Same name form; different answer | §7, Bearings #3 item 5 |
| "A Service with no endpoints is broken" | Correct Service; selector matches nothing, or Pods not Ready | §4 Snag, Bearings #2 item 3 |
| "A terminating Pod leaves the Service instantly" | Retained with `ready: false`, so traffic drains | §4 Closer Look |
| "The endpoints controller and the EndpointSlice controller are two components" | Two names in the docs for one job | §4 Mnemonic |
| "Kubernetes ships the network" | It ships the *requirements*; a CNI plugin implements them | §1 Fixed Point |

**The most valuable one on that list** is "something is listening on the cluster IP." It has one clean correct answer, it is stated plainly in the documentation, and believing the wrong version makes roughly half of Kubernetes networking incomprehensible — including several things Chapter 10 will assume you understand.

---

## Practice Questions

Twenty-two questions. Five of them draw on earlier chapters and are tagged. One is short answer; the rest are multiple choice. Answers and explanations follow the full set — attempt them all before looking.

---

**1.** Which of the following is required by the Kubernetes network model?

A) Pods communicate across nodes through a NAT gateway maintained by the kubelet
B) All Pods can communicate with all other Pods, on the same node or on different nodes, without proxies or address translation
C) Each container in a Pod receives its own cluster-wide IP address
D) Pods on different nodes communicate via the node's external IP and a mapped port

---

**2.** A Pod is running three containers. **[retrieval: ch5]** How many IP addresses does the cluster allocate for that Pod, and how many entries would that Pod contribute to a matching Service's EndpointSlice?

A) Three addresses, three entries
B) Three addresses, one entry
C) One address, three entries
D) One address, one entry

---

**3.** Which statement about CNI is correct?

A) CNI is the Kubernetes-built-in networking implementation, enabled by default
B) CNI is the interface through which a network plugin implements Pod networking; the plugin is an external binary rather than code compiled into Kubernetes
C) CNI is a Kubernetes API object you create to define a Pod network
D) CNI is the protocol kube-proxy uses to program iptables rules

---

**4.** A Service is created with no `type` field specified. What type is it, and from where is it reachable?

A) NodePort; from any node's IP at a static port, with no cluster IP allocated
B) ClusterIP; from inside the cluster only
C) ClusterIP; from inside the cluster and from any node's IP
D) LoadBalancer; from wherever the provider's load balancer is reachable

---

**5.** You change a Service from `type: ClusterIP` to `type: NodePort`. What happens to the cluster IP?

A) It is released, since NodePort replaces it
B) It is retained — Kubernetes sets up a cluster IP for NodePort Services as well
C) It is retained but becomes unreachable from inside the cluster
D) It is replaced by the node's IP address

---

**6.** Your team runs Kubernetes on bare metal with no cloud-provider integration and no load-balancer add-on installed. You create a `type: LoadBalancer` Service. What happens?

A) Kubernetes provisions a software load balancer on one of the nodes
B) The Service is rejected at admission with a validation error
C) The Service is created and waits for an external address that nothing is going to supply; nothing is broken
D) The Service silently falls back to `type: NodePort`

---

**7.** You need clients inside the cluster to reach `analytics.vendor.example`, a SaaS endpoint outside the cluster, using an in-cluster name. Which Service configuration produces a CNAME with Kubernetes entirely out of the traffic path?

A) `type: ClusterIP` with no selector and manually created EndpointSlices
B) `type: ExternalName` with `externalName: analytics.vendor.example`
C) `type: LoadBalancer` with an annotation naming the vendor
D) A headless Service with `externalName` set

---

**8.** Two Services in namespace `prod`. `db-a` is an ordinary Service with three Ready backends. `db-b` has `.spec.clusterIP` set to `None`, with the same three backends. A client resolves `db-a.prod.svc.cluster.local` and then `db-b.prod.svc.cluster.local`. What differs between the two names, and what differs between the two answers?

A) The headless Service's name takes a different form — `db-b.prod.headless.cluster.local` — and both resolve to a single address
B) The names are identical in form; `db-a` resolves to the Service's cluster IP, and `db-b` resolves to the set of IPs of all the Pods it selects
C) The names are identical in form; both resolve to a cluster IP, and the headless Service's is simply allocated later
D) The headless Service is assigned no DNS record at all, so the second lookup fails

---

**9.** **[retrieval: ch4]** A Pod carries labels that a ReplicaSet selects on and labels that a Service selects on. Someone edits one of those labels. Name both consequences, and say whether the two controllers coordinate.

A) The Pod leaves both sets simultaneously; the controllers coordinate through the owner reference
B) Only the ReplicaSet is affected; Services select on owner references, not labels
C) Each selector is evaluated on its own, so the Pod may drop out of either set, both, or neither, with no coordination between the controllers
D) Nothing happens until the Pod is restarted, at which point both selectors re-evaluate

---

**10.** Where does Kubernetes record the set of Pods currently backing a Service, and what writes it?

A) In the Service's `status` field, written by kube-proxy
B) In EndpointSlice objects, written by the EndpointSlice controller
C) In the Pods' annotations, written by the kubelet
D) In cluster DNS, written by CoreDNS

---

**11.** **[retrieval: ch5]** Chapter 5 said a readiness probe controls whether a Pod receives traffic. Name the object that fact is actually implemented in, and say what a failing probe changes about it.

A) The Pod's `status.phase`; a failing probe moves the Pod to `Failed`
B) The Service's `spec.selector`; a failing probe removes the Pod's labels from it
C) The EndpointSlice; a failing probe removes the Pod's address from the Service's endpoints
D) The node's iptables rules; a failing probe causes kube-proxy to drop packets to the Pod

---

**12.** `kubectl get endpointslices -l kubernetes.io/service-name=web` returns a slice with no endpoints. The Pods you expect are Running. What are the two usual causes?

A) kube-proxy is not running, or the CNI plugin is misconfigured
B) The Service's selector does not match the Pods' labels, or the Pods are not Ready
C) Cluster DNS has not yet published the Service's record, or the Pods' readiness probes have not run for the first time
D) The Pods are in a different namespace from the Service, or the Service was created before the Pods existed

---

**13.** A colleague reports: "I created the Service, it has a cluster IP and a DNS record, but nothing responds and there are zero endpoints." What is the correct characterisation?

A) The Service failed to create properly and should be deleted and recreated
B) Nothing is wrong with the Service — it is being reconciled correctly against a set that is currently empty
C) The API server rejected the selector and defaulted it to empty
D) The DNS record proves the Service works; the problem must be in the client

---

**14.** A Service is created with `.spec.clusterIP` set to `None`. What does that setting do?

A) It releases the Service's cluster IP after allocation, leaving the Service in a degraded state
B) It makes the Service reachable only from inside the cluster — which is what the ClusterIP type already does
C) It creates a headless Service: no single virtual IP is allocated, and DNS returns the addresses of the Pods the Service selects
D) It reserves the Service's name without allocating any endpoints

---

**15.** You are migrating a database into the cluster. Today it runs on external hardware; next month it will run as Pods. You want in-cluster clients to use one unchanging Service name throughout, with traffic proxied by the cluster in both phases. What do you configure today?

A) A `type: ExternalName` Service pointing at the database's hostname
B) A headless Service with no selector
C) A Service with no selector, plus manually managed EndpointSlices holding the external address
D) A `type: ExternalName` Service today, replaced by an ordinary selector-based Service on migration day

---

**16.** kube-proxy's modes on Linux are:

A) userspace (default), iptables, IPVS
B) iptables (default), IPVS, nftables
C) iptables, IPVS (default), eBPF
D) nftables (default), iptables, kernelspace

---

**17.** An engineer SSHes to a worker node and runs `ss -tlnp` looking for a process bound to a Service's cluster IP. What will they find, and why?

A) kube-proxy, because it terminates connections to cluster IPs and forwards them
B) One of the backend Pods, because kube-proxy binds the cluster IP to a chosen endpoint
C) Nothing — the cluster IP is virtual, existing only as a rule that captures and readdresses traffic
D) CoreDNS, because it owns all cluster-internal addresses

---

**18.** Your cluster is running normally, serving traffic to Services, and no kube-proxy is running on any node. What is happening, and which of §1's four rules is the same component also satisfying?

A) The cluster is broken and Services are failing silently; no rule is being satisfied
B) The network plugin implements Service packet forwarding itself — and the same plugin implements the Pod network, satisfying the rule that all Pods can reach all Pods directly
C) The control plane is proxying Service traffic through the API server; rule 4, node-agent reachability
D) Services are being resolved by DNS to Pod IPs directly, bypassing the need for a proxy; rule 1, unique Pod addresses

---

**19. Short answer.** A Pod in namespace `billing` must reach a Service named `ledger` that lives in namespace `payments`.

(a) Write the DNS name it should use for an ordinary address lookup.
(b) That Service exposes a named port `http` over TCP. Write the SRV name for that port.
(c) In one sentence, say what would happen if the Pod used the bare name `ledger`.

---

**20.** **[retrieval: ch6]** A StatefulSet runs three Pods behind a headless Service named `zk` in namespace `prod`. A client resolves `zk.prod.svc.cluster.local` and gets three addresses; it now needs to reach one specific member. Which component answered that lookup, and what form does an individual member's name take?

A) kube-proxy answered, and members are addressed as `<pod-ip>.prod.pod.cluster.local`
B) CoreDNS answered, and each Pod gets a DNS subdomain of the form `$(podname).$(governing service domain)`
C) The API server answered, and individual members are reachable only by raw Pod IP
D) CoreDNS answered, but a headless Service publishes no per-member names — the Pod-by-address record is the only option

---

**21.** **[retrieval: ch4]** Chapter 4 told you a bare service name resolves within the local namespace. What makes that true — what is configured, and by which component?

A) CoreDNS rewrites bare queries to the caller's namespace, using the caller's source IP
B) The Pod's DNS search list contains its own namespace and the cluster's default domain, configured by the kubelet
C) The API server rejects cross-namespace DNS queries unless an FQDN is used
D) kube-proxy scopes DNS traffic per namespace using iptables rules

---

**22.** A colleague describes a Kubernetes networking behaviour this book has not covered and asks how it works. You do not know the specific answer. Using this chapter's synthesis rather than a remembered fact, which pair of questions gets you closest, fastest?

A) "Which node is it on, and is kube-proxy healthy there?"
B) "What does the selector currently match, and which control loop hasn't caught up yet?"
C) "What does the Service's `status` field say, and has DNS propagated?"
D) "Which Service type is it, and does the cluster have a cloud provider?"

---

**Answers with Explanations**

---

**1. B.**

All Pods can communicate with all other Pods, whether on the same node or on different nodes, and Pods can communicate with each other directly, without the use of proxies or address translation [source: k8s-docs-network-model-2026-08-23].

**A** describes a NAT gateway — explicitly forbidden by rule 3. **C** is the each-container-gets-an-IP misconception; every container in a Pod shares the network namespace including the IP address and network ports [source: k8s-docs-pods-2026-08-24]. **D** describes host-port mapping, which is the model Kubernetes replaces; it would be the correct answer for almost any non-Kubernetes container platform, which is precisely why it's attractive.

**2. D. One address, one entry.**

Each Pod is assigned a unique IP address for each address family, and every container in a Pod shares the network namespace including the IP address [source: k8s-docs-pods-2026-08-24]. An EndpointSlice records the Pods currently backing a Service [source: k8s-docs-network-model-2026-08-23] — Pods, not containers.

This is the each-container-gets-an-IP misconception tested at its downstream consequence rather than at its definition. **A** and **B** both assume per-container addressing; **C** assumes per-container endpoints. If you can see that container count and endpoint count are unrelated numbers, the trap has nothing left to catch you with.

**3. B.**

Network plugins use CNI, the Container Network Interface, to implement pod networking, and CNI network plugins are binary plugins — external programs rather than code compiled into Kubernetes [source: k8s-docs-extending-kubernetes-2026-08-23].

**A** inverts the relationship — CNI is an interface, not an implementation. **C** invents an API object; there is no `kind: CNI`. **D** confuses two unrelated components: kube-proxy programs node rules via OS APIs, and has nothing to do with CNI.

**4. B.**

ClusterIP exposes the Service on a cluster-internal IP, makes it reachable only from within the cluster, and is the default used if you don't explicitly specify a type [source: k8s-docs-service-2026-08-23].

**A** is wrong twice over. NodePort is never a default — it must be requested — and requesting it does not skip the cluster IP: Kubernetes sets one up for a NodePort Service as well [source: k8s-docs-service-2026-08-23]. That second clause is trap "NodePort replaces ClusterIP" wearing a different hat.

**C** is the near-miss worth naming: ClusterIP alone does *not* expose anything on node IPs. That is what NodePort adds — and the relationship runs one way only. Getting a cluster IP from NodePort is guaranteed; getting node reachability from ClusterIP is not.

**D** is never a default either, and it is the one type that cannot function without a component Kubernetes does not ship: Kubernetes does not directly offer a load balancing component [source: k8s-docs-service-2026-08-23]. A "default" that only works on some clusters would be a strange default.

**5. B.**

To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP` [source: k8s-docs-service-2026-08-23].

**A** is the trap in its purest form — the belief that types are alternatives rather than layers. **C** invents a restriction. **D** confuses an address with a reachability mechanism: the node IPs are *additional* paths, not a substitute address.

**6. C.**

Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider [source: k8s-docs-service-2026-08-23]. With neither present, nothing is watching for the request, so nothing acts on it.

**A** is the trap. **B** is wrong because the object is entirely valid — validity and effect are different questions. **D** invents a fallback that would be surprising and undocumented behaviour.

Note that the Service still has a cluster IP, so it is fully usable from inside the cluster. Only the external address is missing.

**7. B.**

ExternalName produces a CNAME and no proxying [source: k8s-docs-service-2026-08-23], so the client connects directly to the vendor.

**A** would also work as a way to reach the vendor, but it puts kube-proxy in the path — traffic goes to a cluster IP and is redirected [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23] — which is exactly what the question excludes. **C** and **D** are invented configurations; `externalName` is meaningful only with `type: ExternalName`.

**8. B.**

Normal Services are assigned A and/or AAAA records with a name of the form `my-svc.my-namespace.svc.cluster-domain.example`, resolving to the cluster IP; headless Services are assigned records **with the same name form**, resolving instead to the set of IPs of all of the Pods selected by the Service [source: k8s-docs-dns-pod-service-2026-08-23]. `db-b` is headless because `.spec.clusterIP` is `"None"` [source: k8s-docs-service-2026-08-23].

*Why the wrong answers are wrong:*
- **A** invents a name form. There is no `headless` label; the literal in position 3 is `svc` for both Services, and nothing anywhere in the name announces that one of them is headless. That is the whole point of the item.
- **C** is the trap for anyone who read §5 and took "headless" to mean the cluster IP is delayed rather than declined. `None` is a value somebody typed; no address is ever allocated, and none arrives later.
- **D** is the "headless Services have no DNS record" trap. They have a record. It is the *answer* that differs — one address versus the whole set.

This is the item that pairs §3's types with §7's records, and neither section alone gets you there: from §3 you know what `clusterIP: None` is, and from §7 you know that knowing it changes nothing about the name you type.

**9. C.**

A Service uses labels to allow the control plane to determine which EndpointSlice objects are used for it [source: k8s-docs-garbage-collection-2026-08-24], and a selector is a query over labels. Two controllers evaluating two selectors against one Pod produce two independent results.

**A** confuses ownership with selection — the two mechanisms are explicitly distinguished, and owner references exist so different parts of Kubernetes avoid interfering with objects they don't control [source: k8s-docs-garbage-collection-2026-08-24].

**B** is wrong twice. First, a Service determines its EndpointSlices by *labels*, not by owner references [source: k8s-docs-garbage-collection-2026-08-24] — owner references govern cleanup, not membership. Second, the ReplicaSet is not privileged over the Service in any way; both are ordinary selector evaluations run by ordinary controllers, and neither has standing the other lacks.

**D** invents a restart trigger; selectors are evaluated continuously by watching controllers, not at Pod startup.

**10. B.**

Kubernetes automatically manages EndpointSlice objects to provide information about the Pods currently backing a Service [source: k8s-docs-network-model-2026-08-23]; the EndpointSlice controller populates them to provide a link between Services and Pods [source: k8s-docs-cluster-architecture-2026-08-23].

**A** puts the answer in the wrong object and names the wrong writer — kube-proxy *reads* EndpointSlices [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

**C** puts the answer on the wrong object and names a component that never participates. The kubelet reports a Pod's own status; endpoint membership is computed centrally by a controller reading the API, not written per-Pod by each node. This matters practically as well as conceptually — it is why both of §4's empty-endpoint causes live in the control plane rather than on a node.

**D** confuses a publisher with a source of truth: DNS publishes the answer; it does not compute it.

**11. C.**

If a readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod [source: k8s-docs-pod-lifecycle-2026-08-23]; a Pod's `Ready` condition means it should be added to the load balancing pools of all matching Services [source: k8s-docs-pod-termination-2026-08-24].

**A** is a real and important distinction: a failing readiness probe does *not* change the Pod's phase, kill it, or restart it. That's the liveness probe's job. The Pod keeps running, keeps being counted by its controller, and simply stops receiving traffic. **B** would mean readiness edits your Service, which it does not. **D** describes a downstream effect (kube-proxy reprograms rules because the slice changed) as though it were the mechanism.

**12. B.**

If the endpoints don't match the Pods you expect, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready [source: k8s-docs-debug-pods-2026-08-23].

*Why the tempting wrong answers are wrong:*
- **A** names data-plane components, but endpoint membership is computed entirely in the control plane by a controller reading the API. Neither kube-proxy nor the CNI plugin can empty a slice — kube-proxy reads the slice [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23], it does not write it. This is the designed trap: a networking symptom with two non-networking causes.
- **C** is the closest wrong answer, and it is wrong in two different ways at once. Its second clause is not a separate cause — "probes have not run yet" is one specific way of being *not Ready*, so it collapses into half of B rather than adding anything. Its first clause names a component that plays no part in computing endpoints at all; DNS publishes the Service's address whether the slice is full or empty, which is exactly why Q13's colleague has a DNS record and no traffic.
- **D** pairs one real cause with one imaginary one. Pods in a different namespace genuinely will not be selected — a Service's selector is scoped to its own namespace — so half of D is a live possibility. But the second clause is not: a Service created before its Pods works fine, because the EndpointSlice controller is a control loop that keeps watching, not a one-shot evaluation at creation time. Both halves must hold for the pair to be "the two usual causes," and the ordering half never does.

**13. B.**

The Service has an address and a DNS record because those are allocated on creation, independent of whether any Pod matches. The EndpointSlice is empty because the selector's current answer is the empty set — which the controller has computed correctly.

**A** is the instinct to fix by recreation, and it will produce an identical Service with an identical empty slice. **C** invents an API server behaviour. **D** is the reasoning error worth naming: the presence of a name and an address proves that *reconciliation is happening*, not that it found anything.

This is the second instance in the chapter of the same shape — a valid object whose effect depends on something that isn't there. Chapter 10 gives it a name.

**14. C.**

You create headless Services by explicitly specifying `"None"` for `.spec.clusterIP`; for headless Services with selectors, DNS returns A or AAAA records pointing directly to the Pods [source: k8s-docs-service-2026-08-23].

*Why the wrong answers are wrong:*
- **A** treats `None` as an absence rather than a value, and invents a two-step allocate-then-release mechanism that does not exist. No address is ever allocated.
- **B** confuses two independent axes. "Reachable only from inside the cluster" is the *type* ladder — that is ClusterIP's definition [source: k8s-docs-service-2026-08-23] — and it has nothing to do with whether a single virtual IP exists. A headless Service and an ordinary ClusterIP Service are both internal-only; they differ in how many addresses DNS hands back.
- **D** describes something Kubernetes has no concept of. Endpoints are computed from the selector; a headless Service *with* a selector gets EndpointSlices created for it exactly as a normal one does [source: k8s-docs-service-2026-08-23].

Note that this question deliberately tests only what the setting does. The workload that requires it is a separate fact, tested at Q20.

**15. C.**

A Service used with a corresponding set of EndpointSlice objects and without a selector can abstract other kinds of backends, including ones that run outside the cluster — an external database, or a workload being migrated [source: k8s-docs-service-2026-08-23].

**A** would give clients the vendor hostname directly, meaning that when you migrate you must change what clients resolve *and* the connection semantics change — no proxying today, proxying tomorrow. The question specifically asks for proxying in both phases. **B** removes the single address, which the clients want.

**D** is the answer many practitioners would actually propose, which is why it earns a place here — and it fails the stated requirement for a specific reason. Under ExternalName the client connects directly to the external host with Kubernetes out of the path [source: k8s-docs-service-2026-08-23]; under a selector-based Service it connects to a cluster IP and is redirected [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Swapping one for the other changes what the client's connection actually is — TLS names, source addresses, everything downstream of the connection — and makes migration day a visible cutover rather than an invisible one. C is invisible.

The migration itself, in outline: add the selector, remove the manually managed EndpointSlices. Clients notice nothing.

**16. B.**

On Linux, the available modes are iptables (the default), IPVS, and nftables (GA since Kubernetes 1.33); on Windows there is only kernelspace [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

**A** names `userspace`, which is not among the documented Linux modes — and mislabels it as the default besides. **C** mislabels the default and lists eBPF, which is a plugin data plane rather than a kube-proxy mode. **D** mislabels the default and places the Windows-only mode in the Linux list.

**17. C.**

kube-proxy configures the node to capture traffic to the Service's `clusterIP` and port and redirect it to one of the Service's endpoints [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Capture-and-redirect is not the same as listen-and-forward. Nothing binds the address.

**A** and **B** both assume something terminates the connection at the cluster IP. **D** confuses DNS with addressing entirely — CoreDNS answers name queries; it owns no addresses.

**18. B.**

If you use a network plugin that implements packet forwarding for Services by itself, providing equivalent behavior to kube-proxy, you do not need to run kube-proxy [source: k8s-docs-cluster-architecture-2026-08-23]; Cilium can act as a replacement [source: k8s-docs-cluster-addons-2026-08-24]. And the plugin implementing Service forwarding is the same plugin implementing Pod networking via CNI [source: k8s-docs-extending-kubernetes-2026-08-23] — so it is also satisfying the model's requirement that all Pods reach all Pods directly [source: k8s-docs-network-model-2026-08-23].

**A** assumes kube-proxy's absence is a defect. **C** invents API-server proxying. **D** describes headless-Service behaviour and generalises it to every Service, which is wrong for anything with a cluster IP.

**19.**

**(a)** `ledger.payments.svc.cluster.local`

Four labels in fixed order: the Service's name, the namespace it lives in, the literal `svc`, and the cluster domain [source: k8s-docs-dns-pod-service-2026-08-23] [source: k8s-docs-namespaces-2026-08-23].

**(b)** `_http._tcp.ledger.payments.svc.cluster.local`

SRV records are created for named ports on normal or headless Services, with the form `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example` [source: k8s-docs-dns-pod-service-2026-08-23]. Two things to check yourself on: the leading underscores on *both* prefixed labels, and the fact that the Service's own four labels survive intact underneath. The SRV name is the A-record name with two labels bolted on the front, not a different name.

**(c)** It would resolve within `billing` only — either failing outright, or, if `billing` happens to contain a Service also called `ledger`, succeeding against the wrong one with no error reported anywhere [source: k8s-docs-namespaces-2026-08-23].

*Give yourself partial credit honestly.* The most common misses on this item are reversing labels 1 and 2, dropping the literal `svc`, and writing `_http.tcp.` with only one underscore. All three produce a name that looks plausible and resolves to nothing.

**20. B.**

CoreDNS is the cluster DNS addon that serves these records [source: k8s-docs-dns-pod-service-2026-08-23], launched automatically as a built-in addon [source: k8s-docs-dns-cluster-addon-2026-08-24]. A StatefulSet can use a headless Service to control the domain of its Pods, and as each Pod is created it gets a matching DNS subdomain of the form `$(podname).$(governing service domain)` [source: k8s-docs-statefulset-2026-08-24] — which is what "the headless Service is responsible for the network identity of the Pods" [source: k8s-docs-statefulset-2026-08-24] actually cashes out to.

*Why the wrong answers are wrong:*
- **A** names the wrong component for a DNS answer — kube-proxy programs forwarding rules and never answers a name query [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23] — and then offers the Pod-by-address record, whose form is real but whose position 3 is `pod`, not `prod.pod` as written, and which is keyed to the Pod's *address*, not its identity. An address-keyed name is precisely what a StatefulSet member needs not to depend on.
- **C** puts the API server in the DNS path, where it has no role, and denies the per-member name the StatefulSet documentation states outright.
- **D** gets the component right and the consequence wrong, which makes it the best distractor here. The Pod-by-address record does exist [source: k8s-docs-dns-pod-service-2026-08-23] — but it is not the only option, and it is the wrong one: it changes whenever the Pod's address changes, which defeats the stable identity the StatefulSet exists to provide.

**21. B.**

By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain [source: k8s-docs-dns-pod-service-2026-08-23], and the kubelet configures Pods' DNS so that running containers can look up Services by name [source: k8s-docs-dns-pod-service-2026-08-23].

**A** would be a plausible design and is not the one used; the behaviour is ordinary DNS search-domain resolution on the *client* side, not rewriting on the server side. **C** invents an API server role in DNS. **D** invents a kube-proxy role in DNS.

Converting the rule into a mechanism is the point of this item. Once you know it's a search list, the cross-namespace failure mode stops being arbitrary: the caller's own namespace is tried, a same-named local Service is found, and the lookup stops there — silently.

**22. B.**

This is the only item in the set that tests the method rather than a fact, and the method is §8's: a Service is a label query with a name, and everything else is a control loop publishing that query's current answer. So the two questions that generalise are *what is the query's answer right now* and *which consumer of that answer is behind*. Between them they cover the endpoint list, the node rules, and the DNS record — which is all three consumers — and both are answerable with `kubectl` in under a minute.

*Why the wrong answers are wrong:*
- **A** treats the data plane as the place where truth lives. Endpoint membership is computed in the control plane by a controller reading the API [source: k8s-docs-cluster-architecture-2026-08-23]; a healthy kube-proxy faithfully programming an empty slice looks exactly like a broken one.
- **C** contains two separate errors from the chapter's trap list. The Service does not store its backends — a separate object does [source: k8s-docs-network-model-2026-08-23] — and DNS is a publisher of the answer, not the answer itself. Q13's colleague had a perfectly good DNS record and zero endpoints.
- **D** is a question about one specific fact rather than a method. It is useful for exactly one of the four types, and tells you nothing at all about the other three.

If you picked A or C, that is worth noticing rather than glossing: both are the instincts of someone who has learned the components without the shape they share. Re-read §8's opening walk-back before Chapter 10, which assumes the shape.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **Network model** | Four rules: unique cluster-wide Pod IP; all Pods reach all Pods; **no NAT, no proxies**; node agents reach local Pods |
| **Pod IP** | Belongs to the **Pod**. Containers share it and use `localhost` |
| **CNI** | Kubernetes **defines** the model; a **plugin implements** it. One of the pluggable interfaces this book collects — the second, after CRI |
| **Service** | A stable, long-lived address for a set of Pods **that is expected to change**. An object, not a running thing |
| **ClusterIP** | The **default** type. Inside the cluster only |
| **NodePort** | Every node's IP at a static port — **and also a cluster IP** |
| **LoadBalancer** | Externally exposed by a load balancer **Kubernetes does not supply**. You provide one, or your cloud provider does |
| **ExternalName** | A **CNAME**. Not on the ladder. **No proxying of any kind** |
| **Selector** | The **question**. A query over Pod labels |
| **EndpointSlice** | The **written-down answer**, maintained by the EndpointSlice controller (the Service page calls it the endpoints controller — one job, two names) |
| **Readiness** | The **gate**. Matching the selector is necessary and not sufficient |
| **Empty endpoints** | Selector mismatch, **or** Pods not Ready. Two bugs, two files |
| **Headless** | `clusterIP: None` — deliberate. DNS returns the Pod addresses. StatefulSets need one |
| **No selector** | Supported. Manually managed EndpointSlices, for backends outside the cluster |
| **kube-proxy** | Virtual IP for **every type but ExternalName**. Watches Service + EndpointSlice. **iptables is the default** |
| **Cluster IP** | **Virtual.** Nothing is listening on it. It is a rule, not a socket |
| **Service DNS** | `<service>.<namespace>.svc.<cluster-domain>` — cluster IP for normal, **all Pod IPs for headless** |
| **Bare name** | **Local namespace only**, because that namespace is in the Pod's DNS search list. May succeed against the wrong Service |
| **The Zenith** | A Service is a **label query with a name**. Three loops publish its answer in three formats |

---

🏆 **Safe Harbor** — the Networking competency of Domain 2, complete as far as this book allocates it.

You arrived at this chapter able to run workloads and unable to connect them. You now know what guarantees the cluster network makes, what a Service actually is, how its backends are computed and gated, what programs the node, and what the client types. Chapter 10 carries the rest of the competency — NetworkPolicy, Ingress, the Gateway API — and Chapter 17 carries the service-mesh end of it. The reckoning from here on is kept in names, not addresses.

<!-- AUTHOR-REVIEW: two book-level bookkeeping items surfaced by the curriculum audit, neither editable from inside this chapter. (1) outline.md `kb_tags.commands` declares `kubectl-get-services` and `kubectl-describe-service`; neither appears in this draft, correctly — Stage 2 Gaps #2 records that no cached page shows either with output, and none may be invented. Trim the tags or accept the absence explicitly, so the book-level objective map does not over-report coverage. (2) Record the Networking-competency split in the book-level objective map: Ch 9 = model, Services, EndpointSlice, service proxy, DNS; Ch 10 = NetworkPolicy, Ingress, Gateway API; Ch 17 = service mesh. Today the split exists only in prose cross-bearings, so a later restructure could orphan one. -->

**Voyage Progress:** 🗺️ → 🌊 **Ch 9 of 17** → 🌅

---

## The Voyage Ahead

Everything you just learned works inside a boundary.

Every name resolved to something in the cluster. Every address was reachable by things already in. NodePort and LoadBalancer reach outward, but only by *opening a door* — a port on every node, an address from a provider. Neither of them knows or cares what comes through it. They move packets to a Service, and the Service moves them to a Pod, and at no point does anything inspect what is actually being asked for.

That's the ceiling §3 named. One external address per Service, which does not scale past a handful. No protocol awareness at all, so `shop.example.com/checkout` and `shop.example.com/catalog` are indistinguishable to every mechanism in this chapter.

Chapter 10 crosses the boundary. It introduces the objects that route on the *contents* of an HTTP request — hostnames, paths, headers — so that one address can serve many services. It explains why the Kubernetes project now recommends one API over the one most people learned first, and what "frozen" means in that recommendation, which is a more precise word than it looks and worth exactly the attention you'd give a definition on an exam. And it introduces NetworkPolicy, which is what rule 2's *"barring intentional network segmentation"* was quietly gesturing at all along.

It also opens with a Service that you create, and that does nothing at all — because the component that acts on it has not been installed. You have seen that shape twice in this chapter now. Chapter 10 gives it a name, and once a thing has a name you start seeing it on every watch.

> *"You do not need to know where a thing lies. You need its name, and a watch you trust to keep the reckoning current."*
> — Lodestar Ledgers