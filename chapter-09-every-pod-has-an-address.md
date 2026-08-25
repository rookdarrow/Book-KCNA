---
chapter: 9
chapter_type: "content"
title: "Every Pod Has an Address"
subtitle: "Flat networks, stable names, and the abstraction that survives churn"
exam_domain: "Container Orchestration (competency: Networking)"
domain_weight_pct: 7
complexity: "mixed"
novelty: "moderate"
prereq_factor: "standard"

#-- SUBTITLE NOTE. The arc outline's working subtitle is "Flat networks,
#-- stable names, and the abstraction that makes churn survivable" —
#-- eleven words against this stage's ≤10-word constraint. Tightened
#-- above to ten by collapsing "makes churn survivable" to "survives
#-- churn". All three ideas intact, and the shorter verb lands harder.
#-- See § Open questions #1.

#-- NOVELTY NOTE. Chapter-level label is `moderate`, but §1 alone is
#-- genuinely paradigm-shifting for the reader this book is written for.
#-- An ops professional arrives knowing that machines sit behind NAT,
#-- that ports get mapped, that reaching a process means reaching a host
#-- and then a port on it. §1 tells them none of that is true here: every
#-- Pod is directly routable from every other Pod, no NAT, no proxies.
#-- That is a model replacement, not a model extension. Drafting should
#-- treat §1 with the arousal budget of a paradigm shift even though the
#-- chapter as a whole does not warrant the label.

