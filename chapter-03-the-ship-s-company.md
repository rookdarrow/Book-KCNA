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

# Chapter 3: The Ship's Company
## *"Everyone aboard has one job, and none of them is 'be in charge'"*

**Domain Weight: ~6% of exam (authored estimate) | Complexity: Mixed | Novelty: Paradigm-shifting**

---

## Attention Budget

**Total time: ~85 minutes | Recommended: Single session if you're fresh; otherwise split after the second checkpoint**

| Section | Time | Attention Cost | Best Time to Study |
|---|---|---|---|
| §1 How the Cluster Got the Shape It Has | 11 min | Low | Anytime |
| §2 The Control Plane | 15 min | Medium | Mid-session |
| §3 Node Components in Context | 10 min | Medium | Mid-session |
| ☆ Taking Your Bearings #1 | 6 min | Medium | After a brief break |
| §4 Addons, and What Else Is Optional | 6 min | Low | Anytime |
| §5 The Only Door In | 11 min | High | Peak attention |
| ☆ Taking Your Bearings #2 | 5 min | Medium | After a brief break |
| §6 Controllers and the Control Loop | 14 min | High | Peak attention |
| ☆ Taking Your Bearings #3 | 5 min | Medium | After a brief break |
| §7 Nobody Is in Charge | 7 min | Medium | Anytime after §5 and §6 |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract or complex material — study at peak attention

*If you only have 15 minutes: read §6 and take Taking Your Bearings #3. Six later chapters retrieve §6 by name. Nothing else in this chapter is retrieved as often.*

---

> *"Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration."*
> — the Kubernetes documentation [source: k8s-docs-overview-2026-08-23]

---

## 🧭 Soundings

Before reading this chapter, try these questions. Your score determines how to approach the content. No shame in any score; the score points you at a reading strategy, nothing more. Seven of these test what you already know coming in; one is a deliberate look back at Chapter 2.

1. You have three copies of an application running and you want five. How would you make that happen?

2. It's 3 a.m. A machine holding some of your application's copies fails. Who notices, and what do they do about it?

3. Does every machine in a Kubernetes cluster run the same software?

4. On a worker machine, which component is responsible for making sure the containers described for that machine are actually running? *[retrieval: ch2]*

5. A command-line tool, an internal scheduler, and fifty machine-level agents all need to read and write the same configuration data. How many of them should be allowed to talk to the datastore directly?

6. Does Kubernetes build your container images?

7. Was Kubernetes written from scratch, or does it descend from an earlier internal system at some company?

8. "Orchestration" — is that a loose compliment people pay to container platforms, or is it a technical term with a specific meaning?

<details>
<summary>Click for answers + reading strategy</summary>

1. Most people with scripting experience answer "start two more." §6 is written for that answer.

2. Common answers: a human, woken by a pager. Also common: "something automatic." §6 tells you which one Kubernetes chose and why.

3. No. Kubernetes clusters have two kinds of machine running two different sets of software. §2 and §3 name them.

4. The kubelet. Chapter 2 taught the chain from the kubelet down through the CRI to the runtime. If that came back easily, §3 will be a review. *[retrieval: ch2]*

5. One. Most people with API-design exposure answer this correctly on instinct; §5 is about the consequences, not the rule.

6. No. Images are built elsewhere and pulled. §1 has the rest of that list.

7. It descends. Kubernetes drew on Google's internal container-orchestration experience: the Borg system, and its research successor Omega [source: k8s-history-ten-years-2026-08-23].

8. It's a technical term with a specific meaning, and the meaning is narrower than the way the industry uses the word. §1 plants it; §7 settles it.

**If you got 6+ right:** Skim, with two exceptions. Read §6 at full pace regardless of your score, because six later chapters retrieve it by name. And read §4 rather than skimming it; the optionality material scores well on intuition and still catches people on exam day.

**If you got 3–5 right:** Read at normal pace. This chapter is calibrated for you.

**If you got 0–2 right:** Read carefully, in its own session, and don't move on to Chapter 4 the same day. Chapter 1 told you that Chapters 2 and 3 carry the conceptual load everything else rests on; this is the second of the two. Nothing here is difficult. There are eight component names and one idea, and the idea is worth more than the names.

</details>

---

## Why This Chapter Matters

There is no component in Kubernetes whose job is to be in charge.

That should bother you. If you have ever built or operated a distributed system, the obvious way to make fifty machines agree on something is to put one of them in charge: a coordinator that holds the plan, hands out assignments, and tracks completion. Every workflow engine, every job scheduler, every deployment tool you have used works roughly that way. Kubernetes has no such component. You are about to meet eight components, you will go looking for the one that runs things, and you will not find it. Hold that question. It resolves in §6 and §7, and how it resolves is the most useful thing this chapter has to give you.

What you're building here isn't component recall. It's layer attribution. A practitioner who owns this chapter can be handed a symptom (Pods not starting, a Service with no endpoints, a node gone quiet) and reason about *which loop stopped closing*, instead of guessing which service to restart. Chapter 1 established that this exam measures discrimination rather than memorization. Here the discrimination is architectural: knowing not just what each piece is called but what it can and cannot do, and what has to be true for it to act at all. The component census is the vocabulary. The control loop is the grammar. The exam tests both. Practitioners get paid for the second.

The stakes are structural rather than dramatic. This chapter covers roughly six points of exam surface on this book's own judgment. CNCF and the Linux Foundation publish weights per domain, with competencies named but not individually weighted [source: cncf-kcna-curriculum-pdf-2026-08-23] [source: lf-kcna-exam-page-2026-08-23], so treat that number as an estimate the author is accountable for, not as a figure from the curriculum. What makes the chapter large isn't its exam weight. It's that six later chapters retrieve the control loop by name, and one of them, Chapter 15, is built entirely around you recognizing it somewhere unfamiliar. A reader who finishes here able to recite eight component names but unable to sketch a reconciliation loop from memory has the smaller half of what's on offer.

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Explain** why the container deployment era produced a system shaped like Kubernetes, and state three things Kubernetes deliberately does not do.
- **Name** every control-plane and node component, state its one job, and mark which two are optional and under what circumstances.
- **Trace** what happens between a submitted request and a running container, naming which component acts at each step, and which component never does.
- **Draw** a control loop from memory: desired state, current state, and the action that closes the gap, repeating forever.
- **Distinguish** orchestration in the technical sense (first do A, then B, then C) from a set of independent control processes, and explain why Kubernetes claims to eliminate the need for the first.

*You'll also stop looking for the component that's in charge, which is the single most useful habit this chapter can leave you with.*

---

## §1 — ⚪ How the Cluster Got the Shape It Has

Systems have shapes, and the shapes have reasons. Kubernetes looks the way it looks because of a specific sequence of problems the industry solved one at a time, each solution creating the conditions for the next.

*[cross-bearing: see Ch 2 §4 — the kubelet, CRI, and the container runtime chain]*

### The three deployment eras

**Traditional deployment era.** Early on, organizations ran applications on physical servers. There was no way to define resource boundaries for applications on a physical server, and this caused resource-allocation issues. If multiple applications run on one physical server, one application can take up most of the resources, and the others underperform. The available solution was to run each application on a different physical server, which did not scale, because resources sat underutilized and maintaining many physical servers was expensive [source: k8s-docs-overview-2026-08-23].

**Virtualized deployment era.** Virtualization allowed multiple Virtual Machines to run on a single physical server's CPU. Applications became isolated between VMs, which provides a level of security because the information of one application cannot be freely accessed by another. Utilization improved, hardware costs dropped, and scalability improved because an application could be added or updated easily. With virtualization you can present a set of physical resources as a cluster of disposable virtual machines. But each VM is a full machine running all the components, including its own operating system, on top of virtualized hardware [source: k8s-docs-overview-2026-08-23].

**Container deployment era.** Containers are similar to VMs, but they have relaxed isolation properties that let them share the operating system among the applications. That's why containers are considered lightweight. Like a VM, a container has its own filesystem, share of CPU, memory, process space, and more. Because they are decoupled from the underlying infrastructure, they are portable across clouds and OS distributions [source: k8s-docs-overview-2026-08-23].

That last sentence is the documentation's, and it says *operating system*. The sharper statement, that what a container shares with the host is specifically the **kernel**, is this book's, not the documentation's, and you'll see it written that way where the precision earns its keep. Treat it as our gloss on an accurate but coarse sentence, not as a quotation.

<!-- AUTHOR-REVIEW: book-level divergence — do not resolve in this chapter alone. Cached wording is "share the Operating System (OS) among the applications" (k8s-docs-overview-2026-08-23). Chapter 2 §1 (chapter-02-cargo-in-standard-crates.md:279) matches the snapshot and reinforces it at lines 1148 and 1263. Chapter 1 §Soundings A1 (chapter-01-taking-departure.md:142) sharpens to "operating system kernel" and carries its own unresolved flag at line 140. Chapter 3 now follows Chapter 2: quote the snapshot when citing, and carry the kernel-level precision as a visibly authorial sentence with no source tag. The remaining outlier is Chapter 1 — raise it there or at the reconcile pass. Practice Q2 in this chapter is keyed to the snapshot's wording, not the gloss. -->

<!-- FIGURE: ch03-fig03-deployment-eras-timeline -->
```
   TRADITIONAL              VIRTUALIZED                CONTAINER
   ───────────              ───────────                ─────────

   ┌───────────┐          ┌─────┐ ┌─────┐            ┌───┐┌───┐┌───┐
   │    App    │          │ App │ │ App │            │App││App││App│
   ├───────────┤          ├─────┤ ├─────┤            └───┘└───┘└───┘
   │    OS     │          │Guest│ │Guest│            ┌─────────────┐
   ├───────────┤          │ OS  │ │ OS  │            │  Shared OS  │
   │ Hardware  │          ├─────┴─┴─────┤            ├─────────────┤
   └───────────┘          │  Hypervisor │            │  Hardware   │
                          ├─────────────┤            └─────────────┘
   shares: nothing        │  Host OS    │
   (one app per box)      ├─────────────┤            shares: the
                          │  Hardware   │            operating system
                          └─────────────┘
                          shares: hardware
                          (own OS per VM)
```
*What changes across the eras is not the application. It's what the application shares with everything else on the machine. Read the bottom row.*

This chapter isn't re-teaching the container/VM architecture; Chapter 2 did that in detail. What matters here is the *consequence*. Once your unit of deployment is small, fast, and portable, you stop having a handful of servers with one application each and start having hundreds of interchangeable processes scattered across a pool of machines. That is a fundamentally different management problem, and it's the problem Kubernetes was built for.

*[cross-bearing: see Ch 2 §1 — the architectural container-versus-VM contrast]*

### What Kubernetes provides

The published capability list reads like marketing until you read it as a list of container-era problems, each with a name attached [source: k8s-docs-overview-2026-08-23]:

