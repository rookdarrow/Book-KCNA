---
source_url: "https://kubernetes.io/docs/concepts/services-networking/network-policies/"
fetched_at: "2026-08-24T14:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC-BY-4.0"
objectives_covered: ["D2.1", "D2.2"]
concepts_covered: ["networkpolicy", "l3-l4-control", "application-centric-policy", "pod-selector", "namespace-selector", "ipblock", "cidr-range", "policy-types", "ingress-isolation", "egress-isolation", "non-isolated-default", "additive-policy-semantics", "no-deny-rule", "both-ends-must-allow", "default-deny-by-selection", "node-local-traffic-always-allowed", "self-traffic-unblockable", "policy-plugin-dependency", "networkpolicy-out-of-scope"]
---
# Network Policies — full page (kubernetes.io/docs/concepts/services-networking/network-policies/)

(Depth re-fetch of the 22-line summary held in `k8s-docs-network-policies-2026-08-23.md`. Adds the
field-level detail that snapshot lacked: the resource manifest, the mandatory-fields explanation,
the behaviour of to/from selectors, the empty-podSelector idiom and the default-policy manifests.
The out-of-scope list is reproduced here in full with the parentheticals the summary stripped.)

## Introduction

If you want to control traffic flow at the IP address or port level (OSI layer 3 or 4), NetworkPolicies allow you to specify rules for traffic flow within your cluster, and also between Pods and the outside world. Your cluster must use a network plugin that supports NetworkPolicy enforcement.

If you want to control traffic flow at the IP address or port level for TCP, UDP, and SCTP protocols, then you might consider using Kubernetes NetworkPolicies for particular applications in your cluster. NetworkPolicies are an application-centric construct which allow you to specify how a pod is allowed to communicate with various network "entities" (we use the word "entity" here to avoid overloading the more common terms such as "endpoints" and "services", which have specific Kubernetes connotations) over the network. NetworkPolicies apply to a connection with a pod on one or both ends, and are not relevant to other connections.

The entities that a Pod can communicate with are identified through a combination of the following three identifiers:

1. Other pods that are allowed (exception: a pod cannot block access to itself)
2. Namespaces that are allowed
3. IP blocks (exception: traffic to and from the node where a Pod is running is always allowed, regardless of the IP address of the Pod or the node)

When defining a pod- or namespace-based NetworkPolicy, you use a selector to specify what traffic is allowed to and from the Pod(s) that match the selector.

Meanwhile, when IP-based NetworkPolicies are created, we define policies based on IP blocks (CIDR ranges).

## Prerequisites

Network policies are implemented by the network plugin. To use network policies, you must be using a networking solution which supports NetworkPolicy. Creating a NetworkPolicy resource without a controller that implements it will have no effect.

## The two sorts of pod isolation

There are two sorts of isolation for a pod: isolation for egress, and isolation for ingress. They concern what connections may be established. "Isolation" here is not absolute, rather it means "some restrictions apply". The alternative, "non-isolated for $direction", means that no restrictions apply in the stated direction. The two sorts of isolation (or not) are declared independently, and are both relevant for a connection from one pod to another.

By default, a pod is non-isolated for egress; all outbound connections are allowed. A pod is isolated for egress if there is any NetworkPolicy that both selects the pod and has "Egress" in its `policyTypes`; we say that such a policy applies to the pod for egress. When a pod is isolated for egress, the only allowed connections from the pod are those allowed by the `egress` list of some NetworkPolicy that applies to the pod for egress. Reply traffic for those allowed connections will also be implicitly allowed. The effects of those `egress` lists combine additively.

By default, a pod is non-isolated for ingress; all inbound connections are allowed. A pod is isolated for ingress if there is any NetworkPolicy that both selects the pod and has "Ingress" in its `policyTypes`; we say that such a policy applies to the pod for ingress. When a pod is isolated for ingress, the only allowed connections into the pod are those from the pod's node and those allowed by the `ingress` list of some NetworkPolicy that applies to the pod for ingress. Reply traffic for those allowed connections will also be implicitly allowed. The effects of those `ingress` lists combine additively.

