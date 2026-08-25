I have the full context — the five book-outline stages, the thirteen published cross-bearings pointing into Chapter 9 (two of them section-pinned), Chapter 8's Voyage Ahead handoff, and the cached networking source set. Here is `outline.md` for Chapter 9.

---

```markdown
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

# Chapter 9 Outline — Every Pod Has an Address

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 9: Every Pod Has an Address` | required | top |
| `## *"Flat networks, stable names, and the abstraction that survives churn"*` | required | line 2 |
| Metadata line (domain / weight / complexity / novelty) | required | after subtitle — **conform to the shipped ch-02/-05/-07/-08 house form**, carrying the published 28% domain weight with the CNCF source tag inline plus the authored-allocation disclaimer |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings — **and this one opens Part III**, see below |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings #1–#3` | **required, min 2** | after §3, §5, §7 |
| `★ Fixed Point` ×7 | **required, min 1** | §1, §2, §3, §4, §5, §6, §7 |
| `**Dead Reckoning:**` ×1 min | **required** | §7 — the record shapes stated flat, no maritime register at all. See §7 |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §3 (the ladder is additive; ExternalName is not on it), §7 (the bare name does not cross namespaces) |
| `☀️ Zenith` | expected | §8 |
| `## Exam Alert! 🚨` | **required** | after §8 |
| `## Practice Questions` | **required** | 21 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19; hands to Ch 10 |
| `🏆 Safe Harbor` | expected | chapter close |

**Heading form.** `## ⚪ §1 — Title`, matching Chapters 5–8. Difficulty glyph before the section number.

**Zenith:** exactly one, per Part 18.10. `ch09-zenith-stable-name-over-churn` in §8.

**This chapter opens Part III, and Chapter 8's Voyage Ahead told the reader so.** Chapter 8 closed by naming the question Part II had been carefully not asking — nothing in eight chapters had to *reach* anything else — and ended on a specific promise: *"Chapter 9 opens by giving every Pod an address, and then explaining why that is not enough."* Honour that literally. §1 gives the address; §2 explains why it isn't enough. Chapter 8's `AUTHOR-REVIEW` note at line 108 also records that it **deliberately removed** the assertion "Every Pod gets an address" as unsourced in its own snapshot set, explicitly leaving the claim for this chapter to establish properly. §1 is where that debt is paid, and it must be paid with a source tag on it.

**Attention Budget guidance for drafting.** Eight sections, five distinct costs:

| Section | Cost | Why |
|---|---|---|
| §1 | **high** | Short, but it replaces a model rather than extending one. The no-NAT rule contradicts what most readers know about networks, and contradiction costs more attention than novelty |
| §2 | low | One idea, and Chapter 8's closing paragraph already built the tension. This section resolves it and gets out |
| §3 | **high** | The chapter's most examinable block. Four types, three of B1's traps, and one structural insight (the ladder is additive) that the type list alone does not give |
| §4 | medium | One mechanism and one gate. The mechanism is familiar (a selector); the gate — readiness — is the part the reader does not expect |
| §5 | medium | Two deliberate exceptions. Only comprehensible against §3 and §4, which is why they are here and not there |
| §6 | low | One component, one job, four modes. Mostly recognition, and it is the chapter's arousal-restoration point between two high-cost blocks |
| §7 | **high** | Name shapes are close to pure recall, and the bare-name-versus-FQDN rule is the chapter's cleanest trap |
| §8 | low | Synthesis |

*"If you only have 15 minutes"* should point at **§3's type ladder and §7's record shapes**, then Bearings #3. Those are the two blocks where this chapter's exam points concentrate. §1 is the most important section for *understanding* and the least likely to be tested directly — say so plainly rather than pretending the two coincide.

**Session split.** Recommend two sessions with the break after ☆ Taking Your Bearings #2. That gives §1–§5 (the model, the abstraction, the backends) in one session and §6–§8 (the implementation, the names, the synthesis) in the other, and it separates the two high-cost blocks §3 and §7 into different sessions, which the alternative split does not.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 9 — Every Pod Has an Address". Carried forward without modification:

- **Covers**: **D2.1** — the Kubernetes network model; Pod IP and shared namespace; CNI; Service; ClusterIP; NodePort; LoadBalancer; ExternalName; headless Services; Services without selectors; EndpointSlice; the service proxy; kube-proxy modes; CoreDNS; Service and Pod DNS records; FQDN.
- **Prerequisites**: Ch 4 (labels, selectors), Ch 5 (Pod network namespace), Ch 6 (Pod churn under controllers).
- **Retrieval targets**: **20%** **[B3]**, from Ch 5–8, with the ≥4-back spacing floor satisfied by **Ch 5 (Pod shared network namespace — exactly four back)**. Named anchors: selectors → Service; controller churn.
- **Question budget**: 8 Soundings · 10 Bearings · 21 Practice. Bearings set at 15 below, per B4's "minimums to exceed" and the shape Chapters 3–8 shipped.
- **Figures**: six anchors, listed verbatim in `figures_planned`.
- **Depth band**: substantial.
- **Blocking gaps**: G11 (CNI), G13 (CoreDNS, DNS for Services and Pods), G24 (kube-proxy modes). **Status: G13 and G24 are CLOSED** — `k8s-docs-dns-pod-service-2026-08-23.md` and `k8s-docs-dns-cluster-addon-2026-08-24.md` close G13 outright; `k8s-docs-virtual-ips-kube-proxy-2026-08-23.md` closes G24 outright, including the mode list. **G11 is PARTIALLY closed and is this chapter's one blocking gap** — see § Open questions #2.
- **Note**: CNI planted here is the second of the four pluggable interfaces resolving in Ch 17's secondary Zenith. Chapter 2 already published the forward pointer by section number.

**Two gaps the arc outline did not anticipate** are open, one of them consequential — see § Open questions #3 (Service port mechanics) and #4 (EndpointSlice's own shape).

### Debts falling due in this chapter

**Thirteen published cross-bearings point at Chapter 9**, two of them pinned to a section number. Draft knowing the reader was told to expect each one.

| Owed by | Promise made | Paid in |
|---|---|---|
| `chapter-02` line 600 | *"Ch 9 §1 — CNI and pod networking"* — **section-pinned**, and part of the four-interface set-up whose other three members are Ch 6, Ch 11 and Ch 17 | **§1** |
| `chapter-03` line 459 | *"Services, and how kube-proxy implements them"* | **§2 introduces, §6 implements.** The promise names both halves; pay both |
| `chapter-03` line 603 | *"CoreDNS as the cluster DNS addon, and the Service DNS records it serves"* | **§7** |
| `chapter-04` line 588 | *"cluster DNS, Service records, and FQDNs"* — Chapter 4 gave the reader the name form in **one sentence** and explicitly deferred the mechanism, what serves the records, what else gets one, and how resolution proceeds | **§7**, and all four sub-promises must be discharged |
| `chapter-04` line 835 | *"a Service selects its backends"* — dropped inside the labels-as-universal-join paragraph | **§2 names it, §4 mechanises it** |
| `chapter-05` line 365 | *"why a Service is necessary"* — and the prose says the Pod-IP-changes fact *"is the premise of Chapter 9"* | **§2** |
| `chapter-05` line 858 | *"Ch 9 §4 — readiness and Service endpoint membership"* — **section-pinned**. Chapter 5 taught readiness probes and told the reader that this is the mechanism doing the removing | **§4** |
| `chapter-06` line 431 | *"this churn is exactly why something needs a stable name"* | **§2** |
| `chapter-06` line 485 | *"a Service selects its backends with the same mechanism, which is a different controller reading the same labels"* | **§4** |
| `chapter-06` line 537 | *"EndpointSlice, the object behind a Service's endpoints"* — dropped in an answer key that already taught the labels-versus-ownership distinction | **§4** |
| `chapter-06` line 870 | *"headless Services and stable DNS names"* — Chapter 6 said StatefulSets require one and that you must create it yourself | **§5**, with the DNS half in **§7** |
| `chapter-06` line 890 | *"CNI plugins and how Pod networking gets implemented"* — Chapter 6 noted cluster networking plugins ship as DaemonSets | **§1** |
| `chapter-07` line 881 | *"Services and endpoints"* — Chapter 7 argued that a Service's backends being on distinct nodes is what makes it resilient rather than merely load-balanced | **§4**, one clause |

**On the two section pins.** Unlike Chapter 8, this chapter's numbering is *not* free. §1 must be the CNI-and-pod-networking section and §4 must be the readiness-and-endpoint-membership section. Both fall out naturally from the pedagogy — the flat model must come first and EndpointSlice must come after the Service types — so the constraint costs nothing here. Recording it because a later restructure would silently break two shipped chapters.

**On `chapter-06` line 537.** Chapter 6 has already done half of §4's work. Its answer key states that a Service uses labels to determine which EndpointSlices belong to it *and* that each EndpointSlice additionally carries an owner reference, because ownership and selection are different mechanisms. §4 should retrieve that in one clause rather than re-deriving it. The reader was given the distinction in a context where it was surprising; meeting it again where it is load-bearing is the spacing effect working as designed.

### What this chapter owes forward

| Owed to | What | Why it matters |
|---|---|---|
| **Ch 10** | **The Service-type ladder, intact** | Ch 10's entire argument for Ingress is *"LoadBalancer gives you one external address per Service, and that does not scale."* That argument is unavailable unless §3 has established the ladder and its ceiling. Ch 10 must not re-teach Services |
| **Ch 10** | **A concrete instance of "the object exists but nothing happens without the component"** | Cross-cutting theme #3. **[B3]** designates Ch 10 as the place the pattern is *named*. §4 supplies an earlier and cleaner instance — a Service whose selector matches nothing still gets an IP and a DNS record — which Ch 10 can retrieve as its second example. See § Open questions #5 |
| **Ch 11** | **Headless Services** | Ch 6 introduced StatefulSet and deferred both halves of its identity story. §5 supplies the network half; Ch 11 supplies the storage half and closes the book's one deliberate forward reference |
| **Ch 13 and Ch 16** | **Empty endpoints as a failure signature** | §4 states the fact (no endpoints ⇒ selector mismatch or Pods not Ready). Ch 13 and Ch 16 own the *workflow*. The callback map names "Service→EndpointSlice (Ch 9)" as a mandatory Ch 16 anchor, so §4 must state it in a form Ch 16 can retrieve by name |
| **Ch 17** | **CNI as the second of four pluggable interfaces** | The book's secondary Zenith. Chapter 2 published the pointer by section number; §1 must make CNI's role explicit enough that Ch 17 can collect it rather than introduce it |
| **Ch 17** | **The flat network model as the mesh's precondition** | A sidecar that intercepts a Pod's traffic only makes sense against §1's model. One forward cross-bearing, no content |

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**Open by paying Chapter 8's promise in the first line, and then immediately undercutting it.** Chapter 8 said this chapter opens by giving every Pod an address and then explains why that is not enough. So: every Pod in the cluster has its own IP address, unique across the whole cluster, and any Pod can reach any other Pod at that address directly — no NAT, no proxy, no port mapping, whether they are on the same machine or on machines in different racks. State it plainly, with the source tag, because Chapter 8 deliberately refused to state it. Then, in the next breath: and that address is worth almost nothing, because Chapter 6 taught the reader that a controller may replace any Pod at any moment and the replacement is a different Pod with a different address. **The chapter's whole subject is the gap between those two sentences.**

**The identity frame is the shift from placement to reachability.** Everything from Chapter 2 through Chapter 8 was about getting a workload *onto* something — into a container, onto a node, under a controller, past an admission gate. This is the first chapter where two things have to find each other. Practitioners describe this as the moment Kubernetes stops feeling like a fancy scheduler and starts feeling like a platform, and the reason is specific rather than sentimental: the flat network model is an unusually strong constraint, and once you have it, a large class of problems that dominate ordinary infrastructure work — port collisions, address translation, host-and-port coordination, service registries — simply stop existing. Say what the model buys. Do not gush about it.

**Part III opens here, and the Why section carries that.** Chapter 8's closing paragraph already framed Part III as *"addresses, the abstraction that makes them survivable, how names resolve, and how anything outside the cluster gets in at all"* — that is Chapters 9 through 13, and the first three clauses are this chapter. One sentence placing the reader in the new Part is enough; the book does not use in-chapter Part openers, so this prose is the only place the boundary is visible.

**The curiosity gap, planted as a question.** The chapter's Zenith is that nothing here is new either — that a Service turns out to be a label query with a name attached, reconciled by a control loop, and that the reader has met every one of those pieces already. Plant the doubt without the answer: *there is one object in this chapter, and it does not do anything.* That is deliberately hard to believe about the object the whole of Kubernetes networking is built on, and §8 pays it off.

**The stakes, stated flat.** Seven points on this book's authored allocation — CNCF publishes four domain weights and no competency weights, and the front matter says so. What the number understates is that D2.1 is the largest single competency in Domain 2 and the one the rest of the domain depends on: Chapter 10 cannot teach Ingress without it, and Chapter 13 cannot teach Service troubleshooting without it. **Do not manufacture urgency.** The material is intrinsically interesting and the reader will notice if it is oversold.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Six outcomes, active verbs:

- **State** the four rules of the Kubernetes network model, and name the thing that implements them — which is not Kubernetes.
- **Explain** why a Pod's own IP address is insufficient for anything a client needs to keep talking to, using the churn a controller creates.
- **Choose** between ClusterIP, NodePort, LoadBalancer and ExternalName for a given exposure requirement — and say which three are layers of the same mechanism and which one is not a layer at all.
- **Trace** the path from a Service's selector to the set of addresses traffic actually reaches, and name the condition a Pod must satisfy to be on that list.
- **Write** the DNS name of a Service in another namespace, and say what a bare name would have resolved to instead.
- **Recognise** the whole apparatus — the virtual IP, the endpoint list, the DNS record — as one control loop reconciling the answer to a label query, which is the only thing you actually have to remember.

*You'll also stop thinking of a Service as a load balancer, which is the single most useful correction in this chapter and the one that makes Chapter 10 straightforward instead of confusing.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Prerequisite set per B2: Chapter 4 (labels, selectors, and the one-sentence DNS plant), Chapter 5 (the Pod network namespace), Chapter 6 (Pod churn under controllers), plus ordinary networking literacy about NAT, service discovery and private networks. **Four questions are deliberate retrieval from Chapters 4, 5 and 6; four test priors the reader arrives with.** **[B3]** Soundings sit outside the retrieval budget but do retrieval work anyway, sourced from B2's Prerequisites column.

**Fixed Points this chapter teaches, which Soundings must therefore not reveal:**

1. Every Pod gets its own unique **cluster-wide** IP; all Pods can reach all Pods, on the same node or across nodes, **without NAT and without proxies**; agents on a node can reach all Pods on that node.
2. Kubernetes **defines** the network model and **implements none of it**. A CNI network plugin does — and Kubernetes ships none by default.
3. A Service is a stable, long-lived IP address or hostname for a set of Pods that changes over time. **ClusterIP is the default type.**
4. The types are additive: NodePort **also** allocates a cluster IP, exactly as if you had asked for ClusterIP. ExternalName is not on the ladder at all — it is a DNS CNAME with **no proxying of any kind**.
5. Kubernetes **does not offer a load-balancing component**. You supply one, or you integrate with a cloud provider.
6. A Service finds its backends by selector; the result is written into **EndpointSlice** objects by a controller; and a Pod that is not Ready is not on the list.
7. `clusterIP: None` is a deliberate configuration, not a broken one — DNS returns the Pod addresses directly instead of one virtual IP. A Service **without** a selector is likewise a supported pattern, backed by manually managed EndpointSlices.
8. kube-proxy implements a virtual IP mechanism for every Service type **except ExternalName**, by watching Service and EndpointSlice objects and programming each node. Modes: iptables (default), IPVS, nftables, and kernelspace on Windows.
9. `my-svc.my-namespace.svc.cluster-domain.example` resolves to a normal Service's cluster IP — and **the same name form** on a headless Service resolves to the set of Pod IPs instead.
10. A bare service name resolves only within the client Pod's **own** namespace, because the default DNS search list contains it.

Each question below is checked against that list.

| # | Question topic | What it tests | Spoiler check |
|---|---|---|---|
| 1 | You are running three interchangeable copies of a service. One dies and is replaced by a copy at a different address. What does a client need so nobody has to go and tell it the new address — and name two mechanisms you have seen do that job | The indirection prior, in its general form. Nearly every reader has one — a load balancer, a DNS name, a service registry | Names nothing Kubernetes-specific. Fixed Point #3 is that Kubernetes' answer is a **first-class API object with a selector**, and #4 that it comes in four types that layer. A general instinct for indirection supplies neither, and the reader who has the instinct will find §2 satisfying rather than redundant |
| 2 | **Retrieval from Ch 5 §2.** Chapter 5 said a Pod has one network namespace shared by all its containers. Two containers in one Pod both want to listen on port 8080. What happens? And how does either one reach the other? | The shared-namespace prior — the **≥4-back item in its pre-test position**, and the load-bearing fact for §1's first rule | The reader is retrieving a Chapter 5 fact. Fixed Point #1's new half is *cluster-wide* — that the Pod's address is unique across the whole cluster and directly routable from any other Pod without translation. Knowing that containers share `localhost` says nothing about what happens between Pods, which is the entire subject of §1 |
| 3 | **Retrieval from Ch 6 §4.** A Deployment performs a rolling update and every Pod is replaced. A client somewhere was holding the IP address of one of the old Pods. What happens to that client, and what would have to be true for it not to care? | The churn premise. Chapter 5 line 365 told the reader in as many words that this fact *is the premise of Chapter 9* | Asks the reader to state the problem, not the solution. Fixed Point #3 is the *shape* of the answer — a named object with a stable address and a selector behind it. A reader who answers "it breaks, and it wouldn't care if it were using something that didn't move" has written §2's opening for themselves, which is the ideal outcome |
| 4 | **Retrieval from Ch 4 §7 and Ch 6.** Chapter 4 said a selector is a query over labels, and Chapter 6 said a ReplicaSet finds its Pods that way. Suppose a *different* controller needed to find the same set of Pods, for a different reason. What mechanism would you expect it to use — and what would break if someone edited one Pod's labels? | Cross-cutting theme #5 (labels as the universal join) in pre-test position, and the reasoning §4 depends on | The reader is retrieving a mechanism Chapter 6 already generalised. Fixed Point #6's new content is that the query's *answer* is written down, into an object called an EndpointSlice, by a controller, and that Ready-ness gates membership. None of that is reachable from "it would use a selector" |
| 5 | **Retrieval from Ch 4 §6.** Chapter 4 gave you, in a single sentence, the DNS name form a Service gets. Write it out. Then: a container in namespace `payments` uses only the bare name `database`. Which Service does it reach if there is a `database` Service in both `payments` and `billing`? | The FQDN prior. Chapter 4 stated this explicitly, in one sentence, and deferred everything else here | The reader is retrieving a Chapter 4 fact verbatim, which is exactly what a prerequisite question should do. Fixed Points #9 and #10's new content is *why* the bare name behaves that way (the search list), what serves the records at all, that headless Services reuse the same name form for a different answer, and that Pods get records too. Question 5 reveals none of it |
| 6 | On an ordinary network, a request crosses a NAT boundary. What does the receiving process see as the source address, and name one thing that becomes harder because of it | The NAT prior, which is the model §1 replaces | Deliberately does not mention Kubernetes. Fixed Point #1's force comes from the *prohibition* — the model requires Pod-to-Pod communication without NAT — and that prohibition only lands on a reader who has just remembered what NAT costs them. This question exists to make §1's first rule feel like relief rather than trivia |
| 7 | A platform that manages containers ships with no networking implementation of its own, and expects you to install one before anything works. Give one reason a system would be designed that way, and one cost of the design | The pluggability prior. Chapter 2 taught CRI as exactly this shape, so most readers can reason to it | Fixed Point #2 is that this is Kubernetes' actual arrangement, that the interface is called CNI, and that it is one of four such interfaces. The question asks about the *design pattern* in the abstract; naming Kubernetes' instance of it is §1's work. A reader who answers "so you can choose the implementation, at the cost of nothing working out of the box" has predicted §1's argument, and §1 should acknowledge that when it arrives |
| 8 | Something inside a private network has to be reachable from outside it. Name two mechanisms you have used or seen. For each, say who supplies the box that terminates the outside connection — you, or someone else | The exposure prior, which is §3's frame and the setup for the chapter's least intuitive fact | Fixed Points #4 and #5 are that Kubernetes' four types **layer**, and that Kubernetes provides no load balancer of its own. The question's second clause primes the second fact without stating it: a reader who answers "the cloud provider supplies it" is one step from §3's most-missed point rather than in possession of it |

**Rubric**: standard 6+ / 3–5 / 0–2 per `branded-terms.yaml`. The 0–2 branch carries a specific instruction: **if questions 2, 3 and 4 were the misses, re-read Chapter 5 §2 and Chapter 6 §4 before starting §2.** This chapter's first half is built directly on the Pod's network namespace and on controller churn; without both, §2 reads as a solution to a problem the reader has not felt.

**Note for drafting:** questions 1, 6, 7 and 8 must stay phrased as situations. Question 6 in particular is doing unusual work — it is the only Soundings item in the book so far designed to make the reader remember something *annoying*, so that §1's rule reads as a benefit rather than a specification. Do not soften it into "what is NAT."

---

## 4. Section plan

Eight sections. Two are pinned by number (§1, §4 — see § Debts). The rest follow from a single organising question rather than from a spine imposed on unrelated arcs: **"how do I reach that?"**, asked at eight increasing levels of resolution.

§1 answers it for one Pod reaching another. §2 says why that answer expires. §3 gives the four shapes of a durable answer. §4 says how the durable answer stays correct. §5 gives the two cases where you deliberately don't want one. §6 says what actually moves the packet. §7 says how you find the address without knowing it. §8 observes that all of it was one control loop.

**This is a chapter about an abstraction, and the failure mode is teaching the abstraction before the problem.** The material *wants* to be presented as "here is a Service, it has four types, here are the DNS names." Presented that way it is a vocabulary list. Presented in the order above, every element arrives as an answer to a question the previous section made the reader ask. §2 exists entirely to make §3 necessary; it should be short and should not be folded away.

**One running example threads the chapter.** A frontend Pod that needs a database, deployed as three replicas by a Deployment. §1: both have addresses. §2: the database's addresses change. §3: the database gets a Service. §4: the Service's list updates when the replicas turn over. §5: except when the frontend needs to reach a *specific* replica, which is Chapter 6's StatefulSet problem. §6: here is what happens to the packet on the node. §7: here is what the frontend actually types. §8: none of it was new. Use it deliberately — a single concrete pair costs nothing and keeps eight sections legible as one argument.

### §1 — ⚪ Four Rules and a Plugin

**Section-pinned by `chapter-02` line 600, and it pays Chapter 8's deliberately deferred claim.**

**First, the four rules, stated as rules.** The Kubernetes network model is built out of a small number of requirements, and the reader should meet them as a numbered set because that is how they are examinable and how §8 retrieves them:

1. Each Pod in a cluster gets its own **unique cluster-wide IP address**. A Pod has its own private network namespace, shared by all the containers within it; processes in different containers in the same Pod communicate over `localhost`.
2. The **pod network** (also called the cluster network) handles communication between Pods. Barring intentional network segmentation, all Pods can communicate with all other Pods, **whether on the same node or on different nodes**.
3. Pods communicate **directly, without proxies and without address translation (NAT)**. (One documented exception: on Windows, this does not apply to host-network Pods. State it in a clause; build nothing on it.)
4. **Agents on a node** — system daemons, the kubelet — can communicate with all Pods on that node.

**Second, the observation that makes rule 3 worth a paragraph rather than a line.** This is the chapter's paradigm-shift beat and the payoff for Soundings #6. In ordinary infrastructure, reaching a process means reaching a host and then a port on it, and the address the receiver sees is frequently not the address the sender used. Kubernetes forbids that. The consequence is not aesthetic: it means an application inside the cluster can be written as though every other application is on the same flat network, because it is. Port collisions between different applications stop existing, because they are not sharing a port space. Say what disappears. That is the argument.

**Third, retrieve Chapter 5 in one clause and correct the trap while you are there.** The Pod has the IP; the containers share it. Two containers in one Pod share an address and a port space and can find each other over `localhost`; containers in *different* Pods have distinct addresses and must use IP networking. B1 trap #36 — "each container gets its own IP" — is defused here and nowhere else.

**Fourth, the section's second real idea, and the one Chapter 2 promised by number: Kubernetes implements none of this.** The model above is a specification. Pod networking is implemented by a **network plugin**, and the interface it plugs into is **CNI, the Container Network Interface** — one of the infrastructure extension points Chapter 2 named alongside CRI, CSI and device plugins. The plugin is a binary the kubelet executes. Kubernetes ships no default: Calico, Cilium and Flannel are three of the many implementations, and Chapter 6 already noted that they ship as DaemonSets, which is now a satisfying detail rather than an isolated one. **See § Open questions #2 — the "ships no default" half of this claim is not fully sourced today.**

**Fifth, the practical consequence, which retrieves Chapter 8 at one chapter's distance.** A node whose networking is not correctly configured reports the `NetworkUnavailable` condition — the reader met the node condition list last chapter. This is the shortest possible demonstration that the plugin is not optional infrastructure trivia. One sentence.

**Close by handing to §2, not by summarising.** Every Pod now has an address. The next sentence should be the problem: those addresses belong to Pods, and Chapter 6 taught the reader what happens to Pods.

