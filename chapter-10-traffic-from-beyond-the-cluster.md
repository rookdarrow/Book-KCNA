---
chapter: 10
chapter_type: "content"
title: "Traffic from Beyond the Cluster"
subtitle: "Frozen, superseded, and inert without a controller"
exam_domain: "Container Orchestration (competency: Networking)"
domain_weight_pct: 5
complexity: "mixed"
novelty: "moderate"
prereq_factor: "heavy"

#-- SUBTITLE NOTE. The arc outline's working subtitle is "Ingress is
#-- frozen, Gateway is the future, and neither does anything without a
#-- controller" — fourteen words against this stage's ≤10-word
#-- constraint. Tightened above to seven. The compression is not just
#-- length: "inert" is the word §7 needs for a NetworkPolicy on an
#-- unsupporting plugin, and using it in the subtitle makes the
#-- subtitle cover BOTH halves of the chapter rather than only the
#-- Ingress half. The arc's version names Ingress and Gateway and stops
#-- there, which under-describes a chapter that is 40% NetworkPolicy.
#-- Arc-faithful alternative preserved in § Open questions #1.

#-- EXAM_DOMAIN NOTE. Recorded as D2.1 Networking, matching Ch 9's house
#-- form. The arc outline scopes this chapter "D2.1 (+ D2.2 boundary)"
#-- because NetworkPolicy is listed under BOTH D2.1 Networking and D2.2
#-- Security in B1's concept map. B2's ordering rule #6 settles it:
#-- teach NetworkPolicy once, in Networking, and cross-bear from
#-- Security. This chapter is where it is taught. Ch 12 §9 refers and
#-- never redefines. kb_tags carries both objective IDs.

