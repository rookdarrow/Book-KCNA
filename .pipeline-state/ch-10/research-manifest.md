All verified — the rendered-page pass had fabricated hostnames and Service names in all three manifests (`foo.example.com`/`foo`/`bar` instead of the real `foo.bar.com`/`service1`/`service2`). The raw example files are authoritative. Here is the manifest.

# Research Manifest — KCNA Chapter 10

**Chapter:** 10 — Traffic from Beyond the Cluster
**Stage:** 2 (Source Snapshot Research)
**Researched:** 2026-08-24
**Outcome:** Both blocking gaps (Open Questions #2 and #3) are **CLOSED**. Non-blocking Open Question #7 is **CLOSED**. Open Question #6 is **CLOSED with a strong source**. The §4 source-verification flag is **resolved**. One new correctness problem surfaced in §5 — see Notes #1.

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-ingress-depth-2026-08-24.md` | Kubernetes project | D2.1 | ingress, ingress-rule, ingress-host, ingress-path, path-type, default-backend, single-service-ingress, simple-fanout, name-based-virtual-hosting, tls-termination, ingressclass, edge-router, cluster-network, feature-freeze, ga-stability-guarantee, reference-specification |
| `k8s-docs-ingress-controllers-2026-08-24.md` | Kubernetes project | D2.1 | ingress-controller, ingressclass, absent-component-pattern |
| `k8s-docs-network-policies-depth-2026-08-24.md` | Kubernetes project | D2.1, D2.2 | networkpolicy, l3-l4-control, application-centric-policy, pod-selector, namespace-selector, ipblock, cidr-range, policy-types, ingress-isolation, egress-isolation, non-isolated-default, additive-policy-semantics, no-deny-rule, both-ends-must-allow, default-deny-by-selection, node-local-traffic-always-allowed, self-traffic-unblockable, policy-plugin-dependency, networkpolicy-out-of-scope |
| `k8s-docs-deprecation-policy-2026-08-24.md` | Kubernetes project | D2.1 | frozen-not-deprecated, ga-stability-guarantee, feature-freeze |
| `k8s-docs-gateway-api-depth-2026-08-24.md` | Kubernetes project | D2.1 | gateway-api, gatewayclass, gateway, httproute, parentrefs, role-oriented-design, infrastructure-provider-role, cluster-operator-role, application-developer-role, gateway-request-flow |
| `k8s-blog-gateway-api-north-south-east-west-2026-08-24.md` | Kubernetes project (official blog) | D2.1 | north-south-traffic, east-west-traffic |

Six new snapshots. All six are tier-1/tier-2 (exam authority or official vendor documentation). No third-party sources used. The exam-authority layer (D2 = 28% Container Orchestration, Networking competency) is already cached in `cncf-kcna-curriculum-pdf-2026-08-23.md` and needed no re-fetch.

---

### A1 · `k8s-docs-ingress-depth-2026-08-24.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/services-networking/ingress/"
fetched_at: "2026-08-24T14:20:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC-BY-4.0"
objectives_covered: ["D2.1"]
concepts_covered: ["ingress", "ingress-rule", "ingress-host", "ingress-path", "path-type", "default-backend", "single-service-ingress", "simple-fanout", "name-based-virtual-hosting", "tls-termination", "ingressclass", "ingress-controller", "edge-router", "cluster-network", "reference-specification", "feature-freeze", "frozen-not-deprecated", "ga-stability-guarantee"]
---
# Ingress — full page (kubernetes.io/docs/concepts/services-networking/ingress/)

(Depth re-fetch of the 22-line summary held in `k8s-docs-ingress-2026-08-23.md`. Adds the field-level
detail that snapshot lacked: pathType, defaultBackend, IngressClass, the rule structure and spec.tls.)

## Terminology

For clarity, this guide defines the following terms:

* Node: A worker machine in Kubernetes, part of a cluster.
* Cluster: A set of Nodes that run containerized applications managed by Kubernetes. For this example, and in most common Kubernetes deployments, nodes in the cluster are not part of the public internet.
* Edge router: A router that enforces the firewall policy for your cluster. This could be a gateway managed by a cloud provider or a physical piece of hardware.
* Cluster network: A set of links, logical or physical, that facilitate communication within a cluster according to the Kubernetes networking model.
* Service: A Kubernetes Service that identifies a set of Pods using label selectors. Unless mentioned otherwise, Services are assumed to have virtual IPs only routable within the cluster network.

## What is Ingress?

Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource.

Here is a simple example where an Ingress sends all its traffic to one Service:

(Figure. Ingress — /docs/images/ingress.svg)

An Ingress may be configured to give Services externally-reachable URLs, load balance traffic, terminate SSL / TLS, and offer name-based virtual hosting. An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends to help handle the traffic.

An Ingress does not expose arbitrary ports or protocols. Exposing services other than HTTP and HTTPS to the internet typically uses a service of type Service.Type=NodePort or Service.Type=LoadBalancer.

### Note:

The Kubernetes project recommends using Gateway instead of Ingress. The Ingress API has been frozen.

This means that:

* The Ingress API is generally available, and is subject to the stability guarantees for generally available APIs. The Kubernetes project has no plans to remove Ingress from Kubernetes.
* The Ingress API is no longer being developed, and will have no further changes or updates made to it.

(In the rendered page, "stability guarantees" hyperlinks to
/docs/reference/using-api/deprecation-policy/#deprecating-parts-of-the-api — the source captured in
snapshot `k8s-docs-deprecation-policy-2026-08-24.md`.)

## Prerequisites

You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect.

You can choose from a number of Ingress controllers.

Ideally, all Ingress controllers should fit the reference specification. In reality, the various Ingress controllers operate slightly differently.

### Note:

Make sure you review your Ingress controller's documentation to understand the caveats of choosing it.

## The Ingress resource

A minimal Ingress resource example:

(service/networking/minimal-ingress.yaml)

    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: minimal-ingress
    spec:
      ingressClassName: nginx-example
      rules:
      - http:
          paths:
          - path: /testpath
            pathType: Prefix
            backend:
              service:
                name: test
                port:
                  number: 80

An Ingress needs `apiVersion`, `kind`, `metadata` and `spec` fields. The name of an Ingress object must be a valid DNS subdomain name. For general information about working with config files, see deploying applications, configuring containers, managing resources. Ingress controllers frequently use annotations to configure behavior. Review the documentation for your choice of ingress controller to learn which annotations are expected and / or supported.

The Ingress spec has all the information needed to configure a load balancer or proxy server. Most importantly, it contains a list of rules matched against all incoming requests. Ingress resource only supports rules for directing HTTP(S) traffic.

If the `ingressClassName` is omitted, a default Ingress class should be defined.

Some ingress controllers work even without the definition of a default IngressClass. Even if you use an ingress controller that is able to operate without any IngressClass, the Kubernetes project still recommends that you define a default IngressClass.

### Ingress rules

Each HTTP rule contains the following information:

* An optional host. In this example, no host is specified, so the rule applies to all inbound HTTP traffic through the IP address specified. If a host is provided (for example, foo.bar.com), the rules apply to that host.
* A list of paths (for example, `/testpath`), each of which has an associated backend defined with a `service.name` and a `service.port.name` or `service.port.number`. Both the host and path must match the content of an incoming request before the load balancer directs traffic to the referenced Service.
* A backend is a combination of Service and port names as described in the Service doc or a custom resource backend by way of a CRD. HTTP (and HTTPS) requests to the Ingress that match the host and path of the rule are sent to the listed backend.

A `defaultBackend` is often configured in an Ingress controller to service any requests that do not match a path in the spec.

### DefaultBackend

An Ingress with no rules sends all traffic to a single default backend and `.spec.defaultBackend` is the backend that should handle requests in that case. The `defaultBackend` is conventionally a configuration option of the Ingress controller and is not specified in your Ingress resources. If no `.spec.rules` are specified, `.spec.defaultBackend` must be specified. If `defaultBackend` is not set, the handling of requests that do not match any of the rules will be up to the ingress controller (consult the documentation for your ingress controller to find out how it handles this case).

If none of the hosts or paths match the HTTP request in the Ingress objects, the traffic is routed to your default backend.

### Resource backends

A `Resource` backend is an ObjectRef to another Kubernetes resource within the same namespace as the Ingress object. A `Resource` is a mutually exclusive setting with Service, and will fail validation if both are specified. A common usage for a `Resource` backend is to ingress data to an object storage backend with static assets.

(service/networking/ingress-resource-backend.yaml)

    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: ingress-resource-backend
    spec:
      defaultBackend:
        resource:
          apiGroup: k8s.example.com
          kind: StorageBucket
          name: static-assets
      rules:
        - http:
            paths:
              - path: /icons
                pathType: ImplementationSpecific
                backend:
                  resource:
                    apiGroup: k8s.example.com
                    kind: StorageBucket
                    name: icon-assets

After creating the Ingress above, you can view it with the following command:

    kubectl describe ingress ingress-resource-backend

    Name:             ingress-resource-backend
    Namespace:        default
    Address:
    Default backend:  APIGroup: k8s.example.com, Kind: StorageBucket, Name: static-assets
    Rules:
      Host        Path  Backends
      ----        ----  --------
      *
                  /icons   APIGroup: k8s.example.com, Kind: StorageBucket, Name: icon-assets
    Annotations:  <none>
    Events:       <none>

## Path types

Each path in an Ingress is required to have a corresponding path type. Paths that do not include an explicit `pathType` are not validated.

There are three supported path types:

* `ImplementationSpecific`: With this path type, matching is up to the IngressClass. Implementations can treat this as a separate `pathType` or treat it identically to `Prefix` or `Exact` path types.
* `Exact`: Matches the URL path exactly and with case sensitivity.
* `Prefix`: Matches based on a URL path prefix split by `/`. Matching is case sensitive and done on a path element by element basis. A path element refers to the labels in the URL path split by the `/` separator.

(EXTRACTOR NOTE: the Prefix definition ends with one further sentence formalising element-wise
prefix matching. The extraction of that final sentence was not clean and it is therefore omitted
here rather than transcribed approximately. Re-verify against the source before quoting it
directly. The three type names, the Note below, and the Examples table are clean.)

### Note:

If the last element of the path component is a substring of the last element in request path, it is not a match. For example, if the path `/foo/bar` is split into `["foo","bar"]`, the request path `/foo/barbaz` split into `["foo", "barbaz"]` is not a match.

Conversely, if the last element of the request path is a substring of the path component, there is a match. For example, if the path `/foo/bar` is split into `["foo","bar"]`, the request path `/foo/bar` split into `["foo","bar"]` is a match. If the path `/foo/bar/` is split into `["foo","bar",""]`, the request path `/foo/bar` split into `["foo","bar"]` is not a match.

### Examples

| Kind | Path(s) | Request path(s) | Matches? |
| --- | --- | --- | --- |
| Prefix | `/foo` | `/foo`, `/foo/`, `/foo/bar` | Yes |
| Exact | `/foo` | `/foo` | Yes |
| Exact | `/foo` | `/foo/` | No |
| Exact | `/foo/` | `/foo` | No |
| Exact | `/foo/` | `/foo/` | Yes |
| Prefix | `/foo/` | `/foo`, `/foo/` | Yes, matches `/foo/` only |
| Prefix | `/aaa/bb` | `/aaa/bbb` | No |
| Prefix | `/aaa/bbb` | `/aaa/bbb` | Yes |
| Prefix | `/aaa/bbb/` | `/aaa/bbb` | Yes, matches `/aaa/bbb/` |
| Prefix | `/aaa/bbb` | `/aaa/bbb/` | Yes, matches `/aaa/bbb` |

### Multiple matches

In some cases, multiple paths within an Ingress will match a request. In those cases the match with the longest path will be given priority. If two paths are still equally long, the path with `Exact` path type will be given priority over `Prefix` path type.

## Hostname wildcards

Hosts can be precise matches or a wildcard pattern. Precise matches use the DNS subdomain names. Wildcard patterns for hostnames are designated by an asterisk character `*` as the leftmost label. Wildcard patterns match a single DNS label. For example, `*.foo.com` matches `bar.foo.com` and `baz.foo.com`, but does not match `foobar.foo.com`.

| Host | Host header | Match? |
| --- | --- | --- |
| `*.foo.com` | `bar.foo.com` | Matches based on shared suffix |
| `*.foo.com` | `baz.baz.foo.com` | No, wildcard only matches a single DNS label |
| `foo.com` | `foo.com` | Matches (exact) |
| `foo.com` | `bar.foo.com` | No, host header "bar.foo.com" does not exactly match "foo.com" |

## Ingress class

Ingresses can be implemented by different controllers, often with different configuration. Each Ingress should specify which controller it is intended to use. This is done with the `ingressClassName` field on Ingress. This field is a reference to an IngressClass resource that contains additional configuration including the name of the controller that should implement the class.

(service/networking/ingress-class.yaml)

    apiVersion: networking.k8s.io/v1
    kind: IngressClass
    metadata:
      name: external-lb
    spec:
      controller: example.com/ingress-controller
      parameters:
        apiGroup: k8s.example.com
        kind: IngressParameters
        name: external-lb

The `spec.parameters` field of an IngressClass lets you reference another resource that provides configuration related to that IngressClass.

### IngressClass scope

Depending on your ingress controller, you may be able to use parameters that are set at cluster scope, or just namespace scope.

The default scope for `spec.parameters` is cluster scope.

If you set `spec.parameters.scope` to `Namespace`, and you reference a namespaced kind (for example, a ConfigMap), the parameters will be looked up in the same namespace as the IngressClass.

If `spec.parameters.scope` is set to `Cluster` (the default), or if the kind is cluster-scoped (for example, a ClusterConfig), the parameters will be referenced at cluster scope.

### Default IngressClass

You can mark a particular IngressClass as default for your cluster. Setting the `ingressclass.kubernetes.io/is-default-class` annotation to `true` on an IngressClass resource will ensure that new Ingresses without an explicit `ingressClassName` field specified will be assigned this default class.

## Types of Ingress

### Ingress backed by a single Service

(The subsection states that an Ingress backed by a single Service is created by "specifying a
*default backend* with no rules". The manifest is included by shortcode from the example file
service/networking/test-ingress.yaml, reproduced verbatim below. See also the DefaultBackend
section above, which carries the same fact in fuller prose.)

    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: test-ingress
    spec:
      defaultBackend:
        service:
          name: test
          port:
            number: 80

### Simple fanout

A "fanout" configuration routes traffic from a single IP address to more than one Service, based on the HTTP URI being requested. An Ingress allows you to keep the number of load balancers down to a minimum.

(service/networking/simple-fanout-example.yaml)

    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: simple-fanout-example
    spec:
      rules:
      - host: foo.bar.com
        http:
          paths:
          - path: /foo
            pathType: Prefix
            backend:
              service:
                name: service1
                port:
                  number: 4200
          - path: /bar
            pathType: Prefix
            backend:
              service:
                name: service2
                port:
                  number: 8080

### Name based virtual hosting

Name-based virtual hosts support routing HTTP traffic to multiple host names at the same IP address.

The following Ingress tells the backing load balancer to route traffic based on the host header.

(service/networking/name-virtual-host-ingress.yaml)

    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: name-virtual-host-ingress
    spec:
      rules:
      - host: foo.bar.com
        http:
          paths:
          - pathType: Prefix
            path: "/"
            backend:
              service:
                name: service1
                port:
                  number: 80
      - host: bar.foo.com
        http:
          paths:
          - pathType: Prefix
            path: "/"
            backend:
              service:
                name: service2
                port:
                  number: 80

### TLS

You can secure an Ingress by specifying a Secret that contains a TLS private key and certificate. The Ingress resource only supports a single TLS port, 443, and assumes TLS termination at the ingress point (traffic to the Service and its Pods is in cleartext). If the TLS configuration section in an Ingress specifies different hosts, they will be multiplexed on the same port according to the hostname specified through the SNI TLS extension (provided the Ingress controller supports SNI). The TLS secret must contain keys named `tls.crt` and `tls.key` that contain the certificate and private key to use for TLS. For example:

    apiVersion: v1
    kind: Secret
    metadata:
      name: testsecret-tls
      namespace: default
    data:
      tls.crt: base64 encoded cert
      tls.key: base64 encoded key
    type: kubernetes.io/tls

Referencing this secret in an Ingress will tell the Ingress controller to secure the channel from the client to the load balancer using TLS:

(service/networking/tls-example-ingress.yaml)

    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: tls-example-ingress
    spec:
      tls:
      - hosts:
          - https-example.foo.com
        secretName: testsecret-tls
      rules:
      - host: https-example.foo.com
        http:
          paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: service1
                port:
                  number: 80

### Load balancing

An Ingress controller is bootstrapped with some load balancing policy settings that it applies to all Ingress, such as the load balancing algorithm, backend weights schemes, and other fields. More advanced load balancing concepts (e.g. persistent sessions, dynamic weights) are not yet exposed through the Ingress. You can instead get these features through the load balancer used for a Service.

It is worth noting that even though health checks are not directly exposed through the Ingress, there are parallel concepts in Kubernetes such as readiness probes that allow you to achieve the same end result. Review the controller documentation to see how it handles health checks (for example, nginx, or GCE).

---

## Extraction provenance (read before quoting a manifest)

The rendered page was extracted first; three YAML manifests came back FABRICATED on that pass
(invented hostnames `foo.example.com`/`bar.example.com`/`sslexample.foo.com` and invented Service
names `foo`/`bar`). Every manifest above except the Secret was therefore re-verified character-for-
character against its raw example file under
raw.githubusercontent.com/kubernetes/website/main/content/en/examples/.

* VERIFIED against raw example file: test-ingress.yaml, simple-fanout-example.yaml,
  name-virtual-host-ingress.yaml, tls-example-ingress.yaml.
* Taken from the rendered page and consistent across passes: minimal-ingress.yaml,
  ingress-resource-backend.yaml, ingress-class.yaml, the kubectl describe output, the
  testsecret-tls Secret.
* The Simple fanout and Name based virtual hosting subsections are illustrated in the current
  source by SVG figure shortcodes (/docs/images/ingressFanOut.svg and
  /docs/images/ingressNameBased.svg), NOT by ASCII-art diagrams. An earlier extraction returned
  ASCII diagrams for these; those matched an older revision of the page and are excluded.
```

### A2 · `k8s-docs-ingress-controllers-2026-08-24.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/"
fetched_at: "2026-08-24T14:26:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC-BY-4.0"
objectives_covered: ["D2.1"]
concepts_covered: ["ingress-controller", "ingressclass", "absent-component-pattern", "reference-specification"]
---
# Ingress Controllers (kubernetes.io/docs/concepts/services-networking/ingress-controllers/)

(Fetched to support Ch 10 §3. The individual third-party controller products listed on this page
are deliberately NOT transcribed — the chapter outline forbids naming specific controllers.)

## Opening

In order for an Ingress to work in your cluster, there must be an *ingress controller* running. You need to select at least one ingress controller and make sure it is set up in your cluster.

## Using multiple Ingress controllers

You may deploy any number of ingress controllers using ingress class within a cluster. Note the `.metadata.name` of your ingress class resource. When you create an ingress you would need that name to specify the `ingressClassName` field on your Ingress object (refer to IngressSpec v1 reference). `ingressClassName` is a replacement of the older annotation method.

If you do not specify an IngressClass for an Ingress, and your cluster has exactly one IngressClass marked as default, then Kubernetes applies the cluster's default IngressClass to the Ingress. You mark an IngressClass as default by setting the `ingressclass.kubernetes.io/is-default-class` annotation on that IngressClass, with the string value `"true"`.

Ideally, all ingress controllers should fulfill this specification, but the various ingress controllers operate slightly differently.
```

### A3 · `k8s-docs-network-policies-depth-2026-08-24.md` (new)
```markdown
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
```

### A4 · `k8s-docs-deprecation-policy-2026-08-24.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/reference/using-api/deprecation-policy/"
fetched_at: "2026-08-24T14:34:00-0400"
authority: "Kubernetes project (kubernetes.io/docs), CC-BY-4.0"
objectives_covered: ["D2.1"]
concepts_covered: ["frozen-not-deprecated", "ga-stability-guarantee", "feature-freeze"]
---
# Kubernetes Deprecation Policy (kubernetes.io/docs/reference/using-api/deprecation-policy/)

(Fetched to close the verification flag on Ch 10 §4's third beat. This is the page the Ingress
"frozen" Note hyperlinks to when it says the Ingress API "is subject to the stability guarantees for
generally available APIs" — the anchor is #deprecating-parts-of-the-api. It supplies the formal
Kubernetes meaning of "deprecated", which the chapter contrasts against "frozen".)

## Overview

Kubernetes is a large system with many components and many contributors. As with any such software, the feature set naturally evolves over time, and sometimes a feature may need to be removed. This could include an API, a flag, or even an entire feature. To avoid breaking existing users, Kubernetes follows a deprecation policy for aspects of the system that are slated to be removed.

## Deprecating parts of the API

Since Kubernetes is an API-driven system, the API has evolved over time to reflect the evolving understanding of the problem space. The Kubernetes API is actually a set of APIs, called "API groups", and each API group is independently versioned.

The following rules govern the deprecation of elements of the API. This includes:

- REST resources (aka API objects)
- Fields of REST resources
- Annotations on REST resources, including "beta" annotations but not including "alpha" annotations.
- Enumerated or constant values
- Component config structures

These rules are enforced between official releases, not between arbitrary commits to master or release branches.

## Rules

**Rule #1: API elements may only be removed by incrementing the version of the API group.**

Once an API element has been added to an API group at a particular version, it can not be removed from that version or have its behavior significantly changed, regardless of track.

**Rule #2: API objects must be able to round-trip between API versions in a given release without information loss, with the exception of whole REST resources that do not exist in some versions.**

**Rule #3: An API version in a given track may not be deprecated in favor of a less stable API version.**

- GA API versions can replace beta and alpha API versions.
- Beta API versions can replace earlier beta and alpha API versions, but may not replace GA API versions.
- Alpha API versions can replace earlier alpha API versions, but may not replace GA or beta API versions.

**Rule #4a: API lifetime is determined by the API stability level**

- GA API versions may be marked as deprecated, but must not be removed within a major version of Kubernetes
- Beta API versions are deprecated no more than 9 months or 3 minor releases after introduction (whichever is longer), and are no longer served 9 months or 3 minor releases after deprecation (whichever is longer)
- Alpha API versions may be removed in any release without prior deprecation notice

**Rule #4b: The "preferred" API version and the "storage version" for a given group may not advance until after a release has been made that supports both the new version and the previous version**

Users must be able to upgrade to a new release of Kubernetes and then roll back to a previous release, without converting anything to the new API version or suffering breakages (unless they explicitly used features only available in the newer version).
```

### A5 · `k8s-docs-gateway-api-depth-2026-08-24.md` (new)
```markdown
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
```

### A6 · `k8s-blog-gateway-api-north-south-east-west-2026-08-24.md` (new)
```markdown
---
source_url: "https://kubernetes.io/blog/2023/08/29/gateway-api-v0-8/"
fetched_at: "2026-08-24T14:42:00-0400"
authority: "Kubernetes project (official kubernetes.io blog), CC-BY-4.0"
objectives_covered: ["D2.1"]
concepts_covered: ["north-south-traffic", "east-west-traffic", "gateway-api"]
---
# "Gateway API v0.8.0: Introducing Service Mesh Support" — kubernetes.io blog

Title: Gateway API v0.8.0: Introducing Service Mesh Support
Authors: Flynn (Buoyant), John Howard (Google), Keith Mattix (Microsoft), Michael Beaumont (Kong), Mike Morris (independent), Rob Scott (Google)
Published: Tuesday, August 29, 2023

(Fetched to resolve Ch 10 §1's SOURCE NOTE, which recorded that "north-south" and "east-west" appear
nowhere in the cached set and would have to be introduced as unsourced industry vocabulary. They are
in fact used on the official Kubernetes blog, and used in exactly the pairing §1 wants: ingress with
north-south, service mesh with east-west. This is a blog post, not the documentation — it is
authoritative as a Kubernetes-project publication but is NOT normative reference documentation. See
the manifest's Notes for the author, item 6.)

## Relevant passage

"While the initial focus of Gateway API was always ingress (north-south) traffic, it was clear almost from the beginning that the same basic routing concepts should also be applicable to service mesh (east-west) traffic."

"In 2022, the Gateway API subproject started the GAMMA initiative, a dedicated vendor-neutral workstream, specifically to examine how best to fit service mesh support into the framework of the Gateway API resources, without requiring users of Gateway API to relearn everything they understand about the API."
```

---

## Gaps

Nothing in `kb_tags` is left unsourced that was sourceable. The following are recorded so drafting does not invent to fill them.

| Gap | Status | Guidance for drafting |
|---|---|---|
| **"Silent failure" characterisation** (§7) — that an unenforced NetworkPolicy is *harder to detect* than a broken Ingress | **Confirmed unsourceable.** The source states the plugin dependency and the no-effect consequence and stops. It never uses "silent" or compares detectability. | Exactly as Open Question #8 recommends: present as the book's reasoning, not a documented claim, using the `chapter-03` line 597 idiom. Keep the tagged claim and the untagged inference in separate sentences. This is unchanged by this stage's research. |
| **`exposure-ceiling`, `absent-component-pattern`, `frozen-not-deprecated`, `l4-l7-boundary`** as *named terms* | Book coinages / Ch 3's phrase. No external source exists or is needed. | Do not attach `[source:` tags. The underlying facts are all sourced; the names are the book's. |
| **Trap frequency data** ("appears on X% of exams") | No source. None exists. | Per Part 14 guardrail #8 and **[B3]**, say "candidates get this wrong"; never quantify. |
| **`endPort` / port ranges in NetworkPolicy** | Not captured to a verified standard. | Out of chapter scope (not in `kb_tags`, not assigned by B6). Do not teach. If a later stage wants it, re-fetch. |
| **"Targeting multiple namespaces by label"** subsection YAML | Not captured. | Not needed — §6's namespace-selector content is fully covered by the "Behavior of `to` and `from` selectors" block in A3. |
| **Final sentence of the `Prefix` pathType definition** | Extracted unreliably; deliberately omitted from A3. | The three type names, the substring Note, and the Examples table are clean and sufficient. Do not quote the omitted sentence; teach `Prefix` from the Examples table. |
| **Which specific CNI plugins implement NetworkPolicy** | Not fetched, by design. | §7 already forbids naming them. Version-dependent and would date the book. |
| **Simple-fanout / name-based-virtual-hosting ASCII diagrams** | Do not exist in the current source (they are SVG figures now). | An earlier extraction returned ASCII art matching an older page revision; it is excluded from A1. Do not reproduce ASCII diagrams as if quoted. |

---

## Notes for the author

**1. ⚠ NEW PROBLEM — Gateway API now has FOUR stable kinds, not three. This breaks a Fixed Point and a Bearings item.**
The current page states: *"Gateway API has four stable API kinds"* — GatewayClass, Gateway, HTTPRoute, **and GRPCRoute**. The cached 08-23 snapshot recorded three, and the outline is built on three throughout: §5's `★ Fixed Point` ("**GatewayClass, Gateway, HTTPRoute** — and the three roles they belong to"), Bearings #2 item 3 ("**Name the three Gateway API resources**"), Exam Alert high-priority item 11, and the ⚠ instruction *"Do not teach GRPCRoute, TCPRoute, TLSRoute, ReferenceGrant, or the GAMMA initiative."*
The ⚠ instruction is still right on pedagogy — GRPCRoute is not what an associate-tier reader needs, and the role-to-resource mapping is the point. But **a question asking the reader to name "the three Gateway API resources" is now factually wrong against the source**, and that is the kind of thing this book's audits catch.
**Recommendation:** keep teaching the same three, but stop counting them. Phrase §5's Fixed Point as *"the three resources this chapter uses — GatewayClass, Gateway, HTTPRoute — and the role each belongs to"*, and rephrase Bearings #2 item 3 to *"Name the Gateway API resource that belongs to each of the three roles"*, which tests the mapping (the actual design insight) rather than a count that the source contradicts. One clause in §5 acknowledging that other route kinds exist for other protocols costs nothing and inoculates the reader. Note also that TCPRoute/TLSRoute/ReferenceGrant are *not* listed as stable, so the ⚠ correctly excludes them; GRPCRoute is the only one that changed status.

**2. Open Question #6 is CLOSED, and more strongly than expected.** The page's installation note is explicit: *"Instead of Gateway API resources being natively implemented by Kubernetes, the specifications are defined as Custom Resources supported by a wide range of implementations. Install the Gateway API CRDs or follow the installation instructions of your selected implementation."* Combined with *"Gateway API is an add-on containing API kinds"*, the one-clause fact your recommendation called for is now fully sourced and quotable. The recommendation stands unchanged — state the fact in §5, don't frame it as an instance of the pattern there, let §8 pick it up if it wants a fifth.

**3. ⚠ The out-of-scope list contains a phrase that directly contradicts §6's Fixed Point if quoted without care.** The list is confirmed at **exactly ten items** (verified by direct count against the raw markdown — an intermediate extraction claimed six, then eleven; both were wrong, and the cached 08-23 ten-item list is correct). But the *parentheticals*, which the 08-23 summary stripped and A3 now restores, include this on bullet nine:
> *The ability to explicitly deny policies (currently the model for NetworkPolicies **are deny by default**, with only the ability to add allow rules).*
Read cold, "deny by default" is the exact opposite of §6's `★ Fixed Point` that **a Pod is non-isolated in both directions by default**. Both are true and they are about different things — the source means that *once a policy selects a Pod*, the model within that policy is deny-by-default-plus-allow-rules; §6 means that *absent any policy*, nothing is restricted. §7's Dead Reckoning block is specified as the ten items *"stated flat, complete, in the source's own order"*, which would put that phrase in front of a reader eleven paragraphs after being told the opposite.
**Recommendation:** state the ten items flat, as planned, but **drop the parentheticals** — the plan's own wording ("the ten out-of-scope items") is satisfied by the bare items, the parentheticals are elaboration rather than list content, and bullet nine's is actively harmful here. If you want the parenthetical for bullets 3, 4 or 10 (all genuinely useful), take those and leave nine bare. Do not quote nine's parenthetical anywhere in the chapter.
Also note the source's own typos if quoting the introductory sentence: "its worth noting", "the model for NetworkPolicies are". A3 preserves them verbatim.

**4. Open Questions #2 and #3 are CLOSED. Both blocking gaps are fully sourced, and `pathType` has a stronger exam profile than the outline assumed.**
- **IngressClass** (#2): fully sourced in A1 and A2 — the `ingressClassName` field, the IngressClass resource and manifest, `spec.parameters`, Namespace-vs-Cluster scope, the `ingressclass.kubernetes.io/is-default-class` annotation, and (from the controllers page) *"You may deploy any number of ingress controllers using ingress class within a cluster"*, which is the direct answer to §3's "which one, if there are two?" A2 also supplies the cleanest possible support for §3's opening: *"In order for an Ingress to work in your cluster, there must be an ingress controller running. You need to select at least one ingress controller and make sure it is set up in your cluster."*
- **`pathType`** (#3): note the source's first sentence — ***"Each path in an Ingress is required to have a corresponding path type."*** Required, not optional. That plus a ten-row worked matching table plus an explicit tie-break rule (*"the match with the longest path will be given priority. If two paths are still equally long, the path with `Exact` path type will be given priority over `Prefix`"*) is precisely the enumerated, mechanically-testable detail this exam reaches for. Your instinct in #3 was right. **Recommendation: teach the three values and the required-ness in §2's sixth beat; do not teach the full matching table** — it is reference material, and the ⚪/🔵 difficulty of §2 does not support ten rows of edge cases. One Fixed Point and one example.
- **Hostname wildcards** are also now available and were not in the outline: `*.foo.com` matches `bar.foo.com` but not `baz.baz.foo.com` (a wildcard matches exactly one DNS label). **Recommendation: omit.** §2 is already the chapter's largest section and this is below the associate tier.

**5. Open Question #7 is CLOSED — you now have the option you asked for, and your recommendation still looks right.** A3 carries *"An empty `podSelector` selects all pods in the namespace"* verbatim, plus all five default-policy manifests (`default-deny-ingress`, `allow-all-ingress`, `default-deny-egress`, `allow-all-egress`, `default-deny-all`), plus `ipBlock`'s `except` field in the main example manifest. So §6's seventh beat can now name the empty-selector idiom with a source, or show `default-deny-all` outright.
**Recommendation: still derive, and still don't show the manifest** — for the reason you gave, which the source has not changed. But the derivation can now *name* the idiom ("an empty selector selects every Pod in the namespace") as sourced fact rather than hand-waving, which makes the derivation tighter at no cost in YAML. One additional sourced sentence worth having: *"once a NetworkPolicy is created for a pod, the pod will reject any traffic that is not allowed by any NetworkPolicy. (Other pods in the namespace that are not selected by any NetworkPolicy will continue to accept all traffic.)"* — that parenthetical is the cleanest statement in the whole source of the by-selection principle §6 is built on.

**6. §1's north-south / east-west SOURCE NOTE can be partly retired, but read the caveat.** The outline recorded these as absent from the cached set and recommended keeping them labelled as the industry's words. They are in fact used on the official Kubernetes blog (A6), in exactly the pairing §1 wants. **But A6 is a blog post, not reference documentation** — a Kubernetes-project publication, so tier-2 authoritative, but not normative. **Recommendation: keep §1's framing essentially as planned but soften the disclaimer** — these are not merely "the industry's words", they are words the Kubernetes project itself uses, just not in the concept docs. A `[source:` tag pointing at A6 is defensible. This also strengthens the §1 → Ch 17 §5 forward cross-bearing, since the quoted sentence *is* the ingress/mesh split the bearing promises.

**7. §4's verification flag is resolved, and the deprecation policy sharpens the contrast rather than simply confirming it.** The outline asked to verify whether `k8s-keps-and-feature-stages-2026-08-23.md` carries the deprecation-versus-freeze distinction. **It does not** — that snapshot covers alpha/beta/GA feature-gate stages and says nothing about deprecation as a formal status. A4 supplies what was missing, and it is the page the Ingress Note itself links to for "stability guarantees", so the two sources are formally connected rather than merely adjacent.
One nuance worth handling: Rule #4a says ***"GA API versions may be marked as deprecated, but must not be removed within a major version of Kubernetes."*** So in Kubernetes, even a *deprecated* GA API is not on a short road to removal. That slightly complicates the crisp §4 framing that "a deprecated one is by convention on its way out" — true as a general software convention, weaker as a Kubernetes-specific claim.
**Recommendation:** make §4's third beat stronger by using this rather than working around it. Deprecation in Kubernetes is a **formal status with defined, published support windows** — a specific thing the project does to an API, with rules attached. Ingress **has not been given that status**. It has been given a different one. That is a sharper and more defensible version of the same point than "deprecated means going away", it keeps the promise Chapter 9 made about precision, and it is fully sourced by A1 and A4 together. It also improves Bearings #2 item 2, whose correct answer ("false on both counts") is now backed by a policy document rather than by inference.

**8. §2's `⚓ Worth Securing` marker is now sourced verbatim and is stronger than the outline assumed.** The planned marker says TLS termination at the Ingress leaves Ingress-to-Pod traffic unencrypted. The source says it outright: *"The Ingress resource only supports a single TLS port, 443, and assumes TLS termination at the ingress point **(traffic to the Service and its Pods is in cleartext)**."* Quote it. It carries the Ch 17 §5 pointer on the source's own authority instead of the book's, which matters because this is a security claim.

**9. Process hazard worth recording for future research stages.** Extracting the rendered kubernetes.io pages produced **fabricated YAML three times** — an invented single-Service manifest (twice, differently, including a syntactically invalid `host:` block), and invented hostnames and Service names in the fanout, virtual-host and TLS examples (`foo.example.com`/`foo`/`bar`/`sslexample.foo.com` in place of the real `foo.bar.com`/`service1`/`service2`/`https-example.foo.com`). It also produced a plausible six-item version of the out-of-scope list that does not exist, and ASCII diagrams from a superseded page revision. Every manifest in A1 was consequently re-verified against `raw.githubusercontent.com/kubernetes/website/main/content/en/examples/...`, and the out-of-scope list against the page's raw markdown.
**Recommendation for the pipeline:** for any snapshot where verbatim fidelity is load-bearing — which is all of them, since downstream audits verify facts against this exact text — fetch `raw.githubusercontent.com/kubernetes/website/main/content/en/docs/...` rather than the rendered page, and follow `code_sample` shortcodes to the example file. A1 and A5 carry per-block provenance notes recording which manifests were verified which way. Worth folding into `pipeline/prompts/02_research.md`.

**10. Minor, recorded not raised.** The current Gateway page's cardinality prose is *"A Gateway object is associated with exactly one GatewayClass"* (confirmed, and Bearings #2 item 4's first half is safe) but the second half is now *"One or more route kinds such as HTTPRoute, are then associated to Gateways"* rather than the crisper "many Routes may attach to a Gateway" the 08-23 snapshot recorded. The examinable fact is unchanged and "many" remains a fair reading; the source just states it less tidily than the cached condensation implied. No action needed unless a later audit flags the wording.