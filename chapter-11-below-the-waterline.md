---
chapter: 11
chapter_type: "content"
title: "Below the Waterline"
subtitle: "Storage outlives the Pod that asked for it"
exam_domain: "Container Orchestration (competency: Storage)"
domain_weight_pct: 5
complexity: "mixed"
novelty: "moderate"
prereq_factor: "heavy"

#-- SUBTITLE NOTE. The arc outline's working subtitle is "Storage
#-- outlives the Pod that asked for it" — eight words, inside this
#-- stage's ≤10-word constraint. Carried forward unmodified. It is also
#-- the §7 Zenith heading and the chapter's one-sentence thesis, so the
#-- three agree by construction rather than by coincidence.

#-- EXAM_DOMAIN NOTE. D2.4 Storage, recorded in Ch 9/Ch 10's house form.
#-- Unlike Ch 10, this chapter has NO objective ambiguity: D2.4 is the
#-- only competency it touches and no concept in it is dual-listed.
#-- kb_tags carries the single objective ID.
#--
#-- The 5% figure is the chapter's AUTHORED allocation, not CNCF data.
#-- CNCF publishes four domain weights (44/28/16/12) and no
#-- sub-competency weights — B1 gap G33, B2 disclosure #1. The in-chapter
#-- metadata line must carry the published 28% for D2 with its source tag
#-- and the authored-allocation disclaimer, matching ch-02/-05/-07/-08/
#-- -09/-10 house form. Do not present 5% as published.

#-- PREREQ NOTE. `heavy`, and the SHAPE of the dependency differs from
#-- Ch 10's in a way the Soundings rubric has to respect. Ch 10 was heavy
#-- because it needed ALL of Ch 9. This chapter is heavy because it needs
#-- narrow, specific pieces of SIX earlier chapters — Ch 2 §2 (the
#-- writable container layer), Ch 3 §6 (the control loop), Ch 4 §3
#-- (cluster-scoped) and §4 (ConfigMap/Secret), Ch 5 §1 (the Pod's shared
#-- context), Ch 6 §6 (StatefulSet identity), Ch 7 §2 (feasible nodes),
#-- Ch 10 §3 (the absent-component pattern). A reader who skipped any ONE
#-- of them loses one section, not the chapter.
#--
#-- Consequence for drafting: the Soundings 0–2 branch must NOT say "go
#-- back and read Chapter N." It must name the specific sections, because
#-- the reader's gap is almost certainly narrow and telling them to
#-- re-read a whole chapter is both wrong and discouraging. This is the
#-- first chapter in the book where that distinction matters.

#-- Section plan (no word budgets) ---------------------------------------
#-- Length is content-driven. Arc-outline depth band: "standard" — 5
#-- points. Planning signal only, NOT a target.
#--
#-- ⚠ SECTION NUMBERING IS LOAD-BEARING. Eight published cross-bearings
#-- point into this chapter and TWO name a section by number:
#--   chapter-05 line 349 → *[... see Ch 11 §1 — volume types and lifetimes]*
#--   chapter-09 line 758 → *[... see Ch 11 §6 — StatefulSets and their per-replica volume claims]*
#-- Both match the B6 skeleton exactly. §1 and §6 below are FIXED.
#-- The other six pointers name the chapter without a section and are
#-- free. Verified 2026-08-25 against chapters 01–10.
sections:
  - name: "Three Lifetimes, and the Volumes That Have Them"
    objectives: ["D2.4"]
    requires_figure: true
    figure_anchor: "ch11-fig01-volume-lifetime-ladder"
    checkpoint_after: false
  - name: "The Claim and the Supply"
    objectives: ["D2.4"]
    requires_figure: true
    figure_anchor: "ch11-fig02-pv-pvc-storageclass-binding"
    checkpoint_after: true
  - name: "Provisioning on Demand"
    objectives: ["D2.4"]
    requires_figure: true
    figure_anchor: "ch11-fig03-static-vs-dynamic-provisioning"
    checkpoint_after: false
  - name: "Access Modes and What Happens After"
    objectives: ["D2.4"]
    requires_figure: true
    figure_anchor: "ch11-fig04-access-modes-and-reclaim-policies"
    checkpoint_after: true
  - name: "Who Actually Provides the Storage"
    objectives: ["D2.4"]
    requires_figure: false
    figure_anchor: null
    checkpoint_after: false
  - name: "Pods That Are Not Interchangeable, Revisited"
    objectives: ["D2.4"]
    requires_figure: true
    figure_anchor: "ch11-fig05-statefulset-pvc-pairing"
    checkpoint_after: true
  - name: "Outliving the Pod That Asked"
    objectives: ["D2.4"]
    requires_figure: true
    figure_anchor: "ch11-zenith-outliving-the-pod"
    checkpoint_after: false

#-- Seven sections against 5 weight points — one FEWER than Ch 9 and
#-- Ch 10, which both ran eight. Correct: this is a single arc, not two.
#-- §1 through §6 walk one ladder from the container filesystem to a
#-- claim that survives its cluster, and §7 states what the walk was for.
#-- No section here is a second subject the way Ch 10's §6–§7 were.

#-- Skill v5.3 Part 11: Soundings pre-chapter diagnostic ------------------
#-- FIVE of the eight are retrieval from shipped chapters, which per B3's
#-- design note makes them spaced-retrieval events at zero cost against
#-- the retrieval budget. Three are general infrastructure priors, so a
#-- reader with storage-admin background but weak Kubernetes recall still
#-- scores meaningfully rather than bottoming out.
soundings_planned:
  question_count: 8
  topics:
    - "retrieval from Ch 2 §2 and Ch 5 §4 — a container writes a file, crashes, and is restarted by the kubelet; whether the file is still there, and which layer it was written to"
    - "retrieval from Ch 5 §1 — the two things every container in one Pod shares, one of which this chapter is entirely about"
    - "retrieval from Ch 4 §3 — whether a PersistentVolume is namespaced or cluster-scoped, and how the reader could settle it from the cluster itself"
    - "retrieval from Ch 6 §6 — what makes a StatefulSet's Pods non-interchangeable, and what Chapter 6 said outright that it was deferring"
    - "general infrastructure prior — in a storage array, who creates a LUN and who requests one, and whether the requester has to know the array's vendor"
    - "retrieval from Ch 2 §4, Ch 6 §8, Ch 9 §1 (enumerated in Ch 10's closing) — naming the pluggable interfaces met so far and what each one hands to somebody outside the project"
    - "general infrastructure prior — deleting a VM, and whether its attached disk goes with it; whether the answer depends on how the disk came to exist"
    - "general infrastructure prior — whether two machines can safely mount one block device read-write at the same time without a clustered filesystem"

#-- ✅ FIXED-POINT SPOILER CHECK — all eight cleared.
#-- The chapter's Fixed Points are: the three-lifetime ladder; PV is
#-- supply and PVC is demand and Pods reference claims never volumes;
#-- binding is exclusive and one-to-one; RWO counts NODES not Pods;
#-- dynamically-provisioned volumes inherit the StorageClass reclaim
#-- policy, which defaults to Delete; a StatefulSet's PVCs survive
#-- deletion of the Pod and of the StatefulSet; CSI closes the set of
#-- four. No question stem above states any of them.
#--   Q3 names PersistentVolume but asks ONLY about scope — which Ch 4
#--     taught, graded, and put in its Chapter Summary. It does not hint
#--     at the supply/demand split, which is §2's Fixed Point.
#--   Q5, Q7 and Q8 are deliberately posed OUTSIDE Kubernetes — arrays,
#--     VMs, block devices — so they build the priors that make §2 and §4
#--     land without pre-empting the Kubernetes-specific claims. Q8 in
#--     particular establishes the physical constraint that makes RWO
#--     sensible WITHOUT saying what unit RWO counts.
#--   Q4's answer previews the storage vocabulary, but only because
#--     shipped Ch 6 line 864 already previewed it in those exact terms.
#--     Nothing new is disclosed.

#-- Skill v5.3 Part 8: practice-question budget ---------------------------
#-- B4 allocates 8 / 10 / 17 = 35 and states plainly that the Bearings
#-- figure is a minimum to exceed. Set at 15 across three checkpoints of
#-- 5, matching the shape shipped by Chapters 3–10 without exception.
#-- Chapter total 35 -> 40.
question_budget:
  soundings: 8
  taking_your_bearings: 15             # across 3 checkpoints (5 + 5 + 5)
  practice_questions: 17
  total_this_chapter: 40

#-- Concept / objective / command tagging --------------------------------
kb_tags:
  objectives: ["D2.4"]
  concepts:
    - "volume"
    - "volume-lifetime-ladder"
    - "ephemeral-volume"
    - "persistent-volume-lifetime"
    - "emptydir"
    - "emptydir-medium-memory"
    - "emptydir-size-limit"
    - "hostpath"
    - "hostpath-type-field"
    - "hostpath-security-risk"
    - "configmap-volume"
    - "secret-volume"
    - "secret-volume-tmpfs"
    - "projected-volume"
    - "downwardapi-volume"
    - "generic-ephemeral-volume"
    - "subpath"
    - "subpath-no-updates"
    - "nfs-volume"
    - "local-volume"
    - "persistentvolume"
    - "persistentvolumeclaim"
    - "supply-and-demand-split"
    - "pods-consume-node-resources"
    - "pvcs-consume-pv-resources"
    - "pv-lifecycle-independence"
    - "binding"
    - "exclusive-one-to-one-binding"
    - "unbound-claim"
    - "pv-phase"
    - "released-not-available"
    - "storageclass"
    - "static-provisioning"
    - "dynamic-provisioning"
    - "provisioner"
    - "storageclass-parameters"
    - "default-storageclass"
    - "empty-storage-class-opt-out"
    - "volume-binding-mode"
    - "wait-for-first-consumer"
    - "access-mode"
    - "readwriteonce"
    - "readonlymany"
    - "readwritemany"
    - "readwriteoncepod"
    - "node-count-semantics"
    - "reclaim-policy"
    - "retain"
    - "delete"
    - "recycle-deprecated"
    - "inherited-reclaim-policy"
    - "csi"
    - "csi-driver"
    - "in-tree-volume-plugin"
    - "csi-migration"
    - "fourth-pluggable-interface"
    - "volumeclaimtemplates"
    - "per-replica-pvc"
    - "pvc-survives-deletion"
    - "absent-component-pattern"
  commands:
    - "kubectl-get-pv"
    - "kubectl-get-pvc"
    - "kubectl-get-storageclass"
    - "kubectl-describe-pvc"
    - "kubectl-api-resources"

figures_planned:
  - "ch11-fig01-volume-lifetime-ladder"
  - "ch11-fig02-pv-pvc-storageclass-binding"
  - "ch11-fig03-static-vs-dynamic-provisioning"
  - "ch11-fig04-access-modes-and-reclaim-policies"
  - "ch11-fig05-statefulset-pvc-pairing"
  - "ch11-zenith-outliving-the-pod"
---

# Chapter 11: Below the Waterline
## *"Storage outlives the Pod that asked for it"*

**Exam Domain: Container Orchestration — Storage (D2.4) | Domain Weight: 28% [source: cncf-kcna-curriculum-pdf-2026-08-23]**
**Authored chapter allocation: ~5% of the total exam (CNCF publishes four domain weights and no sub-competency weights; the D2.4 identifier is this book's own numbering, not CNCF's) | Complexity: Mixed | Novelty: Moderate**

---

## Attention Budget

<!-- AUTHOR-REVIEW: Total corrected from ~85 min to ~135 min. The prior table summed to 95 min against a stated 85, and omitted Soundings, the opening blocks, the Exam Alert, all 17 Practice Questions, the Chapter Summary, and The Voyage Ahead. Every row below is an authored estimate; the table now covers the whole chapter and the header matches its sum. -->

**Total time: ~135 minutes | Recommended: Split across 2 sessions — roughly 70 minutes up to the break after §4, and 65 after it**

| Section | Time | Attention Cost | Best Time to Study |
|---------|------|----------------|-------------------|
| 🧭 Soundings | 8 min | Low | Before you read anything else |
| Why This Chapter Matters · What You'll Learn | 4 min | Low | Anytime |
| §1 Three Lifetimes, and the Volumes That Have Them | 15 min | Low | Anytime |
| §2 The Claim and the Supply | 12 min | Medium | Mid-session |
| ☆ Taking Your Bearings #1 | 6 min | Medium | After a brief pause |
| §3 Provisioning on Demand | 12 min | Medium | Mid-session |
| §4 Access Modes and What Happens After | 14 min | Medium | Peak attention — the densest concentration of this chapter's named exam traps |
| ☆ Taking Your Bearings #2 | 8 min | High | After a real break; this one is hard on purpose |
| §5 Who Actually Provides the Storage | 8 min | Low | Anytime |
| §6 Pods That Are Not Interchangeable, Revisited | 10 min | Medium | Mid-session |
| ☆ Taking Your Bearings #3 | 6 min | Medium | After brief break |
| §7 Outliving the Pod That Asked | 4 min | Low | Anytime |
| Exam Alert | 4 min | Low | Anytime |
| Practice Questions (17, with answer keys) | 20 min | High | Its own sitting — the questions interleave sections, and the answer keys teach |
| Chapter Summary | 3 min | Low | Anytime |
| The Voyage Ahead | 2 min | Low | Anytime |

**Attention Cost Key:**
- **Low:** Concrete, familiar concepts — study anytime
- **Medium:** New concepts requiring focus — study when alert
- **High:** Abstract, complex, or effortful retrieval — study at peak attention

*If you only have 15 minutes: read §4. More of this chapter's named exam traps sit there than anywhere else.*

*If you have thirty-five: read §2 and §4, then take ☆ Taking Your Bearings #2.*

---

> *"The cargo does not belong to the crew. It was aboard before this watch, and it will be aboard after."*
> — Lodestar Ledgers

---

## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score determines how to approach the content. No score is a bad score; each one points at a different reading strategy.

1. A container writes a file to `/tmp/report.json`, then the process inside it crashes. The kubelet restarts the container. Is the file still there? Which layer was it written to?

2. Chapter 5 said that every container in a single Pod shares two things. What are they? One of them is what this entire chapter is about.

3. Is a `PersistentVolume` a namespaced resource or a cluster-scoped one? How would you settle the question from the cluster itself, without looking it up?

4. What makes a StatefulSet's Pods non-interchangeable in a way a Deployment's Pods are not? And what did Chapter 6 say, in as many words, that it was deliberately *not* explaining yet?

5. In a traditional storage array, who creates a **LUN (Logical Unit Number)** and who requests one? Does the person requesting need to know the array's vendor?

6. Chapter 10 asked you to hold a count. Name the pluggable interfaces you have met so far in this book, and say what each one hands to somebody outside the Kubernetes project.

7. You delete a virtual machine. Does its attached disk go with it? Does your answer depend on how the disk came to exist in the first place?

8. Can two separate machines mount the same block device read-write at the same time, without a clustered filesystem underneath? What goes wrong if they try?

<details>
<summary>Click for answers + reading strategy</summary>

1. **No — the file is gone.** It was written to the container's writable layer, which is discarded and rebuilt from the image when the container restarts. *[cross-bearing: see Ch 2 §2 — the writable container layer]*

2. **A network namespace (and therefore an IP address) and volumes.** Volumes are this chapter's whole subject. *[cross-bearing: see Ch 5 §1 — the Pod as the unit of scheduling]*

3. **Cluster-scoped.** You settle it from the cluster with `kubectl api-resources --namespaced=false`, which lists every resource kind that does not live inside a Namespace. *[cross-bearing: see Ch 4 §3 — namespaced vs cluster-scoped]*

4. **A stable ordinal identity that survives rescheduling.** `web-0` stays `web-0` on whatever node it lands on. Chapter 6 said outright that it was deferring how that Pod's storage is *provisioned, requested, sized, reclaimed, or shared*. This chapter is where that debt comes due.

5. **The storage administrator creates the LUN; the application team requests one.** The requester specifies a size and a performance need, and does not have to know whether the array is NetApp, Pure, or a pile of disks in a closet.

6. **Three so far.** CRI at the container runtime (Chapter 2), CRDs at the API itself (Chapter 6), CNI at the network (Chapter 9). Each hands a published contract to somebody outside the Kubernetes project so they can plug in an implementation without editing Kubernetes' source. The fourth arrives in §5 of this chapter.

7. **It depends, and the "depends" is the interesting part.** A boot disk created automatically with the VM usually dies with it; a disk you provisioned separately and attached usually survives. Provisioning history determines deletion behavior.

8. **No, not safely.** This is general storage background rather than a Kubernetes rule: two independent filesystem drivers each believing they own the block device will corrupt it, because each caches metadata the other does not know it changed. A clustered filesystem exists to coordinate exactly that.

**Scoring.** Seven of the eight questions above ask for two things. Count a question right only if both halves are right — a half-answer is a gap, and the rubric below is calibrated on that basis.

**If you got 6+ right:** Skim this chapter. Focus on the ★ Fixed Points and the ⚠ Navigational Hazards callouts, and go straight to ☆ Taking Your Bearings #2. That checkpoint is where this chapter's domain analysis puts the heaviest exam yield, and where a confident reader is still most likely to lose points.

**If you got 3–5 right:** Read at normal pace. The material is in reach and this chapter is calibrated for you.

**If you got 0–2 right:** Read carefully, but do not go back and re-read whole chapters. Check three *sections*: Ch 5 §1 (what a Pod shares), Ch 4 §3 (cluster-scoped resources), and Ch 6 §6 (StatefulSet identity). That is three sections, not three chapters. This material assumes narrow, specific things rather than everything that came before it.

</details>

---

## Why This Chapter Matters

For ten chapters, everything you have learned has rested on a single assumption: a Pod is disposable. It can be deleted and replaced. It can be rescheduled onto a different node. It can be scaled from three to thirty and back to one, and no individual Pod's disappearance is an event worth naming.

That assumption is what makes Kubernetes work. It is also exactly what a database cannot tolerate.

