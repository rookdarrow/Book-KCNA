---
chapter: 6
chapter_type: "content"
title: "Fleets, Not Vessels"
subtitle: "Nobody sails one Pod"
exam_domain: "Kubernetes Fundamentals (competency: Kubernetes Core Concepts)"
domain_weight_pct: 6
complexity: "mixed"
novelty: "moderate"
prereq_factor: "standard"

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band for this chapter:
#-- "standard-plus" - 6 points, but this is the control loop's first
#-- instantiation and it closes Part II's trunk. Planning signal only,
#-- NOT a target.
#--
#-- WARNING - SECTION NUMBERING IS CONTESTED. Seven published cross-bearings
#-- point into this chapter. Five agree; three collide on the same number.
#--   chapter-04 line 269  -> *[see Ch 6 §1 - Deployments and ReplicaSets]*
#--   chapter-05 line 553  -> *[see Ch 6 §1 - the resource that holds the surviving intent]*
#--   chapter-05 line 1455 -> *[see Ch 6 §1 - Deployments, ReplicaSets, and the Pod template]*
#--   chapter-05 line 860  -> *[see Ch 6 §4 - what makes a rolling update safe]*
#--   chapter-04 line 688  -> *[see Ch 6 §3 - a controller's selector and the Pods it owns]*
#--   chapter-01 line 435  -> *[see Ch 6 §3 - StatefulSets and stable identity]*   <-- COLLIDES
#--   chapter-02 line 600  -> *[see Ch 6 §3 - CRDs and extending the API]*         <-- COLLIDES
#-- §1, §3 and §4 below honor the first five. The two collisions cannot be
#-- honored by any numbering; they require a two-token edit in shipped text.
#-- See § Open questions #1 for the exact edits and the reasoning.
#-- Do not renumber without re-checking all seven.
sections:
  - name: "The Resource That Holds the Intent"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-fig01-deployment-replicaset-pod-ownership"
    checkpoint_after: false
  - name: "A Loop You Can Watch Working"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "How a Controller Knows Its Own"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Changing the Fleet Under Way"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-fig02-rolling-update-maxsurge-maxunavailable"
    checkpoint_after: false
  #-- §4 also carries ch06-fig03-recreate-vs-rolling. The schema allows one
  #-- anchor per section; both are specified in § Required figures and both
  #-- appear in figures_planned. Do not drop fig03 on a schema technicality.
  - name: "Every Rollout Is a Revision"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "When Pods Are Not Interchangeable"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-fig05-statefulset-vs-deployment-identity"
    checkpoint_after: false
  - name: "One Per Node, and Work That Ends"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-fig04-workload-resource-decision-tree"
    checkpoint_after: false
  - name: "The Control Loop, Extended"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Nobody Sails One Pod"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch06-zenith-control-loop-instantiated"
    checkpoint_after: false

#-- Nine sections, matching Chapter 5's count. §2 and §7 are deliberately
#-- short. See § Open questions #9 for the fold options considered.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "keeping N copies of a process alive without watching a terminal - what has to be written down in advance"
    - "replacing a running service with a new version while it stays reachable"
    - "identifying a set of things by an explicit list of names versus by a property they share"
    - "a two-node database where the members are not interchangeable - what breaks if you swap them"
    - "running an agent on every machine in a fleet, including machines that do not exist yet"
    - "work that finishes versus work that is supposed to never finish - how an init system treats each"
    - "retrieval from Ch 3 - the two states a control loop compares, and what it does with the gap"
    - "retrieval from Ch 5 - a Pod's node dies; Ch 5 said it is not rescheduled, so what did it say happens"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 19 = 37. Bearings raised 10 -> 15 across 3
#-- checkpoints (5 + 5 + 5), matching the precedent set in Ch 3, Ch 4 and
#-- Ch 5, all of which shipped three checkpoints. See § Taking Your Bearings.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 19
  total_this_chapter: 42

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D1.1"]
  concepts:
    - "workload-resource"
    - "deployment"
    - "replicaset"
    - "replicationcontroller-legacy"
    - "pod-template"
    - "podtemplatespec"
    - "ownership-chain"
    - "owner-reference"
    - "controller-adoption"
    - "orphaning"
    - "cascading-deletion"
    - "replicas"
    - "desired-replica-count"
    - "manual-horizontal-scaling"
    - "horizontal-scaling"
    - "vertical-scaling"
    - "horizontalpodautoscaler"
    - "label-selector"
    - "matchlabels"
    - "matchexpressions"
    - "selector-template-agreement"
    - "overlapping-selectors"
    - "deployment-strategy"
    - "rolling-update"
    - "recreate-strategy"
    - "maxsurge"
    - "maxunavailable"
    - "minreadyseconds"
    - "readiness-gated-rollout"
    - "rollout"
    - "revision"
    - "rollout-history"
    - "rollback"
    - "revision-history-limit"
    - "pause-rollout"
    - "resume-rollout"
    - "stuck-rollout"
    - "statefulset"
    - "stable-pod-identity"
    - "pod-interchangeability"
    - "daemonset"
    - "node-local-facility"
    - "job"
    - "run-to-completion"
    - "cronjob"
    - "cronjob-schedule"
    - "custom-resource"
    - "customresourcedefinition"
    - "custom-controller"
    - "operator-pattern"
    - "declarative-api"
    - "dynamic-registration"
  commands:
    - "kubectl-get"
    - "kubectl-describe"
    - "kubectl-apply"
    - "kubectl-scale"
    - "kubectl-rollout-status"
    - "kubectl-rollout-history"
    - "kubectl-rollout-undo"
    - "kubectl-rollout-pause"
    - "kubectl-rollout-resume"
    - "kubectl-delete"

figures_planned:
  - "ch06-fig01-deployment-replicaset-pod-ownership"
  - "ch06-fig02-rolling-update-maxsurge-maxunavailable"
  - "ch06-fig03-recreate-vs-rolling"
  - "ch06-fig04-workload-resource-decision-tree"
  - "ch06-fig05-statefulset-vs-deployment-identity"
  - "ch06-zenith-control-loop-instantiated"
---

# Chapter 6 Outline — Fleets, Not Vessels

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 6: Fleets, Not Vessels` | required | top |
| `## *"Nobody sails one Pod"*` | required | line 2 |
| Metadata line (weight / complexity / novelty) | required | after subtitle |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings #1–#3` | **required, min 2** | after §3, §5, §8 |
| `★ Fixed Point` ×6 | **required, min 1** | §1, §3, §4, §5, §6, §7 |
| `**Dead Reckoning:**` ×1 min | **required** | §4 — rolling-update mechanics stated flat, no fleet register |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §5 (the revision rule), §7 (the three sibling-resource traps, one root cause) |
| `☀️ Zenith` | expected | §9 |
| `## Exam Alert` | **required** | after §9 |
| `## Practice Questions` | **required** | 19 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19 |
| `🏆 Safe Harbor` | expected | chapter close |

Heading form follows the shipped chapters exactly: `## ⚪ §1 — The Resource That Holds the Intent`, and checkpoints as `## ☆ Taking Your Bearings #1`.

**Zenith:** exactly one, per Part 18.10. `ch06-zenith-control-loop-instantiated` in §9. This chapter carries five concept diagrams plus the Zenith — the same load as Chapters 4 and 5, at the upper end of the 2–8 band. `ch06-fig04` (the decision tree) will be the tempting one to inflate into a second Zenith because it is the figure readers will photograph. Resist. Its job is reference; §9's job is recognition.

**Attention Budget guidance for drafting.** Nine sections, five distinct costs:

| Section | Cost | Why |
|---|---|---|
| §1 | medium | One reframe (you will almost never create a Pod) plus a three-layer ownership chain that has to survive six later chapters |
| §2 | low | The reader already owns the control loop from Ch 3. This section makes it concrete and adds one field |
| §3 | medium | The selector mechanism, plus a consequence (template labels must agree) that is not obvious |
| §4 | **high** | Two strategies, two tunable bounds with defaults, and a safety property that depends on Chapter 5's probes. The chapter's densest block |
| §5 | medium | Small closed set of `kubectl rollout` verbs, plus one exact rule about what does and does not create a revision |
| §6 | medium | One distinction, drawn precisely, against a documented misconception — and a deliberate forward reference the reader must be told about |
| §7 | low | Three resources, each with one defining property |
| §8 | medium-high | An abstraction jump: resources that did not exist until someone declared them, and controllers you write |
| §9 | low | Synthesis |

*"If you only have 15 minutes"* should point at **§1 plus the decision tree at the close of §7**, then Bearings #3. That is the highest exam-points-per-minute route through the chapter: the ownership chain is the structural key, and the decision tree is where traps #21, #22 and #23 all resolve.

**Recommended split point** for the two-session reader: after Bearings #2 (end of §5). §1–§5 are the Deployment arc, start to finish. §6–§9 are the rest of the family and what the pattern turns into.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 6 — Fleets, Not Vessels". Carried forward without modification:

- **Covers**: **D1.1** — ReplicaSet; Deployment; rolling update; `maxSurge`/`maxUnavailable`; Recreate; revisions; rollout history; rollback; pause/resume; StatefulSet (introduced with siblings); DaemonSet; Job; CronJob; `kubectl scale`; the HPA concept; custom resources and the operator pattern (definition).
- **Prerequisites**: Ch 4 (objects, selectors), Ch 5 (Pod, probes, requests).
- **Retrieval targets**: **20%** **[B3]** — from Ch 3–5. Named anchors: the control loop (Ch 3) now visible in a named controller; selectors (Ch 4) as the ReplicaSet→Pod join; probes (Ch 5) as what makes a rolling update safe.
- **Question budget**: 8 Soundings · 10 Bearings · 19 Practice · 37 total. Bearings raised to 15 below.
- **Figures**: six anchors, listed verbatim in `figures_planned`.
- **Depth band**: standard-plus.
- **Blocking gaps**: G8 (update mechanics, rollout, rollback) and G10 (CRDs, operator pattern). **Status: both are CLOSED.** Two *new* blocking gaps have opened that B1 did not anticipate — see § Open questions #2.

### Debts falling due in this chapter

Five published chapters defer material here by name. This is the highest inbound-debt chapter in Part II. Draft knowing the reader was told to expect each one.

