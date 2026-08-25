## Exam Alert! 🚨

**High-Priority Topics**

1. **Ingress exposes HTTP and HTTPS only.** No arbitrary ports, no other protocols; anything else uses NodePort or LoadBalancer.
2. **You must have an Ingress controller.** Creating an Ingress resource alone has no effect.
3. **Frozen, not deprecated** — GA, stability guarantees, no removal plans, **and** no further development. Both halves or nothing.
4. **The project recommends using Gateway instead of Ingress.** That is the recommendation as written — it carries no qualifier about new work or existing work. Reading it as *use Gateway for new work* is this book's operational gloss, not the project's wording; §4 sets out why that reading is fair and what it does not license.
5. **Simple fanout routes by URI; name-based virtual hosting routes by host.** Both put many Services behind one address.
6. **An Ingress may terminate TLS**, using a Secret that contains a private key and certificate; traffic onward to the Pods is cleartext.
7. **A Pod is non-isolated in both directions by default.** All ingress and all egress allowed.
8. **Policies are additive and never conflict. There is no deny rule.**
9. **Both ends must allow the connection** — the source's egress and the destination's ingress.
10. **NetworkPolicies are implemented by the network plugin.** No supporting plugin, no effect.
11. **GatewayClass / Gateway / HTTPRoute**, mapped to infrastructure provider / cluster operator / application developer. Exactly one GatewayClass per Gateway; many Routes.
12. **Node-local traffic is always allowed, and a Pod cannot block access to itself.**

**Common Traps** — each one has a specific wrong belief behind it, and the correction is the thing to carry into the exam room.

| The trap | The correction |
|---|---|
| "Creating an Ingress object exposes the app" | Only creating an Ingress resource has no effect. A controller must be running. |
| "Ingress can expose any protocol" | HTTP and HTTPS only. Everything else goes back to NodePort or LoadBalancer. |
| "Ingress is deprecated and will be removed" | Frozen. GA, guaranteed, no removal plans — and no further development. |
| "All Ingress controllers behave identically" | Ideally they fit the reference specification. In reality they operate slightly differently. |
| "Creating a NetworkPolicy secures the cluster" | Only if the network plugin implements NetworkPolicy. Otherwise: no effect, no signal. |
| "A Pod with no NetworkPolicy is closed by default" | Backwards. Non-isolated in both directions until something selects it. |
| "One NetworkPolicy can deny what another allows" | There is no deny rule. Policies combine by union. |
| "Only one end needs to permit the connection" | Both. Source's egress *and* destination's ingress. |
| "NetworkPolicy can block node-local or self traffic" | Neither. Both exceptions are unconditional. |
| "NetworkPolicy can do TLS / name targeting / logging / explicit deny" | All four are on the published out-of-scope list. |
| "Virtual hosting is just DNS" | Opposite sides of the connection. DNS resolves before traffic moves; virtual hosting sorts traffic that has arrived. |
| "Gateway API is a rename of Ingress" | Different API, different resource model, built around a different organising principle. |
| "NetworkPolicy can target a Service" | It selects Pods. Targeting Services by name is explicitly out of scope. |
| "An Ingress controller and a NetworkPolicy plugin are unrelated concerns" | Functionally unrelated. Structurally identical — which is §8. |

**A note on frequency.** Every trap above is a real point of confusion, drawn from the documentation's own emphases and from what the material makes easy to get wrong. What this book will not tell you is how often any of them appears on the exam. The published curriculum gives four domain weights and nothing finer [source: cncf-kcna-curriculum-pdf-2026-08-23] — no question counts, no per-competency split, nothing that would let anyone honestly attach a number to a single trap. Inventing one would be worse than saying nothing.

<!-- AUTHOR-REVIEW: The stronger negative claim in the prior draft — that "the exam's question distribution is not published" anywhere — cannot be verified against the cached corpus, which holds no exam-logistics snapshot at all (no question count, duration, passing score, or distribution). The sentence has been narrowed to what `cncf-kcna-curriculum-pdf-2026-08-23` actually supports: the curriculum publishes four domain-level percentages and nothing finer. Restoring the broader claim requires a research gap for the Linux Foundation KCNA exam/registration page. -->

---