#-- PREREQ NOTE. `heavy`, not `standard` — the first `heavy` in Part III.
#-- B2 lists exactly one prerequisite chapter for this chapter (Ch 9),
#-- which looks light until you notice it means ALL of Ch 9. This
#-- chapter re-teaches no part of the Service model: §1's argument is
#-- arithmetic on Ch 9 §3's ladder, §2's backends are Ch 9's Services,
#-- §6's subjects are Ch 4's selectors pointed at Ch 9's Pod IPs. A
#-- reader who skipped Ch 9 cannot start here. The Soundings rubric's
#-- 0–2 branch must say so in as many words.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "standard" — 5
#-- points. Planning signal only, NOT a target.
#--
#-- ⚠ SECTION NUMBERING IS LOAD-BEARING. Eight published cross-bearings
#-- point into this chapter and FOUR name a section by number — all four
#-- from Chapter 9, which shipped 2026-08-24:
#--   chapter-09 line  544 → *[... see Ch 10 §1 — the exposure ceiling and what crosses it]*
#--   chapter-09 line 1056 → *[... see Ch 10 §2 — name-based virtual hosting]*
#--   chapter-09 line  407 → *[... see Ch 10 §6 — NetworkPolicy]*
#--   chapter-09 line 1706 → *[... see Ch 10 §6 — NetworkPolicy]*
#-- All four match the B6 skeleton exactly. §1, §2 and §6 below are
#-- fixed. Do not renumber without editing chapter-09 in four places.
#-- Verified 2026-08-25 against chapters 01–09.
sections:
  - name: "Where LoadBalancer Runs Out"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch10-fig01-ingress-vs-service-loadbalancer"
    checkpoint_after: false
  - name: "Routing by Host and Path"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch10-fig02-ingress-fanout-and-name-based-hosts"
    checkpoint_after: false
  - name: "The Object Is Not the Implementation"
    objectives: ["D2.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Frozen, Not Deprecated"
    objectives: ["D2.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Roles, Not Just Routes"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch10-fig03-gateway-api-role-split"
    checkpoint_after: true
  - name: "Allowing, Never Denying"
    objectives: ["D2.1", "D2.2"]
    requires_figure: true
    figure_anchor: "ch10-fig04-networkpolicy-additive-selectors"
    checkpoint_after: false
  - name: "What NetworkPolicy Cannot Do"
    objectives: ["D2.1", "D2.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Nothing Happens Without a Controller"
    objectives: ["D2.1", "D2.2"]
    requires_figure: true
    figure_anchor: "ch10-zenith-nothing-without-a-controller"
    checkpoint_after: false

#-- Eight sections against 5 weight points, matching Ch 9's count for two
#-- fewer points. The ratio is defensible because this chapter is TWO
#-- arcs, not one: an API-generations arc (§1–§5, Ingress → freeze →
#-- Gateway) and a policy arc (§6–§7), joined at §8 by a pattern that
#-- happens to be the failure mode of both. Fold options considered and
#-- rejected in § Open questions #10.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "one IP address serving several hostnames — the ordinary web-server prior, and what the server must read to tell them apart"
    - "retrieval from Ch 9 §3 — fifty services, one LoadBalancer Service each, and what that arrangement costs"
    - "retrieval from Ch 9 §3 — which Service type routes /checkout and /catalog to different backends, and why the answer is none"
    - "ordinary firewall priors — is unlisted traffic allowed or denied by default, and can a later rule deny what an earlier rule allowed"
    - "the words 'deprecated' and 'no longer developed' — what each implies about whether a thing will be removed"
    - "retrieval from Ch 3 §4 — the absent-component rule stated back in the reader's own words"
    - "retrieval from Ch 9 §1 — rule 2's 'barring intentional network segmentation' hedge, and at what layer segmentation would have to be enforced"
    - "TLS termination in an ordinary web stack — where the certificate lives, and what the backend server receives"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 17 = 35 and states plainly that the Bearings
#-- figure is a minimum to exceed. Set at 15 across three checkpoints of
#-- 5, matching the shape shipped by Chapters 3–9 without exception.
#-- Chapter total 35 -> 40.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 17
  total_this_chapter: 40

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D2.1", "D2.2"]
  concepts:
    - "edge-router"
    - "cluster-network"
    - "exposure-ceiling"
    - "l4-l7-boundary"
    - "north-south-traffic"
    - "east-west-traffic"
    - "protocol-aware-routing"
    - "ingress"
    - "ingress-rule"
    - "ingress-host"
    - "ingress-path"
    - "path-type"
    - "simple-fanout"
    - "name-based-virtual-hosting"
    - "tls-termination"
    - "default-backend"
    - "single-service-ingress"
    - "ingress-controller"
    - "ingressclass"
    - "reference-specification"
    - "absent-component-pattern"
    - "feature-freeze"
    - "frozen-not-deprecated"
    - "ga-stability-guarantee"
    - "gateway-api"
    - "gatewayclass"
    - "gateway"
    - "httproute"
    - "parentrefs"
    - "role-oriented-design"
    - "infrastructure-provider-role"
    - "cluster-operator-role"
    - "application-developer-role"
    - "gateway-request-flow"
    - "networkpolicy"
    - "l3-l4-control"
    - "application-centric-policy"
    - "pod-selector"
    - "namespace-selector"
    - "ipblock"
    - "cidr-range"
    - "policy-types"
    - "ingress-isolation"
    - "egress-isolation"
    - "non-isolated-default"
    - "additive-policy-semantics"
    - "no-deny-rule"
    - "both-ends-must-allow"
    - "default-deny-by-selection"
    - "node-local-traffic-always-allowed"
    - "self-traffic-unblockable"
    - "policy-plugin-dependency"
    - "silently-inert-policy"
    - "networkpolicy-out-of-scope"
  commands:
    - "kubectl-get-ingress"
    - "kubectl-describe-ingress"
    - "kubectl-get-networkpolicy"

figures_planned:
  - "ch10-fig01-ingress-vs-service-loadbalancer"
  - "ch10-fig02-ingress-fanout-and-name-based-hosts"
  - "ch10-fig03-gateway-api-role-split"
  - "ch10-fig04-networkpolicy-additive-selectors"
  - "ch10-zenith-nothing-without-a-controller"
---

# Chapter 10: Traffic from Beyond the Cluster
## *"Frozen, superseded, and inert without a controller"*

<!-- AUTHOR-REVIEW: The subtitle's "superseded" is supported but untagged — `k8s-docs-network-model-2026-08-23` writes "The Gateway API (or its predecessor, Ingress)". A `[source:]` tag cannot live in the subtitle without breaking the structural contract's subtitle pattern, and this pass may not retitle the section, so the tag belongs at §5 where the Gateway/Ingress relationship is taught. Flagged here so it is not lost between passes. -->

**Domain: Container Orchestration (competency: Networking) | Domain weight: 28% [source: cncf-kcna-curriculum-pdf-2026-08-23] | Complexity: Mixed | Novelty: Moderate**

> *The 28% figure is CNCF's published weight for the whole Container Orchestration domain. The published curriculum gives four domain-level percentages and nothing finer — no weight is attached to Networking, or to any other competency [source: cncf-kcna-curriculum-pdf-2026-08-23]. This book's allocation of that 28% across its Part III chapters is therefore the author's, derived from curriculum breadth rather than from any published figure. See the front matter's weight-allocation disclosure.*

<!-- AUTHOR-REVIEW: The prior wording — "CNCF publishes no per-competency weights" — asserted a universal negative about CNCF's publication practice that the cached corpus cannot establish; absence of finer weights in one snapshot is not absence across CNCF's publications. Narrowed to what `cncf-kcna-curriculum-pdf-2026-08-23` actually attests. To restore the stronger claim, the corpus needs a snapshot of the Linux Foundation KCNA exam/registration page — it currently holds no exam-logistics source at all. The same gap governs the Exam Alert's "the exam's question distribution is not published". -->

---

## Attention Budget

**Total time: ~125 minutes | Recommended: Split across 2 sessions**

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

**The session split goes between §5 and §6.** This chapter is two chapters wearing one number: an API-generations arc (§1–§5) and a policy arc (§6–§7), joined at §8. §6 asks you to unlearn a firewall instinct you have probably held for a decade, and it will land better on a fresh head than on a tired one. The split puts roughly 66 minutes before the break and 58 after it, the last 25 of which are the Exam Alert and the practice set. Take those as a third sitting if the second runs long.

*If you only have 15 minutes: read §6. It is the section most likely to overturn something you currently believe, and believing it costs you points. If you have 35, add §3 and §4 and take Taking Your Bearings #3 — the controller rule, the freeze, and the policy defaults, plus the checkpoint that tests the hardest of the three.*

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

1. **The `Host` header, available only after the TCP connection is established and the request has been sent** `[source: k8s-docs-gateway-api-depth-2026-08-24]`. The client's DNS lookup resolved the name to an address before any traffic moved; the name itself travels inside the request. (HTTPS carries an earlier tell in the **SNI (Server Name Indication)** field of the TLS handshake — traffic for several hostnames can be multiplexed on a single port that way, where the proxy terminating TLS supports SNI `[source: k8s-docs-ingress-depth-2026-08-24]` — but the routing decision is conventionally made on the `Host` header.)

2. **`Service.Type=LoadBalancer`** *[cross-bearing: see Ch 9 §3 — the Service type ladder]*. Fifty of them costs fifty external addresses, fifty provisioned load balancers, fifty line items on a cloud bill, and fifty things to configure, monitor, and eventually decommission.


3. **None of them.** None of them reads HTTP. Three of the four operate on addresses and ports; the fourth, ExternalName, is a DNS alias with no proxying set up at all `[source: k8s-docs-service-2026-08-23]`. `/checkout` and `/catalog` are bytes inside an HTTP request, and nothing in Chapter 9 opens the request to look.

4. Most likely **dropped**, and **the deny wins**. That is how ordinary packet-filtering firewalls behave, and it is a sound instinct nearly everywhere.

5. **Deprecated** implies eventual removal, so you would avoid starting new work on it. **No longer developed** says nothing about removal; it says the thing is finished. It may well be permanent. You might still use it, knowing it will never gain a feature.

6. **An object without its component does nothing.** You have met it at least twice: a `type: LoadBalancer` Service on a cluster with no load balancer to provision, and a Service whose selector matched no Pods.

7. Something has to be able to restrict Pod-to-Pod reachability. Since the CNI plugin is what actually moves the packets, enforcement would have to live down there, wherever the packets themselves are handled.

8. **At the reverse proxy or load balancer at the edge**, which holds the certificate and private key. The application server behind it receives plain HTTP `[source: k8s-docs-ingress-depth-2026-08-24]`.

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

Orders written out in a fair hand, with every heading correct, change nothing at all if nobody has been detailed to read them.

A well-formed Ingress on a cluster with no Ingress controller is a correct object that does nothing. A well-formed NetworkPolicy on a network plugin that does not implement NetworkPolicy is a correct object that does nothing. Unlike the Ingress, it does nothing *quietly*. Unreachability is loud: a pager goes off, a customer complains, somebody is looking at it within minutes. Unrestricted reachability is silent; everything works exactly as it did, which is indistinguishable from a policy working perfectly against traffic nobody happens to be sending. That asymmetry is the most valuable thing in this chapter, and you should have it in hand before you meet either object.

Chapter 9 told you that Chapter 10 would give a name to a shape you had already met twice. Here is the part Chapter 9 did not say: you will meet it **twice more in this chapter alone**, in two objects that have nothing to do with each other. This is where it stops being a curiosity and becomes a rule you can apply to things this book never mentions.

The stakes, stated flat. This is the smallest allocation in Part III, and the material still deserves full attention for two specific reasons. First, `frozen` versus `deprecated` is the most precise word-level distinction in the curriculum, and precise distinctions are what multiple-choice exams are built out of. Second, NetworkPolicy carries more cataloged traps than any other single topic in this book, and every one of them is a case where your existing firewall intuition hands you the wrong answer with complete confidence.

Two reasons. The chapter does not need a third.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Place** any exposure mechanism on the correct side of the layer boundary — what operates on addresses and ports, and what opens the request and reads it.
- **State** what Ingress does, what it explicitly does not do, and which two protocols are the whole of its remit.
- **Distinguish** a simple fanout from name-based virtual hosting, and both from the DNS-based service discovery you learned last chapter.
- **Explain** why a correctly written Ingress can have no effect whatsoever, and name the thing whose absence causes it.
- **Say what `frozen` means** — precisely, in both of its halves — and why it is not the same word as `deprecated`.
- **Name** the three role-mapped Gateway API resources and the organizational role each one belongs to.
- **Predict** whether a given connection is allowed under a given set of NetworkPolicies, using rules that are additive, allow-only, and enforced at both ends of the connection — and starting from the posture a Pod holds before any policy has selected it.
- **Describe** what becomes of a NetworkPolicy that the cluster's network plugin does not implement, and why that failure is the harder of this chapter's two to notice.

*You'll also acquire one rule that outlives this chapter: an object without its component does nothing. You'll use it in Chapter 13, in Chapter 17, and on things this book never gets to.*

---

## ⚪ §1 — Where LoadBalancer Runs Out

You already have the argument. Chapter 9 made it, and made it recently.

One external address per Service. Fifty Services, fifty addresses, fifty provisioned load balancers, fifty bills, fifty things to manage. And no Service type in that chapter reads HTTP, so a single address cannot serve two paths. A Service knows an address and a port, and stops there *[cross-bearing: see Ch 9 §3 — the Service-type ladder and the exposure ceiling]*.

That is the ceiling. This section does not re-derive it. It names the vocabulary the rest of the chapter runs on, and gets out of the way.

### The layer boundary

Everything in Chapter 9 operates at what practitioners call **layer 4**. A Service moves packets to an address and a port and has no opinion about what those packets contain. Everything in §2 through §5 operates at **layer 7**: it reads the request — the host it was addressed to, the path it asked for, sometimes the headers it carries — and decides where to send it on that basis.

The documentation sorts the same two groups without putting layer numbers on them. It describes Ingress as protocol-aware HTTP/HTTPS routing using URIs, hostnames, and paths; Gateway API as dynamic infrastructure provisioning and advanced traffic routing; and `type: LoadBalancer` as the simpler but less configurable mechanism for getting traffic into a cluster [source: k8s-docs-network-model-2026-08-23]. The one place it does reach for **OSI (Open Systems Interconnection)** layer numbers is NetworkPolicy, which it places at the IP address or port level — layer 3 or 4 [source: k8s-docs-network-model-2026-08-23]. That is not a coincidence, and §6 is where it pays.

Keep this boundary marked. It is not decoration and it is not only about §2. §6 goes back *down* to layers 3 and 4, and a reader who has lost the ladder will experience NetworkPolicy as an unrelated topic that happened to land in the same chapter.

> ★ **Fixed Point:** Everything in Chapter 9 moves **packets** to an address. Everything in §2 through §5 reads **requests**. Which side of that boundary a mechanism sits on determines what it can know, and therefore what it can decide.

### North-south and east-west

Two words from ordinary industry vocabulary that this book has not used yet. They make the shape of this chapter sayable in one sentence.

**North-south** traffic enters the cluster from outside. **East-west** traffic moves between Pods inside it. Those two definitions are the industry's, not the project's. What the Kubernetes project supplies is the pairing, in a blog post on Gateway API rather than in the reference documentation, describing the API's initial focus as ingress, "north-south," traffic, and service mesh as the "east-west" case [source: k8s-blog-gateway-api-north-south-east-west-2026-08-24].

This chapter does one of each. §1 through §5 are about north-south. §6 and §7 are about east-west.


> 🪢 **Mnemonic:** *North-south goes through the wall; east-west stays inside it.* §1–§5 is the wall. §6–§7 is inside.

### The edge router

One piece of scaffolding Chapter 9 did not supply, and §3 will need.

The Kubernetes documentation is explicit that in most common deployments, **the nodes in your cluster are not part of the public internet** [source: k8s-docs-ingress-depth-2026-08-24]. Something sits between the two: the **edge router**, a router that enforces the firewall policy for your cluster, whether that is a gateway managed by a cloud provider or a physical piece of hardware [source: k8s-docs-ingress-depth-2026-08-24].

Naming it here means that when §3 tells you an Ingress controller may fulfill an Ingress "usually with a load balancer, though it may also configure your edge router," you already know what that clause is about.

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

Read that twice, because both halves matter. *Routes from outside to Services within* — the things an Ingress routes to, in every case this chapter covers, are ordinary Services. The ClusterIP Services you built in Chapter 9, unchanged, unaware that anything new is in front of them. And *rules defined on the resource*: the routing decisions live in the object you write, not in the controller's configuration file.

An Ingress may be configured to give Services externally-reachable URLs, load balance traffic, terminate SSL/TLS, and offer name-based virtual hosting [source: k8s-docs-ingress-depth-2026-08-24]. Four capabilities, as the documentation enumerates them.

### And what it refuses to do

Immediately after the capabilities, and not buried at the bottom of the section where you would skim past it:

**An Ingress does not expose arbitrary ports or protocols. Exposing services other than HTTP and HTTPS to the internet typically uses a service of type `Service.Type=NodePort` or `Service.Type=LoadBalancer`** [source: k8s-docs-ingress-depth-2026-08-24].

This is more satisfying than a caveat. It means the ladder you learned in Chapter 9 is not superseded by this chapter. It is *specialized past*. Ingress takes over one class of traffic, the HTTP class, and everything else goes back down to §1's layer. A PostgreSQL database, a message broker speaking its own binary protocol, a game server, an SMTP relay: none of those go through an Ingress. They go through NodePort or LoadBalancer, exactly as they did last chapter.

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
![Two stacked panels comparing Ingress routing. In the upper panel, two HTTP requests share the host shop.example.com but differ by path; a single IP address 203.0.113.10 feeds a box labelled 'reads: path' that forks to a catalog Service and a checkout Service. In the lower panel, two requests share the path slash but differ by host; the same IP address feeds a box labelled 'reads: host' that forks to a shop Service and a blog Service. The matched fragment of each request is underlined.](figures/ch10-fig02-ingress-fanout-and-name-based-hosts.svg)

<!-- ASCII-FALLBACK
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
-->

**TLS.** You can secure an Ingress by specifying a **Secret that contains a TLS private key and certificate** [source: k8s-docs-ingress-depth-2026-08-24]. The Ingress resource supports a single TLS port, 443, and **assumes TLS termination at the ingress point — traffic to the Service and its Pods is in cleartext** [source: k8s-docs-ingress-depth-2026-08-24]. The TLS Secret must contain keys named `tls.crt` and `tls.key` [source: k8s-docs-ingress-depth-2026-08-24], and the documentation's example Secret is of type `kubernetes.io/tls`, the Secret type Chapter 4 cataloged *[cross-bearing: see Ch 4 §4 — Secret types, including `kubernetes.io/tls`]*.

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

| `pathType` | Behavior |
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

## ⚪ §3 — The Object Is Not the Implementation

Here is the sentence:

**You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect** [source: k8s-docs-ingress-depth-2026-08-24].

Not "less effect." Not "reduced functionality." None. The manifests in §2 are correct, well-formed, and accepted by the API server, and on a cluster with no Ingress controller they route nothing, because nothing is reading them.

> ★ **Fixed Point:** **You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect** [source: k8s-docs-ingress-depth-2026-08-24].

### What an Ingress controller is

**An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends to help handle the traffic** [source: k8s-docs-ingress-depth-2026-08-24]. There it is: §1's edge router, doing its job in a sentence you can now read without stopping. For an Ingress to work in your cluster, **there must be an ingress controller running**, and you need to select at least one and make sure it is set up [source: k8s-docs-ingress-controllers-2026-08-24].

Notice the structure of what you just read. The Ingress object is a *description of desired routing.* The controller is a control loop that reads that description and makes something in the real world match it. That is Chapter 3's control loop, unchanged and by now familiar: desired state in an object, a controller watching, reality dragged toward the description *[cross-bearing: see Ch 3 §6 — the control loop and the controller pattern]*. Recognizing it here should cost you nothing, which is the point of having learned it once properly.

### The rule, retrieved

Chapter 3 gave you a sentence and asked you to keep it:

**An object without its component does nothing.**

It also told you that you would meet it four more times. This is the first of those four, and Chapter 3 published the pointer to this exact paragraph *[cross-bearing: see Ch 3 §4 — addons, and what else is optional]*.

Two counts run through this chapter, and they are not the same count. Chapter 3's four are the instances it lined up ahead of you: this one, one more in §7, and two in chapters still to come. The other count is your own, the instances you have personally watched fail. That one started last chapter, and it currently stands at two.

You do not have to take the rule on faith, because you have already collected that evidence. Last chapter, twice:

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

If you do not specify an IngressClass on an Ingress and your cluster has **exactly one** IngressClass marked as default, Kubernetes applies that default [source: k8s-docs-ingress-controllers-2026-08-24]. You mark one as default by setting the `ingressclass.kubernetes.io/is-default-class` annotation to the string `"true"` [source: k8s-docs-ingress-controllers-2026-08-24]. If more than one IngressClass carries that marking, an Ingress that omits `ingressClassName` cannot be created at all; the resolution is to ensure at most one is marked default [source: k8s-docs-ingress-depth-2026-08-24]. Some ingress controllers work even without a default IngressClass defined; even so, the Kubernetes project still recommends that you define one [source: k8s-docs-ingress-depth-2026-08-24].

### The honest note

One more fact, and it is the one that keeps this from being a tidy story:

**Ideally, all Ingress controllers should fit the reference specification. In reality, the various Ingress controllers operate slightly differently** [source: k8s-docs-ingress-depth-2026-08-24].

That is the documentation's own phrasing, twice over: the Ingress page and the Ingress Controllers page say the same thing in nearly the same words [source: k8s-docs-ingress-controllers-2026-08-24]. It matters because the promise of a portable object is undercut, precisely, by the gap between a reference specification and any particular implementation of it. The documentation's own advice is to review your controller's documentation to understand the caveats of choosing it [source: k8s-docs-ingress-depth-2026-08-24].

> 🪝 **Snag:** Two clusters, the same Ingress manifest, different behavior. Same chart, different pilot. The object is portable; the controllers are only *ideally* identical. The gap between the reference specification and a particular implementation is where a configuration that worked for a year stops working after a migration, and where the failure looks like a bug in your manifest rather than a difference in the thing reading it.

You now have a rule and three instances of it — three on your own count, one on Chapter 3's. Do not close the pattern here. §7 has a fourth, and it behaves differently from the first three in a way that turns out to matter more than all of them.

*[cross-bearing: see Ch 6 §8 — a custom controller acting on a custom resource is this same shape, met as the operator pattern]*
*[cross-bearing: see Ch 13 §7 — `kubectl top` on a cluster with no metrics-server]*
*[cross-bearing: see Ch 17 §7 — VPA, which is an addon and is not there by default]*

---

## ☆ Taking Your Bearings #1

Five questions on §1 through §3 — the ceiling, the object, and the component that has to exist. Two of them reach back to earlier chapters.

**1.** ⚪ `[retrieval: ch9]` You need to expose a PostgreSQL database and a web application to clients outside the cluster. Which one can an Ingress handle, and what do you use for the other?

**2.** ⚪ One IP address serves `shop.example.com` and `blog.example.com`, routing each to a different Service. Name the Ingress capability. Then: one host, with `/catalog` and `/checkout` going to different Services. Name that one.

**3.** 🔵 A colleague applies a correct Ingress manifest to a fresh cluster. `kubectl get ingress` shows it. No traffic reaches the application. Name the most likely cause, and say what `kubectl get` actually proves.

**4.** 🔵 An Ingress is applied with no `ingressClassName` set. Name the one thing in the cluster that decides whether it is assigned a controller anyway — and say what a *second* IngressClass carrying the same marking would do to that Ingress.

**5.** 🔵 `[retrieval: ch3]` Chapter 3 gave you a one-sentence rule about objects and components. State it, then name the two things from Chapter 9 that were instances of it.

---

**Answers with Explanations:**

**1. The web application, over HTTP/HTTPS. The database needs `Service.Type=NodePort` or `Service.Type=LoadBalancer`.**

An Ingress exposes HTTP and HTTPS routes and nothing else; exposing services other than HTTP and HTTPS typically uses NodePort or LoadBalancer [source: k8s-docs-ingress-depth-2026-08-24]. PostgreSQL speaks its own wire protocol over TCP, so there is nothing for a layer-7 router to read.

The framing that matters here is **specialization, not replacement.** Ingress does not sit *instead of* the Service-type ladder. It sits *above* it, for one class of traffic. The ladder is still the correct answer for everything else, which is why §4's news about the Ingress API being frozen is survivable rather than alarming: nothing you learned in Chapter 9 is going anywhere.

Why a wrong answer is wrong: "use an Ingress for both, with different ports" fails because an Ingress does not expose arbitrary ports at all [source: k8s-docs-ingress-depth-2026-08-24]. The port fields in an Ingress rule name the *backend Service's* port, not a port the Ingress listens on.

**2. Name-based virtual hosting; simple fanout.**

Name-based virtual hosting routes HTTP traffic to multiple host names at the same IP address [source: k8s-docs-ingress-depth-2026-08-24]. Simple fanout routes traffic from a single IP address to more than one Service based on the HTTP URI [source: k8s-docs-ingress-depth-2026-08-24]. Asked as a pair on purpose: the thing to retrieve is not either definition but the **discriminator**, host versus path. Both put many Services behind one address.

The error to watch for is swapping them. The tell is in the manifest: several entries under `paths` is fanout; several entries under `rules`, each with its own `host`, is virtual hosting.

**3. No Ingress controller is installed. `kubectl get` proves only that the object exists.**

Only creating an Ingress resource has no effect; a controller must be present to satisfy it [source: k8s-docs-ingress-depth-2026-08-24]. `kubectl get ingress` returning your object tells you a record is in etcd and the API server will serve it back. It is a fact about storage. It is not a fact about routing, and nothing in that output is evidence that any component has ever looked at the object.

Nothing here is a mistake on your colleague's part. The manifest is correct, the expectation was reasonable, and the missing piece is invisible from the object. That is precisely what makes this pattern worth learning as a *first* question rather than a last resort.

**4. An IngressClass marked as the cluster default. A second one carrying the same marking does not widen the net — it removes it, and the Ingress can no longer be created at all.**

Setting the `ingressclass.kubernetes.io/is-default-class` annotation to the string `"true"` on an IngressClass makes it the cluster default, and new Ingresses that do not specify an `ingressClassName` are assigned that class [source: k8s-docs-ingress-depth-2026-08-24]. The condition is **exactly one**. If more than one IngressClass is marked default, an Ingress that omits `ingressClassName` cannot be created; the resolution is to ensure at most one carries the marking [source: k8s-docs-ingress-depth-2026-08-24].

The instinct to correct: more defaults feels like more coverage. It is the opposite. Two defaults do not give an unclassed Ingress two chances to be adopted. They take away the one chance it had, because the cluster now has no way to choose.

Worth holding next to question 3. Both are the same failure in the end, an object that never reaches a controller. But this one fails at the moment you apply it, and that one applies cleanly and then quietly does nothing. Only one of them tells you.

<!-- AUTHOR-REVIEW: B1.4 was repointed off reference-specification drift (P9 tests that better, and §3 teaches it in prose) onto IngressClass and the default-class mechanism, per the question-quality audit — IngressClass otherwise reaches only one question in the chapter. The item assumes §3 states the consequence of a second default: an Ingress omitting `ingressClassName` can no longer be created. That fact is in k8s-docs-ingress-depth-2026-08-24 and verified by the fact-accuracy audit, but if §3's prose stops at the annotation and the single-default assignment, add the one clause there rather than softening the question. -->

**5. `[retrieval: ch3]` An object without its component does nothing.** The two Chapter 9 instances: a `type: LoadBalancer` Service on a cluster with no load balancer to provision one, and a Service whose selector matches no Pods.

The wrong answer to watch for is stopping at one. `type: LoadBalancer` is the instance people keep, because the absent piece has a name and a price attached to it. The Service whose selector matches nothing is the one they drop — nothing there is *un-installed*, and the object is complete and correct on its own terms. Same shape all the same: a record the cluster will serve back to you, and nothing behind it. And the Ingress controller from §3 is not one of the two. It is the third, and the one you found yourself.

If you can list the instances now, §8 will land as a count you already made rather than as an assertion the book handed you. That is the difference between remembering a rule and holding one.

---

**Checkpoint: You've Now Mastered**

✓ Where the Service-type ladder runs out, and the layer boundary that explains why
✓ What Ingress does, what it refuses to do, and the two shapes it takes
✓ Why a perfectly correct object can accomplish nothing
✓ Which controller an Ingress belongs to, and what happens when nothing says
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

Here is the recommendation as the documentation states it, with nothing attached: **the Kubernetes project recommends using Gateway instead of Ingress** [source: k8s-docs-ingress-depth-2026-08-24]. Not *for new work*. Not *by some deadline*. Not *unless you have a reason*. One unqualified sentence. What sits beside it is equally unqualified: the project has not deprecated Ingress, has announced no removal, and continues to extend it the stability guarantees that GA APIs carry. A light has been hung on the new channel; the old one has not been closed.

Where that leaves you in practice is a second question, and the answer to it is this book's reading rather than the project's wording: **do not panic about what you are running, and think hard before building something new on an API that will never gain a feature again.** If you have heard the recommendation summarized as *"use Gateway for new work"* — including elsewhere in this chapter — that framing is a practitioner's gloss on the second bullet, not a scope the documentation supplies. The documentation says *instead of*, and stops there.

Keep the two apart. On an exam, you are being asked what the project said, not what a sensible engineer does about it.

The project said what it said, precisely. The reasoning behind the decision is not this book's to supply.

*[cross-bearing: see Ch 8 §6 — semantic versioning, which is half the vocabulary this section spends]*

The obvious next question is what "use Gateway instead" actually means. §5.

---

## 🟡 §5 — Roles, Not Just Routes

The temptation is to open with three resource names. Resist it. The resource names are a *consequence*; taught in the wrong order they become three arbitrary things to memorise instead of one idea with three parts.

### The idea

**Gateway API is a family of API kinds that provide dynamic infrastructure provisioning and advanced traffic routing.** It makes network services available using an **extensible, role-oriented, protocol-aware** configuration mechanism [source: k8s-docs-gateway-api-depth-2026-08-24].

*Role-oriented* is the word that matters. Everything else in the API falls out of it.

### The three roles

Gateway API kinds are modeled after the organizational roles responsible for managing Kubernetes service networking [source: k8s-docs-gateway-api-depth-2026-08-24]:

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
![Three stacked ownership bands. The top band, infrastructure provider, contains a GatewayClass box. The middle band, cluster operator, contains a Gateway box joined upward to GatewayClass by an edge labelled 'exactly 1'. The bottom band, application developer, contains three HTTPRoute boxes joined upward to the Gateway by edges labelled 'many, parentRefs'. A caption notes the bands are ownership boundaries, not runtime layers.](figures/ch10-fig03-gateway-api-role-split.svg)

<!-- ASCII-FALLBACK
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
-->

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

*[cross-bearing: see Ch 9 §7 — the client's resolver, which appears here as one step in a flow rather than as a topic]*
*[cross-bearing: see Ch 17 §4 — CRDs as one of the four pluggable interfaces, of which this is a conspicuous instance]*

<!-- AUTHOR-REVIEW: the fact-accuracy audit flagged "the four pluggable interfaces" as an untagged claim that no cached snapshot enumerates (the extending-Kubernetes page lists six extension points and five infrastructure plugins, with CRDs filed separately under API extensions). The phrase is a book coinage owned by Ch 17 §4, and the BINDING term ledger fixes the set as CRI + CNI + CSI + CRDs — so the cross-bearing above is correct as written and takes no source tag. The internal contradiction the audit found is in The Voyage Ahead ("you have collected two now"), which counts CRDs out; that section, not this one, is where the count needs repairing. -->

---

## 🔵 §6 — Allowing, Never Denying

One piece of housekeeping before we get under way, and it is not politeness.

**The word `ingress` is about to mean something completely different, and capitalisation is the tell.** For four sections, `Ingress` has meant an API object and the controller that fulfills it. From here to the end of §7, lowercase `ingress` means **a direction of traffic**: inbound, as opposed to `egress`, outbound. NetworkPolicy has nothing to do with the Ingress object. If you carry the old meaning into this section, you will spend §7 trying to work out how the Ingress controller fits in, and it does not.

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

For Pod- and namespace-based policies, **you use a selector to specify what traffic is allowed to and from the Pods that match the selector.** For IP-based policies, you define the rule on **IP blocks (CIDR ranges)** [source: k8s-docs-network-policies-depth-2026-08-24]. *(CIDR notation is a way of writing a range of IP addresses as an address plus a prefix length: `172.17.0.0/16` means "the addresses whose first sixteen bits are those of 172.17.0.0." An `except` list carves ranges back out of the block — in the manifest below, everything in 172.17.0.0/16 apart from the addresses in 172.17.1.0/24. The glossary carries the expansion.)*

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

**Each NetworkPolicy includes a `podSelector` which selects the grouping of Pods to which the policy applies** — here, Pods labeled `role: db` [source: k8s-docs-network-policies-depth-2026-08-24]. That is the subject. Inside the rules, a different set of selectors chooses who may connect: `podSelector` selects particular Pods in the **same namespace as the NetworkPolicy** as allowed sources or destinations, and `namespaceSelector` selects particular namespaces for which **all** Pods are allowed [source: k8s-docs-network-policies-depth-2026-08-24].

One mechanism, the label selector you learned in Chapter 4, doing two entirely different jobs in one object, at two different depths of the same YAML.

> 🪝 **Snag:** Whether `namespaceSelector` and `podSelector` appear as one `from` entry or two changes the meaning completely. A single entry specifying **both** selects particular Pods *within* particular namespaces, an AND. Two entries in the `from` array is an OR: connections from Pods in the local namespace with the peer label, **or** from any Pod at all in the matching namespaces [source: k8s-docs-network-policies-depth-2026-08-24]. One YAML hyphen is the difference. The documentation's own advice: when in doubt, use `kubectl describe` to see how Kubernetes has interpreted the policy [source: k8s-docs-network-policies-depth-2026-08-24].

### The two sorts of isolation

This is the center of the section, and the place your firewall instinct gets corrected.

There are **two sorts of isolation for a Pod: isolation for egress, and isolation for ingress.** They concern what connections may be established. "Isolation" here is **not absolute** — it means *some restrictions apply*. The alternative, "non-isolated for a direction," means that **no restrictions apply** in that direction. The two are declared independently, and both are relevant for a connection from one Pod to another [source: k8s-docs-network-policies-depth-2026-08-24].

**Egress.** By default, a Pod is **non-isolated for egress; all outbound connections are allowed.** A Pod becomes isolated for egress if there is **any** NetworkPolicy that both **selects the Pod** and has `Egress` in its `policyTypes`. When it is isolated, the only allowed outbound connections are those permitted by the `egress` list of some policy that applies to it [source: k8s-docs-network-policies-depth-2026-08-24].

**Ingress.** By default, a Pod is **non-isolated for ingress; all inbound connections are allowed.** It becomes isolated for ingress on exactly the same terms, with `Ingress` in `policyTypes`. When it is isolated, the only allowed inbound connections are **those from the Pod's node** and those permitted by the `ingress` list of some applicable policy [source: k8s-docs-network-policies-depth-2026-08-24].

Reply traffic for allowed connections is implicitly allowed in both directions [source: k8s-docs-network-policies-depth-2026-08-24], which is to say the mechanism is connection-aware, not packet-by-packet, and you do not need a return rule.

Now collect the debt from Soundings question 4. You almost certainly answered *dropped* and *the deny wins*, because that is how ordinary firewalls work and it is a good instinct nearly everywhere else. Kubernetes is the other way around on both counts. **A Pod starts fully open in both directions, and becomes restricted only because some policy went looking for it and found it.** Nothing is closed until something selects it. This is open water rather than a walled harbour: it stays open until somebody declares a restricted zone and puts you inside it.

> ★ **Fixed Point:** **By default a Pod is non-isolated in both directions.** It becomes isolated for a direction only when some NetworkPolicy both **selects it** and names that direction in `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24]. No policy means no restriction.

A note on `policyTypes`, because it has a default that catches people. Each policy includes a `policyTypes` list which may include `Ingress`, `Egress`, or both. **If no `policyTypes` are specified, `Ingress` will always be set, and `Egress` will be set if the policy has any egress rules** [source: k8s-docs-network-policies-depth-2026-08-24]. So an omitted `policyTypes` is not "neither." It is at minimum `Ingress`.

### Additive, and there is no deny

**The effects of the ingress lists combine additively. The effects of the egress lists combine additively. Network policies do not conflict; they are additive.** If any policy or policies apply to a given Pod for a given direction, the connections allowed in that direction are **the union of what the applicable policies allow.** Thus **order of evaluation does not affect the policy result** [source: k8s-docs-network-policies-depth-2026-08-24].

Sit with that for a moment, because it removes something you have relied on everywhere else.

There is **no deny rule.** None. The API has no syntax for one. Two policies selecting the same Pod produce the union of what they permit, and there is no third policy you can write that subtracts from that union. If a Pod can currently reach something and you want it not to, you do not add a denial. **You remove the grant.**

> ★ **Fixed Point:** **Policies are additive and never conflict. There is no deny rule** [source: k8s-docs-network-policies-depth-2026-08-24]. Two policies produce the union of what they permit. Removing access means removing the grant, not adding a denial.

<!-- FIGURE: ch10-fig04-networkpolicy-additive-selectors -->
![Two NetworkPolicy stanzas, A and B, both selecting Pods labelled role equals db, one permitting ingress from app equals web and the other from app equals batch. Heavy edges run from both stanzas to a single Pod box, and a single arrow runs from that Pod to a rounded blob labelled permitted set containing app equals web plus app equals batch, glossed as one set with two grants. A fourth box labelled app equals other sits unconnected, annotated as not denied but simply never granted.](figures/ch10-fig04-networkpolicy-additive-selectors.svg)

<!-- ASCII-FALLBACK
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
-->

Note what is *not* in that figure: any mark of denial. No barrier, no crossed-out arrow, no red X. The excluded Pod is excluded by the **absence of a grant**, which is a different thing from being blocked, and drawing it as blocking would contradict the Fixed Point above.

### Both ends must allow it

**For a connection from a source Pod to a destination Pod to be allowed, both the egress policy on the source Pod and the ingress policy on the destination Pod need to allow the connection. If either side does not allow the connection, it will not happen** [source: k8s-docs-network-policies-depth-2026-08-24].

This is the rule that costs practitioners the most time, because a policy that is perfectly correct in isolation is only ever half of a working configuration. You write an egress policy on `frontend` permitting traffic to `api`, you verify the YAML, you apply it, and nothing connects, because `api` has an ingress policy that never heard of `frontend`. Two harbours, two authorities: clearance to depart is not permission to enter, and a vessel holding only one of them stays at anchor.

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

And because the model is additive, the reverse also works: an explicit allow-all is a policy with `podSelector: {}` and a single empty rule, `ingress: [{}]`, which permits everything to everything even if other policies have caused some Pods to be treated as isolated [source: k8s-docs-network-policies-depth-2026-08-24]. Union semantics cut both ways: you cannot subtract, and neither can anybody else.

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

When a NetworkPolicy does nothing, **traffic flows exactly as it did before.** `kubectl get networkpolicy` shows the object. `kubectl describe` shows the rules, correctly parsed and neatly formatted. Everything you can observe about the object says it is fine, and the observable behavior of an unenforced policy is *identical* to the observable behavior of a perfectly enforced policy against traffic nobody happens to be sending. There is no signal. There is nothing to notice. One failure fires a flare; the other is an uncharted rock, and nothing on the surface says it is there.

That is not a documented claim; the source states the plugin dependency and the no-effect consequence and stops there. The characterisation of the failure as *silent*, and as harder to detect than a broken Ingress, is this book's reasoning about what those two documented facts imply. Hold the two apart: the dependency is sourced, the inference about detectability is ours. We think it is sound, it is the most valuable thing in this chapter, and it is still an inference.

> ⚠ **Navigational Hazards:** *"I applied a NetworkPolicy, so that traffic is blocked"* is only true if something is enforcing it. Verify that your network plugin supports NetworkPolicy before you rely on one, and test the restriction from somewhere the policy could actually govern rather than trusting the object's existence. The object existing is a fact about etcd.

Nothing about this is careless. You wrote a correct policy, the API accepted it, `kubectl` showed it back to you, and every signal available said the thing was working. The expectation is entirely reasonable. It is the *mechanism* that offers no feedback, and that is worth knowing about in advance precisely because you will not discover it in the moment.

### Where else could it possibly live?

You can reason your way to this dependency rather than memorising it.

Chapter 9 taught that Kubernetes **defines** the network model but provides none of the machinery that satisfies it: a CNI network plugin is required to implement the model, and it does the actual work of wiring Pods onto a network *[cross-bearing: see Ch 9 §1 — CNI and the Kubernetes network model]*. CNI is one of the interfaces where Kubernetes hands off to an implementation — and it is the container runtime, not the kubelet, that loads the plugin: CNI management was removed from the kubelet in Kubernetes 1.24 [source: k8s-docs-network-plugins-2026-08-24].

So if the plugin is what moves the packets, **where else could enforcement possibly live?** Nowhere. The dependency is not an oversight or an inconvenience. It is the only place in the stack where the machinery to enforce a layer-3/4 rule exists.

If you reasoned to something like this in Soundings question 7, you derived the *dependency* before the chapter stated it. Not the consequence — the silence is the part you had no way to predict — but the dependency itself, which is the half that makes the other half inevitable. Notice that.

### What it cannot do, stated flat

> **Dead Reckoning:** The source states this list as current "as of" whichever release you happen to be reading — a version-templated claim with no fixed version behind it, so there is no release number to pin here without asserting more than the documentation does. What follows is the list as it stood at this book's source snapshot, 24 August 2026. Treat it as a list that shrinks over time; check the current page before concluding that an item on it is still impossible [source: k8s-docs-network-policies-depth-2026-08-24].
>
> The following functionality does not exist in the NetworkPolicy API [source: k8s-docs-network-policies-depth-2026-08-24]:
>
> - Forcing internal cluster traffic to go through a common gateway.
> - Anything TLS related.
> - Node specific policies. You can use CIDR notation, but you cannot target nodes by their Kubernetes identities specifically.
> - Targeting of services by name. You can target Pods or namespaces by their labels, which is often a viable workaround.
> - Creation or management of "Policy requests" that are fulfilled by a third party.
> - Default policies which are applied to all namespaces or Pods.
> - Advanced policy querying and reachability tooling.
> - The ability to log network security events, for example connections that are blocked or accepted.
> - The ability to explicitly deny policies.
> - The ability to prevent loopback or incoming host traffic. Pods cannot block localhost access, nor can they block access from their resident node.
>
> The documentation notes that some of these may be achievable through operating-system components such as SELinux, OpenVSwitch or IPTables, through layer-7 technologies such as ingress controllers and service mesh implementations, or through admission controllers [source: k8s-docs-network-policies-depth-2026-08-24].

Ten items. Three of them earn a sentence each, because they are the ones you will actually reach for.

**No TLS.** Anything TLS related is out of scope, and the documentation says outright to use a service mesh or ingress controller for it [source: k8s-docs-network-policies-depth-2026-08-24]. §2 already told you that terminating TLS at the Ingress leaves the leg from Ingress to Pod in cleartext. NetworkPolicy will not encrypt it either. That gap has an owner *[cross-bearing: see Ch 17 §5 — service mesh, mTLS, and what a mesh adds inside the cluster]*.

**No targeting Services by name.** Policies select Pods. You can target Pods or namespaces by label, which the documentation calls a viable workaround [source: k8s-docs-network-policies-depth-2026-08-24], but you cannot write `allow traffic to the checkout Service`. This is surprising after nine chapters in which nearly everything has been Service-shaped, and it is the item on this list a reader is most likely to reach for by reflex.

**No explicit deny.** §6 taught additivity as a *property* of the model: policies grant, and the model has no subtraction operator. The out-of-scope list states that same architectural fact as a *limitation* — the ability to explicitly deny is simply not in the API [source: k8s-docs-network-policies-depth-2026-08-24]. Same fact, met from the side you will actually encounter it on. You go looking for a deny rule, and there is not one.

> 🔭 **Closer Look:** "No targeting of services by name" is stranger than it looks, and it follows directly from §6. A policy selects Pods. A Service is a stable name in front of a set of Pods that *changes*; that is the entire reason Chapter 9 gave you Services. Selecting the Service would mean selecting a moving target through an indirection that the policy layer, sitting at layer 3/4 on Pod IPs, does not have access to. The restriction is a consequence of the architecture, not an omission from the API. Deeper than the exam requires.

Two objects. Four sections apart. Nothing in common except a failure mode.

---

## ☆ Taking Your Bearings #2 — from Ingress to Gateway, and what NetworkPolicy permits once you're inside

Nine questions on §4 through §7. One of them reaches back into an earlier chapter.

**1.** ⚪ True or false, with justification: *Ingress is deprecated and will be removed in a future release.*

**2.** 🟡 Name the three role-mapped Gateway API resources and say which organizational role each belongs to.

**3.** 🟡 How many GatewayClasses is a Gateway associated with, and how many Routes can attach to one Gateway?

**4.** 🟡 A request arrives at a Gateway's IP address. Name the header the reverse proxy uses to match a configuration, and name the two optional things the HTTPRoute may do before the request is forwarded.

**5.** 🔵 `[retrieval: ch4]` Chapter 4 said a NetworkPolicy selects both its subject and its peers. Point at the two selectors in that sentence and say what each one is choosing.

**6.** 🔵 A Pod in namespace `prod` has no NetworkPolicy selecting it anywhere in the cluster. What inbound and outbound traffic is permitted?

**7.** 🟡 **⚠️ This one is intentionally hard. Struggle is the point.** Two NetworkPolicies select the same Pod. Policy A permits inbound traffic from `app: web`. Policy B permits inbound traffic from `app: batch`. What is permitted, and could a third policy be written to forbid `app: web`? If not, what would you write to close every Pod in the namespace to all inbound traffic?

**8.** 🟡 Pod `frontend` has an egress policy permitting traffic to `app: api`. Pod `api` has an ingress policy permitting traffic only from `app: admin`. Can `frontend` reach `api`?

**9.** 🔵 You apply a NetworkPolicy intended to block traffic from a specific Pod. Traffic still flows. Name two distinct explanations, one of which is not a mistake in the policy.

---

**Answers with Explanations:**

**1. False, on both counts.** Ingress has not been deprecated, and there are no plans to remove it [source: k8s-docs-ingress-depth-2026-08-24]. What has been said is narrower: it will not be developed further, and the project recommends Gateway instead [source: k8s-docs-ingress-depth-2026-08-24]. That is a recommendation, not a removal notice. "No longer developed" *feels* like deprecation, and that feeling pulls readers toward the wrong verdict. Deprecation in Kubernetes is a formally defined process with published removal timelines [source: k8s-docs-deprecation-policy-2026-08-24], and the project did not invoke it here. The stability half matters because it removes any migration emergency; the no-development half matters because it caps future capability.

**2. GatewayClass — infrastructure provider. Gateway — cluster operator. HTTPRoute — application developer** [source: k8s-docs-gateway-api-depth-2026-08-24]. Asked as a mapping, not a list — the mapping *is* the design. The three names without the three roles means you've memorised the consequence, missed the cause. One precision the answer key insists on: "cluster operator" here is a role — a team running the cluster — not the operator pattern. The word does double duty in Kubernetes vocabulary, and this is the one place in the book where both senses are in play.

**3. Exactly one GatewayClass. Many Routes** [source: k8s-docs-gateway-api-depth-2026-08-24]. The wrong answer to watch for is Ingress-shaped: one object there carries both the entry point and every routing rule, so it's natural to expect a Gateway to work the same way. It doesn't. Routes attach from outside, and — per question 2 — they belong to a different role than the Gateway does.

**4. The `Host:` header. Then, optionally: header and/or path matching from the HTTPRoute's match rules, and optional modification of the request from its filter rules** [source: k8s-docs-gateway-api-depth-2026-08-24]. The wrong answer to watch for is *the path* — recency pulls readers there, since path matching got far more coverage than hosts. But the `Host:` header selects the configuration first; path and header matching are optional steps that happen after that selection is already made.

**5. `[retrieval: ch4]` The policy's own top-level `podSelector` chooses which Pods the policy applies to. The selectors inside its rules — `podSelector` and `namespaceSelector` under `from`/`to` — choose which Pods and namespaces those Pods may talk to.** Each NetworkPolicy includes a `podSelector` selecting the Pods it applies to [source: k8s-docs-network-policies-depth-2026-08-24]; separately, the selectors inside an `ingress from` or `egress to` section select allowed sources or destinations [source: k8s-docs-network-policies-depth-2026-08-24]. One mechanism, two jobs — the structural insight the rest of this material is built on.

**6. All of both — the Pod is non-isolated for ingress and for egress.** A Pod is non-isolated in both directions by default, and becomes isolated only when some policy both selects it and names that direction in `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24]. Reject explicitly: *"no policy means no traffic."* That's the firewall instinct, and it's exactly backwards — the single most consequential wrong belief a reader can bring here.

**7. Inbound from both `app: web` and `app: batch` — the lists combine additively.** No: there is no deny rule, so nothing can subtract a permission; removing access means removing the grant. Network policies do not conflict — connections allowed in a direction are the union of what applicable policies allow [source: k8s-docs-network-policies-depth-2026-08-24], and explicit deny is on the published out-of-scope list [source: k8s-docs-network-policies-depth-2026-08-24]. The model has no subtraction operator: permissions compose by union only, order is irrelevant, and the only way to reduce what's permitted is to change what grants it. To close the namespace: a policy selecting every Pod (an empty `podSelector` selects them all [source: k8s-docs-network-policies-depth-2026-08-24]), naming `Ingress`, offering no `from` entries. The union of an empty set of grants is empty. Denial is reached by selecting broadly and granting nothing — never by forbidding.

**8. No.** A connection needs both the source's egress policy and the destination's ingress policy to allow it; if either side doesn't, it fails [source: k8s-docs-network-policies-depth-2026-08-24]. `frontend`'s egress is correct and irrelevant on its own — `api` never granted it anything. A clearance to depart isn't a clearance to enter; the far harbour issues its own.

**9. Either the network plugin doesn't implement NetworkPolicy, so the resource has no effect at all — or the traffic falls under an unconditional exception: a Pod cannot block access to itself, and traffic to and from its own node is always allowed** [source: k8s-docs-network-policies-depth-2026-08-24]. The object may be perfect and still inert — a move most troubleshooting instincts don't make, since the reflex is to re-read the YAML. A policy that isn't enforced looks exactly like a policy enforced against traffic nobody is sending. There's no observable difference.

---

**Checkpoint: You've Now Mastered**

✓ *Frozen* and *deprecated*, precisely, in both halves
✓ Gateway API's role-oriented design, and the resources that fall out of it
✓ The cardinality, and the request flow end to end
✓ Non-isolated by default, in both directions, until something selects
✓ Additive, allow-only, no deny rule, order-independent
✓ Denial by construction — select everything, grant nothing
✓ Both ends must allow it
✓ The plugin dependency, and the ten things the API cannot do


## ☀️ §8 — Nothing Happens Without a Controller

This chapter taught two objects that have nothing to do with each other.

One routes HTTP by hostname and path at the edge of the cluster, at layer 7, for traffic coming in from outside. The other permits and forbids TCP connections between Pods inside it, at layers 3 and 4, for traffic that never leaves. Different layers. Different directions. Different problems. In most organizations, different teams.

And they fail the same way.

Write either one perfectly. Apply it successfully. Watch `kubectl get` return it. And nothing happens, because in one case no Ingress controller is installed, and in the other the network plugin does not implement NetworkPolicy.

> ☀️ **Zenith:**
>
> You have now seen this four times, and two of the four were your own from last chapter.
>
> A `type: LoadBalancer` Service with no provider to fulfill it. A Service whose selector matched no Pods. An Ingress with no controller. A NetworkPolicy on a plugin that does not implement one.
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

<!-- AUTHOR-REVIEW: the Ch 3 §6 cross-bearing below nests *why* and *that* inside the convention's own italic span, which breaks emphasis in most renderers and departs from the ratified `*[cross-bearing: see Ch N §M — brief topic]*` form. Structural lint passes it. Recommend recasting the topic without inner emphasis, or dropping the trailing clause. Not changed here — no diagnostic finding names it. -->
*[cross-bearing: see Ch 3 §6 — the control loop, which is *why* this is true rather than merely *that* it is]*
*[cross-bearing: see Ch 4 §1 — the declarative model, and the object as an artifact of intent]*

> ⚓ **Worth Securing:** You now own a question you can ask about anything: **what is watching this, and is it installed?**
>
> Chapter 13 will hand you a cluster where `kubectl top` returns an error, and the answer is metrics-server *[cross-bearing: see Ch 13 §7 — the resource metrics pipeline]*. Chapter 17 will hand you VPA, which is an addon and is not shipped by default *[cross-bearing: see Ch 17 §7 — the autoscaling landscape]*. Those two are the instances §3 was counting toward when it called this the first of four; the count above runs the other way, backward over the four already behind you. Chapter 3 published both of those pointers before you had any of the evidence. You have the evidence now.
>
> It also works on objects this book never mentions, which is the actual return on this chapter.

<!-- FIGURE: ch10-zenith-nothing-without-a-controller -->
![Four side-by-side panels, each with three rows. The top row names a valid object: a LoadBalancer Service, a Service with an empty selector, an Ingress with host and path rules, and a NetworkPolicy with a pod selector. The middle row of each panel shows a dashed, ghosted box naming an absent component — provider, matching Pods, Ingress controller, network plugin — each marked none. The bottom row reads nothing in all four panels; the fourth panel adds the words and nothing tells you. A caption reads: an object without its component does nothing.](figures/ch10-zenith-nothing-without-a-controller.svg)

<!-- ASCII-FALLBACK
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
-->

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
4. **The project recommends using Gateway instead of Ingress.** That is the recommendation as written — it carries no qualifier about new work or existing work. Reading it as *use Gateway for new work* is this book's operational gloss, not the project's wording; §4 sets out why that reading is fair and what it does not license.
5. **Simple fanout routes by URI; name-based virtual hosting routes by host.** Both put many Services behind one address.
6. **An Ingress may terminate TLS**, using a Secret that contains a private key and certificate; traffic onward to the Pods is cleartext.
7. **A Pod is non-isolated in both directions by default.** All ingress and all egress allowed.
8. **Policies are additive and never conflict. There is no deny rule.**
9. **Both ends must allow the connection** — the source's egress and the destination's ingress.
10. **NetworkPolicies are implemented by the network plugin.** No supporting plugin, no effect.
11. **GatewayClass / Gateway / HTTPRoute**, mapped to infrastructure provider / cluster operator / application developer. Exactly one GatewayClass per Gateway; many Routes.
12. **Node-local traffic is always allowed, and a Pod cannot block access to itself.**

**Common Traps** — each one has a specific wrong belief behind it, and the correction is the thing to carry into the exam room.

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
| "Gateway API is a rename of Ingress" | Different API, different resource model, built around a different organizing principle. |
| "NetworkPolicy can target a Service" | It selects Pods. Targeting Services by name is explicitly out of scope. |
| "An Ingress controller and a NetworkPolicy plugin are unrelated concerns" | Functionally unrelated. Structurally identical — which is §8. |

**A note on frequency.** Every trap above is a real point of confusion, drawn from the documentation's own emphases and from what the material makes easy to get wrong. What this book will not tell you is how often any of them appears on the exam. The published curriculum gives four domain weights and nothing finer [source: cncf-kcna-curriculum-pdf-2026-08-23] — no question counts, no per-competency split, nothing that would let anyone honestly attach a number to a single trap. Inventing one would be worse than saying nothing.

<!-- AUTHOR-REVIEW: The stronger negative claim in the prior draft — that "the exam's question distribution is not published" anywhere — cannot be verified against the cached corpus, which holds no exam-logistics snapshot at all (no question count, duration, passing score, or distribution). The sentence has been narrowed to what `cncf-kcna-curriculum-pdf-2026-08-23` actually supports: the curriculum publishes four domain-level percentages and nothing finer. Restoring the broader claim requires a research gap for the Linux Foundation KCNA exam/registration page. -->

---

## Practice Questions

Nineteen questions, four options each. Four draw on earlier chapters, and they are tagged. Answers follow the full set — attempt them all before scrolling.

**1.** ⚪ Three mechanisms, three altitudes. At which OSI layer does each operate: the Service types from Chapter 9, an Ingress, and a NetworkPolicy?

A) Services at layer 4; Ingress at layer 7; NetworkPolicy at layer 7.
B) Services at layer 4; Ingress at layer 7; NetworkPolicy at layer 3 or 4.
C) Services at layer 3; Ingress at layer 4; NetworkPolicy at layer 3.
D) All three at layer 7, differing only in what they are permitted to configure.