| Capability | The problem it solves |
|---|---|
| **Service discovery and load balancing** | Containers move and get new IPs; clients need a stable name. Kubernetes can expose a container using a DNS name or its own IP address, and can load balance and distribute traffic when it's high. |
| **Storage orchestration** | Containers are ephemeral; some data isn't. Kubernetes lets you automatically mount a storage system of your choice — local, public cloud, and more. |
| **Automated rollouts and rollbacks** | Updating hundreds of copies by hand is unmanageable. You describe the desired state and Kubernetes changes actual state to desired state at a controlled rate. |
| **Automatic bin packing** | Placing containers on machines by hand wastes capacity. You tell Kubernetes how much CPU and memory each container needs, and it fits containers onto nodes to make best use of resources. |
| **Self-healing** | Things fail constantly at scale. Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your health check, and doesn't advertise them to clients until they are ready to serve. |
| **Secret and configuration management** | Baking credentials into images is both a security problem and a rebuild problem. You can deploy and update secrets and application configuration without rebuilding images and without exposing secrets in your stack configuration. |
| **Batch execution** | Not every workload is a service. Kubernetes can manage batch and CI workloads, replacing containers that fail if desired. |
| **Horizontal scaling** | Demand changes. Scale up and down with a command, a UI, or automatically based on CPU usage. |
| **IPv4/IPv6 dual-stack** | Allocation of IPv4 and IPv6 addresses to Pods and Services. |
| **Designed for extensibility** | Add features to your cluster without changing upstream source code. |

Read that right-hand column again. Notice how many entries describe something that has to *keep being true* rather than something that has to *happen once*. Self-healing isn't an action; it's a standing condition. Hold that thought. It's the shape of §6.

### What Kubernetes is not

This list is more useful than the last one, and it is tested more often than people expect. Kubernetes is not a traditional, all-inclusive PaaS. Because it operates at the container level rather than the hardware level, it provides some features common to PaaS offerings (deployment, scaling, load balancing) and lets users integrate their own logging, monitoring, and alerting. But Kubernetes is not monolithic, and those default solutions are optional and pluggable. It provides the building blocks for building developer platforms while preserving user choice [source: k8s-docs-overview-2026-08-23].

Specifically, Kubernetes [source: k8s-docs-overview-2026-08-23]:

- **Does not limit the types of applications supported.** It aims to support an extremely diverse variety of workloads — stateless, stateful, data-processing. If an application can run in a container, it should run great on Kubernetes.
- **Does not deploy source code and does not build your application.** CI/CD workflows are determined by organizational culture and preferences as well as technical requirements.
- **Does not provide application-level services** — no middleware (message buses), no data-processing frameworks (Spark), no databases (MySQL), no caches, no cluster storage systems (Ceph) as built-in services. Such things can run *on* Kubernetes, or be accessed by applications running on it.
- **Does not dictate logging, monitoring, or alerting solutions.** It provides some integrations as proof of concept, and mechanisms to collect and export metrics.
- **Does not provide nor mandate a configuration language or system.** It provides a declarative API that arbitrary declarative specifications may target.
- **Does not provide nor adopt any comprehensive machine configuration, maintenance, management, or self-healing systems.**

And one more, which we are going to leave sitting here unresolved:

> 🪝 **Snag:** The documentation also says Kubernetes "is not a mere orchestration system" and that "it eliminates the need for orchestration" [source: k8s-docs-overview-2026-08-23]. The industry uses "orchestration" loosely, as a compliment, and this book used it that way in Chapter 1. The word has a precise technical meaning, and Kubernetes explicitly rejects it. We'll settle this in §7.

*[cross-bearing: see Ch 3 §7 — the orchestration disclaimer, resolved]*

That Snag deserves a moment of honesty, because it's the book correcting its own earlier wording rather than correcting you. Chapter 1 told you that "Kubernetes is an orchestrator — it decides what should run where." At orientation altitude, that's the right answer to the question being asked (orchestrator versus runtime), and it's how practically everyone in the industry talks. But it's the loose sense of the word. The precise sense is the one on the exam, and sharpening it is §7's job.

### Where it came from

On June 6th, 2014, the first commit of Kubernetes was pushed to GitHub: 250 files and 47,501 lines of Go, bash, and markdown [source: k8s-history-ten-years-2026-08-23]. The project did not appear from nothing. Kubernetes drew on Google's internal container-orchestration experience with the Borg system and its research successor Omega, and was written in Go [source: k8s-history-ten-years-2026-08-23]. It arrived into a container moment that Docker had opened the year before [source: k8s-history-ten-years-2026-08-23]. A popular, portable unit of deployment created the demand for something to manage those units at scale.

Kubernetes was announced publicly at DockerCon in June 2014, reached v1.0 in July 2015, and was donated by Google to the newly formed Cloud Native Computing Foundation as its first project [source: k8s-history-ten-years-2026-08-23]. CNCF is part of the nonprofit Linux Foundation [source: cncf-who-we-are-2026-08-23].

The name comes from the Greek word for helmsman or pilot; "K8s" is the numeronym, with eight letters between the K and the s [source: k8s-history-ten-years-2026-08-23]. The brand you're reading did not pick the maritime register to be cute about it. The subject arrived that way.

> 🔭 **Closer Look:** Borg and Omega were two different projects, not one renamed. Borg was the production system; Omega is described as its research successor [source: k8s-history-ten-years-2026-08-23]. Kubernetes inherited from both. This is deeper than the exam requires.

*[cross-bearing: see Ch 17 §1 — the CNCF, its governance, and the cloud native definition]*

---

## §2 — ⚪ The Control Plane

Start with the shape of the thing. A ship's company sorts itself before it works: some stations keep the reckoning, others keep the deck.

A Kubernetes cluster consists of a control plane plus a set of worker machines, called nodes, that run containerized applications. Every cluster needs at least one worker node in order to run Pods. The worker nodes host the Pods that are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault tolerance and high availability [source: k8s-docs-cluster-architecture-2026-08-23].

So: two kinds of machine, two sets of software. That answers Soundings question 3, and it's the first thing to fix in your head, because every component name you're about to learn hangs off it.

<!-- AUTHOR-REVIEW: BLOCKING — snapshot harvest, affects every -2026-08-24 tag in this chapter. Stage 2 fetched five new snapshots for ch-03 and recorded them in `.pipeline-state/ch-03/research-manifest.md`, but `harvest_research_snapshots()` never wrote them into `sources/` (ls sources/ returns 87 files, all dated -2026-08-23). The five are: k8s-docs-control-plane-node-communication-2026-08-24, k8s-docs-cluster-addons-2026-08-24, k8s-docs-etcd-access-control-2026-08-24, k8s-docs-dns-cluster-addon-2026-08-24, etcd-io-what-is-etcd-2026-08-24. Re-run the harvest, or hand-write the five files from the manifest's fenced blocks, before release. No re-fetch is required — the content is already in the manifest. Until then, every -2026-08-24 tag below dangles. -->

<!-- FIGURE: ch03-fig01-control-plane-and-node-components -->
```
┌─── CONTROL PLANE ────────────────────────────────────────────┐
│                                                              │
│   ┌────────────────┐   ┌────────┐   ┌──────────────────┐     │
│   │ kube-apiserver │   │  etcd  │   │  kube-scheduler  │     │
│   └────────────────┘   └────────┘   └──────────────────┘     │
│                                                              │
│   ┌─────────────────────────┐   ╭─────────────────────────╮  │
│   │ kube-controller-manager │   ╎ cloud-controller-manager╎  │
│   └─────────────────────────┘   ╰─────────────────────────╯  │
└──────────────────────────────────────────────────────────────┘

┌─── NODE ─────────────────────────┐  ┌─── NODE ──────────────┐
│                                  │  │                       │
│  ┌─────────┐  ╭────────────╮     │  │  ┌─────────┐  ╭─────  │
│  │ kubelet │  ╎ kube-proxy ╎     │  │  │ kubelet │  ╎ kube-  ...
│  └─────────┘  ╰────────────╯     │  │  └─────────┘  ╰─────  │
│  ┌───────────────────┐           │  │  ┌──────────────      │
│  │ container runtime │           │  │  │ container run ...
│  └───────────────────┘           │  │  └──────────────      │
└──────────────────────────────────┘  └───────────────────────┘

  ┌───┐ solid border = always present
  ╭╌╌╌╮ dashed border = OPTIONAL (see §4)
```
*The whole census on one page. Two regions, eight components, two of them dashed. The dashes are worth as many exam points as the names.*

Now the five components of the control plane. The control plane's components make global decisions about the cluster — scheduling, for example — as well as detecting and responding to cluster events, such as starting up a new Pod when a controller's declared replica count is unsatisfied [source: k8s-docs-cluster-architecture-2026-08-23].

### kube-apiserver

The API server is the component of the control plane that exposes the Kubernetes API. **The API server is the front end for the Kubernetes control plane.** kube-apiserver is designed to scale horizontally: it scales by deploying more instances. You can run several instances and balance traffic between them [source: k8s-docs-cluster-architecture-2026-08-23]. In the components summary the docs describe it plainly as the core component server that exposes the Kubernetes HTTP API [source: k8s-docs-components-2026-08-23].

That "front end" phrase is doing enormous work, and §5 is devoted to unpacking it. For now: everything comes in through here.