So here is the question this chapter opens and does not close until §4: **when the Pod is gone, who decides whether the data is gone too, and when did they decide it?** Not *whether* you can attach storage; you can, and it is not difficult. The question is who holds the authority over the data's survival, and at what moment they exercised it. The answer is more interesting than "you do," and it arrives later than you would expect.

The move this chapter teaches is the one that separates people who *use* a cluster from people who *run* one: separating the request for storage from the supply of it. A developer who understands that they write a claim and never a volume can be handed a cluster whose backing store they have never heard of — Ceph, **EBS (Elastic Block Store)**, a NetApp filer, a single **NFS (Network File System)** export in a rack somewhere — and be productive on it that same afternoon. That is not an exam trick. It is the actual division of labor on every platform team you will ever join.

State this plainly, once: the failure modes in this chapter destroy data rather than merely stop traffic. A Service misconfigured badly is an outage, and outages end. A reclaim policy misunderstood is a deleted volume, and that does not end. This is the chapter where reading carefully has a different payoff than it does elsewhere.

> **Dead Reckoning:** On-disk files in a container are ephemeral. When a container crashes or is stopped, the container state is not saved, so all files created or modified during that container's lifetime are lost; the kubelet restarts the container with a clean state [source: k8s-docs-volumes-2026-08-23]. Volumes exist to solve two problems: surviving container crashes, and sharing files between containers running in one Pod [source: k8s-docs-volumes-2026-08-23]. Persistent volumes exist to solve a third: surviving the Pod itself. Ephemeral volume types have a lifetime linked to a specific Pod; persistent volumes exist beyond the lifetime of any individual Pod [source: k8s-docs-volumes-2026-08-23].

> **Extended Analogy:** Think of the ship's hold, below the waterline.
>
> The cargo is not part of the crew. The crew is relieved and replaced on a schedule that has nothing to do with what is in the hold. Watches change, hands sign off at the end of a voyage, a new complement comes aboard for the next one. Through all of it, the cargo sits where it was stowed.
>
> The hold is inventoried, claimed, and released by a process that runs on entirely different rails from the watch rotation. A shipper files a claim against space in the hold. Somebody working from the stowage plan decides which part of the hold satisfies it. When the claim is released, what happens next — is the cargo landed, is it held for the next voyage, is it destroyed — was settled by the terms of the arrangement long before anyone came to collect it.
>
> That last sentence is this chapter's whole argument. Hold onto it.

<!-- AUTHOR-REVIEW: theming-density audit flagged "quartermaster" here as a locked narrator role-family name (cloud platform / AZ-900), used in a Communications Officer book. Substituted with a stowage-plan phrasing that carries the same binding-loop mapping and names no rank. Revert if the lowercase common-noun use is judged acceptable. -->

---

## What You'll Learn

By the end of this chapter, you'll be able to:

- **Trace** a file from the container filesystem outward, and say at which of three boundaries it stops surviving.
- **Distinguish** a PersistentVolume from a PersistentVolumeClaim from a StorageClass — the three-way distinction this book's domain analysis puts at the front of the Storage competency — and say which one a Pod actually references.
- **Predict** whether a claim will bind, sit unbound, or trigger a volume into existence, given a cluster's provisioning setup.
- **Read** an access mode as a statement about how many *nodes*, not how many Pods (a distinction with an entire fourth mode devoted to it, which should tell you something about how often it gets missed).
- **State** what happens to the data after the claim is deleted, and where that decision was actually made.
- **Explain** why a StatefulSet's storage survives not just a Pod restart but a reschedule onto a different node, closing the loop Chapter 6 opened on purpose.

You will also collect the last of the four pluggable interfaces, and with it a rule about interfaces that Chapter 17 will ask you to state without help.

---

## ⚪ §1 — Three Lifetimes, and the Volumes That Have Them

Chapter 10 told you, in its closing pages, that this chapter opens with a ladder of three different lifetimes, only one of which survives the thing that created it. Here is that ladder. The count is exactly three.

Start at the bottom, where you already are.

A container's filesystem is assembled from the image's read-only layers with a single writable layer on top *[cross-bearing: see Ch 2 §2 — the writable container layer]*. Everything the process writes goes into that writable layer. When the container stops — crash, OOM kill, a `SIGTERM` it handled badly — the kubelet restarts it, and the restarted container gets a clean state assembled fresh from the image [source: k8s-docs-volumes-2026-08-23]. The writable layer is discarded. That is rung one, and the boundary that ends it is **a container restart**.

Now attach a volume. A volume declared in the PodSpec and mounted into a container is not part of the container's filesystem stack; it is mounted into it. When the container restarts, the volume is still there, because the volume belongs to the Pod, not to the container. The documentation states this as a flat rule: *for any kind of volume in a given Pod, data is preserved across container restarts* [source: k8s-docs-volumes-2026-08-23]. That is rung two. It survives the boundary that killed rung one.

But rung two has a boundary of its own. **When a Pod ceases to exist, Kubernetes destroys ephemeral volumes** [source: k8s-docs-volumes-2026-08-23]. Not when the Pod is unhealthy, not when a container inside it dies: when the Pod object itself is gone. Delete the Pod, and its `emptyDir` goes with it.

Rung three is what is left when you ask for storage whose lifetime is not tied to any Pod at all. **Kubernetes does not destroy persistent volumes** [source: k8s-docs-volumes-2026-08-23]. That is the entire distinction, and it is the hold the epigraph was describing: aboard before this watch, aboard after. §2 onward is about how you get one.

<!-- FIGURE: ch11-fig01-volume-lifetime-ladder -->
![Three nested rectangles showing widening storage lifetimes: an innermost container writable layer that survives nothing, a middle Pod-scoped volume that survives a container restart, and an outermost cluster-scoped storage box that survives the Pod's deletion; two arrows mark the boundaries at container restart and at Pod deletion](figures/ch11-fig01-volume-lifetime-ladder.svg)

<!-- ASCII-FALLBACK
```
   ┌──────────────────────────────────────────────────────────────┐
   │  CLUSTER-SCOPED STORAGE                          (rung 3)    │
   │  survives the Pod's deletion                                 │
   │                                                              │
   │   ┌────────────────────────────────────────────────────┐     │
   │   │  POD-SCOPED VOLUME                     (rung 2)    │     │
   │   │  survives a container restart                      │     │
   │   │                                                    │     │
   │   │   ┌──────────────────────────────────────────┐     │     │
   │   │   │  CONTAINER WRITABLE LAYER    (rung 1)    │     │     │
   │   │   │  survives nothing                        │     │     │
   │   │   └──────────────────────────────────────────┘     │     │
   │   │        ▲                                           │     │
   │   │        └── boundary: CONTAINER RESTART             │     │
   │   │            (data below this line is discarded)     │     │
   │   └────────────────────────────────────────────────────┘     │
   │            ▲                                                 │
   │            └── boundary: POD CEASES TO EXIST                 │
   │                (data below this line is discarded)           │
   │                                                              │
   │   nothing in a Pod's lifecycle crosses this outer boundary   │
   └──────────────────────────────────────────────────────────────┘
```
-->

> ★ **Fixed Point**
>
> **Three lifetimes, two boundaries.** The container's writable layer is destroyed by a **container restart**. A Pod-scoped (ephemeral) volume survives that, and is destroyed when **the Pod ceases to exist**. Cluster-scoped persistent storage survives both, because nothing in a Pod's lifecycle reaches it. Every storage question in Kubernetes is a question about which rung you are standing on.

### The volumes that live on rung two

With the ladder in place, the volume types hang off it cleanly. Nearly all of the ones you will meet on the exam are rung-two types: their lifetime is the Pod's.

**`emptyDir`** is the plain one. The volume is created when the Pod is assigned to a node, and as the name says, it is initially empty [source: k8s-docs-volume-types-depth-2026-08-25]. Every container in the Pod can read and write the same files in it, which is the shared-filesystem half of what Chapter 5 told you a Pod's containers have in common *[cross-bearing: see Ch 5 §1 — the Pod's shared context]*. Chapter 5 named it and left it; here it is.

The lifetime rules for `emptyDir` are the ladder restated in one type. *When a Pod is removed from a node for any reason, the data in the `emptyDir` is deleted permanently.* And immediately after: *A container crashing does not remove a Pod from a node*, therefore *the data in an `emptyDir` volume is safe across container crashes* [source: k8s-docs-volume-types-depth-2026-08-25].

Two knobs matter. Setting `emptyDir.medium` to `"Memory"` makes Kubernetes mount a tmpfs — a RAM-backed filesystem — instead of using disk [source: k8s-docs-volume-types-depth-2026-08-25]. Fast, and with a catch the documentation states directly: *while tmpfs is very fast, be aware that, unlike disks, files you write count against the memory limit of the container that wrote them* [source: k8s-docs-volume-types-depth-2026-08-25]. A process that fills a memory-backed `emptyDir` gets OOM-killed for it *[cross-bearing: see Ch 5 §8 — requests, limits, and what a Pod is owed]*. The second knob is `sizeLimit`, which caps the volume's capacity on the default medium [source: k8s-docs-volume-types-depth-2026-08-25].

> 🪝 **Snag:** By default there is *no* cap. The documentation is blunt: *there is no limit on how much space an `emptyDir` or `hostPath` volume can consume, and no isolation between containers or Pods* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. A runaway log writer in one Pod can fill the node's disk and put every other Pod on that node into disk pressure. `sizeLimit` exists because the default is unbounded.

**`hostPath`** mounts a file or directory from the host node's filesystem into your Pod [source: k8s-docs-volume-types-depth-2026-08-25]. It has an optional `type` field alongside the required `path` [source: k8s-docs-volume-types-depth-2026-08-25]. That field controls what Kubernetes checks before mounting: whether the path must already exist, must be a directory, may be created, must be a socket, and so on [source: k8s-docs-volumes-2026-08-23]. The documentation's own framing of `hostPath` is exactly right: *this is not something that most Pods will need, but it offers a powerful escape hatch for some applications* [source: k8s-docs-volume-types-depth-2026-08-25].

An escape hatch is precisely what it is, and escape hatches open both ways.

> ⚠ **Navigational Hazards: `hostPath` is a hole in the wall**
>
> The documentation opens its warning with a sentence that does not hedge: *using the `hostPath` volume type presents many security risks.* *If you can avoid using a `hostPath` volume, you should.* [source: k8s-docs-volume-types-depth-2026-08-25]
>
> Why it is dangerous is more instructive than that it is. *Access to the host filesystem can expose privileged system credentials (such as for the kubelet) or privileged APIs (such as the container runtime socket) that can be used for container escape or to attack other parts of the cluster* [source: k8s-docs-volume-types-depth-2026-08-25]. A Pod that can read `/var/lib/kubelet` can read the node's credentials. A Pod that can write to the container runtime socket can start a privileged container of its own choosing. The Pod boundary you have spent ten chapters trusting is only as strong as the mounts you allow through it.
>
> Restricting access to specific host directories through admission-time validation only holds if those mounts are additionally required to be read-only; give an untrusted Pod a read-write mount and its containers may be able to subvert the restriction [source: k8s-docs-volume-types-depth-2026-08-25].
>
> There is a second-order problem too, and it is the kind that bites in production rather than on an exam: *Pods with identical configuration (such as created from a PodTemplate) may behave differently on different nodes due to different files on the nodes* [source: k8s-docs-volume-types-depth-2026-08-25]. A `hostPath` mount silently makes your Pods node-dependent. The replica that works and the replica that doesn't are running the same image.
>
> This is the workload-to-host boundary problem, and it is why an entire security apparatus exists to police it. Named here, and left here: *[cross-bearing: see Ch 12 §5 — what a Pod may do to its node]*.

**`configMap` and `secret` as volume sources.** Chapter 4 taught you both objects and then told you they would reappear here as volume types mounted into a filesystem *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. This is that reappearance. A ConfigMap's data can be referenced in a volume of type `configMap` and consumed as files by the containerized application [source: k8s-docs-volumes-2026-08-23]. A `secret` volume does the same for a Secret: *you can store secrets in the Kubernetes API and mount them as files for use by Pods without coupling to Kubernetes directly* [source: k8s-docs-volume-types-depth-2026-08-25].

Both are always mounted read-only [source: k8s-docs-volume-types-depth-2026-08-25]. And one detail about `secret` volumes matters more than it looks: *`secret` volumes are backed by tmpfs (a RAM-backed filesystem), so they are never written to non-volatile storage* [source: k8s-docs-volume-types-depth-2026-08-25]. A Secret mounted as a volume does not land on the node's disk. A Secret injected as an environment variable is a different proposition entirely, for reasons Chapter 12 will develop *[cross-bearing: see Ch 12 §4 — Secrets are not encrypted]*. File over environment variable is half an argument already, and you now hold that half.

**`projected`** is the multiplexer. *A `projected` volume maps several existing volume sources into the same directory* [source: k8s-docs-projected-volumes-2026-08-25]. The list of projectable sources runs longer than this chapter needs; the four that matter to you are `secret`, `configMap`, `serviceAccountToken`, and `downwardAPI` [source: k8s-docs-projected-volumes-2026-08-25].

<!-- AUTHOR-REVIEW: the snapshot enumerates six projectable sources (adding `clusterTrustBundle` and `podCertificate`). Trimmed to four on the curriculum-alignment stage's recommendation — the two dropped entries appear nowhere else in the book and are not KCNA material. Full list is in k8s-docs-projected-volumes-2026-08-25 if a later stage wants it restored. -->