Network policies do not conflict; they are additive. If any policy or policies apply to a given pod for a given direction, the connections allowed in that direction from that pod is the union of what the applicable policies allow. Thus, order of evaluation does not affect the policy result.

For a connection from a source pod to a destination pod to be allowed, both the egress policy on the source pod and the ingress policy on the destination pod need to allow the connection. If either side does not allow the connection, it will not happen.

## The NetworkPolicy resource

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: test-network-policy
      namespace: default
    spec:
      podSelector:
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
        - namespaceSelector:
            matchLabels:
              project: myproject
        - podSelector:
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

## Mandatory Fields

**Mandatory Fields**: As with all other Kubernetes config, a NetworkPolicy needs `apiVersion`, `kind`, and `metadata` fields.

**spec**: NetworkPolicy spec has all the information needed to define a particular network policy in the given namespace.

**podSelector**: Each NetworkPolicy includes a `podSelector` which selects the grouping of pods to which the policy applies. The example policy selects pods with the label "role=db". An empty `podSelector` selects all pods in the namespace.

**policyTypes**: Each NetworkPolicy includes a `policyTypes` list which may include either `Ingress`, `Egress`, or both. The `policyTypes` field indicates whether or not the given policy applies to ingress traffic to selected pod, egress traffic from selected pods, or both. If no `policyTypes` are specified on a NetworkPolicy then by default `Ingress` will always be set and `Egress` will be set if the NetworkPolicy has any egress rules.

**ingress**: Each NetworkPolicy may include a list of allowed `ingress` rules. Each rule allows traffic which matches both the `from` and `ports` sections. The example policy contains a single rule, which matches traffic on a single port, from one of three sources, the first specified via an `ipBlock`, the second via a `namespaceSelector` and the third via a `podSelector`.

**egress**: Each NetworkPolicy may include a list of allowed `egress` rules. Each rule allows traffic which matches both the `to` and `ports` sections. The example policy contains a single rule, which matches traffic on a single port to any destination in `10.0.0.0/24`.

## Behavior of `to` and `from` selectors

There are four kinds of selectors that can be specified in an `ingress` `from` section or `egress` `to` section:

**podSelector**: This selects particular Pods in the same namespace as the NetworkPolicy which should be allowed as ingress sources or egress destinations.

**namespaceSelector**: This selects particular namespaces for which all Pods should be allowed as ingress sources or egress destinations.

**namespaceSelector** *and* **podSelector**: A single `to`/`from` entry that specifies both `namespaceSelector` and `podSelector` selects particular Pods within particular namespaces. Be careful to use correct YAML syntax. For example:

    ...
    ingress:
    - from:
      - namespaceSelector:
          matchLabels:
            user: alice
        podSelector:
          matchLabels:
            role: client
    ...

This policy contains a single `from` element allowing connections from Pods with the label `role=client` in namespaces with the label `user=alice`. But the following policy is different:

    ...
    ingress:
    - from:
      - namespaceSelector:
          matchLabels:
            user: alice
      - podSelector:
          matchLabels:
            role: client
    ...

It contains two elements in the `from` array, and allows connections from Pods in the local Namespace with the label `role=client`, *or* from any Pod in any namespace with the label `user=alice`.

When in doubt, use `kubectl describe` to see how Kubernetes has interpreted the policy.

**ipBlock**: This selects particular IP CIDR ranges to allow as ingress sources or egress destinations. These should be cluster-external IPs, since Pod IPs are ephemeral and unpredictable.

Cluster ingress and egress mechanisms often require rewriting the source or destination IP of packets. In cases where this happens, it is not defined whether the NetworkPolicy is applied to the original source or destination IP, or to the rewritten IP.

On the ingress side, this means that in some cases you cannot define network policies based on the source IP of incoming packets if rewriting of the source IP occurs before the policy is applied.

On the egress side, this means that connections to Services with `externalIPs` may or may not be subject to policies based on the `ipBlock`, depending on the implementation.

## Default policies

