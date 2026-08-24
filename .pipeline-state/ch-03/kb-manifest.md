The write is blocked by the same permission failure that hit Stage 2, B3, and Chapter 1's Stage 14 — and this session is non-interactive, so the prompt can't be answered. **Unlike those stages, I will not let the apology become the artifact.** The manifest below is the stage output; the write blocks carry the full file contents for the orchestrator to persist.

# Knowledge-Base Manifest — KCNA Chapter 3

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 3 — The Ship's Company
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-24

**Inputs consulted:** the finalized chapter, `integration.md` (Stage 13), `ch-03/outline.md` frontmatter (`kb_tags`, 38 concepts), `ch-01/kb-manifest.md`, `book-outline/chapter-lineup.md` (B2), `book-outline/retrieval-architecture.md` (B3 — stage-failure notice), `diagnostics/theming-density.md`, `diagnostics/structural.md`, `ch-03/research-manifest.md`, and the shipped `chapter-01` / `chapter-02` files.

## ⚑ Two findings that change what this stage could do

Both verified on disk, not inferred:

1. **`Book-KCNA/knowledge-base/` does not exist.** Chapter 1's Stage 14 composed ten KB files; **none reached disk.** So there is nothing to append to. Every "append" in the task spec becomes a create.
2. **Chapter 2 never ran Stage 13 or Stage 14.** `.pipeline-state/ch-02/` has no `integration.md` and no `kb-manifest.md`, yet `chapter-02-cargo-in-standard-crates.md` is shipped. Chapter 2 owns **D1.4** and the definitions for `container image`, `immutability`, `CRI`, `containerd`, `CRI-O`, `runC`, `registry`, and the named interface pattern — **all of which Chapter 3 leans on, and none of which exist in any ledger.**

I did **not** fabricate Chapter 2's entries. Doing so would mean running Chapter 2's Stage 14 without its integration report, on exactly the contested term (`container` / operating-system-vs-kernel) where drift is most expensive. They are recorded as **Tier 4 — Chapter 2 gap** with defining chapters and no prose.

I **did** reconstruct Chapter 1's glossary, objective-coverage, and retrieval-log tiers verbatim from `ch-01/kb-manifest.md`, which is byte-exact on disk. Chapter 1's **seven concept shards are not reproduced here** — replay them from that manifest's own write blocks to avoid transcription drift.

**Recovery order:** replay Ch 1's seven `concepts/*.md` blocks → then apply this manifest's blocks (which already merge Ch 1 + Ch 3 for the three ledger files) → then run Ch 2 Stages 13–14 and backfill Tier 4.

## Glossary entries

**68 terms tracked — 31 defined · 7 conventions · 28 reserved · 2 optional.** Chapter 3 contributes 21 new definitions, 3 convention locks, and 17 reserved terms.

Stage 13 identified 12 terms needing entries under rule 4. All 12 are recorded; two are recorded as **gaps rather than definitions**, because Rule 5 forbids inventing prose the chapter never wrote:

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **control loop** | ★ "a desired state, a current state, and an action that closes the gap between them — repeating, without terminating" | Chapter 3 §6 |
| **orchestration (technical)** | ★ "execution of a defined workflow: first do A, then B, then C" | Chapter 3 §7 |
| **absent-component pattern** | "an object without its component does nothing" | Chapter 3 §4 |
| **controller** | "control loops that watch the state of your cluster, then make or request changes where needed" | Chapter 3 §6 |
| **desired / current state** | thermostat framing, verbatim | Chapter 3 §6 |
| **control via API server / direct control** | the two controller shapes, verbatim | Chapter 3 §6 |
| **kube-apiserver / etcd / kube-scheduler / kube-controller-manager / cloud-controller-manager** | census definitions, verbatim | Chapter 3 §2 |
| **kubelet / kube-proxy / container runtime** | census definitions, verbatim | Chapter 3 §3 |
| **cluster / control plane / node / addon / hub-and-spoke / Borg / Omega** | verbatim | Chapter 3 §1–§5 |
| **binding** | "the scheduler notifies the API server about its decision" — *partial, one clause* | Chapter 3 §2 → Ch 7 |
| **reconciliation** | ⚑ **GAP** — only definitional text is Practice Q20's distractor rationale | Chapter 3 → needs fix |
| **Pod** | ⚑ **GAP** — used ~40×, never defined, deferral never restated | Chapter 3 → Ch 5 |

Full tiering, including the 17 reserved terms (PaaS, CI/CD, VPA, EndpointSlice, ServiceAccount, Lease, `kube-system`, NetworkPolicy, Argo CD, Ingress, metrics-server, `crictl`, `kubectl top`, Job, CNI, PodSpec, Pod), is in the write block.

## Concept shards — 10 created

Slugs match `kb_tags.concepts` so the tagging round-trips.

