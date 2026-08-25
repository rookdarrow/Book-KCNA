## ⚪ §1 — Four Rules and a Plugin

Kubernetes networking is specified as a small set of requirements. Not a mechanism, not a topology — requirements. Here they are, and they are worth meeting as a numbered set, because that is how they are examinable and how §8 will retrieve them.

**Rule 1.** Each Pod in a cluster gets its own **unique cluster-wide IP address**. A Pod has its own private network namespace, shared by all of the containers within it; processes running in different containers in the same Pod communicate with each other over `localhost` [source: k8s-docs-network-model-2026-08-23].

**Rule 2.** The **pod network** — also called the cluster network — handles communication between Pods. Barring intentional network segmentation, all Pods can communicate with all other Pods, **whether they are on the same node or on different nodes** [source: k8s-docs-network-model-2026-08-23].

**Rule 3.** Pods communicate with each other **directly, without the use of proxies or address translation (NAT)** [source: k8s-docs-network-model-2026-08-23]. (One documented exception: on Windows, this rule does not apply to host-network Pods [source: k8s-docs-network-model-2026-08-23]. Note it; nothing in this book is built on it.)

**Rule 4.** **Agents on a node** — system daemons, the kubelet — can communicate with all Pods on that node [source: k8s-docs-network-model-2026-08-23].

<!-- FIGURE: ch09-fig01-network-model-four-rules -->
```
        node: worker-3                         node: worker-11
   ┌──────────────────────────┐          ┌──────────────────────────┐
   │                          │          │                          │
   │  ┌────────────────────┐  │          │  ┌────────────────────┐  │
   │  │ Pod  10.244.1.7    │  │          │  │ Pod  10.244.4.2    │  │
   │  │ ┌──────┐  ┌──────┐ │  │          │  │                    │  │
   │  │ │ ctr  │↔ │ ctr  │ │  │          │  │                    │  │
   │  │ │  a   │lo│  b   │ │  │          │  │                    │  │
   │  │ └──────┘  └──────┘ │  │          │  │                    │  │
   │  └─────────┬──────────┘  │          │  └─────────┬──────────┘  │
   │            │             │          │            │             │
   │            ├─────────────┼──────────┼────────────┘             │
   │            │             │          │                          │
   │  ┌─────────┴──────────┐  │          │  ┌────────────────────┐  │
   │  │ Pod  10.244.1.8    │  │          │  │ Pod  10.244.4.3    │  │
   │  └────────────────────┘  │          │  └────────────────────┘  │
   │       ▲                  │          │                          │
   │  ┌────┴────┐             │          │                          │
   │  │ kubelet │             │          │                          │
   │  └─────────┘             │          │                          │
   └──────────────────────────┘          └──────────────────────────┘

   Every line above is a direct connection. Nothing sits between the Pods.
```

Rule 3 is the one that deserves a paragraph rather than a line, and it is worth pausing on if you answered Soundings question 6.

In ordinary infrastructure, reaching a process means reaching a *host* and then a *port on that host*, and the address the receiver sees is frequently not the address the sender used. You accept a certain amount of pain as the price of that arrangement: coordinating which application gets which port on which machine, maintaining the translation tables, losing the caller's real identity somewhere in the middle, explaining at eight the next morning why the logs say every request came from the same three addresses.

Kubernetes forbids all of it. The receiving Pod sees the sending Pod's actual address. Two different applications can both listen on port 8080 forever, because they are not sharing a port space — each has its own. An application inside the cluster can be written as though every other application in the cluster is on the same flat network, because it is.

That is not an aesthetic preference. It is the reason the rest of this chapter can be as simple as it is.

> 🪝 **Snag:** "Each container gets its own IP" is the most common form of this mistake, and it usually arrives with readers whose habits were formed one container at a time, where container and address amounted to the same thing. Inside a Pod they do not. The address belongs to the **Pod**. Every container in a Pod shares the network namespace, including the IP address and network ports; inside a Pod, and *only* then, the containers can communicate using `localhost` [source: k8s-docs-pods-2026-08-24]. Containers in *different* Pods have distinct IP addresses and must use IP networking to reach each other [source: k8s-docs-pods-2026-08-24].

