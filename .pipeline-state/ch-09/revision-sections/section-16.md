## ⚪ §8 — A Query With a Name

Back to the claim from the opening. **There is one object in this chapter, and it does not do anything.**

A Service is a **label query with a name attached**. Everything else in this chapter is a control loop reconciling that query's current answer against some piece of the network.

Walk it back through, in the chapter's own order.

**From §2.** The Service is an object. You `apply` it through the same API server door as everything else, and its `spec` is a statement of desired state in exactly the sense Chapter 4 defined: *these Pods should be reachable at a stable address.* It does not run. It does not receive traffic. It states a condition that should hold.

**From §4.** The EndpointSlice controller watches Services and Pods, evaluates the selector, and writes down the answer [source: k8s-docs-cluster-architecture-2026-08-23]. Desired state, observed state, reconciliation. **And this is the same shape as the ReplicaSet controller running over the same labels for an entirely different purpose** — which is exactly what Chapter 6 was telling you when it distinguished selection from ownership. Two loops, one label set, no coordination, no conflict. *[cross-bearing: see Ch 6 §2 — selection versus ownership]*

**From §6.** kube-proxy watches Services and EndpointSlices and programs each node. The documentation says so in as many words: *a control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server* [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. That is the sixth control loop in this book, and you should count it.

**From §7.** Cluster DNS publishes the answer as a name. Same input, third consumer, third format.

**From §1.** And underneath all of it, none of the actual packet-moving is Kubernetes' work at all. Kubernetes defines the network model; a CNI plugin implements it [source: k8s-docs-extending-kubernetes-2026-08-23] — which is the second instance of an arrangement you first met in Chapter 2, where CRI does the same thing for container runtimes. *[cross-bearing: see Ch 2 §4 — CRI as the first pluggable interface]*

<!-- FIGURE: ch09-zenith-stable-name-over-churn -->
```
   ╔═══════════════════════════════════════════════════════════════════════╗
   ║        database.production.svc.cluster.local   ·   10.96.0.42         ║
   ╚═══════════════════════════════════════════════════════════════════════╝
        ▲                    ▲                    ▲                   ▲
        │  t₀                │  t₁                │  t₂               │  t₃
   ┌────┴─────┐        ┌─────┴────┐         ┌─────┴────┐        ┌─────┴────┐
   │ ▲  ▲  ▲  │        │ ▲  ●  ●  │         │ ●  ■  ■  │        │ ◆  ◆  ◆  │
   │.1.7 .4.2 │        │.1.7 .2.8 │         │.2.8 .5.1 │        │.7.3 .8.9 │
   │   .4.3   │        │    .2.9  │         │    .5.4  │        │    .9.0  │
   └──────────┘        └──────────┘         └──────────┘        └──────────┘
     (nothing survives from t₀ to t₃ — not one Pod, not one address)

   ┌───────────────────────────────────────────────────────────────────────┐
   │   query  ────────►  answer  ────────►  publish                        │
   │  (app: db)        (EndpointSlice)          │                          │
   └────────────────────────────────────────────┼──────────────────────────┘
                     ┌──────────────────────────┼──────────────────────────┐
                     ▼                          ▼                          ▼
              ┏━━━━━━━━━━━━┓           ┌──────────────┐           ┌────────────────┐
              ┃ rules layer┃           │ endpoint list│           │  DNS record    │
              ┃   (§6)     ┃           │     (§4)     │           │     (§7)       │
              ┗━━━━━━━━━━━━┛           └──────────────┘           └────────────────┘
                three readers · one answer · one question that never changed
```

☀️ **Zenith:** A Service is a **label query with a name**. The virtual IP, the endpoint list, and the DNS record are three control loops publishing that one query's current answer in three different formats. The Pods were never the stable thing. **The question was.**

That is the chapter's title, made good on. The stable thing was never a Pod — you knew that after §2. But it was never really an IP address either: the cluster IP belongs to nothing, nothing listens on it, and it exists only as a rule that other machinery maintains. What is actually stable is *"which Pods carry the label `app: db` and are Ready"* — a question whose answer is different every few minutes and whose **meaning** is the same forever. Pods churn beneath it the way water churns beneath a fixed star. The question doesn't move.

That is what makes churn survivable. And it is why the abstraction is a declaration rather than a device: a device would have to be somewhere, and would fail when that somewhere failed. A question does not have a location.

### Where the claim overreaches

The claim is a slogan, and slogans need narrowing until they're true.

§3's type ladder and §7's record shapes are **not** consequences of this architecture. They are facts about an API — decisions somebody made about what to call things and how many layers to stack. You cannot derive "NodePort also allocates a cluster IP" from "a Service is a label query," and you cannot derive `_port-name._port-protocol.` from anything at all. Those you memorise, the same as anyone.

Everything else in this chapter, you can rebuild from §1's model plus the observation above. That is a genuinely useful ratio, and it is worth knowing which side of the line each fact sits on before you spend study time on it.

> ⚓ **Worth Securing:** The practical form of the Zenith, for when Kubernetes networking does something you didn't expect. Ask two questions: **what does the selector currently match?** and **which loop hasn't caught up yet?** Between them they cover most of it — and both are answerable with `kubectl` in under a minute, which is more than can be said for most debugging heuristics.

*[cross-bearing: see Ch 15 §5 — the control loop, generalised, pointed at a Git repository]*. This chapter observes that Kubernetes networking is *made of* control loops. Chapter 15 makes the larger argument, and it is the structural claim this whole book is building toward. Don't get ahead of it.

### The boundary

Everything in this chapter has been about the inside of the cluster.

Every name you learned resolves to something with a Pod behind it — or, in ExternalName's case, to a name that isn't Kubernetes' business at all. Every address you learned is reachable only by things that are already in. Even NodePort and LoadBalancer, the two types that reach outward, do it by *offering a door*, not by describing what comes through it or where it should go.

Chapter 10 crosses that boundary properly: one address serving many services, routing decisions made on the contents of an HTTP request rather than on a destination address, and a rule about what happens when you create the object and nobody has installed the thing that acts on it.

---