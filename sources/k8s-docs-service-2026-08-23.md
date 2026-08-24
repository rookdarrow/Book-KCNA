---
source_url: "https://kubernetes.io/docs/concepts/services-networking/service/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Networking"]
concepts_covered: ["service", "clusterip", "nodeport", "loadbalancer", "externalname", "headless-service", "selector", "endpointslice"]
---
# Service (kubernetes.io/docs/concepts/services-networking/service/)

In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in your cluster. The Service API is an abstraction to help you expose groups of Pods over a network. Each Service object defines a logical set of endpoints (usually these endpoints are Pods) along with a policy about how to make those pods accessible.

Motivation: if you use a Deployment to run your app, that Deployment can create and destroy Pods dynamically. Each Pod gets its own IP address; however, the set of Pods running in one moment in time could be different from the set of Pods running that application a moment later. This leads to a problem: if some set of Pods (call them "backends") provides functionality to other Pods (call them "frontends") inside your cluster, how do the frontends find out and keep track of which IP address to connect to? A Service provides a stable outward-facing endpoint that decouples the frontends from the specific backends.

## Service types
- ClusterIP — Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default that is used if you don't explicitly specify a type for a Service.
- NodePort — Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP.
- LoadBalancer — Exposes the Service externally using an external load balancer. Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider.
- ExternalName — Maps the Service to the contents of the externalName field (for example, to the hostname api.foo.bar.example). The mapping configures your cluster's DNS server to return a CNAME record with that external hostname value. No proxying of any kind is set up.

## Headless Services
Sometimes you don't need load-balancing and a single Service IP. In this case, you can create what are termed headless Services, by explicitly specifying "None" for the cluster IP address (.spec.clusterIP). For headless Services that define selectors, the endpoints controller creates EndpointSlices in the Kubernetes API, and modifies the DNS configuration to return A or AAAA records (IPv4 or IPv6 addresses) that point directly to the Pods backing the Service. For headless Services without selectors, no EndpointSlices are created automatically.

## Services without selectors
Services most commonly abstract access to Kubernetes Pods thanks to the selector, but when used with a corresponding set of EndpointSlices objects and without a selector, the Service can abstract other kinds of backends, including ones that run outside the cluster (an external database, a service in another namespace or cluster, a workload being migrated).
