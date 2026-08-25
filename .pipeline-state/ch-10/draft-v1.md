# Chapter 10: Traffic from Beyond the Cluster
## *"Frozen, superseded, and inert without a controller"*

**Domain: Container Orchestration (competency: Networking) | Domain weight: 28% [source: cncf-kcna-curriculum-pdf-2026-08-23] | Complexity: Mixed | Novelty: Moderate**

> *The 28% figure is CNCF's published weight for the whole Container Orchestration domain. CNCF publishes no per-competency weights; this book's allocation of that 28% across its Part III chapters is the author's, derived from curriculum breadth rather than from any published figure. See the front matter's weight-allocation disclosure.*

---

## Attention Budget

**Total time: ~85 minutes | Recommended: Split across 2 sessions**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| 🧭 Soundings | 10 min | Low | Anytime |
| §1 Where LoadBalancer Runs Out | 6 min | Low | Anytime |
| §2 Routing by Host and Path | 12 min | Medium | Mid-session |
| §3 The Object Is Not the Implementation | 8 min | Medium | Mid-session |
| ☆ Taking Your Bearings #1 | 6 min | Medium | After a brief break |
| §4 Frozen, Not Deprecated | 6 min | Medium | Peak attention |
| §5 Roles, Not Just Routes | 12 min | High | Peak attention |
| ☆ Taking Your Bearings #2 | 6 min | Medium | After a brief break |
| §6 Allowing, Never Denying | 14 min | High | **Start of session 2** |
| §7 What NetworkPolicy Cannot Do | 8 min | Medium | Mid-session |
| ☆ Taking Your Bearings #3 | 6 min | High | After a brief break |
| §8 Nothing Happens Without a Controller | 5 min | Low | Anytime |
| Exam Alert + Practice Questions | 25 min | High | Fresh session |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

**The session split goes between §5 and §6.** This chapter is two chapters wearing one number: an API-generations arc (§1–§5) and a policy arc (§6–§7), joined at §8. §6 asks you to unlearn a firewall instinct you have probably held for a decade, and it will land better on a fresh head than on a tired one.

*If you only have 15 minutes: read §3, §4, and §6, and take Bearings #3.*

---

> *"An object is a record of intent. Intent does not act."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score determines how to approach the content; no shame in any score, just different reading strategies. Four of these test priors you arrive with; four are deliberate retrieval from Chapters 3 and 9.

1. You run one web server on one IP address, and it serves `shop.example.com` and `blog.example.com` differently. What does the server have to look at to tell the two apart, and at what point in the connection does that information become available?

2. You have fifty services that all need to be reachable from outside the cluster. Chapter 9 gave you a Service type that does exactly that. Name it, then say what fifty of them costs you: addresses, and anything else you can think of.

3. Which of Chapter 9's four Service types can send `/checkout` to one set of Pods and `/catalog` to another? Say why.

4. On the firewalls you have configured or worked behind: if a packet matches no rule at all, is it allowed or dropped? And if one rule permits something a later rule forbids, which one wins?

5. Two APIs. One is announced as **deprecated**. The other is announced as **no longer being developed, with no further changes**. For each, say whether you would expect it to be removed, and whether you would start a new project on it today.

6. Chapter 3 asked you to remember a one-sentence rule about objects and the components that act on them. Write it down. Then name one place you have already met it.

7. Chapter 9's second network-model rule said all Pods can reach all Pods — *"barring intentional network segmentation."* What do you think that hedge was pointing at, and at what layer would something have to sit to enforce it?

8. A client connects to `https://shop.example.com` and the request eventually reaches an application server. Where does the TLS connection actually end? Who holds the certificate and private key, and what does the application server see arriving?

<details>
<summary>Click for answers + reading strategy</summary>

1. **The `Host` header, available only after the TCP connection is established and the request has been sent.** The client's DNS lookup resolved the name to an address before any traffic moved; the name itself travels inside the request. (HTTPS carries an earlier tell in the SNI field of the TLS handshake, but the routing decision is conventionally made on the `Host` header.)

2. **`Service.Type=LoadBalancer`.** Fifty of them costs fifty external addresses, fifty provisioned load balancers, fifty line items on a cloud bill, and fifty things to configure, monitor, and eventually decommission.

3. **None of them.** All four Service types operate on addresses and ports. `/checkout` and `/catalog` are bytes inside an HTTP request; nothing in Chapter 9 opens the request to look.

4. Most likely **dropped**, and **the deny wins**. That is how ordinary packet-filtering firewalls behave, it is a sound instinct nearly everywhere, and it is the instinct §6 is going to take away from you.

5. **Deprecated** implies eventual removal, so you would avoid starting new work on it. **No longer developed** says nothing about removal; it says the thing is finished. It may well be permanent. You might still use it, knowing it will never gain a feature.

6. **An object without its component does nothing.** You have met it at least twice: a `type: LoadBalancer` Service on a cluster with no load balancer to provision, and a Service whose selector matched no Pods.

7. Something has to be able to restrict Pod-to-Pod reachability. Since the CNI plugin is what actually moves the packets, enforcement would have to live down there, at layer 3 or 4, wherever the packets are.

8. **At the reverse proxy or load balancer at the edge**, which holds the certificate and private key. The application server behind it receives plain HTTP.

---

**If you got 6+ right:** Skim §1 and §2 — you have the priors. Read §4 carefully anyway; it is a word-level distinction and skimming is exactly how people lose that point. Then read §6 and §7 at full attention regardless of your score.

**If you got 3–5 right:** Read at normal pace. The material is in reach and this chapter is calibrated for you.

**If you got 0–2 right:** Read carefully. And if questions 2, 3, or 7 were among your misses, **go back to Chapter 9 first.** Not "review" — go back. This chapter re-teaches no part of the Service model. §1's argument is arithmetic on Chapter 9's ladder, §2's backends are Chapter 9's Services, and §6's subjects are Chapter 9's Pod IPs. A re-read of Chapter 9 will buy you more than a careful read of this chapter will.

</details>

---

## Why This Chapter Matters

Chapter 9 ended by naming a ceiling. One external address per Service is reasonable when you have one Service. It is absurd when you have fifty. And no Service type in that chapter can tell `shop.example.com/checkout` from `shop.example.com/catalog`, because at the layer those mechanisms operate on, the difference between those two requests is bytes in a payload that nothing is opening.

This chapter is what sits above that ceiling *[cross-bearing: see Ch 9 §3 — the Service-type ladder and its limits]*.

But the more valuable thing here is not the objects. It is a question.

Every chapter so far has rewarded the same professional instinct: get the object right, and the cluster does the rest. Write a correct Deployment and Pods appear. Write a correct Service and a stable name appears. That instinct has been reliable for nine chapters, and this is the chapter where it stops being enough. This is where you learn the question that separates people who have run Kubernetes from people who have read about it.

The question is not *did I write the object correctly.* It is **is anything watching this object.**

A well-formed Ingress on a cluster with no Ingress controller is a correct object that does nothing. A well-formed NetworkPolicy on a network plugin that does not implement NetworkPolicy is a correct object that does nothing. Unlike the Ingress, it does nothing *quietly*. Unreachability is loud: a pager goes off, a customer complains, somebody is looking at it within minutes. Unrestricted reachability is silent; everything works exactly as it did, which is indistinguishable from a policy working perfectly against traffic nobody happens to be sending. That asymmetry is the most valuable thing in this chapter, and you should have it in hand before you meet either object.

Chapter 9 told you that Chapter 10 would give a name to a shape you had already met twice. Here is the part Chapter 9 did not say: you will meet it **twice more in this chapter alone**, in two objects that have nothing to do with each other. This is where it stops being a curiosity and becomes a rule you can apply to things this book never mentions.

The stakes, stated flat. This is the smallest allocation in Part III, and the material still deserves full attention for two specific reasons. First, `frozen` versus `deprecated` is the most precise word-level distinction in the curriculum, and precise distinctions are what multiple-choice exams are built out of. Second, NetworkPolicy carries more cataloged traps than any other single topic in this book, and every one of them is a case where your existing firewall intuition hands you the wrong answer with complete confidence.

Two reasons. The chapter does not need a third.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **State** what Ingress does, what it explicitly does not do, and which two protocols are the whole of its remit.
- **Distinguish** a simple fanout from name-based virtual hosting, and both from the DNS-based service discovery you learned last chapter.
- **Explain** why a correctly written Ingress can have no effect whatsoever, and name the thing whose absence causes it.
- **Say what `frozen` means** — precisely, in both of its halves — and why it is not the same word as `deprecated`.
- **Name** the Gateway API resources and the organisational role each one belongs to.
- **Predict** whether a given connection is allowed under a given set of NetworkPolicies, using rules that are additive, allow-only, and applied at both ends.

*You'll also acquire one rule that outlives this chapter: an object without its component does nothing. You'll use it in Chapter 13, in Chapter 17, and on things this book never gets to.*

---

## ⚪ §1 — Where LoadBalancer Runs Out

You already have the argument. Chapter 9 made it, and made it recently.

One external address per Service. Fifty Services, fifty addresses, fifty provisioned load balancers, fifty bills, fifty things to manage. And no Service type in that chapter reads HTTP, so a single address cannot serve two paths. A Service knows an address and a port, and stops there *[cross-bearing: see Ch 9 §3 — the Service-type ladder and the exposure ceiling]*.

That is the ceiling. This section does not re-derive it. It names the vocabulary the rest of the chapter runs on, and gets out of the way.

### The layer boundary

Everything in Chapter 9 operates at **layer 4**. A Service moves packets to an address and a port and has no opinion about what those packets contain. Everything in §2 through §5 operates at **layer 7**: it reads the request — the host it was addressed to, the path it asked for, sometimes the headers it carries — and decides where to send it on that basis. The Kubernetes documentation makes the same split, describing Gateway API and Ingress as protocol-aware HTTP/HTTPS routing using URIs, hostnames, and paths, and `type: LoadBalancer` as the simpler but less configurable mechanism for getting traffic into a cluster [source: k8s-docs-network-model-2026-08-23].

Keep this boundary on your chart. It is not decoration and it is not only about §2. §6 goes back *down* to layers 3 and 4, and a reader who has lost the ladder will experience NetworkPolicy as an unrelated topic that happened to land in the same chapter.

> ★ **Fixed Point:** Everything in Chapter 9 moves **packets** to an address. Everything in §2 through §5 reads **requests**. Which side of that boundary a mechanism sits on determines what it can know, and therefore what it can decide.

### North-south and east-west

Two words from ordinary practitioner vocabulary that this book has not used yet. They make the shape of this chapter sayable in one sentence.

**North-south** traffic enters the cluster from outside. **East-west** traffic moves between Pods inside it. The Kubernetes project itself uses the pairing exactly this way, describing the initial focus of Gateway API as ingress, "north-south," traffic, and service mesh as the "east-west" case [source: k8s-blog-gateway-api-north-south-east-west-2026-08-24].

This chapter does one of each. §1 through §5 are about north-south. §6 and §7 are about east-west.

