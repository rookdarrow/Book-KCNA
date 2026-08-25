---
source_url: "https://kubernetes.io/docs/concepts/services-networking/gateway/"
fetched_at: "2026-08-24T14:38:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC-BY-4.0"
objectives_covered: ["D2.1"]
concepts_covered: ["gateway-api", "gatewayclass", "gateway", "httproute", "parentrefs", "role-oriented-design", "infrastructure-provider-role", "cluster-operator-role", "application-developer-role", "gateway-request-flow"]
---
# Gateway API — depth re-fetch (kubernetes.io/docs/concepts/services-networking/gateway/)

(Depth re-fetch of `k8s-docs-gateway-api-2026-08-23.md`, taken to settle Ch 10 Open Question #6 —
whether Gateway API is present in a default cluster. It is not; see "Installation" below. NOTE that
the current page states FOUR stable API kinds, where the 08-23 snapshot recorded three. See the
research manifest's Notes for the author, item 1 — this affects a Fixed Point and a Bearings item.)

## What is Gateway API

Gateway API is a family of API kinds that provide dynamic infrastructure provisioning and advanced traffic routing.

Make network services available by using an extensible, role-oriented, protocol-aware configuration mechanism. Gateway API is an add-on containing API kinds that provide dynamic infrastructure provisioning and advanced traffic routing.

## Design principles

The following principles shaped the design and architecture of Gateway API:

* **Role-oriented:** Gateway API kinds are modeled after organizational roles that are responsible for managing Kubernetes service networking:
  * **Infrastructure Provider:** Manages infrastructure that allows multiple isolated clusters to serve multiple tenants, e.g. a cloud provider.
  * **Cluster Operator:** Manages clusters and is typically concerned with policies, network access, application permissions, etc.
  * **Application Developer:** Manages an application running in a cluster and is typically concerned with application-level configuration and Service composition.
* **Portable:** Gateway API specifications are defined as custom resources and are supported by many implementations.
* **Expressive:** Gateway API kinds support functionality for common traffic routing use cases such as header-based matching, traffic weighting, and others that were only possible in Ingress by using custom annotations.
* **Extensible:** Gateway allows for custom resources to be linked at various layers of the API. This makes granular customization possible at the appropriate places within the API structure.

## Resource model

Gateway API has four stable API kinds:

* **GatewayClass:** Defines a set of gateways with common configuration and managed by a controller that implements the class.
* **Gateway:** Defines an instance of traffic handling infrastructure, such as cloud load balancer.
* **HTTPRoute:** Defines HTTP-specific rules for mapping traffic from a Gateway listener to a representation of backend network endpoints. These endpoints are often represented as a Service.
* **GRPCRoute:** Defines gRPC-specific rules for mapping traffic from a Gateway listener to a representation of backend network endpoints.

Gateway API is organized into different API kinds that have interdependent relationships to support the role-oriented nature of organizations. A Gateway object is associated with exactly one GatewayClass; the GatewayClass describes the gateway controller responsible for managing Gateways of this class. One or more route kinds such as HTTPRoute, are then associated to Gateways. A Gateway can filter the routes that may be attached to its `listeners`, forming a bidirectional trust model with routes.

### A typical Gateway resource example

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

### A typical HTTPRoute example

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

(EXTRACTOR NOTE on `parentRefs`: the term is attested on the current page only inside the example
manifests above, where an HTTPRoute names its Gateway under `spec.parentRefs`. The current page does
NOT carry a prose sentence of the form "HTTPRoute attaches to a Gateway via parentRefs" — that
phrasing in the 08-23 snapshot appears to be a condensation. The mechanism is sound and sourced by
the manifest; the prose gloss is the book's.)

## Request flow

Here is a simple example of HTTP traffic being routed to a Service by using a Gateway and an HTTPRoute.

(Figure: /docs/images/gateway-request-flow.svg)

In this example, the request flow for a Gateway implemented as a reverse proxy is:

1. The client starts to prepare an HTTP request for the URL `http://www.example.com`
2. The client's DNS resolver queries for the destination name and learns a mapping to one or more IP addresses associated with the Gateway.
3. The client sends a request to the Gateway IP address; the reverse proxy receives the HTTP request and uses the Host: header to match a configuration that was derived from the Gateway and attached HTTPRoute.
4. Optionally, the reverse proxy can perform request header and/or path matching based on match rules of the HTTPRoute.
5. Optionally, the reverse proxy can modify the request; for example, to add or remove headers, based on filter rules of the HTTPRoute.
6. Lastly, the reverse proxy forwards the request to one or more backends.

## Installation

Instead of Gateway API resources being natively implemented by Kubernetes, the specifications are defined as Custom Resources supported by a wide range of implementations. Install the Gateway API CRDs or follow the installation instructions of your selected implementation.
