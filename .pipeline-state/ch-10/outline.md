I have everything I need: the B6/B7 contracts, the eight published cross-bearings into Ch 10 (four section-pinned), the cached sources, and Ch 9's shipped handoff. One significant collision surfaced — Ch 3 §4 already *named* the absent-component pattern that B6 assigns Ch 10 to name.

---

```
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

# Chapter 10 Outline — Traffic from Beyond the Cluster

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 10: Traffic from Beyond the Cluster` | required | top |
| `## *"Frozen, superseded, and inert without a controller"*` | required | line 2 |
| Metadata line (domain / weight / complexity / novelty) | required | after subtitle — **conform to the shipped ch-02/-05/-07/-08/-09 house form**, carrying the published 28% domain weight with the CNCF source tag inline plus the authored-allocation disclaimer |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings #1–#3` | **required, min 2** | after §3, §5, §7 |
| `★ Fixed Point` ×7 | **required, min 1** | §1, §2, §3, §4, §5, §6, §7 |
| `**Dead Reckoning:**` ×1 min | **required** | §7 — the out-of-scope list stated flat, no register at all. See §7 |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §4 (frozen is not deprecated), §7 (a policy on an unsupporting plugin is silently inert) |
| `☀️ Zenith` | expected | §8 |
| `## Exam Alert! 🚨` | **required** | after §8 |
| `## Practice Questions` | **required** | 17 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19; hands to Ch 11 |
| `🏆 Safe Harbor` | expected | chapter close |

**Heading form.** `## 🔵 §2 — Routing by Host and Path`, matching Chapters 5–9 and B6 Collision #3's recommendation. Difficulty glyph before the section number.

**Zenith heading glyph — adopt `☀️`.** B6 Collision #4 recommends `## ☀️ §N — Title` on the closing section for Chapters 9–19. Chapters 5, 6 and 7 shipped that way; Chapters 8 and 9 shipped an ordinary difficulty glyph instead. **This chapter follows B6: `## ☀️ §8 — Nothing Happens Without a Controller`**, *plus* an inline `☀️ **Zenith:**` block inside §8 exactly as `chapter-09` line 1178 does. The two are not alternatives — the heading glyph signposts the section, the inline block is the branded marker the structural contract matches on. See § Open questions #9.

**Zenith:** exactly one, per Part 18.10. `ch10-zenith-nothing-without-a-controller` in §8.

**⚠ The word `ingress` carries two unrelated meanings in this chapter, in adjacent halves of it.** Per the B7 ledger's Canonical forms table, `Ingress` capitalised is the API object and the controller that fulfils it (§2, §3, §4); lowercase `ingress` is a *direction of traffic* in a NetworkPolicy (§6, §7). This is the only chapter in the book that carries both, and it carries them four sections apart with nothing in between to reset the reader. **§6 must open by disposing of the collision explicitly** — one sentence, before any policy semantics, saying that the word is about to mean something completely different and that the capitalisation is the tell. Getting this wrong does not produce a confused sentence; it produces a reader who thinks NetworkPolicy has something to do with the Ingress object, which is a misconception the chapter would then spend §7 failing to dislodge.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 10 — Traffic from Beyond the Cluster". Carried forward without modification:

- **Covers**: **D2.1** — Ingress; Ingress controllers; TLS termination; name-based virtual hosting; simple fanout; edge router; the Ingress freeze and the Gateway recommendation; Gateway API (GatewayClass / Gateway / HTTPRoute, role-oriented design, request flow); NetworkPolicy (ingress and egress isolation, selectors, ipBlock, additive semantics, plugin dependency, the out-of-scope list).
- **Prerequisites**: Ch 9 — Service, ClusterIP, LoadBalancer, DNS.
- **Retrieval targets**: **20%** **[B3]**, from Ch 6–9, with the **≥4-back spacing floor** satisfied by **Ch 4 (labels and selectors, six chapters back)** and redundantly by **Ch 3 (the absent-component pattern, seven back)**. Named anchors: the Service-type ladder against what Ingress actually replaces; selectors now selecting NetworkPolicy subjects.
- **Question budget**: 8 Soundings · 10 Bearings · 17 Practice. Bearings set at 15 below, per B4's "minimums to exceed" and the shape Chapters 3–9 shipped.
- **Figures**: five anchors, listed verbatim in `figures_planned`.
- **Depth band**: standard.
- **Blocking gaps**: G25 (Gateway API detail). **Status: CLOSED.** `k8s-docs-gateway-api-2026-08-23.md` was fetched after B1 assessed the gap and supplies far more than the "one sentence" B1 recorded — all four design principles, the full resource model with cardinality, and the request flow. §5 is fully sourceable. **Two gaps the arc outline did not anticipate are open and both are consequential — see § Open questions #2 and #3.**
- **Note**: NetworkPolicy is taught once, here. Ch 12 §9 cross-bears in. `ch10-zenith` is designated the named home of cross-cutting theme #3. **That designation is now in conflict with shipped text — see § Open questions #4, which is this chapter's one blocking editorial decision.**

### Debts falling due in this chapter

**Eight published cross-bearings point at Chapter 10**, four of them pinned to a section number. Draft knowing the reader was told to expect each one.

| Owed by | Promise made | Paid in |
|---|---|---|
| `chapter-02` line 871 | *"NetworkPolicy"* — dropped in an answer key distinguishing **network** segmentation from **workload-to-host** isolation. The reader was told, while learning RuntimeClass, that NetworkPolicy segments network reachability and does nothing about the boundary between a workload and its host | **§6 opening**, one clause. The scope statement is §6's first Fixed Point anyway; this debt costs nothing extra and closes a loop the reader may well remember, because it was the discriminator on a graded question |
| `chapter-03` line 604 | *"an Ingress with no Ingress controller does nothing at all: the same pattern, first recurrence"* — **and Ch 3 named the pattern**, in a ⚓ Worth Securing callout, with the exact phrase *"an object without its component does nothing"* | **§3**, which must **retrieve Ch 3's phrase verbatim and must not coin a competing one.** See § Open questions #4 |
| `chapter-04` line 835 | *"NetworkPolicy selects both its subject and its peers"* — dropped inside the labels-as-universal-join section. Chapter 4 pre-loaded the *structural* insight of §6 six chapters early | **§6**, and the framing must be Chapter 4's: two selectors doing two different jobs in one object |
| `chapter-06` line 1005 | *"Ingress without an ingress controller"* | **§3** |
| `chapter-09` line 407 | *"Ch 10 §6 — NetworkPolicy"* — **section-pinned**. Ch 9 §1 stated network-model rule 2 with its *"barring intentional network segmentation"* hedge and pointed the hedge here | **§6** |
| `chapter-09` line 544 | *"Ch 10 §1 — the exposure ceiling and what crosses it"* — **section-pinned**, and Ch 9 §3 did the arithmetic already: one external address per Service, fine for one, expensive for fifty; no Service type knows anything about HTTP | **§1** |
| `chapter-09` line 1056 | *"Ch 10 §2 — name-based virtual hosting"* — **section-pinned**, and it arrives with a warning attached: Ch 9 §7 explicitly distinguished **DNS-based service discovery** from **name-based virtual hosting** and told the reader that conflating them *"makes Chapter 10 considerably harder than it needs to be"* | **§2**, and §2 must complete the distinction rather than assume it |
| `chapter-09` line 1706 | *"Ch 10 §6 — NetworkPolicy"* — restated in The Voyage Ahead | **§6** |

**Chapter 9's Voyage Ahead made four specific promises.** It is the immediately preceding chapter and the reader will have read it minutes ago. Honour all four literally:

1. **"Chapter 10 crosses the boundary."** It introduces the objects that route on the *contents* of an HTTP request — hostnames, paths, headers — so one address can serve many services. §1 and §2.
2. **"Something standing at the entrance finally reads the writing on the crate before deciding where it goes."** The crate metaphor is Chapter 2's and has been running for eight chapters. §2 is where it pays off. Use it once; do not run it into the ground.
3. **"It explains why the Kubernetes project now recommends one API over the one most people learned first, and what 'frozen' means in that recommendation, which is a more precise word than it looks and worth exactly the attention you'd give a definition on an exam."** §4. Chapter 9 has effectively pre-sold this fact as examinable; §4 must be worth the build-up.
4. **"It also opens with an object that you create, and that does nothing at all — because the component that acts on it has not been installed. You have seen that shape twice in this chapter now. Chapter 10 gives it a name, and once it has a name you will start seeing it everywhere."** §3 — **and note the mismatch.** Ch 9 says *opens with*; the section pins put the ceiling at §1 and the object at §2–§3. The mismatch is small and one sentence fixes it — see § Open questions #5.

**On Chapter 9's "twice in this chapter."** The two Ch 9 instances the reader is expected to be holding are the bare-metal LoadBalancer Service that waits forever for an external address nobody is providing (Ch 9 §3), and the Service whose selector matches nothing — real object, real cluster IP, real DNS record, empty EndpointSlice, traffic goes nowhere (Ch 9 §4). §3 and §8 should name both back. They are the reader's own evidence, and retrieving them is cheaper and more convincing than asserting the pattern again.

### What this chapter owes forward

| Owed to | What | Why it matters |
|---|---|---|
| **Ch 12 §9** | **NetworkPolicy's additive, allow-only, no-deny semantics, stated in a form that can be retrieved rather than re-derived** | Ch 12 §9 is the Security chapter's Zenith and its whole argument is that RBAC and NetworkPolicy share **one** semantic. That argument only works if §6 has established the NetworkPolicy half cleanly and Ch 12 §3 establishes the RBAC half. **§6 must state the semantic as a semantic**, not as a NetworkPolicy quirk |
| **Ch 12 §5** | **The scope boundary: NetworkPolicy is L3/L4 network reachability and nothing else** | Ch 12 §5 owns `securityContext` — what a Pod may do to its *node*. `chapter-02` line 871 already told the reader these are different axes. §6's scope statement is what keeps Ch 12 §5 from having to re-argue it |
| **Ch 13 §7** | **The pattern, named, retrievable by name** | Cross-cutting theme #3. Ch 13 §7 explains why `kubectl top` fails on a bare cluster and **[B3]** requires it to retrieve the pattern *by name* rather than re-derive it. Whatever name §3 and §8 settle on is the name Ch 13 §7 will use |
| **Ch 17 §7** | **The same, second retrieval** | VPA is an addon and is not shipped by default. Same pattern, fourth instance, and Ch 3 line 606 already published the pointer |
| **Ch 16 §4** | **Nothing** | Ch 16 §4 debugs Services from the application side — selector mismatch, empty EndpointSlice, `port` vs `targetPort`. That is Ch 9's material, not this chapter's. **This chapter owes Ch 16 nothing and must not build an Ingress troubleshooting workflow** on the assumption that it does |
| **Ch 17 §5** | **The gap a mesh fills** | A service mesh does L7 routing, mTLS and policy for *east-west* traffic; this chapter does L7 routing for *north-south* traffic and L3/L4 policy for east-west. §1's L4/L7 framing and §7's out-of-scope list are what make Ch 17 §5's contribution legible. **One forward cross-bearing, no content** |

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**Open on the arithmetic, because Chapter 9 already did it and the reader is holding the result.** Chapter 9 ended by naming a ceiling: one external address per Service is fine for one Service and absurd for fifty, and no Service type in that chapter can tell `shop.example.com/checkout` from `shop.example.com/catalog`, because at the layer they operate on, those are bytes in a payload. This chapter is what sits above that ceiling. Do not re-derive the arithmetic — Chapter 9 line 540 did it in three sentences and the reader read them recently. Retrieve it in one clause and move.

**The identity frame is the shift from writing objects to knowing who reads them.** Every chapter so far has rewarded the same professional instinct: get the object right, and the cluster does the rest. This is the chapter where that instinct is not enough, and where the reader learns the question that separates people who have run Kubernetes from people who have read about it. It is not *did I write the object correctly.* It is **is anything watching this object.** A well-formed Ingress on a cluster with no Ingress controller is a correct object that does nothing. A well-formed NetworkPolicy on a network plugin that does not implement NetworkPolicy is a correct object that does nothing — and unlike the Ingress, it does nothing *quietly*, because unreachability is loud and unrestricted reachability is silent. That asymmetry is the most valuable thing in the chapter and it is worth saying plainly in the opening.

**The curiosity gap is already open and it was Chapter 9 that opened it.** Chapter 9's Voyage Ahead told the reader that Chapter 10 would give a name to a shape they had already met twice. Do not re-open the gap; *acknowledge* it, and add the part Chapter 9 did not say — that they will meet it **twice more in this chapter alone**, in two objects that look nothing like each other, and that this is the chapter where it stops being a curiosity and becomes a rule they can apply to things this book never mentions.

**The stakes, stated flat, with one genuine escalation.** Five points on this book's authored allocation — CNCF publishes four domain weights and no competency weights, and the front matter says so. That is the smallest allocation in Part III and the material is still worth full attention for two reasons that should be given rather than asserted. First, `frozen` versus `deprecated` is the most precise word-level distinction in the whole curriculum, and precise distinctions are what multiple-choice exams are built out of. Second, NetworkPolicy carries **six of B1's cataloged traps** — more than any other single topic in this book — and every one of them is a case where the reader's existing firewall intuition gives the wrong answer. **Do not manufacture urgency beyond that.** The two reasons are real; the chapter does not need a third.

**⚠ Part 14 subject-dignity constraint, and this chapter is where it actually bites.** §7's central fact is that a NetworkPolicy on an unsupporting plugin is a *silent security failure*. That is a real-world harm with real-world victims, and the wry register must stay oriented at the practitioner's reasonable expectation — you wrote a policy, `kubectl get` showed it to you, of course you believed it — and never at anyone's breach, and never at the people whose data moved through the gap. No war stories about incidents. No knowing asides about somebody's bad afternoon. State the mechanism, state the consequence, and let it land without decoration.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Six outcomes, active verbs:

