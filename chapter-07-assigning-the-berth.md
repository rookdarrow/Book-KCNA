---
chapter: 7
chapter_type: "content"
title: "Assigning the Berth"
subtitle: "Filter, score, bind — and then a coin flip"
exam_domain: "Kubernetes Fundamentals (competency: Scheduling)"
domain_weight_pct: 5
complexity: "mixed"
novelty: "moderate"
prereq_factor: "standard"

#-- COMPLEXITY NOTE. The arc outline characterises this chapter as
#-- "procedural material with a clean three-step spine". That is true of
#-- §1-§2 and it is why the depth band is "standard". It is not true of
#-- §3-§5, which are four separate placement vocabularies that the reader
#-- must discriminate between rather than execute. `mixed` is the honest
#-- value; the arc's "procedural" describes the spine, not the whole
#-- chapter. See § Open questions #6.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band for this chapter:
#-- "standard" - 5 points, procedural material with a clean three-step
#-- spine. Planning signal only, NOT a target.
#--
#-- SECTION NUMBERING - two published cross-bearings point into this
#-- chapter with an explicit section number, and two more point at the
#-- chapter with no number (no constraint).
#--   chapter-05 line 969 -> *[see Ch 7 §2 - resource requests as a
#--                            scheduling filter]*            <-- HONORED
#--   chapter-02 line 807 -> *[see Ch 7 §3 - node selection,
#--                            tolerations, and accounting for
#--                            overhead]*                     <-- PARTIAL
#--   chapter-03 line 417 -> *[see Ch 7 - how the scheduler actually
#--                            chooses, in detail]*           (unnumbered)
#--   chapter-04 line 688 -> *[see Ch 7 - node labels and nodeSelector]*
#--                                                           (unnumbered)
#-- The chapter-02 pointer names three topics that cannot share a section
#-- under any dependency-sane arrangement: overhead is resource accounting
#-- (§2), node selection is the Pod's attraction side (§3), tolerations
#-- are the node's repulsion side (§4). §3 honors one of the three.
#-- See § Open questions #1 for the recommended one-token edit.
sections:
  - name: "One Decision, Made Once"
    objectives: ["D1.3"]
    requires_figure: true
    figure_anchor: "ch07-fig01-filter-score-bind"
    checkpoint_after: false
  - name: "What Makes a Node Feasible"
    objectives: ["D1.3"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Asking for a Particular Berth"
    objectives: ["D1.3"]
    requires_figure: true
    figure_anchor: "ch07-fig02-nodeselector-vs-affinity"
    checkpoint_after: false
  - name: "When the Berth Refuses You"
    objectives: ["D1.3"]
    requires_figure: true
    figure_anchor: "ch07-fig03-taints-tolerations-effects"
    checkpoint_after: true
  - name: "Placing Pods Relative to Each Other"
    objectives: ["D1.3"]
    requires_figure: true
    figure_anchor: "ch07-fig04-pod-affinity-anti-affinity-topology"
    checkpoint_after: false
  - name: "Overruling the Scheduler, and Replacing It"
    objectives: ["D1.3"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Everything Is a Filter or a Score"
    objectives: ["D1.3"]
    requires_figure: true
    figure_anchor: "ch07-zenith-berth-assignment"
    checkpoint_after: false

#-- Seven sections against Chapters 5 and 6's nine. This chapter carries
#-- two points less weight and one competency instead of a whole
#-- sub-domain's worth of resources. See § Open questions #7 for the
#-- fold/split options considered and rejected.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "choosing a machine for a job from a fleet with different free capacity - what you need to know in advance"
    - "two candidates that are equal on every measure you can name - how you choose, and whether it matters"
    - "retrieval from Ch 5 - requests versus limits, and which one Ch 5 said the scheduler reads"
    - "retrieval from Ch 5 - a running Pod's node fills up; Ch 5 said a Pod is scheduled once, so what happens"
    - "reserving machines for one team - marking the machines versus marking the jobs, and what each costs"
    - "retrieval from Ch 6 - the loop wants one more Pod and there is nowhere to put it; what does the loop do"
    - "two copies of a service for redundancy both land on the same machine - what was lost, and what would have prevented it"
    - "pinning a job to a specific worker - one good reason, one reason it is a bad habit"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 17 = 35. Bearings raised 10 -> 15 across 3
#-- checkpoints (5 + 5 + 5), matching the shape shipped by Chapters 3, 4,
#-- 5 and 6. See § Taking Your Bearings checkpoints.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 17
  total_this_chapter: 40

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D1.3"]
  concepts:
    - "scheduling"
    - "kube-scheduler"
    - "unbound-pod"
    - "feasible-node"
    - "filtering"
    - "scoring"
    - "binding"
    - "random-tie-break"
    - "unschedulable"
    - "pending-pod"
    - "podfitsresources"
    - "requests-as-scheduling-input"
    - "node-capacity"
    - "node-allocatable"
    - "pod-overhead"
    - "scheduled-once-per-lifetime"
    - "node-labels"
    - "standard-node-labels"
    - "nodeselector"
    - "node-affinity"
    - "required-during-scheduling"
    - "preferred-during-scheduling"
    - "ignored-during-execution"
    - "affinity-operators"
    - "taint"
    - "toleration"
    - "noschedule"
    - "prefernoschedule"
    - "noexecute"
    - "tolerationseconds"
    - "taint-toleration-matching"
    - "built-in-node-condition-taints"
    - "pod-affinity"
    - "pod-anti-affinity"
    - "topology-domain"
    - "topology-key"
    - "topology-spread-constraints"
    - "nodename"
    - "direct-node-assignment"
    - "schedulername"
    - "custom-scheduler"
    - "scheduling-policies"
    - "predicates"
    - "priorities"
    - "scheduling-profiles"
    - "scheduler-plugins"
  commands:
    - "kubectl-get-nodes"
    - "kubectl-get-pods"
    - "kubectl-label"
    - "kubectl-taint"

figures_planned:
  - "ch07-fig01-filter-score-bind"
  - "ch07-fig02-nodeselector-vs-affinity"
  - "ch07-fig03-taints-tolerations-effects"
  - "ch07-fig04-pod-affinity-anti-affinity-topology"
  - "ch07-zenith-berth-assignment"
---

# Chapter 7: Assigning the Berth
## *"Filter, score, bind — and then a coin flip"*

**Exam domain: Kubernetes Fundamentals (44% of the exam) — competency: Scheduling** [source: cncf-kcna-certification-page-2026-08-23] [source: cncf-kcna-curriculum-pdf-2026-08-23] **| Estimated share of the exam: ~5% (authored allocation — CNCF publishes domain weights, not competency weights** [source: cncf-kcna-curriculum-pdf-2026-08-23]**; see front matter) | Complexity: Mixed | Novelty: Moderate**

<!-- AUTHOR-REVIEW: the metadata line above was conformed to the shipped ch-02 / ch-05 house form, which carries the published 44% domain weight and both CNCF source tags inline rather than in a separate italic disclaimer. Neither cncf-kcna-certification-page-2026-08-23 nor cncf-kcna-curriculum-pdf-2026-08-23 was in this stage's referenced-snapshot slice, so the 44% figure is copied from those shipped chapters rather than re-derived. Verify once against the curriculum PDF at book-level reconciliation. -->

---

## Attention Budget

**Total time: ~130 minutes | Recommended: split across two sessions, with the break after ☆ Taking Your Bearings #2**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 — One Decision, Made Once | 10 min | Low | Anytime |
| §2 — What Makes a Node Feasible | 15 min | Medium | When alert |
| ☆ Taking Your Bearings #1 | 8 min | Medium | Straight after §2 |
| §3 — Asking for a Particular Berth | 15 min | Medium | When alert |
| §4 — When the Berth Refuses You | 25 min | **High** | Peak attention |
| ☆ Taking Your Bearings #2 | 8 min | Medium | After a short break |
| §5 — Placing Pods Relative to Each Other | 18 min | Medium-high | When alert |
| §6 — Overruling the Scheduler, and Replacing It | 14 min | Medium | Anytime |
| ☆ Taking Your Bearings #3 | 8 min | Medium | After a short break |
| §7 — Everything Is a Filter or a Score | 6 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** concrete, familiar, or synthesis material — study anytime.
- **Medium:** new concepts requiring focus — study when alert.
- **High:** dense discrimination work — study at peak attention.

*If you only have 15 minutes:* read §1, then read §4's three-effect table, then work ☆ Taking Your Bearings #2. That is, in my judgement, the densest fifteen minutes in the chapter. §1 is the frame every other fact hangs on, and the three taint effects are the tightest discrete-recall block here.

---

> *"The hard part of assigning a berth is not choosing well. It is that you only choose once."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score decides how to read, not whether you're allowed to. There's no wrong answer to arrive with, only different starting positions.

Most of these are about assigning work to machines in general. Three of them ask you to retrieve something specific from Chapters 5 and 6.

1. You have eight machines with different amounts of free memory, and a job that needs 8 GB. Describe how you'd pick a machine for it. Then say what you'd have to know **in advance** to pick it automatically, with no human looking.

2. Two candidate machines come out identical on every measure you can name. How do you choose between them, and does the choice matter?

3. A container declares both a *request* and a *limit* for memory. Chapter 5 said one of those two numbers is read by the scheduler and the other is enforced by the kubelet on the running container. Which is which?

4. A Pod is running happily. Its node then fills up with other work. Chapter 5 was emphatic that a Pod is scheduled once in its lifetime. So what does Kubernetes do about the crowded Pod — move it, or something else?

5. Some machines in your fleet are reserved for one team's workloads. There are two ways to express that: mark the machines, or mark the jobs. What does each approach cost you when a job arrives that nobody remembered to mark?

6. A ReplicaSet wants three Pods and two exist, so it creates a third. There is nowhere in the cluster with room for it. What does the loop do next — give up, retry, error, or something else?

7. You run two copies of a service so that one machine failing doesn't take the service down. Both copies land on the same machine. What have you actually lost, and what would you have had to say in advance to prevent it?

8. In any system that assigns work to workers, give one good reason to override the assignment and pin a job to a named worker — and one reason it's a bad habit.

<details>
<summary>Answers + reading strategy</summary>

1. **Pick one with at least 8 GB available, ideally with headroom.** To automate it, the job's requirement has to be *declared* somewhere a machine can read it. You can't discover "this job needs 8 GB" by looking at a job that hasn't started yet. Hold onto the word *available*; §2 is mostly about what it means.

2. **Any consistent rule works** — lowest hostname, round-robin, least-recently-used. For correctness it doesn't matter. For behaviour it does: a predictable rule concentrates load in predictable places. Kubernetes' actual answer is in §1, and it isn't any of the three above.

3. **The request is the scheduler's input; the limit is the kubelet's enforcement ceiling.** If you had them backwards, mark question 3 wrong and read the note at the bottom of this box.

4. **Nothing moves it.** A Pod is scheduled once and is never rescheduled to a different node. If it has to leave, it is *replaced* by a different Pod, not relocated.

5. **Mark the jobs** and unmarked jobs will happily land on the reserved machines, because nothing told those machines to say no. **Mark the machines** and unmarked jobs are excluded by default. But marking the machines only changes what they *refuse*. Whether it also changes where your marked jobs actually land is a separate question, and §4 turns on the answer.

6. **Nothing dramatic.** The loop's job was to create the missing Pod, and it did. The Pod now exists; it simply has nowhere to run. What the Pod's own status says while that's true is §2's material, and it is worth more than it looks.

7. **You lost the redundancy.** One machine failure now takes down both copies, which is exactly the outcome the second copy existed to prevent. To prevent it you'd have had to say, in advance, that the two copies must not share a machine. Nothing about "two copies" implies "two machines."

8. **Good reason:** the work is tied to something only that machine has — a device, a local disk, a licence dongle. **Bad habit:** the assignment stops adapting. If the machine is full, down, or renamed, the job has nowhere to fall back to, and you've opted out of every check the assigner was performing for free.

---

**If you got 6+ right:** skim. Read §1 and §4 properly, note the ★ Fixed Points and the ⚠ Navigational Hazards, and go straight to the checkpoints. You have the instincts; this chapter is supplying the vocabulary and one or two facts that will surprise you.

**If you got 3–5 right:** read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** read carefully, and start with §1 rather than skipping ahead. **If questions 3, 4 and 6 were among your misses, go back and re-read Chapter 5 §8 and Chapter 5 §4 first.** Those two sections are the entire prerequisite base for §1 through §3, and §2 will read as a list of arbitrary rules without them.

</details>

---

## Why This Chapter Matters

The last chapter ended on the one thing the control loop cannot do. It creates a Pod. It does not decide where the Pod goes. That gap is what this chapter closes. The interesting part isn't that a component called the scheduler picks a node. It's that the choice is made **once**, by a component that does not run anything, and is then never revisited. Pods are scheduled once in their lifetime to a specific node, and a Pod is never "rescheduled" to a different node [source: k8s-docs-pod-lifecycle-2026-08-23]. The machine a Pod lands on is the machine it dies on. Every label, every affinity rule, every taint in this chapter exists for one reason: that decision is irreversible, and you get exactly one chance to influence it.

Chapters 4 through 6 made you someone who can write down what should exist. This chapter makes you someone who can also write down *where* it should exist, and where it must not. That's a real shift. It's the first point in this book where you're reasoning about the cluster as a heterogeneous place — machines with different hardware, different owners, different health — rather than as a uniform pool of capacity. Practitioners hold both directions in their heads at once: what a workload needs from a machine, and what a machine is willing to accept. Newcomers only ever think about the first, which is why a node refusing their Pod reads as the cluster being broken.

The stakes, stated flat. Five points on this book's allocation, which is not a lot. What that number doesn't capture is that scheduling is where four separate facts live that have no home anywhere else in the curriculum: that the decision is a two-step operation, that ties are broken at random, that binding is a notification rather than an action, and that a Pod which can't be placed sits in `Pending` rather than erroring. Each is one sentence. Each is exactly the shape a recognition exam tends to ask about. This chapter is short on volume and dense on returns.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Trace** a Pod from creation to placement through the scheduler's two-step operation, and say what "binding" actually consists of.
- **Name** the factors a scheduling decision takes into account, and say which of them you can influence from a Pod spec or a node label.
- **Explain** why a node with free memory can still be infeasible for a Pod that needs less memory than the node has.
- **Distinguish** the mechanisms for influencing placement by which direction each one asserts — from the Pod, or from the node.
- **Predict** what happens to an already-running Pod when its node gains a taint, changes a label, or fills up.
- **Choose** between `nodeSelector`, node affinity, taints, and inter-Pod rules for a given placement requirement, and say what each one costs.
- **Recognise** every constraint in this chapter as either a filter or a score — which is the only thing you actually have to remember.

*You'll also stop reading `Pending` as an error message, which is a smaller change than it sounds, and I think it saves more marks than anything else here.*

---

## ⚪ §1 — One Decision, Made Once

You met the scheduler in Chapter 3 as a control-plane component and were told, in as many words, that *how* it chooses was being held back until later *[cross-bearing: see Ch 3 §2 — the control plane components]*. This is later.

A scheduler watches for newly created Pods that have no node assigned; for every such Pod it discovers, it becomes responsible for finding a node for that Pod to run on [source: k8s-docs-kube-scheduler-2026-08-23]. `kube-scheduler` is the default one, and it runs as part of the control plane [source: k8s-docs-kube-scheduler-2026-08-23]. The nodes that meet a Pod's scheduling requirements are called **feasible nodes** [source: k8s-docs-kube-scheduler-2026-08-23].

### What goes into the decision

Feasibility is not only about free memory. The documented list of factors a scheduling decision takes into account runs: individual and collective resource requirements, hardware / software / policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and so on [source: k8s-docs-kube-scheduler-2026-08-23]. *Deadlines* are named alongside them in the architecture overview [source: k8s-docs-cluster-architecture-2026-08-23].

This chapter teaches the ones you can control from a Pod spec or a node label: resource requirements, hardware and policy constraints, and affinity. The rest are named here so you recognise them on a list, and so that *"the scheduler checks whether the node has enough memory"* doesn't calcify into the whole story.

### The spine

`kube-scheduler` selects a node in a **2-step operation: filtering, then scoring** [source: k8s-docs-kube-scheduler-2026-08-23].

**Filtering** finds the set of nodes where it is feasible to schedule the Pod. After this step the node list contains any suitable nodes — often more than one. If the list is empty, that Pod isn't yet schedulable [source: k8s-docs-kube-scheduler-2026-08-23].

**Scoring** ranks the survivors. The scheduler assigns a score to each node that survived filtering, based on the active scoring rules, and then assigns the Pod to the node with the highest ranking [source: k8s-docs-kube-scheduler-2026-08-23].

**Binding** is what happens next, and it is not what most people assume. The scheduler notifies the API server about its decision, and *that* is what the word binding names [source: k8s-docs-kube-scheduler-2026-08-23].

<!-- FIGURE: ch07-fig01-filter-score-bind -->
```
   UNBOUND POD
   ┌───────────────┐
   │ spec.nodeName │   (empty — this is what the scheduler watches for)
   └───────┬───────┘
           │
           ▼
 ┌──────────────────┐    ┌──────────────────┐    ┌───────────────────────┐
 │  1. FILTER       │    │  2. SCORE        │    │  3. BIND              │
 │                  │    │                  │    │                       │
 │  node-a   keep   │    │  node-a ..... 72 │    │  kube-scheduler       │
 │  node-b   drop   │───▶│  node-c ..... 91 │───▶│         │             │
 │  node-c   keep   │    │  node-e ..... 68 │    │         ▼             │
 │  node-d   drop   │    │                  │    │  kube-apiserver       │
 │  node-e   keep   │    │  highest wins    │    │  "this Pod: node-c"   │
 │                  │    │                  │    │                       │
 │  = FEASIBLE SET  │    │                  │    │                       │
 └──────────────────┘    └──────────────────┘    └───────────────────────┘

     ─ ─ ─ ─ ─  separate actor, separate moment, separate arrow  ─ ─ ─ ─ ─

                     ┌────────────────────────────────────┐
                     │  kubelet on node-c                 │
                     │         │                          │
                     │         ▼                          │
                     │  container runtime → containers    │
                     └────────────────────────────────────┘
```

Look at where the third arrow goes. The scheduler's arrow lands on the **API server**, not on node-c. Nothing in the scheduler ever touches a container. The kubelet on the chosen node is what starts anything, and it does so because it saw the recorded decision. Not because the scheduler told it to.

> ★ **Fixed Point:**
>
> **The scheduler filters, then scores, then binds. Filtering produces the feasible set; scoring ranks it; binding is a notification to the API server. The kubelet on the chosen node is what actually starts the containers.**

> 🪢 **Mnemonic:** *Filter, score, bind* — three words, in the order they happen, and they're printed on the front of this chapter. If you can say the three words you have most of §1.

### And then a coin flip

Here is the fact that surprises people.

If there is more than one node with equal scores, `kube-scheduler` selects one of them **at random** [source: k8s-docs-kube-scheduler-2026-08-23].

Not the lowest hostname. Not the least loaded. Not round-robin. Random. If you proposed one of the clever answers in Soundings question 2, you were in good company and you were wrong, and being wrong first is exactly why this will stick.

The randomness does real conceptual work, too. It tells you that the scheduler is not trying to be optimal in a way you can reason about or predict. Which means influencing placement is not a matter of understanding the algorithm well enough to out-think it. It's a matter of **saying something**: putting a constraint in the Pod spec, or a mark on the node, that the algorithm is obliged to honour. Everything in §3 through §6 is a way of saying something.

### The decision is irreversible

Chapter 3 told you the scheduler selects a node and records that choice, and that it does not start anything. Chapter 5 told you a Pod is scheduled once in its lifetime *[cross-bearing: see Ch 5 §4 — the Pod's lifecycle]*. Put those together and you have the reason this chapter exists.

Pods are created, assigned a unique ID, and scheduled to run on nodes where they remain until termination or deletion. A Pod is never "rescheduled" to a different node; instead, it is replaced by a new, near-identical Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23]. If a node dies, the Pods running on it are marked for deletion after a timeout, and higher-level controllers such as Deployments create the replacements [source: k8s-docs-pod-lifecycle-2026-08-23].

So there is no "move it later." A berth, once allotted, is not renegotiated. There is only "replace it, and hope the replacement lands somewhere better." That's not a design flaw. It's what makes the whole model simple enough to reason about. But it does mean that everything you want to be true about where a Pod runs has to be true *before* the Pod is created.

> ⚓ **Worth Securing:** If you want a Pod somewhere specific, you have to say so before it exists. Editing a running Pod's placement is not a thing you can do. Every mechanism in this chapter is read at scheduling time, and none of them is enforced continuously afterwards.

---

## 🔵 §2 — What Makes a Node Feasible

Chapter 5 taught you requests and limits, told you that requests are the input to the scheduler's filtering step, and sent you here for the consequence *[cross-bearing: see Ch 5 §8 — requests and limits]*. Here is the consequence, and it's stranger than the promise made it sound.

### The mechanism

The filtering step finds the set of nodes where it is feasible to schedule the Pod. The docs' own example is the **`PodFitsResources`** filter, which checks whether a candidate node has enough available resources to meet a Pod's specific resource **requests** [source: k8s-docs-kube-scheduler-2026-08-23].

Note the word. Requests. Not limits: the kubelet enforces limits on the running container, and it does that after placement, on a node that has already been chosen [source: k8s-docs-resource-management-2026-08-23]. And not observed usage either. As the next few paragraphs show, a request is spent the moment it is granted, whatever the container does with it afterwards.

<!-- AUTHOR-REVIEW: the fact-accuracy stage flagged the absolute negative "the scheduler never consults observed usage" (present in the previous draft here, at the §2 Fixed Point, in the Exam Alert, and in the P3 answer key) as unsourced. The cached corpus supports the positive claims — PodFitsResources checks requests, the kubelet reserves at least the request amount, the scheduler does not over-subscribe Allocatable — but states nothing about live utilisation. All four sites have been re-argued from the booking rather than from the negative. If the mechanism is wanted stated directly, kubernetes.io/docs/concepts/scheduling-eviction/resource-bin-packing/ or the scheduler-config plugin reference is the fetch. Record as gap G-7G. -->

> 🔭 **Closer Look:** `PodFitsResources` is named in the documentation as *an example* of a filter, not as the only one [source: k8s-docs-kube-scheduler-2026-08-23]. Resources are one feasibility test among several; §3 and §4 add more, and §6 covers the fact that the whole filter set is configurable. Don't walk away from this section thinking capacity is the only thing that can make a node infeasible.

### Now the part that surprises everyone

When you specify a resource request for a container, the kube-scheduler uses that information to decide which node to place the Pod on, and the kubelet **reserves at least the request amount** of that resource specifically for that container to use [source: k8s-docs-resource-management-2026-08-23].

Read that again with an accountant's eye. A request is a **booking**. Not an estimate, not a hint, not a starting point for measurement. Once a Pod is placed, its requests are taken off the node's available balance and stay off, whether the container ever touches that memory or not.

> **Before reading on:** a node has 16 GiB of memory available to Pods. Four Pods are running on it, and each one requested 4 GiB. Monitoring says the node is using 2 GiB in total. A fifth Pod arrives requesting 1 GiB. Does it schedule on this node? Decide before you keep reading.

It does not. The four Pods booked 16 GiB between them, and the kubelet reserves at least the request amount for each container whether or not the container ever touches it [source: k8s-docs-resource-management-2026-08-23]. Sixteen booked out of sixteen available means zero left, and a Pod asking for 1 GiB is filtered out. The 2 GiB figure describes what the containers are doing with what they booked; it does not hand any of it back.

This is the fact that converts *"the cluster has loads of free memory but my Pod won't schedule"* from a mystery into arithmetic. A node can be busy and empty at the same time, and only one of those two states is the scheduler's business.

> ★ **Fixed Point:**
>
> **Filtering fits a Pod's *requests* against a node's *available* capacity, and a request is booked whether or not it is ever used. Ten Pods that each requested 1 GiB and each use 50 MiB have filled a 10 GiB node completely, as far as scheduling is concerned.**

The requests / limits / quality-of-service picture is already drawn in `ch05-fig05-requests-limits-qos-classes`. Go back and look at it now that you know which of those numbers the scheduler reads. The QoS classes themselves are Chapter 5's material and matter for eviction rather than for placement *[cross-bearing: see Ch 5 §8 — QoS classes]*; the only thing you need here is which field is the scheduler's input.

### What "available" is measured against

A node's status reports both **Capacity** and **Allocatable** [source: k8s-docs-nodes-2026-08-23]. Allocatable is the one that matters here: *"'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods"*, and *"the scheduler treats 'Allocatable' as the available `capacity` for pods"* [source: k8s-docs-node-allocatable-2026-08-24]. The scheduler does not over-subscribe Allocatable [source: k8s-docs-node-allocatable-2026-08-24].

Practical translation: when you do the arithmetic yourself, do it against Allocatable, not against the machine's total RAM. What makes the two differ, and how it's configured, is Chapter 8's material *[cross-bearing: see Ch 8 — node administration]*.

### One clause about overhead

Chapter 2 mentioned that a RuntimeClass can carry a Pod overhead so the scheduler accounts for the runtime's resource cost, and said the reasoning would arrive later [source: k8s-docs-runtime-class-2026-08-23] *[cross-bearing: see Ch 2 §7 — RuntimeClass]*. This is where it arrives: a Pod running under a sandboxed runtime doesn't consume only what its containers asked for, and the overhead exists so the scheduler's arithmetic accounts for the runtime's own cost rather than pretending it's free.

<!-- AUTHOR-REVIEW: the cached RuntimeClass snapshot states only that the overhead exists "so the scheduler accounts for the runtime's resource cost." It does not state the mechanism (i.e. that overhead is added to the Pod's effective request). Phrasing above is held to what the snapshot supports. If the mechanism is wanted stated, kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/ needs fetching. Record as gap G-7F. -->

### And one clause about making room

There is one circumstance in which the scheduler does something other than wait. If a Pod cannot be scheduled, the scheduler tries to preempt — evict — lower priority Pods to make scheduling of the pending Pod possible [source: k8s-docs-pod-priority-preemption-2026-08-24]. Priority and preemption are real, they're configured with a `PriorityClass` [source: k8s-docs-pod-priority-preemption-2026-08-24], and they're out of scope here. Register that they exist so that nothing in this chapter reads as a lie later.

### The failure mode, which is the exam-critical half

If none of the nodes are suitable, **the Pod remains unscheduled until the scheduler is able to place it** [source: k8s-docs-kube-scheduler-2026-08-23]. Its phase is `Pending`, which covers, among other things, *"time a Pod spends waiting to be scheduled"* [source: k8s-docs-pod-lifecycle-2026-08-23].

That's it. Nothing errors. Nothing times out. Nothing retries with different parameters or gives up and files a complaint. The Pod waits, indefinitely, and the controller that created it has already done its part and moved on. A Pod can sit in `Pending` for a week and the cluster will consider this a perfectly ordinary state of affairs: a vessel riding at anchor outside the harbour, on nobody's list.

> ⚠ **Navigational Hazards:** `Pending` is a **state**, not an error. It is the honest report of a Pod that has been accepted by the cluster and has nowhere to run yet. No component is quietly retrying it with looser constraints, and no timer will eventually convert it into a failure. If you want to know *why* a Pod is Pending, you have to go and ask, which is Chapter 13's whole opening move *[cross-bearing: see Ch 13 — reading Pod failure signatures]*.

And notice what an unschedulable Pod is, structurally: a standing, machine-readable statement that the cluster is short of somewhere to put work. Something could be watching for exactly that. *[cross-bearing: see Ch 17 — reacting to unschedulable Pods]*

One related boundary, while you're here: nothing stops you from booking the entire cluster with requests you don't need. The mechanisms that stop *other people* doing that to you are `ResourceQuota` and `LimitRange`, and they belong to Chapter 8 *[cross-bearing: see Ch 8 — quotas and limit ranges]*.

---

## ☆ Taking Your Bearings #1 — How the Decision Is Made

Five questions on §1 and §2. Two of them reach back into earlier chapters.

**1.** Name the scheduler's three steps in order, and say which component actually starts the container.

- A) Score, filter, bind — and the scheduler starts the container.
- B) Filter, score, bind — and the kubelet on the chosen node starts the container.
- C) Filter, score — and the kubelet starts the container; binding is something the kubelet does.
- D) Filter, bind, score — and the container runtime starts the container on the scheduler's instruction.