> 🪢 **Mnemonic:** *North-south goes through the wall; east-west stays inside it.* §1–§5 is the wall. §6–§7 is inside.

### The edge router

One piece of scaffolding Chapter 9 did not supply, and §3 will need.

The Kubernetes documentation is explicit that in most common deployments, **the nodes in your cluster are not part of the public internet** [source: k8s-docs-ingress-depth-2026-08-24]. Something sits between the two: the **edge router**, a router that enforces the firewall policy for your cluster, whether that is a gateway managed by a cloud provider or a physical piece of hardware [source: k8s-docs-ingress-depth-2026-08-24].

Naming it here means that when §3 tells you an Ingress controller may fulfil an Ingress "usually with a load balancer, though it may also configure your edge router," you already know what that clause is about.

The same terminology block gives the vocabulary for everything else in this chapter, and it should all be familiar: a **node** is a worker machine, part of a cluster; the **cluster network** is the set of links, logical or physical, that carry communication within a cluster according to the Kubernetes networking model; a **Service** identifies a set of Pods using label selectors and is assumed to have a virtual IP routable only within the cluster network [source: k8s-docs-ingress-depth-2026-08-24]. That last clause is the whole problem in one line. The addresses Chapter 9 gave you work beautifully inside the harbour wall, and mean nothing beyond it.

### What comes next, and the first thing worth knowing about it

There is an object for the layer-7 job. It is called Ingress.

And the first thing to know about it is that writing one may accomplish nothing at all. We will get to why in §3. Carry the expectation into §2 *[cross-bearing: see Ch 10 §3 — the Ingress controller and what its absence costs]*.

*[cross-bearing: see Ch 17 §5 — a service mesh does at layer 7 for east-west traffic roughly what §2 does for north-south]*

---

## 🔵 §2 — Routing by Host and Path

Chapter 9 gave you a warning attached to a promise. It told you, by name, that conflating **DNS-based service discovery** with **name-based virtual hosting** would make this chapter considerably harder than it needs to be, and it pointed here *[cross-bearing: see Ch 9 §7 — DNS-based service discovery, and what it is not]*. We will settle that distinction properly, a few beats in.

First, the object.

### What Ingress is

**Ingress exposes HTTP and HTTPS routes from outside the cluster to Services within the cluster. Traffic routing is controlled by rules defined on the Ingress resource** [source: k8s-docs-ingress-depth-2026-08-24].

Read that twice, because both halves matter. *Routes from outside to Services within* — the things an Ingress routes to are ordinary Services. The ClusterIP Services you built in Chapter 9, unchanged, unaware that anything new is in front of them. And *rules defined on the resource*: the routing decisions live in the object you write, not in the controller's configuration file.

An Ingress may be configured to give Services externally-reachable URLs, load balance traffic, terminate SSL/TLS, and offer name-based virtual hosting [source: k8s-docs-ingress-depth-2026-08-24]. Four capabilities. That is the complete list as the documentation gives it.

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

**TLS.** You can secure an Ingress by specifying a **Secret that contains a TLS private key and certificate** [source: k8s-docs-ingress-depth-2026-08-24]. The Ingress resource supports a single TLS port, 443, and **assumes TLS termination at the ingress point — traffic to the Service and its Pods is in cleartext** [source: k8s-docs-ingress-depth-2026-08-24]. The Secret must be of type `kubernetes.io/tls` and contain keys named `tls.crt` and `tls.key` [source: k8s-docs-ingress-depth-2026-08-24], which is the Secret type Chapter 4 catalogued *[cross-bearing: see Ch 4 §4 — Secret types, including `kubernetes.io/tls`]*.

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

> ⚠ **Navigational Hazards:** DNS gave you the address. Virtual hosting decides what happens *after* you have used it. Same hostname, two different jobs, on opposite sides of the connection. This is the confusion Chapter 9 warned you about by name, and the reason it warned you is that a reader who has them merged will spend §5's request flow wondering why the resolver appears twice. DNS is the chart that gets you into the harbour. Virtual hosting is the harbourmaster deciding which berth you take once you are inside it.

### The fields, briefly

An Ingress needs `apiVersion`, `kind`, `metadata` and `spec`, like every object you have written since Chapter 4. The spec **contains a list of rules matched against all incoming requests**, and supports rules for directing HTTP(S) traffic only [source: k8s-docs-ingress-depth-2026-08-24].

Each HTTP rule contains an **optional host** — if no host is specified the rule applies to all inbound HTTP traffic through that IP address; if a host is given, the rules apply to that host — and **a list of paths, each with an associated backend defined with a `service.name` and a `service.port.name` or `service.port.number`.** Both the host and the path must match the content of an incoming request before traffic is directed to the referenced Service [source: k8s-docs-ingress-depth-2026-08-24].

**Path types.** Each path in an Ingress is **required to have a corresponding path type**, and paths without an explicit `pathType` are not validated [source: k8s-docs-ingress-depth-2026-08-24]. There are three:

| `pathType` | Behaviour |
|---|---|
| `Exact` | Matches the URL path exactly, case-sensitively [source: k8s-docs-ingress-depth-2026-08-24] |
| `Prefix` | Matches on a URL path prefix split by `/`, case-sensitively, element by element [source: k8s-docs-ingress-depth-2026-08-24] |
| `ImplementationSpecific` | Matching is up to the IngressClass; implementations may treat it as its own type or identically to `Prefix` or `Exact` [source: k8s-docs-ingress-depth-2026-08-24] |

The element-by-element part of `Prefix` is where people get caught. Matching is done on **path elements** — the labels between `/` separators — not on raw string prefixes. A path of `/foo/bar` does **not** match a request path of `/foo/barbaz`, because the last element `bar` is only a substring of `barbaz`, not equal to it [source: k8s-docs-ingress-depth-2026-08-24]. And where several paths match one request, **the match with the longest path wins; if two are equally long, `Exact` beats `Prefix`** [source: k8s-docs-ingress-depth-2026-08-24].

> 🪝 **Snag:** `Prefix` is not a string prefix. `/aaa/bb` does not match `/aaa/bbb` [source: k8s-docs-ingress-depth-2026-08-24]. The comparison happens element by element, and `bb ≠ bbb`. If you have ever written an nginx `location` block, this is *almost* the semantics you expect, and "almost" is what makes it expensive.

**The default backend.** An Ingress with no rules sends all traffic to a single default backend, and `.spec.defaultBackend` is what handles requests in that case [source: k8s-docs-ingress-depth-2026-08-24]. Conventionally the default backend is a configuration option of the Ingress controller rather than something you specify per-Ingress [source: k8s-docs-ingress-depth-2026-08-24], but note the rule that binds them: **if no `.spec.rules` are specified, `.spec.defaultBackend` must be specified** [source: k8s-docs-ingress-depth-2026-08-24]. And if none of the hosts or paths in any Ingress match an incoming request, the traffic is routed to the default backend [source: k8s-docs-ingress-depth-2026-08-24].

**Hostname wildcards.** Hosts may be precise matches or wildcard patterns, designated by `*` as the leftmost label, and **a wildcard matches exactly one DNS label** [source: k8s-docs-ingress-depth-2026-08-24]. So `*.foo.com` matches `bar.foo.com` but not `baz.baz.foo.com`, and does not match `foobar.foo.com` either [source: k8s-docs-ingress-depth-2026-08-24].

That is the Ingress object. It is a small, legible API, and everything in it does exactly what it says.

None of it has happened yet.

---

## ⚪ §3 — The Object Is Not the Implementation

Here is the sentence:

**You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect** [source: k8s-docs-ingress-depth-2026-08-24].

Not "less effect." Not "reduced functionality." None. The manifests in §2 are correct, well-formed, and accepted by the API server, and on a cluster with no Ingress controller they route nothing, because nothing is reading them.

> ★ **Fixed Point:** **You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect** [source: k8s-docs-ingress-depth-2026-08-24].

### What an Ingress controller is

**An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends to help handle the traffic** [source: k8s-docs-ingress-depth-2026-08-24]. There it is: §1's edge router, doing its job in a sentence you can now read without stopping. For an Ingress to work in your cluster, **there must be an ingress controller running**, and you need to select at least one and make sure it is set up [source: k8s-docs-ingress-controllers-2026-08-24].

Notice the structure of what you just read. The Ingress object is a *description of desired routing.* The controller is a control loop that reads that description and makes something in the real world match it. That is Chapter 3's control loop, unchanged, in its fourth or fifth appearance: desired state in an object, a controller watching, reality dragged toward the description *[cross-bearing: see Ch 3 §6 — the control loop and the controller pattern]*. Recognising it here should cost you nothing, which is the point of having learned it once properly.

### The rule, retrieved

Chapter 3 gave you a sentence and asked you to keep it:

**An object without its component does nothing.**

It also told you that you would meet it four more times. This is the first of the four, and Chapter 3 published the pointer to this exact paragraph *[cross-bearing: see Ch 3 §4 — addons, and what else is optional]*.

You do not have to take the rule on faith, because you have already collected evidence for it. Last chapter, twice:

- A `type: LoadBalancer` Service on a bare-metal cluster with no provider integration. A real object. A real cluster IP. An external address field that stays `<pending>` forever, because Kubernetes does not directly offer a load balancing component; you must provide one, or integrate with a cloud provider [source: k8s-docs-service-2026-08-23] *[cross-bearing: see Ch 9 §3 — LoadBalancer and what has to exist beneath it]*.
- A Service whose selector matched nothing. A real object, a real cluster IP, a real DNS record, an empty EndpointSlice, and traffic that goes nowhere at all *[cross-bearing: see Ch 9 §4 — selectors, EndpointSlices, and the empty case]*.

Now a third: an Ingress with no controller.

> ⚓ **Worth Securing:** Chapter 3's phrase, verbatim, and worth writing on something you will see again: **an object without its component does nothing.** You have now personally met three instances: the LoadBalancer with no provider, the Service with no matching Pods, and this. Three sightings of the same light, and you stop calling it a coincidence and start calling it a landmark.

### Naming which controller: IngressClass

"You must have a controller" raises an obvious follow-up: *which one, if there are two?*

You may deploy any number of ingress controllers in a cluster, using **ingress class** to tell them apart [source: k8s-docs-ingress-controllers-2026-08-24]. Ingresses can be implemented by different controllers, often with different configuration, so **each Ingress should specify which controller it is intended to use** — done with the **`ingressClassName`** field on the Ingress, which references an **IngressClass** resource that carries additional configuration including the name of the controller that should implement the class [source: k8s-docs-ingress-depth-2026-08-24].

```yaml
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
```

If you do not specify an IngressClass on an Ingress and your cluster has **exactly one** IngressClass marked as default, Kubernetes applies that default [source: k8s-docs-ingress-controllers-2026-08-24]. You mark one as default by setting the `ingressclass.kubernetes.io/is-default-class` annotation to the string `"true"` [source: k8s-docs-ingress-controllers-2026-08-24]. Some ingress controllers work even without a default IngressClass defined; even so, the Kubernetes project still recommends that you define one [source: k8s-docs-ingress-depth-2026-08-24].