*[cross-bearing: see Ch 3 §5 — what "front end" actually implies about the cluster's shape]*

### etcd

Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data. If your Kubernetes cluster uses etcd as its backing store, make sure you have a back up plan for the data [source: k8s-docs-cluster-architecture-2026-08-23].

That's the whole official description, and it's terser than it looks. Two words deserve unpacking, and what follows is this book's explanation of them rather than more documentation. *"All cluster data"* means all of it: every object you created, every object the system created, every piece of state the cluster knows about. And *"consistent"* is the property the rest of the architecture leans on. In plain terms, it's what lets independent components reading the same shared state work from the same picture of the world rather than from private, drifting copies. Take that as the gloss it is; the formal guarantees are etcd's own subject, not this chapter's.

> ⚓ **Worth Securing:** etcd is where the cluster lives. It is the backing store for *all* cluster data [source: k8s-docs-cluster-architecture-2026-08-23], which means the other components can be killed, restarted, or replaced and rebuild their working picture from what etcd holds. etcd itself holds the thing that cannot be rebuilt from anywhere else. Losing it is not something you recover from by restarting a process. It's something you recover from by having taken a backup, which is why the documentation's one piece of unsolicited advice about etcd is "make sure you have a back up plan."

*[cross-bearing: see Ch 8 — etcd backup and restore in practice]*
*[cross-bearing: see Ch 12 — Secrets live in etcd, which is why encryption at rest is a separate decision you have to make]*

### kube-scheduler

Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on. Factors taken into account for scheduling decisions include individual and collective resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and deadlines [source: k8s-docs-cluster-architecture-2026-08-23].

One component boundary needs stating precisely right now, because it heads off a mistake that costs points: **the scheduler selects a node and records that choice. It does not start anything.** The scheduler notifies the API server about its decision, in a process called binding [source: k8s-docs-kube-scheduler-2026-08-23]. The container that eventually runs is started by the kubelet on the chosen node. The scheduler makes a decision; something else acts on it. That split will look familiar by the end of §6.

*[cross-bearing: see Ch 7 — how the scheduler actually chooses, in detail]*

### kube-controller-manager

Control plane component that runs controller processes. Logically, each controller is a separate process, but to reduce complexity, they are all compiled into a single binary and run in a single process. There are many different types of controllers — for example: the Node controller (noticing and responding when nodes go down); the Job controller (watching for Job objects that represent one-off tasks, then creating Pods to run those tasks to completion); the EndpointSlice controller (populating EndpointSlice objects to provide a link between Services and Pods); and the ServiceAccount controller (creating default ServiceAccounts for new namespaces) [source: k8s-docs-cluster-architecture-2026-08-23].

> ⚠ **Navigational Hazards:** Read that second sentence twice. *Logically*, each controller is a separate process. That's the conceptual model. *Actually*, they are all compiled into a single binary and run in a single process. This is a single sentence in the documentation and it reads like a trivial implementation note, which is exactly why it gets tested. Candidates who skimmed it will tell you confidently that there's one process per controller, or one container per controller, or one Pod per controller. All three are wrong for the same reason: there is no per-controller unit of any kind. One binary. One process. Many logical controllers inside it.

### cloud-controller-manager

A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster. It runs only controllers that are specific to your cloud provider. **If you are running Kubernetes on your own premises, or in a learning environment inside your own PC, the cluster does not have a cloud controller manager** [source: k8s-docs-cluster-architecture-2026-08-23].

That last sentence is the one to hold onto. This component is genuinely optional. Not "optional but everyone runs it" — *absent* from an entire class of real clusters, including the one on your laptop. §4 comes back to it.

> 🪢 **Mnemonic:** Don't reach for an acronym here; the structure *is* the memory hook. Five components, and they sort themselves. **Three named `kube-`** (apiserver, scheduler, controller-manager) are the core Kubernetes control-plane processes. **One named `cloud-`** (cloud-controller-manager) is the optional bridge to somebody else's infrastructure. **One with no prefix at all**, etcd, because it isn't Kubernetes software; it's a general-purpose datastore that Kubernetes uses. If you can reconstruct that sorting rule, you can reconstruct the list.

---

## §3 — ⚪ Node Components in Context

*[cross-bearing: see Ch 2 §4 — the kubelet, CRI, and container runtime chain, which this section places in its architectural context]*

Node components run on every node, maintaining running Pods and providing the Kubernetes runtime environment [source: k8s-docs-components-2026-08-23]. Three of them. Keep that framing sentence: the node's collective job is to *maintain* running Pods, not to start them once and stand down.

### kubelet

An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod. The kubelet takes a set of PodSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy. **The kubelet doesn't manage containers which were not created by Kubernetes** [source: k8s-docs-cluster-architecture-2026-08-23].

A PodSpec, for now, is simply the description of what containers should run. Chapter 4 gives it a proper treatment.

*[cross-bearing: see Ch 5 — Pods, PodSpecs, and what "running and healthy" means precisely]*

> ⚓ **Worth Securing:** That last clause has practical teeth. If you SSH to a node and start a container by hand with the container runtime directly, the kubelet does not manage it [source: k8s-docs-cluster-architecture-2026-08-23]. It won't restart it, won't maintain it, won't clean it up. Whatever the cluster knows about that node, the hand-started container isn't part of it. This cuts both ways: it's why hand-started containers on a node don't turn up through `kubectl`, and it's why node-level debugging needs a node-level tool rather than the Kubernetes API.

*[cross-bearing: see Ch 13 §5 — `crictl`, and why a node-level tool exists below the Kubernetes API]*

### kube-proxy (optional)

kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept. kube-proxy maintains network rules on nodes. These network rules allow network communication to your Pods from network sessions inside or outside of your cluster. **If you use a network plugin that implements packet forwarding for Services by itself, and providing equivalent behavior to kube-proxy, then you do not need to run kube-proxy on the nodes in your cluster** [source: k8s-docs-cluster-architecture-2026-08-23].

Note the precise hedge: it implements *part* of the Service concept. Service is a Kubernetes object with its own chapter; kube-proxy is the node-level machinery that makes some of it work. Note the optionality condition too, because "optional" here has a specific trigger, something else doing the same job, not a general "you can skip it if you like."

*[cross-bearing: see Ch 9 — Services, and how kube-proxy implements them]*

### Container runtime

A fundamental component that empowers Kubernetes to run containers effectively. It is responsible for managing the execution and lifecycle of containers within the Kubernetes environment. Kubernetes supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI (Container Runtime Interface) [source: k8s-docs-cluster-architecture-2026-08-23].

You already own this one. Chapter 2 walked the chain: the kubelet speaks CRI, the CRI implementation (containerd, CRI-O) manages container lifecycle, and below that sits the low-level runtime that actually creates the process. What §3 adds is *position*. The container runtime is the one node component that is not Kubernetes software at all. It's a separate project, swappable, and not authored by the Kubernetes project: Kubernetes defines the interface and accepts any implementation of it [source: k8s-docs-cluster-architecture-2026-08-23]. That is the same architectural instinct you saw with etcd. Where a good general-purpose component already exists, Kubernetes defines an interface and uses it rather than reimplementing it.

That's the census. Eight components, and here it is in one place.

> **★ Fixed Point**
>
> **Control plane:** kube-apiserver, etcd, kube-scheduler, kube-controller-manager, and cloud-controller-manager *(optional — absent on premises and on your laptop)*.
>
> **Node** (on every node): kubelet, kube-proxy *(optional — unnecessary if a network plugin provides equivalent packet forwarding)*, and the container runtime.
>
> Eight names. Two of them optional, for two different reasons. One of them — the container runtime — is not Kubernetes software. [source: k8s-docs-components-2026-08-23] [source: k8s-docs-cluster-architecture-2026-08-23]

> **Dead Reckoning:** kube-apiserver runs on the control plane and exposes the Kubernetes HTTP API. etcd runs on the control plane and stores all cluster data. kube-scheduler runs on the control plane and assigns unscheduled Pods to nodes. kube-controller-manager runs on the control plane and runs controller processes in a single binary. cloud-controller-manager runs on the control plane when a cloud provider is involved and integrates with that provider's API. kubelet runs on every node and ensures the containers described for that node are running. kube-proxy runs on every node unless something else does its job, and maintains node network rules for Services. The container runtime runs on every node and executes containers. [source: k8s-docs-components-2026-08-23] [source: k8s-docs-cluster-architecture-2026-08-23]

---

## ☆ Taking Your Bearings: The Ship's Company

Five questions. One of them reaches back to Chapter 2.

**Q1.** ⚪ Which of the following components runs on *every node* rather than on the control plane?

A) kube-proxy
B) kube-scheduler
C) etcd
D) cloud-controller-manager

**Q2.** ⚪ "Watches for newly created Pods with no assigned node, and selects a node for them to run on." Which component?

A) kube-controller-manager
B) kubelet
C) kube-apiserver
D) kube-scheduler

**Q3.** 🔵 How does kube-controller-manager run its controllers?

A) All controllers compiled into a single binary, running in a single process
B) One operating-system process per controller, supervised by a parent process
C) One container per controller, all within a single Pod
D) One Pod per controller, all in the kube-system namespace

**Q4.** 🔵 What does etcd store?

A) Only the objects you explicitly created
B) All cluster data
C) Only Pod definitions and node registrations
D) Cluster data plus cached container image layers

**Q5.** 🟡 *[retrieval: ch2]* A Pod has been assigned to a node and its containers need to start. Which node component causes a container to actually start, and through what interface does it do so?

A) kube-proxy, via the iptables rules it maintains on the node
B) kube-scheduler, by connecting directly to that node's container runtime
C) The container runtime, by polling the API server for its own assignments
D) The kubelet, via the Container Runtime Interface (CRI)

---

**Answers with Explanations:**

**Q1 — A.** kube-proxy is a node component; it runs on each node in the cluster, maintaining network rules [source: k8s-docs-cluster-architecture-2026-08-23].
- **B is wrong** — kube-scheduler is a control plane component. It's a common slip because scheduling *results* in something happening on a node, but the scheduler itself lives on the control plane.
- **C is wrong** — etcd is a control plane component and the backing store for all cluster data.
- **D is wrong** — cloud-controller-manager is a control plane component, and an optional one at that.

**Q2 — D.** That is the kube-scheduler's published description, near-verbatim [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — the controller-manager runs controllers. Several of them create Pods, but none of them chooses which node a Pod lands on.
- **B is wrong** — the kubelet acts *after* a node has been chosen, ensuring the containers described for its own node are running. It doesn't select nodes.
- **C is wrong** — the API server serves the API. It stores and serves the fact that a Pod has no node yet; it doesn't decide the node.

**Q3 — A.** Logically each controller is a separate process, but to reduce complexity they are all compiled into a single binary and run in a single process [source: k8s-docs-cluster-architecture-2026-08-23].
- **B is wrong** — and it's wrong in the most tempting way, because the documentation's own sentence begins "Logically, each controller is a separate process." That word *logically* is the whole question.
- **C is wrong** for the same reason B is: there is no per-controller unit of any kind, container or otherwise. The unit is the controller-manager itself, and every controller lives inside it.
- **D is wrong** for that same reason. Whatever the controller-manager happens to be packaged as in your cluster, there is *one* of it, not one per controller.