- `concepts/control-loop.md` — **created** (§6; the book's structural spine)
- `concepts/absent-component-pattern.md` — **created** (§4; B3 cross-cutting theme, canonical name)
- `concepts/control-plane-components.md` — **created** (§2)
- `concepts/node-components.md` — **created** (§3) — *carries a Rule 6 flag*
- `concepts/api-server-hub.md` — **created** (§5)
- `concepts/optional-components.md` — **created** (§4)
- `concepts/orchestration-technical-definition.md` — **created** (§1 Snag + §7)
- `concepts/deployment-eras.md` — **created** (§1) — *carries a Rule 6 flag*
- `concepts/what-kubernetes-is-not.md` — **created** (§1; Exam Alert #5)
- `concepts/kubernetes-origin.md` — **created** (§1)

**Not created, with reasons:** `etcd` — Chapter 8 owns backup/restore and Chapter 12 owns encryption at rest; Chapter 3's treatment is split across `control-plane-components` and `api-server-hub`. **Ch 8's Stage 14 creates it.** `what-kubernetes-provides` — folded into `what-kubernetes-is-not.md` and `control-loop.md` (self-healing), since the chapter's own move is to re-read the capability list *as* loops.

### Rule 6 — canon conflicts carried into the shards

No shard was overwritten (none existed). Four conflicts against composed or shipped canon are recorded **loudly inside the shards**:

1. **`orchestrator` is split, not completed.** Ch 1's ledger recorded one entry with "full treatment Ch 3." Chapter 3 delivers **two senses that disagree** — the loose industry sense (correct at orientation altitude) and the precise sense Kubernetes disclaims. Both rows kept; merging them would destroy the chapter's Zenith.
2. **Ch 1's `container` PROVISIONAL flag is stale, and Chapter 3's own note misreports it.** Ch 2 §1 (ch02:281–285) adjudicates both registers as correct — *"**operating system** as the published wording, **kernel** as the mechanism underneath it"* — with an in-cache warrant from `k8s-docs-runtime-class`. **Chapters 1, 2, and 3 agree on substance;** the only open item is Ch 1's source *tag*. Chapter 3's §1 AUTHOR-REVIEW calls Ch 1 "the remaining outlier," and acting on it would delete the register Ch 2 spends three paragraphs building and Figure 2-1 depends on. Flagged in `deployment-eras.md` and the glossary.
3. **Chapter 3 broadens Ch 2's named interface pattern past its sourced enumeration.** Ch 2's pattern is CRI/CSI/CNI/device-plugins/API-extensions; **etcd is not among them.** Chapter 3 also re-derives the pattern in fresh words without using the name Ch 2 explicitly asked the reader to memorize — a missed retrieval event on a theme Ch 17's secondary Zenith needs. Flagged in `node-components.md`.
4. **Two forward-count claims are off.** "Six later chapters retrieve §6" — B3's control-loop theme is Ch 3→4→6→11→15→17, i.e. **five** later chapters, and the draft bears only four. "You're going to meet it four more times" — only three instances follow; B3's fourth is **NetworkPolicy on a non-enforcing CNI**, which Chapter 3 never bears. Both recorded in the shards so Ch 10 and Ch 11 can close them.

## Voice-exemplar candidates nominated

**Not written to `voice-exemplars.md`** — Rule 1. Nominations only.

Context that bears on promotion: `diagnostics/theming-density.md` scores this chapter **0.5 metaphors per 1000 words — underseasoned**, against a 1–3 band, and notes that *every reading above 0.5 depends entirely on one sidebar*. The Extended Analogy is simultaneously the chapter's best exemplar candidate and nearly its entire metaphor load.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Extended Analogy** | "A ship's company is not a workflow. There is no master schedule pinned in the wardroom listing every action the crew will take between departure and arrival, in order, with dependencies. Such a document would be worthless within the hour, because the sea does not consult it. … The vessel arrives on course not because someone executed a plan but because a few dozen small corrections were made continuously by people who were each watching one thing." | **Strongest in the chapter.** Maritime register doing load-bearing pedagogical work — it replaces *the plan*, which is the exact thing a control loop replaces. Closes by justifying its own placement. |
| **chapter-opening / curiosity gap** | "There is no component in Kubernetes whose job is to be in charge. That should bother you. … You are about to meet eight components, you will go looking for the one that runs things, and you will not find it. Hold that question." | **Strong.** Three sentences to open a gap, name the reader's prior expertise as the source of the confusion, and set the resolution point. |
| **⚓ Worth Securing (inline)** | "The coordination mechanism in Kubernetes is **watching, not telling.** Components don't send each other instructions. They observe shared state and act on what they see." | **Strong.** Model §18.14 length discipline; one sentence carrying the chapter's second-biggest idea. |
| **★ Fixed Point** | "**A control loop is: a desired state, a current state, and an action that closes the gap between them — repeating, without terminating.**" | **Strong.** Memorizable, non-negotiable, and the figure beneath it refuses to draw an entry arrow — text and visual agreeing on the same claim. |
| **self-correction / epistemic honesty** | "⚠ One precision, because the heading overstates. 'Nobody is in charge' is a good chapter title and a bad thesis, and you should leave with the narrower version. … That's a claim about *coordination*, not about *availability*." | **Strong, and unusual.** A chapter disarming its own most quotable line. Best available exemplar of Part 14's simplification-acknowledgment guardrail. |
| **why-wrong explanation** | "**A, B, D are wrong** — plausible-sounding pairs that appear nowhere in the documentation. If any of them felt right, that's worth noticing: real terminology and invented terminology read identically until you've anchored the real pair." | **Strong.** Diagnoses the reasoning failure and hands over a calibration habit rather than a correction. |
| **Dead Reckoning** | "kube-apiserver runs on the control plane and exposes the Kubernetes HTTP API. etcd runs on the control plane and stores all cluster data. …" | **Moderate–strong.** Textbook facts-only register: eight parallel clauses, zero metaphor, no framing. Slightly mechanical by design. |
| **🪝 Snag** | "'The controller does the work' is the intuitive reading and it's wrong. A controller almost never touches a container. It writes something down." | **Moderate.** Good inline-glyph scope; the payoff sentence is excellent. |

**Deliberately not nominated:** every passage from `## Exam Alert!` and the six lines carrying unverifiable frequency claims. Those are pending the Guardrail #8 rewrite (Stage 13 blocking item 1) — promoting them would ratify the non-compliant register into brand canon.

## Objective coverage log

Chapter 3 covers **D1.1 — Kubernetes Core Concepts** at **deep** depth, and is the first chapter to cover any objective. Full registry in the write block, including the ⚑ 13-vs-12 competency discrepancy inherited from Chapter 1 and a new flag: **D1.4 is shipped but unrecorded**, because Chapter 2's Stage 14 never ran.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.1 | Chapter 3 | deep | 2026-08-24 |
| D1.4 | Chapter 2 (shipped) | ⚑ **unrecorded — Ch 2 Stage 14 never ran** | — |

## Retrieval-practice ledger

**Chapter 3 is the first chapter carrying retrieval items** — B3's schedule opens here at the 10% rung, drawn entirely from Chapter 2. **Five tags, all landing; four in the graded pool = 10.5%,** clearing the rung.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| kubelet ensures the containers described for its node are running | ch 2 §4 | ch 3 — Soundings Q4 *(excluded from budget by B3)* |
| kubelet reaches the runtime through CRI | ch 2 §4 | ch 3 — Bearings #1 Q5 |
| containers share the operating system; VMs each boot their own | ch 2 §1 | ch 3 — Practice Q2 |
| immutability — build a new image, recreate the container | ch 2 §2 | ch 3 — Practice Q24 |
| image contents (code, runtime, libraries, defaults) | ch 2 §2 | ch 3 — Practice Q25 |

**One convention Chapter 1 left open is now settled by observation.** Chapter 1's ledger recorded that "the `[retrieval: chN]` tag's rendered form — reader-visible or draft-only — is still undecided," and that **Chapter 3 is the first chapter that needs it settled.** Chapter 3 settled it de facto: tags render **reader-visible, italic-bracketed, in both stem and answer key**. Recorded as OBSERVED PRACTICE awaiting ratification — it is now canon for seventeen chapters whether or not anyone chose it.

Also carried forward: Chapter 1's **binding contract** (Ch 13 must retrieve Ch 8's version skew), the open **★-never-retrieved** item, and the B3 provenance warning.

## Operator notes

1. **This stage could not write.** Permission to `Book-KCNA/knowledge-base/` was denied and the session is non-interactive. This is the **fourth** consecutive stage hitting the same fault (Stage 2 snapshots ×2 chapters, B3, Ch 1 Stage 14). It is an executor configuration problem, not a per-chapter one, and it is now costing real artifacts.
2. **Stage 13's item 18 is half right.** `book-outline/retrieval-architecture.md` is indeed a permission-denied notice with only a prose summary — B3's artifact is lost and **must be re-run**. But `ch-03/diagnostics/theming-density.md` **does** contain its full audit; the apology is only a preamble. Downstream parsers will handle these two files differently.
3. **The five `-2026-08-24` snapshots remain absent.** Verified: `sources/` holds 87 files, zero dated 08-24; `research-manifest.md` holds all five bodies. Eight glossary and shard entries carry `⚑ SNAPSHOT NOT ON DISK`. Recovery is mechanical extraction — no re-fetch.
4. **`diagnostics/structural.md` reports 0 fail / 0 warn / 28 pass** — unlike Chapter 1's 0/0/0, this chapter has genuine structural corroboration.
5. **Outline frontmatter drift:** `question_budget.total_this_chapter: 40` (8 + 13 + 19); the shipped chapter carries 8 Soundings + 13 Bearings + 25 Practice = **46**. The book-level rollup will read low.

---

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===
# KCNA — Knowledge-Base Glossary Ledger

**Working ledger, not the shipped artifact.** This file tracks which terms the book
surfaces, which chapter defines each one, and what definition was actually written.
The published `glossary.md` at the book root (required by skill Part 16, minimum 100
terms) is generated from this ledger at book assembly, once every reserved term has a
real definition.

**Conventions locked at Chapter 1** (per Stage 13 recommendation; author-ratifiable):

1. **Cross-reference cites the chapter of DEFINITION, not first mention.** Chapter 1
   names ~20 terms it never teaches. Citing first mention would point a third of the
   glossary at the orientation chapter.
2. **Reserved terms carry no prose.** A term surfaced but not defined gets a row and a
   defining chapter, nothing more. Paraphrasing a cached source into a definition the
   chapter never wrote is definitional drift, which is worse than no entry.
3. **`curriculum`** = the CNCF-published document (`KCNA_Curriculum.pdf`).
   **`blueprint`** = the domain-and-weight structure that document describes.

**Conventions proposed at Chapter 3** (see "Convention locks proposed at Chapter 3"):

4. **`kube-apiserver`** is the component name; **"the API server"** is the prose form.
5. **No `§N` in cross-bearings that point into undrafted chapters.**
6. **"absent-component pattern"** is the canonical name for B3's cross-cutting theme.

Last updated: 2026-08-24 (Chapter 3, Stage 14)
Terms tracked: 68 — 31 defined · 7 conventions · 28 reserved · 2 optional

---

## ⚑ READ THIS FIRST — this ledger has a Chapter 2 hole

**Chapter 2 never ran Stage 13 or Stage 14.** Verified on disk 2026-08-24:
`.pipeline-state/ch-02/` contains no `integration.md` and no `kb-manifest.md`, though
`chapter-02-cargo-in-standard-crates.md` is shipped at the book root. Chapter 2 is the
book's containerization chapter (competency **D1.4**) and it owns the definitions for
`container`, `container image`, `image layer`, `tag` vs `digest`, `immutability`,
`registry`, `CRI`, `containerd`, `CRI-O`, `runC`, `RuntimeClass`, and the named pattern
"Kubernetes defines an interface and lets the ecosystem implement it."

**None of those are in this ledger.** They are listed under "Tier 4 — Chapter 2 gap"
below with defining chapter recorded and **no definitions written**, because writing
them here would mean doing Chapter 2's Stage 14 without Chapter 2's integration report
— exactly the definitional drift Rule 5 forbids. Chapter 3 leans on all of them.

**Backfill by running Chapter 2 Stages 13 and 14 before the reconcile pass.**

**Second recovery item:** Chapter 1's Stage 14 composed this ledger and nine other KB
files, and none of them reached disk (the same executor write failure). This file
reconstructs Chapter 1's tiers verbatim from `.pipeline-state/ch-01/kb-manifest.md`,
which is byte-exact on disk. Chapter 1's **seven concept shards** were NOT reconstructed
here — replay them directly from that manifest's own `=== WRITE ===` blocks.

---

## Tier 1 — Defined (prose inherited verbatim from chapter text)

### A

**absent-component pattern** — "An object can exist while nothing at all happens, if the
component that would act on it is absent. The object is real; it's stored; `kubectl get`
will show it to you. But an object is a *description*, and descriptions don't do anything
by themselves. Something has to be watching for it and willing to act." Canonical short
form: **"an object without its component does nothing."** (Ch 3 §4, ⚓ Worth Securing)
> **Canonical name — do not re-coin.** B3 names this as one of nine cross-cutting themes
> and schedules it for retrieval *by name*. Chapters 10, 13, and 17 must use this exact
> phrase. See `concepts/absent-component-pattern.md`.

**addon** — "Addons extend the functionality of Kubernetes." Published examples: DNS,
Web UI (Dashboard), Container Resource Monitoring, Cluster-level Logging. Addons "run
*on* the cluster rather than constituting it. A cluster with none of them installed is
still a cluster." (Ch 3 §4)
> Spelling: **`addon`**, one word, per the Kubernetes documentation. Ch 3 line ~466
> reads "add-on" once; flagged for correction.

**API server, the** — *prose form of* **kube-apiserver**. See convention 4.

### B

**binding** — the process by which "the scheduler notifies the API server about its
decision." *Partial: Chapter 3 gives the term one clause, in service of the boundary
that the scheduler selects and records but does not start anything.*
[source: k8s-docs-kube-scheduler-2026-08-23] (Surfaced Ch 3 §2 · full treatment **Ch 7**)

**Borg** — Google's internal production container-orchestration system; Kubernetes "drew
on Google's internal container-orchestration experience with the Borg system and its
research successor Omega." [source: k8s-history-ten-years-2026-08-23] (Ch 3 §1)

### C

**CKA (Certified Kubernetes Administrator)** — "a genuinely hands-on exam taken in a
live terminal." *Partial: Chapter 1 defines it only by contrast with the KCNA's
multiple-choice format.* (Surfaced Ch 1 §1 · full treatment Ch 17 §4)

**cloud-controller-manager** — "A Kubernetes control plane component that embeds
cloud-specific control logic. The cloud controller manager lets you link your cluster
into your cloud provider's API, and separates out the components that interact with that
cloud platform from components that only interact with your cluster. It runs only
controllers that are specific to your cloud provider." **Optional:** "If you are running
Kubernetes on your own premises, or in a learning environment inside your own PC, the
cluster does not have a cloud controller manager."
[source: k8s-docs-cluster-architecture-2026-08-23] (Ch 3 §2)

**cloud native** — "describes characteristics of how a system is built and operated."
It does **not** mean "runs in a public cloud": "The CNCF's own definition covers
workloads deployed across public, private, and hybrid environments."
*DEFERRING ENTRY — the positive definition, with each characteristic examined, is
Chapter 17 §1. Chapter 1 §4 deliberately withholds it for four hundred pages; this
entry preserves that device by carrying only the negative claim, which §4 states
outright anyway.* (Surfaced Ch 1 §1 · defined Ch 17 §1)
> ⚑ AUTHOR DECISION OPEN. Stage 13 referred the glossary-vs-§4 collision without
> defaulting it. Options were: (a) this deferring entry, (b) a full entry accepting
> the spoil, (c) omission. (a) is implemented. Reversible — only this entry changes.

**cluster** — "A Kubernetes cluster consists of a control plane plus a set of worker
machines, called nodes, that run containerized applications. Every cluster needs at
least one worker node in order to run Pods."
[source: k8s-docs-cluster-architecture-2026-08-23] (Ch 3 §2)

**CNCF (Cloud Native Computing Foundation)** — the open-source foundation that hosts
Kubernetes; "part of the nonprofit **Linux Foundation**." Kubernetes was "donated by
Google to the newly formed Cloud Native Computing Foundation as its **first project**."
(Ch 1 §1, Soundings A3 · extended Ch 3 §1 · full treatment Ch 17 §2)

**competency** — *convention, see Tier 2.*

**container** — "a process on the host that has been given an isolated view of the
system." Shares the host's **operating system kernel** with the host; contrast with a
virtual machine, which "boots its own operating system on virtualized hardware."
*Partial: Chapter 1 Soundings A1 gives the discriminating fact only.*
(Surfaced Ch 1 · full treatment **Ch 2 §1 — entry pending Ch 2 Stage 14**)
> ⚑ **STATUS CORRECTED AT CHAPTER 3 — supersedes Chapter 1's flag.** Chapter 1's
> Stage 14 marked this "PROVISIONAL WORDING" and instructed that "Chapter 2's Stage 14
> must NOT lock the sharpened form until this is resolved." **That instruction is now
> stale.** Chapter 2 §1 (ch02:281–285) adjudicates both registers as correct and tells
> the reader to hold both: *"**operating system** as the published wording, **kernel**
> as the mechanism underneath it,"* with an in-cache warrant from
> `k8s-docs-runtime-class-2026-08-23` ("a user-space kernel (such as gVisor)").
> Chapter 3 §1 follows Chapter 2: it quotes the snapshot when citing and carries the
> kernel precision as a visibly authorial, untagged sentence.
>
> **Chapters 1, 2, and 3 therefore agree on substance.** The only open item is
> *attribution*: whether ch01:142's bolded "operating system kernel" may sit on a line
> tagged `k8s-docs-overview-2026-08-23`. Blocked on harvest items A13/A14, per Chapter
> 2's own AUTHOR-REVIEW, which prescribes deleting Chapter 1's parallel flag once they
> land.
>
> ⚠ **Chapter 3's §1 AUTHOR-REVIEW (draft line ~130) misreports this**, calling
> Chapter 1 "the remaining outlier." Acting on that note would flatten ch01:142 toward
> "operating system" and delete the register Chapter 2 spends three paragraphs
> establishing and Figure 2-1 depends on. **Do not act on it.**
> See `concepts/deployment-eras.md`.

**container runtime** — *(two-part definition; both parts are real and neither
supersedes the other)*
- **As a runtime chain participant (Ch 2 §4):** the CRI implementation the kubelet
  speaks to, above the low-level runtime. *Entry pending Ch 2 Stage 14.*
- **As a node component (Ch 3 §3):** "A fundamental component that empowers Kubernetes
  to run containers effectively. It is responsible for managing the execution and
  lifecycle of containers within the Kubernetes environment. Kubernetes supports
  container runtimes such as containerd, CRI-O, and any other implementation of the
  Kubernetes CRI." It is "the one node component that is not Kubernetes software at all."
  [source: k8s-docs-cluster-architecture-2026-08-23]

**control loop** — ★ **Fixed Point.** "A control loop is: a desired state, a current
state, and an action that closes the gap between them — repeating, without terminating."
Documentation framing: "In robotics and automation, a control loop is a non-terminating
loop that regulates the state of a system."
[source: k8s-docs-controllers-2026-08-23] (Ch 3 §6)

**control plane** — the half of a cluster that "manages the worker nodes and the Pods in
the cluster"; its components "make global decisions about the cluster — scheduling, for
example — as well as detecting and responding to cluster events." "In production
environments, the control plane usually runs across multiple computers … providing fault
tolerance and high availability." Five components: kube-apiserver, etcd, kube-scheduler,
kube-controller-manager, cloud-controller-manager (optional).
[source: k8s-docs-cluster-architecture-2026-08-23] (Ch 3 §2)

**control via API server** — the common controller shape: the controller "does not run
any Pods or containers itself. Instead, [it] tells the API server to create or remove
Pods. Other components in the control plane act on the new information."
[source: k8s-docs-controllers-2026-08-23] (Ch 3 §6)

**controller** — "In Kubernetes, controllers are control loops that watch the state of
your cluster, then make or request changes where needed. Each controller tries to move
the current cluster state closer to the desired state." A controller "tracks at least one
Kubernetes resource type" and "might carry the action out itself; more commonly, in
Kubernetes, a controller will send messages to the API server that have useful side
effects." [source: k8s-docs-controllers-2026-08-23] (Ch 3 §6)

**curriculum** — *convention, see Tier 2.*

**current state** — the half of a control loop that reports what is true. Thermostat
framing: "The actual room temperature is the current state."
[source: k8s-docs-controllers-2026-08-23] (Ch 3 §6)

### D

**desired state** — the half of a control loop that records what was asked for.
Thermostat framing: "When you set the temperature, that's telling the thermostat about
your **desired state**." Objects "carry a field that represents the desired state, and
the controller for that resource is responsible for making the current state come closer
to it." [source: k8s-docs-controllers-2026-08-23] (Ch 3 §6 · mechanics **Ch 4**)

**direct control** — the less common controller shape, used when a controller "need[s] to
make changes to things outside your cluster." Such controllers "find their desired state
from the API server, then communicate directly with an external system to bring the
current state closer in line." Documentation's example: provisioning new Nodes.
[source: k8s-docs-controllers-2026-08-23] (Ch 3 §6)

**domain** — *convention, see Tier 2.*

### E

**etcd** — "Consistent and highly-available key value store used as Kubernetes' backing
store for all cluster data. If your Kubernetes cluster uses etcd as its backing store,
make sure you have a back up plan for the data." "Access to etcd is equivalent to root
permission in the cluster, so ideally only the API server should have access to it."
[source: k8s-docs-cluster-architecture-2026-08-23]
[source: k8s-docs-etcd-access-control-2026-08-24 — ⚑ SNAPSHOT NOT ON DISK]
(Ch 3 §2, §5 · backup/restore **Ch 8** · encryption at rest **Ch 12**)
> The chapter is careful that the confinement is a **recommendation with a security
> reason**, not an invariant: the docs say "*ideally* only the API server should have
> access." Do not harden this to an absolute downstream.

### H

**hub-and-spoke API pattern** — "Kubernetes has a hub-and-spoke API pattern. All API
usage from nodes and the Pods they run terminates at the API server, and none of the
other control-plane components are designed to expose remote services."
[source: k8s-docs-control-plane-node-communication-2026-08-24 — ⚑ SNAPSHOT NOT ON DISK]
(Ch 3 §5)
> **Scope, precisely.** This describes how *state* moves. It is not a claim that no
> connection ever runs outward: the API server does open connections to kubelets for
> logs, attach, and port-forward. "Those paths carry a session, not an instruction."

### K

**KCNA (Kubernetes and Cloud Native Associate)** — "the usual entry point to the cloud
native certification family." The Linux Foundation "describes it as demonstrating 'a
user's foundational knowledge and skills in Kubernetes and the wider cloud native
ecosystem.'" Experience level: beginner. Prerequisites: none.
[source: lf-kcna-exam-page-2026-08-23] (Ch 1 §1)

**kube-apiserver** — "The API server is the component of the control plane that exposes
the Kubernetes API. **The API server is the front end for the Kubernetes control plane.**
kube-apiserver is designed to scale horizontally: it scales by deploying more instances.
You can run several instances and balance traffic between them."
[source: k8s-docs-cluster-architecture-2026-08-23]
[source: k8s-docs-components-2026-08-23] (Ch 3 §2, §5)

**kube-controller-manager** — "Control plane component that runs controller processes.
Logically, each controller is a separate process, but to reduce complexity, they are all
compiled into a single binary and run in a single process." Named examples: Node
controller, Job controller, EndpointSlice controller, ServiceAccount controller.
[source: k8s-docs-cluster-architecture-2026-08-23] (Ch 3 §2)
> ⚠ **One binary, one process.** There is no per-controller unit of any kind — not a
> process, not a container, not a Pod.

**kube-proxy** — "kube-proxy is a network proxy that runs on each node in your cluster,
implementing part of the Kubernetes Service concept. kube-proxy maintains network rules
on nodes. These network rules allow network communication to your Pods from network
sessions inside or outside of your cluster." **Optional:** "If you use a network plugin
that implements packet forwarding for Services by itself, and providing equivalent
behavior to kube-proxy, then you do not need to run kube-proxy on the nodes in your
cluster." [source: k8s-docs-cluster-architecture-2026-08-23] (Ch 3 §3 · Services **Ch 9**)

**kube-scheduler** — "Control plane component that watches for newly created Pods with no
assigned node, and selects a node for them to run on. Factors taken into account for
scheduling decisions include individual and collective resource requirements,
hardware/software/policy constraints, affinity and anti-affinity specifications, data
locality, inter-workload interference, and deadlines."
[source: k8s-docs-cluster-architecture-2026-08-23] (Ch 3 §2 · full treatment **Ch 7**)
> **Boundary that must not drift:** "the scheduler selects a node and records that
> choice. It does not start anything." The kubelet on the chosen node starts containers.

**kubelet** — "An agent that runs on each node in the cluster. It makes sure that
containers are running in a Pod. The kubelet takes a set of PodSpecs that are provided
through various mechanisms and ensures that the containers described in those PodSpecs
are running and healthy. **The kubelet doesn't manage containers which were not created
by Kubernetes.**" [source: k8s-docs-cluster-architecture-2026-08-23]
(Ch 2 §4 chain · Ch 3 §3 as node component)

### L

**Linux Foundation, The** — the nonprofit organization that publishes the KCNA exam and
of which CNCF is part. *Partial.* (Ch 1 §1)

**Lodestar, The** (book artifact) — "a single page holding the exam-critical facts,
distinctions, and traps, distilled from the whole book. It's the last thing to read
before the exam." Ships as `the-lodestar.md` at the book root. (Ch 1 §5)

### N

**node / worker node** — the worker machines of a cluster, which "host the Pods that are
the components of the application workload." Node components — kubelet, kube-proxy
(optional), container runtime — "run on every node, maintaining running Pods and
providing the Kubernetes runtime environment."
[source: k8s-docs-components-2026-08-23] (Ch 3 §2, §3)

### O

**Omega** — the **research successor** to Borg, a separate project rather than a rename.
"Borg was the production system; Omega is described as its research successor.
Kubernetes inherited from both."
[source: k8s-history-ten-years-2026-08-23] (Ch 3 §1)

**orchestration (technical sense)** — ★ **Fixed Point.** "**The technical definition of
orchestration is execution of a defined workflow: first do A, then B, then C.**"
Kubernetes explicitly disclaims it: "Kubernetes is not a mere orchestration system. In
fact, it eliminates the need for orchestration … Kubernetes comprises a set of
independent, composable control processes that continuously drive the current state
towards the provided desired state. It shouldn't matter how you get from A to C.
Centralized control is also not required."
[source: k8s-docs-overview-2026-08-23] (Ch 3 §1 Snag · resolved Ch 3 §7)

**orchestrator / container orchestration (loose, industry sense)** — "Kubernetes is an
**orchestrator** — it decides what should run where." (Ch 1 Soundings A2)
> ⚑ **RULE 6 — Chapter 3 SPLITS this term rather than completing it.** Chapter 1's
> Stage 14 recorded one entry with "full treatment Ch 3." Chapter 3 does not deliver one
> definition; it delivers **two senses that disagree**, and the disagreement is the
> chapter's Zenith. The loose sense above is correct at orientation altitude and is how
> the industry speaks. The precise sense (previous entry) is what the exam tests and
> what Kubernetes rejects. Chapter 3 §1 flags its own Chapter 1 wording as the loose
> sense and settles it in §7. **Keep both rows. Do not merge them.**

### P

**PodSpec** — "the description of what containers should run." *Partial — Chapter 3 §3
gives a one-line placeholder only.* (Surfaced Ch 3 §3 · full treatment **Ch 5**)
> ⚑ Chapter 3 §3 prose says "**Chapter 4** gives it a proper treatment" while the
> cross-bearing directly beneath it points to **Ch 5**, and ch02:318 already promised
> the Pod to Ch 5. B2 gives Ch 4 the generic `spec`/`status` fields; the PodSpec proper
> is Ch 5. **This ledger records Ch 5.** Chapter 3's prose needs the fix.

### R

**reconciliation** — "continuous comparison, no defined sequence" — *contrast with
orchestration.* (Ch 3, Practice Q20 distractor rationale)
> ⚑ **DEFINITION GAP, recorded rather than filled.** Chapter 3 uses "reconciliation"
> three times — including in §Why This Chapter Matters, which asks the reader to "sketch
> a reconciliation loop from memory" *before the word is introduced* — but its ★ Fixed
> Point defines "**control loop**" and never ties the two words together. The clause
> above is the only definitional text in the chapter and it is buried in an answer key.
> Per Rule 5 no better definition is invented here.
>
> **Recommended chapter fix:** one appositive at the §6 ★ Fixed Point tying
> "reconciliation" to "control loop." B3 runs the control-loop theme through Ch 4, 6,
> 11, 15, and 17; the word must be retrievable by then.

### V

**virtual machine** — "boots its own operating system on virtualized hardware."
Chapter 3 extends: "each VM is a full machine running all the components, including its
own operating system, on top of virtualized hardware."
*Partial: contrast with container only.* (Surfaced Ch 1 · full treatment Ch 2 §1)

---

## Tier 2 — Convention locks (NOT chapter definitions)

### Locked at Chapter 1

Used precisely throughout Chapter 1 but never explicitly defined there. Recorded as
conventions so nothing masquerades as inherited prose.

| Term | Convention | Status |
|---|---|---|
| **blueprint** | The domain-and-weight *structure* the CNCF curriculum describes | Proposed — Ch 1 body follows it 11×; subtitle and §3 heading say "curriculum" rhetorically |
| **curriculum** | The CNCF-published *document* (`KCNA_Curriculum.pdf`) | Proposed — pairs with the above |
| **competency** | A named topic *inside* a domain. There are **13** | Proposed — see `objective-coverage.md` for the count discrepancy against B2 |
| **domain** | One of the four weighted blocks: 44 / 28 / 16 / 12 | Proposed |

### Convention locks proposed at Chapter 3

Chapter 3 is the first chapter to establish book-wide naming and cross-reference
practice, because it is the first chapter other chapters must agree with.

| Term / rule | Convention | Why it needs locking |
|---|---|---|
| **`kube-apiserver` vs "the API server"** | `kube-apiserver` is the **component name** (census, tables, Fixed Points); **"the API server"** is the **prose reference**. Ch 3 uses the split 15 / 61 times and never mixes them. | The split matches upstream docs but is *established here*. Ch 4–8 reference this component constantly and will drift without the rule. |
| **No `§N` into undrafted chapters** | A cross-bearing may name `§N` only when the target chapter has shipped. Otherwise point at the chapter and topic alone. | Ch 17's section numbers are pre-committed **inconsistently** by three chapters: Ch 1 reserves §1 (cloud native definition), §2 (CNCF governance), §4 (certification ladder); Ch 2 reserves **§4** (four pluggable interfaces); Ch 3 merges Ch 1's §1 and §2 into one §1. **Ch 1 §4 and Ch 2 §4 conflict independently of Chapter 3.** Ch 3 already follows this instinct for 18 of its 20 forward bearings. |
| **"absent-component pattern"** | The canonical name for B3's cross-cutting theme "the object exists but nothing happens without the component." | B3 schedules it for retrieval **by name**. If Ch 10, 13, and 17 each re-coin it, four gotchas stay four gotchas instead of collapsing into one rule. |

**Ch 17 section-number reservation — unresolved, carried forward.** Recorded here so the
reconcile pass has one place to look. Resolving it is an author action.

---

## Tier 3 — Reserved (surfaced but not defined — NO definition written)

Defining chapters assigned from B2 (`chapter-lineup.md`, ratified).

### Reserved at Chapter 1

| Term | Defining chapter | First surfaced |
|---|---|---|
| CNCF Cloud Native Definition v1.1 | Ch 17 | Ch 1 §4 |
| Container Runtime Interface (CRI) | Ch 2 | Ch 1 Soundings A2 (cross-bearing label) |
| declarative vs imperative | Ch 4 | Ch 1 Soundings Q5 |
| deployment strategy | Ch 6 (mechanics) / Ch 15 (vocabulary) | Ch 1 §3 |
| exporter | Ch 18 | Ch 1 §6 (Logbook Entry) |
| GitOps | Ch 15 | Ch 1 §3 |
| Helm | Ch 14 | Ch 1 §3 |
| `kubectl` | Ch 8 | Ch 1 §1 |
| metrics | Ch 18 | Ch 1 §3 |
| observability | Ch 18 | Ch 1 §3 |
| OpenTelemetry | Ch 18 | Ch 1 §3 |
| Pod | Ch 5 | Ch 1 §1 |
| Prometheus | Ch 18 | Ch 1 §3 |
| PromQL | Ch 18 | Ch 1 §6 (Logbook Entry) |
| scheduler / scheduling | Ch 7 | Ch 1 §1 |
| scrape (pull) model | Ch 18 | Ch 1 §6 (Logbook Entry) |
| Service | Ch 9 | Ch 1 §1 |
| StatefulSet | **Ch 6** (introduced) / Ch 11 (completed) | Ch 1 §5 (cross-bearing label) |
| traces | Ch 18 | Ch 1 §3 |

### Reserved at Chapter 3

| Term | Defining chapter | First surfaced | Note |
|---|---|---|---|
| **Argo CD** | Ch 15 | Ch 3 §5 ⚓ | Named + source-tagged, forward-beared |
| **CI/CD** | Ch 15 | Ch 3 §1 | ⚑ **Acronym never expanded** — first use in the book |
| **CNI (Container Network Interface)** | Ch 9 | Ch 3 §3 (as "network plugin") | Ch 3 says "network plugin"; the interface is named in Ch 2 |
| **`crictl`** | Ch 13 §5 | Ch 3 §3 (cross-bearing) | Agrees with ch02:602's identical §5 pointer |
| **EndpointSlice** | Ch 9 | Ch 3 §2 (controller list) | Name-dropped only |
| **Ingress / Ingress controller** | Ch 10 | Ch 3 §4 (cross-bearing) | Absent-component pattern, first recurrence |
| **Job** | Ch 6 | Ch 3 §6 | Used as the documentation's own controller example; the *resource* is Ch 6's |
| **`kubectl top`** | Ch 13 | Ch 3 §4 (cross-bearing) | Absent-component pattern instance |
| **`kube-system` namespace** | Ch 4 | Ch 3, Bearings #1 Q3 distractor | Distractor only |
| **Lease** | Ch 8 (node lifecycle, per lineup — corrected 2026-08-24) | Ch 3, Bearings #1 Q4 rationale | Name-dropped only |
| **metrics-server** | Ch 13 | Ch 3 §4 (cross-bearing) | Absent-component pattern instance |
| **NetworkPolicy** | Ch 10 | *(not yet surfaced — see below)* | B3's 4th absent-component instance; Ch 3 omits the bearing |
| **PaaS** | — *(no owner chapter)* | Ch 3 §1 | ⚑ **Acronym never expanded** — first use in the book. Needs an owner. |
| **Pod** | Ch 5 | Ch 1 §1 · used ~40× in Ch 3 | ⚑ See below |
| **PodSpec** | Ch 5 | Ch 3 §3 | See Tier 1 partial + Ch 4/Ch 5 conflict |
| **ServiceAccount** | Ch 12 | Ch 3 §2 (controller list) | Name-dropped only |
| **VPA (Vertical Pod Autoscaler)** | Ch 17 | Ch 3 §4 (cross-bearing) | ⚑ **Acronym never expanded**; appears only inside a cross-bearing |

> ⚑ **`Pod` is Chapter 3's most-used undefined primitive.** It appears roughly 40 times
> and is load-bearing — the scheduler assigns Pods, the Job controller creates Pods, a
> cluster "needs at least one worker node in order to run Pods." Chapter 2 set the
> reader up for the deferral explicitly ("It is Chapter 5's whole subject", ch02:318);
> Chapter 3 never repeats that promise. **Recommended chapter fix:** one sentence at
> first use in §2 — *"A Pod is the unit Kubernetes schedules; Chapter 5 is its whole
> subject."* This ledger writes no definition (Rule 5).

**Optional (product names — author call whether they belong in a published glossary):**
LFS250 (Ch 1 §2), THRIVE-ONE (Ch 1 §2).

**Deliberately excluded:**
- Terraform, Ansible, CloudFormation — external tools named for calibration in
  Soundings Q5; not KCNA exam terms.
- Branded markers (🧭 ☆ ★ ⚠ — 🏆 ☀️), inline glyphs (⚓ 🪝 🔭 🪢), sidebar types,
  cross-bearings, difficulty indicators (⚪🔵🟡🔴) — brand-level canon, authoritative in
  `knowledge-base/voice/branded-terms.yaml`.

---

## Tier 4 — Chapter 2 gap (shipped chapter, Stage 14 never ran)

**No definitions written.** These are Chapter 2's to define, Chapter 2 shipped, and
Chapter 2's Stage 14 did not run. Chapter 3 depends on every one.

| Term | Defining chapter | Chapter 3's dependence |
|---|---|---|
| container image | Ch 2 §2 | Practice Q25 retrieval item |
| image layer / tag vs digest | Ch 2 §2–3 | Bearings #1 Q4 distractor D ("cached container image layers") |
| immutability (stateless & immutable) | Ch 2 §2 | Practice Q24 retrieval item; §6 "replace, don't mutate" |
| registry | Ch 2 §3 | Bearings #1 Q4 rationale |
| **CRI (Container Runtime Interface)** | Ch 2 §4 | Bearings #1 Q5 retrieval item; §3 census |
| containerd | Ch 2 §4 | §3 census; Practice Q13 |
| CRI-O | Ch 2 §4 | §3 census; Practice Q13 |
| runC | Ch 2 §4 | Ch 2's Fixed Point chain |
| RuntimeClass | Ch 2 §7 | not used in Ch 3 |
| relaxed isolation | Ch 2 §1 | §1 deployment eras; Practice Q2 |
| **"Kubernetes defines an interface and lets the ecosystem implement it"** | Ch 2 §4 (⚓, named) | ⚑ See Rule 6 flag below |

> ⚑ **RULE 6 — Chapter 3 §3 broadens Chapter 2's named pattern past its enumeration.**
> Ch 3 §3 (draft line ~325) says of etcd and the container runtime: *"That is the same
> architectural instinct… Where a good general-purpose component already exists,
> Kubernetes defines an interface and uses it rather than reimplementing it."*
>
> Chapter 2's pattern is specifically *"Kubernetes defines an interface and lets the
> **ecosystem** implement it"* (ch02:598), and its sourced enumeration is **CRI, CSI,
> CNI, device plugins, and API extensions**
> [source: k8s-docs-extending-kubernetes-2026-08-23]. **etcd is not among them** —
> Kubernetes does not define an etcd interface; it consumes a general-purpose datastore.
> The claim is true of the *runtime* and true-but-different of *etcd*, and calling them
> "the same" broadens a sourced list past what it says.
>
> Compounding it: ch02:596–598 is a section titled "The pattern to name now" whose ⚓
> tells the reader *"Give this move a name in your head, because you are about to see it
> three more times."* Chapter 3 hits the first recurrence, re-derives it in fresh words,
> **and never uses the name or bears back to Ch 2 §4.** That is a missed spaced-retrieval
> event on a theme B3 tracks and Ch 17's secondary Zenith depends on.
>
> **Recommended chapter fix:** separate the two instincts — keep the named pattern for
> the container runtime, cross-beared to Ch 2 §4; describe etcd as the adjacent-but-
> distinct instinct of reusing an existing general-purpose component.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===
# Concept: The control loop

**Home:** Chapter 3 §6 · **Competency:** D1.1 · **Status:** canonical
**Depth here:** the single most important concept in the book's structure.

## ★ Fixed Point (verbatim — do not reword)

> **A control loop is: a desired state, a current state, and an action that closes the
> gap between them — repeating, without terminating.**
>
> A Kubernetes controller is a control loop that watches cluster state and acts to move
> current state closer to desired state. It does this continuously, not once. It usually
> acts by asking the API server to change something, not by doing the thing itself.
> [source: k8s-docs-controllers-2026-08-23]

## What Chapter 3 establishes

- **The thermostat framing, from the documentation.** "In robotics and automation, a
  control loop is a non-terminating loop that regulates the state of a system." Setting
  the temperature "is telling the thermostat about your **desired state**"; the actual
  room temperature "is the **current state**."
- **The chapter's own gloss on why that matters:** a thermostat "doesn't execute a
  heating plan… It compares two numbers and acts on the difference, then does it again,
  and again, forever." Nobody wrote a rule about open windows or lit fires.
- **Two controller shapes.** *Control via API server* (common): "The Job controller does
  not run any Pods or containers itself. Instead, the Job controller tells the API server
  to create or remove Pods. Other components in the control plane act on the new
  information." *Direct control* (uncommon): controllers "find their desired state from
  the API server, then communicate directly with an external system."
- **Controllers report on themselves through the same shared state.** "Once the work is
  done for a Job, the Job controller updates that Job object to mark it Finished."
- **The never-stable design position.** "Your cluster never reaches a stable state. As
  long as the controllers for your cluster are running and able to make useful changes,
  it doesn't matter if the overall state is stable or not." The health question is not
  *"has it settled?"* but *"are the loops running, and can they still make useful
  changes?"*
- **Self-healing re-read as loops.** §1 lists self-healing as a capability; §6 turns it
  into a description of loops running: "A gap opens between what you asked for and what
  exists, and something closes it. Nobody triggered anything."

## Figure

`ch03-fig02-control-loop-desired-vs-current` — deliberately drawn with **no entry arrow
and no terminus**. The caption states why: "A loop drawn with a beginning teaches the
wrong thing: this one was already running before your request arrived and will still be
running after it's satisfied." Any redraw must preserve that.

## ⚑ Terminology gap — "reconciliation" is never tied to "control loop"

Chapter 3 uses "reconciliation" three times, including in §Why This Chapter Matters,
which asks the reader to "sketch a reconciliation loop from memory" **before the word is
introduced.** The ★ Fixed Point defines "control loop" and never bridges to it. The only
definitional text in the chapter is Practice Q20's distractor rationale: "reconciliation
is the opposite shape: continuous comparison, no defined sequence."

**Fix:** one appositive at the ★ Fixed Point. B3 runs this theme through Ch 4, 6, 11, 15,
and 17 — the word must be retrievable by then. See `glossary.md` § reconciliation.

## ⚑ Forward-count claim is off by one, and omits a chapter

Chapter 3 states three times (Attention Budget, Soundings rubric, §Why This Chapter
Matters) that **"six later chapters retrieve §6 by name."**

B3's control-loop theme is **Ch 3 → 4 → 6 → 11 → 15 → 17** — that is **five** later
chapters. The draft's own forward cross-bearings name only four (Ch 4, 6, 15, 17) and
**omit Ch 11 entirely.**

**Fix:** change to "five" and add the Ch 11 bearing, or soften to "later chapters." Three
occurrences, one decision.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| Ch 4 | Deliver the `spec` field as "the field that holds desired state," and `status` as its counterpart. §6 forward-bears to this repeatedly. |
| Ch 6 | Instantiate the loop in ReplicaSet — "a control loop you can watch working in real time." B2 calls this the second beat of the book's spine. |
| Ch 11 | **Currently unbeared from Ch 3.** B3 places the theme here (StatefulSet/PV). Either add the bearing in Ch 3 or accept the gap knowingly. |
| Ch 15 | **Primary Zenith.** "The same loop, with a Git repository holding desired state." B1 identifies this as the book's strongest synthesis opportunity; the whole Part IV ordering exists to set it up. Argo CD is named and source-tagged in Ch 3 §5 so the recognition lands. |
| Ch 17 | "The same pattern, named as a principle" — one of the things "cloud native" means. |

## Related

[[absent-component-pattern]] · [[api-server-hub]] · [[orchestration-technical-definition]]
· [[control-plane-components]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===
# Concept: The absent-component pattern

**Home:** Chapter 3 §4 · **Competency:** D1.1 · **Status:** canonical, **named**
**B3 classification:** one of nine cross-cutting themes; the only one that is a *pattern*
rather than a fact.

## ⚓ Worth Securing (verbatim — this is the canonical wording)

> **An object can exist while nothing at all happens, if the component that would act on
> it is absent. The object is real; it's stored; `kubectl get` will show it to you. But
> an object is a *description*, and descriptions don't do anything by themselves.
> Something has to be watching for it and willing to act. Remember the phrase: **an
> object without its component does nothing.** You're going to meet it four more times in
> this book, and each time it will look like a completely different problem until you
> recognize it.**

## ⚑ USE THIS NAME. DO NOT RE-COIN IT.

B3 schedules this theme for retrieval **by name**, and states the reason plainly:
*"Naming it once and retrieving it by name turns four gotchas into one rule."*

If Chapters 10, 13, and 17 each invent their own phrasing, the reader gets four
unrelated gotchas to memorize instead of one rule to apply. **Canonical name:
"absent-component pattern." Canonical short form: "an object without its component does
nothing."**

## How Chapter 3 earns it

Cluster DNS is the honest illustration, and the chapter is careful about whose claim is
whose. DNS is *formally an addon* — a cluster extension, not a control-plane or node
component — and is *"described as a built-in Kubernetes service, launched automatically
by the addon manager"* [source: k8s-docs-dns-cluster-addon-2026-08-24]. That it is
near-universal in practice is marked explicitly as **the author's field observation, not
a documented claim.**

That gap — *near-universal in practice* vs *not part of the cluster's definition* — is
exactly where the pattern lives. Bearings #2 Q3's rationale states it: "Something can be
*near-universal in practice* and still *not part of the cluster's definition*."

## ⚑ Count mismatch: "four more times," three bearings

Chapter 3 promises four recurrences and bears only three:

| # | Instance | Chapter | Beared in Ch 3? |
|---|---|---|---|
| 1 | Ingress with no Ingress controller | Ch 10 | ✓ |
| 2 | `kubectl top` with no metrics-server | Ch 13 | ✓ |
| 3 | VPA is an add-on, not shipped by default | Ch 17 | ✓ |
| 4 | **NetworkPolicy on a CNI that doesn't enforce it** | Ch 10 | ✗ **missing** |

The Ch 9 CoreDNS bearing that sits alongside these is a **DNS pointer, not an
absent-component instance** — it must not be counted as the fourth.

B3's named fourth instance is NetworkPolicy-on-a-non-enforcing-CNI, which is also Ch 10
material. **Adding that bearing makes the count exact and matches B3's theme.** Chapter 2
got the parallel discipline right at ch02:598 ("three more times," three instances).

## Downstream obligations — binding

| Chapter | Obligation |
|---|---|
| Ch 9 | CoreDNS as the cluster DNS addon. **Do not** frame this as an absent-component instance; it is the pointer that sets up the pattern. |
| Ch 10 | **Two** instances: Ingress without a controller (first recurrence, explicitly beared) **and** NetworkPolicy on a non-enforcing CNI (B3's fourth, currently unbeared). Retrieve the pattern **by name** in at least one. |
| Ch 13 | `kubectl top` with no metrics-server. Retrieve by name. |
| Ch 17 | VPA as an add-on not shipped by default. This is the last recurrence and the natural place to collect all four. |

## Related

[[optional-components]] · [[control-loop]] · [[node-components]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-plane-components.md ===
# Concept: Control-plane components

**Home:** Chapter 3 §2 · **Competency:** D1.1 · **Status:** canonical

## The cluster shape

"A Kubernetes cluster consists of a control plane plus a set of worker machines, called
nodes, that run containerized applications. Every cluster needs at least one worker node
in order to run Pods. The worker nodes host the Pods that are the components of the
application workload. The control plane manages the worker nodes and the Pods in the
cluster. In production environments, the control plane usually runs across multiple
computers and a cluster usually runs multiple nodes, providing fault tolerance and high
availability." [source: k8s-docs-cluster-architecture-2026-08-23]

The control plane's components "make global decisions about the cluster — scheduling, for
example — as well as detecting and responding to cluster events, such as starting up a
new Pod when a controller's declared replica count is unsatisfied."

## The five

| Component | One job | Optional? |
|---|---|---|
| **kube-apiserver** | Exposes the Kubernetes HTTP API. **The front end for the control plane.** Scales horizontally by adding instances. | no |
| **etcd** | Consistent, highly-available key value store; backing store for **all** cluster data. | no |
| **kube-scheduler** | Watches for newly created Pods with no assigned node and **selects** a node. | no |
| **kube-controller-manager** | Runs controller processes. **One binary, one process.** | no |
| **cloud-controller-manager** | Embeds cloud-specific control logic; links the cluster to a cloud provider's API. | **yes** |

## Two boundaries that must not drift

**1. The scheduler selects; it does not start.** "The scheduler selects a node and records
that choice. It does not start anything." It "notifies the API server about its decision,
in a process called binding" [source: k8s-docs-kube-scheduler-2026-08-23]. The kubelet on
the chosen node starts the containers. Chapter 3 calls the contrary belief — that the
scheduler contacts the node — "the highest-value wrong answer on the page, because the
belief behind it is genuinely widespread."

**2. One binary, one process.** "Logically, each controller is a separate process, but to
reduce complexity, they are all compiled into a single binary and run in a single
process." Chapter 3's ⚠ Navigational Hazards spells out the failure mode: candidates
answer "one process per controller," "one container per controller," or "one Pod per
controller." **All three are wrong for the same reason: there is no per-controller unit of
any kind.**

## etcd — the two words worth unpacking

The official description is terse. Chapter 3 unpacks two words and marks the unpacking as
**its own, not the documentation's**: *"all cluster data"* means every object you created,
every object the system created, every piece of state the cluster knows about; and
*"consistent"* "is what lets independent components reading the same shared state work
from the same picture of the world rather than from private, drifting copies."

The ⚓ callout is the reusable payload: other components "can be killed, restarted, or
replaced and rebuild their working picture from what etcd holds. etcd itself holds the
thing that cannot be rebuilt from anywhere else."

## 🪢 The mnemonic (verbatim — it is a sorting rule, not an acronym)

> "Five components, and they sort themselves. **Three named `kube-`** (apiserver,
> scheduler, controller-manager) are the core Kubernetes control-plane processes. **One
> named `cloud-`** (cloud-controller-manager) is the optional bridge to somebody else's
> infrastructure. **One with no prefix at all**, etcd, because it isn't Kubernetes
> software; it's a general-purpose datastore that Kubernetes uses."

## Figure

`ch03-fig01-control-plane-and-node-components` — the whole census on one page. **Solid
border = always present; dashed border = optional.** The caption is load-bearing: "The
dashes are worth as many exam points as the names."

## Downstream obligations

| Chapter | Obligation |
|---|---|
| Ch 7 | The scheduler's actual selection algorithm. Ch 3 deliberately withholds it. |
| Ch 8 | etcd backup and restore; the auth → authz → admission gates a request passes. |
| Ch 12 | Secrets live in etcd — why encryption at rest is a separate decision. |

## Related

[[node-components]] · [[api-server-hub]] · [[optional-components]] · [[control-loop]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-components.md ===
# Concept: Node components

**Home:** Chapter 3 §3 · **Competency:** D1.1 · **Status:** canonical
**Prerequisite:** Chapter 2 §4 (the kubelet → CRI → runtime chain)

## Framing sentence (keep it)

"Node components run on every node, maintaining running Pods and providing the Kubernetes
runtime environment" [source: k8s-docs-components-2026-08-23]. Chapter 3 flags the verb:
the node's collective job is to **maintain** running Pods, "not to start them once and
stand down."

## The three

**kubelet** — "An agent that runs on each node in the cluster. It makes sure that
containers are running in a Pod. The kubelet takes a set of PodSpecs that are provided
through various mechanisms and ensures that the containers described in those PodSpecs are
running and healthy. **The kubelet doesn't manage containers which were not created by
Kubernetes.**"

**kube-proxy (optional)** — "a network proxy that runs on each node in your cluster,
implementing **part** of the Kubernetes Service concept. kube-proxy maintains network rules
on nodes." Optional "if you use a network plugin that implements packet forwarding for
Services by itself, and providing equivalent behavior to kube-proxy."

**container runtime** — "A fundamental component that empowers Kubernetes to run containers
effectively. It is responsible for managing the execution and lifecycle of containers
within the Kubernetes environment." containerd, CRI-O, or any CRI implementation.

## The clause with practical teeth

"If you SSH to a node and start a container by hand with the container runtime directly,
the kubelet does not manage it. It won't restart it, won't maintain it, won't clean it up."
Chapter 3 draws the two-way consequence: it is why hand-started containers don't appear
through `kubectl`, **and** why node-level debugging needs a node-level tool (`crictl`,
Ch 13 §5 — a pointer Chapter 2 already made identically at ch02:602).

## What §3 adds beyond Chapter 2: position

The container runtime "is the one node component that is not Kubernetes software at all.
It's a separate project, swappable, and not authored by the Kubernetes project: Kubernetes
defines the interface and accepts any implementation of it."

## ⚑ RULE 6 — this section broadens Chapter 2's named pattern

Chapter 3 §3 continues: *"That is the same architectural instinct you saw with etcd. Where
a good general-purpose component already exists, Kubernetes defines an interface and uses
it rather than reimplementing it."* **Two problems.**

**(a) etcd is not in the enumeration.** Chapter 2's pattern is *"Kubernetes defines an
interface and lets the **ecosystem** implement it"* (ch02:598), and its sourced list is
**CRI, CSI, CNI, device plugins, and API extensions**
[source: k8s-docs-extending-kubernetes-2026-08-23]. Kubernetes does not define an etcd
interface; it consumes a general-purpose datastore. True of the runtime, true-but-different
of etcd — calling them "the same" broadens a sourced list past what it says.

**(b) The name is dropped.** ch02:596–598 is a section titled "The pattern to name now"
whose ⚓ tells the reader *"Give this move a name in your head, because you are about to see
it three more times."* Chapter 3 hits the **first recurrence**, re-derives it in fresh
words, and never uses the name or bears back. That is a missed spaced-retrieval event on a
theme B3 tracks and Ch 17's secondary Zenith depends on.

**Fix:** keep the named pattern for the container runtime, cross-beared to Ch 2 §4;
describe etcd as the adjacent-but-distinct instinct of reusing an existing general-purpose
component.

## ★ Fixed Point — the full census (verbatim)

> **Control plane:** kube-apiserver, etcd, kube-scheduler, kube-controller-manager, and
> cloud-controller-manager *(optional — absent on premises and on your laptop)*.
>
> **Node** (on every node): kubelet, kube-proxy *(optional — unnecessary if a network
> plugin provides equivalent packet forwarding)*, and the container runtime.
>
> Eight names. Two of them optional, for two different reasons. One of them — the
> container runtime — is not Kubernetes software.

## Related

[[control-plane-components]] · [[optional-components]] · [[api-server-hub]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-server-hub.md ===
# Concept: The API server as hub — "watching, not telling"

**Home:** Chapter 3 §5 · **Competency:** D1.1 · **Status:** canonical
**Chapter 3's second-most-important idea**, after the control loop.

## The four facts that compose into a shape

1. "The API server is the front end for the Kubernetes control plane."
   [source: k8s-docs-cluster-architecture-2026-08-23]
2. etcd is "the backing store for all cluster data." [same]
3. "Kubernetes has a hub-and-spoke API pattern. All API usage from nodes and the Pods they
   run terminates at the API server, and none of the other control-plane components are
   designed to expose remote services."
   [source: k8s-docs-control-plane-node-communication-2026-08-24 — ⚑ NOT ON DISK]
4. A controller "might carry the action out itself; more commonly, in Kubernetes, a
   controller will send messages to the API server that have useful side effects."
   [source: k8s-docs-controllers-2026-08-23]

Chapter 3's image for the result: **"Not a chain of command. A chart table: one surface
everyone works from, and no orders issued across it."**

## ⚓ The reusable sentence (verbatim)

> **The coordination mechanism in Kubernetes is watching, not telling.** Components don't
> send each other instructions. They observe shared state and act on what they see.

## Two precisions the chapter is careful about — preserve both

**1. etcd confinement is a RECOMMENDATION, not an invariant.** "Access to etcd is
equivalent to root permission in the cluster, so **ideally** only the API server should
have access to it" [source: k8s-docs-etcd-access-control-2026-08-24 — ⚑ NOT ON DISK].
Chapter 3 states this explicitly: "Read that as what it is: a strong recommendation with a
security reason behind it, not a law of physics." **Do not harden it downstream.**

**2. The hub describes STATE movement, not every connection.** "The API server does open
connections to kubelets: that is how fetching Pod logs, attaching to a running container,
and port-forwarding work. Those paths carry a session, not an instruction. Nothing
travelling on them tells a kubelet what ought to be running."

An earlier draft asserted the absolute form; a prior AUTHOR-REVIEW records that it was
softened deliberately after the source was fetched. **Do not restore the absolute
phrasing.**

## The submission story (component altitude)

1. Request arrives at the API server; validated and persisted. **Nothing is running yet.**
2. The description is now part of cluster state, visible to anything watching.
3. The scheduler notices a Pod with no node, selects one, records the selection back
   through the API server.
4. The kubelet on that node notices and starts the containers through the runtime.
5. Status flows back the same way.

"Read the verbs. *Notices. Selects. Records. Notices.* At no point does one component
instruct another."

## Figure

`ch03-fig04-request-path-through-apiserver`. The caption instructs the reader to look for
the arrow that **isn't** drawn: there is none between any two of the surrounding
components. The figure is scoped to the **state/API path** and deliberately does not draw
the outbound logs/attach/port-forward paths.

## ⚑ Forward-bearing split needed

Ch 3 §5 bears the outbound paths to "Ch 13 — the debugging commands that ride those
outbound paths." B2 gives `logs --previous` to Ch 13 but **`exec` and `port-forward` to
Ch 16.** Split the bearing.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| Ch 8 | The auth → authz → admission gates a request actually passes through. |
| Ch 13 / Ch 16 | The debugging commands riding the outbound paths — split per above. |
| Ch 15 | **The same shape with a Git repository in the hub position.** Ch 3 names Argo CD and source-tags it here precisely so the recognition lands. |

## Related

[[control-loop]] · [[control-plane-components]] · [[orchestration-technical-definition]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/optional-components.md ===
# Concept: What is optional, and whose word that is

**Home:** Chapter 3 §4 · **Competency:** D1.1 · **Status:** canonical

## The count

Eight components and four addons. **Exactly two of the twelve carry the word "optional" in
the documentation itself:** kube-proxy and cloud-controller-manager
[source: k8s-docs-components-2026-08-23]. They carry it for **two genuinely different
reasons.** Addons are a third kind of optional, and Chapter 3 marks that framing as **its
own** — the docs say addons *extend* the cluster and never call them optional.

| What | Why it's optional | Whose word |
|---|---|---|
| **kube-proxy** | Because something else can do its job — a network plugin implementing equivalent packet forwarding for Services. | The documentation's |
| **cloud-controller-manager** | Because there may be no cloud to talk to. On premises or on a laptop, the cluster simply does not have one. | The documentation's |
| **Addons** | Because they extend rather than constitute. The cluster is a cluster without them. | **This book's framing** |

That whose-word column is a Part 14 compliance feature, not decoration. Preserve it.

## ⚠ Navigational Hazards (verbatim)

> **"kube-proxy runs on every node, always."** The documentation says node components run
> on every node, then marks kube-proxy optional in the same breath. Both are true: *when it
> runs, it runs on every node*, but it may not run at all.
>
> **"Every cluster has a cloud-controller-manager."** No. Every cluster on a cloud provider
> that integrates one does. On premises, or on a laptop, that component is simply absent.
>
> The shared lesson: **read the word "optional" when the documentation prints it.** It's
> printed rarely and deliberately, on exactly two of the eight components.

## The distinction worth preserving: absent vs present-but-idle

Bearings #2 Q2's most interesting distractor asserts cloud-controller-manager runs
everywhere "but on the laptop and in the data center it runs with no provider configured."
Chapter 3's rationale: "The component isn't present-but-idle; it is **absent**. An
idle-but-present component would still turn up in a component listing on that cluster. This
one doesn't."

## Addons

"Addons extend the functionality of Kubernetes." Published examples: **DNS**, **Web UI
(Dashboard)**, **Container Resource Monitoring**, **Cluster-level Logging**
[source: k8s-docs-components-2026-08-23] [source: k8s-docs-cluster-addons-2026-08-24 — ⚑
NOT ON DISK]. "Note the word *extend*. Addons are not components in the sense that the
eight names in §3 are components. They run *on* the cluster rather than constituting it."

**Spelling: `addon`, one word.** Chapter 3 line ~466 reads "add-on" once — flagged.

## Where this section leads

§4's whole purpose is the ⚓ that closes it — see [[absent-component-pattern]]. The
optionality material is the setup; the pattern is the payload.

## Related

[[absent-component-pattern]] · [[node-components]] · [[control-plane-components]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/orchestration-technical-definition.md ===
# Concept: Orchestration — the technical definition Kubernetes disclaims

**Home:** Chapter 3 §7 (planted §1) · **Competency:** D1.1 · **Status:** canonical
**This is Chapter 3's ☀️ Zenith.**

## ★ Fixed Point (verbatim)

> **Orchestration, technically, is the execution of a defined workflow: first do A, then
> B, then C.** Kubernetes disclaims it. Kubernetes comprises a set of independent,
> composable control processes that continuously drive current state toward desired state
> — and it shouldn't matter how you get from A to C. Centralized control is not required.
> [source: k8s-docs-overview-2026-08-23]

## The documentation's full passage

> "Kubernetes is not a mere orchestration system. In fact, it eliminates the need for
> orchestration. **The technical definition of orchestration is execution of a defined
> workflow: first do A, then B, then C.** In contrast, Kubernetes comprises a set of
> independent, composable control processes that continuously drive the current state
> towards the provided desired state. It shouldn't matter how you get from A to C.
> Centralized control is also not required. This results in a system that is easier to
> use and more powerful, robust, resilient, and extensible."

## Two senses, both real — the book uses both deliberately

| Sense | Meaning | Where |
|---|---|---|
| **Loose (industry)** | "a thing that manages containers across machines" | Ch 1 Soundings A2: "Kubernetes is an **orchestrator** — it decides what should run where." |
| **Precise (technical)** | "execution of a defined workflow: A then B then C" | Ch 3 §7 — **the one thing Kubernetes says it is not** |

Chapter 3 §1's 🪝 Snag plants the tension and names it as **the book correcting its own
earlier wording, not the reader**: "At orientation altitude, that's the right answer to the
question being asked… But it's the loose sense of the word. The precise sense is the one on
the exam."

**Glossary consequence:** these are **two entries, not one.** See the Rule 6 note in
`glossary.md` under *orchestrator (loose sense)*.

## The synthesis §7 performs

§5 (all state through one hub; coordination is watching, not telling) + §6 (many
independent non-terminating loops) ⇒ **there is no component in charge, and now you can see
why there isn't one.** "There's a description of what should be true, and a set of
independent processes each responsible for one gap between description and reality. Nobody
is executing steps, because nobody wrote steps. What looked like a missing piece of the
architecture *is* the architecture."

## ⚠ The narrowing — preserve it, it is a Part 14 exemplar

Chapter 3 disarms its own chapter title:

> "'Nobody is in charge' is a good chapter title and a bad thesis… The control plane *does*
> make global decisions. The API server *is* a hub that everything depends on. etcd *is* a
> single store whose loss loses the cluster… The accurate claim is narrower and better:
> **there is no component that executes a workflow, and no component that tells another
> component what to do.** That's a claim about *coordination*, not about *availability*."

**Chapters 8, 12, and 13 depend on the narrower version.** Do not let the slogan travel
without it.

## One claim that was deliberately reframed — do not restore

An earlier draft asserted specific kubelet behavior during a control-plane partition ("it
keeps the containers it already knows about running"). **No cached or fetched snapshot
covers kubelet behavior when the API server is unreachable** — `k8s-docs-nodes-2026-08-23`
documents only the control-plane side (Ready → Unknown, API-initiated eviction). The claim
is now framed as a consequence of the sourced "ensures the containers described in those
PodSpecs are running" description. To state partition behavior explicitly, open a research
gap for the kubelet reference first.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| Ch 15 | Primary Zenith. GitOps as the same shape pointed at a Git repository. |
| Ch 17 | "The same pattern, named as a principle" — declarative APIs in the cloud native definition. |

## Related

[[control-loop]] · [[api-server-hub]] · [[what-kubernetes-is-not]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/deployment-eras.md ===
# Concept: The three deployment eras

**Home:** Chapter 3 §1 · **Competency:** D1.1 · **Status:** canonical
**Prerequisite:** Chapter 2 §1 (the container/VM architectural contrast, in detail)

## The three eras (documentation wording)

**Traditional.** "Organizations ran applications on physical servers. There was no way to
define resource boundaries for applications on a physical server, and this caused
resource-allocation issues… The available solution was to run each application on a
different physical server, which did not scale."

**Virtualized.** "Virtualization allowed multiple Virtual Machines to run on a single
physical server's CPU. Applications became isolated between VMs… But each VM is a full
machine running all the components, including its own operating system, on top of
virtualized hardware."

**Container.** "Containers are similar to VMs, but they have relaxed isolation properties
that let them share the operating system among the applications. That's why containers are
considered lightweight. Like a VM, a container has its own filesystem, share of CPU,
memory, process space, and more. Because they are decoupled from the underlying
infrastructure, they are portable across clouds and OS distributions."
[all: source: k8s-docs-overview-2026-08-23]

## The consequence — which is why §1 exists

Chapter 3 explicitly does **not** re-teach the container/VM architecture (Chapter 2 did).
What §1 adds: "Once your unit of deployment is small, fast, and portable, you stop having a
handful of servers with one application each and start having hundreds of interchangeable
processes scattered across a pool of machines. That is a fundamentally different management
problem, and it's the problem Kubernetes was built for."

## Figure

`ch03-fig03-deployment-eras-timeline`. Caption: "What changes across the eras is not the
application. It's what the application shares with everything else on the machine. Read the
bottom row." The bottom row reads: shares nothing → shares hardware → shares the operating
system.

## ⚑ RULE 6 — the kernel/OS register, and a note that misreports it

**The substance is settled and all three chapters agree.** Chapter 2 §1 (ch02:281–285)
adjudicates both registers as correct and instructs the reader to hold both:

> "The Kubernetes documentation and the CNCF glossary say a container **shares the
> operating system**. That is the phrasing the exam is likeliest to use, and the one to
> recognize on an answer sheet. Practitioners and the container-runtime documentation
> usually sharpen it: a container **shares the host's kernel**… Hold both registers:
> **operating system** as the published wording, **kernel** as the mechanism underneath it."

Chapter 2 supplies an in-cache warrant for the sharpening — Kubernetes describes a
sandboxed runtime as supplying "a user-space kernel (such as gVisor)"
[source: k8s-docs-runtime-class-2026-08-23] — a phrase only meaningful if the ordinary case
is the *host's* kernel.

**Chapter 3 follows Chapter 2 correctly.** It quotes the snapshot when citing, then carries
the kernel precision as a visibly authorial, untagged sentence: *"The sharper statement,
that what a container shares with the host is specifically the **kernel**, is this book's,
not the documentation's."*

**⚠ Chapter 3's §1 AUTHOR-REVIEW (draft line ~130) misreports the state of the book.** It
cites ch02:279 alone (which matches the snapshot) rather than ch02:281–285 (which
adjudicates), and concludes "the remaining outlier is Chapter 1."

**Chapter 1 is not an outlier in content.** ch01:142 uses the kernel register that Chapter 2
explicitly blesses. The only live question is **attribution**: whether that bolded phrase
may sit on a line tagged `k8s-docs-overview-2026-08-23`. Blocked on harvest items A13/A14,
per Chapter 2's own AUTHOR-REVIEW, which prescribes deleting Chapter 1's parallel flag once
they land.

**Risk if acted on as written:** an author would flatten ch01:142 toward "operating
system," deleting the register Chapter 2 spends three paragraphs establishing and that
Figure 2-1's derivation ("Three guest kernels on one host means three times the baseline
resource cost") depends on. **Do not act on the note. Rewrite it first.**

Chapter 3's body prose needs no change.

## Retrieval note

Practice Q2 is tagged `[retrieval: ch2]` and the tag is honest — Chapter 2 does teach it.
But **the answer is restated verbatim in this chapter's own §1**, ~70 minutes of reading
earlier, so the item functions as same-chapter recall rather than *spaced* retrieval. See
`retrieval-log.md` for options. Its answer key should also carry Chapter 2's one-clause
two-register note, so a reader holding Ch 1's "kernel" answer isn't silently contradicted.

## Related

[[what-kubernetes-is-not]] · [[kubernetes-origin]] · [[node-components]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/what-kubernetes-is-not.md ===
# Concept: What Kubernetes is (and explicitly is not)

**Home:** Chapter 3 §1 · **Competency:** D1.1 · **Status:** canonical
**Exam Alert priority #5.** The negative list is tested more than its length suggests.

## Not a traditional PaaS

"Kubernetes is not a traditional, all-inclusive PaaS. Because it operates at the container
level rather than the hardware level, it provides some features common to PaaS offerings
(deployment, scaling, load balancing) and lets users integrate their own logging,
monitoring, and alerting. But Kubernetes is not monolithic, and those default solutions are
optional and pluggable. It provides the building blocks for building developer platforms
while preserving user choice." [source: k8s-docs-overview-2026-08-23]

## The six explicit disclaimers (verbatim, all one source)

Kubernetes:
- **Does not limit the types of applications supported.** "If an application can run in a
  container, it should run great on Kubernetes."
- **Does not deploy source code and does not build your application.** "CI/CD workflows are
  determined by organizational culture and preferences as well as technical requirements."
- **Does not provide application-level services** — no middleware (message buses), no
  data-processing frameworks (Spark), no databases (MySQL), no caches, no cluster storage
  systems (Ceph) as built-in services.
- **Does not dictate logging, monitoring, or alerting solutions.**
- **Does not provide nor mandate a configuration language or system.** "It provides a
  declarative API that arbitrary declarative specifications may target."
- **Does not provide nor adopt any comprehensive machine configuration, maintenance,
  management, or self-healing systems.**

Plus the seventh, held over to §7: **"not a mere orchestration system."**

## What Kubernetes provides — and the re-read that matters

The published capability list: service discovery and load balancing · storage orchestration
· automated rollouts and rollbacks · automatic bin packing · self-healing · secret and
configuration management · batch execution · horizontal scaling · IPv4/IPv6 dual-stack ·
designed for extensibility.

Chapter 3's move is to read the list *as container-era problems*, then plant §6:

> "Read that right-hand column again. Notice how many entries describe something that has
> to *keep being true* rather than something that has to *happen once*. Self-healing isn't
> an action; it's a standing condition."

§6 cashes it: self-healing "stops being a feature and becomes a description of loops
running." Practice Q18 is built on exactly that re-read.

## ⚑ Terminology gaps

**PaaS** and **CI/CD** are both first-use-in-the-book here and **neither acronym is
expanded.** PaaS has no owner chapter anywhere in B2. Either expand on first use or assign
an owner.

## Related

[[orchestration-technical-definition]] · [[control-loop]] · [[deployment-eras]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubernetes-origin.md ===
# Concept: Where Kubernetes came from

**Home:** Chapter 3 §1 · **Competency:** D1.1 (with Ch 17 D4.2/D4.3 uptake)
**Status:** canonical · **Tested:** Practice Q4, Q5; Soundings Q7

## The facts (all one source unless noted)

- **First commit: 6 June 2014** — "250 files and 47,501 lines of Go, bash, and markdown."
- **Lineage:** "Kubernetes drew on Google's internal container-orchestration experience with
  the **Borg** system and its research successor **Omega**, and was written in **Go**."
- **Context:** "It arrived into a container moment that Docker had opened the year before.
  A popular, portable unit of deployment created the demand for something to manage those
  units at scale."
- **Milestones:** announced publicly at DockerCon June 2014 · **v1.0 July 2015** · "donated
  by Google to the newly formed Cloud Native Computing Foundation as its **first project**."
- **CNCF** "is part of the nonprofit Linux Foundation" [source: cncf-who-we-are-2026-08-23].
- **Etymology:** "the Greek word for **helmsman or pilot**; 'K8s' is the numeronym, with
  eight letters between the K and the s."

[source: k8s-history-ten-years-2026-08-23]

## 🔭 Closer Look — the distinction that carries the discriminator

"**Borg and Omega were two different projects, not one renamed.** Borg was the production
system; Omega is described as its research successor. Kubernetes inherited from both."

Practice Q4's distractor D ("Omega alone, with no production predecessor") tests precisely
this. Q5's distractor B tests the etymology half (Greek/helmsman, not Latin/shepherd) while
conceding the correct "first project" half — the discriminating half is the etymology.

## The brand note worth keeping

"The brand you're reading did not pick the maritime register to be cute about it. **The
subject arrived that way.**"

This is the only place in the book where the Lodestar register is justified by the subject
matter rather than by brand convention. Chapter 17's CNCF material can retrieve it.

## Downstream obligations

| Chapter | Obligation |
|---|---|
| Ch 17 | CNCF governance, the project lifecycle, and the cloud native definition. Ch 3 bears forward to "Ch 17 §1"; **see the §N reservation conflict in `glossary.md`** — Ch 1 reserves §1 for the definition and §2 for governance, so Ch 3's merged bearing needs reconciling. |

## Related

[[deployment-eras]] · [[what-kubernetes-is-not]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===
# KCNA — Objective Coverage Log

Tracks which exam competency each chapter covers, at what depth, and when it was last
reviewed. Seeded at Chapter 1 with the full competency registry so it is useful from
Chapter 2 onward.

**Identifier scheme:** `D<domain>.<competency>` — the Lodestar convention established in
B1. CNCF publishes four domains and thirteen named competencies with **no numbering and
no sub-weights**. Every per-chapter weight figure is authored judgment and must be
disclosed as such in front matter.

---

## ⚑ Competency count: 13, not 12

`chapter-lineup.md` (B2, ratified) states "12 competencies" and "twelve named
competencies," twice. **This is wrong.** The cached CNCF curriculum enumerates
4 + 4 + 2 + 3 = **13**, and B1's own `D1.1`–`D4.3` scheme yields 13 identifiers.
Chapter 1's domain table is correct.

**Correct B2 before Chapter 19's synthesis, the blueprint appendix, or the front-matter
disclosure inherits the wrong figure.** (Author action — outside Stage 14's write scope.)

Sources: `lf-kcna-exam-page-2026-08-23`, `cncf-kcna-curriculum-pdf-2026-08-23`.

---

## ⚑ D1.4 is shipped but unrecorded — Chapter 2's Stage 14 never ran

`chapter-02-cargo-in-standard-crates.md` is shipped at the book root and covers **D1.4 —
Containerization**. But `.pipeline-state/ch-02/` contains no `integration.md` and no
`kb-manifest.md`: **Chapter 2 never ran Stage 13 or Stage 14.**

Its coverage row below is therefore marked `unrecorded` rather than assigned a depth,
because no Stage 13 audit exists to justify one. **Run Chapter 2 Stages 13–14 and amend.**
Related: `glossary.md` § "Tier 4 — Chapter 2 gap" holds eleven of Chapter 2's terms with
defining chapter recorded and no definitions written.

---

## Coverage by chapter

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| — (none) | Chapter 1 | n/a — orientation chapter, 0% weight, `objectives: []` | 2026-08-24 |
| **D1.4** | **Chapter 2** | ⚑ **unrecorded — Stage 14 never ran** | — |
| **D1.1** | **Chapter 3** | **deep** | **2026-08-24** |

Chapter 1 covers no exam objectives. It does **name** roughly twenty terms belonging to
later competencies without teaching them — tracked as reserved entries in `glossary.md`,
not as coverage.

### Chapter 3 — D1.1 coverage detail

`kb_tags.objectives: ["D1.1"]`; all seven sections carry `objectives: ["D1.1"]`. Authored
weight estimate **~6%**, disclosed twice in the chapter (metadata line and §Why This
Chapter Matters) as the author's judgment rather than a published figure — CNCF names
competencies without individually weighting them.

**D1.1 is not complete after Chapter 3.** B2 assigns it four consecutive chapters (3–6):
cluster → objects → Pod → controllers. Chapter 3 delivers the cluster layer:

| Sub-topic | Depth |
|---|---|
| Deployment eras; what Kubernetes is and is not | deep |
| Control-plane components (5) | deep |
| Node components (3) | deep — with Ch 2's CRI chain as prerequisite |
| Addons and optionality | deep |
| The API-server hub / hub-and-spoke pattern | deep |
| Controllers and the control loop | **deep — the book's structural spine** |
| Orchestration, technically defined | deep |
| Kubernetes origin and history | moderate |
| `spec` / `status` mechanics | **deferred to Ch 4** |
| Pod as a primitive | **deferred to Ch 5** (⚠ used ~40× here, never defined) |
| Scheduler selection algorithm | **deferred to Ch 7** |

---

## Competency registry (13) — planned homes from B2

| ID | Competency | Domain (weight) | Planned chapter(s) | Status |
|---|---|---|---|---|
| D1.1 | Kubernetes Core Concepts | Kubernetes Fundamentals (44%) | Ch 3, 4, 5, 6 | **in progress — Ch 3 covered 2026-08-24** |
| D1.2 | Administration | Kubernetes Fundamentals (44%) | Ch 8 | not yet covered |
| D1.3 | Scheduling | Kubernetes Fundamentals (44%) | Ch 7 | not yet covered |
| D1.4 | Containerization | Kubernetes Fundamentals (44%) | Ch 2 | ⚑ **shipped, unrecorded** |
| D2.1 | Networking | Container Orchestration (28%) | Ch 9, 10 | not yet covered |
| D2.2 | Security | Container Orchestration (28%) | Ch 12 (+ Ch 10 boundary) | not yet covered |
| D2.3 | Troubleshooting | Container Orchestration (28%) | Ch 13 | not yet covered |
| D2.4 | Storage | Container Orchestration (28%) | Ch 11 | not yet covered |
| D3.1 | Application Delivery | Cloud Native Application Delivery (16%) | Ch 14, 15 | not yet covered |
| D3.2 | Debugging | Cloud Native Application Delivery (16%) | Ch 16 | not yet covered |
| D4.1 | Observability | Cloud Native Architecture (12%) | Ch 18 | not yet covered |
| D4.2 | Cloud Native Ecosystem and Principles | Cloud Native Architecture (12%) | Ch 17 | not yet covered |
| D4.3 | Cloud Native Community and Collaboration | Cloud Native Architecture (12%) | Ch 17 | not yet covered |

**Note on D4.3:** B1 flags it as the competency technically-strong candidates most
reliably under-study. B2's mitigation is not a separate chapter but explicit treatment
inside Ch 17 — its own numbered sections, Fixed Points, and Soundings coverage — plus
disproportionate representation in the Ch 19 synthesis and the Ch 20 mock. Track that
this actually happens.

**Curriculum typo worth recording:** the CNCF-published `KCNA_Curriculum.pdf` contains
"Could Native Community and Collaboration" for D4.3. Candidates who download it will see
it. Belongs in the blueprint appendix.

---

## ⚑ Ethical-guardrail status by chapter (Part 14 #8)

Recorded here because coverage claims and frequency claims are the same audit surface.

| Chapter | Guardrail #8 | Note |
|---|---|---|
| Ch 1 | pass | Weight disclosures present |
| Ch 2 | pass | Models the compliant phrasing at ch02:588: *"These are easy to confuse, and the confusion is historical rather than careless."* |
| Ch 3 | **FAIL — open** | Six unverifiable exam-frequency assertions. CNCF publishes no question counts, per-item frequencies, or competency sub-weights (B2 disclosure #2; gaps G33/G34). B2's instruction is explicit: describe such items as "easy to confuse," never "frequently tested." |

**Chapter 3's failing lines:** ~179 ("tested more often than people expect") · ~279 ("which
is exactly why it gets tested") · 445 and 598 ("cheap points on exam day") · 826 ("Pure
recall, cheaply tested, and it is tested") · 828 ("disproportionately tested").

**Two things the author should know.** First, the *underlying judgments are almost
certainly right* — the one-binary-one-process sentence and the two optionality markers are
exactly what a discrimination exam tests. The problem is epistemic register, not judgment.
Second, **line 598's phrasing originated upstream**: `diagnostics/question-quality.md:319`
drafted the missing Bearings #2 rubric and supplied "both are cheap points on exam day"
verbatim, which the revision stage adopted in good faith. **The guardrail is not being
enforced at the stages that write remediation copy** — that is a pipeline fix, not a
drafting one.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===
# KCNA — Retrieval-Practice Ledger

Tracks which earlier-chapter topics have been retrieval-tested, and in which later
chapter. Also records forward commitments the prose has made to the reader, which are
binding contracts rather than preferences.

---

## Retrieval items by chapter

| Tested topic | Original chapter | Retested in |
|---|---|---|
| *(none — Chapter 1 is excluded from the retrieval schedule by design)* | — | — |
| *(Chapter 2 carries no retrieval items — B3 excludes Ch 1, its only predecessor)* | — | — |
| kubelet ensures the containers described for its node are running | ch 2 §4 | **ch 3** — Soundings Q4 *(excluded from budget)* |
| kubelet reaches the runtime through the CRI | ch 2 §4 | **ch 3** — Bearings #1 Q5 |
| containers share the operating system; VMs each boot their own | ch 2 §1 | **ch 3** — Practice Q2 |
| immutability — build a new image, then recreate the container | ch 2 §2 | **ch 3** — Practice Q24 |
| image contents (code, runtime, application and system libraries, defaults) | ch 2 §2 | **ch 3** — Practice Q25 |

**Chapter 1: 0 retrieval items, which is correct.** B3 excludes Ch 1 entirely — the
skill's table assumes Ch 1 is a content chapter, but here it is orientation at 0% weight.
The ramp begins at **Ch 3 (10%, drawing from Ch 2)**.

**Chapter 3: 5 tags, all landing. Rate = 10.5%, clearing B3's 10% rung.** Excluding
Soundings (B3 excludes them from the budget by design), the graded pool is 38 items with
4 retrieval items → 10.5%. All draw from Ch 2 and none from Ch 1, exactly as B3 specifies.
Tags appear in **both stem and answer key**, which is the convention later mechanical
audits need.

**One pedagogy note, not an accuracy defect.** Practice Q2's answer is stated verbatim in
Chapter 3's own §1, roughly 70 minutes of reading before the question. The tag is honest —
Chapter 2 does teach it — but the item functions as **same-chapter recall, not spaced
retrieval.** Options: (a) re-key to a Ch 2 fact §1 does not restate — layers, tags vs
digests, "an image contains no kernel," or "relaxed isolation is a tradeoff, not a
deficiency"; or (b) keep it as reinforcement. The outline named container-vs-VM
specifically, so keeping it is defensible. **Author's call.**

**Also open on Q2:** its answer key marks "The operating system" correct without
referencing the two-register reconciliation Chapter 2 spent three paragraphs building. A
reader who internalized Ch 1's "operating system **kernel**" meets this item and sees their
answer unlisted. One clause from ch02:281 fixes it and costs nothing.

---

## ⚑ Convention now SETTLED BY OBSERVATION — needs ratification

Chapter 1's Stage 14 recorded this as open: *"The `[retrieval: chN]` tag's rendered form —
reader-visible or draft-only annotation — is still undecided… **Chapter 3 is the first
chapter that needs it settled.**"*

**Chapter 3 settled it in practice, not by decision.** Tags render **reader-visible**,
italic-bracketed, in both the question stem and the answer key:

- Soundings Q4 stem: `4. …for that machine are actually running? *[retrieval: ch2]*`
- Practice Q2 stem: `**Q2.** 🔵 *[retrieval: ch2]*`
- Answer key: `**Q5 — D.** *[retrieval: ch2]* The kubelet ensures…`

This is now canon for seventeen remaining chapters whether or not anyone chose it. It has a
reader-facing dimension because Ch 1 §5 describes the retrieval mechanism to readers in
prose — a visible tag corroborates that promise, which is a real argument in its favour.

**Recorded as OBSERVED PRACTICE, pending author ratification.** If the author prefers
draft-only annotations, the change must happen now, before Ch 4 inherits it.

---

## ⚑ Forward commitments — binding

| # | Commitment | Where stated | Status |
|---|---|---|---|
| 1 | **Chapter 13's checkpoint must carry a Chapter 8 retrieval item** (version skew, framed as a troubleshooting cause) | Ch 1 §5, in plain reader-facing prose; QC2.2 makes the pairing a whole question | **OPEN — verify at Ch 13 Stage 13** |
| 2 | **Chapter 11 must retrieve the control loop** | B3's control-loop theme is Ch 3 → 4 → 6 → 11 → 15 → 17 | **OPEN — and Ch 3 does not bear forward to it.** See below |

**Why #1 is a contract, not a preference.** Chapter 1 tells the reader the pairing by name,
then builds a checkpoint question around it whose distractor C asserts (correctly, per B2)
that Ch 13 does not *depend* on Ch 8. B3 schedules it deliberately: version skew is "the
densest pure-recall material in the book, taught at the 40% mark and otherwise never
revisited before exam day," and Ch 13 ← Ch 8 is exactly 5 chapters back, clearing B3's
spacing floor. If Ch 13 ships without it, Chapter 1 has told the reader something false
about the book, in the section teaching them to trust the mechanism.

**Why #2 is newly open.** Chapter 3 claims three times — Attention Budget, Soundings
rubric, §Why This Chapter Matters — that **"six later chapters retrieve §6 by name."** B3's
theme names **five** later chapters (4, 6, 11, 15, 17), and Chapter 3's own forward
cross-bearings name only **four** (4, 6, 15, 17), omitting Ch 11 entirely. Either fix the
count to five and add the Ch 11 bearing, or soften to "later chapters." One decision, three
identical occurrences.

---

## Cross-cutting themes — retrieval status

B3 names nine. Two are now live:

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **The control loop** (B3's headline theme) | **Ch 3 §6** | — | Ch 4 (spec/status), Ch 6 (ReplicaSet), **Ch 11 (unbeared)**, Ch 15 (primary Zenith), Ch 17 |
| **The absent-component pattern** | **Ch 3 §4**, named | — | Ch 10 ×2 (Ingress; **NetworkPolicy — unbeared**), Ch 13 (`kubectl top`), Ch 17 (VPA) |
| **"Kubernetes defines an interface and lets the ecosystem implement it"** | Ch 2 §4, named | ⚑ **Ch 3 §3 hit the first recurrence and did NOT use the name** | Ch 9 (CNI), Ch 11 (CSI), Ch 17 §4 |

**Retrieve named patterns BY NAME.** B3's rationale: "Naming it once and retrieving it by
name turns four gotchas into one rule." A recurrence that re-derives the pattern in fresh
words is a missed retrieval event, not a reinforcement. Chapter 3 made that mistake once
already (see `concepts/node-components.md`).

---

## Open item — a ★ Fixed Point that is never retrieved

Chapter 1 designates `44 / 28 / 16 / 12` as its single ★ Fixed Point and tells the reader to
memorize it above everything else. B3 then excludes Ch 1 from retrieval entirely and lists
"Ch 1 mechanics" among four things that must *not* be retrieved anywhere in the book.

Net effect: **the book's most emphatically flagged must-memorize fact is the one fact never
retrieval-tested.** Defensible — the weights are reinforced structurally — but it sits
oddly beside §5, where Chapter 1 sells retrieval as "the single highest-leverage thing this
book does structurally."

**Referred for author decision.** Cheapest resolution: let the weights be retrieved
*instrumentally* — a Ch 19 item requiring the reader to allocate remaining study time
across domains uses the weights without testing them as facts, and stays inside B3's
exclusion.

---

## ⚑ PROVISIONAL — B3 schedule summary (NOT from the B3 artifact)

> **Provenance warning, RE-CONFIRMED at Chapter 3.** `book-outline/retrieval-architecture.md`
> on disk is a **stage-failure notice**, not the B3 document — the artifact was composed but
> a permission error prevented the write. What follows is transcribed from the prose summary
> embedded in that notice. It is **second-hand and must not be treated as canon.**
>
> Chapter 1's Stage 14 asked for B3 to be re-run "before Chapter 3, which is where the
> schedule actually starts." **That did not happen. Chapter 3 has now been planned, drafted,
> audited, and integrated against a summary of a lost document.** The schedule held — Ch 3
> hit its rung — but Ch 4 onward should not rely on luck. **Re-run B3 with write access.**

**Spacing targets.** Ch 3 at 10%, Ch 4 at 15%, then 20–25% through Ch 18. Five chapters sit
at the 25% ceiling — Ch 13 and 16 (troubleshooting/debugging arc), Ch 15 and 17 (the two
Zeniths), Ch 18 (last content chapter, most accumulated decay).

**Three structural decisions:**
1. Ch 1 excluded from retrieval entirely (orientation, 0% weight). Ch 3's 10% draws from
   Ch 2; no item anywhere tests exam mechanics.
2. Soundings are excluded from the budget but do the work anyway — Part 11 requires they be
   answerable from prerequisites, which in this book means earlier chapters. Drafting
   instruction: source Soundings from B2's Prerequisites column, making the spacing free.
3. **Spacing floor:** from Ch 8 on, at least one item must come from ≥4 chapters back.

**Nine cross-cutting themes**, headed by the control loop (Ch 3 → 4 → 6 → 11 → 15 → 17) and
namespaced-vs-cluster-scoped. One is a pattern rather than a fact: **"the object exists but
nothing happens without the component"** — Ingress without a controller, NetworkPolicy on an
unsupporting CNI, `kubectl top` without metrics-server, VPA not shipped by default. Named at
Ch 3 §4 as the **absent-component pattern**.

**Decay fixes:** Ch 8's version skew → retrieved in Ch 13; release cadence → Ch 17. Ch 7
(scheduling) and Ch 14 (Helm) are similarly thin and get named anchors.

**Four things that must NOT be retrieved:**
1. Ch 1 exam mechanics
2. The dated graduated-project roster (retrieve the maturity *levels* instead)
3. The unpublished 60-question / 75% figures
4. Any `[inferred]` trap framed as exam frequency
=== END WRITE ===
```

---

## What this stage did and did not do

**Composed 14 files:** the glossary ledger, 10 concept shards, the objective-coverage log, the retrieval ledger. **None reached disk** — the write was denied and the session is non-interactive. They are in the blocks above for the orchestrator to persist.

**Did not write, per Rules 1–4:** `voice-exemplars.md` (8 candidates nominated only), `style-decisions.md`, `structural-contract.yaml`, the skill.

**Did not fabricate:** Chapter 2's ledger entries. Chapter 2 shipped without Stages 13–14, and writing its definitions here — on the contested `container` / kernel-vs-OS term above all — is exactly the drift Rule 5 forbids. Eleven terms sit in Tier 4 with defining chapters and no prose, awaiting backfill.

**Did not silently resolve, per Rule 6:** four canon conflicts, all recorded as loud fenced flags inside the shards that Chapters 10, 15, and 17 will read. The one worth your attention first is **Chapter 3's own §1 AUTHOR-REVIEW note**: it tells a future author that Chapter 1 is the odd one out on the kernel/OS register. It isn't — Chapters 1, 2, and 3 agree on substance, and acting on that note would delete a distinction Chapter 2 spends three paragraphs building and Figure 2-1 depends on. Stage 13 caught it; this stage confirmed it against the source lines and propagated the correction into both the glossary and `deployment-eras.md`.

**One thing I'd flag above the chapter level.** Four consecutive stages have now failed to write into the book tree — Stage 2 on two chapters, B3, and Chapter 1's Stage 14. Chapter 3 was planned, drafted, audited, and integrated against a *summary of a lost B3 document*, and eight of its source tags still point at snapshots that exist only inside a manifest. The schedule happened to hold. That's the executor `--add-dir` / permissions configuration, not any chapter's defect, and it's the highest-leverage fix available right now.