### The honest note

One more fact, and it is the one that keeps this from being a tidy story:

**Ideally, all Ingress controllers should fit the reference specification. In reality, the various Ingress controllers operate slightly differently** [source: k8s-docs-ingress-depth-2026-08-24].

That is the documentation's own phrasing, twice over: the Ingress page and the Ingress Controllers page say the same thing in nearly the same words [source: k8s-docs-ingress-controllers-2026-08-24]. It matters because the promise of a portable object is undercut, precisely, by the gap between a reference specification and any particular implementation of it. The documentation's own advice is to review your controller's documentation to understand the caveats of choosing it [source: k8s-docs-ingress-depth-2026-08-24].

> 🪝 **Snag:** Two clusters, the same Ingress manifest, different behaviour. Same chart, different pilot. The object is portable; the controllers are only *ideally* identical. The gap between the reference specification and a particular implementation is where a configuration that worked for a year stops working after a migration, and where the failure looks like a bug in your manifest rather than a difference in the thing reading it.

You now have a rule and three instances of it. Do not close the pattern here. §7 has a fourth, and it behaves differently from the first three in a way that turns out to matter more than all of them.

*[cross-bearing: see Ch 6 §8 — a custom controller acting on a custom resource is this same shape, met as the operator pattern]*
*[cross-bearing: see Ch 13 §7 — `kubectl top` on a cluster with no metrics-server]*
*[cross-bearing: see Ch 17 §7 — VPA, which is an addon and is not there by default]*

---

## ☆ Taking Your Bearings #1

Five questions on §1 through §3 — the ceiling, the object, and the component that has to exist. Two of them reach back to earlier chapters.

**1.** ⚪ `[retrieval: ch9]` You need to expose a PostgreSQL database and a web application to clients outside the cluster. Which one can an Ingress handle, and what do you use for the other?

**2.** ⚪ One IP address serves `shop.example.com` and `blog.example.com`, routing each to a different Service. Name the Ingress capability. Then: one host, with `/catalog` and `/checkout` going to different Services. Name that one.

**3.** 🔵 A colleague applies a correct Ingress manifest to a fresh cluster. `kubectl get ingress` shows it. No traffic reaches the application. Name the most likely cause, and say what `kubectl get` actually proves.

**4.** 🔵 The same Ingress manifest is applied to two clusters, each running a different Ingress controller. Should you expect identical behaviour? Justify your answer.

**5.** 🔵 `[retrieval: ch3]` Chapter 3 gave you a one-sentence rule about objects and components. State it, then name the two things from Chapter 9 that were instances of it.

---

**Answers with Explanations:**

**1. The web application, over HTTP/HTTPS. The database needs `Service.Type=NodePort` or `Service.Type=LoadBalancer`.**

An Ingress exposes HTTP and HTTPS routes and nothing else; exposing services other than HTTP and HTTPS typically uses NodePort or LoadBalancer [source: k8s-docs-ingress-depth-2026-08-24]. PostgreSQL speaks its own wire protocol over TCP, so there is nothing for a layer-7 router to read.

The framing that matters here is **specialisation, not replacement.** Ingress does not sit *instead of* the Service-type ladder. It sits *above* it, for one class of traffic. The ladder is still the correct answer for everything else, which is why §4's news about the Ingress API being frozen is survivable rather than alarming: nothing you learned in Chapter 9 is going anywhere.

Why a wrong answer is wrong: "use an Ingress for both, with different ports" fails because an Ingress does not expose arbitrary ports at all [source: k8s-docs-ingress-depth-2026-08-24]. The port fields in an Ingress rule name the *backend Service's* port, not a port the Ingress listens on.

**2. Name-based virtual hosting; simple fanout.**

Name-based virtual hosting routes HTTP traffic to multiple host names at the same IP address [source: k8s-docs-ingress-depth-2026-08-24]. Simple fanout routes traffic from a single IP address to more than one Service based on the HTTP URI [source: k8s-docs-ingress-depth-2026-08-24]. Asked as a pair on purpose: the thing to retrieve is not either definition but the **discriminator**, host versus path. Both put many Services behind one address.

**3. No Ingress controller is installed. `kubectl get` proves only that the object exists.**

Only creating an Ingress resource has no effect; a controller must be present to satisfy it [source: k8s-docs-ingress-depth-2026-08-24]. `kubectl get ingress` returning your object tells you a record is in etcd and the API server will serve it back. It is a fact about storage. It is not a fact about routing, and nothing in that output is evidence that any component has ever looked at the object.

Nothing here is a mistake on your colleague's part. The manifest is correct, the expectation was reasonable, and the missing piece is invisible from the object. That is precisely what makes this pattern worth learning as a *first* question rather than a last resort.

**4. No.** Ideally all Ingress controllers should fit the reference specification; in reality, the various Ingress controllers operate slightly differently [source: k8s-docs-ingress-depth-2026-08-24].

This one is easy to skim past because it reads like a caveat. It is not a caveat. It is a fact about portability with real operational consequences, and it is the reason the documentation tells you to read your controller's own docs to understand the caveats of choosing it [source: k8s-docs-ingress-depth-2026-08-24].

**5. `[retrieval: ch3]` An object without its component does nothing.** The two Chapter 9 instances: a `type: LoadBalancer` Service on a cluster with no load balancer to provision one, and a Service whose selector matches no Pods.

If you can list the instances now, §8 will land as a count you already made rather than as an assertion the book handed you. That is the difference between remembering a rule and holding one.

---

**Checkpoint: You've Now Mastered**

✓ Where the Service-type ladder runs out, and the layer boundary that explains why
✓ What Ingress does, what it refuses to do, and the two shapes it takes
✓ Why a perfectly correct object can accomplish nothing
✓ The rule, with three of your own instances behind it

Two sections on the API you just learned, and then we go somewhere completely different.

---

## ⚪ §4 — Frozen, Not Deprecated

Chapter 9 told you this section was coming and told you it was worth exam-level attention. Everything here is definition, and precision is the only thing it has to deliver.

### The statement

The Kubernetes documentation carries a note directly beneath its description of Ingress. Here it is, in full:

> The Kubernetes project recommends using Gateway instead of Ingress. The Ingress API has been frozen.
>
> This means that:
>
> - The Ingress API is generally available, and is subject to the stability guarantees for generally available APIs. The Kubernetes project has no plans to remove Ingress from Kubernetes.
> - The Ingress API is no longer being developed, and will have no further changes or updates made to it.

[source: k8s-docs-ingress-depth-2026-08-24]

Two bullets. Both load-bearing. Nearly everyone drops one.

### The split

| The half readers drop | What it actually says | What it means for you |
|---|---|---|
| **Still GA, still guaranteed, no removal plans** | It is not going away, and it is not going to break under you | Your existing Ingress configurations are not a migration emergency |
| **No further development, no changes or updates** | Nothing new will ever be added | Anything Ingress cannot do today, it will never do |

Collapse the first bullet and you get *"Ingress is deprecated,"* which is wrong, and which will have you planning a migration you do not need. Collapse the second and you get *"Ingress is fine, ignore the note,"* which is also wrong, and which will have you designing new systems around an API that has stopped growing.

> ★ **Fixed Point:** **Frozen ≠ deprecated.** Ingress is generally available, subject to GA stability guarantees, with **no plans for removal** — **and** no longer developed, with **no further changes or updates** [source: k8s-docs-ingress-depth-2026-08-24]. Both halves, or you have the wrong fact.

### Why "deprecated" is a different word

The two words point in different directions, and the difference is about *what* is being announced.

**Deprecation is a statement about future removal.** Kubernetes has a formal, published deprecation policy, and it exists precisely so that removals are predictable: the policy governs the removal of API objects, fields, annotations, enumerated values and component config structures, and its stated purpose is to avoid breaking existing users when a feature must be removed [source: k8s-docs-deprecation-policy-2026-08-24]. Under it, GA API versions **may be marked as deprecated, but must not be removed within a major version of Kubernetes** [source: k8s-docs-deprecation-policy-2026-08-24]. Deprecation is the first step on a defined path toward an eventual exit.

**A freeze is a statement about future development.** It says the thing is finished. Nothing more will be added. It says nothing whatsoever about removal, and a frozen API can be permanent.

Kubernetes has said one of these about Ingress and not the other, and the choice was deliberate. When the Ingress note says the API is "subject to the stability guarantees for generally available APIs," it links directly to that deprecation policy: the guarantees are the same ones any GA API enjoys [source: k8s-docs-ingress-depth-2026-08-24].

> ⚠ **Navigational Hazards:** A question offering *"Ingress is deprecated and will be removed in a future release"* is testing exactly one thing: whether you kept both halves. So is a question offering *"Ingress is unaffected and fully supported for new development."* Neither is the answer. Candidates get this wrong in both directions, which is why an exam can build a clean four-option question out of it. The two most attractive distractors write themselves.

> 🪢 **Mnemonic:** *Frozen things keep. They just don't grow.*

### What "recommends" obliges

*Recommends* is not *requires*.

The project recommends Gateway for new work [source: k8s-docs-ingress-depth-2026-08-24]. It has not deprecated Ingress, has announced no removal, and continues to extend it the stability guarantees that GA APIs carry. A light has been hung on the new channel; the old one has not been closed. The honest practitioner reading is: **do not panic about what you are running, and think hard before building something new on an API that will never gain a feature again.**

That is the whole of it. The project said what it said, precisely, and the reasoning behind the decision is not this book's to supply.

*[cross-bearing: see Ch 8 §6 — semantic versioning and API stability, which is the vocabulary this section spends]*

The obvious next question is what "use Gateway instead" actually means. §5.

---

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

Now the resource model reads as a consequence rather than a list. Gateway API has four stable API kinds [source: k8s-docs-gateway-api-depth-2026-08-24]:

- **GatewayClass** — defines a set of gateways with common configuration, managed by a controller that implements the class [source: k8s-docs-gateway-api-depth-2026-08-24].
- **Gateway** — defines an instance of traffic-handling infrastructure, such as a cloud load balancer [source: k8s-docs-gateway-api-depth-2026-08-24].
- **HTTPRoute** — defines HTTP-specific rules for mapping traffic from a Gateway listener to a representation of backend network endpoints, which are often represented as a Service [source: k8s-docs-gateway-api-depth-2026-08-24].
- **GRPCRoute** — the same, for gRPC-specific rules [source: k8s-docs-gateway-api-depth-2026-08-24].

<!-- AUTHOR-REVIEW: source drift. The 2026-08-23 snapshot of this page names three resource kinds (GatewayClass, Gateway, HTTPRoute); the 2026-08-24 depth re-fetch names four stable kinds, adding GRPCRoute. The research manifest flags this as affecting a Fixed Point and a Bearings item. Drafted against the newer snapshot, with the three role-mapped kinds emphasised and GRPCRoute named but not developed, since it maps to the same role as HTTPRoute and the outline explicitly excludes it from teaching scope. Revision stage should confirm which count the exam is calibrated against — a question asking "how many stable kinds" would be answered differently by the two snapshots. -->

