## ⚪ §1 — Where LoadBalancer Runs Out

You already have the argument. Chapter 9 made it, and made it recently.

One external address per Service. Fifty Services, fifty addresses, fifty provisioned load balancers, fifty bills, fifty things to manage. And no Service type in that chapter reads HTTP, so a single address cannot serve two paths. A Service knows an address and a port, and stops there *[cross-bearing: see Ch 9 §3 — the Service-type ladder and the exposure ceiling]*.

That is the ceiling. This section does not re-derive it. It names the vocabulary the rest of the chapter runs on, and gets out of the way.

### The layer boundary

Everything in Chapter 9 operates at what practitioners call **layer 4**. A Service moves packets to an address and a port and has no opinion about what those packets contain. Everything in §2 through §5 operates at **layer 7**: it reads the request — the host it was addressed to, the path it asked for, sometimes the headers it carries — and decides where to send it on that basis.

The documentation sorts the same two groups without putting layer numbers on them. It describes Ingress as protocol-aware HTTP/HTTPS routing using URIs, hostnames, and paths; Gateway API as dynamic infrastructure provisioning and advanced traffic routing; and `type: LoadBalancer` as the simpler but less configurable mechanism for getting traffic into a cluster [source: k8s-docs-network-model-2026-08-23]. The one place it does reach for OSI numbers is NetworkPolicy, which it places at the IP address or port level — layer 3 or 4 [source: k8s-docs-network-model-2026-08-23]. That is not a coincidence, and §6 is where it pays.

Keep this boundary marked. It is not decoration and it is not only about §2. §6 goes back *down* to layers 3 and 4, and a reader who has lost the ladder will experience NetworkPolicy as an unrelated topic that happened to land in the same chapter.

> ★ **Fixed Point:** Everything in Chapter 9 moves **packets** to an address. Everything in §2 through §5 reads **requests**. Which side of that boundary a mechanism sits on determines what it can know, and therefore what it can decide.

### North-south and east-west

Two words from ordinary industry vocabulary that this book has not used yet. They make the shape of this chapter sayable in one sentence.

**North-south** traffic enters the cluster from outside. **East-west** traffic moves between Pods inside it. Those two definitions are the industry's, not the project's — what the Kubernetes project supplies is the pairing, in a blog post on Gateway API rather than in the reference documentation, describing the API's initial focus as ingress, "north-south," traffic, and service mesh as the "east-west" case [source: k8s-blog-gateway-api-north-south-east-west-2026-08-24].

This chapter does one of each. §1 through §5 are about north-south. §6 and §7 are about east-west.

<!-- AUTHOR-REVIEW: the question-quality audit flags north-south/east-west as taught, mnemonic'd, and summarised but never assessed, and offers two remedies: test the pair once, or drop the mnemonic. Kept here on the assumption the question pass takes the first option — the mnemonic also sets up §1's closing harbour-wall figure. If no question is added, revisit. -->

> 🪢 **Mnemonic:** *North-south goes through the wall; east-west stays inside it.* §1–§5 is the wall. §6–§7 is inside.

### The edge router

One piece of scaffolding Chapter 9 did not supply, and §3 will need.

The Kubernetes documentation is explicit that in most common deployments, **the nodes in your cluster are not part of the public internet** [source: k8s-docs-ingress-depth-2026-08-24]. Something sits between the two: the **edge router**, a router that enforces the firewall policy for your cluster, whether that is a gateway managed by a cloud provider or a physical piece of hardware [source: k8s-docs-ingress-depth-2026-08-24].

Naming it here means that when §3 tells you an Ingress controller may fulfil an Ingress "usually with a load balancer, though it may also configure your edge router," you already know what that clause is about.

The same terminology block gives the vocabulary for everything else in this chapter, and it should all be familiar: a **node** is a worker machine, part of a cluster; the **cluster network** is the set of links, logical or physical, that carry communication within a cluster according to the Kubernetes networking model; a **Service** identifies a set of Pods using label selectors and is assumed to have a virtual IP routable only within the cluster network [source: k8s-docs-ingress-depth-2026-08-24]. That last clause is the whole problem in one line. The addresses Chapter 9 gave you work beautifully inside the harbour wall, and mean nothing beyond it.

### What comes next, and the first thing worth knowing about it

There is an object for the layer-7 job. It is called Ingress.

And the first thing to know about it is that writing one may accomplish nothing at all. We will get to why in §3. Carry the expectation into §2 *[cross-bearing: see Ch 10 §3 — the Ingress controller and what its absence costs]*.

*[cross-bearing: see Ch 17 §5 — a service mesh does at layer 7 for east-west traffic roughly what §2 does for north-south]*

---