## ☆ Taking Your Bearings #3

Five questions on §6 and §7 — what is permitted, how permissions add up, and what the mechanism cannot reach.

**1.** 🔵 `[retrieval: ch4]` Chapter 4 said a NetworkPolicy selects both its subject and its peers. Point at the two selectors in that sentence and say what each one is choosing.

**2.** 🔵 A Pod in namespace `prod` has no NetworkPolicy selecting it anywhere in the cluster. What inbound and outbound traffic is permitted?

**3.** 🟡 **⚠️ This one is intentionally hard. Struggle is the point.** Two NetworkPolicies select the same Pod. Policy A permits inbound traffic from `app: web`. Policy B permits inbound traffic from `app: batch`. What is permitted, and could a third policy be written to forbid `app: web`? If it could not, what *would* you write to close every Pod in that namespace to all inbound traffic?

**4.** 🟡 Pod `frontend` has an egress policy permitting traffic to `app: api`. Pod `api` has an ingress policy permitting traffic only from `app: admin`. Can `frontend` reach `api`?

**5.** 🔵 You apply a NetworkPolicy intended to block traffic from a specific Pod. Traffic still flows. Name two distinct explanations, one of which is not a mistake in the policy.

---

**Answers with Explanations:**

**1. `[retrieval: ch4]` The policy's own top-level `podSelector` chooses which Pods the policy applies to. The selectors inside its rules — `podSelector` and `namespaceSelector` under `from`/`to` — choose which Pods and namespaces those Pods may talk to.**

Each NetworkPolicy includes a `podSelector` which selects the grouping of Pods to which the policy applies [source: k8s-docs-network-policies-depth-2026-08-24]; separately, the selectors in an `ingress from` or `egress to` section select Pods and namespaces as allowed sources or destinations [source: k8s-docs-network-policies-depth-2026-08-24].

Six chapters ago, learning about labels, you were told this object would use one mechanism for two jobs. This is the structural insight §6 is built on, and you should be able to point at both selectors in a manifest without hesitating.

**2. All of both — the Pod is non-isolated for ingress and for egress.**

By default a Pod is non-isolated in both directions, and becomes isolated only when some policy both selects it and names that direction in `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24].

Wrong answer to reject explicitly: *"no policy means no traffic."* That is the firewall instinct, and it is exactly backwards. It is also the single most consequential wrong belief a reader can bring to this material, because someone holding it will look at a cluster with no NetworkPolicies and conclude it is locked down.

**3. Inbound from both `app: web` and `app: batch` — the lists combine additively. No: there is no deny rule, so nothing can subtract a permission; removing that access means removing the grant. And to close the namespace, you write a policy that selects every Pod in it and grants nothing.**

Network policies do not conflict; they are additive, and the connections allowed in a direction are the union of what the applicable policies allow [source: k8s-docs-network-policies-depth-2026-08-24]. The ability to explicitly deny is on the published out-of-scope list [source: k8s-docs-network-policies-depth-2026-08-24].

**If you spent a while looking for the deny rule before accepting there isn't one, that is the correct experience of this question.** Every firewall you have configured had one. The absence is genuinely strange, and it is worth stating as a *semantic* rather than a NetworkPolicy quirk: **the model has no subtraction operator.** Permissions compose by union and only by union, order of evaluation is irrelevant, and the only way to reduce what is permitted is to change what grants it.

The third part is the constructive half, and it follows from the first two rather than being a separate technique. An empty `podSelector` selects every Pod in the namespace [source: k8s-docs-network-policies-depth-2026-08-24]; a policy that selects them all, names `Ingress`, and offers no `from` entries isolates every one of them for ingress while permitting nothing. The union of an empty set of grants is empty. **Denial is reached by selecting broadly and granting nothing — never by forbidding.** If you derived that before reading it, you have the model.

Hold on to the phrasing about subtraction. Chapter 12 retrieves this exact semantic by name and builds an argument on it *[cross-bearing: see Ch 12 §9 — additive, never deny]*.

**4. No.** For a connection from a source Pod to a destination Pod to be allowed, both the egress policy on the source and the ingress policy on the destination must allow it; if either side does not, the connection will not happen [source: k8s-docs-network-policies-depth-2026-08-24].

`frontend`'s egress policy is correct and permits exactly what it should. It is also irrelevant on its own, because `api` never granted `frontend` anything. A clearance to depart is not a clearance to enter — the far harbour issues its own, and this one did not. Two objects, both individually sensible, and the connection still fails, which is why this rule costs practitioners so much time.

**5. Either: the network plugin does not implement NetworkPolicy, so the resource has no effect at all; or the traffic falls under one of the unconditional exceptions — a Pod cannot block access to itself, and traffic to and from its own node is always allowed** [source: k8s-docs-network-policies-depth-2026-08-24].

The question deliberately requires you to entertain that **the object may be perfect and still inert.** That is a move most troubleshooting instincts do not make; the reflex is to re-read the YAML, and the YAML is fine.

Say the detection problem out loud, because it is the part worth carrying: **a policy that is not enforced looks exactly like a policy that is enforced against traffic nobody is sending.** There is no observable difference. That is a property of the mechanism, not of anyone's attention.

---

**Checkpoint: You've Now Mastered**

✓ Non-isolated by default, in both directions, until something selects
✓ Additive, allow-only, no deny rule, order-independent
✓ Denial by construction — select everything, grant nothing
✓ Both ends must allow it
✓ The plugin dependency, and the ten things the API cannot do

One section left, and it is about something you already noticed.

---