## 🔵 §3 — Four Ways to Be Reachable

There are four Service types. Three of them are layers of the same mechanism. One of them is not a layer at all, and confusing it for one is the most reliable way to lose a point in this competency.

### The three that stack

**ClusterIP** exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default that is used if you don't explicitly specify a type for a Service [source: k8s-docs-service-2026-08-23].

**NodePort** exposes the Service on each node's IP at a static port — the node port. And here is the part candidates miss: to make the node port available, **Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP`** [source: k8s-docs-service-2026-08-23]. NodePort does not replace ClusterIP. It adds to it.

**LoadBalancer** exposes the Service externally using an external load balancer [source: k8s-docs-service-2026-08-23]. It is the outermost rung — the one that puts an address in *front* of the cluster rather than inside it.

<!-- FIGURE: ch09-fig02-service-types-ladder -->
```
   ┌─ LoadBalancer ─────────────────────────────────────────┐
   │  reachable from: the internet                          │
   │  (external LB supplied by your cloud provider,         │
   │   NOT by Kubernetes)                                   │
   │                                                        │
   │  ┌─ NodePort ───────────────────────────────────────┐  │
   │  │  reachable from: anything that can reach a node   │ │
   │  │  <node-ip>:<static-port>, on every node           │ │
   │  │                                                   │ │
   │  │  ┌─ ClusterIP ─────────────────────────────────┐  │ │
   │  │  │  reachable from: inside the cluster only    │  │ │
   │  │  │  (the default type)                         │  │ │
   │  │  └─────────────────────────────────────────────┘  │ │
   │  └───────────────────────────────────────────────────┘ │
   └────────────────────────────────────────────────────────┘

   Each ring ADDS to the ones inside it. Asking for an outer ring
   does not remove the inner ones — a NodePort Service still has
   its cluster IP.


   ════════════════════════════════════════════════════════════
   NOT ON THE LADDER. NOT A FOURTH RING. SEPARATE MECHANISM.
   ════════════════════════════════════════════════════════════

        ExternalName
        my-svc ──── CNAME ────► api.foo.bar.example
        no cluster IP · no endpoints · no proxying of any kind
```

★ **Fixed Point:** The ladder types are **additive**, and the documented case is the one to memorize: **a NodePort Service also has a cluster IP — Kubernetes sets one up, exactly as if you had requested `type: ClusterIP`** [source: k8s-docs-service-2026-08-23]. Asking for a higher rung never removes the rungs below it.

<!-- AUTHOR-REVIEW: fact-accuracy F2 flagged the stronger form of this claim — that a LoadBalancer Service also carries a node port and a cluster IP — as untagged. The cached `k8s-docs-service-2026-08-23` snapshot documents the allocation for NodePort only; its LoadBalancer entry is one sentence and says nothing about what sits beneath. Curriculum-alignment R5 records that Stage 2 did fetch a page carrying "NodePort and LoadBalancer are supersets of ClusterIP", but that snapshot (`k8s-docs-service-ports-2026-08-24`) was never written to `sources/` and so cannot be cited here. The Fixed Point above has therefore been narrowed to the documented rung. When the snapshot lands, restore the explicit LoadBalancer clause here, in the figure annotation, and in the Bearings #1 item 3 answer key. -->

### The one that is not on the ladder

**ExternalName** maps the Service to the contents of the `externalName` field — for example, to the hostname `api.foo.bar.example`. The mapping configures your cluster's DNS server to return a **CNAME record** with that external hostname value. **No proxying of any kind is set up** [source: k8s-docs-service-2026-08-23].

Read that last sentence as the definition rather than as a footnote. An ExternalName Service has no cluster IP. It has no endpoint list. Nothing intercepts a packet on its behalf, because there is no address to intercept traffic *to*. When a client resolves its name, DNS hands back a different name, and the client connects to whatever that resolves to — directly, with Kubernetes entirely out of the path.

It is a DNS alias flying a Service's colours.