**2.** 🔵 `[retrieval: ch9]` You need to expose an HTTP application and a message broker speaking its own binary protocol, both to clients outside the cluster. What do you need?

A) One Ingress carrying both, with a ClusterIP Service behind each.
B) One Ingress for the HTTP application with a ClusterIP Service behind it; a NodePort or LoadBalancer Service for the broker.
C) Two Ingresses, one per workload, each with a ClusterIP Service behind it.
D) No Ingress — a LoadBalancer Service for each, since an Ingress routes to Pods and both workloads have several.

**3.** ⚪ Which set correctly lists what an Ingress may be configured to provide?

A) Externally-reachable URLs for Services; load balancing; SSL/TLS termination; name-based virtual hosting.
B) Externally-reachable URLs for Services; load balancing; SSL/TLS termination; exposure of arbitrary TCP and UDP ports.
C) Externally-reachable URLs for Services; enforcement of which Pods may receive the traffic; SSL/TLS termination; name-based virtual hosting.
D) Externally-reachable URLs for Services; load balancing; end-to-end TLS all the way to the Pods; name-based virtual hosting.

**4.** 🔵 An Ingress rule has `host: shop.example.com` and two path entries, `/catalog` and `/checkout`, each naming a different backend Service. Which shape is this, and what is the rule reading in order to decide?