**Q4 — B.** etcd is the backing store for all cluster data [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — the cluster creates plenty of objects you didn't (default ServiceAccounts, EndpointSlices, Leases), and those are stored there too.
- **C is wrong** — a subset answer. Believing etcd holds only *some* of the state is the specific misconception that leads people astray later, when Chapter 12 asks why Secret encryption at rest is a separate configuration decision.
- **D is wrong** — image layers live in a registry and, once pulled, are cached on node disk by the kubelet and runtime [source: k8s-docs-images-2026-08-23]. etcd stores API objects, not binary payloads.

**Q5 — D.** *[retrieval: ch2]* The kubelet ensures the containers described in its PodSpecs are running [source: k8s-docs-cluster-architecture-2026-08-23], and it reaches the runtime through the Container Runtime Interface, the extension point Kubernetes defines for alternative container runtimes [source: k8s-docs-extending-kubernetes-2026-08-23].
- **A is wrong** — kube-proxy handles network rules for Services. It has nothing to do with starting containers.
- **B is wrong** — the scheduler selects a node and records the decision. It never contacts a node's runtime. This is the highest-value wrong answer on the page, because the belief behind it ("the scheduler places the Pod on the node, so it must talk to the node") is genuinely widespread.
- **C is wrong** — the container runtime doesn't poll the API server. It sits below the kubelet and is driven by it through CRI. The runtime doesn't know Kubernetes exists.

**If you scored 5/5:** The census is yours. Move straight on; §4 is short.

**If you scored 3–4:** Solid. Review the ones you missed, particularly if Q3 or Q5 was among them, and continue.

**If you scored 0–2:** Go back to §2 and §3 and rebuild the census from the ★ Fixed Point, then re-read the Dead Reckoning block. Ten minutes. The rest of the chapter assumes you can place any component on the right side of the control-plane/node line without thinking about it.

**Checkpoint: You've Now Mastered**
✓ The control-plane/node split, and what each side is for
✓ All eight components and the one job each holds
✓ Which two are optional, and the fact that the reasons differ
✓ That the scheduler decides and the kubelet acts — a split you'll see again

🗺️ **Chapter 3 · Voyage Progress:** census complete → now the arrangement → then the loop

---

## §4 — 🔵 Addons, and What Else Is Optional

This is the shortest section in the chapter and it exists for one sentence at the end of it.

### Addons

Addons extend the functionality of Kubernetes. The published examples are: **DNS**, for cluster-wide DNS resolution; **Web UI (Dashboard)**, for cluster management via a web interface; **Container Resource Monitoring**, for collecting and storing container metrics; and **Cluster-level Logging**, for saving container logs to a central log store [source: k8s-docs-components-2026-08-23] [source: k8s-docs-cluster-addons-2026-08-24].

Note the word *extend*. Addons are not components in the sense that the eight names in §3 are components. They run *on* the cluster rather than constituting it. A cluster with none of them installed is still a cluster.

### Three kinds of optional

You have now met eight components and four addons. **Two of those twelve carry the word "optional" in the documentation itself:** kube-proxy and cloud-controller-manager [source: k8s-docs-components-2026-08-23]. They carry it for two genuinely different reasons. The addons are a third kind of optional, but that framing is this book's rather than the documentation's: the docs say addons *extend* the cluster, and never apply the word "optional" to them.

| What | Why it's optional | Whose word |
|---|---|---|
| **kube-proxy** | Because something else can do its job. If your network plugin implements equivalent packet forwarding for Services, kube-proxy is redundant [source: k8s-docs-cluster-architecture-2026-08-23]. | The documentation's |
| **cloud-controller-manager** | Because there may be no cloud to talk to. On premises or on your laptop, the cluster simply does not have one [source: k8s-docs-cluster-architecture-2026-08-23]. | The documentation's |
| **Addons** | Because they extend rather than constitute [source: k8s-docs-components-2026-08-23]. The cluster is a cluster without them. | This book's framing |

> ⚠ **Navigational Hazards:** Two very common wrong beliefs live here, and they're both cheap points on exam day.
>
> **"kube-proxy runs on every node, always."** The documentation says node components run on every node, then marks kube-proxy optional in the same breath. Both are true: *when it runs, it runs on every node*, but it may not run at all, if a network plugin does the same work.
>
> **"Every cluster has a cloud-controller-manager."** No. Every cluster on a cloud provider that integrates one does. On premises, or on a laptop, that component is simply absent.
>
> The shared lesson is duller and more valuable than either fact: **read the word "optional" when the documentation prints it.** It's printed rarely and it's printed deliberately, on exactly two of the eight components.

### Cluster DNS, and the pattern to name

Cluster DNS is the honest illustration. It is, formally, an addon: a cluster extension, not a control-plane or node component. It is also described as a built-in Kubernetes service, launched automatically by the addon manager [source: k8s-docs-dns-cluster-addon-2026-08-24]. That is why, in the author's experience of real clusters, you will almost always find it present. Services are addressed by name, and Pods expect to be able to resolve those names.

That second half is an observation, not a documented claim. Hold the two apart: *launched automatically where the addon manager runs* is sourced; *practically universal* is the author's report.

Which brings us to the sentence this section exists for.

> ⚓ **Worth Securing — the absent-component pattern.** An object can exist while nothing at all happens, if the component that would act on it is absent. The object is real; it's stored; `kubectl get` will show it to you. But an object is a *description*, and descriptions don't do anything by themselves. Something has to be watching for it and willing to act. Remember the phrase: **an object without its component does nothing.** You're going to meet it four more times in this book, and each time it will look like a completely different problem until you recognize it.

*[cross-bearing: see Ch 9 — CoreDNS as the cluster DNS addon, and the Service DNS records it serves]*
*[cross-bearing: see Ch 10 — an Ingress with no Ingress controller does nothing at all: the same pattern, first recurrence]*
*[cross-bearing: see Ch 13 — `kubectl top` with no metrics-server installed]*
*[cross-bearing: see Ch 17 — VPA is an add-on and is not shipped by default]*

---

## §5 — 🔵 The Only Door In

You have the census. Now the arrangement, because eight components in a list is a vocabulary, and eight components with a shape is an architecture.

Go back to one phrase from §2: **the API server is the front end for the Kubernetes control plane** [source: k8s-docs-cluster-architecture-2026-08-23]. Add the other fact you already have: etcd is the backing store for all cluster data [source: k8s-docs-cluster-architecture-2026-08-23]. Add a third, from the API-communication documentation: Kubernetes has a hub-and-spoke API pattern. All API usage from nodes and the Pods they run terminates at the API server, and none of the other control-plane components are designed to expose remote services [source: k8s-docs-control-plane-node-communication-2026-08-24]. And add one more, from the controllers documentation: a controller "might carry the action out itself; more commonly, in Kubernetes, a controller will send messages to the API server that have useful side effects" [source: k8s-docs-controllers-2026-08-23].

Put those together and a shape appears. Not a chain of command. A chart table: one surface everyone works from, and no orders issued across it.

<!-- FIGURE: ch03-fig04-request-path-through-apiserver -->
```
    kubectl          kube-scheduler       kube-controller-manager
       │                    │                        │
       │                    │                        │
       └──────────┐         │         ┌──────────────┘
                  ▼         ▼         ▼
              ┌───────────────────────────┐
              │      kube-apiserver       │
              └───────────────────────────┘
                  ▲         │         ▲
       ┌──────────┘         │         └──────────────┐
       │                    ▼                        │
       │              ┌──────────┐                   │
   kubelet            │   etcd   │               kubelet
   (node A)           └──────────┘               (node B)
```
*The state path. Every arrow terminates at the API server, and the API server is the one component with an edge to etcd. Now look for the arrow that isn't drawn: there is none between any two of the surrounding components.*

<!-- AUTHOR-REVIEW: the prior draft carried a BLOCKING note here asking Stage 2 to fetch kubernetes.io/docs/concepts/architecture/control-plane-node-communication/. Stage 2 DID fetch it (research-manifest A1); the note was stale and has been removed. Two real qualifications survive the fetch and are now reflected in the prose above and below: (1) "only the API server talks to etcd" is sourced as a RECOMMENDATION — A3's wording is "ideally only the API server should have access to it" — not as an invariant, so the text no longer states it absolutely; (2) A1 documents outbound API-server→kubelet paths (logs, attach, port-forward) that this figure does not draw, so the figure and §5 are now explicitly scoped to the state/API path. Do not restore the absolute phrasing. -->

### What follows from a hub

Consider what has to be true for that picture to work.

Every actor in the cluster interacts with the same front end: the CLI you type into, the scheduler making placement decisions, the controller-manager running its many controllers, every kubelet on every node. None of them keeps its own copy of the truth. None of them reaches around the front end to instruct another component. They all read from and write to one place.

The datastore behind that front end deserves one precise sentence, because the precision matters in Chapter 12. The API server is the component that reads and writes etcd. Access to etcd is equivalent to root permission in the cluster, so ideally only the API server should have access to it [source: k8s-docs-etcd-access-control-2026-08-24]. Read that as what it is: a strong recommendation with a security reason behind it, not a law of physics. Anything else you give etcd access to, you have given root.

One qualification, and it matters later. The hub describes how *state* moves. Everything that reads or writes the cluster's state does so through the API server. It is not a claim that no connection ever runs outward. The API server does open connections to kubelets: that is how fetching Pod logs, attaching to a running container, and port-forwarding work [source: k8s-docs-control-plane-node-communication-2026-08-24]. Those paths carry a session, not an instruction. Nothing traveling on them tells a kubelet what ought to be running.

*[cross-bearing: see Ch 13 — the debugging commands that ride those outbound paths]*

Now consider what the hub means for two components that appear to cooperate. When the scheduler assigns a Pod to a node and the kubelet on that node starts the containers, it *looks* like a handoff. It looks like the scheduler told the kubelet to do something. It didn't. The scheduler recorded a decision. The kubelet, independently, was watching for exactly that kind of record, saw it, and acted. Neither one sent the other anything.

> ⚓ **Worth Securing:** The coordination mechanism in Kubernetes is **watching, not telling.** Components don't send each other instructions. They observe shared state and act on what they see. That single sentence explains most of what looks mysterious about Kubernetes' behavior, and it's the sentence Chapter 15 will retrieve when a controller called Argo CD watches a Git repository that sits outside the cluster [source: argocd-overview-2026-08-23]: the same architecture, with a different thing in the hub position.

*[cross-bearing: see Ch 15 — the same shape, with a Git repository where etcd sits here]*

### The submission story

Concretely, at component altitude. You submit a request describing something that should exist. (Chapter 4 covers what that description looks like and how you write it; the mechanics matter and they're that chapter's to teach.)

1. The request arrives at the API server. It is validated and persisted. Nothing is running yet. Nothing has been "launched."
2. From that moment, the description is simply part of the cluster's state, visible to anything watching.
3. The scheduler, which watches for Pods with no assigned node, notices one and selects a node. It records that selection back through the API server [source: k8s-docs-kube-scheduler-2026-08-23].
4. The kubelet on that node, which watches for Pods assigned to it, notices and starts the containers through the container runtime.
5. Status flows back the same way, through the API server, into etcd, where anything watching can see it.

Read the verbs. *Notices.* *Selects.* *Records.* *Notices.* At no point does one component instruct another. Each one independently observes a state it cares about, does its own job, and writes the result somewhere everyone can see it.

> 🔭 **Closer Look:** Doesn't a single front end become a bottleneck? The documented answer is that kube-apiserver is designed to scale horizontally: you run several instances and balance traffic between them [source: k8s-docs-cluster-architecture-2026-08-23]. A hub with N interchangeable instances behind a load balancer is architecturally still one door, and operationally is not one machine. This is deeper than the exam requires.

*[cross-bearing: see Ch 8 — the authentication, authorization, and admission gates a request actually passes through on its way in]*
*[cross-bearing: see Ch 4 — how you write the description that gets submitted]*

---

## ☆ Taking Your Bearings: Arrangement and Optionality

Four questions.

**Q1.** 🔵 Under what condition is kube-proxy unnecessary on your nodes?

A) When the cluster has only a single node and no cross-node traffic
B) Never — kube-proxy is a required node component in every cluster
C) When your network plugin implements packet forwarding for Services itself
D) When you have not created any Services in the cluster yet

**Q2.** 🔵 You have three clusters: one on a managed cloud provider, one in your company's own data center, and one running on your laptop for learning. In which of them does a cloud-controller-manager run?

A) All three, since every cluster needs one to manage its infrastructure
B) The managed cloud cluster only
C) The managed cloud cluster and the data center cluster
D) All three, but on the laptop and in the data center it runs with no provider configured

**Q3.** 🔵 Cluster DNS is described in the documentation as an addon rather than a component. What follows from that classification?

A) It cannot be used in production clusters
B) It runs on the control plane rather than on the nodes
C) It is required on every cluster and is simply categorized separately
D) It extends the cluster's functionality rather than constituting the cluster

**Q4.** 🟡 When kube-scheduler assigns a Pod to a node and the kubelet on that node then starts the Pod's containers, what has passed between the scheduler and the kubelet?

A) A direct gRPC call from the scheduler to the kubelet on the chosen node
B) An instruction the scheduler wrote straight into etcd, which the kubelet then read
C) Nothing directly — the scheduler recorded its decision through the API server, and the kubelet independently observed it
D) A message routed by kube-proxy from the control plane to the chosen node

---

**Answers with Explanations:**