**2.** Three nodes survive filtering and all three score identically. What does `kube-scheduler` do?

- A) Picks the node with the lowest name, for determinism.
- B) Picks the least-loaded node by current CPU usage.
- C) Picks one of them at random.
- D) Leaves the Pod `Pending` until the tie resolves itself.

**3.** [retrieval: ch5] A container requests 2 GiB of memory and sets a limit of 4 GiB. Which of those two numbers does the scheduler use when deciding whether a node can take this Pod, and what does the other number do?

**4.** 🔵 A node has 16 GiB allocatable memory and four Pods on it, each of which requested 4 GiB. Monitoring shows the node using 2 GiB in total. A new Pod requesting 1 GiB will not schedule there. Explain why, in one sentence.

**5.** [retrieval: ch6] A Deployment wants three replicas. Two are running. The third cannot be placed anywhere in the cluster. Describe the state of the third Pod, and describe what the ReplicaSet controller does about it.

---

**Answers with Explanations:**

**1 — B.**
Filtering produces the feasible set, scoring ranks it, and binding notifies the API server [source: k8s-docs-kube-scheduler-2026-08-23]; the kubelet is the agent on each node that makes sure the containers described in the PodSpecs are running [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** on both counts: the order is inverted (you cannot score nodes you haven't filtered), and the scheduler never starts anything. This is the single most common misconception about the scheduler and it's worth naming as such.
- **C is wrong** because it drops binding, or reassigns it. Binding is the scheduler's third act, not the kubelet's.
- **D is wrong** because binding is not a middle step and the scheduler does not instruct the runtime. It doesn't talk to nodes at all. It talks to the API server.

**2 — C.**
*"If there is more than one node with equal scores, kube-scheduler selects one of these at random"* [source: k8s-docs-kube-scheduler-2026-08-23].
- **A and B are wrong** in the instructive way: they're the answers a competent engineer would design. They are not the answer the system implements, and knowing that is what tells you the scheduler's tie-breaking is not something you can plan around.
- **D is wrong** because a tie is not a failure. A tie means *several* nodes are acceptable, which is the opposite of unschedulable.

**3 — The request.**
The kube-scheduler uses the resource *request* to decide which node to place the Pod on; the *limit* is enforced by the kubelet, which does not allow the running container to use more of the resource than the limit sets [source: k8s-docs-resource-management-2026-08-23]. The kubelet's enforcement happens after placement, on a node already chosen.

**4 — The requests are booked whether or not they're used, so the node is already fully allocated.**
Four Pods × 4 GiB requested = 16 GiB booked against 16 GiB allocatable. The kubelet reserves at least the request amount for each container [source: k8s-docs-resource-management-2026-08-23], and the scheduler does not over-subscribe Allocatable [source: k8s-docs-node-allocatable-2026-08-24]. Usage of 2 GiB describes what the containers are doing with what they booked; it does not return any of it. If you can say this sentence out loud without hesitating, you can diagnose most real `Pending` Pods.

**5 — The Pod is `Pending`, indefinitely; the controller does nothing further.**
The Pod remains unscheduled until the scheduler is able to place it [source: k8s-docs-kube-scheduler-2026-08-23], and its phase is `Pending`, which includes time spent waiting to be scheduled [source: k8s-docs-pod-lifecycle-2026-08-23]. From the controller's point of view, its work is complete — it created the Pod it was missing. Nothing about the Pod's inability to run reflects back on the loop that created it.
*Deliberately not covered here:* what you'd run to find out **why**. `kubectl describe`, the event stream, and the scheduler's own message are Chapter 13's material, and the fact that you know exactly what state to look for is what will make that chapter fast.

---

**Checkpoint: You've Now Mastered**

✓ The two-step operation, and what binding actually is
✓ The documented list of factors a scheduling decision weighs
✓ Why a tie is broken at random, and what that implies about influencing placement
✓ Why a node can be busy and empty at the same time
✓ Why `Pending` is a state and not an error

☐ How a Pod asks for a particular kind of node (next)
☐ How a node refuses a Pod (§4)

---

## 🔵 §3 — Asking for a Particular Berth

Everything so far has been the scheduler's own arithmetic. Now you start putting your thumb on it.

### The direction inverts

Chapter 4 taught label selectors as the universal join, and listed node scheduling constraints as one of the four things they're used for *[cross-bearing: see Ch 4 §5 — labels and selectors]*. Watch what changes here.

Every previous use of labels in this book has been **an object selecting a set of Pods** — a Service selecting its backends, a ReplicaSet selecting the Pods it owns. Here it is **a Pod selecting nodes**. Same mechanism, opposite direction. If you've internalised "selectors find Pods," this will read as backwards for a page or two until you say the inversion out loud.

Nodes have labels [source: k8s-docs-assign-pod-node-2026-08-23]. You can attach them manually, and Kubernetes also populates a standard set of labels on all nodes in a cluster [source: k8s-docs-assign-pod-node-2026-08-23]. The kubelet supplies `kubernetes.io/hostname`, which it populates with the hostname of the node, along with `kubernetes.io/os` and `kubernetes.io/arch` [source: k8s-docs-well-known-labels-2026-08-24]. `topology.kubernetes.io/zone` and `topology.kubernetes.io/region` are populated by the kubelet **or** the cloud-controller-manager [source: k8s-docs-well-known-labels-2026-08-24], which means they show up where the cluster has a cloud provider to ask, and may not be there at all on the single-machine cluster you're learning on. Note that now, because §5's examples lean on the zone label.

You can see them and add to them with the commands you already know from Chapter 4, just pointed at a different resource:

```
kubectl get nodes --show-labels
kubectl label nodes <your-node-name> disktype=ssd
```

[source: k8s-docs-assign-pods-nodes-task-2026-08-24]

One caution, more relevant than it looks: if you use labels for node isolation, choose label keys the kubelet cannot modify. The NodeRestriction admission plugin prevents the kubelet from setting labels with a `node-restriction.kubernetes.io/` prefix [source: k8s-docs-assign-pod-node-2026-08-23]. A node that can label itself into a privileged group is not an isolation boundary. The admission gate that enforces this is Chapter 8's *[cross-bearing: see Ch 8 — admission control]*.

### `nodeSelector`

`nodeSelector` is the simplest recommended form of node selection constraint. You add the `nodeSelector` field to your Pod specification and name the node labels you want the target node to have, and **Kubernetes only schedules the Pod onto nodes that have each of the labels you specify** [source: k8s-docs-assign-pod-node-2026-08-23].

Each. Not any. It is an AND of exact matches and it offers nothing else: no "one of these," no "anything except," no "greater than." That bluntness is a feature for the ninety percent of requirements that are genuinely blunt ("this Pod needs an SSD"). The other ten percent are why the next thing exists.

### Node affinity

Affinity expands the types of constraint you can define: the language is more expressive, you can indicate that a rule is soft or preferred so the scheduler still schedules the Pod even if it can't find a matching node, and you can constrain a Pod using labels on other Pods [source: k8s-docs-assign-pod-node-2026-08-23]. That third capability is §5. The first two are here.

**Node affinity functions like the `nodeSelector` field but is more expressive and allows you to specify soft rules** [source: k8s-docs-assign-pod-node-2026-08-23]. Concretely, it adds two things:

**A richer operator set.** `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt` and `Lt` [source: k8s-docs-assign-pod-node-2026-08-23]. Compare that to `nodeSelector`'s single implicit "equals."

**Two hardness levels**, expressed by two field names that everyone resents on first contact [source: k8s-docs-assign-pod-node-2026-08-23]:

- `requiredDuringSchedulingIgnoredDuringExecution` — the scheduler **can't** schedule the Pod unless the rule is met.
- `preferredDuringSchedulingIgnoredDuringExecution` — the scheduler **tries** to find a node that meets the rule, but if a matching node is not available, it still schedules the Pod.

For preferred rules you can attach a weight to each instance, and those weights feed the node's score alongside the other scoring functions; nodes with the highest total score are prioritised [source: k8s-docs-assign-pod-node-depth-2026-08-24]. You don't need the arithmetic for this exam. You do need to notice where preferred rules land: in the **scoring** step, not the filtering step. Hold that thought until §7.

> 🪢 **Mnemonic:** Read `requiredDuringSchedulingIgnoredDuringExecution` as two clauses joined at the seam: **required when scheduling, ignored once running.** The word is forty-six characters; the meaning is six. Every one of these field names decomposes the same way: first half is what happens at placement, second half is what happens afterwards.

If you do write affinity by hand, two combination rules are worth knowing because they're easy to get backwards: if you specify multiple terms in `nodeSelectorTerms`, the Pod can be scheduled if **one** of the terms is satisfied — terms are ORed; if you specify multiple expressions in a single `matchExpressions` field, the Pod can be scheduled **only if all** the expressions are satisfied — expressions are ANDed [source: k8s-docs-assign-pod-node-depth-2026-08-24].

### The second half of the field name

`IgnoredDuringExecution` means that **if the node's labels change after Kubernetes schedules the Pod, the Pod continues to run** [source: k8s-docs-assign-pod-node-2026-08-23].

You already knew this. You retrieved it in Soundings question 4 and Chapter 5 taught it as a general rule about the Pod's lifetime. What's new is that the rule has a name, and the name is sitting in plain sight inside a field you'll type. A Pod placed on a node labelled `disktype=ssd` does not get evicted when someone strips that label off. The rule was a scheduling-time question and scheduling time is over.

### The gradient

<!-- FIGURE: ch07-fig02-nodeselector-vs-affinity -->
```
                    EXPRESSIVENESS  ────────────────────────────────▶

                  nodeSelector          required node        preferred node
                                          affinity              affinity
               ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
    HARD       │ exact matches,   │  │ In, NotIn,       │  │                  │
    the rule   │ all of them      │  │ Exists,          │  │        —         │
    must be    │ (implicit AND)   │  │ DoesNotExist,    │  │                  │
    met        │                  │  │ Gt, Lt           │  │                  │
               │ no match →       │  │ no match →       │  │                  │
               │ no placement     │  │ no placement     │  │                  │
               └──────────────────┘  └──────────────────┘  └──────────────────┘
               ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
    SOFT       │                  │  │                  │  │ same operators   │
    the rule   │        —         │  │        —         │  │                  │
    is a wish  │                  │  │                  │  │ no match →       │
               │                  │  │                  │  │ placed anyway    │
               └──────────────────┘  └──────────────────┘  └──────────────────┘

    Hardness and expressiveness are independent. Only ONE of the six cells is soft.
```

That figure is worth thirty seconds. The common misreading is that node affinity is simply "more powerful `nodeSelector`," a single upgrade path. It isn't. **`nodeSelector` and `required` node affinity fail identically**: no matching node, no placement, Pod sits in `Pending`. What affinity adds is a second, independent axis. Choosing between the three cells is choosing how much you want to *say*, and separately, how badly you want it *obeyed*.

Reach for `nodeSelector` first. Affinity exists for the requirements `nodeSelector` genuinely cannot express, and a soft rule you didn't need is a rule someone will misread as a guarantee eighteen months from now.

> ★ **Fixed Point:**
>
> **`nodeSelector` is an AND of exact node-label matches — nothing more. Node affinity is the same idea with a richer operator set and an optional soft (`preferred`) mode. `IgnoredDuringExecution` means a label change after binding does not move the Pod.**

Chapter 2 also told you a RuntimeClass can carry scheduling constraints — a `nodeSelector` and tolerations — so that Pods land on nodes that support the handler [source: k8s-docs-runtime-class-2026-08-23]. The `nodeSelector` half of that promise is now discharged. The tolerations half is the next section.

---

## 🔵 §4 — When the Berth Refuses You

This is the densest section in the chapter. Take it at peak attention, and take the three-effect table slowly.

### The inversion

Everything in §3 was a property of a **Pod** that draws it toward certain nodes. This section is the other direction: the mark a berth flies to say *not you*.

> Node affinity is a property of Pods that attracts them to a set of nodes (either as a preference or a hard requirement). Taints are the opposite — they allow a node to repel a set of pods. [source: k8s-docs-taints-tolerations-2026-08-23]

**Tolerations are applied to Pods**, and they allow the scheduler to schedule Pods with matching taints [source: k8s-docs-taints-tolerations-2026-08-23]. One or more taints are applied to a node; this marks that the node should not accept any Pods that do not tolerate the taints [source: k8s-docs-taints-tolerations-2026-08-23].

So: the **taint** lives on the node and is a refusal. The **toleration** lives on the Pod and is an exemption from that refusal. Two objects, two directions, and getting them the wrong way round is the source of most confusion in this material.

Taints go on and come off with `kubectl taint`. The removal form is the same command with a trailing minus sign, which is easy to miss and easy to mistype:

```
kubectl taint nodes node1 key1=value1:NoSchedule
kubectl taint nodes node1 key1=value1:NoSchedule-
```

[source: k8s-docs-taints-tolerations-depth-2026-08-24]

### The qualification that catches everyone

> **Tolerations allow scheduling but don't guarantee scheduling**: the scheduler also evaluates other parameters as part of its function. [source: k8s-docs-taints-tolerations-2026-08-23]

A toleration removes a veto. That is the entire extent of its power. It does not make a request, it does not raise a node's score, it does not reserve anything, and it does not create capacity. Your GPU workload with a matching toleration is now *allowed* onto the GPU nodes, along with being allowed onto every other node in the cluster, which it was already. Nothing has pulled it toward the GPU nodes at all.

> ⚠ **Navigational Hazards:** A toleration is not a request. Taints and tolerations exclude; affinity and `nodeSelector` attract. They are **complementary, not alternative**. If you want a set of nodes dedicated to a workload *and* you want that workload to actually land there, you need both: a taint to keep everyone else off, and a label plus affinity (or `nodeSelector`) to pull your workload on. The documentation says exactly this — if you want to dedicate nodes to a group *and* ensure they only use the dedicated nodes, *"you should additionally add a label similar to the taint to the same set of nodes… and the admission controller should additionally add a node affinity to require that the pods can only schedule onto nodes labeled with `dedicated=groupName`"* [source: k8s-docs-taints-tolerations-depth-2026-08-24]. Using only one of the two is the most common real-world mistake in this material, and it produces a cluster that looks like it's misbehaving when it's doing precisely what you asked.

### The three effects

Learn these by **when they act**: whether the refusal is posted at the approach, or served on a vessel already tied up. That's what separates them, and it's what a question will turn on.

**`NoSchedule`** — no new Pods will be scheduled on the tainted node unless they have a matching toleration. **Pods currently running on the node are not evicted** [source: k8s-docs-taints-tolerations-2026-08-23].

**`PreferNoSchedule`** — the soft version of `NoSchedule`. The control plane will *try* to avoid placing a Pod that does not tolerate the taint on the node, but it is not guaranteed [source: k8s-docs-taints-tolerations-2026-08-23].

**`NoExecute`** — the only effect that touches Pods already on the node. Pods that do not tolerate the taint are **evicted immediately**. Pods that tolerate the taint without specifying `tolerationSeconds` remain bound forever. Pods that tolerate the taint *with* a specified `tolerationSeconds` remain bound for that long, after which the node lifecycle controller evicts them [source: k8s-docs-taints-tolerations-2026-08-23].

<!-- FIGURE: ch07-fig03-taints-tolerations-effects -->
```
        ┌────────────────────────────────────────────────┐
        │  NODE                                          │
        │  taint:  key=value:EFFECT   ───▶  repels       │  refusal originates HERE
        └────────────────────────────────────────────────┘
             ▲                ▲                  ●
             │                │                  └─ Pod C: already aboard, no toleration
             │                └───────────────────  Pod B: arriving, matching toleration
             └────────────────────────────────────  Pod A: arriving, no toleration
                        (tolerations belong to the POD)

   ┌──────────────────┬────────────────┬─────────────────┬─────────────────────┐
   │ EFFECT           │ Pod A          │ Pod B           │ Pod C               │
   │                  │ arriving,      │ arriving,       │ already running,    │
   │                  │ no toleration  │ tolerating      │ no toleration       │
   ├──────────────────┼────────────────┼─────────────────┼─────────────────────┤
   │ NoSchedule       │ not placed     │ may be placed   │ unaffected          │
   │ PreferNoSchedule │ avoided where  │ may be placed   │ unaffected          │
   │                  │ possible       │                 │                     │
   │ NoExecute        │ not placed     │ may be placed   │ EVICTED             │
   └──────────────────┴────────────────┴─────────────────┴─────────────────────┘

   "may be placed" — never "is placed." The other filters and scores still run.
```

Pod C is the whole point of the figure. Two of the three rows leave it completely alone. Only one row reaches out and touches something that was already moored.

> 🪝 **Snag:** `PreferNoSchedule` is a *preference*, and preferences lose. Pods that don't tolerate the taint will land on a `PreferNoSchedule` node when nothing better is available, and that is correct behaviour, not a bug. If you need "never," you need `NoSchedule`.

### Matching

Here the metaphors run out. Four rules, no narrative, stated flat.

> **Dead Reckoning:** A toleration matches a taint when the keys are the same and the effects are the same, and one of two operator conditions holds. If the operator is `Exists`, no value should be specified. If the operator is `Equal`, the values must be equal. Two wildcards modify this. If the key is empty, the operator must be `Exists`, which matches all keys and all values — the effect must still match. An empty effect matches all effects with the given key. [source: k8s-docs-taints-tolerations-2026-08-23]

| Toleration | Matches | Notes |
|---|---|---|
| key + effect + `operator: Equal` + value | Taints with the same key, same effect, same value | The exact-match case |
| key + effect + `operator: Exists` | Taints with the same key and same effect, **any value** | Do not specify a value with `Exists` |
| empty key + `operator: Exists` + effect | **All** taints with that effect, any key, any value | Empty key *requires* `Exists` |
| key + `operator: Exists` + **empty effect** | All effects for that key | Effect wildcard |

And when a node carries more than one taint, the procedure is: *"start with all of a node's taints, then ignore the ones for which the pod has a matching toleration; the remaining un-ignored taints have the indicated effects on the pod"* [source: k8s-docs-taints-tolerations-depth-2026-08-24]. Tolerating three of four taints does not get you onto the node. The fourth still applies.

### The taints Kubernetes adds for you

You are not the only party putting taints on nodes.

> The control plane, using the node controller, automatically creates taints with a `NoSchedule` effect for node conditions. **The scheduler checks taints, not node conditions, when it makes scheduling decisions.** This ensures that node conditions don't directly affect scheduling. [source: k8s-docs-taints-tolerations-depth-2026-08-24]

That's an elegant piece of design. Node health doesn't get a special channel into the scheduler; it gets translated into the *same* mechanism you'd use by hand.

That paragraph covers one of two families. Separately, the node controller also automatically taints a node when certain conditions are true, including the case where the API server cannot communicate with a node's kubelet at all [source: k8s-docs-taints-tolerations-depth-2026-08-24], and those taints are the `NoExecute` pair in the table below. So the built-in family carries both effects, not just `NoSchedule`, and the table shows them together [source: k8s-docs-daemonset-2026-08-24]:

| Taint key | Effect |
|---|---|
| `node.kubernetes.io/not-ready` | `NoExecute` |
| `node.kubernetes.io/unreachable` | `NoExecute` |
| `node.kubernetes.io/disk-pressure` | `NoSchedule` |
| `node.kubernetes.io/memory-pressure` | `NoSchedule` |
| `node.kubernetes.io/pid-pressure` | `NoSchedule` |
| `node.kubernetes.io/unschedulable` | `NoSchedule` |
| `node.kubernetes.io/network-unavailable` | `NoSchedule` |

There is also `node.cloudprovider.kubernetes.io/uninitialized`, added when the kubelet starts with an external cloud provider [source: k8s-docs-taints-tolerations-depth-2026-08-24].

Two of these deserve a note each.

Kubernetes automatically adds a toleration for `node.kubernetes.io/not-ready` and `node.kubernetes.io/unreachable` with `tolerationSeconds=300`, unless you or a controller set those tolerations explicitly [source: k8s-docs-taints-tolerations-depth-2026-08-24]. That five-minute grace period is why a briefly-unreachable node doesn't instantly shed everything running on it.

And `node.kubernetes.io/unschedulable` — remember that one. Marking a node unschedulable is a deliberate administrative act: it prevents the scheduler from placing new Pods onto that node but does not affect the Pods already there, and it is the preparatory step before a reboot or other maintenance [source: k8s-docs-nodes-2026-08-23]. That act is Chapter 8's opening move *[cross-bearing: see Ch 8 — taking a node out of service]*.

### The mechanism you'd already met

Chapter 6 told you that DaemonSets keep running on nodes where nothing else will, and said you'd already met the mechanism in disguise *[cross-bearing: see Ch 6 §7 — DaemonSets]*. Here it is: **the DaemonSet controller automatically adds tolerations for the built-in condition taints** to the Pods it creates — six of the seven unconditionally, with the seventh, `network-unavailable`, added only for DaemonSet Pods that request host networking [source: k8s-docs-daemonset-2026-08-24]. Because the controller sets the `node.kubernetes.io/unschedulable:NoSchedule` toleration automatically, Kubernetes can run DaemonSet Pods on nodes that are marked unschedulable [source: k8s-docs-daemonset-2026-08-24]. And the `NoExecute` tolerations for `not-ready` and `unreachable` carry no `tolerationSeconds`, so DaemonSet Pods running on such nodes are not evicted [source: k8s-docs-daemonset-2026-08-24].

Which is exactly why your log-shipping agent is still reporting from a node that's under memory pressure and refusing all other work. It isn't privileged. It just tolerates almost everything.

> **Logbook Entry:**
>
> A platform team buys eight GPU nodes. They're expensive, they're scarce, and the machine-learning group has waited four months for them. The obvious first move is to keep everyone else off, so the team taints all eight: `kubectl taint nodes gpu-01 dedicated=ml:NoSchedule`, and so on down the list.
>
> That works immediately and visibly. Batch jobs stop landing on the GPU nodes. The team writes it up as done.
>
> The ML group adds the matching toleration to their training Pods and starts a run. The Pods schedule. The run is slow. Someone eventually checks, and every training Pod is sitting on ordinary CPU nodes — the toleration let them onto the GPU nodes and nothing ever pushed them there. In a cluster of two hundred nodes, eight of which are GPUs, the odds of landing on a GPU node by chance are exactly what you'd expect them to be.
>
> The fix takes one line. Label the same eight nodes `dedicated=ml`, and give the training Pods a `nodeSelector` (or a required node affinity) for that label. Now the taint keeps everyone else off, and the label pulls the right work on.
>
> Keeping a berth clear and being steered into it are two different acts, and only one of them had been performed. The version of this story where the team notices in ten minutes and the version where they notice in three weeks differ only in whether somebody knew that a toleration doesn't attract.

> ★ **Fixed Point:**
>
> **A taint is the node's refusal; a toleration is the Pod's exemption from that refusal. Tolerations permit — they never attract. Of the three effects, only `NoExecute` affects Pods that are already running.**

Dedicated nodes also show up later as an isolation control rather than a scheduling one *[cross-bearing: see Ch 12 — workload isolation]*. And a `Pending` Pod whose cause is a taint rather than a shortage of capacity looks identical from the outside until you go and read the events *[cross-bearing: see Ch 13 — diagnosing Pending]*.

---

## ☆ Taking Your Bearings #2 — The Two Directions

Five questions on §3 and §4. One reaches back to Chapter 4.

**1.** [retrieval: ch4] Every previous use of labels in this book has been one object selecting a set of Pods. `nodeSelector` uses the same label-selector mechanism. What is selecting what here, and in which direction?

**2.** ⚠ **This one is intentionally hard, and the intuitive answer is wrong.** Struggle is the point — missing it is expected and is exactly what makes the correct answer stick.

Your organisation has a per-seat licence for a CAD package, and only six machines in the cluster are covered by it. You taint those six `license=cad:NoSchedule` and add a matching toleration to the CAD rendering workload. A colleague reports that the rendering Pods are running on ordinary, unlicensed nodes. Is anything broken?

**3.** A node gains a new taint while Pods are already running on it. For each of the three effects, say whether the running Pods are affected. Then, for `NoExecute` only, say what happens to a Pod that *does* tolerate the taint — with and without a `tolerationSeconds` value.

**4.** 🟡 A Pod is running on a node. Someone removes the node label that the Pod's `requiredDuringSchedulingIgnoredDuringExecution` node-affinity rule was matching on. What happens to the Pod?

- A) It is evicted immediately, because the rule is `required`.
- B) It is evicted after a grace period, then rescheduled elsewhere.
- C) Nothing. It keeps running.
- D) It is marked `Pending` and the kubelet stops its containers.

