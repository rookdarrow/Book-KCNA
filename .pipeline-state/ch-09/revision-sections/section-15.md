## ☆ Taking Your Bearings #3

Five questions on what moves the packet and what you actually type — §6 and §7.

1. 🔵 Name the component that implements the virtual IP mechanism for Services, say which Service type it does **not** implement, and name the two object types it watches.

2. 🟡 A colleague says, "I'll SSH to the node and see what's listening on the cluster IP." What will they find, and why?

3. 🔵 Name kube-proxy's modes and identify the default on Linux. Then say what it would mean to find a cluster running no kube-proxy at all.

4. 🔵 A container in namespace `payments` needs to reach a Service named `ledger` in namespace `billing`. Write the name it should use, and say what would happen if it used just `ledger`.

5. 🟡 Two Services in the same namespace: `db-a` is a normal Service, `db-b` is headless. A client resolves `db-a.prod.svc.cluster.local` and `db-b.prod.svc.cluster.local`. Describe what each lookup returns, and how many answers the client gets.

---

**Answers with Explanations:**

**1. kube-proxy. It does not implement ExternalName. It watches Service and EndpointSlice objects.**

The kube-proxy component is responsible for implementing a virtual IP mechanism for Services of type other than ExternalName; each instance watches the control plane for the addition and removal of Service and EndpointSlice objects [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

*Why a wrong answer is wrong:* **"It watches Services and Pods"** is close and consequential. kube-proxy reads the *computed* answer — the EndpointSlice — not the raw Pods. The EndpointSlice controller is what reads Pods. Two controllers, two inputs, one chain.

**2. Nothing. The cluster IP is virtual — no process is bound to it.**

kube-proxy configures the node to capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. That is the whole documented mechanism, and everything else in this answer follows from it rather than from any separate statement in the documentation: if traffic is *captured and redirected*, then it passes *through* a rule and is never delivered *to* the cluster IP. Nothing accepts a connection there, so there is no socket to find, and `netstat` or `ss` on the node has nothing bound to show you.

*Why the wrong answers are wrong:*
- **"kube-proxy is listening on it"** — kube-proxy programs rules; in the default iptables mode it does not sit in the data path receiving your packets.
- **"One of the backend Pods"** — the backend Pods listen on their *own* addresses. The cluster IP is not one of them.

If you got this one, §6 landed. If you didn't, it's worth a re-read of the Worth Securing callout before you move on, because this idea is load-bearing for everything in Chapter 10.

**3. iptables (the default), IPVS, and nftables on Linux; kernelspace on Windows. A cluster with no kube-proxy means the network plugin implements Service packet forwarding itself.**

The mode list and the default are documented directly [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. And: if you use a network plugin that implements packet forwarding for Services by itself, providing equivalent behavior to kube-proxy, you do not need to run kube-proxy on the nodes in your cluster [source: k8s-docs-cluster-architecture-2026-08-23] — Cilium being a named example of a plugin that can act as a replacement [source: k8s-docs-cluster-addons-2026-08-24].

*A note on what this answer does not say:* it makes no claim about which mode is faster, more scalable, or better, and none about whether replacing kube-proxy performs better than keeping it. The documentation states the list, the default, and the substitution, and says nothing about relative performance — so neither does this book. If you have read that IPVS scales better than iptables for very large Services, that may well be true — but it isn't a claim this material supports, and no exam question you meet should turn on it.

**4. `ledger.billing.svc.cluster.local`. A bare `ledger` would resolve within `payments` only — failing, or worse, silently reaching a different `ledger`.**

A client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain [source: k8s-docs-dns-pod-service-2026-08-23]; a container using only `<service-name>` resolves to the Service local to its namespace, and reaching across namespaces requires the FQDN [source: k8s-docs-namespaces-2026-08-23].

**"It fails" is the incomplete answer, and the incompleteness matters.** If `payments` has no `ledger` Service, you get NXDOMAIN, your application logs a connection error, and you fix it in five minutes. If `payments` *does* have a `ledger` Service — perhaps a test fixture, perhaps a stub someone left behind, perhaps a genuinely different service that happens to share a name — the lookup **succeeds against the wrong Service**. Your application connects. It writes. Nothing anywhere reports an error.

That second case is the one that costs people afternoons, and it's the reason to memorise the FQDN form rather than plan to look it up.

**5. `db-a` returns one address — the Service's cluster IP. `db-b` returns the set of IPs of all the Pods it selects.**

Normal Services are assigned A and/or AAAA records resolving to the cluster IP of the Service; headless Services are assigned records with **the same name form**, but resolving to the set of IPs of all of the Pods selected by the Service, and clients are expected to consume the set or use standard round-robin selection from it [source: k8s-docs-dns-pod-service-2026-08-23].

Both answers come from the same place. Cluster DNS is a built-in service launched automatically as a cluster addon [source: k8s-docs-dns-cluster-addon-2026-08-24], and CoreDNS is what serves it [source: k8s-docs-cluster-addons-2026-08-24]. It is not behaving differently for `db-b` than for `db-a`; the difference is in what each Service's records are defined to contain, not in what publishes them.

The point of the item is that the two names are structurally identical. Nothing in `db-b.prod.svc.cluster.local` announces that it is headless. A client library that assumes one answer per lookup will take the first address it gets and never speak to the other Pods — which is fine for some workloads and quietly wrong for others.

---

**Checkpoint: You've Now Mastered**

✓ kube-proxy's job, its four modes, and its optionality
✓ That the cluster IP is a rule, not a socket
✓ Five DNS record shapes and what each resolves to
✓ Why a bare name is namespace-local, and what that costs when it goes wrong

One section left. It teaches nothing new.

---