#-- PREREQ NOTE. `standard`, not `heavy`. B2 calls D2.1 "the most
#-- prerequisite-hungry of D2's four competencies", but every one of
#-- those prerequisites is internal and recent — Ch 4 (selectors),
#-- Ch 5 (Pod network namespace), Ch 6 (churn under controllers). No
#-- external knowledge is assumed beyond ordinary networking literacy.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "substantial" — 7
#-- points, largest of D2's competencies. Planning signal only, NOT a
#-- target.
#--
#-- ⚠ SECTION NUMBERING IS LOAD-BEARING. Thirteen published cross-bearings
#-- point into this chapter — more than at any chapter so far — and TWO
#-- of them name a section by number:
#--   chapter-02 line 600 → *[cross-bearing: see Ch 9 §1 — CNI and pod networking]*
#--   chapter-05 line 858 → *[cross-bearing: see Ch 9 §4 — readiness and Service endpoint membership]*
#-- §1 and §4 below honour those exactly. Do not renumber without editing
#-- chapter-02 and chapter-05. Verified 2026-08-24 against chapters 02-08.
sections:
  - name: "Four Rules and a Plugin"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch09-fig01-network-model-four-rules"
    checkpoint_after: false
  - name: "The Address That Doesn't Last"
    objectives: ["D2.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Four Ways to Be Reachable"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch09-fig02-service-types-ladder"
    checkpoint_after: true
  - name: "The List Behind the Name"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch09-fig03-service-endpointslice-selector-path"
    checkpoint_after: false
  - name: "When You Don't Want a Single Address"
    objectives: ["D2.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "The Component That Makes It Real"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch09-fig04-kube-proxy-modes"
    checkpoint_after: false
  - name: "Names, and Where They Resolve"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch09-fig05-dns-record-shapes"
    checkpoint_after: true
  - name: "A Query With a Name"
    objectives: ["D2.1"]
    requires_figure: true
    figure_anchor: "ch09-zenith-stable-name-over-churn"
    checkpoint_after: false

#-- Eight sections, matching Chapter 8's count for two more points. The
#-- shape is different, though: Chapter 8 had four unrelated arcs held
#-- together by a spine. This chapter has ONE arc — a packet's question,
#-- "how do I reach that" — asked at eight increasing levels of
#-- resolution. Fold options considered and rejected in § Open questions #10.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "three interchangeable copies of a service, one replaced with a new address — what a client needs so it doesn't have to be told"
    - "retrieval from Ch 5 — two containers in one Pod, both wanting port 8080, and how either reaches the other"
    - "retrieval from Ch 6 — a rolling update replaces every Pod; what happens to a client holding one of the old addresses"
    - "retrieval from Ch 4 and Ch 6 — a selector as a query over labels, and what a second controller reading the same labels would be doing"
    - "retrieval from Ch 4 — the Service DNS name form Ch 4 gave in one sentence, and what a bare name does across a namespace boundary"
    - "NAT and address translation in ordinary networks — what the receiving process sees as the source, and why that is inconvenient"
    - "a platform that manages containers but ships no networking of its own — why a system would be built that way"
    - "exposing something inside a private network to the outside — the mechanisms, and who supplies the box that terminates the connection"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 21 = 39 and states the Bearings figure is a
#-- minimum to exceed. Set at 15 across three checkpoints of 5, matching
#-- the shape shipped by Chapters 3-8. Chapter total 39 -> 44.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 21
  total_this_chapter: 44

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D2.1"]
  concepts:
    - "network-model"
    - "pod-ip"
    - "cluster-wide-ip"
    - "pod-network-namespace"
    - "localhost-communication"
    - "pod-network"
    - "cluster-network"
    - "no-nat-rule"
    - "node-agent-reachability"
    - "cni"
    - "container-network-interface"
    - "network-plugin"
    - "network-unavailable-condition"
    - "service"
    - "stable-endpoint"
    - "service-selector"
    - "clusterip"
    - "virtual-ip"
    - "nodeport"
    - "loadbalancer"
    - "externalname"
    - "cname-record"
    - "service-type-ladder"
    - "endpointslice"
    - "endpointslice-controller"
    - "endpoints-controller"
    - "readiness-gated-membership"
    - "terminating-endpoint"
    - "headless-service"
    - "cluster-ip-none"
    - "service-without-selector"
    - "manually-managed-endpointslice"
    - "service-proxy"
    - "kube-proxy"
    - "kube-proxy-modes"
    - "iptables-mode"
    - "ipvs-mode"
    - "nftables-mode"
    - "kernelspace-mode"
    - "kube-proxy-optional"
    - "cluster-dns"
    - "coredns"
    - "dns-addon"
    - "service-dns-record"
    - "a-record"
    - "aaaa-record"
    - "srv-record"
    - "pod-dns-record"
    - "dns-search-list"
    - "fqdn"
    - "cluster-domain"
    - "dns-policy"
    - "cluster-first"
  commands:
    - "kubectl-get-services"
    - "kubectl-describe-service"
    - "kubectl-get-endpointslices"

figures_planned:
  - "ch09-fig01-network-model-four-rules"
  - "ch09-fig02-service-types-ladder"
  - "ch09-fig03-service-endpointslice-selector-path"
  - "ch09-fig04-kube-proxy-modes"
  - "ch09-fig05-dns-record-shapes"
  - "ch09-zenith-stable-name-over-churn"
---

# Chapter 9: Every Pod Has an Address
## *"Flat networks, stable names, and the abstraction that survives churn"*

**Domain: Container Orchestration (28% of exam) [source: cncf-kcna-curriculum-pdf-2026-08-23] | Competency: Networking | Authored allocation: ~7% — CNCF publishes domain weights only, not competency weights; see front matter**
**Complexity: Mixed | Novelty: Moderate**

---

## Attention Budget

**Total time: ~100 minutes | Recommended: Split across 2 sessions**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 — Four Rules and a Plugin | 12 min | **High** | Peak attention |
| §2 — The Address That Doesn't Last | 6 min | Low | Anytime |
| §3 — Four Ways to Be Reachable | 16 min | **High** | Peak attention |
| ☆ Taking Your Bearings #1 | 6 min | Medium | After brief break |
| §4 — The List Behind the Name | 12 min | Medium | Mid-session |
| §5 — When You Don't Want a Single Address | 9 min | Medium | Mid-session |
| ☆ Taking Your Bearings #2 | 6 min | Medium | After brief break |
| §6 — The Component That Makes It Real | 7 min | Low | Anytime |
| §7 — Names, and Where They Resolve | 14 min | **High** | Peak attention |
| ☆ Taking Your Bearings #3 | 6 min | Medium | After brief break |
| §8 — A Query With a Name | 5 min | Low | Anytime |

<!-- AUTHOR-REVIEW: Header total corrected from ~95 to ~100 to agree with the rows, which sum to 99. The §3 row (16 min) assumes §3 as currently drafted. If the port-mechanics block (`port` / `targetPort` / `nodePort` and the node-port range) is added to §3 during revision, raise that row by ~2 min and re-round the header. Practice-question rebalancing does not affect this table — the Practice block is not a row here. -->

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts—study anytime
- **Medium:** New concepts requiring focus—study when alert
- **High:** Abstract or complex material—study at peak attention (morning for most people)

**Recommended session split:** stop after ☆ Taking Your Bearings #2. That gives you the model, the abstraction, and the backends in one sitting; the implementation, the names, and the synthesis in the next. It also puts §3 and §7 — the chapter's two densest recall blocks — in different sessions. Two hard passages, taken on separate watches. That matters more than it sounds like it should.

*If you only have 15 minutes: read §3's type ladder and §7's record shapes, then take ☆ Taking Your Bearings #3. That is where this chapter's exam points concentrate. §1 is the most important section for understanding what Kubernetes networking actually is, and it is the least likely to be tested directly. Those two facts do not coincide, and there is no point pretending they do.*

---

> *"A harbor is rebuilt piece by piece until nothing original remains. The name on the chart never moves — and the name is how anyone finds it."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Before reading this chapter, try these questions. Your score determines how to approach the content — no shame in any score, just different reading strategies.

1. You are running three interchangeable copies of a service. One of them dies and is replaced by a copy at a different address. What does a client need so that nobody has to go and tell it the new address? Name two mechanisms you have seen do that job.

2. Chapter 5 said a Pod has one network namespace shared by all of its containers. Two containers in one Pod both want to listen on port 8080. What happens? And how does either one reach the other?

3. A Deployment performs a rolling update and every Pod is replaced. A client somewhere was holding the IP address of one of the old Pods. What happens to that client, and what would have to be true for it not to care?

4. Chapter 4 said a selector is a query over labels, and Chapter 6 said a ReplicaSet finds its Pods that way. Suppose a *different* controller needed to find the same set of Pods, for a different reason. What mechanism would you expect it to use — and what would break if someone edited one Pod's labels?

5. Chapter 4 gave you, in a single sentence, the DNS name form a Service gets. Write it out. Then: a container in namespace `payments` uses only the bare name `database`. Which Service does it reach, if there is a `database` Service in both `payments` and `billing`?

6. On an ordinary network, a request crosses a NAT boundary. What does the receiving process see as the source address, and name one thing that becomes harder because of it.

7. A platform that manages containers ships with no networking implementation of its own, and expects you to install one before anything works. Give one reason a system would be designed that way, and one cost of the design.

8. Something inside a private network has to be reachable from outside it. Name two mechanisms you have used or seen. For each, say who supplies the box that terminates the outside connection — you, or someone else.

<details>
<summary>Click for answers + reading strategy</summary>

1. **An indirection — something whose address doesn't change while the things behind it do.** A load balancer with a fixed VIP and a health-checked backend pool; a DNS name re-pointed as backends move; a service registry the client queries. Any two of those count.

2. **The second container cannot bind 8080 — they share one port space.** They reach each other over `localhost`, because they share one network namespace. The Pod has one IP address; the containers share it. *(Chapter 5 §2.)*

3. **The client breaks** — it holds a valid-looking address for something that no longer exists. It would not care if what it had been handed were something that doesn't move. *(Chapter 6 §4.)*

4. **A selector — a query over the same labels.** Editing a Pod's labels can drop it out of one controller's set, out of the other's, or out of both. Nothing arbitrates between them: each evaluates its own query against the same field, and neither is told what the other decided. *(Chapter 4 §7, Chapter 6.)*

5. `<service-name>.<namespace-name>.svc.cluster.local` [source: k8s-docs-namespaces-2026-08-23]. A bare `database` from inside `payments` resolves to the `database` Service **in `payments`** — the caller's own namespace. It never sees the one in `billing`.

<!-- AUTHOR-REVIEW: The question-quality audit flags this answer as a spoiler FAIL — it
     discloses both factual halves of the §7 ★ Fixed Point (the name form, and the bare-name
     rule) before the chapter starts. It cannot be fixed here. Both facts are genuine Chapter 4
     prerequisites, and §7 itself says so, which makes Soundings rule 2 (must be answerable
     from prerequisites) and rule 3 (must not reveal a Fixed Point) unsatisfiable at the same
     time for this item. The audit's ratified remedy is to leave question 5 as written and
     rewrite the §7 Fixed Point so its claim rests on the DNS search-list mechanism — the one
     part this Soundings withholds. That edit belongs to the §7 pass, not this one. -->

6. **The receiving process sees the NAT device's address, not the original sender's.** That makes source-based authorization, rate-limiting, audit logging, and debugging harder — anything that wanted to know *who* actually called.

7. **Reason:** pluggability. Different environments have genuinely different networking requirements, and a single built-in implementation would be wrong for most of them. **Cost:** nothing works out of the box; you must choose and install something before the platform functions at all.

8. Port forwarding on a firewall or router (**you** supply the box); a cloud load balancer with a public address (**the provider** supplies it); a reverse proxy on a bastion host (**you**); a tunnel service (**the provider**). Any two, with the ownership answered.

**If you got 6+ right:** Skim this chapter. Read §3 and §7 properly — they carry the memorizable material — and read every ★ Fixed Point and ⚠ Navigational Hazards callout. Then take all three ☆ Taking Your Bearings checkpoints, because the traps in this chapter are traps for people who already know some networking.

**If you got 3–5 right:** Read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** Read carefully. And specifically: **if questions 2, 3 and 4 were among your misses, go back to Chapter 5 §2 and Chapter 6 §4 before you start §2 of this chapter.** The first half of this chapter is built directly on the Pod's network namespace and on controller churn. Without both of those, §2 reads as a solution to a problem you have not yet felt.

</details>

---

## Why This Chapter Matters

Every Pod in the cluster gets its own IP address, unique across the whole cluster. Any Pod can reach any other Pod at that address directly — no proxies, no address translation — whether the two are on the same machine or on machines in different racks [source: k8s-docs-network-model-2026-08-23]. Chapter 8 pointedly did not tell you that. It had reason not to: the claim wasn't sourceable in that chapter's material, and it belongs here, where it can be stated properly and then immediately complicated.

Because here is the complication. That address is worth almost nothing. Chapter 6 taught you that a controller may replace any Pod at any moment, and that the replacement is not a repaired version of the old Pod — it is a *different Pod*, with a different identity and, now that you know §1's rule, a different address. So the system hands every workload a perfectly good address and then guarantees the address will expire — a bearing on a vessel already under way, true when you take it and wrong by the time you act on it. **The whole subject of this chapter is the gap between those two sentences.**

This is also the first chapter in which two things have to find each other. Everything from Chapter 2 through Chapter 8 was about getting a workload *onto* something — into a container, onto a node, under a controller, past an admission gate. Placement. This chapter is about reachability, and practitioners will tell you it is the point where Kubernetes stops feeling like an unusually opinionated scheduler and starts feeling like a platform. The reason is specific rather than sentimental: the flat network model is an unusually strong constraint, and once you have it, a whole category of problems that dominate ordinary infrastructure work simply stops existing. Port collisions between unrelated applications. Coordinating who gets which host port. Address translation that hides the caller. Maintaining a registry of where things currently live. None of those are solved here. They are *absent*.

Part III of this book opens with this chapter. Chapter 8 closed by naming what Part II had carefully avoided asking, and by describing what comes next as addresses, the abstraction that makes them survivable, how names resolve, and how anything outside the cluster gets in at all. The first three of those are this chapter; the fourth is Chapter 10.

One thing to hold as you read, because it will not make sense until the end. **There is exactly one object in this chapter, and it does not do anything.** That is a strange claim to make about the object that the entirety of Kubernetes networking rests on, and you should not accept it yet. §8 is where it gets paid off.

> **Dead Reckoning:** The Kubernetes network model requires that every Pod have a unique cluster-wide IP, that all Pods be able to reach all other Pods directly without NAT or proxies, and that node agents be able to reach the Pods on their node [source: k8s-docs-network-model-2026-08-23]. Kubernetes defines that model. A CNI network plugin implements it [source: k8s-docs-extending-kubernetes-2026-08-23]. A Service is an API object that provides a stable, long-lived IP address or hostname for a set of Pods that changes over time [source: k8s-docs-network-model-2026-08-23]. Its default type is ClusterIP [source: k8s-docs-service-2026-08-23]. Its current backends are recorded in EndpointSlice objects, maintained by a controller [source: k8s-docs-network-model-2026-08-23]. kube-proxy programs each node to intercept traffic to the Service's address [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Cluster DNS publishes the address under a name [source: k8s-docs-dns-pod-service-2026-08-23].

<!-- AUTHOR-REVIEW: The CNI clause above was narrowed from "Kubernetes does not implement any of that" to the strength k8s-docs-extending-kubernetes-2026-08-23 actually supports — that a CNI plugin implements pod networking — matching the §1 Fixed Point. The snapshot lists CNI among Kubernetes' infrastructure extension points but states no exclusive negative, so the stronger "implements none of it" form is not sourceable here. The stronger normative form ("a CNI plugin is *required* to implement the Kubernetes network model") is available from k8s-docs-network-plugins-2026-08-24, which Stage 2 fetched but which is not present in sources/. Strengthen here, in §1, and in Exam Alert item 12 together once that snapshot lands. -->

**Stakes, stated plainly.** This is roughly seven points on our authored allocation, inside a domain worth 28% [source: cncf-kcna-curriculum-pdf-2026-08-23]. What that number understates is structural: within this book, Networking is the competency the others lean on. Chapter 10 cannot explain Ingress without the Service-type ladder from §3. Chapter 13 cannot explain Service troubleshooting without the endpoint list from §4. You will be back here.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **State** the four rules of the Kubernetes network model, and name the thing that implements them — which is not Kubernetes.
- **Explain** why a Pod's own IP address is insufficient for anything a client needs to keep talking to, using the churn a controller creates.
- **Choose** between ClusterIP, NodePort, LoadBalancer and ExternalName for a given exposure requirement — and say which three are layers of the same mechanism and which one is not a layer at all.
- **Trace** the path from a Service's selector to the set of addresses traffic actually reaches, and name the condition a Pod must satisfy to be on that list.
- **Write** the DNS name of a Service in another namespace, and say what a bare name would have resolved to instead.
- **Recognise** the whole apparatus — the virtual IP, the endpoint list, the DNS record — as one control loop reconciling the answer to a label query, which is the only thing you actually have to remember.

*You'll also stop thinking of a Service as a load balancer, which is the single most useful correction in this chapter and the one that makes Chapter 10 straightforward instead of confusing.*

---

Throughout this chapter, one example: a **frontend** Pod that needs to reach a **database**, where the database runs as three replicas managed by a Deployment. Nothing exotic. It is the most ordinary shape in the catalogue, and each section will hand it to the next.

---

## ⚪ §1 — Four Rules and a Plugin

Kubernetes networking is specified as a small set of requirements. Not a mechanism, not a topology — requirements. Here they are, and they are worth meeting as a numbered set, because that is how they are examinable and how §8 will retrieve them.

**Rule 1.** Each Pod in a cluster gets its own **unique cluster-wide IP address**. A Pod has its own private network namespace, shared by all of the containers within it; processes running in different containers in the same Pod communicate with each other over `localhost` [source: k8s-docs-network-model-2026-08-23].

**Rule 2.** The **pod network** — also called the cluster network — handles communication between Pods. Barring intentional network segmentation, all Pods can communicate with all other Pods, **whether they are on the same node or on different nodes** [source: k8s-docs-network-model-2026-08-23].

**Rule 3.** Pods communicate with each other **directly, without the use of proxies or address translation (NAT)** [source: k8s-docs-network-model-2026-08-23]. (One documented exception: on Windows, this rule does not apply to host-network Pods [source: k8s-docs-network-model-2026-08-23]. Note it; nothing in this book is built on it.)

**Rule 4.** **Agents on a node** — system daemons, the kubelet — can communicate with all Pods on that node [source: k8s-docs-network-model-2026-08-23].

<!-- FIGURE: ch09-fig01-network-model-four-rules -->
```
        node: worker-3                         node: worker-11
   ┌──────────────────────────┐          ┌──────────────────────────┐
   │                          │          │                          │
   │  ┌────────────────────┐  │          │  ┌────────────────────┐  │
   │  │ Pod  10.244.1.7    │  │          │  │ Pod  10.244.4.2    │  │
   │  │ ┌──────┐  ┌──────┐ │  │          │  │                    │  │
   │  │ │ ctr  │↔ │ ctr  │ │  │          │  │                    │  │
   │  │ │  a   │lo│  b   │ │  │          │  │                    │  │
   │  │ └──────┘  └──────┘ │  │          │  │                    │  │
   │  └─────────┬──────────┘  │          │  └─────────┬──────────┘  │
   │            │             │          │            │             │
   │            ├─────────────┼──────────┼────────────┘             │
   │            │             │          │                          │
   │  ┌─────────┴──────────┐  │          │  ┌────────────────────┐  │
   │  │ Pod  10.244.1.8    │  │          │  │ Pod  10.244.4.3    │  │
   │  └────────────────────┘  │          │  └────────────────────┘  │
   │       ▲                  │          │                          │
   │  ┌────┴────┐             │          │                          │
   │  │ kubelet │             │          │                          │
   │  └─────────┘             │          │                          │
   └──────────────────────────┘          └──────────────────────────┘

   Every line above is a direct connection. Nothing sits between the Pods.
```

Rule 3 is the one that deserves a paragraph rather than a line, and it is worth pausing on if you answered Soundings question 6.

In ordinary infrastructure, reaching a process means reaching a *host* and then a *port on that host*, and the address the receiver sees is frequently not the address the sender used. You accept a certain amount of pain as the price of that arrangement: coordinating which application gets which port on which machine, maintaining the translation tables, losing the caller's real identity somewhere in the middle, explaining at eight the next morning why the logs say every request came from the same three addresses.

Kubernetes forbids all of it. The receiving Pod sees the sending Pod's actual address. Two different applications can both listen on port 8080 forever, because they are not sharing a port space — each has its own. An application inside the cluster can be written as though every other application in the cluster is on the same flat network, because it is.

That is not an aesthetic preference. It is the reason the rest of this chapter can be as simple as it is.

> 🪝 **Snag:** "Each container gets its own IP" is the most common form of this mistake, and it usually arrives with readers whose habits were formed one container at a time, where container and address amounted to the same thing. Inside a Pod they do not. The address belongs to the **Pod**. Every container in a Pod shares the network namespace, including the IP address and network ports; inside a Pod, and *only* then, the containers can communicate using `localhost` [source: k8s-docs-pods-2026-08-24]. Containers in *different* Pods have distinct IP addresses and must use IP networking to reach each other [source: k8s-docs-pods-2026-08-24].

*[cross-bearing: see Ch 5 §2 — the Pod's shared network namespace]*. That chapter told you the containers share an address. This chapter tells you what the address is *worth*: it is routable from anywhere in the cluster.

★ **Fixed Point:** Every Pod gets a unique **cluster-wide** IP address, and **all Pods can reach all Pods without NAT and without proxies** — same node or different nodes. The Pod holds the address; its containers share it and reach each other over `localhost`.

### Kubernetes defines it. Something else implements it.

Everything above is a specification. It describes what must be true, and says nothing about how.

Pod networking is implemented by a **network plugin**, and the interface it plugs into is **CNI, the Container Network Interface** — listed among Kubernetes' infrastructure extension points alongside CSI for storage, CRI for container runtimes, and device plugins for custom hardware [source: k8s-docs-extending-kubernetes-2026-08-23]. CNI plugins are **binary plugins**: Kubernetes executes them as external binaries rather than linking them in [source: k8s-docs-extending-kubernetes-2026-08-23].

That published list runs longer than four [source: k8s-docs-extending-kubernetes-2026-08-23], and this book does not follow it item for item. What it follows is **the four pluggable interfaces** — CRI for runtimes, CNI for networking, CSI for storage, and CRDs for object types Kubernetes does not ship. *[cross-bearing: see Ch 2 §4 — CRI, CNI, CSI and CRDs as the four pluggable interfaces]*. That section named CNI and pointed you here. This is the second of the four; Chapter 17 collects all of them *[cross-bearing: see Ch 17 §4 — the four pluggable interfaces, collected]*.

Which network plugin? That is a genuine choice with genuine consequences. **Calico** is a networking and network policy provider supporting overlay and non-overlay networks, with or without BGP. **Cilium** provides a flat Layer 3 network with an eBPF-based data plane, in either native routing or overlay mode, and is a CNCF project at the Graduated level. **Flannel** is an overlay network provider [source: k8s-docs-cluster-addons-2026-08-24]. There are many more.

<!-- AUTHOR-REVIEW: the CNI Fixed Point below is still written to cached-source strength — "a plugin implements it" — and stops short of "a plugin is required" and of "Kubernetes ships none by default." Curriculum-alignment R1/R2 report that Stage 2 DID close this gap on 2026-08-24 with a fetch of kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/, sourcing "A CNI plugin is required to implement the Kubernetes network model" — but that snapshot was never written to ../Book-KCNA/sources/ (the Stage 2 run's write paths were refused; the body survives verbatim in research-manifest.md §1). k8s-docs-network-plugins-2026-08-24.md does not exist on disk, so the tag cannot be cited here without inventing it. Land that snapshot, then strengthen this Fixed Point to "required," and update Exam Alert #12 and the trap-table row "Kubernetes ships the network" to match.
     Second item, same fetch: per curriculum R3 and Stage 2 Notes #1, this section no longer names the kubelet as the executor of CNI binaries. The general extension-points page says the kubelet executes them; the more specific network-plugins page records that CNI management was removed from the kubelet in Kubernetes 1.24, with the container runtime loading the plugins. Naming no executor is the safe form at associate tier. Do not restore "external programs that the kubelet executes."
     Third item, same fetch: it would also restore the mechanism-level detail (node-to-node tunnels, BGP advertisement of Pod CIDRs to physical routers, kernel-level interception) that the 🔭 Closer Look below has been narrowed out of per fact-accuracy F6. -->

★ **Fixed Point:** Kubernetes **defines** the network model. A **CNI network plugin implements** it. The four rules above are requirements the plugin satisfies, not machinery Kubernetes provides [source: k8s-docs-extending-kubernetes-2026-08-23].

<!-- AUTHOR-REVIEW: fact-accuracy F4 — "cluster networking plugins commonly ship as DaemonSets" is untagged in the paragraph below. No cached snapshot describes any plugin's deployment shape; k8s-docs-cluster-addons-2026-08-24 lists Calico, Cilium and Flannel with installation links and says nothing about packaging. Two fixes, neither available in this pass: (a) propagate whatever source tag Chapter 6 §7 carries for the same claim, if it carries one — attribution to Ch 6 does not discharge the sourcing obligation on its own; (b) fetch kubernetes.io/docs/concepts/workloads/controllers/daemonset/, whose "Use cases" section covers cluster networking daemons directly, and which Chapter 6 likely wants cached regardless. Retained rather than cut because it is a retrieval of shipped Ch 6 material and the per-node reasoning is the paragraph's payoff. Build nothing further on it until it is tagged. -->

Chapter 6 noted in passing that cluster networking plugins commonly ship as DaemonSets — one Pod on every node. At the time that was an isolated fact about DaemonSets; now it is a satisfying one. A thing that must configure networking on every node is exactly a thing that wants one copy per node. *[cross-bearing: see Ch 6 §7 — DaemonSets and per-node infrastructure]*

> 🔭 **Closer Look:** The model is a *requirement*, not a description of a mechanism, and that is why implementations differ so widely. The three plugins named above already span overlay and non-overlay networks, with or without BGP, native routing or encapsulation, and an eBPF-based data plane [source: k8s-docs-cluster-addons-2026-08-24]. Those are genuinely different pieces of engineering, and every one of them satisfies the same four rules. An application inside the cluster cannot tell which one it is running on: the model is the contract, and it is the same contract underneath all of them. That last part is the point. Deeper than the exam requires.

One practical consequence, and it retrieves last chapter at exactly one chapter's distance: a node whose network is not correctly configured reports the **`NetworkUnavailable`** condition — `True` if the network for the node is not correctly configured [source: k8s-docs-nodes-2026-08-23]. You met the node condition list in Chapter 8 *[cross-bearing: see Ch 8 §4 — node conditions]*. This is the shortest demonstration available that the plugin is not a footnote.

Rule 2's hedge — *barring intentional network segmentation* — is doing quiet work. Kubernetes has an API for segmenting Pod-to-Pod traffic on purpose, and it is a Chapter 10 subject *[cross-bearing: see Ch 10 §6 — NetworkPolicy]*.

So: every Pod has an address, and any Pod can use it. Which would settle the matter, except that those addresses belong to Pods, and you already know what happens to Pods.

---

## ⚪ §2 — The Address That Doesn't Last

Your frontend Pod has the database Pod's address. It works. Requests go out, responses come back, everything is fine.

Then the database Deployment gets a new image tag and performs a rolling update. Every database Pod is replaced. And Chapter 6 was precise about what "replaced" means: Kubernetes does not repair a Pod and hand it back — a Pod is never rescheduled to a different node; it is replaced by a new, near-identical Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23]. A different Pod. Which, per §1's first rule, has a different address.

The frontend is now holding a valid-looking address for something that does not exist. Nothing malfunctioned. The system did precisely what it was designed to do, and the design broke the client.

*[cross-bearing: see Ch 6 §4 — rolling updates and Pod replacement]*, and *[cross-bearing: see Ch 5 §3 — Pod ephemerality]*, where you were told in as many words that this fact is the premise of Chapter 9. Here it is, being used.

Generalize it, in the documentation's own framing, because the exam's framing of Services descends from this paragraph:

> If some set of Pods (call them "backends") provides functionality to other Pods (call them "frontends") inside your cluster, how do the frontends find out and keep track of which IP address to connect to? [source: k8s-docs-service-2026-08-23]

The set of Pods running at one moment can be different from the set running a moment later [source: k8s-docs-service-2026-08-23]. That is the problem. Notice what it is *not*: it is not a failure mode, not a bug, not a degraded state to be recovered from. It is the normal condition of a system that replaces workloads freely.

A chart names the harbour, never the ships riding in it. That is exactly why the chart is still good next season.

The answer is an object.

A **Service** is a method for exposing a network application that is running as one or more Pods in your cluster. Each Service object defines a **logical set of endpoints** — usually those endpoints are Pods — along with a policy about how to make those Pods accessible [source: k8s-docs-service-2026-08-23]. The Service API lets you provide a **stable, long-lived** IP address or hostname for a service implemented by one or more backend Pods, where the individual Pods making up the service can change over time [source: k8s-docs-network-model-2026-08-23].

Read that last clause again. *Where the individual Pods making up the service can change over time.* The churn is not an inconvenience the Service copes with. The churn is the condition the Service exists for.

★ **Fixed Point:** A Service is a stable, long-lived address for a set of Pods **that is expected to change**. It is not a workaround for churn; it is the abstraction that makes churn a non-event.

How does a Service know which Pods? By a **selector**. Services most commonly abstract access to Kubernetes Pods thanks to the selector [source: k8s-docs-service-2026-08-23] — a query over labels, which is exactly what Chapter 4 told you a selector is, and exactly the mechanism Chapter 6 said a ReplicaSet uses to find its Pods. *[cross-bearing: see Ch 4 §7 — labels and selectors]*. Naming it now and leaving the machinery for §4 is the honest split, because Chapter 4 already told you a Service selects its backends this way. What §4 adds is where the query's answer gets *written down*.

And one fact about defaults, because it is cheap and it is examinable: **ClusterIP** exposes the Service on a cluster-internal IP, making it reachable only from within the cluster, and **it is the default that is used if you don't explicitly specify a type** [source: k8s-docs-service-2026-08-23]. §3 opens there and builds outward.

Before you go on, the correction that is worth more than anything else in this section:

> ⚓ **Worth Securing:** "A Service is a load balancer" is the most durable wrong model in Kubernetes networking, and it is wrong in a specific and useful way. A load balancer is *a thing that runs*: a process, on a machine, receiving your traffic and forwarding it. A Service is a **declaration that gets reconciled** — an object, in exactly the sense Chapter 4 established, stating that a set of Pods should be reachable at a stable address. Whether anything is listening, whether any Pod matches, whether traffic goes anywhere at all: none of that is the Service's doing, and none of it changes whether the Service exists. Almost every confusing thing in the next four sections follows from that distinction.

*[cross-bearing: see Ch 4 §4 — spec and status; a Service is an object like any other]*

---

## 🔵 §3 — Four Ways to Be Reachable

There are four Service types. Three of them are layers of the same mechanism. One of them is not a layer at all, and confusing it for one is the most reliable way to lose a point in this competency.

### The three that stack

**ClusterIP** exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default that is used if you don't explicitly specify a type for a Service [source: k8s-docs-service-2026-08-23].

**NodePort** exposes the Service on each node's IP at a static port — the node port. And here is the part candidates miss: to make the node port available, **Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP`** [source: k8s-docs-service-2026-08-23]. NodePort does not replace ClusterIP. It adds to it.

**LoadBalancer** exposes the Service externally using an external load balancer [source: k8s-docs-service-2026-08-23]. It is the outermost rung — the one that puts an address in *front* of the cluster rather than inside it.

<!-- FIGURE: ch09-fig02-service-types-ladder -->
```
   ┌─ LoadBalancer ─────────────────────────────────────────┐
   │  reachable from: the internet                          │
   │  (external LB supplied by your cloud provider,         │
   │   NOT by Kubernetes)                                   │
   │                                                        │
   │  ┌─ NodePort ───────────────────────────────────────┐  │
   │  │  reachable from: anything that can reach a node   │ │
   │  │  <node-ip>:<static-port>, on every node           │ │
   │  │                                                   │ │
   │  │  ┌─ ClusterIP ─────────────────────────────────┐  │ │
   │  │  │  reachable from: inside the cluster only    │  │ │
   │  │  │  (the default type)                         │  │ │
   │  │  └─────────────────────────────────────────────┘  │ │
   │  └───────────────────────────────────────────────────┘ │
   └────────────────────────────────────────────────────────┘

   Each ring ADDS to the ones inside it. Asking for an outer ring
   does not remove the inner ones — a NodePort Service still has
   its cluster IP.


   ════════════════════════════════════════════════════════════
   NOT ON THE LADDER. NOT A FOURTH RING. SEPARATE MECHANISM.
   ════════════════════════════════════════════════════════════

        ExternalName
        my-svc ──── CNAME ────► api.foo.bar.example
        no cluster IP · no endpoints · no proxying of any kind
```

★ **Fixed Point:** The ladder types are **additive**, and the documented case is the one to memorize: **a NodePort Service also has a cluster IP — Kubernetes sets one up, exactly as if you had requested `type: ClusterIP`** [source: k8s-docs-service-2026-08-23]. Asking for a higher rung never removes the rungs below it.

<!-- AUTHOR-REVIEW: fact-accuracy F2 flagged the stronger form of this claim — that a LoadBalancer Service also carries a node port and a cluster IP — as untagged. The cached `k8s-docs-service-2026-08-23` snapshot documents the allocation for NodePort only; its LoadBalancer entry is one sentence and says nothing about what sits beneath. Curriculum-alignment R5 records that Stage 2 did fetch a page carrying "NodePort and LoadBalancer are supersets of ClusterIP", but that snapshot (`k8s-docs-service-ports-2026-08-24`) was never written to `sources/` and so cannot be cited here. The Fixed Point above has therefore been narrowed to the documented rung. When the snapshot lands, restore the explicit LoadBalancer clause here, in the figure annotation, and in the Bearings #1 item 3 answer key. -->

### The one that is not on the ladder

**ExternalName** maps the Service to the contents of the `externalName` field — for example, to the hostname `api.foo.bar.example`. The mapping configures your cluster's DNS server to return a **CNAME record** with that external hostname value. **No proxying of any kind is set up** [source: k8s-docs-service-2026-08-23].

Read that last sentence as the definition rather than as a footnote. An ExternalName Service has no cluster IP. It has no endpoint list. Nothing intercepts a packet on its behalf, because there is no address to intercept traffic *to*. When a client resolves its name, DNS hands back a different name, and the client connects to whatever that resolves to — directly, with Kubernetes entirely out of the path.

It is a DNS alias flying a Service's colours.

> ⚠ **Navigational Hazards:** ExternalName is not the fourth rung of the ladder. It allocates no address, selects no Pods, and proxies nothing — it is a CNAME record and nothing more. Every exam question that presents it as "the type you use for external things" is testing exactly this. The word "External" in two type names (ExternalName, and LoadBalancer's external load balancer) is doing you no favours; they have nothing mechanically in common.

### The other fact that catches people

Choosing `type: LoadBalancer` does not cause Kubernetes to load-balance anything.

**Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider** [source: k8s-docs-service-2026-08-23].

What `type: LoadBalancer` does is *signal* that an external load balancer should be provisioned. On a managed cluster with cloud-provider integration, something notices that signal, provisions a load balancer, and reports its address back. On a bare-metal cluster with no such integration and no add-on that provides one, a `type: LoadBalancer` Service sits there with no external address indefinitely. Not for thirty seconds. Indefinitely — the signal is raised correctly, and there is nobody ashore to answer it.

And nothing is broken. The object is correct; the declaration is valid; the piece that would act on it is not present. Hold on to that shape — you will see it again in §4, and Chapter 10 will give it a name.

★ **Fixed Point:** **Kubernetes provides no load balancer.** `type: LoadBalancer` is a request for one from somewhere else — your cloud provider, or a component you install.

> 🪢 **Mnemonic:** *Inside · on every node · out in the world · somewhere else entirely.* ClusterIP, NodePort, LoadBalancer, ExternalName — in the order you will meet them, with the last one deliberately phrased so it doesn't sound like a continuation.

### Choosing

Four lines, not a flowchart. The exam tests the definitions and the additivity far more often than it tests the decision.

- Traffic stays inside the cluster → **ClusterIP**.
- You need a fixed port on every node, usually because something in front of the cluster will target it → **NodePort**.
- You have a cloud provider that will hand you an external address → **LoadBalancer**.
- You want an in-cluster name for something that isn't in the cluster at all → **ExternalName**.

<!-- AUTHOR-REVIEW: outline § Open questions #3 flags that `port` vs `targetPort` vs `nodePort`, and the default NodePort range (commonly cited as 30000-32767), are entirely uncached. The outline resolved this in favour of option (a) — fetch and add a short block — and curriculum-alignment R5 records that Stage 2 DID complete that fetch on 2026-08-24. The snapshot was never written to `sources/` (the Stage 2 run could not write to disk); its body survives verbatim inside `research-manifest.md` §3, but `k8s-docs-service-ports-2026-08-24.md` does not exist on disk and cannot be cited. Per the outline's own guidance ("a half-mention is worse than silence"), this section therefore still says nothing about port fields. This is now a plumbing blocker, not a research gap: extract the snapshot to `sources/`, re-run corpus assembly, and the block's natural home is right here, after the decision list. -->

*[cross-bearing: see Ch 8 §1 — a Service is created by the same `apply`, through the same API server door, as every other object]*

### The ceiling

One thing before you leave this section, because Chapter 10 is going to need it.

A LoadBalancer Service gives you one external address per Service. That is fine for one Service. It is expensive and awkward for fifty.

And none of these four types knows anything about HTTP. They move packets. They cannot route on a hostname, or a URL path, or a header, because at the layer they operate at those things are just bytes in a payload. If you want `shop.example.com/checkout` and `shop.example.com/catalog` to reach different backends behind one address, no Service type in this list can do it.

Protocol awareness is precisely what the next layer up exists to supply: **the Gateway API, or its predecessor Ingress, makes Services accessible to clients outside the cluster, with protocol-aware HTTP/HTTPS routing using URIs, hostnames, and paths** [source: k8s-docs-network-model-2026-08-23]. The address arithmetic — one per Service, fifty Services — is this book's own argument for getting there sooner rather than later. Chapter 10 opens exactly there. *[cross-bearing: see Ch 10 §1 — the exposure ceiling and what crosses it]*

---

## ☆ Taking Your Bearings #1

Five questions on the model and the abstraction — §1 through §3. Two of them reach back to earlier chapters.

1. ⚪ A Pod on `worker-3` sends a request to a Pod on `worker-11`. What does the receiving Pod see as the source address, and what two things does the network model guarantee are *not* involved?

2. ⚪ **[retrieval: ch5]** A Pod runs two containers. One listens on 8080. Can the other also listen on 8080? How does each reach the other? And how many IP addresses does the Pod have?

3. 🔵 You create a Service with `type: NodePort`. A colleague says, "so now it's only reachable from outside — we lost the internal address." What is wrong with that, and why?

4. 🔵 **[retrieval: ch6]** Chapter 6 walked a Deployment through a rolling update. State what happens to the Pod IP addresses during that update, and then say what a Service gives a client that the Pod IPs cannot.

5. 🔵 Two Services. One has `type: LoadBalancer` and, twenty minutes after creation, still has no external address. One has `type: ExternalName` pointing at `api.vendor.example`. For each: what is Kubernetes doing, and is anything broken?

---

**Answers with Explanations:**

**1. The sending Pod's own IP address. Not involved: NAT (address translation), and proxies.**

The model states it directly — Pods can communicate with each other directly, without the use of proxies or address translation [source: k8s-docs-network-model-2026-08-23] — and that the guarantee holds whether the Pods are on the same node or different nodes [source: k8s-docs-network-model-2026-08-23].

*Why the tempting wrong answers are wrong:*
- **"The sending node's IP"** would be correct in almost any non-Kubernetes cluster, which is exactly why it's the trap. Node-to-node forwarding with source rewriting is the normal arrangement elsewhere. It is forbidden here.
- **"A translated address from the pod network's NAT pool"** assumes cross-node traffic must be translated. It must not be. §1's third rule forbids address translation between Pods outright [source: k8s-docs-network-model-2026-08-23], and that prohibition binds every plugin equally — whatever a plugin does internally to carry a packet from one node to another, the receiver still sees the sender's own address. Reason from the rule, not from a guess about how any particular plugin moves the bytes.

**2. No — they share one port space. Over `localhost`. One address.**

Every container in a Pod shares the network namespace, including the IP address and network ports; within a Pod, containers share an IP address and port space and can find each other via `localhost` [source: k8s-docs-pods-2026-08-24].

*Why the wrong answers are wrong:*
- **"Yes, they each get their own port space"** is the single-container mental model most people arrive with. Two containers in one Pod compete for ports exactly as two processes on one host do.
- **"Two addresses, one per container"** is the single most common Kubernetes networking misconception. One Pod, one address per address family.

**3. Nothing was lost. Requesting NodePort also allocates a cluster IP.**

To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP` [source: k8s-docs-service-2026-08-23].

Say the rule at the level of the ladder rather than as a fact about NodePort, because the shape is what makes the types easy to hold: **a type that adds reachability keeps what the type beneath it already provided.** The documentation states that shape explicitly for NodePort over ClusterIP [source: k8s-docs-service-2026-08-23]. Hold it in that form and you carry one rule instead of three separate facts — and Chapter 10's argument for Ingress — "one external address per Service, and that does not scale" — becomes available to you without further work.

<!-- AUTHOR-REVIEW: This answer previously read "LoadBalancer implies NodePort implies ClusterIP." The cached Service snapshot documents additivity for NodePort over ClusterIP only; its LoadBalancer entry is a single sentence describing external exposure and saying nothing about cluster IPs or node ports. The claim is narrowed here to the documented rung, pending the targeted re-fetch of kubernetes.io/docs/concepts/services-networking/service/ capturing the `type: LoadBalancer` subsection in full (routed to Stage 2 by the fact-accuracy audit as its highest-priority gap). When it lands, restore the full three-rung statement here and in §3's Fixed Point in one pass, so the checkpoint bullet below and the figure caption stay in agreement.

The same fetch covers answer 5's "Indefinitely." That a provider-less LoadBalancer Service waits forever follows from the cached "Kubernetes does not directly offer a load balancing component," but no cached snapshot describes the observable pending state, so the wording is left as the book's own entailment rather than presented as documented. -->

**4. Every Pod is replaced, and each replacement has a different address. A Service gives the client one address that does not change while the set behind it does.**

A Pod is replaced by a new, near-identical Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23]; §1's first rule gives that new Pod its own address. The Service API provides a stable, long-lived IP address or hostname for a service implemented by one or more backend Pods, where the individual Pods making up the service can change over time [source: k8s-docs-network-model-2026-08-23].

If you answered something like "the client breaks, and it wouldn't have if it were using something that doesn't move" — you have written §2's opening for yourself, which is the ideal outcome for this item.

**5. LoadBalancer: waiting for an external load balancer that nothing is providing. ExternalName: working exactly as designed, as a CNAME with no proxying. Neither is broken.**

Kubernetes does not directly offer a load balancing component; you must provide one, or integrate with a cloud provider [source: k8s-docs-service-2026-08-23]. A cluster with no such integration has nothing to act on the request, so the Service waits. Indefinitely, and correctly.

ExternalName maps the Service to the contents of the `externalName` field by configuring cluster DNS to return a CNAME record; no proxying of any kind is set up [source: k8s-docs-service-2026-08-23]. There is nothing further for it to do.

*Why the tempting wrong answers are wrong:*
- **"The LoadBalancer Service failed to provision"** treats absence of a provider as failure. The declaration is correct; the actor is missing.
- **"The ExternalName Service is proxying traffic to the vendor"** is the trap. It is not in the path at all.

This is a genuinely reasonable thing to be surprised by. Most people meet `type: LoadBalancer` on a managed cluster where it just works, and the first bare-metal cluster is where the assumption surfaces. That's a normal way to learn it.

---

**Checkpoint: You've Now Mastered**

✓ The four rules of the Kubernetes network model, and who implements them
✓ Why a Pod IP is not something a client can hold on to
✓ Four Service types, how the ladder is built, and which one isn't a rung on it at all
✓ That Kubernetes ships no load balancer

Next: the Service has a name and an address — a mark that holds position while everything behind it is replaced. Now find out what *is* behind it, and what a Pod has to do to get on the list.

---

## 🔵 §4 — The List Behind the Name

A Service has a selector. The selector is a query. Somebody has to run the query, and somebody has to write down the answer, and the answer has to stay current while Pods appear and vanish underneath it.

### The path, in four steps

**One.** The Service carries a **selector** over Pod labels [source: k8s-docs-service-2026-08-23].

**Two.** **Kubernetes automatically manages EndpointSlice objects to provide information about the Pods currently backing a Service** [source: k8s-docs-network-model-2026-08-23].

**Three.** The thing doing the managing is the **EndpointSlice controller**, one of the controllers running inside the kube-controller-manager, whose job is described as populating EndpointSlice objects **to provide a link between Services and Pods** [source: k8s-docs-cluster-architecture-2026-08-23]. You met the controller-manager's controller list in Chapter 3 *[cross-bearing: see Ch 3 §3 — the controllers inside kube-controller-manager]*; this is one of the names on it. You will also meet it under an older name — **endpoints controller** — including in a quotation later in this section. One job, two names in the documentation. Not two components.

**Four.** Anything that needs to know a Service's current backends reads the **EndpointSlices** — not the selector. The selector is the question. The EndpointSlice is the written-down answer.

<!-- FIGURE: ch09-fig03-service-endpointslice-selector-path -->
```
  Service: database                                    EndpointSlice
  ┌────────────────────┐                              ┌──────────────────┐
  │ selector:          │                              │ 10.244.1.7:5432  │
  │   app: db          │                              │ 10.244.4.2:5432  │
  └─────────┬──────────┘                              └────────▲─────────┘
            │                                                  │
            │ query                       ┌───────────┐        │
            ▼                             │  Ready?   │        │
   ┌──────────────────┐                   │  ╔═════╗  │        │
   │ Pod  app: db     │ ──── matches ────►│  ║ === ║  ├────────┘
   │      10.244.1.7  │      ✓ Ready      │  ╚═════╝  │
   ├──────────────────┤                   │   GATE    │
   │ Pod  app: db     │ ──── matches ────►│           ├────────┘
   │      10.244.4.2  │      ✓ Ready      │           │
   ├──────────────────┤                   │           │
   │ Pod  app: db     │ ──── matches ────►│ ✗ STOPPED │
   │      10.244.4.9  │      ✗ NOT Ready  │  at gate  │
   ├──────────────────┤                   └───────────┘
   │ Pod  app: cache  │  ✗ never matched the selector
   │      10.244.1.9  │     (different failure — different file)
   └──────────────────┘

            ┌──────────────────────────────┐
            │  EndpointSlice controller    │ ◄── watches Services + Pods,
            │ (in kube-controller-manager) │     writes the slice
            └──────────────────────────────┘
```

### Selection is not ownership

Chapter 6 already did half of this section's work, in a context where it was surprising. Its answer key established that a Service uses **labels** to allow the control plane to determine which EndpointSlice objects are used for that Service, and that in addition to the labels, each EndpointSlice managed on behalf of a Service carries an **owner reference** [source: k8s-docs-garbage-collection-2026-08-24].

Two mechanisms, doing two jobs. Labels answer *which slices belong to this Service*. Owner references answer *what should be cleaned up when this Service is deleted*, and help different parts of Kubernetes avoid interfering with objects they don't control [source: k8s-docs-garbage-collection-2026-08-24]. A fact that was a curiosity in Chapter 6 turns out to be structural here. *[cross-bearing: see Ch 6 §3 — selection versus ownership]*

### Readiness gates membership

Here is the part you were promised.

A Pod that matches the selector is **not automatically a destination**. It has to be **Ready**.

Chapter 5 taught you readiness probes and told you plainly that this is the mechanism doing the removing. The probe's documented behaviour says it outright: `readinessProbe` indicates whether the container is ready to respond to requests, and **if the readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod** [source: k8s-docs-pod-lifecycle-2026-08-23]. And the Pod's `Ready` condition is documented as meaning the Pod is able to serve requests and **should be added to the load balancing pools of all matching Services** [source: k8s-docs-pod-termination-2026-08-24].

That quotation is where the older name surfaces. The *endpoints controller* removing an address and the *EndpointSlice controller* writing the slice are the same job [source: k8s-docs-cluster-architecture-2026-08-23]; if you read them as two components, the path in this section grows a step it does not have.

*[cross-bearing: see Ch 5 §7 — readiness probes]*. That section told you what a readiness probe does. This one tells you where it does it: in the EndpointSlice.

★ **Fixed Point:** **selector → EndpointSlice → traffic.** The selector proposes; readiness disposes. A Pod must both **match the selector** and be **Ready** to appear in the Service's EndpointSlice and receive traffic.

Three chapters converge on that sentence, and it is worth naming the convergence. Chapter 5 gave you the probe. Chapter 6 relied on the mechanism without explaining it — the reason a bad release cannot take a Service down mid-rollout is that a new Pod which never reports Ready never joins the endpoint list, so traffic never reaches it, so the rollout stalls instead of the service failing. Chapter 9 is where the wiring becomes visible. *[cross-bearing: see Ch 6 §4 — why a failed rollout does not take the Service down]*

### The same fact, running backwards

Termination is the mirror image, and it is subtler than you'd guess.

At the same time as the kubelet is starting graceful shutdown of a Pod, **the control plane evaluates whether to remove that shutting-down Pod from EndpointSlice objects**, where those objects represent a Service with a configured selector. ReplicaSets and other workload resources no longer treat the shutting-down Pod as a valid, in-service replica [source: k8s-docs-pod-termination-2026-08-24].

But — and this is the interesting half — **any endpoints that represent the terminating Pods are not immediately removed from EndpointSlices**, and a status indicating terminating state is exposed from the EndpointSlice API. **Terminating endpoints always have their `ready` status as `false`**, so load balancers will not use them for regular traffic [source: k8s-docs-pod-termination-2026-08-24].

So the list is not a boolean membership test. It carries state — and note where that state lives. The Pod has a `Ready` condition; the Pod's *entry in the slice* has a `ready` status of its own [source: k8s-docs-pod-termination-2026-08-24]. A terminating Pod stays on the list, marked, so that anything watching can distinguish "gone" from "going" — which is what lets in-flight connections drain rather than being severed.

> 🔭 **Closer Look:** If traffic draining on a terminating Pod is needed, actual readiness can be checked as a condition called `serving` [source: k8s-docs-pod-termination-2026-08-24]. That is the distinction between "should get new traffic" and "can still handle traffic it already has." Deeper than the exam requires, and the reason graceful shutdown works at all rather than merely being promised.

### Looking at the list

You can inspect it directly:

```
kubectl get endpointslices -l kubernetes.io/service-name=<service-name>
```

Make sure the endpoints in the EndpointSlices match up with the number of Pods you expect to be members of your Service. **If they don't, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready** [source: k8s-docs-debug-pods-2026-08-23].

Two causes. That is the whole diagnostic content of this section, and it is stated as a fact rather than a procedure on purpose — Chapters 13 and 16 own the troubleshooting workflow, and they will retrieve this by name. *[cross-bearing: see Ch 16 §4 — a Service whose endpoint list is empty]*

> 🪝 **Snag:** A Service with no endpoints is not a broken Service. It is a correct Service whose selector currently matches nothing, or whose matching Pods are not Ready. Those are **two different bugs, and they live in two different files** — one is a mismatch between the Service's selector and the Pod template's labels; the other is an application that isn't passing its own health check. Confusing them costs you an afternoon, because you spend it editing the wrong YAML.

One more clause, closing a Chapter 7 loop. That chapter argued that a Service's backends landing on distinct nodes is what makes it resilient rather than merely load-balanced. Now you can see why the argument was necessary: the endpoint list is *just a list*. It has no opinion about where its endpoints are. Topology is the scheduler's problem, which is where you solved it. *[cross-bearing: see Ch 7 §5 — spreading replicas across failure domains]*

<!-- AUTHOR-REVIEW: outline § Open questions #4 — status changed, action still blocked. Stage 2 DID complete the EndpointSlice fetch (kubernetes.io/docs/concepts/services-networking/endpoint-slices/) on 2026-08-24, but its snapshot was never written to ../Book-KCNA/sources/ — the write was refused, and the body survives only inside research-manifest.md §2. So `k8s-docs-endpointslices-2026-08-24` cannot be cited from here without inventing a tag for a file that does not exist. Every claim in this section therefore still rests on five landed snapshots in combination. Still deliberately NOT asserted: why slices rather than one list, the default endpoints-per-slice limit, and ready/serving/terminating as THE documented condition set (the three names appear above only where k8s-docs-pod-termination-2026-08-24 states them individually). Once the snapshot lands on disk, apply curriculum-audit R4: state the three conditions as a documented set and give §4 the full chain — readiness probe -> Pod Ready -> EndpointSlice serving -> (absent termination) ready. Keep publishNotReadyAddresses out; it is a real exception to the readiness gate and would undercut the Fixed Point above. Keep the endpoints-per-slice limit and --max-endpoints-per-slice out of the body entirely. -->

<!-- AUTHOR-REVIEW: cross-bearing targets corrected this pass against the B6 section skeleton and B7 term ledger, both BINDING: readiness probes Ch 5 §6 -> §7 (skeleton pins probe definitions to Ch 5 §7 and names that pin in its own Ch 9 §4 entry); selection-versus-ownership Ch 6 §2 -> §3 (ownerReferences is owned by Ch 6 §3); failure-domain spreading Ch 7 §7 -> §5 (§7 is that chapter's Zenith; topologySpreadConstraints is §5); empty-endpoint troubleshooting Ch 13 §3 -> Ch 16 §4 (the skeleton names "empty EndpointSlice" under Ch 16 §4 explicitly, and that section's entry back-refers to Ch 9 §4 — a reciprocal pair). ONE POINTER LEFT UNRESOLVED: "Ch 3 §3 — the controllers inside kube-controller-manager". The skeleton places kube-controller-manager in Ch 3 §2 (The Control Plane) and node components in §3, which argues for §2; but the B7 ledger records EndpointSlice as first appearing in shipped Ch 3 §3, and the curriculum-alignment audit refers to this back-bearing as landing at §3. Needs a look at shipped Ch 3 to settle which section actually enumerates the controllers. Not changed on inference. -->

### The case that closes the section

A Service whose selector matches nothing is a completely valid object.

It has a cluster IP. It has a DNS record. Its EndpointSlice is empty, and traffic sent to it goes nowhere at all. Nothing is broken; nothing has failed; the declaration is being reconciled correctly against a set that happens to be empty. The control loop is doing exactly its job, and its job produces nothing, because there is nothing to produce.

You met the same shape in §3, with a LoadBalancer Service waiting on a provider that doesn't exist. Two instances now. Chapter 10 will meet a third and give the pattern a name.

---

## 🟡 §5 — When You Don't Want a Single Address

Two deliberate exceptions. They only make sense now — a reader meeting either of these before §3 and §4 has no idea what is being subtracted from what.

### Headless: no single address, on purpose

Sometimes you don't need load-balancing and a single Service IP. In that case, you can create what are termed **headless Services**, by explicitly specifying `"None"` for the cluster IP address (`.spec.clusterIP`) [source: k8s-docs-service-2026-08-23].

What changes depends on whether the Service has a selector:

- For headless Services that **define selectors**, the endpoints controller creates EndpointSlices in the Kubernetes API, and modifies the DNS configuration to return **A or AAAA records that point directly to the Pods** backing the Service [source: k8s-docs-service-2026-08-23].
- For headless Services **without selectors**, no EndpointSlices are created automatically [source: k8s-docs-service-2026-08-23].

That first bullet carries the Kubernetes documentation's own phrasing — *the endpoints controller*. §4 called the same component **the EndpointSlice controller**. These are two names for one job, not two controllers: whichever name you meet, the object being written is an EndpointSlice.

★ **Fixed Point:** `clusterIP: None` is a **configuration, not a failure**. It says: *do not give me one address — give me all of them.* DNS returns the Pod addresses directly instead of a single virtual IP.

> 🪝 **Snag:** "Headless" sounds like something went wrong, and a teammate seeing `<none>` in the CLUSTER-IP column will often say so. It means the Service has no *head* — no single virtual IP standing in front of the set, no flagship to hail on the whole fleet's behalf. The Pods are all still there. You just get all of them, instead of one of them.

### Why anyone would want that

Chapter 6 already handed you the answer and then deferred it.

**StatefulSets currently require a headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service** [source: k8s-docs-statefulset-2026-08-24].

Think about what a StatefulSet is for. Its Pods are created from the same spec, but **are not interchangeable**: each has a persistent identifier that it maintains across any rescheduling [source: k8s-docs-statefulset-2026-08-24]. A database with one primary and two replicas. A quorum of peers that need to know each other by name. In those workloads, "send this to any one of them, I don't care which" is not a convenience — it is *precisely wrong*. If you need to reach the primary, an address that might land you on a read replica is not a stable endpoint. It is a signal sent to the whole fleet when what you needed was to raise one ship by name.

So the headless Service subtracts the one feature the ordinary Service exists to provide, and that subtraction is the feature. *[cross-bearing: see Ch 6 §6 — StatefulSets and stable identity]*, where you were told this and told to wait. §7 shows you what the resulting DNS looks like, and Chapter 11 closes the storage half of the same identity story *[cross-bearing: see Ch 11 §6 — StatefulSets and their per-replica volume claims]*.

### Services without selectors

The second exception is not an exception to the address; it is an exception to the *backends*.

Services most commonly abstract access to Kubernetes Pods thanks to the selector — but when used with a corresponding set of EndpointSlice objects and **without a selector**, the Service can abstract other kinds of backends, including ones that run **outside the cluster**: an external database, a service in another namespace or cluster, or a workload being migrated [source: k8s-docs-service-2026-08-23].

The selector is how a Service *usually* finds its endpoints. It is not what a Service *is*. Remove it, supply the endpoint addresses yourself, and everything downstream — the cluster IP, the DNS record, kube-proxy's interception, the client's connection — proceeds exactly as before.

> ⚓ **Worth Securing:** The selectorless Service is the fixed light a migration steers by. Your application inside the cluster talks to `database.production.svc.cluster.local` from day one — whether that name currently resolves to a managed database in a data centre three hundred kilometres away, or to Pods you moved in last night. The client never learns the difference, and never has to be redeployed to find out. The migration stops being the client's problem, which is usually the hardest part of making it happen at all.

### Two binaries, four cases

Headless-or-not and selector-or-not are independent, which means there are four combinations, and people routinely conflate two of them.

| | **Has a selector** | **No selector** |
|---|---|---|
| **Normal** (has a cluster IP) | The ordinary case from §3 and §4. Cluster IP; EndpointSlices populated automatically from the selector; DNS resolves to the cluster IP. | A cluster IP in front of endpoints you manage yourself. DNS resolves to the cluster IP; traffic is proxied to whatever addresses you supplied [source: k8s-docs-service-2026-08-23]. |
| **Headless** (`clusterIP: None`) | No cluster IP. The endpoints controller creates EndpointSlices; DNS returns A/AAAA records pointing directly at the Pods [source: k8s-docs-service-2026-08-23]. | No cluster IP, and **no EndpointSlices are created automatically** [source: k8s-docs-service-2026-08-23]. |

Four cells, and all four are supported configurations. None of them is an error state.

---

## ☆ Taking Your Bearings #2

Five questions on what's actually behind the name, and the two times you deliberately don't want one — §4 and §5. A name on a chart is only as good as the survey behind it. These five ask what the survey found, and who keeps it current.

1. 🔵 **[retrieval: ch6]** Chapter 6 said a ReplicaSet finds its Pods by selector, and that a Service asking the same question about the same Pods is a *different controller reading the same labels*. Name the object where the Service's answer gets written down, and name the controller that writes it.

2. 🔵 A Service's selector matches four Pods. Three are Ready; one is failing its readiness probe. How many endpoints does the Service have, and what happens to the fourth Pod when its probe starts passing?

3. 🟡 `kubectl get endpointslices` for your Service returns no endpoints. The Pods are running. Name the two usual causes, and say how you would tell them apart.

4. 🔵 A teammate calls a headless Service "broken" because `kubectl` shows no cluster IP. Explain what `clusterIP: None` does, and give one workload for which it is the correct choice.

5. 🔵 You need cluster-internal clients to reach a database that runs on hardware outside the cluster, using an ordinary Service name. Two Service configurations could do this. Name both, and say what is different about what the client experiences.

> ⚠️ **Question 3 is intentionally challenging.** Your instinct will be to look at the network. The answer is in two YAML files. If you struggle with it, that struggle is the point — this is the item most likely to save you real time later, and it encodes better for having been hard.

---

**Answers with Explanations:**

**1. The EndpointSlice. Written by the EndpointSlice controller.**

Kubernetes automatically manages EndpointSlice objects to provide information about the Pods currently backing a Service [source: k8s-docs-network-model-2026-08-23]; the EndpointSlice controller populates EndpointSlice objects to provide a link between Services and Pods [source: k8s-docs-cluster-architecture-2026-08-23].

Worth noticing what Chapter 6's framing bought you here *[cross-bearing: see Ch 6 §3 — how a controller knows its own]*. Two controllers ask the same question — *which Pods carry these labels* — for completely different reasons, and they do not coordinate. The ReplicaSet controller asks in order to count and to create replacements. The EndpointSlice controller asks in order to write down addresses. Neither knows the other exists. Both read the same field.

*Why a wrong answer is wrong:* **"The Service itself stores them"** is the natural guess and it's wrong in an instructive way. The Service stores the *query*. A separate object stores the *answer*, and a separate controller keeps that answer current.

**2. Three endpoints. When the fourth Pod's probe starts passing, it is added to the EndpointSlice and begins receiving traffic.**

A Pod's `Ready` condition means the Pod is able to serve requests and should be added to the load balancing pools of all matching Services [source: k8s-docs-pod-termination-2026-08-24]; if a readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod [source: k8s-docs-pod-lifecycle-2026-08-23].

One naming note before you carry that sentence forward. The documentation calls this component *the endpoints controller* on the Pod-lifecycle page and *the EndpointSlice controller* in the control-plane component list. That is one controller doing one job under two names — nothing additional is running, and question 1's answer and this one are describing the same thing.

Now connect it to Chapter 6, because this is the cheapest place to close that loop *[cross-bearing: see Ch 6 §4 — rolling-update mechanics]*. During a rolling update, a new Pod that never reports Ready **never receives traffic**. That is *why* a bad release cannot take your Service down — the broken replicas are excluded from the endpoint list by the same mechanism that admits the healthy ones. Chapter 6 depended on that behaviour to explain safe rollouts without ever naming the object it happens in. This is the object.

*Why a wrong answer is wrong:* **"Four"** counts the Pods the selector matches and stops there. As §4 put it, the selector proposes and readiness disposes — matching the labels makes a Pod *eligible* for the endpoint list; it does not put the Pod on it. The gate is a second, independent condition, and it is evaluated continuously rather than once at creation.

**3. Either the Service's selector doesn't match the Pods' labels, or the Pods are not Ready. Tell them apart by comparing the Service's selector against the Pods' labels, and by checking the Pods' Ready condition.**

If the endpoints don't match the Pods you expect, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready [source: k8s-docs-debug-pods-2026-08-23].

*Why the tempting wrong answers are wrong:*
- **"The network plugin is misconfigured"** would produce a much broader failure than one Service having no endpoints. Endpoint membership is computed by a controller reading the API; it does not touch the data plane at all.
- **"kube-proxy isn't running"** would break traffic to Services that *do* have endpoints. It cannot empty an endpoint list — kube-proxy reads that list, it doesn't write it.
- **"The Pods are on the wrong nodes"** — the endpoint list has no opinion about node placement whatsoever.

If you found this hard: good. It is genuinely counterintuitive that a *networking* symptom has two *non-networking* causes, and knowing that in advance is worth more than most of the recall material in this chapter.

**4. It means: don't allocate one virtual IP for this Service. DNS returns the Pod addresses directly instead. Correct choice for a StatefulSet.**

You create headless Services by explicitly specifying `"None"` for `.spec.clusterIP`; for headless Services that define selectors, DNS is configured to return A or AAAA records pointing directly to the Pods backing the Service [source: k8s-docs-service-2026-08-23]. StatefulSets currently require a headless Service to be responsible for the network identity of the Pods, and you are responsible for creating it [source: k8s-docs-statefulset-2026-08-24]. That requirement is the direct consequence of what a StatefulSet is for *[cross-bearing: see Ch 6 §6 — StatefulSet and stable identity]*: members that are not interchangeable need names that are not interchangeable either, and a single shared virtual IP cannot supply those.

*Why the wrong answer is wrong:* **"The cluster IP allocation failed"** treats `None` as an absence rather than a value. It is a value. Somebody typed it.

**5. A Service without a selector, backed by manually managed EndpointSlices; or `type: ExternalName`. The difference is proxying: the first puts kube-proxy in the path, the second does not.**

A Service used with a corresponding set of EndpointSlice objects and without a selector can abstract backends that run outside the cluster, including an external database [source: k8s-docs-service-2026-08-23]. ExternalName maps the Service to an external hostname via a CNAME record, and no proxying of any kind is set up [source: k8s-docs-service-2026-08-23].

**The proxying difference is the discriminator, and it is the reason this question exists.** Both are correct answers to the stated requirement, and they behave differently in ways that matter:

- With the **selectorless Service**, the client connects to a cluster IP inside the cluster. Traffic is intercepted on the node and redirected to the external address. The client's connection target is a cluster-internal address; DNS is ordinary Service DNS.
- With **ExternalName**, the client resolves the Service name, gets a CNAME to the external hostname, and connects to it directly. Kubernetes is not in the path at all. Which means TLS certificate names, source addresses seen by the external database, and anything that inspects the connection all behave differently.

This is the chapter's best interleaving item because it needs §3 and §5 simultaneously, and neither section alone gets you there.

---

**Checkpoint: You've Now Mastered**

✓ The path from selector to EndpointSlice to traffic
✓ Readiness as a gate on endpoint membership, not a step in a chain
✓ The two causes of an empty endpoint list, and why neither is a network problem
✓ Headless and selectorless Services as deliberate configurations

*This is the natural end of session one, if you're splitting the chapter — a reasonable place to put in for the night.* What remains is the component that actually moves the packet, the names you type, and the observation that ties all of it together.

---

## 🔵 §6 — The Component That Makes It Real

You now know what a Service declares and where its backends are recorded. Nothing so far has moved a packet.

### One component, one job

**Every node in a Kubernetes cluster runs a kube-proxy** — unless you have deployed your own alternative component in its place. The kube-proxy component is responsible for implementing a **virtual IP mechanism for Services of type other than ExternalName**. Each instance of kube-proxy watches the Kubernetes control plane for the addition and removal of **Service and EndpointSlice objects**. For each Service, kube-proxy calls appropriate APIs — depending on the kube-proxy mode — to configure the node to **capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints** (usually a Pod, but possibly an arbitrary user-provided IP address) [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

Chapter 3 introduced kube-proxy as a node component — a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept [source: k8s-docs-cluster-architecture-2026-08-23] — and left the "how" for here. *[cross-bearing: see Ch 3 §4 — kube-proxy as a node component]*

And then there is this sentence, which you should read twice:

> A control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server. [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]

A control loop. Watching objects, comparing to actual state, reconciling. You have met that shape in Chapters 3, 4, 6, 7 and 8, and here it is again in a reference page about packet forwarding. File that; §8 collects it.

### The cluster IP is virtual

Here is the consequence that reframes everything before it.

**Nothing is listening on a cluster IP.** No process is bound to it. There is no host at that address, no socket, no server. It exists only as a rule, replicated on every node, that says: *packets addressed here go to one of those addresses instead.* That is not a separate fact to memorise — it follows directly from what the documentation says kube-proxy does, which is **capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints** [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Capture and redirect. Nothing in that sentence binds a socket.

<!-- FIGURE: ch09-fig04-kube-proxy-modes -->
```
                       ┌──────────────┐    ┌──────────────────┐
        kube-proxy ───►│   Service    │    │  EndpointSlice   │
        watches        │  10.96.0.42  │    │ 10.244.1.7:5432  │
                       └──────────────┘    │ 10.244.4.2:5432  │
                              │            └──────────────────┘
                              │ programs           │
   ═══ node: worker-3 ════════▼════════════════════▼══════════════════
                                                                     ║
   ┌──────────┐        ┌ ─ ─ ─ ─ ─ ─ ─ ┐                             ║
   │ frontend │        ╎ 10.96.0.42    ╎  ◄── the cluster IP.        ║
   │   Pod    │───────►╎  (nothing is  ╎      no process. no socket. ║
   └──────────┘  to    ╎   here)       ╎      an address with        ║
             10.96.0.42└ ─ ─ ─ ─ ─ ─ ─ ┘      nothing at it.         ║
                              ┊                                      ║
              ┏━━━━━━━━━━━━━━━┻━━━━━━━━━━━━━━━━┓                     ║
              ┃   R U L E S   L A Y E R        ┃ ◄─ traffic passes   ║
              ┃  ┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄┄  ┃    THROUGH, is not   ║
              ┃  mode: iptables (default) ·    ┃    delivered TO      ║
              ┃        IPVS · nftables ·       ┃                     ║
              ┃        kernelspace (Windows)   ┃                     ║
              ┗━━━━━━━━━┳━━━━━━━━━━━━━━┳━━━━━━━┛                     ║
                        │ readdressed  │                             ║
                        ▼              ▼                             ║
                 ┌────────────┐   ┌──────────────────────────────────╨──┐
                 │ 10.244.1.7 │   │ 10.244.4.2  (on worker-11)          │
                 └────────────┘   └─────────────────────────────────────┘
```

This is also why §3's ExternalName exclusion makes sense from the other side. An ExternalName Service has **no address to intercept** — it produces a CNAME and nothing else — so there is nothing for kube-proxy to program. The exclusion isn't a special case; it falls straight out of what kube-proxy does.

> ⚓ **Worth Securing:** Nothing is listening on a cluster IP. It is not a host, not a process, not a port on a machine. It is a rule on every node that **captures** traffic to that address and **redirects** it elsewhere [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Once that lands properly, roughly half of the confusing behaviour in Kubernetes networking stops being confusing — including why the node-level tools you would ordinarily reach for show you nothing bound at that address, and why "a Service is a load balancer" was never quite right.

★ **Fixed Point:** kube-proxy implements the virtual IP mechanism for **every Service type except ExternalName**, by watching **Service and EndpointSlice** objects and programming each node. Modes: **iptables (the default)**, IPVS, nftables on Linux; **kernelspace** on Windows.

### The modes

On Linux nodes, the available modes for kube-proxy are: **iptables** — configures packet forwarding rules using iptables, and is **the default**; **ipvs** — configures packet forwarding rules using IPVS; **nftables** — configures packet forwarding rules using nftables, GA since Kubernetes 1.33. On Windows there is exactly one mode: **kernelspace** — configures packet forwarding rules in the Windows kernel [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

| Mode | Platform | Notes |
|---|---|---|
| `iptables` | Linux | **The default** |
| `ipvs` | Linux | |
| `nftables` | Linux | GA since v1.33 |
| `kernelspace` | Windows | The only mode on Windows |

That is the entire requirement at this level: recognise the four names, and know which one is the default. You do not need to understand how iptables chains differ from IPVS virtual servers, and this book is not going to pretend otherwise to fill a page. A candidate who can name the four and identify iptables as the default has everything this material is likely to ask for.

### kube-proxy is optional

One closing beat, and it is a nice one because it reaches back to §1.

**If you use a network plugin that implements packet forwarding for Services by itself, and provides equivalent behavior to kube-proxy, then you do not need to run kube-proxy on the nodes in your cluster** [source: k8s-docs-cluster-architecture-2026-08-23]. Cilium is a named example: it **can act as a replacement for kube-proxy** [source: k8s-docs-cluster-addons-2026-08-24].

So the plugin that implements the network model can also implement the Service data plane. Which is a good inoculation against reading kube-proxy as load-bearing architecture. It is one implementation of one job, and that job can be done elsewhere.

> 🔭 **Closer Look:** kube-proxy is optional. A plugin like Cilium can do the same work in its own eBPF data plane [source: k8s-docs-cluster-addons-2026-08-24]. If you meet a cluster running no kube-proxy at all, nothing is missing. Deeper than the exam requires, but useful the first time you see it and assume something is wrong.

*[cross-bearing: see Ch 17 §3 — a service mesh moves this interception into a sidecar or an ambient layer]*

---

## 🔵 §7 — Names, and Where They Resolve

Nothing so far has involved a name. The frontend still needs the database's cluster IP from somewhere, and hard-coding a cluster IP is barely better than hard-coding a Pod IP — you'd have to know it before the Service existed.

This section is where you stop needing to know any addresses at all. From here on the frontend steers by name rather than by position, and something else keeps the position current.

### What serves the records

**Kubernetes creates DNS records for Services and Pods. You can contact Services with consistent DNS names instead of IP addresses** [source: k8s-docs-dns-pod-service-2026-08-23]. Kubernetes publishes information about Pods and Services which is used to program DNS, and **the kubelet configures Pods' DNS so that running containers can look up Services by name rather than IP** [source: k8s-docs-dns-pod-service-2026-08-23].

The server doing the answering is **CoreDNS** — the cluster DNS addon that serves these records [source: k8s-docs-dns-pod-service-2026-08-23], listed under Service Discovery in the cluster addons as a flexible, extensible DNS server which can be installed as the in-cluster DNS for Pods [source: k8s-docs-cluster-addons-2026-08-24].

And the reason you have never installed it, never configured it, and possibly never thought about it: **DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on** [source: k8s-docs-dns-cluster-addon-2026-08-24].

Chapter 3 promised you CoreDNS by name *[cross-bearing: see Ch 3 §4 — cluster addons and CoreDNS]*, and Chapter 4 gave you a Service's DNS name in a single sentence and explicitly deferred four things: the mechanism, what serves the records, what else gets one, and how resolution actually proceeds *[cross-bearing: see Ch 4 §3 — namespaces and Service DNS names]*. All four are discharged in this section.

### The Service record

**Normal (not headless) Services are assigned DNS A and/or AAAA records, depending on the IP family of the Service, with a name of the form `my-svc.my-namespace.svc.cluster-domain.example`. This resolves to the cluster IP of the Service** [source: k8s-docs-dns-pod-service-2026-08-23].

Four labels, in a fixed order:

| Position | Part | What it is |
|---|---|---|
| 1 | `my-svc` | The Service's name |
| 2 | `my-namespace` | The namespace the Service lives in |
| 3 | `svc` | Literal. Marks this as a Service record |
| 4 | `cluster-domain.example` | The cluster domain — commonly `cluster.local` |

So the frontend types `database.production.svc.cluster.local`, and gets back a cluster IP that will not change for the life of the Service, regardless of what happens to the Pods behind it.

### The same name, a different answer

Here is the section's best fact, and it is the one people are most often surprised by.

**Headless Services (without a cluster IP) are also assigned DNS A and/or AAAA records with the same name form; unlike normal Services, this resolves to the set of IPs of all of the Pods selected by the Service. Clients are expected to consume the set or else use standard round-robin selection from the set** [source: k8s-docs-dns-pod-service-2026-08-23].

The name did not change shape. Same four labels, same order, same everything. What changed is the *number of answers*: one cluster IP for a normal Service, the whole Pod set for a headless one.

§5 told you this happens. This is where you can see that it happens **without a different name**, which is why it catches people — the client's configuration file looks identical in both cases.

★ **Fixed Point:** The **same name form** — `<service>.<namespace>.svc.<cluster-domain>` — gives you the **cluster IP** for a normal Service and **the set of Pod IPs** for a headless one.

### Why a bare name works, and where it stops

Chapter 4 gave you the rule flat: a bare `<service-name>` resolves to the Service local to your namespace, and reaching across namespaces requires the fully qualified domain name [source: k8s-docs-namespaces-2026-08-23].

Here is why, and it is more satisfying than a rule.

**By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain** [source: k8s-docs-dns-pod-service-2026-08-23].

That is it. That is the entire mechanism. It is not special-case Kubernetes behaviour — it is ordinary DNS search-domain resolution, the same thing that has let you type a short hostname on a corporate network for thirty years. A Pod in `payments` searching for `ledger` tries `ledger.payments.svc.cluster.local`, because `payments.svc.cluster.local` is in its search list. It finds something. It stops.

★ **Fixed Point:** A bare name resolves in the client Pod's **own namespace only** — **because that namespace is in the Pod's DNS search list**. This is not a Kubernetes special case; it is ordinary DNS search-domain resolution, which is also why crossing a namespace boundary requires the full `<service>.<namespace>.svc.<cluster-domain>`.

> ⚠ **Navigational Hazards:** The bare name is the single most common cross-namespace mistake, and it fails in the worst available way. If **no** Service of that name exists in the caller's namespace, you get a resolution failure — annoying, but obvious, and you'll fix it in a minute. If a Service of that **same name** exists in the caller's namespace, the lookup **succeeds**, and your application connects to the wrong thing. No error. No timeout. No log line. Just the wrong database, answering questions it shouldn't have been asked. This is why the FQDN rule is worth memorising rather than looking up.

> 🪢 **Mnemonic:** *service, namespace, svc, cluster.local.* Four labels, always in that order. The two in the middle are the ones people reverse under pressure — and note that `svc` is a literal, not an abbreviation of anything in your cluster.

### The other record shapes

Two more, compactly, plus one that closes §5's loop.

**SRV records** are created for **named ports** that are part of normal or headless Services, with the form `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example` [source: k8s-docs-dns-pod-service-2026-08-23]. Note that the Service's own four labels are intact at the end; the port-name and protocol are prefixed on.

**Pods** get records too. In general a Pod has the DNS resolution of the form `pod-ipv4-address.my-namespace.pod.cluster-domain.example` — for example, `172-17-0-3.default.pod.cluster.local` [source: k8s-docs-dns-pod-service-2026-08-23]. The dots in the address become dashes, because dots are label separators in DNS and cannot appear inside a label. Note also that position 3 is `pod`, not `svc`.

And the one that finishes the StatefulSet story: the Pod spec has optional **`hostname` and `subdomain`** fields; **when both are set and a headless Service exists with the same name as the subdomain, the Pod's FQDN is `hostname.subdomain.namespace.svc.cluster-domain.example`** [source: k8s-docs-dns-pod-service-2026-08-23].

Note the shape, because it is the same shape by which an individual StatefulSet member is individually addressable. §5 told you a StatefulSet requires a headless Service to be responsible for the network identity of its Pods; a stable per-member name of this shape, surviving rescheduling, is what "network identity" cashes out to. *[cross-bearing: see Ch 6 §6 — StatefulSet Pod naming]*

<!-- FIGURE: ch09-fig05-dns-record-shapes -->
```
                    ┌───────────────┬──────────────┬───────┬─────────────────┐
                    │       1       │      2       │   3   │        4        │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Service (normal)  │    my-svc     │ my-namespace │  svc  │ cluster.local   │  → the cluster IP
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Service (headless)│    my-svc     │ my-namespace │  svc  │ cluster.local   │  → ALL the Pod IPs
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  SRV (named port)  │ _http._tcp.   │ my-namespace │  svc  │ cluster.local   │  → the named port
     prefixed with →│    my-svc     │              │       │                 │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Pod (by address)  │  172-17-0-3   │ my-namespace │  pod  │ cluster.local   │  → that Pod
                    │  (dots→dashes)│              │  ▲▲▲  │                 │
  ──────────────────┼───────────────┼──────────────┼───────┼─────────────────┤  ─────────────────────────
  Pod (hostname +   │   hostname.   │  namespace   │  svc  │ cluster.local   │  → that Pod, by a
     subdomain)     │   subdomain   │              │       │                 │     stable name
  ──────────────────┴───────────────┴──────────────┴───────┴─────────────────┘  ─────────────────────────

  Columns 2 and 4 are identical in every row.
  Column 3 is `svc` for everything except the Pod-by-address record.
  The top two rows are the SAME NAME. Only the answer differs.
```

> **Dead Reckoning:** The five record shapes, stated flat.
>
> | Name shape | Resolves to |
> |---|---|
> | `my-svc.my-namespace.svc.cluster-domain.example` (normal Service) | The cluster IP of the Service |
> | `my-svc.my-namespace.svc.cluster-domain.example` (headless Service) | The set of IPs of all Pods selected by the Service |
> | `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example` | The named port on that Service |
> | `pod-ipv4-address.my-namespace.pod.cluster-domain.example` (e.g. `172-17-0-3.default.pod.cluster.local`) | That Pod |
> | `hostname.subdomain.namespace.svc.cluster-domain.example` (requires `hostname` + `subdomain` set, and a headless Service named for the subdomain) | That Pod, by a stable name |
>
> Record types are A and/or AAAA depending on the IP family, except SRV records, which are SRV. Cluster DNS is served by CoreDNS, launched automatically by the addon manager. Pod DNS configuration is written by the kubelet. A bare service name resolves within the client Pod's own namespace because that namespace is in the Pod's default DNS search list. [source: k8s-docs-dns-pod-service-2026-08-23] [source: k8s-docs-dns-cluster-addon-2026-08-24]

> 🔭 **Closer Look:** A Pod's `dnsPolicy` field controls how its DNS is configured. `ClusterFirst` — any query that does not match the configured cluster domain suffix is forwarded to an upstream nameserver — **is the default policy if `dnsPolicy` is not explicitly specified** [source: k8s-docs-dns-pod-service-2026-08-23]. Also available: `Default` (inherit resolution config from the node), `ClusterFirstWithHostNet` (for Pods running with `hostNetwork`), and `None`, where the Pod ignores DNS settings from the Kubernetes environment and all settings come from the `dnsConfig` field [source: k8s-docs-dns-pod-service-2026-08-23]. Note the trap in the naming: the value called `Default` is *not* the default. Deeper than the exam requires — but if you ever meet a Pod that can't resolve cluster names at all, this field is where to look.

One boundary worth marking before Chapter 10. What you have just learned is **DNS-based service discovery** — mapping a name to an address, in the ordinary DNS sense. Chapter 10 introduces **name-based virtual hosting**: routing HTTP traffic to multiple host names at the same IP address [source: k8s-docs-ingress-2026-08-23]. Both involve hostnames, and they sit on opposite sides of the connection — one turns a name into an address before any traffic moves, the other sorts traffic that has already arrived at a single address. Conflating them makes Chapter 10 considerably harder than it needs to be. *[cross-bearing: see Ch 10 §2 — name-based virtual hosting]*

<!-- AUTHOR-REVIEW: outline explicitly scopes out CoreDNS Corefile configuration, custom nameservers, stub domains, and CoreDNS plugins. The dns-cluster-addon snapshot's own note records the rest of that page as out of scope. Nothing on cluster DNS customisation appears above; that omission is deliberate, not a gap. -->

<!-- AUTHOR-REVIEW: cross-bearing targets in this section were retargeted to conform to the BINDING B6 section skeleton, which no diagnostic flagged. Changes: `Ch 3 §6` -> `Ch 3 §4` (skeleton: Ch 3 §4 is "Addons, and What Else Is Optional"; §6 is the control loop); `Ch 4 §6` -> `Ch 4 §3` (skeleton: Ch 4 §3 "Where a Name Lives" owns namespaces; §6 is the chapter synthesis); `Ch 6 §5` -> `Ch 6 §6` (skeleton: Ch 6 §6 "When Pods Are Not Interchangeable" owns StatefulSet identity; §5 is "Every Rollout Is a Revision"); `Ch 10 §3` -> `Ch 10 §2` (skeleton: Ch 10 §2 "Routing by Host and Path" owns name-based virtual hosting; §3 owns Ingress controllers). The draft's back-pointers appear to be consistently off against the skeleton chapter-wide, not only in this section -- recommend a chapter-wide pointer sweep at the integration-check stage, and revert here if the skeleton's extraction is what is wrong rather than the draft. -->

---

## ☆ Taking Your Bearings #3

Five questions on what moves the packet and what you actually type — §6 and §7.

1. 🔵 Name the component that implements the virtual IP mechanism for Services, say which Service type it does **not** implement, and name the two object types it watches.

2. 🟡 A colleague says, "I'll SSH to the node and see what's listening on the cluster IP." What will they find, and why?

3. 🔵 Name kube-proxy's modes and identify the default on Linux. Then say what it would mean to find a cluster running no kube-proxy at all.

4. 🔵 A container in namespace `payments` needs to reach a Service named `ledger` in namespace `billing`. Write the name it should use, and say what would happen if it used just `ledger`.

5. 🟡 Two Services in the same namespace: `db-a` is a normal Service, `db-b` is headless. A client resolves `db-a.prod.svc.cluster.local` and `db-b.prod.svc.cluster.local`. Describe what each lookup returns, and how many answers the client gets.

---

**Answers with Explanations:**

**1. kube-proxy. It does not implement ExternalName. It watches Service and EndpointSlice objects.**

The kube-proxy component is responsible for implementing a virtual IP mechanism for Services of type other than ExternalName; each instance watches the control plane for the addition and removal of Service and EndpointSlice objects [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

*Why a wrong answer is wrong:* **"It watches Services and Pods"** is close and consequential. kube-proxy reads the *computed* answer — the EndpointSlice — not the raw Pods. The EndpointSlice controller is what reads Pods. Two controllers, two inputs, one chain.

**2. Nothing. The cluster IP is virtual — no process is bound to it.**

kube-proxy configures the node to capture traffic to the Service's `clusterIP` and port, and redirect that traffic to one of the Service's endpoints [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. That is the whole documented mechanism, and everything else in this answer follows from it rather than from any separate statement in the documentation: if traffic is *captured and redirected*, then it passes *through* a rule and is never delivered *to* the cluster IP. Nothing accepts a connection there, so there is no socket to find, and `netstat` or `ss` on the node has nothing bound to show you.

*Why the wrong answers are wrong:*
- **"kube-proxy is listening on it"** — kube-proxy programs rules; in the default iptables mode it does not sit in the data path receiving your packets.
- **"One of the backend Pods"** — the backend Pods listen on their *own* addresses. The cluster IP is not one of them.

If you got this one, §6 landed. If you didn't, it's worth a re-read of the Worth Securing callout before you move on, because this idea is load-bearing for everything in Chapter 10.

**3. iptables (the default), IPVS, and nftables on Linux; kernelspace on Windows. A cluster with no kube-proxy means the network plugin implements Service packet forwarding itself.**

The mode list and the default are documented directly [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. And: if you use a network plugin that implements packet forwarding for Services by itself, providing equivalent behavior to kube-proxy, you do not need to run kube-proxy on the nodes in your cluster [source: k8s-docs-cluster-architecture-2026-08-23] — Cilium being a named example of a plugin that can act as a replacement [source: k8s-docs-cluster-addons-2026-08-24].

*A note on what this answer does not say:* it makes no claim about which mode is faster, more scalable, or better, and none about whether replacing kube-proxy performs better than keeping it. The documentation states the list, the default, and the substitution, and says nothing about relative performance — so neither does this book. If you have read that IPVS scales better than iptables for very large Services, that may well be true — but it isn't a claim this material supports, and no exam question you meet should turn on it.

**4. `ledger.billing.svc.cluster.local`. A bare `ledger` would resolve within `payments` only — failing, or worse, silently reaching a different `ledger`.**

A client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain [source: k8s-docs-dns-pod-service-2026-08-23]; a container using only `<service-name>` resolves to the Service local to its namespace, and reaching across namespaces requires the FQDN [source: k8s-docs-namespaces-2026-08-23].

**"It fails" is the incomplete answer, and the incompleteness matters.** If `payments` has no `ledger` Service, you get NXDOMAIN, your application logs a connection error, and you fix it in five minutes. If `payments` *does* have a `ledger` Service — perhaps a test fixture, perhaps a stub someone left behind, perhaps a genuinely different service that happens to share a name — the lookup **succeeds against the wrong Service**. Your application connects. It writes. Nothing anywhere reports an error.

That second case is the one that costs people afternoons, and it's the reason to memorise the FQDN form rather than plan to look it up.

**5. `db-a` returns one address — the Service's cluster IP. `db-b` returns the set of IPs of all the Pods it selects.**

Normal Services are assigned A and/or AAAA records resolving to the cluster IP of the Service; headless Services are assigned records with **the same name form**, but resolving to the set of IPs of all of the Pods selected by the Service, and clients are expected to consume the set or use standard round-robin selection from it [source: k8s-docs-dns-pod-service-2026-08-23].

Both answers come from the same place. Cluster DNS is a built-in service launched automatically as a cluster addon [source: k8s-docs-dns-cluster-addon-2026-08-24], and CoreDNS is what serves it [source: k8s-docs-cluster-addons-2026-08-24]. It is not behaving differently for `db-b` than for `db-a`; the difference is in what each Service's records are defined to contain, not in what publishes them.

The point of the item is that the two names are structurally identical. Nothing in `db-b.prod.svc.cluster.local` announces that it is headless. A client library that assumes one answer per lookup will take the first address it gets and never speak to the other Pods — which is fine for some workloads and quietly wrong for others.

---

**Checkpoint: You've Now Mastered**

✓ kube-proxy's job, its four modes, and its optionality
✓ That the cluster IP is a rule, not a socket
✓ Five DNS record shapes and what each resolves to
✓ Why a bare name is namespace-local, and what that costs when it goes wrong

One section left. It teaches nothing new.

---

## ⚪ §8 — A Query With a Name

Back to the claim from the opening. **There is one object in this chapter, and it does not do anything.**

A Service is a **label query with a name attached**. Everything else in this chapter is a control loop reconciling that query's current answer against some piece of the network.

Walk it back through, in the chapter's own order.

**From §2.** The Service is an object. You `apply` it through the same API server door as everything else, and its `spec` is a statement of desired state in exactly the sense Chapter 4 defined: *these Pods should be reachable at a stable address.* It does not run. It does not receive traffic. It states a condition that should hold.

**From §4.** The EndpointSlice controller watches Services and Pods, evaluates the selector, and writes down the answer [source: k8s-docs-cluster-architecture-2026-08-23]. Desired state, observed state, reconciliation. **And this is the same shape as the ReplicaSet controller running over the same labels for an entirely different purpose** — which is exactly what Chapter 6 was telling you when it distinguished selection from ownership. Two loops, one label set, no coordination, no conflict. *[cross-bearing: see Ch 6 §2 — selection versus ownership]*

**From §6.** kube-proxy watches Services and EndpointSlices and programs each node. The documentation says so in as many words: *a control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server* [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. That is the sixth control loop in this book, and you should count it.

**From §7.** Cluster DNS publishes the answer as a name. Same input, third consumer, third format.

**From §1.** And underneath all of it, none of the actual packet-moving is Kubernetes' work at all. Kubernetes defines the network model; a CNI plugin implements it [source: k8s-docs-extending-kubernetes-2026-08-23] — which is the second instance of an arrangement you first met in Chapter 2, where CRI does the same thing for container runtimes. *[cross-bearing: see Ch 2 §4 — CRI as the first pluggable interface]*

<!-- FIGURE: ch09-zenith-stable-name-over-churn -->
```
   ╔═══════════════════════════════════════════════════════════════════════╗
   ║        database.production.svc.cluster.local   ·   10.96.0.42         ║
   ╚═══════════════════════════════════════════════════════════════════════╝
        ▲                    ▲                    ▲                   ▲
        │  t₀                │  t₁                │  t₂               │  t₃
   ┌────┴─────┐        ┌─────┴────┐         ┌─────┴────┐        ┌─────┴────┐
   │ ▲  ▲  ▲  │        │ ▲  ●  ●  │         │ ●  ■  ■  │        │ ◆  ◆  ◆  │
   │.1.7 .4.2 │        │.1.7 .2.8 │         │.2.8 .5.1 │        │.7.3 .8.9 │
   │   .4.3   │        │    .2.9  │         │    .5.4  │        │    .9.0  │
   └──────────┘        └──────────┘         └──────────┘        └──────────┘
     (nothing survives from t₀ to t₃ — not one Pod, not one address)

   ┌───────────────────────────────────────────────────────────────────────┐
   │   query  ────────►  answer  ────────►  publish                        │
   │  (app: db)        (EndpointSlice)          │                          │
   └────────────────────────────────────────────┼──────────────────────────┘
                     ┌──────────────────────────┼──────────────────────────┐
                     ▼                          ▼                          ▼
              ┏━━━━━━━━━━━━┓           ┌──────────────┐           ┌────────────────┐
              ┃ rules layer┃           │ endpoint list│           │  DNS record    │
              ┃   (§6)     ┃           │     (§4)     │           │     (§7)       │
              ┗━━━━━━━━━━━━┛           └──────────────┘           └────────────────┘
                three readers · one answer · one question that never changed
```

☀️ **Zenith:** A Service is a **label query with a name**. The virtual IP, the endpoint list, and the DNS record are three control loops publishing that one query's current answer in three different formats. The Pods were never the stable thing. **The question was.**

That is the chapter's title, made good on. The stable thing was never a Pod — you knew that after §2. But it was never really an IP address either: the cluster IP belongs to nothing, nothing listens on it, and it exists only as a rule that other machinery maintains. What is actually stable is *"which Pods carry the label `app: db` and are Ready"* — a question whose answer is different every few minutes and whose **meaning** is the same forever. Pods churn beneath it the way water churns beneath a fixed star. The question doesn't move.

That is what makes churn survivable. And it is why the abstraction is a declaration rather than a device: a device would have to be somewhere, and would fail when that somewhere failed. A question does not have a location.

### Where the claim overreaches

The claim is a slogan, and slogans need narrowing until they're true.

§3's type ladder and §7's record shapes are **not** consequences of this architecture. They are facts about an API — decisions somebody made about what to call things and how many layers to stack. You cannot derive "NodePort also allocates a cluster IP" from "a Service is a label query," and you cannot derive `_port-name._port-protocol.` from anything at all. Those you memorise, the same as anyone.

Everything else in this chapter, you can rebuild from §1's model plus the observation above. That is a genuinely useful ratio, and it is worth knowing which side of the line each fact sits on before you spend study time on it.

> ⚓ **Worth Securing:** The practical form of the Zenith, for when Kubernetes networking does something you didn't expect. Ask two questions: **what does the selector currently match?** and **which loop hasn't caught up yet?** Between them they cover most of it — and both are answerable with `kubectl` in under a minute, which is more than can be said for most debugging heuristics.

*[cross-bearing: see Ch 15 §5 — the control loop, generalised, pointed at a Git repository]*. This chapter observes that Kubernetes networking is *made of* control loops. Chapter 15 makes the larger argument, and it is the structural claim this whole book is building toward. Don't get ahead of it.

### The boundary

Everything in this chapter has been about the inside of the cluster.

Every name you learned resolves to something with a Pod behind it — or, in ExternalName's case, to a name that isn't Kubernetes' business at all. Every address you learned is reachable only by things that are already in. Even NodePort and LoadBalancer, the two types that reach outward, do it by *offering a door*, not by describing what comes through it or where it should go.

Chapter 10 crosses that boundary properly: one address serving many services, routing decisions made on the contents of an HTTP request rather than on a destination address, and a rule about what happens when you create the object and nobody has installed the thing that acts on it.

---

## Exam Alert! 🚨

**High-Priority Topics**

1. **Every Pod gets a unique cluster-wide IP**, and all Pods reach all Pods **without NAT and without proxies** — same node or across nodes [source: k8s-docs-network-model-2026-08-23].
2. **The Pod holds the IP; its containers share it** and communicate over `localhost` [source: k8s-docs-pods-2026-08-24].
3. **ClusterIP is the default** Service type, and is reachable only from inside the cluster [source: k8s-docs-service-2026-08-23].
4. **NodePort also allocates a cluster IP** — the documentation is explicit that Kubernetes sets one up "the same as if you had requested a Service of type: ClusterIP" [source: k8s-docs-service-2026-08-23].
5. **Kubernetes does not provide a load balancer.** You supply one, or integrate with a cloud provider [source: k8s-docs-service-2026-08-23].
6. **ExternalName is a CNAME with no proxying of any kind** [source: k8s-docs-service-2026-08-23].
7. **`clusterIP: None` is deliberate** — DNS returns the Pod addresses directly [source: k8s-docs-service-2026-08-23].
8. **A Service without a selector is a supported pattern**, backed by manually managed EndpointSlices [source: k8s-docs-service-2026-08-23].
9. **`<service>.<namespace>.svc.<cluster-domain>`**, and a **bare name resolves in the local namespace only** [source: k8s-docs-dns-pod-service-2026-08-23] [source: k8s-docs-namespaces-2026-08-23].
10. **kube-proxy implements the virtual IP for every type except ExternalName**; **iptables is the default mode** [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].
11. **A Pod must be Ready to be an endpoint** [source: k8s-docs-pod-lifecycle-2026-08-23].
12. **Kubernetes defines the network model; a CNI network plugin implements it** [source: k8s-docs-extending-kubernetes-2026-08-23].

<!-- AUTHOR-REVIEW: two items narrowed relative to draft-v1, both awaiting fetches that §1 and §3 are also waiting on.

     (a) Item 4 previously read "the types are additive", which generalises the rule to LoadBalancer. The cached Service
     snapshot documents the cluster-IP allocation for NodePort only ("To make the node port available, Kubernetes sets up
     a cluster IP address, the same as if you had requested a Service of type: ClusterIP"); its LoadBalancer entry is a
     single sentence about external exposure and says nothing about the rungs beneath it. The general form is very likely
     correct but is not in the corpus. Restore it once the `type: LoadBalancer` subsection of
     kubernetes.io/docs/concepts/services-networking/service/ is cached in full. Same fetch resolves the "waits
     indefinitely" claim in §3.

     (b) Item 12 previously read "and implements none of it". The cited snapshot supports the positive half — CNI is
     listed among Kubernetes' infrastructure extension points "to implement pod networking" — but states no exclusive
     negative. This now mirrors §1's Fixed Point wording exactly, which is the form §1 already holds itself to. Restore
     the stronger claim, and the stronger normative form ("a CNI plugin is required"), when the network-plugins page
     fetch lands. The Dead Reckoning block in "Why This Chapter Matters" carries the same overreach and needs the same
     treatment. -->

---

**Common Traps** — every one of these is a documented mistake with a specific correct answer, which is to say every one is a hazard somebody has already run onto and marked. Don't let the wrong version be the one that's fresh when you sit down.

| The trap | The correction | Where it's defused |
|---|---|---|
| "Pods need NAT or a proxy to reach Pods on other nodes" | Direct, no NAT, no proxy — that's rule 3 | §1, Bearings #1 item 1 |
| "Each container in a Pod gets its own IP" | The **Pod** has the address; containers share it | §1 Snag, Bearings #1 item 2 |
| "NodePort replaces ClusterIP" | NodePort **also** allocates a cluster IP | §3 Fixed Point, Bearings #1 item 3 |
| "LoadBalancer means Kubernetes provides a load balancer" | It provides none. You supply one | §3 Fixed Point, Bearings #1 item 5 |
| "ExternalName proxies traffic" | CNAME only. No proxying of any kind | §3 Navigational Hazards, Bearings #1 item 5 |
| "A headless Service is a broken Service" | `clusterIP: None` is a value somebody typed | §5 Fixed Point, Bearings #2 item 4 |
| "A Service without a selector is invalid" | Supported pattern, used for external backends | §5, Bearings #2 item 5 |
| "A bare service name works across namespaces" | Local namespace only — and it may succeed *wrongly* | §7 Navigational Hazards, Bearings #3 item 4 |
| "Something is listening on the cluster IP" | Nothing is. It's a forwarding rule, not a socket | §6 Worth Securing, Bearings #3 item 2 |
| "kube-proxy is required" | Optional, if the plugin does equivalent forwarding | §6 Closer Look, Bearings #3 item 3 |
| "Headless Services have no DNS record" | Same name form; different answer | §7, Bearings #3 item 5 |
| "A Service with no endpoints is broken" | Correct Service; selector matches nothing, or Pods not Ready | §4 Snag, Bearings #2 item 3 |
| "A terminating Pod leaves the Service instantly" | Retained with `ready: false`, so traffic drains | §4 Closer Look |
| "Kubernetes ships the network" | It defines the *requirements*; a CNI plugin implements them | §1 Fixed Point |

**The most valuable one on that list** is "something is listening on the cluster IP." It has one clean correct answer, and that answer follows directly from what kube-proxy is documented to do — configure the node to *capture* traffic addressed to the Service's cluster IP and port, and *redirect* that traffic to one of the Service's endpoints [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Capture-and-redirect requires nothing bound to that address, which is exactly why nothing is bound to it. Believing the wrong version makes roughly half of Kubernetes networking incomprehensible — including several things Chapter 10 will assume you understand.

---

## Practice Questions

Twenty-two questions. Four of them draw on earlier chapters and are tagged; one is deliberately not multiple choice. Answers and explanations follow the full set — attempt them all before looking.

---

**1.** Which of the following is required by the Kubernetes network model?

A) Pods communicate across nodes through a NAT gateway maintained by the kubelet
B) All Pods can communicate with all other Pods, on the same node or on different nodes, without proxies or address translation
C) Each container in a Pod receives its own cluster-wide IP address
D) Pods on different nodes communicate via the node's external IP and a mapped port

---

**2.** A Pod is running three containers. **[retrieval: ch5]** How many IP addresses does the cluster allocate for that Pod, and how many entries would that Pod contribute to a matching Service's EndpointSlice?

A) Three addresses, three entries
B) Three addresses, one entry
C) One address, three entries
D) One address, one entry

---

**3.** Which statement about CNI is correct?

A) CNI is the Kubernetes-built-in networking implementation, enabled by default
B) CNI is the interface through which a network plugin implements Pod networking; the plugin is an external binary rather than a Kubernetes component
C) CNI is a Kubernetes API object you create to define a Pod network
D) CNI is the protocol kube-proxy uses to program iptables rules

---

**4.** A Service is created with no `type` field specified. What type is it, and from where is it reachable?

A) NodePort; from any node's IP at a static port
B) ClusterIP; from inside the cluster only
C) ClusterIP; from inside the cluster and from any node's IP
D) LoadBalancer; from wherever the provider's load balancer is reachable

---

**5.** You change a Service from `type: ClusterIP` to `type: NodePort`. What happens to the cluster IP?

A) It is released, since NodePort replaces it
B) It is retained — Kubernetes sets up a cluster IP for NodePort Services as well
C) It is retained but becomes unreachable from inside the cluster
D) It is replaced by the node's IP address

---

**6.** Your team runs Kubernetes on bare metal with no cloud-provider integration and no load-balancer add-on installed. You create a `type: LoadBalancer` Service. What happens?

A) Kubernetes provisions a software load balancer on one of the nodes
B) The Service is rejected at admission with a validation error
C) The Service is created and waits indefinitely for an external address; nothing is broken
D) The Service silently falls back to `type: NodePort`

---

**7.** A Service resolves to `api.vendor.example`, and a client Pod connects to it successfully. An engineer runs a packet capture on the node, expecting to find the connection matched by a kube-proxy rule, and finds no rule for that Service at all. Which type is the Service, and why is there no rule to capture?

A) NodePort — a NodePort Service surrenders its cluster IP, so kube-proxy has no address left to program a rule against
B) ClusterIP — kube-proxy programs rules only for Services that are reachable from outside the cluster
C) ExternalName — it is implemented purely as a DNS CNAME, and kube-proxy's virtual-IP mechanism covers every type except this one
D) LoadBalancer — the provider's load balancer handles the traffic, so no node-level rule is needed

---

**8.** You need clients inside the cluster to reach `analytics.vendor.example`, a SaaS endpoint outside the cluster, using an in-cluster name. Which Service configuration produces a CNAME with Kubernetes entirely out of the traffic path?

A) `type: ClusterIP` with no selector and manually created EndpointSlices
B) `type: ExternalName` with `externalName: analytics.vendor.example`
C) `type: LoadBalancer` with an annotation naming the vendor
D) A headless Service with `externalName` set

<!-- AUTHOR-REVIEW: the curriculum-alignment audit (R5/R7) asks for one further §3 item on Service port mechanics — `port` / `targetPort` / `nodePort` and the `--service-node-port-range` default. It is not written, because the snapshot that would source it (`k8s-docs-service-ports-2026-08-24`) does not exist in ../Book-KCNA/sources/ — Stage 2 fetched it but could not write it, and its body survives only inside research-manifest.md §3. The §3 prose carries the matching AUTHOR-REVIEW block for the same reason. Add the question here, after Q8, once R1 lands the snapshot and §3 teaches the fields. -->

---

**9.** **[retrieval: ch4]** A Pod carries labels that a ReplicaSet selects on and labels that a Service selects on. Someone edits one of those labels. Name both consequences, and say whether the two controllers coordinate.

A) The Pod leaves both sets simultaneously; the controllers coordinate through the owner reference
B) Only the ReplicaSet is affected; Services select on owner references, not labels
C) Each selector is evaluated independently, so the Pod may drop out of either set, both, or neither
D) Nothing happens until the Pod is restarted, at which point both selectors re-evaluate

---

**10.** Where does Kubernetes record the set of Pods currently backing a Service, and what writes it?

A) In the Service's `status` field, written by kube-proxy
B) In EndpointSlice objects, written by the EndpointSlice controller
C) In the Pods' annotations, written by the kubelet
D) In cluster DNS, written by CoreDNS

---

**11.** **[retrieval: ch5]** Chapter 5 said a readiness probe controls whether a Pod receives traffic. Name the object that fact is actually implemented in, and say what a failing probe changes about it.

A) The Pod's `status.phase`; a failing probe moves the Pod to `Failed`
B) The Service's `spec.selector`; a failing probe removes the Pod's labels from it
C) The EndpointSlice; a failing probe removes the Pod's address from the Service's endpoints
D) The node's iptables rules; a failing probe causes kube-proxy to drop packets to the Pod

---

**12.** `kubectl get endpointslices -l kubernetes.io/service-name=web` returns a slice with no endpoints. The Pods you expect are Running. What are the two usual causes?

A) kube-proxy is not running, or the CNI plugin is misconfigured
B) The Service's selector does not match the Pods' labels, or the Pods are not Ready
C) The Service's DNS record has not propagated yet, or the slice you fetched is a stale cached read
D) The Pods are in a different namespace from the Service, or the Service was created before the Pods existed

---

**13.** A colleague reports: "I created the Service, it has a cluster IP and a DNS record, but nothing responds and there are zero endpoints." What is the correct characterisation?

A) The Service failed to create properly and should be deleted and recreated
B) Nothing is wrong with the Service — it is being reconciled correctly against a set that is currently empty
C) The API server rejected the selector and defaulted it to empty
D) The DNS record proves the Service works; the problem must be in the client

---

**14.** What does setting `.spec.clusterIP` to `None` do, and which workload type requires it?

A) Reserves the Service's name in DNS without allocating any endpoints; required by CronJobs
B) Makes the Service reachable only from inside the cluster, with no external path; required by StatefulSets for Pod network identity
C) Creates a headless Service — DNS returns the Pod addresses directly instead of one virtual IP; required by StatefulSets for Pod network identity
D) Removes the Service's selector, so its endpoints must be maintained by hand; required by Deployments with more than one replica

---

**15.** You are migrating a database into the cluster. Today it runs on external hardware; next month it will run as Pods. You want in-cluster clients to use one unchanging Service name throughout, with traffic proxied by the cluster in both phases. What do you configure today?

A) A `type: ExternalName` Service pointing at the database's hostname
B) A headless Service with no selector
C) A Service with no selector, plus manually managed EndpointSlices holding the external address
D) A `type: ExternalName` Service now, swapped for a selector-based Service on migration day

---

**16.** kube-proxy's modes on Linux are:

A) userspace (default), iptables, IPVS
B) iptables (default), IPVS, nftables
C) iptables, IPVS (default), eBPF
D) nftables (default), iptables, kernelspace

---

**17.** An engineer SSHes to a worker node and runs `ss -tlnp` looking for a process bound to a Service's cluster IP. What will they find, and why?

A) kube-proxy, because it terminates connections to cluster IPs and forwards them
B) One of the backend Pods, because kube-proxy binds the cluster IP to a chosen endpoint
C) Nothing — the cluster IP is virtual, existing only as a forwarding rule that captures and readdresses traffic
D) CoreDNS, because it owns all cluster-internal addresses

---

**18.** Your cluster is running normally, serving traffic to Services, and there are no kube-proxy Pods anywhere. What is happening, and which of §1's four rules is the same component also satisfying?

A) The cluster is broken and Services are failing silently; no rule is being satisfied
B) The network plugin implements Service packet forwarding itself — and the same plugin implements the Pod network, satisfying the rule that all Pods can reach all Pods directly
C) The control plane is proxying Service traffic through the API server; rule 4, node-agent reachability
D) Services are being resolved by DNS to Pod IPs directly, bypassing the need for a proxy; rule 1, unique Pod addresses

---

**19.** *Not multiple choice — write the two names out before checking.* A Pod in namespace `billing` must reach a Service named `ledger` in namespace `payments`. The Service exposes a port named `http` over TCP, and the cluster uses the default cluster domain. Write (a) the name the Pod would use for an ordinary address lookup, and (b) the SRV name that would return the port number and hostname for that named port.

---

**20.** A StatefulSet's three Pods sit behind a headless Service. A client resolves the Service's name and receives three addresses rather than one. What served that answer, and what name form reaches one specific member?

A) kube-proxy served it from its endpoint cache; individual members are reached at `<pod-ip-dashed>.<namespace>.pod.cluster.local`
B) CoreDNS, the cluster's DNS addon, served it from the Service's endpoints; individual members are reached at `<pod-name>.<service-name>.<namespace>.svc.cluster.local`
C) The API server served it directly; individual members are reached by appending an ordinal to the Service's own name
D) CoreDNS served it, but only the set is addressable — a headless Service deliberately gives up per-member names

---

**21.** **[retrieval: ch4]** Chapter 4 told you a bare service name resolves within the local namespace. What makes that true — what is configured, and by which component?

A) CoreDNS rewrites bare queries to the caller's namespace, using the caller's source IP
B) The Pod's DNS search list contains its own namespace and the cluster's default domain, configured by the kubelet
C) The API server rejects cross-namespace DNS queries unless an FQDN is used
D) kube-proxy scopes DNS traffic per namespace using iptables rules

---

**22.** You meet a Kubernetes networking behaviour this chapter never covered. Applying the chapter's method rather than recalling a fact, which pair of questions will locate it?

A) Which node is the traffic on, and which iptables rule matches it
B) Which object holds the declaration of intent, and which controller is reconciling that declaration into a published answer
C) Which CNI plugin is installed, and which of its features is enabled
D) Which DNS record exists for it, and what address that record returns

---

**Answers with Explanations**

---

**1. B.**

All Pods can communicate with all other Pods, whether on the same node or on different nodes, and Pods can communicate with each other directly, without the use of proxies or address translation [source: k8s-docs-network-model-2026-08-23].

**A** describes a NAT gateway — explicitly forbidden by rule 3. **C** is the each-container-gets-an-IP misconception; every container in a Pod shares the network namespace including the IP address and network ports [source: k8s-docs-pods-2026-08-24]. **D** describes host-port mapping, which is the model Kubernetes replaces; it would be the correct answer for almost any non-Kubernetes container platform, which is precisely why it's attractive.

**2. D. One address, one entry.**

Each Pod is assigned a unique IP address for each address family, and every container in a Pod shares the network namespace including the IP address [source: k8s-docs-pods-2026-08-24]. An EndpointSlice records the Pods currently backing a Service [source: k8s-docs-network-model-2026-08-23] — Pods, not containers.

This is the each-container-gets-an-IP misconception tested at its downstream consequence rather than at its definition. **A** and **B** both assume per-container addressing; **C** assumes per-container endpoints. If you can see that container count and endpoint count are unrelated numbers, the trap has nothing left to catch you with.

**3. B.**

Network plugins use CNI, the Container Network Interface, to implement pod networking, and CNI plugins are external binaries that Kubernetes executes rather than in-process Kubernetes components [source: k8s-docs-extending-kubernetes-2026-08-23].

**A** inverts the relationship — CNI is an interface, not an implementation. **C** invents an API object. **D** confuses two unrelated components: kube-proxy programs node rules via OS APIs, and has nothing to do with CNI.

<!-- AUTHOR-REVIEW: option B and this explanation previously named the kubelet as the executor of CNI plugin binaries. Dropped per curriculum-alignment R3. The cached general page (k8s-docs-extending-kubernetes-2026-08-23) supports "Kubernetes executes external binaries" and mentions the kubelet; Stage 2 recorded that a more specific and more recent page states CNI management was removed from the kubelet in Kubernetes 1.24, with the container runtime loading the plugins. That page is not on disk (see the §1 AUTHOR-REVIEW block), so this item names no executor rather than naming a superseded one. §1's prose still carries the older wording and should be brought into line by the pass that owns it. -->

**4. B.**

ClusterIP exposes the Service on a cluster-internal IP, makes it reachable only from within the cluster, and is the default used if you don't explicitly specify a type [source: k8s-docs-service-2026-08-23].

**A** fails on its first half before the second one matters: NodePort is never a default, it must be asked for, and asking for it would additionally allocate the cluster IP that B describes [source: k8s-docs-service-2026-08-23]. **C** is the near-miss worth naming: ClusterIP alone does *not* expose anything on node IPs. That is what NodePort adds — and the additivity runs one way only. Getting a cluster IP from NodePort is guaranteed; getting node reachability from ClusterIP is not. **D** is not a default either, and it is the one type on this list that cannot function at all without a component Kubernetes does not supply [source: k8s-docs-service-2026-08-23] — which is the subject of question 6.

**5. B.**

To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of `type: ClusterIP` [source: k8s-docs-service-2026-08-23].

**A** is the trap in its purest form — the belief that types are alternatives rather than layers. **C** invents a restriction. **D** confuses an address with a reachability mechanism: the node IPs are *additional* paths, not a substitute address.

**6. C.**

Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider [source: k8s-docs-service-2026-08-23]. With neither present, nothing acts on the request.

**A** is the trap. **B** is wrong because the object is entirely valid — validity and effect are different questions. **D** invents a fallback that would be surprising and undocumented behaviour.

Nothing here is broken and nothing needs fixing. The Service exists and is reconciled; only its external address is absent.

<!-- AUTHOR-REVIEW: this explanation previously closed by asserting that such a Service "still has a cluster IP and, per the additive rule, a node port," and that it remains usable from inside the cluster and from the nodes. Narrowed per fact-accuracy F2. The cached Service snapshot documents additivity for NodePort only ("To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP"); its LoadBalancer entry is a single sentence that says nothing about the rungs beneath it. The keyed answer's "waits indefinitely" is likewise entailed by the sourced premise rather than stated by any snapshot (W2). Both are resolved by the same targeted re-fetch of the type: LoadBalancer subsection; restore the fuller wording once it lands. -->

**7. C.**

ExternalName maps the Service to the contents of the `externalName` field by configuring the cluster's DNS to return a CNAME record with that external hostname value; **no proxying of any kind is set up** [source: k8s-docs-service-2026-08-23]. kube-proxy provides the virtual IP mechanism for Services of type *other than* ExternalName [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23] — so there is no rule to find, because ExternalName is the one type outside its scope.

**A** is the types-are-alternatives trap wearing a diagnostic disguise: a NodePort Service keeps its cluster IP, because Kubernetes sets one up for NodePort Services as well [source: k8s-docs-service-2026-08-23]. There would be rules for both paths, not none. **B** inverts kube-proxy's scope — ClusterIP is the type it most obviously serves. **D** assumes an external load balancer displaces the node-level rules; it does not, because LoadBalancer is inside the "other than ExternalName" set too.

**8. B.**

ExternalName produces a CNAME and no proxying [source: k8s-docs-service-2026-08-23], so the client connects directly to the vendor.

**A** would also work as a way to reach the vendor, but it puts kube-proxy in the path — traffic goes to a cluster IP and is redirected — which is exactly what the question excludes. **C** and **D** are invented configurations; `externalName` is meaningful only with `type: ExternalName`.

**9. C.**

A Service uses labels to allow the control plane to determine which EndpointSlice objects are used for it [source: k8s-docs-garbage-collection-2026-08-24], and a selector is a query over labels. Two controllers evaluating two selectors against one Pod produce two independent results.

**A** confuses ownership with selection — the two mechanisms are explicitly distinguished, and owner references exist so different parts of Kubernetes avoid interfering with objects they don't control [source: k8s-docs-garbage-collection-2026-08-24]. **B** is wrong twice: a Service selects on labels, not on owner references, and the ReplicaSet holds no privileged position over the Service — both are ordinary selector evaluations by ordinary controllers, and neither is told about the other. **D** invents a restart trigger; selectors are evaluated continuously by watching controllers, not at Pod startup.

**10. B.**

Kubernetes automatically manages EndpointSlice objects to provide information about the Pods currently backing a Service [source: k8s-docs-network-model-2026-08-23]; the EndpointSlice controller populates them to provide a link between Services and Pods [source: k8s-docs-cluster-architecture-2026-08-23].

**A** puts the answer in the wrong object and names the wrong writer — kube-proxy *reads* EndpointSlices [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. **C** puts the answer on the wrong object too, and names a component that never participates: the kubelet reports the status of Pods on its own node, whereas endpoint membership is computed centrally by a controller reading the API [source: k8s-docs-cluster-architecture-2026-08-23], not written per-Pod by each node. **D** confuses a publisher with a source of truth: DNS publishes the answer; it does not compute it.

**11. C.**

If a readiness probe fails, the endpoints controller removes the Pod's IP address from the endpoints of all Services that match the Pod [source: k8s-docs-pod-lifecycle-2026-08-23]; a Pod's `Ready` condition means it should be added to the load balancing pools of all matching Services [source: k8s-docs-pod-termination-2026-08-24].

**A** is a real and important distinction: a failing readiness probe does *not* change the Pod's phase, kill it, or restart it. That's the liveness probe's job. The Pod keeps running, keeps being counted by its controller, and simply stops receiving traffic. **B** would mean readiness edits your Service, which it does not. **D** describes a downstream effect (kube-proxy reprograms rules because the slice changed) as though it were the mechanism.

**12. B.**

If the endpoints don't match the Pods you expect, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready [source: k8s-docs-debug-pods-2026-08-23].

**A** names data-plane components, and it is the most tempting option because the symptom presents as a networking failure. But endpoint membership is computed entirely in the control plane, by a controller reading the API [source: k8s-docs-cluster-architecture-2026-08-23]. Neither kube-proxy nor the CNI plugin can empty a slice; both are downstream readers of it.

**C** pairs two instincts imported from outside Kubernetes. DNS propagation delay is a real phenomenon in the public DNS and has no bearing on an EndpointSlice, which you read from the API server directly. And `kubectl` reads through to the API server rather than serving you a cached copy — a stale-read explanation would let you off the hook for a diagnosis you have not made yet.

**D** is the closest of the three, and worth taking seriously. Its first half is real: a Service's selector is namespace-scoped, so Pods in another namespace are never selected — but that is a *special case of the first documented cause*, not a separate one, which is why the option's framing is wrong even where its fact is right. Its second half is flatly wrong and is the reason to reject the pair: creation order does not matter to a control loop. The controller reconciles continuously, so a Service created before its Pods picks them up the moment they appear.

**13. B.**

The Service has an address and a DNS record because those are allocated on creation, independent of whether any Pod matches. The EndpointSlice is empty because the selector's current answer is the empty set — which the controller has computed correctly.

**A** is the instinct to fix by recreation, and it will produce an identical Service with an identical empty slice. **C** invents an API server behaviour. **D** is the reasoning error worth naming: the presence of a name and an address proves that *reconciliation is happening*, not that it found anything.

This is the second instance in the chapter of the same shape — a valid object whose effect depends on something that isn't there. Chapter 10 gives it a name.

**14. C.**

You create headless Services by explicitly specifying `"None"` for `.spec.clusterIP`; for headless Services with selectors, DNS returns A or AAAA records pointing directly to the Pods [source: k8s-docs-service-2026-08-23]. StatefulSets currently require a headless Service to be responsible for the network identity of the Pods [source: k8s-docs-statefulset-2026-08-24].

**B** is the option to dwell on, because half of it is correct. Its workload clause is right — StatefulSets do require a headless Service — and two options here name StatefulSets precisely so that knowing the workload does not hand you the answer. Its definition clause is the confusion this question exists to catch: "reachable only from inside the cluster" is what *ClusterIP* means, a rung on the type ladder. Headless sits on a different axis entirely. It is about whether a virtual IP is allocated at all, not about who may reach one.

**A** invents a behaviour and attaches it to a workload with no Service requirement of any kind. A headless Service with selectors most certainly has endpoints — returning them directly is the entire point.

**D** crosses the two axes of §5's four-cell table. Headless (`clusterIP: None`) and selectorless are independent choices; a Service can be either, both, or neither. Setting `.spec.clusterIP` to `None` does not touch the selector, and Deployments require neither.

**15. C.**

A Service used with a corresponding set of EndpointSlice objects and without a selector can abstract other kinds of backends, including ones that run outside the cluster — an external database, or a workload being migrated [source: k8s-docs-service-2026-08-23].

**A** would give clients the vendor hostname directly, meaning that when you migrate you must change what clients resolve *and* the connection semantics change — no proxying today, proxying tomorrow. The question specifically asks for proxying in both phases. **B** removes the single address, which the clients want.

**D** is the plan most teams actually propose, and it is worth understanding why it loses to C rather than merely being wrong. Today it behaves exactly like A: a CNAME with no proxying [source: k8s-docs-service-2026-08-23], so the connection semantics still change on migration day. And the swap is a visible cutover, which is the thing the requirement was written to avoid. C keeps one name, one cluster IP, and one proxying path throughout; the only thing that changes is the contents of a slice.

The migration itself follows from the two facts above rather than from any documented procedure: add the selector, and the controller takes over the slice you had been writing by hand. Clients notice nothing.

**16. B.**

On Linux, the available modes are iptables (the default), IPVS, and nftables (GA since Kubernetes 1.33); on Windows there is only kernelspace [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23].

**A** names a mode that is not among the documented Linux modes. **C** mislabels the default and lists eBPF, which is a plugin data plane rather than a kube-proxy mode. **D** mislabels the default and places the Windows-only mode in the Linux list.

**17. C.**

kube-proxy configures the node to capture traffic to the Service's `clusterIP` and port and redirect it to one of the Service's endpoints [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. Capture-and-redirect is not the same as listen-and-forward. Nothing binds the address.

**A** and **B** both assume something terminates the connection at the cluster IP. **D** confuses DNS with addressing entirely — CoreDNS answers name queries; it owns no addresses.

**18. B.**

If you use a network plugin that implements packet forwarding for Services by itself, providing equivalent behavior to kube-proxy, you do not need to run kube-proxy [source: k8s-docs-cluster-architecture-2026-08-23]; Cilium can act as a replacement [source: k8s-docs-cluster-addons-2026-08-24]. And the plugin implementing Service forwarding is the same plugin implementing Pod networking via CNI [source: k8s-docs-extending-kubernetes-2026-08-23] — so it is also satisfying the model's requirement that all Pods reach all Pods directly [source: k8s-docs-network-model-2026-08-23].

**A** assumes kube-proxy's absence is a defect. **C** invents API-server proxying. **D** describes headless-Service behaviour and generalises it to every Service, which is wrong for anything with a cluster IP.

**19.**

**(a) `ledger.payments.svc.cluster.local`**

A normal Service is assigned an A or AAAA record of the form `my-svc.my-namespace.svc.cluster-domain.example`, resolving to the Service's cluster IP [source: k8s-docs-dns-pod-service-2026-08-23]. With the default cluster domain that is `<service-name>.<namespace-name>.svc.cluster.local` [source: k8s-docs-namespaces-2026-08-23].

**(b) `_http._tcp.ledger.payments.svc.cluster.local`**

Named ports get an SRV record of the form `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example` [source: k8s-docs-dns-pod-service-2026-08-23]. The two leading underscore labels are the port's name and its protocol, in that order, prefixed onto the ordinary Service name from part (a).

Two things to check yourself on. First, the shape is stable: everything to the right of the Service name is the same in both answers, and the SRV form only prepends. If you wrote something with `payments` and `ledger` in the other order, that is the error to fix before exam day, because it will produce a name that resolves to nothing rather than an error you can read.

Second — and this is the part that costs points — the bare name `ledger` is not an answer to either half. From a Pod in `billing`, a bare name is tried against that Pod's own search list, which begins with its own namespace [source: k8s-docs-dns-pod-service-2026-08-23]. It will not reach `payments`. If a `ledger` Service also happens to exist in `billing`, the bare name will resolve — to the wrong one, silently.

**20. B.**

DNS is a built-in Kubernetes service launched automatically as a cluster addon [source: k8s-docs-dns-cluster-addon-2026-08-24], and CoreDNS is what serves it [source: k8s-docs-cluster-addons-2026-08-24]. For headless Services with selectors, DNS returns A or AAAA records pointing directly to the Pods [source: k8s-docs-service-2026-08-23] — three addresses for three Pods, which is exactly what the client saw. Individual members of a StatefulSet are addressable at `$(podname).$(governing service domain)` [source: k8s-docs-statefulset-2026-08-24], which expands to the form in B.

Note that both halves of the answer come from the same place. The set and the member are two questions put to one component.

**A** is wrong on both halves. kube-proxy has no role in name resolution at all — and in a headless Service there is no virtual IP for it to program in the first place. The `pod.cluster.local` form it names is real, but it is the Pod record, keyed on a dashed rendering of the Pod's IP address [source: k8s-docs-dns-pod-service-2026-08-23], which is exactly the unstable identifier a StatefulSet exists to avoid.

**C** puts the API server in the DNS path, which it never occupies, and grafts the ordinal onto the wrong label. The ordinal is already inside the Pod's own name; the member's name is the Pod name under the governing Service's domain, not the Service name with a number attached.

**D** inverts the reason headless exists. Per-member addressability is the point, and it is why a StatefulSet requires a headless Service to be responsible for the network identity of its Pods [source: k8s-docs-statefulset-2026-08-24].

**21. B.**

By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain [source: k8s-docs-dns-pod-service-2026-08-23], and the kubelet configures Pods' DNS so that running containers can look up Services by name [source: k8s-docs-dns-pod-service-2026-08-23].

**A** would be a plausible design and is not the one used; the behaviour is ordinary DNS search-domain resolution on the *client* side, not rewriting on the server side. **C** invents an API server role in DNS. **D** invents a kube-proxy role in DNS.

Converting the rule into a mechanism is the point of this item. Once you know it's a search list, the cross-namespace failure mode stops being arbitrary: the caller's own namespace is tried *first*, so a same-named local Service wins, silently.

**22. B.**

This is the only question in the set that tests the method rather than a fact, and it is the one worth carrying out of the chapter. Every mechanism in §1 through §7 had the same two-part shape. A Service declares a selector; the EndpointSlice controller publishes the current answer [source: k8s-docs-cluster-architecture-2026-08-23]. An EndpointSlice declares a set of endpoints; kube-proxy watches the Service and EndpointSlice objects and maintains the node's rules accordingly [source: k8s-docs-virtual-ips-kube-proxy-2026-08-23]. A Service's name declares an identity; cluster DNS publishes what it currently resolves to. Find the object and find the loop, and you have located a behaviour you have never read about.

**A** is a node-level answer to a cluster-level question. It describes one implementation kube-proxy happens to use on Linux today — and the mode is configurable and the component itself optional [source: k8s-docs-cluster-architecture-2026-08-23], so the method fails on the first cluster that does it differently.

**C** assumes the plugin is where every networking answer lives. It is where the *model* is implemented, but Services, endpoints and names are API-level and are the same whichever plugin you installed.

**D** stops one step short, and stops in the same place question 10's option D did: DNS publishes answers, it does not compute them. Naming the publisher without naming the loop behind it leaves you able to read the current state and unable to explain why it is what it is.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **Network model** | Four rules: unique cluster-wide Pod IP; all Pods reach all Pods; **no NAT, no proxies**; node agents reach local Pods |
| **Pod IP** | Belongs to the **Pod**. Containers share it and use `localhost` |
| **CNI** | Kubernetes **defines** the model; a **plugin implements** it. Second of **the four pluggable interfaces** this book tracks |
| **Service** | A stable, long-lived address for a set of Pods **that is expected to change**. An object, not a running thing |
| **ClusterIP** | The **default** type. Inside the cluster only |
| **NodePort** | Every node's IP at a static port — **and also a cluster IP** |
| **LoadBalancer** | Exposed externally by a load balancer **the provider supplies. Kubernetes supplies none** |
| **ExternalName** | A **CNAME**. Not on the ladder. **No proxying of any kind** |
| **Selector** | The **question**. A query over Pod labels |
| **EndpointSlice** | The **written-down answer**, maintained by the EndpointSlice controller |
| **Readiness** | The **gate**. Matching the selector is necessary and not sufficient |
| **Empty endpoints** | Selector mismatch, **or** Pods not Ready. Two bugs, two files |
| **Headless** | `clusterIP: None` — deliberate. DNS returns the Pod addresses. StatefulSets need one |
| **No selector** | Supported. Manually managed EndpointSlices, for backends outside the cluster |
| **kube-proxy** | Virtual IP for **every type but ExternalName**. Watches Service + EndpointSlice. **iptables is the default** |
| **Cluster IP** | **Virtual.** kube-proxy captures traffic addressed to it and redirects; nothing is listening. A **rule, not a socket** |
| **Cluster DNS** | **CoreDNS**, a built-in addon, serves every record below. It publishes the answer; it does not decide it |
| **Service DNS** | `<service>.<namespace>.svc.<cluster-domain>` — cluster IP for normal, **all Pod IPs for headless** |
| **Bare name** | **Local namespace only.** May succeed against the wrong Service |
| **The Zenith** | A Service is a **label query with a name**. Three loops publish its answer in three formats |

<!-- AUTHOR-REVIEW: LoadBalancer row narrowed per the fact-accuracy finding on
     additivity. The cached `k8s-docs-service-2026-08-23` snapshot documents the
     cluster-IP allocation for NodePort only ("Kubernetes sets up a cluster IP
     address, the same as if you had requested a Service of type: ClusterIP"); its
     LoadBalancer entry is one sentence and says nothing about a cluster IP or a node
     port. Restore "on top of NodePort" here, in §3's Fixed Point, in the Exam Alert
     and in the Common Traps table together — not piecemeal — once the targeted
     re-fetch of the Service page's `type: LoadBalancer` subsection lands in sources/.
     The "Kubernetes supplies none" half is separately sourced and stands as written. -->

<!-- AUTHOR-REVIEW: The Voyage Progress strip below reads "Ch 9 of 17". The binding
     B6 section skeleton runs Ch 1-20 (Ch 19 synthesis, Ch 20 mock exam). Either the
     strip counts a subset it does not name, or the denominator is stale. Left as
     shipped because no diagnostic adjudicated it and the other chapters' strips are
     not visible from this pass — confirm the figure once and sweep every chapter
     together. -->

---

🏆 **Safe Harbor** — the cluster's own network, and every object that names it.

You arrived at this chapter able to run workloads and unable to connect them. You now know what guarantees the cluster network makes, what a Service actually is, how its backends are computed and gated, what programs the node, and what the reader — sorry, the *client* — types. A Service is a name on the chart: what sits under it changes with the tide, and the name does not.

That is the inside of the cluster accounted for. Domain 2's Networking competency runs wider than one chapter — traffic arriving from outside, and the policy that decides which of it is allowed, is Chapter 10's work — but Chapters 10, 13 and 16 all stand on what you just finished.

**Voyage Progress:** 🗺️ → 🌊 **Ch 9 of 17** → 🌅

---

## The Voyage Ahead

Everything you just learned works inside a boundary — water the cluster itself controls, where every address in play is one the cluster handed out.

Every name resolved to something already on this side of it. Every address was reachable by things already inside. NodePort and LoadBalancer reach outward, but only by *opening a door* — a port on every node, an address from a provider. Neither of them knows or cares what comes through it. They move packets to a Service, and the Service moves them to a Pod, and at no point does anything open the crate to see what the cargo is.

That's the ceiling §3 named. One external address per Service, which does not scale past a handful. No protocol awareness at all, so `shop.example.com/checkout` and `shop.example.com/catalog` are indistinguishable to every mechanism in this chapter.

Chapter 10 crosses the boundary. It introduces the objects that route on the *contents* of an HTTP request — hostnames, paths, headers — so that one address can serve many services, and something standing at the entrance finally reads the writing on the crate before deciding where it goes. It explains why the Kubernetes project now recommends one API over the one most people learned first, and what "frozen" means in that recommendation, which is a more precise word than it looks and worth exactly the attention you'd give a definition on an exam. And it introduces NetworkPolicy, which is what rule 2's *"barring intentional network segmentation"* was quietly gesturing at all along *[cross-bearing: see Ch 10 §6 — NetworkPolicy]*.

It also opens with an object that you create, and that does nothing at all — because the component that acts on it has not been installed. You have seen that shape twice in this chapter now. Chapter 10 gives it a name, and once it has a name you will start seeing it everywhere.

> *"A light is known by its character, not its position — and only because someone ashore keeps it burning to the same pattern."*
> — Lodestar Ledgers