**The cardinality is examinable, so state it as such.** A Gateway object is associated with **exactly one** GatewayClass, and the GatewayClass describes the gateway controller responsible for managing Gateways of that class. One or more route kinds are then associated to Gateways: **many** Routes may attach to a Gateway. A Gateway can filter the routes that may attach to its `listeners`, forming a bidirectional trust model with routes [source: k8s-docs-gateway-api-depth-2026-08-24].

> ★ **Fixed Point:** **GatewayClass, Gateway, HTTPRoute** — and the role each belongs to. A Gateway is associated with **exactly one** GatewayClass; **many** Routes may attach to one Gateway [source: k8s-docs-gateway-api-depth-2026-08-24].

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

> ⚓ **Worth Securing:** The role split *is* the innovation. Ingress put infrastructure choice, cluster policy, and application routing into one object that one team had to own, which is a large part of why so much real-world Ingress configuration ends up living in controller-specific annotations. The documentation says so almost in passing: Gateway API kinds support common cases such as header-based matching and traffic weighting "that were only possible in Ingress by using custom annotations" [source: k8s-docs-gateway-api-depth-2026-08-24].

### The request flow

Concrete, end to end, for a Gateway implemented as a reverse proxy [source: k8s-docs-gateway-api-depth-2026-08-24]:

1. The client starts to prepare an HTTP request for `http://www.example.com`.
2. The client's DNS resolver queries for the destination name and learns a mapping to one or more IP addresses associated with the Gateway.
3. The client sends a request to the Gateway IP address; the reverse proxy receives the HTTP request and uses the **`Host:` header** to match a configuration derived from the Gateway and attached HTTPRoute.
4. Optionally, the reverse proxy performs request header and/or path matching based on the HTTPRoute's match rules.
5. Optionally, the reverse proxy modifies the request — adding or removing headers, say — based on the HTTPRoute's filter rules.
6. Lastly, the reverse proxy forwards the request to one or more backends.

Step 2 and step 3 are the §2 distinction, drawn in the specification's own hand. DNS does its work and finishes; the `Host` header does its work afterward, on a connection that has already arrived.

And step 3 is Soundings question 1's answer, seven sections later. You worked out that a server distinguishing two hostnames on one address has to read the `Host` header, from ordinary web experience, before this chapter started. Here is the same mechanism in a Kubernetes specification, doing the same job under a different name. That is usually how this material goes: the priors were right, the vocabulary is new.

### The other design principles

Three more, briefly [source: k8s-docs-gateway-api-depth-2026-08-24]:

- **Portable** — Gateway API specifications are defined as custom resources and are supported by many implementations.
- **Expressive** — the kinds support common traffic routing cases such as header-based matching and traffic weighting, which in Ingress were only possible through custom annotations. That is the concrete answer to what §4's freeze costs you.
- **Extensible** — custom resources can be linked at various layers of the API, making granular customization possible at the appropriate places within the structure.

### Is it there?

Having just been told to prefer Gateway, the obvious next question is whether it is in your cluster. It is not.

**Instead of Gateway API resources being natively implemented by Kubernetes, the specifications are defined as Custom Resources supported by a wide range of implementations.** You install the Gateway API CRDs, or follow the installation instructions of your selected implementation [source: k8s-docs-gateway-api-depth-2026-08-24]. The docs describe Gateway API as "an add-on containing API kinds" [source: k8s-docs-gateway-api-depth-2026-08-24], and the cluster addon list carries it among the networking entries [source: k8s-docs-cluster-addons-2026-08-24].

> 🔭 **Closer Look:** The API that supersedes Ingress is not built into the API server the way Ingress is. It arrives as custom resources *[cross-bearing: see Ch 6 §8 — custom resources and CustomResourceDefinitions]*. That is deeper than the exam requires, and it is a rather good demonstration of Chapter 6's claim that the extension mechanism is powerful enough to build first-class-looking APIs on top of. The successor to a built-in API is, structurally, an extension.

*[cross-bearing: see Ch 9 §6 — the client's resolver, which appears here as one step in a flow rather than as a topic]*
*[cross-bearing: see Ch 17 §4 — CRDs as one of the four pluggable interfaces, of which this is a conspicuous instance]*

---

## ☆ Taking Your Bearings #2

Five questions on §4 and §5 — one API frozen, one API recommended, and the difference that word makes.

**1.** ⚪ State both halves of what the Kubernetes project has said about the Ingress API.

**2.** ⚪ True or false, with justification: *Ingress is deprecated and will be removed in a future release.*

**3.** 🟡 Name the three role-mapped Gateway API resources and say which organisational role each belongs to.

**4.** 🟡 How many GatewayClasses is a Gateway associated with, and how many Routes can attach to one Gateway?

**5.** 🟡 A request arrives at a Gateway's IP address. Name the header the reverse proxy uses to match a configuration, and name the two optional things the HTTPRoute may do before the request is forwarded.

---

**Answers with Explanations:**

**1. It is frozen: generally available and subject to the stability guarantees for GA APIs, with no plans for removal — *and* no longer being developed, with no further changes or updates** [source: k8s-docs-ingress-depth-2026-08-24].

An answer carrying only one half is wrong, because one half is precisely the error being tested.

And it is worth saying *why* both halves matter rather than just repeating them. The stability half means there is **no migration emergency**: what you are running keeps working, keeps being supported, and is not scheduled for removal. The no-development half means there is **no future capability**: whatever gap you find in Ingress today is permanent. Those two facts drive different decisions, one about existing systems, one about new ones, and that is exactly why the project stated both.

**2. False, on both counts.** Ingress has not been deprecated, and there are no plans to remove it [source: k8s-docs-ingress-depth-2026-08-24]. What has been said is that it will not be developed further, and that the project recommends Gateway for new work.

Distractor logic: this option is attractive because "no longer developed" *feels* like deprecation. In Kubernetes, deprecation is a formally defined process with published rules about removal timelines [source: k8s-docs-deprecation-policy-2026-08-24], and the project did not invoke it here.

**3. GatewayClass — infrastructure provider. Gateway — cluster operator. HTTPRoute — application developer** [source: k8s-docs-gateway-api-depth-2026-08-24].

Asked as a mapping rather than a list because the mapping *is* the design. If you can produce the three names but not the three roles, you have memorised the consequence and missed the cause.

One point of precision the answer key must make: **"cluster operator" is a role — a team or a person who runs the cluster — not the operator pattern from Chapter 6.** The word does double duty in Kubernetes vocabulary, and this is the one place in this book where both senses are in play.

**4. Exactly one GatewayClass. Many Routes** [source: k8s-docs-gateway-api-depth-2026-08-24].

Pure recall, and exactly the kind of cardinality detail multiple-choice exams reach for, because it is unambiguous and either known or not.

**5. The `Host:` header. Then, optionally: header and/or path matching based on the HTTPRoute's match rules, and optional modification of the request based on its filter rules** [source: k8s-docs-gateway-api-depth-2026-08-24].

This closes Soundings question 1. You named the `Host` header at the start of this chapter, from ordinary web experience and before reading a word of Kubernetes networking. The specification agrees with you. Notice that: a fair amount of this material is your existing knowledge wearing new vocabulary, and recognising which parts are genuinely new is how you spend study time well.

---

**Checkpoint: You've Now Mastered**

✓ `Frozen` and `deprecated`, precisely, in both halves
✓ Gateway API's role-oriented design, and the resources that fall out of it
✓ The cardinality, and the request flow end to end

That closes the API arc. What follows shares a chapter with it and shares nothing else: different layer, different direction, different problem. Take the break here if you are taking one.

---

## 🔵 §6 — Allowing, Never Denying

One piece of housekeeping before we get under way, and it is not politeness.

**The word `ingress` is about to mean something completely different, and capitalisation is the tell.** For four sections, `Ingress` has meant an API object and the controller that fulfils it. From here to the end of §7, lowercase `ingress` means **a direction of traffic**: inbound, as opposed to `egress`, outbound. NetworkPolicy has nothing to do with the Ingress object. If you carry the old meaning into this section, you will spend §7 trying to work out how the Ingress controller fits in, and it does not.

Good. Now the object.

### What a NetworkPolicy controls

**NetworkPolicies let you specify rules for traffic flow at the IP address or port level — OSI layer 3 or 4 — within your cluster, and also between Pods and the outside world** [source: k8s-docs-network-policies-depth-2026-08-24]. They are an **application-centric construct**, which lets you specify how a Pod is allowed to communicate with various network *entities* — a word the documentation chose deliberately to avoid overloading "endpoints" and "services," which already have specific Kubernetes meanings [source: k8s-docs-network-policies-depth-2026-08-24]. And they **apply to a connection with a Pod on one or both ends, and are not relevant to other connections** [source: k8s-docs-network-policies-depth-2026-08-24].

Note what that rules out. This is **network reachability**: who may open a connection to whom, at layer 3 or 4, and nothing else. It is not the boundary between a workload and the host it runs on. Chapter 2 already told you those were different axes, and it told you on a graded question *[cross-bearing: see Ch 2 §7 — RuntimeClass, and workload-to-host isolation as a separate concern]*. The other axis of Pod security has its own chapter *[cross-bearing: see Ch 12 §5 — what a Pod may do to its node]*.

And note the layer. §1 spent five sections climbing to layer 7 to read hostnames and paths. This section is back down at 3 and 4, reading addresses and ports. Different problem, different altitude.

### Three identifiers, and two selectors doing different jobs

The entities a Pod can communicate with are identified through a combination of three identifiers [source: k8s-docs-network-policies-depth-2026-08-24]:

1. **Other Pods** that are allowed — with the exception that a Pod cannot block access to itself.
2. **Namespaces** that are allowed.
3. **IP blocks** — with the exception that traffic to and from the node where a Pod is running is always allowed, regardless of the IP address of the Pod or the node.

For Pod- and namespace-based policies, **you use a selector to specify what traffic is allowed to and from the Pods that match the selector.** For IP-based policies, you define the rule on **IP blocks (CIDR ranges)** [source: k8s-docs-network-policies-depth-2026-08-24]. *(CIDR notation is a way of writing a range of IP addresses as an address plus a prefix length: `172.17.0.0/16` means "the addresses whose first sixteen bits are those of 172.17.0.0." The glossary carries the expansion.)*

Chapter 4 saw this coming. It told you, six chapters ago, that **a NetworkPolicy selects both its subject and its peers** *[cross-bearing: see Ch 4 §5 — labels and selectors as the universal join]*. Pause on that, because it is the structurally most interesting thing in this section. Here is the shape:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:              # <-- chooses the SUBJECT: who this policy governs
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
    - namespaceSelector:    # <-- chooses PEERS: who may connect
        matchLabels:
          project: myproject
    - podSelector:          # <-- also chooses PEERS
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
```

[source: k8s-docs-network-policies-depth-2026-08-24]

**Each NetworkPolicy includes a `podSelector` which selects the grouping of Pods to which the policy applies** — here, Pods labelled `role: db` [source: k8s-docs-network-policies-depth-2026-08-24]. That is the subject. Inside the rules, a different set of selectors chooses who may connect: `podSelector` selects particular Pods in the **same namespace as the NetworkPolicy** as allowed sources or destinations, and `namespaceSelector` selects particular namespaces for which **all** Pods are allowed [source: k8s-docs-network-policies-depth-2026-08-24].

One mechanism, the label selector you learned in Chapter 4, doing two entirely different jobs in one object, at two different depths of the same YAML.

> 🪝 **Snag:** Whether `namespaceSelector` and `podSelector` appear as one `from` entry or two changes the meaning completely. A single entry specifying **both** selects particular Pods *within* particular namespaces, an AND. Two entries in the `from` array is an OR: connections from Pods in the local namespace with the peer label, **or** from any Pod at all in the matching namespaces [source: k8s-docs-network-policies-depth-2026-08-24]. One YAML hyphen is the difference. The documentation's own advice: when in doubt, use `kubectl describe` to see how Kubernetes has interpreted the policy [source: k8s-docs-network-policies-depth-2026-08-24].

### The two sorts of isolation

This is the centre of the section, and the place your firewall instinct gets corrected.

There are **two sorts of isolation for a Pod: isolation for egress, and isolation for ingress.** They concern what connections may be established. "Isolation" here is **not absolute** — it means *some restrictions apply*. The alternative, "non-isolated for a direction," means that **no restrictions apply** in that direction. The two are declared independently, and both are relevant for a connection from one Pod to another [source: k8s-docs-network-policies-depth-2026-08-24].

**Egress.** By default, a Pod is **non-isolated for egress; all outbound connections are allowed.** A Pod becomes isolated for egress if there is **any** NetworkPolicy that both **selects the Pod** and has `Egress` in its `policyTypes`. When it is isolated, the only allowed outbound connections are those permitted by the `egress` list of some policy that applies to it [source: k8s-docs-network-policies-depth-2026-08-24].

**Ingress.** By default, a Pod is **non-isolated for ingress; all inbound connections are allowed.** It becomes isolated for ingress on exactly the same terms, with `Ingress` in `policyTypes`. When it is isolated, the only allowed inbound connections are **those from the Pod's node** and those permitted by the `ingress` list of some applicable policy [source: k8s-docs-network-policies-depth-2026-08-24].

Reply traffic for allowed connections is implicitly allowed in both directions [source: k8s-docs-network-policies-depth-2026-08-24], which is to say the mechanism is connection-aware, not packet-by-packet, and you do not need a return rule.

Now collect the debt from Soundings question 4. You almost certainly answered *dropped* and *the deny wins*, because that is how ordinary firewalls work and it is a good instinct nearly everywhere else. Kubernetes is the other way around on both counts. **A Pod starts fully open in both directions, and becomes restricted only because some policy went looking for it and found it.** Nothing is closed until something selects it.

> ★ **Fixed Point:** **By default a Pod is non-isolated in both directions.** It becomes isolated for a direction only when some NetworkPolicy both **selects it** and names that direction in `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24]. No policy means no restriction.

