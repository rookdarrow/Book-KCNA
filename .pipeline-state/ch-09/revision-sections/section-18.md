## Practice Questions

Twenty-two questions. Four of them draw on earlier chapters and are tagged; one is deliberately not multiple choice. Answers and explanations follow the full set — attempt them all before looking.

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
B) CNI is the interface through which a network plugin implements Pod networking; the plugin is an external binary rather than a Kubernetes component
C) CNI is a Kubernetes API object you create to define a Pod network
D) CNI is the protocol kube-proxy uses to program iptables rules

---

**4.** A Service is created with no `type` field specified. What type is it, and from where is it reachable?

A) NodePort; from any node's IP at a static port
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
C) The Service is created and waits indefinitely for an external address; nothing is broken
D) The Service silently falls back to `type: NodePort`

---

**7.** A Service resolves to `api.vendor.example`, and a client Pod connects to it successfully. An engineer runs a packet capture on the node, expecting to find the connection matched by a kube-proxy rule, and finds no rule for that Service at all. Which type is the Service, and why is there no rule to capture?

A) NodePort — a NodePort Service surrenders its cluster IP, so kube-proxy has no address left to program a rule against
B) ClusterIP — kube-proxy programs rules only for Services that are reachable from outside the cluster
C) ExternalName — it is implemented purely as a DNS CNAME, and kube-proxy's virtual-IP mechanism covers every type except this one
D) LoadBalancer — the provider's load balancer handles the traffic, so no node-level rule is needed

---

**8.** You need clients inside the cluster to reach `analytics.vendor.example`, a SaaS endpoint outside the cluster, using an in-cluster name. Which Service configuration produces a CNAME with Kubernetes entirely out of the traffic path?

A) `type: ClusterIP` with no selector and manually created EndpointSlices
B) `type: ExternalName` with `externalName: analytics.vendor.example`
C) `type: LoadBalancer` with an annotation naming the vendor
D) A headless Service with `externalName` set

<!-- AUTHOR-REVIEW: the curriculum-alignment audit (R5/R7) asks for one further §3 item on Service port mechanics — `port` / `targetPort` / `nodePort` and the `--service-node-port-range` default. It is not written, because the snapshot that would source it (`k8s-docs-service-ports-2026-08-24`) does not exist in ../Book-KCNA/sources/ — Stage 2 fetched it but could not write it, and its body survives only inside research-manifest.md §3. The §3 prose carries the matching AUTHOR-REVIEW block for the same reason. Add the question here, after Q8, once R1 lands the snapshot and §3 teaches the fields. -->

---

**9.** **[retrieval: ch4]** A Pod carries labels that a ReplicaSet selects on and labels that a Service selects on. Someone edits one of those labels. Name both consequences, and say whether the two controllers coordinate.

A) The Pod leaves both sets simultaneously; the controllers coordinate through the owner reference
B) Only the ReplicaSet is affected; Services select on owner references, not labels
C) Each selector is evaluated independently, so the Pod may drop out of either set, both, or neither
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
C) The Service's DNS record has not propagated yet, or the slice you fetched is a stale cached read
D) The Pods are in a different namespace from the Service, or the Service was created before the Pods existed

---

**13.** A colleague reports: "I created the Service, it has a cluster IP and a DNS record, but nothing responds and there are zero endpoints." What is the correct characterisation?

A) The Service failed to create properly and should be deleted and recreated
B) Nothing is wrong with the Service — it is being reconciled correctly against a set that is currently empty
C) The API server rejected the selector and defaulted it to empty
D) The DNS record proves the Service works; the problem must be in the client

---

**14.** What does setting `.spec.clusterIP` to `None` do, and which workload type requires it?

A) Reserves the Service's name in DNS without allocating any endpoints; required by CronJobs
B) Makes the Service reachable only from inside the cluster, with no external path; required by StatefulSets for Pod network identity
C) Creates a headless Service — DNS returns the Pod addresses directly instead of one virtual IP; required by StatefulSets for Pod network identity
D) Removes the Service's selector, so its endpoints must be maintained by hand; required by Deployments with more than one replica