**5.** Give one placement requirement that `nodeSelector` cannot express but node affinity can, and name the feature of affinity that makes the difference.

---

**Answers with Explanations:**

**1 — The Pod's spec selects nodes, by the nodes' labels. The direction is inverted relative to every prior use.**
Nodes have labels, and the recommended approaches to constraining placement all use label selectors [source: k8s-docs-assign-pod-node-2026-08-23]. Same machinery, opposite subject and object: previously a controller or Service selected Pods; here the Pod selects nodes. If this felt backwards while reading §3, that reaction was correct and worth keeping.

**2 — No. Nothing is broken, and the cluster is doing exactly what you told it.**
*"Tolerations allow scheduling but don't guarantee scheduling"* [source: k8s-docs-taints-tolerations-2026-08-23]. The taint keeps *other* Pods off the licensed nodes. The toleration makes your Pods *eligible* for the licensed nodes, and they were already eligible for every untainted node in the cluster, so they land wherever the ordinary scoring puts them.

**The fix requires a second, opposite mechanism.** Label the licensed nodes (say `license=cad`) and give the workload a `nodeSelector` or a required node affinity for that label. The documentation prescribes exactly this pairing for dedicated nodes: add a label similar to the taint to the same set of nodes, and add a node affinity requiring that the Pods can only schedule onto nodes carrying it [source: k8s-docs-taints-tolerations-depth-2026-08-24].

