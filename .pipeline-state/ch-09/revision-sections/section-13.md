## 🔵 §6 — The Component That Makes It Real

You now know what a Service declares and where its backends are recorded. Nothing so far has moved a packet.

### One component, one job

**Every node in a Kubernetes cluster runs a kube-proxy** — unless you have deployed your own alternative component in its place. The kube-proxy component is responsible for implementing a **virtual IP mechanism for Services of type other than ExternalName**. Each instance of kube-proxy watches the Kubernetes control plane for the addition and removal of **Service and EndpointSlice objects**. For each Service, kube-proxy calls appropriate APIs — depending on the kube-proxy mode — to configure the node to **capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints** (usually a Pod, but possibly an arbitrary user-provided IP address) [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

Chapter 3 introduced kube-proxy as a node component — a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept [source: k8s-docs-cluster-architecture-2026-08-23] — and left the "how" for here. *[cross-bearing: see Ch 3 §4 — kube-proxy as a node component]*

And then there is this sentence, which you should read twice:

> A control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server. [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]

A control loop. Watching objects, comparing to actual state, reconciling. You have met that shape in Chapters 3, 4, 6, 7 and 8, and here it is again in a reference page about packet forwarding. File that; §8 collects it.

### The cluster IP is virtual

Here is the consequence that reframes everything before it.

**Nothing is listening on a cluster IP.** No process is bound to it. There is no host at that address, no socket, no server. It exists only as a rule, replicated on every node, that says: *packets addressed here go to one of those addresses instead.* That is not a separate fact to memorise — it follows directly from what the documentation says kube-proxy does, which is **capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints** [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Capture and redirect. Nothing in that sentence binds a socket.

<!-- FIGURE: ch09-fig04-kube-proxy-modes -->
```
                       ┌──────────────┐    ┌──────────────────┐
        kube-proxy ───►│   Service    │    │  EndpointSlice   │
        watches        │  10.96.0.42  │    │ 10.244.1.7:5432  │
                       └──────────────┘    │ 10.244.4.2:5432  │
                              │            └──────────────────┘
                              │ programs           │
   ═══ node: worker-3 ════════▼════════════════════▼══════════════════
                                                                     ║
   ┌──────────┐        ┌ ─ ─ ─ ─ ─ ─ ─ ┐                             ║
   │ frontend │        ╎ 10.96.0.42    ╎  ◄── the cluster IP.        ║
   │   Pod    │───────►╎  (nothing is  ╎      no process. no socket. ║
   └──────────┘  to    ╎   here)       ╎      an address with        ║
             10.96.0.42└ ─ ─ ─ ─ ─ ─ ─ ┘      nothing at it.         ║
                              ┊                                      ║
              ┏━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━┓                     ║
              ┃   R U L E S   L A Y E R        ┃ ◄─ traffic passes   ║
              ┃  ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄  ┃    THROUGH, is not   ║
              ┃  mode: iptables (default) ·    ┃    delivered TO      ║
              ┃        IPVS · nftables ·       ┃                     ║
              ┃        kernelspace (Windows)   ┃                     ║
              ┗━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━┛                     ║
                        │ readdressed  │                             ║
                        ▼              ▼                             ║
                 ┌────────────┐   ┌──────────────────────────────────╨──┐
                 │ 10.244.1.7 │   │ 10.244.4.2  (on worker-11)          │
                 └────────────┘   └─────────────────────────────────────┘
```

This is also why §3's ExternalName exclusion makes sense from the other side. An ExternalName Service has **no address to intercept** — it produces a CNAME and nothing else — so there is nothing for kube-proxy to program. The exclusion isn't a special case; it falls straight out of what kube-proxy does.

> ⚓ **Worth Securing:** Nothing is listening on a cluster IP. It is not a host, not a process, not a port on a machine. It is a rule on every node that **captures** traffic to that address and **redirects** it elsewhere [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Once that lands properly, roughly half of the confusing behaviour in Kubernetes networking stops being confusing — including why the node-level tools you would ordinarily reach for show you nothing bound at that address, and why "a Service is a load balancer" was never quite right.

★ **Fixed Point:** kube-proxy implements the virtual IP mechanism for **every Service type except ExternalName**, by watching **Service and EndpointSlice** objects and programming each node. Modes: **iptables (the default)**, IPVS, nftables on Linux; **kernelspace** on Windows.

### The modes

On Linux nodes, the available modes for kube-proxy are: **iptables** — configures packet forwarding rules using iptables, and is **the default**; **ipvs** — configures packet forwarding rules using IPVS; **nftables** — configures packet forwarding rules using nftables, GA since Kubernetes 1.33. On Windows there is exactly one mode: **kernelspace** — configures packet forwarding rules in the Windows kernel [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

| Mode | Platform | Notes |
|---|---|---|
| `iptables` | Linux | **The default** |
| `ipvs` | Linux | |
| `nftables` | Linux | GA since v1.33 |
| `kernelspace` | Windows | The only mode on Windows |

That is the entire requirement at this level: recognise the four names, and know which one is the default. You do not need to understand how iptables chains differ from IPVS virtual servers, and this book is not going to pretend otherwise to fill a page. A candidate who can name the four and identify iptables as the default has everything this material is likely to ask for.

### kube-proxy is optional

One closing beat, and it is a nice one because it reaches back to §1.

**If you use a network plugin that implements packet forwarding for Services by itself, and provides equivalent behavior to kube-proxy, then you do not need to run kube-proxy on the nodes in your cluster** [source: k8s-docs-cluster-architecture-2026-08-23]. Cilium is a named example: it **can act as a replacement for kube-proxy** [source: k8s-docs-cluster-addons-2026-08-24].

So the plugin that implements the network model can also implement the Service data plane. Which is a good inoculation against reading kube-proxy as load-bearing architecture. It is one implementation of one job, and that job can be done elsewhere.

> 🔭 **Closer Look:** kube-proxy is optional. A plugin like Cilium can do the same work in its own eBPF data plane [source: k8s-docs-cluster-addons-2026-08-24]. If you meet a cluster running no kube-proxy at all, nothing is missing. Deeper than the exam requires, but useful the first time you see it and assume something is wrong.

*[cross-bearing: see Ch 17 §3 — a service mesh moves this interception into a sidecar or an ambient layer]*

---