A note on `policyTypes`, because it has a default that catches people. Each policy includes a `policyTypes` list which may include `Ingress`, `Egress`, or both. **If no `policyTypes` are specified, `Ingress` will always be set, and `Egress` will be set if the policy has any egress rules** [source: k8s-docs-network-policies-depth-2026-08-24]. So an omitted `policyTypes` is not "neither." It is at minimum `Ingress`.

### Additive, and there is no deny

**The effects of the ingress lists combine additively. The effects of the egress lists combine additively. Network policies do not conflict; they are additive.** If any policy or policies apply to a given Pod for a given direction, the connections allowed in that direction are **the union of what the applicable policies allow.** Thus **order of evaluation does not affect the policy result** [source: k8s-docs-network-policies-depth-2026-08-24].

Sit with that for a moment, because it removes something you have relied on everywhere else.

There is **no deny rule.** None. The API has no syntax for one. Two policies selecting the same Pod produce the union of what they permit, and there is no third policy you can write that subtracts from that union. If a Pod can currently reach something and you want it not to, you do not add a denial. **You remove the grant.**

> ★ **Fixed Point:** **Policies are additive and never conflict. There is no deny rule** [source: k8s-docs-network-policies-depth-2026-08-24]. Two policies produce the union of what they permit. Removing access means removing the grant, not adding a denial.

<!-- FIGURE: ch10-fig04-networkpolicy-additive-selectors -->
```
   POLICY A                                          PERMITTED SET
   podSelector: role=db  ─────┐                    ╭───────────────╮
   ingress from: app=web      │                    │               │
                              ▼                    │   app=web     │
                        ┌───────────┐              │      +        │
                        │  Pod      │─────────────▶│   app=batch   │
                        │  role=db  │              │               │
                        └───────────┘              │  (one set,    │
                              ▲                    │   two grants) │
   POLICY B                   │                    ╰───────────────╯
   podSelector: role=db  ─────┘
   ingress from: app=batch
                                                     ┌───────────┐
   ═══▶  podSelector (chooses the SUBJECT)            │ app=other │
   ───▶  peer selector (chooses WHO MAY CONNECT)      └───────────┘
                                                       no arrow.
                                                       not denied —
                                                       simply never
                                                       granted.
```

Note what is *not* in that figure: any mark of denial. No barrier, no crossed-out arrow, no red X. The excluded Pod is excluded by the **absence of a grant**, which is a different thing from being blocked, and drawing it as blocking would contradict the Fixed Point above.

### Both ends must allow it

**For a connection from a source Pod to a destination Pod to be allowed, both the egress policy on the source Pod and the ingress policy on the destination Pod need to allow the connection. If either side does not allow the connection, it will not happen** [source: k8s-docs-network-policies-depth-2026-08-24].

This is the rule that costs practitioners the most time, because a policy that is perfectly correct in isolation is only ever half of a working configuration. You write an egress policy on `frontend` permitting traffic to `api`, you verify the YAML, you apply it, and nothing connects, because `api` has an ingress policy that never heard of `frontend`.

> ★ **Fixed Point:** **Both ends must allow it.** The source Pod's egress policy *and* the destination Pod's ingress policy [source: k8s-docs-network-policies-depth-2026-08-24].

> ⚠ **Navigational Hazards:** If your firewall instinct says *"unlisted traffic is dropped"* and *"the more restrictive rule wins,"* both instincts are wrong here. And they are wrong in the direction that makes a cluster **more open than you expect**, not less. Candidates get both of these wrong, reliably, and they get them wrong *confidently*, which is worse. The default is open. Nothing denies. The union permits.

> 🪢 **Mnemonic:** *Nothing is closed until something selects it; nothing selected can be re-closed by another rule; and both ends have to agree.*

### Getting default-deny with no deny rule

The obvious objection: if there is no deny rule, how does anyone ever lock anything down?

Follow the two facts you already have. A Pod becomes isolated for a direction when a policy selects it and names that direction. Once isolated, the only permitted connections are the ones some policy's list allows. So: **select the Pods, name the direction, and permit nothing.** Isolation without permission *is* denial, arrived at by construction rather than by a deny keyword.

The mechanism for "select every Pod in the namespace" is an **empty `podSelector`**, which **selects all Pods in the namespace** [source: k8s-docs-network-policies-depth-2026-08-24]:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

No `ingress` list. No `egress` list. Every Pod in the namespace selected, both directions named, nothing permitted. **This ensures that even Pods without any other NetworkPolicy selected will not be allowed any ingress or egress traffic** [source: k8s-docs-network-policies-depth-2026-08-24]. The same shape with only `Ingress` in `policyTypes` gives you default-deny inbound and leaves outbound alone [source: k8s-docs-network-policies-depth-2026-08-24].

And because the model is additive, the reverse also works: an explicit allow-all is a policy with `podSelector: {}` and a single empty rule, `ingress: [- {}]`, which permits everything to everything even if other policies have caused some Pods to be treated as isolated [source: k8s-docs-network-policies-depth-2026-08-24]. Union semantics cut both ways: you cannot subtract, and neither can anybody else.

The documentation puts the whole model in one sentence worth memorising: **a Pod will accept all traffic by default; however, once a NetworkPolicy is created for a Pod, the Pod will reject any traffic that is not allowed by any NetworkPolicy — and other Pods in the namespace that are not selected by any NetworkPolicy will continue to accept all traffic** [source: k8s-docs-network-policies-depth-2026-08-24].

### The two exceptions

Both were in the three-identifiers list above, and both are unconditional:

- **A Pod cannot block access to itself** [source: k8s-docs-network-policies-depth-2026-08-24].
- **Traffic to and from the node where a Pod is running is always allowed, regardless of the IP address of the Pod or the node** [source: k8s-docs-network-policies-depth-2026-08-24].

The second one is why the ingress isolation rule says the allowed inbound connections are "those from the Pod's node **and** those allowed by the ingress list": node-local traffic is not something a policy grants, it is something no policy can take away.

> 🪝 **Snag:** These two exceptions get rediscovered regularly by someone testing a policy from the wrong place. `kubectl exec` into the Pod and curl itself: allowed, always, and it proves nothing. Test from the node: allowed, always, and it proves nothing either. If you want to know whether a restriction works, the traffic has to originate somewhere the policy could actually govern.

