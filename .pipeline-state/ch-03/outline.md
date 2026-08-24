Everything I need is in hand. Emitting `outline.md`:

---

```
---
chapter: 3
chapter_type: "content"
title: "The Ship's Company"
subtitle: "Everyone aboard has one job, and none of them is 'be in charge'"
exam_domain: "Kubernetes Fundamentals (competency: Kubernetes Core Concepts)"
domain_weight_pct: 6
complexity: "mixed"
novelty: "paradigm-shifting"
prereq_factor: "standard"

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band for this chapter:
#-- "standard-plus" — 6 points, but it opens the book's structural spine and
#-- the control-loop treatment must carry five later callbacks. Planning
#-- signal only, NOT a target.
#--
#-- WARNING Section NUMBERING IS LOAD-BEARING. The published Chapter 2 ships two
#-- cross-bearings that name sections of this chapter by number:
#--   ch02 §4 -> *[cross-bearing: see Ch 3 §1 - how the cluster got the shape it has]*
#--   ch02 §4 -> *[cross-bearing: see Ch 3 §3 - node components in context]*
#-- §1 and §3 below honor those. Do not renumber without editing chapter-02.
#--
#-- WARNING Comment lines in this block deliberately use "#--" with NO space after
#-- the hash. scripts/run_chapters.sh line 72 slugifies the FIRST line matching
#-- ^#\s+ in the draft-plus-borrowed-frontmatter text, which is why Chapter 2
#-- shipped as chapter-02-section-plan-no-word-budgets.md. See Open questions #4.
sections:
  - name: "How the Cluster Got the Shape It Has"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch03-fig03-deployment-eras-timeline"
    checkpoint_after: false
  - name: "The Control Plane"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch03-fig01-control-plane-and-node-components"
    checkpoint_after: false
  - name: "Node Components in Context"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: true
  - name: "Addons, and What Else Is Optional"
    objectives: ["D1.1"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "The Only Door In"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch03-fig04-request-path-through-apiserver"
    checkpoint_after: true
  - name: "Controllers and the Control Loop"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch03-fig02-control-loop-desired-vs-current"
    checkpoint_after: true
  - name: "Nobody Is in Charge"
    objectives: ["D1.1"]
    requires_figure: true
    figure_anchor: "ch03-zenith-nobody-is-in-charge"
    checkpoint_after: false

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
soundings_planned:
  question_count: 8
  topics:
    - "scaling from three copies to five — a script that starts two, or something that keeps checking"
    - "who notices when a machine dies at 3 a.m., and what they do about it"
    - "whether every machine in a cluster runs the same software"
    - "which node component is responsible for the containers described for that node"
    - "how many components should be allowed to talk to a shared datastore directly"
    - "whether Kubernetes builds your container images"
    - "whether Kubernetes was written from scratch or descended from an internal system"
    - "what 'orchestration' means precisely, as a technical term"

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 19 = 37. Bearings raised 10 -> 13; see
#-- § "Taking Your Bearings checkpoints" for justification and B4's own sanction.
question_budget:
  soundings: 8
  taking_your_bearings: 13             # across 3 checkpoints (5 + 4 + 4)
  practice_questions: 19
  total_this_chapter: 40

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D1.1"]
  concepts:
    - "deployment-eras"
    - "traditional-deployment-era"
    - "virtualized-deployment-era"
    - "container-deployment-era"
    - "what-kubernetes-provides"
    - "what-kubernetes-is-not"
    - "self-healing"
    - "automatic-bin-packing"
    - "kubernetes-origin"
    - "borg"
    - "omega"
    - "helmsman-etymology"
    - "cncf-first-project"
    - "cluster"
    - "control-plane"
    - "worker-node"
    - "kube-apiserver"
    - "etcd"
    - "kube-scheduler"
    - "kube-controller-manager"
    - "cloud-controller-manager"
    - "kubelet"
    - "kube-proxy"
    - "container-runtime"
    - "addons"
    - "cluster-dns"
    - "optional-components"
    - "highly-available-control-plane"
    - "api-server-as-front-end"
    - "controller"
    - "control-loop"
    - "reconciliation"
    - "desired-state"
    - "current-state"
    - "control-via-api-server"
    - "direct-control"
    - "node-controller"
    - "job-controller"
    - "endpointslice-controller"
    - "serviceaccount-controller"
    - "orchestration-technical-definition"
    - "composable-control-processes"
  commands: []

figures_planned:
  - "ch03-fig01-control-plane-and-node-components"
  - "ch03-fig02-control-loop-desired-vs-current"
  - "ch03-fig03-deployment-eras-timeline"
  - "ch03-fig04-request-path-through-apiserver"
  - "ch03-zenith-nobody-is-in-charge"
---

# Chapter 3 Outline — The Ship's Company

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 3: The Ship's Company` | required | top |
| `## *"Everyone aboard has one job, and none of them is 'be in charge'"*` | required | line 2 |
| Metadata line (weight / complexity / novelty) | required | after subtitle |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings` ×3 | **required, min 2** | after §3, §5, §6 |
| `★ Fixed Point` ×3 | **required, min 1** | §3, §6, §7 |
| `**Dead Reckoning:**` ×1 min | **required** | §3 (component → its one job, plainly) |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §2 (one binary, one process), §4 (what's optional) |
| `☀️ Zenith` | expected | §7 |
| `## Exam Alert` | **required** | after §7 |
| `## Practice Questions` | **required** | 19 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19 |
| `🏆 Safe Harbor` | expected | chapter close |

**Zenith:** exactly one, per Part 18.10. `ch03-zenith-nobody-is-in-charge` in §7. Do not add a second dramatic synthesis illustration — §6's control-loop figure is a concept diagram, not a Zenith, and must not be dressed as one.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 3 — The Ship's Company". Carried forward without modification:

- **Covers**: **D1.1** — deployment eras; what Kubernetes is and is not; control-plane components (kube-apiserver, etcd, kube-scheduler, kube-controller-manager, cloud-controller-manager); node components (kubelet, kube-proxy, container runtime); addons; controllers; **the control loop**; desired vs current state; Kubernetes origin and history.
- **Prerequisites**: Ch 2 — containers, container runtime, CRI.
- **Retrieval targets**: **10%** **[B3]** — the schedule's opening rung, drawn entirely from Ch 2. Named anchors: the CRI boundary (which component actually talks to the runtime), image immutability, container-vs-VM.
- **Question budget**: 8 Soundings · 10 Bearings · 19 Practice · 37 total. Bearings raised to 13 below.
- **Figures**: five anchors, listed verbatim in `figures_planned`.
- **Depth band**: standard-plus.

**What this chapter owes forward.** More than any other chapter in the book. The control loop is the book's single structural argument, stated three times at increasing altitude, and Chapter 3 is where it is first stated:

| Concept | Retrieved at | Contract |
|---|---|---|
| **The control loop** | Ch 4 (15%), Ch 6 (20%), Ch 8 (≥4-back floor), Ch 11, Ch 15 (**25%, the primary Zenith**), Ch 17 | Named anchor six times. The Ch 15 retrieval *is* the book's Zenith; if it does not land here it cannot land there |
| kube-apiserver / etcd as state of record | Ch 4 (15%), Ch 8, Ch 12 (Secret hardening) | Named anchor |
| Control-plane / node split | Ch 8 (node lifecycle), Ch 13 (node health) | Named anchor |
| kube-proxy's role (not its modes) | Ch 9 (service proxy) | Handoff — Ch 3 names it, Ch 9 implements it |
| Controllers as a named pattern | Ch 6 (workload controllers), Ch 15 (Argo CD as a controller) | Cross-cutting theme 1 |
| "The object exists but nothing happens without the component" | Ch 10, Ch 13, Ch 17 | **[B3]** cross-cutting theme — the *seed* is planted here, in §4's optionality material |

`ch03-fig02-control-loop-desired-vs-current` is the most reused figure in the book. Ch 6, Ch 15, and Ch 17 all re-present its shape at higher altitudes. Design it once, deliberately, for three later re-presentations — see § Required figures.

**Reader positioning**: Communications Officer role family, **junior tier**. Single unified brand voice; only atmospheric register and reader rank differ.