A pod will accept all traffic by default. However, once a NetworkPolicy is created for a pod, the pod will reject any traffic that is not allowed by any NetworkPolicy. (Other pods in the namespace that are not selected by any NetworkPolicy will continue to accept all traffic.)

### Default deny all ingress traffic

You can create a "default" ingress NetworkPolicy for a namespace which prevents all ingress traffic by creating a NetworkPolicy that selects all pods but does not allow any ingress traffic.

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: default-deny-ingress
    spec:
      podSelector: {}
      policyTypes:
      - Ingress

This ensures that even pods without any other ingress NetworkPolicy selected will not be allowed ingress traffic.

### Allow all ingress traffic

If you want to allow all traffic to all pods in a namespace (even if policies are added that cause some pods to be treated as "isolated"), you can create a policy that explicitly allows all ingress traffic.

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-all-ingress
    spec:
      podSelector: {}
      ingress:
      - {}
      policyTypes:
      - Ingress

### Default deny all egress traffic

You can create a "default" egress NetworkPolicy for a namespace which prevents all egress traffic by creating a NetworkPolicy that selects all pods but does not allow any egress traffic.

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: default-deny-egress
    spec:
      podSelector: {}
      policyTypes:
      - Egress

This ensures that even pods without any other egress NetworkPolicy selected will not be allowed egress traffic.

### Allow all egress traffic

If you want to allow all traffic to all pods in a namespace (even if policies are added that cause some pods to be treated as "isolated"), you can create a policy that explicitly allows all egress traffic.

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-all-egress
    spec:
      podSelector: {}
      egress:
      - {}
      policyTypes:
      - Egress

### Default deny all ingress and all egress traffic

You can create a "default" NetworkPolicy for a namespace which prevents all ingress and all egress traffic by creating a NetworkPolicy that selects all pods but does not allow any ingress or egress traffic.

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: default-deny-all
    spec:
      podSelector: {}
      policyTypes:
      - Ingress
      - Egress

This ensures that even pods without any other NetworkPolicy selected will not be allowed any ingress or egress traffic.

## Targeting a Namespace by its name

The Kubernetes control plane sets an immutable label `kubernetes.io/metadata.name` on all namespaces, the value of the label is the namespace name.

While NetworkPolicy cannot target a namespace by its name with some object field, you can use the standardized label to target a specific namespace.

## What you can't do with network policies (at least, not yet)

(Reproduced from the raw markdown source of the page. Ten bullets, verified by direct count against
raw.githubusercontent.com/kubernetes/website/main/content/en/docs/concepts/services-networking/network-policies.md.
Glossary-tooltip shortcodes have been resolved to their display text; the source's own typos —
"its worth noting", "the model for NetworkPolicies are deny by default" — are preserved.)

As of Kubernetes {{< skew currentVersion >}}, the following functionality does not exist in the NetworkPolicy API, but you might be able to implement workarounds using Operating System components (such as SELinux, OpenVSwitch, IPTables, and so on) or Layer 7 technologies (Ingress controllers, Service Mesh implementations) or admission controllers. In case you are new to network security in Kubernetes, its worth noting that the following User Stories cannot (yet) be implemented using the NetworkPolicy API.

- Forcing internal cluster traffic to go through a common gateway (this might be best served with a service mesh or other proxy).
- Anything TLS related (use a service mesh or ingress controller for this).
- Node specific policies (you can use CIDR notation for these, but you cannot target nodes by their Kubernetes identities specifically).
- Targeting of services by name (you can, however, target pods or namespaces by their labels, which is often a viable workaround).
- Creation or management of "Policy requests" that are fulfilled by a third party.
- Default policies which are applied to all namespaces or pods (there are some third party Kubernetes distributions and projects which can do this).
- Advanced policy querying and reachability tooling.
- The ability to log network security events (for example connections that are blocked or accepted).
- The ability to explicitly deny policies (currently the model for NetworkPolicies are deny by default, with only the ability to add allow rules).
- The ability to prevent loopback or incoming host traffic (Pods cannot currently block localhost access, nor do they have the ability to block access from their resident node).
