## 🔵 §2 — Routing by Host and Path

Chapter 9 gave you a warning attached to a promise. It told you, by name, that conflating **DNS-based service discovery** with **name-based virtual hosting** would make this chapter considerably harder than it needs to be, and it pointed here *[cross-bearing: see Ch 9 §7 — DNS-based service discovery, and what it is not]*. We will settle that distinction properly, a few beats in.

First, the object.

### What Ingress is

**Ingress exposes HTTP and HTTPS routes from outside the cluster to Services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource** [source: k8s-docs-ingress-depth-2026-08-24].

Read that twice, because both halves matter. *Routes from outside to Services within* — the things an Ingress routes to, in every case this chapter covers, are ordinary Services. The ClusterIP Services you built in Chapter 9, unchanged, unaware that anything new is in front of them. And *rules defined on the resource*: the routing decisions live in the object you write, not in the controller's configuration file.

An Ingress may be configured to give Services externally-reachable URLs, load balance traffic, terminate SSL/TLS, and offer name-based virtual hosting [source: k8s-docs-ingress-depth-2026-08-24]. Four capabilities, as the documentation enumerates them.

### And what it refuses to do

Immediately after the capabilities, and not buried at the bottom of the section where you would skim past it:

**An Ingress does not expose arbitrary ports or protocols. Exposing services other than HTTP and HTTPS to the internet typically uses a service of type `Service.Type=NodePort` or `Service.Type=LoadBalancer`** [source: k8s-docs-ingress-depth-2026-08-24].

This is more satisfying than a caveat. It means the ladder you learned in Chapter 9 is not superseded by this chapter. It is *specialised past*. Ingress takes over one class of traffic, the HTTP class, and everything else goes back down to §1's layer. A PostgreSQL database, a message broker speaking its own binary protocol, a game server, an SMTP relay: none of those go through an Ingress. They go through NodePort or LoadBalancer, exactly as they did last chapter.

> ★ **Fixed Point:** Ingress is **HTTP and HTTPS only.** It exposes no arbitrary ports and no other protocols. Anything else goes back down to `Service.Type=NodePort` or `Service.Type=LoadBalancer`.

### The shapes an Ingress takes

Four, and they are best learned as a progression rather than as a list.

**Ingress backed by a single Service.** The degenerate case: no rules at all, one default backend, everything goes to one place [source: k8s-docs-ingress-depth-2026-08-24].

```yaml
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
```

Worth thirty seconds, mostly so the more interesting cases have a baseline to differ from.

**Simple fanout.** A fanout configuration **routes traffic from a single IP address to more than one Service, based on the HTTP URI being requested** — which, as the documentation dryly notes, allows you to keep the number of load balancers down to a minimum [source: k8s-docs-ingress-depth-2026-08-24]. This is our running example. One host, two paths, two backends:

```yaml
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
```

One `host`. Two entries under `paths`. Each names a backend Service and a port. That is the whole shape.

**Name-based virtual hosting.** Name-based virtual hosts **support routing HTTP traffic to multiple host names at the same IP address** [source: k8s-docs-ingress-depth-2026-08-24]. Note what changed: the list is now at the level of `host`, and the paths beneath each are just `/`.

```yaml
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
```

Compare the two manifests side by side. They put the same number of Services behind the same single address. They differ in **which part of the request the rule reads**: the path in one, the host in the other. That is the entire distinction, and it is the one an exam will ask you to make.

> ★ **Fixed Point:** **Simple fanout** splits by *path* at one host. **Name-based virtual hosting** splits by *host* at one address. Both put many Services behind one IP; they differ only in what the rule reads.

<!-- FIGURE: ch10-fig02-ingress-fanout-and-name-based-hosts -->
```
                    SIMPLE FANOUT — split by PATH

   GET /catalog HTTP/1.1                     ┌──────────────────┐
   Host: shop.example.com                    │  catalog Service │
        ▲▲▲▲▲▲▲▲                             └──────────────────┘
                                                      ▲
        ┌──────────────┐    ┌──────────────┐          │ path = /catalog
   ───▶ │ 203.0.113.10 │───▶│ reads: path  │──────────┤
        └──────────────┘    └──────────────┘          │ path = /checkout
                                                      ▼
   GET /checkout HTTP/1.1                    ┌──────────────────┐
   Host: shop.example.com                    │ checkout Service │
        ▲▲▲▲▲▲▲▲▲                            └──────────────────┘


           NAME-BASED VIRTUAL HOSTING — split by HOST

   GET / HTTP/1.1                            ┌──────────────────┐
   Host: shop.example.com                    │   shop Service   │
         ▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲                    └──────────────────┘
                                                      ▲
        ┌──────────────┐    ┌──────────────┐          │ host = shop…
   ───▶ │ 203.0.113.10 │───▶│ reads: host  │──────────┤
        └──────────────┘    └──────────────┘          │ host = blog…
                                                      ▼
   GET / HTTP/1.1                            ┌──────────────────┐
   Host: blog.example.com                    │   blog Service   │
         ▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲▲                    └──────────────────┘

   Same address in both. Same number of Services in both.
   ▲▲▲ marks the part of the request the rule matched on.
```