---

**15.** You are migrating a database into the cluster. Today it runs on external hardware; next month it will run as Pods. You want in-cluster clients to use one unchanging Service name throughout, with traffic proxied by the cluster in both phases. What do you configure today?

A) A `type: ExternalName` Service pointing at the database's hostname
B) A headless Service with no selector
C) A Service with no selector, plus manually managed EndpointSlices holding the external address
D) A `type: ExternalName` Service now, swapped for a selector-based Service on migration day

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
C) Nothing — the cluster IP is virtual, existing only as a forwarding rule that captures and readdresses traffic
D) CoreDNS, because it owns all cluster-internal addresses

---

**18.** Your cluster is running normally, serving traffic to Services, and there are no kube-proxy Pods anywhere. What is happening, and which of §1's four rules is the same component also satisfying?

A) The cluster is broken and Services are failing silently; no rule is being satisfied
B) The network plugin implements Service packet forwarding itself — and the same plugin implements the Pod network, satisfying the rule that all Pods can reach all Pods directly
C) The control plane is proxying Service traffic through the API server; rule 4, node-agent reachability
D) Services are being resolved by DNS to Pod IPs directly, bypassing the need for a proxy; rule 1, unique Pod addresses

---

**19.** *Not multiple choice — write the two names out before checking.* A Pod in namespace `billing` must reach a Service named `ledger` in namespace `payments`. The Service exposes a port named `http` over TCP, and the cluster uses the default cluster domain. Write (a) the name the Pod would use for an ordinary address lookup, and (b) the SRV name that would return the port number and hostname for that named port.

---

**20.** A StatefulSet's three Pods sit behind a headless Service. A client resolves the Service's name and receives three addresses rather than one. What served that answer, and what name form reaches one specific member?

A) kube-proxy served it from its endpoint cache; individual members are reached at `<pod-ip-dashed>.<namespace>.pod.cluster.local`
B) CoreDNS, the cluster's DNS addon, served it from the Service's endpoints; individual members are reached at `<pod-name>.<service-name>.<namespace>.svc.cluster.local`
C) The API server served it directly; individual members are reached by appending an ordinal to the Service's own name
D) CoreDNS served it, but only the set is addressable — a headless Service deliberately gives up per-member names

---

**21.** **[retrieval: ch4]** Chapter 4 told you a bare service name resolves within the local namespace. What makes that true — what is configured, and by which component?

A) CoreDNS rewrites bare queries to the caller's namespace, using the caller's source IP
B) The Pod's DNS search list contains its own namespace and the cluster's default domain, configured by the kubelet
C) The API server rejects cross-namespace DNS queries unless an FQDN is used
D) kube-proxy scopes DNS traffic per namespace using iptables rules

---

**22.** You meet a Kubernetes networking behaviour this chapter never covered. Applying the chapter's method rather than recalling a fact, which pair of questions will locate it?

A) Which node is the traffic on, and which iptables rule matches it
B) Which object holds the declaration of intent, and which controller is reconciling that declaration into a published answer
C) Which CNI plugin is installed, and which of its features is enabled
D) Which DNS record exists for it, and what address that record returns

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

Network plugins use CNI, the Container Network Interface, to implement pod networking, and CNI plugins are external binaries that Kubernetes executes rather than in-process Kubernetes components [source: k8s-docs-extending-kubernetes-2026-08-23].

**A** inverts the relationship — CNI is an interface, not an implementation. **C** invents an API object. **D** confuses two unrelated components: kube-proxy programs node rules via OS APIs, and has nothing to do with CNI.