**Q1 — C.** If you use a network plugin that implements packet forwarding for Services by itself, providing equivalent behavior to kube-proxy, you do not need to run kube-proxy [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — cluster size has nothing to do with it. A single-node cluster still needs Service networking to work.
- **B is wrong** — the documentation labels kube-proxy optional explicitly. This is trap #1 in this chapter's list, and it catches people precisely because "runs on each node" and "optional" sit two sentences apart.
- **D is wrong** — and instructively so. The optionality has nothing to do with your usage patterns. It's about whether *something else already does the job*.

**Q2 — B.** If you are running Kubernetes on your own premises, or in a learning environment inside your own PC, the cluster does not have a cloud controller manager [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — this is the misconception itself. The component exists to link a cluster to a cloud provider's API; with no cloud provider, there is nothing to link.
- **C is wrong** — a data center cluster running on your own premises is exactly the case the documentation names as *not* having one.
- **D is wrong**, and it's the most interesting wrong answer here. The component isn't present-but-idle; it is absent. An idle-but-present component would still turn up in a component listing on that cluster. This one doesn't.

**Q3 — D.** Addons extend the functionality of Kubernetes [source: k8s-docs-components-2026-08-23] [source: k8s-docs-cluster-addons-2026-08-24].
- **A is wrong** — addons are entirely production-appropriate. Cluster DNS in particular is launched automatically by the addon manager [source: k8s-docs-dns-cluster-addon-2026-08-24].
- **B is wrong** — the addon/component distinction is about role, not placement. Addons run as ordinary workloads on the cluster.
- **C is wrong** — and this is the useful confusion to clear up. Something can be *near-universal in practice* and still *not part of the cluster's definition*. The gap between those two is exactly where the absent-component pattern lives.

**Q4 — C.** The scheduler notifies the API server of its decision [source: k8s-docs-kube-scheduler-2026-08-23]; the kubelet watches the API server and acts on what it sees. Coordination in Kubernetes is watching, not telling.
- **A is wrong** — this is the most natural assumption in the whole chapter and it's the one to unlearn. It's how you'd build it. It's not how it's built: none of the other control-plane components are designed to expose remote services [source: k8s-docs-control-plane-node-communication-2026-08-24]. Note the precise claim — not that no connection ever exists between the control plane and a node, but that no component *directs* another.
- **B is wrong** — the API server is the component that reads and writes etcd, and everything else goes through it [source: k8s-docs-etcd-access-control-2026-08-24].
- **D is wrong** — kube-proxy maintains network rules for Services. It is not a message bus for control-plane traffic.

> **Design note:** Q4 is the integrative item, and the one that most rewards having actually read §5 rather than skimmed it. If you got it right by reasoning rather than recall, you have the chapter's second-most-important idea.

**If you scored 4/4:** You have the arrangement. §6 is the payoff.

**If you scored 3:** Solid. If Q4 was the one you missed, that's the one to go back for.

**If you scored 0–2:** Re-read §5, particularly "The submission story," and look again at the figure, specifically at the arrow that isn't drawn. Then re-read the ⚠ Navigational Hazards in §4. Both traps in this checkpoint turn on the word "optional," and both are cheap points on exam day.

**Checkpoint: You've Now Mastered**
✓ What "optional" means for each of the three optional things — and whose word it is in each case
✓ The addon/component distinction, and the absent-component pattern
✓ The hub arrangement: state moves through the API server, and the API server is what reaches etcd
✓ That apparent cooperation between components is independent observation of shared state

🌊 **Chapter 3 · Voyage Progress:** census complete → arrangement complete → now the loop

---

## §6 — 🔵 Controllers and the Control Loop

This is the section the rest of the book leans on. If you read one section of this chapter at full attention, read this one.

### Start where the documentation starts

In robotics and automation, a control loop is a non-terminating loop that regulates the state of a system. Here is one example: a thermostat in a room. When you set the temperature, that's telling the thermostat about your **desired state**. The actual room temperature is the **current state**. The thermostat acts to bring the current state closer to the desired state, by turning equipment on or off [source: k8s-docs-controllers-2026-08-23].

Sit with how ordinary that is. A thermostat doesn't execute a heating plan. It doesn't calculate that reaching 20°C will require 14 minutes of furnace time and then run the furnace for 14 minutes. It compares two numbers and acts on the difference, then does it again, and again, forever. It never finishes. If someone opens a window, the thermostat doesn't need to be told; the gap widens and it acts. If someone lights a fire, same story in the other direction. Nobody wrote a rule about windows or fires.

**In Kubernetes, controllers are control loops that watch the state of your cluster, then make or request changes where needed. Each controller tries to move the current cluster state closer to the desired state** [source: k8s-docs-controllers-2026-08-23].

<!-- FIGURE: ch03-fig02-control-loop-desired-vs-current -->
```
              ┌──────────────────┐
       ┌─────▶│  DESIRED STATE   │──────┐
       │      └──────────────────┘      │
       │                                ▼
  ┌─────────┐                     ┌──────────┐
  │ CURRENT │◀────────────────────│ COMPARE  │
  │  STATE  │                     └──────────┘
  └─────────┘                           │
       ▲                                ▼
       │      ┌──────────────────┐      │
       └──────│  ACT TO CLOSE    │◀─────┘
              │     THE GAP      │
              └──────────────────┘

        no start.  no end.  no exit condition.
```
*Notice there is no entry arrow and no terminus. A loop drawn with a beginning teaches the wrong thing: this one was already running before your request arrived and will still be running after it's satisfied.*

### The controller pattern, precisely

A controller tracks at least one Kubernetes resource type. Those objects carry a field that represents the desired state, and the controller for that resource is responsible for making the current state come closer to it. The controller might carry the action out itself; more commonly, in Kubernetes, a controller will send messages to the API server that have useful side effects [source: k8s-docs-controllers-2026-08-23].

Read that last clause carefully, because it is the distinction most people get wrong.

**Control via API server.** The Job controller is the documentation's own example of a built-in controller. A Job is a Kubernetes resource that runs a Pod, or perhaps several Pods, to carry out a task and then stop. When the Job controller sees a new task it makes sure that, somewhere in your cluster, the kubelets on a set of Nodes are running the right number of Pods to get the work done. **The Job controller does not run any Pods or containers itself. Instead, the Job controller tells the API server to create or remove Pods. Other components in the control plane act on the new information** — there are new Pods to schedule and run — and eventually the work is done [source: k8s-docs-controllers-2026-08-23].

(The Job *resource*, how you write one and when to reach for it, is Chapter 6's material. We're using it here only because it's the documentation's own chosen example of a controller, and swapping in a different one would cost precision for no gain.)

> 🪝 **Snag:** "The controller does the work" is the intuitive reading and it's wrong. A controller almost never touches a container. It writes something down. Then a different component, one that has never heard of this controller, notices what was written and acts. If you take one habit from this section, take this one: when something happens in Kubernetes, ask *which component actually performed the action*, and expect the answer to be different from *which controller wanted it*.

**Direct control.** The less common shape. Some controllers need to make changes to things outside your cluster. If you use a control loop to make sure there are enough Nodes in your cluster, that controller needs something outside the current cluster to set up new Nodes. Controllers that interact with external state find their desired state from the API server, then communicate directly with an external system to bring the current state closer in line [source: k8s-docs-controllers-2026-08-23].

Note what's the same and what's different. The loop is identical: desired state read from the API server, current state observed, act to close the gap. Only the *direction of the action* changes: inward through the API server in the common case, outward to some external system in the uncommon one.

Controllers also update the objects that configure them. Once the work is done for a Job, the Job controller updates that Job object to mark it Finished [source: k8s-docs-controllers-2026-08-23]. The loop reports on itself through the same shared state it reads from.

> **★ Fixed Point**
>
> **A control loop is: a desired state, a current state, and an action that closes the gap between them — repeating, without terminating.**
>
> A Kubernetes controller is a control loop that watches cluster state and acts to move current state closer to desired state. It does this continuously, not once. It usually acts by asking the API server to change something, not by doing the thing itself. [source: k8s-docs-controllers-2026-08-23]

> **Extended Analogy:**
>
> A ship's company is not a workflow. There is no master schedule pinned in the wardroom listing every action the crew will take between departure and arrival, in order, with dependencies. Such a document would be worthless within the hour, because the sea does not consult it.
>
> What exists instead is standing orders. The helmsman's standing order is a heading: compare the compass to the ordered course, and correct. Not once, but continuously, every few seconds, for the whole watch. The lookout's standing order is a horizon: observe, and report anything on it. The engineer's standing order is a pressure range: watch the gauge, act when it drifts. Each rating holds one comparison and one response, and each of them performs it forever, without waiting to be told and without coordinating with the others.
>
> The vessel arrives on course not because someone executed a plan but because a few dozen small corrections were made continuously by people who were each watching one thing. No one aboard is running the voyage. The voyage is what all of that watching adds up to.
>
> The reason this analogy earns its place here rather than in the prose: what a control loop replaces is *the plan*, and that's easier to feel in a setting where you can picture the plan being useless.

### Desired versus current state

Now the claim that unsettles people, and the most quietly radical idea in the chapter.

Kubernetes takes a cloud-native view of systems, and is able to handle constant change. Your cluster could be changing at any point as work happens and control loops automatically fix failures. This means that, potentially, **your cluster never reaches a stable state. As long as the controllers for your cluster are running and able to make useful changes, it doesn't matter if the overall state is stable or not** [source: k8s-docs-controllers-2026-08-23].

That is not a caveat. That is a design position, and it is unusual enough to deserve a moment.

Most systems you've operated treat "converged and quiet" as the healthy state and "constantly changing" as an alarm. Kubernetes inverts it. Constant change is expected: machines fail, load shifts, images get updated, someone deletes something they shouldn't have. A cluster that is never quite finished reconciling isn't malfunctioning; it's a vessel underway, where the small correction is the normal condition and perfect stillness would be the thing worth investigating. The health question isn't *"has it settled?"* It's *"are the loops running, and can they still make useful changes?"*

Now go back to Soundings question 1: three copies, you want five. The script answer works exactly once, in exactly the conditions you wrote it for. The loop answer handles the same request, plus the machine that dies at 3 a.m., plus the one that dies while you're recovering from the first one, plus the copy someone deletes by hand next Tuesday, without anybody writing a rule for any of those cases. You didn't handle those cases. You stated a desired state and left something watching.

This is also where §1's capability list cashes out. Self-healing was listed as something Kubernetes *provides* [source: k8s-docs-overview-2026-08-23]: restarting containers that fail, replacing containers, killing containers that fail a health check. Read it now with §6's vocabulary and it stops being a feature and becomes a description of loops running. A gap opens between what you asked for and what exists, and something closes it. Nobody triggered anything.

*[cross-bearing: see Ch 4 — the field that holds desired state, and its status counterpart]*
*[cross-bearing: see Ch 6 — ReplicaSet, a control loop you can watch working in real time]*
*[cross-bearing: see Ch 15 — the same loop, with a Git repository holding desired state]*

---

## ☆ Taking Your Bearings: Controllers and the Loop

Four questions. These are the ones that matter most.

**Q1.** 🔵 A component continuously compares a recorded target replica count against the number of Pods actually running, and creates or deletes Pods when they differ. Is this a control loop, and what are its two states?

A) Yes — desired state is the recorded target count; current state is the number actually running
B) Yes — desired state is the number actually running; current state is the recorded target count
C) No — it's a scheduled task that runs at intervals, and it has no states
D) No — control loops observe state but never create or delete objects

**Q2.** 🔵 The Job controller receives a new Job. What does it actually do?

A) Starts the containers for the Job directly on the nodes it selects
B) Tells the API server to create Pods; other components act on that information
C) Chooses which node each of the Job's Pods will run on, then starts them
D) Connects to each node's kubelet and instructs it to run the Job's Pods

**Q3.** 🟡 Two controllers: Controller A reconciles the number of running replicas against a declared count. Controller B ensures enough Nodes exist in the cluster, provisioning new machines when needed. Which uses control via the API server, and which uses direct control?

A) Both use control via the API server
B) A uses direct control; B uses control via the API server
C) A uses control via the API server; B uses direct control
D) Both use direct control

**Q4.** 🟡 A cluster's state is changing continuously and never settles into a steady configuration. Is this a malfunction?

A) No — as long as the controllers are running and able to make useful changes, overall stability doesn't matter
B) Yes — a healthy cluster converges on a stable state and then stays there
C) Yes — continuous change means some controller is stuck repeating its reconciliation
D) No, but only in clusters that have some form of autoscaling enabled

---

**Answers with Explanations:**