**Taints exclude. Affinity attracts. A dedicated-node setup needs both.** That sentence is the single most transferable operational fact in this chapter.

**3 — `NoSchedule`: unaffected. `PreferNoSchedule`: unaffected. `NoExecute`: non-tolerating Pods are evicted immediately.**
With `NoSchedule`, Pods currently running on the node are not evicted [source: k8s-docs-taints-tolerations-2026-08-23]. `PreferNoSchedule` is the soft version of the same thing and likewise concerns placement only [source: k8s-docs-taints-tolerations-2026-08-23]. `NoExecute` affects Pods already running: non-tolerating Pods are evicted immediately [source: k8s-docs-taints-tolerations-2026-08-23].
The classic wrong answer is that `NoSchedule` evicts. It doesn't, and the word *Schedule* in the name is telling you so.

**For a Pod that *does* tolerate a `NoExecute` taint:** without a `tolerationSeconds` value it remains bound forever; with one, it remains bound for that long, after which the node lifecycle controller evicts it [source: k8s-docs-taints-tolerations-2026-08-23]. Kubernetes sets that value for you on exactly two taints — `not-ready` and `unreachable`, at `tolerationSeconds=300` — unless you or a controller set those tolerations explicitly [source: k8s-docs-taints-tolerations-depth-2026-08-24]. Five minutes of grace, then the node sheds its work.