You have already used one of these without being told what it was. In Chapter 5, a Pod's ServiceAccount token arrived in the container's filesystem via a projected token volume *[cross-bearing: see Ch 5 §6 — a Pod's identity]*. That was `serviceAccountToken`, one entry in the list above. The mechanism you met carrying an identity token is the same mechanism, generalized: assemble several distinct sources into one directory so the application sees a single coherent config tree instead of four mount points.

**`downwardAPI`** makes a Pod's own metadata available to the application running inside it. *Within the volume, you can find the exposed data as read-only files in plain text format* [source: k8s-docs-volume-types-depth-2026-08-25]. A container that needs to know its own Pod name, namespace, or labels reads them from a file rather than being told at build time.

**Generic ephemeral volumes** are the interesting hybrid, and they are the type most likely to make you re-read the ladder. They are *similar to `emptyDir` volumes in the sense that they provide a per-pod directory for scratch data that is usually empty after provisioning*, but with capabilities `emptyDir` does not have: *storage can be local or network-attached*, *volumes can have a fixed size that Pods are not able to exceed*, and typical volume operations like snapshotting, cloning, and resizing are supported if the driver supports them [source: k8s-docs-ephemeral-volumes-2026-08-25].

Here is the mechanism. Read it twice; it prefigures §6. The Pod spec carries a full PersistentVolumeClaim template inline. When such a Pod is created, *the ephemeral volume controller then creates an actual PersistentVolumeClaim object in the same namespace as the Pod and ensures that the PersistentVolumeClaim gets deleted when the Pod gets deleted* [source: k8s-docs-ephemeral-volumes-2026-08-25]. A real claim, created for you, garbage-collected with the Pod. Rung two behavior, built out of rung three machinery.

Naming is deterministic: *the name is a combination of the Pod name and volume name, with a hyphen (-) in the middle* [source: k8s-docs-ephemeral-volumes-2026-08-25]. A Pod named `my-app` with a volume named `scratch-volume` produces a PVC named `my-app-scratch-volume`.

> 🔭 **Closer Look:** That deterministic naming has a sharp edge the documentation calls out explicitly. A Pod named `pod-a` with volume `scratch` and a Pod named `pod` with volume `a-scratch` both compute to the PVC name `pod-a-scratch` [source: k8s-docs-ephemeral-volumes-2026-08-25]. Kubernetes detects the conflict: a PVC is only used for an ephemeral volume if it was created for that Pod, checked via the ownership relationship, and *an existing PVC is not overwritten or modified* [source: k8s-docs-ephemeral-volumes-2026-08-25]. But detection is not resolution: *without the right PVC, the Pod cannot start* [source: k8s-docs-ephemeral-volumes-2026-08-25]. Below KCNA depth; recorded because it is the kind of thing that costs someone an afternoon.

**`subPath`** is not a volume type at all. It is a mount modifier, and it earns its place here because of one exception you were promised by name in Chapter 4.

The general mechanism first: *sometimes, it is useful to share one volume for multiple uses in a single Pod. The `volumeMounts[*].subPath` property specifies a sub-path inside the referenced volume instead of its root* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. One PVC, mounted into a MySQL container at its `mysql` subdirectory and into a PHP container at its `html` subdirectory: two containers, two mount points, one underlying volume.

Now the exception. Chapter 4 told you flatly that a mounted ConfigMap picks up changes when the ConfigMap is updated, and told you the exception had a name and would arrive here *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. Here it is, a flat rule with no conditions attached: *a container using a ConfigMap as a `subPath` volume mount will not receive updates when the ConfigMap changes* [source: k8s-docs-volume-types-depth-2026-08-25].

The same applies to the two neighbors: *a container using a Secret as a `subPath` volume mount will not receive Secret updates* [source: k8s-docs-volume-types-depth-2026-08-25], and *a container using the downward API as a `subPath` volume mount does not receive updates when field values change* [source: k8s-docs-volume-types-depth-2026-08-25].

> 🪢 **Mnemonic:** **`subPath` cuts the wire.** A whole-volume mount stays connected to the object that feeds it. A `subPath` mount takes a snapshot of one path and stops listening. If you mount config with `subPath` and then wonder why your rolling ConfigMap update did nothing, this is why.

<!-- AUTHOR-REVIEW: `chapter-04` line 761 carries a RESEARCH GAP comment noting that the ConfigMap auto-update hedge was uncited at the time Ch 4 shipped. The `subPath` half of that claim is now sourced here to k8s-docs-volume-types-depth-2026-08-25. Worth feeding to any Ch 4 retrofit. -->

### The rung-three teasers

Two volume types on the list belong to rung three and are named here only so you recognize the shape when §2 formalizes it.

**`nfs`** allows an existing NFS share to be mounted into a Pod, and the contrast with `emptyDir` is exactly the ladder: *unlike `emptyDir`, which is erased when a Pod is removed, the contents of an `nfs` volume are preserved, and the volume is merely unmounted* [source: k8s-docs-volume-types-depth-2026-08-25]. Preserved, not deleted. Merely unmounted. That sentence is rung three in miniature. It also means the data can be pre-populated before any Pod exists, and shared between Pods. NFS in particular *can be mounted by multiple writers simultaneously* [source: k8s-docs-volume-types-depth-2026-08-25], which will matter a great deal in §4.

**`local`** represents a mounted local storage device: a disk, a partition, a directory [source: k8s-docs-volume-types-depth-2026-08-25]. Unlike `hostPath`, `local` volumes are used *in a durable and portable manner without manually scheduling Pods to nodes*, because *the system is aware of the volume's node constraints by looking at the node affinity on the PersistentVolume* [source: k8s-docs-volume-types-depth-2026-08-25]. It has a hard restriction: *local volumes can only be used as a statically created PersistentVolume. Dynamic provisioning is not supported* [source: k8s-docs-volume-types-depth-2026-08-25]. And an honest limitation: *if a node becomes unhealthy, then the `local` volume becomes inaccessible to the Pod. The Pod using this volume is unable to run* [source: k8s-docs-volume-types-depth-2026-08-25].

Both of those types name a `PersistentVolume`. You have not been told what one is. That is next.

---

## ⚪ §2 — The Claim and the Supply

Before anything else, dispose of a collision that the documentation itself sets up.

You have just spent a section learning that a **volume** is a field in a PodSpec: a thing declared inside a Pod, mounted into its containers, scoped to its lifetime. Now you are going to meet an object called a **PersistentVolume**, and the natural reading is that it is the same noun with a modifier — a volume, but persistent.

It is not. The documentation describes a PersistentVolume as being *volume plugins like Volumes, but* with *a lifecycle independent of any individual Pod that uses the PV* [source: k8s-docs-persistent-volumes-2026-08-23]. That "like Volumes" is precisely what invites the confusion. A `volume` is a field in a PodSpec. A `PersistentVolume` is a cluster-scoped API object with its own name, its own lifecycle, and its own existence independent of every Pod in the cluster. Different things. Similar words. Keep them apart.

Here is the arrangement. The cleanest way in is the documentation's own proportion:

> **Pods consume node resources and PVCs consume PV resources.** [source: k8s-docs-persistent-volumes-2026-08-23]

Read that as an analogy with four terms. A Pod does not create CPU; it requests some, and the scheduler finds a node that has it *[cross-bearing: see Ch 7 §2 — what makes a node feasible]*. A PersistentVolumeClaim does not create storage; it requests some, and a control loop finds a PersistentVolume that has it. The parallel is exact, which is why the documentation reaches for it.

**A PersistentVolume (PV) is a piece of storage in the cluster** that has been provisioned by an administrator or dynamically provisioned using StorageClasses. *It is a resource in the cluster just like a node is a cluster resource.* This API object *captures the details of the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage system* [source: k8s-docs-persistent-volumes-2026-08-23]. That is the supply side: a real piece of storage, described to Kubernetes, sitting in the cluster waiting to be used.

**A PersistentVolumeClaim (PVC) is a request for storage by a user** [source: k8s-docs-persistent-volumes-2026-08-23]. The glossary is even blunter about what it does and does not contain: a claim *specifies the amount of storage, how the storage will be accessed (read-only, read-write and/or exclusive) and how it is reclaimed (retained, recycled or deleted)*, while *details of the storage itself are described in the PersistentVolume object* [source: k8s-glossary-storage-terms-2026-08-25]. A claim says *how much* and *how*. It does not say *which array*.

That split explains something you learned seven chapters ago and probably filed as a fact to memorize. Chapter 4 taught you that a PersistentVolume is cluster-scoped, naming it alongside Nodes and StorageClasses *[cross-bearing: see Ch 4 §3 — where a name lives]*. What it did not tell you — because it had no reason to yet — is that the **claim** is namespaced. You now have the reason for both halves rather than a rule for one. Supply is a cluster-wide resource, like a node: it belongs to no team, and the administrator who provisioned it did so for the cluster. Demand comes from a specific application in a specific namespace, and belongs to whoever owns that namespace. The scoping is not an arbitrary API decision; it is the supply/demand split expressed in the API's own vocabulary. The hold belongs to the ship. The claim belongs to whoever is shipping.

And the claim's namespace is load-bearing at consumption time too: *claims must exist in the same namespace as the Pod using the claim. The cluster finds the claim in the Pod's namespace and uses it to get the PersistentVolume backing the claim* [source: k8s-docs-persistent-volumes-depth-2026-08-25].

That leaves the routing detail this whole section exists to fix.

> ★ **Fixed Point**
>
> **PV is supply. PVC is demand. A Pod references the claim — never the volume.**
>
> *Pods use claims as volumes. The cluster inspects the claim to find the bound volume and mounts that volume for a Pod. Users schedule Pods and access their claimed PVs by including a `persistentVolumeClaim` section in a Pod's `volumes` block* [source: k8s-docs-persistent-volumes-2026-08-23].
>
> The Pod's line terminates at the PVC. It never touches the PV. That single routing fact is what lets a developer write a manifest that works on a cluster backed by EBS and on a cluster backed by Ceph without changing a character.

<!-- FIGURE: ch11-fig02-pv-pvc-storageclass-binding -->
![A supply column holding a cluster-scoped PersistentVolume and a demand column holding a namespaced PersistentVolumeClaim, both feeding a central binding control loop that produces an exclusive one-to-one bound pair; a Pod arrow points at the bound claim and stops there, and a disconnected StorageClass box sits to one side](figures/ch11-fig02-pv-pvc-storageclass-binding.svg)

<!-- ASCII-FALLBACK
```
        SUPPLY                                   DEMAND
   (cluster-scoped)                            (namespaced)
   created by an admin                       created by a user

   ┌───────────────────┐                  ┌────────────────────┐
   │ PersistentVolume  │                  │ PersistentVolume-  │
   │   pv-fast-01      │                  │   Claim  "data"    │
   │   50Gi   RWO      │                  │   requests 20Gi    │
   │   [NFS / EBS /    │                  │   requests RWO     │
   │    Ceph / …]      │                  │   ns: production   │
   └─────────┬─────────┘                  └─────────┬──────────┘
             │                                      │
             │      ┌────────────────────────┐      │
             └─────▶│   BINDING control loop │◀─────┘
                    │  watches for new PVCs, │
                    │  finds a matching PV,  │
                    │  binds them together   │
                    └───────────┬────────────┘
                                │
                       EXCLUSIVE, ONE-TO-ONE
                                │
                                ▼
                    ┌────────────────────────┐
   ┌──────────┐     │   PVC "data" is BOUND  │
   │   Pod    │────▶│   to PV pv-fast-01     │
   └──────────┘     └────────────────────────┘
        ▲
        └── the Pod's line terminates HERE, at the claim.
            It never reaches the PersistentVolume.

   ┌──────────────┐
   │ StorageClass │  ← a third object, off to one side.
   └──────────────┘     Not explained yet. See §3.
```
-->

### Binding

The matching is done by a control loop, and naming it as one costs nothing and buys a great deal: *a control loop in the control plane watches for new PVCs, finds a matching PV (if possible), and binds them together* [source: k8s-docs-persistent-volumes-2026-08-23]. Watch, compare desired against actual, act, repeat. That is the same machinery that runs Deployments, Jobs, and every other controller in the cluster *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*. There is no separate storage subsystem with its own logic. There is a controller, doing what controllers do.

Two properties of binding are exam material and both are counter-intuitive in the same direction: readers expect binding to be looser than it is.

**Binding is exclusive and one-to-one.** *Once bound, PersistentVolumeClaim binds are exclusive, regardless of how they were bound. A PVC to PV binding is a one-to-one mapping* [source: k8s-docs-persistent-volumes-2026-08-23]. A 50Gi PV satisfying a 20Gi claim does not have 30Gi left over for someone else. It is spoken for, entirely, by that claim.

**An unmatched claim waits forever.** *Claims will remain unbound indefinitely if a matching volume does not exist. Claims will be bound as matching volumes become available* [source: k8s-docs-persistent-volumes-2026-08-23]. Not an error. Not a timeout. Not a failure event you can alert on cleanly. The claim simply sits, and a Pod that references it does not start.

> 🪝 **Snag:** "The claim is 20Gi and the PV is 50Gi, so it will fit" is a reasonable guess and a wrong one, because *fits* is not the only criterion. A claim can also specify a `storageClassName`, and *only PVs of the requested class, ones with the same `storageClassName` as the PVC, can be bound to the claim* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. It can specify a label selector, where *only the volumes whose labels match the selector can be bound to the claim* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. All requirements from both `matchLabels` and `matchExpressions` are ANDed together [source: k8s-docs-persistent-volumes-depth-2026-08-25], reusing the selector grammar you already know *[cross-bearing: see Ch 4 §5 — labels and selectors]*. It can even name a specific volume: *a PVC can specify a particular PersistentVolume by name using the `volumeName` field* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Capacity is one filter among several.

### Phases

A PersistentVolume reports where it stands in its own lifecycle through a phase. The concept documentation names four, and the third one is the one that catches people.

| Phase | Meaning |
|---|---|
| `Available` | Provisioned, and no claim has taken it |
| `Bound` | Matched to a claim, and spoken for by that claim alone |
| `Released` | The claim is gone; the cluster has not yet finished with the volume |
| `Failed` | Automatic reclamation was attempted and did not succeed |

[source: k8s-docs-persistent-volumes-depth-2026-08-25]

`Released` is not `Available`. A volume whose claim has been deleted has *left* the bound state without *entering* the free state. Why that gap exists, and what closes it, is §4's business.

> 🪝 **Snag:** Two Kubernetes-project sources count the phases differently, and you should know it before an exam option makes the point for you. The concept documentation names the four above. The API reference for `PersistentVolume` v1 additionally documents a `Pending` phase, *used for PersistentVolumes that are not available* [source: k8s-api-ref-persistentvolume-v1-2026-08-25]. Learn the four — they describe the arc from free to bound to released that this chapter is built on. But if `Pending` turns up as an option, do not eliminate it on the grounds that no such phase exists. It exists. It is simply not one of the four the teaching documentation walks you through.

<!-- AUTHOR-REVIEW: PV phase count remains an open research gap — the concept page enumerates four phases, the v1 API reference five (adding `Pending`), and the cached depth snapshot flags the disagreement itself. The Snag above hedges the reader; a further retrieval of /docs/concepts/storage/persistent-volumes/#phase would settle the count and also clear the `Released`/`Failed` bullet prose for direct quotation. Until then the table paraphrases rather than quotes, per the snapshot's retrieval note. -->

> ⚓ **Worth Securing:** Kubernetes will not let you pull storage out from under a running Pod by accident. *The purpose of the Storage Object in Use Protection feature is to ensure that PersistentVolumeClaims in active use by a Pod and PersistentVolumes that are bound to PVCs are not removed from the system, as this may result in data loss* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Delete a PVC that a Pod is using and *the PVC is not removed immediately. PVC removal is postponed until the PVC is no longer actively used by any Pods* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. You will see it sitting in `Terminating` with `kubernetes.io/pvc-protection` in its finalizers list. If you have ever run `kubectl delete pvc` and watched it hang, this is why. It is protecting you.

A claim that never binds is, from the Pod's point of view, indistinguishable from a scheduling failure: the Pod sits in `Pending` and nothing happens. Chapter 13 will teach you to tell those two apart from the symptoms *[cross-bearing: see Ch 13 §2 — Pods that never start]*. This chapter supplies the mechanism; that one supplies the diagnosis.

---

## ☆ Taking Your Bearings #1

Five questions on the lifetime ladder and the supply/demand split. Answers and explanations follow; attempt them first.

**1.** A Pod runs a single container that writes `/data/cache.db`, where `/data` is an `emptyDir` volume. The container hits a null pointer and exits with code 1. The kubelet restarts it. Then, ten minutes later, you run `kubectl delete pod` and the Deployment's ReplicaSet creates a replacement. What is the state of `cache.db` after each event?

A) Gone after the crash; gone after the delete
B) Present after the crash; gone after the delete
C) Present after the crash; present after the delete
D) Gone after the crash; present after the delete

**2.** *[retrieval: ch2]* A different container in a different Pod writes `/tmp/scratch.log`, with no volume mounted anywhere. The process crashes and the kubelet restarts the container. Where was that file written, and is it still there?

A) To the image's read-only layers; still there, because image layers are immutable
B) To the container's writable layer; still there, because the layer persists across restarts
C) To the container's writable layer; gone, because the restarted container is assembled fresh from the image
D) To the container's writable layer; gone, because the Pod was replaced

**3.** Which statement correctly describes what a Pod references in order to use persistent storage?

A) The Pod's `volumes` block names a PersistentVolume directly, and Kubernetes finds a matching claim
B) The Pod's `volumes` block names a PersistentVolumeClaim, and the cluster uses the claim to find the bound PersistentVolume
C) The Pod's `volumes` block names a StorageClass, which selects a PersistentVolume at mount time
D) The Pod names both the PersistentVolume and the PersistentVolumeClaim, so the binding can be verified

**4.** A cluster has one PersistentVolume: 100Gi, `Available`, no StorageClass, no labels. A user creates a 10Gi PVC with no class and no selector; it binds. A second user then creates a 5Gi PVC with no class and no selector. What happens to the second claim?

A) It binds to the same PV, since 90Gi of capacity remains unused
B) It binds to the same PV and the first claim is evicted, since binding is exclusive
C) It remains unbound indefinitely, and will bind only if a matching volume becomes available
D) It fails immediately with an error, since no `Available` PV exists

**5.** An administrator deletes a PersistentVolumeClaim whose PV has the `Retain` reclaim policy. Immediately afterward, what phase is the PersistentVolume in, and what does that phase mean?

A) `Available` — the volume is free and the next matching claim will bind to it
B) `Released` — the claim is gone, but the volume has not been reclaimed and is not yet reusable
C) `Failed` — deleting a bound claim is an error condition
D) `Bound` — the reclaim policy `Retain` preserves the binding until an admin intervenes

---

**Answers with Explanations:**

**1 — B.** Present after the crash. Gone after the delete. If you reached for C, you reached for the trap this question was built around, and you are in large company.

- **A is wrong** because a container crash does not remove the Pod from the node, and *the data in an `emptyDir` volume is safe across container crashes* [source: k8s-docs-volume-types-depth-2026-08-25]. The file survives the restart.
- **B is correct.** Crash → survives (rung two beats a container restart). Delete → gone, because *when a Pod is removed from a node for any reason, the data in the `emptyDir` is deleted permanently* [source: k8s-docs-volume-types-depth-2026-08-25]. And the replacement Pod is a *different Pod*; its `emptyDir` is created empty when it is assigned to a node.
- **C is wrong** and is the single most common `emptyDir` misconception: assuming that because a volume survived a container restart, it must be persistent. It survives one boundary and not the other.
- **D is wrong** in both halves, and each half is a belief worth naming. "Gone after the crash" is *restart means fresh everything* — true of the container filesystem, false of the volume. "Present after the delete" is *the controller restores the volume along with the Pod* — the ReplicaSet restores the Pod, and an `emptyDir` in a new Pod is new and empty. D has the ladder exactly inverted.

**2 — C.** The file went to the container's writable layer, and the restarted container gets a clean state assembled from the image [source: k8s-docs-volumes-2026-08-23]. Rung one survives nothing.
- **A is wrong** because image layers are read-only; a write to a path backed by an image layer is copied up into the writable layer, not written into the image.
- **B is wrong** because it confuses the writable layer's *location* (correct) with its *lifetime* (wrong). This is the misconception the whole ladder exists to correct.
- **D is wrong** on the event, and this is the near-miss to sit with. The location is right and the outcome is right — the file is gone — but nothing replaced the Pod. The container exited and the kubelet restarted it inside the same Pod, on the same node. Rung one is erased by the *container* boundary, several rungs below the one D names. Arriving at the right outcome through the wrong boundary is still arriving wrongly, and the exam will offer you that option.

**3 — B.** *Pods use claims as volumes. The cluster inspects the claim to find the bound volume and mounts that volume for a Pod* [source: k8s-docs-persistent-volumes-2026-08-23].
- **A is wrong**, and it is the reversal to watch for. It has the direction of the relationship backwards: claims find volumes, not the other way around, and the Pod's reference terminates at the claim.
- **C is wrong**: a StorageClass is not something a Pod mounts. §3 covers what it actually does.
- **D is wrong**: the Pod names only the claim. It has no field for a PV.

**4 — C.** *Claims will remain unbound indefinitely if a matching volume does not exist. Claims will be bound as matching volumes become available* [source: k8s-docs-persistent-volumes-2026-08-23]. The only PV is `Bound`, so there is nothing to match.
- **A is wrong** because *a PVC to PV binding is a one-to-one mapping* and binds are exclusive [source: k8s-docs-persistent-volumes-2026-08-23]. Leftover capacity is not shareable. This is the "big enough, so it fits" trap.
- **B is wrong**: binding exclusivity protects the existing bind; it does not preempt it.
- **D is wrong** in an instructive way. There is no immediate error. The claim sits, quietly, and the Pod that references it sits in `Pending`. "Fails immediately" would at least be visible; "waits forever" is what actually happens.

**5 — B.** *When the PersistentVolumeClaim is deleted, the PersistentVolume still exists and the volume is considered 'released'. But it is not yet available for another claim because the previous claimant's data remains on the volume* [source: k8s-docs-persistent-volumes-depth-2026-08-25].
- **A is wrong**, and this specific wrong answer teaches more than the right one. `Released` ≠ `Available`. The volume is not reusable. §4 covers what an administrator has to do to make it so.
- **C is wrong**: the `Failed` phase records a volume whose automatic reclamation did not succeed [source: k8s-docs-persistent-volumes-depth-2026-08-25]. That is a later event and a different one. Deleting a bound claim is routine, not an error.
- **D is wrong**: the binding does not survive the claim's deletion. The claim is gone.