**Q1 — A.** Controllers are control loops that watch cluster state and make or request changes, each trying to move current state closer to desired state [source: k8s-docs-controllers-2026-08-23].
- **B is wrong** — and it's the reversal to catch. Desired state is what you asked for; current state is what's true. Getting them backwards inverts the entire model.
- **C is wrong** — a scheduled task runs at intervals and completes. A control loop is non-terminating and driven by the gap between two states, not by a clock.
- **D is wrong** — creating and deleting objects is exactly how most Kubernetes controllers close the gap.

**Q2 — B.** The Job controller does not run any Pods or containers itself; it tells the API server to create or remove Pods, and other components in the control plane act on the new information [source: k8s-docs-controllers-2026-08-23].
- **A is wrong** — controllers don't touch containers. That's the kubelet's job, and only for its own node.
- **C is wrong** — node selection is kube-scheduler's job, and it happens after the Pods exist as objects. The Job controller doesn't choose placement.
- **D is wrong** — nothing on the control plane instructs a kubelet. The kubelet watches the API server and acts on what it finds there.

**Q3 — C.** Controller A works entirely inside the cluster: it reads desired state from the API server and asks the API server to create or remove Pods, which is control via the API server. Controller B needs something outside the cluster to set up new Nodes, so it finds desired state from the API server and then communicates directly with an external system, which is direct control [source: k8s-docs-controllers-2026-08-23].
- **A is wrong** — no amount of API-server messaging can conjure a machine that doesn't exist. B has to reach outside.
- **B is wrong** — the pairing is backwards. Replica reconciliation is the textbook in-cluster case.
- **D is wrong** — direct control is explicitly the less common shape; treating it as the default inverts the documentation's framing.

**Q4 — A.** Your cluster could be changing at any point as work happens and control loops automatically fix failures; potentially, your cluster never reaches a stable state, and as long as the controllers are running and able to make useful changes, it doesn't matter if the overall state is stable [source: k8s-docs-controllers-2026-08-23].
- **B is wrong** — this is the intuition most operators bring from other systems, and it's the one Kubernetes explicitly discards.
- **C is wrong** — "stuck in a loop" imports a pathology that doesn't apply. The loop is *supposed* to run forever; running forever isn't the symptom.
- **D is wrong** — the documentation's claim isn't conditional on any feature. It's a statement about the system's design position generally.

**If you scored 4/4:** You have the idea the rest of the book is built on. §7 is the payoff, and it's short.

**If you scored 3:** Review the one you missed and continue.

**If you scored 0–2:** Re-read §6 before continuing, and pay particular attention to the ★ Fixed Point and the Job-controller paragraph. Chapter 4 opens on the mechanics of desired state and assumes you have the concept.

**Checkpoint: You've Now Mastered**
✓ The control loop: desired state, current state, action, repeating
✓ What a controller actually does — and what it delegates
✓ Control via API server versus direct control, and which is common
✓ Why a cluster that never settles isn't a broken cluster

🌅 **Chapter 3 · Voyage Progress:** census → arrangement → **loop complete**

---

## §7 — 🟡 Nobody Is in Charge

☀️ **Zenith**

Put §5 and §6 side by side.

From §5: all state moves through one hub, and components coordinate by watching that state rather than by instructing each other. None of the other control-plane components are even designed to expose remote services [source: k8s-docs-control-plane-node-communication-2026-08-24]. From §6: many independent loops each watch that state and act on their own account, continuously, without terminating.

Now the question this chapter opened with. Where is the component that's in charge?

There isn't one, and now you can see *why* there isn't one, which is more useful than the fact. There is no component whose job is to hold the plan, because there is no plan in that sense. There's a description of what should be true, and a set of independent processes each responsible for one gap between description and reality. Nobody is executing steps, because nobody wrote steps. What looked like a missing piece of the architecture is the architecture.

### The disclaimer, paid off

Back to §1's Snag, in the documentation's own words:

> Kubernetes is not a mere orchestration system. In fact, it eliminates the need for orchestration. **The technical definition of orchestration is execution of a defined workflow: first do A, then B, then C.** In contrast, Kubernetes comprises a set of independent, composable control processes that continuously drive the current state towards the provided desired state. It shouldn't matter how you get from A to C. Centralized control is also not required. This results in a system that is easier to use and more powerful, robust, resilient, and extensible. [source: k8s-docs-overview-2026-08-23]

> **★ Fixed Point**
>
> **Orchestration, technically, is the execution of a defined workflow: first do A, then B, then C.** Kubernetes disclaims it. Kubernetes comprises a set of independent, composable control processes that continuously drive current state toward desired state — and it shouldn't matter how you get from A to C. Centralized control is not required. [source: k8s-docs-overview-2026-08-23]

Everyone in the industry, including this book in Chapter 1, calls Kubernetes an orchestrator. In the loose sense, meaning a thing that manages containers across machines, that's a perfectly good description, and it was the right altitude for an orientation chapter. In the precise sense the documentation is using, it's the one thing Kubernetes says it is not. The exam tests the precise sense. Now you have both, and you know which is which.

*[cross-bearing: see Ch 1 §2 — where this book first called Kubernetes an orchestrator, in the industry's loose sense]*

### What this buys

A distinction you can't cash out is just trivia, so: why is this worth building a system around?

**A system with no coordinator has no component whose failure leaves the others without instructions.** Not because everything keeps working — some things very much stop working — but because none of them were *taking* instructions in the first place. A kubelet's standing job is not an order it received; it is a comparison it holds, against the PodSpecs it already has [source: k8s-docs-cluster-architecture-2026-08-23]. There is no instruction queue to drain and no coordinator to wait on, because the work was never expressed that way.

<!-- AUTHOR-REVIEW: the prior draft asserted specific kubelet behavior during a control-plane partition ("it keeps the containers it already knows about running"). No cached or newly-fetched snapshot covers kubelet behavior when the API server is unreachable — k8s-docs-nodes-2026-08-23 documents only the control-plane side (Ready → Unknown, API-initiated eviction). The claim has been reframed above as a consequence of the sourced "ensures the containers described in those PodSpecs are running" description rather than as reported partition behavior. If the partition behavior is wanted explicitly, open a research gap for the kubelet reference or kubernetes.io/docs/concepts/architecture/nodes/ node-lifecycle; do not restore the unsourced version. -->

**A system that describes outcomes rather than sequences absorbs changes to the outcome without anyone rewriting the sequence.** Change the described state and every loop that cares about it recomputes its own gap. Nobody edits a workflow, because nobody wrote one. It shouldn't matter how you get from A to C, so when C changes, nothing about the path needs redesigning.

⚠ **One precision, because the heading overstates.** "Nobody is in charge" is a good chapter title and a bad thesis, and you should leave with the narrower version. The control plane *does* make global decisions about the cluster [source: k8s-docs-cluster-architecture-2026-08-23]. The API server *is* a hub that everything depends on. etcd *is* a single store whose loss loses the cluster. There are absolutely critical components here, and Chapters 8, 12, and 13 all depend on you knowing which.

The accurate claim is narrower and better: **there is no component that executes a workflow, and no component that tells another component what to do.** The hub holds state and serves it. It does not direct. That's a claim about *coordination*, not about *availability*, and the difference between those two is worth more to you on exam day than the slogan.

### What you're carrying forward

You now own a shape. Desired state, current state, an action closing the gap, repeating without end. You will meet it again in Chapter 6, where a ReplicaSet lets you watch it work in real time. In Chapter 15, where the desired state lives in a Git repository outside the cluster and a controller inside the cluster reaches out for it, which will look like a completely new technology until you recognize it. And in Chapter 17, where it turns out to be one of the things "cloud native" means.

That's why §6 was worth more than the eight names, and why the eight names were worth learning anyway: you can't reason about which loop stopped closing if you can't name the pieces.

🏆 **Safe Harbor reached — the architecture is behind you.**

*[cross-bearing: see Ch 6 — controllers you configure yourself]*
*[cross-bearing: see Ch 15 — the loop, pointed somewhere unexpected]*
*[cross-bearing: see Ch 17 — the same pattern, named as a principle]*

---

## Exam Alert! 🚨

**High-Priority Topics:**

1. **The census, with optionality marked.** Eight components across two planes. kube-proxy and cloud-controller-manager are the two the documentation marks optional, and for different reasons. Pure recall, cheaply tested, and it is tested.
2. **The control loop.** Desired state, current state, an action that closes the gap, never terminating. The highest-value idea in this chapter by a wide margin.
3. **kube-controller-manager: many logical controllers, one binary, one process.** One sentence in the documentation, disproportionately tested.
4. **Kubernetes is not a mere orchestration system.** The technical definition of orchestration is execution of a defined workflow: first A, then B, then C. Kubernetes disclaims it in favor of independent, composable control processes.
5. **What Kubernetes is not.** Not a traditional all-inclusive PaaS. Does not build your source. Does not ship middleware, databases, or caches. Does not mandate logging or configuration solutions.

**Common Traps:**

- **"kube-proxy is required on every node."** — Optional when a network plugin provides equivalent packet forwarding for Services [source: k8s-docs-cluster-architecture-2026-08-23].
- **"Every cluster has a cloud-controller-manager."** — Absent on premises and in a learning environment on your own PC [source: k8s-docs-cluster-architecture-2026-08-23].
- **"The controller-manager runs one process per controller."** — Logically separate, but compiled into a single binary and run in a single process [source: k8s-docs-cluster-architecture-2026-08-23].
- **"Kubernetes is an orchestrator that runs A then B then C."** — That is the technical definition of orchestration, which Kubernetes explicitly disclaims [source: k8s-docs-overview-2026-08-23].
- **"Kubernetes is a PaaS."** — Not a traditional, all-inclusive PaaS; the PaaS-like features it does offer are optional and pluggable [source: k8s-docs-overview-2026-08-23].
- **"The scheduler places the Pod on the node."** — The scheduler *selects* a node and notifies the API server of that decision [source: k8s-docs-kube-scheduler-2026-08-23]. The kubelet on that node starts the containers. (How the scheduler chooses is Chapter 7's.)
- **"The controller does the work."** — A controller usually asks the API server to change something. A different component performs the action.

---

## Practice Questions

**Q1.** ⚪ In the traditional deployment era, what was the only practical way to give an application resource isolation on a physical server?

A) Configure per-application resource quotas in the operating system
B) Run each application under a separate OS user account with per-user limits
C) Run each application on a different physical server
D) Run each application inside its own hypervisor partition

**Q2.** 🔵 *[retrieval: ch2]* Containers have relaxed isolation properties compared with virtual machines. Architecturally, what is it that containers share with each other that separate VMs do not?

A) The operating system
B) The physical hardware underneath the machine
C) Their filesystem and process space
D) The network interface on the host

**Q3.** ⚪ Which of the following does Kubernetes explicitly *not* do?

A) Restart containers that fail their health check
B) Automatically mount a storage system of your choice
C) Expose a container using a DNS name or its own IP address
D) Deploy your source code and build your application

**Q4.** 🔵 Kubernetes drew on which internal Google system, and what language is it written in?

A) MapReduce, a data-processing framework; written in C++
B) Borg, and its research successor Omega; written in Go
C) Spanner, a globally distributed database; written in Java
D) Omega alone, with no production predecessor; written in Rust

**Q5.** ⚪ Kubernetes was donated by Google to which foundation, and what does the name mean?

A) The Apache Software Foundation, as an incubating project; the name is an acronym
B) The Cloud Native Computing Foundation, as one of several launch projects; the name is Latin for shepherd
C) The Cloud Native Computing Foundation, as its first project; the name is Greek for helmsman or pilot
D) The Open Container Initiative, alongside runC; the name is Greek for cluster