---

## 1. Why This Chapter Matters

Planning notes for the required `## Why This Chapter Matters` section. 2–3 paragraphs of drafted prose; the notes below specify the work, not the wording.

**The curiosity gap: there is no component in Kubernetes whose job is to be in charge.** No coordinator, no conductor, no master process holding the plan. That is genuinely counterintuitive to anyone who has built or operated a distributed system, because the obvious way to make fifty machines agree is to put one of them in charge. Open the gap here, keep it open through the whole component census in §2–§4 (where the reader will be *looking* for the component that runs things and will not find it), and pay it off in §6 and §7. This is the chapter's spine and it should not be softened into a teaser — state the claim flatly and let it sit.

**The identity frame is systems reading rather than component recall.** A practitioner who has this chapter can be handed a symptom — Pods not starting, a Service with no endpoints, a node gone silent — and reason about which loop stopped closing, rather than guessing which service to restart. Chapter 1 established that this exam measures discrimination; here the discrimination is *layer attribution*, and it is the same skill Chapters 13 and 16 will formalize into a triage flow. Say once, plainly, that the component census is the vocabulary and the control loop is the grammar, and that the exam tests both but rewards the second.

**The stakes are structural and should be stated without inflation.** Roughly six points sit here on this book's authored judgment (CNCF publishes no sub-competency weights — see § Open questions #6), which makes this a mid-sized chapter by exam surface and the largest by downstream dependency. Six later chapters retrieve the control loop by name, and one of them — Chapter 15 — is built entirely around the reader recognizing it in an unfamiliar place. A reader who leaves this chapter able to recite eight component names but unable to draw a reconciliation loop has the smaller half. Say that, calmly, and move on; the brand's ethical guardrails forbid manufactured urgency and this reader is an adult professional.

---

## 2. What You'll Learn

Planning notes for the expected `## What You'll Learn` section. Five outcomes, active verbs:

- **Explain** why the container deployment era produced a system shaped like Kubernetes, and state three things Kubernetes deliberately does not do.
- **Name** every control-plane and node component, state its one job, and mark which two are optional and under what circumstances.
- **Trace** what happens between a submitted request and a running container, naming which component acts at each step — and which component never does.
- **Draw** a control loop from memory: desired state, current state, and the action that closes the gap, repeating forever.
- **Distinguish** orchestration in the technical sense — first do A, then B, then C — from a set of independent control processes, and explain why Kubernetes claims to eliminate the need for the former.

*You'll also stop looking for the component that's in charge, which is the single most useful habit this chapter can leave you with.*

---

## 3. Soundings plan

**8 questions** (content-chapter baseline per skill Part 8 and `branded-terms.yaml`). Chapter 3's prerequisite set is "general IT literacy plus Chapters 1–2," so seven test **priors the reader arrives with** and one is deliberate retrieval from Chapter 2. **[B3]** Soundings are excluded from the retrieval budget but do retrieval work anyway, sourced from B2's Prerequisites column; that is the design, and Q4 below is where it happens.

⚠ **Hard constraint discovered in the published Chapters 1 and 2.** Three of the obvious Chapter 3 pre-test questions are already spent:

- **Ch 1 A1** and **Ch 2 §1** both state the container/VM distinction. Not re-asked here in any form. It survives as a *Practice Question* retrieval item (where the reader has now been taught it), not as a pre-test.
- **Ch 1 A2** states the orchestrator/runtime split — "Kubernetes is an **orchestrator** — it decides what should run where." Q8 below deliberately re-enters this from the opposite side, asking what orchestration means *precisely*, because Chapter 1's answer used the industry's loose sense and this chapter must sharpen it. See § Open questions #1 — this is the chapter's most important reconciliation and it is not optional.
- **Ch 1 A5** and its cross-bearing assign declarative-vs-imperative to **Ch 4 §1**. Q1 below tests the *imperative instinct* without naming the declarative/imperative pair, which stays Chapter 4's to name.

| # | Topic (not wording) | Prerequisite / intuition tested | Why it is useful as a pre-test |
|---|---|---|---|
| 1 | Scaling three copies to five: a script that starts two, or something that keeps checking the count? | Whether the reader's default implementation instinct is a one-shot action or a continuous comparison | The single highest-value pre-test in the chapter. Nearly every reader with scripting background answers "start two," and that answer is the exact model §6 has to replace. Surfacing it first means §6 corrects a live belief rather than filling a void |
| 2 | A machine holding some of your application's copies fails at 3 a.m. Who notices, and what do they do? | Ops intuition about failure detection and remediation ownership | Approaches the same Fixed Point from the failure side rather than the growth side. Readers who answer "a human, from a pager" are the readers §6 is written for; readers who answer "something automatic" get to skim §6 and slow down for §7 |
| 3 | Does every machine in a Kubernetes cluster run the same software? | Cluster-architecture intuition from any prior distributed system | Gates §2 and §3 and calibrates `ch03-fig01`. Cheap, concrete, and a wrong answer here predicts a hard time with the whole census |
| 4 | Which component on a node is responsible for the containers described for that node? | **Retrieval from Ch 2 §4** — the kubelet's position in the kubelet → CRI → runtime chain | **[B3]**'s designated Soundings retrieval item. Chapter 2 taught this chain as its most-reused Fixed Point; the reader who read it can answer, and the reader who skimmed it gets a signal to go back. §3's job is to place the kubelet among its peers, not to reveal that it exists, so this spoils nothing |
| 5 | A CLI tool, an internal scheduler, and fifty node agents all need to read and write the same configuration. How many of them should talk to the datastore directly? | Architectural instinct about front doors and shared state | Gates §5. Most readers with API-design exposure answer "one," which is right, and then spend §5 discovering the consequences rather than the rule. Readers who answer "all of them, it's faster" get the section they need |
| 6 | Does Kubernetes build your container images? | Answerable from Ch 2 (images are built elsewhere and pulled) plus general platform literacy | Pre-tests §1's "what Kubernetes is not" without giving the list. Also the cheapest available correction to the reader who arrived thinking Kubernetes is a PaaS, which is B1 trap #5 |
| 7 | Was Kubernetes written from scratch, or does it descend from an earlier internal system? | Industry-history literacy | Gates §1's origin material. Genuinely tested content, not trivia, and it gives the reader who under-studies institutional material (B1's warning about D4.3) an early signal that this book will ask such things |
| 8 | "Orchestration" — is it a loose compliment or a technical term with a specific meaning? What does it mean precisely? | Vocabulary precision; whether the reader distinguishes industry shorthand from defined terms | The chapter's sharpest discrimination and its hardest one. Also the designed re-entry into the Ch 1 A2 tension: a reader who answers "coordinating containers" is repeating what Chapter 1 told them, and §1 is about to sharpen it. **Answer-key constraint below is strict** |

**Rubric** (standard 8-question scale, per `branded-terms.yaml`):

- **6+ right** — skim, with two exceptions. Read §6 at full pace regardless of score, because six later chapters retrieve it by name, and read §4 rather than skimming it, because the optionality material scores well on intuition and still catches people.
- **3–5 right** — read at normal pace. This chapter is calibrated for you.
- **0–2 right** — read carefully, in its own session, and do not move to Chapter 4 the same day. Chapter 1 already told you Chapters 2 and 3 carry the conceptual load everything else rests on; this is the second of the two. Nothing here is difficult. There are eight component names and one idea, and the idea is worth more than the names.

**Fixed-Point spoiler check — passes, with one item under discipline.** The chapter's three Fixed Points are (a) the component census with optionality marked, (b) the control loop, and (c) Kubernetes' rejection of the technical definition of orchestration.

- Q1 and Q2 pre-test the *priors* behind (b) from two different directions without naming reconciliation, desired state, or current state. Their answer keys must say only which instinct is common and where the chapter addresses it.
- Q3 and Q4 approach (a) from outside. Q3 asks only whether machines differ; it does not enumerate. Q4 names one component the reader was already taught in Chapter 2. Neither gives the census.
- Q8 pre-tests (c) and is the one at risk. **Its answer key gives the dictionary sense only** — orchestration as the execution of a defined workflow — and stops. It must not state that Kubernetes disclaims it, must not use the phrase "eliminates the need for orchestration," and must not contrast composable control processes. All three belong to §1's plant and §7's payoff, and spending them in an answer key costs both.