**4 — C.**
`IgnoredDuringExecution` means that if the node labels change after Kubernetes schedules the Pod, the Pod continues to run [source: k8s-docs-assign-pod-node-2026-08-23]. The `required` half applies at scheduling time; the `Ignored` half applies afterwards, and both halves are in the field name.
- **A is wrong** because it reads only the first half of the name. `required` describes what the scheduler must honour, not what the kubelet must continuously enforce.
- **B is wrong** on two counts: nothing evicts, and even if something did, a Pod is not rescheduled to a different node — it would be *replaced* [source: k8s-docs-pod-lifecycle-2026-08-23].
- **D is wrong** because `Pending` describes a Pod that hasn't been placed. This one has been placed and is running.

**5 — Any soft requirement, or any rule needing an operator other than equality.**
`nodeSelector` is an AND of exact label matches: Kubernetes only schedules the Pod onto nodes that have each of the labels you specify [source: k8s-docs-assign-pod-node-2026-08-23]. Node affinity is more expressive and allows soft rules [source: k8s-docs-assign-pod-node-2026-08-23], and it supports `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt` and `Lt` [source: k8s-docs-assign-pod-node-2026-08-23]. So: "prefer SSD nodes but run anywhere" needs `preferred`; "any zone except zone-c" needs `NotIn`; "a node that has a GPU label at all, whatever its value" needs `Exists`.

---

**Checkpoint: You've Now Mastered**

✓ Which direction each mechanism asserts from — Pod, or node
✓ The three taint effects and which one touches running Pods
✓ What `tolerationSeconds` does, and the one place Kubernetes sets it for you
✓ Why a toleration alone never gets your Pod where you wanted it
✓ How to decode any `…DuringScheduling…DuringExecution` field name on sight

☐ Placing Pods relative to *each other* (next)
☐ Getting out of the scheduler's way entirely (§6)

*Good place for a break. §5 changes altitude.*

---

## 🟡 §5 — Placing Pods Relative to Each Other

Everything so far has constrained a Pod against a property of a **node**. This section constrains a Pod against the properties of **other Pods**, and to do that, it needs an abstraction you haven't met.

### Start with the failure

Two replicas of a service, created so that one machine failing doesn't take the service down. Both land on the same node. Two hulls, one mooring, and one bad night takes both. The service now has exactly the availability it had with one replica, plus double the resource bill.

Nothing in §2 or §3 prevents this. Here is why. The two Pods have identical requests, identical labels, identical affinity — they came out of one Deployment, so of course they do *[cross-bearing: see Ch 6 §1 — Deployments and ReplicaSets]*. Nothing in their specs distinguishes one node from another, and nothing tells the scheduler that these two Pods are related, so it is entirely free to pick the same node twice. It is not being careless. You never told it these two were connected.

That's the gap. Redundancy is a property of a **set**, and none of the mechanisms so far can express a property of a set. Every rule you've written has been about one Pod and one node, evaluated in isolation.

### Inter-Pod affinity and anti-affinity

Inter-pod affinity and anti-affinity let you constrain Pods against **labels on other Pods** — "only schedule on nodes in the same zone as a Pod with this label," or "spread these Pods across nodes" [source: k8s-docs-assign-pod-node-2026-08-23].

- **Pod affinity attracts.** Schedule this Pod where a Pod carrying that label already is. Useful for co-locating things that talk to each other constantly.
- **Pod anti-affinity repels.** Do not schedule this Pod where a Pod carrying that label already is. This is the availability tool.

Both come in the same `required` and `preferred` flavours as node affinity. This is genuinely the same machinery pointed at a different set of labels, not a second system to learn. One exception, since §3 just handed you six operators: `Gt` and `Lt` are node-affinity-only and are not available for `podAffinity` [source: k8s-docs-assign-pod-node-depth-2026-08-24]. `podAntiAffinity` in `requiredDuringSchedulingIgnoredDuringExecution` mode means only a single Pod can be scheduled into a single topology domain; in `preferredDuringSchedulingIgnoredDuringExecution` mode you lose the ability to enforce the constraint [source: k8s-docs-topology-spread-constraints-2026-08-24].

Notice the phrase that keeps appearing: *topology domain*.

### The domain is a variable

This is the hard idea in the section, and it's the one that makes §5 🟡 rather than 🔵.

The domain is not always "the node." You express the topology domain using a **`topologyKey`, which is the key for the node label that the system uses to denote the domain** [source: k8s-docs-assign-pod-node-depth-2026-08-24]. Nodes that have a label with that key and identical values are considered to be in the same topology [source: k8s-docs-topology-spread-constraints-2026-08-24].

So the same rule, over the same cluster, means different things depending on which label you name.

<!-- FIGURE: ch07-fig04-pod-affinity-anti-affinity-topology -->
```
   SAME CLUSTER. SAME RULE: "no two Pods labelled app=web in one domain."
   THE ONLY DIFFERENCE IS THE topologyKey.

   topologyKey: kubernetes.io/hostname       topologyKey: topology.kubernetes.io/zone
   a domain = one node                       a domain = one zone

   ┌── zone-a ──────────────────┐            ┌── zone-a ──────────────────┐
   │  n1 [web]   n2 [web]       │            │  n1 [web]   n2      n3     │
   │  n3 [web]                  │            │                            │
   └────────────────────────────┘            └────────────────────────────┘
   ┌── zone-b ──────────────────┐            ┌── zone-b ──────────────────┐
   │  n4 [web]   n5 [web]       │            │  n4 [web]   n5      n6     │
   │  n6 [web]                  │            │                            │
   └────────────────────────────┘            └────────────────────────────┘

   6 domains  →  up to 6 Pods placed         2 domains  →  at most 2 Pods placed

   One label key changed. The rule's meaning changed with it.
```

Same cluster, same six nodes, same two zones, same rule text. Change one label key and the rule goes from "spread across machines" to "spread across failure zones," which is dramatically stricter, and, if you only have two zones, dramatically more likely to leave Pods `Pending`.

> ★ **Fixed Point:**
>
> **Inter-Pod rules are evaluated against the labels of Pods that are *already placed*, within a topology domain defined by a node label (`topologyKey`). The domain is the part people forget — it is a variable, not a synonym for "node."**

> 🔭 **Closer Look:** The documentation states the cost of these rules without explaining it: *"Inter-pod affinity and anti-affinity require substantial amounts of processing which can slow down scheduling in large clusters significantly. We do not recommend using them in clusters larger than several hundred nodes"* [source: k8s-docs-assign-pod-node-depth-2026-08-24]. The explanation below is mine rather than theirs, and it is the obvious one. To decide whether a single node is feasible, the scheduler now has to know what's already running everywhere else in the domain: the answer for node-a depends on the contents of node-b. That's a fundamentally different cost shape from "does this node have 4 GiB free." This is a sharp tool. It is not free.

### Topology spread constraints

Anti-affinity can say "not in the same domain." What people usually *want* is "distributed fairly evenly, and tell me how much unevenness you'll tolerate." That's a different requirement, and it has a purpose-built mechanism.

> You can use *topology spread constraints* to control how Pods are spread across your cluster among failure-domains such as regions, zones, nodes, and other user-defined topology domains. [source: k8s-docs-topology-spread-constraints-2026-08-24]

> This can help to achieve high availability as well as efficient resource utilization. [source: k8s-docs-topology-spread-constraints-2026-08-24]

Like everything else in this section, they rely on node labels to identify the topology domain each node is in [source: k8s-docs-topology-spread-constraints-2026-08-24]. Four fields carry the meaning, and for this exam you want to recognise them rather than compose them:

| Field | What it says |
|---|---|
| `topologyKey` | The key of node labels. Nodes that have a label with this key and identical values are considered to be in the same topology. [source: k8s-docs-topology-spread-constraints-2026-08-24] |
| `labelSelector` | Finds the matching Pods. Pods matching this selector are counted to determine the number of Pods in their corresponding topology domain. [source: k8s-docs-topology-spread-constraints-2026-08-24] |
| `maxSkew` | Describes the degree to which Pods may be unevenly distributed. Must be specified and must be greater than zero. [source: k8s-docs-topology-spread-constraints-2026-08-24] |
| `whenUnsatisfiable` | `DoNotSchedule` (the default) tells the scheduler not to schedule the Pod; `ScheduleAnyway` tells the scheduler to still schedule it while prioritizing nodes that minimize the skew. [source: k8s-docs-topology-spread-constraints-2026-08-24] |

Read `whenUnsatisfiable` again and you'll see something you have already met three times. `DoNotSchedule` is a hard rule; `ScheduleAnyway` is a soft one. Required and preferred, once more, under new names. That's the fourth appearance of the same pair in this chapter, and §7 is about to tell you why.

> 🪝 **Snag:** "Spread my replicas evenly across nodes" and "never put two of these together" are different requirements. Anti-affinity states the second and only approximates the first. If you find yourself writing anti-affinity rules and then reasoning about how many replicas you're allowed to have, you wanted spread constraints.

One honest limitation, because it's the kind of thing that bites in production and it's cheap to know now: *"There's no guarantee that the constraints remain satisfied when Pods are removed. For example, scaling down a Deployment may result in imbalanced Pods distribution"* [source: k8s-docs-topology-spread-constraints-2026-08-24]. These are scheduling-time constraints. Like everything else in this chapter, they describe a decision, not a standing invariant.

Distribution matters downstream too: a Service's backends being on distinct nodes is what makes the Service resilient rather than merely load-balanced *[cross-bearing: see Ch 9 — Services and endpoints]*.

---

## 🟡 §6 — Overruling the Scheduler, and Replacing It

Two escape hatches at two different altitudes, held together by one frame. Everything so far has been about *influencing* a decision the scheduler makes. This section is about not letting it make the decision at all.

### `nodeName` — the Pod-level hatch

`nodeName` is a more direct form of node selection than affinity or `nodeSelector`. It's a field in the Pod spec, and **if it is not empty, the scheduler ignores the Pod** and the kubelet on the named node tries to place the Pod on that node [source: k8s-docs-assign-pod-node-2026-08-23]. Using `nodeName` **overrules** using `nodeSelector` or affinity and anti-affinity rules [source: k8s-docs-assign-pod-node-depth-2026-08-24].

Overrules — not "takes precedence within the same evaluation." The scheduler doesn't run. Nothing you wrote in §2 through §5 is consulted, because the component that would have consulted it was skipped.

Which produces the one failure mode in this chapter that isn't `Pending` [source: k8s-docs-assign-pod-node-depth-2026-08-24]:

> - If the named node does not exist, the Pod will not run, and in some cases may be automatically deleted.
> - If the named node does not have the resources to accommodate the Pod, the Pod will fail and its reason will indicate why, for example OutOfmemory or OutOfcpu.
> - Node names in cloud environments are not always predictable or stable.

Every other placement failure in this chapter leaves a Pod waiting patiently for conditions to improve. This one fails outright, because the feasibility check that would have caught the problem in advance never happened. You took responsibility for it, and nobody is going to tell you when you get it wrong.

So the framing matters: **`nodeName` is not the most forceful way of asking.** It is the absence of asking — mooring where you like, and telling no one. The API does let you specify a node for a Pod when you create it, *"but this is unusual and is only done in special cases"* [source: k8s-docs-kube-scheduler-2026-08-23], which, coming from reference documentation, is a stronger discouragement than it looks.

### The case that makes binding concrete

Here's the thing that reframes the whole section, and it comes from a resource you already know.

The DaemonSet controller does not use `nodeName` to place its Pods. It creates a Pod for each eligible node and adds the `spec.affinity.nodeAffinity` field of the Pod to match the target host. After the Pod is created, **the default scheduler typically takes over and then binds the Pod to the target host by setting the `.spec.nodeName` field** [source: k8s-docs-daemonset-2026-08-24].

Read that last clause again. Binding *is* writing `.spec.nodeName`. That's the whole physical content of the operation the scheduler performs in step three. It tells the API server which node, the API server records it in that field, and the kubelet on that node notices its own name.

So `nodeName` is not a special user-facing shortcut at all. It is **the field that binding writes to**, and setting it by hand means filling in the scheduler's answer before it was asked the question.

> ⚓ **Worth Securing:** `nodeName` is the scheduler's output, not a separate API. When you set it yourself you aren't overriding a decision — you're pre-writing it, and skipping every check that would have validated it. That's why the failure is immediate rather than patient.

### `schedulerName` — the cluster-level hatch