*[cross-bearing: see Ch 9 §1 — the network model's second rule, and the "barring intentional network segmentation" hedge that pointed here]*
*[cross-bearing: see Ch 4 §3 — namespaces, which are the second of the three identifiers]*
*[cross-bearing: see Ch 5 §1 — the Pod IP, which is ultimately what a policy is about]*
*[cross-bearing: see Ch 12 §9 — RBAC and NetworkPolicy as one shared semantic]*

---

## 🟡 §7 — What NetworkPolicy Cannot Do

Two facts. This section teaches two facts and nothing else, and the first one is the highest-consequence sentence in the chapter.

### The prerequisite

**Network policies are implemented by the network plugin. To use network policies, you must be using a networking solution which supports NetworkPolicy. Creating a NetworkPolicy resource without a controller that implements it will have no effect** [source: k8s-docs-network-policies-depth-2026-08-24].

Read that last clause against §3's. *Only creating an Ingress resource has no effect.* *Creating a NetworkPolicy resource without a controller that implements it will have no effect.* The same sentence, twice, four sections apart, about two objects with nothing else in common.

> ★ **Fixed Point:** **NetworkPolicies are implemented by the network plugin.** On a plugin that does not implement NetworkPolicy, the resource has no effect [source: k8s-docs-network-policies-depth-2026-08-24].

### Why this one is worse

Here is the asymmetry, and it is the reason §7 exists as its own section.

When an Ingress does nothing, **requests fail.** The site is down, somebody's monitoring fires, a user complains, and within minutes someone is looking at it. The failure announces itself.

When a NetworkPolicy does nothing, **traffic flows exactly as it did before.** `kubectl get networkpolicy` shows the object. `kubectl describe` shows the rules, correctly parsed and neatly formatted. Everything you can observe about the object says it is fine, and the observable behaviour of an unenforced policy is *identical* to the observable behaviour of a perfectly enforced policy against traffic nobody happens to be sending. There is no signal. There is nothing to notice. One failure fires a flare; the other is an uncharted rock, and nothing on the surface says it is there.

That is not a documented claim; the source states the plugin dependency and the no-effect consequence and stops there. The characterisation of the failure as *silent*, and as harder to detect than a broken Ingress, is this book's reasoning about what those two documented facts imply. Hold the two apart: the dependency is sourced, the inference about detectability is ours. We think it is sound, it is the most valuable thing in this chapter, and it is still an inference.

> ⚠ **Navigational Hazards:** *"I applied a NetworkPolicy, so that traffic is blocked"* is only true if something is enforcing it. Verify that your network plugin supports NetworkPolicy before you rely on one, and test the restriction from somewhere the policy could actually govern rather than trusting the object's existence. The object existing is a fact about etcd.

Nothing about this is careless. You wrote a correct policy, the API accepted it, `kubectl` showed it back to you, and every signal available said the thing was working. The expectation is entirely reasonable. It is the *mechanism* that offers no feedback, and that is worth knowing about in advance precisely because you will not discover it in the moment.

### Where else could it possibly live?

You can reason your way to this dependency rather than memorising it.

Chapter 9 taught that Kubernetes **defines** the network model and implements none of it: a CNI plugin does the actual work of wiring Pods onto a network *[cross-bearing: see Ch 9 §1 — CNI and the Kubernetes network model]*. CNI is one of the interfaces where Kubernetes hands off to an implementation: network plugins are binary plugins the kubelet executes, and CNI is the interface used to implement pod networking [source: k8s-docs-extending-kubernetes-2026-08-23].

So if the plugin is what moves the packets, **where else could enforcement possibly live?** Nowhere. The dependency is not an oversight or an inconvenience. It is the only place in the stack where the machinery to enforce a layer-3/4 rule exists.

If you reasoned to something like this in Soundings question 7, you derived §7's central fact before the chapter told you. Notice that.

### What it cannot do, stated flat

> **Dead Reckoning:** As of the current release, the following functionality does not exist in the NetworkPolicy API [source: k8s-docs-network-policies-depth-2026-08-24]:
>
> - Forcing internal cluster traffic to go through a common gateway.
> - Anything TLS related.
> - Node specific policies. You can use CIDR notation, but you cannot target nodes by their Kubernetes identities specifically.
> - Targeting of services by name. You can target Pods or namespaces by their labels, which is often a viable workaround.
> - Creation or management of "Policy requests" that are fulfilled by a third party.
> - Default policies which are applied to all namespaces or Pods.
> - Advanced policy querying and reachability tooling.
> - The ability to log network security events, for example connections that are blocked or accepted.
> - The ability to explicitly deny policies. The model for NetworkPolicies is deny by default, with only the ability to add allow rules.
> - The ability to prevent loopback or incoming host traffic. Pods cannot block localhost access, nor can they block access from their resident node.
>
> The documentation notes that some of these may be achievable through operating-system components such as SELinux, OpenVSwitch or IPTables, through layer-7 technologies such as ingress controllers and service mesh implementations, or through admission controllers [source: k8s-docs-network-policies-depth-2026-08-24].

Ten items. Three of them earn a sentence each, because they are the ones you will actually reach for.

**No TLS.** Anything TLS related is out of scope, and the documentation says outright to use a service mesh or ingress controller for it [source: k8s-docs-network-policies-depth-2026-08-24]. §2 already told you that terminating TLS at the Ingress leaves the leg from Ingress to Pod in cleartext. NetworkPolicy will not encrypt it either. That gap has an owner *[cross-bearing: see Ch 17 §5 — service mesh, mTLS, and what a mesh adds inside the cluster]*.

**No targeting Services by name.** Policies select Pods. You can target Pods or namespaces by label, which the documentation calls a viable workaround [source: k8s-docs-network-policies-depth-2026-08-24], but you cannot write `allow traffic to the checkout Service`. This is surprising after nine chapters in which nearly everything has been Service-shaped, and it is the item on this list a reader is most likely to reach for by reflex.

**No explicit deny.** §6 taught additivity as a *property*; the out-of-scope list states the same fact as a *limitation*, in the documentation's own words: the model is deny by default with only the ability to add allow rules [source: k8s-docs-network-policies-depth-2026-08-24]. Same fact, met from the side you will actually encounter it on. You go looking for a deny rule, and there is not one.

> 🔭 **Closer Look:** "No targeting of services by name" is stranger than it looks, and it follows directly from §6. A policy selects Pods. A Service is a stable name in front of a set of Pods that *changes*; that is the entire reason Chapter 9 gave you Services. Selecting the Service would mean selecting a moving target through an indirection that the policy layer, sitting at layer 3/4 on Pod IPs, does not have access to. The restriction is a consequence of the architecture, not an omission from the API. Deeper than the exam requires.

<!-- AUTHOR-REVIEW: the out-of-scope list is stated by the source as applying "as of Kubernetes {{< skew currentVersion >}}" — a version-templated claim. The Dead Reckoning block above renders this as "as of the current release," which is faithful but leaves the reader without a version anchor. Revision stage may want to pin a concrete version, or add a decay note. -->

Two objects. Four sections apart. Nothing in common except a failure mode.

---

## ☆ Taking Your Bearings #3

Five questions on §6 and §7 — what is permitted, how permissions add up, and what the mechanism cannot reach.

**1.** 🔵 `[retrieval: ch4]` Chapter 4 said a NetworkPolicy selects both its subject and its peers. Point at the two selectors in that sentence and say what each one is choosing.

**2.** 🔵 A Pod in namespace `prod` has no NetworkPolicy selecting it anywhere in the cluster. What inbound and outbound traffic is permitted?

**3.** 🟡 **⚠️ This one is intentionally hard. Struggle is the point.** Two NetworkPolicies select the same Pod. Policy A permits inbound traffic from `app: web`. Policy B permits inbound traffic from `app: batch`. What is permitted — and could a third policy be written to forbid `app: web`?

**4.** 🟡 Pod `frontend` has an egress policy permitting traffic to `app: api`. Pod `api` has an ingress policy permitting traffic only from `app: admin`. Can `frontend` reach `api`?

**5.** 🔵 You apply a NetworkPolicy intended to block traffic from a specific Pod. Traffic still flows. Name two distinct explanations, one of which is not a mistake in the policy.

---

**Answers with Explanations:**

**1. `[retrieval: ch4]` The policy's own top-level `podSelector` chooses which Pods the policy applies to. The selectors inside its rules — `podSelector` and `namespaceSelector` under `from`/`to` — choose which Pods and namespaces those Pods may talk to.**

Each NetworkPolicy includes a `podSelector` which selects the grouping of Pods to which the policy applies [source: k8s-docs-network-policies-depth-2026-08-24]; separately, the selectors in an `ingress from` or `egress to` section select Pods and namespaces as allowed sources or destinations [source: k8s-docs-network-policies-depth-2026-08-24].

Six chapters ago, learning about labels, you were told this object would use one mechanism for two jobs. This is the structural insight §6 is built on, and you should be able to point at both selectors in a manifest without hesitating.

**2. All of both — the Pod is non-isolated for ingress and for egress.**

By default a Pod is non-isolated in both directions, and becomes isolated only when some policy both selects it and names that direction in `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24].

Wrong answer to reject explicitly: *"no policy means no traffic."* That is the firewall instinct, and it is exactly backwards. It is also the single most consequential wrong belief a reader can bring to this material, because someone holding it will look at a cluster with no NetworkPolicies and conclude it is locked down.

**3. Inbound from both `app: web` and `app: batch` — the lists combine additively. And no: there is no deny rule, so nothing can subtract a permission. Removing that access means removing the grant.**

Network policies do not conflict; they are additive, and the connections allowed in a direction are the union of what the applicable policies allow [source: k8s-docs-network-policies-depth-2026-08-24]. The ability to explicitly deny is on the published out-of-scope list [source: k8s-docs-network-policies-depth-2026-08-24].

**If you spent a while looking for the deny rule before accepting there isn't one, that is the correct experience of this question.** Every firewall you have configured had one. The absence is genuinely strange, and it is worth stating as a *semantic* rather than a NetworkPolicy quirk: **the model has no subtraction operator.** Permissions compose by union and only by union, order of evaluation is irrelevant, and the only way to reduce what is permitted is to change what grants it.

Hold on to that phrasing. Chapter 12 retrieves this exact semantic by name and builds an argument on it *[cross-bearing: see Ch 12 §9 — additive, never deny]*.

**4. No.** For a connection from a source Pod to a destination Pod to be allowed, both the egress policy on the source and the ingress policy on the destination must allow it; if either side does not, the connection will not happen [source: k8s-docs-network-policies-depth-2026-08-24].

`frontend`'s egress policy is correct and permits exactly what it should. It is also irrelevant on its own, because `api` never granted `frontend` anything. Two objects, both individually sensible, and the connection still fails, which is why this rule costs practitioners so much time.

**5. Either: the network plugin does not implement NetworkPolicy, so the resource has no effect at all; or the traffic falls under one of the unconditional exceptions — a Pod cannot block access to itself, and traffic to and from its own node is always allowed** [source: k8s-docs-network-policies-depth-2026-08-24].

The question deliberately requires you to entertain that **the object may be perfect and still inert.** That is a move most troubleshooting instincts do not make; the reflex is to re-read the YAML, and the YAML is fine.

Say the detection problem out loud, because it is the part worth carrying: **a policy that is not enforced looks exactly like a policy that is enforced against traffic nobody is sending.** There is no observable difference. That is a property of the mechanism, not of anyone's attention.

---

**Checkpoint: You've Now Mastered**

✓ Non-isolated by default, in both directions, until something selects
✓ Additive, allow-only, no deny rule, order-independent
✓ Both ends must allow it
✓ The plugin dependency, and the ten things the API cannot do

One section left, and it is about something you already noticed.

---

## ☀️ §8 — Nothing Happens Without a Controller

This chapter taught two objects that have nothing to do with each other.

One routes HTTP by hostname and path at the edge of the cluster, at layer 7, for traffic coming in from outside. The other permits and forbids TCP connections between Pods inside it, at layers 3 and 4, for traffic that never leaves. Different layers. Different directions. Different problems. In most organisations, different teams.

And they fail the same way.

Write either one perfectly. Apply it successfully. Watch `kubectl get` return it. And nothing happens, because in one case no Ingress controller is installed, and in the other the network plugin does not implement NetworkPolicy.

> ☀️ **Zenith:**
>
> You have now seen this four times, and two of the four were your own from last chapter.
>
> A `type: LoadBalancer` Service with no provider to fulfil it. A Service whose selector matched no Pods. An Ingress with no controller. A NetworkPolicy on a plugin that does not implement one.
>
> Chapter 3 gave you the sentence — *an object without its component does nothing* — and told you that you would meet it four more times. This is where that debt comes due in full.
>
> But the rule is not a fact about Ingress, and it is not a fact about NetworkPolicy. It is a fact about **what a Kubernetes object is**, which you have held since Chapter 4 without necessarily seeing where it led.
>
> An object is a record of intent. Intent does not act.
>
> Something has to be watching, and willing, and *present*. Every object in this book works this way: the Deployment that produced Pods, the Service that produced a stable name, the Job that ran to completion. In all of those cases the watcher happened to be there, so the object appeared to do the work itself. These four are simply the cases where the watcher is missing, and the appearance falls away.

A chart drawn perfectly is still a chart. Somebody has to stand the watch.

You did not need the book to tell you this, incidentally. Soundings question 6 asked you to write down Chapter 3's rule and name a place you had met it, and if you answered that question you had already assembled most of the argument. The four instances are yours; the sentence was handed to you seven chapters ago.

*[cross-bearing: see Ch 3 §6 — the control loop, which is *why* this is true rather than merely *that* it is]*
*[cross-bearing: see Ch 4 §1 — the declarative model, and the object as an artifact of intent]*

> ⚓ **Worth Securing:** You now own a question you can ask about anything: **what is watching this, and is it installed?**
>
> Chapter 13 will hand you a cluster where `kubectl top` returns an error, and the answer is metrics-server *[cross-bearing: see Ch 13 §7 — the resource metrics pipeline]*. Chapter 17 will hand you VPA, which is an addon and is not shipped by default *[cross-bearing: see Ch 17 §7 — the autoscaling landscape]*. Chapter 3 published both of those pointers before you had any of the evidence. You have the evidence now.
>
> It also works on objects this book never mentions, which is the actual return on this chapter.

<!-- FIGURE: ch10-zenith-nothing-without-a-controller -->
```
  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
  │   Service   │  │   Service   │  │   Ingress   │  │NetworkPolicy│
  │type:LoadBal.│  │selector: {} │  │  host+path  │  │ podSelector │
  │   ✓ valid   │  │   ✓ valid   │  │   ✓ valid   │  │   ✓ valid   │
  ├─────────────┤  ├─────────────┤  ├─────────────┤  ├─────────────┤
  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│  │┌ ─ ─ ─ ─ ─ ┐│
  │  provider   │  │matching Pods│  │ Ingress     │  │  network    │
  │   ( none )  │  │   ( none )  │  │ controller  │  │  plugin     │
  │└ ─ ─ ─ ─ ─ ┘│  │└ ─ ─ ─ ─ ─ ┘│  │  ( none )   │  │  ( none )   │
  │             │  │             │  │└ ─ ─ ─ ─ ─ ┘│  │└ ─ ─ ─ ─ ─ ┘│
  ├─────────────┤  ├─────────────┤  ├─────────────┤  ├─────────────┤
  │   nothing   │  │   nothing   │  │   nothing   │  │   nothing   │
  │             │  │             │  │             │  │ …and nothing│
  │             │  │             │  │             │  │  tells you  │
  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘

           An object without its component does nothing.
```

Look at the fourth panel one more time. Three of these announce themselves. One does not.

---

🏆 **Safe Harbor** — Chapter 10 complete. You crossed the boundary from moving packets to reading requests, met the API that does it and the one that supersedes it, went back down two layers to restrict traffic inside the cluster, and collected a rule that will outlast every object in this chapter.

🗺️ → 🌊 → 🌅 — *Part III: passage. Two chapters of the network behind you.*

---

## Exam Alert! 🚨

**High-Priority Topics**

1. **Ingress exposes HTTP and HTTPS only.** No arbitrary ports, no other protocols; anything else uses NodePort or LoadBalancer.
2. **You must have an Ingress controller.** Creating an Ingress resource alone has no effect.
3. **Frozen, not deprecated** — GA, stability guarantees, no removal plans, **and** no further development. Both halves or nothing.
4. **The project recommends Gateway for new work.**
5. **Simple fanout routes by URI; name-based virtual hosting routes by host.** Both put many Services behind one address.
6. **An Ingress may terminate TLS**, using a Secret that contains a private key and certificate; traffic onward to the Pods is cleartext.
7. **A Pod is non-isolated in both directions by default.** All ingress and all egress allowed.
8. **Policies are additive and never conflict. There is no deny rule.**
9. **Both ends must allow the connection** — the source's egress and the destination's ingress.
10. **NetworkPolicies are implemented by the network plugin.** No supporting plugin, no effect.
11. **GatewayClass / Gateway / HTTPRoute**, mapped to infrastructure provider / cluster operator / application developer. Exactly one GatewayClass per Gateway; many Routes.
12. **Node-local traffic is always allowed, and a Pod cannot block access to itself.**

**Common Traps** — candidates get all of these wrong, and each one has a specific wrong belief behind it.

| The trap | The correction |
|---|---|
| "Creating an Ingress object exposes the app" | Only creating an Ingress resource has no effect. A controller must be running. |
| "Ingress can expose any protocol" | HTTP and HTTPS only. Everything else goes back to NodePort or LoadBalancer. |
| "Ingress is deprecated and will be removed" | Frozen. GA, guaranteed, no removal plans — and no further development. |
| "All Ingress controllers behave identically" | Ideally they fit the reference specification. In reality they operate slightly differently. |
| "Creating a NetworkPolicy secures the cluster" | Only if the network plugin implements NetworkPolicy. Otherwise: no effect, no signal. |
| "A Pod with no NetworkPolicy is closed by default" | Backwards. Non-isolated in both directions until something selects it. |
| "One NetworkPolicy can deny what another allows" | There is no deny rule. Policies combine by union. |
| "Only one end needs to permit the connection" | Both. Source's egress *and* destination's ingress. |
| "NetworkPolicy can block node-local or self traffic" | Neither. Both exceptions are unconditional. |
| "NetworkPolicy can do TLS / name targeting / logging / explicit deny" | All four are on the published out-of-scope list. |
| "Virtual hosting is just DNS" | Opposite sides of the connection. DNS resolves before traffic moves; virtual hosting sorts traffic that has arrived. |
| "Gateway API is a rename of Ingress" | Different API, different resource model, built around a different organising principle. |
| "NetworkPolicy can target a Service" | It selects Pods. Targeting Services by name is explicitly out of scope. |
| "An Ingress controller and a NetworkPolicy plugin are unrelated concerns" | Functionally unrelated. Structurally identical — which is §8. |

**A note on frequency.** Every trap above is a real point of confusion drawn from the documentation's own emphases and from what the material actually makes easy to get wrong. This book does not tell you how often any of them appears on the exam, because the exam's question distribution is not published and inventing a percentage would be worse than saying nothing.

---

## Practice Questions

Seventeen questions. Four draw on earlier chapters, and they are tagged. Answers follow the full set — attempt them all before scrolling.

**1.** ⚪ At which OSI layer do the Service types from Chapter 9 operate, and at which layer does an Ingress operate? What does that difference determine?

**2.** 🔵 `[retrieval: ch9]` You need to expose an HTTP application and a message broker speaking its own binary protocol, both to clients outside the cluster. How many Ingresses do you need, and how many Services of which types?

**3.** ⚪ Which four capabilities may an Ingress be configured to provide?

**4.** 🔵 An Ingress rule has `host: shop.example.com` and two path entries, `/catalog` and `/checkout`, each naming a different backend Service. Which Ingress shape is this, and what is the rule reading in order to decide?

**5.** 🟡 An Ingress path is configured with `pathType: Prefix` and `path: /aaa/bb`. A request arrives for `/aaa/bbb`. Does it match? Explain.

**6.** ⚪ A cluster runs one Ingress controller. An engineer applies an Ingress manifest with no `ingressClassName` field. Under what condition does it still get handled, and what makes that condition true?

**7.** 🔵 `[retrieval: ch3]` Chapter 3 said a controller watches for objects and drives reality toward what they describe. An Ingress controller is one. Name what it watches and name what it changes.

**8.** 🔵 An Ingress object exists in a cluster and no traffic is being routed by it. The manifest passes review with no errors found. What is the most likely explanation, and what is notable about the manifest in this scenario?

**9.** 🟡 Two clusters run the same Ingress manifest under two different Ingress controllers, and the behaviour differs in a subtle way. Is this a bug in the manifest, a bug in one controller, or expected? Cite the documentation's own position.

**10.** ⚪ State what the Kubernetes project has said about the Ingress API, in both of its halves, and say what each half implies operationally.

**11.** 🔵 You are choosing an API for external HTTP routing on a system being designed today. Which does the Kubernetes project recommend — and does that recommendation mean the other one will stop working?

**12.** 🟡 Express the same requirement twice: one host, two paths, two backend Services. Name the resources involved in the Ingress vocabulary, then in the Gateway API vocabulary, and say which role owns each Gateway API resource.

**13.** 🔵 A Pod is selected by a NetworkPolicy whose `policyTypes` lists only `Ingress`. What is permitted outbound from that Pod?

**14.** 🟡 Namespace `prod` contains Pods `web`, `api`, and `db`. One NetworkPolicy exists: it selects `db` and permits ingress from `app: api`. Can `web` reach `db`? Can `web` reach `api`? Can `db` reach an external address?

**15.** 🟡 An engineer wants to prevent a Pod labelled `app: legacy` from reaching the `payments` Pods. Two policies already permit that traffic. Write the approach — not the YAML — and say why the obvious approach does not exist.

**16.** 🔵 A NetworkPolicy has been applied and traffic that should now be blocked is still flowing. The policy is correct. Give the explanation, and say what makes this failure mode distinctively hard to catch.

**17.** 🟡 `[retrieval: ch3]` Name the rule Chapter 3 gave you about objects and components, then list every instance of it you have met in this book so far.

---

### Answers with Explanations

**1. Chapter 9's Service types operate at layer 4; Ingress operates at layer 7. That determines what each can know, and therefore what each can decide.**

A layer-4 mechanism moves packets to an address and a port. A layer-7 mechanism reads the request itself — hostname, path, headers — and routes on the contents. The Kubernetes docs describe Ingress and Gateway API as protocol-aware HTTP/HTTPS routing using URIs, hostnames and paths, against `type: LoadBalancer` as the simpler, less-configurable path [source: k8s-docs-network-model-2026-08-23].

*Why "Ingress operates at layer 4 with extra features" is wrong:* it is not an enhancement to the Service types. It is a different altitude, which is why non-HTTP protocols cannot use it at all.

**2. `[retrieval: ch9]` One Ingress, for the HTTP application. The broker goes to a Service of type NodePort or LoadBalancer — an Ingress cannot carry it.**

An Ingress does not expose arbitrary ports or protocols; exposing services other than HTTP and HTTPS typically uses NodePort or LoadBalancer [source: k8s-docs-ingress-depth-2026-08-24]. The HTTP application also needs a backing Service (a ClusterIP is sufficient), since an Ingress routes to Services rather than directly to Pods.

The point of this item is **specialisation, not replacement.** A candidate who thinks Ingress supersedes the Service ladder will look for a way to put the broker behind the Ingress, and there is not one.

**3. Give Services externally-reachable URLs; load balance traffic; terminate SSL/TLS; offer name-based virtual hosting** [source: k8s-docs-ingress-depth-2026-08-24].

*Wrong option worth rejecting:* "expose arbitrary TCP ports." That is the fifth thing people assume is on the list and it is the one thing explicitly excluded.

**4. Simple fanout. The rule is reading the HTTP URI — the path.**

A fanout configuration routes traffic from a single IP address to more than one Service based on the HTTP URI being requested [source: k8s-docs-ingress-depth-2026-08-24].

*Why "name-based virtual hosting" is wrong:* virtual hosting splits on **host**, and here there is only one host. The tell is where the list lives in the manifest: several entries under `paths` is fanout; several entries under `rules` each with its own `host` is virtual hosting.

**5. No, it does not match.**

`Prefix` matching is done on a **path element by path element** basis, and the docs give this exact case: `Prefix` with path `/aaa/bb` against request path `/aaa/bbb` is **not** a match [source: k8s-docs-ingress-depth-2026-08-24]. The elements are compared as whole labels; `bb` and `bbb` are different labels, and the fact that one is a string prefix of the other is irrelevant.

*Why "yes, `bb` is a prefix of `bbb`" is wrong:* this is exactly the misconception the path-type rules exist to prevent, and the documentation states it explicitly. If the last element of the path component is a *substring* of the last element in the request path, it is not a match [source: k8s-docs-ingress-depth-2026-08-24].

**6. It gets handled if the cluster has exactly one IngressClass marked as default. That is made true by the `ingressclass.kubernetes.io/is-default-class` annotation set to `"true"` on that IngressClass** [source: k8s-docs-ingress-controllers-2026-08-24].

If `ingressClassName` is omitted and exactly one default IngressClass exists, Kubernetes applies it [source: k8s-docs-ingress-controllers-2026-08-24]. Note the "exactly one." The condition is not "at least one."

**7. `[retrieval: ch3]` It watches Ingress objects, and the Services those objects reference. It changes a load balancer — or the edge router, or additional frontends — to match.**

An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends [source: k8s-docs-ingress-depth-2026-08-24]. That is the control-loop shape from Chapter 3 with the nouns filled in: desired state in an object, a controller watching, external reality reconciled toward the description.

This item is deliberately framed forward rather than backward. The value is in converting a memorised component name into a recognised instance of a pattern.

**8. No Ingress controller is installed. What is notable is that nothing is wrong with the manifest at all.**

Only creating an Ingress resource has no effect [source: k8s-docs-ingress-depth-2026-08-24]. This item exists because the reflex on "nothing is routing" is to re-read the YAML, and re-reading the YAML will produce nothing, indefinitely, because the YAML is correct.

*Distractor logic:* every wrong option in this family names something in the manifest — a bad `pathType`, a wrong Service port, a missing `host`. All of them are plausible causes of routing failures in general. None of them is the cause when the manifest reviews clean.

**9. Expected.** Ideally all Ingress controllers should fit the reference specification; in reality, the various Ingress controllers operate slightly differently [source: k8s-docs-ingress-depth-2026-08-24].

The documentation's own follow-up is to review your controller's documentation to understand the caveats of choosing it [source: k8s-docs-ingress-depth-2026-08-24]. Neither the manifest nor the controller is at fault in the sense the question invites: the portability of the object is real but not total, and the gap is documented rather than accidental.

**10. Frozen: (a) generally available and subject to the stability guarantees for GA APIs, with no plans for removal; (b) no longer being developed, with no further changes or updates** [source: k8s-docs-ingress-depth-2026-08-24].

Operationally: (a) means no migration emergency for what you run today. (b) means no future capability — whatever Ingress cannot do now, it never will.

*The two wrong options are the two one-half answers, and both must be rejected explicitly:* "deprecated and being removed" drops the stability half; "unaffected and fully supported for new development" drops the no-development half. Offering only one of these in a question would teach the other, which is why a well-built item offers both.

**11. Gateway. And no — Ingress will not stop working.**

The project recommends using Gateway instead of Ingress [source: k8s-docs-ingress-depth-2026-08-24], and simultaneously states that Ingress is GA, carries GA stability guarantees, and has no removal plans [source: k8s-docs-ingress-depth-2026-08-24]. Both facts are true at once, pointing in different directions, and holding both is the whole skill this section tests.

**12. Ingress vocabulary: one Ingress object, with one rule containing two paths, each naming a backend Service and port — plus the two Services themselves and an Ingress controller to fulfil it.**

**Gateway API vocabulary: a GatewayClass (infrastructure provider), a Gateway (cluster operator), and an HTTPRoute attached to that Gateway via `parentRefs` with two path matches and two `backendRefs` (application developer)** [source: k8s-docs-gateway-api-depth-2026-08-24].

The exercise is worth doing because it shows that Gateway API is not a new routing model to learn from scratch. It is the shapes you already know, redistributed across resources that belong to different owners. The routing requirement did not change. The ownership boundaries did.

**13. All outbound traffic is permitted.**

A Pod is isolated for egress only if some NetworkPolicy both selects it and has `Egress` in its `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24]. This policy names only `Ingress`, so it does not isolate the Pod for egress at all, and the default — non-isolated, all outbound connections allowed [source: k8s-docs-network-policies-depth-2026-08-24] — still stands.