A) Name-based virtual hosting; the rule is reading the `Host:` header.
B) Simple fanout; the rule is reading the HTTP URI — the path.
C) A single-service Ingress; the rule reads nothing, because `defaultBackend` sends everything to one Service.
D) Name-based virtual hosting; the rule is reading the path, because a `host` is present.

**5.** 🟡 An Ingress path is configured with `pathType: Prefix` and `path: /aaa/bb`. A request arrives for `/aaa/bbb`. Does it match?

A) Yes — `bb` is a prefix of `bbb`, and that is what `Prefix` means.
B) No — `Prefix` matches element by element, and `bb` and `bbb` are different elements.
C) No — `Prefix` matches only the configured path itself and nothing longer.
D) Undeterminable from the manifest, because `pathType` semantics are left to the controller.

**6.** ⚪ A cluster runs one Ingress controller. An engineer applies an Ingress manifest with no `ingressClassName` field. Under what condition does it still get handled?

A) Whenever at least one IngressClass exists in the cluster.
B) When exactly one IngressClass is marked as default, by the `ingressclass.kubernetes.io/is-default-class` annotation set to `"true"`.
C) Always — with one controller installed, there is nothing else the Ingress could mean.
D) Never — `ingressClassName` is a required field and the manifest will be rejected.

**7.** 🔵 `[retrieval: ch3]` Chapter 3 said a controller watches for objects and drives reality toward what they describe. An Ingress controller is one. What does it watch, and what does it change?

