---
source_url: "https://kubernetes.io/docs/concepts/services-networking/network-policies/"
fetched_at: "2026-08-23T22:45:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Networking", "D2 Security"]
concepts_covered: ["networkpolicy", "ingress-isolation", "egress-isolation", "podselector", "namespaceselector", "ipblock", "cni-support"]
---
# Network Policies (kubernetes.io/docs/concepts/services-networking/network-policies/)

If you want to control traffic flow at the IP address or port level (OSI layer 3 or 4), NetworkPolicies allow you to specify rules for traffic flow within your cluster, and also between Pods and the outside world. NetworkPolicies are an application-centric construct which allow you to specify how a pod is allowed to communicate with various network "entities" over the network. NetworkPolicies apply to a connection with a pod on one or both ends, and are not relevant to other connections.

The entities that a Pod can communicate with are identified through a combination of the following three identifiers: other pods that are allowed (exception: a pod cannot block access to itself); namespaces that are allowed; IP blocks (exception: traffic to and from the node where a Pod is running is always allowed, regardless of the IP address of the Pod or the node). When defining a pod- or namespace-based NetworkPolicy, you use a selector to specify what traffic is allowed to and from the Pod(s) that match the selector. When IP-based NetworkPolicies are created, we define policies based on IP blocks (CIDR ranges).

## Prerequisites
Network policies are implemented by the network plugin. To use network policies, you must be using a networking solution which supports NetworkPolicy. Creating a NetworkPolicy resource without a controller that implements it will have no effect.

## The two sorts of pod isolation
There are two sorts of isolation for a pod: isolation for egress, and isolation for ingress. By default, a pod is non-isolated for egress; all outbound connections are allowed. A pod is isolated for egress if there is any NetworkPolicy that both selects the pod and has "Egress" in its policyTypes; the only allowed connections from the pod are those allowed by the egress list of some NetworkPolicy that applies to the pod for egress. By default, a pod is non-isolated for ingress; all inbound connections are allowed. A pod is isolated for ingress if there is any NetworkPolicy that both selects the pod and has "Ingress" in its policyTypes; the only allowed connections into the pod are those from the pod's node and those allowed by the ingress list of some NetworkPolicy that applies to the pod for ingress. The effects of those ingress lists combine additively. Network policies do not conflict; they are additive. For a connection from a source pod to a destination pod to be allowed, both the egress policy on the source pod and the ingress policy on the destination pod need to allow the connection.

## What you can't do with network policies (as of the current release)
Forcing internal cluster traffic to go through a common gateway; anything TLS related; node specific policies; targeting of services by name; creation or management of "Policy requests" that are fulfilled by a third party; default policies which are applied to all namespaces or pods; advanced policy querying and reachability tooling; the ability to log network security events; the ability to explicitly deny policies; the ability to prevent loopback or incoming host traffic.