---

**If you scored 0–2:** Go back to §1's ladder figure and §2's Fixed Point specifically, about eight minutes of re-reading. The rest of the chapter builds directly on those two.

**If you scored 3–4:** Solid. Review the ones you missed, understand *why*, and continue.

**If you scored 5:** You have the foundation. §3 and §4 are where the exam yield concentrates, and you are in good shape to absorb them.

---

**Checkpoint: You've Now Mastered**
✓ The three-rung lifetime ladder and the two boundaries that define it
✓ Which volume types live on which rung, and what `subPath` cuts off
✓ PV as supply, PVC as demand, and why a Pod references only the claim
✓ Binding as an exclusive, one-to-one control-loop match that waits indefinitely
✓ The PV phases, and that `Released` is not `Available`

Two questions remain open, and they are the ones that matter: where does a PV come from if nobody made one, and what happens to the data when the claim is gone?

🗺️→🌊→🌅 · **Voyage Progress: two sections of seven. The vocabulary is set; the mechanics start now.**

---

## 🔵 §3 — Provisioning on Demand

Everything in §2 assumed a PersistentVolume already existed. Somebody made one, it sat there `Available`, and a claim found it.

That model works, and it has a name. It does not scale past a certain point, for a reason that becomes obvious the moment you try it. An administrator pre-creating PVs has to guess: how many, what sizes, what performance tiers, for which teams. Guess low and claims sit unbound. Guess high and you have provisioned storage nobody asked for. Guess wrong about the size distribution and you have forty 10Gi volumes and a team that needs one 400Gi volume. It is stocking the hold for a manifest nobody has written yet.

The object that fixes this is the StorageClass, and it is the third element that has been sitting off to the side of the figure since §2.

### What a StorageClass is

*A StorageClass provides a way for administrators to describe the classes of storage they offer. Different classes might map to quality-of-service levels, or to backup policies, or to arbitrary policies determined by the cluster administrators. Kubernetes itself is unopinionated about what classes represent* [source: k8s-docs-storage-classes-2026-08-25].

That last sentence is doing real work. Kubernetes does not know what `fast` means, or `bulk`, or `archive`. It knows those are names an administrator chose and attached to a provisioning configuration. The documentation offers a comparison that lands well for anyone with a storage background: *the Kubernetes concept of a storage class is similar to "profiles" in some other storage system designs* [source: k8s-docs-storage-classes-2026-08-25].

The problem it solves is stated back in the PersistentVolumes documentation, and it reads as a problem statement rather than a feature description: *cluster administrators need to be able to offer a variety of PersistentVolumes that differ in more ways than size and access modes, without exposing users to the details of how those volumes are implemented. For these needs, there is the StorageClass resource* [source: k8s-docs-persistent-volumes-2026-08-23].

*Without exposing users to the details.* That is the supply/demand split from §2, extended one level: the user asks for `fast`, and never learns what `fast` is made of.

*Each StorageClass contains the fields `provisioner`, `parameters`, and `reclaimPolicy`, which are used when a PersistentVolume belonging to the class needs to be dynamically provisioned to satisfy a PersistentVolumeClaim* [source: k8s-docs-storage-classes-2026-08-25]. And *the name of a StorageClass object is significant, and is how users can request a particular class* [source: k8s-docs-storage-classes-2026-08-25]. The name is the API. When a developer writes `storageClassName: low-latency`, they are using that name as the entire interface to a provisioning system they know nothing else about.

Here is what one actually looks like:

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: low-latency
  annotations:
    storageclass.kubernetes.io/is-default-class: "false"
provisioner: csi-driver.example-vendor.example
reclaimPolicy: Retain # default value is Delete
allowVolumeExpansion: true
mountOptions:
  - discard # this might enable UNMAP / TRIM at the block storage layer
volumeBindingMode: WaitForFirstConsumer
parameters:
  guaranteedReadWriteLatency: "true" # provider-specific
```
[source: k8s-docs-storage-classes-2026-08-25]

Note `parameters`. That field is a passthrough: its contents are meaningful to the provisioner and opaque to Kubernetes. `guaranteedReadWriteLatency: "true"` means something to that vendor's driver and nothing at all to the API server.

Two fields in that example, `allowVolumeExpansion` and `mountOptions`, get no treatment in this chapter, and that is deliberate rather than an oversight. They are real provisioning-behavior knobs, and they are reproduced here so you are looking at an actual StorageClass rather than a trimmed one. They sit outside this chapter's scope; nothing later depends on them.

<!-- AUTHOR-REVIEW: the curriculum-alignment audit suggested optionally glossing allowVolumeExpansion with the storage-classes page's "you can only use the volume expansion feature to grow a Volume, not to shrink it." That sentence is not attested in any snapshot this chapter has cited, so it is not quoted here. If a verification pass confirms it in k8s-docs-storage-classes-2026-08-25, swap the paragraph above for a one-sentence sourced gloss. -->

The `provisioner` field is the one that makes the class do anything: *each StorageClass has a provisioner that determines what volume plugin is used for provisioning PVs. This field must be specified* [source: k8s-docs-storage-classes-2026-08-25]. Provisioners come in two flavors: internal ones shipped alongside Kubernetes with `kubernetes.io`-prefixed names, and *external provisioners, which are independent programs that follow a specification defined by Kubernetes*, whose authors *have full discretion over where their code lives, how the provisioner is shipped, how it needs to be run* [source: k8s-docs-storage-classes-2026-08-25]. Hold that phrase — *independent programs* — because §5 is about what happens when nobody runs one.

### Two ways a volume comes to exist

<!-- FIGURE: ch11-fig03-static-vs-dynamic-provisioning -->
![A flowchart starting at PVC creation, branching on whether a matching PersistentVolume already exists; yes leads to static binding, no leads to a second decision requiring both a named StorageClass and a configured provisioner, whose true branch is dynamic provisioning and whose false branch dead-ends at a claim that waits indefinitely with the Pod stuck in Pending](figures/ch11-fig03-static-vs-dynamic-provisioning.svg)

<!-- ASCII-FALLBACK
```
                        A PVC IS CREATED
                               │
                               ▼
              ┌────────────────────────────────┐
              │ Does a matching PV already     │
              │ exist and is it Available?     │
              └───────┬────────────────┬───────┘
                      │ YES            │ NO
                      ▼                ▼
        ═════ STATIC ═════      ┌─────────────────────────┐
                                │ Does the claim name a   │
   admin pre-created a PV       │ StorageClass, AND is a  │
   carrying the real storage    │ provisioner configured  │
   details                      │ for that class?         │
              │                 └───┬─────────────────┬───┘
              │                     │ BOTH            │ EITHER
              │                     │ TRUE            │ MISSING
              ▼                     ▼                 ▼
     ┌─────────────────┐  ═══ DYNAMIC ═══     ┌──────────────────┐
     │  binder matches │                      │  CLAIM WAITS,    │
     │  claim ↔ PV     │  provisioner creates │  INDEFINITELY    │
     └────────┬────────┘  a PV for this claim │                  │
              │                    │          │  Pod stays in    │
              │                    ▼          │  Pending.        │
              │           ┌─────────────────┐ │  No error event  │
              │           │  binder matches │ │  that says so.   │
              │           │  claim ↔ new PV │ └──────────────────┘
              │           └────────┬────────┘        ▲
              │                    │                 │
              └────────┬───────────┘        an object without its
                       ▼                    component does nothing
              ┌─────────────────┐
              │   PVC is BOUND  │
              │  Pod can mount  │
              └─────────────────┘
```
-->

**Static provisioning** is the §2 model, named. *A cluster administrator creates a number of PVs. They carry the details of the real storage, which is available for use by cluster users* [source: k8s-docs-persistent-volumes-2026-08-23]. Supply exists first; demand arrives later and matches against it.

**Dynamic provisioning** inverts the order. *When none of the static PVs the administrator created match a user's PersistentVolumeClaim, the cluster may try to dynamically provision a volume specially for the PVC* [source: k8s-docs-persistent-volumes-2026-08-23]. Demand arrives first, and supply is manufactured to fit it.

Note the word *may*. It is doing precise work, and the next sentence explains why.

> ★ **Fixed Point**
>
> **Dynamic provisioning requires two conditions, not one.**
>
> *This provisioning is based on StorageClasses: the PVC must request a storage class and the administrator must have created and configured that class for dynamic provisioning to occur* [source: k8s-docs-persistent-volumes-2026-08-23].
>
> The claim must name a class **and** that class must be configured to provision. One without the other yields a claim that waits forever, which, per §2, is not an error, not a timeout, and not a failure event. It is silence.

### Defaults, and one opt-out that surprises people

A cluster does not have to make every developer name a class explicitly. *You can mark a StorageClass as the default for your cluster. When a PVC does not specify a `storageClassName`, the default StorageClass is used* [source: k8s-docs-storage-classes-2026-08-25]. The mark is an annotation: `storageclass.kubernetes.io/is-default-class: "true"` [source: k8s-docs-persistent-volumes-depth-2026-08-25].

Where a default exists, that is what lets a developer write a five-line PVC and get a working disk without knowing any of this. Whether a given cluster has one is a question to ask rather than assume; the ⚓ below covers what happens when the answer is no.

Now the case that catches people. There are two ways a PVC can appear to "not ask for a class," and they behave differently:

| What the PVC has | What happens |
|---|---|
| No `storageClassName` field at all | The default StorageClass is used, if one exists |
| `storageClassName: ""` (empty string) | Dynamic provisioning is **disabled for that claim** |

*A PVC with its `storageClassName` set to `""` is explicitly stating that it is bound with a PV with no class, hence the PV's `storageClassName` must also be empty. A PVC with no `storageClassName` is not quite the same and is treated differently by the cluster* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. And from the lifecycle section, stated as a consequence: *claims that request the class `""` effectively disable dynamic provisioning for themselves* [source: k8s-docs-persistent-volumes-2026-08-23].

> 🪝 **Snag:** `storageClassName: ""` is not "use whatever the cluster's default is." It is the opposite: "do not use a class at all, and do not provision anything for me." A reader who writes it expecting the default gets a claim that will only ever bind to a classless PV, and on a cluster where every PV comes from a StorageClass, that means it never binds. Empty string is an opt-out, not a shrug.

> ⚓ **Worth Securing:** A cluster can have no default at all: *if you don't mark any StorageClass as default (and one hasn't been set for you by, for example, a cloud provider), then Kubernetes cannot apply that defaulting for PersistentVolumeClaims that need it* [source: k8s-docs-storage-classes-2026-08-25]. Such a PVC is not rejected: *the new PVC creates as you defined it, and the `storageClassName` of that PVC remains unset until a default becomes available* [source: k8s-docs-storage-classes-2026-08-25]. And if a default appears later, the control plane retroactively updates those waiting PVCs to point at it [source: k8s-docs-storage-classes-2026-08-25]. This is a control loop doing exactly what control loops do: the desired state was underspecified, and the moment the information arrived, it reconciled *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*.

### The claim that waits because nobody installed the thing

You were set up for this two chapters ago. Chapter 10's closing said: *you will meet several objects in Chapter 11 that describe storage without providing any, and at least one arrangement where a claim sits unbound because the thing that would satisfy it has not been installed. You know what question to ask about that now.*

You do. The phrase is Chapter 3's, and Chapter 10 §3 named it as a pattern: **an object without its component does nothing** *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*.

A StorageClass is a description of a provisioning capability. It is not the provisioning capability. Create a StorageClass whose `provisioner` names a driver that nobody deployed, and you get a perfectly valid API object that provisions exactly nothing. Claims naming that class sit unbound. Pods referencing those claims sit `Pending`.

This is the third sighting of the same light. An Ingress with no Ingress controller routes nothing. A NetworkPolicy on a CNI plugin that doesn't implement policy blocks nothing. A StorageClass with no running provisioner creates nothing. Each time, the object exists, `kubectl get` shows it, `kubectl describe` shows a sensible spec, and nothing happens, because the object was always only ever a request addressed to a component that has to be separately installed and running.

You will see it a fourth time in §5, and by then the recognition should be automatic.

### When binding waits for the scheduler

One more StorageClass field, and it connects storage to something you learned four chapters ago in a way that is genuinely load-bearing rather than decorative.

*The `volumeBindingMode` field controls when volume binding and dynamic provisioning should occur. When unset, `Immediate` mode is used by default* [source: k8s-docs-storage-classes-2026-08-25]. `Immediate` means what it says: *volume binding and dynamic provisioning occurs once the PersistentVolumeClaim is created* [source: k8s-docs-storage-classes-2026-08-25].

That sounds fine until you think about *where* the volume gets created. Consider a cloud with three availability zones and block storage that can only be attached to instances in the same zone. The claim is created; `Immediate` binding provisions a volume in zone A; then the scheduler tries to place the Pod and discovers the only nodes with enough memory are in zone C. The documentation states the outcome without softening it: *for storage backends that are topology-constrained and not globally accessible from all Nodes in the cluster, PersistentVolumes will be bound or provisioned without knowledge of the Pod's scheduling requirements. This may result in unschedulable Pods* [source: k8s-docs-storage-classes-2026-08-25].

The fix is to make binding wait: *a cluster administrator can address this issue by specifying the `WaitForFirstConsumer` mode which will delay the binding and provisioning of a PersistentVolume until a Pod using the PersistentVolumeClaim is created. PersistentVolumes will be selected or provisioned conforming to the topology that is specified by the Pod's scheduling constraints. These include, but are not limited to, resource requirements, node selectors, pod affinity and anti-affinity, and taints and tolerations* [source: k8s-docs-storage-classes-2026-08-25].

Read that list of constraints again: resource requirements, node selectors, affinity, anti-affinity, taints and tolerations. That is Chapter 7's filter phase, item for item *[cross-bearing: see Ch 7 §2 — what makes a node feasible]*. `WaitForFirstConsumer` exists because scheduling and storage placement are not two decisions that happen to interact. They are one decision, and making them separately produces a Pod that cannot run.

The `local` volume documentation makes the same argument independently, which is a good sign that it is the real reason rather than a rationalization: *when using local volumes, it is recommended to create a StorageClass with `volumeBindingMode` set to `WaitForFirstConsumer`. Delaying volume binding ensures that the PersistentVolumeClaim binding decision will also be evaluated with any other node constraints the Pod may have, such as node resource requirements, node selectors, Pod affinity, and Pod anti-affinity* [source: k8s-docs-volume-types-depth-2026-08-25].

> 🔭 **Closer Look:** `WaitForFirstConsumer` sits above the depth this book judges KCNA to require. CNCF publishes the Storage competency as a single word and nothing more; this book's domain analysis reads that word as centring on the three-way distinction between PersistentVolume, PersistentVolumeClaim, and StorageClass, not on tuning binding modes. What you should carry forward from this subsection is the consequence, not the field name: **volume binding can wait on scheduling, because binding a volume before the scheduler has picked a node can bind it somewhere the Pod cannot go.** If you remember that sentence and forget `volumeBindingMode` entirely, you have taken the right thing.
>
> Two operational notes for the day you meet this in a real cluster. First, the mode is not universally supported: *the following plugins support `WaitForFirstConsumer` with dynamic provisioning: CSI volumes, provided that the specific CSI driver supports this* [source: k8s-docs-storage-classes-2026-08-25]. Second, it interacts badly with one particular shortcut: *if you choose to use `WaitForFirstConsumer`, do not use `nodeName` in the Pod spec to specify node affinity. If `nodeName` is used in this case, the scheduler will be bypassed and PVC will remain in `pending` state* [source: k8s-docs-storage-classes-2026-08-25]. Bypass the scheduler *[cross-bearing: see Ch 7 §6 — overruling the scheduler]* and you have removed the very consumer the binding was waiting for.

---

## 🔵 §4 — Access Modes and What Happens After

Calibrate on the exam yield rather than the difficulty glyph, because on this section the two point in opposite directions.

This section is marked 🔵 Standard, and that rating is honest. Access modes and reclaim policies are enumerable facts with no conceptual depth to speak of. There is no hard idea here. But five of the seven exam traps this chapter's domain analysis identified live in this section and the last one, and four of them are here. **This material is not hard, and it is where the points are.** Read it as though it were 🔴, and take the checkpoint that follows seriously.

Two questions, and they are the two halves of one question. *What may you do with this volume?* That is access modes. *What happens when you stop?* That is reclaim policy. Anyone who has managed storage before will recognize that these are always asked together.

> **Dead Reckoning:** There are four access modes. `ReadWriteOnce` (RWO): the volume can be mounted as read-write by a single node. `ReadOnlyMany` (ROX): the volume can be mounted as read-only by many nodes. `ReadWriteMany` (RWX): the volume can be mounted as read-write by many nodes. `ReadWriteOncePod` (RWOP): the volume can be mounted as read-write by a single Pod [source: k8s-docs-persistent-volumes-depth-2026-08-25]. In the CLI they are abbreviated RWO, ROX, RWX, and RWOP [source: k8s-docs-persistent-volumes-depth-2026-08-25]. A volume can only be mounted using one access mode at a time, even if it supports many [source: k8s-docs-persistent-volumes-depth-2026-08-25].
>
> There are three reclaim policies, one of which is deprecated. `Retain`: when the claim is deleted the PV still exists, the volume is considered released, and an administrator must manually reclaim it. `Delete`: removes both the PersistentVolume object from Kubernetes and the associated storage asset in the external infrastructure. `Recycle`: deprecated [source: k8s-docs-persistent-volumes-2026-08-23].
>
> The defaults differ by how the volume came to exist: `Retain` is the default for manually created PersistentVolumes, and `Delete` is the default for dynamically provisioned PersistentVolumes [source: k8s-api-ref-persistentvolume-v1-2026-08-25].

Now the parts that need explaining.

### Access modes count nodes

The Soundings asked you whether two machines can safely mount one block device read-write at the same time. They cannot, not without a clustered filesystem coordinating them.

That is not a Kubernetes fact, and no Kubernetes document will tell you so. It is ordinary storage knowledge that the platform inherits from the hardware beneath it. Two independent filesystem drivers, each caching metadata for the same device, will eventually write over each other's bookkeeping and destroy the filesystem. Two crews restowing the same hold from two different manifests lose the cargo, and neither crew notices until somebody goes looking for it.

That physical constraint is what access modes encode. The unit is the **node**, because the node is where the mount happens and the kernel's filesystem driver is what would be doing the corrupting.

The documentation puts the constraint's origin plainly: *a PersistentVolume can have any access mode supported by the resource provider. For example, NFS can support multiple read/write clients, but an iSCSI volume can only be used by one client at a time. Each PV gets its own set of access modes describing that specific PV's capabilities* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Access mode is not a policy you choose. It is a capability the underlying storage either has or does not.

And here is the sentence that generates the single most common storage mistake in Kubernetes, followed immediately by its own remedy: *ReadWriteOnce access mode still can allow multiple Pods to access the volume when the Pods are running on the same node. For single Pod access, use ReadWriteOncePod* [source: k8s-docs-persistent-volumes-depth-2026-08-25].

> ★ **Fixed Point**
>
> **RWO counts nodes. RWOP is the one that counts Pods.**
>
> Three of the four modes are statements about how many *nodes* may mount the volume. Only `ReadWriteOncePod` changes the unit: *use ReadWriteOncePod access mode if you want to ensure that only one Pod across whole cluster can read and write that PVC* [source: k8s-docs-persistent-volumes-depth-2026-08-25].
>
> The existence of a fourth mode devoted entirely to the Pod/node distinction is itself the evidence that the distinction is hard to hold. Kubernetes shipped a whole access mode because people kept assuming RWO already meant it.

<!-- FIGURE: ch11-fig04-access-modes-and-reclaim-policies -->
![Two side-by-side reference panels: the left lists four access modes with the unit being nodes except for ReadWriteOncePod, which is highlighted as the only Pod-scoped mode; the right tabulates three reclaim policies showing Retain keeps the PV object, asset and data, Delete destroys all three, and Recycle is deprecated, with a footer noting Delete is the default for dynamically provisioned volumes](figures/ch11-fig04-access-modes-and-reclaim-policies.svg)

<!-- ASCII-FALLBACK
```
 ┌─ WHAT YOU MAY DO ────────────┐  ┌─ WHAT HAPPENS AFTER ───────────┐
 │  access modes                │  │  reclaim policies              │
 │  UNIT = NODES (except RWOP)  │  │  when the claim is deleted     │
 │                              │  │                                │
 │  RWO   ▣ · ·   1 node, r/w   │  │           PV obj  asset  data  │
 │  ROX   ▣ ▣ ▣   many, r/o     │  │  Retain     kept   kept   kept │
 │  RWX   ▣ ▣ ▣   many, r/w     │  │  Delete     gone   gone   gone │
 │  RWOP  ◉ · ·   1 POD, r/w    │  │  ~Recycle~   —      —      —   │
 │        ↑                     │  │   (deprecated)                 │
 │        └─ the unit changes   │  │                                │
 │           HERE, and only     │  │  DEFAULT for dynamically       │
 │           here               │  │  provisioned volumes: Delete   │
 └──────────────────────────────┘  └────────────────────────────────┘
