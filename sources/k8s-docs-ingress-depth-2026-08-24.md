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