A) It watches Ingress objects and the Services they reference, and changes a load balancer — or the edge router, or additional frontends — to match.
B) It watches Ingress objects and changes the Services they reference.
C) The API server watches Ingress objects and configures the load balancer; the controller only validates the manifest.
D) It watches Pods and changes the Ingress object's status to match.

**8.** 🔵 Two objects, both correct as written, both doing nothing: an Ingress on a cluster with no Ingress controller, and a NetworkPolicy on a cluster whose network plugin does not implement NetworkPolicy. What is absent in each, and in what one respect do the two situations differ?

A) The controller and the plugin. They differ in nothing that matters — both fail identically.
B) The controller and the plugin. They differ in what you can see: one produces traffic that visibly fails to arrive, the other produces no signal at all.
C) A `defaultBackend` and an `ipBlock`. Both objects are incomplete as written.
D) The controller and the plugin. They differ in that the Ingress is rejected at admission and the NetworkPolicy is accepted.

**9.** ⚪ What has the Kubernetes project said about the Ingress API, in both of its halves?

A) That it is deprecated, and scheduled for removal in a future release.
B) That it is generally available and subject to the stability guarantees for GA APIs with no plans for removal — and that it is no longer being developed, with no further changes or updates.
C) That it is generally available, fully supported, and actively developed for new work.
D) That it is no longer being developed, and therefore deprecated by definition.