- **Objectives**: D2.1
- **Concepts introduced**: `network-model`, `pod-ip`, `cluster-wide-ip`, `pod-network-namespace`, `localhost-communication`, `pod-network`, `cluster-network`, `no-nat-rule`, `node-agent-reachability`, `cni`, `container-network-interface`, `network-plugin`, `network-unavailable-condition`
- **Sources**: `k8s-docs-network-model-2026-08-23.md` (all four rules verbatim, including the Windows host-network exception). `k8s-docs-pods-2026-08-24.md` (unique IP per address family; every container shares the network namespace including IP and ports; `localhost` only inside the Pod; containers in different Pods have distinct IPs and cannot use OS-level IPC without special configuration). `k8s-docs-extending-kubernetes-2026-08-23.md` (Network plugins — CNI, the Container Network Interface, to implement pod networking; binary plugins executed by the kubelet). `k8s-docs-cluster-addons-2026-08-24.md` (Calico, Cilium, Flannel as networking providers; Cilium as a CNCF Graduated project). `k8s-docs-nodes-2026-08-23.md` (the `NetworkUnavailable` condition)
- ⚠ **SOURCE GAP — BLOCKING for one clause. See § Open questions #2.** No cached source states that Kubernetes ships **no** network plugin by default, or that a cluster without one has non-functional Pod networking. The cached set supports "CNI is the interface, plugins implement pod networking, here are three plugins" — it does not support "and you must install one." `kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/` closes it
- **Figure**: `ch09-fig01-network-model-four-rules`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — every Pod gets a unique cluster-wide IP, and **all Pods reach all Pods without NAT and without proxies**, same node or not. The Pod holds the address; its containers share it
  - `★ **Fixed Point:**` — Kubernetes **defines** this model and **implements none of it**. A CNI network plugin does
  - `> 🪝 **Snag:**` — "each container gets its own IP" is the most common form of this mistake, and it is usually caused by experience with plain Docker, where it is true. Inside a Pod, the address is the Pod's
  - `> 🔭 **Closer Look:**` — the model is a *requirement*, not a description of a mechanism, which is why implementations differ so wildly: overlay networks, native routing, BGP, eBPF data planes. All of them satisfy the same four rules by completely different means. Deeper than the exam requires
- **Cross-bearings**: back to Ch 2 §4 (**mandatory — the pinned payoff**; CNI was named there as one of four pluggable interfaces and pointed at this section by number); back to Ch 5 §2 (**mandatory** — the Pod network namespace, whose cluster-wide half arrives here); back to Ch 6 §7 (network plugins ship as DaemonSets, which the reader was told to expect); back to Ch 8 §4 (the `NetworkUnavailable` node condition); forward to Ch 10 (NetworkPolicy is the "intentional network segmentation" rule 2 hedges against); forward to Ch 17 §4 (**mandatory** — CNI as the second of the four interfaces, collected into the secondary Zenith)
- ⚠ **Do not teach NetworkPolicy.** Rule 2's "barring intentional network segmentation" is the hook and it must stay a hook. Chapter 10 owns the API, the additive semantics, and the plugin-dependency trap
- ⚠ **Do not teach dual-stack.** The sources say "for each address family" and "A and/or AAAA records"; quote that phrasing where it appears and expand nothing. IPv4/IPv6 dual-stack configuration is above associate tier

### §2 — ⚪ The Address That Doesn't Last

**Short by design. This section's only job is to make §3 necessary — and it discharges three published cross-bearings while doing it** (`chapter-05` line 365, `chapter-06` line 431, and the first half of `chapter-03` line 459).

**Open on the running example and let it fail.** The frontend has the database Pod's address. A rolling update replaces the database Pods. Chapter 6 established that the replacement is a *different Pod*, and §1 just established that a different Pod has a different address. The frontend is now holding a valid-looking address for something that no longer exists. Nothing malfunctioned; the system did exactly what it was designed to do.

**Then generalise it in the documentation's own framing**, which is unusually clear and worth following: if some set of Pods (call them backends) provides functionality to other Pods (call them frontends) inside the cluster, how do the frontends find out and keep track of which IP address to connect to? The set of Pods running at one moment can be different from the set running a moment later. That is the problem statement, and it is worth quoting closely because the exam's framing of Services descends from it.

**Then the answer, stated as an object rather than as a capability.** A Service is a method for exposing a network application running as one or more Pods. It defines a **logical set of endpoints** — usually Pods — along with a policy for making them accessible, and it provides a **stable, long-lived** IP address or hostname that decouples frontends from specific backends. The stable thing is the Service; the unstable things are behind it.

**Name the selector here, in one sentence, and defer the machinery.** A Service most commonly identifies its endpoints with a **selector** over Pod labels — which the reader already knows is a query, from Chapter 4, and already knows is how a ReplicaSet finds its Pods, from Chapter 6. §4 is where the query's answer gets written down. Naming it now and mechanising it later is the honest split; hiding it until §4 would be coy, because Chapter 4 already told the reader this in as many words.

**Then the default, because it is one fact and it is examinable.** `ClusterIP` is the type you get if you do not specify one, and it exposes the Service on a cluster-internal address reachable only from inside the cluster. §3 opens on that and builds outward.

**Close on the correction that is worth more than anything else in the section.** A Service is not a load balancer, a proxy server, or a piece of software. It is a **declaration** — an object, in the sense Chapter 4 established, stating that a set of Pods should be reachable at a stable address. Whether anything is listening, whether any Pod matches, whether the traffic goes anywhere at all: none of that is the Service's doing. Plant that here; §8 collects it.

- **Objectives**: D2.1
- **Concepts introduced**: `service`, `stable-endpoint`, `service-selector`, `clusterip`
- **Sources**: `k8s-docs-service-2026-08-23.md` (Service as a method for exposing a network application; a logical set of endpoints plus a policy for accessibility; the frontend/backend motivation paragraph verbatim; ClusterIP as the default and cluster-internal only; "Services most commonly abstract access to Kubernetes Pods thanks to the selector"). `k8s-docs-network-model-2026-08-23.md` (the Service API provides a stable, long-lived IP address or hostname for a service implemented by one or more backend Pods, where the individual Pods can change over time)
- **Figure**: none. **Part 18.9 reasoning:** this section's content is a *problem statement*, and the diagram that would illustrate it — Pods churning behind a fixed address — is `ch09-zenith-stable-name-over-churn`, drawn once at the end where it means something. Drawing it here would spend the Zenith's impact eight sections early and would violate Part 18.7 by restating prose the reader is already holding
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — a Service is a stable, long-lived address for a set of Pods **that is expected to change**. The churn is not a failure the Service works around; it is the condition the Service exists for
  - `> ⚓ **Worth Securing:**` — "a Service is a load balancer" is the single most durable wrong model in Kubernetes networking, and it is wrong in a specific way: a load balancer is a *thing that runs*. A Service is a *declaration that gets reconciled*. Every confusing thing about Services in the next four sections follows from that distinction
- **Cross-bearings**: back to Ch 5 §2 (**mandatory — pinned payoff**; Chapter 5 said the Pod-IP-changes fact "is the premise of Chapter 9", and this is that premise being used); back to Ch 6 §4 (**mandatory** — the rolling update whose churn this is); back to Ch 4 §7 (the selector as a query over labels, named here and mechanised in §4); back to Ch 4 §4 (spec and status — a Service is an object like any other); forward to **§3** (the four types) and **§4** (how the query's answer is kept current); forward to Ch 10 (the first half of `chapter-03` line 459's promise; the second half is §6)
- ⚠ **Keep this section short.** Its value is entirely in the tension it creates. A §2 that explains Service types, ports, or endpoints has stolen §3's and §4's material and left the reader with no reason to want them

### §3 — 🔵 Four Ways to Be Reachable

