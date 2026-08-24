---
source_url: "https://kubernetes.io/docs/concepts/services-networking/gateway/"
fetched_at: "2026-08-23T23:15:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Networking"]
concepts_covered: ["gateway-api", "gatewayclass", "gateway", "httproute", "role-oriented", "ingress-successor"]
---
# Gateway API (kubernetes.io/docs/concepts/services-networking/gateway/)

Gateway API is a family of API kinds that provide dynamic infrastructure provisioning and advanced traffic routing. Make network services available by using an extensible, role-oriented, protocol-aware configuration mechanism. Gateway is an add-on containing API kinds that provide dynamic infrastructure provisioning and advanced traffic routing.

## Design principles
- Role-oriented — Gateway is composed of API resources which model organizational roles that use and configure Kubernetes service networking: the Infrastructure Provider (manages infrastructure that lets multiple isolated clusters serve multiple tenants), the Cluster Operator (manages clusters and is typically concerned with policies, network access, application permissions), and the Application Developer (manages an application running in a cluster and is typically concerned with application-level configuration and Service composition).
- Portable — Gateway specifications are defined as custom resources and are supported by many implementations.
- Expressive — Gateway API kinds support functionality for common traffic routing use cases such as header-based matching, traffic weighting, and others that were only possible in Ingress by using custom annotations.
- Extensible — Gateway allows for custom resources to be linked at various layers of the API. This makes granular customization possible at the appropriate places within the API structure.

## Resource model
GatewayClass — defines a set of gateways with common configuration and managed by a controller that implements the class. Gateway — defines an instance of traffic handling infrastructure, such as a cloud load balancer; describes how traffic can be translated to Services within the cluster. HTTPRoute — specifies HTTP-specific rules for mapping traffic from a Gateway listener to a representation of backend network endpoints; attached to a Gateway via parentRefs. A Gateway is associated with exactly one GatewayClass; many Routes may attach to a Gateway.

## Request flow
The client's DNS resolver learns the IP address associated with the Gateway; the client sends the request to the Gateway IP address; the reverse proxy receives the HTTP request and uses the Host header to match a configuration that was derived from the Gateway and attached HTTPRoute; optionally performs request header and/or path matching based on match rules of the HTTPRoute; optionally modifies the request based on filter rules of the HTTPRoute; and lastly forwards the request to one or more backends.
