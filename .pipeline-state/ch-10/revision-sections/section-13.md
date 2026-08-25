## 🔵 §6 — Allowing, Never Denying

One piece of housekeeping before we get under way, and it is not politeness.

**The word `ingress` is about to mean something completely different, and capitalisation is the tell.** For four sections, `Ingress` has meant an API object and the controller that fulfils it. From here to the end of §7, lowercase `ingress` means **a direction of traffic**: inbound, as opposed to `egress`, outbound. NetworkPolicy has nothing to do with the Ingress object. If you carry the old meaning into this section, you will spend §7 trying to work out how the Ingress controller fits in, and it does not.

Good. Now the object.

### What a NetworkPolicy controls

**NetworkPolicies let you specify rules for traffic flow at the IP address or port level — OSI layer 3 or 4 — within your cluster, and also between Pods and the outside world** [source: k8s-docs-network-policies-depth-2026-08-24]. They are an **application-centric construct**, which lets you specify how a Pod is allowed to communicate with various network *entities* — a word the documentation chose deliberately to avoid overloading "endpoints" and "services," which already have specific Kubernetes meanings [source: k8s-docs-network-policies-depth-2026-08-24]. And they **apply to a connection with a Pod on one or both ends, and are not relevant to other connections** [source: k8s-docs-network-policies-depth-2026-08-24].

Note what that rules out. This is **network reachability**: who may open a connection to whom, at layer 3 or 4, and nothing else. It is not the boundary between a workload and the host it runs on. Chapter 2 already told you those were different axes, and it told you on a graded question *[cross-bearing: see Ch 2 §7 — RuntimeClass, and workload-to-host isolation as a separate concern]*. The other axis of Pod security has its own chapter *[cross-bearing: see Ch 12 §5 — what a Pod may do to its node]*.

And note the layer. §1 spent five sections climbing to layer 7 to read hostnames and paths. This section is back down at 3 and 4, reading addresses and ports. Different problem, different altitude.

### Three identifiers, and two selectors doing different jobs

The entities a Pod can communicate with are identified through a combination of three identifiers [source: k8s-docs-network-policies-depth-2026-08-24]:

1. **Other Pods** that are allowed — with the exception that a Pod cannot block access to itself.
2. **Namespaces** that are allowed.
3. **IP blocks** — with the exception that traffic to and from the node where a Pod is running is always allowed, regardless of the IP address of the Pod or the node.

For Pod- and namespace-based policies, **you use a selector to specify what traffic is allowed to and from the Pods that match the selector.** For IP-based policies, you define the rule on **IP blocks (CIDR ranges)** [source: k8s-docs-network-policies-depth-2026-08-24]. *(CIDR notation is a way of writing a range of IP addresses as an address plus a prefix length: `172.17.0.0/16` means "the addresses whose first sixteen bits are those of 172.17.0.0." An `except` list carves ranges back out of the block — in the manifest below, everything in 172.17.0.0/16 apart from the addresses in 172.17.1.0/24. The glossary carries the expansion.)*

Chapter 4 saw this coming. It told you, six chapters ago, that **a NetworkPolicy selects both its subject and its peers** *[cross-bearing: see Ch 4 §5 — labels and selectors as the universal join]*. Pause on that, because it is the structurally most interesting thing in this section. Here is the shape:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:              # <-- chooses the SUBJECT: who this policy governs
    matchLabels:
      role: db
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - ipBlock:
        cidr: 172.17.0.0/16
        except:
        - 172.17.1.0/24
    - namespaceSelector:    # <-- chooses PEERS: who may connect
        matchLabels:
          project: myproject
    - podSelector:          # <-- also chooses PEERS
        matchLabels:
          role: frontend
    ports:
    - protocol: TCP
      port: 6379
  egress:
  - to:
    - ipBlock:
        cidr: 10.0.0.0/24
    ports:
    - protocol: TCP
      port: 5978