**TLS.** You can secure an Ingress by specifying a **Secret that contains a TLS private key and certificate** [source: k8s-docs-ingress-depth-2026-08-24]. The Ingress resource supports a single TLS port, 443, and **assumes TLS termination at the ingress point — traffic to the Service and its Pods is in cleartext** [source: k8s-docs-ingress-depth-2026-08-24]. The TLS Secret must contain keys named `tls.crt` and `tls.key` [source: k8s-docs-ingress-depth-2026-08-24], and the documentation's example Secret is of type `kubernetes.io/tls` — the Secret type Chapter 4 catalogued *[cross-bearing: see Ch 4 §4 — Secret types, including `kubernetes.io/tls`]*.

```yaml
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
```

This is the chapter's cheapest retrieval and one of its most satisfying. You have known what a Secret is since Chapter 4; here is one doing a visible job.

> ⚓ **Worth Securing:** TLS termination at the Ingress means the private key lives in a Secret in the cluster and the backend Services can speak plain HTTP. Convenient, and worth knowing precisely, because the documentation says outright that traffic onward to the Service and its Pods is in cleartext [source: k8s-docs-ingress-depth-2026-08-24]. Encrypting *that* leg is a different problem with a different answer *[cross-bearing: see Ch 17 §5 — what a service mesh adds inside the cluster]*.

### The distinction Chapter 9 asked for

Both DNS-based service discovery and name-based virtual hosting involve hostnames. They sit on **opposite sides of the connection**.

DNS turns a name into an address **before any traffic moves.** A client that wants `shop.example.com` asks a resolver, gets back `203.0.113.10`, and only then opens a connection. The name has done its work and is, as far as the network is concerned, finished.

Virtual hosting sorts traffic that has **already arrived** at a single address, by reading the name back out of the request. The client that resolved `shop.example.com` and the client that resolved `blog.example.com` got the *same* address from DNS. They are both now talking to the same socket on the same machine. The only thing distinguishing them is the `Host` header they each sent, and something at that address has to open the request and read it.

> ⚠ **Navigational Hazards:** DNS gave you the address. Virtual hosting decides what happens *after* you have used it. Same hostname, two different jobs, on opposite sides of the connection. This is the confusion Chapter 9 warned you about by name, and the reason it warned you is that a reader who has them merged will spend §5's request flow wondering why the resolver appears twice. Once you are inside, virtual hosting is the harbourmaster deciding which berth you take.

### The fields, briefly

An Ingress needs `apiVersion`, `kind`, `metadata` and `spec`, like every object you have written since Chapter 4. The spec **contains a list of rules matched against all incoming requests**, and supports rules for directing HTTP(S) traffic only [source: k8s-docs-ingress-depth-2026-08-24].

Each HTTP rule contains an **optional host** — if no host is specified the rule applies to all inbound HTTP traffic through that IP address; if a host is given, the rules apply to that host — and **a list of paths, each with an associated backend defined with a `service.name` and a `service.port.name` or `service.port.number`.** Both the host and the path must match the content of an incoming request before traffic is directed to the referenced Service [source: k8s-docs-ingress-depth-2026-08-24].

**Path types.** Each path in an Ingress is **required to have a corresponding path type**, and paths without an explicit `pathType` are not validated [source: k8s-docs-ingress-depth-2026-08-24]. There are three:

| `pathType` | Behaviour |
|---|---|
| `Exact` | Matches the URL path exactly, case-sensitively [source: k8s-docs-ingress-depth-2026-08-24] |
| `Prefix` | Matches on a URL path prefix split by `/`, case-sensitively, element by element [source: k8s-docs-ingress-depth-2026-08-24] |
| `ImplementationSpecific` | Matching is up to the IngressClass; implementations may treat it as its own type or identically to `Prefix` or `Exact` [source: k8s-docs-ingress-depth-2026-08-24] |

The element-by-element part of `Prefix` is where people get caught. Matching is done on **path elements** — the labels between `/` separators — not on raw string prefixes. A path of `/foo/bar` does **not** match a request path of `/foo/barbaz`, because the last element `bar` is only a substring of `barbaz`, not equal to it [source: k8s-docs-ingress-depth-2026-08-24].

> 🪝 **Snag:** `Prefix` is not a string prefix. `/aaa/bb` does not match `/aaa/bbb` [source: k8s-docs-ingress-depth-2026-08-24]. The comparison happens element by element, and `bb ≠ bbb`. If you have carried over an instinct from string-prefix path matching anywhere else, this is *almost* the semantics you expect, and "almost" is what makes it expensive.

**The default backend.** An Ingress with no rules sends all traffic to a single default backend, and `.spec.defaultBackend` is what handles requests in that case [source: k8s-docs-ingress-depth-2026-08-24]. Conventionally the default backend is a configuration option of the Ingress controller rather than something you specify per-Ingress [source: k8s-docs-ingress-depth-2026-08-24], but note the rule that binds them: **if no `.spec.rules` are specified, `.spec.defaultBackend` must be specified** [source: k8s-docs-ingress-depth-2026-08-24]. And if none of the hosts or paths in any Ingress match an incoming request, the traffic is routed to the default backend [source: k8s-docs-ingress-depth-2026-08-24].

That is the Ingress object. It is a small, legible API, and everything in it does exactly what it says.

None of it has happened yet.

---