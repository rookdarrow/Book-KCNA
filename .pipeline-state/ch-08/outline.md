I have the full context: the five book-outline stages, the eleven published cross-bearings pointing into Chapter 8, Chapter 7's Voyage Ahead handoff, and the cached source set. Here is `outline.md` for Chapter 8.

---

```markdown
---
chapter: 8
chapter_type: "content"
title: "Standing the Watch"
subtitle: "The commands you'll actually type, and the versions that bite"
exam_domain: "Kubernetes Fundamentals (competency: Administration)"
domain_weight_pct: 5
complexity: "mixed"
novelty: "moderate"
prereq_factor: "standard"

#-- SUBTITLE NOTE. The arc outline's working subtitle is "The commands
#-- you'll actually type, and the versions that will bite you" — twelve
#-- words, against this stage's ≤10-word constraint. Tightened above to
#-- ten by dropping "will ... you", which keeps both clauses, keeps the
#-- wry "actually", and keeps the rhythm. See § Open questions #1.

#-- COMPLEXITY NOTE. The arc outline's depth band is "standard — 5 points,
#-- but four unrelated conceptual arcs". `mixed` is the honest complexity
#-- value: §1, §4 and §7 are procedural; §2 and §8 are abstract; §6 is
#-- close to pure recall. No single label covers it. The four-arc problem
#-- is a *structural* difficulty, not a conceptual one, and it is solved
#-- by the spine in § Section plan rather than by a complexity label.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "standard". Planning
#-- signal only, NOT a target.
#--
#-- SECTION NUMBERING — eleven published cross-bearings point into this
#-- chapter. NONE carries a section number; every one is chapter-scoped
#-- ("see Ch 8 — kubectl, in full"). This chapter is therefore free to
#-- number its sections as it likes, which is unusual and worth using.
#-- Verified 2026-08-24 against chapter-01, -03, -04, -07. See § Debts.
sections:
  - name: "The Grammar of a Command"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig01-kubectl-verb-resource-grammar"
    checkpoint_after: false
  - name: "Three Gates and a Logbook"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig02-three-api-gates"
    checkpoint_after: false
  - name: "Dividing a Shared Cluster"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig05-quota-vs-limitrange"
    checkpoint_after: true
  - name: "Taking a Node Out of Service"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig04-node-lifecycle-cordon-drain"
    checkpoint_after: false
  - name: "Who Owns the Control Plane"
    objectives: ["D1.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Versions That Are Allowed to Disagree"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-fig03-version-skew-window"
    checkpoint_after: false
  - name: "The One Backup That Matters"
    objectives: ["D1.2"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Rules, or Consequences"
    objectives: ["D1.2"]
    requires_figure: true
    figure_anchor: "ch08-zenith-consequences-not-rules"
    checkpoint_after: false

#-- Eight sections against Chapter 7's seven. One more section for the
#-- same 5 points, because the arc outline's "four unrelated arcs" is
#-- real and folding them produces sections that change subject halfway.
#-- The spine that makes eight sections read as one chapter is described
#-- in § Section plan opening. Fold options considered and rejected in
#-- § Open questions #9.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "a client tool that talks to a remote server — what it must know before it can talk, and what happens when there are two servers"
    - "retrieval from Ch 3 — which component is the only door into the cluster, and what that implies about who checks you at it"
    - "the distinct questions any server must answer about an incoming request before doing the work"
    - "retrieval from Ch 4 — what namespaces were for, and the mechanism Ch 4 named for dividing resources between teams"
    - "retrieval from Ch 7 — the built-in taint for a node about to be rebooted, and what it did to Pods already running there"
    - "retrieval from Ch 4 — the Lease objects in kube-node-lease, and what the control plane should conclude when they stop"
    - "two pieces of software in one system at different versions — which direction of mismatch is more dangerous, and why"
    - "running on a managed platform versus your own hardware — which operational duties move, and which stay yours"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 17 = 35, and names this chapter first on its
#-- list of chapters expected to exceed the Bearings minimum. Arc outline
#-- carries that forward as "12-15 Bearings (three checkpoints)". Set at
#-- 15 across three checkpoints of 5, matching the shape shipped by
#-- Chapters 3-7. Chapter total 35 -> 40.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 17
  total_this_chapter: 40

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D1.2"]
  concepts:
    - "kubectl"
    - "kubectl-syntax"
    - "verb-resource-grammar"
    - "resource-type-abbreviation"
    - "kubeconfig"
    - "kubeconfig-precedence"
    - "in-cluster-authentication"
    - "serviceaccount-token-file"
    - "namespace-override"
    - "api-access-gates"
    - "authentication"
    - "authorization"
    - "admission-control"
    - "admission-controller"
    - "mutating-admission"
    - "validating-admission"
    - "dynamic-admission-control"
    - "auditing"
    - "hub-and-spoke-api-pattern"
    - "tls-bootstrapping"
    - "resource-quota"
    - "limit-range"
    - "namespaced-vs-cluster-scoped"
    - "node-registration"
    - "node-self-registration"
    - "cordon"
    - "drain"
    - "uncordon"
    - "unschedulable-node"
    - "node-conditions"
    - "ready-condition"
    - "memorypressure"
    - "diskpressure"
    - "pidpressure"
    - "networkunavailable"
    - "node-heartbeats"
    - "node-lease"
    - "node-controller"
    - "api-initiated-eviction"
    - "node-monitor-grace-period"
    - "cluster-planning-axes"
    - "managed-kubernetes"
    - "self-hosted-cluster"
    - "kubeadm"
    - "minikube"
    - "kind"
    - "k3s"
    - "semantic-versioning"
    - "supported-releases"
    - "three-supported-minors"
    - "patch-support-window"
    - "version-skew"
    - "upgrade-order"
    - "release-cadence"
    - "etcd-backup"
    - "etcd-snapshot"
    - "etcd-access-equals-root"
    - "disaster-recovery"
  commands:
    - "kubectl-get"
    - "kubectl-describe"
    - "kubectl-explain"
    - "kubectl-config"
    - "kubectl-cordon"
    - "kubectl-drain"
    - "kubectl-uncordon"
    - "etcdctl-snapshot-save"
    - "etcdutl-snapshot-restore"

figures_planned:
  - "ch08-fig01-kubectl-verb-resource-grammar"
  - "ch08-fig02-three-api-gates"
  - "ch08-fig03-version-skew-window"
  - "ch08-fig04-node-lifecycle-cordon-drain"
  - "ch08-fig05-quota-vs-limitrange"
  - "ch08-zenith-consequences-not-rules"
---

# Chapter 8 Outline — Standing the Watch

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 8: Standing the Watch` | required | top |
| `## *"The commands you'll actually type, and the versions that bite"*` | required | line 2 |
| Metadata line (domain / weight / complexity / novelty) | required | after subtitle — **conform to the shipped ch-02/-05/-07 house form**, which carries the published 44% domain weight with both CNCF source tags inline plus the authored-allocation disclaimer |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings #1–#3` | **required, min 2** | after §3, §5, §7 |
| `★ Fixed Point` ×6 | **required, min 1** | §1, §2, §3, §4, §6, §7 |
| `**Dead Reckoning:**` ×1 min | **required** | §6 — the skew table stated flat, no watch-standing register at all. See §6 |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §4 (cordon is not drain), §6 (kubectl is the exception to the never-newer rule) |
| `☀️ Zenith` | expected | §8 |
| `## Exam Alert! 🚨` | **required** | after §8 |
| `## Practice Questions` | **required** | 17 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19, and this one closes Part II |
| `🏆 Safe Harbor` | expected | chapter close |

**Heading form.** `## ⚪ §1 — Title`, matching Chapters 5, 6 and 7. Difficulty glyph before the section number.

**Zenith:** exactly one, per Part 18.10. `ch08-zenith-consequences-not-rules` in §8. This chapter carries five concept diagrams plus the Zenith — one more than Chapter 7, and the count is justified: five of the chapter's six figures are *reference* diagrams for material that is otherwise a wall of prose rules (the command grammar, the gate sequence, the skew window, the node state machine, the quota/limit contrast). This is the most reference-shaped chapter in Part II and the figure budget should reflect that. `ch08-fig03` and `ch08-fig05` both belong in The Lodestar; design them at quarter-page legibility.

**Attention Budget guidance for drafting.** Eight sections, five distinct costs:

| Section | Cost | Why |
|---|---|---|
| §1 | low | One four-slot grammar and a file path. The reader has been typing these commands since Chapter 4 without being told the rule |
| §2 | **high** | The chapter's only genuinely new conceptual model, and its most examinable. Three gates, in order, each with a different kind of "no" |
| §3 | medium | Two mechanisms that are easy to state and easy to swap. The discrimination is the work, not the definitions |
| §4 | medium | Procedural, but with a state machine underneath and a deliberate callback to Chapter 7's taint table |
| §5 | low | Planning questions and four tool names. Genuinely easy material, deliberately placed after the hard block as an arousal restoration point |
| §6 | **high** | The densest pure-recall block in the book (**[B3]**). Five components, four different skew rules, one exception |
| §7 | medium | Short, but it is the chapter's only irreversible-consequence material and it earns a slow read |
| §8 | low | Synthesis |

*"If you only have 15 minutes"* should point at **§2's gate sequence and §6's skew table**, then Bearings #3. Those are the two blocks where this chapter's exam points actually live; §1, §4 and §5 are recognition material the reader will mostly get right on instinct.

**Session split.** Recommend two sessions with the break after ☆ Taking Your Bearings #2. That puts §1–§5 (the request path and the node) in one session and §6–§8 (versions, disaster, synthesis) in the other, which also isolates §6's recall block at the start of a fresh session where it belongs.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 8 — Standing the Watch". Carried forward without modification:

- **Covers**: **D1.2** — kubectl syntax and verbs; kubeconfig; in-cluster auth; cluster planning axes; managed vs self-hosted; bootstrap tooling (kubeadm, minikube, kind, k3s); the three API access gates (authentication → authorization → admission); auditing; ResourceQuota and LimitRange; node lifecycle (cordon/drain/uncordon, node conditions, leases); semantic versioning; supported releases; version skew; release cadence; etcd backup.
- **Prerequisites**: Ch 3 (control plane), Ch 4 (objects, namespaces), Ch 7 (nodes as scheduling targets).
- **Retrieval targets**: **20%** **[B3]**, from Ch 3–7, **with the ≥4-back spacing floor now active** — at least one item must come from Ch 2–4. Named anchors: the OCI/CRI boundary (Ch 2) or the control loop (Ch 3) as the ≥4-back item; namespaces (Ch 4) under ResourceQuota; node conditions against scheduling (Ch 7).
- **Question budget**: 8 Soundings · 12–15 Bearings · 17 Practice. Set at 15 Bearings below.
- **Figures**: six anchors, listed verbatim in `figures_planned`.
- **Depth band**: standard.
- **Blocking gaps**: G1 (kubectl command surface), G26 (node lifecycle), G27 (etcd backup), G28 (bootstrap tooling). **Status: G26, G27 and G28 are CLOSED. G1 is closed for this chapter's purposes** (`kubectl events`, `top`, `port-forward` and `debug` remain uncached but belong to Ch 13 and Ch 16, not here). **Three gaps the arc outline did not anticipate are open and two of them are blocking** — see § Open questions #2, #3, #4.
- **[B3] The book's worst decay problem lives here.** §6's skew block is the densest pure-recall material in the book, taught at the 40% mark. The fix is scheduled and non-negotiable: **version skew is retrieved in Ch 13** (as a troubleshooting cause) and **release cadence in Ch 17** (where the three-supported-minors rule and the ~3/year cadence explain each other). **The admission gate is retrieved in Ch 12** (Pod Security Admission). See § What this chapter owes forward.

**One inherited discrepancy, resolved the same way Chapters 6 and 7 resolved it.** B4's schedule puts Chapters 6–8 at ~15%; B3's schedule and the arc outline both put Chapter 8 at 20%, and the arc tags the figure **[B3]**. The arc outline is the later stage and carries explicit provenance, so **20%** is operative. Recorded once; not re-litigated.

### Debts falling due in this chapter

**Eleven published cross-bearings point at Chapter 8** — more than at any other chapter in the book so far. Draft knowing the reader was told to expect each one by name. All eleven are chapter-scoped; **none names a section number**, so section numbering here is unconstrained.

| Owed by | Promise made | Paid in |
|---|---|---|
| `chapter-01` line 466 | Named as one of the three chapters a working developer most reliably has gaps in | Whole chapter. Do not add a callback — the reader will feel it |
| `chapter-03` line 408 | *"etcd backup and restore in practice"* | **§7** |
| `chapter-03` line 671 | *"the authentication, authorization, and admission gates a request actually passes through on its way in"* | **§2** — the reader was given the three names in order, in prose, at the point the API server was introduced. §2 discharges it |
| `chapter-04` line 316 | *"kubectl, in full"* — the full command surface, its verbs, its flags, how it authenticates | **§1** |
| `chapter-04` line 584 | *"node conditions and heartbeats"* — the Leases in `kube-node-lease` and what the node controller does when they stop | **§4** |
| `chapter-04` line 590 | *"ResourceQuota"* — named as the mechanism by which namespaces divide cluster resources | **§3** |
| `chapter-07` line 408 | *"node administration"* — what makes Capacity and Allocatable differ, and how it is configured | **§4** — see § Open questions #6, this one is partially unpayable |
| `chapter-07` line 430 | *"quotas and limit ranges"* — the mechanisms that stop other people booking the whole cluster | **§3** |
| `chapter-07` line 519 | *"admission control"* — the gate that enforces the NodeRestriction plugin's label prefix rule | **§2** |
| `chapter-07` line 702 | *"taking a node out of service"* — and the prose says this act is **"Chapter 8's opening move"** | **§1 opening example, resolved in §4.** See below |
| `chapter-07` line 945 | *"cluster administration"* — where scheduling profile configuration actually lives | **§5**, one clause |