`kube-scheduler` is designed so that, if you want and need to, **you can write your own scheduling component and use that instead** [source: k8s-docs-kube-scheduler-2026-08-23]. Pods can name which scheduler should handle them; a DaemonSet, for example, exposes `.spec.template.spec.schedulerName` for exactly this purpose [source: k8s-docs-daemonset-2026-08-24].

You do not need to know how to build a scheduler. You need to know that the seat is pluggable: the default scheduler is a default, not a fixture. That fact gets collected with several of its siblings much later *[cross-bearing: see Ch 17 — the cluster's extension points]*.

### The vocabulary you'll meet in older material

There are two documented ways to configure the filtering and scoring behaviour of the scheduler [source: k8s-docs-kube-scheduler-2026-08-23]:

- **Scheduling Policies** — **Predicates** for filtering, and **Priorities** for scoring.
- **Scheduling Profiles** — **plugins** that implement different scheduling stages, including `QueueSort`, `Filter`, `Score`, `Bind`, `Reserve` and `Permit`. `kube-scheduler` can run different profiles.

Treat this as a **vocabulary mapping onto §1's spine**, not as two configuration systems you might choose between. Predicates are filtering under an older name. Priorities are scoring under an older name. The profile plugin stages are the same pipeline with more seats exposed, and two of those seat names, `Filter` and `Score`, are just the steps you already know.

| Older name | What it is |
|---|---|
| Predicate | A filter — decides whether a node is feasible |
| Priority | A score — ranks the nodes that survived filtering |

If you read an older blog post that says "the PodFitsResources predicate," you now know that's a filter, and you can carry on reading. That's what this material is worth on this exam.

<!-- AUTHOR-REVIEW: currency question CLOSED — do not re-open. A prior draft flagged the Scheduling Policies model as possibly removed upstream and routed the question to the fact-accuracy stage. The research stage had already investigated: it re-fetched the live kube-scheduler page and found it character-identical to the cached snapshot on this passage, and recorded that there is nothing to reconcile. The prose above deliberately teaches Predicates/Priorities as *older names for the two steps* rather than as a currently-selectable configuration option, so it is true under every reading. Do NOT add a "Policies have been removed" claim — that assertion appears nowhere in the cached corpus and would itself be an untagged factual claim. -->

> ★ **Fixed Point:**
>
> **`nodeName` bypasses the scheduler entirely. It overrules `nodeSelector` and every affinity rule, and because it skips the feasibility check, a Pod that doesn't fit *fails* rather than waiting in `Pending`. Predicates are filters; Priorities are scores.**

Where profile configuration actually lives — which is to say, in the control plane's own component configuration — is a question about running a cluster rather than using one *[cross-bearing: see Ch 8 — cluster administration]*.

---

## ☆ Taking Your Bearings #3 — Relative Placement, and Opting Out

Five questions on §5 and §6, with one that needs three sections at once.

**1.** Your three replicas all land on one node. Nothing in their spec is wrong. Explain why the scheduler was entitled to do that, and name the kind of rule that would have prevented it.

**2.** 🟡 An inter-Pod anti-affinity rule uses a `topologyKey` of `topology.kubernetes.io/zone` rather than `kubernetes.io/hostname`. What changes about where the Pods may land?

**3.** A Pod spec sets both a `nodeSelector` and a `nodeName`. Which wins, and what happens if the named node cannot fit the Pod?

- A) The `nodeSelector` wins; `nodeName` is only a hint.
- B) `nodeName` wins and the scheduler is bypassed; if the node can't fit the Pod, the Pod stays `Pending`.
- C) `nodeName` wins and the scheduler is bypassed; if the node can't fit the Pod, the Pod fails.
- D) The API rejects the Pod, because the two fields conflict.

**4.** Map the older Predicates-and-Priorities vocabulary onto the two steps you learned in §1.

**5.** 🟡 A DaemonSet's Pod is running on a node that is under memory pressure and is refusing all other work. Explain how it got there, and name the component that placed it.

---

**Answers with Explanations:**

**1 — Because nothing in the spec expressed a relationship between the three Pods; inter-Pod anti-affinity (or a topology spread constraint) is the kind of rule that would have.**
Three replicas from one Deployment are identical: same requests, same labels, same node constraints. Nothing in their specs distinguishes one node from another, and nothing expresses a relationship between the three, so the scheduler placing all three in one place is a legal outcome of a decision made three times independently. Inter-pod anti-affinity constrains Pods against labels on other Pods [source: k8s-docs-assign-pod-node-2026-08-23], which is the only kind of rule in this chapter that can say anything about a *set*.

**2 — The exclusion now applies per zone rather than per node, which is strictly stronger.**
Nodes with the same value for the `topologyKey` label are considered to be in the same topology [source: k8s-docs-topology-spread-constraints-2026-08-24]. With `kubernetes.io/hostname`, each node is its own domain, so two Pods may not share a node but two Pods in different nodes of the same zone are fine. With `topology.kubernetes.io/zone`, each zone is one domain, so two Pods may not share a *zone* at all. In a two-zone cluster, a required anti-affinity rule on the zone key caps you at two placeable Pods regardless of how many nodes you own; the rest sit `Pending`. The domain is the variable, and changing it changes the answer.

**3 — C.**
Using `nodeName` overrules using `nodeSelector` or affinity and anti-affinity rules [source: k8s-docs-assign-pod-node-depth-2026-08-24], and if the `nodeName` field is not empty the scheduler ignores the Pod [source: k8s-docs-assign-pod-node-2026-08-23]. If the named node does not have the resources to accommodate the Pod, the Pod **fails**, with a reason such as `OutOfmemory` or `OutOfcpu` [source: k8s-docs-assign-pod-node-depth-2026-08-24].
- **A is wrong**: `nodeName` is not a hint, it's a bypass.
- **B is the good distractor**, because `Pending` is the correct answer for every *other* failure in this chapter. It's wrong here precisely because nothing ran the feasibility check — there is no scheduler waiting for conditions to improve.
- **D is wrong**: the API accepts the Pod. Nothing about the combination is invalid; `nodeSelector` simply never gets read.

**4 — Predicates are filtering; Priorities are scoring.**
Scheduling Policies configure the scheduler with Predicates for filtering and Priorities for scoring [source: k8s-docs-kube-scheduler-2026-08-23]. Same two steps, older names. The Profiles model exposes the same stages as plugin extension points, two of which are literally called `Filter` and `Score` [source: k8s-docs-kube-scheduler-2026-08-23].

**5 — The DaemonSet controller set node affinity for that node and added tolerations for the built-in condition taints; the ordinary default scheduler then typically placed it.**
The DaemonSet controller creates a Pod for each eligible node and adds `spec.affinity.nodeAffinity` matching the target host; after the Pod is created, the default scheduler typically takes over and binds the Pod to the target host by setting `.spec.nodeName` [source: k8s-docs-daemonset-2026-08-24]. Separately, the controller automatically adds tolerations for the built-in node-condition taints, including `node.kubernetes.io/memory-pressure:NoSchedule` [source: k8s-docs-daemonset-2026-08-24].

**The point worth taking from this:** nothing special happened. This is the ordinary scheduler doing its ordinary job, on a Pod that was constructed to be feasible on exactly one node and to tolerate what that node is complaining about. There's no privileged path and no bypass. And the binding step you learned as a vocabulary word in §1 turns out to be a field write you can point at.

---

**Checkpoint: You've Now Mastered**

✓ Why identical replicas are entitled to land in identical places
✓ That the topology domain is a variable, and what changing it costs
✓ What `nodeName` actually is, and the one failure that isn't `Pending`
✓ Predicates → filter, Priorities → score

☐ The one thing you actually have to remember (next, and it's short)

---

## ☀️ §7 — Everything Is a Filter or a Score

You've now learned six vocabularies for influencing placement. They have six different syntaxes, they live in different places in the spec, half of them are on Pods and half on nodes, and one of them has a field name forty-six characters long. They look like six separate systems.

They are not.

> ☀️ **Zenith**
>
> **Every mechanism in this chapter plugs into one of exactly two slots in §1's pipeline. It either removes nodes from consideration — a filter — or it changes the ranking of the nodes that survived — a score. Six vocabularies. Two slots. That's the chapter.**

<!-- FIGURE: ch07-zenith-berth-assignment -->
```
  FILTERS — remove nodes                     SCORES — rank what remains
  ┌────────────────────────────────┐         ┌────────────────────────────────┐
  │ requests vs allocatable        │         │ preferred node affinity        │
  │ nodeSelector                   │         │ PreferNoSchedule               │
  │ required node affinity         │         │ preferred inter-Pod rules      │
  │ untolerated NoSchedule         │         │ ScheduleAnyway spread          │
  │ untolerated NoExecute          │         │ other scoring plugins          │
  │ required inter-Pod rules       │         │                                │
  │ DoNotSchedule spread           │         │                                │
  └───────────────┬────────────────┘         └────────────────┬───────────────┘
                  │                                           │
                  ▼                                           ▼
          ┌──────────────┐       ┌──────────────┐      ┌──────────────┐
          │  1. FILTER   │ ────▶ │  2. SCORE    │ ───▶ │  3. BIND     │
          └──────────────┘       └──────────────┘      └──────┬───────┘
                                                              │
                                                              ▼
                                                        ┌───────────┐
  spec.nodeName ────────────────────────────────────────▶│  a node   │
  neither a filter nor a score — it deletes the choice   └───────────┘
```

<!-- AUTHOR-REVIEW: the fact-accuracy stage flagged that no cached snapshot assigns any individual mechanism to a named scheduler stage. §7's synthesis — hard rules filter, soft rules score — is the chapter's organising frame and follows from the documented behaviours (an untolerated NoSchedule taint means the node will not accept the Pod; PreferNoSchedule means the control plane will only try to avoid it). The two-column figure above and the answer keys for Practice Q10 and Q13 state the assignment mechanism-by-mechanism, which the corpus supports by inference rather than by a source sentence. Both answer keys have been re-phrased to derive the assignment from the documented behaviour rather than to assert a stage registration. The fetch that would source it directly is kubernetes.io/docs/reference/scheduling/config/, which enumerates each plugin against its extension points (TaintToleration appears at both Filter and Score; InterPodAffinity at PreFilter, Filter and Score). This is the single highest-value snapshot this chapter is still missing — recommend fetching before the book-level pass. -->

Same three stages you saw on the first page of this chapter. Nothing new has been added to the pipeline. Everything you learned in §2 through §5 contributed to step one or step two, and the `required` / `preferred` distinction that kept recurring under four different names — required vs preferred node affinity, `NoSchedule` vs `PreferNoSchedule`, required vs preferred inter-Pod rules, `DoNotSchedule` vs `ScheduleAnyway` — was never four distinctions. It was always the same one: *is this a filter, or is this a score?*

Hard rules filter. Soft rules score. That is the whole taxonomy.

And there is exactly one thing in this chapter that fits neither slot, which is why it's drawn outside the pipeline. `nodeName` does not narrow the feasible set and it does not adjust a ranking. It removes the decision. That is precisely why it's dangerous, and precisely why the documentation calls it unusual [source: k8s-docs-kube-scheduler-2026-08-23].

> ⚓ **Worth Securing:** The diagnostic question for any placement problem you'll ever meet: *is this a filter that excluded every node, or a score that ranked the wrong one first?* The two have completely different symptoms. A filter problem leaves a Pod `Pending` forever; a score problem puts the Pod somewhere you didn't want, immediately and silently. Knowing which one you're looking at is most of the diagnosis.

One last thing to notice, and then we'll stop. The scheduler watches for newly created Pods that have no node assigned [source: k8s-docs-kube-scheduler-2026-08-23], compares what exists against what has been placed, and acts on the difference. That shape should be familiar by now. It's the same shape as every controller in Chapter 6. The scheduler is not an exception to the cluster's architecture; it's another instance of it, wearing a specialised hat. Keep that in your peripheral vision; the book comes back to it properly later.

---

## Exam Alert! 🚨

**High-Priority Topics**

1. **Filter → score → bind**, in that order. Binding is a notification to the API server.
2. **The scheduler does not start the container.** The kubelet on the chosen node does.
3. **Equal scores break at random.**
4. **An unschedulable Pod stays `Pending`.** Not an error. Nothing times out.
5. **Filtering fits *requests*** against Allocatable — not limits, and a request stays booked whether or not it is used.
6. **A Pod is scheduled once and is never rescheduled.** It gets replaced, not moved.
7. **The three taint effects and their timing** — only `NoExecute` touches running Pods.
8. **A toleration permits; it does not attract.**
9. **`nodeName` bypasses the scheduler**, overrules `nodeSelector` and affinity, and fails rather than waiting.

**Common Traps**

You met the first of these in Chapter 3, where it was defused explicitly and you were told it would come back *[cross-bearing: see Ch 3 §2 — the control plane]*. Here's the piece Chapter 3 held back.

| Trap | The correction |
|---|---|
| "The scheduler places the Pod on the node." | It notifies the API server. The kubelet on the chosen node is what starts containers. |
| "The scheduler picks the single best node, deterministically." | Ties are broken at random [source: k8s-docs-kube-scheduler-2026-08-23]. |
| "An unschedulable Pod errors out." | It remains unscheduled until the scheduler is able to place it [source: k8s-docs-kube-scheduler-2026-08-23]. |
| "A failed Pod is rescheduled to a healthy node." | A Pod is never rescheduled to a different node; it is replaced by a new Pod with a different UID [source: k8s-docs-pod-lifecycle-2026-08-23]. |
| "A toleration schedules the Pod onto the tainted node." | Tolerations allow scheduling but don't guarantee it — the scheduler still evaluates every other parameter [source: k8s-docs-taints-tolerations-2026-08-23]. **The most durable error in this material.** |
| "`NoSchedule` evicts the Pods already running." | It doesn't. Pods currently running are not evicted [source: k8s-docs-taints-tolerations-2026-08-23]. Only `NoExecute` does. |
| "Node affinity moves a Pod when the node's labels change." | `IgnoredDuringExecution` — the Pod continues to run [source: k8s-docs-assign-pod-node-2026-08-23]. |
| "`PreferNoSchedule` means never." | It's a preference; the control plane will try to avoid the node but it is not guaranteed [source: k8s-docs-taints-tolerations-2026-08-23]. |
| "`nodeSelector` and affinity are two syntaxes for the same power." | Affinity adds soft rules and five operators `nodeSelector` cannot express [source: k8s-docs-assign-pod-node-2026-08-23]. |
| "A Pod with `nodeName` set that doesn't fit will wait." | It fails, with a reason such as `OutOfmemory` [source: k8s-docs-assign-pod-node-depth-2026-08-24]. The one failure here that isn't `Pending`. |

---

## Practice Questions

Eighteen questions. Four reach back into earlier chapters, and four require two sections of this chapter at once. Answers and explanations follow the full set.

**1.** Which statement correctly describes what `kube-scheduler` does with an unbound Pod?

A) Filter, score, bind — and the scheduler then instructs the kubelet on the chosen node directly.
B) Filter, score, bind — and the scheduler notifies the API server of its choice.
C) Score, filter, bind — the nodes are ranked first, then the unsuitable ones are dropped.
D) Filter, bind, score — the Pod is bound, then ranked against the alternatives.