*[cross-bearing: see Ch 5 §2 — the Pod's shared network namespace]*. That chapter told you the containers share an address. This chapter tells you what the address is *worth*: it is routable from anywhere in the cluster.

★ **Fixed Point:** Every Pod gets a unique **cluster-wide** IP address, and **all Pods can reach all Pods without NAT and without proxies** — same node or different nodes. The Pod holds the address; its containers share it and reach each other over `localhost`.

### Kubernetes defines it. Something else implements it.

Everything above is a specification. It describes what must be true, and says nothing about how.

Pod networking is implemented by a **network plugin**, and the interface it plugs into is **CNI, the Container Network Interface** — listed among Kubernetes' infrastructure extension points alongside CSI for storage, CRI for container runtimes, and device plugins for custom hardware [source: k8s-docs-extending-kubernetes-2026-08-23]. CNI plugins are **binary plugins**: Kubernetes executes them as external binaries rather than linking them in [source: k8s-docs-extending-kubernetes-2026-08-23].

That published list runs longer than four [source: k8s-docs-extending-kubernetes-2026-08-23], and this book does not follow it item for item. What it follows is **the four pluggable interfaces** — CRI for runtimes, CNI for networking, CSI for storage, and CRDs for object types Kubernetes does not ship. *[cross-bearing: see Ch 2 §4 — CRI, CNI, CSI and CRDs as the four pluggable interfaces]*. That section named CNI and pointed you here. This is the second of the four; Chapter 17 collects all of them *[cross-bearing: see Ch 17 §4 — the four pluggable interfaces, collected]*.

Which network plugin? That is a genuine choice with genuine consequences. **Calico** is a networking and network policy provider supporting overlay and non-overlay networks, with or without BGP. **Cilium** provides a flat Layer 3 network with an eBPF-based data plane, in either native routing or overlay mode, and is a CNCF project at the Graduated level. **Flannel** is an overlay network provider [source: k8s-docs-cluster-addons-2026-08-24]. There are many more.

<!-- AUTHOR-REVIEW: the CNI Fixed Point below is still written to cached-source strength — "a plugin implements it" — and stops short of "a plugin is required" and of "Kubernetes ships none by default." Curriculum-alignment R1/R2 report that Stage 2 DID close this gap on 2026-08-24 with a fetch of kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/, sourcing "A CNI plugin is required to implement the Kubernetes network model" — but that snapshot was never written to ../Book-KCNA/sources/ (the Stage 2 run's write paths were refused; the body survives verbatim in research-manifest.md §1). k8s-docs-network-plugins-2026-08-24.md does not exist on disk, so the tag cannot be cited here without inventing it. Land that snapshot, then strengthen this Fixed Point to "required," and update Exam Alert #12 and the trap-table row "Kubernetes ships the network" to match.
     Second item, same fetch: per curriculum R3 and Stage 2 Notes #1, this section no longer names the kubelet as the executor of CNI binaries. The general extension-points page says the kubelet executes them; the more specific network-plugins page records that CNI management was removed from the kubelet in Kubernetes 1.24, with the container runtime loading the plugins. Naming no executor is the safe form at associate tier. Do not restore "external programs that the kubelet executes."
     Third item, same fetch: it would also restore the mechanism-level detail (node-to-node tunnels, BGP advertisement of Pod CIDRs to physical routers, kernel-level interception) that the 🔭 Closer Look below has been narrowed out of per fact-accuracy F6. -->

★ **Fixed Point:** Kubernetes **defines** the network model. A **CNI network plugin implements** it. The four rules above are requirements the plugin satisfies, not machinery Kubernetes provides [source: k8s-docs-extending-kubernetes-2026-08-23].

<!-- AUTHOR-REVIEW: fact-accuracy F4 — "cluster networking plugins commonly ship as DaemonSets" is untagged in the paragraph below. No cached snapshot describes any plugin's deployment shape; k8s-docs-cluster-addons-2026-08-24 lists Calico, Cilium and Flannel with installation links and says nothing about packaging. Two fixes, neither available in this pass: (a) propagate whatever source tag Chapter 6 §7 carries for the same claim, if it carries one — attribution to Ch 6 does not discharge the sourcing obligation on its own; (b) fetch kubernetes.io/docs/concepts/workloads/controllers/daemonset/, whose "Use cases" section covers cluster networking daemons directly, and which Chapter 6 likely wants cached regardless. Retained rather than cut because it is a retrieval of shipped Ch 6 material and the per-node reasoning is the paragraph's payoff. Build nothing further on it until it is tagged. -->

Chapter 6 noted in passing that cluster networking plugins commonly ship as DaemonSets — one Pod on every node. At the time that was an isolated fact about DaemonSets; now it is a satisfying one. A thing that must configure networking on every node is exactly a thing that wants one copy per node. *[cross-bearing: see Ch 6 §7 — DaemonSets and per-node infrastructure]*

> 🔭 **Closer Look:** The model is a *requirement*, not a description of a mechanism, and that is why implementations differ so widely. The three plugins named above already span overlay and non-overlay networks, with or without BGP, native routing or encapsulation, and an eBPF-based data plane [source: k8s-docs-cluster-addons-2026-08-24]. Those are genuinely different pieces of engineering, and every one of them satisfies the same four rules. An application inside the cluster cannot tell which one it is running on: the model is the contract, and it is the same contract underneath all of them. That last part is the point. Deeper than the exam requires.

One practical consequence, and it retrieves last chapter at exactly one chapter's distance: a node whose network is not correctly configured reports the **`NetworkUnavailable`** condition — `True` if the network for the node is not correctly configured [source: k8s-docs-nodes-2026-08-23]. You met the node condition list in Chapter 8 *[cross-bearing: see Ch 8 §4 — node conditions]*. This is the shortest demonstration available that the plugin is not a footnote.

Rule 2's hedge — *barring intentional network segmentation* — is doing quiet work. Kubernetes has an API for segmenting Pod-to-Pod traffic on purpose, and it is a Chapter 10 subject *[cross-bearing: see Ch 10 §6 — NetworkPolicy]*.

So: every Pod has an address, and any Pod can use it. Which would settle the matter, except that those addresses belong to Pods, and you already know what happens to Pods.

---