**On `chapter-07` line 702 — "Chapter 8's opening move."** This is the one debt with a placement constraint attached, and it is worth honouring literally rather than loosely. The resolution: **`kubectl cordon` is the first command in the chapter.** It appears in §1 as the worked example of the command grammar — verb, resource type, name — and §1 deliberately does *not* say what it does beyond the one sentence Chapter 7 already gave. That opens a loop the reader carries through §2 and §3 and which §4 closes with the full treatment. So the promise is kept exactly (`cordon` is the opening move, the first command typed), and the chapter gets a curiosity gap for free rather than spending its opening on its fourth-most-interesting arc.

Chapter 7's Voyage Ahead reinforces this: it lists four things the reader cannot yet do, in this order — take a node out of service, stop a team booking the cluster, reason about versions, and name the three gates. §1's opening example answers the first as a *command shape* while §2–§7 answer all four as consequences.

### What this chapter owes forward

Four debts, three of them **[B3]** decay fixes that are mandatory rather than optional.

| Owed to | What | Why it is mandatory |
|---|---|---|
| **Ch 13** | **Version skew as a troubleshooting cause** | **[B3]** decay fix. §6 is taught at the 40% mark and dies there without this. Ch 13 must retrieve it by name, not by allusion |
| **Ch 17** | **Release cadence beside the three-supported-minors rule** | **[B3]** decay fix. The two facts explain each other and neither is memorable alone. Ch 17 owns the KEP/SIG material they sit inside |
| **Ch 12** | **The admission gate** | **[B3]**. Pod Security Admission is an admission controller; Ch 12 derives it from §2's gate rather than re-establishing it. §2 must therefore state the gate in a form Ch 12 can point at |
| **Ch 12** | **Namespaced vs cluster-scoped, operationally** | Cross-cutting theme #2 (4 → 8 → 12). §3/§4's hinge is the middle beat: ResourceQuota is namespaced, Node is not. Ch 12 *derives* the RBAC four-way matrix from this rather than memorising it |

Additionally, **§2 plants the extension point** that Ch 17 collects: dynamic admission control via webhooks is one of the four API-access extension points in Ch 17's synthesis. One forward cross-bearing, no content.

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**Open on the command, not on the topic.** Chapter 7 ended by naming a command the reader cannot yet type and telling them it was this chapter's opening move. Honour that in the first line: `kubectl cordon node-7`. Three words that take a machine out of service without disturbing anything running on it. Then the observation that makes the whole chapter: **the reader has typed commands in this shape for four chapters without ever being told what the shape is.** They have run `kubectl apply -f`, `kubectl get pods`, `kubectl scale`. Nobody explained the grammar, and it worked anyway — which is exactly the condition under which a candidate walks into an exam confident and loses five points to a question about which component is allowed to be one minor version newer than which.

**The identity frame is the shift from user to watchstander.** Chapters 2 through 7 made the reader someone who can describe what should run and where. This chapter makes them someone who is *responsible for the thing it runs on*. That is a different posture, and the register should carry it: a watch is not a task you complete, it is a period during which you are accountable. Practitioners on watch think in terms of what they can take out of service safely, what they can stop other people doing, and what they cannot get back. Say that in the practitioner's register. Do not moralise about it, and do not inflate it into a lecture about responsibility.

**Then the curiosity gap, which is the chapter's actual thesis and should be planted here as a question rather than an answer.** Everything in this chapter is a command or a rule, and lists of commands and rules are the least memorable material in any study guide. So plant the doubt: *by the end of this chapter you will not have learned a single new mechanism.* Every administrative act here is a write through a door the reader already knows, reconciled by a controller they already met. That claim is deliberately hard to believe at the start of a chapter that contains four unrelated-looking arcs, and §8 pays it off. Open the loop; do not explain it.

**The stakes, stated flat and without inflation.** Five points on this book's authored allocation — CNCF publishes four domain weights and no competency weights, and the front matter says so. What the number understates is the *shape* of these points: §6's version-skew material is the single most mechanically checkable block in the curriculum, which makes it the easiest place in the exam to lose points you had every opportunity to keep. And **[B3]** flags this chapter as the book's worst decay risk — taught once, at the 40% mark, and otherwise unvisited. That is a fact about the book's architecture and the fix is scheduled downstream; it is not a reason to inflate the chapter or to manufacture urgency here. The reader is an adult professional and will notice if you do.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Six outcomes, active verbs:

- **Decompose** any `kubectl` command into its four slots, and say where the tool found the cluster it just talked to.
- **Trace** a request through the three gates it passes before anything is written down, and say what each gate can and cannot do about it.
- **Distinguish** a ResourceQuota from a LimitRange by what each one constrains and at what scope — and say which one makes a Pod that was previously valid stop being accepted.
- **Take** a node out of service and put it back, and predict what happens to the Pods on it at each step.
- **State** which Kubernetes components are permitted to disagree about their version, by how much, and in which direction.
- **Recognise** every administrative act in this chapter as a write through one door, reconciled by a controller you already know — which is the only thing you actually have to remember.

*You'll also stop reading the version-skew table as arbitrary trivia, which is a smaller change than it sounds and is worth more exam points than anything else in Part II.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Chapter 8's prerequisite set is Chapter 3 (the control plane and the API server as the single door), Chapter 4 (objects, spec/status, namespaces, `kube-node-lease`) and Chapter 7 (nodes as scheduling targets, the `unschedulable` taint), plus general operational literacy about client tools, shared systems, and version mismatch. **Four questions test priors the reader arrives with; four are deliberate retrieval from Chapters 3, 4 and 7.** **[B3]** Soundings sit outside the retrieval budget but do retrieval work anyway, sourced from B2's Prerequisites column.

**Fixed Points this chapter teaches, which Soundings must therefore not reveal:**

1. `kubectl [command] [TYPE] [NAME] [flags]` — one grammar, four slots. Resource types are case-insensitive and accept singular, plural or abbreviated forms; **names are case-sensitive**.
2. `kubectl` finds its cluster in `$HOME/.kube/config`, overridden by `KUBECONFIG` or `--kubeconfig`; running inside a Pod it detects in-cluster conditions and acts against the ServiceAccount's namespace unless told otherwise.
3. A request passes three gates in order: **authentication**, then **authorization**, then **admission control**. Each says no differently, and only admission can change the request.
4. ResourceQuota constrains a **namespace in aggregate**; LimitRange constrains **individual objects** and supplies defaults.
5. `cordon` stops new Pods and leaves running ones alone; `drain` evicts them; `uncordon` restores scheduling. DaemonSet Pods tolerate an unschedulable node.
6. A node has two heartbeat forms — status updates and a Lease — and `Ready` becomes **Unknown**, not False, when the control plane stops hearing from it.
7. Release branches are maintained for the most recent **three** minor releases, with ~1 year of patch support, at roughly three minor releases a year.
8. kubelet may be up to **three** minors older than kube-apiserver and must never be newer. **`kubectl` is the only component permitted to be newer**, within one minor in either direction.
9. All cluster state is in etcd; access to etcd is equivalent to root in the cluster; a snapshot is the only thing that brings a cluster back after losing every control-plane node.

Each question below is checked against that list.