| Owed by | Promise made | Paid in |
|---|---|---|
| **Ch 3 §6** (line 831) | *"ReplicaSet, a control loop you can watch working in real time"* | **§2** — the loop with a name, a field, and a `kubectl` command that makes it visible |
| **Ch 3 close** (line 956) | *"controllers you configure yourself"* | **§8** — custom resources plus custom controllers, which is where that promise actually lands |
| **Ch 2 §4** (line 600) | CRDs named as the fourth socket in *"Kubernetes defines an interface and lets the ecosystem implement it"* | **§8** — the API-extension socket, defined. The four-way collection stays Ch 17's |
| **Ch 4 §1** (line 269) | The three-replica Deployment used as the `spec`/`status` worked example, with *"meet the resource properly later"* | **§1** — the same example, now as the resource rather than the illustration |
| **Ch 4 §5** (line 688) | *"A ReplicaSet knows which Pods are its Pods by selector"* | **§3** — the mechanism, and the consequence Chapter 4 did not state |
| **Ch 5 §7** (line 860) | *"probes are what make a rolling update safe: a new Pod that never reports ready is a new Pod that never receives traffic"* | **§4** — the safety property, discharged where the rollout is |
| **Ch 5 Voyage Ahead** (line 1455) | *"If Pods are designed to be replaced, who does the replacing?"* — plus the three-part answer: a count that was wanted, a template for replacements, a loop that notices | **§1 and §2** — the question is the chapter's opening beat, and Chapter 5 already framed it better than a re-argument would |

Chapter 5's Voyage Ahead is unusually generous: it states the problem, names the three pieces of the answer, and hands the reader a cliffhanger. **Do not re-argue it.** §1 opens by collecting the question in one clause and answering it. A chapter that spends four paragraphs re-establishing a setup the previous chapter already built has started admiring itself.

### What this chapter owes forward

