# Fact-Accuracy Audit — Chapter 9

**Mode detected: STANDARD.** The `Cached sources` section contains 22 populated snapshots, and the draft carries ~145 inline `[source:` tags. Neither adoption-mode trigger fires. Untagged factual claims are therefore FAIL.

**Note on line references.** The draft was supplied inline without line numbering (`draft-v2.md` unavailable; audited against `draft-v1.md` per the pipeline note). Line numbers below are approximate positional estimates. Every finding quotes verbatim draft text so the revision stage can locate it by exact string search rather than by line.

---

## Summary

- Total factual claims inspected: **164**
- Tagged claims verified: **141**
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0**
- **Untagged factual claims (FAIL): 8**
- **Contradicted claims (FAIL): 0**
- Minor discrepancies (WARN): **15**

No tagged claim in this chapter disagrees with the snapshot it cites. Every `[source:]` tag resolves to a snapshot present in the supplied corpus, and every quoted or near-quoted passage I checked matches its snapshot text. The failure mode in this draft is not misquotation — it is a small set of confident, untagged assertions that the cached corpus does not reach, several of which the chapter's own prose elsewhere disclaims.

Three of the eight FAILs (F2, F4, F8) and two WARNs (W2, W12) are resolved by two targeted fetches. Those are flagged inline.

The draft's three `AUTHOR-REVIEW` blocks (§1 network-plugin defaults, §3 port fields, §4 EndpointSlice internals, plus §7's scope note) are correctly placed and correctly restrictive. Nothing in this audit contradicts them; F1 and F3 are the two places where the draft's discipline lapses in the same way those blocks were written to prevent.

---

## FAIL — Untagged factual claims

### F1 — "Why This Chapter Matters" (~line 132): "Networking is the largest of Domain 2's four competencies and the one the others lean on."

**Why it's a factual claim:** It asserts a relative weighting among published exam competencies.

**What the corpus supports:** That Domain 2 has exactly four competencies is verified — `cncf-kcna-curriculum-pdf-2026-08-23`: *"28% – Container Orchestration: Networking; Security; Troubleshooting; Storage"*, corroborated by `lf-kcna-exam-page-2026-08-23`. That Networking is the **largest** of them is supported by neither. Both authoritative sources publish percentages at the domain level only.

**Internal inconsistency:** the chapter's own header states this explicitly — *"CNCF publishes domain weights only, not competency weights; see front matter"* — and the Stakes paragraph offers "largest" three sentences later as though it were published.

