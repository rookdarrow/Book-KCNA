---
chapter: 5
chapter_type: "content"
title: "The Smallest Vessel"
subtitle: "A Pod is not a container, and that distinction is worth points"
exam_domain: "Kubernetes Fundamentals (competency: Kubernetes Core Concepts)"
domain_weight_pct: 7
complexity: "mixed"
novelty: "moderate"
prereq_factor: "standard"

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band for this chapter:
#-- "substantial" - 7 points, and requests/limits introduced here feed four
#-- later chapters. Planning signal only, NOT a target.
#--
#-- WARNING SECTION NUMBERING IS LOAD-BEARING AND ALREADY PUBLISHED. Three
#-- shipped chapters name sections of this chapter by number:
#--   chapter-02 line 318 -> *[cross-bearing: see Ch 5 §1 - the Pod as the unit of scheduling]*
#--   chapter-02 line 783 -> *[cross-bearing: see Ch 5 §5 - Pod phases and container states]*
#--   chapter-04 line 531 -> *[cross-bearing: see Ch 5 §6 - a Pod's identity]*
#-- §1, §5 and §6 below honor those exactly. The §6 placement is the one
#-- constraint that shaped this plan most; see § Open questions #1 for why
#-- it turns out to be defensible rather than merely tolerated.
#-- Do not renumber without editing all three published chapters.
#--
#-- chapter-03 line 447 carries an UNNUMBERED cross-bearing to this chapter
#-- ("Pods, PodSpecs, and what 'running and healthy' means precisely").
#-- That is a debt with two halves: §1 owes the PodSpec, §7 owes "healthy".
sections:
  - name: "The Pod as the Unit of Scheduling"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch05-fig01-pod-shared-network-namespace"
    checkpoint_after: false
  - name: "More Than One Container Aboard"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Everything That Must Happen First"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch05-fig03-init-containers-sequence"
    checkpoint_after: true
  - name: "Scheduled Once, Replaced Never"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Pod Phases and Container States"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch05-fig02-pod-phases-and-container-states"
    checkpoint_after: true
  - name: "A Pod's Identity"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Three Probes, Three Jobs"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch05-fig04-three-probes-compared"
    checkpoint_after: false
  - name: "What a Pod Is Owed"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch05-fig05-requests-limits-qos-classes"
    checkpoint_after: true
  - name: "The Smallest Deployable Unit"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch05-zenith-smallest-deployable-unit"
    checkpoint_after: false

#-- Nine sections - the most of any chapter so far. Driven by the pinned
#-- numbering (see frontmatter warning) plus a genuine five-arc load.
#-- §2, §4 and §6 are deliberately short; see § Open questions #6.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "what a process actually needs before another process can reach it over the network"
    - "two programs on one machine that must share a filesystem path - how do you arrange that"
    - "a startup that must not begin serving until a migration has finished"
    - "the difference between 'the process is alive' and 'the process can do its job'"
    - "what a load balancer does with a backend that stops answering health checks"
    - "reserving capacity versus capping consumption, in any system the reader already knows"
    - "retrieval from Ch 4 - which half of an object reports what is actually true"
    - "retrieval from Ch 2 - a container cannot start because the image would not pull; where does that show up"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 21 = 39. Bearings raised 10 -> 15 across 3
#-- checkpoints (5 + 5 + 5); see § "Taking Your Bearings checkpoints" for
#-- justification and B4's standing sanction ("minimums are minimums").
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 21
  total_this_chapter: 44

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D1.1"]
  concepts:
    - "pod"
    - "smallest-deployable-unit"
    - "co-located-co-scheduled"
    - "pod-shared-context"
    - "pod-network-namespace"
    - "pod-ip"
    - "localhost-communication"
    - "pod-shared-volumes"
    - "podspec"
    - "pod-template"
    - "single-container-pod"
    - "multi-container-pod"
    - "sidecar-container"
    - "init-container"
    - "init-container-ordering"
    - "run-to-completion"
    - "pod-lifetime"
    - "pod-ephemerality"
    - "pod-uid"
    - "scheduled-once"
    - "pod-replacement"
    - "pod-eviction"
    - "pod-termination"
    - "pod-phase"
    - "phase-pending"
    - "phase-running"
    - "phase-succeeded"
    - "phase-failed"
    - "phase-unknown"
    - "container-state"
    - "state-waiting"
    - "state-running"
    - "state-terminated"
    - "restart-policy"
    - "restart-backoff"
    - "backoff-reset"
    - "serviceaccount"
    - "default-serviceaccount"
    - "serviceaccount-name"
    - "tokenrequest"
    - "projected-token-volume"
    - "workload-identity"
    - "probe"
    - "liveness-probe"
    - "readiness-probe"
    - "startup-probe"
    - "probe-exec"
    - "probe-httpget"
    - "probe-tcpsocket"
    - "probe-grpc"
    - "probe-parameters"
    - "resource-request"
    - "resource-limit"
    - "cpu-unit"
    - "millicpu"
    - "memory-units"
    - "cpu-throttling"
    - "oom-kill"
    - "ephemeral-storage"
    - "hugepages"
    - "extended-resources"
    - "qos-class"
    - "qos-guaranteed"
    - "qos-burstable"
    - "qos-besteffort"
  commands:
    - "kubectl-get"
    - "kubectl-describe"
    - "kubectl-explain"

figures_planned:
  - "ch05-fig01-pod-shared-network-namespace"
  - "ch05-fig02-pod-phases-and-container-states"
  - "ch05-fig03-init-containers-sequence"
  - "ch05-fig04-three-probes-compared"
  - "ch05-fig05-requests-limits-qos-classes"
  - "ch05-zenith-smallest-deployable-unit"
---

# Chapter 5 Outline — The Smallest Vessel

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 5: The Smallest Vessel` | required | top |
| `## *"A Pod is not a container, and that distinction is worth points"*` | required | line 2 |
| Metadata line (weight / complexity / novelty) | required | after subtitle |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings` ×3 | **required, min 2** | after §3, §5, §8 |
| `★ Fixed Point` ×5 | **required, min 1** | §1, §3, §5, §7, §8 |
| `**Dead Reckoning:**` ×1 min | **required** | §5 (phase and state, plainly, without the vessel register) |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §5 (phase-vs-state, and "Running" oversold), §8 (`m` versus `M`) |
| `☀️ Zenith` | expected | §9 |
| `## Exam Alert` | **required** | after §9 |
| `## Practice Questions` | **required** | 21 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19 |
| `🏆 Safe Harbor` | expected | chapter close |

**Zenith:** exactly one, per Part 18.10. `ch05-zenith-smallest-deployable-unit` in §9. This chapter carries five concept diagrams — the same count as Chapter 4, at the upper end of the 2–8 band. None of the five may be dressed as a second Zenith, and `ch05-fig05` in particular will be tempting to inflate because it is the figure four later chapters retrieve. Resist; its job is reference, not revelation.

**Attention Budget guidance for drafting.** Six distinct costs:

| Section | Cost | Why |
|---|---|---|
| §1 | medium | One reframe, one figure, and a piece of vocabulary that overwrites a word the reader already thinks they own |
| §2 | low | Short. Two coupling mechanisms and one anti-pattern |
| §3 | medium | Ordering semantics plus a failure mode |
| §4 | low | Mostly consequence-drawing from §1 and Ch 4's Voyage Ahead |
| §5 | **high** | Two vocabularies of five and three words, a Pod-level field readers assume is per-container, and a backoff schedule. The densest recall block in the chapter |
| §6 | low | A plant, deliberately |
| §7 | medium-high | Three probes × four mechanisms × failure behaviors; the discrimination is the work |
| §8 | **high** | Two enforcement mechanisms that behave differently, two unit systems, and a three-class taxonomy |
| §9 | low | Synthesis |

*"If you only have 15 minutes"* should point at **§5 plus Bearings #2**. Phase-versus-state is the single highest-leverage distinction in the chapter and Chapter 13 is built directly on top of it.

**Recommended split point** for the two-session reader: after Bearings #2 (end of §5). That is the natural seam — §1–§5 are *what a Pod is and what it does*; §6–§8 are *what the kubelet does for it*.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 5 — The Smallest Vessel". Carried forward without modification:

- **Covers**: **D1.1** — the Pod concept and shared network namespace; multi-container and init containers; Pod phases; container states; `restartPolicy`; restart backoff; liveness/readiness/startup probes and probe mechanisms; resource requests and limits; QoS classes; ServiceAccount as Pod identity (planted).
- **Prerequisites**: Ch 2 (containers, images), Ch 4 (object anatomy, labels).
- **Retrieval targets**: **20%** **[B3]** — from Ch 2–4. Named anchors: `imagePullPolicy` (Ch 2) as a cause of a container state; `spec`/`status` (Ch 4) read against Pod phase; labels (Ch 4) on a Pod.
- **Question budget**: 8 Soundings · 10 Bearings · 21 Practice · 39 total. Bearings raised to 15 below.
- **Figures**: six anchors, listed verbatim in `figures_planned`.
- **Depth band**: substantial.
- **Blocking gaps**: G3 (requests, limits, QoS classes) and G7 (ServiceAccounts). **Status: G7 is closed; G3 is half-open.** See § Open questions #2.

### Three debts falling due in this chapter

Chapters 2, 3 and 4 all deferred material here by name. Draft knowing the reader was told to expect each one.