**The chapter's most examinable section.** Three of B1's eight Chapter 9 traps live here (#37, #38, #39), and the structural insight the type list alone does not convey is what defuses two of them.

**Teach the three ladder types in order, and make the additivity explicit at each step**, because the additivity *is* the exam content:

- **ClusterIP** exposes the Service on a cluster-internal IP. Reachable only from inside the cluster. This is the default if no type is specified.
- **NodePort** exposes the Service on **each node's IP at a static port**. And — the part candidates miss — to make the node port work, Kubernetes **also sets up a cluster IP, exactly as if you had requested `type: ClusterIP`**. NodePort does not replace ClusterIP; it adds to it.
- **LoadBalancer** exposes the Service externally using an external load balancer, layered on top of the NodePort/ClusterIP arrangement beneath it.

**Then the one that is not on the ladder**, and it should be visibly separated from the other three rather than presented as a fourth item in a list:

- **ExternalName** maps the Service to the contents of its `externalName` field — for example, a hostname like `api.foo.bar.example`. The mapping configures the cluster's DNS to return a **CNAME record** with that external hostname. **No proxying of any kind is set up.** There is no cluster IP, no endpoint list, and nothing intercepts a packet. It is a DNS alias wearing a Service's clothes.

**The second fact that catches people, and it deserves its own beat.** *Kubernetes does not directly offer a load-balancing component.* Choosing `type: LoadBalancer` does not cause Kubernetes to load-balance anything; it signals that an external load balancer should be provisioned, and you must supply one or integrate with a cloud provider. On a bare-metal cluster with no such integration, a LoadBalancer Service sits with no external address indefinitely, and nothing is broken. **This is the chapter's clearest instance of the pattern Chapter 10 will name** — see § Open questions #5.

**Ground the choice, briefly.** One short decision frame: internal-only traffic → ClusterIP; a fixed port on every node, usually for something in front of the cluster → NodePort; a cloud provider that will give you an external address → LoadBalancer; an alias to something that isn't in the cluster at all → ExternalName. Four lines, not a flowchart. The exam tests the definitions and the additivity, not the decision.

**Close by naming the ceiling, because Chapter 10 needs it.** One external address per Service does not scale to fifty Services, and none of these four types knows anything about HTTP — they move packets, not requests. That is exactly the gap Ingress and the Gateway API fill, and saying so in one sentence here means Chapter 10 opens with a problem the reader already has rather than a solution they did not ask for.

- **Objectives**: D2.1
- **Concepts introduced**: `service-type-ladder`, `nodeport`, `loadbalancer`, `externalname`, `cname-record`, `virtual-ip`
- **Sources**: `k8s-docs-service-2026-08-23.md` (all four type definitions verbatim, including "Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP" for NodePort; "Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider" for LoadBalancer; the CNAME mapping and "No proxying of any kind is set up" for ExternalName). `k8s-docs-network-model-2026-08-23.md` (`type: LoadBalancer` as "a simpler, but less-configurable, mechanism for cluster ingress … when using a supported Cloud Provider"; Ingress as protocol-aware HTTP/HTTPS routing, which is the contrast the closing paragraph rests on)
- ⚠ **SOURCE GAP — see § Open questions #3.** Nothing cached covers `port` versus `targetPort` versus `nodePort`, or the default NodePort range. The section as specified above does not need them and is fully sourceable as written; the question is whether the chapter *should* teach them. Decide before drafting
- **Figure**: `ch09-fig02-service-types-ladder`
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `★ **Fixed Point:**` — the three ladder types are **additive**. NodePort also gets a cluster IP; LoadBalancer sits on top of both. Asking for a higher rung does not remove the rungs below it
  - `★ **Fixed Point:**` — **Kubernetes provides no load balancer.** `type: LoadBalancer` asks for one from somewhere else
  - `> ⚠ **Navigational Hazards:**` — ExternalName is not the fourth rung of the ladder. It allocates no address, selects no Pods, and proxies nothing: it is a CNAME record. Every question that treats it as "the type for external things" is testing whether you know that
  - `> 🪢 **Mnemonic:**` — *inside, on every node, out in the world, somewhere else entirely.* Four types, in the order the reader will meet them on the exam
- **Cross-bearings**: back to **§2** (the default type, named there); back to Ch 8 §1 (a Service is created by the same `apply` through the same door — one clause, retrieval only); forward to **§6** (ExternalName is the one type kube-proxy does not implement, which is the same fact from the other side); forward to **§7** (ExternalName's CNAME is a DNS fact, and §7 is where DNS lives); forward to Ch 10 (**mandatory** — the ceiling this section names is Ingress's entire justification)
- ⚠ **Do not teach Ingress, Gateway API, or the Ingress freeze.** Naming the ceiling is the ceiling. Chapter 10 owns all of it, and `frozen ≠ deprecated` is B2's designated most-precise-fact-in-the-curriculum — do not spend it here
- ⚠ **Do not teach `sessionAffinity`, external traffic policies, or `allocateLoadBalancerNodePorts`.** Uncached and above tier

### §4 — 🔵 The List Behind the Name

**Section-pinned by `chapter-05` line 858, and the payoff for three further cross-bearings** (`chapter-04` line 835, `chapter-06` line 485, `chapter-06` line 537). Chapter 5 taught readiness probes and told the reader in as many words that when Chapter 9 explains how a Service knows which Pods to send traffic to, *this is the mechanism doing the removing*. That promise sets the section's shape: the selector is the expected half, readiness is the half the reader was promised and does not have.

**First, the path, in four steps.** The Service carries a selector. The selector is a query over Pod labels. Kubernetes **automatically manages EndpointSlice objects** that record which Pods currently back the Service — populated by the **EndpointSlice controller**, one of the controllers in the kube-controller-manager that Chapter 3 listed, whose stated job is to *provide a link between Services and Pods*. Anything that needs to know the Service's current backends reads the EndpointSlices, not the selector.

**Second, retrieve Chapter 6's distinction rather than re-deriving it.** Chapter 6's answer key already established that a Service uses **labels** to determine which EndpointSlice objects belong to it, and that each EndpointSlice *additionally* carries an owner reference, because selection and ownership are different mechanisms doing different jobs. One clause of retrieval, and the reader gets the satisfaction of a fact that was surprising in Chapter 6 turning out to be load-bearing here.

**Third — and this is the pinned promise — readiness gates membership.** A Pod that matches the selector is not automatically a destination. It has to be **Ready**, in exactly the sense Chapter 5 taught: the readiness probe is what puts a Pod on the list and what takes it off. This is why a new Pod that never reports ready never receives traffic, which is the mechanism Chapter 6 relied on to make rolling updates safe without ever explaining it. Three chapters converge here; say so.

**Fourth, the termination half, because it is the same fact running backwards and it is genuinely subtle.** When a Pod begins graceful shutdown, the control plane evaluates whether to remove it from the EndpointSlices of Services with a configured selector — and workload controllers stop treating it as a valid in-service replica. But endpoints for terminating Pods are **not immediately removed**: a terminating state is exposed through the EndpointSlice API, and terminating endpoints always have `ready: false`, so load balancers will not send them regular traffic. The list is not a boolean membership test; it carries state.

**Fifth, the diagnostic fact — stated as a fact, not as a workflow.** You can look at the list: `kubectl get endpointslices -l kubernetes.io/service-name=<service-name>`. If the endpoints do not match the Pods you expect, there are exactly two usual causes: **the Service's selector does not match the Pods' labels, or the Pods are not Ready.** State those two causes and stop. Chapter 13 and Chapter 16 own the workflow; this is the fact they will retrieve.

**Sixth, one clause paying `chapter-07` line 881.** Chapter 7 argued that a Service's backends landing on distinct nodes is what makes it resilient rather than merely load-balanced. Now the reader can see why: the endpoint list is just a list, and it has no opinion about where the endpoints are. Topology is the scheduler's job, which the reader did two chapters ago.

**Close on the observation that sets up §8 and hands Chapter 10 its example.** A Service whose selector matches nothing is a completely valid object. It has an address. It has a DNS record. Its EndpointSlice is empty, and traffic to it goes nowhere at all. Nothing is broken and nothing has failed — the declaration is being reconciled correctly against a set that happens to be empty.

- **Objectives**: D2.1
- **Concepts introduced**: `endpointslice`, `endpointslice-controller`, `readiness-gated-membership`, `terminating-endpoint`
- **Commands**: `kubectl-get-endpointslices` (the verb is Chapter 8's; only the resource type and the label selector are new)
- **Sources**: `k8s-docs-network-model-2026-08-23.md` ("Kubernetes automatically manages EndpointSlice objects to provide information about the pods currently backing a Service"). `k8s-docs-cluster-architecture-2026-08-23.md` (the EndpointSlice controller "populates EndpointSlice objects to provide a link between Services and Pods"). `k8s-docs-garbage-collection-2026-08-24.md` (a Service uses labels to determine which EndpointSlice objects are used for it; each managed EndpointSlice additionally carries an owner reference — **already cited in Ch 6, retrieved here**). `k8s-docs-pod-termination-2026-08-24.md` (the control plane evaluates removal from EndpointSlices for Services with a configured selector; terminating endpoints are not immediately removed, terminating state is exposed via the EndpointSlice API, and terminating endpoints always have `ready: false`). `k8s-docs-debug-pods-2026-08-23.md` (`kubectl get endpointslices -l kubernetes.io/service-name=${SERVICE_NAME}`; if endpoints don't match the expected Pods, the selector probably doesn't match the Pods' labels, or the Pods are not Ready). `k8s-docs-service-2026-08-23.md` (Services abstract access to Pods thanks to the selector)
- ⚠ **SOURCE GAP — non-blocking. See § Open questions #4.** The section's claims above are all sourceable, but from five snapshots in combination rather than from the object's own documentation. EndpointSlice's *shape* — why slices rather than one list, the default size limit, the `ready`/`serving`/`terminating` conditions as a set — is uncached. §4 as specified does not assert any of it
- **Figure**: `ch09-fig03-service-endpointslice-selector-path`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — selector → EndpointSlice → traffic. The selector is the *question*; the EndpointSlice is the *written-down answer*, kept current by a controller; the Pod must be **Ready** to be on it
  - `> 🪝 **Snag:**` — a Service with no endpoints is not a broken Service. It is a correct Service whose selector currently matches nothing, or whose Pods are not Ready. Those are two different bugs and they are in two different files
  - `> 🔭 **Closer Look:**` — a terminating Pod is not deleted from the list the instant it starts shutting down. It stays, flagged terminating with `ready: false`, so that traffic drains rather than being cut. Deeper than the exam requires, and the reason graceful shutdown works at all
- **Cross-bearings**: back to Ch 5 §6 (**mandatory — the pinned payoff**; readiness probes, whose purpose the reader was told would be explained here); back to Ch 4 §7 (**mandatory** — labels and selectors as the universal join, cross-cutting theme #5); back to Ch 6 §2 (**mandatory** — a controller's selector and the Pods it owns, and the selection-versus-ownership distinction from Chapter 6's answer key); back to Ch 6 §4 (why a bad release cannot take the Service down — this is the mechanism); back to Ch 3 §3 (the EndpointSlice controller as one of the controllers listed there); back to Ch 7 §7 (one clause — backends on distinct nodes); forward to Ch 10 (the empty-endpoints case as the pattern's earlier instance); forward to Ch 13 and Ch 16 (**mandatory** — "Service→EndpointSlice" is a named Ch 16 retrieval anchor)
- ⚠ **Do not build a troubleshooting workflow.** The `debug-pods` snapshot is Chapter 13's and Chapter 16's primary source and it is tempting to mine it here. Take exactly the two-causes fact. No decision tree, no `kubectl describe` walkthrough, no Pod failure signatures
- ⚠ **Do not teach the legacy `Endpoints` (v1) resource.** Uncached, and teaching a superseded API to an associate-tier reader costs more than it returns

### §5 — 🟡 When You Don't Want a Single Address

**Two deliberate exceptions, and they are only comprehensible now** — a reader meeting headless Services before §3 and §4 has no idea what is being subtracted. Pays `chapter-06` line 870.

**First, headless, and lead with the intent rather than the field.** Sometimes you do not want load balancing and you do not want a single Service IP. You get that by explicitly setting `.spec.clusterIP` to `None`. What changes: for a headless Service **that defines selectors**, the endpoints controller still creates EndpointSlices, and it modifies the DNS configuration to return **A or AAAA records pointing directly to the Pods** backing the Service. For a headless Service **without** selectors, no EndpointSlices are created automatically.

**Second, why anyone would want that** — and Chapter 6 already handed the reader the answer. A StatefulSet requires a headless Service to be responsible for the network identity of its Pods, and *you* are responsible for creating it. When the workload is a set of distinguishable members — a database with a primary and replicas, a quorum of peers — "any one of these will do" is precisely wrong. Chapter 6 deferred this; §5 collects it, and Chapter 11 closes the storage half of the same story.

**Third, Services without selectors, framed as a supported pattern rather than an error state.** A Service can be used **with** a corresponding set of EndpointSlices and **without** a selector, to abstract other kinds of backends — an external database, a service in another namespace or another cluster, a workload being migrated into the cluster. The selector is how a Service *usually* finds its endpoints. It is not how a Service is *defined*. The clients on the inside get a normal Service name and never learn that what is behind it is not a Pod.

**Fourth, the combination table, because two independent binaries produce four cases and readers routinely conflate two of them.** Headless-or-not × selector-or-not: normal + selector (§3/§4's ordinary case); normal + no selector (a virtual IP in front of manually managed endpoints); headless + selector (DNS returns the Pod IPs); headless + no selector (no EndpointSlices created automatically). Four cells, one line each. This is the cheapest possible defence against B1 traps #40 and #41 and it is the section's highest-value artefact.

- **Objectives**: D2.1
- **Concepts introduced**: `headless-service`, `cluster-ip-none`, `service-without-selector`, `manually-managed-endpointslice`, `endpoints-controller`
- **Sources**: `k8s-docs-service-2026-08-23.md` (headless Services — "you can create what are termed headless Services, by explicitly specifying 'None' for the cluster IP address (.spec.clusterIP)"; the with-selectors and without-selectors behaviours; Services without selectors abstracting external databases, other-namespace or other-cluster services, and workloads being migrated). `k8s-docs-statefulset-2026-08-24.md` (StatefulSets currently require a headless Service to be responsible for the network identity of the Pods, and you are responsible for creating it — **already cited in Ch 6, retrieved here**). `k8s-docs-dns-pod-service-2026-08-23.md` (the headless resolution behaviour; full treatment in §7)
- **Figure**: none. **Part 18.9 reasoning:** the section's one genuinely visual artefact is the 2×2 combination table, and a *table* is the right form for it — the content is a discrete cross-product with no spatial, temporal or flow structure. Drawing it as a figure would add extraneous load (Part 18.3) for no germane gain, and the chapter already carries five figures
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2**
- **Markers planned**:
  - `★ **Fixed Point:**` — `clusterIP: None` is a **configuration, not a failure**. It says: do not give me one address, give me all of them
  - `> 🪝 **Snag:**` — "headless" sounds like something went wrong. It means the Service has no *head* — no single virtual IP fronting the set. The Pods are all still there; you just get all of them instead of one of them
  - `> ⚓ **Worth Securing:**` — the selectorless Service is the quiet workhorse of migrations. Your application inside the cluster talks to `database.production.svc.cluster.local` from day one, whether that name currently resolves to a managed database in another data centre or to Pods you moved in last night. The client never learns the difference, which means the migration is not the client's problem
- **Cross-bearings**: back to Ch 6 §5 (**mandatory — the pinned payoff**; the headless Service a StatefulSet requires, which Chapter 6 explicitly deferred to "the rest of Services"); back to **§3** (the ladder — this is what removing its bottom rung does); back to **§4** (the selector, now optional); forward to **§7** (**mandatory** — the DNS behaviour is stated here and mechanised there); forward to Ch 11 (**mandatory** — the storage half of StatefulSet identity, closing the book's one deliberate forward reference)
- ⚠ **Do not teach StatefulSet Pod naming, ordinal indexes, or ordered deployment.** Chapter 6 taught them. One retrieval clause is the ceiling
- ⚠ **Do not manually author EndpointSlice YAML.** Uncached, and an associate-tier reader needs the *pattern*, not the manifest

### §6 — 🔵 The Component That Makes It Real

**The chapter's arousal-restoration point, deliberately placed between §3 and §7 — its two highest-cost sections. Pays the second half of `chapter-03` line 459.** Chapter 3 introduced kube-proxy as a node component and promised the reader that Chapter 9 would explain how it implements Services.

**First, the job, stated once and clearly.** Every node runs a kube-proxy — unless you have deployed an alternative component in its place. It implements a **virtual IP mechanism** for Services of **every type except ExternalName**. Each instance watches the control plane for the addition and removal of **Service and EndpointSlice objects**, and for each Service it configures the node to **capture traffic to the Service's cluster IP and port and redirect it to one of the Service's endpoints** — usually a Pod, though possibly an arbitrary user-supplied IP.

**Second, the sentence that is the chapter's Zenith hiding in a reference page**, and it should be quoted almost verbatim because §8 depends on it: *a control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server.* The reader has met control loops in Chapters 3, 4, 6, 7 and 8. This is the sixth. Note it in one clause; do not deliver the payoff yet.

**Third, the consequence that reframes everything before it.** The cluster IP is **virtual**. No process is bound to it. Nothing is listening on it. It is an address that exists only as a rule on each node, saying *packets for this address go to one of those addresses instead.* This is why §3's ExternalName exclusion makes sense — an ExternalName Service has no address to intercept, so kube-proxy has nothing to do — and it is why a Service is not a load balancer in the sense of "a thing that runs somewhere and receives your traffic."

**Fourth, the modes, as a compact table.** On Linux: **iptables** (the default), **IPVS**, and **nftables** (GA since Kubernetes 1.33). On Windows there is exactly one: **kernelspace**. The reader needs to recognise these names and know which is the default. Nothing about them needs to be *understood* at associate tier, and drafting should say so plainly rather than pad the section — a candidate who can name the four and identify iptables as the default has everything the exam is likely to want. See § Open questions #8 on how to state the nftables version without pinning the book to it.

**Fifth, and briefly: kube-proxy is optional.** If you use a network plugin that implements packet forwarding for Services by itself, providing equivalent behaviour, you do not need to run kube-proxy at all. Cilium is the named example that can act as a replacement. This is a nice closing beat because it retrieves §1 — the plugin that implements the network model can also implement the Service data plane — and because it inoculates the reader against reading kube-proxy as load-bearing architecture when it is one implementation of one job.

- **Objectives**: D2.1
- **Concepts introduced**: `service-proxy`, `kube-proxy-modes`, `iptables-mode`, `ipvs-mode`, `nftables-mode`, `kernelspace-mode`, `kube-proxy-optional`
- **Sources**: `k8s-docs-virtual-ips-kube-proxy-2026-08-23.md` (every node runs kube-proxy unless replaced; the virtual IP mechanism for Services of type other than ExternalName; watching Service and EndpointSlice objects; capturing traffic to the cluster IP and port and redirecting to an endpoint, usually a Pod but possibly an arbitrary user-provided IP; the control-loop synchronisation sentence; all four modes with iptables as the default and nftables GA since 1.33). `k8s-docs-network-model-2026-08-23.md` (a service proxy implementation monitors Service and EndpointSlice objects and programs the data plane, using OS or cloud-provider APIs to intercept or rewrite packets). `k8s-docs-cluster-architecture-2026-08-23.md` (kube-proxy is optional; if your network plugin implements packet forwarding for Services itself with equivalent behaviour, you do not need to run kube-proxy). `k8s-docs-components-2026-08-23.md` (kube-proxy as a node component — **already cited in Ch 3, retrieved here**). `k8s-docs-cluster-addons-2026-08-24.md` (Cilium can act as a replacement for kube-proxy)
- **Figure**: `ch09-fig04-kube-proxy-modes` — **see § Open questions #6 on the anchor name, which under-describes what the figure needs to be**
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — kube-proxy implements the virtual IP for **every Service type except ExternalName**, by watching **Service and EndpointSlice** objects and programming each node. Modes: iptables (default), IPVS, nftables, and kernelspace on Windows
  - `> ⚓ **Worth Securing:**` — nothing is listening on a cluster IP. It is not a host, not a process, not a port on a machine. It is a rule on every node saying *send this somewhere else*. Once that lands, half the confusing behaviour of Kubernetes networking stops being confusing
  - `> 🔭 **Closer Look:**` — kube-proxy is optional, and increasingly often absent: a plugin like Cilium can do the same job in its own data plane. If you meet a cluster with no kube-proxy Pods, nothing is missing. Deeper than the exam requires
- **Cross-bearings**: back to Ch 3 §4 (**mandatory — the pinned payoff**; kube-proxy was named as a node component and its Service implementation deferred here); back to **§1** (the plugin that implements the network model may also implement this); back to **§3** (the ExternalName exclusion, from the other side); back to **§4** (EndpointSlice is what kube-proxy actually reads); forward to **§8** (the control-loop sentence, whose payoff is deferred); forward to Ch 17 (a service mesh moves this job into a sidecar or an ambient layer — one clause, no content)
- ⚠ **Do not explain how iptables, IPVS or nftables work.** Naming them and identifying the default is the entire associate-tier requirement. A packet-filtering tutorial here is the clearest possible violation of Part 6's signal-to-noise principle
- ⚠ **Do not name cross-cutting theme #3.** "The object exists but nothing happens without the component" is **[B3]**-designated to be *named* in Chapter 10. §6 may state its instances concretely; it must not give the pattern a name. See § Open questions #5

### §7 — 🔵 Names, and Where They Resolve

**The chapter's second high-cost section and the payoff for two published cross-bearings** (`chapter-03` line 603, `chapter-04` line 588). Chapter 4's promise is unusually specific — it deferred *the mechanism, what serves those records, what else gets one, and how resolution actually proceeds* — and all four must be discharged here.

**First, what serves the records, because Chapter 3 and Chapter 4 both promised it.** Kubernetes creates DNS records for Services and Pods, so you can contact Services by consistent names instead of IP addresses. **CoreDNS** is the cluster DNS addon that serves them, and cluster DNS is a **built-in service launched automatically by the addon manager** — which is why the reader has never had to install it and has never thought about it. The **kubelet configures each Pod's DNS** so that containers can look up Services by name.

**Second, the Service record, stated exactly.** A normal (not headless) Service is assigned A and/or AAAA records at `my-svc.my-namespace.svc.cluster-domain.example`, resolving to the **cluster IP** of the Service. That is the form Chapter 4 gave the reader in one sentence, now with its parts named: service, namespace, `svc`, cluster domain.

**Third — and this is the section's best beat — the same name form, a different answer.** A **headless** Service is assigned records at **the same name form**, and they resolve to **the set of IPs of all the Pods** the Service selects. Clients are expected to consume the set, or use standard round-robin selection from it. The name did not change shape. The number of answers did. §5 told the reader this happens; §7 is where they see that it happens *without a different name*, which is the part that surprises people.

**Fourth, the bare-name rule and its cause**, which is where Chapter 4's "how resolution actually proceeds" is discharged. By default, a client Pod's **DNS search list includes the Pod's own namespace and the cluster's default domain**. That is the whole explanation for a rule Chapter 4 stated flat: a bare `<service-name>` resolves within the local namespace only, and reaching across namespaces requires the fully qualified name. It is not a special case in Kubernetes; it is ordinary DNS search-domain behaviour, and saying so converts a rule into a consequence.

**Fifth, the other two record shapes, compactly.** **SRV** records are created for **named ports** that are part of normal or headless Services: `_port-name._port-protocol.my-svc.my-namespace.svc.cluster-domain.example`. **Pods** get records too, generally of the form `pod-ipv4-address.my-namespace.pod.cluster-domain.example` — for example `172-17-0-3.default.pod.cluster.local`, with the dashes where the dots were. And when a Pod sets both `hostname` and `subdomain`, and a headless Service exists whose name matches the subdomain, the Pod's FQDN becomes `hostname.subdomain.namespace.svc.cluster-domain.example` — which is the mechanism giving StatefulSet members individually addressable names, closing §5's loop.

**This section carries the chapter's `Dead Reckoning` block.** Five name shapes with a maritime frame around them would be actively harmful. State them flat, in a table, with one column for the shape and one for what it resolves to. The reader trying to memorise these before an exam should be able to find this block by flipping, and it should read like a reference card because it is one — `ch09-fig05` and this table are both destined for The Lodestar.

**Sixth, `dnsPolicy`, at whatever depth the author chooses** — see § Open questions #7. The recommendation is a single `🔭 Closer Look` naming `ClusterFirst` as the default and noting that `None` plus `dnsConfig` exists for Pods that must ignore cluster DNS entirely. Not a Fixed Point.

- **Objectives**: D2.1
- **Concepts introduced**: `cluster-dns`, `coredns`, `dns-addon`, `service-dns-record`, `a-record`, `aaaa-record`, `srv-record`, `pod-dns-record`, `dns-search-list`, `fqdn`, `cluster-domain`, `dns-policy`, `cluster-first`
- **Sources**: `k8s-docs-dns-pod-service-2026-08-23.md` (Kubernetes creates DNS records for Services and Pods; the kubelet configures Pods' DNS; CoreDNS as the cluster DNS addon; the default search list including the Pod's own namespace and the cluster's default domain; the normal-Service A/AAAA record form resolving to the cluster IP; the headless form resolving to the set of Pod IPs with round-robin client selection; the SRV record form for named ports; the Pod record form and the `172-17-0-3.default.pod.cluster.local` example; `hostname` + `subdomain` + matching headless Service producing `hostname.subdomain.namespace.svc.cluster-domain.example`; the four `dnsPolicy` values with `ClusterFirst` as the default). `k8s-docs-dns-cluster-addon-2026-08-24.md` ("DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on"). `k8s-docs-cluster-addons-2026-08-24.md` (CoreDNS listed under Service Discovery). `k8s-docs-namespaces-2026-08-23.md` (the FQDN form and the bare-name-is-local rule — **already cited in Ch 4, retrieved here**)
- **Figure**: `ch09-fig05-dns-record-shapes`
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `★ **Fixed Point:**` — `<service>.<namespace>.svc.<cluster-domain>`. A **bare** name resolves in the client Pod's **own namespace only**, because that namespace is in its search list. Crossing a namespace means using the full name
  - `★ **Fixed Point:**` — the **same name form** gives you the cluster IP for a normal Service and **the set of Pod IPs** for a headless one
  - `**Dead Reckoning:**` — the five record shapes, in a table, with no metaphor: normal Service, headless Service, SRV for named ports, Pod by dashed IP, and Pod by hostname-and-subdomain
  - `> ⚠ **Navigational Hazards:**` — the bare name is the single most common cross-namespace mistake, and it fails in the worst possible way: if a Service of the same name exists in the caller's own namespace, it resolves successfully to the wrong thing. No error, no timeout, just the wrong database
  - `> 🪢 **Mnemonic:**` — *service, namespace, svc, cluster.local* — four labels, always in that order, and the two in the middle are the ones people get backwards
- **Cross-bearings**: back to Ch 4 §6 (**mandatory — the pinned payoff**; all four deferred sub-promises discharged here); back to Ch 3 §6 (**mandatory** — CoreDNS as the cluster DNS addon, promised there by name); back to **§5** (**mandatory** — the headless behaviour asserted there is explained here); back to **§3** (ExternalName's CNAME is a DNS fact and this is where DNS lives); back to Ch 6 §5 (`hostname` + `subdomain` is how StatefulSet members get individual names); forward to Ch 10 (name-based virtual hosting is an entirely different layer of naming — one clause, to pre-empt the conflation); forward to Ch 13 and Ch 16 (name resolution as a failure mode)
- ⚠ **Do not teach Corefile configuration, custom nameservers, stub domains, or CoreDNS plugins.** The `dns-cluster-addon` snapshot's own note records that the rest of that page is out of scope for this chapter. Cluster DNS *customisation* is not in any CNCF competency list
- ⚠ **Do not conflate DNS-based service discovery with Ingress host routing.** They are different layers and Chapter 10 needs the distinction clean

### §8 — ⚪ A Query With a Name

**The chapter's one Zenith**, and the payoff for the curiosity gap planted in Why This Chapter Matters. Short — one claim, demonstrated.

**The claim: there is one object in this chapter, and it does not do anything.** A Service is a label query with a name attached. Everything else in the chapter is a control loop reconciling that query's current answer against some piece of the network.

**The demonstration, in the chapter's own order**, each item one or two sentences:

- **§2.** The Service is an object. You `apply` it through the same door as everything else, and its `spec` is a statement of desired state exactly as Chapter 4 defined it: *these Pods should be reachable at a stable address.*
- **§4.** The EndpointSlice controller watches Services and Pods, evaluates the selector, and writes down the answer. Desired state, current state, reconciliation. **This is a control loop, and it is the same one the ReplicaSet controller runs over the same labels for a different purpose** — which is precisely what Chapter 6's answer key told the reader when it distinguished selection from ownership.
- **§6.** kube-proxy watches Services and EndpointSlices and programs each node. The source says so in as many words: *a control loop ensures that the rules on each node are reliably synchronized with the Service and EndpointSlice state as indicated by the API server.* That is the sixth control loop in this book and the reader should be told so by number.
- **§7.** Cluster DNS publishes the answer as a name. Same input, third consumer.
- **§1.** And underneath all of it, none of the packet-moving is Kubernetes' work at all — a CNI plugin implements the model, and Chapter 2's CRI was the first instance of exactly this arrangement.

**Then the reframe that gives the chapter its title.** The stable thing was never a Pod, and it was never even an IP address — the cluster IP belongs to nothing and nothing listens on it. **The stable thing is the query, and the name you gave it.** Pods come and go underneath; the question "which Pods have these labels and are Ready" has a different answer every few minutes and the same *meaning* forever. That is what makes churn survivable, and it is why the abstraction is a declaration rather than a device.

**Be honest about the exception**, because the claim overclaims slightly. §3's type ladder and §7's record shapes are not consequences of the architecture — they are facts about the API that must be memorised. Say so. This book has an established habit of narrowing a slogan until it is true, and a Zenith that quietly omits its counterexamples is a slogan.

**Close by planting Chapter 10 rather than summarising Chapter 9.** Everything in this chapter was about the inside of the cluster. Every name resolved to something with a Pod behind it, and every address was reachable only by things that were already in. That is the boundary Chapter 10 crosses.

- **Objectives**: D2.1
- **Concepts introduced**: none. Synthesis only
- **Sources**: none new. Every claim retrieves a source already cited in §1–§7 or in Chapters 2, 3, 4 and 6
- **Figure**: `ch09-zenith-stable-name-over-churn`
- **Checkpoint after**: no
- **Markers planned**:
  - `☀️ **Zenith:**` — a Service is a **label query with a name**. The virtual IP, the endpoint list and the DNS record are three control loops publishing that query's current answer in three formats. The Pods were never the stable thing; the question was
  - `> ⚓ **Worth Securing:**` — the practical form: when Kubernetes networking behaves in a way you did not expect, ask *what does the selector currently match*, and *which loop has not caught up yet.* Those two questions cover most of it
- **Cross-bearings**: back to §1–§7 (each demonstration item); back to Ch 3 §5 (**mandatory** — the control loop, cross-cutting theme #1, on its fourth beat); back to Ch 4 §7 (labels as the universal join, theme #5); back to Ch 6 §2 (**mandatory** — the selection-versus-ownership distinction, which is this section's strongest evidence); back to Ch 2 §4 (CRI as the first pluggable interface); forward to Ch 10 (the boundary); forward to Ch 15 (the control loop's fifth beat, pointed at a Git repository — the book's **primary** Zenith); forward to Ch 17 §4 (the four interfaces, collected)
- ⚠ **Do not introduce anything.** A Zenith that teaches is a ninth section. This one recognises
- ⚠ **Do not claim the primary Zenith's ground.** Chapter 15 owns "the control loop, generalised." §8 observes that this chapter's machinery is *made of* control loops; it must not make the leap to "and therefore everything is." That leap is Chapter 15's payoff and it is the book's structural argument

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 15 questions total.** B4 allocates 10 and states plainly that the figure is a minimum to exceed; Chapters 3 through 8 all shipped 15 across three checkpoints of 5. This chapter has three separable blocks that map cleanly onto the section groups, so three is structural rather than decorative. Chapter total moves 39 → 44.

- **#1 after §3** covers the model and the abstraction (§1–§3): what the network guarantees, and the four shapes of a durable address.
- **#2 after §5** covers the backends (§4–§5): how the list stays correct, and the two cases where you deliberately don't want one.
- **#3 after §7** covers the implementation and the names (§6–§7): what moves the packet, and what you actually type.

Folding to two would put §3's type ladder and §7's record shapes — the chapter's two densest recall blocks — in the same checkpoint, which is exactly the adjacency the Attention Budget session split is designed to prevent.

**Retrieval-practice content: 20%** **[B3]** — drawn from **Chapters 5 through 8**, with the **≥4-back spacing floor** satisfied by Chapter 5. Against a combined Bearings-plus-Practice pool of 36, the target is ~7 items, allocated **3 in Bearings and 4 in Practice** (7 of 36 = 19.4%), matching the allocation shape Chapters 7 and 8 used.

Each of the arc outline's named anchors has one place it belongs:

| Named anchor | Placement | Why here |
|---|---|---|
| **Controller churn (Ch 6)** | Bearings #1, item 4 | §2's entire argument is Chapter 6's churn. Asking immediately after §3 tests whether the reader can state the *problem* now that they have been given the solution — which is a harder and better question than asking before |
| **Selectors → Service (Ch 6 §2)** | Bearings #2, item 1 | §4 *is* the selector arriving in its second role. The retrieval and the teaching are the same beat, and Chapter 6's answer key already framed the two-controllers-one-label-set case |
| **≥4-BACK FLOOR: the Pod network namespace (Ch 5 §2)** | Bearings #1, item 2 | §1's first rule is Chapter 5's fact promoted to cluster scope. **Exactly four chapters back** — the floor requires ≥4 and this meets it |

**On the ≥4-back floor.** Chapter 5 is the minimum permissible distance, which makes Bearings #1 item 2 a single point of failure. Practice carries a second ≥4-back item (Chapter 4's selectors, five back) as redundancy, exactly as Chapter 8's outline did when the floor first went live.

### ☆ Taking Your Bearings #1 — after §3

- **Topic**: the flat network, and the four shapes of an address that lasts
- **Questions**: 5
- **Retrieval from earlier chapters**: 2 of 5 (one named anchor, one ≥4-back floor item)
- **Difficulty**: ⚪ for items 1–2, 🔵 for 3–5

  1. A Pod on `worker-3` sends a request to a Pod on `worker-11`. State what the receiving Pod sees as the source address, and name the two things the model guarantees are *not* involved. **Correct answer: the sending Pod's own IP; no NAT and no proxy.** Trap answers should include the node's IP (the answer that would be right in almost any non-Kubernetes cluster) and a NAT-translated address.
  2. **Retrieval from Ch 5 §2. [≥4-BACK FLOOR ITEM]** A Pod runs two containers. One listens on 8080. Can the other also listen on 8080? How does each reach the other? And how many IP addresses does the Pod have? **Correct answer: no, they share one port space; over `localhost`; one.** **Four chapters back.** This item satisfies **[B3]**'s spacing floor and defuses B1 trap #36 in the same breath.
  3. 🔵 You create a Service with `type: NodePort`. A colleague says "so now it's only reachable from outside — we lost the internal address." What is wrong with that, and why? **Correct answer: nothing was lost; requesting NodePort also allocates a cluster IP, exactly as if `ClusterIP` had been requested.** **Directly tests B1 trap #37, which is the most mechanically checkable fact in §3.**
  4. 🔵 **Retrieval from Ch 6 §4.** Chapter 6 walked a Deployment through a rolling update. State what happens to the Pod IP addresses during that update, and then say what a Service gives a client that the Pod IPs cannot. **Correct answer: every Pod is replaced, and each replacement has a different address; the Service gives one address that does not change while the set behind it does.** Named anchor, framed so the reader states the problem in the terms §2 gave them.
  5. 🔵 Two Services. One has `type: LoadBalancer` and no external address after twenty minutes. One has `type: ExternalName` pointing at `api.vendor.example`. For each, say what Kubernetes is doing and whether anything is broken. **Correct answers: the LoadBalancer Service is waiting for an external load balancer that nothing is providing — Kubernetes offers no load-balancing component; the ExternalName Service is a CNAME with no proxying, working exactly as designed. Neither is broken.** **Tests B1 traps #38 and #39 in one item**, and it is deliberately built so the reader must resist the pull of "no address means failure."

- **Answer-key requirement**: item 3's key must state the additivity as a *rule about the ladder* rather than a fact about NodePort, because the same rule is what makes LoadBalancer comprehensible and Chapter 10's argument available.
- **Answer-key requirement**: item 5's key must not moralise about the bare-metal LoadBalancer case. It is an extremely common and entirely reasonable surprise; per Part 14, the wry register stays oriented at the practitioner's expectation, not at anyone's outage.

### ☆ Taking Your Bearings #2 — after §5

- **Topic**: who is actually behind the name, and the two times you don't want one
- **Questions**: 5
- **Retrieval from earlier chapters**: 1 of 5 (named anchor)
- **Difficulty**: 🔵 throughout, with item 3 at 🟡

  1. **Retrieval from Ch 6 §2 — the selector in its second role.** Chapter 6 said a ReplicaSet finds its Pods by selector, and that a Service asking the same question about the same Pods is a *different controller reading the same labels*. Name the object where the Service's answer gets written down, and name the controller that writes it. **Correct answer: EndpointSlice; the EndpointSlice controller.** Named anchor, and the discharge of `chapter-06` line 537 appearing as an assessment item.
  2. A Service's selector matches four Pods. Three are Ready; one is failing its readiness probe. How many endpoints does the Service have, and what happens to the fourth Pod when its probe starts passing? **Correct answer: three; it is added to the EndpointSlice and starts receiving traffic.** **The pinned `chapter-05` line 858 promise, tested.**
  3. 🟡 `kubectl get endpointslices` for your Service returns no endpoints. The Pods are running. Name the two usual causes and say how you would tell them apart. **Correct answers: the selector does not match the Pods' labels, or the Pods are not Ready; compare the Service's selector against the Pods' labels, and check the Pods' Ready condition.** **This is the chapter's designated struggle item** — label it per Part 10B and normalise the difficulty, because the reader's instinct will be to look at the network and the answer is in two YAML files.
  4. A teammate calls a headless Service "broken" because `kubectl` shows no cluster IP. Explain what `clusterIP: None` does and give one workload for which it is the correct choice. **Correct answer: it is deliberate — DNS returns the Pod addresses directly instead of one virtual IP, for cases where you do not want load balancing; a StatefulSet, which requires a headless Service for its Pods' network identity.** **Tests B1 trap #40** and closes a Chapter 6 loop.
  5. You need cluster-internal clients to reach a database that runs on hardware outside the cluster, using an ordinary Service name. Two Service configurations could do this. Name both, and say what is different about what the client experiences. **Correct answers: a Service without a selector, backed by manually managed EndpointSlices — the traffic is proxied to the external address; or `type: ExternalName` — the client gets a CNAME and connects directly, with no proxying.** **Tests B1 trap #41**, and it is the chapter's best interleaving item because it requires §3 and §5 simultaneously.

- **Answer-key requirement**: item 2's key must connect readiness to Chapter 6's rolling updates explicitly — a new Pod that never reports Ready never receives traffic, which is *why* a bad release cannot take the Service down. Chapter 6 relied on that mechanism without naming it; this key is the cheapest place to close the loop.
- **Answer-key requirement**: item 5's key must state the proxying difference as the discriminator. Both options are correct answers to the *requirement*; only one of them puts kube-proxy in the path, and that is the fact the item exists to teach.

### ☆ Taking Your Bearings #3 — after §7

- **Topic**: what moves the packet, and what you actually type
- **Questions**: 5
- **Retrieval from earlier chapters**: 0. The chapter's 20% is met by Bearings #1 items 2 and 4, Bearings #2 item 1, and four Practice items. A fourth Bearings retrieval would push this checkpoint off its own topic, and this topic is the chapter's densest recall material
- **Difficulty**: 🔵, with items 2 and 5 at 🟡

  1. Name the component that implements the virtual IP mechanism for Services, say which Service type it does **not** implement, and name the two object types it watches. **Correct answers: kube-proxy; ExternalName; Service and EndpointSlice.** The chapter's cleanest single-fact recall item.
  2. 🟡 A colleague says "I'll SSH to the node and see what's listening on the cluster IP." What will they find, and why? **Correct answer: nothing — the cluster IP is virtual. No process is bound to it; it exists as a forwarding rule that captures traffic to that address and redirects it to an endpoint.** **This item tests whether §6's central idea actually landed**, and it is the one most likely to separate readers who understood the section from readers who read it.
  3. Name kube-proxy's modes and identify the default on Linux. Then say what it would mean to find a cluster running no kube-proxy at all. **Correct answers: iptables (default), IPVS, nftables on Linux, kernelspace on Windows; it means the network plugin implements Service packet forwarding itself, which is supported and increasingly common.**
  4. A container in namespace `payments` needs to reach a Service named `ledger` in namespace `billing`. Write the name it should use, and say what would happen if it used just `ledger`. **Correct answers: `ledger.billing.svc.cluster.local`; a bare `ledger` resolves within the client's own namespace only — it would fail, or worse, silently reach a *different* `ledger` in `payments`.** **Tests B1 trap #46**, the chapter's most consequential naming error.
  5. 🟡 Two Services, `db-a` and `db-b`, in the same namespace. `db-a` is a normal Service; `db-b` is headless. A client resolves `db-a.prod.svc.cluster.local` and `db-b.prod.svc.cluster.local`. Describe what each lookup returns and how many answers the client gets. **Correct answers: `db-a` returns one address — the Service's cluster IP; `db-b` returns the set of IPs of all the Pods it selects, and the client is expected to consume the set or round-robin over it.** Tests the section's best fact: same name shape, different kind of answer.

- **Answer-key requirement**: item 3's key must not assert that any particular mode is faster or better. The cached source states the mode list and the default, and nothing about relative performance; per Ethical Guardrail #4, the key claims no certainty the source does not carry.
- **Answer-key requirement**: item 4's key must state the *silent wrong answer* failure explicitly. "It fails" is the incomplete version; "it succeeds against the wrong Service" is the one that costs people afternoons, and it is the reason the FQDN rule is worth memorising rather than looking up.

---

## 6. Exam Alert plan

**High-priority topics** — the twelve most likely to be tested directly, in descending order of confidence:

1. **Every Pod gets a unique cluster-wide IP**, and all Pods reach all Pods **without NAT and without proxies**, same node or across nodes.
2. **The Pod holds the IP; its containers share it** and communicate over `localhost`.
3. **ClusterIP is the default** Service type and is reachable only from inside the cluster.
4. **NodePort also allocates a cluster IP** — the types are additive.
5. **Kubernetes does not provide a load balancer.** You supply one or integrate with a cloud provider.
6. **ExternalName is a CNAME with no proxying of any kind.**
7. **`clusterIP: None` is deliberate** — DNS returns the Pod addresses directly.
8. **A Service without a selector is a supported pattern**, backed by manually managed EndpointSlices.
9. **`<service>.<namespace>.svc.<cluster-domain>`**, and a **bare name resolves in the local namespace only**.
10. **kube-proxy implements the virtual IP for every type except ExternalName**; iptables is the default mode.
11. **A Pod must be Ready to be an endpoint.** The selector proposes; readiness disposes.
12. **Kubernetes defines the network model and implements none of it** — a CNI plugin does.

**Common traps to call out.** B1 traps #35, #36, #37, #38, #39, #40, #41 and #46 all belong to this chapter and **all eight are `[source]`-tagged**, so all eight may be described as things candidates get wrong. **None is `[inferred]`, so no hedging is required** — and equally, none may be dressed with invented frequency figures (Part 14 guardrail #8, and **[B3]**'s fourth do-not-retrieve rule).

| B1 # | Trap | Where it is defused |
|---|---|---|
| 35 | "Pods need NAT or a proxy to reach Pods on other nodes" | §1 rule 3, Bearings #1 item 1 |
| 36 | "Each container in a Pod gets its own IP" | §1 Snag, Bearings #1 item 2 |
| 37 | "NodePort replaces ClusterIP" | §3 Fixed Point, Bearings #1 item 3 |
| 38 | "LoadBalancer means Kubernetes provides a load balancer" | §3 Fixed Point, Bearings #1 item 5 |
| 39 | "ExternalName proxies traffic" | §3 Navigational Hazards, Bearings #1 item 5 |
| 40 | "A headless Service is a broken Service" | §5 Fixed Point and Snag, Bearings #2 item 4 |
| 41 | "A Service without a selector is invalid" | §5, Bearings #2 item 5 |
| 46 | "A bare service name works across namespaces" | §7 Navigational Hazards, Bearings #3 item 4 |

**Six non-B1 traps worth adding**, all visible now that the networking snapshot set has been read in full. B1 catalogued this competency from index-level coverage of three of its topics:

- **"Something is listening on the cluster IP."** Nothing is. It is a forwarding rule on every node, not a socket. **This is the chapter's most valuable non-B1 trap** — it has one clean correct answer, it is stated plainly in the cached source, and believing the wrong version makes half of Kubernetes networking incomprehensible. §6 Worth Securing, Bearings #3 item 2.
- **"kube-proxy is required."** It is optional if your network plugin implements equivalent Service packet forwarding; Cilium is the named example. §6 Closer Look, Bearings #3 item 3.
- **"Headless Services have no DNS record."** They have records at the *same name form* as a normal Service; the records resolve to the Pod set instead of a cluster IP. §7, Bearings #3 item 5.
- **"A Service with no endpoints is broken."** It is a correct Service whose selector matches nothing or whose Pods are not Ready. §4 Snag, Bearings #2 item 3.
- **"A terminating Pod leaves the Service instantly."** It is retained with `ready: false` and a terminating state, so traffic drains. §4 Closer Look.
- **"Kubernetes ships the network."** It ships the *requirements*. A CNI plugin ships the network, and different plugins satisfy the same four rules by completely different means. §1 Fixed Point. **Conditional on the § Open questions #2 fetch.**

**Do not include** in the Exam Alert: Ingress, Ingress controllers, the Ingress freeze, Gateway API, or NetworkPolicy in any form (all Ch 10 — and the freeze in particular is B2's designated most-precise fact, which must not be spent early); StatefulSet ordinals, ordered deployment, or PV pairing (Ch 6 and Ch 11); Service troubleshooting as a workflow, Pod failure signatures, or `kubectl describe` walkthroughs (Ch 13 and Ch 16); service mesh, sidecar-versus-ambient, or mTLS (Ch 17); `port`/`targetPort`/`nodePort` mechanics and the NodePort range **unless § Open questions #3 is resolved in favour of teaching them**.

---

## 7. Practice Questions plan

**21 questions** (B4 allocation, unchanged). Distribution follows exam-point density rather than section count — §3 and §7 between them carry eight of the twelve priority topics:

| Block | Questions | Notes |
|---|---|---|
| §1–§2 — the network model, CNI, why a Service exists | 4 | Includes **1 retrieval item**. At least 2 must be about the four rules; §2's material is better tested as part of a §3 or §4 question than on its own |
| §3 — the type ladder | 5 | Includes **1 retrieval item**. **Every one of B1 traps #37, #38 and #39 must appear as a distractor at least once.** At least 2 must be scenario-shaped ("you need X, which type") rather than definitional |
| §4 — selector, EndpointSlice, readiness | 4 | Includes **1 retrieval item**. Must include one item whose correct answer is *"nothing is wrong"* |
| §5 — headless and selectorless | 2 | Two is right for two special cases. One on each, and the headless one should require the reader to name the workload type that needs it |
| §6 — kube-proxy | 3 | One recall (modes and default), one on the virtual-IP nature of the cluster IP, one on kube-proxy's optionality |
| §7 — DNS and names | 3 | Includes **1 retrieval item**. At least one must require the reader to *write* a name rather than recognise one |

**Retrieval allocation: 4 of the 21 draw from Chapters 4–8**, allocated *within* this count and not added to it:

- **The Pod network namespace** (Ch 5 §2) — §1–§2 block. Framed as a discrimination item: *a Pod runs three containers. How many IP addresses does the cluster allocate, and how many entries does that Pod produce in a Service's EndpointSlice?* Correct answer: one, and one. Tests whether the reader has actually collapsed container-count and endpoint-count, which is where trap #36 does its damage downstream.
- **Labels and selectors** (Ch 4 §7) — §3 block. **[≥4-back, five chapters]**, carried as redundancy for the floor. Framed as: *a Pod carries the labels a ReplicaSet selects on and the labels a Service selects on. Someone edits one label. Name both consequences, and say whether the two controllers coordinate.* Correct answer: it may leave the ReplicaSet's set and the Service's endpoint list independently; they do not coordinate, because they are independent queries over the same labels.
- **Readiness probes** (Ch 5 §6) — §4 block. Framed forward rather than backward: *Chapter 5 said a readiness probe controls whether a Pod receives traffic. Name the object that fact is actually implemented in, and say what a failing probe changes about it.* Correct answer: the EndpointSlice; the Pod is removed from the endpoint list. This item does double duty as a retrieval and as the pinned `chapter-05` line 858 promise assessed rather than merely stated.
- **Namespaces** (Ch 4 §6) — §7 block. Framed as: *Chapter 4 said a bare service name resolves within the local namespace. Now say what makes that true — what is configured, and by which component?* Correct answer: the Pod's DNS search list contains its own namespace and the cluster's default domain, configured by the kubelet. Converts a memorised rule into a mechanism, which is exactly what §7 is for.

**Interleaving strategy.** At least **five** questions must require two sections at once:

- **Types + DNS (§3 + §7)** — given a Service type and a client's namespace, what name does the client use and what does it resolve to? Run it once for a normal Service and once for a headless one.
- **Selector + readiness + churn (§4 + Ch 5 + Ch 6)** — during a rolling update, at a moment when two old Pods are terminating and two new Pods are starting but not yet Ready, how many endpoints does the Service have, and what state are the terminating ones in?
- **Headless + DNS + StatefulSet (§5 + §7 + Ch 6)** — why a StatefulSet needs a headless Service, and what a client gets when it resolves its name.
- **Model + kube-proxy (§1 + §6)** — a cluster running no kube-proxy Pods and working normally. What is doing kube-proxy's job, and which of §1's four rules does it also implement?
- **Everything + §8** — a Kubernetes networking behaviour the chapter did not cover. What object holds the declaration, and which loop is publishing its answer? The correct answer is the *method*, not a fact, and it is the only question in the set that tests the Zenith.

**Trap-answer requirement** (skill Part 11): every wrong option must target a specific misconception and the answer key must explain why each is wrong. For the §3 block, wrong options must be drawn from B1 traps #37–#39 in their exact wrong form, with **#37 appearing at least twice in two different question shapes** because "NodePort replaces ClusterIP" is the most mechanically testable error in the chapter. For the §1 block, the each-container-gets-an-IP misconception must appear as a distractor in addition to its Bearings appearance.

**One calibration note.** This chapter's failure mode as a question set is *recognition inflation* — twenty-one items asking "which type is this" and "what does this name resolve to." The material genuinely does contain two blocks of near-pure recall (§3's types, §7's shapes), and those blocks deserve about eight of the twenty-one. The remaining thirteen should test **prediction** ("how many endpoints, and why") and **diagnosis** ("nothing is listening, is anything wrong"). A question answerable by matching a term against a table has tested the reader's short-term memory of a table — and this chapter, unusually, has an alternative available for almost every fact, because nearly everything in it is derivable from §1's model plus §8's observation.

---

## 8. Required figures

Six anchors, exactly as the arc outline specifies. §2 and §5 deliberately carry none — see each section's Figure line for the Part 18.3/18.7/18.9 reasoning.

**A note on this chapter's figure register.** This chapter's figures are more *structural* than Chapter 8's reference diagrams: four of the five concept figures depict a path or a relationship rather than a lookup table, which is exactly the case Part 18.8 says is worth illustration budget. `ch09-fig02` and `ch09-fig05` are the two destined for The Lodestar; design both at quarter-page legibility. The Zenith carries the brand's illustrative register; the other five do not, and should not be dressed up.

### `ch09-fig01-network-model-four-rules`

- **Purpose**: §1's Fixed Point, dual-coded. The model as a set of guarantees rather than a topology.
- **Content**: two nodes side by side, two Pods on each. Inside one Pod, two containers drawn sharing a single boundary labelled with one IP address, with a short `localhost` arrow between them. Between Pods on the *same* node, a direct arrow. Between Pods on *different* nodes, a direct arrow crossing the node boundary — **the same weight and style as the same-node arrow**. A small kubelet glyph on one node with an arrow to each Pod on that node.
- **Design requirement — the two inter-Pod arrows must be visually identical.** That identity *is* the model's second and third rules. Any styling that makes the cross-node path look heavier, dashed, or routed reintroduces exactly the mental model the section is replacing.
- **Design requirement — nothing may sit between the Pods.** No gateway box, no NAT box, no proxy glyph. The absence is the content, and an illustrator's instinct will be to fill that space.
- **Label count**: one Pod IP, one `localhost`, two node names, one kubelet — five. Within the Part 18.12 ceiling.

### `ch09-fig02-service-types-ladder`

- **Purpose**: §3's Fixed Point — the additivity, which the type list alone cannot show.
- **Content**: three nested or stacked bands showing ClusterIP at the base, NodePort containing it, LoadBalancer containing both, each band annotated with what it adds and who can reach it. **Set visibly apart, outside the stack entirely** — different position, no containment relationship, ideally separated by whitespace and a rule — a fourth element for ExternalName, drawn as a name-to-name arrow with a CNAME label and an explicit "no traffic path" annotation.
- **Design requirement — the separation of ExternalName is the pedagogy.** If it appears as a fourth band, the figure teaches the trap instead of defusing it. It must be visually impossible to read the four as a single sequence.
- **Design requirement — annotate the LoadBalancer band with its provider.** A small "supplied by your cloud provider, not by Kubernetes" note attached to that band carries Fixed Point #5 at the moment the reader is looking at it.
- **Lodestar candidate.** This figure is the chapter's single highest-value reference artefact.
- **Label count**: three band names, three reachability annotations, one provider note, one ExternalName label with its CNAME annotation — seven. At the ceiling; do not add.

### `ch09-fig03-service-endpointslice-selector-path`

- **Purpose**: §4's Fixed Point — selector → EndpointSlice → traffic, with readiness as a gate rather than a step.
- **Content**: left to right. A Service object showing only its selector (`app: db`). An arrow labelled "query" to a set of five Pods, three of which carry the matching label. A **gate glyph** between the matched Pods and the next stage, labelled `Ready`, with one of the three matched Pods stopped at it. An EndpointSlice object listing the two addresses that got through. A small controller glyph sitting beside the arrow from Pods to EndpointSlice, labelled "EndpointSlice controller", with a watch-loop arrow.
- **Design requirement — the gate must be a gate, not an arrow.** The section's whole promised content is that matching the selector is necessary and not sufficient. A figure in which readiness is one more step in a chain says the opposite.
- **Design requirement — show a non-matching Pod and a matching-but-not-Ready Pod as visibly different failures.** Those are §4's two usual causes of an empty endpoint list, and distinguishing them in the figure is what makes Bearings #2 item 3 answerable from memory.
- **Label count**: selector, "query", `Ready`, EndpointSlice, controller name — five, plus Pod labels. At the ceiling.

### `ch09-fig04-kube-proxy-modes`

- **Purpose**: §6's Fixed Point. **⚠ The anchor name under-describes what this figure needs to be — see § Open questions #6.** The modes are a four-row table and a table is the right form for them; what needs a *figure* is the data path, with the mode as the swappable layer inside it.
- **Content**: one node. A client Pod on it sends a packet addressed to a cluster IP. The packet meets a rules layer on the node — drawn as a labelled band the packet passes *through*, not a box it is delivered *to* — and emerges readdressed to one of three endpoint Pods, two of which are on a different node. Beside the rules band, a small swap annotation listing the four mode names with `iptables` marked as the default. Above, a watch arrow from the band up to a Service object and an EndpointSlice object, labelled "kube-proxy watches".
- **Design requirement — the cluster IP must be shown as an address with nothing at it.** A dotted or ghosted target with no Pod behind it, dissolved at the rules band. This is the figure's whole argument and it is the section's Worth Securing callout in visual form.
- **Design requirement — the mode names are an annotation, not a structure.** Four boxes for four modes would imply the reader needs to distinguish them. They need to recognise them and know the default.
- **Label count**: cluster IP, rules band, four mode names with a default marker, "kube-proxy watches", Service, EndpointSlice — nine if every mode is counted, six if the mode list reads as one annotation block. **Design it so the mode list reads as one block**, or the figure exceeds the Part 18.12 ceiling.

### `ch09-fig05-dns-record-shapes`

- **Purpose**: §7's `Dead Reckoning` block, dual-coded. Reference, not narrative.
- **Content**: the five name shapes stacked, each broken into its labelled parts with the same parts in the same columns — `<service>` / `<namespace>` / `svc` / `<cluster-domain>` for the Service records, `<pod-ip-dashed>` / `<namespace>` / `pod` / `<cluster-domain>` for the Pod record, and the SRV and hostname-subdomain forms aligned to the same right-hand columns. A right-hand column per row stating what it resolves to: *the cluster IP* / *all the Pod IPs* / *the named port* / *that Pod* / *that Pod, by a stable name*.
- **Design requirement — the alignment is the pedagogy**, exactly as in `ch08-fig01`. The figure's argument is that four differently-shaped names share three of their four parts. Unaligned rows say nothing the prose did not.
- **Design requirement — the two Service rows must be visibly adjacent and visibly identical in shape.** Normal and headless produce the same name and different answers; that is §7's best fact and this is where it becomes obvious at a glance.
- **Lodestar candidate.** Along with `ch09-fig02`, this is what a reader will look at on the morning of the exam.
- **Label count**: four part-names shared across rows, five resolves-to annotations — nine, but the four part-names are column headers rather than per-row labels, so effective label load is five. Acceptable; do not add a sixth row.

### `ch09-zenith-stable-name-over-churn`

- **Purpose**: the chapter's one Zenith. §8's claim, in the brand's illustrative register.
- **Content**: the chapter's running example over time. Left to right across three or four time slices, the Pods behind a service change completely — different positions, different addresses, different nodes, none of the same shapes surviving from first slice to last. Above them, unchanged across every slice, one name and one address. Beneath, drawn as a steady band running the full width, the loop: *query → answer → publish*, with three small consumers hanging off the published answer — the rules band from `fig04`, the endpoint list from `fig03`, and a DNS record from `fig05`.
- **Design requirement — the churn must be genuinely total.** If any Pod survives from the first slice to the last, the figure undercuts its own claim. Nothing beneath the name persists.
- **Design requirement — the three consumers must be recognisably the three earlier figures.** This is the Zenith's argument in one visual gesture: three things the reader learned separately are three readers of one answer. Reusing the visual vocabulary is what makes the recognition free.
- **Register note.** This is the chapter's only figure permitted the brand's illustrative treatment. Given the book's world register — Communications Officer, early interstellar — the natural framing is a fixed bearing held while the fleet beneath it changes composition entirely. Do not caption it with the Zenith's sentence; per Part 18.7 the caption adds context, not a restatement.
- **Label count**: one name, one address, three loop stages, three consumers — eight. At the ceiling for a figure this narrative; if it feels crowded, cut the loop-stage labels first and let the band carry it.

---

## 9. Open questions for the author

1. **Subtitle length — 11 words against a ≤10-word constraint (editorial, non-blocking).**
   The arc outline's working subtitle is *"Flat networks, stable names, and the abstraction that makes churn survivable."* Frontmatter above carries *"Flat networks, stable names, and the abstraction that survives churn"* — exactly 10, all three ideas intact, and the active verb lands harder than the periphrastic one. Alternative if you prefer the original rhythm: *"Flat networks, stable names, and an abstraction that survives churn"* (10). **Recommendation: take the version in the frontmatter.** If you'd rather override the constraint and keep the arc's original, say so and it goes back verbatim — the constraint is this stage's, not the contract's.

2. **⚠ BLOCKING — CNI is named but its consequence is not sourced. (Arc gap G11, partially closed.)**
   §1 is **section-pinned** by `chapter-02` line 600 and is also the plant for Chapter 17's secondary Zenith, so it has to carry weight. What *is* cached: `k8s-docs-extending-kubernetes` line 23 names "Network plugins (CNI, the Container Network Interface, to implement pod networking)" as one of five infrastructure extension points, and line 15 records that the kubelet executes CNI plugins as external binaries; `k8s-docs-cluster-addons` supplies Calico, Cilium and Flannel; `k8s-docs-cluster-architecture` records that a plugin implementing Service packet forwarding makes kube-proxy unnecessary. What is **not** cached anywhere: that Kubernetes **ships no network plugin by default**, that a cluster without one has non-functional Pod networking, or how the kubelet invokes the plugin when a Pod's sandbox is created. §1's argument — *Kubernetes specifies this model and implements none of it* — is currently half-sourced, and it is the half that makes the section worth its pin.
   **Fetch: `kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/`.** Scope guard: take the plugin's responsibility and the fact that one must be installed. Do **not** take CNI plugin configuration, `--cni-conf-dir`, or plugin authoring — all far above associate tier. Routed to Stage 2. **§1 can be drafted without it at reduced strength; it cannot be drafted as specified.**

3. **⚠ NEAR-BLOCKING — Service port mechanics are entirely uncached. Decide whether to teach them.**
   Nothing in the source set covers `port` versus `targetPort` versus `nodePort`, and nothing gives the default NodePort range (30000–32767). §3 as specified above does not need them — the type ladder, the additivity, and the load-balancer fact are all fully sourced — so this is a scope decision rather than a source failure. The case *for* teaching them: "what port do I actually connect to" is the first question any reader has after §3, the port/targetPort distinction is a genuine and common confusion, and the NodePort range is exactly the kind of concrete number an associate-tier multiple-choice exam likes. The case *against*: CNCF's competency list names Service types, not Service fields, and the chapter is already the book's longest by section count.
   Three options: **(a)** fetch the Service page's port and NodePort-range sections and give §3 a short block; **(b)** teach the port/targetPort distinction only, from a fetch, and omit the range; **(c)** omit both, and let Chapter 10 handle "which port" when it does Ingress backends. **Recommendation: (a).** It is one fetch on a page already cached at a shallower depth, it answers the reader's most obvious next question, and the NodePort range is cheap to state and plausible to be tested. If you take (c), the chapter must not gesture at ports at all — a half-mention is worse than silence.

4. **EndpointSlice has no source of its own (non-blocking; recorded so the fact-accuracy audit does not misread it).**
   §4 is section-pinned and pays four cross-bearings, and every claim it makes above is sourceable — but from **five** snapshots in combination (`network-model`, `cluster-architecture`, `pod-termination`, `debug-pods`, `garbage-collection`) rather than from the object's own documentation. That is fine for what §4 asserts and thin if anything more is wanted. Uncached: why *slices* rather than one list, the default endpoints-per-slice limit, and the `ready` / `serving` / `terminating` conditions as a documented set rather than as two facts drawn from the termination page.
   **Fetch if convenient: `kubernetes.io/docs/concepts/services-networking/endpoint-slices/`.** **Recommendation: fetch it if Stage 2 is going out for #2 and #3 anyway** — same doc tree, and it would let §4's Closer Look state the conditions properly instead of inferring them. If it does not land, §4 drafts as specified and asserts nothing beyond the five snapshots. **Do not** let a drafter reach for the slice-size limit or the conditions vocabulary without it.

5. **Cross-cutting theme #3 — Chapter 9 has a cleaner instance than the chapter that names it.**
   **[B3]** designates Chapter 10 as the place "the object exists but nothing happens without the component" is *named*, so that Chapters 13 and 17 can retrieve it by name. Chapter 10's instance is Ingress-without-a-controller. But this chapter has **two earlier and arguably cleaner instances**: a `type: LoadBalancer` Service on a cluster with no cloud integration (§3), and a Service whose selector matches nothing (§4). Both are simpler than the Ingress case and both arrive a chapter sooner.
   Two options: **(a)** keep **[B3]**'s placement — Chapter 9 states its instances concretely without naming the pattern, and Chapter 10 names it with three examples in hand instead of one; **(b)** move the naming to Chapter 9 §4 and have Chapter 10 retrieve rather than introduce. **Recommendation: (a).** The pattern is most memorable named at the point where it is most *surprising*, and "I created an Ingress and nothing happened" is a sharper surprise than "my Service has no endpoints." But the decision has a real cost either way, and it is worth making deliberately rather than by default — Chapter 10's outline should be told which way it went.

6. **`ch09-fig04-kube-proxy-modes` — the anchor name describes a table, not a figure.**
   Four proxy modes are a discrete list with no spatial or temporal structure; per Part 18.9 that is a table, and drawing it as a figure adds extraneous load for no germane gain. What §6 genuinely needs illustrated is the **data path** — a packet meeting a rules layer at a virtual address and emerging readdressed — with the modes as an annotation on the swappable layer. The figure content specified in § Required figures does that.
   **Recommendation: keep the anchor ID verbatim and reshape the content.** The ID is the join key that Stage 10 and the `certcomp-diagrams` pipeline consume, the arc outline published it, and renaming it now buys nothing. Recording the mismatch here so the image-spec stage does not read the name literally and produce a four-box mode diagram. If you'd rather the ID matched its content, `ch09-fig04-service-proxy-data-path` is the accurate name and the arc outline would need editing to match.

7. **`dnsPolicy` — in scope or out?**
   The DNS snapshot carries all four values (`Default`, `ClusterFirst`, `ClusterFirstWithHostNet`, `None`) with `ClusterFirst` documented as the default. CNCF's competency list says "DNS for Services and Pods," which arguably reaches it. Against inclusion: three of the four values only matter for host-network Pods or for Pods deliberately opting out of cluster DNS, neither of which an associate-tier candidate will meet, and `Default` versus `ClusterFirst` is a naming trap (the value called `Default` is *not* the default) that costs a paragraph to defuse properly. **Recommendation: one `🔭 Closer Look` in §7, naming `ClusterFirst` as the default and noting that `None` plus `dnsConfig` exists.** Not a Fixed Point, not in the Exam Alert, not in a question. If you want it tested, it needs the `Default`-is-not-the-default trap stated explicitly, and that is a fourth Navigational Hazard in a chapter that already has two.

8. **nftables "GA since Kubernetes 1.33" — a version-pinned fact in a book with a shelf life.**
   The source states it plainly and it is worth stating. But Chapter 8 established this book's discipline around version numbers — state the rule, let the numbers illustrate it, never let a question turn on one — and the same discipline applies here. **Recommendation: §6 states the mode list with iptables as the default and notes nftables as the newest of the three, giving the GA version in a parenthetical.** No question may turn on the version. Recording it so the fact-accuracy audit reads the parenthetical as deliberate rather than as an un-updated number, and so a reader studying eighteen months from now cannot get a question wrong for the right reason.

9. **Windows and dual-stack — scope guards, recorded so omissions read as decisions.**
   Three Windows-specific facts appear in the cached sources: the network model's host-network-Pod exception, the `kernelspace` proxy mode, and (implicitly) the absence of the other three modes. §1 states the first in a clause and §6 lists the second in the mode table; nothing else Windows-specific appears anywhere in the chapter, and nothing is built on either. Similarly, the sources' "for each address family" and "A and/or AAAA" phrasing is quoted where it appears and **dual-stack is never explained**. Both are correct handling for an associate-tier book. Recorded so the audit does not flag them as gaps.

10. **Eight sections for seven points — fold options considered and rejected.**
    Chapter 8 shipped eight for five points; this chapter proposes eight for seven, so the density is lower and the case is easier. Three folds were still considered: **§2 into §3** (open the type ladder with the churn problem) — rejected, §2 discharges three published cross-bearings including one whose prose says the churn fact *is the premise of Chapter 9*, and burying that inside a section about types pays a headline promise in a subordinate clause; **§5 into §3** (headless as a fifth type) — rejected outright, and it is worth stating why: presenting headless as a *type* is precisely the misconception B1 trap #40 describes, and the structural choice would teach it before the prose could correct it; **§6 into §4** (kube-proxy as the consumer of EndpointSlice) — the closest call, and rejected because §6 is the chapter's designated arousal-restoration point between its two highest-cost sections, and folding it puts §3 and §7 in adjacent high-attention positions with nothing between them. **The eight sections are the right shape.** Raised so the reviewer knows the alternatives were weighed.

11. **Zenith-section heading glyph — two shipped chapters disagree (book-level, recorded).**
    Chapter 7 shipped `## ☀️ §7 — Everything Is a Filter or a Score`; Chapter 8 shipped `## ⚪ §8 — Rules, or Consequences`. The glyph slot in the house heading form is a *difficulty* indicator, and ☀️ is not one of the four difficulty indicators — so Chapter 8's form is the more defensible and it is also the more recent. §8 above is specified as `## ⚪ §8 — A Query With a Name`, with the `☀️ **Zenith:**` marker inside the section where it belongs. **Recommendation: follow Chapter 8, and add Chapter 7 to the book-level reconciliation sweep already queued for Chapters 2 and 3's heading drift.** Do not fix Chapter 7 from inside this chapter.

12. **Domain weight disclosure (recurring, no action needed).**
    `domain_weight_pct: 7` is authored judgement. CNCF publishes four domain weights — D2 Container Orchestration at 28% — and no competency weights (B1 gap G33, B2 disclosure #1). The metadata line must carry the disclaimer in the shipped house form and the front matter must already say so. Recorded per-chapter so no chapter ships without it.

13. **Heading-form drift in Chapters 2 and 3 (recurring, do not fix from here).**
    Chapters 2 and 3 ship `## §1 — ⚪ Title`; Chapters 5 through 8 ship `## ⚪ §1 — Title`. Chapter 9 follows the later form. Still queued for a book-level reconciliation sweep; do not fix Chapters 2 and 3 from inside this chapter.
```

---

**Four things worth your attention before Stage 2 runs:**

1. **Two of the arc outline's three blocking gaps for this chapter are already closed.** G13 (CoreDNS and DNS for Services and Pods) and G24 (kube-proxy modes) are both fully covered by snapshots fetched after B1 ran — `k8s-docs-dns-pod-service`, `k8s-docs-dns-cluster-addon` and `k8s-docs-virtual-ips-kube-proxy` between them supply every record shape, the search-list explanation, all four proxy modes and the default. **G11 (CNI) is the one that remains**, and it's half-closed: CNI is named as an interface, but nothing cached says Kubernetes ships no plugin — which is the half §1's pinned argument rests on. One fetch closes it.

2. **Section numbering is not free here, unlike Chapter 8.** Thirteen inbound cross-bearings, and two of them pin sections by number: `chapter-02` line 600 pins §1 to CNI, `chapter-05` line 858 pins §4 to readiness-and-endpoint-membership. Both fall out naturally from the pedagogy, so the constraint costs nothing — but a later restructure would silently break two shipped chapters, and the outline records the pins in a frontmatter comment so it can't happen quietly.

3. **One genuine cross-chapter decision, raised as Open question #5.** **[B3]** wants cross-cutting theme #3 named in Chapter 10 (Ingress without a controller). Chapter 9 has two earlier and simpler instances — a LoadBalancer Service on bare metal, and a Service whose selector matches nothing. The outline keeps B3's placement and has §3 and §4 state their instances concretely so Chapter 10 names the pattern with three examples instead of one, but it's worth an explicit decision rather than a default, and Chapter 10's outline should be told which way it went.

4. **Question budget moves 39 → 44**, matching the 15-Bearings-across-three-checkpoints shape Chapters 3 through 8 all shipped. B4 states the 10 is a floor to exceed; the chapter has three separable blocks and folding to two checkpoints would put its two densest recall sections back to back.