**2.** After filtering, four nodes remain and all four receive the same score. What happens?

A) The scheduler re-runs scoring with additional plugins until a winner emerges.
B) The scheduler selects one of the four at random.
C) The scheduler selects the node with the earliest creation timestamp.
D) The Pod is marked unschedulable because the result is ambiguous.

**3.** A node reports 32 GiB of RAM, of which 30 GiB is allocatable. Three Pods run on it, having requested 8 GiB each; between them they are currently using 3 GiB. A new Pod requests 12 GiB of memory. Assuming memory is the only constraint, will the new Pod be filtered onto this node?

A) Yes — 30 GiB minus 3 GiB used leaves 27 GiB available.
B) Yes — the scheduler over-subscribes memory by design.
C) No — 24 GiB is already booked against 30 GiB allocatable, leaving 6 GiB, which is less than 12 GiB.
D) No — the three Pods' *limits* sum to more than the node's allocatable memory, which blocks new placements.

**4.** A Pod has been sitting in `Pending` for six hours. Which statement is accurate?

A) The scheduler has failed and will emit an error after a configurable timeout.
B) The Pod is retried with progressively relaxed constraints until it fits.
C) The Pod is in a normal state; it remains unscheduled until the scheduler is able to place it.
D) The controller that created the Pod will delete it and create a replacement.

**5.** [retrieval: ch5] Your Pod was placed on a modestly-specced node an hour ago. A much better node has since joined the cluster and is sitting nearly idle. What happens to the running Pod?

A) The scheduler re-evaluates placement periodically and migrates it.
B) Nothing. It stays where it is for the rest of its life.
C) The kubelet on the new node claims it.
D) It is evicted and rescheduled at the next scoring cycle.

**6.** [retrieval: ch3] Which pair correctly assigns responsibility?

A) The scheduler records the placement decision with the API server; the kubelet on that node starts the containers.
B) The scheduler starts the containers directly; the kubelet reports their status back to the control plane.
C) The controller manager records the placement decision; the scheduler then starts the containers on that node.
D) The scheduler selects the node and notifies that node's kubelet directly; the kubelet starts the containers.

**7.** A Pod's `nodeSelector` matches exactly one node in the cluster. That node does not have enough allocatable memory for the Pod's request. What happens?

A) The Pod schedules onto the next-best node, since `nodeSelector` is advisory rather than binding.
B) The Pod fails immediately with `OutOfmemory`, because its placement was fully determined.
C) The Pod stays `Pending` — both the label filter and the resource filter must pass, and one of them doesn't.
D) The scheduler evicts a Pod from the matched node to make room, since a `nodeSelector` was specified.

**8.** A Pod is running on a node it reached via `requiredDuringSchedulingIgnoredDuringExecution` node affinity on the label `disktype=ssd`. An operator removes that label from the node. What happens to the Pod?

A) It is evicted, because the rule was `required` and is enforced continuously.
B) It continues to run, because the rule was a scheduling-time question only.
C) It is evicted once `tolerationSeconds` elapses, as with a `NoExecute` taint.
D) It moves to a different node that still carries the label.

**9.** A platform team taints eight GPU nodes with `dedicated=gpu:NoSchedule` and adds a matching toleration to the ML team's training Pods. The training Pods are landing on ordinary CPU nodes. Which single change makes them land on the GPU nodes?

A) Add a second toleration for the same taint, so that the match is unambiguous to the scheduler.
B) Change the taint's effect to `NoExecute`, which is the stronger form and will pull the Pods across.
C) Label the eight GPU nodes and give the training Pods a `nodeSelector` or a required node affinity for that label.
D) Remove the taint, since the taint is what is currently keeping the training Pods off the GPU nodes.

**10.** Which of the scheduler's two steps does an *untolerated* `NoSchedule` taint participate in, and which does `PreferNoSchedule` participate in?

A) Both participate in filtering.
B) `NoSchedule` filters; `PreferNoSchedule` scores.
C) `NoSchedule` scores; `PreferNoSchedule` filters.
D) Neither participates in either — taints are evaluated after binding.

**11.** A node that is already running Pods gains a new taint. Which statement about the running Pods is correct?

A) `NoSchedule` and `NoExecute` both evict non-tolerating Pods; `PreferNoSchedule` does not.
B) All three effects evict non-tolerating Pods, differing only in speed.
C) Only `NoExecute` evicts non-tolerating Pods; `NoSchedule` and `PreferNoSchedule` affect new placements only.
D) None of the three affects running Pods; taints are a placement-time mechanism only.

**12.** [retrieval: ch4] Chapter 4 introduced set-based label selectors with operators such as `in`, `notin` and `exists`. Which statement about node affinity's operators is correct?

A) Node affinity supports only equality, exactly like `nodeSelector`.
B) Node affinity supports `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt` and `Lt`.
C) Node affinity supports the same implicit equality as `nodeSelector`, plus `Gt` and `Lt` for numeric comparison.
D) Node affinity has no operators; its expressiveness comes solely from the soft/hard distinction.

**13.** A node carries a `NoSchedule` taint. A new Pod has no toleration for it, but does carry a required inter-Pod affinity rule saying it must be co-located with a Pod that happens to be running on that node. What happens?

A) The Pod schedules there, because pod affinity is evaluated after taints and therefore overrides them.
B) The Pod does not schedule there — the untolerated taint removes the node during filtering, and pod affinity cannot restore a node that has been filtered out.
C) The Pod schedules there, because a required pod-affinity rule is a filter and a `NoSchedule` taint only affects scoring.
D) The Pod schedules on a neighbouring node in the same topology domain, which satisfies the co-location rule.

**14.** A team's inter-Pod anti-affinity rule uses `topologyKey: kubernetes.io/hostname`. They change it to `topology.kubernetes.io/zone` in a cluster with two zones and twelve nodes. What is the effect on a Deployment with six replicas carrying the matching label?

A) No change — the rule already spread the Pods across nodes.
B) The rule becomes weaker; more Pods can share a zone.
C) The rule becomes stricter; with a required rule and two domains, at most two replicas can be placed and the rest stay `Pending`.
D) The rule becomes stricter, and the scheduler places the extra replicas on whichever nodes minimise the skew rather than leaving them `Pending`.

**15.** [retrieval: ch6] A DaemonSet achieves perfect one-per-node distribution without any anti-affinity rule or topology spread constraint. Why doesn't it need one?

A) The DaemonSet controller silently injects anti-affinity into every Pod it creates.
B) Distribution is the resource's definition — the controller creates one Pod per eligible node, so there is no set-level constraint for the scheduler to enforce.
C) DaemonSet Pods bypass the scheduler entirely via `nodeName`.
D) The scheduler applies a built-in default spread constraint to all DaemonSet Pods.

**16.** A Pod spec sets `nodeSelector: {disktype: ssd}`, a required node affinity for zone `zone-a`, and `nodeName: worker-07`. `worker-07` has neither an SSD label nor a `zone-a` label, and lacks the memory for the Pod. What happens?

A) The API server rejects the Pod for contradictory placement fields.
B) The scheduler resolves the conflict in favour of the most specific constraint and places the Pod in `zone-a`.
C) The scheduler ignores the Pod entirely; the kubelet on `worker-07` tries to place it and the Pod fails, with a reason such as `OutOfmemory`.
D) The Pod stays `Pending` until an SSD node in `zone-a` named `worker-07` appears.

**17.** You read an older article describing "the PodFitsResources predicate" and "the LeastRequestedPriority priority." Onto which parts of the modern two-step operation do those map?

A) Predicates map to binding; priorities map to filtering.
B) Predicates map to filtering; priorities map to scoring.
C) Both map to scoring; filtering had no configurable component.
D) Neither maps onto the modern operation; they describe a different algorithm.

**18.** A Pod carries a toleration with `key: dedicated`, `operator: Exists`, and no `effect` field. Which of a node's taints does that single toleration cover?

A) Only `dedicated` taints carrying the `NoSchedule` effect, since that is the default effect.
B) Every taint on the node whose key is `dedicated`, whatever its value and whatever its effect.
C) Every taint on the node regardless of key, because `Exists` with no value is the universal wildcard.
D) None — a toleration that omits `effect` is incomplete and is rejected when the Pod is created.

---

**Answers with Explanations:**

**1 — B.** Filtering finds the feasible set, scoring ranks it, and the scheduler then notifies the API server in a process called binding [source: k8s-docs-kube-scheduler-2026-08-23]. **A** gets the sequence right and the actor wrong: the scheduler talks to the API server, not to nodes, and the kubelet acts on a decision it *observed* rather than one it was told. **C** inverts the two steps — scoring runs on the nodes that survived filtering, so it cannot precede it. **D** puts binding before the decision has been made, which is incoherent: binding *is* the decision being recorded.

**2 — B.** *"If there is more than one node with equal scores, kube-scheduler selects one of these at random"* [source: k8s-docs-kube-scheduler-2026-08-23]. **A** invents a re-scoring loop that doesn't exist; nothing escalates a tie. **C** is the tidy deterministic answer a reasonable engineer would design, and it's wrong, which is what makes it a good distractor. **D** confuses a tie (several nodes are acceptable) with an empty feasible set (none are).

**3 — C.** The kubelet reserves at least the request amount of a resource for the container [source: k8s-docs-resource-management-2026-08-23], and the scheduler does not over-subscribe Allocatable [source: k8s-docs-node-allocatable-2026-08-24] — where Allocatable, not total RAM, is what the scheduler treats as available capacity for Pods [source: k8s-docs-node-allocatable-2026-08-24]. Three Pods × 8 GiB = 24 GiB booked; 30 − 24 = 6 GiB left; 12 > 6. **A** is the trap: it does the arithmetic against *usage*, and it also uses the wrong baseline. The reservation stands whether or not the container touches the memory [source: k8s-docs-resource-management-2026-08-23], so used-versus-booked is not the subtraction the filter performs. **B** contradicts the source directly — the scheduler does not over-subscribe Allocatable. **D** puts the limit in the scheduler's hands; limits are enforced by the kubelet on the running container, after placement [source: k8s-docs-resource-management-2026-08-23], and never enter the filter.

**4 — C.** If none of the nodes are suitable, the Pod remains unscheduled until the scheduler is able to place it [source: k8s-docs-kube-scheduler-2026-08-23], and `Pending` explicitly covers time spent waiting to be scheduled [source: k8s-docs-pod-lifecycle-2026-08-23]. **A** invents a timeout; nothing in the documented behaviour converts waiting into failure. **B** invents constraint relaxation — nothing rewrites your spec on your behalf. **D** describes a controller behaviour that isn't triggered by a Pod being unplaceable; the Pod exists, so the controller's count is already satisfied.

**5 — B.** Pods are scheduled once in their lifetime to a specific node, and a Pod is never "rescheduled" to a different node [source: k8s-docs-pod-lifecycle-2026-08-23]. This is the same rule you learned in Chapter 5 with a node-*failure* motivation; here it applies to a strictly better opportunity, and the answer is identical. Kubernetes does not optimise placement continuously. **A** and **D** both describe a rebalancing loop the platform does not have — nothing revisits a placement after binding. **C** has the wrong actor and the wrong direction: a kubelet never claims Pods. It acts on Pods the API server has already recorded as bound to its own node.

**6 — A.** The scheduler selects a node and notifies the API server [source: k8s-docs-kube-scheduler-2026-08-23]; the kubelet is an agent on each node that makes sure containers described in the PodSpecs are running [source: k8s-docs-cluster-architecture-2026-08-23]. **B** puts container-starting in the scheduler's hands, which is the most common misconception about this component and the reason `ch07-fig01` draws two separate arrows. **C** compounds that error with a second one: the controller manager runs controllers, not placement bookkeeping. **D** concedes that the kubelet starts containers and still gets the topology wrong — the scheduler does not talk to nodes at all. Its arrow lands on the API server, and the kubelet reads from there.

**7 — C.** Both are filters. `nodeSelector` restricts the Pod to nodes carrying each specified label [source: k8s-docs-assign-pod-node-2026-08-23]; `PodFitsResources` checks whether a candidate node has enough available resources for the Pod's requests [source: k8s-docs-kube-scheduler-2026-08-23]. The single label-matching node fails the resource filter, the feasible list is empty, and the Pod isn't yet schedulable [source: k8s-docs-kube-scheduler-2026-08-23]. **A** treats `nodeSelector` as soft — it isn't; Kubernetes only schedules the Pod onto nodes carrying *each* label. **B** is the `nodeName` failure mode borrowed into the wrong question: `nodeName` skips the feasibility check, but `nodeSelector` doesn't, so this Pod waits. **D** invents preemption-on-demand triggered by a selector; preemption is a priority mechanism, not a selector one.