```

[source: k8s-docs-network-policies-depth-2026-08-24]

**Each NetworkPolicy includes a `podSelector` which selects the grouping of Pods to which the policy applies** — here, Pods labelled `role: db` [source: k8s-docs-network-policies-depth-2026-08-24]. That is the subject. Inside the rules, a different set of selectors chooses who may connect: `podSelector` selects particular Pods in the **same namespace as the NetworkPolicy** as allowed sources or destinations, and `namespaceSelector` selects particular namespaces for which **all** Pods are allowed [source: k8s-docs-network-policies-depth-2026-08-24].

One mechanism, the label selector you learned in Chapter 4, doing two entirely different jobs in one object, at two different depths of the same YAML.

> 🪝 **Snag:** Whether `namespaceSelector` and `podSelector` appear as one `from` entry or two changes the meaning completely. A single entry specifying **both** selects particular Pods *within* particular namespaces, an AND. Two entries in the `from` array is an OR: connections from Pods in the local namespace with the peer label, **or** from any Pod at all in the matching namespaces [source: k8s-docs-network-policies-depth-2026-08-24]. One YAML hyphen is the difference. The documentation's own advice: when in doubt, use `kubectl describe` to see how Kubernetes has interpreted the policy [source: k8s-docs-network-policies-depth-2026-08-24].

### The two sorts of isolation

This is the centre of the section, and the place your firewall instinct gets corrected.

There are **two sorts of isolation for a Pod: isolation for egress, and isolation for ingress.** They concern what connections may be established. "Isolation" here is **not absolute** — it means *some restrictions apply*. The alternative, "non-isolated for a direction," means that **no restrictions apply** in that direction. The two are declared independently, and both are relevant for a connection from one Pod to another [source: k8s-docs-network-policies-depth-2026-08-24].

**Egress.** By default, a Pod is **non-isolated for egress; all outbound connections are allowed.** A Pod becomes isolated for egress if there is **any** NetworkPolicy that both **selects the Pod** and has `Egress` in its `policyTypes`. When it is isolated, the only allowed outbound connections are those permitted by the `egress` list of some policy that applies to it [source: k8s-docs-network-policies-depth-2026-08-24].

**Ingress.** By default, a Pod is **non-isolated for ingress; all inbound connections are allowed.** It becomes isolated for ingress on exactly the same terms, with `Ingress` in `policyTypes`. When it is isolated, the only allowed inbound connections are **those from the Pod's node** and those permitted by the `ingress` list of some applicable policy [source: k8s-docs-network-policies-depth-2026-08-24].

Reply traffic for allowed connections is implicitly allowed in both directions [source: k8s-docs-network-policies-depth-2026-08-24], which is to say the mechanism is connection-aware, not packet-by-packet, and you do not need a return rule.

Now collect the debt from Soundings question 4. You almost certainly answered *dropped* and *the deny wins*, because that is how ordinary firewalls work and it is a good instinct nearly everywhere else. Kubernetes is the other way around on both counts. **A Pod starts fully open in both directions, and becomes restricted only because some policy went looking for it and found it.** Nothing is closed until something selects it. This is open water rather than a walled harbour: it stays open until somebody declares a restricted zone and puts you inside it.

> ★ **Fixed Point:** **By default a Pod is non-isolated in both directions.** It becomes isolated for a direction only when some NetworkPolicy both **selects it** and names that direction in `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24]. No policy means no restriction.

A note on `policyTypes`, because it has a default that catches people. Each policy includes a `policyTypes` list which may include `Ingress`, `Egress`, or both. **If no `policyTypes` are specified, `Ingress` will always be set, and `Egress` will be set if the policy has any egress rules** [source: k8s-docs-network-policies-depth-2026-08-24]. So an omitted `policyTypes` is not "neither." It is at minimum `Ingress`.

### Additive, and there is no deny

**The effects of the ingress lists combine additively. The effects of the egress lists combine additively. Network policies do not conflict; they are additive.** If any policy or policies apply to a given Pod for a given direction, the connections allowed in that direction are **the union of what the applicable policies allow.** Thus **order of evaluation does not affect the policy result** [source: k8s-docs-network-policies-depth-2026-08-24].

Sit with that for a moment, because it removes something you have relied on everywhere else.

There is **no deny rule.** None. The API has no syntax for one. Two policies selecting the same Pod produce the union of what they permit, and there is no third policy you can write that subtracts from that union. If a Pod can currently reach something and you want it not to, you do not add a denial. **You remove the grant.**

> ★ **Fixed Point:** **Policies are additive and never conflict. There is no deny rule** [source: k8s-docs-network-policies-depth-2026-08-24]. Two policies produce the union of what they permit. Removing access means removing the grant, not adding a denial.

<!-- FIGURE: ch10-fig04-networkpolicy-additive-selectors -->
```
   POLICY A                                          PERMITTED SET
   podSelector: role=db  ─────┐                    ╭───────────────╮
   ingress from: app=web      │                    │               │
                              ▼                    │   app=web     │
                        ┌───────────┐              │      +        │
                        │  Pod      │─────────────▶│   app=batch   │
                        │  role=db  │              │               │
                        └───────────┘              │  (one set,    │
                              ▲                    │   two grants) │
   POLICY B                   │                    ╰───────────────╯
   podSelector: role=db  ─────┘
   ingress from: app=batch
                                                     ┌───────────┐
   ═══▶  podSelector (chooses the SUBJECT)            │ app=other │
   ───▶  peer selector (chooses WHO MAY CONNECT)      └───────────┘
                                                       no arrow.
                                                       not denied —
                                                       simply never
                                                       granted.
```