| Owed by | Promise made | Paid in |
|---|---|---|
| **Ch 2 §1** (line 318) | *"Containers are not the unit Kubernetes schedules. Something wraps them."* Plus: the Pod "comes with a shared network namespace and a lifecycle of its own" | **§1** — the wrapper, named, with the shared namespace as the *reason* rather than a feature |
| **Ch 2 §6** (line 783) | `ImagePullBackOff` is reported as a container in the **Waiting** state, and "container states are Chapter 5's material" | **§5** — the state vocabulary, with `ImagePullBackOff` as its worked example. The *diagnosis* stays Chapter 13's |
| **Ch 3 §5** (line 447) | The kubelet "ensures containers described in PodSpecs are running and healthy" — Ch 5 gives the PodSpec its proper treatment and says what "running and healthy" means precisely | **§1** (the PodSpec) and **§7** (health, which turns out to be three different questions, not one) |
| **Ch 4 §4** (line 531) | The `kubernetes.io/service-account-token` Secret type is named and left alone; "the identity model those tokens belong to… is Chapter 5's introduction and Chapter 12's full treatment" | **§6** — introduction only, at the altitude Ch 4 promised |
| **Ch 4 Voyage Ahead** (lines 1186–1192) | A Pod's `status` has a **phase**; a Pod is never rescheduled but *replaced* with a different UID; *"Chapter 5 introduces the disposable thing"* | **§4** (disposability, UID) and **§5** (phase) |

The Ch 4 Voyage Ahead is unusually specific — it names `phase`, names the UID behavior, and even cites the sources. That is a gift and a constraint. §4 and §5 must land as *the promised material arriving*, not as a re-argument. One clause of acknowledgment each; a callback that restates its own setup has started admiring itself.

### What this chapter owes forward

This is the highest forward-debt chapter in Part II. Two of the book's nine cross-cutting themes originate here, and one figure is retrieved in four later chapters.