- **State** what Ingress does, what it explicitly does not do, and which two protocols are the whole of its remit.
- **Distinguish** a simple fanout from name-based virtual hosting, and both from the DNS-based service discovery you learned last chapter.
- **Explain** why a correctly written Ingress can have no effect whatsoever, and name the thing whose absence causes it.
- **Say what `frozen` means** — precisely, in both of its halves — and why it is not the same word as `deprecated`.
- **Name** the three Gateway API resources and the organisational role each one belongs to.
- **Predict** whether a given connection is allowed under a given set of NetworkPolicies, using rules that are additive, allow-only, and applied at both ends.

*You'll also acquire one rule that outlives this chapter: an object without its component does nothing. You'll use it in Chapter 13, in Chapter 17, and on things this book never gets to.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Prerequisite set per B2: Chapter 9 in its entirety, plus ordinary priors about reverse proxies, virtual hosting, firewalls, TLS, and software deprecation. **Four questions are deliberate retrieval from Chapters 3 and 9; four test priors the reader arrives with.** **[B3]** Soundings sit outside the retrieval budget but do retrieval work anyway, sourced from B2's Prerequisites column.

**Fixed Points this chapter teaches, which Soundings must therefore not reveal:**

1. Ingress exposes **HTTP and HTTPS routes only**. It does not expose arbitrary ports or protocols; anything else uses NodePort or LoadBalancer.
2. An Ingress may give Services externally-reachable URLs, load balance traffic, terminate SSL/TLS, and offer name-based virtual hosting.
3. **You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect.**
4. Ingress controllers *ideally* fit the reference specification; in reality they operate slightly differently.
5. The Ingress API is **frozen**: GA, subject to GA stability guarantees, no plans for removal — **and** no longer developed, with no further changes or updates. The project recommends Gateway instead.
6. Gateway API is **role-oriented**, modelling three roles: infrastructure provider, cluster operator, application developer.
7. GatewayClass / Gateway / HTTPRoute. A Gateway is associated with **exactly one** GatewayClass; **many** Routes may attach to one Gateway.
8. NetworkPolicies control traffic at **OSI layer 3 or 4**, are **application-centric**, and apply to a connection with a Pod on one or both ends.
9. **By default a Pod is non-isolated in both directions.** It becomes isolated for a direction only when some NetworkPolicy selects it *and* names that direction in `policyTypes`.
10. **Policies are additive and never conflict. There is no deny rule.**
11. **Both ends must allow it** — the source Pod's egress policy and the destination Pod's ingress policy.
12. Two things a policy can never do: a Pod **cannot block access to itself**, and traffic **to and from the node where a Pod is running is always allowed**.
13. NetworkPolicies are implemented **by the network plugin**. Creating one without a controller that implements it **has no effect**.

Each question below is checked against that list.

| # | Question topic | What it tests | Spoiler check |
|---|---|---|---|
| 1 | You run one web server on one IP address, and it serves `shop.example.com` and `blog.example.com` differently. What does the server have to look at to tell the two apart — and at what point in the connection does it become available? | The virtual-hosting prior. Most readers have configured this, in Apache, nginx, or a cloud load balancer, without necessarily having named it | Names nothing Kubernetes-specific. Fixed Points #1–#3 are that Kubernetes has an **object** for this, that it covers HTTP/HTTPS **only**, and that the object does nothing on its own. Knowing what a `Host` header is supplies none of those. The reader who answers well will find §2 fast rather than redundant, which is the correct outcome for a prior this common |
| 2 | **Retrieval from Ch 9 §3.** You have fifty services that all need to be reachable from outside the cluster. Chapter 9 gave you a Service type that does that. Name it, then say what fifty of them costs you — in addresses, and in anything else you can think of | The ceiling, which §1 is built on and which Ch 9 line 540 stated outright. **This is the chapter's most important prior and it is only one chapter back**, so it should be nearly free | The reader is retrieving a Chapter 9 fact deliberately. Fixed Point #2's new content is what the *replacement* looks like — one address, rules on it, routing by host and path. "Fifty addresses is expensive" is the problem statement, not the solution, and §1 exists to convert it into a demand |
| 3 | **Retrieval from Ch 9 §3.** Which of Chapter 9's four Service types can send `/checkout` to one set of Pods and `/catalog` to another? Say why | The L4/L7 boundary, in the form Ch 9 line 542 already gave the reader. The correct answer is **none of them**, and the reason is that they move packets rather than reading requests | Ch 9 said this explicitly. Retrieving it is not spoiling it. Fixed Point #1 — the HTTP/HTTPS-only remit, and that other protocols fall *back* to NodePort and LoadBalancer — is the reciprocal fact and is not reachable from here. The reader learns that the new thing does HTTP; they do not yet learn that it does **only** HTTP, which is trap #43's whole target |
| 4 | On the firewalls you have configured or worked behind: if a packet matches no rule at all, is it allowed or dropped? And if one rule permits something a later rule forbids, which one wins? | **The chapter's most important prior, and the one the chapter contradicts.** Nearly every reader answers "denied by default" and "the deny wins", because that is how ordinary firewalls behave and it is a good instinct everywhere else | Deliberately does not mention Kubernetes. Fixed Points #9 and #10 are the **inversion** of both halves — non-isolated by default, and no deny rule exists to win with. This question exists so that §6 lands as a genuine correction rather than as a list of properties. It is the direct structural analogue of Chapter 9's NAT question, and like that one it must stay phrased as a situation |
| 5 | Two APIs. One is announced as **deprecated**. The other is announced as **no longer being developed, with no further changes**. For each, say whether you would expect it to be removed, and whether you would start a new project on it today | The deprecation prior, and the reader's semantic intuition about a word they use constantly | Names no Kubernetes API. Fixed Point #5 is that Ingress is specifically the **second** of these, that both halves of the statement are load-bearing, and that the project's recommendation to use Gateway coexists with a commitment not to remove Ingress. The question surfaces the distinction as a *general* one so §4 can land it as a *specific* one — which is exactly the beat Chapter 9's Voyage Ahead promised |
| 6 | **Retrieval from Ch 3 §4.** Chapter 3 asked you to remember a one-sentence rule about objects and the components that act on them. Write it down. Then name one place you have already met it | The named pattern, seven chapters back — the **≥4-back floor item in pre-test position**, and the chapter's spine | ⚑ **Read the spoiler analysis carefully.** This question can be answered by a reader who then predicts Fixed Point #3. That is acceptable and in fact desirable: per skill Part 11 rule 2, Soundings questions must be answerable from prerequisites, and Ch 3 line 601 made this one a prerequisite on purpose. The stem names no Chapter 10 object. What the chapter teaches is not the rule — the reader was already given the rule — but **two new instances, one of which fails silently**, plus the promotion of an aside into something they can apply to objects this book never covers. The rule is the pre-test; the applications are the chapter |
| 7 | **Retrieval from Ch 9 §1.** Chapter 9's second network-model rule said all Pods can reach all Pods — *"barring intentional network segmentation."* What do you think that hedge was pointing at, and at what layer would something have to sit to enforce it? | The hedge, which Ch 9 §1 planted and pointed here by number twice. Tests whether the reader noticed a qualifier that most readers skim past | Ch 9 published the pointer, so the *existence* of an answer is not a secret. Fixed Points #8 through #13 — layer 3/4, application-centric, non-isolated default, additive, both-ends, the two exceptions, the plugin dependency — are the entire content of §6 and §7 and none of them is reachable from "something must be able to restrict it." A reader who reasons that the enforcement has to live wherever the packets actually move has independently derived §7's plugin dependency, and §7 should acknowledge that when it arrives |
| 8 | A client connects to `https://shop.example.com` and the request eventually reaches an application server. Where does the TLS connection actually end? Who holds the certificate and private key, and what does the application server see arriving? | The TLS-termination prior. Nearly universal among the readers this book targets, and rarely stated precisely | Fixed Point #2 includes TLS termination as one of four things an Ingress may do, and §2 adds the Kubernetes-specific mechanism — a Secret holding the key and certificate, which retrieves Chapter 4. The prior supplies the concept; §2 supplies the object. No overlap |

**Rubric**: standard 6+ / 3–5 / 0–2 per `branded-terms.yaml`. **The 0–2 branch carries an unusually specific and unusually blunt instruction**, because this chapter's `prereq_factor` is `heavy` and the dependency is on exactly one chapter: **if questions 2, 3 or 7 were the misses, go back to Chapter 9 before starting §1.** Not "review" — go back. This chapter re-teaches no part of the Service model, and a reader without Ch 9 §3's ladder will find §1's argument unmotivated and §2's backends unintelligible. Say it plainly and without softening; the reader's time is better spent on a re-read than on a chapter that cannot land.

**Note for drafting:** questions 1, 4, 5 and 8 must stay phrased as situations drawn from the reader's own working life. **Question 4 is doing the heaviest lifting in the set** and its phrasing decides whether §6 works. It must make the reader commit to "default deny, and the deny wins" *before* §6 tells them Kubernetes does neither. Do not soften it into "how do firewalls work," and do not hedge it — the whole value is in the reader being confidently wrong for ninety seconds.

---

## 4. Section plan

Eight sections. Three are pinned by number (§1, §2, §6 — see § Debts). The chapter is **two arcs joined at the Zenith**, and drafting should hold that shape consciously rather than letting it read as one long list:

- **§1–§5, the API-generations arc.** Where the previous chapter's mechanism runs out (§1), the object that goes above it (§2), the thing that has to exist for the object to matter (§3), why that object is now in a peculiar and precisely-worded state of retirement (§4), and what the project wants you to use instead (§5).
- **§6–§7, the policy arc.** How you restrict traffic on the flat network Chapter 9 built (§6), and the two things that restriction cannot do (§7).
- **§8 joins them**, and the join is not thematic decoration: §3's Ingress-without-a-controller and §7's policy-on-an-unsupporting-plugin are **the same failure in two objects that have nothing else in common.** That is what makes the Zenith earned rather than asserted.

**The chapter's failure mode is treating the two arcs as one topic because they share a chapter.** They do not share a topic; they share a *pattern*, and the pattern is §8's property. §5 must not gesture at NetworkPolicy, and §6 must not gesture back at Ingress except in the one sentence disposing of the word collision. Let §8 do the joining.

**One running example threads the chapter**, and it should be the same shop Chapter 9 used in its ceiling argument, because continuity across a chapter boundary is nearly free here. `shop.example.com` with a `catalog` Service and a `checkout` Service, both ClusterIP. §1: two LoadBalancers would be two addresses and two bills. §2: one Ingress, two paths. §3: nothing happens, because nobody installed a controller. §4: the API you just used is frozen. §5: here is the same routing expressed in the API that replaces it. §6: now `checkout` should be reachable from `catalog` but not from anything else. §7: and here is what that policy cannot do for you. §8: two of these objects did nothing until something was watching them.

### §1 — ⚪ Where LoadBalancer Runs Out

**Section-pinned by `chapter-09` line 544.** Chapter 9 §3 wrote the argument and Chapter 9's Voyage Ahead restated it. §1's job is emphatically **not** to make the argument again — it is to accept it, name the vocabulary the rest of the chapter needs, and get out. This is a short section.

**First, retrieve the ceiling in one move.** One external address per Service. Fifty Services, fifty addresses, fifty provisioned load balancers, fifty things to pay for and manage. And no Service type reads HTTP, so one address cannot serve two paths. Two sentences of retrieval, cross-beared to Ch 9 §3. **Do not re-derive it and do not re-illustrate it in prose** — the reader read this within the hour.

**Second, name the layer boundary, because the rest of the chapter is organised by it.** Chapter 9's mechanisms operate at **layer 4**: they move packets to an address and a port and have no opinion about the contents. What this chapter adds operates at **layer 7**: it reads the request — the host it was addressed to, the path it asked for — and decides on that basis. The distinction is worth its own beat because §6 goes *back down* to layers 3 and 4, and a reader without the ladder in mind will experience NetworkPolicy as an unrelated topic that happened to land in the same chapter.

**Third, name north-south and east-west**, briefly, because they are ordinary practitioner vocabulary this book has not yet used and because they are the cleanest way to say what §1–§5 and §6–§7 are respectively about. Traffic entering the cluster from outside is north-south; traffic between Pods inside it is east-west. Two clauses. This chapter does one of each, which is worth saying out loud once.

**Fourth, the edge router, from the source's own terminology section.** The reader needs one piece of scaffolding that Chapter 9 did not supply: the cluster's nodes are **not part of the public internet**, and there is a router that enforces the cluster's firewall policy — a gateway managed by a cloud provider, or a physical piece of hardware. That is the **edge router**, and it is the thing an Ingress controller may configure. Naming it here keeps §3's "usually with a load balancer, though it may also configure your edge router" from arriving as an unexplained clause.

**Close by naming the object and handing to §2 — and this is where Chapter 9's fourth promise gets kept.** Chapter 9 said this chapter *opens* with an object that does nothing. Under the pinned numbering the object arrives in §2 and its inertness in §3, so §1's last line should name it and flag the shape: there is an object for this, it is called Ingress, and the first thing worth knowing about it is that writing one may accomplish absolutely nothing. That one sentence converts a mismatch into a deliberate two-beat setup. See § Open questions #5.

