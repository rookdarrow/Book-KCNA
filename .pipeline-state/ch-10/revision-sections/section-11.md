## 🟡 §5 — Roles, Not Just Routes

The temptation is to open with three resource names. Resist it. The resource names are a *consequence*; taught in the wrong order they become three arbitrary things to memorise instead of one idea with three parts.

### The idea

**Gateway API is a family of API kinds that provide dynamic infrastructure provisioning and advanced traffic routing.** It makes network services available using an **extensible, role-oriented, protocol-aware** configuration mechanism [source: k8s-docs-gateway-api-depth-2026-08-24].

*Role-oriented* is the word that matters. Everything else in the API falls out of it.

### The three roles

Gateway API kinds are modelled after the organisational roles responsible for managing Kubernetes service networking [source: k8s-docs-gateway-api-depth-2026-08-24]:

- **Infrastructure Provider** — manages infrastructure that allows multiple isolated clusters to serve multiple tenants; a cloud provider, for example [source: k8s-docs-gateway-api-depth-2026-08-24].
- **Cluster Operator** — manages clusters, and is typically concerned with policies, network access, and application permissions [source: k8s-docs-gateway-api-depth-2026-08-24].
- **Application Developer** — manages an application running in a cluster, and is typically concerned with application-level configuration and Service composition [source: k8s-docs-gateway-api-depth-2026-08-24].

A note on vocabulary before we go further. **"Cluster operator" here is a role name — a job a person or team holds — not the operator pattern.** This book has otherwise reserved "operator" for the custom-resource-plus-custom-controller shape you met in Chapter 6 *[cross-bearing: see Ch 6 §8 — the operator pattern]*. Two words, two unrelated meanings, and this is the only place in the book they sit near each other. When Gateway API says *cluster operator*, it means the humans who run the cluster.

### The resources

Now the resource model reads as a consequence rather than a list. Gateway API has four stable API kinds [source: k8s-docs-gateway-api-depth-2026-08-24]; three of them carry the role split, and those three are the ones this chapter uses:

- **GatewayClass** — defines a set of gateways with common configuration, managed by a controller that implements the class [source: k8s-docs-gateway-api-depth-2026-08-24].
- **Gateway** — defines an instance of traffic-handling infrastructure, such as a cloud load balancer [source: k8s-docs-gateway-api-depth-2026-08-24].
- **HTTPRoute** — defines HTTP-specific rules for mapping traffic from a Gateway listener to a representation of backend network endpoints, which are often represented as a Service [source: k8s-docs-gateway-api-depth-2026-08-24]; GRPCRoute does the same for gRPC-specific rules [source: k8s-docs-gateway-api-depth-2026-08-24].

**The cardinality is examinable, so state it as such.** A Gateway object is associated with **exactly one** GatewayClass, and the GatewayClass describes the gateway controller responsible for managing Gateways of that class. One or more route kinds are then associated to Gateways: **many** Routes may attach to a Gateway. A Gateway can filter the routes that may attach to its `listeners`, forming a bidirectional trust model with routes [source: k8s-docs-gateway-api-depth-2026-08-24].

> ★ **Fixed Point:** The three resources this chapter uses — **GatewayClass, Gateway, HTTPRoute** — and the role each belongs to. A Gateway is associated with **exactly one** GatewayClass; **many** Routes may attach to one Gateway [source: k8s-docs-gateway-api-depth-2026-08-24].

### The mapping, which is the whole design

<!-- FIGURE: ch10-fig03-gateway-api-role-split -->
```
  ┌───────────────────────────────────────────────────────────┐
  │  INFRASTRUCTURE PROVIDER                                  │
  │                                                           │
  │                   ┌──────────────┐                        │
  │                   │ GatewayClass │                        │
  │                   └──────────────┘                        │
  └──────────────────────────▲────────────────────────────────┘
                             │ exactly 1
  ┌──────────────────────────┼────────────────────────────────┐
  │  CLUSTER OPERATOR        │                                │
  │                   ┌──────┴───────┐                        │
  │                   │   Gateway    │                        │
  │                   └──────────────┘                        │
  └───────────▲──────────────▲──────────────▲─────────────────┘
              │              │              │  many (parentRefs)
  ┌───────────┼──────────────┼──────────────┼─────────────────┐
  │  APPLICATION DEVELOPER   │              │                 │
  │     ┌─────┴─────┐  ┌─────┴─────┐  ┌─────┴─────┐           │
  │     │ HTTPRoute │  │ HTTPRoute │  │ HTTPRoute │           │
  │     └───────────┘  └───────────┘  └───────────┘           │
  └───────────────────────────────────────────────────────────┘

  Bands are ownership boundaries, not runtime layers.
```

The infrastructure provider supplies the GatewayClass. The cluster operator creates the Gateway. The application developer writes the HTTPRoute. Each concern gets its own resource, so each role can hold its own without needing edit rights on anyone else's.

Here is what a Gateway looks like — the cluster operator's object:

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: Gateway
metadata:
  name: example-gateway
  namespace: example-namespace
spec:
  gatewayClassName: example-class
  listeners:
  - name: http
    protocol: HTTP
    port: 80
    hostname: "www.example.com"
    allowedRoutes:
      namespaces:
        from: Same
```

And an HTTPRoute — the application developer's:

```yaml
apiVersion: gateway.networking.k8s.io/v1
kind: HTTPRoute
metadata:
  name: example-httproute