*Why "outbound is now blocked" is wrong:* the two directions are declared independently. Restricting one says nothing about the other.

**14. `web` cannot reach `db`. `web` can reach `api`. `db` can reach an external address.**

Take them one at a time. `db` is selected by a policy naming `Ingress`, so it is isolated for ingress, and the only inbound connections permitted are those from its node and those the policy's ingress list allows, which is `app: api` only [source: k8s-docs-network-policies-depth-2026-08-24]. So `web` is out.

`api` is selected by no policy at all, so it remains non-isolated for ingress: all inbound allowed [source: k8s-docs-network-policies-depth-2026-08-24]. `web` reaches it. (And `web` is itself unselected, so it is non-isolated for egress too; both ends allow it.)

`db`'s policy names only `Ingress`, so `db` is not isolated for egress. All outbound connections allowed [source: k8s-docs-network-policies-depth-2026-08-24].

*The trap here is assuming one policy in a namespace changes the namespace's posture.* It changes exactly one Pod's posture, in exactly one direction.

**15. The approach: find and remove or narrow the grants that currently permit it. There is no deny policy, because the API has no explicit-deny mechanism.**

Policies are additive and combine by union [source: k8s-docs-network-policies-depth-2026-08-24], and the ability to explicitly deny policies is on the published out-of-scope list. The model is deny by default with only the ability to add allow rules [source: k8s-docs-network-policies-depth-2026-08-24].