**10.** 🔵 You are choosing an API for external HTTP routing on a system being designed today. Which does the Kubernetes project recommend, and does that recommendation mean the other one will stop working?

A) Gateway. Yes — Ingress will be removed once Gateway API reaches GA.
B) Gateway. No — Ingress is GA, carries the GA stability guarantees, and has no removal plans.
C) Ingress, because it is GA and Gateway API is not present in a default cluster.
D) Neither; the project is explicitly neutral between the two.

**11.** 🟡 Express one requirement twice — one host, two paths, two backend Services — first in the Ingress vocabulary, then in the Gateway API vocabulary, with the owning role for each Gateway API resource.

A) Ingress: one Ingress with one rule and two paths. Gateway API: one Gateway with two paths — the same object renamed, owned by the application developer.
B) Ingress: one Ingress with one rule and two paths, plus the two Services and a controller to fulfill it. Gateway API: a GatewayClass (infrastructure provider), a Gateway (cluster operator), and an HTTPRoute with two path matches and two `backendRefs` (application developer).
C) Ingress: one Ingress per path, so two. Gateway API: one HTTPRoute per path, so two, both owned by the cluster operator.
D) Ingress: one Ingress and one IngressClass. Gateway API: one Gateway and one GatewayClass — HTTPRoute being the Gateway API name for an IngressClass.

**12.** 🔵 In Gateway API, how many GatewayClasses does a Gateway reference, and how many Routes may attach to one Gateway?

A) Exactly one GatewayClass; many Routes.
B) Many GatewayClasses; exactly one Route.
C) Exactly one of each.
D) Many of each.

**13.** 🔵 A Pod is selected by a NetworkPolicy whose `policyTypes` lists only `Ingress`. What is permitted outbound from that Pod?

A) All outbound traffic.
B) No outbound traffic — declaring one direction isolates both.
C) Outbound traffic only to Pods in the same namespace.
D) Outbound traffic only to the peers named in the policy's `ingress` list, applied in reverse.

**14.** 🟡 Namespace `prod` contains Pods `web`, `api`, and `db`. One NetworkPolicy exists: it selects `db` and permits ingress from `app: api`. It declares no egress rules. Can `web` reach `db`? Can `web` reach `api`? Can `db` reach an external address?

A) No · Yes · Yes
B) No · No · Yes
C) No · No · No
D) Yes · Yes · No

**15.** 🟡 An engineer wants to stop a Pod labeled `app: legacy` from reaching the `payments` Pods. Two existing policies currently permit that traffic. What is the approach?

A) Write a more restrictive policy selecting `payments` that excludes `app: legacy`; the more restrictive policy wins.
B) Find and remove or narrow the two policies that currently permit it. There is no deny policy to write.
C) Add a deny rule naming `app: legacy` to one of the two existing policies.
D) Apply a policy selecting `app: legacy` with `policyTypes: [Egress]` and an empty egress list, which removes only its access to `payments`.

**16.** 🟡 `[retrieval: ch4]` A single NetworkPolicy carries a selector at the top of its `spec` and further selectors underneath `ingress.from`. Which chooses what — and what happens to the policy's effect on a Pod if someone relabels that Pod out from under the top-level selector?

A) The top-level `podSelector` chooses the Pods the policy governs; the selectors under `ingress.from` choose peers. Relabelling drops the Pod out of the policy's subjects, leaving it non-isolated — less restricted, not more.
B) The top-level `podSelector` chooses the Pods the policy governs; the selectors under `ingress.from` choose peers. Relabelling drops the Pod out of every policy, and a Pod outside every policy receives nothing.
C) The selectors under `ingress.from` choose the Pods the policy governs; the top-level `podSelector` chooses peers. Relabelling changes nothing about the policy's subjects.
D) All the selectors choose peers; the policy governs the whole namespace. Relabelling narrows the peer set.

**17.** 🔵 A NetworkPolicy has been applied. The policy is correct as written, and traffic it should be blocking is still flowing. Three of the four explanations below are ones this chapter has given you. Which is the one that **cannot** be the explanation?

A) The cluster's network plugin does not implement NetworkPolicy, so the resource has no effect.
B) The traffic is node-local, or the Pod is reaching itself — neither can be blocked by any policy.
C) Another policy in the namespace permits the same traffic, and policies combine by union.
D) The policy targets the destination Service rather than the Pods behind it, so it selects nothing.

**18.** 🟡 `[retrieval: ch3]` Name the rule Chapter 3 gave you about objects and components, and every instance of it you have met in this book so far.

A) *An object without its component does nothing.* Instances: a `type: LoadBalancer` Service with no provider to fulfill it (Ch 9 §3); a Service whose selector matches no Pods (Ch 9 §4); an Ingress with no Ingress controller (Ch 10 §3); a NetworkPolicy on a plugin that does not implement NetworkPolicy (Ch 10 §7).
B) *An object without its component does nothing.* Instances: an Ingress with no Ingress controller, and a NetworkPolicy on a plugin that does not implement NetworkPolicy.
C) *An object takes effect once the API server has admitted it.* Instances: the four above.
D) *An object without its component does nothing.* Instances: a `type: LoadBalancer` Service with no provider; an Ingress with no controller; a NetworkPolicy on an unsupporting plugin; an Ingress whose `pathType` does not match the request path.

---

**19.** ⚪ A cluster runs a frontend Pod that receives requests from users on the internet and, to serve them, calls a backend Pod in the same cluster. Which describes the two flows, and which of this chapter's mechanisms governs each?

A) Both are north-south; Ingress governs the first, NetworkPolicy the second
B) The user-to-frontend flow is north-south and is governed by Ingress; the frontend-to-backend flow is east-west and is governed by NetworkPolicy
C) The user-to-frontend flow is east-west and is governed by Ingress; the frontend-to-backend flow is north-south and is governed by NetworkPolicy
D) Both are east-west, because both flows terminate inside the cluster

---

### Answers with Explanations

**1. B.**

The documentation attaches OSI layer numbers to exactly one of these three: network policies control traffic flow at the IP address or port level — OSI layer 3 or 4 [source: k8s-docs-network-policies-depth-2026-08-24]. The layer numbering for Services and Ingress is ordinary practitioner vocabulary rather than a documented label; what is documented is the capability difference. Ingress is described as protocol-aware HTTP/HTTPS routing using URIs, hostnames and paths, set against `type: LoadBalancer` as the simpler, less-configurable path [source: k8s-docs-network-model-2026-08-23].

The shape worth carrying out of the chapter is the round trip. §2 through §5 climb to where the request itself is readable. §6 descends again, and the descent is why §7's limits are the limits they are.

*Why A is wrong:* it puts NetworkPolicy at layer 7. That is the error behind every expectation that a policy can match a hostname, a URL path, or a Service name — and every one of those is on the published out-of-scope list precisely because the mechanism is not up there.

*Why C is wrong:* it demotes Ingress to layer 4, which would make it a variant of the Service types rather than a different altitude. If that were true, the broker in question 2 could go behind it.

*Why D is wrong:* it collapses the distinction the whole chapter is built on. A mechanism that cannot read the request cannot route on its contents, no matter what it is permitted to configure.

**2. B.** `[retrieval: ch9]`

An Ingress does not expose arbitrary ports or protocols; exposing services other than HTTP and HTTPS typically uses NodePort or LoadBalancer [source: k8s-docs-ingress-depth-2026-08-24]. The HTTP application still needs a Service behind the Ingress — an Ingress backend is a combination of Service and port, which is the case this chapter covers, rather than a Pod [source: k8s-docs-ingress-depth-2026-08-24] — and a ClusterIP is sufficient, because the Ingress is what makes it externally reachable.

The point of the item is **specialization, not replacement.** A candidate who believes Ingress supersedes the Service ladder goes looking for a way to put the broker behind the Ingress, and there is not one.

*Why A is wrong:* it is the specialization error in its purest form. The Ingress cannot carry the broker at all, so no arrangement of Services behind it helps.

*Why C is wrong:* two Ingresses do not solve a protocol problem. Adding a second one that also cannot carry binary traffic changes nothing.

*Why D is wrong:* the premise is false. An Ingress routes to a Service and port, not to individual Pods, so "several Pods" is not an obstacle — that is what the Service is for.

**3. A.**

An Ingress may be configured to give Services externally-reachable URLs, load balance traffic, terminate SSL/TLS, and offer name-based virtual hosting [source: k8s-docs-ingress-depth-2026-08-24].

