## Chapter Summary

| Concept | Remember This |
|---|---|
| **The exposure ceiling** | One external address per Service *[cross-bearing: see Ch 9 §3 — the four Service types]*. Fine for one; expensive for fifty. No Service type reads HTTP. |
| **The layer boundary** | Chapter 9 moves packets to an address. This chapter reads requests. Which side you are on determines what you can know. |
| **North-south / east-west** | Into the cluster / between Pods. §1–§5 is one; §6–§7 is the other. |
| **Edge router** | The router enforcing the cluster's firewall policy. A cloud gateway or physical hardware. An Ingress controller may configure it. |
| **Ingress** | HTTP and HTTPS routes from outside to Services within, controlled by rules on the resource. **Nothing else.** |
| **The four capabilities** | Externally-reachable URLs, load balancing, TLS termination, name-based virtual hosting. |
| **Simple fanout** | One address, one host, many paths → many Services. The rule reads the **URI**. |
| **Name-based virtual hosting** | One address, many hosts → many Services. The rule reads the **host**. |
| **DNS vs virtual hosting** | DNS resolves a name *before* traffic moves. Virtual hosting sorts traffic that has *already arrived*. Opposite sides of the connection. |
| **`pathType`** | `Exact`, `Prefix`, `ImplementationSpecific`. `Prefix` matches element by element, not by string prefix. |
| **Ingress controller** | **Required.** Creating an Ingress alone has no effect. Ideally all fit the reference spec; in reality they differ. |
| **IngressClass** | `ingressClassName` names which controller should fulfil an Ingress. One default class applies when the field is omitted. |
| **Frozen ≠ deprecated** | GA + stability guarantees + no removal plans **and** no further development. Both halves. |
| **Gateway API** | Extensible, role-oriented, protocol-aware. Not built in — installed as custom resources. |
| **The three roles** | Infrastructure provider → GatewayClass. Cluster operator → Gateway. Application developer → HTTPRoute. |
| **Gateway cardinality** | Exactly one GatewayClass per Gateway. Many Routes per Gateway. |
| **NetworkPolicy scope** | Layer 3/4, application-centric, applies to connections with a Pod on one or both ends. Not host isolation. |
| **The three identifiers** | Pods, namespaces, IP blocks. Selectors for the first two; CIDR for the third. |
| **Non-isolated by default** | A Pod is open in both directions until some policy selects it *and* names that direction. |
| **Additive, no deny** | Policies never conflict; the permitted set is the union. Removing access means removing the grant. |
| **Both ends** | Source's egress *and* destination's ingress. Either one refusing kills the connection. |
| **Default-deny by construction** | Empty `podSelector`, both `policyTypes`, no rules. Isolation without permission is denial. |
| **The two exceptions** | A Pod cannot block access to itself. Node-local traffic is always allowed. |
| **Plugin dependency** | NetworkPolicies are implemented by the network plugin. No supporting plugin, no effect, no signal. |
| **Out of scope** | No TLS, no Service-name targeting, no logging, no explicit deny, no loopback blocking, and five more. |
| **The rule** | An object without its component does nothing. Four instances of the pattern so far. Ask: *what is watching this, and is it installed?* |

<!-- AUTHOR-REVIEW: "One external address per Service" is untagged here and in §1 (fact-accuracy WARN 4). No cached Ch 10 snapshot states the ratio — it is inherited Ch 9 material, so the row now carries a cross-bearing to Ch 9 §3 instead of a source tag. If Ch 9 did not source it either, this is a chapter-crossing research gap rather than a Ch 10 defect. -->

<!-- AUTHOR-REVIEW: The `pathType` row drops "Longest match wins; `Exact` breaks ties" per curriculum-alignment R3, which authorises the three values, required-ness, and the element-wise example only. If the §2 pass declines the matching cut at the precedence rule, restore the clause here so the two do not disagree. -->

---