*The obvious wrong answer — "write a more restrictive policy selecting `payments` that excludes `app: legacy`" — is the specific shape a firewall-experienced engineer's mistake takes.* It is more useful as a distractor than a generically wrong option, because the person choosing it has a coherent mental model that happens to be the wrong one. The correction is not "you wrote it wrong," it is "there is no such rule to write."

**16. The network plugin does not implement NetworkPolicy, so the resource has no effect. What makes it distinctively hard to catch is that there is no observable difference between an unenforced policy and a correctly enforced one against traffic nobody is sending.**

Network policies are implemented by the network plugin, and creating a NetworkPolicy resource without a controller that implements it will have no effect [source: k8s-docs-network-policies-depth-2026-08-24]. The object is present, `kubectl` displays it correctly, and every signal available to you says it is working.

Note the contrast with question 8. Both are the same structural failure, object present and component absent, and they differ entirely in how you find out. One breaks a website. The other breaks nothing you can see.

**17. `[retrieval: ch3]` An object without its component does nothing.**

Four instances:
- A `type: LoadBalancer` Service on a cluster with no provider to fulfil it (Ch 9 §3).
- A Service whose selector matches no Pods (Ch 9 §4).
- An Ingress with no Ingress controller (Ch 10 §3) [source: k8s-docs-ingress-depth-2026-08-24].
- A NetworkPolicy on a plugin that does not implement NetworkPolicy (Ch 10 §7) [source: k8s-docs-network-policies-depth-2026-08-24].

If you produced all four, §8's argument is one you assembled rather than one you were handed, and the question you take forward from it (*what is watching this, and is it installed?*) is a tool rather than a slogan.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **The exposure ceiling** | One external address per Service. Fine for one; expensive for fifty. No Service type reads HTTP. |
| **The layer boundary** | Chapter 9 moves packets to an address. This chapter reads requests. Which side you are on determines what you can know. |
| **North-south / east-west** | Into the cluster / between Pods. §1–§5 is one; §6–§7 is the other. |
| **Edge router** | The router enforcing the cluster's firewall policy. A cloud gateway or physical hardware. An Ingress controller may configure it. |
| **Ingress** | HTTP and HTTPS routes from outside to Services within, controlled by rules on the resource. **Nothing else.** |
| **The four capabilities** | Externally-reachable URLs, load balancing, TLS termination, name-based virtual hosting. |
| **Simple fanout** | One address, one host, many paths → many Services. The rule reads the **URI**. |
| **Name-based virtual hosting** | One address, many hosts → many Services. The rule reads the **host**. |
| **DNS vs virtual hosting** | DNS resolves a name *before* traffic moves. Virtual hosting sorts traffic that has *already arrived*. Opposite sides of the connection. |
| **`pathType`** | `Exact`, `Prefix`, `ImplementationSpecific`. `Prefix` matches element by element, not by string prefix. Longest match wins; `Exact` breaks ties. |
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
| **The rule** | An object without its component does nothing. Four instances so far. Ask: *what is watching this, and is it installed?* |

---

## The Voyage Ahead

You have spent two chapters on the network, and you have been treating one thing as a given the entire time: that a Pod which restarts is a Pod that starts over. Chapter 5 said it directly — Pods are cattle, replaced rather than repaired — and Chapters 6 through 10 have quietly depended on it. A Service can point at an interchangeable set of backends precisely because they *are* interchangeable.

Chapter 11 is where that assumption runs out.

Some workloads write things down. A database has a disk, and the contents of that disk are not a detail of the Pod. They are the entire point of running it. Chapter 11 works out what happens to data when the Pod that produced it is deleted, and the answer turns out to be a ladder of three different lifetimes, only one of which survives the thing that created it.

It also closes a loop this book left open on purpose. Chapter 6 introduced StatefulSet and told you it was about stable *identity*, not about writing to disk, and then admitted the explanation was incomplete and would stay that way until storage arrived. Storage arrives in Chapter 11, and the second half of that answer arrives with it: what a per-replica volume claim is, and why it outlives not just the Pod but the rescheduling.

And you will meet a third pluggable interface. You have collected two now: CRI at the container runtime, CNI at the network. Chapter 11 brings CSI, and by the time Chapter 17 collects all four in one place, the shape will be so familiar that the collection will feel like recognition rather than instruction.

One last thing to carry across the chapter boundary. You will meet several objects in Chapter 11 that describe storage without providing any, and at least one arrangement where a claim sits unbound because the thing that would satisfy it has not been installed.

You know what question to ask about that now.

> *"An object is a record of intent. Intent does not act. Something has to be watching."*