*Why B is wrong:* arbitrary TCP and UDP ports are the fifth thing people assume is on the list and the one thing explicitly excluded — exposing services other than HTTP and HTTPS typically uses NodePort or LoadBalancer instead [source: k8s-docs-ingress-depth-2026-08-24]. This is the single most common wrong answer about what an Ingress is for.

*Why C is wrong:* deciding which Pods may receive traffic is NetworkPolicy's job, and it lives at a different layer entirely. An Ingress routes; it does not authorize.

*Why D is wrong:* the Ingress resource assumes TLS termination at the ingress point — traffic onward to the Service and its Pods is in cleartext [source: k8s-docs-ingress-depth-2026-08-24]. "End-to-end TLS to the Pods" is the opposite of what terminating TLS means, and the distinction matters the moment anyone asks what is on the wire inside the cluster.

**4. B.**

A fanout configuration routes traffic from a single IP address to more than one Service based on the HTTP URI being requested [source: k8s-docs-ingress-depth-2026-08-24].

*Why A is wrong:* virtual hosting splits on **host**, and here there is only one host to split on. The tell is where the list lives in the manifest: several entries under `paths` is fanout; several entries under `rules`, each with its own `host`, is virtual hosting.

*Why C is wrong:* `defaultBackend` handles requests that match none of the rules, and if no `.spec.rules` are specified then `.spec.defaultBackend` must be [source: k8s-docs-ingress-depth-2026-08-24]. This manifest has rules and paths, so the rules do the deciding; the default backend is a fallback, not the mechanism.

*Why D is wrong:* it gets the mechanism right and the name wrong, which is the more dangerous half of the error. The presence of a `host` does not make something virtual hosting — *several* hosts do.

**5. B.**

`Prefix` matching is done on a **path element by path element** basis, and the documentation gives this exact case: `Prefix` with path `/aaa/bb` against request path `/aaa/bbb` is **not** a match [source: k8s-docs-ingress-depth-2026-08-24]. The elements are compared as whole labels. That `bb` happens to be a string prefix of `bbb` is irrelevant.

*Why A is wrong:* this is the misconception the rule exists to prevent, and the documentation heads it off explicitly — if the last element of the path is a substring of the last element in the request path, it is not a match [source: k8s-docs-ingress-depth-2026-08-24].

*Why C is wrong:* it over-corrects. `Prefix` does match longer request paths — `/aaa/bb/cc` matches — provided every configured element matches a whole element of the request.

*Why D is wrong:* controllers do vary in documented ways, but this is not one of them. `Prefix` semantics are pinned by the specification with a worked example. Reaching for "it depends on the controller" where the spec is explicit is the caveat from §3 applied somewhere it does not belong.

**6. B.**

If `ingressClassName` is omitted and exactly one default IngressClass exists, Kubernetes applies it, and an IngressClass is marked as default by setting the `ingressclass.kubernetes.io/is-default-class` annotation to `"true"` [source: k8s-docs-ingress-controllers-2026-08-24].

Note the "exactly one." The condition is not "at least one."

*Why A is wrong:* an IngressClass existing is not the same as an IngressClass being marked default. The annotation is the whole mechanism.

*Why C is wrong:* the number of controllers installed is not what the rule is written against. The cluster resolves the class from the IngressClass resources, not by inferring that there is only one candidate.

*Why D is wrong:* `ingressClassName` is optional, which is exactly why the default-class mechanism exists.

**7. A.**

An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends [source: k8s-docs-ingress-depth-2026-08-24]. That is Chapter 3's control-loop shape with the nouns filled in: desired state recorded in an object, a controller watching, external reality reconciled toward the description.

The value of the item is in converting a memorised component name into a recognized instance of a pattern.

*Why B is wrong:* the controller reads the Services to learn where to send traffic. It does not modify them. Reversing this makes the Ingress sound like a mutation of the Service layer rather than a layer above it.

*Why C is wrong — and this is the misconception worth naming:* the API server stores the object and serves it back. It changes nothing outside the cluster. That distinction *is* the difference between a record and a control loop, and it is the reason an Ingress with no controller sits there looking perfectly healthy.

*Why D is wrong:* it inverts the direction of the loop. The object is the input, not the output.

**8. B.**

Both are the same structural failure. Only creating an Ingress resource has no effect [source: k8s-docs-ingress-depth-2026-08-24]; network policies are implemented by the network plugin, and creating a NetworkPolicy resource without a controller that implements it will have no effect [source: k8s-docs-network-policies-depth-2026-08-24]. In both cases nothing is wrong with the object at all, which is why re-reading the YAML produces nothing, indefinitely.

The difference is what reaches you. A website that does not load is a report; nobody has to go looking. Traffic that flows when a policy says it should not produces no report from anyone, because the only party who would notice is the traffic you were trying to stop.

*One clarification on provenance:* the two "no effect" facts are documented. The characterisation of the second failure as the harder one to detect is this book's reasoning about what those two facts imply, not a documented claim.

*Why A is wrong:* structurally identical, operationally not. Treating them as the same failure is what leaves the second one running for months.

*Why C is wrong:* neither object is incomplete. A `defaultBackend` is optional when rules are present, and `ipBlock` is one of three peer identifiers, not a requirement. The whole point is that both manifests review clean.

*Why D is wrong:* the API server admits both. It stores objects; it does not check that something exists to act on them. If it rejected an Ingress on a controller-less cluster, this chapter's central pattern would not exist.

**9. B.**

Both halves, in the project's own words: generally available and subject to the stability guarantees for GA APIs, with no plans for removal; and no longer being developed, with no further changes or updates [source: k8s-docs-ingress-depth-2026-08-24].

Operationally, the first half means there is no migration emergency for what you run today. The second means there is no future capability — whatever Ingress cannot do now, it never will.

*Why A is wrong:* it drops the stability half and replaces it with the wrong status. `deprecated` is a formal state with published consequences, and Ingress has not been given it.

*Why C is wrong:* it drops the no-development half. "Fully supported" is true; "actively developed" is the part the announcement specifically denies.

*Why D is wrong:* it fuses the two halves into a conclusion neither supports. No longer being developed says nothing about removal. GA APIs may be marked deprecated, but must not be removed within a major version of Kubernetes [source: k8s-docs-ingress-depth-2026-08-24] — and Ingress has not been marked deprecated in the first place.

Offering only one of A or C would teach the other, which is why a well-built item offers both.

**10. B.**

The Kubernetes project recommends using Gateway instead of Ingress [source: k8s-docs-ingress-depth-2026-08-24]. It simultaneously states that Ingress is GA, carries the GA stability guarantees, and has no removal plans [source: k8s-docs-ingress-depth-2026-08-24]. Both facts are true at once and point in different directions, and holding both is the skill this section tests. The practical reading — that the recommendation bites hardest on work being designed today, and least on work already running — is this book's gloss, not the project's wording.

*Why A is wrong:* Ingress is already GA and already guaranteed. There is no removal event waiting on Gateway API's maturity.

*Why C is wrong:* GA status is not a recommendation, and installation friction is not either. Gateway API arrives as custom resources rather than in a default cluster [source: k8s-docs-gateway-api-depth-2026-08-24], which is a real operational cost — and it is a separate question from what the project recommends.

*Why D is wrong:* the recommendation is explicit and unqualified. Reading neutrality into it is the mirror error of reading a deprecation into it.

**11. B.**

Ingress vocabulary: one Ingress object, one rule containing two paths, each naming a backend Service and port — plus the two Services and an Ingress controller to fulfill it [source: k8s-docs-ingress-depth-2026-08-24].

Gateway API vocabulary: a GatewayClass belonging to the infrastructure provider, a Gateway belonging to the cluster operator, and an HTTPRoute attached to that Gateway via `parentRefs`, carrying two path matches and two `backendRefs`, belonging to the application developer [source: k8s-docs-gateway-api-depth-2026-08-24].

The exercise is worth doing because it shows Gateway API is not a new routing model to learn from scratch. It is the shapes you already know, redistributed across resources that belong to different owners. The routing requirement did not change. The ownership boundaries did.

*Why A is wrong — and it is the tempting one:* it reads Gateway API as a rename of Ingress. It is not. Ingress is one object with one owner; Gateway API is three objects with three owners, and that split is the reason the API exists at all. A candidate who believes it is a rename will not be able to say why anyone bothered.

*Why C is wrong:* neither API needs one object per path. An Ingress rule holds many paths; an HTTPRoute holds many matches. And routes belong to the application developer, not the cluster operator — collapsing the roles is the same error as A wearing different clothes.

*Why D is wrong:* HTTPRoute is not the Gateway API analogue of IngressClass. GatewayClass is. HTTPRoute is where the routing rules live, which in the Ingress vocabulary is the Ingress object itself.

**12. A.**

A Gateway references exactly one GatewayClass, and Routes attach to Gateways rather than the other way round, so a single Gateway carries many [source: k8s-docs-gateway-api-depth-2026-08-24].

The cardinality is the kind of detail multiple-choice exams reach for, and it also encodes the role split. One GatewayClass per Gateway, because the infrastructure provider defines one kind of thing and the cluster operator instantiates it. Many Routes per Gateway, because many application teams share one entry point without asking each other's permission — which is the problem the three-role design was drawn to solve.

<!-- AUTHOR-REVIEW: the "exactly one GatewayClass" half is stated directly by the snapshot. The "many Routes" half is the reading §5 gives of the resource model rather than a counted statement in the source; Stage 2 note #10 flagged the same wording drift in §5 and left it. If a later pass tightens §5's phrasing, tighten this key to match. -->

*Why B is wrong:* it inverts both. A Gateway that could reference many classes would have no defined infrastructure behind it, and a Gateway limited to one Route would reproduce exactly the per-Service cost problem §1 opened with.

*Why C is wrong:* one Route per Gateway is the same cost problem again, and it would make the application-developer role meaningless — every new route would require a cluster operator.

*Why D is wrong:* many GatewayClasses per Gateway would leave the infrastructure ambiguous. The class is what determines the implementation.

**13. A.**

A Pod is isolated for egress only if some NetworkPolicy both selects it and has `Egress` in its `policyTypes` [source: k8s-docs-network-policies-depth-2026-08-24]. This policy names only `Ingress`, so it does not isolate the Pod for egress at all, and the default — non-isolated, all outbound connections allowed [source: k8s-docs-network-policies-depth-2026-08-24] — still stands.

*Why B is wrong:* the two directions are declared independently. Restricting one says nothing about the other, and this is the most reliably mis-answered fact in the section.

*Why C is wrong:* namespace boundaries are not a default. Nothing about declaring ingress isolation creates an egress rule of any shape, namespace-scoped or otherwise.

*Why D is wrong:* ingress rules are not applied in reverse to egress. They govern one direction, and they govern it only because `Ingress` is named in `policyTypes`.

**14. A.**

Take them one at a time.

`web` → `db`: **no.** `db` is selected by a policy naming `Ingress`, so it is isolated for ingress, and the only inbound connections permitted are those from its node and those the policy's ingress list allows — which is `app: api` only [source: k8s-docs-network-policies-depth-2026-08-24].

`web` → `api`: **yes.** `api` is selected by no policy at all, so it remains non-isolated for ingress and all inbound is allowed [source: k8s-docs-network-policies-depth-2026-08-24]. `web` is itself unselected, so it is non-isolated for egress. Both ends allow it, which is what a connection needs.

`db` → external: **yes.** The policy declares no egress rules, and if no `policyTypes` are specified then `Ingress` is set by default [source: k8s-docs-network-policies-depth-2026-08-24]. `db` is not isolated for egress, so all outbound connections are allowed.

*Why B is wrong:* it gets `web` → `api` backwards. This is the trap — assuming one policy in a namespace changes the *namespace's* posture. It changes exactly one Pod's posture, in exactly one direction.

*Why C is wrong:* it extends the same error to `db`'s outbound traffic, treating the policy as a wall around the namespace rather than a statement about one Pod's inbound connections.

