## The Voyage Ahead

Everything you just learned works inside a boundary — water the cluster itself controls, where every address in play is one the cluster handed out.

Every name resolved to something already on this side of it. Every address was reachable by things already inside. NodePort and LoadBalancer reach outward, but only by *opening a door* — a port on every node, an address from a provider. Neither of them knows or cares what comes through it. They move packets to a Service, and the Service moves them to a Pod, and at no point does anything open the crate to see what the cargo is.

That's the ceiling §3 named. One external address per Service, which does not scale past a handful. No protocol awareness at all, so `shop.example.com/checkout` and `shop.example.com/catalog` are indistinguishable to every mechanism in this chapter.

Chapter 10 crosses the boundary. It introduces the objects that route on the *contents* of an HTTP request — hostnames, paths, headers — so that one address can serve many services, and something standing at the entrance finally reads the writing on the crate before deciding where it goes. It explains why the Kubernetes project now recommends one API over the one most people learned first, and what "frozen" means in that recommendation, which is a more precise word than it looks and worth exactly the attention you'd give a definition on an exam. And it introduces NetworkPolicy, which is what rule 2's *"barring intentional network segmentation"* was quietly gesturing at all along *[cross-bearing: see Ch 10 §6 — NetworkPolicy]*.

It also opens with an object that you create, and that does nothing at all — because the component that acts on it has not been installed. You have seen that shape twice in this chapter now. Chapter 10 gives it a name, and once it has a name you will start seeing it everywhere.

> *"A light is known by its character, not its position — and only because someone ashore keeps it burning to the same pattern."*
> — Lodestar Ledgers