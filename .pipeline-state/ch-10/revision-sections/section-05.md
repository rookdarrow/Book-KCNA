## What You'll Learn

By the end of this chapter, you'll be able to:

- **Place** any exposure mechanism on the correct side of the layer boundary — what operates on addresses and ports, and what opens the request and reads it.
- **State** what Ingress does, what it explicitly does not do, and which two protocols are the whole of its remit.
- **Distinguish** a simple fanout from name-based virtual hosting, and both from the DNS-based service discovery you learned last chapter.
- **Explain** why a correctly written Ingress can have no effect whatsoever, and name the thing whose absence causes it.
- **Say what `frozen` means** — precisely, in both of its halves — and why it is not the same word as `deprecated`.
- **Name** the three role-mapped Gateway API resources and the organisational role each one belongs to.
- **Predict** whether a given connection is allowed under a given set of NetworkPolicies, using rules that are additive, allow-only, and enforced at both ends of the connection — and starting from the posture a Pod holds before any policy has selected it.
- **Describe** what becomes of a NetworkPolicy that the cluster's network plugin does not implement, and why that failure is the harder of this chapter's two to notice.

*You'll also acquire one rule that outlives this chapter: an object without its component does nothing. You'll use it in Chapter 13, in Chapter 17, and on things this book never gets to.*

---