*Why D is wrong:* it swaps the directions — permitting the inbound connection the policy restricts and restricting the outbound one it never mentions.

**15. B.**

Policies are additive and combine by union [source: k8s-docs-network-policies-depth-2026-08-24], and the ability to explicitly deny is on the published out-of-scope list. If two policies permit the traffic, the only way to stop permitting it is to stop permitting it — remove the grants, or narrow them so `app: legacy` falls outside.

*Why A is wrong:* this is the specific shape a firewall-experienced engineer's mistake takes, and it deserves an explicit answer rather than a shrug. There is no precedence between policies. A new policy does not override an old one, no matter how narrow it is; it adds its allowances to theirs. The correction is not "you wrote it wrong." It is "there is no such rule to write."

*Why C is wrong:* the API has no deny verb to add. A policy expresses what is permitted; there is nowhere in the schema to say what is not.

*Why D is wrong, and this one is close enough to be worth slowing down for:* selecting `app: legacy` with `policyTypes: [Egress]` and an empty egress list *does* work — it isolates the Pod for egress and permits nothing outbound. That is the default-deny idiom, applied correctly. What it does not do is remove *only* its access to `payments`. It removes access to everything, including DNS. The mechanism is right; the claim about its scope is wrong, and the scope is the whole question.

**16. A.** `[retrieval: ch4]`

The top-level `podSelector` in a policy's `spec` chooses which Pods the policy governs. The selectors underneath `ingress.from` — `podSelector` and `namespaceSelector` there — choose which peers are permitted [source: k8s-docs-network-policies-depth-2026-08-24]. Same selector grammar from Chapter 4, two entirely different jobs, distinguished only by where they sit in the document. (The third peer identifier, `ipBlock`, is not a selector at all — it names CIDR ranges, which have no labels to select on.)

Relabel a Pod out from under the top-level selector and the policy stops selecting it. It is not partially governed or governed by a narrower rule. It is outside the policy, and since a Pod is isolated only because some policy selects it, it reverts to non-isolated: all inbound allowed [source: k8s-docs-network-policies-depth-2026-08-24].

That consequence is worth sitting with, because it runs against the instinct. Editing a label — usually the safest change anyone makes — can make a Pod **less** restricted, and nothing about the operation announces that it has done so.

*Why B is wrong:* it has the mechanism right and the consequence exactly backwards. A Pod selected by no policy is not closed; it is open. This is trap #48 arriving through a side door, and if you chose B, that is the reflex to name.

*Why C is wrong:* it inverts the two positions. Under that reading, the peers would be governed and the governed Pods would be permitted — which would make every policy in the chapter mean the opposite of what it says.

*Why D is wrong:* a policy governs the Pods its top-level selector matches, never the namespace wholesale. An empty `podSelector` selects every Pod in the namespace, but that is a selector doing its job, not a default.

**17. D.**

A NetworkPolicy selects Pods. It has no field that names a Service, and targeting Services by name is on the published out-of-scope list [source: k8s-docs-network-policies-depth-2026-08-24]. So D is not a policy that is failing — it is a policy that cannot be written. If someone reports having written it, they have written something else.

The other three are all live:

**A** is §7's case. Network policies are implemented by the network plugin, and creating a NetworkPolicy resource without a controller that implements it will have no effect [source: k8s-docs-network-policies-depth-2026-08-24].

**B** is §6's pair of unconditional exceptions — traffic from a Pod's own node, and a Pod reaching itself, are permitted regardless of any policy [source: k8s-docs-network-policies-depth-2026-08-24].

**C** is union semantics doing what union semantics do. Policies are additive [source: k8s-docs-network-policies-depth-2026-08-24], so a second policy permitting the traffic permits it, and the order the two were written in does not matter.

The discriminating move here is rejecting a candidate that sounds like a policy problem and is not one. Three plausible explanations and a mechanism that does not exist is a harder set than three wrong ones, and it is closer to what a real hour of debugging feels like.

**18. A.** `[retrieval: ch3]`

*An object without its component does nothing.* Four instances so far:

- A `type: LoadBalancer` Service on a cluster with no provider to fulfill it (Ch 9 §3).
- A Service whose selector matches no Pods (Ch 9 §4).
- An Ingress with no Ingress controller (Ch 10 §3) [source: k8s-docs-ingress-depth-2026-08-24].
- A NetworkPolicy on a plugin that does not implement NetworkPolicy (Ch 10 §7) [source: k8s-docs-network-policies-depth-2026-08-24].

If you produced all four, §8's argument is one you assembled rather than one you were handed, and the question you take forward from it — *what is watching this, and is it installed?* — is a tool rather than a slogan.

*Why B is wrong, and it is the likeliest miss:* the common error here is undercounting, not misnaming. Recalling only this chapter's two instances leaves the pattern looking like an Ingress quirk. It is the two from Chapter 9 that make it a pattern, and it is the pattern that transfers to Chapter 13's metrics-server and Chapter 17's VPA.

*Why C is wrong:* admission is not the rule. The API server admitted every one of these four objects and stored them faithfully; that is precisely why none of them announced a problem. Mistaking storage for effect is the same error as question 7's option C.

*Why D is wrong:* it states the rule correctly and then supplies an instance that is not one. An Ingress with a mismatched `pathType` is a broken object with its component present — a manifest bug, findable by reading the manifest. Every genuine instance of this pattern is an object with nothing wrong with it. If re-reading the YAML can fix it, it is not this.

**19. B.**

North-south traffic enters the cluster from outside; east-west traffic moves between Pods inside it. The user's request crosses the boundary, so it is north-south, and §1–§5 — Ingress and Gateway API — are what govern that crossing. The frontend's call to the backend never leaves the cluster, so it is east-west, and §6–§7 — NetworkPolicy — are what govern that.

**A** collapses the distinction by calling both flows north-south, which would leave NetworkPolicy governing traffic that crossed the cluster boundary — not what it does. **C** inverts the two terms; this is the miss worth checking yourself against, because the words carry no intrinsic direction and are easy to swap. **D** mistakes *where the traffic ends* for *where it came from*: a request that terminates on a Pod inside the cluster is still north-south if it originated outside.

The pairing is also the chapter's own map: §1–§5 is one direction, §6–§7 the other. If you can place the two halves of this chapter, you can place the two terms.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **The exposure ceiling** | One external address per Service *[cross-bearing: see Ch 9 §3 — the four Service types]*. Fine for one; expensive for fifty. No Service type reads HTTP. |
| **The layer boundary** | Chapter 9 moves packets to an address. This chapter reads requests. Which side you are on determines what you can know. |
| **North-south / east-west** | Into the cluster / between Pods. §1–§5 is one; §6–§7 is the other. |
| **Edge router** | The router enforcing the cluster's firewall policy. A cloud gateway or physical hardware. An Ingress controller may configure it. |
| **Ingress** | HTTP and HTTPS routes from outside to Services within, controlled by rules on the resource. **Nothing else.** |
| **The four capabilities** | Externally-reachable URLs, load balancing, TLS termination, name-based virtual hosting. |
| **Simple fanout** | One address, one host, many paths → many Services. The rule reads the **URI**. |
| **Name-based virtual hosting** | One address, many hosts → many Services. The rule reads the **host**. |
| **DNS vs virtual hosting** | DNS resolves a name *before* traffic moves. Virtual hosting sorts traffic that has *already arrived*. Opposite sides of the connection. |
| **`pathType`** | `Exact`, `Prefix`, `ImplementationSpecific`. `Prefix` matches element by element, not by string prefix. |
| **Ingress controller** | **Required.** Creating an Ingress alone has no effect. Ideally all fit the reference spec; in reality they differ. |
| **IngressClass** | `ingressClassName` names which controller should fulfill an Ingress. One default class applies when the field is omitted. |
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
| **The rule** | An object without its component does nothing. Four instances of the pattern so far. Ask: *what is watching this, and is it installed?* |


<!-- AUTHOR-REVIEW: The `pathType` row drops "Longest match wins; `Exact` breaks ties" per curriculum-alignment R3, which authorizes the three values, required-ness, and the element-wise example only. If the §2 pass declines the matching cut at the precedence rule, restore the clause here so the two do not disagree. -->

---

## The Voyage Ahead

You have spent two chapters on the network, and you have been treating one thing as a given the entire time: that a Pod which restarts is a Pod that starts over. Chapter 5 said it directly — Pods are cattle, replaced rather than repaired — and Chapters 6 through 10 have quietly depended on it. A Service can point at an interchangeable set of backends precisely because they *are* interchangeable.

Chapter 11 is where that assumption runs out.

Some workloads write things down. A database has a disk, and the contents of that disk are not a detail of the Pod. They are the entire point of running it. Chapter 11 works out what happens to data when the Pod that produced it is deleted, and the answer turns out to be a ladder of three different lifetimes, only one of which survives the thing that created it.

It also closes a loop this book left open on purpose. Chapter 6 introduced StatefulSet and told you it was about stable *identity*, not about writing to disk, and then admitted the explanation was incomplete and would stay that way until storage arrived. Storage arrives in Chapter 11, and the second half of that answer arrives with it: what a per-replica volume claim is, and why it outlives not just the Pod but the rescheduling.

<!-- AUTHOR-REVIEW: The fact-accuracy audit flagged this next paragraph twice — the "four
     pluggable interfaces" claim was untagged, and the draft's count ("you have collected two
     now") contradicted §5's cross-bearing naming CRDs as one of the four. One of the fixes the
     audit offered was to drop CRDs from the set and repoint §5 at API extensions. That fix is
     declined here, because both binding contracts fix the set the other way: the B6 section
     skeleton assigns CRI to Ch 2 §4, CNI to Ch 9 §1, CSI to Ch 11 §5 and CRDs to Ch 6 §8 as the
     four, and the B7 canonical-forms row names "the four pluggable interfaces" as this book's own
     phrase for exactly that set, noting that shipped Ch 2 §4 already points at that wording. §5's
     cross-bearing therefore stands unedited and this section was corrected instead: the count is
     now three-of-four collected, which is what a reader who met CRDs in Ch 6 actually holds. The
     grouping is now owned as the book's rather than the documentation's, and the documentation's
     larger and differently-cut map is tagged. No snapshot in the corpus enumerates a canonical
     set of four; if the exam is calibrated against one, that remains a research gap. Note also
     that this is the chapter's third distinct "four" (§3 and §8 carry the absent-component-
     pattern count) — hence the full phrase rather than a bare number here. -->

And you will meet the last of the four pluggable interfaces. You have three of them already, collected one chapter at a time: CRI at the container runtime in Chapter 2, CRDs at the API itself in Chapter 6, CNI at the network last chapter. If you counted along with Chapter 9 and arrived at two, you were counting something narrower and counting it correctly — that chapter was tallying the times Kubernetes *hands the work to somebody else*, which CRI and CNI both do and CRDs do not. This is the wider set: the four places the project publishes an interface and lets you supply what sits behind it. Chapter 11 brings CSI, at storage, and that closes the set. By the time Chapter 17 gathers all four in one place, the shape should be familiar enough that the gathering feels like recognition rather than instruction.

One caution about that number, since this chapter has made a point of separating what a source says from what we have concluded from it. *The four pluggable interfaces* is this book's phrase and this book's grouping. The documentation's own map of where Kubernetes can be extended is larger than ours and cut differently: six extension points, five plugin types under infrastructure alone, and custom resources filed under a different heading entirely [source: k8s-docs-extending-kubernetes-2026-08-23]. Chapter 17 sets both maps side by side *[cross-bearing: see Ch 17 §4 — the four pluggable interfaces, collected]*. What makes our four a set is a judgement rather than a heading: at each of them, Kubernetes defines an interface and hands the implementation to somebody else. The judgement is ours. The four interfaces are real, and each one is sourced where you met it.

One last thing to carry across the chapter boundary. You will meet several objects in Chapter 11 that describe storage without providing any, and at least one arrangement where a claim sits unbound because the thing that would satisfy it has not been installed.

You know what question to ask about that now.

> *"An object is a record of intent. Intent does not act. Something has to be watching."*