spec:
  parentRefs:
  - name: example-gateway
  hostnames:
  - "www.example.com"
  rules:
  - matches:
    - path:
        type: PathPrefix
        value: /login
    backendRefs:
    - name: example-svc
      port: 8080
```

[source: k8s-docs-gateway-api-depth-2026-08-24]

Look at what those two manifests do and do not contain. The Gateway names its class and declares its listeners and which namespaces may attach routes; it says nothing about `/login`. The HTTPRoute names its parent Gateway under **`parentRefs`**, declares its hostnames and path matches and backends; it says nothing about ports, protocols, or which load balancer implementation is underneath. The seam between them is exactly the seam between the two roles.

<!-- AUTHOR-REVIEW: the phrase "an HTTPRoute attaches to a Gateway via parentRefs" is this book's gloss. The current source page attests `parentRefs` only inside the example manifest, not in a prose sentence of that form (the extractor flagged this explicitly). The mechanism is sourced by the manifest; the wording is ours. -->

And compare that HTTPRoute against §2's fanout Ingress. Same requirement, expressed in a different vocabulary: one host, a path match, a backend Service and port. This is not a new routing model to learn from scratch; it is the shapes you already know, redistributed across resources that belong to different owners.

> ⚓ **Worth Securing:** The role split *is* the innovation. Two things are documented. Ingress controllers frequently use annotations to configure behavior [source: k8s-docs-ingress-depth-2026-08-24], and Gateway API kinds support common cases such as header-based matching and traffic weighting "that were only possible in Ingress by using custom annotations" [source: k8s-docs-gateway-api-depth-2026-08-24]. The reading that joins them — that so much real-world configuration ended up in annotations *because* Ingress put infrastructure choice, cluster policy, and application routing into one object that one team had to own — is this book's, not the documentation's.

### The request flow

Concrete, end to end, for a Gateway implemented as a reverse proxy [source: k8s-docs-gateway-api-depth-2026-08-24]:

1. The client starts to prepare an HTTP request for `http://www.example.com`.
2. The client's DNS resolver queries for the destination name and learns a mapping to one or more IP addresses associated with the Gateway.
3. The client sends a request to the Gateway IP address; the reverse proxy receives the HTTP request and uses the **`Host:` header** to match a configuration derived from the Gateway and attached HTTPRoute.
4. Optionally, the reverse proxy performs request header and/or path matching based on the HTTPRoute's match rules.
5. Optionally, the reverse proxy modifies the request — adding or removing headers, say — based on the HTTPRoute's filter rules.
6. Lastly, the reverse proxy forwards the request to one or more backends.

Step 2 and step 3 are the §2 distinction, drawn in the specification's own hand. DNS does its work and finishes; the `Host` header does its work afterward, on a connection that has already arrived. One question is asked across open water, before anything moves; the other is asked at the quayside, of something already tied up alongside.

And step 3 is Soundings question 1's answer, seven sections later. You worked out that a server distinguishing two hostnames on one address has to read the `Host` header, from ordinary web experience, before this chapter started. Here is the same mechanism in a Kubernetes specification, doing the same job under a different name. That is usually how this material goes: the priors were right, the vocabulary is new.

### The other design principles

Three more, briefly [source: k8s-docs-gateway-api-depth-2026-08-24]:

- **Portable** — Gateway API specifications are defined as custom resources and are supported by many implementations.
- **Expressive** — the kinds support common traffic routing cases such as header-based matching and traffic weighting, which in Ingress were only possible through custom annotations. That is the concrete answer to what §4's freeze costs you.
- **Extensible** — custom resources can be linked at various layers of the API, making granular customization possible at the appropriate places within the structure.

### Is it there?

Having just been told to prefer Gateway API, the obvious next question is whether it is in your cluster. It is not.

**Instead of Gateway API resources being natively implemented by Kubernetes, the specifications are defined as Custom Resources supported by a wide range of implementations.** You install the Gateway API CRDs, or follow the installation instructions of your selected implementation [source: k8s-docs-gateway-api-depth-2026-08-24]. The docs describe Gateway API as "an add-on containing API kinds" [source: k8s-docs-gateway-api-depth-2026-08-24], and the cluster addon list carries it among the networking entries [source: k8s-docs-cluster-addons-2026-08-24].

> 🔭 **Closer Look:** The API the project names as Ingress's successor [source: k8s-docs-network-model-2026-08-23] is not built into the API server the way Ingress is. It arrives as custom resources *[cross-bearing: see Ch 6 §8 — custom resources and CustomResourceDefinitions]*. That is deeper than the exam requires, and it is a rather good demonstration of Chapter 6's claim that the extension mechanism is powerful enough to build first-class-looking APIs on top of. The successor to a built-in API is, structurally, an extension.

*[cross-bearing: see Ch 9 §6 — the client's resolver, which appears here as one step in a flow rather than as a topic]*
*[cross-bearing: see Ch 17 §4 — CRDs as one of the four pluggable interfaces, of which this is a conspicuous instance]*

<!-- AUTHOR-REVIEW: the fact-accuracy audit flagged "the four pluggable interfaces" as an untagged claim that no cached snapshot enumerates (the extending-Kubernetes page lists six extension points and five infrastructure plugins, with CRDs filed separately under API extensions). The phrase is a book coinage owned by Ch 17 §4, and the BINDING term ledger fixes the set as CRI + CNI + CSI + CRDs — so the cross-bearing above is correct as written and takes no source tag. The internal contradiction the audit found is in The Voyage Ahead ("you have collected two now"), which counts CRDs out; that section, not this one, is where the count needs repairing. -->

---