**Q6.** ⚪ The documentation says that in production environments the control plane usually runs across multiple computers. What does that buy?

A) Higher throughput, because each control-plane machine serves a different namespace
B) Fault tolerance and high availability
C) Reduced etcd storage, because cluster data is sharded across the machines
D) A higher ceiling on the number of worker nodes a single cluster can hold

**Q7.** ⚪ Which component is described as the front end for the Kubernetes control plane?

A) kube-apiserver
B) kube-controller-manager
C) etcd
D) kubelet

**Q8.** ⚪ What is etcd's role in a Kubernetes cluster?

A) It runs the containers that make up the control-plane components
B) It caches container images so that Pods start faster on each node
C) It routes API traffic across multiple kube-apiserver instances
D) It is a consistent, highly-available key value store holding all cluster data

**Q9.** 🔵 kube-apiserver is described as designed to scale horizontally. What does that mean in practice?

A) It automatically grows its memory allocation as request load increases
B) It spawns one worker process for each connected client
C) You deploy more instances of it and balance traffic between them
D) It shards cluster data across multiple independent etcd clusters

**Q10.** 🔵 Which of these is *not* listed among the factors kube-scheduler takes into account?

A) How recently each candidate node was rebooted
B) Individual and collective resource requirements
C) Affinity and anti-affinity specifications
D) Data locality

**Q11.** 🔵 The kubelet is given a set of PodSpecs. What is its responsibility?

A) To choose which node each PodSpec should run on
B) To store the PodSpecs durably so that they survive a restart
C) To ensure the containers described in those PodSpecs are running and healthy
D) To forward the PodSpecs to kube-proxy for network configuration

**Q12.** 🔵 You SSH to a worker node and start a container by hand using the container runtime directly. What does the kubelet do about it?

A) It restarts it if it exits, since it is running on a managed node
B) Nothing — the kubelet doesn't manage containers that were not created by Kubernetes
C) It reports it to the API server as an unmanaged Pod on that node
D) It terminates it immediately as an unauthorized workload on a managed node

**Q13.** 🔵 Which node component is *not* Kubernetes software — that is, a separate project that Kubernetes drives through a defined interface?

A) kubelet
B) kube-proxy
C) All three node components are Kubernetes project components
D) The container runtime

**Q14.** 🟡 A cluster has an object created and stored, but the component that would normally act on that kind of object is not installed. What happens?

A) The API server rejects the object at creation time as unserviceable
B) kube-controller-manager automatically installs the missing component
C) Nothing happens — the object exists as a description, but nothing acts on it
D) The kubelet on each node takes over the missing component's responsibilities

**Q15.** 🟡 A kubelet needs to know which Pods it is responsible for. Where does it get that, and what else does it talk to in order to get it?

A) From kube-scheduler, which pushes each assignment directly to the node it selected
B) From the API server, which it watches — not from the scheduler or another kubelet
C) From etcd, which it reads directly, bypassing the API server for lower latency
D) From kube-proxy on the same node, which relays control-plane traffic inward

**Q16.** 🔵 In Kubernetes, when a controller "wants" a Pod to exist, what does it typically do?

A) Sends messages to the API server that have useful side effects
B) Creates the container directly through the node's container runtime
C) Writes the Pod definition into etcd itself, bypassing the API server
D) Instructs the target node's kubelet over a dedicated control channel

**Q17.** 🔵 What are the two states a control loop compares?

A) Requested state and allocated state
B) Declared state and validated state
C) Desired state and current state
D) Committed state and applied state

**Q18.** 🟡 §1 lists self-healing among the things Kubernetes provides: restarting containers that fail, replacing containers, killing containers that don't respond to a health check. In §6's terms, what makes self-healing a standing condition rather than an action?

A) It is scheduled to run at a fixed interval, re-checking every container each time
B) It is a loop comparing the state you asked for against the state that exists, acting whenever the two differ
C) It runs once when a Pod is created and then hands responsibility to the kubelet
D) It is triggered by an operator or an external monitoring system when a failure is detected

**Q19.** 🟡 A controller needs to provision a new virtual machine from a cloud provider because the cluster needs more Nodes. Which control shape is this, and where does it get its desired state?

A) Direct control; it finds desired state from the API server, then talks to the external system
B) Control via the API server; it finds desired state in the cloud provider's own API
C) Direct control; it finds desired state in a configuration file on the control plane
D) Control via the API server; it reads desired state directly out of etcd

**Q20.** 🟡 A system is described as "executing a defined workflow: first do A, then B, then C." In the documentation's terms, what is that system doing?

A) Reconciliation
B) Declarative configuration
C) Automatic bin packing
D) Orchestration

**Q21.** 🟡 The documentation says Kubernetes eliminates the need for orchestration. What does it say Kubernetes comprises instead?

A) A centralized coordinator that computes an optimal execution order for the cluster
B) A workflow engine with pluggable, user-defined step definitions
C) A message bus over which the components exchange instructions with each other
D) A set of independent, composable control processes driving current state toward desired state

**Q22.** 🟡 The Node controller notices when nodes go down and responds. Which component is it running inside, and what does "responds" mean in control-loop terms?

A) It runs inside kube-controller-manager; it compares expected node state against observed, and asks the API server to act
B) It runs inside the kubelet on each node, and it restarts that node's containers when they stop
C) It runs inside kube-scheduler, and it moves the failed node's Pods to other nodes itself
D) It runs as its own separate control-plane component and instructs the affected node's kubelet directly

**Q23.** 🟡 kube-proxy and cloud-controller-manager are both marked optional in the documentation. Is it for the same reason?

A) No — one because another component may already do its job; the other because there may be nothing for it to integrate with
B) Yes — both are optional because a cluster below a certain size does not need either of them
C) Yes — both are optional because an addon can be installed to replace either of them
D) No — one is optional only in single-node clusters; the other only in clusters that define no Services

**Q24.** 🔵 *[retrieval: ch2]* You need to change one line of configuration baked into a running container's filesystem. What is the correct process?

A) Edit the file inside the running container and restart its process
B) Build a new image that includes the change, then recreate the container from it
C) Mount a writable layer over the container and patch the file in place
D) Ask the kubelet to hot-patch the container's filesystem on the node

**Q25.** 🔵 *[retrieval: ch2]* What does a container image contain?

A) The application binary only — libraries come from the node at run time
B) A full guest operating system, including its own kernel, like a VM disk image
C) The application's source code, which the node compiles when the container starts
D) The code, its runtime, application and system libraries, and default settings

---

**Answers with Explanations:**

**Q1 — C.** There was no way to define resource boundaries for applications on a physical server; the solution was to run each application on a different physical server, which didn't scale and was expensive [source: k8s-docs-overview-2026-08-23].
- **A is wrong** — the documented problem statement is precisely that no such boundary mechanism existed.
- **B is wrong**, and instructively so. Separate user accounts were a real historical practice, and they do constrain *some* things, but not the ones that mattered. One application could still consume most of the machine's CPU or memory and starve the rest, which is exactly the failure the documentation describes.
- **D is wrong** — hypervisors are the *next* era. That's the whole point of the progression.

**Q2 — A.** *[retrieval: ch2]* Containers have relaxed isolation properties that let them share the operating system among the applications, which is why they are considered lightweight; a VM, by contrast, is a full machine running all the components, including its own operating system, on top of virtualized hardware [source: k8s-docs-overview-2026-08-23].
- **B is wrong** — VMs share the physical hardware too. That's what virtualization *is*, and it's the previous era's change, not this one.
- **C is wrong** — and it's the reversal worth catching. A container has *its own* filesystem, and its own share of CPU, memory, and process space [source: k8s-docs-overview-2026-08-23]. Those are among the things that stay separate.
- **D is wrong** — networking is configurable in both models and isn't the architectural distinction the era transition turns on.

**Q3 — D.** Kubernetes does not deploy source code and does not build your application; CI/CD workflows are determined by organizational culture, preferences, and technical requirements [source: k8s-docs-overview-2026-08-23].
- **A, B, C are wrong** — all three appear in the published capability list as things Kubernetes does: self-healing, storage orchestration, and service discovery respectively [source: k8s-docs-overview-2026-08-23].

**Q4 — B.** Kubernetes drew on Google's internal container-orchestration experience, Borg and its research successor Omega, and was written in Go [source: k8s-history-ten-years-2026-08-23].
- **A is wrong** — MapReduce is a data-processing framework, an unrelated lineage, and the language is wrong.
- **C is wrong** — Spanner is a distributed database, and the language is wrong.
- **D is wrong** — Omega alone is incomplete. Borg came first and was the production system; Omega is described as its research successor. The language is also wrong.

**Q5 — C.** Kubernetes was donated by Google to the newly formed Cloud Native Computing Foundation as its first project, and the name comes from the Greek word for helmsman or pilot [source: k8s-history-ten-years-2026-08-23].
- **A is wrong** on both halves; the CNCF is part of the nonprofit Linux Foundation [source: cncf-who-we-are-2026-08-23], not Apache, and the name is not an acronym.
- **B is wrong** on the second half, which is the discriminating half. "First project" is right; the etymology is Greek, not Latin, and it is helmsman, not shepherd.
- **D is wrong** — the OCI is a separate Linux Foundation body governing container format and runtime specifications [source: oci-overview-2026-08-23], and it is where Docker donated runC, not where Google donated Kubernetes.