| Concept | Retrieved at | Contract |
|---|---|---|
| **Requests and limits** (theme 8) | Ch 7 (**named anchor** — requests as the scheduler's filter input), Ch 13 (**named anchor** — OOMKilled and Evicted), Ch 17 (autoscaling targets), Ch 18 (the numbers metrics report against) | `ch05-fig05` is the artifact all four retrieve. Design it as a reference table that survives four re-presentations, not as a one-time explainer |
| **Identity** (theme 7) | Ch 12 (**named anchor** — ServiceAccount collected from its planting, as an RBAC subject), Ch 15 (the delivery agent's identity) | §6 plants; Ch 12 harvests. **Do not pre-empt Ch 12** — see § Open questions #4 for the exact boundary |
| **Pod shared network namespace** | Ch 9 (**≥4-back floor item, mandatory** — exactly four chapters back) | `ch05-fig01` must still be legible when Ch 9 refers back to it. Ch 9's whole Service argument rests on "the Pod has one IP" |
| **Pod phases and container states** | Ch 13 (**named anchor**), Ch 16 (**named anchor** — application-side triage) | The chapter's most load-bearing output. Ch 13's method *is* "read the phase before you read the logs" |
| **Probes** | Ch 6 (what makes a rolling update safe — **named anchor**), Ch 9 (readiness → EndpointSlice membership), Ch 18 (**named anchor** — probes are health-checking and are *not* observability) | Readiness's Service-endpoint consequence is a forward plant that Ch 9 collects; state it in §7 and do not develop it |
| **Pod volumes** | Ch 11 (**≥4-back floor item** — as volume types) | §1 names shared storage as part of the Pod's shared context and stops. Volume *types* are Ch 11's |
| **Pod ephemerality / replacement** | Ch 6 (why a controller must exist), Ch 11 (why StatefulSet identity is different) | §4 is the setup for Chapter 6's entire premise |

**Scope boundary with Chapter 13 — state it once and hold it.** Chapter 5 owns the *vocabulary*: what a phase is, what a container state is, what `ImagePullBackOff` and `CrashLoopBackOff` are called and what they mean. Chapter 13 owns the *method*: which command to run, which events to read, what to do next. If a paragraph in §5 begins recommending a diagnostic sequence, it belongs in Chapter 13. The reciprocal cross-bearing pair is already half-built — Ch 2 line 783 points diagnosis at Ch 13 explicitly, so the boundary is published and the reader will notice if this chapter crosses it.

**Scope boundary with Chapter 6.** Chapter 5 says *a Pod is disposable and something else must replace it*, names that something as a workload resource, and stops. Deployment, ReplicaSet, and the Pod template are Chapter 6's, and Chapter 4 already published the forward cross-bearing to Ch 6 §1 for them.

**Reader positioning**: Communications Officer role family, **junior tier**. Single unified brand voice; only atmospheric register and reader rank differ.

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**The curiosity gap: the reader already knows this word, and they are about to find out they know it wrong.** Every reader arriving here has run a container. Many have run a hundred. The word "Pod" has been in front of them since Chapter 2 with an explicit IOU attached, and the natural assumption — Pod is Kubernetes' word for container — is wrong in a way that quietly corrupts everything downstream. It is wrong about IP addresses, wrong about what a Service selects, wrong about what `restartPolicy` applies to, and wrong about what a phase describes. Open the gap on the asymmetry the subtitle states: the distinction is not pedantry, it is the load-bearing wall. Keep it open through §1–§8 and close it at §9, where the whole chapter turns out to be consequences of one design decision.

**The identity frame is diagnosis, not configuration.** Chapters 3 and 4 gave the reader a system to look at and something to write. Chapter 5 gives them the first thing they will ever *read under pressure*. Practitioners do not look up Pod phases when things are going well; they look at them at the moment something has stopped working, and the reason experienced operators are fast in that moment is not that they know more commands — it is that they know which of two vocabularies they are looking at and what each one can and cannot tell them. That is the shift this chapter delivers: from someone who describes infrastructure to someone who can read what infrastructure is telling them. Say it in the practitioner's register, not the exam's.

**The stakes are structural, and honest about the number.** Seven points on this book's authored judgment — CNCF publishes no sub-competency weights, and the front matter says so (see § Open questions #9). But the count understates it, because this is the chapter four later chapters retrieve by name. Requests and limits show up again in scheduling, in troubleshooting, in autoscaling, and in metrics. Phase versus container state *is* Chapter 13's method. The shared network namespace is the premise of Chapter 9. A reader who leaves this chapter able to recite five phase names but unable to say why the Pod has an IP and the container does not will re-learn this chapter four times in worse conditions. State that calmly, once. No manufactured urgency — Part 14 forbids it, and this reader is an adult professional who will notice.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Six outcomes, active verbs:

- **Explain** why Kubernetes schedules Pods rather than containers, and name the two things every container in a Pod shares.
- **Distinguish** a Pod's phase from a container's state — and say which one a crash-looping application is reported under.
- **Predict** what happens when each of the three probes fails, and which one silently takes a Pod out of service without restarting anything.
- **Choose** between a request and a limit for a given requirement, and say which component acts on each.
- **Trace** a Pod from creation through failure to replacement, and explain why "rescheduled" is the wrong word for what happens.
- **Identify** what a Pod is to the API server when it has been given no identity at all (it has one anyway).

*You'll also stop saying "container" when you mean "Pod," which is a smaller change than it sounds and fixes about a third of the mistakes people make on this exam.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Chapter 5's prerequisite set is Chapter 2 (containers, images, `imagePullPolicy`) and Chapter 4 (object anatomy, `spec`/`status`, labels), plus general operational literacy. **Six questions test priors the reader arrives with; two are deliberate retrieval from Chapters 2 and 4.** **[B3]** Soundings sit outside the retrieval budget but do retrieval work anyway, sourced from B2's Prerequisites column.

**Fixed Points this chapter teaches, which Soundings must therefore not reveal:**

1. The Pod — not the container — is the unit of scheduling, and it holds one IP shared by all its containers.
2. Pod phase and container state are two different vocabularies at two different scopes.
3. Liveness failure restarts; readiness failure de-registers without restarting; a startup probe suppresses both until it succeeds.
4. Requests are what the scheduler reads; limits are what the kubelet and kernel enforce — and CPU and memory limits are enforced by completely different mechanisms.

Each question below is checked against that list.

| # | Question topic | What it tests | Spoiler check |
|---|---|---|---|
| 1 | Two processes need to talk to each other over the network. What is the minimum they each need — and what changes if they happen to be on the same machine? | The networking prior, in its general form. Sets up "shared namespace" as an answer to a question the reader has already asked | Names nothing Kubernetes-specific. §1's teaching is that Kubernetes *chose* to give the shared namespace to a group of containers and made that group the schedulable unit. A general networking prior spoils none of it |
| 2 | Two programs must read and write the same directory. Outside Kubernetes, how do you arrange that? | The shared-storage prior | §1 names shared volumes as part of the Pod's shared context; §2 uses it as one of the two coupling mechanisms. Volume *types* are Chapter 11's and are not touched here |
| 3 | A service must not start accepting traffic until a database migration has completed. How would you enforce that ordering with the tools you have used before? | The init-container prior, by analogy to entrypoint scripts, systemd ordering, or CI job dependencies | §3 teaches Kubernetes' specific answer — a separate ordered container that must exit successfully — plus its failure behavior. The general instinct is the ramp, not the answer |
| 4 | "The process is running" and "the process can do its job" — describe a situation where the first is true and the second is false. | **The chapter's most valuable pre-test.** It surfaces the liveness/readiness distinction as a *problem* before §7 gives it as a *solution* | Never mentions probes. This is the pretesting effect working as Richland describes: the reader notices the gap, then §7 fills the exact gap they noticed. It reveals nothing about which probe does which |
| 5 | A load balancer health-checks its backends. One backend stops answering. What does the load balancer do — and, importantly, what does it *not* do? | The readiness prior, and specifically the "de-register without killing" behavior | The Fixed Point is that Kubernetes has *three* probes and that readiness is the one with this behavior. A reader with the load-balancer prior still learns all of that, and lands it faster |
| 6 | In any system you have capacity-planned — a JVM heap, a cgroup, a cloud instance type, a database connection pool — what is the difference between reserving capacity and capping it? | The requests/limits prior | §8's Fixed Points are *which component reads which*, that CPU capping is throttling and memory capping is killing, and the QoS classes that fall out. A reader who has the reserve-versus-cap instinct still learns every one of those |
| 7 | **Retrieval from Ch 4 §2** — an object has two nested fields. One you write; one the system maintains. Name both, and say which one reports what is actually true. | **[B3]**'s designated `spec`/`status` anchor, in its pre-test position | This is the anchor's setup, not its payoff. The Fixed Point is that a Pod's `status` carries a *phase* — a small closed vocabulary — and that phase is Pod-scoped while container state is not. Retrieving `spec`/`status` reveals neither. A reader who misses this gets a clear signal to re-read Ch 4 §2 before §5 |
| 8 | **Retrieval from Ch 2 §6** — a container will not start because its image could not be pulled. Chapter 2 gave this failure a name. What is it, and what did Chapter 2 say it would eventually be reported *as*? | **[B3]**'s `imagePullPolicy` anchor. Also a fairness check: Chapter 2 explicitly told the reader to bank this name | The published Ch 2 already states that `ImagePullBackOff` is reported as a container in **Waiting**. This question retrieves what the reader was *told*; §5 teaches the full three-state vocabulary and why Waiting is the state where "hasn't started yet" and "can't start" both live. Retrieving one instance does not give the taxonomy |

**Rubric**: standard 6+ / 3–5 / 0–2 per `branded-terms.yaml`. The 0–2 branch carries a specific instruction rather than a generic one: **if questions 7 and 8 were the misses, re-read Chapter 4 §2 and Chapter 2 §6 before starting §5** — those are the two published cross-bearings this chapter collects, and §5 will read as arbitrary vocabulary without them.

**Note for drafting:** questions 4, 5 and 6 are unusually strong pre-tests because each surfaces a *problem* the chapter later solves. Keep them phrased as situations, not definitions. A Soundings question that can be answered by reciting a term has stopped doing metacognitive work.

---

## 4. Section plan

Nine sections. **§1, §5 and §6 are pinned by published cross-bearings** (see the frontmatter warning). The ordering below is built around that constraint; see the note under §6 for why the pinned position turns out to be the right one on its own merits.

The chapter's shape, at a glance: **§1–§3 what a Pod is · §4–§5 what happens to it · §6–§8 what the kubelet does for it · §9 why all of it follows from one decision.**

### §1 — ⚪ The Pod as the Unit of Scheduling

**Pinned by `chapter-02` line 318.** The reframe, and the chapter's foundation. Three movements.

**First, the definition, taken at the documentation's own altitude:** a Pod represents a set of one or more running containers on your cluster, and it is the smallest thing you can ask Kubernetes to run. Containers in a Pod are co-located and co-scheduled to run on the same node — that phrase is already published in Chapter 2, so quote it back and then explain what it costs and buys.

**Second, and this is the section's real work: the shared context.** Each Pod gets its own unique cluster-wide IP address, and it has a private network namespace shared by all of the containers within it; processes in different containers in the same Pod communicate over `localhost`. Do not present this as a feature list. Present it as the *reason the wrapper exists*: if you want two containers to behave like two processes on one host, you have to give them one host's worth of shared context, and the network namespace is the irreducible part of that. Name shared storage as the second part of the shared context and stop — volume types are Chapter 11's.

**Third, the PodSpec**, paying Chapter 3's debt: everything Chapter 4 taught applies unchanged — four fields, a `spec` you write, a `status` you read — and the Pod's `spec` is what Chapter 3 called a PodSpec when it described the kubelet's job. One sentence, then move on; the reader does not need it developed, they need it *connected*.

Close on the trap, because it is the most efficient possible ending: each container in a Pod does **not** get its own IP. The Pod gets one, and all its containers share it.

- **Objectives**: D1.1
- **Concepts introduced**: `pod`, `smallest-deployable-unit`, `co-located-co-scheduled`, `pod-shared-context`, `pod-network-namespace`, `pod-ip`, `localhost-communication`, `pod-shared-volumes`, `podspec`
- **Sources**: `k8s-docs-workloads-2026-08-23.md` (a Pod represents a set of one or more running containers; workloads run inside a set of Pods). `k8s-docs-containers-2026-08-23.md` (containers in a Pod are co-located and co-scheduled; each node runs the containers forming the Pods assigned to it). `k8s-docs-network-model-2026-08-23.md` (unique cluster-wide IP; private network namespace shared by all containers; `localhost` between containers). ⚠ **The Pod concept page itself is not in the cached set** — see § Open questions #2. Everything above is sourceable today from secondary mentions, but §1 deserves the primary page
- **Figure**: `ch05-fig01-pod-shared-network-namespace`
- **Checkpoint after**: no
- **Markers planned**:
  - `★ **Fixed Point:**` — the Pod is the unit of scheduling; one IP per Pod, shared by every container in it, which talk to each other over `localhost`. **This is the chapter's most-retrieved Fixed Point** (Ch 9's ≥4-back floor item). Write it to be quotable four chapters later
  - `> 🪝 **Snag:**` — B1 trap #36, inline: "each container gets its own IP" is the single most common carry-over error from single-container Docker experience
- **Cross-bearings**: back to Ch 2 §1 (**mandatory — this is the pinned payoff**; the reader was told "something wraps them," so name the wrapper and acknowledge the promise in one clause); back to Ch 3 §5 (the kubelet and the PodSpec); back to Ch 4 §2 (four fields, unchanged); forward to Ch 9 (the Pod IP is why a Service has to exist); forward to Ch 11 (volume types)
- ⚠ **Do not teach the pause/infrastructure container.** It is an implementation detail, it is not in the cached sources, and it is below associate tier. The shared namespace is the fact; how the kubelet holds it open is not
- ⚠ **Do not develop shared storage here.** One clause naming it as part of the shared context. Chapter 11 owns volumes and Chapter 4 already published a forward pointer to it

### §2 — 🔵 More Than One Container Aboard

Short, and deliberately so. The documentation frames Pods as used in two main ways: **one container per Pod**, which is by far the most common case and the one the reader should default to; and **multiple tightly-coupled containers** that need to share resources — a main application container plus one or more helpers that consume or supplement it.

Two mechanisms and only two: the shared network namespace from §1 (they reach each other on `localhost`) and a shared volume. If a proposed multi-container Pod does not need either, it should be two Pods. Say that plainly, because it is the practical decision rule and the exam frames the same idea as "tightly coupled."

Name the **sidecar** pattern by name — the reader will meet the word constantly and will meet it again in Chapter 17 as the service mesh's data plane. Whether §2 teaches the *modern implementation* (a sidecar as an init container with `restartPolicy: Always`) is an open decision — see § Open questions #3.

Close on the anti-pattern, which is the section's Snag: a Pod is not a small VM. The instinct to put a web server, a database, and a cache in one Pod because they are "one application" is exactly what §1's co-scheduling guarantee makes possible and exactly what makes it a mistake — they scale together, fail together, and are replaced together whether or not that is what you wanted.

- **Objectives**: D1.1
- **Concepts introduced**: `single-container-pod`, `multi-container-pod`, `sidecar-container`
- **Sources**: `k8s-docs-workloads-2026-08-23.md`, `k8s-docs-network-model-2026-08-23.md` (`localhost` coupling), `k8s-docs-containers-2026-08-23.md` (co-location). ⚠ **The "two main ways" framing and the sidecar container page are not cached** — see § Open questions #2 and #3. Also `istio-service-mesh-2026-08-23.md` exists and documents sidecar mode, but it is Chapter 17's source and must not be pulled forward
- **Figure**: none. `ch05-fig01` already carries the shared-context claim and re-drawing it with two containers instead of one would be redundancy of exactly the kind Part 18.7 warns against
- **Checkpoint after**: no
- **Markers planned**:
  - `> 🪝 **Snag:**` — the Pod-as-VM anti-pattern
  - `> ⚓ **Worth Securing:**` — the decision rule, stated as a rule: *if they don't need `localhost` or a shared volume, they don't need to be one Pod*
- **Cross-bearings**: forward to Ch 17 (sidecar as the mesh data plane — one pointer, no development); forward to Ch 13 (a multi-container Pod's logs require naming the container, which is Chapter 13's problem, not this one)
- ⚠ **Do not teach mesh injection, ambient mode, or Envoy.** Chapter 17 owns all of it and B1 trap #102 lives there

### §3 — 🔵 Everything That Must Happen First

Init containers. The mechanics are simple and the semantics are what get tested.

Init containers run **before** the app containers, **in the order they are declared**, and each must **run to completion successfully** before the next starts. Only when all of them have succeeded does the kubelet start the app containers. That ordering guarantee is the entire point — it is the answer to Soundings Q3, and the reader should feel it click.

The failure behavior is the tested part: if an init container fails, the kubelet restarts it according to the Pod's `restartPolicy`, which means a Pod with a broken init container sits in `Pending` retrying rather than progressing — and a Pod whose `restartPolicy` is `Never` fails outright. Note that this is a forward-linked fact: §5 defines `restartPolicy` properly, so §3 states the dependency and §5 discharges it. That is deliberate and the draft should signal it rather than hide it.

Distinguish init containers from app containers on the one axis that matters: init containers must exit, app containers are expected to keep running. That single axis generates most of the differences, including why classic init containers do not carry the probes §7 is about.

- **Objectives**: D1.1
- **Concepts introduced**: `init-container`, `init-container-ordering`, `run-to-completion`
- **Sources**: ⚠ **Not cached. This section has no primary source today** — see § Open questions #2. `k8s-docs-pod-lifecycle-2026-08-23.md` supplies `restartPolicy` and backoff, which the failure behavior depends on, but the init-container page itself must be fetched
- **Figure**: `ch05-fig03-init-containers-sequence`
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `★ **Fixed Point:**` — init containers run in order, to completion, before any app container starts; if one fails, the Pod does not proceed
  - `> 🪢 **Mnemonic:**` — an ordering hook for *in order, to completion, all of them, then the app*. Keep it short; a mnemonic longer than the fact it encodes is a net loss
- **Cross-bearings**: forward to §5 (`restartPolicy`, which this section depends on and does not define); forward to Ch 16 (debugging init containers is explicitly named in D3.2 and is Chapter 16's, not this chapter's)
- ⚠ **Do not teach init-container resource accounting** (the effective-request maximum rule) unless the fetched source establishes it as associate-tier. It is a real rule and it is genuinely obscure; §8 is the only place it could go and §8 is already the chapter's densest section. Default: omit, flag in § Open questions

### §4 — ⚪ Scheduled Once, Replaced Never

Short, and it is mostly consequence-drawing — Chapter 4's Voyage Ahead already stated the facts and cited the sources, so this section's job is to make them *mean* something.

The lifetime, in order: a Pod is created, assigned a unique **UID**, and scheduled once in its lifetime to a specific node, where it remains until termination or deletion. It is never rescheduled to a different node. If the node dies, the Pod is not moved — it is marked for deletion after a timeout and **replaced** by a new, near-identical Pod with a different UID. Pods do not survive evictions due to lack of resources or node maintenance.

Then the consequence, which is the section's reason for existing and Chapter 6's premise: if the thing that runs your application is designed to be replaced rather than repaired, then *something else has to be holding the intent that survives it*. Name that something as a workload resource, point at Chapter 6, and stop.

Close by connecting disposability back to Chapter 2's immutability. Same instinct, one level up: you do not repair a running container, you build a new image; you do not repair a failed Pod, you get a new Pod. That parallel is real, it is worth one sentence, and it is one of the chapter's retrieval items.

- **Objectives**: D1.1
- **Concepts introduced**: `pod-lifetime`, `pod-ephemerality`, `pod-uid`, `scheduled-once`, `pod-replacement`, `pod-eviction`, `pod-termination`
- **Sources**: `k8s-docs-pod-lifecycle-2026-08-23.md` (scheduled once; ephemeral rather than durable; never rescheduled; replaced with a different UID; node death and the deletion timeout; no survival of evictions; higher-level controllers create replacements). `k8s-docs-names-and-uids-2026-08-24.md` (UIDs distinguish historical occurrences of similar entities). `k8s-docs-containers-2026-08-23.md` (immutability, for the parallel)
- **Figure**: none. The lifetime is a sequence of four facts and prose carries it; a timeline diagram here would compete with `ch05-fig02` one section later for the same attention with less payoff
- **Checkpoint after**: no
- **Markers planned**:
  - `> 🪝 **Snag:**` — B1 trap #9: a failed Pod is not rescheduled onto a healthy node. "Rescheduled" is the wrong word for what happens and using it will lead the reader to the wrong answer
  - `> ⚓ **Worth Securing:**` — the UID point, which is genuinely useful in the field and not only on the exam: same name, different object, and the cluster knows the difference even when you don't
- **Cross-bearings**: back to Ch 4 §2 (UID as one of the identifying fields in `metadata` — **the tool was already handed over**, Ch 4's Voyage Ahead says so explicitly); back to Ch 2 (immutability, the same instinct one level up); forward to Ch 6 §1 (the resource that holds the surviving intent — note Ch 4 line 269 already published this pointer, so match its wording rather than inventing a second phrasing); forward to Ch 11 (StatefulSet identity is the exception that proves this rule)
- ⚠ **Graceful termination** (`terminationGracePeriodSeconds`, SIGTERM then SIGKILL, `preStop`) is not in the cached snapshot and is an open scope decision — see § Open questions #5

### §5 — 🔵 Pod Phases and Container States

**Pinned by `chapter-02` line 783.** The densest section in the chapter and the most load-bearing output of it. Three movements, and the order matters.

**First, phase.** The Pod's `status` carries a `phase` — Chapter 4's Voyage Ahead promised exactly this, so collect it in a clause. Five values, and each needs a precise gloss rather than a label: **Pending** (accepted by the cluster, but one or more containers not yet set up and running — and this explicitly includes both time spent waiting to be scheduled *and* time spent pulling images), **Running** (bound to a node, all containers created, at least one running or starting or restarting), **Succeeded** (all containers terminated successfully, none will restart), **Failed** (all terminated, at least one in failure, no automatic restart), **Unknown** (the state could not be obtained, typically a communication problem with the node).

**Second, container state.** Three values, per container: **Waiting** (still doing what it needs in order to start — pulling the image, applying Secret data — with a `Reason` field that summarizes why), **Running** (executing, with a `startedAt` timestamp), **Terminated** (ran to completion or failed, with a reason, an exit code, and timestamps).

**Third, the distinction, which is the whole point.** Phase is Pod-scoped; state is per-container. A Pod can report `Running` while one of its containers sits in `Waiting`. Two traps fall directly out of this and both must be called out explicitly: the phase/state confusion itself, and the fact that `Running` is oversold by its own name — the definition includes "or is in the process of starting or restarting," which means **a crash-looping Pod reports `Running`**. That second one is the single most consequential misreading in the chapter, and Chapter 13's entire method is built on the reader not having it.

Then `restartPolicy`, which belongs here because it is what turns a `Terminated` state into a new `Running` one. It is a **Pod-level** field with three values — `Always` (default), `OnFailure`, `Never` — and it applies to **all containers in the Pod**. It cannot be set per container. The kubelet restarts with exponential backoff: 10s, 20s, 40s, capped at five minutes; once a container has run 10 minutes without incident, the backoff timer resets.

Land `ImagePullBackOff` here as the worked example, because Chapter 2 promised it and because it is the cleanest possible demonstration of the phase/state split — the Pod is `Pending`, the container is `Waiting`, and the `Reason` is what tells you which. Then hand diagnosis to Chapter 13 and stop. Chapter 2 already published that boundary; honor it.

- **Objectives**: D1.1
- **Concepts introduced**: `pod-phase`, `phase-pending`, `phase-running`, `phase-succeeded`, `phase-failed`, `phase-unknown`, `container-state`, `state-waiting`, `state-running`, `state-terminated`, `restart-policy`, `restart-backoff`, `backoff-reset`
- **Sources**: `k8s-docs-pod-lifecycle-2026-08-23.md` (all five phases with their exact glosses; all three container states with their recorded fields; `restartPolicy` values, Pod-level scope, and the full backoff schedule including the 10-minute reset). `k8s-docs-images-2026-08-23.md` (`ImagePullBackOff` as a Waiting state, for the worked example and the retrieval item)
- **Figure**: `ch05-fig02-pod-phases-and-container-states`
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2** (carries 2 of the chapter's 3 Bearings retrieval items)
- **Markers planned**:
  - `**Dead Reckoning:**` — **the chapter's required facts-only block, and it belongs exactly here.** Five phases and three states, stated flat, no vessel register, no metaphor. This is reference material the reader will come back to under stress and the brand's own guidance says that is what Dead Reckoning is for
  - `★ **Fixed Point:**` — phase is Pod-scoped, state is per-container, and `Running` does not mean working
  - `⚠ **Navigational Hazards**` — the chapter's primary hazards block. B1 traps #6 (phase vs state), #7 (`Running` oversold), #8 (`restartPolicy` is not per-container). Three traps, one block, because they share a root cause: reading a Pod-level signal as a container-level one
  - `> 🔭 **Closer Look:**` — the backoff schedule and its reset, which is the kind of number that looks arbitrary until you see that it is a cap plus a forgiveness window
- **Cross-bearings**: back to Ch 2 §6 (**mandatory — pinned payoff**; `ImagePullBackOff` is a container in Waiting, exactly as promised); back to Ch 4 §2 (`status` is where phase lives, and you never write it); forward to Ch 13 §2 (diagnosis — Ch 2 already published this pointer; match it); forward to Ch 16 (application-scope triage)
- ⚠ **Hard boundary.** No diagnostic sequences, no `kubectl describe` walkthroughs, no event reading. Chapter 13 owns method. If the draft starts saying "first check X, then check Y," it has crossed the line
- ⚠ **`CrashLoopBackOff` may be named** — the reader will meet it and §5 is where the vocabulary lives — but it must be named as *a container Waiting with that reason*, not as a diagnostic procedure. One sentence

### §6 — ⚪ A Pod's Identity

**Pinned by `chapter-04` line 531.** Short by design. This is a **plant**, and the discipline is not to over-deliver it.

A ServiceAccount is a type of **non-human account** that provides a distinct identity in the cluster. Pods use one to identify themselves to the API server. Four facts and no more:

1. ServiceAccounts are **namespaced** objects, and every namespace gets one named `default` when it is created. (Chapter 4 taught namespaced-versus-cluster-scoped; this is that boundary doing work.)
2. If you deploy a Pod and do not assign it a ServiceAccount, **Kubernetes assigns the namespace's `default`** — so every Pod has an identity whether or not anyone chose one.
3. The `default` ServiceAccount gets **no permissions** beyond the API discovery permissions granted to all authenticated principals. Having an identity and being able to do anything with it are different questions.
4. You assign one via `spec.serviceAccountName`.

Then one sentence on credentials, because Chapter 4 named the Secret type and left it: since v1.22 the token is short-lived and automatically rotating, obtained through the TokenRequest API and mounted as a projected volume; the long-lived token Secret Chapter 4 listed is the legacy form. Name it, do not develop it.

Close by handing the rest to Chapter 12 explicitly. RBAC, what a ServiceAccount can be *granted*, token hardening, and the privilege-escalation path are all Chapter 12's, and Chapter 4 already told the reader that in as many words.

- **Objectives**: D1.1 (planted; full treatment is D2.2 in Ch 12)
- **Concepts introduced**: `serviceaccount`, `default-serviceaccount`, `serviceaccount-name`, `tokenrequest`, `projected-token-volume`, `workload-identity`
- **Sources**: `k8s-docs-service-accounts-2026-08-23.md` (non-human account; distinct identity; namespaced; `default` per namespace; automatic assignment; no permissions beyond API discovery; `spec.serviceAccountName`; TokenRequest and projected volume since v1.22; long-lived token Secrets not recommended). `k8s-docs-secret-2026-08-23.md` (the `kubernetes.io/service-account-token` type Chapter 4 named). **G7 is closed** — this section is fully sourced today
- **Figure**: none, deliberately. Four facts and a plant do not warrant a diagram, and Part 18.3 says a visual that does not earn germane load is a net cost
- **Checkpoint after**: no
- **Markers planned**:
  - `> ⚓ **Worth Securing:**` — "every Pod has an identity whether or not you gave it one" is the fact practitioners find genuinely surprising and it is the hook Chapter 12 pulls on
- **Cross-bearings**: back to Ch 4 §4 (**mandatory — pinned payoff**; the `service-account-token` type was named and deferred here, and this is the deferral being honored); back to Ch 4 §3 (namespaced scope, doing real work rather than being recited); forward to Ch 12 (**the harvest** — RBAC subjects, token hardening, trap #62); forward to Ch 15 (theme 7's third stop: the delivery agent's identity)
- ⚠ **Do not teach RBAC, Roles, bindings, or the four-way matrix.** Chapter 12 derives that matrix from Chapter 4's namespaced/cluster-scoped boundary — **[B3]** names this explicitly — and pre-empting it here would spend the derivation early and badly
- ⚠ **Do not teach `imagePullSecrets` here** even though the ServiceAccount source lists it as a use case. Chapter 4 §4 already owns it and closed Chapter 2's loop with it

**On the pinned position.** §6 sits between the lifecycle block (§5) and the health block (§7), which looks at first like an interruption. It reads better than it looks, for a reason worth stating in the draft: §5 ends with a Pod being destroyed and replaced by a different object with a different UID, which raises the question of what, if anything, persists about *who* a Pod is. §6 answers it — identity is not a property of the instance, it is a property of the declaration, and the replacement Pod has the same one. That is a genuine bridge rather than a seam. Draft it as one sentence of transition, not a paragraph.

### §7 — 🔵 Three Probes, Three Jobs

This is where Chapter 3's "running and healthy" gets its precise answer, and the answer is that "healthy" is three different questions.

Open with the definition: a probe is a diagnostic performed periodically by the kubelet on a container. Then the four **mechanisms**, which are orthogonal to the three types and should be taught first so they do not tangle with them: `exec` (run a command; success is exit status 0), `httpGet` (HTTP GET against the Pod's IP, port and path; success is status ≥200 and <400), `tcpSocket` (success if the port is open), `grpc` (a gRPC health check). Any type can use any mechanism.

Then the three **types**, and for each one the only thing that really matters — **what happens when it fails**:

- **liveness** — is the container running? On failure the kubelet **kills the container**, which is then subject to its restart policy. This is §5's `restartPolicy` doing visible work, which is why §5 comes first.
- **readiness** — can the container respond to requests? On failure the endpoints controller **removes the Pod's IP from the endpoints of every Service that matches it**. The container keeps running. Nothing is restarted. This is the behavior Soundings Q5 primed and it is the one people get wrong.
- **startup** — has the application started? While a startup probe is configured and has not yet succeeded, **all other probes are disabled**. On failure the kubelet kills the container and applies the restart policy.

Name the parameters as a set (`initialDelaySeconds`, `periodSeconds`, `timeoutSeconds`, `successThreshold`, `failureThreshold`) without tuning advice — the exam tests that they exist and roughly what they govern, not how to pick values.

Close on the discrimination the whole section exists for: liveness and readiness look similar and do opposite things. One restarts and does not remove from service; one removes from service and does not restart.

- **Objectives**: D1.1
- **Concepts introduced**: `probe`, `liveness-probe`, `readiness-probe`, `startup-probe`, `probe-exec`, `probe-httpget`, `probe-tcpsocket`, `probe-grpc`, `probe-parameters`
- **Sources**: `k8s-docs-pod-lifecycle-2026-08-23.md` (probe definition; all four mechanisms with their success criteria; all three types with their exact failure behaviors; the startup-probe suppression rule; the five parameters). Fully sourced today
- **Figure**: `ch05-fig04-three-probes-compared`
- **Checkpoint after**: no — Bearings #3 falls after §8 and covers §6–§8 together. See § "Taking Your Bearings checkpoints" for why
- **Markers planned**:
  - `★ **Fixed Point:**` — the three failure behaviors, in one place. This is the highest-density exam fact in the chapter after phase-versus-state
  - `> 🪝 **Snag:**` — B1 trap #11: a configured startup probe **disables** the other two until it succeeds. Readers consistently assume the three run in parallel from the start
  - `> 🪢 **Mnemonic:**` — optional, and only if a genuinely good one exists for *liveness restarts / readiness de-registers / startup suppresses*. A forced mnemonic here is worse than none; the failure behaviors are memorable on their own once contrasted
- **Cross-bearings**: back to Ch 3 §5 (**the unnumbered debt** — "running and healthy," now answered precisely); back to §5 (liveness failure feeds `restartPolicy`, which the reader already has); forward to Ch 9 (readiness and Service endpoints — **name the consequence, do not develop it**; EndpointSlice is Chapter 9's object); forward to Ch 6 (probes are what make a rolling update safe — **[B3]** named anchor, so plant it cleanly); forward to Ch 18 (**[B3]** named anchor: probes are health-checking and are *not* observability — do not pre-empt the distinction, just leave the hook)
- ⚠ **Do not teach EndpointSlice.** "Removed from the endpoints of matching Services" is the sourced phrasing and it is enough. Chapter 9 owns the object

### §8 — 🟡 What a Pod Is Owed

The chapter's second-densest section and the one with the longest forward reach. Four movements.

**First, the two words and who reads each — the section's core distinction.** A **request** is what the **kube-scheduler** reads to decide which node the Pod goes on, and the kubelet reserves at least that much of the resource for the container. A **limit** is what the **kubelet enforces** so the running container cannot exceed it. Crucially: if the node has spare capacity, a container is *allowed* to exceed its request. It is never allowed to exceed its limit. Requests are about placement; limits are about containment. Two components, two jobs.

**Second, and this is the part that gets tested: the two enforcement mechanisms are not the same.** CPU limits are enforced by **throttling** — the kernel restricts CPU access as the container approaches the limit, so a CPU limit is a hard limit that slows you down. Memory limits are enforced by **OOM kills** — the kernel may terminate a container that exceeds its memory limit, but *terminations only happen when the kernel detects memory pressure*, so memory limits are enforced **reactively** and an over-allocating container may not be killed immediately. Exceeding CPU makes you slow; exceeding memory makes you dead, eventually, unpredictably. That asymmetry explains a large fraction of real production behavior and it is worth the paragraph.

**Third, resource types and units.** Types: `cpu`, `memory`, `ephemeral-storage`, `hugepages-<size>`, plus extended resources exposed by device plugins. CPU units: 1 cpu unit equals one physical or virtual core; fractional values are allowed; `0.1` equals `100m` ("one hundred millicpu"); precision finer than `1m` is not permitted; and CPU is always **absolute, never relative** — `500m` is the same computing power on a 1-core node and a 48-core node. Memory units: plain integers or the suffixes `E`, `P`, `T`, `G`, `M`, `k` and their power-of-two forms `Ei`, `Pi`, `Ti`, `Gi`, `Mi`, `Ki`. Then the trap the documentation itself calls out: **`M` means megabytes and `m` means millibytes**, so `400m` of memory is a request for four-tenths of one byte.

**Fourth, QoS classes** — Guaranteed, Burstable, BestEffort — as what falls out of how you filled in the first two. ⚠ **This movement is currently unsourced; see § Open questions #2.** Do not draft it from memory.

Close with the forward reach, briefly and without listing chapters like a table of contents: these two numbers come back. They are what the scheduler filters on, what the system reports when a Pod is killed for using too much, what autoscalers compare against, and what monitoring measures utilization *relative to*. One sentence.

- **Objectives**: D1.1 (introduced here; applied under D1.3 in Ch 7 and D2.3 in Ch 13)
- **Concepts introduced**: `resource-request`, `resource-limit`, `cpu-unit`, `millicpu`, `memory-units`, `cpu-throttling`, `oom-kill`, `ephemeral-storage`, `hugepages`, `extended-resources`, `qos-class`, `qos-guaranteed`, `qos-burstable`, `qos-besteffort`
- **Sources**: `k8s-docs-resource-management-2026-08-23.md` (requests as scheduler input; kubelet reservation and enforcement; over-request allowed, over-limit not; CPU throttling as a hard kernel limit; memory OOM kill as reactive under pressure; all four resource types plus extended resources; full CPU and memory unit rules including the `m`/`M` warning). ⚠ **QoS classes are not in the cached set — G3 is half-open** — see § Open questions #2
- **Figure**: `ch05-fig05-requests-limits-qos-classes`. **Design note: this is the chapter's most reused artifact** — retrieved in Ch 7, Ch 13, Ch 17 and Ch 18. Build it as a durable reference, not a one-time explainer
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `★ **Fixed Point:**` — requests are what the scheduler reads; limits are what the kubelet enforces; CPU limits throttle and memory limits kill
  - `⚠ **Navigational Hazards**` — the `m`-versus-`M` memory suffix, which is documented in the source as an explicit warning and is the most mechanically checkable gotcha in the chapter
  - `> 🔭 **Closer Look:**` — CPU as an absolute quantity, and why that means a `500m` request is portable across node sizes in a way most capacity intuitions are not
- **Cross-bearings**: forward to Ch 7 (**[B3]** named anchor — requests as the scheduler's filter input; `PodFitsResources`); forward to Ch 13 (**[B3]** named anchor — OOMKilled and Evicted, diagnosed there, named here at most in passing); forward to Ch 17 (autoscaling reads these numbers); forward to Ch 18 (metrics report utilization against them)
- ⚠ **Do not teach `ResourceQuota` or `LimitRange`.** Both are Chapter 8's, both are cluster-administration concerns, and both are easy to slide into from here. §8 is about what one Pod asks for
- ⚠ **Do not diagnose `OOMKilled` or `Evicted`.** Chapter 13 owns them. §8 may explain the *mechanism* (memory limit exceeded under pressure) because that is what this section teaches; it may not explain what to do about it

### §9 — ☀️ The Smallest Deployable Unit

The Zenith. Synthesis, not new material — and the synthesis is genuinely available here rather than manufactured, which is what makes it worth the illustration.

Everything in this chapter is a consequence of one decision: **the unit of scheduling wraps containers instead of being one.** Walk the consequences the reader has just spent eight sections learning, and let them recognize each as something they already know:

- The Pod has an IP, not the container — because the shared network namespace is what the wrapper exists to provide (§1).
- Containers reach each other on `localhost` — same reason (§1, §2).
- `restartPolicy` is Pod-level and applies to all containers — because the Pod is the unit (§5).
- The phase is Pod-level while the state is per-container — because the Pod is the unit but the containers are what actually run (§5).
- Identity is per-Pod (§6).
- Services will select Pods, not containers — and Chapter 9 will need that (§1 → forward).
- Requests are declared per container, but scheduling happens per Pod — because the scheduler is placing the wrapper (§8).

Then the payoff sentence for the chapter's curiosity gap: the reader who came in thinking "Pod is Kubernetes' word for container" now has a list of seven things that would each be wrong under that assumption. The distinction was never pedantry.

Close by setting up Chapter 6 in the terms Chapter 4 already published — the disposable thing is now understood, and the thing that holds the intent is next.

- **Objectives**: D1.1
- **Concepts introduced**: none. Synthesis only
- **Sources**: no new tags. Every claim is a restatement of a sourced claim from §1–§8
- **Figure**: `ch05-zenith-smallest-deployable-unit`
- **Checkpoint after**: no
- **Markers planned**:
  - `☀️ **Zenith**` — the chapter's one Zenith
  - `🏆 **Safe Harbor**` — at the chapter close, after the Voyage Ahead
- **Cross-bearings**: forward to Ch 6 §1 (**match Ch 4's published phrasing** — "Chapter 5 introduces the disposable thing. Chapter 6 introduces what holds the intent"); forward to Ch 9 (Services select Pods)
- ⚠ **No new facts in the Zenith.** If the draft introduces anything here that was not established in §1–§8, it has turned the synthesis into a ninth content section and the "aha" will not land

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 15 questions total.** B4 allocates 10; this outline raises it to 15 on B4's own standing instruction that the 10 is *"a contract to exceed, not a target to hit."* B4 names Chapters 8, 12 and 17 as the likely candidates based on objective load; Chapter 5 was not on that list, and the case for adding it is the section count. Five distinct conceptual arcs — Pod anatomy (§1–§3), lifetime and status vocabulary (§4–§5), identity (§6), health (§7), resources (§8) — across nine sections, in four different cognitive modes: structural understanding, closed-vocabulary recall, behavioral prediction, and quantitative reasoning. Folding those into two checkpoints would put unrelated modes in one block and pay an alternating-attention cost for nothing (skill Part 4). Soundings stay at 8 and Practice stays at 21, so the chapter total moves 39 → 44 against a book carrying 715 questions against a 300 floor.

**Retrieval-practice content: 20%** **[B3]** — drawn from **Chapters 2, 3 and 4**. Chapter 1 is excluded from the retrieval schedule entirely and no item may test exam mechanics. Against a combined Bearings-plus-Practice pool of 36, the 20% target is ~7 items, allocated **3 in Bearings and 4 in Practice** (7 of 36 = 19.4%).

⚠ **Note a conflict for reconciliation.** B4's retrieval table (`length-budget.md` § "Retrieval-practice spacing") places Ch 4–5 at ~10% from Ch 2–3. B3, the arc outline's callback map, and the skill's own Part 10 table all place Ch 5 at **20% from Ch 2–4**. This outline follows 20%, which is both the later stage and the skill's default. See § Open questions #8.

Each of B3's three named anchors has exactly one section where it belongs:

| **[B3]** named anchor | Placement | Why here |
|---|---|---|
| **`imagePullPolicy` (Ch 2) as a cause of a container state** | Bearings #2, item 4 | §5 has just delivered the state vocabulary and used `ImagePullBackOff` as its worked example. The retrieval and the pinned Chapter 2 payoff are the same beat |
| **`spec`/`status` (Ch 4) read against Pod phase** | Bearings #2, item 5 | §5 is the first moment in the book where Chapter 4's abstraction has a concrete `status` sub-field to point at. The translation *is* the retrieval |
| **Labels (Ch 4) on a Pod** | Practice Questions, §1–§3 block | Better as a discriminator with distractors than as an open item, and it is doing setup work for Ch 6 and Ch 9 that a checkpoint item would spend too early |

### ☆ Taking Your Bearings #1 — after §3

- **Topic**: what a Pod is
- **Questions**: 5
- **Retrieval from earlier chapters**: 1 of 5 (20% of this checkpoint)
- **Difficulty**: mostly ⚪, with item 5 at 🔵

  1. Two containers in the same Pod. How many IP addresses are involved, and how do the two containers reach each other? **Tests §1's Fixed Point directly.** Trap answers must include "two IPs" (B1 #36) and "through a Service."
  2. You are asked to put a web server and its database in one Pod because they are "one application." Give the strongest argument against, in one sentence. **Correct answer turns on shared fate: they scale, fail, and get replaced together.**
  3. An init container exits with status 1. What does the Pod do next, and what has *not* happened yet? Tests ordering plus the failure dependency on `restartPolicy` that §5 will formalize.
  4. Three init containers are declared. Under what circumstances does the third one run? **Correct answer: only after the first two have each run to completion successfully.** Trap answers cover "in parallel" and "in any order."
  5. 🔵 **Retrieval from Ch 3 §5 — the kubelet.** Chapter 3 said the kubelet ensures the containers described in PodSpecs are running and healthy. Now that you know what a Pod is: what object is the kubelet reading, and what is it comparing it against? **This is the chapter's designated Chapter 3 retrieval and it deliberately closes the unnumbered cross-bearing at line 447.** It is the checkpoint's hardest item by design.

- **Answer-key requirement**: item 1 needs a full why-wrong treatment for the "two IPs" option. That misconception is load-bearing for Chapter 9 and this is the last cheap place to correct it.

### ☆ Taking Your Bearings #2 — after §5

- **Topic**: lifetime, phase, and state
- **Questions**: 5
- **Retrieval from earlier chapters**: 2 of 5 (40% of this checkpoint — deliberately front-loaded; see the note below)
- **Difficulty**: 🔵 throughout, with item 3 at 🟡

  1. A Pod reports phase `Running`. One of its containers is in `Waiting`. Is the Pod broken? **Correct answer: the two signals are at different scopes and both readings are legitimate; `Running` requires at least one container running, starting, or restarting.** Trap answers target B1 #6 and #7.
  2. `restartPolicy` is set on one container in a two-container Pod. What actually happens? **Correct answer: it cannot be — the field is Pod-level and applies to all containers** (B1 #8).
  3. 🟡 A container has been crash-looping for twenty minutes. Roughly how long is the kubelet now waiting between restart attempts, and what would reset it? Tests the backoff schedule and the 10-minute forgiveness window. **This is the chapter's designated struggle item** — label it as such per Part 10B and normalize the difficulty.
  4. **Retrieval from Ch 2 §6 — `imagePullPolicy` and `ImagePullBackOff`.** Chapter 2 told you to bank a name and said its state was this chapter's material. Give the phase, the container state, and the field on the container status that tells you which failure it is. **[B3]** named anchor, and the pinned Chapter 2 payoff appearing as an assessment item.
  5. **Retrieval from Ch 4 §2 — `spec` and `status`.** Which of the two carries `phase`, who writes it, and what would it mean if you tried to set it yourself? **[B3]** named anchor.

- **Note on the 40% concentration.** This checkpoint carries two of the chapter's three Bearings retrieval items because both **[B3]** anchors land in §5 and nowhere else — `imagePullPolicy` needs the container-state vocabulary and `spec`/`status` needs a concrete status sub-field. Spreading them to hit an even per-checkpoint distribution would place each one where it does not belong. The chapter's overall rate is 19.4%, which is the figure that matters.
- **Answer-key requirement**: item 1 needs why-wrong treatment for both trap options separately. They are two different misconceptions that happen to produce the same wrong answer, and Chapter 13 depends on the reader having neither.

### ☆ Taking Your Bearings #3 — after §8

- **Topic**: identity, health, and what a Pod is owed
- **Questions**: 5
- **Retrieval from earlier chapters**: 0. The chapter's 20% is met by Bearings #1 item 5, Bearings #2 items 4–5, and four Practice items; a fourth Bearings retrieval would push this checkpoint off its own topic
- **Difficulty**: 🔵, with item 5 at 🟡

  1. A Pod is created with no ServiceAccount specified. What identity does it have, and what can it do with it? **Two-part answer: the namespace's `default`, and essentially nothing — no permissions beyond API discovery.** Trap answers cover "none" and "cluster-admin."
  2. A liveness probe and a readiness probe both fail on the same container. Describe both consequences. **Correct answer: the container is killed and restarted per `restartPolicy`, and it is removed from the endpoints of matching Services.** The item exists to force both behaviors into one answer.
  3. A container takes four minutes to start. Which probe solves this, and what does configuring it do to the other two? Tests B1 #11 — the suppression rule is the half people miss.
  4. A container has a memory request of `256Mi` and a memory limit of `512Mi`. The node has spare memory. The container is using `400Mi`. Is anything wrong? **Correct answer: no — exceeding a request is allowed when capacity exists; only the limit is a hard boundary.**
  5. 🟡 **Interleaved with §5.** Two containers, identical images, identical code. One has a CPU limit it is exceeding; the other has a memory limit it is exceeding. Describe what an operator observes in each case, and name the phase and container state each ends up in. **Correct answer: the CPU case is throttled and stays `Running`; the memory case is eventually terminated — reactively, under pressure, not immediately — and shows a `Terminated` state.** This item requires §5 and §8 together and it is the direct precursor to Chapter 13's `OOMKilled` material.

- **Answer-key requirement**: item 5's answer key must stop short of diagnosis. Naming the mechanism is this chapter's job; `kubectl describe` and the event stream are Chapter 13's.

---

## 6. Exam Alert plan

**High-priority topics** — the seven most likely to be tested directly, in descending order of confidence:

1. **Pod phase versus container state**, with the scopes named. The highest-value distinction in the chapter and the one Chapter 13's method rests on.
2. **The three probes and their failure behaviors** — specifically that readiness de-registers without restarting and liveness restarts without de-registering.
3. **`restartPolicy` is a Pod-level field** with three values that applies to every container in the Pod.
4. **One IP per Pod**, shared by all containers, which talk over `localhost`.
5. **Requests versus limits** — which component reads which, and that CPU limits throttle while memory limits kill.
6. **A Pod is scheduled once and never rescheduled** — it is replaced, with a new UID.
7. **Every Pod has a ServiceAccount**, defaulting to the namespace's `default`, which carries no meaningful permissions.

**Common traps to call out.** All seven below are `[source]`-tagged in B1's D1 table, so all may be described as things candidates get wrong. **None are `[inferred]`, so no hedging is required** — and equally, none may be dressed with invented frequency figures (Part 14 guardrail #8, and **[B3]**'s fourth do-not-retrieve rule).

| B1 # | Trap | Where it is defused |
|---|---|---|
| 6 | Confusing Pod phase with container state | §5 Navigational Hazards + Bearings #2 item 1 |
| 7 | "`Running` means the app is working" | §5 Navigational Hazards + Bearings #2 item 1 |
| 8 | "`restartPolicy` can be set per container" | §5 Navigational Hazards + Bearings #3 item 2 |
| 9 | Assuming a failed Pod is rescheduled to a healthy node | §4 Snag |
| 10 | "Liveness and readiness do the same thing" | §7 Fixed Point + Bearings #3 item 2 |
| 11 | Forgetting that a startup probe **disables** the other probes | §7 Snag + Bearings #3 item 3 |
| 36 | "Each container in a Pod gets its own IP" | §1 Snag + Bearings #1 item 1 |

Traps 6, 7 and 8 are three of the chapter's seven and all live in §5, which is why §5 carries the primary `⚠ Navigational Hazards` block rather than distributing warnings evenly. They also share a single root cause — reading a Pod-scoped signal as a container-scoped one — and the block should say so, because naming the root cause converts three memorizations into one rule.

**One non-B1 trap worth adding**, because the documentation itself flags it: the memory suffix `m` versus `M`. It is not in B1's inventory (B1 catalogued conceptual traps, not unit notation), but the source calls it out explicitly and it is mechanically checkable, which makes it exactly the kind of thing a multiple-choice item is built from. It gets §8's Navigational Hazards block.

**Do not include** in the Exam Alert: `OOMKilled` and `Evicted` diagnosis (Ch 13), EndpointSlice (Ch 9), RBAC (Ch 12), or any framing of `CrashLoopBackOff` as a diagnostic procedure.

---

## 7. Practice Questions plan

**21 questions** (B4 allocation, unchanged). Distribution follows section weight, not section count — §2, §4 and §6 are short by design and are not entitled to proportional coverage:

| Block | Questions | Notes |
|---|---|---|
| §1–§3 — the Pod, multi-container, init | 5 | Includes **1 retrieval item** |
| §4–§5 — lifetime, phase, state, `restartPolicy` | 6 | The chapter's trap concentration; at least 4 must carry trap answers targeting B1 #6–#9 |
| §6 — identity | 2 | Includes **1 retrieval item**. Two is correct for a plant; more would over-teach material Chapter 12 owns |
| §7 — probes | 4 | At least 2 must force a liveness/readiness discrimination rather than a definition |
| §8 — requests, limits, QoS | 4 | Includes **2 retrieval items** |

**Retrieval allocation: 4 of the 21 draw from Chapters 2–4**, allocated *within* this count and not added to it:

- **Labels on a Pod** (Ch 4 §5) — §1–§3 block. **[B3]** named anchor. Frame it as *what would select this Pod*, which sets up ReplicaSet in Ch 6 and Service in Ch 9 without teaching either.
- **The `kubernetes.io/service-account-token` Secret type** (Ch 4 §4) — §6 block. Closes the loop Chapter 4 explicitly opened, in the assessment rather than the prose, which is the stronger placement.
- **Image immutability** (Ch 2) — §8 block, paired with Pod replacement: the same replace-don't-repair instinct at two levels. The parallel is real and §4 draws it; this item checks whether it transferred.
- **The control loop** (Ch 3 §6) — §8 block, framed as the kubelet running a reconciliation loop that keeps the containers described in the Pod spec running. Deliberately phrased differently from Bearings #1 item 5 so it is a second retrieval rather than a repeat: that item asks *what the kubelet reads*, this one asks *what makes it a loop*.

**Interleaving strategy.** At least **five** questions must require two sections at once. Single-section questions do not build the discrimination this exam tests, and this chapter's sections are unusually interdependent:

- Probe + `restartPolicy` (§7 + §5) — liveness failure only restarts if the policy permits it.
- Phase + init container (§5 + §3) — a Pod stuck behind a failing init container, and what phase it reports.
- Limit + container state (§8 + §5) — the memory-limit case and the state it produces.
- Multi-container + phase (§2 + §5) — one container of three has terminated; what does the Pod report?
- Identity + namespace (§6 + Ch 4 §3) — why the `default` ServiceAccount a Pod receives depends on where the Pod lives.

**Trap-answer requirement** (skill Part 11): every wrong option must target a specific misconception and the answer key must explain why each is wrong. For the §4–§5 block, wrong options should be drawn directly from B1 traps #6–#9 rather than invented — documented misconceptions make better distractors than plausible-sounding fabrications, and they are the ones the reader will actually meet.

**One calibration note.** This chapter's material is unusually amenable to *behavioral* questions — "what happens when X fails" — rather than definitional ones. Lean hard on that. A question that asks the reader to predict a consequence tests the mental model; a question that asks them to match a term to a definition tests whether they read the chapter. KCNA is a recognition exam, but the recognition it tests is of *situations*, not vocabulary lists.

---

## 8. Required figures

Six anchors, exactly as the arc outline specifies. §2, §4 and §6 deliberately carry none — see each section's Figure line for the Part 18.3/18.7 reasoning.

### `ch05-fig01-pod-shared-network-namespace`

- **Purpose**: §1's Fixed Point, dual-coded. The reader's structural template for what a Pod actually is, and the figure Chapter 9 refers back to as its ≥4-back retrieval anchor.
- **Content**: one Pod boundary containing two containers; one IP address attached to the Pod boundary, not to either container; a `localhost` path drawn *between* the containers and *inside* the boundary; a shared volume touching both. Node boundary shown around the Pod to make co-scheduling visible.
- **Design requirement — the attachment point is the pedagogy.** The IP label must be visibly bound to the Pod boundary and not to a container. A figure that places the IP ambiguously teaches the exact misconception (#36) the section corrects. This must survive grayscale (Part 18.11).
- **Label count**: Pod, two containers, IP, `localhost`, shared volume, node — seven. At the Part 18.12 ceiling; do not add anything.
- **Reuse note**: Chapter 9 retrieves this figure's *claim* by name. Design it once for two appearances.

### `ch05-fig02-pod-phases-and-container-states`

- **Purpose**: the chapter's highest-value distinction, made visible. Two vocabularies at two scopes.
- **Content**: two parallel tracks. The upper track: the five Pod phases. The lower track: the three container states, shown *nested inside* the Pod track so the scope relationship is structural rather than asserted. One worked overlay: a Pod at `Running` with one container at `Waiting`.
- **Design requirement — nesting, not adjacency.** If the two vocabularies are drawn side by side as peer lists, the figure teaches that they are alternatives. They are not; one contains the other. The containment must be the first thing the eye resolves.
- **Label count**: five phases plus three states plus two scope labels — ten. **Over the ~7 ceiling**, which is a real constraint and not a formality. Resolution: the five phase names are a single closed set the reader reads as one unit rather than five independent labels, and the same for the three states. If the illustrator finds it still reads as crowded, split into `fig02a` (phases) and `fig02b` (states with the overlay) rather than dropping the worked example — the overlay is the whole point. Flag to the author if the split is taken, since it changes the anchor count.

### `ch05-fig03-init-containers-sequence`

- **Purpose**: §3's ordering guarantee, which is a temporal claim and therefore exactly what Part 18.9 says warrants a diagram.
- **Content**: a horizontal sequence — init 1 runs and exits successfully, init 2 runs and exits successfully, then app containers start together. A second row showing the failure path: init 2 exits non-zero, restarts, and nothing downstream has begun.
- **Design requirement**: the app containers must be visibly *parallel* to each other and *sequential* to the init containers. That contrast is the section's fact in one image.
- **Label count**: two init containers, two app containers, one exit-status marker, one restart arrow — six. Within budget.

### `ch05-fig04-three-probes-compared`

- **Purpose**: §7's Fixed Point. A three-way comparison where the distinguishing property is the *failure behavior*, not the definition.
- **Content**: three rows, one per probe type. Columns: what it asks, what happens on failure, what does *not* happen on failure. The third column is the one that does the teaching and it should not be an afterthought.
- **Design requirement — comparative, per Part 18.10.** This is the chapter's one comparative illustration and it earns its place because the three probes are the textbook case of similar-sounding alternatives with different behaviors. It must be readable as a table, because that is what the reader will come back to.
- **Label count**: three rows × three columns plus headers. Tabular, so the ~7 ceiling applies to visual elements rather than cells.
- **Note**: probe *mechanisms* (exec / httpGet / tcpSocket / grpc) do **not** belong in this figure. They are orthogonal to the types and adding them turns a clean 3×3 into a 3×3×4 that teaches nothing. Mechanisms stay in prose.

### `ch05-fig05-requests-limits-qos-classes`

- **Purpose**: §8's Fixed Point, and **the chapter's most reused artifact** — retrieved in Chapters 7, 13, 17 and 18.
- **Content**: two movements in one figure. Upper: a single container's resource band, with the request marked as a floor the scheduler reads and the limit as a ceiling the kubelet enforces, and the region between them marked as "allowed if capacity exists." Lower: the three QoS classes as the outcomes of how the two values were filled in.
- **Design requirement — durability.** Four later chapters point at this. It must read correctly when re-presented with no surrounding prose, which means the component attribution (scheduler reads the floor, kubelet enforces the ceiling) has to be *in* the figure, not only in the caption.
- **Label count**: request, limit, allowed region, two component attributions, three QoS classes — eight. Slightly over; the three QoS class names function as one closed set. If it crowds, the lower movement splits to `fig06` — flag to the author, as it changes the anchor count.
- ⚠ **Blocked on the QoS source gap.** The upper movement can be specified today; the lower movement cannot. See § Open questions #2.

### `ch05-zenith-smallest-deployable-unit`

- **Purpose**: the chapter's one Zenith. The synthesis moment where seven separate facts resolve into one design decision.
- **Content**: the Pod at the center, with the chapter's consequences radiating from it — one IP, `localhost`, Pod-level `restartPolicy`, Pod-level phase, per-container state, per-Pod identity, per-Pod scheduling. Each consequence tagged with the section that taught it.
- **Design requirement — this is a dramatic synthesis illustration, not a summary diagram** (Part 18.10). It is the chapter's arousal beat at its conceptual climax and it should carry the brand's illustrative register, not the reference register of `fig05`. The section tags are a navigational aid and must not dominate.
- **Label count**: seven consequences plus the central node — eight. At the ceiling and justified: the count *is* the argument. Dropping one to hit seven would weaken the point that this many things follow from one decision.
- **Register note**: Communications Officer family, junior tier. The vessel image is available and the chapter is named for it — the smallest vessel that can be given a berth of its own. Use it once, here, and let §1–§8's prose stay plain per B2's density guidance.

---

## 9. Open questions for the author

1. **§6's pinned position — confirm the resolution, or accept a published-text edit.** `chapter-04` line 531 pins ServiceAccounts to §6, which places identity between the status vocabulary (§5) and the health block (§7). The section plan above argues this is a genuine bridge rather than a seam — §5 ends with a Pod being destroyed and replaced, which raises the "what persists about who this Pod is" question that §6 answers. **Recommendation: keep the pin.** The alternative is editing a shipped chapter to move the pointer, and the pedagogical cost of the current position is one transition sentence. Flagging it because the reader of this outline will notice the ordering and should know it was chosen, not inherited by accident.

2. **⚠ BLOCKING — four research gaps, three of them load-bearing.** The research stage must fetch these before drafting:

   | Gap | Page | Blocks | Severity |
   |---|---|---|---|
   | **QoS classes** (G3, half-open) | `kubernetes.io/docs/concepts/workloads/pods/pod-qos/` | §8's fourth movement, `ch05-fig05`'s lower half, one Exam Alert item | **Blocking.** G3 was flagged as blocking at B2 and only its requests/limits half is cached. Guaranteed / Burstable / BestEffort appear nowhere in the source set |
   | **The Pod concept page** | `kubernetes.io/docs/concepts/workloads/pods/` | §1 and §2 | **Blocking.** §1 is currently sourced entirely from secondary mentions in `workloads/`, `containers/` and `network-model/`. Each individual claim is sourceable, but the chapter's foundational section deserves its primary page — including the "two main ways Pods are used" framing that §2 rests on |
   | **Init containers** | `kubernetes.io/docs/concepts/workloads/pods/init-containers/` | §3 entirely | **Blocking.** §3 has no primary source at all today |
   | **Pod termination** | The tail of `pod-lifecycle/` — the cached snapshot stops after Container probes | §4, if the scope decision in #5 goes that way | Conditional |

   G7 (ServiceAccounts) is **closed** — `k8s-docs-service-accounts-2026-08-23.md` fully covers §6 at the plant altitude.

3. **Sidecar containers — teach the modern implementation, or only the pattern?** Kubernetes now implements sidecars as init containers with `restartPolicy: Always`, which is a genuinely useful fact and also a somewhat surprising one. **Question:** is that implementation detail associate-tier, or does §2 name the *pattern* only and leave the mechanism alone? **Recommendation: name the pattern in §2, and add the implementation only if the fetched init-container and sidecar pages establish it plainly.** Arguments for including it: it connects §2 and §3, which otherwise sit adjacent without interacting, and it prevents the reader forming the wrong model of what a sidecar is. Argument against: it adds a restartable-init-container special case to a section deliberately kept short. Requires the source fetch either way.

4. **The §6 / Ch 12 boundary — confirm the four-fact ceiling.** §6 as planned teaches: namespaced, `default` per namespace, automatic assignment, no permissions, `spec.serviceAccountName`, plus one sentence on TokenRequest. Everything else — RBAC subjects, the four-way matrix, token hardening, the Pod-creation privilege-escalation path (B1 #61), and trap #62 — is Chapter 12's. **Recommendation: hold the ceiling.** **[B3]** specifies that Chapter 12 must *derive* the RBAC matrix from Chapter 4's namespaced/cluster-scoped boundary rather than memorize it, and spending any of that derivation here would damage a chapter seven ahead for a marginal gain now.

5. **Graceful termination — in or out?** `terminationGracePeriodSeconds`, SIGTERM-then-SIGKILL, and `preStop` hooks are not in the cached snapshot (it truncates after probes) and are not named in B1's concept inventory for D1.1. They are, however, real associate-tier knowledge and they connect to twelve-factor disposability in Chapter 15. **Recommendation: include a brief treatment in §4 if the fetched source supports it, at the level of "termination is a request with a deadline, not an instant event," and no further.** If the research stage confirms it is absent from the curriculum's concept set, omit entirely rather than teaching uncited material.

6. **Nine sections — confirm, or fold.** This is the most sections of any chapter drafted so far (Ch 4 had six). Three of the nine (§2, §4, §6) are deliberately short. **Two fold options exist:** §2 into §1 (multi-container as a subsection of the Pod concept), and §4 into §5 (lifetime as the opening movement of the status section). **Recommendation: keep nine.** §5 is already the chapter's highest-attention-cost section and adding the lifetime material to it would make it the section readers abandon. §2's brevity is a feature — it is the section that tells the reader *not* to do something, and short is the right register for that. Folding either would also break the pinned numbering, since §5 and §6 are fixed by published text.

7. **Init-container resource accounting — omit by default.** The effective-request rule (a Pod's effective request is the higher of the sum of its app containers and the largest single init container) is real, obscure, and would have to live in §8, which is already the chapter's densest section. **Recommendation: omit unless the fetched init-container page presents it as core.** Flagging it because it is the kind of fact that looks like a gap to a reviewer who knows it.

8. **B4 versus B3 retrieval-rate conflict — reconcile.** `length-budget.md` § "Retrieval-practice spacing" places Ch 4–5 at ~10% drawing from Ch 2–3. `arc-outline.md` § "Cross-chapter callback map" places Ch 5 at **20% drawing from Ch 2–4** and marks it **[B3]**; the skill's Part 10 table and this stage's own prompt both say Ch 5+ is 20%. **This outline follows 20%.** Chapter 4's outline used 15%, which agrees with B3 and the skill against B4's ~10%, so the precedent is already set. **Recommendation: treat B4's table as superseded and correct it if `length-budget.md` is ever regenerated.** Note also that `retrieval-architecture.md` is a stub — the B3 stage output was lost to a blocked write and survives only as the summary in that file plus the `[B3]`-tagged figures carried into the arc outline. That is the second symptom of the same lost artifact and is worth recording.

9. **Domain weight disclosure.** `domain_weight_pct: 7` is authored judgment, not published data — CNCF publishes four domain weights and twelve named competencies with no sub-weights (B1 §G33, §G36). The front matter already carries the disclosure. **No action needed**; recorded here so the drafting stage does not present 7% as an official figure in the chapter's metadata line. The metadata line should read as this book's allocation, matching whatever phrasing Chapters 2–4 already published.

10. **Bearings raised 10 → 15.** Sanctioned by B4's standing instruction, but Chapter 5 was not on B4's named list of likely-to-exceed chapters (8, 12, 17). **Recommendation: accept.** The chapter total moves 39 → 44 against a book at 715 questions versus a 300 floor, and the Stage 8 question-quality audit is expected to cut weak items anyway. If the author prefers to hold the book to B4's exact table, drop Bearings #3 to 4 items by folding items 2 and 3 — but note that costs the startup-probe suppression rule its checkpoint coverage, and that is trap #11.

11. **Confirm what Chapter 5 does *not* touch.** Ephemeral containers and `kubectl debug` (Ch 16), `ResourceQuota` and `LimitRange` (Ch 8), EndpointSlice (Ch 9), volume types (Ch 11), `OOMKilled`/`Evicted` diagnosis (Ch 13), Pod templates and workload controllers (Ch 6), scheduling filters and taints (Ch 7). Static Pods, `spec.os`, and topology spread are either out of associate scope or belong to Chapter 7. **Recommendation: hold all of these out.** Recording the list because this chapter's material is adjacent to more of the book than any other in Part II, and every one of these is a plausible-feeling place to drift.