| # | Question topic | What it tests | Spoiler check |
|---|---|---|---|
| 1 | You have a command-line tool on your laptop that manages a server somewhere else. Before it can do anything, what does it need to know — and what changes when you're responsible for two of those servers? | The client-configuration prior in its general form, and specifically that "which server" is itself a piece of state | Names nothing Kubernetes-specific. Fixed Point #2 is the *file path, the override precedence, and the in-cluster detection*, none of which a general instinct supplies. Readers who answer "an address and a credential" have set themselves up perfectly for §1 |
| 2 | **Retrieval from Ch 3.** Chapter 3 was emphatic that one component is the only way in — nothing else exposes a remote service. Name it, and say what that architecture implies about where you would put a security check | The hub-and-spoke prior in its pre-test position, and the reasoning step §2 depends on | The reader is retrieving a Chapter 3 fact and drawing one inference. Fixed Point #3 is that there are **three** gates, **in a specific order**, with **different powers** — the inference "checks go at the door" supplies none of that, and readers who get here on their own will find §2 satisfying rather than redundant |
| 3 | A server receives a request to do something expensive. List the distinct questions it must answer before it does the work — and say whether any of them could result in the request being *changed* rather than accepted or refused | **The chapter's most valuable pre-test.** Most readers will produce two questions — who are you, are you allowed. The third is the one they will not have, and the "changed rather than refused" clause makes the gap felt rather than merely present | Deliberately does not name authentication, authorization or admission. The reader who produces two of three has *discovered* the gap in their own model, which is exactly what a pre-test is for. Fixed Point #3's names, order and the mutate/reject distinction all remain unrevealed |
| 4 | **Retrieval from Ch 4 §6.** Chapter 4 said namespaces are for environments with many users across teams or projects, and named the mechanism by which cluster resources get divided between them. What was it called, and what do you think it constrains? | **[B3]**'s designated namespaces anchor, in its pre-test position. Chapter 4 stated this explicitly and sent the reader here | The reader is retrieving a name Chapter 4 gave them. Fixed Point #4 is the *contrast* — quota is aggregate and namespace-scoped, LimitRange is per-object and supplies defaults — and the second clause invites a guess that is usually right in the wrong way (readers say "how much you can use" and miss that it also forces you to *declare* usage). Nothing about LimitRange is revealed |
| 5 | **Retrieval from Ch 7 §4.** Chapter 7's family table included a built-in taint named `node.kubernetes.io/unschedulable`, with a `NoSchedule` effect, applied deliberately rather than by a failing disk. What did it do to Pods already running on the node? | The load-bearing prior for §4, and the direct payoff for a published cross-bearing | The reader is retrieving Chapter 7's `NoSchedule` timing rule. Fixed Point #5 is the *three-command sequence* and specifically that a second command exists to evict what `cordon` deliberately left alone. Knowing that `NoSchedule` spares running Pods is precisely the setup for "so how do you get rid of them", which §4 answers |
| 6 | **Retrieval from Ch 4 §6.** Chapter 4 pointed at the `kube-node-lease` namespace and said the Lease objects in it are how the control plane knows a node is still alive. If those Leases stop being renewed, what *should* the control plane conclude, and what should it not conclude? | The node-health prior, framed as a distributed-systems reasoning question | Asks for reasoning, not for a status string. Fixed Point #6 is that the `Ready` condition goes to **Unknown** rather than False — a three-valued rather than two-valued answer — and that there are two heartbeat forms rather than one. A reader who answers "it should conclude it can't tell" has reasoned their way to the shape of the right answer without having the vocabulary, which makes §4 land harder |
| 7 | Two components of one system are running at different versions. One is a client, one is a server. Which direction of mismatch worries you more — a newer client talking to an older server, or an older client talking to a newer server — and why? | The skew prior. Deliberately framed as a design intuition rather than a rule | §6's Fixed Points (#7, #8) are the *specific numbers* — three minors for kubelet, one either way for kubectl, three supported release branches — and the fact that kubectl is the sole exception to never-newer. A general intuition about client/server compatibility supplies none of the numbers and, usefully, most readers' intuition here is *right in general and wrong for kubectl*, which is the trap #8 exists to defuse |
| 8 | You are running a service on a cloud provider's managed platform. Your colleague runs the same service on hardware in a rack. Name two operational duties that are yours in one case and not the other | The ownership prior, which is §5's entire frame and the motivation for §6 and §7 | §5 is planning axes and four tool names; §7 is the backup. Neither Fixed Point (#9 especially) is reachable from a general instinct about managed platforms. Readers who name "patching" and "backups" have written §5's thesis for themselves, which is the ideal outcome for a section this easy |

**Rubric**: standard 6+ / 3–5 / 0–2 per `branded-terms.yaml`. The 0–2 branch carries a specific instruction: **if questions 2, 4, 5 and 6 were the misses, re-read Chapter 3 §2 and Chapter 4 §6 before starting §2.** Those two sections are the prerequisite base for more than half this chapter, and §2 in particular will read as an arbitrary list of three words without Chapter 3's single-door architecture in place.

**Note for drafting:** question 3 is the set's centrepiece and should be written to *invite an incomplete answer*. A reader who confidently lists two gates and then meets a third has had a small, honest experience of their own model being incomplete — which is the pretesting effect working exactly as Part 11 describes. Do not soften it with a hint. Questions 1, 3, 7 and 8 must stay phrased as situations; a Soundings question answerable by reciting a term has stopped doing metacognitive work.

---

## 4. Section plan

Eight sections. **No published cross-bearing pins a section number** (all eleven are chapter-scoped — verified 2026-08-24), so this chapter is free to order for pedagogy rather than for compatibility. It should use that freedom, because the arc outline's central problem is real: D1.2 is **four unrelated arcs**, and a chapter that presents them as four unrelated arcs is a chapter the reader forgets.

**The spine that makes them one chapter: follow a single command in.** §1 is the command leaving your laptop. §2 is what it passes through on the way in. §3 is the gate that can refuse it on someone else's behalf. §4 is what it did when it arrived. §5 asks who owns the thing it arrived at. §6 asks which versions of that thing will accept it. §7 asks what happens when the thing it wrote to is gone. §8 observes that none of this was new.

That spine also solves the arousal problem. Four unrelated arcs in a five-point chapter is a recipe for a flat read; a request path is a narrative. And it puts the two hard blocks (§2, §6) at opposite ends with the chapter's easiest section (§5) between them as the Part 2 arousal-restoration point.

**One command threads all eight sections:** `kubectl cordon node-7`. It is §1's grammar example, §2's worked request (it is authenticated, authorized, admitted, and persisted), §4's full treatment, and §8's proof — because `cordon` turns out to write a field that Chapter 7's taint machinery was already watching. Use it deliberately. It is the cheapest structural device available and it discharges a published promise at the same time.

### §1 — ⚪ The Grammar of a Command

**Discharges `chapter-04` line 316 ("kubectl, in full") and opens the chapter with `chapter-07` line 702's promised move.**

**First, the grammar, because it is one line and the reader has never been shown it.** Every `kubectl` invocation is `kubectl [command] [TYPE] [NAME] [flags]`. The **command** is the operation — `create`, `get`, `describe`, `delete`. **TYPE** is the resource type. **NAME** is the specific resource; omit it and you get all of them. **Flags** are optional, and a flag on the command line overrides both default values and any corresponding environment variable. Draw it as four slots and then run three commands the reader has already typed through the same four slots, so the shape becomes visible retroactively.

**Second, the two small facts inside the grammar that are exam-shaped.** Resource types are **case-insensitive**, and you may use the singular, plural, or abbreviated form — `pod`, `pods`, `po` are the same thing. Resource **names are case-sensitive**. That asymmetry is a one-sentence Fixed Point and it is precisely the shape of a distractor.

**Third, the verb surface.** Give the reader the list as a table rather than as prose: `get`, `describe`, `apply`, `create`, `delete`, `logs`, `exec`, `scale`, `rollout`, `explain`, `config`. Several are already familiar and should be marked as such — `apply` from Chapter 4, `scale` and `rollout` from Chapter 6 — because the retrieval is free and it makes the table feel like an inventory rather than a list of new things. `explain` deserves one sentence of its own: it returns documentation for a resource type, and it is the only entry in the table that answers a question about the API rather than about your cluster.

**Fourth, where the cluster came from, which is the section's second real idea.** For configuration, `kubectl` looks for a file named `config` in the `$HOME/.kube` directory. You can specify other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag. State the precedence plainly. This is also the answer to Soundings question 1 and the reader should feel it land.

**Fifth, the in-cluster case, which is genuinely surprising and is one clean fact.** `kubectl` first determines whether it is running inside a Pod: it checks for the `KUBERNETES_SERVICE_HOST` and `KUBERNETES_SERVICE_PORT` environment variables and for a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. If all three are present, in-cluster authentication is assumed — and the tool then acts against the **ServiceAccount's namespace** rather than a default, unless `--namespace` says otherwise. Chapter 4 used the second half of this fact once, in an answer key; here it gets its full statement.

**Close on the command that opens the chapter, and stop.** `kubectl cordon node-7`. Verb, resource type, name — the grammar, instantiated. Say only what Chapter 7 already said: it takes a node out of service without disturbing what is running on it. Then say explicitly that the rest of what that command does is §4's, and move on. **Do not teach `drain` here.** The loop is the point.

- **Objectives**: D1.2
- **Concepts introduced**: `kubectl`, `kubectl-syntax`, `verb-resource-grammar`, `resource-type-abbreviation`, `kubeconfig`, `kubeconfig-precedence`, `in-cluster-authentication`, `serviceaccount-token-file`, `namespace-override`
- **Commands**: `kubectl-get`, `kubectl-describe`, `kubectl-explain`, `kubectl-config`, `kubectl-cordon`
- **Sources**: `k8s-docs-kubectl-overview-2026-08-23.md` (the `kubectl [command] [TYPE] [NAME] [flags]` syntax and each slot's meaning; resource types case-insensitive with singular/plural/abbreviated forms; names case-sensitive; flags override defaults and environment variables; `$HOME/.kube/config`, `KUBECONFIG`, `--kubeconfig`; the in-cluster detection triple and the ServiceAccount-namespace behaviour; the operations table). `k8s-docs-nodes-2026-08-23.md` (`kubectl cordon $NODENAME` marks a node unschedulable; prevents new Pods without affecting existing ones)
- **Figure**: `ch08-fig01-kubectl-verb-resource-grammar`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — one grammar, four slots. **Types are case-insensitive and abbreviable; names are case-sensitive.** The asymmetry is the examinable half
  - `> ⚓ **Worth Securing:**` — `kubectl explain` is the entry in the verb table that pays off longest. It answers questions about the API itself, which means it works on resource types you have never seen, including ones this book does not cover
  - `> 🪝 **Snag:** ` — `kubectl` inside a Pod does not use your kubeconfig and does not default to the `default` namespace. It uses the Pod's ServiceAccount and that ServiceAccount's namespace. Debugging sessions run from inside a cluster surprise people with this at least once
- **Cross-bearings**: back to Ch 4 §2 (**mandatory — the pinned "kubectl, in full" payoff**; `apply` was given one sentence and the reader was sent here); back to Ch 6 (`scale` and `rollout`, met as workload operations, now placed in the verb table); back to Ch 7 §4 (**mandatory** — the `node.kubernetes.io/unschedulable` taint, whose command this is); forward to **§4** (what `cordon` actually does — the loop this section deliberately leaves open); forward to Ch 13 and Ch 16 (`logs`, `exec` and the diagnostic verbs, named here and used there)
- ⚠ **Do not re-teach declarative versus imperative.** Chapter 4 §1 and §6 own it, taught it thoroughly, and closed with the precise claim ("the objects are declarations, and the imperative commands work by changing declarations"). Repeating it is channel redundancy (Part 18.7). One clause of retrieval is the ceiling
- ⚠ **Do not teach `kubectl top`, `events`, `port-forward` or `debug`.** They are Ch 13's and Ch 16's, they are uncached, and naming them here without content invites the reader to expect coverage that is four chapters away

### §2 — 🔵 Three Gates and a Logbook

**The chapter's hardest and most examinable section, and the payoff for `chapter-03` line 671 and `chapter-07` line 519.** Chapter 3 named the three gates in prose at the point the API server was introduced and promised them here. This is the only genuinely new conceptual model in the chapter.

**Open on the question Soundings #3 asked**, and on the answer most readers gave: two gates, not three. Name that gently and use it — a reader who has just discovered a hole in their own model is the most receptive reader this chapter gets.

**Then the three, in order, with the distinction that makes them three rather than one.**

- **Authentication** establishes *who* is making the request. The API server listens on a secure HTTPS port with one or more forms of client authentication enabled; nodes are provisioned with the cluster's public root certificate and valid client credentials, typically a client certificate; Pods authenticate with a ServiceAccount bearer token injected at instantiation.
- **Authorization** decides whether that identity may perform *this action on this object*. One or more forms of authorization should be enabled, particularly where anonymous requests or ServiceAccount tokens are allowed. RBAC is one authorizer among several — name it and hand it to Chapter 12; do not teach Roles or bindings here.
- **Admission control** is the one the reader did not have. Admission controllers see a request that has already been authenticated and authorized, and act on it before it is persisted. **This is the only gate that can change the request rather than merely accepting or refusing it.**

**The mutate-or-reject distinction is the section's Fixed Point and the reason the three gates are not one gate.** Authentication and authorization answer yes or no. Admission may answer yes, no, or *yes, but not as you wrote it*. That is a genuinely different kind of power and it is what makes admission the extension point Chapter 17 collects.

**Ground it in two examples the reader already has**, which costs almost nothing and turns an abstraction into a mechanism:

- Chapter 7 §3 met the **NodeRestriction** admission plugin, which prevents the kubelet from setting labels with a `node-restriction.kubernetes.io/` prefix. Chapter 7 stated the rule and pointed here for the enforcement. This is that.
- §3's ResourceQuota and LimitRange are enforced at this gate. Say so in one clause and let §3 collect it. This is the join that makes §3 feel like a consequence rather than a fourth arc.

**Then auditing, briefly and honestly.** Auditing records the sequence of activities affecting the cluster; it sits alongside the three gates in the cluster-administration guidance as part of securing a cluster. **See § Open questions #4 — with the current source set this is a named topic, not a taught one**, and drafting must not inflate it past what is on disk. One or two sentences, and a clear statement that the exam-relevant fact is that it exists and what it records.

**Close on the architectural point, which retrieves Chapter 3 and sets up §8.** All API usage from nodes and the Pods they run terminates at the API server; none of the other control-plane components is designed to expose remote services. That is why three gates at one door is a complete access-control story rather than one of many. The single door was Chapter 3's most load-bearing idea and it is why this chapter has a spine at all.

- **Objectives**: D1.2
- **Concepts introduced**: `api-access-gates`, `authentication`, `authorization`, `admission-control`, `admission-controller`, `mutating-admission`, `validating-admission`, `dynamic-admission-control`, `auditing`, `tls-bootstrapping`
- **Sources**: `k8s-docs-cluster-administration-2026-08-23.md` (Securing a cluster: Controlling Access to the Kubernetes API, Authenticating, Authorization, Using Admission Controllers, Auditing; Securing the kubelet: control plane–node communication, TLS bootstrapping, kubelet authentication/authorization). `k8s-docs-extending-kubernetes-2026-08-23.md` (API access extensions: authentication, authorization, dynamic admission control via webhooks; webhooks are synchronous HTTP requests to a remote backend and add a potential point of failure). `k8s-docs-control-plane-node-communication-2026-08-24.md` (hub-and-spoke; all API usage from nodes and their Pods terminates at the API server; no other control-plane component exposes remote services; secure HTTPS port with client authentication enabled; authorization especially where anonymous requests or ServiceAccount tokens are allowed; nodes provisioned with the cluster root certificate; kubelet TLS bootstrapping named). `k8s-docs-assign-pod-node-2026-08-23.md` (the NodeRestriction admission plugin and the `node-restriction.kubernetes.io/` prefix). `k8s-docs-cloud-native-security-2026-08-23.md` (securing the cluster means effective authentication and authorization for API access). `k8s-docs-pod-security-standards-2026-08-23.md` (the built-in Pod Security Admission controller — **one clause only**, forward reference to Ch 12)
- ⚠ **SOURCE GAP — BLOCKING. See § Open questions #2.** Two cached sources give the three names in the canonical order, but **no cached source states the sequential-gate semantics** — that a request passes them in order, that admission runs after authorization and before persistence, or that admission controllers may mutate. The Fixed Point as specified above is **not fully sourceable today**. `kubernetes.io/docs/concepts/security/controlling-access/` is the canonical fetch and it closes this outright
- **Figure**: `ch08-fig02-three-api-gates`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — authentication, then authorization, then admission. Authentication asks *who*; authorization asks *may you*; admission asks *should this, exactly as written, be allowed to happen* — and it is the only one of the three that can change your answer instead of refusing it
  - `> 🪢 **Mnemonic:**` — *who, may, and how.* Three words, in order, and each maps to one gate
  - `> ⚠ **Navigational Hazards:**` — authorization and admission are not two names for the same check. Authorization has no opinion about the *contents* of your request; admission has no opinion about your *identity*. A request can be fully authorized and still be rejected — or quietly rewritten — at the third gate
  - `> 🔭 **Closer Look:**` — dynamic admission control means the cluster calls out to a webhook you supplied. The docs are candid that this adds a potential point of failure: your webhook being down is now something that can stop the cluster accepting requests. Deeper than the exam requires
- **Cross-bearings**: back to Ch 3 §5 (**mandatory — the pinned payoff**; the three gates were named in Chapter 3's prose and deferred here); back to Ch 7 §3 (**mandatory** — NodeRestriction, whose enforcement gate this is); forward to **§3** (quota and LimitRange are enforced here); forward to Ch 12 (**mandatory [B3] anchor** — Pod Security Admission is an admission controller, and RBAC is one authorizer; Ch 12 derives both from this section rather than re-establishing them); forward to Ch 17 (dynamic admission control as one of the four API-access extension points)
- ⚠ **Do not teach RBAC.** Roles, ClusterRoles, bindings, the additive-no-deny rule and the four-way matrix are all Chapter 12's, and Chapter 12 needs them intact. Naming RBAC as *an* authorizer is the ceiling
- ⚠ **Do not teach Pod Security Standards.** Ch 12 owns privileged/baseline/restricted and the enforce/audit/warn modes. One clause naming PSA as an example of a built-in admission controller, no more
- ⚠ **Do not teach Konnectivity or SSH tunnels.** The `control-plane-node-communication` snapshot flags them as Chapter 8 material, but they are above associate tier and the exam does not reach them. See § Open questions #7

### §3 — 🔵 Dividing a Shared Cluster

**Discharges two published cross-bearings** — `chapter-04` line 590 ("ResourceQuota") and `chapter-07` line 430 ("quotas and limit ranges") — and carries **[B3]**'s designated namespaces anchor.

**Open by collecting Chapter 7's complaint.** Chapter 7 §2 ended on the observation that nothing stops you booking the entire cluster with requests you will never use, and said the mechanisms that stop *other people* doing it to you live here. That is the section's motivation and it is already in the reader's hands.

**Then the two mechanisms, and keep them apart from the first sentence.** ResourceQuota is a per-namespace mechanism for dividing cluster resources among users and teams — a **ceiling on the namespace in aggregate**. LimitRange constrains **individual objects**: it supplies defaults and bounds so that Pods specify their resource requirements at all. The cached security guidance states the pair's purposes in one sentence — define ResourceQuotas to fairly allocate shared resources, and use LimitRanges to ensure that Pods specify their resource requirements — and that sentence is the cleanest available statement of the contrast.

**The discrimination is the section's whole job, so make it structural rather than definitional.** Two questions: *what is being counted* (the namespace's total, versus one object's numbers) and *what happens to a manifest that says nothing about resources* (quota may refuse it; LimitRange may fill it in). A reader who can answer both can never swap the two, and swapping the two is the only mistake this section exists to prevent.

**Then the hinge, which is the section's most valuable thirty seconds and is cross-cutting theme #2's Chapter 8 beat.** ResourceQuota and LimitRange are **namespaced**. The Nodes that §4 is about to discuss are **not** — Chapter 4 established that Nodes, PersistentVolumes and StorageClasses live outside namespaces entirely. So the two halves of "stop people using too much" sit on opposite sides of a boundary the reader already knows: you can quota a *team*, and you cannot quota a *machine*. Name that boundary out loud, because Chapter 12 will **derive** the RBAC four-way matrix from it rather than asking the reader to memorise four combinations.

**Close by connecting back to §2 in one clause.** Both of these are enforced at the admission gate. Neither is a separate subsystem. This is the chapter's first instalment of §8's claim and it should be stated as an observation, not as a promise.

- **Objectives**: D1.2
- **Concepts introduced**: `resource-quota`, `limit-range`, `namespaced-vs-cluster-scoped`
- **Sources**: `k8s-docs-namespaces-2026-08-23.md` (namespaces are a way to divide cluster resources between multiple users via resource quota; namespaces are for environments with many users across teams or projects; a Kubernetes resource can be in only one namespace). `k8s-docs-cloud-native-security-2026-08-23.md` (define ResourceQuotas to fairly allocate shared resources; use LimitRanges to ensure that Pods specify their resource requirements). `k8s-docs-cluster-administration-2026-08-23.md` (set up and manage resource quota for shared clusters). `k8s-docs-extending-kubernetes-2026-08-23.md` (ResourceQuota named as an API resource used for configuration rather than extension)
- ⚠ **SOURCE GAP — BLOCKING. See § Open questions #3.** What is cached supports the *contrast* and the *scope*, and nothing else. There is no cached statement of what a ResourceQuota can count (compute totals, object counts, storage), of the rule that once a quota exists in a namespace Pods must specify requests and limits, or of LimitRange's min/max/default structure. **A section built only on what is on disk today is three paragraphs and cannot carry two published cross-bearings.** `kubernetes.io/docs/concepts/policy/resource-quotas/` and `.../limit-ranges/` are the fetches
- **Figure**: `ch08-fig05-quota-vs-limitrange`
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `★ **Fixed Point:**` — ResourceQuota counts the **namespace**; LimitRange constrains the **object**. One is a ceiling on a team, the other is a rule about a manifest
  - `> 🪝 **Snag:**` — a LimitRange that supplies a default request changes what your manifest means without changing your manifest. The Pod you get is not the Pod you wrote, and `kubectl get pod -o yaml` is where you find out
  - `> ⚓ **Worth Securing:**` — the two are usually deployed together and for a reason. A quota with no LimitRange means one team member who omits requests can consume the namespace's whole allocation with a single Pod
- **Cross-bearings**: back to Ch 4 §6 (**mandatory — [B3]'s designated namespaces anchor** and the pinned "ResourceQuota" payoff; Chapter 4 named the mechanism and sent the reader here); back to Ch 7 §2 (**mandatory** — the pinned "quotas and limit ranges" payoff, and the complaint this section answers); back to Ch 5 §8 (requests and limits — the numbers a LimitRange defaults); back to **§2** (the gate that enforces both); forward to **§4** (the scope hinge); forward to Ch 12 (**mandatory** — namespaced vs cluster-scoped, from which the RBAC matrix is derived)
- ⚠ **Do not teach QoS classes.** Chapter 5 owns them. A LimitRange's defaults can change a Pod's QoS class, which is a true and tempting observation and is one clause at most
- ⚠ **Do not teach eviction under quota pressure.** Quota rejects at admission; it does not evict. Conflating the two creates a trap the chapter would then have to defuse

### §4 — 🔵 Taking a Node Out of Service

**Closes the loop §1 opened, and discharges `chapter-04` line 584, `chapter-07` line 408 and `chapter-07` line 702.** This is the section the reader has been waiting three sections for, and it should acknowledge that in its first line.

**First, where nodes come from**, in two sentences, because the reader has never been told. There are two ways a Node object appears: the kubelet on a node **self-registers** with the control plane, which is the default, or a human adds the Node object manually. After a Node object is created the control plane checks it is valid — that a kubelet has registered whose registration matches the object's `metadata.name` — and if the node is healthy it becomes eligible to run Pods. Node names must be valid DNS subdomain names and must be unique. This is a small block and it exists mainly so that §8's claim about writes-through-one-door has a node-side instance.

**Second, the three commands, which are the section's spine and the chapter's opening promise.**

- `kubectl cordon $NODENAME` marks a node unschedulable. It prevents the scheduler from placing new Pods onto that node and **does not affect the Pods already on it**. It is the preparatory step before a reboot or other maintenance.
- `kubectl drain` evicts the Pods that `cordon` deliberately left running.
- `kubectl uncordon` restores scheduling.

**The cordon/drain distinction is the section's Fixed Point** and it is exactly the shape the exam asks about. `cordon` alone is not maintenance-ready; a node that is cordoned is a node nothing new lands on and everything old keeps running on. Two commands, two different jobs, and the mistake is always the same direction — assuming `cordon` did what `drain` does.

**One exception worth naming**: Pods that are part of a DaemonSet tolerate being run on an unschedulable node. Chapter 6 taught DaemonSet as one-per-matching-node and Chapter 7 taught the built-in condition tolerations; this is where the two meet, and it is a free retrieval.

**Third, node conditions**, presented as a table because that is what they are: `Ready`, `DiskPressure`, `MemoryPressure`, `PIDPressure`, `NetworkUnavailable`. `kubectl describe node <name>` shows them. The one that carries an exam-relevant subtlety is `Ready`, which is **three-valued**: True if the node is healthy and accepting Pods, False if it is not, and **Unknown** if the node controller has not heard from the node within the node-monitor-grace-period. Unknown is the answer to Soundings question 6 and it is more interesting than either of the other two: it is the cluster admitting it cannot tell, which is a different claim from "the node is broken."

Round out the Node status shape in one sentence: a node's status also contains Addresses, Capacity and Allocatable, and Info. **Chapter 7 §2 pointed here for what makes Capacity and Allocatable differ — see § Open questions #6; that promise is only partially payable on the current source set.**

**Fourth, heartbeats and the node controller, which is where the control loop reappears.** There are two heartbeat forms: updates to a Node's `.status`, and Lease objects in the `kube-node-lease` namespace, one per node. Chapter 4 pointed at exactly these Leases and said they were how the control plane knows a node is alive. The node controller is a control-plane component that assigns a CIDR block at registration, keeps its node list in sync with the cloud provider's machine list, and monitors node health — updating `Ready` to Unknown when a node becomes unreachable and triggering API-initiated eviction of the node's Pods if it stays unreachable.

**Say plainly that the node controller is a control loop.** It observes, compares, and acts. The reader met the pattern in Chapter 3 and has seen five instances of it since. This is the sixth, and naming it as such costs one sentence and buys §8 half its argument.

**Do not state a duration for the grace period.** The source names the parameter and gives no value. See § Open questions #5.

- **Objectives**: D1.2
- **Concepts introduced**: `node-registration`, `node-self-registration`, `cordon`, `drain`, `uncordon`, `unschedulable-node`, `node-conditions`, `ready-condition`, `memorypressure`, `diskpressure`, `pidpressure`, `networkunavailable`, `node-heartbeats`, `node-lease`, `node-controller`, `api-initiated-eviction`, `node-monitor-grace-period`
- **Commands**: `kubectl-cordon`, `kubectl-drain`, `kubectl-uncordon`, `kubectl-describe`
- **Sources**: `k8s-docs-nodes-2026-08-23.md` (self-registration as the default versus manual Node creation; the control plane's validity check against `metadata.name`; DNS-subdomain naming and uniqueness; `kubectl cordon` marks unschedulable, prevents new Pods, does not affect existing Pods, is the preparatory step before reboot or maintenance; `kubectl drain` evicts; `kubectl uncordon` restores; DaemonSet Pods tolerate an unschedulable node; Node status contains Addresses, Conditions, Capacity and Allocatable, Info; the five conditions and the three-valued `Ready`; node-monitor-grace-period named; `kubectl describe node`; two heartbeat forms — status updates and Leases in `kube-node-lease`; the node controller's three jobs including API-initiated eviction). `k8s-docs-node-allocatable-2026-08-24.md` (Allocatable is the compute available for Pods; the scheduler treats Allocatable as available capacity and does not over-subscribe it — **and see its extraction note: no arithmetic relationship between Capacity and Allocatable is extractable**)
- **Figure**: `ch08-fig04-node-lifecycle-cordon-drain`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — `cordon` stops arrivals and touches nothing already aboard. `drain` clears what is aboard. `uncordon` reopens. Three commands, three jobs, and the maintenance sequence needs the first two
  - `> ⚠ **Navigational Hazards:**` — a cordoned node is not an empty node. If you reboot after `cordon` alone, every Pod on that node goes down with it. This is the most consequential single confusion in the chapter and it has a real operational cost
  - `> 🪢 **Mnemonic:**` — a cordon is a rope across the door. It stops people coming in. It does not remove the people already inside
  - `> 🔭 **Closer Look:**` — `Ready: Unknown` is not a fourth failure mode. It is the control plane declining to guess. The distinction matters when you are deciding whether to intervene: False means the node told you it is unhealthy; Unknown means nobody has heard from it, which could equally be a network partition
- **Cross-bearings**: back to **§1** (the command that opened the chapter, now fully explained); back to Ch 7 §4 (**mandatory** — `node.kubernetes.io/unschedulable` in the built-in taint family; `cordon` is that taint, applied deliberately, and this is the retrieval **[B3]** names for node conditions against scheduling); back to Ch 4 §6 (**mandatory — the pinned "node conditions and heartbeats" payoff**; the `kube-node-lease` namespace the reader was told connects forward); back to Ch 3 (the control loop — the node controller is one, and **[B3]**'s ≥4-back candidate); back to Ch 6 §7 (DaemonSet Pods tolerating an unschedulable node); back to **§3** (the scope hinge: quota is namespaced, a Node is not); forward to Ch 13 (**mandatory** — node health as a troubleshooting input, and the `Evicted` signature)
- ⚠ **Do not teach PodDisruptionBudgets or `--ignore-daemonsets`.** Neither is in the curriculum and neither is cached. `drain` gets one clause: it evicts
- ⚠ **Do not teach the `Evicted` Pod signature.** Chapter 13 owns Pod failure signatures and needs `Evicted` intact
- ⚠ **Do not state a node-monitor-grace-period value.** Name the parameter, not a number

### §5 — ⚪ Who Owns the Control Plane

**The chapter's arousal-restoration point (Part 2), deliberately placed after its hardest run**, and the section that makes §6 and §7 feel necessary rather than arbitrary. It is also the easiest material in Part II and should read that way — short, concrete, and unhurried.

**Open on the reframe, which is what earns this section its place.** Everything so far in this chapter has been something you *do*. This section is about something you *own*, and the two are not the same. The pivot question is Soundings #8's: which of the duties in this chapter are yours at all?

**Then the planning axes, as questions rather than as a taxonomy**, because the source presents them as questions and because a list of questions is a better read than a list of categories. Do you want to try Kubernetes on your own machine, or build a high-availability multi-node cluster? Hosted, or hosting your own? On-premises or in the cloud? Bare metal or VMs? Running a cluster, or developing Kubernetes itself? Five questions, and the honest observation that the answers are mostly determined by circumstance rather than chosen.

**Then the tools, split by the axis that matters.** For **learning**: minikube runs a single- or multi-node local cluster; kind runs local clusters using Docker containers as nodes ("Kubernetes IN Docker"). For **production self-management**: kubeadm is the officially supported tool for creating clusters — installing the control plane and joining nodes — and k3s is a lightweight distribution. Alongside these, managed and turnkey certified services from cloud providers, where you hand the control plane to a provider.

**One requirement that is not optional in any of these cases**, and it is a free ≥4-back retrieval: a container runtime — containerd or CRI-O — must be installed on every node, and `kubectl` is the command-line tool for managing any cluster regardless of how it was built. Chapter 2 taught the CRI boundary six chapters ago and this is the first time it has been operationally consequential. Use it; **[B3]** designates the Ch 2 CRI boundary as this chapter's ≥4-back spacing-floor candidate.

**Close on the ownership consequence, which is the section's whole point and the bridge into §6 and §7.** A managed control plane means the provider decides when you upgrade and holds the etcd backup. A self-hosted control plane means both are yours. The next two sections are, precisely, the two duties that move: **which versions are allowed to disagree** (§6), and **what you cannot get back** (§7). Say it in one sentence and let the sections do the rest.

Also collect `chapter-07` line 945 here, in one clause: scheduler profile configuration lives in the control plane's own component configuration, which is a thing you can reach only if you own the control plane.

- **Objectives**: D1.2
- **Concepts introduced**: `cluster-planning-axes`, `managed-kubernetes`, `self-hosted-cluster`, `kubeadm`, `minikube`, `kind`, `k3s`
- **Sources**: `k8s-docs-cluster-administration-2026-08-23.md` (the planning questions verbatim: local versus HA multi-node, hosted versus self-hosted, on-prem versus IaaS, bare metal versus VMs, running versus developing; and "familiarize yourself with the components needed to run a cluster"). `k8s-docs-setup-tooling-2026-08-23.md` (minikube and kind for learning environments; the production evaluation frame of what to manage versus hand to a provider; managed/turnkey certified services; kubeadm as the officially supported tool for creating clusters, installing the control plane and joining nodes; k3s as a lightweight distribution; a container runtime — containerd or CRI-O — must be installed on every node; kubectl manages any cluster)
- **Figure**: none. Five planning questions and four tool names have no spatial or temporal structure, and a four-box "tooling landscape" diagram would be decorative — Part 18.9's explicit no-illustrate case. The chapter's five reference figures are all elsewhere and this section is deliberately the light one
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2**
- **Markers planned**:
  - `> ⚓ **Worth Securing:**` — kind and minikube are not toys with a different name for the same thing. kind runs nodes as containers, which makes it fast to create and destroy and makes it the usual choice for CI; minikube runs a local cluster with a broader set of addons, which makes it the usual choice for learning
  - `> **Logbook Entry:**` — sidebar. The honest version of the managed-versus-self-hosted decision as practitioners actually experience it: the control plane is not the expensive part, the operational calendar is. Keep it oriented at the practitioner's experience (Part 14 subject dignity), and do not turn it into vendor advocacy in either direction
- **Cross-bearings**: back to Ch 2 (**mandatory — [B3]'s ≥4-back spacing-floor item**; the CRI runtime that must exist on every node, six chapters back and operationally consequential for the first time); back to Ch 3 (the control-plane components you are choosing whether to own); back to Ch 7 §6 (**mandatory** — the pinned "cluster administration" payoff for where scheduler profile configuration lives); forward to **§6** and **§7** (the two duties that move)
- ⚠ **Do not evaluate or rank the tools.** The exam tests recognition — which tool is for learning, which is the officially supported bootstrapper. Comparative recommendations are out of scope and age badly
- ⚠ **Do not teach the CNCF certified-distribution programme.** Chapter 17 owns CNCF programmes and landscape

### §6 — 🟡 Versions That Are Allowed to Disagree

**The densest pure-recall block in the book (**[B3]**), and the chapter's second high-attention section.** It is also the section most likely to be mis-drafted, because the material is a table and the temptation is to print the table and move on. The table has to be *derived* from one rule or the reader will not retain it past the chapter.

**Open with the rule that generates most of the table**, before any numbers: **nothing may be newer than the API server it talks to.** Every component in the cluster is a client of one door, and a client that is newer than its server may ask for things the server has never heard of. That single sentence covers the kubelet, kube-proxy, the controller-manager, the scheduler and the cloud-controller-manager. Then the numbers become the *sizes of the windows*, not five unrelated facts.

**Then the versioning vocabulary**, in two sentences. Kubernetes versions are `x.y.z` — major, minor, patch — following Semantic Versioning terminology. The project maintains release branches for the most recent **three** minor releases; 1.19 and newer receive approximately one year of patch support, with applicable fixes including security fixes backported to those three branches depending on severity and feasibility.

**Then the cadence**, which is the fact that makes the three-branch rule intelligible: since 2021 the project ships **three minor releases per year**, roughly every fifteen weeks, with patch releases cut monthly from the supported branches. Three releases a year and three supported branches is approximately a one-year window, which is exactly the patch-support figure. **[B3]** schedules Ch 17 to retrieve cadence beside the three-minor rule for exactly this reason: each explains the other and neither survives alone.

**Then the skew table itself, as Dead Reckoning.** This is the chapter's mandatory facts-only block. No watch-standing register, no metaphor, no framing — the reader wants this material flat and scannable, and the contract requires one such block per chapter. State it as five rows:

| Component | Rule |
|---|---|
| kube-apiserver (HA) | Newest and oldest instances within **one** minor version of each other |
| kubelet | Never newer than kube-apiserver; up to **three** minors older |
| kube-proxy | Never newer than kube-apiserver; up to three minors older; up to three older **or newer** than the kubelet beside it |
| controller-manager / scheduler / CCM | Never newer than the API servers they talk to; expected to match, may be **one** minor older to allow live upgrade |
| **kubectl** | Within **one** minor version, **older or newer** |

**Then the exception, which is where the exam points are.** `kubectl` is the only entry in the table permitted to be *newer* than the API server. Every intuition the reader built in the first half of the section says never-newer, and for one component that intuition is wrong. This is B1 trap #28 and it is worth its own callout: the reason kubectl is the exception is that it is a user tool outside the cluster rather than a component inside it, which also explains why its window is symmetric.

**Close on the upgrade order that falls out of the rules**, in two sentences. If nothing may be newer than the API server, the API server is upgraded first and everything else follows. Do not extend this into an upgrade procedure — the derivation is the point, not the runbook.

- **Objectives**: D1.2
- **Concepts introduced**: `semantic-versioning`, `supported-releases`, `three-supported-minors`, `patch-support-window`, `version-skew`, `upgrade-order`, `release-cadence`
- **Sources**: `k8s-version-skew-policy-2026-08-23.md` (x.y.z and Semantic Versioning; release branches for the most recent three minor releases; 1.19+ ~1 year of patch support; backporting depends on severity and feasibility; all five skew rules verbatim, including the kubelet three-minor window with the <1.25 two-minor caveat, kube-proxy's relationship to its kubelet, and kubectl's symmetric one-minor window). `k8s-releases-cadence-2026-08-23.md` (three minor releases per year since 2021, ~every 15 weeks, SIG Release; monthly patch releases; ~1 year patch support for 1.19+, ~9 months for 1.18 and older; the currently-supported roster with EOL dates as of the snapshot)
- **Figure**: `ch08-fig03-version-skew-window`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — nothing may be newer than the API server. kubelet may be three minors older. **`kubectl` is the single exception in both directions, at one minor.**
  - `> **Dead Reckoning:**` — **mandatory contract element**, and this is its home. The five-row table, stated flat, with no register and no metaphor. If the drafting stage puts Dead Reckoning anywhere else in this chapter it has chosen worse
  - `> ⚠ **Navigational Hazards:**` — the kubelet rule and the kubectl rule are different rules and candidates apply the first to the second. kubelet: three minors, older only. kubectl: one minor, either direction. B1 trap #28
  - `> 🪢 **Mnemonic:**` — *three back, three a year, three branches.* The kubelet's window, the release cadence, and the number of supported minors are all three, which is a coincidence and a useful one
  - `> 🪝 **Snag:**` — "Kubernetes supports the last two releases" is a common half-memory. It is **three**. B1 trap #29
- **Cross-bearings**: back to Ch 3 (the components in the table, each of which the reader can now name); back to **§5** (this is a duty that moves — on a managed control plane the provider owns the upgrade calendar); forward to Ch 13 (**mandatory [B3] decay anchor** — version skew as a troubleshooting cause); forward to Ch 17 (**mandatory [B3] decay anchor** — release cadence beside the three-supported-minors rule, inside the KEP and SIG Release material)
- ⚠ **The version numbers in the sources are dated data and must be handled as such.** The snapshot names 1.36, 1.35 and 1.34 with specific EOL dates. **Teach the rule and illustrate it with the numbers, marked as of the snapshot date** — the same discipline **[B3]** applies to the CNCF graduated-project roster (do-not-retrieve item #2). A reader studying eight months after publication will have three different numbers and the same rule. Never let a Practice Question turn on the specific minor version
- ⚠ **Do not teach feature gates or the alpha/beta/stable stages.** See § Open questions #8 — the recommendation is that Chapter 17 owns them alongside KEPs, where the graduation story makes them one idea instead of two
- ⚠ **Do not write an upgrade runbook.** kubeadm upgrade procedures are not in the curriculum and are not cached

### §7 — 🔵 The One Backup That Matters

**Short, and the chapter's only irreversible-consequence material.** Discharges `chapter-03` line 408.

**Open on the fact that gives the section its weight**, which Chapter 3 already gave the reader: all Kubernetes objects are stored in etcd. Everything in this book that the reader has written down — every Deployment, every ConfigMap, every Secret, every Node object — is one datastore's contents. Periodically backing up etcd data is important to recover clusters under disaster scenarios such as **losing all control-plane nodes**. That is the scenario; name it concretely.

**Then the mechanics, briefly.** Two ways to back up: a built-in snapshot (`etcdctl snapshot save`), or a volume snapshot of etcd's storage. Restore uses `etcdutl snapshot restore`, which operates directly on the data files, after which the control-plane components are restarted against the restored data directory. Two commands and one sentence about what restore actually is. **Do not teach the TLS flags** — the `etcd-access-control` snapshot explicitly notes that the page's TLS configuration guidance was not verbatim-verified, so `--cacert`, `--cert` and `--key` may be named as existing (the backup snapshot does list them) but no configuration guidance may be given.

**Then the security fact, which is the section's Fixed Point and is more examinable than the commands.** The snapshot file contains all the Kubernetes state and critical information — so keep it encrypted and store it outside the control-plane nodes. And the sharper statement from the access-control guidance: **access to etcd is equivalent to root permission in the cluster, so ideally only the API server should have access to it.** Those two facts together say something the reader should feel: an unencrypted etcd snapshot sitting on a control-plane node is both a backup and a complete compromise waiting to be copied.

**Close by connecting to §5 in one clause.** On a managed control plane this is the provider's job and you may not even be able to reach etcd. On a self-hosted cluster it is yours, and it is the one duty in this chapter where the consequence of skipping it is not recoverable by doing it later.

- **Objectives**: D1.2
- **Concepts introduced**: `etcd-backup`, `etcd-snapshot`, `etcd-access-equals-root`, `disaster-recovery`
- **Commands**: `etcdctl-snapshot-save`, `etcdutl-snapshot-restore`
- **Sources**: `k8s-docs-etcd-backup-2026-08-23.md` (all Kubernetes objects are stored in etcd; periodic backup is important for disaster recovery such as losing all control plane nodes; the snapshot file contains all Kubernetes state and critical information, keep it encrypted and store it outside the control plane nodes; two backup methods — `etcdctl snapshot save backup.db` and a volume snapshot; restore via `etcdutl snapshot restore` operating directly on the data files; control-plane components restarted against the restored data directory). `k8s-docs-etcd-access-control-2026-08-24.md` (etcd is a consistent and highly-available key value store used as Kubernetes' backing store for all cluster data; **access to etcd is equivalent to root permission in the cluster so ideally only the API server should have access to it**)
- **Figure**: none. Two commands and a warning have no structure worth drawing, and a backup/restore flow diagram would restate the prose (Part 18.7 redundancy). The chapter's figure budget is better spent on `fig03` and `fig05`, both of which are reference material
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `★ **Fixed Point:**` — every object you have ever created lives in etcd. Access to etcd is equivalent to root in the cluster. A snapshot is therefore both your only disaster recovery and your most dangerous single file
  - `> ⚓ **Worth Securing:**` — "store it outside the control plane nodes" is the whole point of the sentence. A snapshot that lives only on the machines it protects against losing is not a backup
  - `> 🔭 **Closer Look:**` — restore is not a command you run against a running cluster. `etcdutl snapshot restore` operates on the data files directly, and the control-plane components come back up against the restored directory. That is why restore is a maintenance event rather than an operation
- **Cross-bearings**: back to Ch 3 §2 (**mandatory — the pinned "etcd backup and restore in practice" payoff**; Chapter 3 introduced etcd as the store and pointed here); back to Ch 4 (every object the reader has written is what is in the snapshot); back to **§5** (whose job this is); back to **§2** (only the API server should reach etcd — which is the same single-door architecture, stated from the other side); forward to Ch 12 (Secret hardening and encryption at rest — the reason "keep it encrypted" is not paranoia)
- ⚠ **Do not teach encryption at rest.** Chapter 12 owns it, and it is one of that chapter's better beats. One clause naming the connection is the ceiling
- ⚠ **Do not give TLS configuration guidance.** The flags may be named as existing; their configuration was not verbatim-verified in the cached snapshot

### §8 — ☀️ Rules, or Consequences

**The chapter's one Zenith**, and the payoff for the curiosity gap opened in Why This Chapter Matters. Short — this section makes one claim and demonstrates it.

**The claim: you did not learn a single new mechanism in this chapter.** Every administrative act in it is a write through the one door, reconciled by a controller you already met.

**The demonstration, in the chapter's own order**, each item one or two sentences:

- **§1.** `kubectl` is a client of the API server. Chapter 3's single door, addressed by a command-line tool.
- **§2.** The three gates are not a subsystem. They are what the single door does before it writes anything down. Chapter 3 told you every request terminates at the API server; this is the "and then what" of that sentence.
- **§3.** A ResourceQuota is an object. You `apply` it like any other. It takes effect because an admission controller reads it at the gate — so a quota is a declaration that changes what other declarations are allowed to say.
- **§4.** **This is the strongest instance and it should be the one that lands.** `kubectl cordon` does not have a special channel to the node. It writes a field on a Node object. Chapter 7's built-in taint machinery — the `node.kubernetes.io/unschedulable` taint the reader met in a table, with a `NoSchedule` effect — was already watching for exactly that. The scheduler then does what the scheduler always does. Nothing about `cordon` is new; it is Chapter 7's mechanism with an operator's hand on it.
- **§4, again.** The node controller observes heartbeats, compares against desired state, and acts. It is a control loop. It is the sixth one in this book.
- **§6.** The skew rules are the compatibility contract of the same one door. Every rule in the table is about which clients that door will accept.
- **§7.** etcd is what is behind the door, and the reason only the API server should reach it is the same reason there is only one door.

**Then the reframe that gives the chapter its title and closes the Voyage-Ahead promise Chapter 7 made.** Chapter 7 said Chapter 8 is where the rules turn into consequences. That is the sentence to land on: a list of administrative rules is unmemorable, and a set of consequences of one architecture is not. If the reader can hold "one door, and controllers behind it", they can regenerate most of this chapter without having memorised it — and the parts they cannot regenerate (the skew numbers) are exactly the parts §6 flagged as needing memorisation.

**Be honest about the exception**, because the claim overclaims slightly and the reader will notice. §5 and §6 are not consequences of the architecture; they are facts about the project. Say so. A Zenith that quietly excludes its counterexamples is a slogan, and Chapter 4 §6 already established this book's habit of narrowing a slogan until it is true.

- **Objectives**: D1.2
- **Concepts introduced**: none. Synthesis only
- **Sources**: none new. Every claim retrieves a source already cited in §1–§7 or in Chapters 3, 4, 6 and 7
- **Figure**: `ch08-zenith-consequences-not-rules`
- **Checkpoint after**: no
- **Markers planned**:
  - `☀️ **Zenith:**` — one door, and behind it controllers you have already met. Everything in this chapter is a write to the first, reconciled by the second
  - `> ⚓ **Worth Securing:**` — the practical form: when you meet a Kubernetes administrative feature this book has not covered, the first question is *what object does it write* and the second is *what controller is watching*. Those two questions answer most of them
- **Cross-bearings**: back to §1–§7 (each demonstration item); back to Ch 3 §2 and §5 (the single door and the control loop — the two ideas this section is built from); back to Ch 7 §4 (the taint `cordon` writes); forward to Ch 12 (the same door, with its locks examined properly); forward to Ch 17 (the extension points, which are the door's documented seams)
- ⚠ **Do not introduce anything.** A Zenith that teaches is a ninth section. This one recognises

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 15 questions total.** B4 allocates 10 and names Chapter 8 **first** on its list of chapters expected to exceed the minimum ("kubectl surface / API gates / node lifecycle / version skew — four unrelated arcs"). The arc outline carries that as 12–15. Set at 15 across three checkpoints of 5, matching the shape Chapters 3 through 7 shipped. Chapter total moves 35 → 40.

The structural case for three rather than two: the chapter has three separable modes, and they map cleanly onto the section blocks. #1 covers the request path (§1–§3) — how a command gets in and what can stop it. #2 covers the machine and its ownership (§4–§5) — what you can do to a node and whether it is yours. #3 covers the two duties that cannot be improvised (§6–§7) — versions and disaster. Folding to two would put §6's recall block in the same checkpoint as §4's procedures, which is the exact adjacency the Attention Budget split is designed to avoid.

**Retrieval-practice content: 20%** **[B3]** — drawn from **Chapters 2 through 7**, with the **≥4-back spacing floor now active** for the first time in the book. Against a combined Bearings-plus-Practice pool of 32, the 20% target is ~6–7 items, allocated **3 in Bearings and 4 in Practice** (7 of 32 = 21.9%), matching Chapter 7's allocation. Chapter 1 is excluded from the retrieval schedule entirely and no item may test exam mechanics.

Each of **[B3]**'s named anchors has exactly one place it belongs:

| **[B3]** named anchor | Placement | Why here |
|---|---|---|
| **Namespaces (Ch 4) under ResourceQuota** | Bearings #1, item 5 | §3 is the payoff for a published cross-bearing Chapter 4 dropped by name. The retrieval and the discharge are the same beat |
| **Node conditions against scheduling (Ch 7)** | Bearings #2, item 1 | §4's `cordon` *is* Chapter 7's `unschedulable` taint. Asking immediately after §4 is the shortest gap between teaching and retrieval, so this item must be the hard version — the identity, not the definition |
| **≥4-BACK FLOOR: the CRI boundary (Ch 2)** | Bearings #2, item 4 | §5 states that a container runtime must be installed on every node, which is the first time Chapter 2's CRI boundary has been operationally consequential. **Six chapters back** — the floor requires ≥4 and this comfortably clears it |

**On the ≥4-back floor.** **[B3]** activates it at this chapter specifically to stop the schedule degenerating into "test the previous chapter." Bearings #2 item 4 satisfies it. Practice carries a second ≥4-back item (Ch 3's control loop, five back) as redundancy, because this is the floor's first live chapter and a single item is a single point of failure.

### ☆ Taking Your Bearings #1 — after §3

- **Topic**: the path a command takes in, and the two things that can refuse it
- **Questions**: 5
- **Retrieval from earlier chapters**: 1 of 5 (**[B3]** named anchor)
- **Difficulty**: ⚪ for items 1–2, 🔵 for 3–5

  1. Decompose `kubectl describe node worker-3` into its four slots and name each one. Then say which of the four you could change the capitalisation of without breaking the command. **Correct answer: command / TYPE / NAME / flags; the type is case-insensitive and abbreviable, the name is not.** **Tests §1's Fixed Point directly.** Trap answers should include a version claiming both are case-insensitive and one claiming both are case-sensitive.
  2. You run `kubectl get pods` from a shell on your laptop and from inside a running Pod. Both succeed and return different results. Explain both differences — what identity each used, and what namespace each looked in. **Correct answer: the laptop used the kubeconfig at `$HOME/.kube/config` and its context's namespace; the in-cluster invocation detected the two environment variables and the ServiceAccount token file, authenticated as the ServiceAccount, and looked in the ServiceAccount's namespace.**
  3. 🔵 Name the three gates a request passes in order, and say which of them can result in the request being *changed* rather than accepted or rejected. **Correct answer: authentication, authorization, admission; only admission can mutate.** **This is the chapter's single most examinable item.** Trap answers must include a two-gate version (the most common incomplete model, and the one Soundings #3 predicted), a version with the order reversed, and a version attributing mutation to authorization.
  4. 🔵 A request is refused. You are told the identity was valid and the identity had permission to perform this action on this resource. Which gate refused it, and give one plausible reason. **Correct answer: admission; e.g. it violated a ResourceQuota, or a policy plugin rejected the object's contents.** Tests whether the reader can use the gate model diagnostically rather than recite it.
  5. 🔵 **Retrieval from Ch 4 §6 — namespaces.** Chapter 4 said namespaces are the unit by which cluster resources get divided between users, and named the mechanism. Name it, say what scope it constrains, and then say what the *other* mechanism in §3 constrains instead. **Correct answer: ResourceQuota, namespace-aggregate; LimitRange, individual objects.** **[B3]** named anchor and the published Chapter 4 payoff appearing as an assessment item.

- **Answer-key requirement**: item 3's key must state the mutate/reject distinction as the *reason there are three gates rather than one*, not merely as a property of the third. That framing is what makes Chapter 12's Pod Security Admission derivable rather than memorisable, and **[B3]** designates that handoff as mandatory.
- **Answer-key requirement**: item 4's key must not enumerate admission controllers. Naming one plausible cause is enough; the full plugin surface is out of scope and Chapter 12 owns the policy-engine landscape.

### ☆ Taking Your Bearings #2 — after §5

- **Topic**: taking a machine out of service, and finding out whose machine it is
- **Questions**: 5
- **Retrieval from earlier chapters**: 2 of 5 (one **[B3]** named anchor, one **≥4-back floor item**)
- **Difficulty**: 🔵 throughout, with item 2 at 🟡

  1. **Retrieval from Ch 7 §4 — the built-in taint family.** Chapter 7 listed `node.kubernetes.io/unschedulable` with a `NoSchedule` effect among the built-in condition taints, and noted it is applied deliberately rather than by a failing component. What command applies it, and — using Chapter 7's rule about that effect — what happens to the Pods already running on the node? **Correct answer: `kubectl cordon`; nothing happens to them, because `NoSchedule` affects only new placements.** **[B3]** named anchor, deliberately written as the identity between the two chapters rather than as a definition.
  2. 🟡 An engineer cordons a node and immediately reboots it for maintenance. Three services go down. What did they skip, and why did the cordon not prevent this? **Correct answer: they skipped `drain`; `cordon` stops new Pods arriving and deliberately leaves running Pods alone.** **This is the chapter's designated struggle item** — label it as such per Part 10B and normalise the difficulty. The intuitive reading of "take a node out of service" is that it empties the node, and the reader should be told that expecting that is reasonable and wrong.
  3. A node stops responding. Its `Ready` condition changes. To what value, and what does that value mean that "False" would not? **Correct answer: Unknown — the node controller has not heard from the node within the grace period; False would mean the node reported itself unhealthy.** Trap answers must include False and NotReady.
  4. **Retrieval from Ch 2 — the container runtime. [≥4-BACK FLOOR ITEM]** You bootstrap a cluster with kubeadm. Before any node can run a Pod, one piece of software must already be installed on it that kubeadm does not provide. Name it, name the two named implementations, and say which interface Kubernetes uses to talk to it. **Correct answer: a container runtime; containerd or CRI-O; the CRI.** **Six chapters back.** This item exists to satisfy **[B3]**'s spacing floor and it is a good item on its own merits — it is the first point in the book where Chapter 2's CRI boundary has an operational consequence.
  5. Two engineers describe their clusters. One says "we upgraded to 1.36 last Tuesday"; the other says "we got upgraded to 1.36 last Tuesday." What is different about their situations, and name one further duty that differs. **Correct answer: self-hosted versus managed control plane; etcd backup is the standard second answer, upgrade scheduling the first.** Sets up §6 and §7 as consequences rather than topics.

- **Note on the retrieval concentration.** Two of the chapter's three Bearings retrieval items land in this checkpoint. That is correct rather than convenient: both anchors belong to §4 and §5 and nowhere else, and spreading them for an even per-checkpoint rate would place each where it does not belong. The chapter's overall rate is 21.9%, which is the figure the contract specifies.
- **Answer-key requirement**: item 2's key must state the cordon/drain division as an operational rule and must not moralise about the mistake. The scenario is a real outage with real users behind it; per Part 14's subject-dignity guardrail, the wry register stays oriented at the practitioner's reasonable-but-wrong expectation, not at the consequences borne by the people whose services went down.

### ☆ Taking Your Bearings #3 — after §7

- **Topic**: the two things you cannot improvise — versions, and what you cannot get back
- **Questions**: 5
- **Retrieval from earlier chapters**: 0. The chapter's 20% is met by Bearings #1 item 5, Bearings #2 items 1 and 4, and four Practice items. A fourth Bearings retrieval would push this checkpoint off its own topic, and this topic is the one **[B3]** says is most at risk of decaying
- **Difficulty**: 🔵, with items 2 and 4 at 🟡

  1. Your cluster's API servers are at 1.36. For each of these, say whether it is supported: a kubelet at 1.33; a kubelet at 1.37; a `kubectl` at 1.37; a kube-scheduler at 1.34. **Correct answers: supported (three minors older is the limit); not supported (never newer); supported (one minor newer is allowed for kubectl only); not supported (scheduler may be at most one minor older).** **The chapter's densest recall item and the one closest to an actual exam question.**
  2. 🟡 State the one rule that generates four of the five rows of the skew table, and then name the row it does not generate and say why that row is different. **Correct answer: nothing may be newer than the API server; `kubectl` is the exception because it is a user tool outside the cluster rather than a component inside it.** Tests whether the reader derived the table or memorised it — and the derivation is what survives to exam day.
  3. How many minor releases does the project maintain release branches for, roughly how long is patch support, and roughly how many minor releases ship per year? Then say why those three numbers are consistent with each other. **Correct answers: three; approximately one year for 1.19 and newer; three per year — three releases a year across three branches is about a year of coverage.** **[B3]** schedules Ch 17 to retrieve cadence beside the three-minor rule for exactly this reason; this item is where the connection is first made.
  4. 🟡 You lose every control-plane node. Your worker nodes are untouched and your applications are still serving traffic. What have you actually lost, and what single artefact would let you get it back? **Correct answer: the cluster's entire record of intent — every object, since all Kubernetes objects live in etcd; an etcd snapshot.** The scenario is deliberately constructed so the reader must notice that running workloads and cluster state are different things.
  5. An etcd snapshot is sitting unencrypted on one of your control-plane nodes. Give two separate reasons this is wrong. **Correct answers: it is not stored outside the nodes it protects against losing, so it does not survive the disaster it exists for; and access to etcd is equivalent to root in the cluster, so an unencrypted snapshot is a complete compromise in one file.**

- **Answer-key requirement**: item 1's key must not turn on the specific version numbers. State the rule for each row and note that the numbers illustrate it as of this book's snapshot. Version rosters age; the rules do not, and a reader studying a year from now must not be able to get this item wrong for the right reason.
- **Answer-key requirement**: item 3's key must name the forward connection explicitly — that Chapter 17 will meet the release cadence again inside the project's governance material, where the two facts explain each other. **[B3]** designates this as one of the book's three mandatory decay fixes, and the key is the cheapest place to install the pointer.

---

## 6. Exam Alert plan

**High-priority topics** — the ten most likely to be tested directly, in descending order of confidence:

1. **The three gates in order** — authentication, then authorization, then admission.
2. **Only admission can change the request.** The other two accept or refuse.
3. **kubelet may be three minors older than kube-apiserver and must never be newer.**
4. **`kubectl` is the only component permitted to be newer**, within one minor either way.
5. **Three supported minor releases**, ~1 year of patch support, ~3 minor releases a year.
6. **`cordon` stops arrivals; `drain` evicts.** A cordoned node is not an empty node.
7. **`Ready` is three-valued.** Unknown means the control plane has not heard from the node.
8. **ResourceQuota is namespace-aggregate; LimitRange is per-object.**
9. **`kubectl [command] [TYPE] [NAME] [flags]`** — types case-insensitive and abbreviable, names case-sensitive.
10. **All objects live in etcd; access to etcd is equivalent to root in the cluster.**

**Common traps to call out.** B1 traps #27, #28 and #29 are all `[source]`-tagged, so all three may be described as things candidates get wrong. **None is `[inferred]`, so no hedging is required** — and equally, none may be dressed with invented frequency figures (Part 14 guardrail #8, and **[B3]**'s fourth do-not-retrieve rule).

| B1 # | Trap | Where it is defused |
|---|---|---|
| 27 | "kubelet must match the API server version" | §6 opening rule, Bearings #3 item 1 |
| 28 | Applying the kubelet skew rule to kubectl | §6 Navigational Hazards, Bearings #3 items 1 and 2 |
| 29 | "Kubernetes supports the last two minor releases" | §6 Snag, Bearings #3 item 3 |
| 14 | "Everything lives in a namespace" | §3's scope hinge — retrieved from Ch 4 rather than re-taught, and used to set up Ch 12 |

**Seven non-B1 traps worth adding**, all visible now that G26, G27 and G28 have closed. B1 catalogued this competency's operational material as blocking gaps and therefore had no source to catalogue traps from:

- **"`cordon` takes the node out of service."** It stops new Pods; it does not move the ones already there. **This is the chapter's most valuable non-B1 trap** — it has a real operational cost, it is stated explicitly in the cached source, and it has one clean correct answer. §4's Navigational Hazards and Bearings #2 item 2.
- **"Authorization and admission are two words for the same check."** Authorization has no opinion about the request's contents; admission has no opinion about your identity. §2's Navigational Hazards.
- **"`Ready: False` is what an unreachable node reports."** An unreachable node reports `Unknown`; `False` is a node that reported itself unhealthy. §4, Bearings #2 item 3.
- **"A ResourceQuota limits how big any one Pod can be."** That is LimitRange. Quota is an aggregate ceiling on the namespace. §3, Bearings #1 item 5.
- **"`kubectl` inside a Pod behaves the same as on your laptop."** It detects in-cluster conditions, authenticates as the ServiceAccount, and defaults to the ServiceAccount's namespace. §1's Snag, Bearings #1 item 2.
- **"Resource names are case-insensitive because resource types are."** Types are; names are not. §1's Fixed Point.
- **"An etcd snapshot on the control-plane node is a backup."** It is a copy that dies with the thing it was protecting — and, unencrypted, a root-equivalent credential. §7, Bearings #3 item 5.

**Do not include** in the Exam Alert: RBAC roles and bindings, Pod Security Standards, encryption at rest, or the policy-engine landscape (all Ch 12); `kubectl top`, `events`, `logs --previous`, node health as a diagnostic workflow, or any Pod failure signature (Ch 13); `kubectl debug`, `port-forward`, ephemeral containers (Ch 16); KEPs, feature stages, SIG Release, the CNCF certification ladder (Ch 17); metrics-server (Ch 13 and Ch 18); Konnectivity and SSH tunnels (above tier — see § Open questions #7).

---

## 7. Practice Questions plan

**17 questions** (B4 allocation, unchanged). Distribution follows exam-point density rather than section count — §5 is a full section but carries almost no examinable surface, while §6 is one section carrying four of the chapter's ten priority topics:

| Block | Questions | Notes |
|---|---|---|
| §1–§2 — the grammar, kubeconfig, the three gates | 5 | Includes **1 retrieval item**. At least 3 must be about the gates; the gate sequence is the chapter's highest-value block and five questions on §1's grammar would be a waste of the allocation |
| §3 — quota and limit range | 2 | Includes **1 retrieval item**. Two is right for a section whose examinable content is one contrast, and it rises to 3 if the § Open questions #3 fetch lands and the section grows |
| §4 — node lifecycle and conditions | 3 | Includes **1 retrieval item**. Must include one item where the correct answer is a *sequence* of commands rather than a single command |
| §5 — ownership and bootstrap tooling | 2 | Pure recognition. Which tool is for learning, which is the officially supported bootstrapper, what moves when the control plane is managed |
| §6 — versions and skew | 4 | Includes **1 retrieval item**. **No question may turn on a specific minor version number.** At least 2 must require applying a rule to a scenario rather than reciting the rule |
| §7 — etcd | 1 | One question, and it should be the security one rather than the command one |

**Retrieval allocation: 4 of the 17 draw from Chapters 2–7**, allocated *within* this count and not added to it:

- **The control loop** (Ch 3 §5) — §4 block. **[≥4-back, five chapters]**, carried as redundancy for the floor's first live chapter. Framed as a discrimination item: *the node controller notices a node has stopped reporting and evicts its Pods. Name the pattern, and name two earlier components in this book that work the same way.* Correct answer: the control loop; any two of the workload controllers from Chapter 6, or the scheduler's watch from Chapter 7.
- **spec versus status** (Ch 4 §4) — §1–§2 block. Framed forward rather than backward: *`kubectl cordon` writes something. Is it a `spec` field or a `status` field, and how do you know?* Correct answer: `spec` — it is a statement of desired state, and Chapter 4 established that `status` is written by the system, not by you. This item is doing double duty as a retrieval and as §8's argument tested before §8 makes it.
- **Namespaced versus cluster-scoped** (Ch 4 §6) — §3 block. Deliberately framed differently from Bearings #1 item 5, which asks about the quota/LimitRange contrast: this one asks *why you cannot write a ResourceQuota that limits how many Nodes a team may use.* Correct answer: Nodes are not namespaced, and a ResourceQuota constrains a namespace.
- **Requests and limits** (Ch 5 §8) — §6 block or §3 block, drafter's choice. Framed as: *a LimitRange supplies a default request to a Pod whose manifest specified none. Chapter 5 said one of requests and limits is read by the scheduler. What just changed about where this Pod can be placed?* Correct answer: it can now be filtered out of nodes it would previously have fitted, because it now books capacity it did not book before.

**Interleaving strategy.** At least **four** questions must require two sections at once:

- **Gates + quota (§2 + §3)** — a Pod manifest that would exceed its namespace's quota. Which gate refuses it, and does the refusal depend on who submitted it?
- **Grammar + node lifecycle (§1 + §4)** — given only the four-slot grammar and the sentence "take node worker-3 out of service and clear it", produce the two commands in order.
- **Ownership + versions + etcd (§5 + §6 + §7)** — for a managed control plane and a self-hosted one, say which of the chapter's duties are yours in each case. This is the item that makes §5 examinable.
- **Everything + §8** — an administrative action the chapter did not cover. What object does it write, and what is watching? The correct answer is the *method*, not a fact, and it is the only question in the set that tests the Zenith.

**Trap-answer requirement** (skill Part 11): every wrong option must target a specific misconception and the answer key must explain why each is wrong. For the §6 block, wrong options should be drawn from B1 traps #27–#29 in their exact wrong form — particularly #28, which must appear at least twice in two different question shapes, because applying the kubelet rule to `kubectl` is the chapter's most durable error. For the §4 block, the cordon-empties-the-node misconception must appear as a distractor at least once in addition to its Bearings appearance.

**One calibration note.** This chapter's failure mode as a question set is the opposite of Chapter 7's. Chapter 7 risked seventeen enumeration items; this chapter risks seventeen *lookup* items — which version, which command, which gate — because the material genuinely is a set of lookups. Pure lookup should account for no more than six of the seventeen, and §6 is the only section where lookup items are unavoidable (and even there, item 2 of Bearings #3 shows the derivable alternative). The high-value question modes here are **application** ("given this cluster, is this supported") and **diagnosis** ("which gate refused this, and how do you know"). A question that can be answered by pattern-matching a number against a table has tested the reader's short-term memory of a table.

---

## 8. Required figures

Six anchors, exactly as the arc outline specifies. §5 and §7 deliberately carry none — see each section's Figure line for the Part 18.3/18.7/18.9 reasoning.

**A note on this chapter's figure register.** Five of the six are *reference* diagrams rather than dramatic illustrations, and that is correct for the most reference-shaped chapter in Part II. `ch08-fig03` and `ch08-fig05` in particular are utilitarian by design — the same posture Chapter 7 took with `ch07-fig03`. Only the Zenith carries the brand's illustrative register. Do not let the illustrator dress the reference figures up; their job is to be scanned, and two of them are going into The Lodestar.

### `ch08-fig01-kubectl-verb-resource-grammar`

- **Purpose**: §1's Fixed Point, dual-coded. The shape the reader has been typing for four chapters without seeing.
- **Content**: one command line — `kubectl cordon node-7` — broken into four labelled slots, drawn as segments of a single line rather than as a stack. Below it, three more commands the reader has already run (`kubectl apply -f deploy.yaml`, `kubectl get pods`, `kubectl scale deployment/web --replicas=5`) aligned so that each one's slots sit in the same columns. Empty slots visibly empty.
- **Design requirement — the alignment is the pedagogy.** The figure's argument is that four commands the reader thinks of as unrelated have identical structure. If the examples are stacked without column alignment, the figure says nothing the prose did not. The columns must line up and the empty slots must read as empty rather than as absent.
- **Design requirement — case sensitivity must be visible.** The TYPE column should carry a small annotation showing `pod` / `pods` / `po` as equivalent; the NAME column a matching annotation showing that `node-7` and `Node-7` are not. This is the section's examinable half and prose alone under-signals it.
- **Label count**: four slot names, one case-sensitivity annotation pair — six. Within the Part 18.12 ceiling.

### `ch08-fig02-three-api-gates`

- **Purpose**: §2's Fixed Point, and the chapter's most examinable single fact. This is the figure most likely to be recalled in the exam room.
- **Content**: a left-to-right sequence. A request enters from the left. Gate one, **Authentication** — *who are you*. Gate two, **Authorization** — *may you do this*. Gate three, **Admission** — *should this, as written, be allowed*. Then persistence to etcd on the right. Each gate has a rejection path leaving the sequence, and **the third gate has a second outgoing path that rejoins the sequence with the request visibly altered.**
- **Design requirement — the mutation path is the figure's whole argument.** A three-box diagram with three identical reject arrows teaches that the gates are three of the same thing, which is exactly the model §2 exists to correct. The third gate must have two outgoing paths and one of them must show a modified request continuing. If only one element of this figure survives review, it is that path.
- **Design requirement — the gates must be ordered and the order must be unambiguous.** No parallel arrangement, no "these three checks happen." Left to right, one after another, with the request unable to reach gate two without passing gate one.
- **Design requirement — grayscale.** The three gates must be distinguishable by shape or position, not by colour (Part 18.11).
- **Label count**: three gate names, three questions, request, etcd, reject, mutate — the questions push this to eleven. **Over the ceiling.** Resolution: the three questions (*who are you* / *may you* / *should this*) go in the caption as a numbered gloss, not in-frame. That brings the in-frame count to seven and the questions are better as a caption line anyway, since the caption's job is to say what to notice (Part 18.7).
- **Reuse note**: **this belongs in The Lodestar**, and Chapter 12 will point at it rather than redrawing the gate model. Design it to be legible at one-quarter page.

### `ch08-fig03-version-skew-window`

- **Purpose**: §6's Dead Reckoning table, made spatial. The most purely utilitarian figure in the chapter.
- **Content**: a horizontal version axis with the kube-apiserver's minor version as a vertical reference line at the centre. Each component is one horizontal bar showing its permitted range relative to that line: kubelet extends three to the left and stops dead at the line; kube-proxy the same; controller-manager, scheduler and CCM extend one to the left and stop at the line; **`kubectl` is the only bar that crosses to the right**, extending one in each direction.
- **Design requirement — the reference line is a wall for every bar but one.** The entire table reduces to "one bar crosses the line," and the figure exists to make that visible in one glance. If the drawing does not make `kubectl`'s bar visually exceptional, it has failed and the reader will go back to memorising five rows.
- **Design requirement — no absolute version numbers in the figure.** Label the reference line "kube-apiserver" and the axis in relative minors (−3, −2, −1, 0, +1). Version rosters age; this figure must not. The specific 1.36/1.35/1.34 illustration belongs in the prose, marked as of the snapshot date.
- **Label count**: five component names, five axis ticks, the reference line — eleven. **Over the ceiling, and justified**: the count *is* the table, and dropping a component would leave the reader with a partial rule. Mitigation: the five component names are row labels in a left-hand gutter rather than in-frame annotations, so the reader reads one row at a time.
- **Reuse note**: **this belongs in The Lodestar.** It is the highest-density exam-fact-per-square-inch artefact the book will produce. Design at quarter-page legibility and check it in grayscale.

### `ch08-fig04-node-lifecycle-cordon-drain`

- **Purpose**: §4's Fixed Point, and the defusal of the chapter's most consequential trap.
- **Content**: one node drawn four times in sequence, with the same three Pods aboard at the start. **Schedulable** — Pods aboard, new Pods arriving. **Cordoned** (`kubectl cordon`) — the same three Pods still aboard and visibly unchanged, with an arriving Pod turned away. **Drained** (`kubectl drain`) — the three Pods gone, node empty. **Uncordoned** (`kubectl uncordon`) — new Pods arriving again. Command names on the transitions, not on the states.
- **Design requirement — the three original Pods must be visibly identical between panels one and two.** This is the figure's entire job. Any visual change to them at the cordon step — greying, dimming, a warning mark — teaches the trap the figure exists to defuse. They are unaffected and they must look unaffected.
- **Design requirement — the DaemonSet exception stays in prose.** Adding a fourth, tolerating Pod to all four panels would make the figure precise and unreadable. One sentence in §4 covers it.
- **Label count**: four state names, three command names, node, Pods — nine. Slightly over, mitigated by the sequence structure: the reader reads panel by panel and holds two labels at a time.
- **Reuse note**: Chapter 13 may point at this figure when it reaches node health; do not let Chapter 13 redraw it.

### `ch08-fig05-quota-vs-limitrange`

- **Purpose**: §3's Fixed Point. The chapter's only comparative illustration (Part 18.10).
- **Content**: one namespace drawn twice, side by side, containing the same four Pods. **Left, ResourceQuota**: a single boundary around the namespace's total, with the four Pods' consumption stacking against it and the fifth Pod refused because the total is reached. **Right, LimitRange**: no namespace boundary at all; instead each of the four Pods carries its own bounds, and a fifth Pod arriving with *no* resource fields is shown being filled in with a default rather than refused.
- **Design requirement — the two panels must fail differently, and both failures must be visible.** The left panel's fifth Pod is *rejected*; the right panel's fifth Pod is *modified*. That is the contrast, it is the same mutate-versus-reject distinction §2 established at the gate, and a figure where both panels simply refuse something has drawn one mechanism twice.
- **Design requirement — the scope boundary must be present on the left and absent on the right.** The quota's boundary is drawn around the namespace; the LimitRange's constraints are drawn around individual Pods. Scope is the discrimination and it should be legible before any label is read.
- **Label count**: two mechanism names, namespace boundary, four Pods (as a group label), the refused Pod, the defaulted Pod — seven. At the ceiling.
- **Reuse note**: **this belongs in The Lodestar**, paired with `fig03`. Chapter 12 will retrieve its scope boundary when deriving the RBAC matrix.

### `ch08-zenith-consequences-not-rules`

- **Purpose**: the chapter's one Zenith. The claim that nothing in this chapter was new.
- **Content**: the API server drawn as a single door at the centre. From the left, the chapter's administrative acts arriving as writes — a `cordon`, a ResourceQuota, an `apply`, a node registration — all converging on the same door. Behind the door, the controllers that do the actual work, **each labelled with the chapter that introduced it**: the scheduler (Ch 7), the node controller (Ch 4/Ch 8), the workload controllers (Ch 6), the control loop itself (Ch 3). And etcd behind all of them.
- **Design requirement — the chapter numbers on the controllers are the payload.** The figure's argument is *you already met everything behind this door*. Without the chapter attributions it is an architecture diagram the reader has seen a version of in Chapter 3; with them it is a claim about what they have learned. Do not let the illustrator drop them as clutter.
- **Design requirement — one door, and the arrows must converge on it.** If any administrative act is drawn reaching a controller directly, the figure says there are side channels, which is the opposite of the section's claim and would also contradict Chapter 3's hub-and-spoke.
- **Design requirement — visual continuity with Chapter 3's architecture figure.** The recognition is what makes this a Zenith rather than a summary. The reader must see the diagram they met at the 15% mark, now with their own hands on it.
- **Label count**: four administrative acts, four controllers with chapter tags, the door, etcd — ten or eleven. **Over the ceiling, and justified**: the count is the argument, exactly as `ch07-zenith`'s eight mechanisms were. Mitigation: acts on the left, controllers on the right, visually separated so the reader holds one side at a time.
- **Register note**: Communications Officer family, junior tier. This is the chapter's only dramatic synthesis illustration and it should carry the brand's illustrative register — the standing-the-watch image is available, the chapter is named for it, and §1–§7's prose is deliberately plain. Use it once, here.

---

## 9. Open questions for the author

1. **Subtitle length — 12 words against a ≤10-word constraint (editorial, non-blocking).**
   The arc outline's working subtitle is *"The commands you'll actually type, and the versions that will bite you."* This stage's frontmatter constraint is ≤10 words. Frontmatter above carries *"The commands you'll actually type, and the versions that bite"* — exactly 10, both clauses intact, the wry "actually" preserved, ending on a harder consonant. Alternative if you prefer to keep "you": *"The commands you'll type, and the versions that will bite"* (10). **Recommendation: take the version in the frontmatter.** If you'd rather override the constraint and keep the arc's original, say so and it goes back verbatim — the constraint is this stage's, not the contract's.

2. **⚠ BLOCKING — the three API access gates are not fully sourced.**
   This is the chapter's central Fixed Point, it is the payoff for a published cross-bearing (`chapter-03` line 671), and **no cached source states the sequential-gate semantics.** What *is* cached: `k8s-docs-extending-kubernetes` line 19 gives the three names in canonical order ("authentication, authorization, dynamic admission control (webhooks)") as an extension-point taxonomy, and `k8s-docs-cluster-administration` lists them in the same order as page titles under "Securing a cluster." Neither states that a request passes them **in sequence**, that admission runs **after** authorization and **before** persistence, or that admission controllers may **mutate** rather than only reject. Every one of those is load-bearing for §2's Fixed Point, for `ch08-fig02`, and for Chapter 12's derivation of Pod Security Admission.
   **Fetch: `kubernetes.io/docs/concepts/security/controlling-access/`** — the canonical page, and it closes all four sub-claims outright. Secondary, if cheap: `kubernetes.io/docs/reference/access-authn-authz/admission-controllers/` for the mutating/validating distinction and one or two named built-in plugins. **§2 cannot be drafted as specified without the first of these.** Routed to Stage 2.

3. **⚠ BLOCKING — ResourceQuota and LimitRange are named but not documented.**
   Two published cross-bearings promise this section by name (`chapter-04` line 590, `chapter-07` line 430). What is cached supports exactly two claims: quota is the mechanism by which namespaces divide resources among users, and the functional contrast (quota allocates shared resources fairly; LimitRange ensures Pods specify their requirements). Nothing cached says **what a quota can count** (compute totals, object counts, storage), nothing says **what happens to a Pod that omits requests in a quota'd namespace**, and nothing describes **LimitRange's min/max/default structure**. A section built strictly on disk is three paragraphs and cannot carry two chapter-scoped promises.
   **Fetch: `kubernetes.io/docs/concepts/policy/resource-quotas/` and `kubernetes.io/docs/concepts/policy/limit-ranges/`.** Scope guard: take the quota *scope* and *what it counts*, the requests-must-be-specified rule, and LimitRange's default/min/max shape. Do **not** take quota scopes/scope-selectors, priority-class quota, or the full countable-resource list — all above associate tier. Routed to Stage 2.

4. **Auditing is a named topic with no cached definition (non-blocking, but decide before drafting).**
   `k8s-docs-cluster-administration` lists "Auditing" as a page title under Securing a cluster and gives nothing else. The B1 domain analysis defines it ("recording the sequence of activities affecting the cluster") but B1 is a pipeline artefact, not a source, and §2 cannot cite it. Two options: **(a)** fetch `kubernetes.io/docs/tasks/debug/debug-cluster/audit/` and give auditing two or three sentences — what an audit record is, what stages are recorded, that it is policy-driven; or **(b)** reduce auditing in §2 to a single sentence naming it as a component of securing a cluster, cited to the cluster-administration page, with no definition asserted. **Recommendation: (b) unless the fetch is already cheap.** Auditing is one line in the competency list and the exam's comprehension tier almost certainly asks only that it exists. Option (a) is strictly better if Stage 2 is fetching for #2 and #3 anyway, since it is the same doc tree.

5. **`node-monitor-grace-period` has a name and no value (resolved, recorded for the audit).**
   `k8s-docs-nodes` names the parameter in the definition of `Ready: Unknown` and gives no duration. §4 names the parameter and states no number, which is the correct handling. Recording it here so the fact-accuracy audit does not flag the omission as a gap — it is deliberate. If a later fetch supplies a default, it may be added as an illustration, never as a rule.

6. **`chapter-07` line 408's promise is only partially payable.**
   Chapter 7 §2 told the reader: *"What makes the two differ, and how it's configured, is Chapter 8's material."* The `node-allocatable` snapshot's extraction note is explicit that the Capacity → Allocatable relationship exists only as an un-transcribable image on the source page, and that `kube-reserved`, `system-reserved`, `eviction-threshold` and cgroup enforcement were deliberately not extracted as "Chapter 8's territory." So Chapter 8 has the promise and not the material.
   Three options: **(a)** fetch the reservation model from `kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources/` in full and give §4 a short block; **(b)** pay the promise partially — §4 names `kube-reserved` and `system-reserved` as the reservations that make the two differ, without the arithmetic, and that is enough to satisfy a reader who was promised "what makes the two differ"; **(c)** demote the Chapter 7 pointer to `*[cross-bearing: see Ch 8 — node administration]*` scope, which it already is (it is chapter-scoped, not section-pinned), and accept partial payment silently. **Recommendation: (b).** It discharges the promise honestly, costs two sentences, and the reservation model's configuration detail is above associate tier — the exam does not ask how to set `--kube-reserved`. Flagging because it is a published promise and the reader may notice.

7. **Konnectivity and SSH tunnels — routed here by a snapshot note, but above tier.**
   The `control-plane-node-communication` snapshot states that its SSH-tunnels and Konnectivity sections "belong to the Chapter 8 API-access material." Having read them: they are control-plane-to-node transport security, not API access control, and neither appears in any CNCF competency list. SSH tunnels are additionally deprecated, which makes teaching them a net negative. **Recommendation: omit both entirely from §2.** The snapshot's routing note was written from Chapter 3's vantage and reasonably assumed Chapter 8 would want them; Chapter 8 does not. Recording the decision so the fact-accuracy audit does not read the omission as an oversight. If you disagree, the cheapest honest home is a single `🔭 Closer Look` in §2 naming Konnectivity as the replacement for a deprecated mechanism, explicitly marked as deeper than the exam requires.

8. **Feature stages (alpha / beta / stable) — Chapter 8 or Chapter 17?**
   `k8s-keps-and-feature-stages-2026-08-23.md` is tagged for both D4 Community and D1 Administration, and the feature-stage material has a genuine claim on §6: enabling a feature gate is an administrative act, and "which stage is this feature at" is a version question. But the arc outline routes KEPs to Chapter 17, and the stages only make sense as the *output* of the KEP graduation process — alpha, beta and stable are graduation criteria before they are cluster settings. Splitting them from KEPs means teaching the stages twice or teaching them without their reason.
   **Recommendation: Chapter 17 owns both, and §6 does not mention feature gates.** §6 already carries the book's densest recall block and does not need a sixth thing. Flagging it because it is a cross-chapter boundary and the arc outline does not adjudicate it explicitly — if you'd rather §6 carry the stages, the natural home is after the cadence paragraph, and Chapter 17 would then retrieve rather than introduce them.

9. **Eight sections for five points — fold options considered and rejected.**
   Chapter 7 shipped seven sections for the same weight; this chapter proposes eight. Three folds were considered: **§5 into §1** (put cluster provenance before the command surface) — rejected, it opens the chapter on its weakest material and forfeits the §5-as-restoration-point placement that the two high-attention sections require; **§7 into §5** (etcd backup as one more ownership duty) — rejected, it buries the chapter's only irreversible-consequence material inside its lightest section and drops a published cross-bearing's payoff to a subsection; **§3 into §2** (quota as an admission example) — the closest call, and rejected because §3 also carries the namespaced/cluster-scoped hinge that Chapter 12 depends on, and folding it makes that hinge a paragraph inside a section about something else. **The eight sections are the right shape; the spine is what makes them read as one chapter.** Raised only so the reviewer knows the alternatives were weighed.

10. **Heading-form drift in Chapters 2 and 3 (recorded, do not fix from here).**
    Chapter 7's outline flagged that Chapters 2 and 3 ship `## §1 — ⚪ Title` while Chapters 5, 6 and 7 ship `## ⚪ §1 — Title`. Chapter 8 follows the later form. Still queued for a book-level reconciliation sweep; do not fix Chapters 2 and 3 from inside this chapter.

11. **Domain weight disclosure (recurring, no action needed).**
    `domain_weight_pct: 5` is authored judgement. CNCF publishes four domain weights and no competency weights (B1 gap G33, B2 disclosure #1). The metadata line must carry the disclaimer in the shipped house form and the front matter must already say so. Recorded per-chapter so no chapter ships without it.

12. **Chapter 8 closes Part II — the Voyage Ahead has a structural job.**
    This is the last chapter before Part III, and Chapter 7's Safe Harbor already told the reader so ("One chapter left before Part III"). The Voyage Ahead should therefore do two things rather than one: hand off to Chapter 9 (every Pod has an address — and the reader has now met the flat cluster from the administrator's side without ever being told how anything in it reaches anything else), and close Part II as a unit. B2's framing is available and good: Part II is *ship, cargo, and company* — the container, the cluster, the objects, the Pod, the controllers, the placement, and the watch. Chapter 9 opens Part III by asking how any of it talks. Flagging so the drafting stage does not write a chapter-to-chapter handoff and miss the part boundary.
```

---

**Three things worth your attention before Stage 2 runs:**

1. **Two blocking source gaps, both in the chapter's first half.** The three API access gates (§2) and ResourceQuota/LimitRange (§3) are each promised by published cross-bearings and neither is adequately cached. §2's gap is the more serious — it's the chapter's central Fixed Point and Chapter 12 builds on it. Three fetches close both (`controlling-access/`, `resource-quotas/`, `limit-ranges/`), all in the same doc tree, so Stage 2 can take them in one pass. The arc outline's four named blocking gaps (G1, G26, G27, G28) are all closed; these two are new.

2. **Eleven inbound cross-bearings, none section-pinned.** More promises land on this chapter than on any other so far, and unusually, every one is chapter-scoped — so section numbering was free, and the outline uses that freedom to run the eight arcs along a single request path rather than as four unrelated blocks. The one placement constraint (`chapter-07` line 702, "Chapter 8's opening move") is honoured literally: `kubectl cordon` is the chapter's first command, in §1, with its full treatment deferred to §4 as a deliberate open loop.

3. **§6 is where the book's worst decay problem lives, and the outline treats derivation as the fix.** B3's scheduled retrievals in Chapters 13 and 17 are recorded as mandatory, but the more durable mitigation is inside §6 itself: teach the one rule that generates four of the five skew rows, then the single exception. A reader who derives the table keeps it; a reader who memorises it loses it by Chapter 12. Bearings #3 item 2 tests which one happened.