**8 — B.** `IgnoredDuringExecution` means that if the node labels change after Kubernetes schedules the Pod, the Pod continues to run [source: k8s-docs-assign-pod-node-2026-08-23]. **A** reads only the first half of the field name; `required` governs the scheduler, not a continuous enforcement loop. **C** confuses affinity with tolerations — `tolerationSeconds` belongs to `NoExecute` taints and has no meaning for node affinity. **D** contradicts the once-only rule: a Pod is never rescheduled to a different node [source: k8s-docs-pod-lifecycle-2026-08-23].

**9 — C.** *"Tolerations allow scheduling but don't guarantee scheduling"* [source: k8s-docs-taints-tolerations-2026-08-23], and the documented dedicated-node pattern requires *both* a taint and a matching label plus node affinity if the Pods must only use the dedicated nodes [source: k8s-docs-taints-tolerations-depth-2026-08-24]. **A** treats the problem as a matching failure, but the toleration is already matching correctly; a duplicate changes nothing, because a toleration's only power is to remove a veto. **B** confuses strength of refusal with attraction: `NoExecute` would additionally evict every non-tolerating Pod already on those nodes [source: k8s-docs-taints-tolerations-2026-08-23], and the training Pods would still land wherever ordinary scoring puts them. **D** deletes the half of the setup that was working — the exclusion — and still supplies no pull, so the GPU nodes would fill with everyone else's work and the training Pods would be no likelier to be there.

**10 — B.** An untolerated `NoSchedule` taint means no new Pods will be scheduled on the node [source: k8s-docs-taints-tolerations-2026-08-23] — the node is taken out of consideration entirely, which is what filtering does. `PreferNoSchedule` means the control plane will *try* to avoid the node but it is not guaranteed [source: k8s-docs-taints-tolerations-2026-08-23] — the node stays in the running with a worse standing, which is what scoring does. **A** makes the soft effect hard, which would mean a `PreferNoSchedule` node could never take a non-tolerating Pod; the source says otherwise. **C** inverts both, and would make `NoSchedule` merely a discouragement. **D** is the answer of someone who thinks a toleration raises a node's score: taints are weighed before binding, not after, because binding is the recording of a decision already made.

**11 — C.** `NoSchedule` does not evict Pods currently running on the node; `PreferNoSchedule` is its soft form; `NoExecute` evicts non-tolerating Pods immediately [source: k8s-docs-taints-tolerations-2026-08-23]. **A** lets `NoSchedule` evict, which is the classic error, and the word *Schedule* in its name is the clue against it. **B** flattens all three into a single behaviour differing only in timing, which erases the one distinction the effects exist to draw. **D** overcorrects: `NoExecute` genuinely does reach Pods already running, and that's precisely what separates it from the other two.

**12 — B.** Node affinity supports `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt` and `Lt` [source: k8s-docs-assign-pod-node-2026-08-23], a richer vocabulary than `nodeSelector`'s implicit equality. **A** describes `nodeSelector`, not affinity, and misses both of affinity's additions. **C** is the half-remembered version: `Gt` and `Lt` are indeed the unusual pair (they're the ones unavailable to `podAffinity` [source: k8s-docs-assign-pod-node-depth-2026-08-24]), but affinity adds four more besides — the set-membership and existence operators are the ones you'll reach for daily. **D** drops the operator set entirely; expressiveness and hardness are two *independent* additions, and this option keeps only one of them.

**13 — B.** An untolerated `NoSchedule` taint marks the node as not accepting Pods that do not tolerate it [source: k8s-docs-taints-tolerations-2026-08-23], so the node is out of consideration before any ranking begins. Pod affinity is also a feasibility question — it can only ever *narrow* the surviving set, never restore a node that has already been excluded. **A** invents an evaluation ordering in which a later rule can readmit a node an earlier one rejected; nothing works that way, and filters compose by intersection, not by precedence. **C** gets the direction of both mechanisms wrong at once: it correctly files pod affinity as a filter but misfiles `NoSchedule` as a mere ranking penalty, when an untolerated `NoSchedule` node will not accept the Pod at all. **D** sounds plausible and isn't: a *required* co-location rule constrains the Pod to the topology domain containing the target Pod, and with a hostname-scoped domain that means the target's node specifically, not its neighbourhood.

**14 — C.** Nodes with identical values for the `topologyKey` label are in the same topology domain [source: k8s-docs-topology-spread-constraints-2026-08-24], and required-mode pod anti-affinity means only a single Pod can be scheduled into a single topology domain [source: k8s-docs-topology-spread-constraints-2026-08-24]. Twelve nodes gave twelve domains; two zones give two. Four of the six replicas have nowhere legal to go. **A** misses that the domain itself changed — the rule text is identical, which is exactly the trap. **B** has the direction backwards: fewer, larger domains is stricter, not looser. **D** borrows the behaviour of a *topology spread constraint* set to `ScheduleAnyway`, which does tell the scheduler to place the Pod anyway while prioritising nodes that minimise the skew [source: k8s-docs-topology-spread-constraints-2026-08-24]. A required anti-affinity rule has no such soft mode — the `preferred` form exists, but choosing it means you lose the ability to enforce the constraint [source: k8s-docs-topology-spread-constraints-2026-08-24], which is a different thing from placing to minimise skew.

**15 — B.** The DaemonSet controller creates a Pod for each eligible node and sets that Pod's node affinity to match the target host [source: k8s-docs-daemonset-2026-08-24]. Each Pod is constructed for one specific node, so there is no set-level relationship left for a scheduling constraint to enforce. **A** describes a mechanism the controller doesn't use — it uses node *affinity* per Pod, not anti-affinity across the set. **C** is wrong: the default scheduler typically takes over and binds the Pod [source: k8s-docs-daemonset-2026-08-24], so the ordinary pipeline runs. **D** invents a built-in default that isn't documented, and would have to apply to every DaemonSet in every cluster.
*This is a discrimination question as much as a retrieval one: "the Pods end up spread out" and "a spreading constraint was enforced" are not the same claim.*

**16 — C.** If the `nodeName` field is not empty, the scheduler ignores the Pod and the kubelet on the named node tries to place it [source: k8s-docs-assign-pod-node-2026-08-23]; `nodeName` overrules `nodeSelector` and affinity and anti-affinity rules [source: k8s-docs-assign-pod-node-depth-2026-08-24]; and if the named node lacks the resources, the Pod fails with a reason such as `OutOfmemory` [source: k8s-docs-assign-pod-node-depth-2026-08-24]. **A** invents API validation that doesn't happen — the fields are not checked against one another. **B** invents conflict resolution, but there is no conflict to resolve, because the component that would have read the other two fields never ran. **D** is the trap, because `Pending` is the right answer everywhere else in this chapter. Here nothing performed the feasibility check, so there is nothing waiting for conditions to improve.

**17 — B.** Scheduling Policies configure the scheduler with Predicates for filtering and Priorities for scoring [source: k8s-docs-kube-scheduler-2026-08-23]. The names changed; the two steps didn't. **A** inverts the mapping, which would put a *fits-resources* test in the ranking stage. **C** is wrong on the specific point that filtering had no configurable component: Predicates were exactly that component. **D** denies a correspondence the source states directly in the same sentence that names both terms.

**18 — B.** A toleration matches a taint when the keys are the same and the effects are the same, with the operator condition satisfied — and two wildcards modify that. An **empty effect matches all effects with the given key** [source: k8s-docs-taints-tolerations-2026-08-23]. So this toleration covers `dedicated` taints at `NoSchedule`, `PreferNoSchedule` and `NoExecute` alike, and `Exists` with no value means the taint's value is irrelevant too. **A** reads the missing `effect` as a default rather than as a wildcard; there is no "default effect" in the matching rules, only a wildcard. **C** confuses the two wildcards. The all-keys wildcard requires an **empty key**, and in that case the operator must be `Exists` [source: k8s-docs-taints-tolerations-2026-08-23]; here the key is `dedicated`, so taints with other keys are untouched — and untouched matters, because you start with all of a node's taints, ignore the ones with a matching toleration, and the remainder still have their effects on the Pod [source: k8s-docs-taints-tolerations-depth-2026-08-24]. **D** invents a validation rule; the empty effect is a documented wildcard, not an omission the API rejects.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **The two-step operation** | Filter, then score. Filtering produces the feasible set; scoring ranks it. |
| **Scheduling factors** | Resource requirements, hardware / software / policy constraints, affinity and anti-affinity, data locality, inter-workload interference, deadlines [source: k8s-docs-kube-scheduler-2026-08-23] [source: k8s-docs-cluster-architecture-2026-08-23]. |
| **Binding** | A notification to the API server [source: k8s-docs-kube-scheduler-2026-08-23] — concretely, writing `.spec.nodeName` [source: k8s-docs-daemonset-2026-08-24]. Not an act of starting anything. |
| **Who starts the container** | The kubelet on the chosen node. Never the scheduler. |
| **Tie-break** | Equal scores are broken **at random**. Not deterministically, not by load. |
| **Feasibility** | Requests fitted against Allocatable. A request stays booked whether or not it is used — and limits never enter the filter. |
| **`Pending`** | A state, not an error. Nothing times out, nothing retries with looser rules, nothing gives up. |
| **Scheduled once** | A Pod is never rescheduled to a different node. It is replaced, with a new UID. |
| **Node labels** | Same selector mechanism as Chapter 4, pointed the other way: the Pod selects nodes. |
| **`nodeSelector`** | An AND of exact label matches. Blunt, readable, hard. |
| **Node affinity** | Same idea, richer operators (`In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt`, `Lt`), plus a soft mode. |
| **`IgnoredDuringExecution`** | A node's labels changing after binding does not move the Pod. |
| **Taints** | Live on the **node**. A refusal. Three effects. |
| **Tolerations** | Live on the **Pod**. An exemption from the refusal. They permit; they never attract. |
| **Effect timing** | Only `NoExecute` touches Pods that are already running. |
| **`tolerationSeconds`** | Only meaningful with `NoExecute`. Kubernetes sets it to 300 for `not-ready` and `unreachable` unless you override it. |
| **Dedicated nodes** | Taint to exclude, label + affinity to attract. Both. Always. |
| **Inter-Pod rules** | Constrain a Pod against the labels of Pods already placed, within a topology domain. |
| **`topologyKey`** | The node label whose values define the domain boundaries. It's a variable, not "the node." |
| **Topology spread** | The purpose-built mechanism for even distribution. `DoNotSchedule` filters; `ScheduleAnyway` scores. |
| **`nodeName`** | Bypasses the scheduler. Overrules everything. Fails instead of waiting. |
| **Predicates / Priorities** | Older names for filtering and scoring. |
| **The whole chapter** | Every mechanism is a filter or a score. `nodeName` is neither — it deletes the choice. |

---

## The Voyage Ahead

You can now say where a Pod should go, where it must not go, and what it should be near. What you cannot yet say is anything about the machine itself.

You have no way to take a node out of service before you reboot it. No way to stop one team booking the entire cluster's memory with requests they'll never use. No idea which versions of which components are allowed to disagree with each other, or what happens when they do. And no vocabulary for the three gates every request passes through on its way into the API server — which is the same API server this whole chapter has been quietly writing to.

There's a clue already in your hands. In §4 you met a built-in taint called `node.kubernetes.io/unschedulable`, sitting in the family table with a `NoSchedule` effect, and it wasn't put there by a failing disk or an exhausted process table. Marking a node unschedulable is a deliberate administrative act: it stops new Pods arriving without disturbing the ones already there, and it is the preparatory step before a reboot or other maintenance [source: k8s-docs-nodes-2026-08-23]. The command that does it, the command that clears the node out afterwards, and everything else in the `kubectl` surface that a cluster administrator actually uses — that's Chapter 8, and it's the last chapter of Part II.

Chapter 8 is where the rules you've been learning turn into consequences.

---

🏆 **Safe Harbor**

You have finished the hardest five points in Part II. Scheduling is the material that most study guides present as a catalogue of six unrelated features, and you have it as one pipeline with two slots.

The next time you see a Pod stuck in `Pending`, you will not wonder whether something is broken. You will ask which filter emptied the list, and that is the question a practitioner asks.

🗺️ → 🌊 → 🌅 · **Part II · Chapter 7.** One chapter left before Part III.

> *"You cannot move a berth once it is assigned. You can only be careful about what you said before it was."*

<!-- AUTHOR-REVIEW: outline Open Question #1 — chapter-02 line 807 carries *[cross-bearing: see Ch 7 §3 — node selection, tolerations, and accounting for overhead]*. Those three topics land in §3, §4 and §2 respectively, so the "§3" is partially wrong. This draft honors the chapter-05 §2 pin exactly and does not attempt to edit shipped Chapter 2 text. Recommended fix remains the one-token deletion of "§3" from that pointer, matching the two other unnumbered Chapter 7 pointers. Not actionable from inside this chapter. -->

<!-- AUTHOR-REVIEW: outline Open Question #11 — this draft back-bears to Ch 6 §1 (Deployments/ReplicaSets) and Ch 6 §7 (DaemonSets) using the ch-06 outline's planned section numbering, since chapter-06's shipped file is incomplete and its final numbering is not verifiable. Re-verify both pointers after the ch-06 harvest is re-run. Note also that Book-KCNA currently ships chapters 01–05 only, so §4's DaemonSet callback and §5's Deployment back-bearing both point at unshipped text — a sequencing decision for the author, not a defect in this chapter. -->
