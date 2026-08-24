I have the full context: the book-outline stages (B1 domain analysis, B2 lineup, B3 retrieval architecture, B4 question budget, B5 arc outline), the cached sources, the four published cross-bearings pointing into Chapter 7, and the Chapter 6 outline as the format precedent. Here is `outline.md` for Chapter 7.

```markdown
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

# Chapter 7 Outline — Assigning the Berth

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 7: Assigning the Berth` | required | top |
| `## *"Filter, score, bind — and then a coin flip"*` | required | line 2 |
| Metadata line (weight / complexity / novelty) | required | after subtitle |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings #1–#3` | **required, min 2** | after §2, §4, §6 |
| `★ Fixed Point` ×5 | **required, min 1** | §1, §2, §3, §4, §6 |
| `**Dead Reckoning:**` ×1 min | **required** | §4 — the taint/toleration matching rules stated flat, with no berth register at all |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §2 (Pending is not an error), §4 (a toleration is not a request) |
| `☀️ Zenith` | expected | §7 |
| `## Exam Alert` | **required** | after §7 |
| `## Practice Questions` | **required** | 17 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19 |
| `🏆 Safe Harbor` | expected | chapter close |

**Heading form.** Chapters 5 and 6 ship `## ⚪ §1 — Title`; Chapters 2 and 3 ship `## §1 — ⚪ Title`. Follow the later form (`## ⚪ §1 —`), which is what Chapters 5 and 6 established and what the reader has seen most recently. Flagged for a reconciliation sweep in § Open questions #12; do not fix Chapters 2 and 3 from inside this chapter.

**Zenith:** exactly one, per Part 18.10. `ch07-zenith-berth-assignment` in §7. This chapter carries four concept diagrams plus the Zenith — one fewer than Chapters 4, 5 and 6, which is correct for a 5-point chapter. `ch07-fig03` (the three taint effects) will be the tempting one to inflate, because a three-row table is easy to make look important. Resist. Its job is reference; §7's job is recognition.

**Attention Budget guidance for drafting.** Seven sections, four distinct costs:

| Section | Cost | Why |
|---|---|---|
| §1 | low | Three steps, one boundary the reader already met in Chapter 3, and one fact (the coin flip) that is memorable on first contact |
| §2 | medium | One genuinely counter-intuitive idea — the scheduler books capacity rather than measuring it — resting on Chapter 5's requests |
| §3 | medium | Two mechanisms on a gradient, plus a modifier (`IgnoredDuringExecution`) whose name is longer than its meaning |
| §4 | **high** | The chapter's densest block: an inverted direction of assertion, three effects with different timing, and a matching rule with four cases |
| §5 | medium-high | An altitude jump from node properties to Pod properties, over a topology abstraction the reader has not met |
| §6 | medium | Two escape hatches at different altitudes — one Pod field, one cluster configuration — plus a vocabulary mapping |
| §7 | low | Synthesis |

*"If you only have 15 minutes"* should point at **§1 plus §4's three-effect block**, then Bearings #2. That is the highest exam-points-per-minute route: the spine is the frame every other fact hangs on, and the taint effects are the chapter's densest recall material.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 7 — Assigning the Berth". Carried forward without modification:

- **Covers**: **D1.3** — scheduling overview; feasible nodes; filtering; scoring; binding; random tie-break; unschedulable Pods; node labels; `nodeSelector`; node affinity (required vs preferred); pod affinity/anti-affinity; taints and tolerations (NoSchedule / PreferNoSchedule / NoExecute); `nodeName`; topology spread; scheduling policies vs profiles.
- **Prerequisites**: Ch 5 (Pod, requests/limits), Ch 6 (workload resources creating Pods).
- **Retrieval targets**: **20%** **[B3]** — from Ch 4–6. Named anchors: labels (Ch 4) now doing node selection rather than Pod selection; requests (Ch 5) as the filter input; the controller (Ch 6) that produced the unscheduled Pod.
- **Question budget**: 8 Soundings · 10 Bearings · 17 Practice · 35 total. Bearings raised to 15 below.
- **Figures**: five anchors, listed verbatim in `figures_planned`.
- **Depth band**: standard.
- **Blocking gaps**: G4 (taints/tolerations, affinity, `nodeSelector`, topology spread) and G3 (requests, limits, QoS). **Status: G3 CLOSED. G4 is 90% closed — topology spread constraints remain entirely uncached.** See § Open questions #2.
- **[B3] Decay risk — thin downstream presence.** This is one of two chapters B3 singles out as at risk of being taught once and never revisited. Two downstream anchors are **mandatory and non-negotiable**: Ch 13 (Pending as a scheduling-failure signature) and Ch 17 (Cluster Autoscaler reacting to unschedulable Pods). See § What this chapter owes forward.

**One inherited discrepancy, resolved.** B4's `length-budget.md` retrieval schedule puts Chapters 6–8 at ~15%; B3's schedule and the arc outline both put Chapter 7 at 20%, and the arc outline tags the figure **[B3]**. The arc outline is the later stage and carries the explicit provenance tag, so **20%** is the operative figure. Chapter 6 resolved the same conflict the same way. Recorded once here so it is not re-litigated per chapter.

### Debts falling due in this chapter

Six published sections defer material here by name. Draft knowing the reader was told to expect each one.

| Owed by | Promise made | Paid in |
|---|---|---|
| **Ch 3 §2** (line 417) | *"how the scheduler actually chooses, in detail"* — dropped immediately after the kube-scheduler component paragraph | **§1**, which is exactly this and nothing more. Chapter 3 already stated the binding boundary; §1 collects it rather than re-arguing it |
| **Ch 3 §2** (line 415) | *"the scheduler selects a node and records that choice. It does not start anything… That split will look familiar by the end of §6"* | **§1**. The split is already installed. §1's job is to name the three steps it decomposes into |
| **Ch 4 §5** (line 688) | *"Node scheduling constraints use labels on nodes; the recommended approaches all use label selectors"* → *[see Ch 7 — node labels and nodeSelector]* | **§3**. Unnumbered pointer, no numbering constraint. This is **[B3]**'s designated labels anchor |
| **Ch 5 §8** (line 969) | *"requests are the input to the scheduler's filtering step"* → *[see Ch 7 §2]* | **§2** — pinned, and honored exactly |
| **Ch 2 §7** (line 807) | RuntimeClass carries `nodeSelector`, `tolerations` and a Pod overhead; *"Register that they exist; the reasoning behind them arrives later"* | **§2** (overhead, one clause), **§3** (node selection), **§4** (tolerations). The pointer's `§3` is partially broken — see § Open questions #1 |
| **Ch 6 Voyage Ahead** | *"It creates a Pod. It does not decide where the Pod goes… a Pod sits in `Pending` while the count it was supposed to satisfy stays unsatisfied, and the loop that created it goes on cheerfully wanting one more."* Also names the DaemonSet's tolerations as the mechanism already seen in disguise | **§1 and §2** for the opening beat; **§4** for the DaemonSet callback |

Chapter 6's Voyage Ahead is, like Chapter 5's before it, unusually generous — it states the problem, names the failure mode by its exact status string, and even plants the taint/toleration mechanism as something already met. **Do not re-argue it.** §1 collects it in one clause and moves.

### What this chapter owes forward