<!-- AUTHOR-REVIEW: option B and this explanation previously named the kubelet as the executor of CNI plugin binaries. Dropped per curriculum-alignment R3. The cached general page (k8s-docs-extending-kubernetes-2026-08-23) supports "Kubernetes executes external binaries" and mentions the kubelet; Stage 2 recorded that a more specific and more recent page states CNI management was removed from the kubelet in Kubernetes 1.24, with the container runtime loading the plugins. That page is not on disk (see the §1 AUTHOR-REVIEW block), so this item names no executor rather than naming a superseded one. §1's prose still carries the older wording and should be brought into line by the pass that owns it. -->

**4. B.**

ClusterIP exposes the Service on a cluster-internal IP, makes it reachable only from within the cluster, and is the default used if you don't explicitly specify a type [source: k8s-docs-service-2026-08-23].

**A** fails on its first half before the second one matters: NodePort is never a default, it must be asked for, and asking for it would additionally allocate the cluster IP that B describes [source: k8s-docs-service-2026-08-23]. **C** is the near-miss worth naming: ClusterIP alone does *not* expose anything on node IPs. That is what NodePort adds — and the additivity runs one way only. Getting a cluster IP from NodePort is guaranteed; getting node reachability from ClusterIP is not. **D** is not a default either, and it is the one type on this list that cannot function at all without a component Kubernetes does not supply [source: k8s-docs-service-2026-08-23] — which is the subject of question 6.

**5. B.**