⚠ **Answer-key discipline for drafting.** One line per question, then stop. Q1, Q2, and Q8 will each tempt a paragraph, and each of those paragraphs is a Fixed Point this chapter is about to spend properly. Q5 has the same risk at lower intensity. Q7 is the one place a second line is permitted, because the Borg/Omega lineage is a fact rather than a mechanism and naming it early costs nothing.

---

## 4. Section plan

### §1 — ⚪ How the Cluster Got the Shape It Has

The target of a published Chapter 2 cross-bearing, and the chapter's framing section. Three moves in order. First, the three deployment eras as the docs tell them: traditional (applications on physical servers, no resource boundaries, one-app-per-server as the only isolation and it did not scale), virtualized (multiple VMs per physical CPU, isolation and better utilization, each VM a full machine with its own OS), container (relaxed isolation, shared OS, lightweight, decoupled from the underlying infrastructure and therefore portable). Second, what Kubernetes provides — the published capability list, presented as *consequences of the container era's problems* rather than as a feature bullet list, because the exam rewards knowing why each item is on the list. Third, what Kubernetes is **not**, and this is the section's real payload: not a traditional all-inclusive PaaS, does not build your source, does not ship middleware or databases or caches, does not mandate a logging or configuration solution, and — planted here, not resolved — **not a mere orchestration system**. Close with origin and naming: the Borg lineage and its research successor Omega, written in Go, first commit 2014-06-06, announced at DockerCon June 2014, v1.0 July 2015, donated by Google to the newly formed CNCF as its first project, the name from the Greek for helmsman or pilot, and K8s as the numeronym.

- **Objectives**: D1.1
- **Concepts introduced**: `deployment-eras`, `traditional-deployment-era`, `virtualized-deployment-era`, `container-deployment-era`, `what-kubernetes-provides`, `what-kubernetes-is-not`, `self-healing`, `automatic-bin-packing`, `kubernetes-origin`, `borg`, `omega`, `helmsman-etymology`, `cncf-first-project`
- **Sources**: `k8s-docs-overview-2026-08-23.md` (the three eras verbatim; the provides list; the is-not list including the orchestration disclaimer), `k8s-history-ten-years-2026-08-23.md` (Borg, Omega, Go, first-commit date, DockerCon, v1.0, CNCF donation, helmsman etymology, numeronym), `cncf-who-we-are-2026-08-23.md` (CNCF as part of the Linux Foundation)
- **Figure**: **`ch03-fig03-deployment-eras-timeline`** — required
- **Checkpoint after**: no
- **Markers planned**:
  - `> 🪝 **Snag:**` on the word "orchestration" — the plant. Two sentences at most: the industry uses it loosely, the term has a precise meaning, and the precise meaning is one Kubernetes explicitly rejects. Do not resolve here
  - `> 🔭 **Closer Look:**` optional, on Omega as the research successor to Borg. Genuinely deeper than the exam requires; cut without regret