| Concept | Retrieved at | Contract |
|---|---|---|
| **Pending as a scheduling failure** | **Ch 13 (mandatory [B3] anchor)** — *"Pending → scheduling filters and taints"* is B3's named primary fix for this chapter's decay problem | §2 must state the Pending-is-not-an-error fact in a form Chapter 13 can quote and then extend into a diagnosis. Ch 7 names the state; Ch 13 supplies the procedure |
| **Unschedulable Pods** | **Ch 17 (mandatory [B3] anchor)** — the unschedulable Pod is Cluster Autoscaler's trigger | §2's "the Pod waits" must be written so that "…and something could be watching for exactly that" is a natural continuation, not a retrofit |
| **Requests as booked capacity** | Ch 13 (OOMKilled and Evicted), Ch 17 (autoscaling targets), Ch 18 (utilization relative to requests) | Chapter 5 owns the definition; §2 owns the scheduling consequence. Do not re-teach the definition — three chapters downstream already back-bear to Ch 5 §8, not here |
| **Taints and tolerations** | Ch 8 (`node.kubernetes.io/unschedulable` and what `cordon` actually does), Ch 12 (dedicated nodes as an isolation control, one clause) | §4 must name the built-in node-condition taints as a family, because Chapter 8's cordon story is unintelligible without them |
| **Node labels** | Ch 8 (the NodeRestriction admission plugin, as an instance of the admission gate), Ch 11 (storage topology, if the fetch supports it) | §3 names the `node-restriction.kubernetes.io/` prefix and forward-bears to Ch 8. One clause; the gate itself is Chapter 8's |
| **Pod anti-affinity and spreading** | Ch 9 (why a Service's backends being on distinct nodes matters), Ch 18 (availability as an SLO input, if it arises) | §5's availability motivation must be stated once, plainly, so Chapter 9 can point at it |
| **The scheduler is replaceable** | Ch 17 (extension points synthesis — the scheduler as one more pluggable seat) | §6 states the fact and stops. **Do not pre-collect the four-socket extension story**; that is Chapter 17's secondary Zenith |

**Scope boundary with Chapter 8 — state it once and hold it.** Chapter 7 owns node *labels* and node *taints* as scheduling inputs. Chapter 8 owns node *lifecycle*: `cordon`, `drain`, `uncordon`, node conditions, leases, and the `kubectl` command surface generally. §4 may name `node.kubernetes.io/unschedulable` as a built-in taint. If a paragraph starts explaining what `kubectl drain` evicts, it has crossed.

**Scope boundary with Chapter 13.** §2 names `Pending` and says the Pod waits. What to run to find out *why* — `kubectl describe`, the event stream, the scheduler's own message — is Chapter 13's, and B3 designates it as the retrieval that keeps this chapter alive. Handing Chapter 13 a fully diagnosed Pending Pod costs it its best anchor.

**Scope boundary with Chapter 17.** §6 says the scheduler is replaceable and that profiles are how its behaviour is configured. Cluster Autoscaler, Karpenter, VPA and KEDA are Chapter 17's, and the unschedulable-Pod trigger is specifically B3's second decay fix for this chapter. Naming Cluster Autoscaler here spends the anchor early.

**Reader positioning**: Communications Officer role family, **junior tier**. Single unified brand voice; only atmospheric register and reader rank differ.

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**The curiosity gap is already open, and Chapter 6 opened it precisely.** The previous chapter ended on the one thing the control loop cannot do: it creates a Pod, and it does not decide where the Pod goes. Collect that in a clause. Then widen it into the question the chapter actually answers, which is more interesting than "a component called the scheduler picks a node." The interesting fact is that the decision is made **once, by a component that does not run anything, and then never revisited**. A Pod is scheduled once in its lifetime and is never rescheduled to a different node. The machine it lands on is the machine it dies on. Everything else in this chapter — every label, every affinity rule, every taint — exists because that decision is irreversible and you get exactly one chance to influence it. Open there.

**The identity frame is the shift from describing workloads to describing the fleet they run on.** Chapters 4 through 6 made the reader someone who can write down what should exist. This chapter makes them someone who can also write down *where it should exist, and where it must not* — which is the first point in the book where the reader is reasoning about the cluster as a heterogeneous place rather than a uniform pool. Practitioners think about placement in terms of two directions at once: what a workload needs from a machine, and what a machine will accept. Newcomers only ever think about the first, which is why their first encounter with a tainted node reads as the cluster being broken. Say it in the practitioner's register; do not moralise about it.

**The stakes, stated flat and without inflation.** Five points on this book's authored allocation — CNCF publishes four domain weights and no sub-weights, and the front matter says so. What that number does not capture is that scheduling is where four separate exam-checkable facts live that have no home anywhere else in the curriculum: the two-step operation, the random tie-break, the binding boundary, and Pending-as-a-state-rather-than-an-error. Each is a single sentence and each is exactly the shape a recognition exam asks about. **[B3]** also flags this chapter as a decay risk — it is taught once at the 40% mark and revisited only twice. That is a fact about the book's architecture, not a reason to inflate the chapter; the fix is scheduled downstream and is Chapter 13's and Chapter 17's job, not this chapter's. No manufactured urgency. The reader is an adult professional and will notice.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Six outcomes, active verbs:

- **Trace** a Pod from creation to placement through the scheduler's two-step operation, and say what "binding" actually consists of.
- **Explain** why a node with free memory can still be infeasible for a Pod that needs less memory than it has.
- **Distinguish** the four mechanisms for influencing placement by which direction each one asserts — from the Pod, or from the node.
- **Predict** what happens to an already-running Pod when a node gains a taint, changes a label, or fills up.
- **Choose** between `nodeSelector`, node affinity, taints, and inter-Pod rules for a given placement requirement, and say what each one costs.
- **Recognise** every constraint in this chapter as either a filter or a score — which is the only thing you actually have to remember.

*You'll also stop reading `Pending` as an error message, which is a smaller change than it sounds and saves more exam points than anything else in the chapter.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Chapter 7's prerequisite set is Chapter 4 (labels and selectors), Chapter 5 (the Pod, requests and limits, scheduled-once) and Chapter 6 (workload resources creating Pods), plus general operational literacy about assigning work to machines. **Five questions test priors the reader arrives with; three are deliberate retrieval from Chapters 5 and 6.** **[B3]** Soundings sit outside the retrieval budget but do retrieval work anyway, sourced from B2's Prerequisites column.

**Fixed Points this chapter teaches, which Soundings must therefore not reveal:**

1. The scheduler filters, then scores, then binds — and binding is a notification to the API server, not an act of starting anything.
2. When several nodes score equally, one is chosen **at random**.
3. Filtering fits a Pod's **requests** against a node's *available* capacity — booked capacity, not observed usage, and not limits.
4. An unschedulable Pod stays `Pending` indefinitely. It is not an error and nothing times out.
5. `nodeSelector` is the blunt form; node affinity adds soft (`preferred`) rules and a richer operator set. `IgnoredDuringExecution` means a label change after binding does not move the Pod.
6. Taints repel from the node's side; tolerations permit but do not guarantee. Three effects, and only `NoExecute` touches Pods that are already running.
7. Inter-Pod affinity and anti-affinity constrain a Pod against the labels on *other Pods* within a topology domain.
8. `nodeName` bypasses the scheduler entirely and overrules everything else in the chapter.

Each question below is checked against that list.

| # | Question topic | What it tests | Spoiler check |
|---|---|---|---|
| 1 | You have eight machines with different amounts of free memory and a job that needs 8 GB. Describe how you would pick a machine — and say what you would have to know *in advance* to pick it automatically. | The placement prior in its general form, and specifically that automation requires the job's need to be *declared* rather than discovered | Names nothing Kubernetes-specific. §2's teaching is the counter-intuitive half — that "free" means unbooked rather than unused. A general instinct spoils none of it, and readers who answer "look at `free -m`" have set themselves up perfectly for §2 |
| 2 | Two candidate machines come out identical on every measure you can name. How do you choose between them, and does the choice matter? | The tie-breaking prior, framed as a design question | Deliberately does not ask "what would Kubernetes do." Most readers will propose round-robin, least-recently-used, or lowest hostname. §1's Fixed Point is that the real answer is *random*, which is more surprising after the reader has invested in a cleverer answer |
| 3 | **Retrieval from Ch 5 §8.** A container declares a request and a limit for memory. Chapter 5 said one of the two is read by the scheduler and the other is enforced by the kubelet. Which is which? | **[B3]**'s designated requests anchor, in its pre-test position. Chapter 5 stated this and sent the reader here | This is the anchor's setup, not its payoff. §2's Fixed Point is the *consequence* — that the request is booked whether or not it is used, so a busy node and an idle node with identical requests are equally full to the scheduler. Retrieving which field the scheduler reads reveals none of that |
| 4 | **Retrieval from Ch 5 §4.** A Pod is running happily. Its node then fills up with other work. Chapter 5 was emphatic that a Pod is scheduled once in its lifetime. So what does Kubernetes do — move it, or something else? | Trap #9 in pre-test position, and the load-bearing prior for §3's `IgnoredDuringExecution` and for the whole chapter's framing | The reader is retrieving a fact Chapter 5 taught explicitly. §3's Fixed Point is the *naming* — that this behaviour has a name inside the affinity rule and applies to labels too. The general once-only fact is the ramp |
| 5 | Some machines in your fleet are reserved for one team's workloads. There are two ways to express that: mark the machines, or mark the jobs. What does each approach cost you when a job arrives that nobody remembered to mark? | **The chapter's most valuable pre-test.** It surfaces the affinity-versus-taint asymmetry — mark the jobs and unmarked jobs land anywhere; mark the machines and unmarked jobs are excluded by default | Never mentions taints, tolerations or affinity. The Fixed Point being protected (#6) is the *direction of assertion* plus the three effects and their timing. This question makes the reader feel the asymmetry without handing them any of the vocabulary |
| 6 | **Retrieval from Ch 6.** A ReplicaSet wants three Pods and two exist, so it creates a third. There is nowhere in the cluster with room for it. What does the loop do next — give up, retry, error, or something else? | **[B3]**'s designated controller anchor. Chapter 6's Voyage Ahead set this up in its exact words | The reader is retrieving Chapter 6's *behaviour* — the loop goes on cheerfully wanting one more. §2's Fixed Point (#4) is the Pod's side of the same event: the status string, and that nothing times out. Knowing the loop keeps wanting does not tell you what the Pod's status says |
| 7 | You run two copies of a service so that one machine failing does not take the service down. Both copies land on the same machine. What have you actually lost, and what would you have had to say in advance to prevent it? | The anti-affinity prior, framed by its motivation rather than its mechanism | §5's teaching is that the constraint is expressed against *other Pods' labels* within a *topology domain* — a two-part abstraction. The reader who feels the failure has somewhere to put the mechanism; nothing here names it |
| 8 | In any system that assigns work to workers, give one good reason to override the assignment and pin a job to a named worker — and one reason it is a bad habit. | The `nodeName` prior. Deliberately asks for the cost as well as the benefit, because §6's Fixed Point is as much about what you give up as about what the field does | §6 teaches that `nodeName` overrules `nodeSelector` and affinity, and that the Pod simply fails if the named node cannot take it. A general instinct about pinning does not supply either consequence |

**Rubric**: standard 6+ / 3–5 / 0–2 per `branded-terms.yaml`. The 0–2 branch carries a specific instruction: **if questions 3, 4 and 6 were the misses, re-read Chapter 5 §8 and Chapter 5 §4 before starting §2.** Those two sections are the entire prerequisite base for §1–§3, and §2 will read as arbitrary rules without them.

**Note for drafting:** questions 1, 2, 5, 7 and 8 each surface a *problem* the chapter later solves, and questions 2 and 5 are the two most valuable in the set because both invite an answer that turns out to be wrong in an instructive way. Keep them phrased as situations. A Soundings question that can be answered by reciting a term has stopped doing metacognitive work.

---

## 4. Section plan

Seven sections. **§2 is pinned by a published cross-bearing** (`chapter-05` line 969); **§3 is partially pinned** (`chapter-02` line 807). See the frontmatter note and § Open questions #1.

### §1 — ⚪ One Decision, Made Once

**Collects Chapter 6's Voyage Ahead in the first clause and Chapter 3 §2's promise in the second.** Both are already stated well; the section's job is to answer, not to re-establish.

**First, the frame.** Scheduling in Kubernetes means assigning a newly-created, unbound Pod to a suitable node — and `kube-scheduler` is the default component that does it, running as part of the control plane, watching for Pods with no node assigned. The reader met that component in Chapter 3. What Chapter 3 deliberately withheld is *how* it chooses, and it said so.

**Second, the spine, which is the section's real work.** The choice is a two-step operation. **Filtering** eliminates the nodes where the Pod cannot run at all; what survives is the set of *feasible nodes*. **Scoring** ranks the survivors by the active scoring rules. The highest score wins. Then **binding**: the scheduler notifies the API server of its choice. Draw those three as a sequence and label what each step takes in and puts out, because the entire rest of the chapter is a catalogue of things that plug into step one or step two.

**Third, the coin flip.** If more than one node ties for the highest score, `kube-scheduler` selects one **at random**. State it plainly and let it be startling. It is the chapter's most memorable single fact, it is exactly the shape of a multiple-choice distractor, and it also does real conceptual work: it tells the reader that the scheduler is not trying to be optimal in a way they can predict, which is why influencing placement requires *saying something*, not reasoning about the algorithm.

**Fourth, the boundary Chapter 3 already installed.** The scheduler decides and records. The kubelet on the chosen node starts the containers. Chapter 3 stated this and said the split would look familiar; §1 collects it in a sentence rather than re-arguing it. This is where the once-only fact belongs too: a Pod is scheduled once in its lifetime and is never rescheduled to a different node. If the node dies, the Pod does not move — it is replaced by a new, near-identical Pod with a different UID, by a controller. The reader has this from Chapter 5; naming it here as *the reason the decision matters* is the new part.

- **Objectives**: D1.3
- **Concepts introduced**: `scheduling`, `kube-scheduler`, `unbound-pod`, `feasible-node`, `filtering`, `scoring`, `binding`, `random-tie-break`, `scheduled-once-per-lifetime`
- **Sources**: `k8s-docs-kube-scheduler-2026-08-23.md` (a scheduler watches for newly created Pods with no Node assigned; kube-scheduler is the default and runs as part of the control plane; feasible nodes; the 2-step filtering-then-scoring operation; assigns the Pod to the highest-ranked node; *if there is more than one node with equal scores, kube-scheduler selects one of these at random*; binding is notifying the API server of the decision). `k8s-docs-pod-lifecycle-2026-08-23.md` (Pods are scheduled once in their lifetime to a specific node; a Pod is never "rescheduled" to a different node). `k8s-docs-cluster-architecture-2026-08-23.md` and `k8s-docs-components-2026-08-23.md` (the scheduler as a control-plane component — already cited in Ch 3, retrieved here)
- **Figure**: `ch07-fig01-filter-score-bind`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — filter, then score, then bind. Binding is a *notification*; the kubelet on the chosen node is what starts anything. **This is the chapter's most-retrieved Fixed Point.** Write it to be quotable in §7, in Chapter 13 and in The Lodestar
  - `> ⚓ **Worth Securing:**` — the practical rule: if you want a Pod somewhere specific, you have to say so before it is created. There is no "move it later"
  - `> 🪢 **Mnemonic:**` — *filter, score, bind* is three words in the order they happen, and the subtitle is on the cover of the chapter. If the reader can say the three words they have most of §1
- **Cross-bearings**: back to Ch 3 §2 (**mandatory — the pinned payoff for "how the scheduler actually chooses, in detail"**, and for the binding boundary Chapter 3 promised would look familiar); back to Ch 6's Voyage Ahead (**mandatory** — the reader was handed the question in its exact terms); back to Ch 5 §4 (scheduled once, replaced never); forward to Ch 13 (what a Pod that never gets past this stage looks like from the outside)
- ⚠ **Do not teach preemption here.** It is named in §6 at most, one clause. See § Open questions #3
- ⚠ **Do not name Cluster Autoscaler.** It is B3's second decay anchor and belongs to Chapter 17

### §2 — 🔵 What Makes a Node Feasible

**Pinned by `chapter-05` line 969.** Chapter 5 taught requests and limits and told the reader that requests are the input to the scheduler's filtering step, then sent them here. This section discharges that promise and then adds the part Chapter 5 could not.

**The mechanism first.** Filtering finds the set of nodes where it is feasible to schedule the Pod. The canonical example is the `PodFitsResources` filter, which checks whether a candidate node has enough available resources to meet the Pod's specific resource *requests*. Note the word: requests. Not limits, which the kubelet enforces once the container is running; not observed usage, which the scheduler does not consult.

**Then the counter-intuitive consequence, which is the section's Fixed Point.** The kubelet reserves at least the request amount of a resource specifically for that container. So a request is a *booking*, and the scheduler is doing accounting against bookings, not measurement against usage. A node running ten containers that each requested 1 GiB and each actually use 50 MiB is, to the scheduler, ten gibibytes full. `free -m` on that node will say otherwise and the scheduler will not care. This is the fact that turns "the cluster has plenty of memory but my Pod won't schedule" from a mystery into arithmetic, and it is worth a worked example with actual numbers.

**A note on what "available" is measured against.** A node reports both `capacity` and `allocatable` — the second is what remains after the system's own reservations. One or two sentences; the reader needs the word to exist, not the reservation model. See § Open questions #8.

**Pod overhead, one clause.** Chapter 2 §7 told the reader that a RuntimeClass can carry a Pod overhead so the scheduler accounts for the runtime's resource cost, and said the reasoning would arrive later. Here is later: the overhead is added to the Pod's effective request, so a Pod running under a sandboxed runtime books more than its containers asked for. One clause and a back cross-bearing. Do not re-teach RuntimeClass.

**Close on the failure mode, which is the section's exam-critical half.** If filtering leaves an empty list, the Pod is not schedulable — and it stays `Pending` until the scheduler is able to place it. Nothing errors. Nothing times out. Nothing retries with different parameters. The Pod waits, indefinitely, and the controller that created it goes on wanting one more. This is the sentence Chapter 13 will quote and extend, and the sentence Chapter 17 will point at when something starts watching for exactly this condition. Write it to be quoted.

- **Objectives**: D1.3
- **Concepts introduced**: `podfitsresources`, `requests-as-scheduling-input`, `node-capacity`, `node-allocatable`, `pod-overhead`, `unschedulable`, `pending-pod`
- **Sources**: `k8s-docs-kube-scheduler-2026-08-23.md` (the filtering step finds the set of Nodes where it's feasible to schedule the Pod; the `PodFitsResources` filter checks whether a candidate Node has enough available resources to meet a Pod's specific resource requests; if the list is empty, that Pod isn't yet schedulable; if none of the nodes are suitable, the pod remains unscheduled until the scheduler is able to place it). `k8s-docs-resource-management-2026-08-23.md` (when you specify the resource request for containers in a Pod, the kube-scheduler uses this information to decide which node to place the Pod on; the kubelet reserves at least the request amount of that system resource specifically for that container; a container may use more than its request if the node has it available). `k8s-docs-nodes-2026-08-23.md` (a Node's status contains Capacity and Allocatable). `k8s-docs-runtime-class-2026-08-23.md` (RuntimeClass can carry a Pod overhead so the scheduler accounts for the runtime's resource cost). `k8s-docs-pod-lifecycle-2026-08-23.md` (`Pending` as a phase)
- **Figure**: none. The requests/limits/QoS relationship is already drawn in `ch05-fig05-requests-limits-qos-classes`, and **[B3]** designates this chapter as one of its four retrieval sites. **Refer to that figure by name rather than redrawing it** — same move Chapter 6 §3 made with `ch04-fig03`, and it is a spacing-effect retrieval at zero production cost
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `★ **Fixed Point:**` — filtering fits **requests** against *available* capacity. The scheduler books; it does not measure. A node can be busy and empty at the same time, and only one of those is the scheduler's business
  - `> **Before reading on:**` — generation-effect prompt: *a node has 16 GiB of memory. Four Pods on it each requested 4 GiB and each is using 200 MiB. A fifth Pod requests 1 GiB. Does it schedule?* Let the reader derive "no" before it is stated
  - `> ⚠ **Navigational Hazards:**` — `Pending` is a state, not an error. Nothing is retrying with different parameters and nothing will give up. A Pod can sit there for a week
  - `> 🔭 **Closer Look:**` — `PodFitsResources` is *one* filter, named in the docs as an example. The full filter set is configurable, which is §6's material. One short aside so the reader does not walk away thinking resources are the only feasibility test
- **Cross-bearings**: back to Ch 5 §8 (**mandatory — the pinned payoff**; the reader was told requests are the scheduler's input and sent here); back to Ch 2 §7 (**mandatory** — the RuntimeClass overhead promise, discharged in one clause); back to Ch 6 (the controller that created this Pod is still counting); forward to Ch 8 (`ResourceQuota` and `LimitRange` are how a cluster stops you booking the whole thing — one pointer, no content); forward to Ch 13 (**mandatory [B3] anchor** — `Pending` is the first Pod-failure signature Chapter 13 teaches); forward to Ch 17 (**mandatory [B3] anchor** — something can watch for unschedulable Pods and add nodes)
- ⚠ **Do not teach QoS classes.** They are Chapter 5's and the exam-relevant scheduling fact is requests-as-input, not the class taxonomy. One clause naming the connection is the ceiling
- ⚠ **Do not teach eviction under node pressure.** Evicted is Chapter 13's signature; §4's `NoExecute` is a different mechanism and conflating them is a trap the chapter should not create

### §3 — 🔵 Asking for a Particular Berth

**Partially pinned by `chapter-02` line 807; carries the unnumbered pointer from `chapter-04` line 688 and [B3]'s designated labels anchor.** Chapter 4 taught label selectors as the universal join and listed node scheduling constraints as one of four uses. This is that use collected — and it collects it with a direction inversion Chapter 4 did not state.

**The inversion first, because it is the section's cheapest win.** Every previous use of labels in this book has been *a controller selecting Pods*. Here it is *a Pod selecting nodes*. Same mechanism, opposite direction. Nodes have labels — you can attach them manually, and Kubernetes also populates a standard set on every node in a cluster. Say the inversion out loud; readers who have internalised labels-select-Pods will otherwise spend a page quietly confused.

**Then `nodeSelector`**, which is the simplest recommended form of node selection constraint: a field in the Pod spec listing node labels, and Kubernetes only schedules the Pod onto nodes that have *each* of the labels you specify. Blunt, readable, and adequate for most real requirements. It is an AND of exact matches and nothing else — which is precisely what makes the next thing exist.

**Then node affinity**, as the same idea with three additions. It is more expressive; it supports a richer operator set (`In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt`, `Lt`); and — the important one — it can express a rule as *soft*. The two forms are `requiredDuringSchedulingIgnoredDuringExecution`, where the scheduler cannot schedule the Pod unless the rule is met, and `preferredDuringSchedulingIgnoredDuringExecution`, where the scheduler tries to find a matching node but schedules the Pod anyway if it cannot. Those names are ugly and long and the reader will resent them; the correct move is to point out that they are two words joined — a *scheduling* half and an *execution* half — and that reading them as two halves makes them decode instantly rather than needing memorisation.

**And the execution half is the fact worth stopping on.** `IgnoredDuringExecution` means that if the node's labels change after the Pod is scheduled, the Pod continues to run. This is the once-only rule from Chapter 5 showing up inside a field name. The reader retrieved it in Soundings question 4; here it acquires a name.

**Close on the gradient**, which is what `ch07-fig02` draws: `nodeSelector` is blunt and hard; `required` affinity is expressive and hard; `preferred` affinity is expressive and soft. Choosing between them is choosing how much you want to say and how badly you want it obeyed.

- **Objectives**: D1.3
- **Concepts introduced**: `node-labels`, `standard-node-labels`, `nodeselector`, `node-affinity`, `required-during-scheduling`, `preferred-during-scheduling`, `ignored-during-execution`, `affinity-operators`
- **Sources**: `k8s-docs-assign-pod-node-2026-08-23.md` (nodes have labels; Kubernetes populates a standard set on all nodes; the recommended approaches all use label selectors; `nodeSelector` is the simplest recommended form and Kubernetes only schedules the Pod onto nodes that have *each* of the labels specified; affinity is more expressive, supports soft/preferred rules, and can constrain against labels on other Pods; the two `DuringScheduling…DuringExecution` forms and what each means; `IgnoredDuringExecution` means the Pod continues to run if node labels change after scheduling; operators `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt`, `Lt`; the `node-restriction.kubernetes.io/` prefix and the NodeRestriction admission plugin). `k8s-docs-labels-selectors-2026-08-23.md` (equality-based and set-based selectors, retrieved from Ch 4)
- **Figure**: `ch07-fig02-nodeselector-vs-affinity`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — `nodeSelector` is an AND of exact label matches. Node affinity is the same idea with soft rules and a richer operator set. `IgnoredDuringExecution` means a label change after binding does not move the Pod
  - `> 🪢 **Mnemonic:**` — read `requiredDuringSchedulingIgnoredDuringExecution` as two clauses: *required when scheduling, ignored once running*. The word is long; the meaning is eight words
  - `> ⚓ **Worth Securing:**` — reach for `nodeSelector` first. Affinity exists for the cases `nodeSelector` cannot express, and a soft rule you did not need is a rule someone will misread later
- **Cross-bearings**: back to Ch 4 §5 (**mandatory — [B3]'s designated labels anchor**; the reader was told node constraints use label selectors and sent here, and the direction inversion is the payoff); back to Ch 2 §7 (RuntimeClass carries a `nodeSelector` — the second third of that pointer's promise); back to Ch 5 §4 (once-only, now visible inside a field name); forward to Ch 8 (the NodeRestriction admission plugin, as one instance of the admission gate — **one clause only**); forward to §7
- ⚠ **Do not teach affinity `weight` arithmetic** for preferred rules. Naming that preferred rules can be weighted is the ceiling; the scoring arithmetic is not associate-tier. See § Open questions #6
- ⚠ **Do not teach `nodeName` here.** It is §6's, and its Fixed Point is that it is *not* a form of asking

### §4 — 🔵 When the Berth Refuses You

**The chapter's densest section**, and the one that pays the third of Chapter 2's three promises. It is also where Chapter 6's Voyage Ahead pointed when it said the reader had already met the mechanism in disguise.

**Open with the inversion, stated as a contrast.** Node affinity is a property of *Pods* that attracts them to a set of nodes. Taints are the opposite: they allow a *node* to repel a set of Pods. Tolerations are applied to Pods and allow the scheduler to schedule a Pod with a matching taint. One or more taints are applied to a node; that marks the node as not accepting any Pod that does not tolerate the taints. The whole section is downstream of that one sentence, and `ch07-fig03`'s job is to make the direction visible before the effects are enumerated.

**Then the qualification that produces the section's best trap.** Tolerations allow scheduling but do **not** guarantee it — the scheduler still evaluates every other parameter as part of its function. A toleration removes a veto. It does not make a request, it does not raise a score, and it does not create capacity. Readers will assume otherwise because "tolerate" sounds like a permission slip that comes with a seat attached.

**Then the three effects, which are the chapter's densest recall block.** Teach them by *when they act*, because that is what distinguishes them and it is also what a question will turn on:

- `NoSchedule` — no new Pods scheduled onto the node unless they tolerate the taint. Pods already running are **not** evicted.
- `PreferNoSchedule` — the soft version. The control plane will *try* to avoid placing a non-tolerating Pod there. Not guaranteed.
- `NoExecute` — the only one that touches running Pods. Non-tolerating Pods are evicted immediately. Pods that tolerate it with no `tolerationSeconds` stay bound indefinitely; Pods that tolerate it *with* `tolerationSeconds` stay for that long and are then evicted by the node lifecycle controller.

**Then matching, which is the Dead Reckoning block.** A toleration matches a taint if the keys are the same and the effects are the same, and either the operator is `Exists` (with no value specified) or the operator is `Equal` and the values are equal. Two wildcards: an empty key requires the `Exists` operator and matches all keys and values, though the effect must still match; an empty effect matches all effects for the given key. This is four rules with no metaphor available and no narrative to hang them on. **Write it as `— Dead Reckoning`, flat, in a table, with no berth register at all.** That contrast is itself pedagogically useful — the reader should be able to feel the chapter drop into reference mode and back out.

**Close on the built-in taints, which is where the DaemonSet callback lands.** The control plane adds taints to nodes automatically to represent conditions: `node.kubernetes.io/not-ready` and `unreachable` at `NoExecute`; `disk-pressure`, `memory-pressure`, `pid-pressure`, `unschedulable` and `network-unavailable` at `NoSchedule`. And the DaemonSet controller adds tolerations for all of them to the Pods it creates — which is exactly why a DaemonSet's log agent keeps running on a node that is under memory pressure and unschedulable for everything else. Chapter 6 promised this callback by name in its Voyage Ahead. Collect it.

- **Objectives**: D1.3
- **Concepts introduced**: `taint`, `toleration`, `noschedule`, `prefernoschedule`, `noexecute`, `tolerationseconds`, `taint-toleration-matching`, `built-in-node-condition-taints`
- **Sources**: `k8s-docs-taints-tolerations-2026-08-23.md` (node affinity attracts, taints repel; tolerations are applied to Pods and allow the scheduler to schedule Pods with matching taints; *tolerations allow scheduling but don't guarantee scheduling* — the scheduler also evaluates other parameters; the three effects and their exact semantics including `tolerationSeconds` and node-lifecycle-controller eviction; the four matching rules and the two empty-field wildcards). `k8s-docs-daemonset-2026-08-24.md` (the table of built-in node-condition taints with their effects, and that the DaemonSet controller adds `node.kubernetes.io/unschedulable:NoSchedule` automatically so DaemonSet Pods can run on unschedulable nodes). `k8s-docs-runtime-class-2026-08-23.md` (RuntimeClass can carry tolerations)
- **Figure**: `ch07-fig03-taints-tolerations-effects`
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2**
- **Markers planned**:
  - `★ **Fixed Point:**` — a taint is the node's refusal; a toleration is the Pod's exemption from that refusal. Only `NoExecute` affects Pods that are already running
  - `> **Dead Reckoning:**` — **required marker for this chapter.** The four matching rules and the two wildcards, stated flat with no metaphor
  - `> ⚠ **Navigational Hazards:**` — a toleration is not a request. It removes an objection; it does not attract, prioritise, or reserve. To *attract* a Pod to the dedicated nodes you tainted, you need affinity as well — the two mechanisms are complementary, not alternatives, and using only one is the most common real-world mistake in this material
  - `> 🪝 **Snag:**` — `PreferNoSchedule` is a preference. Pods will land on `PreferNoSchedule` nodes when nothing better is available, and that is correct behaviour, not a bug
  - `> **Logbook Entry:**` — the dedicated-nodes pattern told as a short scenario: a GPU pool that the platform team taints, and the two separate things a workload has to say to get one. Sidebar scope, opt-in depth, and it is the concrete case that makes the taint-plus-affinity pairing stick
- **Cross-bearings**: back to Ch 2 §7 (RuntimeClass tolerations — the last third of that promise); back to Ch 6 §7 and Ch 6's Voyage Ahead (**mandatory** — the DaemonSet's tolerations, named there as the mechanism already met in disguise); back to Ch 3 §3 (node components and node health, lightly); forward to Ch 8 (what `cordon` actually does, and the node conditions behind these taints — **one pointer, no content**); forward to Ch 12 (dedicated nodes as an isolation control — **one clause at most**); forward to Ch 13 (a Pending Pod whose cause is a taint, not capacity)
- ⚠ **Do not teach `kubectl cordon`, `drain` or `uncordon`.** Chapter 8 owns node lifecycle. §4 may name the `node.kubernetes.io/unschedulable` taint as a family member; the verbs are Chapter 8's
- ⚠ **Do not teach node conditions in detail.** `Ready`, `DiskPressure` and the rest are Chapter 8's; §4 needs them only as the things the built-in taints represent
- ⚠ **The `kubectl taint` command form is not present in the cached snapshot.** See § Open questions #10 before writing any command line

### §5 — 🟡 Placing Pods Relative to Each Other

The chapter's altitude jump. Everything so far has constrained a Pod against a property of a *node*. This section constrains a Pod against the properties of *other Pods* — which requires an abstraction the reader has not met.

**Lead with the motivation, not the mechanism**, because Soundings question 7 has already put the reader in the right place. Two replicas of a service that both land on the same node have not delivered the redundancy they were created for. Nothing in §2 or §3 prevents that: both Pods have identical requests, identical labels, and identical affinity, so both are equally feasible on every node and the scheduler is free to pick the same one twice. Redundancy is a property of the *set*, and none of the mechanisms so far can express a property of a set.

**Then the mechanism.** Inter-Pod affinity and anti-affinity let you constrain a Pod against the labels of Pods already running on a node — or in some other topological domain. Affinity co-locates: *schedule this only where a Pod with that label is already running*. Anti-affinity separates: *do not schedule this where a Pod with that label is already running*. Both come in the same `required` and `preferred` flavours as node affinity, which is a straight retrieval from §3 rather than new machinery.

**Then the topology abstraction, which is what makes this 🟡.** The domain is not always "the node." It is whatever a chosen node label divides the cluster into — a node, a rack, an availability zone. That is why the docs' own examples read *"only schedule on nodes in the same zone as a Pod with this label."* The topology key is the label whose *values* define the boundaries of the domains. Draw this; the sentence is hard and the picture is easy, and it is `ch07-fig04`'s whole job.

**Then topology spread constraints**, as the purpose-built answer to the motivation the section opened with. Anti-affinity can say "not on the same node"; spread constraints say "distribute these evenly across these domains, within this tolerance," which is what people actually want and what anti-affinity approximates awkwardly. ⚠ **This block has no cached source.** See § Open questions #2 — if the fetch does not land before drafting, the section must name topology spread constraints as existing, state that they are the purpose-built mechanism for even distribution, and stop. Guessing at the field semantics is not an option.

**Close on the cost**, which is the honest note and the reason this section is 🟡 rather than 🔵: inter-Pod rules make the scheduler's job substantially more expensive, because feasibility for one Pod now depends on what is already placed. The docs recommend against them in very large clusters. The reader should leave knowing this is a sharp tool.

- **Objectives**: D1.3
- **Concepts introduced**: `pod-affinity`, `pod-anti-affinity`, `topology-domain`, `topology-key`, `topology-spread-constraints`
- **Sources**: `k8s-docs-assign-pod-node-2026-08-23.md` (inter-pod affinity and anti-affinity allow you to constrain Pods against labels on other Pods — *"only schedule on nodes in the same zone as a Pod with this label"*, or *"spread these Pods across nodes"*; the same required/preferred forms apply). ⚠ **No cached source for topology spread constraints at all** — see § Open questions #2. ⚠ The large-cluster performance caveat is **not** in the cached snapshot either; it needs the same fetch or must be cut
- **Figure**: `ch07-fig04-pod-affinity-anti-affinity-topology`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — inter-Pod rules are evaluated against Pods *already placed*, within a topology domain defined by a node label. The domain is the part people forget
  - `> 🔭 **Closer Look:**` — why this is expensive: every candidate node now requires knowing what is on every other node in the domain. One short aside, and it is the justification for the closing caveat
  - `> 🪝 **Snag:**` — "spread my replicas across nodes" and "never put two of these together" are different requirements. Anti-affinity says the second and only approximates the first
- **Cross-bearings**: back to §3 (required/preferred is the same pair, second use); back to Ch 4 §5 (a third direction for the same label mechanism — Pods selecting Pods); back to Ch 6 §1 (the replicas that need separating came from one Deployment, and nothing about the Deployment expresses their relationship to each other); forward to Ch 9 (a Service's backends and why their distribution matters); forward to Ch 11 (storage topology, **conditional** — only if Chapter 11's sources support it)
- ⚠ **Do not teach availability zones as a cloud concept.** The topology key is a node label; whether its values happen to be zone names is the cluster operator's business
- ⚠ **Do not invent field names or YAML for topology spread constraints** if the source fetch has not landed

### §6 — 🟡 Overruling the Scheduler, and Replacing It

Two escape hatches at two different altitudes, held together by one frame: everything so far has been *influencing* a decision the scheduler makes. This section is about not letting it make the decision at all.

**First, `nodeName` — the Pod-level hatch.** It is a field in the Pod spec, and it is a more direct form of node selection than affinity or `nodeSelector`. If `nodeName` is not empty, the scheduler **ignores the Pod entirely**, and the kubelet on the named node tries to place it. `nodeName` overrules `nodeSelector` and every affinity and anti-affinity rule. And if the named node does not exist, or does not have the resources, the Pod simply fails — because the component whose job was to notice that in advance was skipped.

The framing matters here. `nodeName` is not the most forceful way of asking. It is the absence of asking. The API does permit specifying a node when you create a Pod, and the docs call this *unusual and only done in special cases* — which is a stronger discouragement than it looks, coming from reference documentation. Say why: you have taken responsibility for a check the system was doing for free, and you will not be told when you get it wrong.

**Second, the interesting middle case**, which is worth one short paragraph because it makes binding concrete. The DaemonSet controller does not use `nodeName` to place its Pods. It sets the Pod's `nodeAffinity` to match the target node and lets the default scheduler take over — and the scheduler then binds the Pod by setting `.spec.nodeName`. So `nodeName` is not a special user-facing shortcut at all; it is *the field binding writes to*, and setting it yourself is pre-empting the scheduler's own output. That reframe is the cheapest possible way to make "binding" stop being a vocabulary word.

**Third, `schedulerName` and custom schedulers — the cluster-level hatch.** `kube-scheduler` is designed so that you can write your own scheduling component and use that instead, and a Pod can name which scheduler should handle it. A DaemonSet, for instance, exposes `.spec.template.spec.schedulerName` for exactly this. Two sentences and a forward pointer; the reader needs to know the seat is pluggable, not how to build a scheduler.

**Fourth, how the default scheduler's own behaviour is configured**, which is the section's exam-checkable vocabulary. There are two supported models. **Scheduling Policies** is the older one: *Predicates* do filtering and *Priorities* do scoring. **Scheduling Profiles** is the plugin model: plugins implement stages including `QueueSort`, `Filter`, `Score`, `Bind`, `Reserve` and `Permit`, and `kube-scheduler` can run more than one profile at once.

Teach this as a **vocabulary mapping onto §1's spine**, not as two configuration systems. Predicates are filtering under an older name; Priorities are scoring under an older name; the profile plugin stages are the same pipeline with more seats exposed. A reader who sees the words *Predicate* and *Priority* in an old blog post and can map them onto filter and score has everything this material is worth. ⚠ **Currency risk** — see § Open questions #5.

- **Objectives**: D1.3
- **Concepts introduced**: `nodename`, `direct-node-assignment`, `schedulername`, `custom-scheduler`, `scheduling-policies`, `predicates`, `priorities`, `scheduling-profiles`, `scheduler-plugins`
- **Sources**: `k8s-docs-assign-pod-node-2026-08-23.md` (`nodeName` is a more direct form of node selection; if not empty the scheduler ignores the Pod and the kubelet on the named node tries to place it; using `nodeName` overrules `nodeSelector` and affinity/anti-affinity; if the named node does not exist or lacks resources, the Pod fails). `k8s-docs-kube-scheduler-2026-08-23.md` (kube-scheduler is designed so you can write your own scheduling component; the API lets you specify a node for a Pod at creation, but this is unusual and only done in special cases; the two supported configuration models — Scheduling Policies with Predicates and Priorities, and Scheduling Profiles with plugins implementing QueueSort, Filter, Score, Bind, Reserve, Permit; kube-scheduler can run different profiles). `k8s-docs-daemonset-2026-08-24.md` (the DaemonSet controller sets `spec.affinity.nodeAffinity` and the default scheduler then binds by setting `.spec.nodeName`; `.spec.template.spec.schedulerName` selects a different scheduler)
- **Figure**: none. `ch07-fig01` already carries the pipeline this section names alternative implementations of, and the Zenith figure will show `nodeName` sitting outside it. A third diagram of the same three stages would be exactly the channel redundancy Part 18.7 warns against
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `★ **Fixed Point:**` — `nodeName` bypasses the scheduler. It overrules `nodeSelector` and affinity, and it removes the feasibility check, so the Pod fails rather than waits
  - `> 🪢 **Mnemonic:**` — Predicates filter, Priorities prioritise (score). The old names describe the same two steps
  - `> ⚓ **Worth Securing:**` — `nodeName` is what binding *writes*. Setting it by hand is not a special API; it is filling in the scheduler's answer before it was asked the question
- **Cross-bearings**: back to §1 (binding, now shown as a field write); back to §3 (`nodeName` overrules everything §3 taught); back to Ch 6 §7 (how a DaemonSet Pod actually reaches its node — the answer is "the ordinary scheduler," which surprises people); forward to Ch 8 (`kubeadm` and self-hosted clusters are where profile configuration would live — **one pointer**); forward to Ch 17 (the scheduler as one more pluggable seat, collected with CRI, CNI, CSI and CRDs — **name nothing; Chapter 17 owns the collection**)
- ⚠ **Do not pre-collect the extension-point synthesis.** §6 establishes that the scheduler is replaceable and stops. Chapter 17's secondary Zenith is the four-way collection, and naming CRI/CNI/CSI alongside it here spends that Zenith's setup
- ⚠ **Do not teach how to write a scheduler plugin**, and do not enumerate the full plugin stage list beyond the six the cached source names

### §7 — ☀️ Everything Is a Filter or a Score

The chapter's Zenith and its one dramatic synthesis illustration. Short — synthesis sections earn their effect by arriving, not by elaborating.

**The recognition.** The chapter has taught six vocabularies for influencing placement, and they look like six separate systems with six separate syntaxes. They are not. Every one of them plugs into one of exactly two slots in §1's spine:

- **Filters** — things that remove nodes from consideration. Insufficient available capacity for the Pod's requests. `nodeSelector`. `required` node affinity. A `NoSchedule` or `NoExecute` taint without a matching toleration. `required` inter-Pod rules.
- **Scores** — things that change the ranking of nodes that survived. `preferred` node affinity. `PreferNoSchedule`. `preferred` inter-Pod rules. The rest of the scoring plugins.

Six vocabularies, two slots. That is the whole chapter, and it is why the subtitle names the two steps and the coin flip and nothing else.

**The one exception, drawn deliberately outside the loop.** `nodeName` is neither. It does not narrow the feasible set and it does not adjust a score — it removes the decision. That is exactly why it is dangerous and exactly why the docs call it unusual.

**One sentence of spine continuity, and no more.** The scheduler is itself a control loop: it watches for Pods with no assigned node and acts on the difference between what exists and what is placed. The reader should notice. **[B3]** designates Chapter 15 as the book's primary Zenith for the control loop and Chapter 17 as the secondary; this chapter gets a nod, not a movement. One sentence, and stop.

- **Objectives**: D1.3
- **Concepts introduced**: none new. Synthesis only
- **Sources**: no new citations. Every claim in §7 is a re-statement of something sourced in §1–§6, and the drafting stage should carry the tags forward rather than re-citing
- **Figure**: `ch07-zenith-berth-assignment`
- **Checkpoint after**: no
- **Markers planned**:
  - `☀️ **Zenith**` — the chapter's one Zenith, per Part 18.10
  - `> ⚓ **Worth Securing:**` — the diagnostic question for any placement problem: *is this a filter that excluded every node, or a score that ranked the wrong one first?* The two have completely different symptoms — `Pending` forever versus placed-somewhere-you-did-not-want — and knowing which you are looking at is most of the diagnosis
  - `🏆 **Safe Harbor**` — chapter close, with the Voyage Progress strip `🗺️ → 🌊 → 🌅` and the Part II position line, matching the form Chapters 5 and 6 shipped
- **Cross-bearings**: back to §1 (**mandatory** — the figure and the claim are both re-presentations of `ch07-fig01`); forward to Ch 8 (the last chapter of Part II, and the one that turns the rest of D1 from rules into consequences); forward to Ch 13 (**mandatory [B3] anchor** — the Voyage Ahead should hand Chapter 13 the `Pending` Pod explicitly, the way Chapter 6 handed this chapter the unplaced one)

**The Voyage Ahead should do for Chapter 8 what Chapter 6 did for this one.** Chapter 8 is administration: the `kubectl` surface, the three API access gates, node lifecycle, version skew. The honest bridge is that this chapter's reader can now say where a Pod should go but has no vocabulary for the machine it goes *on* — no way to take a node out of service, no way to cap what a namespace may book, and no idea which versions of which components are allowed to disagree. Name the taint you met in §4, `node.kubernetes.io/unschedulable`, and point out that something puts it there on purpose. That is Chapter 8's opening and it is already in the reader's hands.

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 15 questions total.** B4 allocates 10; this raises it to 15 on B4's standing instruction that the minimum is *"a contract to exceed, not a target to hit."* Chapters 3, 4, 5 and 6 all carry three checkpoints, so this is the book's established shape. The structural case is that the chapter has three separable modes: mechanism (§1–§2), the two directions of constraint (§3–§4), and relative placement plus opting out (§5–§6). Folding to two would put the taint effects and the topology abstraction in one block — two of the chapter's three hardest things, back to back, in different cognitive modes. Chapter total moves 35 → 40.

**Retrieval-practice content: 20%** **[B3]** — drawn from **Chapters 4, 5 and 6**. Chapter 1 is excluded from the retrieval schedule entirely and no item may test exam mechanics. Against a combined Bearings-plus-Practice pool of 32, the 20% target is ~6–7 items, allocated **3 in Bearings and 4 in Practice** (7 of 32 = 21.9%).

Each of B3's three named anchors has exactly one section where it belongs:

| **[B3]** named anchor | Placement | Why here |
|---|---|---|
| **Requests (Ch 5) as the filter input** | Bearings #1, item 3 | §2 is the payoff for a pinned cross-bearing Chapter 5 dropped by section number. The retrieval and the discharge are the same beat |
| **The controller (Ch 6) that produced the unscheduled Pod** | Bearings #1, item 5 | §2's Pending fact is only interesting because something upstream is still counting. Chapter 6's Voyage Ahead framed it exactly this way |
| **Labels (Ch 4) now doing node selection rather than Pod selection** | Bearings #2, item 1 | §3 is where the direction inverts. Asking immediately after is the shortest gap between teaching and retrieval, so this item must be the *hard* version — the inversion, not the definition |

### ☆ Taking Your Bearings #1 — after §2

- **Topic**: how the decision is made, and what makes a node eligible to receive it
- **Questions**: 5
- **Retrieval from earlier chapters**: 2 of 5 (both **[B3]** named anchors; see the concentration note below)
- **Difficulty**: mostly ⚪, with item 4 at 🔵

  1. Name the scheduler's three steps in order, and say which component actually starts the container. **Tests §1's Fixed Point directly.** Trap answers must include a version where the scheduler starts the container, and a version that omits binding entirely or treats it as the kubelet's action.
  2. Three nodes survive filtering and all three score identically. What does `kube-scheduler` do? **Correct answer: picks one at random.** Trap answers must be the plausible alternatives readers proposed in Soundings question 2 — lowest name, least loaded, round-robin. This is the item that rewards having been wrong earlier.
  3. **Retrieval from Ch 5 §8 — requests and limits.** A container requests 2 GiB and limits at 4 GiB. Which number does the scheduler use when deciding whether a node can take this Pod, and what does the other number do? **[B3]** named anchor and the pinned Chapter 5 payoff appearing as an assessment item.
  4. 🔵 A node has 16 GiB of memory and four Pods on it, each of which requested 4 GiB. Monitoring shows the node using 2 GiB total. A new Pod requesting 1 GiB will not schedule there. Explain why, in one sentence. **Correct answer: the requests are booked whether or not they are used, so the node is fully allocated regardless of actual usage.** **The checkpoint's hardest item by design**, and the one that most directly predicts whether the reader will be able to diagnose a real Pending Pod.
  5. **Retrieval from Ch 6.** A Deployment wants three replicas, two are running, and the third cannot be placed anywhere. Describe the state of the third Pod and describe what the ReplicaSet controller does about it. **Correct answer: the Pod is `Pending` indefinitely; the controller does nothing further, because from its point of view the Pod exists — the gap it was closing is closed.** **[B3]** named anchor. This item is doing double duty: it is the retrieval, and it is the setup for Chapter 13's first failure signature.

- **Note on the 40% concentration.** Two of the chapter's three Bearings retrieval items land here because both anchors belong to §2 and nowhere else. Spreading them for an even per-checkpoint rate would place each one where it does not belong. The chapter's overall rate is 21.9%, which is the figure that matters.
- **Answer-key requirement**: item 5's key must stop short of diagnosis. Naming the state is this chapter's job; `kubectl describe`, the event stream, and what to do about it are Chapter 13's, and **[B3]** designates that handoff as one of two mandatory anchors keeping this chapter alive.

### ☆ Taking Your Bearings #2 — after §4

- **Topic**: the two directions — what a Pod asks for, and what a node refuses
- **Questions**: 5
- **Retrieval from earlier chapters**: 1 of 5
- **Difficulty**: 🔵 throughout, with item 4 at 🟡

  1. **Retrieval from Ch 4 §5 — labels and selectors.** Every previous use of labels in this book has been one object selecting a set of Pods. `nodeSelector` uses the same mechanism. What is selecting what, and in which direction? **Correct answer: the Pod's spec selects nodes by their labels — the direction is inverted relative to every prior use.** **[B3]** named anchor, deliberately written as the inversion rather than the definition.
  2. You taint a set of nodes `dedicated=gpu:NoSchedule` and add a matching toleration to your GPU workload. A colleague reports the GPU Pods are running on ordinary nodes. Is anything broken? **Correct answer: no — a toleration permits, it does not attract. You also need affinity or a `nodeSelector` to pull them to the GPU nodes.** **This is the chapter's designated struggle item** — label it as such per Part 10B and normalise the difficulty, because the intuitive answer is wrong and the reader should be told that missing it is expected.
  3. A node gains a new taint while Pods are already running on it. For each of the three effects, say whether the running Pods are affected. **Correct answer: `NoSchedule` and `PreferNoSchedule` affect only new placements; `NoExecute` evicts non-tolerating Pods immediately.** Trap answers should include a version where `NoSchedule` evicts.
  4. 🟡 A Pod is running on a node. Someone removes the node label that the Pod's `requiredDuringSchedulingIgnoredDuringExecution` affinity rule was matching on. What happens to the Pod? **Correct answer: nothing — `IgnoredDuringExecution` means exactly that, and Chapter 5's once-only rule is why.** Tests whether the reader can decode the field name rather than recognise it.
  5. Give one placement requirement that `nodeSelector` cannot express and node affinity can, and say which feature of affinity makes the difference. **Correct answer: any soft/preferred requirement, or any rule needing `NotIn`, `Exists`, `Gt` or `Lt` — `nodeSelector` is an AND of exact matches only.**

- **Answer-key requirement**: item 2's key must state the complementarity explicitly — taints exclude, affinity attracts, and a dedicated-node setup needs both. This is the single most transferable operational fact in the chapter and it is not stated as a rule in any cached source, so the key is where it becomes explicit.

### ☆ Taking Your Bearings #3 — after §6

- **Topic**: placing Pods relative to each other, and getting out of the scheduler's way
- **Questions**: 5
- **Retrieval from earlier chapters**: 0. The chapter's 20% is met by Bearings #1 items 3 and 5, Bearings #2 item 1, and four Practice items; a fourth Bearings retrieval would push this checkpoint off its own topic
- **Difficulty**: 🔵, with items 2 and 5 at 🟡

  1. Your three replicas all land on one node. Nothing in their spec is wrong. Explain why the scheduler was entitled to do that, and name the kind of rule that would have prevented it.
  2. 🟡 An inter-Pod anti-affinity rule uses a topology key of `topology.kubernetes.io/zone` rather than `kubernetes.io/hostname`. What changes about where the Pods may land? **Correct answer: the exclusion now applies per zone rather than per node — two Pods may share a node only if… no: they may not share a *zone*, which is stricter.** Tests whether the topology domain is understood as a variable rather than as "the node." **This is the section's hardest idea and the item exists to check it.**
  3. A Pod spec sets both a `nodeSelector` and a `nodeName`. Which wins, and what happens if the named node cannot fit the Pod? **Correct answer: `nodeName` wins and the scheduler is bypassed entirely; the Pod fails rather than waiting in `Pending`, because nothing performed the feasibility check.** Trap answers should include "it stays Pending," which is right for every other failure in the chapter and wrong here.
  4. Map the older Predicates-and-Priorities vocabulary onto the two steps you learned in §1. **Correct answer: Predicates are filtering, Priorities are scoring.**
  5. 🟡 **Interleaved with §1 and §4.** A DaemonSet's Pod ends up on a node that is under memory pressure and is refusing all other work. Explain how it got there and which component placed it. **Correct answer: the DaemonSet controller sets node affinity for the target node and adds tolerations for the built-in condition taints; the ordinary default scheduler then binds it by writing `.spec.nodeName`.** This item requires §1, §4 and §6 together, and it is the one that makes "binding" concrete.

- **Answer-key requirement**: item 5's key must name the mechanism as *the ordinary scheduler doing its ordinary job* rather than as a special case. That reframe is what makes §6's `nodeName`-is-binding's-output claim land, and it is also a Chapter 6 debt discharged.

---

## 6. Exam Alert plan

**High-priority topics** — the nine most likely to be tested directly, in descending order of confidence:

1. **Filter → score → bind**, in that order, with binding as a notification to the API server.
2. **The scheduler does not start the container.** The kubelet on the chosen node does.
3. **Equal scores break at random.**
4. **An unschedulable Pod stays `Pending`.** It is not an error and nothing times out.
5. **Filtering fits requests**, not limits and not observed usage.
6. **A Pod is scheduled once and never rescheduled** — retrieved from Chapter 5, and the reason placement is worth influencing at all.
7. **The three taint effects and their timing**, especially that only `NoExecute` touches running Pods.
8. **A toleration permits; it does not attract.**
9. **`nodeName` bypasses the scheduler** and overrules `nodeSelector` and affinity.

**Common traps to call out.** B1 traps #24, #25, #26 and #9 are all `[source]`-tagged, so all four may be described as things candidates get wrong. **None are `[inferred]`, so no hedging is required** — and equally, none may be dressed with invented frequency figures (Part 14 guardrail #8, and **[B3]**'s fourth do-not-retrieve rule).

| B1 # | Trap | Where it is defused |
|---|---|---|
| 24 | "The scheduler places the Pod on the node" | §1 Fixed Point, Bearings #1 item 1 |
| 25 | "The scheduler picks the single best node deterministically" | §1, Bearings #1 item 2 |
| 26 | "An unschedulable Pod errors out" | §2 Navigational Hazards, Bearings #1 item 5 |
| 9 | "A failed Pod is rescheduled to a healthy node" | §1 close (retrieved from Ch 5 §4), Bearings #2 item 4 |

Trap #24 is worth special handling: **Chapter 3 §2 already defused it**, explicitly and well, and told the reader it would recur. Repeating the correction from scratch would be channel redundancy (Part 18.7). The right move is to *retrieve* it — "you already know this; here is the piece Chapter 3 held back" — which is also a free spacing-effect hit.

**Six non-B1 traps worth adding**, all visible now that G4's two fetches have landed. B1 catalogued this competency as a blocking gap and therefore had no source to catalogue traps from:

- **"A toleration schedules the Pod on the tainted node."** It does not. Tolerations allow scheduling but do not guarantee it; the scheduler still evaluates every other parameter. §4's Navigational Hazards and Bearings #2 item 2. **This is the chapter's most valuable non-B1 trap** — it is the one that produces real-world confusion, it is stated explicitly in the cached source, and it has a clean correct answer.
- **`NoSchedule` treated as evicting running Pods.** Only `NoExecute` does. §4's effect table.
- **"Node affinity moves a Pod when the node's labels change."** `IgnoredDuringExecution` says otherwise, and Chapter 5's once-only rule is the reason. §3.
- **"`PreferNoSchedule` means never."** It is a preference and the control plane will place Pods there when nothing better exists. §4's Snag.
- **"`nodeSelector` and affinity are two syntaxes for the same power."** Affinity adds soft rules and five operators `nodeSelector` cannot express. §3, Bearings #2 item 5.
- **"A Pod with `nodeName` set that cannot fit will wait."** It fails. Every other failure in the chapter produces `Pending`; this one does not, which is exactly what makes it a good distractor. §6, Bearings #3 item 3.

**Do not include** in the Exam Alert: `cordon`/`drain`/`uncordon` or node conditions (Ch 8); `ResourceQuota` and `LimitRange` (Ch 8); QoS classes (Ch 5, already taught); OOMKilled and Evicted (Ch 13); Cluster Autoscaler, Karpenter, VPA, KEDA (Ch 17); the four-socket extension synthesis (Ch 17); anything about diagnosing a Pending Pod procedurally (Ch 13).

---

## 7. Practice Questions plan

**17 questions** (B4 allocation, unchanged). Distribution follows section weight rather than section count — §1 is short but carries three of the chapter's nine exam-priority topics, and §5's material is a third of the chapter's difficulty in one section:

| Block | Questions | Notes |
|---|---|---|
| §1–§2 — the spine, feasibility, requests, Pending | 6 | Includes **2 retrieval items**. At least 2 must require a numeric or predictive answer, not a definition |
| §3–§4 — node selection and taints | 6 | Includes **1 retrieval item**. All four B1 traps and the two §4 non-B1 traps must appear as distractors here, not only in the Exam Alert |
| §5 — inter-Pod rules and topology | 3 | Includes **1 retrieval item**. Three is correct given the topology-spread source gap; if the fetch lands and the section grows, this may go to 4 by taking one from §6 |
| §6 — overruling and reconfiguring | 2 | Two is right for a section whose whole content is three facts and a vocabulary mapping |

**Retrieval allocation: 4 of the 17 draw from Chapters 2–6**, allocated *within* this count and not added to it:

- **Scheduled once, replaced never** (Ch 5 §4) — §1–§2 block. Framed forward rather than backward: *a better node joins the cluster an hour after your Pod was placed. What happens?* Chapter 5 taught the rule with a node-failure motivation; this supplies a second, more surprising instance of the same rule.
- **The scheduler decides, the kubelet acts** (Ch 3 §2) — §1–§2 block. **Four chapters back.** B3's ≥4-back spacing floor does not formally activate until Chapter 8, but adopting it one chapter early costs nothing and this is the natural candidate, since Chapter 3 planted the fact specifically so this chapter could collect it. Recorded as voluntary early adoption, not as a schedule change.
- **Labels and selector operators** (Ch 4 §5) — §3–§4 block. Deliberately framed differently from Bearings #2 item 1: that item asks about the *direction* of selection, this one asks whether the operator vocabulary the reader learned for Pod selectors transfers to node affinity.
- **DaemonSet: one Pod per matching node** (Ch 6 §7) — §5 block, attached to the spreading discussion. Framed as *a DaemonSet achieves perfect distribution across nodes without any anti-affinity rule. Why doesn't it need one?* Correct answer: distribution is the resource's definition rather than a scheduling constraint. It is a retrieval and a discrimination item at once.

**Interleaving strategy.** At least **four** questions must require two sections at once:

- Spine + taints (§1 + §4) — which of the scheduler's two steps a `NoSchedule` taint participates in, and which one `PreferNoSchedule` participates in. This is §7's Zenith claim, tested before §7 states it.
- Requests + node selection (§2 + §3) — a Pod with a `nodeSelector` matching exactly one node, and that node lacks capacity. Which failure do you get?
- Taints + inter-Pod rules (§4 + §5) — a node that repels, and a Pod that wants to be near a Pod on that node. Two constraints, one of which is a filter the other cannot override.
- `nodeName` + everything (§6 + §2 + §3) — the field that makes every other mechanism in the chapter irrelevant, and the one failure mode that is not `Pending`.

**Trap-answer requirement** (skill Part 11): every wrong option must target a specific misconception and the answer key must explain why each is wrong. For the §1–§2 block, wrong options should be drawn from B1 traps #24–#26 in their exact wrong form. For the §3–§4 block, the toleration-attracts misconception must appear at least twice, in two different question shapes, because it is the chapter's most durable error.

**One calibration note.** This chapter has an obvious failure mode as a question set: it is full of enumerable lists — three effects, six operators, two configuration models, four matching rules — and it would be easy to write seventeen recall items that all reduce to "which of these four is not one of the three." Resist. The high-value question modes here are **prediction** ("what does the cluster do next") and **discrimination** ("which mechanism expresses this requirement"). Pure enumeration should account for no more than three of the seventeen, and the taint effects are the only list that genuinely earns one, because the *timing* differences between the three are behavioural rather than nominal.

---

## 8. Required figures

Five anchors, exactly as the arc outline specifies. §2 and §6 deliberately carry none — see each section's Figure line for the Part 18.3/18.7/18.9 reasoning.

### `ch07-fig01-filter-score-bind`

- **Purpose**: §1's Fixed Point, dual-coded. The structural frame every other fact in the chapter attaches to, and the shape the Zenith re-presents.
- **Content**: a left-to-right pipeline. On the left, a Pod with no node, and the full set of cluster nodes. Stage one, **Filter**: the node set narrows, with the excluded nodes visibly removed rather than greyed. Stage two, **Score**: the survivors carry numeric ranks. Stage three, **Bind**: an arrow from the scheduler to the API server — *not* to the node — and a separate, visibly distinct arrow from the kubelet on the chosen node to the container it starts.
- **Design requirement — the binding arrow must not point at the node.** This figure's single most important job is defusing trap #24, and a diagram where the scheduler's arrow lands on a node teaches the trap rather than the correction. The scheduler talks to the API server; the kubelet talks to the container runtime. Two arrows, two sources, visually distinct. Must survive grayscale (Part 18.11).
- **Label count**: Pod, node set, Filter, Score, Bind, API server, kubelet — seven. At the Part 18.12 ceiling; do not add the tie-break to this figure, it belongs in prose.
- **Reuse note**: §7's Zenith is a re-presentation of this shape. Design them together.

### `ch07-fig02-nodeselector-vs-affinity`

- **Purpose**: §3's Fixed Point. A comparative illustration (Part 18.10), and the chapter's only one.
- **Content**: three columns on one axis of expressiveness. Column one, `nodeSelector`: an AND of exact matches, hard. Column two, `required` node affinity: richer operators, still hard. Column three, `preferred` node affinity: richer operators, soft. Under each column, the same worked requirement expressed three ways, with a marker showing which columns *can* express it.
- **Design requirement — hardness and expressiveness must read as two independent axes.** The common misreading is that affinity is simply "more powerful `nodeSelector`," which loses the fact that `required` affinity and `nodeSelector` fail identically. Draw hardness as a property of the row and expressiveness as a property of the column, so the reader can see that only one of the three cells is soft.
- **Label count**: three mechanism names, two axis labels, hard/soft markers — seven at most. At the ceiling.
- **Note**: do not render full YAML. A field name and a shape is enough; this is a concept diagram, not a reference card.

### `ch07-fig03-taints-tolerations-effects`

- **Purpose**: §4's Fixed Point, and the chapter's densest recall block made visual.
- **Content**: a node with a taint, and three Pods approaching it — one with no toleration, one with a matching toleration, one already running on the node when the taint is applied. The three effects are three rows, and each row shows what happens to all three Pods. `NoExecute`'s row is the only one where the already-running Pod moves.
- **Design requirement — timing is the pedagogy, and the already-running Pod is how it shows.** A figure that only depicts arriving Pods cannot distinguish `NoSchedule` from `NoExecute`, which is the exact distinction the figure exists for. The third Pod — the one already aboard — must be present in all three rows and must be visibly unaffected in two of them.
- **Design requirement — direction.** The taint must read as emanating from the *node* and the toleration as belonging to the *Pod*. Colour is not sufficient (grayscale constraint); the shapes or the arrow origins have to carry it.
- **Label count**: three effect names, node, three Pod states, taint, toleration — nine. **Over the ~7 ceiling.** Resolution: the figure is read row by row rather than apprehended whole, and the three effect names are the row headers rather than in-frame labels. If the illustrator finds it still crowded, the fix is to drop the `tolerationSeconds` case to prose, not to drop a row.
- **Reuse note**: this belongs in The Lodestar. Design it to be legible at one-quarter page.

### `ch07-fig04-pod-affinity-anti-affinity-topology`

- **Purpose**: §5's hardest idea — that the topology domain is a variable, not "the node."
- **Content**: one cluster drawn twice, side by side, with the same six nodes and the same anti-affinity rule. Left: topology key is the hostname label, so the domains are individual nodes and the Pods are separated per node. Right: topology key is the zone label, so the domains are the two zones and the same rule produces a much stronger separation. Same rule, same cluster, different key, different outcome.
- **Design requirement — the two panels must be identical except for the key.** The entire argument is that one label changes the meaning of the rule. Any other difference between the panels — different node counts, different Pod counts, different placement of the surviving Pods for reasons unrelated to the key — destroys it.
- **Label count**: two topology keys, node group boundaries, two Pod sets, the rule itself — six or seven. Within budget if the rule is stated in the caption rather than in-frame.
- ⚠ **Blocked on the topology-spread source gap only if the figure is extended to cover spread constraints.** As specified above it covers affinity/anti-affinity and the topology-key variable, both of which are sourced today. **Do not extend it to spread constraints** unless the fetch lands. See § Open questions #2.

### `ch07-zenith-berth-assignment`

- **Purpose**: the chapter's one Zenith. The claim that six vocabularies occupy two slots.
- **Content**: `ch07-fig01`'s pipeline at the centre — unmistakably the same shape, not a redrawn variant — with the chapter's mechanisms arranged as inputs feeding into either the Filter stage or the Score stage. Filter side: capacity against requests, `nodeSelector`, `required` node affinity, non-tolerated `NoSchedule`/`NoExecute`, `required` inter-Pod rules. Score side: `preferred` node affinity, `PreferNoSchedule`, `preferred` inter-Pod rules. And `nodeName` drawn **outside the pipeline entirely**, with an arrow that bypasses both stages and lands on the outcome.
- **Design requirement — `nodeName`'s bypass is half the figure's argument.** If it is drawn as a third input alongside the others, the figure says "there are three slots," which is wrong and undoes §6. It must visually leave the pipeline alone.
- **Design requirement — visual continuity with `ch07-fig01`.** The recognition is the payload. If the reader does not see the same three stages they saw at the start of the chapter, the Zenith becomes a ninth list.
- **Label count**: two stage names, eight mechanisms, `nodeName` — eleven. **Over the ceiling, and justified**: the count *is* the argument, exactly as `ch06-zenith`'s six controllers were. Dropping a mechanism to hit seven would weaken the claim that all of them sort into two slots. The mitigation is that the labels are grouped into two visually distinct columns, so the reader holds one column at a time.
- **Register note**: Communications Officer family, junior tier. This is a dramatic synthesis illustration, not a reference diagram (Part 18.10) — it carries the brand's illustrative register, unlike `fig03`, which is deliberately utilitarian. The berth-assignment image is available and the chapter is named for it. Use it once, here, and let §1–§6's prose stay plain per B2's density guidance.

---

## 9. Open questions for the author

1. **⚠ BLOCKING (editorial) — `chapter-02` line 807 points at Ch 7 §3 for three topics that cannot share a section.**

   | Published pointer | Wants §3 to be | Status under this plan |
   |---|---|---|
   | `chapter-05` line 969 | *"resource requests as a scheduling filter"* → §2 | **Honored** — §2 is exactly this |
   | `chapter-02` line 807 | *"node selection, tolerations, and accounting for overhead"* → §3 | **Partial** — node selection is §3; overhead is §2; tolerations are §4 |

   The three topics named in Chapter 2's pointer belong to three different mechanisms: Pod overhead is resource accounting and must sit with requests; node selection is the Pod's attraction side; tolerations are the node's repulsion side. Putting all three in one section would mean teaching the taint/affinity contrast — the chapter's most important discrimination — inside a section whose other half is arithmetic.

   **Recommendation: make one edit in shipped text** — `chapter-02` line 807, `*[cross-bearing: see Ch 7 §3 — node selection, tolerations, and accounting for overhead]*` → `*[cross-bearing: see Ch 7 — node selection, tolerations, and accounting for overhead]*`. Dropping the section number converts a partially-wrong pointer into a correct one, changes no words, and matches the two other Chapter 7 pointers (`chapter-03` line 417 and `chapter-04` line 688), both of which are already unnumbered. This is a smaller intervention than Chapter 6 required and it is mechanical.

   **Alternative considered and rejected:** merging §3 and §4 into one "constraining placement" section to honor the pointer literally. Rejected because it would produce the chapter's longest section, carry two figures, and — the real cost — bury the direction-of-assertion contrast that is the material's central idea inside a section that is *about* four mechanisms rather than *about* two directions.

2. **⚠ BLOCKING (research) — topology spread constraints have zero cached coverage.** B1 flagged this inside G4 and the flag is still live. Both G4 fetches landed on 2026-08-23 and between them close `nodeSelector`, node affinity (required and preferred, operators, `IgnoredDuringExecution`), inter-Pod affinity and anti-affinity, `nodeName`, taints, all three effects, `tolerationSeconds`, and the matching rules. **What did not land is the topology-spread page.**

   | Gap | Page | Blocks | Severity |
   |---|---|---|---|
   | **Topology spread constraints** | `kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/` | §5's closing block; possibly one Practice item | **Blocking for that block only.** The concept is named in the arc outline's Covers list, so it cannot simply be dropped without a scope decision |
   | **Large-cluster performance caveat on inter-Pod rules** | same page family | §5's closing note | Secondary. Cut if unsourced |

   **Recommendation: fetch the page.** It is a single routine fetch and it also carries the performance caveat. **If it does not land before drafting**, §5 must name topology spread constraints as existing, state in one sentence that they are the purpose-built mechanism for even distribution across domains (which is inferable from the arc outline's own framing and from the anti-affinity contrast), carry no field names, and the section must not claim more. Inventing `maxSkew`, `whenUnsatisfiable` or `topologyKey` semantics from memory is not an option — this is exactly the failure mode the cached-snapshot rule exists to prevent.

3. **Preemption and PriorityClass — in, out, or one clause?** Neither has a dedicated cached source. Preemption is mentioned twice in passing: `k8s-docs-daemonset-2026-08-24.md` (*"the default scheduler may preempt (evict) some of the existing Pods based on the priority of the new Pod"*) and `k8s-docs-pod-qos-2026-08-24.md` (*"the kube-scheduler does not consider QoS class when selecting which Pods to preempt"*). That is enough to source the *existence* of preemption and nothing more.

   **Recommendation: one clause in §2, no more, and no PriorityClass mechanics.** The clause belongs where the reader learns that a Pod can be unschedulable: *there is one circumstance in which the scheduler makes room rather than waiting, and it is out of scope here.* Naming it prevents the reader from later thinking the chapter lied to them; teaching it means teaching priority classes, preemption policies and the eviction interaction, which is CKA-tier material with no cached source and no place in a 5-point associate chapter. If the author wants it in properly, `kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/` is the fetch — but I would not spend the section.

4. **Cordon, drain, and `node.kubernetes.io/unschedulable`.** Chapter 8 owns node lifecycle, and B2's rationale for that placement is sound. But `node.kubernetes.io/unschedulable:NoSchedule` is a built-in taint, it is in the cached DaemonSet source with its effect, and §4's built-in-taint block is where it naturally belongs.

   **Recommendation: name the taint in §4's built-in list, with no verbs and a forward cross-bearing to Ch 8.** The reader meets it as a member of a family, which is the cheapest way to install it; Chapter 8 then explains what puts it there and what `drain` additionally does. Naming the taint is not teaching node lifecycle. The specific thing to avoid is a sentence of the form "when you cordon a node…" — the moment `cordon` appears as a verb with an object, the section has taken Chapter 8's material.

5. **Scheduling Policies — currency risk.** The cached `k8s-docs-kube-scheduler-2026-08-23.md` snapshot presents Policies and Profiles as *"two supported ways to configure the filtering and scoring behavior."* In current upstream Kubernetes the Policy model has been removed, not merely deprecated, and the live page's framing differs. The snapshot is what the source-tagging rule binds us to, and re-fetching during a downstream audit is explicitly forbidden (style-decisions.md, Fact Accuracy, 2026-04-18).

   **Recommendation: teach the vocabulary mapping and not the configuration.** §6 should present Predicates and Priorities as *the older names for filtering and scoring* — a mapping the reader may meet in older material — rather than as a currently-supported configuration option they might choose. That framing is true under both the snapshot and current upstream, it is the only part of the material with exam value, and it does not require the outline to assert a currency claim the snapshot cannot support. **Flag for the fact-accuracy stage** so the framing is reviewed against the snapshot deliberately rather than by accident.

6. **Affinity depth ceiling — confirm.** §3 as planned teaches: node labels, the standard label set, `nodeSelector` as an AND of exact matches, node affinity's two `DuringScheduling…DuringExecution` forms, the six operators by name, and what `IgnoredDuringExecution` means. It does **not** teach `weight` values on preferred rules, `nodeAffinityPolicy`/`nodeTaintsPolicy`, multiple `nodeSelectorTerms` OR-vs-AND semantics, or YAML at any length.

   **Recommendation: hold that ceiling.** KCNA is a comprehension exam — name the components, describe the two-step flow, distinguish the mechanisms. The weight arithmetic is CKA/CKAD material. If the author wants one concession, the `nodeSelectorTerms`-are-ORed / `matchExpressions`-are-ANDed rule is the single most useful piece of the omitted set, but it needs a source line the current snapshot does not contain.

   **Related: the `complexity` frontmatter value.** The arc outline calls this chapter procedural; the frontmatter says `mixed`. The spine is procedural and §3–§5 are not — they are four vocabularies the reader must discriminate between, which is comprehension work rather than procedure. `mixed` is the honest value and it matches what Chapter 6 declared for comparable material. **Recommendation: accept `mixed`**, and note that this is a frontmatter refinement rather than a departure from the arc's depth band, which stays `standard`.

7. **Seven sections against Chapters 5 and 6's nine — confirm, or split.** Two split options exist: §4 into taints-and-effects plus matching-rules (the section is the chapter's densest), and §6 into `nodeName` plus scheduler-configuration (two different altitudes). **Recommendation: keep seven.** §4's matching rules are already isolated as a Dead Reckoning block, which gives the reader the visual break a section split would give them at lower cost, and the two halves genuinely are one topic. §6's two halves share a frame — *not letting the scheduler decide* — and splitting them would produce two sections of three facts each, which reads as padding. Seven sections for five points is proportionate against Chapter 6's nine for six.

8. **Node `allocatable` versus `capacity` — Chapter 7 or Chapter 8?** The distinction is sourced in `k8s-docs-nodes-2026-08-23.md`, which is primarily a Chapter 8 source. It matters here because "available resources" in the `PodFitsResources` description is measured against allocatable, not capacity, and a reader who does the arithmetic with capacity will get an answer that does not match reality.

   **Recommendation: one or two sentences in §2, naming both words and the relationship, with the reservation model itself left to Chapter 8.** The reader needs to know the number they should be doing arithmetic against. They do not need to know what the kubelet reserves or how it is configured.

9. **Domain weight disclosure.** `domain_weight_pct: 5` is authored judgment, not published data — CNCF publishes four domain weights and twelve named competencies with no sub-weights (B1 §G33, §G36). The front matter already carries the disclosure. **No action needed**; recorded here so the drafting stage does not present 5% as an official figure in the chapter's metadata line. Match whatever phrasing Chapters 2–6 already published.

10. **Command forms are not in the cached snapshots.** The chapter's `kb_tags.commands` list is deliberately short — `kubectl get nodes`, `kubectl get pods`, `kubectl label`, `kubectl taint` — and **none of the four appear with their argument syntax in any cached source.** `k8s-docs-kubectl-overview-2026-08-23.md` covers the verb-resource grammar generally but not these specific invocations; the taints page snapshot omits the `kubectl taint nodes node1 key1=value1:NoSchedule` example that the live page carries.

    **Recommendation: use command *names* freely and command *lines* not at all**, unless a fetch supplies them. "You can taint a node with `kubectl taint`" is sourced by the general grammar; "run `kubectl taint nodes node1 dedicated=gpu:NoSchedule`" is not. This chapter can teach everything it needs to teach without a single full command line, and Chapter 8 owns the command surface anyway — which makes restraint here both correct and cheap. If the author wants worked command lines, the taints page needs re-fetching at full depth.

11. **⚠ Chapter 6's shipped file is incomplete, and three of this chapter's back-bearings depend on it.** `chapter-06-fleets-not-vessels.md` currently contains only Practice Questions, Chapter Summary and The Voyage Ahead — roughly the last 30% — and the pipeline-state notes on the ch-06 harvest record a known extraction fault (overlapping `<details>` snapshot regions, triplicated tail) plus an unresolved 19-vs-21 question count. The Voyage Ahead *is* present and is quotable, so §1's opening beat and §4's DaemonSet callback are safe. **What is not verifiable from shipped text is Chapter 6's final section numbering**, and this outline back-bears to Ch 6 §1 and Ch 6 §7.

    **Recommendation: treat the ch-06 outline's planned numbering as authoritative for now** (§1 The Resource That Holds the Intent, §7 One Per Node and Work That Ends — both of which this chapter's pointers match), **and re-verify before Chapter 7 drafts.** If Chapter 6's harvest is re-run and its sections renumber, two pointers in this outline need updating. This is a pipeline-state issue rather than a content decision, but it is the kind of thing that silently produces a broken cross-bearing three chapters later.

12. **Heading-form inconsistency across shipped chapters.** Chapters 2 and 3 ship `## §1 — ⚪ Title`; Chapters 5 and 6 ship `## ⚪ §1 — Title`. Both parse and neither violates the structural contract, but they are visibly different in a table of contents. This outline specifies the Chapter 5/6 form.

    **Recommendation: hold the Chapter 5/6 form here and schedule a reconciliation sweep for the whole book at the Stage-B6 reconciliation pass**, rather than fixing Chapters 2 and 3 from inside Chapter 7. Two chapters is a small sweep and doing it once, deliberately, beats doing it per-chapter by drift.

13. **Confirm what Chapter 7 does *not* touch.** `cordon`, `drain`, `uncordon`, node conditions, leases, `ResourceQuota`, `LimitRange`, version skew, the `kubectl` command surface, the three API access gates (Ch 8); Services, EndpointSlice, kube-proxy (Ch 9); NetworkPolicy (Ch 10); PersistentVolume, PVC, StorageClass, access modes, storage topology (Ch 11); RBAC, ServiceAccounts, Pod Security Standards, `securityContext` (Ch 12); diagnosing a Pending Pod, `kubectl describe`, events, OOMKilled, Evicted, `kubectl top`, metrics-server (Ch 13); Helm (Ch 14); GitOps and Argo CD (Ch 15); Cluster Autoscaler, Karpenter, VPA, KEDA, scale-to-zero, the four-socket extension synthesis, service mesh (Ch 17); observability and the golden signals (Ch 18). **Recommendation: hold all of these out.** Three are places where one extra paragraph would feel natural and would cost a later chapter its setup: the Pending diagnosis (Ch 13's first failure signature and **[B3]**'s primary decay fix for this chapter), Cluster Autoscaler (**[B3]**'s second decay fix), and the extension-point collection (Ch 17's secondary Zenith). Those three are not optional restraint — they are load-bearing for the book's retrieval schedule.
```

**Summary of what this stage produced and the three things that need your attention:**

1. **One editorial fix in shipped text.** `chapter-02` line 807 points at `Ch 7 §3` for three topics — node selection, tolerations, and Pod overhead — that land in §3, §4 and §2 respectively. Recommended fix is to drop the `§3` (a one-token edit), which matches the two other unnumbered Chapter 7 pointers. The `chapter-05` §2 pin is honored exactly.

2. **One live research gap.** B1's G4 is 90% closed — the two scheduling fetches on 2026-08-23 cover `nodeSelector`, node affinity, inter-Pod rules, `nodeName`, taints, all three effects and the matching rules. **Topology spread constraints have zero cached coverage** and are named in the arc outline's Covers list. One routine fetch closes it; the fallback (name it, one sentence, no field names) is specified in §5 if it doesn't land.

3. **A pipeline-state issue worth knowing about.** `chapter-06-fleets-not-vessels.md` currently holds only its last ~30% — the ch-06 notes record a harvester extraction fault. The Voyage Ahead survived and is quotable, so this chapter's opening beat is safe, but Chapter 6's final section numbering isn't verifiable from shipped text and two back-bearings here depend on it.