To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP` [source: k8s-docs-service-2026-08-23].

**A** is the trap in its purest form — the belief that types are alternatives rather than layers. **C** invents a restriction. **D** confuses an address with a reachability mechanism: the node IPs are *additional* paths, not a substitute address.

**6. C.**

Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider [source: k8s-docs-service-2026-08-23]. With neither present, nothing acts on the request.

**A** is the trap. **B** is wrong because the object is entirely valid — validity and effect are different questions. **D** invents a fallback that would be surprising and undocumented behaviour.

Nothing here is broken and nothing needs fixing. The Service exists and is reconciled; only its external address is absent.

<!-- AUTHOR-REVIEW: this explanation previously closed by asserting that such a Service "still has a cluster IP and, per the additive rule, a node port," and that it remains usable from inside the cluster and from the nodes. Narrowed per fact-accuracy F2. The cached Service snapshot documents additivity for NodePort only ("To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP"); its LoadBalancer entry is a single sentence that says nothing about the rungs beneath it. The keyed answer's "waits indefinitely" is likewise entailed by the sourced premise rather than stated by any snapshot (W2). Both are resolved by the same targeted re-fetch of the type: LoadBalancer subsection; restore the fuller wording once it lands. -->

**7. C.**

ExternalName maps the Service to the contents of the `externalName` field by configuring the cluster's DNS to return a CNAME record with that external hostname value; **no proxying of any kind is set up** [source: k8s-docs-service-2026-08-23]. kube-proxy provides the virtual IP mechanism for Services of type *other than* ExternalName [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23] — so there is no rule to find, because ExternalName is the one type outside its scope.

**A** is the types-are-alternatives trap wearing a diagnostic disguise: a NodePort Service keeps its cluster IP, because Kubernetes sets one up for NodePort Services as well [source: k8s-docs-service-2026-08-23]. There would be rules for both paths, not none. **B** inverts kube-proxy's scope — ClusterIP is the type it most obviously serves. **D** assumes an external load balancer displaces the node-level rules; it does not, because LoadBalancer is inside the "other than ExternalName" set too.

**8. B.**

ExternalName produces a CNAME and no proxying [source: k8s-docs-service-2026-08-23], so the client connects directly to the vendor.

**A** would also work as a way to reach the vendor, but it puts kube-proxy in the path — traffic goes to a cluster IP and is redirected — which is exactly what the question excludes. **C** and **D** are invented configurations; `externalName` is meaningful only with `type: ExternalName`.

**9. C.**

A Service uses labels to allow the control plane to determine which EndpointSlice objects are used for it [source: k8s-docs-garbage-collection-2026-08-24], and a selector is a query over labels. Two controllers evaluating two selectors against one Pod produce two independent results.

**A** confuses ownership with selection — the two mechanisms are explicitly distinguished, and owner references exist so different parts of Kubernetes avoid interfering with objects they don't control [source: k8s-docs-garbage-collection-2026-08-24]. **B** is wrong twice: a Service selects on labels, not on owner references, and the ReplicaSet holds no privileged position over the Service — both are ordinary selector evaluations by ordinary controllers, and neither is told about the other. **D** invents a restart trigger; selectors are evaluated continuously by watching controllers, not at Pod startup.

**10. B.**

Kubernetes automatically manages EndpointSlice objects to provide information about the Pods currently backing a Service [source: k8s-docs-network-model-2026-08-23]; the EndpointSlice controller populates them to provide a link between Services and Pods [source: k8s-docs-cluster-architecture-2026-08-23].

**A** puts the answer in the wrong object and names the wrong writer — kube-proxy *reads* EndpointSlices [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. **C** puts the answer on the wrong object too, and names a component that never participates: the kubelet reports the status of Pods on its own node, whereas endpoint membership is computed centrally by a controller reading the API [source: k8s-docs-cluster-architecture-2026-08-23], not written per-Pod by each node. **D** confuses a publisher with a source of truth: DNS publishes the answer; it does not compute it.

**11. C.**

If a readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod [source: k8s-docs-pod-lifecycle-2026-08-23]; a Pod's `Ready` condition means it should be added to the load balancing pools of all matching Services [source: k8s-docs-pod-termination-2026-08-24].

**A** is a real and important distinction: a failing readiness probe does *not* change the Pod's phase, kill it, or restart it. That's the liveness probe's job. The Pod keeps running, keeps being counted by its controller, and simply stops receiving traffic. **B** would mean readiness edits your Service, which it does not. **D** describes a downstream effect (kube-proxy reprograms rules because the slice changed) as though it were the mechanism.

**12. B.**

If the endpoints don't match the Pods you expect, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready [source: k8s-docs-debug-pods-2026-08-23].

**A** names data-plane components, and it is the most tempting option because the symptom presents as a networking failure. But endpoint membership is computed entirely in the control plane, by a controller reading the API [source: k8s-docs-cluster-architecture-2026-08-23]. Neither kube-proxy nor the CNI plugin can empty a slice; both are downstream readers of it.

**C** pairs two instincts imported from outside Kubernetes. DNS propagation delay is a real phenomenon in the public DNS and has no bearing on an EndpointSlice, which you read from the API server directly. And `kubectl` reads through to the API server rather than serving you a cached copy — a stale-read explanation would let you off the hook for a diagnosis you have not made yet.

**D** is the closest of the three, and worth taking seriously. Its first half is real: a Service's selector is namespace-scoped, so Pods in another namespace are never selected — but that is a *special case of the first documented cause*, not a separate one, which is why the option's framing is wrong even where its fact is right. Its second half is flatly wrong and is the reason to reject the pair: creation order does not matter to a control loop. The controller reconciles continuously, so a Service created before its Pods picks them up the moment they appear.

**13. B.**

The Service has an address and a DNS record because those are allocated on creation, independent of whether any Pod matches. The EndpointSlice is empty because the selector's current answer is the empty set — which the controller has computed correctly.

**A** is the instinct to fix by recreation, and it will produce an identical Service with an identical empty slice. **C** invents an API server behaviour. **D** is the reasoning error worth naming: the presence of a name and an address proves that *reconciliation is happening*, not that it found anything.

This is the second instance in the chapter of the same shape — a valid object whose effect depends on something that isn't there. Chapter 10 gives it a name.

**14. C.**

You create headless Services by explicitly specifying `"None"` for `.spec.clusterIP`; for headless Services with selectors, DNS returns A or AAAA records pointing directly to the Pods [source: k8s-docs-service-2026-08-23]. StatefulSets currently require a headless Service to be responsible for the network identity of the Pods [source: k8s-docs-statefulset-2026-08-24].

**B** is the option to dwell on, because half of it is correct. Its workload clause is right — StatefulSets do require a headless Service — and two options here name StatefulSets precisely so that knowing the workload does not hand you the answer. Its definition clause is the confusion this question exists to catch: "reachable only from inside the cluster" is what *ClusterIP* means, a rung on the type ladder. Headless sits on a different axis entirely. It is about whether a virtual IP is allocated at all, not about who may reach one.

**A** invents a behaviour and attaches it to a workload with no Service requirement of any kind. A headless Service with selectors most certainly has endpoints — returning them directly is the entire point.

**D** crosses the two axes of §5's four-cell table. Headless (`clusterIP: None`) and selectorless are independent choices; a Service can be either, both, or neither. Setting `.spec.clusterIP` to `None` does not touch the selector, and Deployments require neither.

**15. C.**

A Service used with a corresponding set of EndpointSlice objects and without a selector can abstract other kinds of backends, including ones that run outside the cluster — an external database, or a workload being migrated [source: k8s-docs-service-2026-08-23].

**A** would give clients the vendor hostname directly, meaning that when you migrate you must change what clients resolve *and* the connection semantics change — no proxying today, proxying tomorrow. The question specifically asks for proxying in both phases. **B** removes the single address, which the clients want.

**D** is the plan most teams actually propose, and it is worth understanding why it loses to C rather than merely being wrong. Today it behaves exactly like A: a CNAME with no proxying [source: k8s-docs-service-2026-08-23], so the connection semantics still change on migration day. And the swap is a visible cutover, which is the thing the requirement was written to avoid. C keeps one name, one cluster IP, and one proxying path throughout; the only thing that changes is the contents of a slice.

The migration itself follows from the two facts above rather than from any documented procedure: add the selector, and the controller takes over the slice you had been writing by hand. Clients notice nothing.

**16. B.**

On Linux, the available modes are iptables (the default), IPVS, and nftables (GA since Kubernetes 1.33); on Windows there is only kernelspace [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

**A** names a mode that is not among the documented Linux modes. **C** mislabels the default and lists eBPF, which is a plugin data plane rather than a kube-proxy mode. **D** mislabels the default and places the Windows-only mode in the Linux list.

**17. C.**

kube-proxy configures the node to capture traffic to the Service's `clusterIP` and port and redirect it to one of the Service's endpoints [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Capture-and-redirect is not the same as listen-and-forward. Nothing binds the address.

**A** and **B** both assume something terminates the connection at the cluster IP. **D** confuses DNS with addressing entirely — CoreDNS answers name queries; it owns no addresses.

**18. B.**

If you use a network plugin that implements packet forwarding for Services by itself, providing equivalent behavior to kube-proxy, you do not need to run kube-proxy [source: k8s-docs-cluster-architecture-2026-08-23]; Cilium can act as a replacement [source: k8s-docs-cluster-addons-2026-08-24]. And the plugin implementing Service forwarding is the same plugin implementing Pod networking via CNI [source: k8s-docs-extending-kubernetes-2026-08-23] — so it is also satisfying the model's requirement that all Pods reach all Pods directly [source: k8s-docs-network-model-2026-08-23].

**A** assumes kube-proxy's absence is a defect. **C** invents API-server proxying. **D** describes headless-Service behaviour and generalises it to every Service, which is wrong for anything with a cluster IP.

**19.**

**(a) `ledger.payments.svc.cluster.local`**

A normal Service is assigned an A or AAAA record of the form `my-svc.my-namespace.svc.cluster-domain.example`, resolving to the Service's cluster IP [source: k8s-docs-dns-pod-service-2026-08-23]. With the default cluster domain that is `<service-name>.<namespace-name>.svc.cluster.local` [source: k8s-docs-namespaces-2026-08-23].

**(b) `_http._tcp.ledger.payments.svc.cluster.local`**

Named ports get an SRV record of the form `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example` [source: k8s-docs-dns-pod-service-2026-08-23]. The two leading underscore labels are the port's name and its protocol, in that order, prefixed onto the ordinary Service name from part (a).

Two things to check yourself on. First, the shape is stable: everything to the right of the Service name is the same in both answers, and the SRV form only prepends. If you wrote something with `payments` and `ledger` in the other order, that is the error to fix before exam day, because it will produce a name that resolves to nothing rather than an error you can read.

Second — and this is the part that costs points — the bare name `ledger` is not an answer to either half. From a Pod in `billing`, a bare name is tried against that Pod's own search list, which begins with its own namespace [source: k8s-docs-dns-pod-service-2026-08-23]. It will not reach `payments`. If a `ledger` Service also happens to exist in `billing`, the bare name will resolve — to the wrong one, silently.

**20. B.**

DNS is a built-in Kubernetes service launched automatically as a cluster addon [source: k8s-docs-dns-cluster-addon-2026-08-24], and CoreDNS is what serves it [source: k8s-docs-cluster-addons-2026-08-24]. For headless Services with selectors, DNS returns A or AAAA records pointing directly to the Pods [source: k8s-docs-service-2026-08-23] — three addresses for three Pods, which is exactly what the client saw. Individual members of a StatefulSet are addressable at `$(podname).$(governing service domain)` [source: k8s-docs-statefulset-2026-08-24], which expands to the form in B.

Note that both halves of the answer come from the same place. The set and the member are two questions put to one component.

**A** is wrong on both halves. kube-proxy has no role in name resolution at all — and in a headless Service there is no virtual IP for it to program in the first place. The `pod.cluster.local` form it names is real, but it is the Pod record, keyed on a dashed rendering of the Pod's IP address [source: k8s-docs-dns-pod-service-2026-08-23], which is exactly the unstable identifier a StatefulSet exists to avoid.

**C** puts the API server in the DNS path, which it never occupies, and grafts the ordinal onto the wrong label. The ordinal is already inside the Pod's own name; the member's name is the Pod name under the governing Service's domain, not the Service name with a number attached.

**D** inverts the reason headless exists. Per-member addressability is the point, and it is why a StatefulSet requires a headless Service to be responsible for the network identity of its Pods [source: k8s-docs-statefulset-2026-08-24].

**21. B.**

By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain [source: k8s-docs-dns-pod-service-2026-08-23], and the kubelet configures Pods' DNS so that running containers can look up Services by name [source: k8s-docs-dns-pod-service-2026-08-23].

**A** would be a plausible design and is not the one used; the behaviour is ordinary DNS search-domain resolution on the *client* side, not rewriting on the server side. **C** invents an API server role in DNS. **D** invents a kube-proxy role in DNS.

Converting the rule into a mechanism is the point of this item. Once you know it's a search list, the cross-namespace failure mode stops being arbitrary: the caller's own namespace is tried *first*, so a same-named local Service wins, silently.

**22. B.**

This is the only question in the set that tests the method rather than a fact, and it is the one worth carrying out of the chapter. Every mechanism in §1 through §7 had the same two-part shape. A Service declares a selector; the EndpointSlice controller publishes the current answer [source: k8s-docs-cluster-architecture-2026-08-23]. An EndpointSlice declares a set of endpoints; kube-proxy watches the Service and EndpointSlice objects and maintains the node's rules accordingly [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. A Service's name declares an identity; cluster DNS publishes what it currently resolves to. Find the object and find the loop, and you have located a behaviour you have never read about.

**A** is a node-level answer to a cluster-level question. It describes one implementation kube-proxy happens to use on Linux today — and the mode is configurable and the component itself optional [source: k8s-docs-cluster-architecture-2026-08-23], so the method fails on the first cluster that does it differently.

**C** assumes the plugin is where every networking answer lives. It is where the *model* is implemented, but Services, endpoints and names are API-level and are the same whichever plugin you installed.

**D** stops one step short, and stops in the same place question 10's option D did: DNS publishes answers, it does not compute them. Naming the publisher without naming the loop behind it leaves you able to read the current state and unable to explain why it is what it is.

---