- **Cross-bearings**: back to Ch 2 §4 (reciprocal — Chapter 2 promised this section by number); back to Ch 2 §1 (the architectural container/VM contrast this section retells at historical altitude); forward to §7 (the orchestration disclaimer, resolved); forward to Ch 17 §1 (the CNCF cloud-native definition — Chapter 1's Soundings A4 already routed it there and this section must not pre-empt it)
- ⚠ **The Chapter 1 reconciliation lands here, and it is the chapter's most important precision decision.** Published Chapter 1 answer A2 reads: "Kubernetes is an **orchestrator** — it decides what should run where." The cached overview snapshot reads: "Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration. The technical definition of orchestration is execution of a defined workflow: first do A, then B, then C." Both statements are defensible — Chapter 1 used the industry's loose sense, which was the right altitude for an orientation chapter — but a reader who remembers A2 will read §1 as a contradiction unless the book says out loud that it is sharpening its own earlier wording. **Draft it as a deliberate correction of the book's own first pass, not as a correction of the reader**, and keep the warmth: the loose sense is how everyone talks, and the precise sense is what the exam tests. Raised in § Open questions #1
- ⚠ **Precision constraint inherited from two live AUTHOR-REVIEW notes.** Chapter 1 A1 sharpened the snapshot's "shares the Operating System (OS)" to "operating system **kernel**" and flagged it; Chapter 2 §1 inherited the same flag and was told to resolve it. This section retells the era transition and will hit the same phrase a third time. **Whatever Chapter 2 resolved, match it exactly.** Three chapters diverging on the book's most-quoted sentence is precisely what the reconcile pass will surface. See § Open questions #7
- ⚠ **Scope boundary with Ch 17.** The CNCF material here is limited to *provenance* — the foundation exists, Kubernetes was its first donated project, CNCF is part of the Linux Foundation. Governance structure, maturity levels, the graduated roster, TOC/TAGs, and the cloud-native definition are all Chapter 17's, and Chapter 1's Soundings already cross-beared readers there. Name the foundation, do not characterize it
- ⚠ **Scope boundary with Ch 2.** The eras are historical here. The architectural container/VM contrast belongs to Chapter 2 §1 and was already taught; this section retells the transition as *why a system like this got built*, and should back-bear rather than re-explain

### §2 — ⚪ The Control Plane

Open with the cluster definition and the split: a Kubernetes cluster is a control plane plus a set of worker machines called nodes, every cluster needs at least one worker node in order to run Pods, and in production the control plane usually runs across multiple machines for fault tolerance. Then the five control-plane components, each with its one job. **kube-apiserver** — the front end that exposes the Kubernetes HTTP API; designed to scale horizontally by deploying more instances behind a load balancer. **etcd** — consistent, highly available key-value store, the backing store for *all* cluster data, and the docs' own terse instruction to have a backup plan. **kube-scheduler** — watches for newly created Pods with no assigned node and selects a node for them, weighing resource requirements, hardware and policy constraints, affinity, data locality, and deadlines. **kube-controller-manager** — runs the controller processes; logically each controller is separate, but they are all compiled into a single binary running in a single process, with Node, Job, EndpointSlice, and ServiceAccount named as examples. **cloud-controller-manager** — optional, embeds cloud-provider-specific logic, links the cluster to a provider API, and is simply **absent** when you run on premises or on a laptop.

- **Objectives**: D1.1
- **Concepts introduced**: `cluster`, `control-plane`, `worker-node`, `kube-apiserver`, `etcd`, `kube-scheduler`, `kube-controller-manager`, `cloud-controller-manager`, `highly-available-control-plane`
- **Sources**: `k8s-docs-cluster-architecture-2026-08-23.md` (all five components at paragraph depth; the HA framing), `k8s-docs-components-2026-08-23.md` (the one-line-per-component summaries — useful for the Dead Reckoning block in §3)
- **Figure**: **`ch03-fig01-control-plane-and-node-components`** — required, introduced here and re-presented in §3 and §4. See § Required figures for the two-stage reading requirement
- **Checkpoint after**: no
- **Markers planned**:
  - `> ⚠ **Navigational Hazards:**` on the controller-manager — B1 trap #3. Many logical controllers, one binary, one process. This is the highest-yield single sentence in the section and it reads as a triviality unless it is marked
  - `> 🪢 **Mnemonic:**` for the five control-plane components, if and only if one can be built that is not embarrassing. The four *plus* etcd shape — three kube-prefixed components, one optional cloud- prefixed one, and one that is not Kubernetes software at all — is itself the memory hook, and naming that structure may serve better than an acronym. Author's call; do not force it
  - `> ⚓ **Worth Securing:**` on etcd being the only stateful component. Everything else can be restarted, replaced, or scaled; etcd holds the cluster and is the one thing whose loss is not recoverable by restarting something
- **Cross-bearings**: forward to §5 (the API server's position, which this section states and §5 explains); forward to Ch 8 (etcd backup, version skew, and the API access gates — all named here at most in passing); forward to Ch 7 (what the scheduler actually does, in detail); forward to Ch 12 (Secrets are stored in etcd, which is why encryption at rest is a separate decision)
- ⚠ **Scope boundary with Ch 7 — tight, and drafting will drift.** The scheduler's factor list is quoted here because it is part of what the component *is*. Filtering, scoring, binding, the random tie-break, and unschedulable Pods are Chapter 7's and must not appear. The one sentence Chapter 3 owes is the component boundary: **the scheduler selects a node and records that choice; the kubelet on that node starts the containers.** That much is a component fact and it defuses the front half of B1 trap #24 without teaching Chapter 7's mechanism
- ⚠ **Scope boundary with Ch 8.** etcd backup (G27), version skew, node lifecycle, and the authentication → authorization → admission gates are all Chapter 8's. §2 may say "have a backup plan" because the architecture snapshot says exactly that, and must not say how
- ⚠ **Depth question on etcd.** The cached sources give "consistent and highly-available key value store" and nothing more — no gloss on what consistency costs, no quorum, no Raft. At associate tier that is probably correct depth, but the phrase is jargon presented as though it were plain, and this book's standard is to define terms before using them. Recommend one plain sentence on what "consistent" buys the reader (every component reads the same answer) and no more. Raised in § Open questions #9

### §3 — ⚪ Node Components in Context

The target of the second published Chapter 2 cross-bearing, and the section where the census closes. Three components, and the framing matters: these run on every node and their collective job is to maintain running Pods and provide the Kubernetes runtime environment. **kubelet** — the agent on each node; takes a set of PodSpecs provided through various mechanisms and ensures the containers described in them are running and healthy; and, in the sentence most worth marking, **does not manage containers that were not created by Kubernetes**. **kube-proxy** — optional; a network proxy on each node maintaining the node network rules that implement part of the Service concept; unnecessary if the network plugin implements equivalent packet forwarding itself. **Container runtime** — responsible for managing container execution and lifecycle; containerd, CRI-O, or any other CRI implementation. This last one is where Chapter 2 is retrieved rather than repeated: the reader already owns the kubelet → CRI → containerd/CRI-O → runC chain, and §3's contribution is to place the kubelet among its peers and show that the runtime is the one node component that is *not* Kubernetes software. Close the census with the Fixed Point and the Dead Reckoning block.

- **Objectives**: D1.1
- **Concepts introduced**: `kubelet`, `kube-proxy`, `container-runtime`
- **Sources**: `k8s-docs-cluster-architecture-2026-08-23.md` (all three at paragraph depth, including the not-created-by-Kubernetes clause and kube-proxy's optionality condition), `k8s-docs-components-2026-08-23.md` (the node-components framing sentence)
- **Figure**: none new. Re-present `ch03-fig01` with the node half in focus. Do not commission a second diagram of the same cluster
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #1**
- **Markers planned**:
  - `★ **Fixed Point:**` — **the census.** Control plane: kube-apiserver, etcd, kube-scheduler, kube-controller-manager, and cloud-controller-manager (optional). Node: kubelet, kube-proxy (optional), container runtime. Eight names, two of them optional, one of them not Kubernetes software. This is the chapter's pure-recall payload and it belongs here, at the point the census is complete, not split across §2 and §3
  - `> **Dead Reckoning:**` — the contract-required facts-only block, and this chapter's natural home for it. One line per component: name, where it runs, its one job. No metaphor, no ship, no elaboration. The chapter is metaphor-forward by title and this block is the reader's escape hatch from it
  - `> ⚓ **Worth Securing:**` on the kubelet ignoring containers it did not create — the fact that makes `docker run` on a node invisible to Kubernetes, and the reason node-level debugging needs its own tool
- **Cross-bearings**: back to Ch 2 §4 (reciprocal — Chapter 2 promised this section by number, and the CRI chain is retrieved here); forward to Ch 9 (kube-proxy modes and how Services are actually implemented); forward to Ch 13 §5 (`crictl`, and why a node-level tool exists below the Kubernetes API); forward to Ch 5 (PodSpec — named here, defined there)
- ⚠ **Scope boundary with Ch 9 — the sharpest in the chapter.** kube-proxy's *role* is Chapter 3's; its *modes* (iptables, IPVS, nftables) are Chapter 9's and are a known research gap there (G24). Do not name a mode. Similarly, "implements part of the Service concept" is the correct hedge — Service is Chapter 9's object and must be named without being taught
- ⚠ **Scope boundary with Ch 5.** "PodSpec" appears in the kubelet's own definition and cannot be avoided. Name it as "the description of what containers should run" and cross-bear forward. Pod phases, container states, `restartPolicy`, and probes are all Chapter 5's, and this is the section where drafting will reach for them to make the kubelet's job concrete. Resist; the kubelet's job is stateable without them

### §4 — 🔵 Addons, and What Else Is Optional

The shortest section, and it earns its place by making one pattern explicit rather than by adding names. Addons first: cluster extensions rather than components, implemented using Kubernetes resources, and the published four — DNS, the web UI Dashboard, container resource monitoring, and cluster-level logging. Then the point the section exists for. The reader has now met eight components and four addons, and three of those twelve are marked optional in the documentation for three different reasons: kube-proxy because something else can do its job, cloud-controller-manager because there may be no cloud to talk to, and addons because they extend rather than constitute. Name the general pattern once, because **[B3]** designates it a cross-cutting theme retrieved four more times: **an object can exist while nothing acts on it, if the component that would act is absent.** Cluster DNS is the honest illustration — technically an addon, effectively mandatory, and almost every cluster ships it.

- **Objectives**: D1.1
- **Concepts introduced**: `addons`, `cluster-dns`, `optional-components`
- **Sources**: `k8s-docs-components-2026-08-23.md` (the addon list and the "extend the functionality" framing), `k8s-docs-cluster-architecture-2026-08-23.md` (kube-proxy and cloud-controller-manager optionality)
- **Figure**: none. Re-present `ch03-fig01`, or rely on its required visual distinction between mandatory and optional components — see § Required figures
- **Checkpoint after**: no (the following checkpoint covers §4 and §5 together)
- **Markers planned**:
  - `> ⚠ **Navigational Hazards:**` covering B1 traps #1 and #2 together — "kube-proxy runs on every node" and "every cluster has a cloud-controller-manager." Both are `[source]`-tagged and both are cheap points. Pairing them in one callout is better than two, because the shared lesson is *read the word optional in the documentation*
  - `> ⚓ **Worth Securing:**` on the object-without-a-component pattern, named as a pattern. **[B3]** wants this retrievable by name, so give it a name and use the same name in Chapters 10, 13, and 17
- **Cross-bearings**: forward to Ch 9 (CoreDNS as the DNS addon, and Service DNS records); forward to Ch 10 (an Ingress with no controller does nothing — the same pattern, first recurrence); forward to Ch 13 (`kubectl top` without metrics-server); forward to Ch 17 (VPA is not shipped by default)
- ⚠ **Research thinness, non-blocking.** The cached snapshot lists the four addons as bare bullets with no elaboration. Nothing on disk supports the claim that cluster DNS is effectively mandatory in practice, which is true and useful and currently unsourceable. Either source it in Stage 2 (`kubernetes.io/docs/concepts/cluster-administration/addons/`) or state it as the author's observation rather than as documented fact. Raised in § Open questions #8
- ⚠ **Section-existence question.** This material could fold into §3 as a closing subsection. It is kept separate because the optionality pattern is a **[B3]** cross-cutting theme retrieved four times and buried patterns do not survive retrieval — and because renumbering is constrained by two published cross-bearings that pin §1 and §3. Raised in § Open questions #5

### §5 — 🔵 The Only Door In

The structural half of the chapter's argument. The reader has the census; this section arranges it. The API server is the front end for the control plane, and the arrangement that follows from that is hub-and-spoke: `kubectl`, the scheduler, the controller-manager, and every kubelet on every node all interact with the API server, and the API server is what reads and writes etcd. Draw the consequence explicitly and then draw the *absence* — there is no arrow from the scheduler to a kubelet, none from a controller to a node, none between two nodes. Components that appear to cooperate are not talking; they are each watching the same state and acting on what they see. Tell the submission story at component altitude to make it concrete: a request arrives at the API server, is persisted, and from that moment separate components independently notice that there is work to do. That story is the chapter's second-most-important beat and it sets up §6 completely.

- **Objectives**: D1.1
- **Concepts introduced**: `api-server-as-front-end`
- **Sources**: `k8s-docs-cluster-architecture-2026-08-23.md` (API server as front end; horizontal scaling; etcd as backing store for all cluster data), `k8s-docs-controllers-2026-08-23.md` (controllers commonly send messages to the API server rather than acting directly; "Other components in the control plane act on the new information")
- **Figure**: **`ch03-fig04-request-path-through-apiserver`** — required. The absence of lateral arrows is the pedagogy; see § Required figures
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #2**
- **Markers planned**:
  - `> ⚓ **Worth Securing:**` on watching-versus-being-told as the coordination mechanism. This is the sentence Chapter 15 will retrieve when Argo CD watches a Git repository
  - `> 🔭 **Closer Look:**` optional, on why a hub does not become a bottleneck — the API server scales horizontally by adding instances, which the architecture snapshot states directly. Genuinely optional depth
- **Cross-bearings**: forward to §6 (what the watchers do with what they see); forward to Ch 4 (`kubectl apply` and the object it submits — named here, taught there); forward to Ch 8 (the three API access gates the request actually passes through); forward to Ch 15 (the same shape with a Git repository in the hub position)
- ⚠ **BLOCKING research gap — the section's central claim is not currently sourceable.** The cached set supports (a) the API server is the front end for the control plane, (b) etcd is the backing store for all cluster data, (c) controllers commonly message the API server rather than acting directly, and (d) "Centralized control is also not required." It does **not** state that only the API server talks to etcd, and it does **not** state that components never communicate directly with each other. Both are load-bearing for §5, for `ch03-fig04`, and for §7's Zenith. Stage 2 must fetch `kubernetes.io/docs/concepts/architecture/control-plane-node-communication/` — a page the architecture snapshot lists as a related topic and which was not captured. **If that fetch fails, §5 must narrow to what the snapshots support** and `ch03-fig04` must lose its no-lateral-arrows claim, which would cost the Zenith most of its force. Raised in § Open questions #2 as the chapter's one blocking item
- ⚠ **Scope boundary with Ch 4.** The submission story wants `kubectl apply` and it wants `spec`. Both are Chapter 4's, and Chapter 1's Soundings A5 already cross-beared declarative-vs-imperative there. Tell the story with "a request describing what should exist" and cross-bear; do not name the fields
- ⚠ **Scope boundary with Ch 8.** Authentication, authorization, and admission are the three gates that request actually passes. Chapter 8 owns them. §5 may say the request is validated and persisted; it may not enumerate

### §6 — 🔵 Controllers and the Control Loop

The chapter's most important section and the one the whole book leans on. Start where the documentation starts, with the thermostat, because it is the source's own analogy and it is a good one: you set a desired temperature, the room has a current temperature, and the thermostat acts to close the gap by turning equipment on or off, without ever completing. Generalize: in Kubernetes, controllers are control loops that watch cluster state and make or request changes, each trying to move current state closer to desired state. Then the pattern with precision. A controller tracks at least one resource type; those objects carry a field describing desired state; the controller is responsible for making current state approach it. It usually does not act directly — the Job controller is the documentation's own example, and the sentence to dwell on is that **the Job controller does not run any Pods or containers itself; it tells the API server to create or remove Pods**, and other components act on that new information. Name the second, less common shape: direct control, where a controller finds desired state from the API server and then talks to something outside the cluster to bring it in line. Close with the claim that unsettles people and is the chapter's most quietly radical idea: the cluster may never reach a stable state, and that is fine — as long as the controllers are running and able to make useful changes, it does not matter whether the overall state is stable.

- **Objectives**: D1.1
- **Concepts introduced**: `controller`, `control-loop`, `reconciliation`, `desired-state`, `current-state`, `control-via-api-server`, `direct-control`, `node-controller`, `job-controller`, `endpointslice-controller`, `serviceaccount-controller`
- **Sources**: `k8s-docs-controllers-2026-08-23.md` — the whole snapshot, which is unusually complete for this material (thermostat, controller pattern, control via API server with the Job worked example, direct control, desired-versus-current-state and the never-stable claim). `k8s-docs-cluster-architecture-2026-08-23.md` for the four named built-in controllers
- **Figure**: **`ch03-fig02-control-loop-desired-vs-current`** — required. The book's most reused figure; see § Required figures for the three-altitude design requirement
- **Checkpoint after**: **yes — ☆ Taking Your Bearings #3**
- **Markers planned**:
  - `★ **Fixed Point:**` — **the control loop.** Desired state, current state, an action that closes the gap, repeating without terminating. Phrase it so it can be quoted verbatim in Chapters 6, 15, and 17, because it will be. This is the single most reused item in the book and it should read as though it were written to be reused
  - `> **Extended Analogy:**` — the chapter's one sidebar, and this is where it belongs. The ship's company of the title: every rating holds a standing order rather than waiting on instruction, the watch is continuous rather than task-based, and the vessel stays on course through many small independent corrections rather than one plan executed in sequence. **Density constraint:** one sidebar, and the metaphor stays inside it. The section's body prose uses the thermostat, because the thermostat is the source's analogy and it is more precise
  - `> 🪝 **Snag:**` on "the controller does the work" — it usually does not; it asks the API server to, and something else acts. This is the distinction Chapter 15 needs
- **Cross-bearings**: back to §5 (the loop runs through the hub, which is why watching works); back to §1 (the orchestration plant, now answerable); forward to Ch 4 (the field that holds desired state, and its status counterpart); forward to Ch 6 (ReplicaSet as a control loop you can watch work); forward to Ch 15 (**the primary Zenith** — the same loop pointed at a Git repository)
- ⚠ **Scope boundary with Ch 4 — the most delicate in the chapter.** The control loop needs "desired state" and Chapter 4 owns `spec` and `status`. Teach the loop conceptually and completely, using "the field that says what should be true" rather than the field name, and cross-bear forward. The cached snapshot itself says "these objects have a spec field," so the word is available and the temptation is real; using it here means Chapter 4 introduces a term the reader already met, which weakens Chapter 4's own opening. Author may overrule, but the two chapters must agree — raised in § Open questions #3
- ⚠ **Scope boundary with Ch 6.** The four named built-in controllers are named here as evidence that controllers are plural and ordinary, not taught. Deployment, ReplicaSet, StatefulSet, DaemonSet, Job-as-a-workload-resource, and CronJob are all Chapter 6's. §6 may use the Job controller as the documentation's worked example — it is the source's own choice of example and swapping it costs precision — while making clear that the Job *resource* arrives later
- ⚠ **Do not over-teach reconciliation loops as an implementation.** Watch/list semantics, informers, resync periods, and work queues are all above associate tier and none are in the cached set. The exam tests the pattern, not the plumbing

### §7 — 🟡 Nobody Is in Charge

The Zenith, and a genuinely short section — the work was done in §5 and §6, and this is where the two halves meet. The reader now knows that all state moves through one hub, and that many independent loops each watch that state and act on their own account. Put those together and the chapter's opening claim resolves: there is no component whose job is to hold the plan, because there is no plan in that sense. Return to §1's plant and pay it off with the documentation's own words — Kubernetes is not a mere orchestration system; it eliminates the need for orchestration; the technical definition of orchestration is the execution of a defined workflow, first A then B then C; Kubernetes instead comprises a set of independent, composable control processes that continuously drive current state toward desired state; it should not matter how you get from A to C; and centralized control is not required. Then say what this buys, because the reader should leave with a reason and not only a distinction: a system with no central coordinator has no single component whose failure stops everything, and one that describes outcomes rather than sequences can absorb a change to the outcome without anyone rewriting the sequence. Close by naming what the reader has just acquired — a shape they will meet four more times — and hand off to Chapter 4.

- **Objectives**: D1.1
- **Concepts introduced**: `orchestration-technical-definition`, `composable-control-processes`
- **Sources**: `k8s-docs-overview-2026-08-23.md` (the full is-not-orchestration passage, including the A-then-B-then-C definition and the centralized-control clause), `k8s-docs-controllers-2026-08-23.md` (the never-stable-state claim)
- **Figure**: **`ch03-zenith-nobody-is-in-charge`** — required, and the chapter's only Zenith
- **Checkpoint after**: no. The Zenith closes the chapter's argument and a checkpoint immediately after it would deflate the beat. Exam Alert follows
- **Markers planned**:
  - `☀️ **Zenith**` — the synthesis moment, marked
  - `★ **Fixed Point:**` — the orchestration disclaimer, in the documentation's own terms. Third and last Fixed Point
  - `🏆 **Safe Harbor**` — chapter close
- **Cross-bearings**: back to §1 (the plant, now paid); back to Ch 1 (the sharpened sense of a word Chapter 1 used loosely — say so plainly); forward to Ch 6, Ch 15, Ch 17 (where this shape recurs)
- ⚠ **Hard precision constraint — the title's claim is stronger than the truth, and the section must be more careful than its heading.** "Nobody is in charge" is a good heading and a bad thesis. The control plane does make global decisions; the API server *is* the hub every component depends on; losing etcd does lose the cluster. The accurate claim is narrower and better: **there is no component that executes a workflow, and no component that tells another component what to do.** The hub holds state and serves it; it does not direct. Draft §7 to the narrow claim and let the heading be the heading. A reader who leaves believing Kubernetes has no critical components has been taught something false, and Chapters 8, 12, and 13 all depend on them knowing better
- ⚠ **Do not overclaim resilience.** "No single point of failure" is not a supportable statement about a cluster with one etcd. The supportable statement is about *coordination* rather than *availability*: no component's failure leaves the others without instructions, because none of them were taking instructions. Availability is Chapter 8's material

---

## 5. Taking Your Bearings checkpoints

**Three checkpoints, 13 questions total.** B4 allocates 10; this outline raises it to 13 on B4's own instruction: *"Outlines should treat the 10 as a contract to exceed, not a target to hit."* Chapter 3 carries two-and-a-half arcs — the framing (§1), the component census (§2–§4), and the architecture-and-loop argument (§5–§7) — and the census alone is eight names with two optionality exceptions, which is the largest pure-recall load in the first half of the book. Folding it in with the control loop would put name-recall and abstract-pattern reasoning in one block, which are different cognitive modes and a needless alternating-attention cost (skill Part 4). Practice Questions stay at 19 and Soundings at 8, so the chapter total moves 37 → 40 against a book with 415 questions of headroom.

**Retrieval-practice content: 10%** **[B3]** — the schedule's opening rung, drawn **entirely from Chapter 2**. Chapter 1 is excluded from the retrieval schedule entirely and no item may test exam mechanics. Against a combined Bearings-plus-Practice pool of 32, the 10% target is ~3 items, allocated **1 in Bearings and 2 in Practice** (3 of 32 = 9.4%). Placement is not arbitrary — each of **[B3]**'s three named anchors has exactly one section where it belongs:

| Ch 2 anchor | Placed in | Why it fits rather than bolts on |
|---|---|---|
| The CRI boundary — which component talks to the runtime | **Bearings #1**, item 5 | §3 introduces the container runtime as a node component; the question the reader must answer is *which of these eight components actually invokes it*, which is genuinely integrative |
| Container vs VM | **Practice**, 1 item | §1 retells the era transition at historical altitude; the item asks the reader to supply the architectural reason, which Ch 2 taught |
| Image immutability | **Practice**, 1 item | The control loop's response to a changed desired state is to replace rather than mutate — the same instinct as rebuilding an image rather than patching a container. A real conceptual link, not a topic collision |

### ☆ Taking Your Bearings #1 — after §3

- **Topic**: the component census — who is where, and what each one does
- **Count**: 5
- **Retrieval from earlier chapters**: 1 of 5 (20% of this checkpoint; contributes to the chapter's ~10%)
- **Question design**:
  1. **Placement.** Given a component, state whether it runs on the control plane or on every node. Rotate which component is tested; kube-proxy and the container runtime are the highest-value because both are node components readers routinely place on the control plane
  2. **One job, given the job.** Describe a responsibility and ask which component holds it. Distractors should be *adjacent* components, not random ones — "watches for Pods with no assigned node" against the controller-manager, not against etcd
  3. **The controller-manager's shape.** B1 trap #3. Trap answers offer one process per controller, one container per controller, and one Pod per controller. All three are plausible and all three are wrong
  4. **etcd's scope.** What is stored there, and what "all cluster data" includes. Trap answers should offer a subset — "only the objects you created," "only Pod definitions" — because the belief that etcd holds part of the state is the one that leads readers astray in Chapter 12
  5. **Retrieval from Ch 2 — the CRI boundary.** Given the node components, identify which one actually causes a container to start, and through what interface. This is the chapter's designated retrieval item and it is deliberately the checkpoint's hardest
- **Trap-answer targets**: one-process-per-controller (#3); placing kube-proxy or the container runtime on the control plane; etcd holding a subset of state; the belief that the scheduler starts containers (front half of #24 only — the mechanism is Ch 7's)
- **Why-wrong explanations**: required for every option, per the contract and the ethical checklist

### ☆ Taking Your Bearings #2 — after §5

- **Topic**: what is optional, and how the pieces are arranged
- **Count**: 4
- **Retrieval from earlier chapters**: 0
- **Question design**:
  1. **kube-proxy's optionality.** B1 trap #1. Not just *that* it is optional but *under what condition* — a network plugin providing equivalent packet forwarding. Trap answers should include "optional in single-node clusters" and "optional if you don't use Services," both wrong for instructive reasons
  2. **cloud-controller-manager's absence.** B1 trap #2. Given a deployment context — on-premises, a laptop, a managed cloud cluster — say whether the component is present
  3. **Addon versus component.** Given something like cluster DNS, classify it and say what follows from the classification. This is where the object-without-a-component pattern gets its first test, one chapter before Chapter 10 needs it
  4. **The arrangement.** Given two components, say whether they communicate directly. At least one pairing should be one readers assume talks — scheduler and kubelet is the best candidate. **Conditional on the §5 research gap closing;** if `control-plane-node-communication` is not fetched, this item must be rewritten to test the API server's front-end role only, which is sourced
- **Trap-answer targets**: kube-proxy as mandatory (#1); universal CCM presence (#2); treating addons as components; assuming the scheduler instructs the kubelet
- **⚓ Design note**: item 4 is the checkpoint's integrative item and the one that most rewards having read §5 rather than skimmed it

### ☆ Taking Your Bearings #3 — after §6

- **Topic**: controllers and the control loop
- **Count**: 4
- **Retrieval from earlier chapters**: 0
- **Question design**:
  1. **The loop, stated.** Given a described behavior, identify whether it is a control loop and name its two states. This is the chapter's Fixed Point and it earns a dedicated item
  2. **What a controller actually does.** The Job-controller distinction: it does not run Pods, it asks the API server to create them, and something else acts. Trap answers should offer the controller starting containers directly, the controller scheduling the Pod, and the controller talking to the kubelet
  3. **Control via API server versus direct control.** Given a controller's job — reconciling replica counts, or provisioning a machine that does not yet exist — say which shape applies. Four items in, this is the discrimination most readers have not made
  4. **Never reaching a stable state.** Whether a cluster that never stabilizes is malfunctioning. Trap answers should treat instability as a failure condition, which is the intuitive and wrong reading, and the explanation should quote the documentation's own position
- **Trap-answer targets**: the controller acting directly on containers; treating direct control as the common case; reading continuous change as malfunction; conflating the controller with the thing it controls
- ⚠ **Scope guard**: no item in this checkpoint may require `spec`/`status` field names (Ch 4), ReplicaSet or Deployment (Ch 6), CRDs or the operator pattern (Ch 6), or GitOps (Ch 15). This is the checkpoint where drafting will reach forward, because every one of those makes the loop more concrete and every one of them is somebody else's

---

## 6. Exam Alert plan

**High-priority topics** — the five this chapter would defend as most worth the reader's memory:

1. **The census, with optionality marked.** Eight components across two planes; kube-proxy and cloud-controller-manager optional, and for different reasons. Pure recall, cheaply tested, and the exam does test it.
2. **The control loop.** Desired state, current state, an action that closes the gap, never terminating. The most reused idea in the book and the chapter's highest-value item by a wide margin.
3. **kube-controller-manager: many logical controllers, one binary, one process.** A single sentence, disproportionately tested, and invisible unless marked.
4. **Kubernetes is not a mere orchestration system.** The technical definition of orchestration is the execution of a defined workflow; Kubernetes disclaims it and describes itself as independent, composable control processes. Also the reconciliation of a word Chapter 1 used loosely.
5. **What Kubernetes is not.** Not a traditional all-inclusive PaaS; does not build source; does not ship middleware, databases, or caches; does not mandate logging or configuration solutions.

**Common traps to call out** — each carries its B1 number and evidence tag. All five are `[source]`-tagged, which is unusual and worth noting: this chapter has no `[inferred]` traps and therefore no framing constraint under Ethical Guardrail #8.

| B1 # | Trap | Tag | Where the chapter defuses it |
|---|---|---|---|
| 1 | "kube-proxy is required on every node" | `[source]` | §4 ⚠ Navigational Hazards; Bearings #2 item 1 |
| 2 | "Every cluster has a cloud-controller-manager" | `[source]` | §2 (stated) and §4 ⚠ (marked); Bearings #2 item 2 |
| 3 | "The controller-manager runs one process per controller" | `[source]` | §2 ⚠ Navigational Hazards; Bearings #1 item 3 |
| 4 | "Kubernetes is an orchestrator that runs A then B then C" | `[source]` | §1 🪝 Snag plants it; §7 Fixed Point pays it; Soundings Q8 pre-tests the prior; Bearings #3 |
| 5 | "Kubernetes is a PaaS" | `[source]` | §1; Soundings Q6 pre-tests it; Practice |
| 24 (front half only) | "The scheduler places the Pod on the node" | `[source]` | §2 scope note — the scheduler selects and records; the kubelet starts. **The filter → score → bind mechanism is Chapter 7's and must not appear here** |

**Do not include** in the Exam Alert: version skew, node lifecycle, etcd backup, or the API access gates (all Chapter 8); the scheduling algorithm (Chapter 7); `spec`/`status` field names or declarative-versus-imperative (Chapter 4); Pod phases, container states, or probes (Chapter 5); CRDs and the operator pattern (Chapter 6); kube-proxy modes (Chapter 9); the CNCF cloud-native definition, maturity levels, or governance (Chapter 17).

---

## 7. Practice Questions plan

**Target count: 19** — from B4's weight-monotonic derivation `15 + 2 × (weight − 4)` at this chapter's 6 points. Comfortably inside the skill's 15–25 per-chapter range; nothing clipped.

**Distribution across sections**, proportional to conceptual load and exam surface:

| Section | Questions | Rationale |
|---|---|---|
| §1 eras, is-not, history | 3 | The is-not list carries most of this; the eras and origin material are each worth one |
| §2 control plane | 4 | Largest allocation. Five components, the densest name surface in the chapter |
| §3 node components | 3 | Three components, one of which (the runtime) is retrieved rather than taught |
| §4 addons and optionality | 2 | Small surface, high per-item value — both traps live here |
| §5 the API server's position | 2 | Constrained by the research gap; do not write a third until §5's sourcing is settled |
| §6 controllers and the control loop | 4 | Tied for largest. The chapter's Fixed Point and the book's most retrieved idea |
| §7 synthesis | 1 | One integrative item on the orchestration disclaimer; the Zenith is not a question bank |
| **Total** | **19** | |

**Retrieval allocation: 2 of the 19 draw from Chapter 2**, allocated within this count and not added to it — one on the container/VM architectural reason behind §1's era transition, one on immutability as the same replace-don't-mutate instinct the control loop shows. Both are listed in § Taking Your Bearings checkpoints with their placement rationale.

**Interleaving strategy.** **At least 5 of the 19 must require combining two sections.** The highest-value pairings are already known:

- **§2 + §6** — given a controller's job, name the component that houses it and the loop it runs. The single best integrative item in the chapter, and it tests both Fixed Points at once
- **§3 + §5** — given a node component, say what it talks to and what it does not. Directly defuses the assumption that the scheduler instructs the kubelet
- **§1 + §7** — given a described system behavior, say whether it is orchestration in the technical sense
- **§4 + §6** — an object exists, the controller that would act on it is absent; what happens? First recurrence of the **[B3]** cross-cutting pattern, one chapter before Chapter 10 needs it
- **§2 + §4** — which components are optional, and is the reason the same for each?

**Difficulty mix**: roughly 6 ⚪ Foundation, 9 🔵 Standard, 4 🟡 Advanced. The Advanced items should be the four integrative pairings above, not obscure facts — this is a beginner exam and difficulty should come from combination, not from depth.

---

## 8. Required figures

Five anchors, exactly as the arc outline specifies. Note that §3 and §4 deliberately carry no figure of their own and re-present `ch03-fig01`; commissioning a second cluster diagram would violate the coherence principle for no pedagogical gain.

### `ch03-fig01-control-plane-and-node-components`

- **Purpose**: the cluster map. Dual-coding target for the chapter's first Fixed Point (the census), and the reader's spatial anchor for §2, §3, and §4.
- **Content**: two bounded regions. Control plane containing kube-apiserver, etcd, kube-scheduler, kube-controller-manager, cloud-controller-manager. A node containing kubelet, kube-proxy, container runtime — with a second, partially shown node to make "every node" visible without doubling the label count.
- **Design requirements, both load-bearing**:
  1. **Optional components must be visually distinguished from mandatory ones** — a distinct border treatment, legible in grayscale, carried in the legend. This single choice defuses B1 traps #1 and #2 in the figure rather than only in prose, and it is why §4 needs no figure of its own.
  2. **Must support two-stage reading.** §2 presents it with the control-plane half in focus; §3 re-presents the same figure with the node half in focus. Either two crops of one master or one figure whose emphasis is carried in the caption — author's call, but the underlying geometry must be identical so the reader recognizes it the second time.
- **Label count**: eight components plus two region labels. At the ceiling of the ~7-label guidance in Part 18.12 and justified only because the labels *are* the content. Do not add arrows to this figure; arrows are `ch03-fig04`'s job.

### `ch03-fig02-control-loop-desired-vs-current`

- **Purpose**: the chapter's central Fixed Point, and **the most reused figure in the book**.
- **Content**: a closed loop with three stations — desired state, current state, the action that closes the gap — and no terminus. The absence of a start or end point is the pedagogy; a loop drawn with an entry arrow teaches the wrong thing.
- **Design requirement — three-altitude reuse.** Chapter 6 re-presents this shape with a ReplicaSet in it, Chapter 15 with a Git repository, Chapter 17 at pattern altitude. Design the master abstractly enough that the three later versions are recognizably the *same* diagram with different labels, and record the label slots in the figure spec so the later chapters inherit rather than reinvent. **[B3]** makes the Chapter 15 recognition the book's primary Zenith; it depends on this figure being visually memorable here.
- **Label count**: four or fewer. Deliberately sparse — this is the one figure in the chapter that should look almost empty.

### `ch03-fig03-deployment-eras-timeline`

- **Purpose**: the historical frame for §1, and the dual-coding target for the traditional → virtualized → container progression.
- **Content**: three eras left to right, each showing what the deployment unit was and what it shared with the host. The comparison axis should be *what is shared*, since that is the axis the whole progression turns on.
- **Design requirement**: this figure sits adjacent to Chapter 2's `ch02-fig01-vm-vs-container-stack`, which draws the same contrast architecturally. **They must not look like the same figure.** Chapter 3's is a timeline; Chapter 2's is a stack. If the two converge visually the reader will read the second as a repeat and skip it. Flag for the diagram pipeline to review both together.

### `ch03-fig04-request-path-through-apiserver`

- **Purpose**: §5's structural claim, and the setup for the Zenith.
- **Content**: `kubectl`, kube-scheduler, kube-controller-manager, and two kubelets, each with an arrow to kube-apiserver; kube-apiserver with an arrow to etcd. **The pedagogy is the arrows that are absent** — nothing from scheduler to kubelet, nothing between nodes, nothing bypassing the API server to etcd.
- **Design requirement**: the caption must draw attention to the absence explicitly, because a reader scanning the figure will see arrows and not notice the missing ones. Per Part 18.7 the caption adds context rather than restating content, and "notice what does not connect" is exactly the right kind of context.
- ⚠ **Blocked on the §5 research gap.** The no-lateral-arrows claim is not currently supported by any cached snapshot. If Stage 2 cannot source it, this figure must be redrawn to the weaker claim — the API server as front end — and §7's Zenith loses most of its force. Do not commission until § Open questions #2 resolves.

### `ch03-zenith-nobody-is-in-charge`

- **Purpose**: the chapter's single dramatic synthesis illustration, per Part 18.10.
- **Content**: the ship's company at work — many hands, each at a station, each acting on a standing order, no figure giving instructions, and (per the locked architectural rule) no narrator face. The visual argument is a vessel underway and correct on course with nobody at the center of the frame.
- **Design requirement**: must not read as *unmanned*. The register is distributed competence, not absence — a busy deck, not an empty one. An empty scene would illustrate the chapter's overclaim (see the §7 precision constraint) rather than its actual thesis.
- **Register note**: Communications Officer role family, junior tier; age-of-sail through early-steam era placement per the arc outline. Atmospheric only — the prose voice does not change.

---

## 9. Open questions for the author

1. **The Chapter 1 "orchestrator" reconciliation — resolve before drafting §1.** Published Chapter 1 answer A2 calls Kubernetes "an **orchestrator**"; the cached documentation says it "is not a mere orchestration system" and "eliminates the need for orchestration." Both are correct at their own altitudes and the exam tests the second. Recommendation: §1 sharpens the book's own earlier wording explicitly and warmly — the loose sense is how the industry talks and was the right call for an orientation chapter, the precise sense is what gets tested — and Soundings Q8 sets it up. The alternative, editing Chapter 1's A2, is worse: A2 is answering a different question (orchestrator versus runtime) and is correct for that question. **Confirm the sharpen-forward approach.**

2. **BLOCKING — §5's central claim is unsourced.** Nothing cached states that only the API server writes etcd, or that components do not communicate directly. Stage 2 must fetch `kubernetes.io/docs/concepts/architecture/control-plane-node-communication/`, which the architecture page lists as a related topic and which was not captured. §5, `ch03-fig04`, Bearings #2 item 4, and the force of the §7 Zenith all depend on it. **If the fetch fails, all four narrow to the API-server-as-front-end claim.** This is the chapter's one blocking item.

3. **Does §6 use the word `spec`?** The control loop needs "desired state," Chapter 4 owns `spec`/`status`, and the cached controllers snapshot uses the word `spec` directly. Recommendation: §6 teaches the loop in plain language and cross-bears forward, so Chapter 4 gets to introduce its own vocabulary. Cost: the reader meets the concept before the noun, which some readers find unsatisfying. **Either choice is defensible; the two chapters must agree.**

4. **Chapter 2 shipped under the wrong filename, and this is a runner defect worth fixing.** The published file is `chapter-02-section-plan-no-word-budgets.md`. Cause: `scripts/run_chapters.sh` line 72 slugifies the first line matching `^#\s+` in the draft after prepending the outline's frontmatter (lines 65–71), and Chapter 2's frontmatter contains the comment `# --- Section plan (no word budgets) ---`. This outline mitigates defensively by writing frontmatter comments as `#--` with no following space, so Chapter 3 should materialize correctly. **Two follow-ups the mitigation does not cover:** (a) the regex should prefer `^#\s+Chapter\s+\d+` or search only after the frontmatter block; (b) `existing = list(book.glob(...))` at line 75 means Chapter 2's bad name is now sticky and needs a manual `git mv` plus a check for anything referencing it.

5. **Should §4 exist?** The addons-and-optionality material is thin enough to fold into §3 as a closing subsection. It is kept separate because the object-without-a-component pattern is a **[B3]** cross-cutting theme retrieved four times and buried patterns do not survive retrieval. Note that folding it is cheap — §4 is not named by any published cross-bearing — while renumbering §1 or §3 is not, because both are pinned by published Chapter 2 text.

6. **Per-chapter weight (6%) is authored judgment, not CNCF data** (B1 gap G33, B2 disclosure #1). CNCF publishes four domain weights and no sub-competency weights. The metadata line, the Attention Budget, and the Practice Questions count all inherit this. Front matter carries the disclosure; §1 should not repeat it.

7. **"Operating system" versus "kernel" — third occurrence, still unresolved.** Chapter 1 A1 sharpened the snapshot's "shares the Operating System (OS)" to "operating system **kernel**" and flagged it for review; Chapter 2 §1 inherited the flag and was instructed to resolve it. §1 of this chapter retells the era transition and hits the phrase again. **Whatever Chapter 2 decided, match it.** If Chapter 2 has not yet resolved it, resolve it now for all three, because the reconcile pass will surface any divergence in the book's most-quoted sentence.

8. **Cluster DNS as effectively mandatory** is true, useful, and currently unsourceable — the cached snapshot lists addons as bare bullets. Either fetch `kubernetes.io/docs/concepts/cluster-administration/addons/` in Stage 2 or state it as the author's observation rather than as documented fact. Non-blocking.

9. **etcd depth.** Cached sources give "consistent and highly-available key value store" and stop. Recommendation: one plain sentence on what "consistent" buys the reader — every component reads the same answer — and nothing on quorum or Raft, which are above associate tier and unsourced. **Confirm that this is the right ceiling.**

10. **Bearings raised 10 → 13** across three checkpoints (5 + 4 + 4), per B4's "contract to exceed" instruction. Chapter total moves 37 → 40. Book headroom is 415 questions above the floor. **Confirm.**

11. **Epigraph.** Recommendation: the documentation's own line — *"Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration."* — attributed to the Kubernetes documentation. It is real, citable, on-theme, and unintelligible on first reading, which makes it a curiosity gap rather than a spoiler; §7 makes it land. If the author judges that it gives away too much of the Zenith, the fallback is Grace Hopper's *"The most dangerous phrase in the language is 'we've always done it this way'"*, which fits §1's era progression and spoils nothing.

12. **Chapter 3 introduces no commands** (`kb_tags.commands: []`). Chapter 8 owns the `kubectl` surface and Chapter 4 owns `kubectl apply`; §5's submission story is told at component altitude deliberately. **Confirm that no command belongs here** — `kubectl get nodes` is the only plausible candidate and it would need Chapter 8's kubeconfig material to be meaningful.

---

*Stage 1 complete for Chapter 3. Seven sections, three checkpoints (13 Bearings), 8 Soundings, 19 Practice Questions, 40 total. Five figures. Section numbering honors two published Chapter 2 cross-bearings (§1, §3). One blocking research gap (§5's control-plane/node communication claim) and one runner defect flagged with a mitigation already applied.*
```

---

A few things worth your attention before Stage 2:

1. **One blocking gap.** §5's whole argument — that only the API server touches etcd and that components never talk to each other directly — isn't supported by anything in `sources/`. The cached architecture page lists `control-plane-node-communication` as a related topic but it was never fetched. Without it, §5, `ch03-fig04`, one Bearings item, and most of the Zenith's force have to narrow to the weaker "API server is the front end" claim.

2. **Chapter 1 calls Kubernetes "an orchestrator."** The docs say it "eliminates the need for orchestration." Both are fine at their own altitude, but Chapter 3 is where the reader hits the seam, so I've made the sharpening a designed beat (Soundings Q8 → §1 plant → §7 payoff) rather than letting it read as the book contradicting itself.

3. **Chapter 2 shipped as `chapter-02-section-plan-no-word-budgets.md`.** `run_chapters.sh:72` slugifies the first `^#\s+` line after prepending the outline's frontmatter, and that comment block won. I wrote this outline's comments as `#--` (no space) so Chapter 3 should land correctly, but the regex still needs fixing and Chapter 2's name is now sticky via the glob at line 75 — it'll need a manual `git mv`.