- **Objectives**: D2.1
- **Concepts introduced**: `exposure-ceiling`, `l4-l7-boundary`, `north-south-traffic`, `east-west-traffic`, `protocol-aware-routing`, `edge-router`, `cluster-network`
- **Sources**: `k8s-docs-ingress-2026-08-23.md` (the Terminology block verbatim — Node, Cluster with "nodes in the cluster are not part of the public internet", **Edge router** as "a router that enforces the firewall policy for your cluster (a gateway managed by a cloud provider or a physical piece of hardware)", Cluster network, and Service as identifying Pods by label selector with virtual IPs "only routable within the cluster network"). `k8s-docs-network-model-2026-08-23.md` (Gateway API and Ingress as the protocol-aware HTTP/HTTPS routing layer using URIs, hostnames and paths; `type: LoadBalancer` as the simpler but less-configurable mechanism for cluster ingress). `k8s-docs-service-2026-08-23.md` (retrieval only — the type definitions, already taught in Ch 9)
- ⚠ **SOURCE NOTE — north-south / east-west are not in the cached set.** They are standard industry vocabulary rather than Kubernetes-project terminology, and no snapshot uses them. Either introduce them explicitly as the industry's words rather than the project's, or cut them. **Recommendation: keep, labelled.** They earn their place by making the chapter's two-arc structure sayable in one sentence, and the book has been scrupulous elsewhere about marking the author's framing as the author's. Do not attach a `[source:` tag to them
- **Figure**: `ch10-fig01-ingress-vs-service-loadbalancer`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — everything in Chapter 9 moves **packets** to an address. Everything in §2–§5 reads **requests**. That is the layer boundary, and which side a mechanism sits on determines what it can possibly know
  - `> 🪢 **Mnemonic:**` — *north-south goes through the wall; east-west stays inside it.* §1–§5 is the wall; §6–§7 is inside
- **Cross-bearings**: back to Ch 9 §3 (**mandatory — the pinned payoff**; the ladder and the ceiling, retrieved rather than restated); back to Ch 9 §7 (one clause — the Service names of the previous chapter are the backends of this one); forward to **§2**; forward to **§6** (the layer boundary, which §6 crosses back over); forward to Ch 17 §5 (one clause — a service mesh does at layer 7 for east-west traffic what §2 does for north-south)
- ⚠ **Do not re-teach the Service types.** Ch 9 §3 owns them. The B7 ledger records them as Ch 9's and this chapter as a referrer. A §1 that re-explains NodePort has spent the reader's patience on something they already have
- ⚠ **Keep this section short.** It is scaffolding, not content. Its one original contribution is the layer boundary; everything else is retrieval and vocabulary

### §2 — 🔵 Routing by Host and Path

**Section-pinned by `chapter-09` line 1056, and the pin arrived with a warning attached.** Chapter 9 §7 told the reader in as many words that conflating **DNS-based service discovery** with **name-based virtual hosting** *"makes Chapter 10 considerably harder than it needs to be"*, and pointed here. §2 must complete that distinction rather than assume the reader carried it.

**First, what Ingress is, in the source's own frame.** Ingress **exposes HTTP and HTTPS routes from outside the cluster to Services within the cluster.** Traffic routing is controlled by **rules defined on the Ingress resource**. That is the definition; give it plainly and early, and note that the backends it routes to are ordinary Services — the ClusterIP Services of Chapter 9, unchanged and unaware.

**Second, the four capabilities, as a set**, because they are how the object is described wherever it is described: an Ingress may be configured to give Services **externally-reachable URLs**, **load balance traffic**, **terminate SSL/TLS**, and offer **name-based virtual hosting**.

**Third, the limit, stated immediately after the capabilities and not buried.** An Ingress **does not expose arbitrary ports or protocols.** Exposing anything other than HTTP and HTTPS to the internet typically uses `Service.Type=NodePort` or `Service.Type=LoadBalancer` — which is a genuinely satisfying structural fact rather than a caveat, because it means the ladder Chapter 9 taught is not superseded by this chapter, it is *specialised past*. The reader who wants to expose a database or a game server or anything speaking its own protocol goes back down to §1's layer. **Trap #43 lives here** and this is the only place it is defused.

**Fourth, the shapes an Ingress takes, which is the section's examinable core.** Four, from the source's own list, and they should be taught as a progression rather than an enumeration:

- **Ingress backed by a single Service** — the degenerate case, one rule, one backend. Worth thirty seconds so the more interesting cases have a baseline.
- **Simple fanout** — routes traffic from a **single IP address** to **more than one Service**, based on the **HTTP URI**. This is the running example: `shop.example.com/catalog` and `shop.example.com/checkout`, one address, two Services.
- **Name-based virtual hosting** — routing HTTP traffic to **multiple host names at the same IP address**. `shop.example.com` and `blog.example.com`, same address, different Services.
- **TLS** — secure an Ingress by specifying a **Secret** that contains a TLS private key and certificate. This retrieves Chapter 4 at six chapters' distance and it is the chapter's cheapest retrieval: the reader knows what a Secret is, and here is a Secret doing a job they can see.

**Fifth — the distinction Chapter 9 demanded, and it deserves its own short beat.** Both DNS-based service discovery and name-based virtual hosting involve hostnames, and they sit on **opposite sides of the connection**. DNS turns a name into an address *before any traffic moves*; virtual hosting sorts traffic that has *already arrived* at a single address, by reading the name out of the request. Chapter 9 stated exactly this and pointed here; §2 should complete it by making it concrete against the running example — the client's resolver returns one address for both hostnames, and the sorting happens after the connection is established.

**Sixth, the fields, at whatever depth § Open questions #3 resolves.** An Ingress rule carries a host and a set of paths, and each path names a backend Service and port. **`pathType` and the default backend are not in the cached source set** — see the gap note below and § Open questions #3 before drafting this paragraph.

- **Objectives**: D2.1
- **Concepts introduced**: `ingress`, `ingress-rule`, `ingress-host`, `ingress-path`, `simple-fanout`, `name-based-virtual-hosting`, `tls-termination`, `single-service-ingress`, and conditionally `path-type` and `default-backend`
- **Commands**: `kubectl-get-ingress` (the verb is Chapter 8's; only the resource type is new)
- **Sources**: `k8s-docs-ingress-2026-08-23.md` (What is Ingress — the HTTP/HTTPS scope, rules defined on the resource, the four capabilities, and "An Ingress does not expose arbitrary ports or protocols. Exposing services other than HTTP and HTTPS to the internet typically uses a service of type Service.Type=NodePort or Service.Type=LoadBalancer"; Types of Ingress — single Service, simple fanout by HTTP URI, name-based virtual hosting, TLS via a Secret containing key and certificate, load balancing). `k8s-docs-secret-2026-08-23.md` (retrieval only — the `kubernetes.io/tls` Secret type, already taught in Ch 4 §4). `k8s-docs-dns-pod-service-2026-08-23.md` (retrieval only — the discovery half of the fifth beat, already taught in Ch 9 §7)
- ⚠ **SOURCE GAP — BLOCKING for the sixth beat. See § Open questions #3.** The cached Ingress snapshot is a 22-line summary. It does **not** contain: `pathType` and its three values (`Exact`, `Prefix`, `ImplementationSpecific`), the default backend, the `spec.rules[].http.paths[].backend.service.name`/`.port` structure, `spec.tls[]`, or a worked manifest. B6 assigns *path types* and *default backend* to this section and neither is currently sourceable. Fetching `kubernetes.io/docs/concepts/services-networking/ingress/` in full closes it
- **Figure**: `ch10-fig02-ingress-fanout-and-name-based-hosts`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — Ingress is **HTTP and HTTPS only**. It exposes no arbitrary ports and no other protocols. Anything else goes back down to NodePort or LoadBalancer
  - `★ **Fixed Point:**` — **simple fanout** splits by *path* at one host; **name-based virtual hosting** splits by *host* at one address. Both put many Services behind one IP; they differ in what the rule reads
  - `> ⚠ **Navigational Hazards:**` — DNS gave you the address. Virtual hosting decides what happens *after* you have used it. Same hostname, two completely different jobs, on opposite sides of the connection — this is the confusion Chapter 9 warned you about by name
  - `> ⚓ **Worth Securing:**` — TLS termination at the Ingress means the private key lives in a Secret in the cluster and the backend Services can speak plain HTTP. Convenient, and worth knowing precisely, because it means the traffic between the Ingress and the Pod is *not* encrypted by this arrangement — which is one of the things Chapter 17 will say a service mesh is for
- **Cross-bearings**: back to Ch 9 §7 (**mandatory — the pinned payoff**; the discovery-versus-virtual-hosting distinction Chapter 9 flagged and deferred); back to Ch 9 §2 (the Services being routed to are ordinary ClusterIP Services and this chapter changes nothing about them); back to Ch 4 §4 (**mandatory** — the Secret holding the TLS key and certificate); back to **§1** (the layer boundary — this is what reading the request buys); forward to **§3** (**mandatory** — none of this has happened yet); forward to **§5** (HTTPRoute expresses the same two shapes); forward to Ch 17 §5 (one clause — what terminating TLS at the edge leaves un-encrypted)
- ⚠ **Do not teach specific Ingress controller products.** Not `ingress-nginx`, not Traefik, not any cloud provider's implementation. §3 owns the fact that they differ; naming and comparing them is out of scope for the exam and dates the book badly
- ⚠ **Do not teach `cert-manager`, `external-dns`, or annotation-driven controller configuration.** Uncached, ecosystem-specific, above associate tier
- ⚠ **Do not write a full Ingress manifest** unless § Open questions #3 resolves in favour of fetching the field-level source. A partial manifest with invented field names is worse than no manifest

### §3 — ⚪ The Object Is Not the Implementation

**The chapter's spine, and the payoff for three published cross-bearings** (`chapter-03` line 604, `chapter-06` line 1005, and Chapter 9's Voyage Ahead promise). **⚑ Read § Open questions #4 before drafting this section** — the B6 skeleton and the arc outline both designate this chapter as the place the pattern is *named*, and shipped Chapter 3 already named it.

**First, the fact, stated as flatly as the source states it.** *You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect.* Do not build up to this and do not soften it. §1's last line already told the reader it was coming; the sentence should land like a door closing.