```
-->

Two more facts about access modes that are easy to state and easy to forget:

*A volume can only be mounted using one access mode at a time, even if it supports many. For example, a NFS volume can be mounted as ReadWriteOnce on one node and read-only on another node at the same time, but not on the same node for both read-write and read-only* [source: k8s-docs-persistent-volumes-depth-2026-08-25].

And a limit on what the mode actually enforces: *a volume access mode does not enforce write protection. For example, if you provision a ReadOnlyMany volume, it does not prevent an application from writing to the mounted volume if the Pod's securityContext allows write access* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. `ReadOnlyMany` describes what the storage supports. It is not a permission system *[cross-bearing: see Ch 12 §5 — what a Pod may do to its node]*.

> 🪢 **Mnemonic:** **Read the last word as the unit.** `ReadWriteOnce`: once *per node*. `ReadOnlyMany`: many *nodes*. `ReadWriteMany`: many *nodes*. `ReadWriteOncePod`: the unit is in the name, because it is the exception. Three modes leave the unit implicit and one spells it out; the one that spells it out is the one that differs.

### Reclaim: what happens after

Delete a PersistentVolumeClaim and the storage does not simply vanish, nor does it simply persist. What happens is determined by a policy attached to the PersistentVolume, and, critically, that policy was usually chosen by someone else, earlier.

*When a user is done with their volume, they can delete the PVC objects from the API that allows reclamation of the resource. The reclaim policy for a PersistentVolume tells the cluster what to do with the volume after it has been released of its claim* [source: k8s-docs-persistent-volumes-2026-08-23].

**Retain.** *The `Retain` reclaim policy allows for manual reclamation of the resource. When the PersistentVolumeClaim is deleted, the PersistentVolume still exists and the volume is considered 'released'. But it is not yet available for another claim because the previous claimant's data remains on the volume* [source: k8s-docs-persistent-volumes-depth-2026-08-25].

The word doing the work there is *manual*. Retain does not mean "kept and reusable." It means "kept and stuck." The administrator's steps are enumerated:

> 1. Delete the PersistentVolume. The associated storage asset in external infrastructure still exists after the PV is deleted.
> 2. Manually clean up the data on the associated storage asset accordingly.
> 3. Manually delete the associated storage asset.
>
> [source: k8s-docs-persistent-volumes-depth-2026-08-25]

And if you want the storage back in service: *if you want to reuse the same storage asset, create a new PersistentVolume with the same storage asset definition* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. A *new* PersistentVolume object. The released one does not go back to `Available` on its own, ever.

**Delete.** *For volume plugins that support the `Delete` reclaim policy, deletion removes both the PersistentVolume object from Kubernetes, as well as the associated storage asset in the external infrastructure* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Both. The API object and the actual disk in the actual cloud.

**Recycle** is deprecated. *The recommended approach is to use dynamic provisioning* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. For completeness: where it is still supported, it *performs a basic scrub (`rm -rf /thevolume/*`) on the volume and makes it available again for a new claim* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. It exists on the exam as a name you should recognize and correctly identify as retired.

### Where the decision was actually made

Now the part that answers the question this chapter opened with.

*Volumes that were dynamically provisioned inherit the reclaim policy of their StorageClass, which defaults to `Delete`* [source: k8s-docs-persistent-volumes-depth-2026-08-25].

And the StorageClass's own default, from the class's side: *if no `reclaimPolicy` is specified when a StorageClass object is created, it will default to `Delete`* [source: k8s-docs-storage-classes-2026-08-25].

Follow the chain. A developer writes a PVC. It names no class, so the cluster's default class applies. That class's author did not set `reclaimPolicy`, so it is `Delete`. The volume is provisioned and inherits `Delete`. Some months later the developer deletes the PVC — perhaps while cleaning up a namespace, perhaps as part of tearing down a test environment that turned out to be sharing a class with production — and the disk is destroyed.

Nobody in that story made a decision about the data's survival. The terms of the arrangement were set once, in a StorageClass manifest, by an administrator who was configuring a cluster and not thinking about this specific developer or this specific volume: standing orders written before this cargo, this shipper, or this voyage existed. The documentation says as much, in the mildest possible terms: *the administrator should configure the StorageClass according to users' expectations; otherwise, the PV must be edited or patched after it is created* [source: k8s-docs-persistent-volumes-depth-2026-08-25].

> ★ **Fixed Point**
>
> **Dynamically provisioned volumes inherit the StorageClass's reclaim policy, and that policy defaults to `Delete`.**
>
> The decision about whether your data survives the deletion of your claim was made by whoever wrote the StorageClass: before your namespace existed, before your application was written, and without reference to either. If you never looked at your cluster's default StorageClass, you do not know what happens when you delete a PVC.
>
> `kubectl get storageclass` takes two seconds. Run it on a cluster you care about.

> ⚠ **Navigational Hazards: the reclaim cluster**
>
> Three closely-related mistakes, all of which produce the same category of outcome: the one where the data is gone.
>
> **"Deleting a PVC keeps the data."** Only if the reclaim policy says so, and for a dynamically provisioned volume the inherited default is `Delete` [source: k8s-docs-persistent-volumes-depth-2026-08-25]. The safe assumption is the opposite of the intuitive one.
>
> **"Retain means the volume is reusable."** It means `Released`, not `Available`. *It is not yet available for another claim because the previous claimant's data remains on the volume* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Reclaiming it takes three manual steps and produces a *new* PV object.
>
> **"`Recycle` will scrub it and hand it back."** `Recycle` is deprecated [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Do not plan around it, and recognize it on an exam as the retired option.
>
> The through-line: every one of these is a wrong guess about a default someone else set. That is what makes them dangerous rather than merely wrong. You cannot catch them by reading your own manifest. They were settled in somebody else's.

> ⚓ **Worth Securing:** Manually created PersistentVolumes default to `Retain` [source: k8s-api-ref-persistentvolume-v1-2026-08-25], the opposite of the dynamic default. This is not an inconsistency; it is the API being sensible about intent. If an administrator hand-built a PV pointing at a real NFS export, deleting the API object should not scrub the export. If a provisioner created a volume on demand for one claim, cleaning it up when the claim is gone is the point of having it created on demand. The defaults differ because the situations differ.

### Chapter 6's five verbs, settled

Chapter 6 §6 made an unusually blunt deferral. It told you about StatefulSets and stable identity, and then said: *you have not been told how that storage is provisioned, requested, sized, reclaimed, or shared. That is deliberate.*

Five verbs. Here they are, closed:

| Verb | Where it was answered |
|---|---|
| **provisioned** | §3 — statically by an administrator, or dynamically by a provisioner named in a StorageClass |
| **requested** | §2 — by a PersistentVolumeClaim, which is a request for storage by a user |
| **sized** | §2 — the claim requests a capacity; binding matches it against a PV that satisfies it |
| **reclaimed** | §4 — by the reclaim policy, `Retain` or `Delete`, inherited from the class for dynamic volumes |
| **shared** | §4 — by the access mode, which states how many nodes (or, for RWOP, how many Pods) may mount it |

Chapter 6 was right that it was deliberate. Every one of those verbs needed the supply/demand split before it could be answered honestly, and that split is the whole content of §2. Explaining "reclaimed" in Chapter 6 would have required explaining StorageClasses, which would have required explaining provisioning, which would have required the PV/PVC distinction: an entire chapter, arriving five chapters early, in the middle of a discussion about workload controllers.

What Chapter 6 kept back for itself, and still owns, is **identity** *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*. §6 of this chapter is where the two halves meet.

---

## 🔵 §5 — Who Actually Provides the Storage

Chapter 10 closed by telling you that this chapter brings the last of the four pluggable interfaces, and that with it the set closes. Here it is.

You have three already, collected one chapter at a time. CRI at the container runtime *[cross-bearing: see Ch 2 §4 — the Container Runtime Interface]*. CRDs at the API itself *[cross-bearing: see Ch 6 §8 — the control loop, extended]*. CNI at the network *[cross-bearing: see Ch 9 §1 — four rules and a plugin]*. The fourth is CSI, at storage.

**The Container Storage Interface (CSI) defines a standard interface for container orchestration systems (like Kubernetes) to expose arbitrary storage systems to their container workloads** [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].

The glossary states the consequence: *CSI allows vendors to create custom storage plugins for Kubernetes without adding them to the Kubernetes repository (out-of-tree plugins)* [source: k8s-glossary-storage-terms-2026-08-25]. And from the volumes page, the same claim in the sharpest available form: vendors *can implement `csi` volumes to introduce new storage systems into Kubernetes without ever having to edit the core Kubernetes code* [source: k8s-docs-volumes-2026-08-23].

*Without ever having to edit the core Kubernetes code.* If that phrasing feels familiar, it should. It is structurally identical to what CRI bought at the runtime boundary and what CNI bought at the network boundary. Same move, fourth socket.

### Why it exists: the world before

The reason CSI was necessary takes one paragraph, and it makes the argument concrete rather than architectural.

*Previously, all volume plugins were "in-tree". The "in-tree" plugins were built, linked, compiled, and shipped with the core Kubernetes binaries. This meant that adding a new storage system to Kubernetes (a volume plugin) required checking code into the core Kubernetes code repository* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].

Sit with the consequences of that. The documentation records the arrangement, not what it cost the people living inside it, so what follows is this book's reading rather than a sourced claim. A storage vendor wanting Kubernetes support had to submit code to the Kubernetes project, have it reviewed by Kubernetes maintainers, and wait for a Kubernetes release. Their bug fixes shipped on Kubernetes' schedule, not their own. Meanwhile, Kubernetes maintainers were reviewing and carrying storage code for hardware they did not own and could not test.

*Both CSI and FlexVolume allow volume plugins to be developed independently of the Kubernetes code base, and deployed (installed) on Kubernetes clusters as extensions* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. FlexVolume was the earlier attempt and is now deprecated: *using an out-of-tree CSI driver is the recommended way to integrate external storage with Kubernetes* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].

> ★ **Fixed Point**
>
> **CSI is a published contract between two parties, and one of them is not Kubernetes.**
>
> The specification states its own purpose in a sentence that says more than any Kubernetes documentation can: CSI exists to *"define an industry standard 'Container Storage Interface' (CSI) that will enable storage vendors (SP) to develop a plugin once and have it work across a number of container orchestration (CO) systems"* [source: csi-spec-objective-2026-08-25].
>
> Read *"across a number of container orchestration systems."* CSI is not a Kubernetes feature that vendors happen to use. It is a cross-orchestrator standard that Kubernetes happens to implement, the same shape as OCI at the image and runtime boundary *[cross-bearing: see Ch 2 §5 — the Open Container Initiative]*. Storage stops being Kubernetes' problem and becomes a vendor's, on terms both parties agreed to in public.
>
> With this you hold all four: **CRI, CNI, CSI, CRDs.** Chapter 17 will ask you to state the shape they have in common without help *[cross-bearing: see Ch 17 §4 — every place Kubernetes lets you in]*.

### What a driver is, and what installing one puts in the cluster

Chapter 2 promised you "CSI and storage drivers," with *drivers* in the promise. So: what is a driver, concretely?

A CSI driver is software you deploy into the cluster, and it deploys as ordinary Kubernetes workloads. *A CSI driver is typically deployed in Kubernetes as two components: a controller component and a per-node component* [source: kubernetes-csi-docs-deployment-2026-08-25]. The controller component *can be deployed as a Deployment or StatefulSet on any node in the cluster*, and the node component *should be deployed on every node in the cluster through a DaemonSet* [source: kubernetes-csi-docs-deployment-2026-08-25].

That shape should be recognizable without further explanation. One controller, running somewhere, handling the cluster-wide operations: create this volume, delete that one *[cross-bearing: see Ch 6 §1 — the resource that holds the intent]*. One agent per node, running everywhere, handling the node-local operations: mount this volume into this path on this machine. DaemonSet is exactly the workload type for "one per node" *[cross-bearing: see Ch 6 §7 — one per node, and work that ends]*. A CSI driver is not exotic infrastructure. It is a Deployment and a DaemonSet, running software somebody else wrote.

Installing one also puts an object in the cluster: *CSIDriver captures information about a Container Storage Interface (CSI) volume driver deployed on the cluster* [source: k8s-api-ref-csidriver-v1-2026-08-25]. Which makes it the fourth object in this chapter that describes storage without providing any — PV, PVC, StorageClass, CSIDriver — and the one where the gap is most literal, since its whole documented job is to *capture information about* a driver that exists elsewhere.

Once installed, the driver's volumes are usable in three ways: *through a reference to a PersistentVolumeClaim*, *with a generic ephemeral volume*, or *with a CSI ephemeral volume if the driver supports that* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. The PersistentVolumeClaim path is the one §2 through §4 described.

### The fourth sighting

You have now seen the pattern three times in three sections: an Ingress without a controller, a StorageClass without a provisioner, and now this. Here is the fourth, and the sources state it not as a warning but as a plain ordering requirement:

*To use a CSI driver from a storage provider, you must first deploy it to your cluster. You will then be able to create a Storage Class that uses that CSI driver* [source: k8s-glossary-storage-terms-2026-08-25].

*First.* Then. And from the migration documentation, in case the point needed to be blunter: *as part of that migration, you — or another cluster administrator — must have installed and configured the appropriate CSI driver for that storage. **The core of Kubernetes does not install that software for you**.* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]

**An object without its component does nothing** *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*. A StorageClass naming a CSI driver nobody deployed is not an exotic failure you have to imagine. It is the documented prerequisite, unmet. The claim sits unbound. The Pod sits `Pending`. `kubectl get storageclass` shows the class, healthy and correct, describing a capability that does not exist.

That is the same light, the fourth time. And once you have seen it four times, you stop asking "is the object there?" and start asking "is the *component* there?", which is the question Chapter 10 said you would know to ask.

> 🔭 **Closer Look: CSI migration**
>
> CNCF publishes the Storage competency as a single word. This book's reading of it puts CSI at recall depth: name the storage interface, say what it is for, and stop there. What follows goes deeper than that reading requires, and is here for the day you meet it in a cluster rather than on a test.
>
> The in-tree plugins did not vanish when CSI arrived; they were migrated behind it. *The `CSIMigration` feature directs operations against existing in-tree plugins to corresponding CSI plugins (which are expected to be installed and configured). As a result, operators do not have to make any configuration changes to existing Storage Classes, PersistentVolumes, or PersistentVolumeClaims (referring to in-tree plugins) when transitioning to a CSI driver that supersedes an in-tree plugin* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].
>
> The compatibility promise is unusually strong: *existing PVs created by an in-tree volume plugin can still be used in the future without any configuration changes, even after the migration to CSI is completed for that volume type, and even after you upgrade to a version of Kubernetes that doesn't have compiled-in support for that kind of storage* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. Your manifests keep working; the machinery underneath them was replaced. *The actual storage management now happens through the CSI driver* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].
>
> The operations CSI covers: *provisioning/delete, attach/detach, mount/unmount, and resizing of volumes* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. That list is the storage lifecycle, and it maps cleanly onto everything §2 through §4 described.

> 🪝 **Snag:** CSI is an interface, not a product. There is no "CSI storage" you can buy or deploy, any more than there is "CNI networking." What you deploy is a *driver*, written by whoever owns the storage it speaks to — one for a cloud provider's block store, one for a software-defined storage project, one for an on-premises array — each implementing the same contract against different hardware. A question that treats CSI as a storage system rather than as the interface storage systems implement is testing exactly this confusion.

<!-- AUTHOR-REVIEW: The three named CSI drivers previously listed here (AWS EBS, Ceph, vSphere) were genericized — no cached snapshot enumerates driver implementations. Research gap to open: the kubernetes-csi drivers list, (the `ebs.csi.aws.com` clause that stood here was struck 2026-08-30: that string appears nowhere in the chapter any more — Bearings #3 Q2 now uses `blockstore.example.com` — so no source is owed for it). If that source lands, restore the named examples with a tag. -->

---

## 🔵 §6 — Pods That Are Not Interchangeable, Revisited

In Chapter 6, you were told that this explanation was incomplete. Not implied. Told, in as many words, with the deferred material enumerated and the deferral labeled deliberate.

This is the missing half, arriving on schedule.

Chapter 6 §6 gave you StatefulSet identity: Pods with stable ordinals, `web-0` and `web-1` and `web-2`, names that stick across rescheduling rather than being regenerated with each replacement *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*. Chapter 9 gave you the network half of that identity: the headless Service *[cross-bearing: see Ch 9 §5 — when you don't want a single address]* and the per-Pod DNS names it produces *[cross-bearing: see Ch 9 §7 — names, and where they resolve]*. What was missing both times was storage, and storage needed the whole of §2 through §4 before it could be explained without hand-waving.

### One claim per Pod, from a template

The mechanism is a field on the StatefulSet: `volumeClaimTemplates`. It looks like this, in the documentation's own nginx example:

```yaml
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "my-storage-class"
      resources:
        requests:
          storage: 1Gi
```
[source: k8s-docs-statefulset-storage-2026-08-25]

That is a PersistentVolumeClaim spec — the same fields §2 taught you, in the same shapes — sitting inside a workload controller as a template rather than as an object. And the rule for what the controller does with it is one sentence:

**For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim** [source: k8s-docs-statefulset-storage-2026-08-25].

Not one claim for the set. One claim *per Pod*, minted from the template as each Pod is created. A three-replica StatefulSet named `web` with a template named `www` yields three claims, and the naming follows the same ordinal identity Chapter 6 taught, so you can read a cluster's storage from its Pod names and vice versa.

Where those claims get their storage is §3, arriving as a consequence rather than as a rule: *the storage for a given Pod must either be provisioned by a PersistentVolume Provisioner based on the requested storage class, or pre-provisioned by an admin* [source: k8s-docs-statefulset-2026-08-24]. Dynamic or static. The two paths from §3, with nothing special added for StatefulSets.

<!-- FIGURE: ch11-fig05-statefulset-pvc-pairing -->
![Three stacked bands showing a three-replica StatefulSet named web, each Pod paired one-to-one with its own PersistentVolumeClaim named www-web-0 through www-web-2; in the second band web-1 has moved to a different node and keeps its claim, and in the third band web-1 is deleted while its claim remains in place](figures/ch11-fig05-statefulset-pvc-pairing.svg)

<!-- ASCII-FALLBACK
```
   StatefulSet "web"  ·  volumeClaimTemplates: [ www ]  ·  replicas: 3

     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │  web-0  │        │  web-1  │        │  web-2  │
     └────┬────┘        └────┬────┘        └────┬────┘
          │                  │                  │
          ▼                  ▼                  ▼
     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │ PVC     │        │ PVC     │        │ PVC     │
     │ www-    │        │ www-    │        │ www-    │
     │ web-0   │        │ web-1   │        │ web-2   │
     └─────────┘        └─────────┘        └─────────┘

   ── STATE 1: web-1 is RESCHEDULED to a different node ──────────

     node-a              node-c              node-b
     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │  web-0  │        │  web-1  │◀── moved from node-b
     └────┬────┘        └────┬────┘        └────┬────┘
          │                  │  the claim line   │
          ▼                  ▼  FOLLOWS the Pod  ▼
     [www-web-0]        [www-web-1]        [www-web-2]

   ── STATE 2: web-1 is DELETED ──────────────────────────────────

     ┌─────────┐             ✕             ┌─────────┐
     │  web-0  │        (Pod gone)         │  web-2  │
     └────┬────┘             ╎             └────┬────┘
          │                  ╎                  │
          ▼                  ▼                  ▼
     [www-web-0]        [www-web-1]        [www-web-2]
                        ↑ THE CLAIM REMAINS.
                          Nothing cleans it up.
```
-->

### The reschedule, which is the under-weighted half

Chapter 10 promised you two things about per-replica claims: that they outlive the Pod, and that they outlive *the rescheduling*. Most readers weight the first and skim the second. The second is the more interesting one.

A StatefulSet's Pod keeps the same PersistentVolumeClaim for the whole of its lifecycle, and when that Pod is rescheduled onto a different node, its `volumeMounts` mount that same claim wherever it lands [source: k8s-docs-statefulset-2026-08-24].

<!-- AUTHOR-REVIEW: the 2026-08-25 capture of the StatefulSet "Stable Storage" section flags the 08-24 wording of these two sentences as differing load-bearingly (PersistentVolumes vs PersistentVolumeClaims) and records itself as the verifiable version. The substance is stated here in the book's own words rather than quoted, and the verified 08-25 statement of the same behavior is quoted in the Closer Look below. -->

Note what that does *not* say. It does not say the storage moves. It does not say the data is copied. It says the mount happens wherever the Pod lands, because the Pod's storage is attached to *the claim*, and the claim is not attached to a node at all. The claim is a namespaced API object with no node in it, lashed to no particular deck. The volume behind it is cluster-scoped. Neither one cares which machine `web-1` is running on today.

That is why a StatefulSet can survive a node failure with its data intact [source: k8s-docs-statefulset-storage-2026-08-25], and stating it explicitly explains something otherwise mysterious: the identity you learned in Chapter 6 is not just a naming convention. `web-1` is a name that carries a claim with it. Reschedule the Pod and the claim comes along, because the claim was never anywhere else.

> ⚓ **Worth Securing:** This also explains the constraint you may have wondered about back in Chapter 6: why StatefulSets recreate a Pod with the *same* ordinal rather than just adding a new one. A Deployment's replacement Pod is a new Pod with a new name and no history. A StatefulSet's replacement for `web-1` must be *named* `web-1`, because the name is how it finds `www-web-1`. Identity and storage are one mechanism seen from two sides.

### The claims survive the workload

Now the part that costs people real money.

> ★ **Fixed Point**
>
> **A StatefulSet's PersistentVolumeClaims are not deleted when the Pod is deleted, or when the StatefulSet is deleted. This must be done manually.**
>
> The claims are governed by a retention policy, and that policy's default is to keep them: *Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted* [source: k8s-docs-statefulset-storage-2026-08-25], and *the default for policies is Retain* [source: k8s-docs-statefulset-storage-2026-08-25].
>
> The volumes behind those claims persist alongside them: *the PersistentVolumes associated with the Pods' PersistentVolume Claims are not deleted when the Pods, or StatefulSet are deleted. This must be done manually* [source: k8s-docs-statefulset-storage-2026-08-25]. Read that second sentence carefully and notice which object it is about — the PersistentVolumes, not the claims. Both survive, for different reasons stated in different places. The claims are the ones you will find still sitting in the namespace afterward.
>
> `kubectl delete statefulset web` removes the workload and leaves `www-web-0`, `www-web-1`, and `www-web-2` sitting in the namespace, bound, billing, and invisible to anyone who thinks deleting a workload cleans up after itself.

The reason is stated as a deliberate choice rather than an oversight: *deleting and/or scaling a StatefulSet down will not delete the volumes associated with the StatefulSet. This is done to ensure data safety, which is generally more valuable than an automatic purge of all related StatefulSet resources* [source: k8s-docs-statefulset-2026-08-24].

Read that as a judgment call, because that is what it is. Kubernetes chose the failure mode where the hold stays full of cargo nobody remembers loading over the failure mode where one command puts a database over the side. Given the two, it chose correctly. But it means the cleanup is yours, and nobody will remind you.

> 🔭 **Closer Look: the retention policy field**
>
> That default is configurable. *The optional `.spec.persistentVolumeClaimRetentionPolicy` field controls if and how PVCs are deleted during the lifecycle of a StatefulSet* [source: k8s-docs-statefulset-storage-2026-08-25], with two independently settable policies: `whenDeleted`, which *configures the volume retention behavior that applies when the StatefulSet is deleted*, and `whenScaled`, which *configures the volume retention behavior that applies when the replica count of the StatefulSet is reduced* [source: k8s-docs-statefulset-storage-2026-08-25]. Each takes `Delete` or `Retain`, and `Retain` is the default for both [source: k8s-docs-statefulset-storage-2026-08-25].
>
> One boundary to know: these policies apply only to *voluntary* removal. *If a Pod associated with a StatefulSet fails due to node failure, and the control plane creates a replacement Pod, the StatefulSet retains the existing PVC. The existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch* [source: k8s-docs-statefulset-storage-2026-08-25]. A node dying is not a scale-down. Your data does not get cleaned up because a machine crashed.
>
> <!-- AUTHOR-REVIEW: the retrieval for k8s-docs-statefulset-storage-2026-08-25 also returned a sentence about a StatefulSetAutoDeletePVC feature gate whose current stability stage could not be confirmed. Deliberately omitted rather than stated with a possibly-stale stage. The Retain default is the safe claim and is what is stated above. -->

> 🪝 **Snag:** There is a mechanism elsewhere in this chapter that does the *opposite*, and the contrast is worth holding. A **generic ephemeral volume** also creates a PVC per Pod, and *when the Pod is deleted, the Kubernetes garbage collector deletes the PVC, which then usually triggers deletion of the volume because the default reclaim policy of storage classes is to delete volumes* [source: k8s-docs-ephemeral-volumes-2026-08-25]. Two mechanisms, both creating one claim per Pod, with exactly opposite deletion behavior. The difference is intent: an ephemeral volume is scratch space that happens to be provisioned like real storage, and a StatefulSet's claim is real storage that happens to be created by a controller.

---

## ☆ Taking Your Bearings #2 — Persistent Volumes, Reclaim Policy, and the CSI/StatefulSet Pairing

Eight questions on §3 through §6: access modes, reclaim policy, CSI, and the StatefulSet storage pairing. Two of them reach back into earlier chapters.

**1.** A PersistentVolume is bound with access mode `ReadWriteOnce`. Three Pods are scheduled: `pod-a` and `pod-b` on node-1, and `pod-c` on node-2. All three reference the same PVC. Which Pods can mount the volume read-write?

A) Only `pod-a` — RWO means exactly one Pod
B) `pod-a` and `pod-b` — RWO permits multiple Pods on the same node
C) All three — RWO restricts writes but not mounts
D) None — RWO is invalid for multi-Pod configurations and the PVC will fail to bind

**2.** A team's cluster has a single StorageClass marked default, whose manifest specifies no `reclaimPolicy`. A developer creates a PVC with no `storageClassName`, gets a bound 50Gi volume, runs a database on it for six months, then deletes the PVC while decommissioning the namespace. What happens to the data, and where was that decided?

A) Data is retained; decided by the PVC, which defaults to `Retain`
B) Data is retained; decided by the PersistentVolume, since manually created PVs default to `Retain`
C) Data is destroyed; decided by the StorageClass, whose unspecified `reclaimPolicy` defaults to `Delete` and is inherited by the dynamically provisioned volume
D) Data is destroyed; decided at deletion time by the user, since deleting a PVC always deletes its backing storage

**3.** *[retrieval: ch7]* A StorageClass sets `volumeBindingMode: WaitForFirstConsumer`. A developer creates a PVC using that class, then creates a Pod that references it. The Pod requests 64Gi of memory and no node in the cluster has that much allocatable. What is the state of the PVC and the Pod?

A) PVC `Bound`, Pod `Pending` — the volume provisions immediately and the Pod waits for a node
B) PVC `Pending`, Pod `Pending` — binding waits for the scheduler to pick a node, and the scheduler never does
C) PVC `Bound`, Pod `Pending` — the volume provisions in the zone with the most free capacity, and the Pod waits for a node there
D) PVC `Failed`, Pod `Failed` — a claim that cannot be satisfied is marked failed, and a Pod whose volume failed is marked failed with it

**4.** An administrator wants to be certain that a PVC's data survives when the PVC is deleted, and that the storage can be handed to a different application afterward with the old data cleaned off. The volume was dynamically provisioned from a class with `reclaimPolicy: Retain`. Which sequence is correct after the PVC is deleted?

A) The PV returns to `Available` and the next matching claim binds to it, inheriting the previous data
B) The PV becomes `Released`; the admin deletes the PV, cleans the storage asset, deletes the asset, and creates a new PV if the asset is to be reused
C) The PV becomes `Released` and Kubernetes scrubs it automatically before returning it to `Available`
D) The PV becomes `Failed` because `Retain` cannot complete automatic reclamation

**5.** Which statement most accurately describes what CSI is?

A) A storage system maintained by the CNCF that Kubernetes clusters can deploy for persistent volumes
B) A standard interface allowing storage vendors to write one plugin that works across container orchestration systems, without editing core Kubernetes code
C) A Kubernetes-internal API used by the kubelet to mount volumes, not exposed to external vendors
D) The successor to StorageClass, replacing dynamic provisioning with vendor-managed volumes

**6.** *[retrieval: ch6]* You run `kubectl get statefulset` in a namespace and get "No resources found." You then run `kubectl get pvc` in the same namespace and see `www-web-0`, `www-web-1`, and `www-web-2`, all `Bound`. What is the most likely explanation, and what does it tell you about identity and storage?

A) The claims are orphaned by a bug; StatefulSet deletion is supposed to remove them
B) A StatefulSet named `web` was deleted; its per-replica PVCs survive by design and must be removed manually
C) The claims belong to a Deployment, since Deployments also generate per-replica claims
D) The StatefulSet is in a different namespace; PVCs are cluster-scoped and appear everywhere

**7.** A StatefulSet has three replicas and one `volumeClaimTemplate`. `web-1` is running on `node-b`. `node-b` fails and the control plane schedules the replacement `web-1` onto `node-e`. What happens to `web-1`'s storage?

A) A new PVC is created for the replacement Pod on `node-e`, and the old data is lost with the failed node
B) The existing PVC is retained, and the cluster attaches the existing volume to the node where the new Pod launches
C) The data is copied from `node-b` to `node-e` by the StatefulSet controller before the Pod starts
D) The Pod cannot be rescheduled, because a StatefulSet's storage is pinned to its original node

**8.** A StatefulSet named `cache` declares three replicas and two entries in `volumeClaimTemplates`, named `data` and `wal`. Once all three Pods are running, how many PersistentVolumeClaims exist in the namespace, and what are they named?

A) Three — `cache-0`, `cache-1`, and `cache-2`; each Pod receives one claim regardless of how many templates the set declares
B) Six — `data-cache-0` through `data-cache-2`, and `wal-cache-0` through `wal-cache-2`
C) Two — `data-cache` and `wal-cache`; each template produces one claim, which all three Pods mount
D) Six — `cache-data-0` through `cache-data-2`, and `cache-wal-0` through `cache-wal-2`

---

**Answers with Explanations:**

**1 — B.** *ReadWriteOnce still permits multiple Pods to access the volume when those Pods run on the same node* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. `pod-a` and `pod-b` share node-1; `pod-c`, on node-2, cannot join them — RWO tests are about counting nodes, not counting Pods.
- **A** confuses RWO with `ReadWriteOncePod`, the mode that actually limits access to one Pod.
- **C** ignores that "Once" is a real node constraint — `pod-c` is blocked.
- **D** is wrong outright: RWO is valid and common; nothing about it blocks binding.

**2 — C.** No `storageClassName` → the default class applies → that class specifies no `reclaimPolicy` → *unspecified `reclaimPolicy` defaults to `Delete`* [source: k8s-docs-storage-classes-2026-08-25] → *dynamically provisioned volumes inherit the reclaim policy of their StorageClass* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Deleting the claim destroys the PV and its backing asset.
- **A** is wrong: a PVC carries no reclaim policy of its own.
- **B** is wrong for a subtle reason: `Retain` genuinely is the default for *manually created* PVs [source: k8s-api-ref-persistentvolume-v1-2026-08-25]. Choosing B means you knew a real fact and applied it to the wrong provisioning path.
- **D** is wrong: destruction follows the policy, not a blanket rule about deletion. Getting the outcome right for the wrong reason is still wrong, and the exam will offer you that option.

**3 — B.** `WaitForFirstConsumer` *delays binding and provisioning until a Pod using the claim exists*, then provisions *conforming to the topology the Pod's scheduling constraints specify* [source: k8s-docs-storage-classes-2026-08-25]. No node satisfies the Pod's memory request, so the scheduler never picks one *[cross-bearing: see Ch 7 §2 — what makes a node feasible]*, so binding never proceeds. Both objects sit `Pending`.
- **A** describes `Immediate` mode — the behavior this mode exists to avoid.
- **C** is the most reasonable of the three wrong answers, since it assumes the provisioner falls back to some sensible policy — free capacity, spare headroom, whichever zone looks emptiest. It does not; the *Pod's* constraints are the only input, and there are none yet.
- **D** confuses `Failed`, a PV phase for unsuccessful automatic reclamation, with an unscheduled Pod waiting in `Pending`.

**4 — B.** `Retain` means the volume and its data survive claim deletion, but survival is not reuse. The PV moves to `Released`, and a `Released` volume is not yet available to another claim because the previous claimant's data remains on it [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Reclaiming it is manual: delete the PV, clean the storage asset by hand, delete the asset, and provision a new PV if it's to be reused. The two manual deletions plus a fresh PV are the price of the guarantee — nothing is thrown away without a human choosing that, and nothing is handed to the next tenant without a human clearing it first.
- **A** describes `Delete` or an automatic rebind — not what `Retain` does.
- **C** invents automatic scrubbing. Nothing scrubs a `Retain` volume; declining to do so is the entire point of choosing it.
- **D** is wrong: `Retain` has no automatic reclamation to fail at. It isn't attempting one.

**5 — B.** The spec's own objective: *"enable storage vendors to develop a plugin once and have it work across a number of container orchestration systems"* [source: csi-spec-objective-2026-08-25]; vendors add storage systems *without editing core Kubernetes code* [source: k8s-docs-volumes-2026-08-23].
- **A** treats an interface as a product. There is no "CSI storage," only CSI *drivers*, one per vendor.
- **C** inverts the design: CSI is explicitly out-of-tree and vendor-facing.
- **D** is wrong: CSI and StorageClass are complementary — a StorageClass names a provisioner, and a CSI driver is often what that provisioner is.

**6 — B.** A StatefulSet's `persistentVolumeClaimRetentionPolicy` defaults both `whenDeleted` and `whenScaled` to `Retain` [source: k8s-docs-statefulset-storage-2026-08-25]. Deleting `web` left its claims in place; the PVs behind them survive too, and removing them is manual. The naming, `<template>-<statefulset>-<ordinal>`, confirms a set called `web` with a template called `www`. The lesson: the claim is attached to the *name*, not the workload object — the same shape as the reclaim-policy surprises earlier in this checkpoint, decided by someone who is not in the room when the object is deleted.
- **A** is wrong: this is deliberate, since *data safety is generally more valuable than an automatic purge* [source: k8s-docs-statefulset-2026-08-24].
- **C** is wrong: Deployments have no `volumeClaimTemplates`; replicas share whatever claim the PodSpec names.
- **D** is wrong twice: PVCs are namespaced, not cluster-scoped *[cross-bearing: see Ch 4 §3 — where a name lives]*, and the query ran in the right namespace.

**7 — B.** *If a Pod fails due to node failure and the control plane creates a replacement, the StatefulSet retains the existing PVC; the volume is unaffected and the cluster attaches it to the node where the new Pod launches* [source: k8s-docs-statefulset-storage-2026-08-25]. Storage in Kubernetes is attached at the cluster level and mounted where needed; it does not live on a node the way local disk does.
- **A** is wrong: the replacement reuses `www-web-1` — the point of stable identity.
- **C** is wrong: nothing is copied; the volume was never "on" node-b in the sense this implies.
- **D** inverts the mechanism: the claim's independence from any node is what permits the reschedule.

**8 — B.** *For each `volumeClaimTemplates` entry, each Pod receives one PersistentVolumeClaim* [source: k8s-docs-statefulset-storage-2026-08-25]. Three Pods against two templates is six claims, named `<template>-<statefulset>-<ordinal>` — template first.
- **A** drops the "per template" clause from the rule.
- **C** is Deployment-shaped thinking: a single shared claim is what a PodSpec-named PVC gives a Deployment's replicas — exactly what `volumeClaimTemplates` exists to avoid *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*.
- **D** gets the count and components right and the order wrong — `cache-data-0` matches nothing that exists, and it is the trap most likely to survive a quick glance, since every piece of it is individually correct.

---

**Checkpoint: You've Now Mastered**
✓ Access modes as node-count semantics, and RWOP as the one exception
✓ The three reclaim policies, including which one is retired
✓ That dynamically provisioned volumes inherit `Delete` by default, from the class
✓ That `Released` requires three manual steps and a new PV object to become reusable
✓ Chapter 6's five deferred verbs, all five closed
✓ CSI as the fourth pluggable interface, and as a cross-orchestrator standard rather than a Kubernetes feature
✓ What a CSI driver is — a Deployment plus a DaemonSet, written by somebody outside the project
✓ `volumeClaimTemplates`, the one-claim-per-Pod-per-template rule, and the `<template>-<set>-<ordinal>` name it produces
✓ Why a StatefulSet's storage follows a reschedule, and why identity is the mechanism that makes it possible
✓ That the claims outlive the workload, deliberately, and that cleanup is yours

## ☀️ §7 — Outliving the Pod That Asked

Look back at what you did in this chapter, and notice that you only ever asked one question.

*Does the file survive the container restart?* *Does the volume survive the Pod?* *Does the claim survive the workload?* *Does the data survive the claim?* Four questions, one shape: **what survives what?** Every section widened the scope by exactly one step, and the ladder in §1 was the whole chapter drawn small.

Here is what makes it worth the walk. At every rung, the thing that would seem to have the most at stake in the answer is not the thing that decides it.

The container does not decide whether its files survive a restart. The image layout decided that, before the container existed. The Pod does not decide whether its volume survives deletion; the volume's *type* decided it, chosen in a manifest by whoever wrote the PodSpec. And the claim does not decide whether the data survives the claim's deletion. The StorageClass decided that, in a `reclaimPolicy` field, in a manifest written by an administrator who was configuring a cluster and had never heard of your application.

The workload never gets a vote. That is not a defect. It is the same separation that runs through everything you have learned:

A Pod does not decide which node it lands on; the scheduler does, by filtering and scoring *[cross-bearing: see Ch 7 §1 — one decision, made once]*. A Deployment does not decide how many replicas exist right now; a control loop does, reconciling toward the number in the spec *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*. And an object does not decide whether anything happens to it; the component that watches for it does, if somebody installed one *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*.

Storage is that pattern applied to durability. And the reason for naming it is practical rather than aesthetic: it is why a developer can be handed a cluster they have never seen and be productive on it the same afternoon. They write a claim. Somebody else — possibly years ago, possibly a vendor they will never meet, possibly a CSI driver running as a DaemonSet on nodes they will never log into — arranged for that claim to be satisfiable. The developer does not need to know how. That ignorance is not a gap in their knowledge. It is the interface working.

Go back to the epigraph. *The cargo does not belong to the crew. It was aboard before this watch, and it will be aboard after.* Watches change. What sits below the waterline is not consulted about the handover, and that is exactly why the handover works: a ship that renegotiated its cargo at every change of watch would not be carrying anything, it would be holding a meeting. The Pod is a watch. The claim is the entry in the papers. What becomes of the cargo when the papers are torn up was settled in a `reclaimPolicy` field, long before this watch came aboard.

> ☀️ **Zenith:** Chapter 4 taught you that a Kubernetes object is a record of intent, and that the record outlives the thing that acts on it *[cross-bearing: see Ch 4 §1 — you file a declaration]*. That is the same sentence as this chapter's title.
>
> The claim is a record of intent about storage. It outlives the Pod that asked for it, because it was never the Pod's to begin with. It was filed on the Pod's behalf, against a supply the Pod knows nothing about, under terms settled before the Pod was scheduled. **Storage outlives the Pod that asked for it**, not because storage is special, but because *records of intent outlive the things that act on them*, and a claim is a record of intent.
>
> Ten chapters of Kubernetes, and it is one idea wearing different clothes.

<!-- FIGURE: ch11-zenith-outliving-the-pod -->
![A two-lane timeline: the upper Pod lane shows three separate segments each labelled web-1, on node-b then node-e then node-e, with visible gaps between them; the lower Storage lane is a single unbroken line labelled www-web-1 running the full width, with claim connectors dropping from each Pod segment to the storage line](figures/ch11-zenith-outliving-the-pod.svg)

<!-- ASCII-FALLBACK
```
   Pod    ├──web-1──┤        ├──web-1──┤    ├──web-1──┤
           (node-b)           (node-e)       (node-e)
              ╎                  ╎              ╎
              ╎ claims           ╎ claims       ╎ claims
              ▼                  ▼              ▼
 Storage ═══════════════════════════════════════════════════▶
          www-web-1 — one continuous line, never broken

                    time ──────────────────────────────────▶
```
-->

---

## Exam Alert! 🚨

**High-Priority Topics:**

1. **PersistentVolume vs PersistentVolumeClaim vs StorageClass.** CNCF publishes the Storage competency as a single word under Container Orchestration. This book's reading of it puts the three-way PV/PVC/StorageClass distinction at the center, which is why it leads this list. Know: PV is supply and cluster-scoped; PVC is demand and namespaced; StorageClass describes *classes* of storage and enables dynamic provisioning. And know that a Pod references the claim [source: k8s-docs-persistent-volumes-2026-08-23].

2. **Access modes, and what unit each counts.** RWO, ROX, RWX count **nodes**. RWOP counts **Pods** [source: k8s-docs-persistent-volumes-depth-2026-08-25]. If you memorize one sentence from this chapter, make it that one.

3. **Reclaim policy, and where the decision was made.** Retain / Delete / Recycle(deprecated). Dynamically provisioned volumes inherit the class's policy, which defaults to `Delete` [source: k8s-docs-persistent-volumes-depth-2026-08-25]; manually created PVs default to `Retain` [source: k8s-api-ref-persistentvolume-v1-2026-08-25].

4. **Static vs dynamic provisioning, and the two conditions dynamic requires.** The claim must request a class **and** the administrator must have created and configured that class for provisioning [source: k8s-docs-persistent-volumes-2026-08-23].

**Common Traps** — these are documented targets in this book's domain analysis, not merely things that are easy to confuse:

| Trap | Correction |
|---|---|
| "A PVC binds to any PV that's big enough" | Binding is exclusive and one-to-one, and an unmatched claim stays unbound **indefinitely** [source: k8s-docs-persistent-volumes-2026-08-23] |
| Reversing PV and PVC | PV is supply, PVC is demand, Pods reference **claims** [source: k8s-docs-persistent-volumes-2026-08-23] |
| "ReadWriteOnce means one Pod" | It means one **node**; multiple Pods on that node may share it. RWOP is the one-Pod mode [source: k8s-docs-persistent-volumes-depth-2026-08-25] |
| "Deleting a PVC always keeps the data" | Dynamic volumes inherit the class's policy, defaulting to **Delete** [source: k8s-docs-persistent-volumes-depth-2026-08-25] |
| "Retain means the PV is immediately reusable" | It becomes `Released`, not `Available`; manual reclamation takes three steps and a new PV object [source: k8s-docs-persistent-volumes-depth-2026-08-25] |
| Expecting `Recycle` to be live | Deprecated; use dynamic provisioning [source: k8s-docs-persistent-volumes-depth-2026-08-25] |
| "Class `\"\"` uses the default class" | It **disables dynamic provisioning** for that claim [source: k8s-docs-persistent-volumes-2026-08-23] |

**Two more that are worth knowing** — both are sourced facts and both are common mistakes, though they have not been assessed for exam frequency the way the seven above have:

- **`emptyDir` survives container crashes but not Pod removal.** *A container crashing does not remove a Pod from a node*, so the data is safe across crashes, but *when a Pod is removed from a node for any reason, the data in the `emptyDir` is deleted permanently* [source: k8s-docs-volume-types-depth-2026-08-25].
- **A StatefulSet's PVCs survive deletion of the Pod and of the StatefulSet**, and must be deleted manually. The retention policy that governs this defaults to `Retain`, which leaves PVCs created from a `volumeClaimTemplate` unaffected when their Pod is deleted [source: k8s-docs-statefulset-storage-2026-08-25].

---

## Practice Questions

Seventeen questions, interleaved rather than grouped by section.

<!-- AUTHOR-REVIEW: Two deliberate deviations from the outline's practice allocation, both recorded per the question-quality audit. (1) §2 receives 3 items rather than the outline's 4. Q13 was recast from a near-duplicate of Bearings #2 Q5 into a §2 binding-filters item; no further §1 item was converted, because each remaining §1 item pays a specific debt (Q5 the chapter-04:762 subPath promise, Q9 the Ch 12 §5 plant, Q17 the generic-ephemeral/StatefulSet discrimination). (2) The recommended Ch 5 projected-volume retrieval item was applied as a conversion of Q1 rather than as an eighteenth question, to hold the outline's question_budget of 17 exactly. Q1's former emptyDir/Secret lifetime content remains tested at Bearings #1 Q1-Q2 and Practice Q14. -->

**1.** *[retrieval: ch5]* In Chapter 5, a Pod's ServiceAccount token arrived inside the container's filesystem without any `configMap` or `secret` volume being declared. Which volume type delivered it, and what else can that type carry?

A) A `secret` volume; it can carry Secret data and nothing else
B) A `projected` volume; it maps several existing volume sources — among them `secret`, `configMap`, `downwardAPI`, and `serviceAccountToken` — into a single directory
C) A `hostPath` volume mounting the node's kubelet credentials directory
D) A `generic ephemeral` volume provisioned by the ServiceAccount controller

**2.** Which object does an application developer write in order to obtain persistent storage, on a cluster where they have no administrative access?

A) A PersistentVolume, specifying the backing storage system
B) A StorageClass, specifying a provisioner
C) A PersistentVolumeClaim, specifying a size and access mode
D) A CSIDriver, specifying the vendor's driver name

**3.** A cluster has a working default StorageClass with `reclaimPolicy` unspecified. A PVC is created without a `storageClassName`, binds successfully, and is later deleted. What happens to the PV and the backing storage asset?

A) Both are retained; the PV becomes `Released`
B) Both are deleted, because the class defaults to `Delete` and the volume inherited it
C) The PV is deleted but the backing asset is retained
D) The PV becomes `Available` and the asset is scrubbed

**4.** *[retrieval: ch4]* Chapter 4 named three cluster-scoped resources, two of which this chapter has now given you a reason for. Which set is correct?

A) Node, PersistentVolume, PersistentVolumeClaim
B) Node, PersistentVolume, StorageClass
C) PersistentVolume, PersistentVolumeClaim, StorageClass
D) Namespace, PersistentVolume, PersistentVolumeClaim

**5.** A ConfigMap named `app-config` is mounted into a container using `subPath: settings.yaml`. An operator updates the ConfigMap with `kubectl apply`. What does the running container see?

A) The updated content, after the kubelet's sync period
B) The updated content immediately, since ConfigMap volumes are watched
C) The original content — a `subPath` mount does not receive updates
D) An error, since ConfigMaps mounted with `subPath` become invalid on update

**6.** Which of the following is required for dynamic provisioning to occur when a PVC is created?

A) The PVC must request a storage class, and the administrator must have created and configured that class for provisioning
B) A matching PersistentVolume must already exist in the `Available` phase
C) The PVC must specify `volumeName` naming the PV to be created
D) The cluster must have exactly one StorageClass marked default, so that the provisioner is unambiguous

**7.** An `nfs` volume is used by three Pods spread across three different nodes, all writing to it. Which access mode does this arrangement require the PersistentVolume to support?

A) `ReadWriteOnce`
B) `ReadOnlyMany`
C) `ReadWriteMany`
D) `ReadWriteOncePod`

**8.** *[retrieval: ch10]* A cluster administrator creates a StorageClass whose `provisioner` field references a CSI driver that has not been installed. Which previously-named pattern does this instantiate, and what will a claim requesting that class do?

A) The absent-component pattern — "an object without its component does nothing"; the claim remains unbound
B) The eventual-consistency pattern; the claim binds after a reconciliation delay
C) The admission-rejection pattern; the StorageClass is rejected at creation
D) The default-fallback pattern; the claim falls back to the default StorageClass

**9.** Which statement about `hostPath` volumes is accurate?

A) They are the recommended way to provide node-local durable storage, superseding `local` volumes
B) They present many security risks, and should be avoided where possible — a `local` PersistentVolume is the suggested alternative
C) They are automatically read-only, which mitigates the security concern
D) They provide the same node-affinity awareness as `local` volumes

**10.** A StatefulSet named `db` has two replicas and one `volumeClaimTemplate` named `data`. What PersistentVolumeClaims exist once both Pods are running, and what happens to them if the StatefulSet is deleted?

A) One claim, `data-db`, shared by both Pods; deleted with the StatefulSet
B) Two claims, `data-db-0` and `data-db-1`; both deleted with the StatefulSet
C) Two claims, `data-db-0` and `data-db-1`; both survive and must be deleted manually
D) Two claims, `data-db-0` and `data-db-1`; both are garbage-collected when their Pods are deleted

**11.** A PersistentVolume supports both `ReadWriteOnce` and `ReadOnlyMany`. Can it be mounted read-write on node-1 and read-only on node-1 at the same time?

A) Yes — a PV may use all of its supported access modes concurrently
B) No — a volume can only be mounted using one access mode at a time
C) Yes, but only if the two mounts are in different namespaces
D) No — supporting two access modes is invalid and the PV will be rejected

**12.** *[retrieval: ch2]* CSI, CRI, CNI, and CRDs are described in this book as the four pluggable interfaces. What do all four have in common?

A) All four are implemented by DaemonSets running on every node
B) All four are cluster-scoped API objects
C) All four publish a contract that lets someone outside the Kubernetes project supply an implementation without editing core Kubernetes code
D) All four were introduced in the same Kubernetes release and are versioned together

**13.** `kubectl get pv` shows exactly one PersistentVolume on a cluster: 100Gi, phase `Available`, `storageClassName: fast`, carrying the label `tier=production`. A user then creates a 10Gi PersistentVolumeClaim requesting `storageClassName: fast` with a selector of `matchLabels: {tier: staging}`. What happens?

A) It binds — the PV satisfies both the capacity request and the class request
B) It binds — label selectors filter Pods onto nodes, not claims onto volumes
C) It remains unbound — a selector on a claim is an additional requirement, and every requirement must be satisfied
D) It binds, and the PV's `tier` label is updated to `staging` to reflect its new claimant

**14.** An `emptyDir` volume is configured with `medium: Memory`. A container writes 2GiB of data into it. The container has a memory limit of 1GiB and is currently using 200MiB of heap. What happens?

A) Nothing — tmpfs usage is accounted to the node, not the container
B) The write fails with ENOSPC once the node's RAM is exhausted
C) The container is OOM-killed, because files written to a memory-backed `emptyDir` count against the writing container's memory limit
D) The volume automatically spills to disk when the memory limit is approached

**15.** After a PVC bound to a `Retain`-policy PV is deleted, which sequence returns the underlying storage asset to service for a *different* application, with the old data removed?

A) Wait for the PV to return to `Available`, then bind a new claim to it
B) Delete the PV, manually clean the storage asset, manually delete the asset, and create a new PV if reusing the same asset definition
C) Patch the PV's `claimRef` to null, which returns it to `Available` with data intact
D) Set the PV's reclaim policy to `Recycle`, which scrubs and republishes it

**16.** A StatefulSet Pod named `cache-2` is running on `node-x` with claim `store-cache-2`. `node-x` is cordoned and drained. What is true of the replacement Pod?

A) It will be named `cache-3` and will receive a newly provisioned claim
B) It will be named `cache-2` and will mount `store-cache-2` on whichever node it is scheduled to
C) It cannot be scheduled elsewhere, since its storage is bound to `node-x`
D) It will be named `cache-2` but will start with an empty volume until the data is replicated

**17.** Which statement about generic ephemeral volumes is correct?

A) They are identical to `emptyDir` in every respect except that they can be network-attached
B) They cause a real PersistentVolumeClaim to be created in the Pod's namespace, which is deleted when the Pod is deleted
C) They cannot be provisioned by CSI drivers, only by in-tree plugins
D) Their PVCs survive Pod deletion and must be cleaned up manually, like a StatefulSet's

---

**Answers with Explanations:**

**1 — B.** A projected volume maps several existing volume sources into the same directory [source: k8s-docs-projected-volumes-2026-08-25], and `serviceAccountToken` is one of those sources. That is how a token reaches a container whose PodSpec declares no Secret at all — the mechanism you met in Chapter 5 as a special case is the general one *[cross-bearing: see Ch 5 §6 — a Pod's identity]*.
- **A** names a real volume type with the wrong reach. A `secret` volume carries Secret data — and carries it on tmpfs, so it is *never written to non-volatile storage* [source: k8s-docs-volume-types-depth-2026-08-25] — but it composes nothing, and the Pod in the question declared no Secret to compose from. **C** is this chapter's hazard wearing a plausible costume: a Pod reading the node's kubelet credentials directory is precisely the escape the `hostPath` warning exists to prevent [source: k8s-docs-volume-types-depth-2026-08-25], and it is not how any token is delivered. **D** invents a provisioner. A generic ephemeral volume is requested in the PodSpec and satisfied by a storage driver; the ServiceAccount controller issues no volumes.

**2 — C.** *A PersistentVolumeClaim (PVC) is a request for storage by a user* [source: k8s-docs-persistent-volumes-2026-08-23], specifying size and access mode while *details of the storage itself are described in the PersistentVolume object* [source: k8s-glossary-storage-terms-2026-08-25].
- **A** is the administrator's object and is cluster-scoped. **B** is also the administrator's, and requires knowing a provisioner. **D** describes a driver installation, not a storage request.

**3 — B.** *If no `reclaimPolicy` is specified when a StorageClass object is created, it will default to `Delete`* [source: k8s-docs-storage-classes-2026-08-25], and *volumes that were dynamically provisioned inherit the reclaim policy of their StorageClass* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. `Delete` *removes both the PersistentVolume object from Kubernetes, as well as the associated storage asset* [source: k8s-docs-persistent-volumes-depth-2026-08-25].
- **A** describes `Retain`, which is the manual-creation default, not the dynamic one. **C** splits the two deletions, which `Delete` does not do. **D** describes `Recycle`, deprecated.

**4 — B.** Chapter 4 named PersistentVolume as a canonical cluster-scoped resource; claims are namespaced, and *claims must exist in the same namespace as the Pod using the claim* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. The reason is the supply/demand split: supply belongs to the cluster, demand belongs to a team.
- **A** is wrong on the PersistentVolume. A PV is a cluster resource in the same sense a node is a cluster resource — it belongs to no namespace because it belongs to no team, and it was very likely created before the namespace that will consume it existed.
- **C** is wrong on the PersistentVolumeClaim, and it is the most reasonable wrong answer here: having correctly placed the PV at cluster scope, it assumes the claim follows its supply. It does not. The claim is the tenant's half of the arrangement, and it lives where the tenant lives, in the same namespace as the Pod that mounts it.
- **D** is wrong on both halves; it inverts the relationship entirely, putting supply inside a namespace and demand outside every namespace.

**5 — C.** *A container using a ConfigMap as a `subPath` volume mount will not receive updates when the ConfigMap changes* [source: k8s-docs-volume-types-depth-2026-08-25].
- **A** and **B** describe whole-volume mount behavior, which is the rule this is the exception to. **D** invents a failure mode. Nothing errors; it simply does not update, which is worse, because it is silent.

**6 — A.** *The PVC must request a storage class and the administrator must have created and configured that class for dynamic provisioning to occur* [source: k8s-docs-persistent-volumes-2026-08-23]. Two conditions.
- **B** describes static provisioning; in fact dynamic provisioning is what happens when *no* matching PV exists. **C** invents a field usage; `volumeName` binds to an existing PV. **D** attaches the mechanism to the wrong thing. A default class decides what happens to a claim that names *no* class; it is not a precondition for provisioning. A claim that names `fast` provisions against `fast` whether or not any class is marked default — and *you can have a cluster without any default StorageClass* [source: k8s-docs-storage-classes-2026-08-25], on which every classless claim simply waits.

**7 — C.** *ReadWriteMany — the volume can be mounted as read-write by many nodes* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Three nodes, all writing.
- **A** would permit only one node. **B** would forbid the writes. **D** would permit only one Pod cluster-wide, which is even more restrictive than A.

**8 — A.** *To use a CSI driver from a storage provider, you must first deploy it to your cluster* [source: k8s-glossary-storage-terms-2026-08-25], and *the core of Kubernetes does not install that software for you* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. The claim stays unbound indefinitely.
- **B** is wrong because there is no retry that ends in a bind. *Claims will remain unbound indefinitely if a matching volume does not exist* [source: k8s-docs-persistent-volumes-2026-08-23] — the binder is a control loop, and a loop reconciling toward a volume that nothing will ever create converges on waiting. This is not a delay before success; it is the terminal state.
- **C** deserves an explicit rejection: the API server validates schema, not the existence of running components. A StorageClass naming a provisioner nobody deployed is a valid object.
- **D** is wrong because a claim that names a class does not fall back to another one. The default class applies only to a claim with *no* `storageClassName` field; naming a class is a commitment to that class, and there is nothing in the binding path that quietly substitutes a different one.

**9 — B.** *Using the `hostPath` volume type presents many security risks. If you can avoid using a `hostPath` volume, you should. For example, define a local PersistentVolume, and use that instead* [source: k8s-docs-volume-types-depth-2026-08-25].
- **A** inverts the recommendation. **C** is false; read-only must be *required* by admission-time validation to be effective [source: k8s-docs-volume-types-depth-2026-08-25]. **D** is the distinction that makes `local` preferable: *the system is aware of the volume's node constraints by looking at the node affinity on the PersistentVolume* [source: k8s-docs-volume-types-depth-2026-08-25], which `hostPath` does not provide.

**10 — C.** For each `volumeClaimTemplate` entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim [source: k8s-docs-statefulset-storage-2026-08-25] — hence two, named `data-db-0` and `data-db-1`. Their survival is governed by `persistentVolumeClaimRetentionPolicy`, whose `whenDeleted` and `whenScaled` fields both default to `Retain` [source: k8s-docs-statefulset-storage-2026-08-25]. Deleting the StatefulSet therefore leaves both claims standing, and removing them is a deliberate manual act.
- **A** describes a shared claim, which is what a Deployment referencing a single PVC would give you. **B** gets the naming right and the survival wrong, which is the more expensive half — a reader holding B will delete a StatefulSet expecting the storage to go with it, and be billed for volumes they believe are gone. **D** describes generic ephemeral volumes, not `volumeClaimTemplates`. The two mechanisms both produce one claim per Pod and differ precisely on deletion: the ephemeral-volume controller *ensures that the PersistentVolumeClaim gets deleted when the Pod gets deleted* [source: k8s-docs-ephemeral-volumes-2026-08-25], while a StatefulSet's claims are retained by default. Same shape, opposite ending.

**11 — B.** *A volume can only be mounted using one access mode at a time, even if it supports many. For example, a NFS volume can be mounted as ReadWriteOnce on one node and read-only on another node at the same time, but not on the same node for both read-write and read-only* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. The question's scenario is the documentation's exact counterexample.
- **A** ignores the "one at a time" constraint. **C** invents a namespace dimension. **D** is false; a PV listing several supported modes is entirely normal.

**12 — C.** Each of the four publishes a contract so an implementation can be supplied from outside. CSI states it directly — vendors can *introduce new storage systems into Kubernetes without ever having to edit the core Kubernetes code* [source: k8s-docs-volumes-2026-08-23] — and the extension-points documentation groups CSI, CNI, and CRI together as infrastructure extensions alongside CRDs as API extensions [source: k8s-docs-extending-kubernetes-2026-08-23]. Grouping these four as *the* four pluggable interfaces is this book's framing, not a Kubernetes ranking.
- **A** is true of some node components but not of CRDs or the CSI controller component. **B** is false; CRI is not an API object at all. **D** is fabricated; they arrived at different times and version independently.

**13 — C.** Capacity is one filter among several, not the whole test. A claim's `storageClassName` must match the volume's, and where a claim carries a `selector`, the volume must satisfy every requirement in it — `matchLabels` and `matchExpressions` are ANDed together, so a candidate volume has to clear all of them [source: k8s-docs-persistent-volumes-depth-2026-08-25]. The single PV here clears the size and clears the class, and fails on `tier`. That is enough. *Claims will remain unbound indefinitely if a matching volume does not exist* [source: k8s-docs-persistent-volumes-2026-08-23], and nothing in the cluster will report this as an error.
- **A** is the trap this question exists for: it treats "big enough, right class" as sufficient. It is necessary, not sufficient. **B** misplaces the mechanism. Label selectors are the book's universal join *[cross-bearing: see Ch 4 §5 — the universal join]*; they attach controllers to Pods, Services to endpoints, and — here — claims to volumes. **D** inverts the direction of the match. Binding selects a volume that already satisfies the claim; it never edits the volume to make it fit.

**14 — C.** *While tmpfs is very fast, be aware that, unlike disks, files you write count against the memory limit of the container that wrote them* [source: k8s-docs-volume-types-depth-2026-08-25]. 2GiB written into tmpfs plus 200MiB of heap, against a 1GiB limit, is an OOM kill *[cross-bearing: see Ch 5 §8 — what a Pod is owed]*.
- **A** is the misconception the documentation exists to correct. **B** describes what would happen with a `sizeLimit` on the default medium, not with a memory limit. **D** invents a spill mechanism.

**15 — B.** The documented steps: delete the PV, manually clean up the data on the associated storage asset, manually delete the asset. And *if you want to reuse the same storage asset, create a new PersistentVolume with the same storage asset definition* [source: k8s-docs-persistent-volumes-depth-2026-08-25].
- **A** never happens; `Released` does not become `Available` on its own [source: k8s-docs-persistent-volumes-depth-2026-08-25]. **C** describes an undocumented manual hack and, critically, leaves the old data in place, which the question explicitly required removing. **D** relies on a deprecated policy.

**16 — B.** A StatefulSet Pod keeps its ordinal identity across rescheduling *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*, so the replacement comes back as `cache-2`. Its claim is independent of any node: when the replacement is scheduled, its volume mounts follow the PersistentVolumeClaims associated with that ordinal, wherever the scheduler puts it [source: k8s-docs-statefulset-storage-2026-08-25]. Kubernetes documents the same behavior for the harsher, involuntary case — when a Pod is lost to node failure, *the existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch* [source: k8s-docs-statefulset-storage-2026-08-25]. A drain is the gentler version of the same story.
- **A** describes Deployment-style replacement, where replicas are interchangeable and names are regenerated. **C** inverts the mechanism; claim independence from nodes is what *enables* the reschedule. **D** invents replication that Kubernetes does not perform.

**17 — B.** *The ephemeral volume controller then creates an actual PersistentVolumeClaim object in the same namespace as the Pod and ensures that the PersistentVolumeClaim gets deleted when the Pod gets deleted* [source: k8s-docs-ephemeral-volumes-2026-08-25].
- **A** understates the differences: generic ephemeral volumes also support fixed size caps, snapshotting, cloning, and resizing where the driver supports them [source: k8s-docs-ephemeral-volumes-2026-08-25]. **C** is backwards; they *can* be provided by CSI drivers and by *any* driver supporting dynamic provisioning [source: k8s-docs-ephemeral-volumes-2026-08-25]. **D** describes StatefulSet behavior, which is the exact opposite of this mechanism and is the discrimination the question is testing.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **The lifetime ladder** | Three rungs, two boundaries. Container restart kills rung one. Pod deletion kills rung two. Nothing in a Pod's lifecycle reaches rung three. |
| **`emptyDir`** | Safe across container crashes, deleted permanently when the Pod is removed. `medium: Memory` makes it tmpfs and charges it to the writing container's memory limit. |
| **`hostPath`** | A powerful escape hatch with many security risks. Avoid it; prefer a `local` PersistentVolume. Makes Pods silently node-dependent. |
| **`subPath`** | Cuts the update wire. ConfigMap, Secret, and downwardAPI mounts via `subPath` do not receive updates. |
| **PersistentVolume** | Supply. Cluster-scoped. Created by an administrator or by a provisioner. Captures the real storage's implementation details. |
| **PersistentVolumeClaim** | Demand. Namespaced. Requests a size and an access mode. **A Pod references this, never the PV.** |
| **Binding** | A control loop match. Exclusive, one-to-one, and filtered on more than size — class, selector, and `volumeName` each narrow the field, and every requirement is ANDed. An unmatched claim stays unbound indefinitely: not an error, just silence. |
| **PV phases** | The concept documentation names four: `Available` → `Bound` → `Released` → (`Failed`). `Released` is not `Available`. The API reference documents a fifth, `Pending`; if you meet it on an answer sheet, recognize it rather than rule it out. |
| **StorageClass** | Describes classes of storage. Names a `provisioner`, carries opaque `parameters`, sets `reclaimPolicy`. The name is the interface. |
| **Dynamic provisioning** | Two conditions: the claim names a class **and** the class is configured to provision. One without the other waits forever. |
| **`storageClassName: ""`** | Opts *out* of dynamic provisioning. Not the same as omitting the field, which gets the default. |
| **Access modes** | RWO / ROX / RWX count **nodes**. RWOP counts **Pods**, and exists because people assume RWO already does. One mode at a time. |
| **Reclaim policies** | `Retain` (kept, released, manual three-step reclamation), `Delete` (PV object and backing asset both destroyed), `Recycle` (deprecated). |
| **The inherited default** | Dynamic volumes inherit the class's policy, defaulting to `Delete`. Manually created PVs default to `Retain`. |
| **CSI** | The fourth pluggable interface. A cross-orchestrator standard, not a Kubernetes feature. A driver is a Deployment plus a DaemonSet, and Kubernetes will not install it for you. |
| **`volumeClaimTemplates`** | One PVC per Pod, named `<template>-<set>-<ordinal>`. Follows the Pod across reschedules because it was never on a node. |
| **PVC survival** | A StatefulSet's claims outlive the Pod *and* the StatefulSet, by design. Cleanup is manual, and nobody will remind you. |

<!-- AUTHOR-REVIEW: The PV-phases row now hedges the four-vs-five count, per the fact-accuracy FAIL on §2 ("there are four" asserted against k8s-api-ref-persistentvolume-v1-2026-08-25, which enumerates five and carries its own SOURCE DISAGREEMENT marker) and curriculum-audit P3. That fix is scoped to §2 as a 🪝 Snag; the summary must not be the first place the reader meets `Pending`. If §2's hedge is not applied, either apply it or revert this row to the bare four-phase chain. -->

---

## The Voyage Ahead

You now hold all four pluggable interfaces, and with them a rule you can state without help: an object without its component does nothing. You have watched that rule fire at the Ingress controller, at the network plugin, at the provisioner, and at the CSI driver — four sightings, one light. Chapter 17 will collect all four interfaces in one place and ask you what they have in common; you already know.

But this chapter also left something exposed, and the next one is about it.

Twice in these pages, storage handed a workload something it should probably not have had. `hostPath` mounts the node's filesystem into a Pod, and the documentation's warning was not about disk space. It was about *privileged system credentials* and *container escape*. Secrets mount as files backed by tmpfs, never written to non-volatile storage, which is a security property so specific it can only exist because someone was worried about the alternative.

Both of those are the same question wearing different clothes: **what is a workload allowed to do, and who decided?** You have spent this chapter learning that storage decisions were made elsewhere, by someone else, before you arrived — reading the manifest, not holding the keys. Chapter 12 asks the harder version. Not *what happens to your data* but *who is allowed to touch it*, and it turns out that Kubernetes' answer has a shape you have already met twice in this chapter without noticing.

Here is the tell. Carry it with you: the permission system you are about to learn has no way to say *no*. None. There is no deny rule, anywhere in it. You have already seen one other Kubernetes system with exactly that property *[cross-bearing: see Ch 10 §6 — allowing, never denying]*, and by the end of the next chapter you will understand why two systems built for entirely different purposes arrived at the same design, and why that design is a feature rather than an omission.

Bring the `secret` volume with you. Chapter 12 §4 has an argument to make about file mounts versus environment variables, and you already hold half of it.

---

🏆 **Safe Harbor** — Domain 2's storage competency is complete. You can trace a file from the container filesystem out to a cluster-scoped volume and name what stops it at each boundary; you can distinguish a PersistentVolume from a claim from a class and say which one a Pod actually references; you can predict whether a claim binds, waits, or provisions; you can read an access mode as a node count; and you can say where the decision about your data's survival was actually made. Chapter 6's five deferred verbs are all settled, and the book's one deliberate forward reference is closed.

> *"The hold is inventoried by people who never sail. That is not a failure of the arrangement. That is the arrangement."*