**Q6 — B.** In production environments the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault tolerance and high availability [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — nothing partitions control-plane duties by namespace. kube-apiserver instances are interchangeable [source: k8s-docs-cluster-architecture-2026-08-23].
- **C is wrong** — running the control plane across several machines is not a data-sharding scheme, and the documentation describes no such sharding.
- **D is wrong** — a plausible-sounding benefit that the documentation does not claim here. The stated purpose is availability, not capacity.

**Q7 — A.** The API server is the front end for the Kubernetes control plane [source: k8s-docs-cluster-architecture-2026-08-23].
- **B is wrong** — the controller-manager runs controllers; it's a client of the front end, not the front end.
- **C is wrong** — etcd is the backing store *behind* the front end, not the front end itself. This is the most tempting wrong answer if you think of "front end" as "where the data is."
- **D is wrong** — the kubelet is a node agent.

**Q8 — D.** Verbatim role from the documentation: a consistent and highly-available key value store used as Kubernetes' backing store for all cluster data [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — etcd is a datastore, not a runtime.
- **B is wrong** — image caching happens on nodes, managed by the kubelet and runtime [source: k8s-docs-images-2026-08-23].
- **C is wrong** — that describes a load balancer sitting in front of multiple kube-apiserver instances, which is a real thing but not etcd.

**Q9 — C.** kube-apiserver is designed to scale horizontally: it scales by deploying more instances, and you can run several and balance traffic between them [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — that's vertical scaling, and it isn't what the documentation describes.
- **B is wrong** — a process-per-client model is not what "scales horizontally" means here; the unit of scaling is the whole instance.
- **D is wrong** — data sharding across etcd clusters is not part of the described design.

**Q10 — A.** The listed factors are resource requirements, hardware/software/policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and deadlines [source: k8s-docs-cluster-architecture-2026-08-23]. Time-since-reboot is plausible as a stability heuristic, and some systems do weigh something like it, but it is not among the factors Kubernetes lists.
- **B, C, D are wrong as answers** because all three *are* listed factors.

**Q11 — C.** The kubelet takes a set of PodSpecs provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — node selection belongs to kube-scheduler.
- **B is wrong** — durable storage is etcd's job, reached through the API server.
- **D is wrong** — kube-proxy maintains network rules; it isn't downstream of the kubelet's PodSpec handling.

**Q12 — B.** The kubelet doesn't manage containers which were not created by Kubernetes [source: k8s-docs-cluster-architecture-2026-08-23].
- **A is wrong** — "running on a managed node" isn't the criterion; *created by Kubernetes* is.
- **C is wrong** — the kubelet's stated responsibility is the containers described in its PodSpecs. A container it didn't create isn't one of those, so there is nothing for it to maintain or account for.
- **D is wrong** — the kubelet doesn't police the node. It doesn't manage what isn't its business, which is different from acting against it.

**Q13 — D.** Kubernetes supports container runtimes such as containerd, CRI-O, and any other implementation of the Kubernetes CRI [source: k8s-docs-cluster-architecture-2026-08-23]. These are separate projects driven through the Container Runtime Interface [source: k8s-docs-extending-kubernetes-2026-08-23].
- **A and B are wrong** — kubelet and kube-proxy are Kubernetes project components.
- **C is wrong** — the whole design point of CRI is that the runtime is pluggable and external.

**Q14 — C.** The object exists as a stored description; something has to be watching for it and willing to act, and if that component is absent, nothing acts. This is the absent-component pattern from §4.
- **A is wrong** — the API server validates the object's structure, not whether a consumer for it exists.
- **B is wrong** — nothing in Kubernetes self-installs missing components in response to an object appearing.
- **D is wrong** — the kubelet has exactly one job and doesn't inherit others.

**Q15 — B.** All API usage from nodes and the Pods they run terminates at the API server, and none of the other control-plane components are designed to expose remote services [source: k8s-docs-control-plane-node-communication-2026-08-24]. The kubelet watches the API server and acts on what it finds.
- **A is wrong** — the scheduler notifies the API server of its decision [source: k8s-docs-kube-scheduler-2026-08-23]. It does not push anything to a node.
- **C is wrong** — the API server is the component that reads and writes etcd; access to etcd is root-equivalent and is meant to be confined to it [source: k8s-docs-etcd-access-control-2026-08-24].
- **D is wrong** — kube-proxy maintains network rules for Services. It is not a control-plane relay.

**Q16 — A.** A controller might carry the action out itself, but more commonly a controller sends messages to the API server that have useful side effects [source: k8s-docs-controllers-2026-08-23].
- **B is wrong** — the Job controller explicitly does not run any Pods or containers itself [source: k8s-docs-controllers-2026-08-23].
- **C is wrong** — controllers go through the API server, not around it.
- **D is wrong** — there is no such dedicated channel; the kubelet watches the API server.

**Q17 — C.** Desired state and current state: the thermostat's set temperature and the room's actual temperature, generalized [source: k8s-docs-controllers-2026-08-23].
- **A, B, D are wrong** — plausible-sounding pairs that appear nowhere in the documentation. If any of them felt right, that's worth noticing: real terminology and invented terminology read identically until you've anchored the real pair.

**Q18 — B.** Controllers are control loops that watch cluster state and act to move current state closer to desired state, continuously [source: k8s-docs-controllers-2026-08-23]. Self-healing — restarting failed containers, replacing containers, killing ones that fail a health check [source: k8s-docs-overview-2026-08-23] — is that comparison running, not a procedure someone invoked.
- **A is wrong** — a clock-driven sweep is a scheduled task. A control loop is driven by the gap between two states, not by an interval.
- **C is wrong** — "runs once and hands off" is exactly the model §6 replaces. Nothing about the loop terminates when a Pod comes up.
- **D is wrong** — no external trigger is involved. The whole point is that nobody has to notice and initiate.

**Q19 — A.** Controllers that interact with external state find their desired state from the API server, then communicate directly with an external system to bring the current state closer in line, and provisioning Nodes is the documentation's own example [source: k8s-docs-controllers-2026-08-23].
- **B is wrong** — desired state always comes from the API server, even for direct-control controllers. That's what makes them Kubernetes controllers.
- **C is wrong** — no local config file holds desired state; that would break the whole model.
- **D is wrong** on both halves: this is direct control, and components reach etcd through the API server rather than around it.

**Q20 — D.** The technical definition of orchestration is execution of a defined workflow: first do A, then B, then C [source: k8s-docs-overview-2026-08-23].
- **A is wrong** — reconciliation is the opposite shape: continuous comparison, no defined sequence.
- **B is wrong** — declarative configuration describes an end state without a path.
- **C is wrong** — bin packing is a placement optimization, not a workflow model.

**Q21 — D.** Kubernetes comprises a set of independent, composable control processes that continuously drive the current state towards the provided desired state; it shouldn't matter how you get from A to C, and centralized control is not required [source: k8s-docs-overview-2026-08-23].
- **A is wrong** — and it names the exact thing the documentation disclaims: centralized control is explicitly not required.
- **B is wrong** — a workflow engine with pluggable steps is still a workflow engine. Making the steps configurable doesn't stop the system from executing a defined sequence.
- **C is wrong**, and it is the mental model §5 spent a whole section dismantling. Components do not exchange instructions; they observe shared state. None of the other control-plane components are even designed to expose remote services [source: k8s-docs-control-plane-node-communication-2026-08-24].

**Q22 — A.** The Node controller is one of the controllers run by kube-controller-manager — noticing and responding when nodes go down — and every controller in that binary runs in the same single process [source: k8s-docs-cluster-architecture-2026-08-23]. "Responds" means what it means for every controller: compare, then ask the API server to change something [source: k8s-docs-controllers-2026-08-23].
- **B is wrong** — the kubelet manages containers on its own node. It is not where the Node controller lives, and a node that has gone down is not running a kubelet you can rely on.
- **C is wrong** — kube-scheduler assigns unscheduled Pods to nodes; it doesn't monitor node health, and it doesn't move Pods itself.
- **D is wrong** — the Node controller is not a separate component, and nothing on the control plane instructs a kubelet directly.

**Q23 — A.** kube-proxy is unnecessary when a network plugin implements equivalent packet forwarding for Services; cloud-controller-manager is absent when you run on your own premises or on your own PC, because there is no cloud provider to link to [source: k8s-docs-cluster-architecture-2026-08-23].
- **B is wrong** — cluster size is irrelevant to both.
- **C is wrong** — addons don't substitute for either.
- **D is wrong** — both halves invent conditions the documentation doesn't state.

**Q24 — B.** *[retrieval: ch2]* Containers are intended to be stateless and immutable; you should not change the code of a container that is already running. The correct process is to build a new image that includes the change, then recreate the container from the updated image [source: k8s-docs-containers-2026-08-23].
- **A is wrong** — editing in place is exactly the practice immutability rules out, and the change vanishes on the next restart.
- **C is wrong**, but not because the mechanism doesn't exist. A container's writable layer is real. It's wrong because anything written there belongs to *that container instance* and is gone the moment the container is replaced, which is a thing Kubernetes does constantly. That's the practical teeth of immutability: the change lives in the image, or it doesn't survive.
- **D is wrong** — there is no such kubelet capability. The kubelet starts and stops containers through the CRI [source: k8s-docs-extending-kubernetes-2026-08-23]; it doesn't reach inside their filesystems. Note the connection to this chapter, though: the control loop's response to a changed desired state is the same instinct — replace, don't mutate.

**Q25 — D.** *[retrieval: ch2]* A container image is a ready-to-run software package containing everything needed to run an application: the code and any runtime it requires, application and system libraries, and default values for any essential settings [source: k8s-docs-containers-2026-08-23].
- **A is wrong** — the standardization from having dependencies included is precisely what makes a container repeatable across environments [source: k8s-docs-containers-2026-08-23]. If libraries came from the node, that guarantee would be gone.
- **B is wrong** — and it's the VM confusion again. A full machine with its own operating system is the virtualized era's unit, not the container era's [source: k8s-docs-overview-2026-08-23].
- **C is wrong** — an image is ready to run. Nothing is compiled at container start.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **Three deployment eras** | Traditional (one app per server, nothing shared) → virtualized (own OS per VM, hardware shared) → container (operating system shared, lightweight, portable) |
| **What Kubernetes is not** | Not an all-inclusive PaaS. Doesn't build your source. No built-in databases, middleware, or caches. Doesn't mandate logging or config solutions. Not a mere orchestration system. |
| **Origin** | Descended from Google's Borg (and its research successor Omega). Written in Go. First commit 2014-06-06. v1.0 July 2015. CNCF's first donated project. Name = Greek for helmsman. |
| **Cluster shape** | A control plane plus a set of worker nodes. At least one worker node is needed to run Pods. In production the control plane runs across multiple computers, for fault tolerance and high availability. |
| **kube-apiserver** | Front end for the control plane. Exposes the Kubernetes HTTP API. Scales horizontally by adding instances. |
| **etcd** | Consistent, highly-available key value store. Backing store for *all* cluster data. Access to it is root-equivalent. Have a backup plan. |
| **kube-scheduler** | Watches for Pods with no assigned node and selects one, then notifies the API server (binding). Selects and records — does not start anything. |
| **kube-controller-manager** | Runs controller processes. Logically separate, but **one binary, one process.** |
| **cloud-controller-manager** | **Optional.** Links the cluster to a cloud provider's API. Absent on premises and on your laptop. |
| **kubelet** | On every node. Ensures the containers described in its PodSpecs are running and healthy. Doesn't manage containers it didn't create. |
| **kube-proxy** | **Optional.** On every node when present. Maintains node network rules implementing part of the Service concept. Unnecessary if a network plugin does the same job. |
| **Container runtime** | On every node. Runs the containers. Not Kubernetes software — containerd, CRI-O, or any CRI implementation. |
| **Addons** | Extend the cluster rather than constituting it. DNS, Dashboard, resource monitoring, cluster-level logging. |
| **Absent-component pattern** | An object without its component does nothing. The description exists; nothing acts on it. |
| **The hub** | State moves through the API server, and the API server is what reads and writes etcd. Coordination is watching, not telling. (Outbound API-server→kubelet paths exist for logs, attach, and port-forward; they carry sessions, not instructions.) |
| **★ Control loop** | Desired state, current state, an action that closes the gap — repeating, non-terminating. |
| **Controller behavior** | Usually asks the API server to change something; other components act on that. Direct control (reaching outside the cluster) is the less common shape. |
| **Never stable** | A cluster may never reach a stable state, and that's fine — what matters is that the controllers are running and able to make useful changes. |
| **★ Orchestration** | Technically: execution of a defined workflow, A then B then C. Kubernetes disclaims it in favor of independent, composable control processes. Centralized control is not required. |

---

## The Voyage Ahead

You've met the crew and you know how they coordinate. What you don't yet have is the thing they're all watching.

Every component in this chapter reads from and writes to the same shared state, and that state is made of *objects*, the descriptions you submit and the system maintains. §6 kept saying "the field that says what should be true" and cross-bearing forward, because that field has a name, and a counterpart that reports what actually is true, and a set of conventions for how you write both. Chapter 4 gives them to you.

That's when the control loop stops being an architecture diagram and becomes something you operate. You'll write a description, submit it, and watch a loop you now understand go to work on it. The reason that will feel unremarkable rather than magical is that you did the work in this chapter first.

Now that you look at a Kubernetes cluster and see loops rather than services, the rest of the book gets considerably easier.

> *"The vessel arrives on course not because someone executed a plan, but because a few dozen small corrections were made continuously by people who were each watching one thing."*