> ⚠ **Navigational Hazards:** ExternalName is not the fourth rung of the ladder. It allocates no address, selects no Pods, and proxies nothing — it is a CNAME record and nothing more. Every exam question that presents it as "the type you use for external things" is testing exactly this. The word "External" in two type names (ExternalName, and LoadBalancer's external load balancer) is doing you no favours; they have nothing mechanically in common.

### The other fact that catches people

Choosing `type: LoadBalancer` does not cause Kubernetes to load-balance anything.

**Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider** [source: k8s-docs-service-2026-08-23].

What `type: LoadBalancer` does is *signal* that an external load balancer should be provisioned. On a managed cluster with cloud-provider integration, something notices that signal, provisions a load balancer, and reports its address back. On a bare-metal cluster with no such integration and no add-on that provides one, a `type: LoadBalancer` Service sits there with no external address indefinitely. Not for thirty seconds. Indefinitely — the signal is raised correctly, and there is nobody ashore to answer it.

And nothing is broken. The object is correct; the declaration is valid; the piece that would act on it is not present. Hold on to that shape — you will see it again in §4, and Chapter 10 will give it a name.

★ **Fixed Point:** **Kubernetes provides no load balancer.** `type: LoadBalancer` is a request for one from somewhere else — your cloud provider, or a component you install.

> 🪢 **Mnemonic:** *Inside · on every node · out in the world · somewhere else entirely.* ClusterIP, NodePort, LoadBalancer, ExternalName — in the order you will meet them, with the last one deliberately phrased so it doesn't sound like a continuation.

### Choosing

Four lines, not a flowchart. The exam tests the definitions and the additivity far more often than it tests the decision.

- Traffic stays inside the cluster → **ClusterIP**.
- You need a fixed port on every node, usually because something in front of the cluster will target it → **NodePort**.
- You have a cloud provider that will hand you an external address → **LoadBalancer**.
- You want an in-cluster name for something that isn't in the cluster at all → **ExternalName**.

<!-- AUTHOR-REVIEW: outline § Open questions #3 flags that `port` vs `targetPort` vs `nodePort`, and the default NodePort range (commonly cited as 30000-32767), are entirely uncached. The outline resolved this in favour of option (a) — fetch and add a short block — and curriculum-alignment R5 records that Stage 2 DID complete that fetch on 2026-08-24. The snapshot was never written to `sources/` (the Stage 2 run could not write to disk); its body survives verbatim inside `research-manifest.md` §3, but `k8s-docs-service-ports-2026-08-24.md` does not exist on disk and cannot be cited. Per the outline's own guidance ("a half-mention is worse than silence"), this section therefore still says nothing about port fields. This is now a plumbing blocker, not a research gap: extract the snapshot to `sources/`, re-run corpus assembly, and the block's natural home is right here, after the decision list. -->

*[cross-bearing: see Ch 8 §1 — a Service is created by the same `apply`, through the same API server door, as every other object]*

### The ceiling

One thing before you leave this section, because Chapter 10 is going to need it.

A LoadBalancer Service gives you one external address per Service. That is fine for one Service. It is expensive and awkward for fifty.

And none of these four types knows anything about HTTP. They move packets. They cannot route on a hostname, or a URL path, or a header, because at the layer they operate at those things are just bytes in a payload. If you want `shop.example.com/checkout` and `shop.example.com/catalog` to reach different backends behind one address, no Service type in this list can do it.

Protocol awareness is precisely what the next layer up exists to supply: **the Gateway API, or its predecessor Ingress, makes Services accessible to clients outside the cluster, with protocol-aware HTTP/HTTPS routing using URIs, hostnames, and paths** [source: k8s-docs-network-model-2026-08-23]. The address arithmetic — one per Service, fifty Services — is this book's own argument for getting there sooner rather than later. Chapter 10 opens exactly there. *[cross-bearing: see Ch 10 §1 — the exposure ceiling and what crosses it]*

---