| Concept | Retrieved at | Contract |
|---|---|---|
| **The control loop, instantiated** (the spine's middle beat) | Ch 15 (**the book's primary Zenith** — the same loop pointed at a Git repository), Ch 17 (the pattern named as a principle) | `ch06-zenith` must be visibly the same shape as `ch03-fig02`. The three-beat spine only works if beat two is recognizable as beat one |
| **Workload resources create Pods** | Ch 7 (**named anchor** — the controller that produced the unscheduled Pod), Ch 9 (**named anchor** — ReplicaSet churn as the reason a stable name is needed) | §2's replacement behavior is what both retrieve. State it in a form that survives being quoted |
| **StatefulSet identity** | Ch 11 (**the reciprocal pair** — PV pairing closes the loop), Ch 16 (StatefulSet + PVC in application-side debugging) | `ch06-fig05` and `ch11-fig05` are a designed pair. **Build them together or the loop does not close** |
| **Revision and rollback** | Ch 14 (**named anchor** — *"Ch 6 rollback vs Helm rollback: different mechanisms, same word"*) | §5 must make the mechanism explicit enough that Ch 14 has something to contrast against. "Rollback" as a bare verb gives Ch 14 nothing |
| **Rolling-update mechanics** | Ch 15 (**named anchor** — mechanics now given strategy vocabulary: blue/green, canary, A/B) | §4 owns `maxSurge`/`maxUnavailable`/`Recreate`. It does **not** name blue/green or canary except as a single forward pointer |
| **CRDs** | Ch 17 (**the secondary Zenith** — CRI/CNI/CSI/CRDs resolved into one pluggability story), Ch 14 (CRDs shipped as chart content), Ch 15 (Argo CD as a controller on a custom resource) | §8 defines; Ch 17 collects. Do not pre-collect |
| **DaemonSet** | Ch 18 (**named anchor** — node-level log agents as DaemonSets), Ch 9 (CNI plugins as DaemonSets) | §7's one-per-node property is what both retrieve |
| **HPA** | Ch 13 (metrics-server as HPA's input), Ch 17 (the autoscaling landscape) | §2 names HPA as *the thing that writes `replicas` when it is not you*, and stops |

**Scope boundary with Chapter 15 — state it once and hold it.** Chapter 6 owns rolling-update *mechanics*: the two strategy values, the two bounds, what the defaults are, what readiness has to do with it. Chapter 15 owns strategy *vocabulary*: blue/green, canary, A/B, and the sync hooks that implement them. If a paragraph in §4 starts explaining what canary means, it has crossed. B2 split these deliberately — the mechanics are Deployment fields, the vocabulary needs Argo's hooks to attach to.

**Scope boundary with Chapter 11.** §6 teaches StatefulSet at the level of *why it is different*: Pods are not interchangeable, each has a stable identity, each is typically paired with its own durable storage. PersistentVolume, PersistentVolumeClaim, StorageClass, access modes, and the provisioning model are Chapter 11's, and the reader must be *told* the loop is being left open rather than left to notice.

**Scope boundary with Chapter 13.** The cached Deployment source says you can use a Deployment's status as an indicator that a rollout has stuck. §4 or §5 may say that the signal exists and name it. What to run, what events to read, and what to do next is Chapter 13's.

**Reader positioning**: Communications Officer role family, **junior tier**. Single unified brand voice; only atmospheric register and reader rank differ.

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**The curiosity gap is already open, and Chapter 5 opened it.** The previous chapter ended on a question it deliberately refused to answer: if Pods are designed to be replaced rather than repaired, who does the replacing? Collect that question in the first sentence and then widen it, because the honest answer is stranger than "a thing called a Deployment." The answer is that Kubernetes has *no special replacement machinery at all*. It has the same control loop the reader met in Chapter 3, given a count to hold and a template to copy from. Everything in this chapter — rolling updates, rollbacks, one-Pod-per-node, scheduled batch work, and the operator running your database — is that one loop with different desired state plugged into it. Open on the promise that this chapter has fewer ideas in it than it looks like, and close it at §9 when the reader can see it.

**The identity frame is the shift from operator to author of intent.** Chapter 5 made the reader someone who can read what infrastructure is telling them. Chapter 6 makes them someone who states what should be true and lets the system be responsible for it. That is the actual behavioral difference between people who are new to Kubernetes and people who are not: newcomers reach for the Pod, then for a script that recreates the Pod, then for a cron job that checks whether the script ran. Practitioners write down the count and the template and go home. Say it in the practitioner's register. The reader has probably already written one of those scripts.

**The stakes, stated flat and without inflation.** Six points on this book's authored allocation — CNCF publishes four domain weights and no sub-weights, and the front matter says so. But the number understates the chapter twice over. First, this is the beat the book's spine passes through: Chapter 3 introduced the control loop, Chapter 6 instantiates it, Chapter 15 generalizes it, and a reader who does not feel the shape here will experience Chapter 15's Zenith as a fifth list to memorize instead of a recognition. Second, the workload-resource decision — Deployment or StatefulSet or DaemonSet or Job — is the kind of thing a recognition exam asks about directly, and the three documented traps around it are all confusions a reader can be inoculated against in a single figure. No manufactured urgency; the reader is an adult professional and will notice.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Six outcomes, active verbs:

- **Trace** the ownership chain from a Deployment down to a running Pod, and say which layer holds the count and which holds the template.
- **Explain** how a controller knows which Pods belong to it — and what breaks when two controllers disagree about that.
- **Predict** what a cluster does during a rolling update, given `maxSurge` and `maxUnavailable`, and name the thing that makes the update safe rather than merely gradual.
- **Distinguish** the six workload resources by the one property that separates each from its nearest neighbor.
- **State** what actually creates a new revision — and what looks like it should, but doesn't.
- **Define** a custom resource, a custom controller, and the pattern that is the two of them together.

*You'll also stop reaching for `kubectl run`, which is a smaller change than it sounds and is the point of the whole chapter.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Chapter 6's prerequisite set is Chapter 3 (the control loop), Chapter 4 (objects, labels, selectors) and Chapter 5 (the Pod and its disposability), plus general operational literacy. **Six questions test priors the reader arrives with; two are deliberate retrieval from Chapters 3 and 5.** **[B3]** Soundings sit outside the retrieval budget but do retrieval work anyway, sourced from B2's Prerequisites column.

**Fixed Points this chapter teaches, which Soundings must therefore not reveal:**

1. You will almost never create a Pod directly; a workload resource holds the intent, and the chain is Deployment → ReplicaSet → Pod.
2. A controller finds its Pods by label selector, not by name — which is why the template's labels must agree with the selector, and why overlapping selectors are a hazard rather than a curiosity.
3. A new revision is created **if and only if** `.spec.template` changes. Scaling does not create one.
4. `RollingUpdate` is the default strategy; `maxSurge` and `maxUnavailable` both default to 25%; `Recreate` kills every old Pod before creating any new one.
5. Deployment versus StatefulSet is about **interchangeability**, not about whether the app writes to disk.
6. DaemonSet means one Pod per matching node, added automatically as nodes join — it is not a replica count.
7. Job runs to completion once; CronJob runs the same Job repeatedly on a schedule.
8. A custom resource alone stores structured data. A custom resource plus a custom controller is the operator pattern.

Each question below is checked against that list.

| # | Question topic | What it tests | Spoiler check |
|---|---|---|---|
| 1 | You want three copies of a process running on a machine at all times. One dies at 3 a.m. What would have to be written down *in advance* for something else to restore it without waking you? | The desired-state prior in its general form. Sets up "a count plus a template" as the answer to a question the reader has already had at work | Names nothing Kubernetes-specific. §1's teaching is the *layering* — that the count and the template live in different objects, and which one owns which. A general instinct spoils none of that |
| 2 | You need to replace a running service with a new version while it stays reachable the whole time. Describe how you have done this, or would do it, with tools you already know. | The rolling-update prior — load-balancer pools, drain-and-swap, two environments and a DNS flip | §4's Fixed Points are the two *named bounds* and their defaults, and the readiness dependency. A reader with the general instinct still has to learn all of it, and lands it faster |
| 3 | Two ways to identify a group of things: an explicit list of names, or a rule about a property they share. What does each cost you when the group changes while you are not looking? | The selector prior, framed as a trade-off rather than a definition | This is the setup for §3, not its payoff. §3's Fixed Point is the *consequence* — that the template's labels must agree with the selector, and that two rules matching the same thing is a hazard. Nothing here reveals that |
| 4 | A two-member database: one primary, one replica, each with its own data on disk. What actually breaks if you swap which machine is which — hostnames, storage, and all? | **The chapter's most valuable pre-test.** It surfaces *non-interchangeability* as a problem before §6 gives it a resource name | Never mentions StatefurSet or Kubernetes. The trap being defused (#21) is that people think the distinguishing property is "writes to disk"; this question walks the reader into identity being the real issue without naming the answer |
| 5 | A log-collection agent has to run on every machine in your fleet — including the machines that will be added next Tuesday. How would you express that requirement, as opposed to "run six copies"? | The DaemonSet prior, and specifically the difference between *per-node* and *a number* | §7's Fixed Point is the resource name plus the automatic-on-join behavior. The question makes the reader feel the distinction; it does not hand them trap #22's correction |
| 6 | Your init system supervises two things: a web server that should never exit, and a nightly backup script that should exit. How does it treat them differently, and what does "healthy" mean for each? | The Job prior, by analogy to systemd service-versus-oneshot or a CI job | §7 teaches the two resource names and the once-versus-schedule split (trap #23). The general instinct is the ramp |
| 7 | **Retrieval from Ch 3 §6.** A control loop compares two things and acts on the difference. Name both, and say what the loop does when they match. | **[B3]**'s designated control-loop anchor, in its pre-test position | This is the anchor's setup. §2's teaching is that a named controller — ReplicaSet — is this loop with a specific field as its desired state, and that you can watch it work. Retrieving the abstract shape reveals none of the instantiation |
| 8 | **Retrieval from Ch 5 §4.** A Pod's node dies. Chapter 5 was emphatic that the Pod is not rescheduled. What did it say happens instead — and what did it say was left unanswered? | A fairness check as much as a retrieval: Chapter 5's Voyage Ahead explicitly told the reader to carry this question into Chapter 6 | The reader is retrieving a question, not an answer. §1 and §2 supply the answer. If they can already state the question, the chapter's opening will land as arrival rather than setup |

**Rubric**: standard 6+ / 3–5 / 0–2 per `branded-terms.yaml`. The 0–2 branch carries a specific instruction: **if questions 7 and 8 were the misses, re-read Chapter 3 §6 and Chapter 5 §4 before starting §2.** Those are the two published cross-bearings this chapter collects, and §2 will read as a vocabulary drill without them.

**Note for drafting:** questions 1, 4, 5 and 6 each surface a *problem* the chapter later solves. Keep them phrased as situations. A Soundings question that can be answered by reciting a term has stopped doing metacognitive work.

---

## 4. Section plan

Nine sections. **§1, §3 and §4 are pinned by published cross-bearings** (see the frontmatter warning and § Open questions #1).

The chapter's shape, at a glance: **§1–§3 what holds the intent and how it finds its Pods · §4–§5 changing that intent safely · §6–§7 the rest of the family · §8–§9 the pattern, extended and recognized.**

### §1 — ⚪ The Resource That Holds the Intent

**Pinned by three published cross-bearings** (`chapter-04` line 269, `chapter-05` lines 553 and 1455). Collect Chapter 5's cliffhanger in the first clause, then answer it.

**First, the answer, stated once:** you do not manage Pods directly. You use a workload resource that manages a set of Pods on your behalf, and that resource configures a controller that makes sure the right number of the right kind of Pod are running to match the state you specified. That sentence is the whole chapter in miniature and it is quotable from the source — use it early and let the rest of the section unpack it.

**Second, the ownership chain, which is the section's real work.** A Deployment manages a set of Pods to run an application workload, usually one that does not maintain state, and it provides declarative updates for Pods *and ReplicaSets*. That second half is the part readers skip. There are three layers, not two: the Deployment holds the template and the update policy; the ReplicaSet holds a count; the Pods are what actually run. Draw the chain, and be explicit about which layer owns which piece of intent, because §4 and §5 are both consequences of the Deployment layer existing separately from the ReplicaSet layer.

**Third, the Pod template.** Everything Chapter 5 taught about a Pod's `spec` is unchanged — it is now nested inside the workload resource as `.spec.template`, and that is the thing a replacement gets copied from. One sentence connecting it back; the reader does not need it developed, they need it *located*.

Close on the reframe, which is the most efficient possible ending: the Pod the reader spent Chapter 5 learning is something they will almost never create directly. Not because Pods are unimportant — because being the thing that gets created *for* you is what a Pod is for.

- **Objectives**: D1.1
- **Concepts introduced**: `workload-resource`, `deployment`, `replicaset`, `pod-template`, `podtemplatespec`, `ownership-chain`, `replicationcontroller-legacy`
- **Sources**: `k8s-docs-workloads-2026-08-23.md` (you don't need to manage each Pod directly; workload resources configure controllers; Deployment for stateless workloads where any Pod is interchangeable; ReplicaSet replacing the legacy ReplicationController). `k8s-docs-deployment-2026-08-23.md` (a Deployment provides declarative updates for Pods and ReplicaSets; you describe a desired state and the Deployment controller changes actual state at a controlled rate; create a Deployment to rollout a ReplicaSet, and the ReplicaSet creates Pods in the background). `k8s-docs-objects-2026-08-23.md` (the three-replica `spec`/`status` example Chapter 4 already used). ⚠ **The ReplicaSet page itself is not cached** — see § Open questions #2
- **Figure**: `ch06-fig01-deployment-replicaset-pod-ownership`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — the chain is Deployment → ReplicaSet → Pod; the Deployment holds the template and the update policy, the ReplicaSet holds the count, the Pods run. **This is the chapter's most-retrieved Fixed Point.** Write it to be quotable in Chapters 7, 9, 14 and 15
  - `> ⚓ **Worth Securing:**` — the practical rule: if you find yourself writing a bare Pod manifest for anything other than a one-off experiment, you have picked the wrong object
- **Cross-bearings**: back to Ch 5 §4 and Ch 5's Voyage Ahead (**mandatory — this is the pinned payoff**; the reader was handed a question, so answer it and acknowledge it in one clause); back to Ch 4 §1 (the three-replica example, now as the resource); back to Ch 4 §2 (four fields, unchanged, one nesting level down); forward to Ch 14 (a Helm chart's job is to template this object)
- ⚠ **Do not teach `kubectl run` or bare-Pod workflows** beyond one clause naming them as the thing you are not going to do
- ⚠ **ReplicationController gets one clause**, as the legacy resource ReplicaSet replaced. It is named in the cached source, so the reader may meet the word; it is not worth a paragraph

### §2 — ⚪ A Loop You Can Watch Working

**Pays Chapter 3's promise verbatim.** Short, and its job is to convert an abstraction the reader already accepted into something concrete.

The ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. It has a field — `.spec.replicas` — that is the desired state, and a count of Pods that actually exist, which is the current state. When those differ it creates or deletes Pods until they agree. That is Chapter 3's thermostat with the numbers filled in, and the reader should feel the recognition rather than be told to have it.

Then the demonstration, which is why this section exists at all: delete a Pod that a ReplicaSet owns and watch a replacement appear. Nobody triggered it. Nothing was scheduled. The loop noticed a gap and closed it. Chapter 3 promised a loop the reader could watch working in real time; this is that, and one `kubectl delete` plus one `kubectl get pods` is the entire demonstration.

**Scaling** is the same field seen from the other side. Horizontal scaling means changing the number of replicas — `kubectl scale` is a first-class verb for exactly that — and the loop treats "you asked for five and there are three" identically to "you asked for three and one died." Same gap, same closing action. That equivalence is worth stating explicitly because it is the cleanest possible demonstration that self-healing is not a separate feature.

Close by naming the **HorizontalPodAutoscaler** as the thing that writes `replicas` when it is not you: an API resource plus a controller that periodically adjusts the replica count to match observed resource utilization. One sentence, one forward cross-bearing to Ch 17, and stop. The autoscaling landscape is Chapter 17's and there is a whole D4 competency waiting for it.

- **Objectives**: D1.1
- **Concepts introduced**: `replicas`, `desired-replica-count`, `manual-horizontal-scaling`, `horizontal-scaling`, `horizontalpodautoscaler`
- **Sources**: `k8s-docs-controllers-2026-08-23.md` (controllers are control loops; a controller tracks a resource type whose `spec` is desired state; the controller sends messages to the API server rather than acting directly). `k8s-docs-autoscaling-2026-08-23.md` (horizontal scaling changes the replica count; manual horizontal scaling via kubectl; HPA is an API resource plus a controller adjusting replicas to match observed utilization). `k8s-docs-kubectl-overview-2026-08-23.md` (`scale` — update the size of the specified deployment). ⚠ **The ReplicaSet page is not cached**; the "maintain a stable set of replica Pods" definition needs its primary source
- **Figure**: none. `ch06-fig01` already carries the structural claim, and a second diagram of the same three boxes with an arrow labelled "reconcile" would be exactly the channel redundancy Part 18.7 warns against. The Ch 3 loop figure is the visual the reader retrieves here, by reference
- **Checkpoint after**: no
- **Markers planned**:
  - `> ⚓ **Worth Securing:**` — self-healing and scaling are the same operation. The loop cannot tell the difference between a Pod you deleted and a Pod that died
  - `> 🔭 **Closer Look:**` — the controller does not create Pods itself; it asks the API server to, and other components act on that. Chapter 3 established this and the cached controller source states it plainly. One short aside, because it is the fact that makes "nobody is in charge" true at this altitude too
- **Cross-bearings**: back to Ch 3 §6 (**mandatory — the pinned payoff for "a control loop you can watch working in real time"**); back to Ch 5 §4 (the Pod that got replaced, now with an agent); forward to Ch 7 (the Pod this loop just created still has to be placed somewhere, and sometimes cannot be); forward to Ch 9 (**named anchor** — this churn is why a stable name has to exist); forward to Ch 13 (metrics-server is what an HPA reads); forward to Ch 17 (VPA, KEDA, Cluster Autoscaler, Karpenter — the landscape)
- ⚠ **Do not teach VPA, KEDA, Cluster Autoscaler, or scale-to-zero.** All four are Chapter 17's, and traps #104 and #106 are defused there. See § Open questions #4 for the horizontal-versus-vertical plant

### §3 — 🔵 How a Controller Knows Its Own

**Pinned by `chapter-04` line 688.** Chapter 4 taught label selectors as the universal join and listed four places they are used; this is the first one collected, and it collects it with a consequence Chapter 4 did not state.

**The mechanism**: a ReplicaSet does not track its Pods by name or by a list. It has a selector, and its Pods are whichever Pods match it. Chapter 4 already gave the reader `matchLabels` and `matchExpressions`, so this is retrieval plus one new use, not new machinery.

**The consequence, which is the section's Fixed Point**: because membership is a *query*, the labels in the Pod template must agree with the selector. If they don't, the controller creates Pods that it then cannot see, notices the gap again, and creates more. The reader should be able to predict that outcome before being told it, which makes this a good place for a generation-effect prompt.

**Ownership** is the second half. Pods created by a controller carry an owner reference back to it, which is what makes cascading deletion work: delete the Deployment and the ReplicaSets and Pods go with it. This is also the mechanism behind the hazard — two controllers whose selectors overlap will fight over the same Pods, each one seeing a count that keeps changing for reasons it did not cause.

Close on the practical rule: give each workload a label that is genuinely unique to it, and do not hand-write labels that overlap across controllers.

- **Objectives**: D1.1
- **Concepts introduced**: `label-selector`, `matchlabels`, `matchexpressions`, `selector-template-agreement`, `owner-reference`, `cascading-deletion`, `overlapping-selectors`, `controller-adoption`, `orphaning`
- **Sources**: `k8s-docs-labels-selectors-2026-08-23.md` (selectors, equality and set-based, `matchLabels` equivalent to `matchExpressions` with operator `In`). `k8s-docs-workloads-2026-08-23.md` (controllers make sure the right number of the right kind of Pod are running). ⚠ **This section has no primary source for its ownership half.** The ReplicaSet page and the owners-and-dependents / garbage-collection page must be fetched — see § Open questions #2 and #3
- **Figure**: none. The join is already drawn in `ch04-fig03-labels-selectors-join`; the right move is to *refer to that figure by name* rather than redraw it, which is also a spacing-effect retrieval at zero cost
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `★ **Fixed Point:**` — a controller's Pods are the Pods matching its selector. Membership is a query, not a list, and the template's labels must satisfy it
  - `> **Before reading on:**` — generation-effect prompt: *the template's labels do not match the selector. The controller creates a Pod. What happens next?* Let the reader derive the runaway before it is stated
  - `> 🪝 **Snag:**` — two controllers with overlapping selectors fight, and neither one reports an error. It looks like flapping, not like a config mistake
- **Cross-bearings**: back to Ch 4 §5 (**mandatory — the pinned payoff**; the reader was told "a ReplicaSet knows which Pods are *its* Pods by selector" and sent here); forward to Ch 9 (a Service selects its backends the same way — a *different* controller reading the *same* labels, which is the point); forward to Ch 12 (deleting a workload does not delete what it referenced)
- ⚠ **Do not teach garbage-collection internals**, finalizers, or foreground-versus-background deletion. Cascading deletion is the associate-tier fact; the machinery is not. See § Open questions #3 for the `--cascade=orphan` decision

### §4 — 🔵 Changing the Fleet Under Way

**Pinned by `chapter-05` line 860.** The chapter's densest section, and the one that pays Chapter 5's probe promise.

**The mechanism first.** You declare the new state of the Pods by updating the Pod template. A new ReplicaSet is created, and the Deployment manages moving Pods from the old ReplicaSet to the new one at a controlled rate. This is where §1's three-layer chain earns its keep: *two ReplicaSets exist at once*, one scaling down and one scaling up, and the Deployment is the layer holding both. A reader who has the chain will find the rolling update obvious. A reader who does not will find it magic.

**Then the two bounds**, which are the exam-checkable content. `.spec.strategy.type` is `RollingUpdate` by default, and `RollingUpdate` takes `maxUnavailable` (the maximum number of Pods that can be unavailable during the update) and `maxSurge` (the maximum number of Pods that can be created over the desired number). Both accept an absolute number or a percentage. **Both default to 25%.** Work one example numerically — ten replicas, defaults, so at most twelve Pods exist and at least eight are available — because the arithmetic is what a question would ask for and because doing it once makes the two names stop being interchangeable.

**Then `Recreate`**, which is the contrast that makes `RollingUpdate` legible: all existing Pods are killed before new ones are created. That is downtime, deliberately chosen. It exists because some applications genuinely cannot have two versions running at once — a schema migration, an exclusive lock, a licence check. Present it as a legitimate choice with a known cost, not as the wrong answer.

**Close on safety, which is Chapter 5's promise.** A gradual replacement is not automatically a safe one. What makes it safe is that a new Pod does not count as available until it reports ready, so a new version that never becomes ready never displaces the old one — the rollout stalls instead of taking down the service. Name `minReadySeconds` here if the fetched source supports it. This is the moment Chapter 5's probes stop being a health-checking feature and become a release-safety mechanism, and the draft should let that land.

- **Objectives**: D1.1
- **Concepts introduced**: `deployment-strategy`, `rolling-update`, `recreate-strategy`, `maxsurge`, `maxunavailable`, `minreadyseconds`, `readiness-gated-rollout`
- **Sources**: `k8s-docs-deployment-2026-08-23.md` (`.spec.strategy` is `Recreate` or `RollingUpdate`, `RollingUpdate` is the default; Recreate kills all existing Pods before creating new ones; `maxUnavailable` and `maxSurge` definitions and the 25% defaults; declaring a new state by updating the PodTemplateSpec creates a new ReplicaSet which the Deployment moves Pods to at a controlled rate). `k8s-docs-pod-lifecycle-2026-08-23.md` (readiness). ⚠ `minReadySeconds` and `progressDeadlineSeconds` are **not** in the cached snapshot — see § Open questions #7
- **Figures**: `ch06-fig02-rolling-update-maxsurge-maxunavailable` **and** `ch06-fig03-recreate-vs-rolling`. Two figures in one section is unusual and justified: fig02 explains the bounds, fig03 draws the contrast, and merging them would produce an over-labelled diagram doing two jobs badly
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — `RollingUpdate` is the default; `maxSurge` and `maxUnavailable` both default to 25%; `Recreate` kills all old Pods first
  - `**Dead Reckoning:**` — **the chapter's required facts-only block lands here.** State the update mechanism with no fleet register at all: fields, values, defaults, order of operations. §4 is the section where a reader under time pressure most needs the unornamented version
  - `> 🪢 **Mnemonic:**` — a hook for which bound is which. *Surge is above the line, unavailable is below it.* Keep it that short
  - `> 🪝 **Snag:**` — a stalled rollout is not a failed one. The Deployment sits there, both ReplicaSets alive, waiting for a Pod that will never become ready
- **Cross-bearings**: back to Ch 5 §7 (**mandatory — the pinned payoff**; probes as what makes this safe); back to §1 (two ReplicaSets, one Deployment — the chain doing work); forward to Ch 13 (diagnosing the stuck rollout); forward to Ch 15 (**one pointer only** — blue/green, canary and A/B are strategy *vocabulary* and live there)
- ⚠ **Do not name blue/green, canary, or A/B** except in that single forward cross-bearing. B2 split mechanics from vocabulary deliberately and Chapter 15's Zenith depends on the vocabulary arriving there
- ⚠ **Do not teach `kubectl rollout status` here.** It belongs with the other rollout verbs in §5, and splitting the command surface across two sections costs an alternating-attention switch for nothing

### §5 — 🔵 Every Rollout Is a Revision

The consequence of §4, and the section that gives Chapter 14 something to contrast against.

**The rule, stated exactly, because the exactness is the content**: a Deployment's revision is created when a rollout is triggered, and a new revision is created **if and only if** the Pod template changes. Other updates — scaling, notably — do not create a revision. That "if and only if" is the section's Fixed Point and it is precisely the kind of boundary a recognition exam tests, because the intuitive answer ("any change to the Deployment") is wrong and the correct answer is one clause long.

**Then the verb surface**, which is small and closed: `kubectl rollout status` to watch one, `history` to list revisions, `undo` to go back to the previous one, `undo --to-revision=<n>` for a specific one, `pause` and `resume` to batch several template edits into a single rollout instead of triggering one per edit. Present `pause`/`resume` with its actual motivation from the source — applying multiple fixes without triggering unnecessary rollouts — because without the motivation it reads as an arbitrary pair of commands.

**Then the retention fact**: by default all of a Deployment's rollout history is kept so you can roll back at any time, modifiable through the revision history limit. Worth one clause because "can I still roll back?" is a real operational question and the default answer is yes.

Close by naming what a rollback actually *is*, since Chapter 14 will need the contrast: rolling back is not undoing an edit or restoring a backup. It is setting the Pod template to a previous value and letting the same rolling update run in the other direction. Same loop, same mechanics, opposite direction. State it in a form Chapter 14 can quote.

- **Objectives**: D1.1
- **Concepts introduced**: `rollout`, `revision`, `rollout-history`, `rollback`, `revision-history-limit`, `pause-rollout`, `resume-rollout`, `stuck-rollout`
- **Sources**: `k8s-docs-deployment-2026-08-23.md` (a revision is created when a rollout is triggered, if and only if `.spec.template` changed; scaling does not create a revision; all rollout history kept by default, modifiable via revision history limit; `kubectl rollout history` / `undo` / `--to-revision`; pause and resume to apply multiple fixes without unnecessary rollouts; the Deployment status as an indicator that a rollout has stuck). `k8s-docs-kubectl-overview-2026-08-23.md` (`rollout` — manage the rollout of a resource; valid types include deployments, daemonsets and statefulsets)
- **Figure**: none. A revision list is a table, and the draft should render it as one. Part 18.9 is explicit that procedural content whose text form is already optimal does not warrant a diagram
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2**
- **Markers planned**:
  - `★ **Fixed Point:**` — a revision is created if and only if the Pod template changes. Scaling does not create a revision
  - `⚠ **Navigational Hazards**` — the primary hazards block for the Deployment arc. The template-only revision rule, and the related error of expecting `rollout undo` to reverse a scale
  - `> ⚓ **Worth Securing:**` — `pause` before a batch of edits. It is the difference between one rollout and four
- **Cross-bearings**: back to §4 (rollback runs the same rolling update backwards); forward to Ch 13 (reading a stuck rollout); forward to Ch 14 (**named anchor** — *"Ch 6 rollback vs Helm rollback: different mechanisms, same word."* State this chapter's mechanism precisely enough that the contrast has something to land on); forward to Ch 15 (Argo CD's rollback to any committed config — a third thing wearing the same word)
- ⚠ **Do not turn the `kubectl rollout` verbs into a command reference.** Chapter 8 owns the command surface. Here they exist because the concepts need names attached

### §6 — 🔵 When Pods Are Not Interchangeable

**The book's one deliberate forward reference lands here.** Short, precise, and it must tell the reader what it is leaving open.

**Open with the property, not the resource.** Chapter 5 established that Pods are disposable; §1 and §2 established that a Deployment's Pods are *interchangeable* — any Pod in the Deployment can be replaced by any other, which is exactly why a template and a count are sufficient to describe the whole workload. Then ask the question Soundings #4 already planted: what if they are not interchangeable? What if this one is the primary and that one is the replica, and each has data that belongs to it specifically?

**Then the resource**: a StatefulSet lets you run one or more related Pods that *do* track state. Each Pod is matched with its own persistent storage, and the Pods have stable identities rather than interchangeable ones. Code running in a StatefulSet's Pods can replicate data to other Pods in the same StatefulSet to improve resilience — which is the source's own example and is worth using because it makes "related" concrete.

**Then the trap, drawn where the distinction is actually being made** (B1 #21): the difference between Deployment and StatefulSet is *not* whether the application writes to disk. A stateless web server can write to disk; a Deployment Pod can mount a volume. The distinguishing property is whether the Pods are interchangeable. Say it in those words, because the wrong version is the version most readers arrive with.

**Then declare the open loop, explicitly.** The storage half of this — PersistentVolume, PersistentVolumeClaim, StorageClass, access modes, how the pairing is actually provisioned — is Chapter 11's, and the reader is being told that on purpose. This is the only place in the book where a concept is deliberately left half-taught, and the honest move is to say so rather than let a sharp reader wonder what got skipped. One sentence, one forward cross-bearing, and move on.

- **Objectives**: D1.1
- **Concepts introduced**: `statefulset`, `stable-pod-identity`, `pod-interchangeability`
- **Sources**: `k8s-docs-workloads-2026-08-23.md` (StatefulSet runs one or more related Pods that track state; matching each Pod with a PersistentVolume; replicating data to other Pods in the same StatefulSet; Deployment is a good fit for stateless workloads *where any Pod is interchangeable*). ⚠ **The StatefulSet page is not cached** — the ordinal-index naming, ordered creation and termination, and the stable network-identity guarantee all need it. See § Open questions #2 and #5
- **Figure**: `ch06-fig05-statefulset-vs-deployment-identity` — **build as a reciprocal pair with `ch11-fig05`**
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — the distinguishing property is interchangeability, not disk. StatefulSet is for related Pods with stable identities, typically each paired with its own storage
  - `> 🪝 **Snag:**` — B1 trap #21 inline, in its exact wrong form so the reader recognizes their own belief
  - `> **Extended Analogy:**` *(optional sidebar)* — a crew where any bosun's mate can stand any watch, versus a crew where the pilot who knows this harbour is the pilot who knows this harbour. Only if it earns its space; §6 is short and a sidebar longer than the section is a net loss
- **Cross-bearings**: forward to Ch 11 (**mandatory, and the reciprocal half must be built** — the PV pairing, access modes, and what "each Pod matched with a PersistentVolume" actually requires); forward to Ch 16 (debugging StatefulSets is explicitly named in D3.2); forward to Ch 9 (stable network identity depends on a headless Service, which Chapter 9 owns — one pointer, no development)
- ⚠ **Do not teach PersistentVolume, PersistentVolumeClaim, StorageClass, access modes, or provisioning.** Every one of them is Chapter 11's and B2's whole justification for this placement is that the *taxonomy* belongs here and the *storage* belongs there

### §7 — ⚪ One Per Node, and Work That Ends

Three resources, one defining property each, and then the figure that collects all six. Deliberately brisk — this is a taxonomy section, and taxonomy sections that linger become lists.

**DaemonSet** defines Pods that provide facilities local to nodes. Every time you add a node that matches the specification, the control plane schedules a Pod for that DaemonSet onto the new node. Each Pod does a job similar to a system daemon on a classic Unix server. Give the reader the three real use classes the source names — fundamental cluster facilities like a networking plugin, node management, and optional platform enhancements — because they make the abstraction concrete and because two of them come back later (CNI plugins in Chapter 9, log agents in Chapter 18). The trap (#22) is reaching for a DaemonSet to "run several copies": a DaemonSet is not a replica count and has no `replicas` field. The count is a consequence of how many nodes match.

**Job** defines a task that runs to completion and then stops. **CronJob** runs the same Job repeatedly according to a schedule. That is the whole distinction (#23) and it is worth stating in exactly that parallel form, because the parallel structure is what makes the pair memorable. Connect back to Chapter 5's phase vocabulary: work that ends is work that reaches `Succeeded` or `Failed`, which are the two phases the reader learned and has had no use for until now. That connection is free, it is a retrieval, and it retroactively justifies two phase names that felt like padding in Chapter 5.

**Close with the decision tree**, which is the section's payoff and the chapter's most practically useful artifact. Does the work end? Job, or CronJob if it repeats on a schedule. Does it need to run on every node? DaemonSet. Otherwise it is a long-running service, and then the only question left is whether the Pods are interchangeable: Deployment if yes, StatefulSet if no. Six resources, four questions, and the three documented traps in this chapter are all defused by getting the questions in the right order.

- **Objectives**: D1.1
- **Concepts introduced**: `daemonset`, `node-local-facility`, `job`, `run-to-completion`, `cronjob`, `cronjob-schedule`
- **Sources**: `k8s-docs-workloads-2026-08-23.md` (DaemonSet defines Pods providing node-local facilities, scheduled automatically onto matching nodes as they join, similar to a system daemon, with the three use classes; Job runs a task to completion once; CronJob runs the same Job on a schedule). `k8s-docs-controllers-2026-08-23.md` (the Job controller as the worked example of a built-in controller — a genuinely useful reuse, since Chapter 3 already quoted it). ⚠ **The DaemonSet, Job and CronJob pages are not cached** — see § Open questions #2
- **Figure**: `ch06-fig04-workload-resource-decision-tree`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — DaemonSet is one Pod per matching node, automatically as nodes join. Job runs to completion once. CronJob runs a Job on a schedule
  - `⚠ **Navigational Hazards**` — the second hazards block, collecting traps #22 and #23 **with their shared root cause named**: all three sibling-resource traps come from choosing a resource by what the application *is* rather than by how its Pods need to be *managed*. Naming the root cause converts three memorizations into one rule
  - `> 🪢 **Mnemonic:**` — a hook for the decision tree's question order. Optional; only if it beats just reading the figure
- **Cross-bearings**: back to Ch 5 §5 (`Succeeded` and `Failed`, finally used); back to Ch 3 §6 (the Job controller was Chapter 3's own example of a built-in controller — collect it); forward to Ch 9 (CNI plugins ship as DaemonSets); forward to Ch 18 (**named anchor** — node-level log agents as DaemonSets); forward to Ch 7 (a DaemonSet's Pods still go through scheduling, and taints are how a node opts out)
- ⚠ **Do not teach Job parallelism, completions, backoff limits, or CronJob concurrency policy** unless the fetched pages establish them as associate-tier. Default: omit. The KCNA-level fact is once-versus-on-a-schedule

### §8 — 🟡 The Control Loop, Extended

**Pays Chapter 3's "controllers you configure yourself" and Chapter 2's fourth-socket promise.** The chapter's abstraction jump, and the setup for two later Zeniths.

**Start with the resource, not the pattern.** A resource is an endpoint in the Kubernetes API that stores a collection of objects of a certain kind — the built-in `pods` resource holds Pod objects. A *custom* resource is an extension of that API that is not necessarily present in a default installation. Custom resources can appear and disappear in a running cluster through dynamic registration, and once one is installed, users create and access its objects with `kubectl` exactly as they do for built-in resources. That last clause is the one that makes it click: nothing about the tooling changes.

**Then the CRD**, which is the object that does the installing. Defining a CustomResourceDefinition creates a new custom resource with a name and schema you specify, and the Kubernetes API then serves and stores it for you — no API server of your own required.

**Then the honest limitation, which is the section's Fixed Point**: on their own, custom resources only let you store and retrieve structured data. A CRD by itself is a shape in a database. Nothing happens. What makes it a *declarative API* is combining it with a custom controller — you declare desired state, the controller keeps current state in sync. That is Chapter 3's loop, written by someone who is not the Kubernetes project.

**Then the pattern, named**: the operator pattern combines custom resources and custom controllers. It captures the aim of a human operator who manages a service — someone with deep knowledge of how the system ought to behave, how to deploy it, and how to react when there are problems — as code. Use the source's examples, because they are concrete and they are the kind of thing that makes the abstraction stop being abstract: deploying an application on demand, taking and restoring backups, handling upgrades alongside schema changes, choosing a leader for a distributed application. And note the closing loop: an operator's controller normally runs outside the control plane, as an ordinary containerized workload — usually a Deployment. The thing that extends Kubernetes is itself deployed by Kubernetes, using the resource from §1.

Close by naming this as the fourth socket. Chapter 2 promised the reader they would meet this move three more times and pointed here for one of them. Collect the promise, name API extension as the socket, and hand the four-way synthesis forward to Chapter 17 without doing it.

- **Objectives**: D1.1
- **Concepts introduced**: `custom-resource`, `customresourcedefinition`, `custom-controller`, `operator-pattern`, `declarative-api`, `dynamic-registration`
- **Sources**: `k8s-docs-custom-resources-2026-08-23.md` (resource as an API endpoint; custom resource as an extension not necessarily in a default install; dynamic registration; kubectl access identical to built-ins; on their own custom resources only store and retrieve structured data; combined with a custom controller they provide a true declarative API; declarative versus imperative; CRD defines a custom resource with a name and schema, and the API serves and stores it; the operator pattern combines custom resources and custom controllers). `k8s-docs-operator-pattern-2026-08-23.md` (motivation — capturing the human operator's knowledge; operators are clients of the API acting as controllers for a custom resource; extend cluster behaviour without modifying Kubernetes' own code; the automation examples; the controller normally runs outside the control plane, as a Deployment). `k8s-docs-extending-kubernetes-2026-08-23.md` (the published extension points, already quoted in Ch 2)
- **Figure**: none. The pattern is Chapter 3's loop with different labels, and drawing it here would spend the recognition that §9's Zenith needs. This is a deliberate withhold, not an oversight
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `★ **Fixed Point:**` — a custom resource alone stores structured data. A custom resource plus a custom controller is the operator pattern
  - `> 🪝 **Snag:**` — "we installed the CRD but nothing happened." This is the correct behaviour. **Name this as an instance of the book's recurring pattern — the object exists but nothing happens without the component** — the same shape as Ingress without a controller (Ch 10), `kubectl top` without metrics-server (Ch 13), and VPA not shipped by default (Ch 17). **[B3]** identifies this as one of the nine cross-cutting themes and specifies that naming it once and retrieving it by name turns four gotchas into one rule. **This is the naming.**
  - `> 🔭 **Closer Look:**` — API aggregation exists as the other extension route, with more flexibility and more work. One sentence; Chapter 17 owns extension points
- **Cross-bearings**: back to Ch 2 §4 (**mandatory — the pinned payoff**, with the section-number caveat in § Open questions #1); back to Ch 3's close (**mandatory** — "controllers you configure yourself"); back to §1 (the operator's own controller is deployed by a Deployment); forward to Ch 14 (CRDs shipped as chart content, and why charts have a `crds/` directory); forward to Ch 15 (Argo CD is a controller acting on custom resources); forward to Ch 17 (**the secondary Zenith** — CRI, CNI, CSI and CRDs collected)
- ⚠ **Do not teach the Operator Framework, OLM, Kubebuilder, or operator maturity levels.** None are in the cached sources and none are associate-tier
- ⚠ **Do not name Knative, Argo CD, or any specific operator implementation** beyond a forward pointer. Chapter 15 and Chapter 17 own them, and trap #82 lives in Ch 17

### §9 — ☀️ Nobody Sails One Pod

The chapter's one Zenith. Synthesis only — no new facts, no new vocabulary.

The move is a re-presentation. Take Chapter 3's control-loop shape and plug this chapter's controllers into it one at a time. The ReplicaSet's desired state is a number. The Deployment's is a template plus an update policy. The DaemonSet's is *one per matching node*, which is a number that the cluster computes rather than one you write. The Job's is *completion*. The CronJob's is *a Job existing at each scheduled time*. The operator's is whatever its author decided a database, or a certificate, or a message queue ought to look like. Six controllers, one shape, and the reader has been looking at the same diagram for the entire chapter without being told.

Then the second beat, which is the one that carries forward: the shape is not a Kubernetes implementation detail. It is the thing Kubernetes *is*. §8 already showed the reader that anyone can write a controller. Chapter 15 will show them a controller whose desired state lives outside the cluster entirely — in a Git repository — and that will look like a new technology right up until this section makes it look like the same one.

Close on the chapter title. Nobody sails one Pod: not because a single Pod is forbidden, but because a single Pod is a statement about right now, and every resource in this chapter is a statement about what should keep being true.

- **Objectives**: D1.1
- **Concepts introduced**: none — synthesis only
- **Sources**: no new tags. Every claim is already sourced in §1–§8
- **Figure**: `ch06-zenith-control-loop-instantiated`
- **Checkpoint after**: no
- **Markers planned**:
  - `☀️ **Zenith**` — the chapter's single Zenith marker
  - `🏆 **Safe Harbor**` — chapter close, after the Voyage Ahead
- **Cross-bearings**: back to Ch 3 §6 (the shape, first met); forward to Ch 15 (**the book's primary Zenith** — the same loop with desired state in a repository); forward to Ch 17 (the pattern named as a cloud-native principle)
- ⚠ **Do not introduce anything here.** If a fact appears for the first time in §9, it belongs in §1–§8. A Zenith that teaches is a summary wearing a costume

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 15 questions total.** B4 allocates 10; this raises it to 15 on B4's standing instruction that the minimum is *"a contract to exceed, not a target to hit."* All three shipped content chapters (3, 4 and 5) carry three checkpoints, so this is the book's established shape rather than an escalation. The structural case is that Chapter 6 has three genuinely separate arcs in three different cognitive modes — structural understanding (§1–§3), behavioral prediction with arithmetic (§4–§5), and taxonomic discrimination plus one abstraction jump (§6–§8). Folding those into two checkpoints would put unrelated modes in one block and pay an alternating-attention cost for nothing (skill Part 4). Chapter total moves 37 → 42.

**Retrieval-practice content: 20%** **[B3]** — drawn from **Chapters 3, 4 and 5**. Chapter 1 is excluded from the retrieval schedule entirely and no item may test exam mechanics. Against a combined Bearings-plus-Practice pool of 34, the 20% target is ~7 items, allocated **3 in Bearings and 4 in Practice** (7 of 34 = 20.6%).

Each of B3's three named anchors has exactly one section where it belongs:

| **[B3]** named anchor | Placement | Why here |
|---|---|---|
| **The control loop (Ch 3) now visible in a named controller** | Bearings #1, item 4 | §2 is the payoff for a promise Chapter 3 made by name. The retrieval and the promise are the same beat |
| **Selectors (Ch 4) as the ReplicaSet→Pod join** | Bearings #1, item 5 | §3 is where the join is made. Asking it immediately after is the shortest possible gap between teaching and retrieval, which is why this item has to be the *hard* version, not the recall version |
| **Probes (Ch 5) as what makes a rolling update safe** | Bearings #2, item 4 | §4 discharges Chapter 5's published promise. The retrieval is the discharge |

### ☆ Taking Your Bearings #1 — after §3

- **Topic**: what holds the intent, and how it finds its Pods
- **Questions**: 5
- **Retrieval from earlier chapters**: 2 of 5 (both **[B3]** named anchors; see the concentration note below)
- **Difficulty**: mostly ⚪, with item 5 at 🔵

  1. Name the three layers between a Deployment and a running container process, and say which layer holds the replica count and which holds the Pod template. **Tests §1's Fixed Point directly.** Trap answers must include a two-layer chain (Deployment → Pod) and a chain with the count and template swapped.
  2. You delete a Pod that a ReplicaSet owns. Describe what happens and what caused it. **Correct answer turns on nothing having been triggered** — a gap appeared and a loop closed it.
  3. A Deployment's template labels do not match its selector. Predict the state of the cluster sixty seconds later. **Correct answer: a growing population of Pods the controller cannot see, and a replica count that never appears satisfied.** This is the generation-effect prompt from §3, now as an assessment item.
  4. **Retrieval from Ch 3 §6 — the control loop.** Chapter 3 gave you a loop with two states and an action. Fill all three in for a ReplicaSet, using the actual field name for the desired state. **[B3]** named anchor, and the pinned Chapter 3 payoff appearing as an assessment item.
  5. 🔵 **Retrieval from Ch 4 §5 — selectors.** Chapter 4 listed four things that use label selectors and told you a ReplicaSet was one of them. Now that you have seen it work: a Service in Chapter 9 will select Pods with the same mechanism. What would it mean for one Pod to be selected by both a ReplicaSet and a Service at once? **Correct answer: nothing unusual — they are independent queries over the same labels, and the Pod is simply a member of two sets.** **The checkpoint's hardest item by design**, and it is doing setup work for Chapter 9 that a definition-recall item would waste.

- **Note on the 40% concentration.** Two of the chapter's three Bearings retrieval items land here because both **[B3]** anchors belong to §2 and §3 and nowhere else. Spreading them for an even per-checkpoint rate would place each one where it does not belong. The chapter's overall rate is 20.6%, which is the figure that matters.
- **Answer-key requirement**: item 1 needs full why-wrong treatment for the two-layer option. That compression is load-bearing for §4 — a reader who thinks a Deployment owns Pods directly cannot understand why two ReplicaSets exist during a rollout.

### ☆ Taking Your Bearings #2 — after §5

- **Topic**: changing the fleet, and what a change is recorded as
- **Questions**: 5
- **Retrieval from earlier chapters**: 1 of 5
- **Difficulty**: 🔵 throughout, with item 2 at 🟡

  1. A Deployment with ten replicas is updated using default strategy settings. What is the largest number of Pods that may exist during the update, and the smallest number that must be available? **Correct answer: twelve and eight, from the 25% defaults.** Trap answers must include the values with `maxSurge` and `maxUnavailable` swapped, and the version that treats 25% as applying to the pair jointly.
  2. 🟡 You scale a Deployment from three replicas to six, then run `kubectl rollout history`. How many revisions do you see, and why? **Correct answer: no new revision — scaling does not change the Pod template.** **This is the chapter's designated struggle item** — label it as such per Part 10B and normalize the difficulty, because the intuitive answer is wrong and the reader should be told that missing it is expected.
  3. Your application cannot run two versions at once because of a schema lock. Which strategy do you choose, and what exactly are you accepting? **Correct answer: `Recreate`, and you are accepting downtime as a deliberate cost.** The item exists to establish that `Recreate` is a choice, not a mistake.
  4. **Retrieval from Ch 5 §7 — probes.** You push a broken image. The new Pods start but never report ready. Describe what the Deployment does, and what the users of the service experience. **Correct answer: the rollout stalls with both ReplicaSets alive; the old Pods keep serving; users see nothing.** **[B3]** named anchor and the pinned Chapter 5 payoff. This is the item that converts probes from a health feature into a release-safety mechanism.
  5. You need to change the image, an environment variable, and the resource limits on one Deployment. How do you do it as one rollout rather than three, and what are the two commands? Tests `pause`/`resume` with its actual motivation attached.

- **Answer-key requirement**: item 4's key must stop short of diagnosis. Naming the stall is this chapter's job; `kubectl describe` and the event stream are Chapter 13's.

### ☆ Taking Your Bearings #3 — after §8

- **Topic**: the rest of the family, and the pattern extended
- **Questions**: 5
- **Retrieval from earlier chapters**: 0. The chapter's 20% is met by Bearings #1 items 4–5, Bearings #2 item 4, and four Practice items; a fourth Bearings retrieval would push this checkpoint off its own topic
- **Difficulty**: 🔵, with item 5 at 🟡

  1. An application writes to a local disk. Does that mean it needs a StatefulSet? Answer in one sentence and give the property that actually decides. **Correct answer: no — the deciding property is whether the Pods are interchangeable.** Trap answers must be built from B1 #21 in its exact wrong form.
  2. You need six copies of a service running for capacity. A colleague suggests a DaemonSet. What is wrong with that, and what determines a DaemonSet's Pod count? **Correct answer: a DaemonSet has no replica count; it runs one Pod per matching node, so the count is a consequence of the cluster** (B1 #22).
  3. Nightly, at 02:00, a report has to be generated and the process must exit when it is done. Name the resource, and name the resource it creates each time it fires (B1 #23).
  4. You install a CRD for a resource called `Backup`, then create a `Backup` object. `kubectl get backup` shows it. Nothing else happens. Is the cluster broken? **Correct answer: no — a custom resource alone stores structured data; without a controller there is nothing to act on it.** Trap answers should target "the CRD is misconfigured" and "it needs to be in kube-system."
  5. 🟡 **Interleaved with §1.** An operator manages a database. Where does the operator's own controller run, and using which of this chapter's resources? **Correct answer: outside the control plane, as an ordinary workload — normally a Deployment.** This item requires §1 and §8 together and it is the direct precursor to Chapter 15's recognition that a delivery tool is just another controller.

- **Answer-key requirement**: item 4's key must explicitly name the recurring pattern — *the object exists but nothing happens without the component* — because **[B3]** designates this as a named, retrievable theme and Chapters 10, 13 and 17 all retrieve it by that name.

---

## 6. Exam Alert plan

**High-priority topics** — the eight most likely to be tested directly, in descending order of confidence:

1. **The workload-resource decision** — which resource for which shape of work. This is the chapter's highest-value block and it is the one a recognition exam can ask about in a single sentence.
2. **Deployment versus StatefulSet is about interchangeability**, not about disk.
3. **DaemonSet is one Pod per matching node**, added automatically as nodes join, with no replica count.
4. **Job runs to completion once; CronJob runs a Job on a schedule.**
5. **The ownership chain** Deployment → ReplicaSet → Pod, and which layer holds what.
6. **`RollingUpdate` is the default strategy**; `maxSurge` and `maxUnavailable` both default to **25%**; `Recreate` kills all old Pods first.
7. **A revision is created if and only if the Pod template changes** — scaling does not create one.
8. **A CRD alone stores data; CRD plus custom controller is the operator pattern.**

**Common traps to call out.** Traps #21, #22 and #23 are all `[source]`-tagged in B1's D1 table, so all three may be described as things candidates get wrong. **None are `[inferred]`, so no hedging is required** — and equally, none may be dressed with invented frequency figures (Part 14 guardrail #8, and **[B3]**'s fourth do-not-retrieve rule).

| B1 # | Trap | Where it is defused |
|---|---|---|
| 21 | "Deployment vs StatefulSet is about whether the app writes to disk" | §6 Snag + Fixed Point, Bearings #3 item 1 |
| 22 | Reaching for a DaemonSet to "run several copies" | §7 Navigational Hazards, Bearings #3 item 2 |
| 23 | Job vs CronJob confusion | §7 Navigational Hazards, Bearings #3 item 3 |

All three share one root cause — choosing a resource by what the application *is* rather than by how its Pods need to be *managed* — which is why §7 carries a single hazards block naming the root cause rather than three scattered warnings. Naming it once converts three memorizations into one rule, and it is also what makes `ch06-fig04` a decision tree rather than a comparison table.

**Four non-B1 traps worth adding**, all documented in the cached Deployment and custom-resources sources. B1 catalogued these areas as blocking gaps (G8, G10) and therefore had no source to catalogue traps from; now that both gaps are closed, the traps are visible:

- **"Scaling creates a revision."** It does not — only a Pod template change does. Mechanically checkable, exactly the shape a multiple-choice item is built from. §5's hazards block.
- **`maxSurge` and `maxUnavailable` transposed.** The two names are symmetrical and the defaults are identical, which is precisely what makes them confusable. §4's mnemonic.
- **"`Recreate` is a mistake."** It is a supported strategy with a stated cost. Framing it as an error is its own trap. §4.
- **"Installing a CRD makes something happen."** §8's Snag, named as the recurring *object-without-component* pattern.

**Do not include** in the Exam Alert: blue/green, canary or A/B (Ch 15); PersistentVolume or access modes (Ch 11); VPA, KEDA, Cluster Autoscaler or Karpenter (Ch 17); rollout *diagnosis* procedures (Ch 13); any Helm rollback contrast (Ch 14 draws it).

---

## 7. Practice Questions plan

**19 questions** (B4 allocation, unchanged). Distribution follows section weight, not section count — §2 and §7 are short by design, but §7 carries three of the chapter's exam-priority topics and is weighted accordingly:

| Block | Questions | Notes |
|---|---|---|
| §1–§3 — ownership chain, ReplicaSet, selectors | 6 | Includes **2 retrieval items** |
| §4–§5 — rolling update, strategy, revisions, rollback | 6 | The chapter's arithmetic block; at least 2 must require a numeric answer |
| §6–§7 — StatefulSet, DaemonSet, Job, CronJob | 5 | Includes **1 retrieval item**. All three B1 traps must appear as distractors here, not only in the Exam Alert |
| §8 — custom resources and operators | 2 | Includes **1 retrieval item**. Two is correct for a definitional plant; more would over-teach material Chapters 15 and 17 own |

**Retrieval allocation: 4 of the 19 draw from Chapters 3–5**, allocated *within* this count and not added to it:

- **`spec` and `status` on a workload resource** (Ch 4 §2) — §1–§3 block. Framed as *where does the replica count you asked for live, and where does the number actually running live*, which is Chapter 4's abstraction with a second concrete instance.
- **Pod disposability and the new UID** (Ch 5 §4) — §1–§3 block. Framed against §2's replacement behaviour: the replacement Pod is not the old Pod recovered, and the reader should be able to say why that matters for anything holding the Pod's identity.
- **Pod phases `Succeeded` and `Failed`** (Ch 5 §5) — §6–§7 block, attached to Job. Deliberately the two phases Chapter 5 taught with no use case attached; this is the item that supplies the use case retroactively.
- **The control loop as a general shape** (Ch 3 §6) — §8 block, framed as *what does a custom controller have in common with kube-controller-manager's built-ins*. Deliberately phrased differently from Bearings #1 item 4 so it is a second retrieval rather than a repeat: that item asks the reader to fill in a ReplicaSet's two states, this one asks what generalizes.

**Interleaving strategy.** At least **five** questions must require two sections at once:

- Ownership chain + rolling update (§1 + §4) — why two ReplicaSets exist mid-rollout, and which one the Deployment is scaling down.
- Selector + StatefulSet (§3 + §6) — a StatefulSet's Pods are also selected by labels, yet they are not interchangeable. What does the selector *not* tell you?
- Revision rule + scaling (§5 + §2) — two changes, one revision; which one and why.
- Probes + rolling update (Ch 5 §7 + §4) — the stalled rollout, from the probe's side rather than the Deployment's.
- Operator + Deployment (§8 + §1) — the controller that extends Kubernetes is deployed by Kubernetes.

**Trap-answer requirement** (skill Part 11): every wrong option must target a specific misconception and the answer key must explain why each is wrong. For the §6–§7 block, wrong options should be drawn directly from B1 traps #21–#23 rather than invented — documented misconceptions make better distractors than plausible-sounding fabrications, and they are the ones the reader will actually meet.

**One calibration note.** This chapter divides cleanly into two question modes: *selection* ("which resource, and why") and *prediction* ("what does the cluster do next"). Both are legitimate and the block distribution above roughly balances them. What to avoid is the third mode — field-name recall divorced from behaviour. `maxSurge` is worth a question because the *number it produces* is worth knowing; it is not worth a question that asks the reader to identify which of four field names is spelled correctly.

---

## 8. Required figures

Six anchors, exactly as the arc outline specifies. §2, §3, §5 and §8 deliberately carry none — see each section's Figure line for the Part 18.3/18.7/18.9 reasoning. §4 carries two, which is the one deviation from one-per-section and is justified below.

### `ch06-fig01-deployment-replicaset-pod-ownership`

- **Purpose**: §1's Fixed Point, dual-coded. The reader's structural template for every workload in the rest of the book, and the figure §4's two-ReplicaSet rollout depends on.
- **Content**: three stacked layers. Deployment at the top, visibly holding two things — a Pod template and an update strategy. One ReplicaSet below it, holding a replica count. Three Pods below that, each visibly a copy of the template. Ownership arrows point *downward* from owner to owned; the reader should be able to see that intent flows down and existence is reported up.
- **Design requirement — the layer attribution is the pedagogy.** Which layer holds the template and which holds the count must be readable without the caption. A figure that draws three boxes with unlabelled arrows teaches the chain but not the division of labour, and the division of labour is what §4 and §5 both rest on. Must survive grayscale (Part 18.11).
- **Label count**: Deployment, ReplicaSet, three Pods (one label), template, replica count, strategy — seven. At the Part 18.12 ceiling; do not add anything.
- **Reuse note**: Chapter 14 and Chapter 15 both refer back to this shape. Design it once for three appearances.

### `ch06-fig02-rolling-update-maxsurge-maxunavailable`

- **Purpose**: §4's Fixed Point. A quantitative relationship, which Part 18.9 names explicitly as warranting a diagram.
- **Content**: a horizontal band chart across time. A centre line at the desired replica count. A dashed ceiling above it at desired + `maxSurge`, and a dashed floor below it at desired − `maxUnavailable`. Two populations drawn against that band — old-version Pods declining, new-version Pods rising — with the total staying inside the ceiling and the available count staying above the floor throughout.
- **Design requirement — the two bounds must be visually opposite.** Surge is a ceiling on *total*; unavailable is a floor on *available*. Drawing them as two lines of the same kind on the same axis is what produces the transposition error the mnemonic exists to prevent. Above-the-line versus below-the-line is the whole design.
- **Label count**: desired, surge ceiling, unavailable floor, old population, new population, time axis — six. Within budget.
- **Note**: use the worked ten-replica example's actual numbers (12 and 8) rather than abstract symbols. The figure and the prose should be the same example.

### `ch06-fig03-recreate-vs-rolling`

- **Purpose**: §4's contrast, and the chapter's one comparative illustration (Part 18.10).
- **Content**: two timelines, stacked. Upper — `Recreate`: all old Pods terminate, a visible gap where zero Pods are available, then new Pods start. Lower — `RollingUpdate`: the two populations overlap and available count never reaches zero. Same time axis, same replica count, so the two are directly comparable.
- **Design requirement — the gap is the pedagogy.** The zero-availability window in the upper timeline must be the most visually prominent thing in the figure. Everything else is context for that gap. If the gap is subtle, the figure has failed.
- **Label count**: two strategy names, the gap, two populations, time axis — six. Within budget.
- **Note on carrying two figures in one section**: fig02 explains the mechanism's bounds; fig03 explains why the mechanism exists at all. Merging them would put four timelines and three reference lines in one frame, well over the label ceiling, teaching both things worse. Keep them separate.

### `ch06-fig04-workload-resource-decision-tree`

- **Purpose**: §7's payoff and the chapter's most practically useful artifact. The single figure that defuses B1 traps #21, #22 and #23 together.
- **Content**: a decision tree with four questions and six leaves. *Does the work end?* → yes: *does it repeat on a schedule?* → CronJob / Job. → no: *does it need to run on every node?* → yes: DaemonSet. → no: *are the Pods interchangeable?* → yes: Deployment (with ReplicaSet noted as what it manages) / no: StatefulSet.
- **Design requirement — question order is load-bearing.** The tree must ask about the *shape of the work* before it asks about the *nature of the application*, because reversing that order is precisely the root cause the §7 hazards block names. A tree that opens with "is it stateful?" reproduces the trap it is supposed to defuse.
- **Label count**: four decision nodes, six leaves — ten. **Over the ~7 ceiling**, which is a real constraint. Resolution: a decision tree is read sequentially along one path rather than apprehended as a whole, so working memory holds one branch at a time rather than ten simultaneous labels. This is the same exemption a flowchart earns and it is the reason Part 18.10 lists decision trees as a concept-diagram type. If the illustrator finds it still reads as crowded, the fix is to shorten the node text, not to prune branches — all six resources must appear or the tree stops being usable.
- **Reuse note**: this is the figure readers will screenshot. It also belongs in The Lodestar. Design it to be legible at one-quarter page.

### `ch06-fig05-statefulset-vs-deployment-identity`

- **Purpose**: §6's Fixed Point, and **half of a designed reciprocal pair** with `ch11-fig05`.
- **Content**: two rows. Upper — a Deployment: three Pods with opaque generated names, and an arrow showing one being replaced by a fourth Pod with a *different* name, with the caption-level point being that nothing depended on which one it was. Lower — a StatefulSet: three Pods with ordinal names, each attached to its own storage, and an arrow showing one being replaced by a Pod with the *same* name reattaching to the *same* storage.
- **Design requirement — the storage attachment must be drawn as belonging to the identity, not to the Pod.** That is the claim Chapter 11 completes, and if this figure attaches storage to the Pod it will contradict `ch11-fig05` rather than set it up. **Build the two figures together.** ⚠ This is the book's one deliberate forward reference and the figure pair is the mechanism that closes it.
- **Label count**: two resource names, two Pod sets (one label each), storage, replacement arrows — seven. At the ceiling.
- ⚠ **Blocked on the StatefulSet source gap.** The interchangeability claim is sourceable today from the workloads overview; the ordinal-naming convention is not. See § Open questions #2 and #5 — if the fetch does not land, the lower row must use generic distinct names rather than invented ordinals.

### `ch06-zenith-control-loop-instantiated`

- **Purpose**: the chapter's one Zenith, and **the middle beat of the book's three-beat spine**.
- **Content**: Chapter 3's control-loop shape at the centre — unmistakably the same shape as `ch03-fig02`, not a redrawn variant — with this chapter's six controllers arranged around it, each one showing only what its desired state *is*: a number, a template plus a policy, one-per-matching-node, completion, a schedule, and "whatever its author decided." The loop itself is drawn once. That is the argument.
- **Design requirement — visual continuity with `ch03-fig02` is the entire point.** `ch03-fig02` was flagged in the arc outline as the book's most reused figure, to be designed deliberately for re-presentation at three later altitudes. This is altitude two. If the reader does not recognize the shape on sight, the figure has failed and Chapter 15's Zenith loses its setup. Coordinate with whoever renders `ch03-fig02` and with `ch15`'s Zenith spec.
- **Label count**: the loop's two states plus six desired-state descriptors — eight. At the ceiling and justified: the count *is* the argument. Dropping one controller to hit seven would weaken the claim that all of them are the same shape.
- **Register note**: Communications Officer family, junior tier. This is a dramatic synthesis illustration, not a reference diagram (Part 18.10) — it carries the brand's illustrative register, unlike `fig04`, which is deliberately utilitarian. The fleet image is available and the chapter is named for it. Use it once, here, and let §1–§8's prose stay plain per B2's density guidance.

---

## 9. Open questions for the author

1. **⚠ BLOCKING (editorial) — three published chapters point at Ch 6 §3 and want three different things.**

   | Published pointer | Wants §3 to be | Status under this plan |
   |---|---|---|
   | `chapter-04` line 688 | *"a controller's selector and the Pods it owns"* | **Honored** — §3 is exactly this |
   | `chapter-01` line 435 | *"StatefulSets and stable identity"* | **Broken** — StatefulSet is §6 |
   | `chapter-02` line 600 | *"CRDs and extending the API"* | **Broken** — CRDs are §8 |

   No numbering satisfies all three; at least two must be edited regardless of how this chapter is arranged. **Recommendation: keep the plan above and make two one-token edits in shipped text** — `chapter-01` line 435 `§3` → `§6`, and `chapter-02` line 600 `§3` → `§8`.

   The reasoning: Chapter 4's pointer is honored because it is a real in-prose navigational pointer dropped at the exact moment the reader meets the ReplicaSet→Pod selector join, and because its topic sits naturally at §3 in a dependency-ordered chapter. Chapter 1's is an *illustration of the cross-bearing convention* ("you'll see pointers like…") rather than a navigational aid, so it costs the least to correct. Chapter 2's sits in the load-bearing four-sockets list and matters more, but CRDs cannot move earlier than §8 without teaching API extension before the reader has met a single built-in controller. Both edits are mechanical and neither changes a sentence's meaning. Also worth noting: Chapter 5's Voyage Ahead independently confirms this plan's §3 and §4 in prose — *"Probes are what make a rolling update safe. Labels are how a controller finds the Pods it owns"* — in that order.

2. **⚠ BLOCKING — five research gaps, four of them load-bearing.** B1's two named gaps for this chapter (G8, G10) are both **closed**: `k8s-docs-deployment-2026-08-23.md` covers strategy, both bounds and their defaults, the revision rule, rollback, and pause/resume; `k8s-docs-custom-resources-2026-08-23.md` and `k8s-docs-operator-pattern-2026-08-23.md` fully cover §8. What B1 did not anticipate is that **none of the sibling workload-resource pages are cached** — the entire family is currently sourced from one paragraph each in the workloads overview.

   | Gap | Page | Blocks | Severity |
   |---|---|---|---|
   | **ReplicaSet** | `kubernetes.io/docs/concepts/workloads/controllers/replicaset/` | §2's definition, §3 entirely | **Blocking.** §3 has no primary source for its ownership half at all, and §2's "maintain a stable set of replica Pods" is currently paraphrase |
   | **Owners and dependents / garbage collection** | `kubernetes.io/docs/concepts/architecture/garbage-collection/` | §3's ownerReferences and cascading deletion | **Blocking.** Same section, second half |
   | **StatefulSet** | `kubernetes.io/docs/concepts/workloads/controllers/statefulset/` | §6, and the lower row of `ch06-fig05` | **Blocking.** The interchangeability claim is sourceable from the workloads overview; ordinal naming and ordering guarantees are not |
   | **DaemonSet** | `.../controllers/daemonset/` | §7's first third | **Blocking.** One cached paragraph is enough for the concept but not for a section |
   | **Job and CronJob** | `.../controllers/job/` and `.../controllers/cron-jobs/` | §7's remainder | High. The once-versus-schedule distinction is cached; nothing else is |

   None of these are exotic. All five are core concept pages and the fetch is routine — flagging them because the chapter *looks* well-sourced (its two named gaps closed) while four of its nine sections are actually running on secondary mentions.

3. **How much ownership machinery is associate-tier?** §3 as planned teaches: selector-based membership, template-labels-must-agree, owner references, cascading deletion, and the overlapping-selector hazard. It does **not** teach finalizers, foreground versus background deletion, or `--cascade=orphan`. **Recommendation: hold that ceiling, and add controller *adoption* of pre-existing bare Pods only if the fetched ReplicaSet page presents it plainly** — it is the fact that makes "membership is a query" viscerally true, and it is also the one that most often surprises people. `--cascade=orphan` should stay out regardless; it is a `kubectl` flag, which makes it Chapter 8's territory even if the concept is §3's.

4. **Horizontal versus vertical scaling — plant in §2, or hold entirely for Ch 17?** B2 splits autoscaling deliberately: manual scaling and the HPA *concept* here, the landscape (VPA, KEDA, Cluster Autoscaler, Karpenter) in Chapter 17. Trap #103 (confusing horizontal with vertical) is a D4 trap and Chapter 17 defuses it. **Recommendation: one clause in §2 naming horizontal scaling as "changing the number of replicas" with a forward cross-bearing, and no mention of vertical scaling at all.** Introducing the contrast here means introducing it without VPA to attach it to, which produces a definition the reader has nowhere to put. The clause costs nothing and gives Chapter 17 the word it needs to contrast against.

5. **StatefulSet depth ceiling — confirm.** §6 as planned teaches: Pods are not interchangeable, identities are stable, each Pod is typically matched with its own storage, and the distinguishing property is interchangeability rather than disk. Ordinal naming and ordered creation/termination are *conditional on the source fetch* and, if included, should be one sentence. Everything else — PV, PVC, StorageClass, access modes, headless Services, the actual provisioning path — is Chapter 11's or Chapter 9's. **Recommendation: hold the ceiling and make the open loop explicit in prose.** B2's justification for this placement is that the taxonomy belongs here; if §6 grows past the taxonomy it will have taken Chapter 11's material without Chapter 11's prerequisites, which is exactly the failure the split was designed to avoid.

6. **`minReadySeconds` and `progressDeadlineSeconds` — in or out?** Neither is in the cached Deployment snapshot, which covers strategy, bounds, rollback and pause/resume but stops short of the timing fields. `minReadySeconds` is the field that makes §4's safety argument precise rather than hand-wavy, and it connects directly to Chapter 5's probes. `progressDeadlineSeconds` is what actually produces the "stuck rollout" signal the cached source alludes to. **Recommendation: include `minReadySeconds` in §4 if the fetch supports it, at one sentence; include `progressDeadlineSeconds` only as the mechanism behind the stuck-rollout status, not as a tunable to configure.** If neither lands, §4's safety claim still works — it just rests on readiness alone.

7. **ReplicationController — one clause, or omit?** The cached workloads page names it as the legacy resource ReplicaSet replaced. It appears in old tutorials and in `kubectl scale`'s own help text (which the cached kubectl overview reproduces: *"update the size of the specified replication controller / deployment"*). **Recommendation: one clause in §1, as a name the reader may meet and should recognize as superseded.** Omitting it entirely means a reader who hits it in a search result has no way to know it is obsolete; a paragraph would be teaching a dead resource.

8. **Bearings raised 10 → 15.** Sanctioned by B4's standing instruction and consistent with Chapters 3, 4 and 5, all of which shipped three checkpoints. **Recommendation: accept.** Chapter total moves 37 → 42 against a book already well clear of the 300 floor, and the Stage 8 question-quality audit is expected to cut weak items anyway. If the author prefers B4's exact table, drop Bearings #3 to 4 by folding items 2 and 3 — but note that costs trap #22 or #23 its checkpoint coverage, and those are two of the chapter's three documented traps.

9. **Nine sections — confirm, or fold.** Two fold options exist: §2 into §1 (the ReplicaSet loop as the second movement of the ownership section), and §5 into §4 (revisions as the tail of the rollout section). **Recommendation: keep nine.** §2 exists to pay a promise Chapter 3 made by name, and burying that payoff inside a longer section would waste it. §4 is already the chapter's highest-attention-cost section and adding the revision rule plus five `kubectl rollout` verbs would make it the section readers abandon. Folding §5 would also break the natural split point after Bearings #2, which is the cleanest seam in the chapter.

10. **Domain weight disclosure.** `domain_weight_pct: 6` is authored judgment, not published data — CNCF publishes four domain weights and twelve named competencies with no sub-weights (B1 §G33, §G36). The front matter already carries the disclosure. **No action needed**; recorded here so the drafting stage does not present 6% as an official figure in the chapter's metadata line. Match whatever phrasing Chapters 2–5 already published.

11. **Confirm what Chapter 6 does *not* touch.** Scheduling, `nodeSelector`, affinity and taints (Ch 7); `ResourceQuota`, `LimitRange`, node lifecycle and the `kubectl` command surface (Ch 8); Services, EndpointSlice, headless Services (Ch 9); PersistentVolume, PVC, StorageClass, access modes (Ch 11); RBAC and ServiceAccount permissions (Ch 12); rollout and Pod-failure *diagnosis* (Ch 13); Helm charts, releases, and Helm's own rollback (Ch 14); blue/green, canary, A/B, GitOps, Argo CD (Ch 15); the four-socket extension synthesis, VPA, KEDA, Cluster Autoscaler, Karpenter, Knative, service mesh (Ch 17); log agents as an observability topic (Ch 18). **Recommendation: hold all of these out.** This chapter's material touches more of the book than any other in Part II — six of these are places where a single extra paragraph would feel natural and would cost a later chapter its setup.