Note what is *not* in that figure: any mark of denial. No barrier, no crossed-out arrow, no red X. The excluded Pod is excluded by the **absence of a grant**, which is a different thing from being blocked, and drawing it as blocking would contradict the Fixed Point above.

### Both ends must allow it

**For a connection from a source Pod to a destination Pod to be allowed, both the egress policy on the source Pod and the ingress policy on the destination Pod need to allow the connection. If either side does not allow the connection, it will not happen** [source: k8s-docs-network-policies-depth-2026-08-24].

This is the rule that costs practitioners the most time, because a policy that is perfectly correct in isolation is only ever half of a working configuration. You write an egress policy on `frontend` permitting traffic to `api`, you verify the YAML, you apply it, and nothing connects, because `api` has an ingress policy that never heard of `frontend`. Two harbours, two authorities: clearance to depart is not permission to enter, and a vessel holding only one of them stays at anchor.

> ★ **Fixed Point:** **Both ends must allow it.** The source Pod's egress policy *and* the destination Pod's ingress policy [source: k8s-docs-network-policies-depth-2026-08-24].

> ⚠ **Navigational Hazards:** If your firewall instinct says *"unlisted traffic is dropped"* and *"the more restrictive rule wins,"* both instincts are wrong here. And they are wrong in the direction that makes a cluster **more open than you expect**, not less. Candidates get both of these wrong, reliably, and they get them wrong *confidently*, which is worse. The default is open. Nothing denies. The union permits.

> 🪢 **Mnemonic:** *Nothing is closed until something selects it; nothing selected can be re-closed by another rule; and both ends have to agree.*

### Getting default-deny with no deny rule

The obvious objection: if there is no deny rule, how does anyone ever lock anything down?

Follow the two facts you already have. A Pod becomes isolated for a direction when a policy selects it and names that direction. Once isolated, the only permitted connections are the ones some policy's list allows. So: **select the Pods, name the direction, and permit nothing.** Isolation without permission *is* denial, arrived at by construction rather than by a deny keyword.

The mechanism for "select every Pod in the namespace" is an **empty `podSelector`**, which **selects all Pods in the namespace** [source: k8s-docs-network-policies-depth-2026-08-24]:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

No `ingress` list. No `egress` list. Every Pod in the namespace selected, both directions named, nothing permitted. **This ensures that even Pods without any other NetworkPolicy selected will not be allowed any ingress or egress traffic** [source: k8s-docs-network-policies-depth-2026-08-24]. The same shape with only `Ingress` in `policyTypes` gives you default-deny inbound and leaves outbound alone [source: k8s-docs-network-policies-depth-2026-08-24].

And because the model is additive, the reverse also works: an explicit allow-all is a policy with `podSelector: {}` and a single empty rule, `ingress: [{}]`, which permits everything to everything even if other policies have caused some Pods to be treated as isolated [source: k8s-docs-network-policies-depth-2026-08-24]. Union semantics cut both ways: you cannot subtract, and neither can anybody else.

The documentation puts the whole model in one sentence worth memorising: **a Pod will accept all traffic by default; however, once a NetworkPolicy is created for a Pod, the Pod will reject any traffic that is not allowed by any NetworkPolicy — and other Pods in the namespace that are not selected by any NetworkPolicy will continue to accept all traffic** [source: k8s-docs-network-policies-depth-2026-08-24].

### The two exceptions

Both were in the three-identifiers list above, and both are unconditional:

- **A Pod cannot block access to itself** [source: k8s-docs-network-policies-depth-2026-08-24].
- **Traffic to and from the node where a Pod is running is always allowed, regardless of the IP address of the Pod or the node** [source: k8s-docs-network-policies-depth-2026-08-24].

The second one is why the ingress isolation rule says the allowed inbound connections are "those from the Pod's node **and** those allowed by the ingress list": node-local traffic is not something a policy grants, it is something no policy can take away.

> 🪝 **Snag:** These two exceptions get rediscovered regularly by someone testing a policy from the wrong place. `kubectl exec` into the Pod and curl itself: allowed, always, and it proves nothing. Test from the node: allowed, always, and it proves nothing either. If you want to know whether a restriction works, the traffic has to originate somewhere the policy could actually govern.

*[cross-bearing: see Ch 9 §1 — the network model's second rule, and the "barring intentional network segmentation" hedge that pointed here]*
*[cross-bearing: see Ch 4 §3 — namespaces, which are the second of the three identifiers]*
*[cross-bearing: see Ch 5 §1 — the Pod IP, which is ultimately what a policy is about]*
*[cross-bearing: see Ch 12 §9 — RBAC and NetworkPolicy as one shared semantic]*

---