**Fix:** Either (a) delete "largest of Domain 2's four competencies" and keep the structural argument, which stands on its own ("the one the others lean on" is a claim about *this book's* chapter dependencies and is fine), or (b) reframe as authored allocation, matching the header's disclosure: "Networking carries the largest share of our authored allocation within Domain 2." Option (b) is preferred — it preserves the beat and stays inside the transparency contract the front matter already established. No research gap needed; CNCF does not publish this figure and no fetch will produce it.

---

### F2 — §3 (~lines 316, 425, 1330): LoadBalancer additivity, asserted in three places

**The three instances, verbatim:**
1. §3 "The three that stack": *"**LoadBalancer** exposes the Service externally using an external load balancer [source: k8s-docs-service-2026-08-23] — sitting on top of the NodePort and cluster-IP arrangement beneath it."*
2. Bearings #1 answer 3: *"LoadBalancer implies NodePort implies ClusterIP."*
3. Practice Q7 answer: *"Note that the Service still has a cluster IP and, per the additive rule, a node port."*

**Why it's a factual claim:** It asserts specific API allocation behavior for a Service type.

**What the corpus supports:** Additivity is documented for **NodePort only**. `k8s-docs-service-2026-08-23`: *"NodePort — Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP."* The cached LoadBalancer entry is one sentence and says nothing about cluster IPs or node ports: *"LoadBalancer — Exposes the Service externally using an external load balancer."*

In instance (1) the `[source:]` tag covers the clause before the em-dash; the additivity clause is appended outside it. Instances (2) and (3) are wholly untagged, and (3) states the unsupported half as an established rule ("per the additive rule").

**Consequence:** the "three rungs stack" framing is a Fixed Point, a figure (`ch09-fig02-service-types-ladder`), an Exam Alert item, a Common Traps row, and a Chapter Summary row. It is load-bearing and currently rests on a half-cached premise.

**Fix:** Open a research gap for a targeted re-fetch of `kubernetes.io/docs/concepts/services-networking/service/`, capturing the `type: LoadBalancer` subsection in full (not the type-list summary bullet already cached). That subsection documents the cluster-IP and node-port allocation. Until it lands, narrow the ladder claim to what the snapshot carries: NodePort → ClusterIP additivity, with LoadBalancer described as "exposed externally by a provider-supplied load balancer" without asserting the rungs beneath it. **This same fetch resolves W2.**

---

### F3 — §6 Closer Look (~line 786): "kube-proxy is optional, and increasingly often absent — a plugin like Cilium can do the same work in its own eBPF data plane, usually with better performance characteristics at scale."

**Why it's a factual claim:** Two separate assertions — an adoption trend ("increasingly often absent") and a comparative performance claim ("usually with better performance characteristics at scale") — about third-party software.

**What the corpus supports:** The optionality is verified (`k8s-docs-cluster-architecture-2026-08-23`) and Cilium's eBPF data plane and kube-proxy-replacement capability are verified (`k8s-docs-cluster-addons-2026-08-24`: *"Cilium can act as a replacement for kube-proxy"*). Neither the trend nor the performance comparison appears in any cached snapshot. `k8s-docs-cluster-addons-2026-08-24` is a neutral list page and makes no performance claims about any plugin.

**Internal contradiction — this is the sharpest one in the chapter.** Bearings #3 answer 3, ~90 lines later, disavows exactly this move: *"it makes no claim about which mode is faster, more scalable, or better. The documentation states the list and the default and says nothing about relative performance, so neither does this book."* The Closer Look makes the claim the answer key promises the book does not make. A reader who notices will trust the answer key less, which is expensive for a chapter whose Bearings items carry this much of the teaching.

**Fix:** Cut both unsupported halves. The Closer Look's actual payload — *"If you meet a cluster with no kube-proxy Pods in `kube-system`, nothing is missing"* — survives intact and is the useful part. Suggested: "kube-proxy is optional. A plugin like Cilium can do the same work in its own eBPF data plane." No fetch required; deletion is the correct fix, and it brings §6 into line with the standard §7 already sets.

---

### F4 — §1 (~line 236): "Chapter 6 noted in passing that cluster networking plugins commonly ship as DaemonSets — one Pod on every node."

**Why it's a factual claim:** It asserts how third-party networking software is packaged and deployed.

**What the corpus supports:** Nothing. No DaemonSet documentation is cached. `k8s-docs-cluster-addons-2026-08-24` lists Calico, Cilium and Flannel with installation links but describes no deployment shape. The attribution to Chapter 6 does not discharge the sourcing obligation — a cross-chapter retrieval inherits the earlier chapter's tag, and none is carried here.

**Fix:** Two options. (a) If Chapter 6 carries a source tag for the DaemonSet-per-node claim, propagate that tag here. (b) Otherwise open a research gap for `kubernetes.io/docs/concepts/workloads/controllers/daemonset/`, whose "Use cases" section covers cluster-storage/networking daemons — that page will support the claim directly and is a cheap fetch that Chapter 6 likely wants cached anyway. The paragraph's rhetorical payoff ("a thing that must configure networking on every node is exactly a thing that wants one copy per node") is worth preserving, so prefer fetching over cutting.

---

### F5 — §1 Snag (~line 210) and Bearings #1 answer 2 (~line 430): claims about Docker's networking model

**The two instances, verbatim:**
1. *"it is usually the residue of experience with plain Docker, where something like it is true"*
2. *"**\"Yes, they each get their own port space\"** is Docker's model, not Kubernetes'."*

**Why it's a factual claim:** Instance (2) is a flat assertion about a named third-party product's behavior, stated without hedge in an answer key.

**What the corpus supports:** No Docker documentation is cached. The Kubernetes half of both sentences is properly tagged and verified against `k8s-docs-pods-2026-08-24`; only the Docker comparison is unsourced.

**Fix:** Lowest-cost fix is to make instance (2) match instance (1)'s hedging and drop the product name from the assertion: "**\"Yes, they each get their own port space\"** is the single-container mental model most people arrive with. Two containers in one Pod compete for ports exactly as two processes on one host do." That keeps the corrective force without asserting anything about Docker. If the comparison is judged pedagogically necessary, open a research gap for Docker's container-networking documentation — but the softening is the better trade here, since the Docker contrast is decoration and the Kubernetes fact is the point.

---

### F6 — §1 Closer Look (~line 228) and Bearings #1 answer 1 (~line 415): CNI plugin implementation mechanics

**The instances, verbatim:**
1. *"Overlay networks encapsulate Pod traffic inside node-to-node tunnels. Native-routing plugins make Pod addresses routable in the underlying network directly. BGP-based plugins advertise Pod CIDRs to physical routers. eBPF data planes intercept in the kernel."*
2. *"Overlay-based plugins do encapsulate the traffic — but encapsulation is not translation, and the Pod at the far end still sees the original source address."*

**Why it's a factual claim:** Four specific mechanism descriptions attributed to named categories of third-party software, plus a behavioral guarantee about overlay plugins.

**What the corpus supports:** `k8s-docs-cluster-addons-2026-08-24` supports the *vocabulary* — Calico: *"including non-overlay and overlay networks, with or without BGP"*; Cilium: *"a simple flat Layer 3 network... in either native routing or overlay/encapsulation mode"* with *"an eBPF-based data plane"*; Flannel: *"an overlay network provider"*. It supports none of the mechanisms: no tunnels, no CIDR advertisement to physical routers, no kernel interception, and no statement that encapsulated traffic preserves the original source address.

Instance (2) is the more consequential of the two: it is the rationale for rejecting a distractor in a Bearings item, so a reader is being taught to rely on it.

**Fix:** For instance (1), either tag the categories to `k8s-docs-cluster-addons-2026-08-24` and cut to what that snapshot names (overlay vs. non-overlay, with or without BGP, eBPF data plane, native routing vs. encapsulation), or keep the mechanics and open a research gap for `kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/` — the same fetch the §1 `AUTHOR-REVIEW` block already routes to Stage 2 for Open question #2. Folding this into that pending fetch is the efficient path. For instance (2), the correct source-anchored form is available without any fetch: rest the rejection on Rule 3 itself (`k8s-docs-network-model-2026-08-23` — Pods communicate *"directly, without the use of proxies or address translation (NAT)"*), which is what the model *requires of any plugin*, rather than on what overlay plugins are asserted to do.

---

### F7 — §3 "The ceiling" (~line 380): "in most clouds each of those addresses is a billable resource with its own lifecycle"

**Why it's a factual claim:** A claim about cloud-provider commercial terms.

**What the corpus supports:** Nothing. No cloud-provider pricing or product documentation is cached, and the KCNA sources are silent on it.

**Fix:** Cut the billing clause. The argument for the Chapter 10 handoff does not need it — *"That is fine for one Service. It is expensive and awkward for fifty"* already carries the scaling point, and "expensive and awkward" is an authored judgment rather than a sourced assertion, which is fine in this position. Do not open a research gap; per-cloud pricing is volatile and would need re-verification every edition, which is a poor trade for one subordinate clause.

---

### F8 — Practice Q18 answer (~line 1395): "**A** names a retired mode."

**Why it's a factual claim:** It asserts the deprecation history of a named kube-proxy mode (`userspace`, offered in distractor A).

**What the corpus supports:** `k8s-docs-virtual-ips-kube-proxy-2026-08-23` enumerates the current modes — *"On Linux nodes, the available modes for kube-proxy are: iptables... ipvs... nftables (GA since Kubernetes 1.33). There is only one mode available for kube-proxy on Windows: kernelspace"* — and does not mention `userspace` at all, retired or otherwise. The cached snapshot supports "not among the documented modes." It does not support "retired," which is a claim about version history.

**Fix:** No fetch needed. Reword to the supported form: "**A** names a mode that is not among the documented Linux modes." This is also the pedagogically better rationale, since the exam-relevant skill is recognising the current list, not recalling removal history.

---

## WARN — Minor discrepancies

**W1 — "Kubernetes implements none of it" overreaches its snapshot (two locations).**
Dead Reckoning, ~line 138 (untagged): *"Kubernetes does not implement any of that; a network plugin does."* Exam Alert item 12, ~line 1080 (tagged): *"**Kubernetes defines the network model and implements none of it** — a CNI plugin does [source: k8s-docs-extending-kubernetes-2026-08-23]."*
`k8s-docs-extending-kubernetes-2026-08-23` supports the positive half — *"Network plugins (CNI, the Container Network Interface, to implement pod networking)"* — but states no exclusive negative. The §1 `AUTHOR-REVIEW` block already identifies this exact boundary and holds §1's prose to the weaker form ("the plugin implements pod networking," never "and Kubernetes ships none"). Dead Reckoning and Exam Alert escape that discipline. Recommend matching §1's Fixed Point wording — *"Kubernetes **defines** the network model. A **CNI network plugin implements** it"* — in both places, and restoring the stronger claim only when the network-plugins fetch lands.

**W2 — `type: LoadBalancer` "waits indefinitely" is an inference, and it is a keyed answer.**
§3, ~line 350: *"a `type: LoadBalancer` Service sits there with no external address indefinitely. Not for thirty seconds. Indefinitely."* Restated as the keyed answer to Practice Q7 and in Bearings #1 answer 5. The tagged premise is solid (`k8s-docs-service-2026-08-23`: *"Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider"*), and the pending-forever consequence follows, but no cached snapshot describes the observable state. Resolved by the same Service-page re-fetch recommended in **F2**.

**W3 — Tag attribution imprecision in §6 (~line 720).**
Draft: *"a network proxy that maintains network rules on nodes, implementing part of the Kubernetes Service concept [source: k8s-docs-components-2026-08-23]"*. The components snapshot's full entry is *"kube-proxy (optional) — Maintains network rules on nodes to implement Services."* The near-verbatim phrasing quoted is from `k8s-docs-cluster-architecture-2026-08-23`: *"kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept."* Substance is supported by both; only the attribution is off. Retag to `k8s-docs-cluster-architecture-2026-08-23`, or carry both tags.

**W4 — "Host header" exceeds the Ingress snapshot (~line 890).**
Draft: *"Chapter 10 introduces **name-based virtual hosting**, where an HTTP router uses the `Host` header to decide which backend gets the request [source: k8s-docs-ingress-2026-08-23]."* `k8s-docs-ingress-2026-08-23` says *"name based virtual hosting (routing HTTP traffic to multiple host names at the same IP address)"* — accurate, but it never names the `Host` header. Recommend the snapshot's own phrasing, or defer the header mechanism to Chapter 10 where the fetch can support it.

**W5 — "four pluggable interfaces" against a five-item enumeration.**
§1 cross-bearing (~line 232) and Chapter Summary (~line 1432): *"the four pluggable interfaces"* / *"Second of the four pluggable interfaces."* `k8s-docs-extending-kubernetes-2026-08-23` lists **five** infrastructure extensions: *"Device Plugins (custom hardware); Storage plugins (CSI...); Network plugins (CNI...); Container runtime (CRI...); kubelet image credential provider plugins."* CRI/CNI/CSI/device-plugins is a defensible teaching grouping, but stating it as a count invites a reader to check. Recommend "four of Kubernetes' infrastructure extension points" or "the four you will meet in this book." Note §1's own tagged sentence is correctly non-exhaustive (*"listed among Kubernetes' infrastructure extension points alongside..."*) — only the count-bearing restatements need adjusting.

**W6 — "Nothing is listening on a cluster IP" is an entailment, not a documented statement, and it is load-bearing.**
§6 (~lines 745–760), plus the Worth Securing callout, a Fixed Point, and Practice Q19. `k8s-docs-virtual-ips-kube-proxy-2026-08-23` documents *"configure the node to capture traffic to the Service's clusterIP and port, and redirect that traffic to one of the Service's endpoints"* — capture-and-redirect entails no bound socket, and the draft's reasoning is sound. But the downstream specifics (*"why you can't `ping` some cluster IPs usefully, why `netstat` on a node shows you nothing"*, and Q19's *"`ss -tlnp`... will show you nothing bound there"*) are behavioral predictions no snapshot states. Not wrong; simply reasoned rather than cited, in a passage the chapter itself calls the most valuable trap on the list. Recommend carrying the capture/redirect tag onto each restatement so the entailment chain is visible.

**W7 — hostname/subdomain identified as the StatefulSet identity mechanism (~line 862).**
Draft: *"That is the mechanism by which individual StatefulSet members become individually addressable."* `k8s-docs-dns-pod-service-2026-08-23` documents the `hostname`/`subdomain` FQDN form; `k8s-docs-statefulset-2026-08-24` documents StatefulSet Pod DNS independently as *"$(podname).$(governing service domain)"*, derived from the StatefulSet name and ordinal. The two forms are consistent, but neither snapshot states that StatefulSet identity *is implemented via* the Pod spec's hostname/subdomain fields. Recommend softening to a shape observation ("the same shape of name a StatefulSet member gets") rather than a causal identification.

**W8 — "D2.1" presented as a published objective ID (~line 1462).**
Safe Harbor: *"That is the whole of D2.1"*, and the heading *"Domain 2 Networking, complete."* Neither `cncf-kcna-curriculum-pdf-2026-08-23` nor `lf-kcna-exam-page-2026-08-23` numbers competencies; both list them as unnumbered names under a weighted domain. A reader may reasonably take "D2.1" for CNCF's own label. The completeness claim ("the whole of") is also unverifiable, since no sub-objective list is published to check coverage against. Recommend "the whole of Domain 2's Networking competency, as far as this book allocates it" — consistent with the header's authored-allocation disclosure.

**W9 — "no port mapping" added to the model's guarantees (~line 118).**
Draft: *"no NAT, no proxy, no port mapping"* tagged to `k8s-docs-network-model-2026-08-23`, which specifies *"without the use of proxies or address translation (NAT)"*. Port mapping is neither named nor forbidden by the snapshot. It is a fair consequence of per-Pod addressing, but the enumerated triple reads as a quotation of the rule. Recommend matching §1's Rule 3, which states it correctly.

**W10 — "kube-proxy Pods in `kube-system`" (~line 788).**
Deployment shape not in the corpus. `k8s-docs-namespaces-2026-08-23` supports what `kube-system` is (*"The namespace for objects created by the Kubernetes system"*); nothing supports kube-proxy running as Pods there. Low consequence — it appears in a beyond-exam aside — but it is the same category as **F4** and would be covered by a DaemonSet fetch.

**W11 — Attention Budget arithmetic (~lines 18–34).** Header states *"Total time: ~95 minutes"*; the section rows sum to 99 (12+6+16+6+12+9+6+7+14+6+5). Not source-verifiable and therefore outside this audit's remit — flagged because it is a checkable number in the chapter and the structural linter may not cover totals. Either figure works; make them agree.

**W12 — "The newest of the three" (~line 772).** The kube-proxy mode table's note for `nftables`. `k8s-docs-virtual-ips-kube-proxy-2026-08-23` states *"GA since Kubernetes 1.33"* but establishes no ordering among the three Linux modes. The GA date is the sourced fact; recency is inferred. Trivial — recommend keeping only the parenthetical.

**W13 — "one address per Service" attributed to the Gateway/Ingress rationale (~line 386).**
Draft: *"That gap — one address per Service, and no protocol awareness — is exactly what the Gateway API and its predecessor Ingress exist to fill [source: k8s-docs-network-model-2026-08-23]."* The protocol-awareness half is supported (*"Ingress — protocol-aware HTTP/HTTPS routing using URIs, hostnames, and paths"*). The snapshot's actual statement of purpose is broader and does not mention address economy: *"The Gateway API (or its predecessor, Ingress) allows you to make Services accessible to clients that are outside the cluster."* Recommend tagging the protocol-awareness half and marking the address-count half as the chapter's own argument.

**W14 — Migration procedure in Q17 answer (~line 1385).** *"The migration itself, when it comes, is: add the selector, delete the manual EndpointSlices."* Operationally sound and consistent with `k8s-docs-service-2026-08-23`'s selectorless-Service description, but no cached snapshot documents the transition procedure. Low consequence; it sits after the keyed answer as commentary.

**W15 — "It has no endpoint list" for ExternalName (~line 334).** Entailed by *"No proxying of any kind is set up"* plus kube-proxy's *"Services of type other than ExternalName"* scope, but not stated. The neighbouring claim (*"has no cluster IP"*) is on the same footing. Both are safe inferences; noted for completeness since §3's ExternalName block is heavily examined in this chapter (Q8, Q9, Bearings #1 item 5, Bearings #2 item 5).

---

## PASS — Verified claims

Sampled coverage evidence. Each was checked against the cited snapshot's text; all match.

**Network model (§1, Rules 1–4, Bearings #1 item 1, Q1)** — `k8s-docs-network-model-2026-08-23`. Unique cluster-wide Pod IP; shared private network namespace with `localhost` between containers; all-Pods-to-all-Pods same node or different nodes; *"directly, without the use of proxies or address translation (NAT)"*; the Windows host-network-Pod exception, reproduced with its parenthetical intact; node agents reaching Pods on their node. All four rules verbatim or near-verbatim.

**Pod addressing (§1 Snag, Bearings #1 item 2, Q2)** — `k8s-docs-pods-2026-08-24`. *"Every container in a Pod shares the network namespace, including the IP address and network ports"*; *"Inside a Pod (and **only** then)... using `localhost`"*; *"Containers in different Pods have distinct IP addresses"*; *"Each Pod is assigned a unique IP address for each address family."* Q2's derivation (one address, one endpoint entry) is sound against this plus the EndpointSlice definition.

**CNI as extension point (§1, §8, Exam Alert 12)** — `k8s-docs-extending-kubernetes-2026-08-23`. CNI listed under infrastructure extensions *"to implement pod networking"*; *"Binary plugins — Kubernetes executes external binaries; used by the kubelet (CSI storage plugins, CNI network plugins)."* (See W1 for the one overreaching restatement.)

**Plugin descriptions (§1)** — `k8s-docs-cluster-addons-2026-08-24`. Calico as networking and network policy provider, overlay/non-overlay, with or without BGP; Cilium's flat Layer 3 network, eBPF data plane, native routing or overlay mode, *"a CNCF project at the Graduated level"*; Flannel as overlay provider. All three accurate, including the Graduated-level qualifier.

**`NetworkUnavailable` (§1)** — `k8s-docs-nodes-2026-08-23`: *"NetworkUnavailable — True if the network for the node is not correctly configured."* Verbatim.

**Pod churn (§2, Bearings #1 item 4, Q4)** — `k8s-docs-pod-lifecycle-2026-08-23`: *"A Pod is never \"rescheduled\" to a different node; instead, it is replaced by a new, near-identical Pod with a different UID."* Verbatim.

**Service definition and motivation (§2)** — `k8s-docs-service-2026-08-23`. The backends/frontends block quote is verbatim, including the quoted terms; *"the set of Pods running in one moment in time could be different from the set of Pods running that application a moment later"*; *"logical set of endpoints"*; *"Services most commonly abstract access to Kubernetes Pods thanks to the selector."*

**Service types (§3, Exam Alert 3/5/6, Q5/Q6/Q8/Q9)** — `k8s-docs-service-2026-08-23`. ClusterIP default and cluster-internal-only; NodePort's cluster-IP allocation, verbatim; *"Kubernetes does not directly offer a load balancing component"*, verbatim; ExternalName's CNAME behavior and *"No proxying of any kind is set up"*, verbatim. (LoadBalancer additivity excepted — see F2.)

**EndpointSlice path (§4, Bearings #2 item 1, Q11)** — `k8s-docs-network-model-2026-08-23`: *"Kubernetes automatically manages EndpointSlice objects to provide information about the pods currently backing a Service"*, verbatim; `k8s-docs-cluster-architecture-2026-08-23`: *"EndpointSlice controller (populates EndpointSlice objects to provide a link between Services and Pods)"*, verbatim, correctly placed inside kube-controller-manager.

**Selection vs. ownership (§4, §8, Q10)** — `k8s-docs-garbage-collection-2026-08-24`. The Service/EndpointSlice labels-plus-owner-reference passage is reproduced accurately, including *"Owner references help different parts of Kubernetes avoid interfering with objects they don't control."*

**Readiness gating (§4, Bearings #2 item 2, Q12, Q13)** — `k8s-docs-pod-lifecycle-2026-08-23`: *"if the readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod"*, verbatim. `k8s-docs-pod-termination-2026-08-24`: *"`Ready`: the Pod is able to serve requests and should be added to the load balancing pools of all matching Services"*, verbatim. Q12's supporting distinction (readiness does not change phase or restart the container; that is liveness) checks correctly against the same snapshot's probe-type descriptions.

**Termination and draining (§4, Q13)** — `k8s-docs-pod-termination-2026-08-24`. Control-plane EndpointSlice re-evaluation during graceful shutdown; *"not immediately removed"*; *"Terminating endpoints always have their `ready` status as `false`"*; the `serving` condition. Q13's arithmetic (four Ready + one terminating retained with `ready: false` = five entries) is correct against this.

**Empty-endpoint diagnosis (§4, Bearings #2 item 3, Q14)** — `k8s-docs-debug-pods-2026-08-23`. The `kubectl get endpointslices -l kubernetes.io/service-name=${SERVICE_NAME}` form matches the snapshot exactly, and the two-cause statement (*"the Service's selector probably does not match the Pods' labels, or the Pods are not Ready"*) is verbatim.

**Headless and selectorless Services (§5, the four-cell table, Q16, Q17)** — `k8s-docs-service-2026-08-23`. `.spec.clusterIP` set to `"None"`; A/AAAA records to Pods for headless-with-selectors; *"For headless Services without selectors, no EndpointSlices are created automatically"*; the external-backend use case including *"an external database... a workload being migrated."* All four table cells check out.

**StatefulSet requirement (§5, Q16)** — `k8s-docs-statefulset-2026-08-24`: *"StatefulSets currently require a Headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service"*, verbatim; *"not interchangeable: each has a persistent identifier that it maintains across any rescheduling."*

**kube-proxy (§6, Bearings #3 items 1/2/3, Q18, Q19, Q20)** — `k8s-docs-virtual-ips-kube-proxy-2026-08-23`. The opening block including the *"unless you have deployed your own alternative component"* parenthetical; *"virtual IP mechanism for Services of type other than ExternalName"*; watching Service and EndpointSlice objects; capture-and-redirect including *"usually a Pod, but possibly an arbitrary user-provided IP address"*; the control-loop sentence, quoted verbatim; all four modes with iptables as default and `nftables` GA since 1.33; kernelspace as the sole Windows mode. Optionality verified against `k8s-docs-cluster-architecture-2026-08-23` and Cilium-as-replacement against `k8s-docs-cluster-addons-2026-08-24`.

**Cluster DNS (§7, Dead Reckoning table, Bearings #3 items 4/5, Q21)** — `k8s-docs-dns-pod-service-2026-08-23`. All five record shapes verified individually: normal Service A/AAAA to cluster IP; headless same-name-form resolving to the Pod set with the round-robin note; the SRV form `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example`; the Pod form with the `172-17-0-3.default.pod.cluster.local` example; the hostname/subdomain FQDN with both preconditions. Search-list behavior (*"a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain"*) and kubelet-configures-Pod-DNS both verbatim. `dnsPolicy` values and the `ClusterFirst` default verified, including the naming trap the Closer Look flags.

**CoreDNS provenance (§7)** — `k8s-docs-cluster-addons-2026-08-24` (Service Discovery entry) and `k8s-docs-dns-cluster-addon-2026-08-24`: *"DNS is a built-in Kubernetes service launched automatically using the _addon manager_ cluster add-on"*, verbatim.

**Namespace DNS (Soundings 5, §7, Q21)** — `k8s-docs-namespaces-2026-08-23`: the `<service-name>.<namespace-name>.svc.cluster.local` form and the bare-name/local-namespace/FQDN rule, both accurate.

**Domain weighting (header, Stakes)** — `cncf-kcna-curriculum-pdf-2026-08-23`, corroborated by `lf-kcna-exam-page-2026-08-23`: Container Orchestration at 28%, with Networking among its four competencies. The authored-allocation disclosure in the header is correctly framed. (The "largest competency" claim is the sole exception — F1.)

**Ingress forward-reference (§3 ceiling, "The Voyage Ahead")** — `k8s-docs-ingress-2026-08-23` supports the Gateway recommendation and the frozen-API framing previewed for Chapter 10: *"The Kubernetes project recommends using Gateway instead of Ingress. The Ingress API has been frozen."*

---

## Scope notes

- **Recap surfaces audited by anchor, not individually flagged.** The Exam Alert list, Common Traps table, and Chapter Summary table restate body claims. Each row was checked against its body anchor and its anchor's tag; rows are reported only where the recap says something the body's tag does not carry (F2 instance 3, W1, W5). This avoids duplicating a single sourcing defect across four locations.
- **Analogies, mnemonics and voice devices excluded** per rule 3 — the navigator framing, the "label query with a name" Zenith, the migration vignette in §5, the ASCII figures' illustrative IP addresses, and the closing epigraphs assert no external fact.
- **Pedagogical and structural claims excluded** — chapter dependencies ("Chapter 10 cannot explain Ingress without §3"), attention-cost ratings, session-split advice, "the sixth control loop in this book", and Voyage Progress are internal to the book, not external facts. W8 is the one exception, because it presents a book-internal identifier in a form a reader will mistake for a vendor label.
- **Question and answer-key consistency spot-checked.** All 21 practice questions have exactly one defensible keyed answer against the cached corpus, and the four `[retrieval:]` tags match the stated count of four. Distractor rationales were audited as factual claims; two failed (F8, and F6 instance 2 in Bearings #1).
- **No re-fetching performed** per rule 2. Where the corpus is silent, findings say so rather than resolving from background knowledge — F2 in particular describes a claim that is very likely true of Kubernetes but is not in the supplied snapshots, and is reported on that basis.

## Recommended research gaps, consolidated

Two fetches close five findings:

1. **`kubernetes.io/docs/concepts/services-networking/service/` — `type: LoadBalancer` subsection in full.** Closes F2 and W2. Highest priority: the Service-type ladder is the chapter's most heavily examined structure.
2. **`kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/`** — already routed to Stage 2 by the §1 `AUTHOR-REVIEW` block for Open question #2. Fold F6 into it, and it additionally discharges W1.

One optional fetch: **`kubernetes.io/docs/concepts/workloads/controllers/daemonset/`** ("Use cases" section) closes F4 and W10, and is likely wanted by Chapter 6 regardless.

F1, F3, F5, F7 and F8 need no fetch — each is fixed by deletion or by narrowing to what is already cached.