**Second, what an Ingress controller actually is.** The component **responsible for fulfilling the Ingress** — usually with a load balancer, though it may also configure the **edge router** (§1's vocabulary, now doing its job) or additional frontends to help handle the traffic. Note what this means structurally: the Ingress object is a *description of desired routing*, and the controller is a control loop that reads it and makes something in the real world match. **This is Chapter 3's control loop, unchanged**, and the reader should be told so in one clause — it is the fourth or fifth instance they have seen and recognising it is free.

**Third, retrieve Chapter 3's rule by name.** Chapter 3 §4 gave the reader the phrase — *an object without its component does nothing* — and told them they would meet it four more times. This is the first of the four, and Chapter 3 published the pointer. **Retrieve the phrase verbatim; do not coin a synonym.** Then hand them their own evidence from last chapter: the LoadBalancer Service on a cluster with no provider integration that waits forever, and the Service whose selector matched nothing and had an address, a DNS record, and an empty endpoint list. They have already seen this twice. This is the third.

**Fourth, IngressClass, at whatever depth § Open questions #2 resolves.** The mechanism by which an Ingress says *which* controller should fulfil it, which matters because a cluster may run more than one. **Not in the cached source set** — see the gap note.

**Fifth, the fact that keeps this from being a tidy story, and it is examinable.** *Ideally, all Ingress controllers should fit the reference specification; in reality, the various Ingress controllers operate slightly differently.* This is **trap #45**, and it is worth a beat of its own because it is the honest note in an otherwise clean abstraction: the object is portable, its behaviour is not entirely. State it; do not editorialise about it.

**Close by holding the pattern open rather than closing it.** The reader now has a rule and three instances. §8 will add a fourth from §7 and turn it into something they can use on objects this book never mentions. Do not resolve it here — §3 is where the pattern becomes *conscious*, not where it becomes complete.

- **Objectives**: D2.1
- **Concepts introduced**: `ingress-controller`, `absent-component-pattern`, `reference-specification`, and conditionally `ingressclass`
- **Commands**: `kubectl-describe-ingress` (as the way you see that nothing has been assigned; the verb is Chapter 8's)
- **Sources**: `k8s-docs-ingress-2026-08-23.md` (Prerequisites — "You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect. Ideally, all Ingress controllers should fit the reference specification; in reality, the various Ingress controllers operate slightly differently"; What is Ingress — "An Ingress controller is responsible for fulfilling the Ingress, usually with a load balancer, though it may also configure your edge router or additional frontends to help handle the traffic"). `k8s-docs-controllers-2026-08-23.md` (retrieval only — the control loop, taught at Ch 3 §6). `k8s-docs-cluster-addons-2026-08-24.md` (retrieval only — addons are not all shipped by default, taught at Ch 3 §4)
- ⚠ **SOURCE GAP — BLOCKING for the fourth beat. See § Open questions #2.** `IngressClass` appears **nowhere** in the cached set. B6 assigns it to this section. Everything else in §3 is fully sourced. Fetching the full Ingress concepts page closes this and § Open questions #3 together, which is why they are one fetch and two decisions
- **Figure**: none. **Part 18.9 reasoning:** this section's content is a *negation* — the thing that does not happen — and the honest visual for it is the Zenith, where the pattern is drawn once across all four of its instances. A figure here would either duplicate `ch10-fig01` with a controller box added, or pre-spend `ch10-zenith`'s entire argument five sections early. Part 18.7 also applies: the section's central sentence is nine words long and a diagram restating it adds extraneous load for no germane gain
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `★ **Fixed Point:**` — **you must have an Ingress controller to satisfy an Ingress. Only creating an Ingress resource has no effect.** Not "less effect". None
  - `> ⚓ **Worth Securing:**` — retrieve Chapter 3's phrase here, verbatim, and count the instances the reader has personally met: the LoadBalancer with no provider, the Service with no matching Pods, and now this. Three sightings is the point at which a pattern stops being a coincidence
  - `> 🪝 **Snag:**` — trap #45. Two clusters, the same Ingress manifest, different behaviour. The object is portable; the controllers are only *ideally* identical, and the gap between the reference specification and any particular implementation is where a working configuration stops working after a migration
- **Cross-bearings**: back to Ch 3 §4 (**mandatory — the pinned payoff**; Chapter 3 named the rule and pointed at this exact sentence); back to Ch 3 §6 (**mandatory** — the controller pattern, of which this is an instance); back to Ch 9 §3 and Ch 9 §4 (**mandatory** — the reader's own two prior sightings); back to Ch 6 §8 (one clause — a custom controller acting on a custom resource is the same shape, which the reader met as the operator pattern); forward to **§7** (**mandatory** — the second instance in this chapter, and the one that fails quietly); forward to **§8**; forward to Ch 13 §7 and Ch 17 §7 (**mandatory** — Chapter 3 line 605 and line 606 already published both pointers)
- ⚠ **Do not name this the "Ingress problem" or invent a Chapter-10-specific label.** The whole value of cross-cutting theme #3 is that one name covers four unlike situations. A second name for the same rule destroys it

### §4 — ⚪ Frozen, Not Deprecated

**Chapter 9's Voyage Ahead pre-sold this section as examinable, in as many words.** It told the reader that `frozen` is *"a more precise word than it looks and worth exactly the attention you'd give a definition on an exam."* That is a promise about **precision**, and precision is the only thing this section has to deliver. It is short, it is almost pure definition, and it should not be padded.

**First, the statement, in both halves, quoted closely.** The Kubernetes project recommends using **Gateway** instead of Ingress. The Ingress API **has been frozen**: it is **generally available and subject to the stability guarantees for GA APIs** — the project has **no plans to remove Ingress** — but it is **no longer being developed and will have no further changes or updates.**

**Second, split it deliberately, because the trap is in the splitting.** Readers reliably collapse this into one of two wrong summaries: *"Ingress is deprecated"* (drops the stability half) or *"Ingress is fine, ignore the note"* (drops the no-development half). Both halves are load-bearing and they point in different directions:

| The half readers drop | What it actually says | What it means for you |
|---|---|---|
| **Still GA, still guaranteed, no removal plans** | It is not going away and it is not going to break | Existing Ingress configurations are not a migration emergency |
| **No further development, no changes or updates** | Nothing new will ever be added | Anything Ingress cannot do today, it will never do |

**Third, the word `deprecated`, by contrast** — and this is where Soundings question 5 pays off. Deprecation is a signal about a thing's *future removal*. A freeze is a signal about its *future development*. A frozen API can be permanent; a deprecated one is by convention on its way out. Kubernetes has said one of these about Ingress and not the other, and it said the specific one on purpose. **Trap #44 lives here** and it is the single most precise fact in the curriculum, per B2.

**Fourth, what the recommendation does and does not oblige.** *Recommends* is not *requires*. The project recommends Gateway for new work; it has not deprecated Ingress, has not announced removal, and continues to guarantee it. The honest practitioner reading is: do not panic about what you are running, and think hard before building something new on an API that will never gain a feature again. State it that way — it is accurate, it is useful, and it does not overclaim.

- **Objectives**: D2.1
- **Concepts introduced**: `feature-freeze`, `frozen-not-deprecated`, `ga-stability-guarantee`
- **Sources**: `k8s-docs-ingress-2026-08-23.md` (the Note, verbatim and complete — the Gateway recommendation, "The Ingress API has been frozen", GA status and stability guarantees, "the project has no plans to remove Ingress", and "no longer being developed and will have no further changes or updates"). `k8s-keps-and-feature-stages-2026-08-23.md` (the alpha/beta/GA stage vocabulary and what a GA stability guarantee is, taught in outline at Ch 8 — **verify this snapshot's coverage of the deprecation-versus-freeze distinction before relying on it for the third beat; if it does not carry it, present the contrast as reasoning from the two quoted definitions rather than as a sourced claim**)
- **Figure**: none. **Part 18.9 reasoning:** the section's content is a **two-cell distinction between two words**, and the right form for that is the table in the second beat — which is prose furniture, not a figure. Part 18.9's own test is explicit that a concept warrants illustration when it has spatial, temporal or flow structure, or when it distinguishes similar-sounding *alternatives* with mechanisms behind them. `frozen` versus `deprecated` has no mechanism; it is semantics. Illustrating it would produce a decorative graphic, which Part 18.4 bans outright
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — **frozen ≠ deprecated.** Ingress is GA, covered by stability guarantees, with **no plans for removal** — **and** no longer developed, with no further changes or updates. Both halves, or you have the wrong fact
  - `> ⚠ **Navigational Hazards:**` — trap #44. A question that offers "Ingress is deprecated and will be removed" is testing exactly one thing: whether you kept both halves. So is a question that offers "Ingress is unaffected and fully supported for new development." Neither is the answer
  - `> 🪢 **Mnemonic:**` — *frozen things keep. They just don't grow.*
- **Cross-bearings**: back to **§2** and **§3** (the API just taught is the API now being characterised — say so, because a reader who was not told may wonder why they learned it); back to Ch 8 §6 (one clause — semantic versioning and API stability, which is the vocabulary this section spends); forward to **§5** (**mandatory** — "recommends Gateway instead" is §5's entire brief)
- ⚠ **Do not editorialise about the project's decision.** No opinion about whether the freeze was right, no speculation about timelines, no commentary on migration burden. Part 14 guardrails #3 and #4: the source says what it says, the book reports it precisely, and the reader draws their own conclusion
- ⚠ **Do not state or imply a removal date.** There is none, and inventing one would be exactly the fabrication guardrail #1 forbids

### §5 — 🟡 Roles, Not Just Routes

**Blocking gap G25 is CLOSED** — `k8s-docs-gateway-api-2026-08-23.md` supplies substantially more than B1 anticipated. §5 is fully sourceable and can be taught properly rather than named in passing.

**First, what Gateway API is, and lead with the design idea rather than the resource list.** Gateway API is a family of API kinds providing **dynamic infrastructure provisioning and advanced traffic routing**, made available through an **extensible, role-oriented, protocol-aware** configuration mechanism. The temptation is to open with GatewayClass/Gateway/HTTPRoute, and it should be resisted: the resource split is a *consequence* of the role split, and taught in that order it is three things to memorise instead of one idea with three parts.

**Second, the roles, which are the section's title and its point.** Gateway API models three organisational roles:

- **Infrastructure Provider** — manages infrastructure that lets multiple isolated clusters serve multiple tenants.
- **Cluster Operator** — manages clusters; typically concerned with policies, network access, and application permissions.
- **Application Developer** — manages an application running in a cluster; typically concerned with application-level configuration and Service composition.

**⚠ Per the B7 ledger's Canonical forms, `cluster operator` here is a *role name*, not a person, and §5 must say so.** The book has otherwise reserved "operator" for the operator pattern of Ch 6 §8. One clause disposing of the collision, in the same spirit as §6's `ingress` clause.

**Third, the resource model, now motivated.** **GatewayClass** defines a set of gateways with common configuration, managed by a controller that implements the class. **Gateway** defines an instance of traffic-handling infrastructure — such as a cloud load balancer — and describes how traffic can be translated to Services within the cluster. **HTTPRoute** specifies HTTP-specific rules mapping traffic from a Gateway listener to backend endpoints, and attaches to a Gateway via **`parentRefs`**. The cardinality is examinable and should be stated as such: a Gateway is associated with **exactly one** GatewayClass; **many** Routes may attach to one Gateway.

**Fourth, map the resources onto the roles explicitly**, because that mapping is the whole reason the API is shaped this way and it is the thing a reader will actually be asked. The infrastructure provider supplies the GatewayClass; the cluster operator creates the Gateway; the application developer writes the HTTPRoute. One line, and the figure carries it.

**Fifth, the request flow, which is worth walking because it is concrete and the source gives it end to end.** The client's DNS resolver learns the IP address associated with the Gateway; the client sends the request to that address; the reverse proxy receives the HTTP request and uses the **`Host` header** to match a configuration derived from the Gateway and its attached HTTPRoute; it optionally performs header or path matching per the HTTPRoute's match rules; optionally modifies the request per the HTTPRoute's filter rules; and forwards it to one or more backends. **Note for drafting: the `Host`-header step is Soundings question 1's answer arriving seven sections later**, and it is worth one clause of acknowledgement — the reader guessed this at the start of the chapter.

**Sixth, the other three design principles, briefly.** **Portable** — Gateway specifications are defined as **custom resources** and supported by many implementations. **Expressive** — supports header-based matching, traffic weighting and other cases *"that were only possible in Ingress by using custom annotations"*, which is the concrete answer to what §4's freeze costs you. **Extensible** — custom resources can be linked at various layers of the API.

**Seventh — and this is optional, see § Open questions #6 — the third instance of the pattern.** The source calls Gateway *"an add-on containing API kinds"* and says the specifications are defined as **custom resources**. Both facts point the same way: Gateway API is not in a default cluster; something installs it. That is the pattern again, in a third object, in the same section arc. It strengthens §8 considerably. It also risks turning §5 into a reprise of §3. **Author's call.**

- **Objectives**: D2.1
- **Concepts introduced**: `gateway-api`, `gatewayclass`, `gateway`, `httproute`, `parentrefs`, `role-oriented-design`, `infrastructure-provider-role`, `cluster-operator-role`, `application-developer-role`, `gateway-request-flow`
- **Sources**: `k8s-docs-gateway-api-2026-08-23.md` (the whole snapshot — the opening definition, all four design principles with the three role descriptions verbatim, the resource model with GatewayClass/Gateway/HTTPRoute and the exactly-one/many cardinality, and the six-step request flow). `k8s-docs-custom-resources-2026-08-23.md` (retrieval only — custom resources and CRDs, taught at Ch 6 §8)
- **Figure**: `ch10-fig03-gateway-api-role-split`
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2**
- **Markers planned**:
  - `★ **Fixed Point:**` — **GatewayClass, Gateway, HTTPRoute** — and the three roles they belong to. A Gateway has **exactly one** GatewayClass; **many** Routes may attach to one Gateway
  - `> ⚓ **Worth Securing:**` — the role split is the actual innovation. Ingress put infrastructure choice, cluster policy and application routing in one object that one team had to own, which is why so much real-world Ingress configuration lives in vendor-specific annotations. Gateway API gives each concern its own resource so each role can hold its own
  - `> 🔭 **Closer Look:**` — the Gateway resources are custom resources, which means the API that supersedes Ingress is not built into the API server the way Ingress is. Deeper than the exam requires, and a neat illustration of Chapter 6's point that the extension mechanism is powerful enough to build first-class-looking APIs on
- **Cross-bearings**: back to **§4** (**mandatory** — "recommends Gateway instead" is why this section exists); back to **§2** (**mandatory** — HTTPRoute expresses the same fanout and virtual-hosting shapes, and the reader should see the correspondence rather than learn two unrelated route models); back to Ch 6 §8 (**mandatory** — custom resources, and the operator-pattern controller that would implement a GatewayClass); back to Ch 9 §6 (one clause — the client's resolver, which is now a step in a flow rather than a topic); forward to Ch 17 §4 (one clause — CRDs as one of the four pluggable interfaces, of which this is a conspicuous instance)
- ⚠ **Do not teach GRPCRoute, TCPRoute, TLSRoute, ReferenceGrant, or the GAMMA initiative.** Uncached and above associate tier. HTTPRoute is the one the source names and the one the reader needs
- ⚠ **Do not present Gateway API as a migration guide.** No before/after manifests, no conversion tooling, no "here is your Ingress rewritten". The exam tests what it is and what shape it has
- ⚠ **Do not teach mTLS or mesh integration here.** Ch 17 §5 owns both

### §6 — 🔵 Allowing, Never Denying

**Section-pinned by `chapter-09` lines 407 and 1706 — the only section in this chapter with two pins — and it is the sole definition home for NetworkPolicy in the entire book.** Ch 12 §9 refers here and never redefines. It also pays `chapter-02` line 871 and `chapter-04` line 835.

**First, dispose of the word collision, before anything else.** One sentence: the word `ingress` is about to mean *a direction of traffic* rather than *the API object of the last four sections*, and capitalisation is the tell. See the Chapter-type note — this is not optional politeness, it is the difference between a reader who learns NetworkPolicy and one who spends §7 trying to work out how it relates to the Ingress controller.

**Second, the scope, which is also `chapter-02` line 871's debt.** NetworkPolicies control **traffic flow at the IP address or port level — OSI layer 3 or 4.** They are an **application-centric construct**: they specify how a *Pod* is allowed to communicate with various network entities. They apply to a connection with a Pod on **one or both ends**, and are **not relevant to other connections.** Note what this rules out, once, and cross-bear it: this is network reachability, not the boundary between a workload and its host. Chapter 2 already told the reader those were different axes, on a graded question.

**Third, the three identifiers, and this is where `chapter-04` line 835 pays.** A Pod's permitted counterparts are identified through a combination of three things: **other Pods** that are allowed, **namespaces** that are allowed, and **IP blocks** (CIDR ranges). For Pod- and namespace-based policies you use a **selector** to specify what traffic is allowed to and from the Pods that match the selector; for IP-based policies you define the rule on CIDR ranges. **Frame this exactly as Chapter 4 framed it** — the object contains a selector choosing its *subject* and selectors choosing its *peers*, two jobs for one mechanism, which is cross-cutting theme #5 arriving in its most structurally interesting instance. Gloss CIDR in one clause per the B7 ledger; the glossary owns the expansion.

**Fourth, the two sorts of isolation — the section's centre and the answer to Soundings question 4.** There are two: isolation for **egress**, and isolation for **ingress**, and they are independent.

- **By default, a Pod is non-isolated for egress**: all outbound connections are allowed. It becomes isolated for egress if **any** NetworkPolicy both **selects the Pod** and has `Egress` in its `policyTypes`. Once isolated, the only allowed outbound connections are those permitted by the egress list of some policy that applies to it.
- **By default, a Pod is non-isolated for ingress**: all inbound connections are allowed. It becomes isolated for ingress on the same terms with `Ingress` in `policyTypes`. Once isolated, the only allowed inbound connections are those from **the Pod's node** and those permitted by some applicable policy's ingress list.

**This is the inversion Soundings question 4 set up, and drafting should collect the debt explicitly.** The reader's firewall instinct says default-deny; Kubernetes is default-*allow*, and a Pod is only ever restricted because a policy went looking for it. Say so.

**Fifth, additivity — and state it as a semantic, not as a quirk, because Ch 12 §9 has to retrieve it.** The effects of ingress lists **combine additively**. **Network policies do not conflict; they are additive.** There is **no deny rule**. Two policies selecting the same Pod produce the union of what they permit, and there is no syntax by which one could subtract from the other. Removing access means removing the grant, not adding a denial. **Trap #49.**

**Sixth, both ends.** For a connection from a source Pod to a destination Pod to be allowed, **both** the egress policy on the source **and** the ingress policy on the destination need to allow it. **Trap #50**, and it is the one that costs practitioners the most time, because a policy that looks correct in isolation is only half of a working configuration.

**Seventh, default-deny by selection — the constructive consequence, at whatever depth § Open questions #7 resolves.** The reader will immediately ask how you get default-deny if there is no deny rule, and the answer follows from the fourth and fifth beats: select the Pods, name the direction, and permit nothing. Isolation without permission is denial. **The canonical mechanism for "select every Pod in the namespace" is an empty `podSelector`, which is not in the cached snapshot** — see the gap note

**Eighth, the two exceptions, stated here and expanded in §7.** A Pod **cannot block access to itself**. And traffic **to and from the node where a Pod is running is always allowed**, regardless of the Pod's or the node's IP address. **Trap #51.**

- **Objectives**: D2.1, D2.2
- **Concepts introduced**: `networkpolicy`, `l3-l4-control`, `application-centric-policy`, `pod-selector`, `namespace-selector`, `ipblock`, `cidr-range`, `policy-types`, `ingress-isolation`, `egress-isolation`, `non-isolated-default`, `additive-policy-semantics`, `no-deny-rule`, `both-ends-must-allow`, `default-deny-by-selection`, `node-local-traffic-always-allowed`, `self-traffic-unblockable`
- **Commands**: `kubectl-get-networkpolicy`
- **Sources**: `k8s-docs-network-policies-2026-08-23.md` (the whole snapshot except the Prerequisites and out-of-scope blocks, which are §7's — the L3/L4 scope, the application-centric framing, the one-or-both-ends rule, the three identifiers with both exceptions, the selector-versus-CIDR split, the two sorts of isolation with both defaults and both `policyTypes` conditions, the node-traffic allowance inside the ingress rule, additive combination, "Network policies do not conflict; they are additive", and the both-ends requirement). `k8s-docs-labels-selectors-2026-08-23.md` (retrieval only — selectors, taught at Ch 4 §5). `k8s-docs-namespaces-2026-08-23.md` (retrieval only — Ch 4 §3)
- ⚠ **SOURCE GAP — non-blocking, affects the seventh beat only. See § Open questions #7.** The cached snapshot does not state that an **empty `podSelector` selects all Pods in the namespace**, nor does it give the canonical default-deny manifest, nor `ipBlock`'s `except` field. The seventh beat can be written as a *derivation* from the fourth and fifth beats without asserting either — and doing so is arguably better pedagogy — but it cannot name the empty-selector idiom without a source
- **Figure**: `ch10-fig04-networkpolicy-additive-selectors`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — **by default a Pod is non-isolated in both directions.** It becomes isolated for a direction only when some policy selects it *and* names that direction. No policy means no restriction
  - `★ **Fixed Point:**` — **policies are additive and never conflict. There is no deny rule.** Two policies produce the union of what they permit
  - `★ **Fixed Point:**` — **both ends must allow it.** Source's egress *and* destination's ingress
  - `> ⚠ **Navigational Hazards:**` — traps #48 and #49 together. If your firewall instinct says "unlisted traffic is dropped" and "the deny wins", both instincts are wrong here, and they are wrong in the direction that makes a cluster *more* open than you expect rather than less
  - `> 🪝 **Snag:**` — trap #51. A Pod cannot block access to itself, and traffic to and from its own node is always allowed. Two exceptions, both unconditional, and both regularly rediscovered by someone testing a policy from the wrong place
  - `> 🪢 **Mnemonic:**` — *nothing is closed until something selects it; nothing selected can be re-opened by another rule; and both ends have to agree.*
- **Cross-bearings**: back to Ch 9 §1 (**mandatory — the pinned payoff, twice over**; rule 2's *"barring intentional network segmentation"* hedge, which Chapter 9 pointed here by number in two places); back to Ch 4 §5 (**mandatory** — labels and selectors, and specifically Chapter 4's own observation that a NetworkPolicy selects both its subject and its peers); back to Ch 4 §3 (namespaces as the second identifier); back to Ch 2 §7 (**mandatory** — network segmentation versus workload-to-host isolation, the discriminator on a Chapter 2 graded question); back to Ch 5 §1 (the Pod IP, which is what a policy is ultimately about); forward to **§7** (**mandatory** — the two things this cannot do); forward to Ch 12 §9 (**mandatory** — RBAC and NetworkPolicy as one shared additive semantic; this chapter supplies half of that argument and must not make it); forward to Ch 12 §5 (one clause — the other axis of Pod security)
- ⚠ **Do not make Ch 12 §9's argument.** The RBAC parallel is genuinely striking and it will be tempting to draw it here. **One forward cross-bearing, no content.** Ch 12 §9 is the Security chapter's Zenith and its entire payoff is the reader recognising a semantic they already hold. Spending it here damages a later chapter to decorate this one
- ⚠ **Do not teach RBAC, `securityContext`, Pod Security Standards, or the 4Cs.** All Ch 12
- ⚠ **Do not write a full NetworkPolicy manifest** unless § Open questions #7 resolves in favour of fetching field-level source. The semantics above are fully teachable without one, and an invented manifest is worse than none

### §7 — 🟡 What NetworkPolicy Cannot Do

**The chapter's second instance of the pattern, and its most consequential fact.** §3's Ingress-without-a-controller fails *loudly* — the traffic does not arrive and someone notices within minutes. This one fails *silently*, and that asymmetry is what §7 exists to make unforgettable.

**First, the prerequisite, stated as flatly as §3's was.** *Network policies are implemented by the network plugin.* To use them you must be using a networking solution that supports NetworkPolicy. **Creating a NetworkPolicy resource without a controller that implements it will have no effect.** Same sentence shape as §3's; the echo is deliberate and the reader should hear it.

**Second, the asymmetry, which is the section's whole reason for existing.** When an Ingress does nothing, requests fail and you find out. When a NetworkPolicy does nothing, **traffic flows exactly as it did before**, which is indistinguishable from a policy working on traffic that was always going to be allowed. `kubectl get networkpolicy` shows the object. `kubectl describe` shows the rules. Everything looks correct, and nothing is enforced. **Trap #47**, and it is the highest-consequence single fact in this chapter.

**⚠ Part 14 subject dignity applies with unusual force here.** The consequence of this failure is unauthorised access to real systems holding real people's data. The wry register stays on the practitioner's entirely reasonable belief — you wrote it, the API accepted it, the object is right there — and **never** on a breach, a victim, or anyone's incident. No war stories. State the mechanism and the consequence and stop.

**Third, the retrieval, and it should be posed as a question the reader can answer.** Chapter 9 §1 taught that Kubernetes defines the network model and implements none of it — a CNI plugin does. So: if the plugin implements the network, where else *could* policy enforcement possibly live? The dependency is not an inconvenience or an oversight; it is the only place the machinery exists. A reader who reasoned to this in Soundings question 7 should be told they did.

**Fourth, the out-of-scope list — and this is the chapter's required `Dead Reckoning` block.** State it flat, complete, and with no register at all, exactly as the source gives it. As of the current release you cannot use NetworkPolicy for: forcing internal cluster traffic through a common gateway; anything TLS-related; node-specific policies; targeting of Services by name; creation or management of policy requests fulfilled by a third party; default policies applied to all namespaces or Pods; advanced policy querying and reachability tooling; logging of network security events; explicitly denying policies; or preventing loopback or incoming host traffic. **Trap #52**, and the list is the answer to it.

**Fifth, pull three items out of the list for one sentence each**, because they are the ones a reader will actually reach for and being told *no* precisely is more useful than being told *no* generally: **no TLS** (which is Chapter 17's mesh, and the forward pointer belongs here), **no targeting Services by name** (policies select Pods, not Services — which is a genuinely surprising consequence of everything §6 taught and worth naming), and **no explicit deny** (§6's additivity, restated as a *limitation* rather than a property, which is the same fact from the side the reader will meet it on).

**Close by handing to §8.** Two objects in this chapter, four sections apart, sharing nothing except a failure mode. That is the observation §8 turns into a rule.

- **Objectives**: D2.1, D2.2
- **Concepts introduced**: `policy-plugin-dependency`, `silently-inert-policy`, `networkpolicy-out-of-scope`
- **Sources**: `k8s-docs-network-policies-2026-08-23.md` (Prerequisites — "Network policies are implemented by the network plugin. To use network policies, you must be using a networking solution which supports NetworkPolicy. Creating a NetworkPolicy resource without a controller that implements it will have no effect"; and the complete out-of-scope list, all ten items, verbatim). `k8s-docs-extending-kubernetes-2026-08-23.md` (retrieval only — CNI as the interface, taught at Ch 9 §1)
- ⚠ **SOURCE NOTE — the "silent" characterisation is the author's, not the source's.** The source states the plugin dependency and the no-effect consequence. It does not use the word *silent* or characterise the failure as harder to detect than other failures. That inference is sound and it is the section's most valuable content, but it is the book's reasoning rather than a documented claim. **Present it as reasoning, in the book's established idiom for author observations** — Chapter 3 line 597 is the model: *hold the two apart*
- **Figure**: none. **Part 18.9 reasoning:** the section is a **list of absences** plus one asymmetry. Absences do not illustrate — a diagram of what a mechanism cannot do is either an empty frame or a set of crossed-out boxes, and the latter is precisely the decorative-negative-space anti-pattern. The asymmetry between loud and silent failure *is* visual, and it is drawn once, at scale, in `ch10-zenith`, where it can be shown across all four instances rather than one. The out-of-scope list is a `Dead Reckoning` block; flat text is the correct form for it and Part 18.7 forbids restating it in a caption
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `★ **Fixed Point:**` — **NetworkPolicies are implemented by the network plugin.** On a plugin that does not support them, the resource has no effect — and unlike a broken Ingress, nothing about the cluster's behaviour tells you
  - `> ⚠ **Navigational Hazards:**` — trap #47. "I applied a NetworkPolicy, so that traffic is blocked" is only true if something is enforcing it. Verify the plugin supports NetworkPolicy before you rely on one, and test the restriction from the outside rather than trusting the object's existence
  - `> — **Dead Reckoning:**` — **the required Dead Reckoning block for this chapter.** The ten out-of-scope items, stated flat, complete, no metaphor, no maritime register, in the source's own order
  - `> 🔭 **Closer Look:**` — "no targeting of Services by name" is stranger than it looks and follows directly from §6. A policy selects Pods, and a Service is a name in front of a set of Pods that changes. Selecting the Service would mean selecting a moving target through an indirection the policy layer does not have. Deeper than the exam requires
- **Cross-bearings**: back to **§6** (**mandatory** — the semantics this section bounds); back to Ch 9 §1 (**mandatory** — CNI, and the reason the dependency exists where it does); back to **§3** (**mandatory** — the same failure, and the reader should be told to compare them); forward to **§8** (**mandatory**); forward to Ch 17 §5 (**mandatory** — "anything TLS related" is out of scope here and is a substantial part of what a mesh supplies); forward to Ch 12 §9 (one clause only — see §6's warning)
- ⚠ **Do not turn this into a troubleshooting workflow.** No decision tree for "is my policy working", no verification recipe, no `kubectl exec` connectivity testing. Ch 13 owns platform-scope troubleshooting and Ch 16 owns application-scope. This section owns two *facts*
- ⚠ **Do not name specific CNI plugins as supporting or not supporting NetworkPolicy.** That is version-dependent, changes, and the cached set does not carry it. The reader needs to know the dependency exists and that they must check — not a table that will be wrong in a year

### §8 — ☀️ Nothing Happens Without a Controller

**The chapter's one Zenith, and — per B6 and the arc outline — the named home of cross-cutting theme #3. ⚑ That designation needs the § Open questions #4 decision applied before this section is drafted.**

**The observation, which is the whole section.** This chapter taught two objects that have nothing to do with each other. One routes HTTP by hostname and path at the edge of the cluster. The other permits and forbids TCP connections between Pods inside it. Different layers, different directions, different problems, different teams. **And they fail the same way.** Write either one perfectly, apply it successfully, watch `kubectl get` return it — and nothing happens, because in one case no Ingress controller is installed and in the other the network plugin does not implement NetworkPolicy.

**Then the count, using the reader's own evidence.** They have now seen this four times, and two of the four were their own from last chapter: a LoadBalancer Service with no provider to fulfil it; a Service whose selector matched nothing; an Ingress with no controller; a NetworkPolicy on a plugin that does not implement one. Chapter 3 gave them the sentence and told them they would meet it four more times. This is where the debt is paid in full.

**Then the promotion, which is what makes this a Zenith rather than a summary.** The rule is not a fact about Ingress or a fact about NetworkPolicy. It is a fact about **what a Kubernetes object is** — which the reader has held since Chapter 4 without necessarily seeing the consequence. An object is a record of intent. Intent does not act. Something has to be watching, and willing, and *present*. Every object in this book works this way; the four instances are simply the cases where the watcher happens to be missing.

**Then the forward use, stated as a tool rather than as a preview.** The reader now has a question they can ask about anything: *what is watching this, and is it installed?* Chapter 13 will use it on `kubectl top` returning an error on a cluster with no metrics-server. Chapter 17 will use it on VPA. Both pointers were published in Chapter 3 and both are now armed. And it works on objects this book never mentions, which is the actual return on the chapter.

**⚠ The Zenith's failure mode is smugness.** The pattern is genuinely elegant and the temptation is to present it as a clever thing the book noticed. It is not — it is a direct consequence of the declarative model, and the reader half-derived it themselves in Soundings question 6. The register should be *recognition*, in the sense skill Part 9 means: the satisfaction is the reader's, not the narrator's.

- **Objectives**: D2.1, D2.2
- **Concepts introduced**: none. Synthesis only — §8 introduces no new vocabulary and must not
- **Sources**: none new. Every claim in this section is retrieval from §3, §7, Ch 3 §4, Ch 3 §6, Ch 4 §1, Ch 9 §3 and Ch 9 §4
- **Figure**: `ch10-zenith-nothing-without-a-controller`
- **Checkpoint after**: no
- **Markers planned**:
  - `☀️ **Zenith:**` — the chapter's single Zenith block, and per the Chapter-type note it sits **inside** §8 in addition to the heading glyph. Content: two objects with nothing in common, one failure mode, and the reason — an object is a record of intent, and intent does not act
  - `> ⚓ **Worth Securing:**` — the question, stated as a question the reader now owns: *what is watching this, and is it installed?* Give it to them as a tool, and name the two places they are about to use it
  - `🏆 Safe Harbor` — chapter completion, at the close
- **Cross-bearings**: back to **§3** and **§7** (**mandatory** — the two instances); back to Ch 3 §4 (**mandatory** — the rule, and the promise that it would recur four times); back to Ch 3 §6 and Ch 4 §1 (**mandatory** — the control loop and the declarative model, which are *why* the rule is true rather than merely *that* it is); back to Ch 9 §3 and Ch 9 §4 (**mandatory** — the reader's own two earlier sightings); forward to Ch 13 §7 (**mandatory**) and Ch 17 §7 (**mandatory**)
- ⚠ **Do not introduce NetworkPolicy or Ingress content here.** If a fact only appears in §8, it is in the wrong section
- ⚠ **Do not extend the pattern to examples the book has not taught.** Four instances, all of them the reader's own. Inventing a fifth from outside the book weakens the argument by making it look like a general observation rather than a rule the reader has personally accumulated evidence for

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 15 questions total.** B4 allocates 10 and states plainly that the figure is a minimum to exceed; Chapters 3 through 9 all shipped 15 across three checkpoints of 5. Chapter total moves 35 → 40.

- **#1 after §3** covers the ceiling, the object, and the component (§1–§3): what Ingress does, what it refuses to do, and why it may do nothing at all.
- **#2 after §5** covers the API generations (§4–§5): the precise state of the frozen API, and the shape of the one that replaces it.
- **#3 after §7** covers policy (§6–§7): what a NetworkPolicy permits, how permissions combine, and the two things the mechanism cannot reach.

**On the shape.** #2 covers only two sections and is the smallest block in the chapter. It is still correct: §4 is the chapter's most precisely examinable fact and §5 is its largest body of new vocabulary, and folding them into #1 would produce a six-section checkpoint spanning the entire API arc — which is exactly the density the Attention Budget session split exists to prevent. Folding them into #3 would put the Gateway API resource model next to NetworkPolicy semantics, which share nothing and would interleave badly for the wrong reason.

**Retrieval-practice content: 20%** **[B3]** — drawn from **Chapters 6 through 9**, with the **≥4-back spacing floor** satisfied twice over, by **Chapter 4** (labels and selectors, six back) and **Chapter 3** (the absent-component rule, seven back). Against a combined Bearings-plus-Practice pool of 32, the target is ~6–7 items, allocated **3 in Bearings and 4 in Practice** (7 of 32 = 21.9%), matching the allocation shape Chapters 7 through 9 used.

Each of the arc outline's named anchors has one place it belongs:

| Named anchor | Placement | Why here |
|---|---|---|
| **The Service-type ladder against what Ingress replaces (Ch 9 §3)** | Bearings #1, item 1 | §2's most-missed fact is that Ingress does **not** replace the ladder — non-HTTP traffic goes back down to it. Testing the ladder and the replacement in one item is the cheapest defence against trap #43 |
| **Selectors now selecting NetworkPolicy subjects (Ch 4 §5)** | Bearings #3, item 1 | **[≥4-BACK FLOOR ITEM — six chapters]**. §6 *is* the selector in its third role, and Chapter 4 line 835 published the pointer. The retrieval and the teaching are the same beat |
| **The absent-component rule (Ch 3 §4)** | Bearings #1, item 5 | **[≥4-BACK REDUNDANCY — seven chapters]**. Chapter 8's outline established the practice of carrying a second ≥4-back item so the floor does not rest on one question, and Chapter 9 followed it. This chapter's spine makes the redundancy free |

**On the floor.** Unusually, this chapter satisfies the ≥4-back requirement with margin rather than at the minimum — Chapter 4 is six back and Chapter 3 is seven. Both are load-bearing content rather than manufactured distance, which is the ideal case the floor was designed to produce.

### ☆ Taking Your Bearings #1 — after §3

- **Topic**: above the ceiling — the object, its remit, and the component that has to exist
- **Questions**: 5
- **Retrieval from earlier chapters**: 2 of 5 (one named anchor, one ≥4-back redundancy item)
- **Difficulty**: ⚪ for items 1–2, 🔵 for 3–5

  1. **Retrieval from Ch 9 §3.** You need to expose a PostgreSQL database and a web application to clients outside the cluster. Which one can an Ingress handle, and what do you use for the other? **Correct answers: the web application, over HTTP/HTTPS; the database needs `Service.Type=NodePort` or `Service.Type=LoadBalancer`, because Ingress exposes no arbitrary ports or protocols.** Named anchor. **Directly tests B1 trap #43**, and it is framed so that the reader must hold both layers rather than choosing between them.
  2. One IP address serves `shop.example.com` and `blog.example.com`, routing each to a different Service. Name the Ingress capability. Then: one host, `/catalog` and `/checkout` to different Services. Name that one. **Correct answers: name-based virtual hosting; simple fanout.** The chapter's cleanest pair of definitions, and deliberately asked as a pair so the discriminator — host versus path — is what the reader retrieves.
  3. 🔵 A colleague applies a correct Ingress manifest to a fresh cluster. `kubectl get ingress` shows it. No traffic reaches the application. Name the most likely cause and say what `kubectl get` proves about it. **Correct answer: no Ingress controller is installed; `kubectl get` proves only that the object exists, which is a fact about etcd rather than about routing.** **The section's Fixed Point, tested as a diagnosis rather than a definition.**
  4. 🔵 The same Ingress manifest is applied to two clusters, each running a different Ingress controller. Should you expect identical behaviour? Justify. **Correct answer: no — ideally all controllers fit the reference specification, but in reality they operate slightly differently.** **Tests B1 trap #45**, which is the trap in this section most likely to be skimmed past because it sounds like a caveat rather than a fact.
  5. 🔵 **Retrieval from Ch 3 §4. [≥4-BACK REDUNDANCY ITEM]** Chapter 3 gave you a one-sentence rule about objects and components. State it, then name the two things from Chapter 9 that were instances of it. **Correct answers: an object without its component does nothing; a `type: LoadBalancer` Service on a cluster with no load balancer to provision one, and a Service whose selector matches no Pods.** **Seven chapters back.** This item satisfies **[B3]**'s spacing floor redundantly and it arms §8 — a reader who can list the instances at §3 will find §8's count persuasive rather than assertive.

- **Answer-key requirement**: item 1's key must state the relationship as *specialisation, not replacement* — Ingress sits above the ladder for one class of traffic and the ladder is still the answer for everything else. That framing is what makes §4's freeze survivable as a fact and what keeps trap #43 defused rather than merely answered.
- **Answer-key requirement**: item 3's key must not treat the colleague as careless. The manifest was correct; the expectation was reasonable; the missing piece is invisible from the object. Part 14 — the wry register stays on the situation, not on the person in it.

### ☆ Taking Your Bearings #2 — after §5

- **Topic**: one API frozen, one API recommended, and the difference that word makes
- **Questions**: 5
- **Retrieval from earlier chapters**: 0. The chapter's 20% is met by Bearings #1 items 1 and 5, Bearings #3 item 1, and four Practice items. A retrieval item here would push a two-section checkpoint off its own topic, and this topic is the chapter's most precisely examinable material
- **Difficulty**: ⚪ for items 1–2, 🟡 for 3–5

  1. State both halves of what the Kubernetes project has said about the Ingress API. **Correct answer: it is frozen — generally available, subject to GA stability guarantees, with no plans for removal — and it is no longer developed, with no further changes or updates.** **Tests B1 trap #44 directly**, and the key must reject an answer carrying only one half, because one half is precisely the error.
  2. True or false, with justification: *Ingress is deprecated and will be removed in a future release.* **Correct answer: false on both counts — it has not been deprecated and there are no plans to remove it. What has been said is that it will not be developed further and that the project recommends Gateway for new work.**
  3. 🟡 Name the three Gateway API resources and say which organisational role each belongs to. **Correct answers: GatewayClass — infrastructure provider; Gateway — cluster operator; HTTPRoute — application developer.** The section's core recall item, and it is asked as a mapping rather than a list because the mapping is the design.
  4. 🟡 How many GatewayClasses is a Gateway associated with, and how many Routes can attach to one Gateway? **Correct answers: exactly one; many.** Pure recall, and the kind of cardinality detail multiple-choice exams reach for.
  5. 🟡 A request arrives at a Gateway's IP address. Name the header the reverse proxy uses to match a configuration, and name the two optional things the HTTPRoute may do before the request is forwarded. **Correct answers: the `Host` header; optional header and/or path matching per its match rules, and optional modification of the request per its filter rules.** **This item closes Soundings question 1** — the reader guessed `Host` at the start of the chapter from ordinary web experience, and here it is in the specification.

- **Answer-key requirement**: item 1's key must state *why* both halves matter in operational terms — the stability half means no migration emergency, the no-development half means no new capability ever. A key that just repeats the sentence has tested recall of a sentence rather than understanding of a position.
- **Answer-key requirement**: item 3's key must name `cluster operator` as a **role**, not a person or a job title, per the B7 ledger's Canonical forms entry. The book uses "operator" for the operator pattern everywhere else and this is the one place the word means something different.

### ☆ Taking Your Bearings #3 — after §7

- **Topic**: what is permitted, how permissions add up, and what the mechanism cannot reach
- **Questions**: 5
- **Retrieval from earlier chapters**: 1 of 5 (named anchor, and the ≥4-back floor item)
- **Difficulty**: 🔵 throughout, with items 3 and 4 at 🟡

  1. **Retrieval from Ch 4 §5. [≥4-BACK FLOOR ITEM]** Chapter 4 said a NetworkPolicy selects both its subject and its peers. Point at the two selectors in that sentence and say what each one is choosing. **Correct answer: the policy's own `podSelector` chooses which Pods the policy applies to; the selectors inside its rules choose which Pods and namespaces those Pods may talk to.** **Six chapters back.** Named anchor and floor item in one, and it is the structural insight §6 is built on.
  2. A Pod in namespace `prod` has no NetworkPolicy selecting it anywhere in the cluster. What inbound and outbound traffic is permitted? **Correct answer: all of both — a Pod is non-isolated for ingress and for egress by default.** **Tests B1 trap #48**, which is the single most consequential wrong instinct a reader can bring to this material.
  3. 🟡 Two NetworkPolicies select the same Pod. Policy A permits inbound traffic from `app: web`. Policy B permits inbound traffic from `app: batch`. What is permitted, and could a third policy be written to forbid `app: web`? **Correct answers: inbound from both `app: web` and `app: batch` — the lists combine additively; and no, there is no deny rule, so nothing can subtract a permission. Removing the access means removing the grant.** **Tests B1 trap #49**, and it is **the chapter's designated struggle item** — label it per Part 10B and normalise the difficulty, because a reader with firewall experience will look hard for the deny rule before accepting there isn't one.
  4. 🟡 Pod `frontend` has an egress policy permitting traffic to `app: api`. Pod `api` has an ingress policy permitting traffic only from `app: admin`. Can `frontend` reach `api`? **Correct answer: no — both the source's egress policy and the destination's ingress policy must allow the connection, and the destination's does not.** **Tests B1 trap #50**, and it is the chapter's best two-object reasoning item.
  5. You apply a NetworkPolicy intended to block traffic from a specific Pod. Traffic still flows. Name two distinct explanations, one of which is not a mistake in the policy. **Correct answers: the network plugin does not implement NetworkPolicy, so the resource has no effect at all; or the traffic falls under one of the unconditional exceptions — a Pod cannot block access to itself, and traffic to and from its own node is always allowed.** **Tests B1 traps #47 and #51 in one item**, and it deliberately requires the reader to consider that the object may be perfect and still inert.

- **Answer-key requirement**: item 3's key must state additivity as a **semantic** — the model has no subtraction operator — rather than as a NetworkPolicy behaviour. Ch 12 §9 retrieves this by name and the phrasing here is what it retrieves.
- **Answer-key requirement**: item 5's key must state the detection asymmetry explicitly and without moralising: a policy that is not enforced looks exactly like a policy that is enforced against traffic nobody is sending. Per Part 14, the key stays oriented at the practitioner's reasonable belief, and says nothing about consequences borne by anyone outside the room.

---

## 6. Exam Alert plan

**High-priority topics** — the twelve most likely to be tested directly, in descending order of confidence:

1. **Ingress exposes HTTP and HTTPS only.** No arbitrary ports, no other protocols; anything else uses NodePort or LoadBalancer.
2. **You must have an Ingress controller. Creating an Ingress resource alone has no effect.**
3. **Frozen, not deprecated** — GA, stability guarantees, no removal plans, **and** no further development. Both halves.
4. **The project recommends Gateway for new work.**
5. **Simple fanout routes by URI; name-based virtual hosting routes by host.** Both put many Services behind one address.
6. **An Ingress may terminate TLS**, using a Secret containing the private key and certificate.
7. **A Pod is non-isolated in both directions by default.** All ingress and all egress allowed.
8. **Policies are additive and never conflict. There is no deny rule.**
9. **Both ends must allow the connection** — source's egress and destination's ingress.
10. **NetworkPolicies are implemented by the network plugin.** No supporting plugin, no effect.
11. **GatewayClass / Gateway / HTTPRoute**, mapped to infrastructure provider / cluster operator / application developer.
12. **Node-local traffic is always allowed and a Pod cannot block access to itself.**

**Common traps to call out.** **Ten of B1's cataloged traps belong to this chapter — #42 through #45 and #47 through #52 — which is the largest single-chapter trap cluster in the book.** All ten are `[source]`-tagged, so all ten may be described as things candidates get wrong. **None is `[inferred]`, so no hedging is required** — and equally, none may be dressed with invented frequency figures (Part 14 guardrail #8, and **[B3]**'s fourth do-not-retrieve rule). Say "candidates get this wrong"; do not say "this appears on 15% of exams."

| B1 # | Trap | Where it is defused |
|---|---|---|
| 42 | "Creating an Ingress object exposes the app" | §3 Fixed Point, Bearings #1 item 3 |
| 43 | "Ingress can expose any protocol" | §2 Fixed Point, Bearings #1 item 1 |
| 44 | "Ingress is deprecated / being removed" | §4 Fixed Point and Navigational Hazards, Bearings #2 items 1 and 2 |
| 45 | "All Ingress controllers behave identically" | §3 Snag, Bearings #1 item 4 |
| 47 | "Creating a NetworkPolicy secures the cluster" | §7 Fixed Point and Navigational Hazards, Bearings #3 item 5 |
| 48 | "A Pod with no NetworkPolicy is closed by default" | §6 Fixed Point, Bearings #3 item 2 |
| 49 | "One NetworkPolicy can deny traffic another allows" | §6 Fixed Point, Bearings #3 item 3 |
| 50 | "Only one end needs to permit the connection" | §6 Fixed Point, Bearings #3 item 4 |
| 51 | "NetworkPolicy can block node-local or self traffic" | §6 Snag, Bearings #3 item 5 |
| 52 | "NetworkPolicy can do TLS / name targeting / logging / explicit deny" | §7 Dead Reckoning |

**Four non-B1 traps worth adding**, all visible now that the Ingress, Gateway API and NetworkPolicy snapshots have been read in full:

- **"Virtual hosting is just DNS."** It is not, and Chapter 9 §7 flagged the confusion by name and pointed here. DNS resolves a name to an address before traffic moves; virtual hosting sorts traffic that has already arrived at one address. §2 Navigational Hazards, Bearings #1 item 2.
- **"Gateway API is a rename of Ingress."** It is a different API with a different resource model built around a different organising principle — three roles, three resources. §5, Bearings #2 item 3.
- **"NetworkPolicy can target a Service."** It cannot; it selects Pods. This is on the published out-of-scope list and it is the item on that list a reader is most likely to reach for, because everything else in Part III has been Service-shaped. §7 Closer Look.
- **"An Ingress controller and a NetworkPolicy plugin are unrelated concerns."** They are unrelated *functionally* and identical *structurally*, which is the chapter's Zenith. §8.

**Do not include** in the Exam Alert: Service types, EndpointSlice, kube-proxy, cluster DNS, or the network model's four rules (all Ch 9 — this chapter refers and never re-teaches); RBAC's additive semantics or the RBAC/NetworkPolicy parallel (Ch 12 §3 and Ch 12 §9 — **spending the parallel here damages the Security chapter's Zenith**); `securityContext`, Pod Security Standards, or the 4Cs (Ch 12); service mesh, mTLS, ambient mode, or Envoy (Ch 17 §5); metrics-server and `kubectl top` (Ch 13 §7 — the pattern's third instance is *pointed at*, never taught here); Ingress troubleshooting as a workflow (Ch 13 and Ch 16); `pathType`, the default backend, and IngressClass **unless § Open questions #2 and #3 resolve in favour of fetching the field-level source**.

---

## 7. Practice Questions plan

**17 questions** (B4 allocation, unchanged). Distribution follows exam-point density and trap concentration rather than section count:

| Block | Questions | Notes |
|---|---|---|
| §1 — the ceiling and the layer boundary | 2 | Includes **1 retrieval item**. Both must be about the L4/L7 distinction rather than about Service types, which are Ch 9's to test |
| §2 — the Ingress object | 3 | Includes **1 retrieval item**. **Trap #43 must appear as a distractor at least once.** At least one item must require distinguishing fanout from virtual hosting by what the rule reads |
| §3 — the controller | 3 | Includes **1 retrieval item**. **Trap #42 must appear in two different question shapes** — it is the chapter's most mechanically testable fact. One item must have "nothing is wrong with the object" as its correct answer |
| §4 — frozen | 2 | Both must require **both halves**. A one-half answer must be a distractor in each, in its two different wrong forms |
| §5 — Gateway API | 2 | One on the role/resource mapping, one on cardinality or request flow. Neither should require memorising the four design principles as a list |
| §6 — NetworkPolicy semantics | 4 | Includes **1 retrieval item**. **Traps #48, #49 and #50 must each appear as a distractor at least once.** At least two must be *prediction* items — given these policies, is this connection allowed |
| §7 — the limits | 1 | Trap #47. One item, and it must be the silent-failure case rather than a recall check on the out-of-scope list |

**Retrieval allocation: 4 of the 17 draw from Chapters 3, 4, 6 and 9**, allocated *within* this count and not added to it:

- **The Service-type ladder** (Ch 9 §3) — §1 block. Framed as a discrimination item: *you need to expose an HTTP application and a message broker speaking its own binary protocol. How many Ingresses and how many Services of what types?* Correct answer: one Ingress for the HTTP application, and the broker goes to NodePort or LoadBalancer — Ingress cannot carry it. Tests whether the reader has understood specialisation rather than replacement.
- **The control loop** (Ch 3 §6) — §3 block. Framed forward rather than backward: *Chapter 3 said a controller watches for objects and drives reality toward what they describe. An Ingress controller is one. Name what it watches and name what it changes.* Correct answer: it watches Ingress objects (and the Services they reference) and configures a load balancer, edge router, or frontend to match. Converts a memorised component name into an instance of a pattern.
- **Labels and selectors** (Ch 4 §5) — §6 block. **[≥4-back, six chapters]**, carried as redundancy for the floor alongside Bearings #3 item 1. Framed as: *a single NetworkPolicy contains three selectors. One chooses the Pods the policy governs; two choose Pods and namespaces those Pods may talk to. Which is which, and what happens to the policy's effect if someone relabels a Pod that the first selector was matching?* Correct answer: the `podSelector` at the top governs; the selectors inside the rules choose peers; relabelling removes that Pod from the policy's subjects entirely, which — because policies are the only thing that isolates — makes it *less* restricted, not more.
- **The absent-component rule** (Ch 3 §4) — §7 block. **[≥4-back, seven chapters]**. Framed as: *name the rule Chapter 3 gave you, then list every instance of it you have met in this book so far.* Correct answers: an object without its component does nothing; a LoadBalancer Service with no provider, a Service whose selector matches nothing, an Ingress with no controller, and a NetworkPolicy on an unsupporting plugin. This item is the Zenith assessed rather than merely asserted, and it should be positioned last in the set.

**Interleaving strategy.** At least **four** questions must require two sections at once:

- **§2 + §4 (the object and its status)** — you are designing external routing for a new application today. Which API does the project recommend, and does that recommendation mean the other one will stop working? Two facts, opposite directions, one answer.
- **§2 + §5 (the two route models)** — express the same requirement — one host, two paths, two backends — in the Ingress vocabulary and then in the Gateway API vocabulary. Name the resources involved in each.
- **§6 + §7 (semantics against limits)** — a policy that looks correct, traffic that flows anyway, and three candidate explanations of which two are in this chapter and one is not.
- **§3 + §7 + §8 (the pattern, both ends)** — two objects, both correct, both inert. Name what is missing in each case, and name the one difference in how you would *find out*. The correct answer is the detection asymmetry, and it is the only question in the set that tests the Zenith's operational value rather than its elegance.

**Trap-answer requirement** (skill Part 11): every wrong option must target a specific misconception and the answer key must explain why each is wrong. For the §4 block, the two wrong options must be the **two different one-half answers** — "deprecated and being removed" and "unaffected, use it freely for new work" — because those are the two real failure modes and offering only one of them teaches the other. For the §6 block, trap #48's wrong form ("no policy means no traffic") must appear at least once, and trap #49's ("the more restrictive policy wins") at least once; the latter is the specific shape a firewall-experienced reader's error takes, and it is more useful as a distractor than a generically wrong option.

**One calibration note.** This chapter's failure mode as a question set is *definition inflation* — seventeen items asking "what does Ingress do", "what does frozen mean", "what is an HTTPRoute". The material genuinely contains two blocks of near-pure definition (§2's capabilities, §5's resource model) and those deserve about five of the seventeen. The remaining twelve should test **prediction** (given these two policies, is this connection allowed) and **diagnosis** (the object is correct and nothing happens — why, and how would you know). §6 in particular rewards prediction items far more than recall items: the four rules of isolation, additivity, both-ends and the two exceptions compose into scenarios that are genuinely worth reasoning through, and a reader who can answer three of those can answer any recall question about them.

---

## 8. Required figures

Five anchors, exactly as the arc outline specifies. §3, §4 and §7 deliberately carry none — see each section's Figure line for the Part 18.3/18.7/18.9 reasoning. **This is the highest count of deliberately-unillustrated sections in any chapter so far, and it is correct**: three of this chapter's eight sections have negation, semantics, or a list of absences as their content, and Part 18.9's decision framework excludes all three.

**A note on this chapter's figure register.** Four of the five are structural, and two of them — `fig01` and `fig04` — carry an argument that the prose can state but not *show*. `ch10-fig02` is the chapter's Lodestar candidate. The Zenith carries the brand's illustrative register; the other four do not, and should not be dressed up.

### `ch10-fig01-ingress-vs-service-loadbalancer`

- **Purpose**: §1's Fixed Point, dual-coded. The layer boundary, drawn as a difference in what each mechanism can see.
- **Content**: two arrangements side by side, same problem in both. **Left:** three Services, each with its own `type: LoadBalancer`, each with its own external address, three separate arrows entering the cluster from outside. **Right:** one external address, one box at the boundary, three arrows fanning out from it to the same three Services. The boundary box is annotated with what it reads — `Host`, path — and the left arrangement is annotated with what it reads: nothing.
- **Design requirement — the asymmetry must be in the *annotations*, not in the arrow count.** The obvious version of this figure says "three addresses versus one", which is the cheap half of the argument. The expensive half is that the right-hand box **reads the request** and the left-hand arrows do not, and that has to be visible or the figure has only made the cost argument.
- **Design requirement — do not draw the Ingress controller.** §3's whole point is that the reader does not yet know anything is there. The boundary box is unlabelled infrastructure at this stage; the Zenith figure is where the missing component becomes visible.
- **Label count**: three Service names, two address annotations, one "reads Host and path", one "reads nothing" — seven. At the Part 18.12 ceiling; do not add.

### `ch10-fig02-ingress-fanout-and-name-based-hosts`

- **Purpose**: §2's Fixed Point — the two routing shapes, and specifically the discriminator between them.
- **Content**: two panels stacked, sharing a single external address drawn identically in both. **Top panel, simple fanout:** one host `shop.example.com`, two paths `/catalog` and `/checkout`, arrows to two Services. **Bottom panel, name-based virtual hosting:** two hosts `shop.example.com` and `blog.example.com`, no paths shown at all, arrows to two Services. In each panel, the part of the request the rule matched on is **visually emphasised in the request line itself** — the path segment in the top, the hostname in the bottom.
- **Design requirement — the shared address must be drawn identically in both panels, in the same position.** That identity is the whole point: both shapes put many Services behind one IP, and they differ only in what the rule reads. If the two panels differ in layout, the figure teaches "two unrelated features" instead of "one mechanism, two match fields".
- **Design requirement — show the request line, not just the boxes.** The reader needs to see `GET /catalog HTTP/1.1` with `Host: shop.example.com` and see which part got matched. This is also the cheapest possible defence against the DNS-versus-virtual-hosting confusion Chapter 9 flagged: the request has already arrived, and the figure shows it arriving.
- **Lodestar candidate.** This is the chapter's single highest-value reference artefact and the one a reader will want on the morning of the exam.
- **Label count**: one address, two hostnames, two paths, four Service names — nine, but the Service names read as endpoints of arrows rather than as independent labels. **Design so the Service names read as arrow terminations**, or drop to two Services per panel sharing names across panels.

### `ch10-fig03-gateway-api-role-split`

- **Purpose**: §5's Fixed Point — the three resources *as* the three roles, which is the thing the resource list alone cannot show.
- **Content**: three horizontal bands, stacked, each band belonging to one role. **Top band, Infrastructure Provider:** GatewayClass. **Middle band, Cluster Operator:** Gateway, with a `1` annotation on the link up to GatewayClass. **Bottom band, Application Developer:** two or three HTTPRoutes, with a `many` annotation on the links up to the Gateway, labelled `parentRefs`. Each band carries a one-line statement of what that role is concerned with, from the source's own descriptions.
- **Design requirement — the cardinality annotations are content, not decoration.** *Exactly one* GatewayClass per Gateway and *many* Routes per Gateway is a Bearings item and a likely exam item. Drawing three boxes in a column without the numbers loses the examinable half.
- **Design requirement — the bands must read as organisational boundaries, not as a call stack.** Different teams own different bands; that is the design principle the whole API is built on. A rendering that looks like a layered architecture diagram implies a runtime relationship instead of an ownership one.
- **Design requirement — do not draw the request path in this figure.** The request flow is §5's fifth beat and it is prose. Adding a traffic arrow through the bands would collapse the ownership story into a routing story and lose the reason the figure exists.
- **Label count**: three role names, three resource names, two cardinality annotations, one `parentRefs` — nine. Over the comfortable ceiling. **Cut the three role concern-statements to the caption** and the in-figure count drops to nine labels of which three are one-word role names; if it still feels crowded, drop `parentRefs` first, since §5's prose carries it.

### `ch10-fig04-networkpolicy-additive-selectors`

- **Purpose**: §6's Fixed Points — additivity, and the two-selectors-one-object structure Chapter 4 promised.
- **Content**: a single subject Pod in the centre. **From the left**, two separate NetworkPolicy objects, each drawn with its own `podSelector` arrow pointing at the subject Pod (this is the *subject* selection), and each with a rule list containing a peer selector. Policy A's rule permits `app: web`; Policy B's permits `app: batch`. **To the right of the subject Pod**, the resulting permitted set drawn as a **union** — both `app: web` and `app: batch`, visually merged into one region rather than two adjacent ones. Somewhere clearly outside that region, a third Pod carrying neither label, with **no arrow at all** — not a crossed-out arrow, not a blocked arrow. Nothing.
- **Design requirement — the permitted set must be drawn as a union, not as two lists.** Additivity is the section's hardest fact for a firewall-experienced reader and this is the figure's job. Two adjacent boxes say "two policies"; one merged region says "one permitted set assembled from two grants", which is the actual semantic.
- **Design requirement — there must be no deny glyph anywhere in the figure.** No red X, no barrier, no crossed-out arrow. The excluded Pod is excluded by *absence of a grant*, and any visual that depicts denial as an action contradicts the section's central Fixed Point. **This is the single most important design constraint in the chapter**, and it is the one an illustrator's instinct will most reliably violate, because "show what is blocked" is the obvious way to draw a security diagram.
- **Design requirement — the two selector roles must be visually distinguishable.** The `podSelector` arrows (choosing the subject) and the peer selectors (choosing who may connect) are different jobs, and Chapter 4 line 835 promised the reader they would see both in one object. Different arrow styles or different attachment points; the figure fails its Chapter 4 debt if the two read as the same relation.
- **Label count**: two policy names, two peer labels, one subject Pod, one union region — six. Comfortably within the ceiling, which is fortunate, because the design constraints above are demanding.

### `ch10-zenith-nothing-without-a-controller`

- **Purpose**: the chapter's one Zenith. §8's claim, in the brand's illustrative register.
- **Content**: four panels in a row, one per instance, each drawn in the same three parts — **the object** (present, solid, correct), **the component** (absent, drawn as an empty outline in a consistent position), **the effect** (nothing). Left to right: a `type: LoadBalancer` Service with no provider; a Service whose selector matches no Pods; an Ingress with no controller; a NetworkPolicy on a plugin that does not implement it. Beneath all four, running the full width, one sentence — Chapter 3's phrase.
- **Design requirement — the four panels must be structurally identical and visually rhyme.** Same three parts, same positions, same weights, only the contents differ. The argument *is* the repetition: four unlike problems with one shape. Panels that differ in layout say "four examples"; panels that rhyme say "one rule".
- **Design requirement — the empty component slot must be in the same place in all four.** That consistent gap is what the reader's eye should learn to look for, and it is the operational habit §8 is trying to install: *what is watching this, and is it installed?*
- **Design requirement — mark the fourth panel differently, and only the fourth.** The NetworkPolicy case is the one that fails silently, and the figure's last beat is that difference. A small annotation on the fourth panel's effect — *and nothing tells you* — is enough. Do not annotate the other three; the contrast is the content.
- **Register note.** This is the chapter's only figure permitted the brand's illustrative treatment. Given the book's world register — Communications Officer, early interstellar — the natural framing is a bank of four signal stations, orders posted and legible at each, no operator at any of them. Per Part 18.7 the caption adds context rather than restating the Zenith's sentence, which is already inside the figure.
- **Label count**: four object names, one shared sentence, one fourth-panel annotation — six, with the three-part structure carrying the rest through repetition rather than labelling. Well within the ceiling, which is correct for a figure this narrative.

---

## 9. Open questions for the author

1. **Subtitle — 14 words in the arc outline against a ≤10-word constraint (editorial, non-blocking).**
   The arc's working subtitle is *"Ingress is frozen, Gateway is the future, and neither does anything without a controller."* The frontmatter carries *"Frozen, superseded, and inert without a controller"* — seven words, and it covers the NetworkPolicy half of the chapter as well as the Ingress half, which the arc's version does not. Arc-faithful alternative at exactly ten: *"Ingress is frozen, Gateway is next, and neither acts alone"* — but "acts alone" is vaguer than "inert" and loses the word §7 needs. **Recommendation: take the version in the frontmatter.** If you prefer the arc's explicit naming of both APIs, say so and the ten-word variant goes in.

2. **⚠ BLOCKING — IngressClass is assigned to §3 by B6 and appears in no cached source.**
   The cached `k8s-docs-ingress-2026-08-23.md` is a 22-line summary that covers terminology, the definition, the freeze note, the controller prerequisite, and the four Ingress types. It contains **no mention of IngressClass**. B6 assigns "Ingress controllers; IngressClass" to §3. Without a source, §3 can teach the controller dependency (fully sourced) but cannot explain how an Ingress names the controller that should fulfil it — which is a real hole, because "you must have a controller" immediately raises "which one, if there are two?". **Recommendation: fetch `kubernetes.io/docs/concepts/services-networking/ingress/` in full.** One fetch closes this and #3 together.

3. **⚠ BLOCKING — `pathType` and the default backend are assigned to §2 by B6 and are likewise uncached.**
   Same snapshot, same limitation. The Types-of-Ingress block gives the four *shapes* but no field-level detail: no `pathType` and its three values, no default backend, no rule structure, no `spec.tls[]`. §2 as specified above is fully sourceable **without** them — the four shapes plus the HTTP/HTTPS limit plus TLS-via-Secret is a coherent and examinable section. The question is whether the chapter *should* go deeper. **Recommendation: fetch the full page (same fetch as #2), then decide.** `pathType` in particular has a plausible exam profile — `Prefix` versus `Exact` is exactly the kind of enumerated detail this exam reaches for — and it would be better to have the source and choose not to use it than to discover the gap during drafting.

4. **⚠ BLOCKING (editorial, not source) — the pattern was already named in Chapter 3, and two other stages think Chapter 10 names it.**
   B6 says §3 *"names the pattern"* and is the *"definition home for cross-cutting theme 3"*. The arc outline says *"name the pattern here so Ch 13 and Ch 17 can retrieve it by name."* Chapter 9's Voyage Ahead says *"Chapter 10 gives it a name."* **But shipped `chapter-03` line 601 already named it**, in a ⚓ Worth Securing callout, with the phrase *"an object without its component does nothing"*, and published forward pointers to Chapters 9, 10, 13 and 17 — describing Chapter 10 as *"the same pattern, first recurrence."*
   Three stages therefore disagree with one shipped chapter, and the shipped chapter wins by the B7 ledger's own precedence rule.
   **Recommendation, and it is what the section plan above assumes: Chapter 10 does not coin a name.** §3 retrieves Chapter 3's phrase verbatim and §8 promotes it — from an aside the reader was told to remember, to a rule they have now accumulated four instances of and can apply to objects this book never mentions. This is honest, it keeps one name across five chapters (which is the entire point of a cross-cutting theme), and it makes §8 a *better* Zenith rather than a worse one, because "here is a name for a thing" is weaker than "here is why the thing was always true."
   **What this needs from you:** confirmation, plus a decision on whether to update B6's Ch 10 §3 row and the arc outline's Chapter 10 note so the next stage does not re-raise this. The alternative — Chapter 10 coins a competing name — would require editing shipped `chapter-03` and should not be chosen lightly.

5. **Chapter 9 says this chapter "opens with" the inert object; the section pins put it at §2–§3 (minor, one sentence).**
   `chapter-09` line 1708: *"It also opens with an object that you create, and that does nothing at all."* Under the pins, §1 is the exposure ceiling and the object arrives at §2 with its inertness at §3. **Recommendation: no renumbering — §1's pin is explicit and Chapter 9 published it itself at line 544.** Instead, §1's closing line names the object and flags the shape (see the §1 plan's closing beat), which turns a mismatch into a deliberate setup and keeps Chapter 9's promise readable as kept. Flagging it because a reader who cross-checks will notice, and because a later stage might otherwise "fix" the numbering.

6. **Should §5 name Gateway API as the pattern's third instance in this chapter? (Pedagogical, non-blocking.)**
   The Gateway API snapshot calls Gateway *"an add-on containing API kinds"* and says the specifications are *"defined as custom resources"*. Both facts support the statement that Gateway API is not present in a default cluster and something must install it — which would be a **third** instance of the chapter's pattern, in a third unlike object.
   **For:** it strengthens §8 measurably, it is sourceable, and it is a fact a reader will want (having just been told to prefer Gateway, "is it there?" is the obvious next question).
   **Against:** §5 is already the chapter's largest body of new vocabulary, and a reprise of §3's argument four sections later risks the chapter feeling like it has one idea. It also slightly weakens §8's cleanest framing — *two objects with nothing in common* is a sharper opening than *three*.
   **Recommendation: include it as a one-clause fact in §5 (Gateway API is an add-on built on custom resources; it is not in a default cluster) and do NOT frame it as an instance of the pattern there.** Let §8 pick it up if it wants a fifth. That gets the useful fact in front of the reader without spending §3's beat twice.

7. **How deep should §6 go on the default-deny idiom, and does it need a manifest? (Non-blocking, but decide before drafting §6.)**
   The cached NetworkPolicy snapshot gives the full semantics — isolation, defaults, `policyTypes`, additivity, both-ends, both exceptions — but does **not** state the empty-`podSelector`-selects-all-Pods idiom, does not give the canonical default-deny manifest, and does not cover `ipBlock`'s `except` field. §6's seventh beat can be written as a **derivation** ("select the Pods, name the direction, permit nothing") without asserting any uncached mechanism, and there is a decent argument that deriving it is better teaching than showing a manifest to copy.
   **Recommendation: derive it, and do not fetch.** An associate-tier reader needs to know that default-deny is achievable and *why* it works given no deny rule exists; they do not need the YAML. If you would rather have the option, `kubernetes.io/docs/concepts/services-networking/network-policies/` in full closes it.

8. **The `[source:` tag for the "silent failure" characterisation (small, but it recurs).**
   §7's most valuable content — that an unenforced NetworkPolicy is harder to detect than a broken Ingress — is the book's reasoning, not a documented claim. The source states the plugin dependency and the no-effect consequence and stops. The book has an established idiom for exactly this (`chapter-03` line 597: *"That second half is an observation, not a documented claim. Hold the two apart"*). **Recommendation: use that idiom, do not tag the inference, and keep the tagged claim and the untagged inference in separate sentences.** Raising it because §7 is the one place in this chapter where the untagged half is more memorable than the tagged half, which is exactly when the discipline matters most.

9. **Zenith heading glyph — Chapter 9 shipped against B6's recommendation (cosmetic, one line).**
   B6 Collision #4 recommends `## ☀️ §N — Title` on the closing section for Chapters 9–19. Chapters 5, 6 and 7 shipped that way; Chapters 8 and 9 shipped a difficulty glyph and put `☀️ **Zenith:**` inline instead (`chapter-09` line 1178). This outline adopts B6 — `## ☀️ §8` **plus** the inline block, which satisfies both the recommendation and the structural contract's marker pattern. **Recommendation: adopt as specified, and treat conforming Chapters 8 and 9 as a separate one-line cosmetic sweep if you want Part III internally uniform.** Not this stage's call, and nothing breaks either way.

10. **Section-count sanity: eight sections against five weight points (recorded, no action requested).**
    Chapter 9 ran eight sections for seven points; this chapter runs eight for five, which is the highest section-to-weight ratio in Part III so far. Two folds were considered and rejected:
    - **Fold §4 into §5** (freeze plus successor as one section). Rejected: Chapter 9's Voyage Ahead specifically pre-sold `frozen` as a precise, exam-worthy definition, and burying it inside a section about a different API undersells a promise the reader is holding. §4 is short by design; short is not the same as foldable.
    - **Fold §7 into §6** (policy semantics plus limits as one section). Rejected on two grounds: B6 assigns them separately, and more importantly §7's first half is the chapter's second instance of the pattern and needs to sit adjacent to §8 to do its structural job. A combined §6 would bury the Zenith's second leg in the middle of a long section.
    Both remain available if a later stage finds the chapter overlong in draft. Recording the reasoning so the decision does not have to be re-derived.
```