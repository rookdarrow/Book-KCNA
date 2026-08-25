I have everything I need: both binding contracts, the eight published cross-bearings into Ch 11 (two section-pinned), Ch 10's four explicit handoff promises, the cached sources, and B1's seven sourced storage traps. One collision surfaced — **shipped Ch 10 has already told the reader CSI is the *last* of the four pluggable interfaces, while B6 calls it "the third."**

---

```
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

# Chapter 11 Outline — Below the Waterline

## Chapter-type note (read first)

`chapter_type: content`. No contract exemptions apply. Drafting must deliver every required element:

| Required element | Strictness | Where it lands |
|---|---|---|
| `# Chapter 11: Below the Waterline` | required | top |
| `## *"Storage outlives the Pod that asked for it"*` | required | line 2 |
| Metadata line (domain / weight / complexity / novelty) | required | after subtitle — **conform to shipped ch-02/-05/-07/-08/-09/-10 house form**, carrying the published **28%** D2 weight with its CNCF source tag inline, plus the authored-allocation disclaimer for the 5% chapter figure |
| `## Attention Budget` | required | before epigraph |
| Epigraph blockquote | expected | after Attention Budget |
| `## 🧭 Soundings` | expected | after epigraph — **8 questions** (content baseline) |
| `## Why This Chapter Matters` | **required** | after Soundings |
| `## What You'll Learn` | expected | after Why-This-Chapter-Matters |
| `## ☆ Taking Your Bearings #1–#3` | **required, min 2** | after §2, §4, §6 |
| `★ Fixed Point` ×6 | **required, min 1** | §1, §2, §3, §4, §5, §6 |
| `**Dead Reckoning:**` ×1 min | **required** | §4 — the four access modes and three reclaim policies stated flat, no register at all. See §4 |
| `⚠ Navigational Hazards` ×2 | expected, min 1 | §1 (hostPath is an escape hatch with security risk), §4 (reclaim default is Delete, and Retain does not mean reusable) |
| `☀️ Zenith` | expected | §7 |
| `## Exam Alert! 🚨` | **required** | after §7 |
| `## Practice Questions` | **required** | 17 questions |
| `## Chapter Summary` | **required** | table |
| `## The Voyage Ahead` | **required** | closing — name locked 2026-04-19; hands to Ch 12 |
| `🏆 Safe Harbor` | expected | chapter close |

**Heading form.** `## 🔵 §2 — The Claim and the Supply`, matching Chapters 5–10 and B6 Collision #3's recommendation. Difficulty glyph before the section number.

**Zenith heading glyph — adopt `☀️`.** `## ☀️ §7 — Outliving the Pod That Asked`, per B6 Collision #4 and the precedent Ch 10 set, *plus* an inline `☀️ **Zenith:**` block inside §7. The heading glyph signposts the section; the inline block is what the structural contract matches on. Both, not either.

**Zenith:** exactly one, per Part 18.10. `ch11-zenith-outliving-the-pod` in §7.

**⚠ One word collision, and it is milder than Ch 10's.** `volume` carries the Kubernetes sense throughout; the Docker-volume sense is not used anywhere in this chapter (B7 Canonical forms). The live risk instead is the **`Volume` / `PersistentVolume` near-miss** — a reader who has just learned that a `volume` is a Pod-scoped thing in §1 meets `PersistentVolume` in §2 and reasonably assumes it is the same noun with a modifier. It is not: one is a field in a PodSpec, the other is a cluster-scoped API object. **§2 must open by disposing of this explicitly**, in one sentence, before any supply/demand material. The documentation itself invites the confusion by calling PVs "volume plugins like Volumes" — quote that and then separate them, rather than hoping the reader does not notice.

---

## Arc-outline inheritance

Authoritative input: `.pipeline-state/book-outline/arc-outline.md` § "Chapter 11 — Below the Waterline". Carried forward without modification:

- **Covers**: **D2.4** — volume types (`emptyDir`, `hostPath`, `configMap`/`secret`, `projected`, ephemeral); PersistentVolume; PersistentVolumeClaim; StorageClass; static vs dynamic provisioning; binding; reclaim policies (Retain / Delete / Recycle); access modes (RWO / ROX / RWX / RWOP); CSI; StatefulSet + PV pairing.
- **Prerequisites**: Ch 4 (objects, ConfigMap/Secret as volume sources), Ch 5 (Pod volumes), Ch 6 (StatefulSet, introduced). **See the PREREQ NOTE in frontmatter** — the real dependency set is wider and narrower than this line implies.
- **Retrieval targets**: **20%** **[B3]**, from Ch 6–10, with the **≥4-back spacing floor** satisfied several times over: **Ch 4 (ConfigMap/Secret as volume sources, and cluster-scoped, seven back)**, **Ch 2 (the writable container layer, nine back)**, **Ch 7 (feasible nodes, four back, via `WaitForFirstConsumer`)**. Named anchors: StatefulSet identity (Ch 6, five back) completed rather than restated; Pod volume mounts (Ch 5).
- **Question budget**: 8 Soundings · 10 Bearings · 17 Practice. Bearings set at 15 below, per B4's "minimums to exceed" and the shape Chapters 3–10 shipped.
- **Figures**: six anchors, listed verbatim in `figures_planned`.
- **Depth band**: standard.
- **Blocking gaps**: G11 (CSI), G12 (volume types other than PV/PVC). **G12 status: CLOSED** — `k8s-docs-volumes-2026-08-23.md` covers `configMap`, `downwardAPI`, `emptyDir` (including `medium: Memory` and `sizeLimit`), `hostPath` (including the `type` field and the security warning), `persistentVolumeClaim`, `projected`, `secret`, `nfs`, `local` and `csi`. **G11 status: OPEN and consequential** — see § Open questions #2. **Four further gaps the arc outline did not anticipate are open — see § Open questions #3.**
- **Note**: **Closes the book's one deliberate forward reference.** `ch11-fig05` is the back half of the Ch 6 StatefulSet cross-bearing and must be built as a reciprocal pair with `ch06-fig05-statefulset-vs-deployment-identity` (verified present at `chapter-06` line 816). CSI planted here is collected in Ch 17 §4. **The arc outline and B6 both call CSI "the third" of the four interfaces; shipped Ch 10 has already told the reader it is the last. See § Open questions #1 — this chapter's one blocking editorial decision.**

### Debts falling due in this chapter

**Eight published cross-bearings point at Chapter 11**, two pinned to a section number, plus four un-pointered promises made in Ch 10's closing. Draft knowing the reader was told to expect each one.

| Owed by | Promise made | Paid in |
|---|---|---|
| `chapter-02` line 600 | *"Ch 11 — CSI and storage drivers"* — dropped in the four-interfaces passage that Ch 2 calls *"the spine of the book's closing argument"* | **§5**. The word *drivers* is in the promise, so §5 owes the reader what a CSI driver actually is and installs, not only that CSI exists |
| `chapter-04` line 540 | *"Ch 11 — PersistentVolumes and StorageClasses"* — dropped in the namespaced/cluster-scoped section, where PV and StorageClass were the named cluster-scoped examples | **§2 and §3**. §2 must *use* the scope fact rather than re-teach it: the reason a PVC is namespaced and a PV is not IS the supply/demand split |
| `chapter-04` line 722 | *"Ch 11 — ConfigMap and Secret volumes"*, tagged `[source: k8s-docs-volumes-2026-08-23]` — the reader was told both objects reappear as volume types mounted into a filesystem | **§1** |
| `chapter-04` line 762 | *"Ch 11 — ConfigMap and Secret volumes, and the `subPath` exception"* — **the `subPath` exception is named in the promise**, attached to Ch 4's hedge about mounted ConfigMaps updating automatically | **§1**, and this is the tightest of the eight: the reader was promised a *specific named exception*, so §1 must state that a container using a ConfigMap as a `subPath` mount does not receive updates. Note the ⚠ RESEARCH GAP comment already sitting at `chapter-04` line 761 — the Ch 4 half is uncited, and §1's citation will be the first time this claim is sourced in the book |
| `chapter-05` line 349 | *"Ch 11 §1 — volume types and lifetimes"* — **section-pinned**. Ch 5 §1 named the shared `emptyDir` as the second half of the Pod's shared context and said outright *"We name it here and leave it"* | **§1** |
| `chapter-05` line 775 | *"Ch 11 — projected volumes"* — dropped where TokenRequest tokens are mounted | **§1**, and the framing must connect back: the projected volume the reader already met carrying a ServiceAccount token is the same mechanism, generalised |
| `chapter-06` line 868 | *"Ch 11 — PersistentVolumes, claims, and how a Pod's storage follows its identity"* — preceded at line 862 by an explicit, unusually blunt deferral: *"you have not been told how that storage is provisioned, requested, sized, reclaimed, or shared. That is deliberate"* | **§2, §3, §4, §6.** Ch 6 enumerated five verbs. Every one has to be answered somewhere in this chapter, and §6 has to visibly close the loop rather than merely mention StatefulSets |
| `chapter-09` line 758 | *"Ch 11 §6 — StatefulSets and their per-replica volume claims"* — **section-pinned**, and Ch 9 §6 had just shown the reader the headless-Service DNS half of the same identity | **§6** |
| `chapter-10` line 1846 (Voyage Ahead) | *"a ladder of three different lifetimes, only one of which survives the thing that created it"* | **§1.** The reader was given the shape and the count before the chapter opened. §1 must deliver exactly three rungs — not four, not "several" |
| `chapter-10` line 1848 | *"what a per-replica volume claim is, and why it outlives not just the Pod but the rescheduling"* | **§6.** Two claims promised, and *rescheduling* is the one readers under-weight |
| `chapter-10` line 1866 | *"you will meet the last of the four pluggable interfaces… Chapter 11 brings CSI, at storage, and that closes the set"* | **§5**, and it fixes the ordinal — see § Open questions #1 |
| `chapter-10` lines 1870–1872 | *"You will meet several objects in Chapter 11 that describe storage without providing any, and at least one arrangement where a claim sits unbound because the thing that would satisfy it has not been installed. **You know what question to ask about that now.**"* | **§3 and §5.** This is the chapter's single best retrieval hook and it was set up two chapters in advance. The phrase to retrieve is Chapter 3's, verbatim, exactly as Ch 10 §3 and §8 retrieved it: **an object without its component does nothing.** **Do not coin a competing phrase.** A PVC naming a StorageClass with no provisioner installed is the fourth sighting of the same light |

### What this chapter owes forward

| Owed to | What must be plantable | Where it is planted |
|---|---|---|
| **Ch 12 §4** | Secret hardening prefers file mounts over environment variables — an argument that only works if the reader knows Secret-as-volume | §1, where the `secret` volume source is taught (and `tmpfs`-backed, never written to non-volatile storage, which is half of §12.4's argument already) |
| **Ch 12 §5** | `hostPath` as the workload-to-host boundary problem `securityContext` and Pod Security Standards exist to police | §1's ⚠ Navigational Hazards on `hostPath`. Plant, do not resolve |
| **Ch 13 §2** | Volume-mount failure as a Pods-that-never-start signature; a PVC stuck unbound as a cause of `Pending` | §2 (unbound indefinitely) and §3 (no provisioner). Ch 13 diagnoses; this chapter supplies the mechanism |
| **Ch 16 §6** | StatefulSet debugging from the application side needs per-replica PVC and its naming | §6 |
| **Ch 17 §4** | CSI as one of the four collected | §5 |

---

## 1. Why This Chapter Matters

*Planning notes for drafting — not prose.*

**The curiosity gap.** Open on the gap Ch 10 pre-loaded and then leave it open until §4: everything the reader has learned for ten chapters has been built on Pods being disposable, and disposability is exactly what a database cannot tolerate. The question that stays open is not *"how do I attach a disk"* — it is *"when the Pod is gone, who decides whether the data is gone too, and when did they decide it?"* That question resolves at §4 (reclaim policy, set on the StorageClass, inherited by the volume, decided before the reader ever created the claim) and pays off again at §6.

**The identity frame.** The move this chapter teaches is the one that separates people who *use* a cluster from people who *run* one: separating the request for storage from the supply of it. A developer who understands that they write a claim and never a volume can be handed a cluster whose backing store they have never heard of and be productive on it the same afternoon. That is not an exam trick; it is the actual division of labour on every platform team the reader will join.

**The stakes.** Concrete and honest: the failure modes here are the ones that destroy data rather than merely stop traffic. A Service misconfigured badly is an outage. A reclaim policy misunderstood is a deleted volume. Say this plainly once and do not repeat it — Part 14 forbids fear-mongering, and one accurate sentence outperforms three dramatic ones.

**Dead Reckoning + Extended Analogy.** The chapter needs both. Dead Reckoning: on-disk files in a container are ephemeral; volumes exist to solve two named problems — surviving container crashes, and sharing files between containers in one Pod — and persistent volumes exist to solve a third, surviving the Pod. Extended Analogy: the ship's hold below the waterline — the cargo is not part of the crew, the crew is relieved and replaced on schedule, and the hold is inventoried, claimed, and released by a process that has nothing to do with the watch rotation. Keep it to one sidebar; the title is already carrying the metaphor.

---

## 2. What You'll Learn

Four to six outcomes, active verbs, one with a wry parenthetical per Part 15:

- **Trace** a file from the container filesystem outward, and say at which of three boundaries it stops surviving.
- **Distinguish** a PersistentVolume from a PersistentVolumeClaim from a StorageClass — the three-way distinction the exam blueprint calls out by name — and say which one a Pod actually references.
- **Predict** whether a claim will bind, stay unbound, or trigger a volume into existence, given a cluster's provisioning setup.
- **Read** an access mode as a statement about how many *nodes*, not how many Pods (a distinction with a specific mode devoted to the difference, which should tell you how often it is gotten wrong).
- **State** what happens to the data after the claim is deleted, and where that decision was actually made.
- **Explain** why a StatefulSet's storage survives not just a Pod restart but a reschedule onto a different node — closing the loop Chapter 6 opened on purpose.

*Closing line, per house form:* You will also collect the last of the four pluggable interfaces, and with it a rule about interfaces that Chapter 17 will ask you to state without help.

---

## 3. Soundings plan

Eight questions, per the content-chapter baseline. Rubric is the standard 6+ / 3–5 / 0–2 — **but see the PREREQ NOTE: the 0–2 branch must name specific sections, not whole chapters.** Suggested 0–2 wording: *"Check Ch 5 §1 (what a Pod shares), Ch 4 §3 (cluster-scoped resources) and Ch 6 §6 (StatefulSet identity) before starting. That is three sections, not three chapters — this material assumes narrow, specific things rather than everything that came before."*

| # | Topic | Prerequisite / intuition tested | Why it works as a pre-test |
|---|---|---|---|
| 1 | Container writes a file, crashes, kubelet restarts it — is the file there? | **Ch 2 §2** (writable container layer) + **Ch 5 §4** (restart, not replacement) | The lowest rung of §1's ladder. A reader who gets this right already holds the bottom of the ladder and can skim §1's opening. A reader who says "yes, it's fine" has the misconception §1 exists to correct, surfaced *before* the correction arrives |
| 2 | The two things every container in one Pod shares | **Ch 5 §1**, verbatim material | Cheap confidence-builder placed second per the early-easy-win rule, and it primes the reader to notice that this chapter is about the half Ch 5 named and left |
| 3 | Is a PersistentVolume namespaced or cluster-scoped, and how would you settle it from the cluster? | **Ch 4 §3**, which named PV as a cluster-scoped example three times and graded it | Retrieval at seven-back — the ≥4-back floor, satisfied inside the Soundings at zero budget cost. The second half (`kubectl api-resources --namespaced=false`) tests whether the reader retained the *method* or only the fact |
| 4 | What makes StatefulSet Pods non-interchangeable, and what did Ch 6 say it was deliberately not explaining? | **Ch 6 §6**, including its explicit deferral at line 862 | Tests whether the reader registered a promise as a promise. This is metacognitive rather than technical, and it is the one that most changes reading strategy: a reader who remembers the deferral will read §6 as a payoff rather than as new material |
| 5 | In a storage array, who creates a LUN and who requests one — and does the requester need to know the vendor? | General infrastructure prior; no chapter | Builds §2's supply/demand intuition entirely outside Kubernetes, so no Fixed Point is touched. A storage admin scores here even if they scored 0 on Q1–Q4, which is the point of mixing prior types |
| 6 | Name the pluggable interfaces met so far and what each hands outside the project | **Ch 2 §4**, **Ch 6 §8**, **Ch 9 §1**, enumerated together in Ch 10's closing | Sets up §5 and pre-tests the *pattern* rather than any one instance. Answer key confirms the count is three and that the fourth arrives in §5 — which shipped Ch 10 already told them |
| 7 | Delete a VM — does its disk go too? Does it depend on how the disk came to exist? | General infrastructure prior | The second clause is the whole question. It builds the intuition that provisioning history determines deletion behaviour, which is exactly §4's reclaim-policy inheritance, without naming Retain or Delete |
| 8 | Can two machines mount one block device read-write simultaneously without a clustered filesystem? | General infrastructure prior | Establishes the physical constraint that makes RWO sensible. Crucially it does **not** reveal that Kubernetes counts nodes rather than Pods — it makes that revelation *land* in §4 instead of arriving unmotivated |

**Spoiler audit: clean.** See the FIXED-POINT SPOILER CHECK block in frontmatter for the per-question reasoning. Summary: no stem states the ladder, the supply/demand split, the binding cardinality, the RWO unit, the reclaim default, the StatefulSet PVC survival rule, or CSI's position in the set.

---

## 4. Section plan

Seven sections, one arc. The through-line is a single question asked at increasing scope — *what survives what?* — and each section widens the scope by one step. §7 states the answer the walk was building toward.

---

### §1 — ⚪ Three Lifetimes, and the Volumes That Have Them

**Must cover.** The three-rung lifetime ladder: the container filesystem (discarded on container restart), the Pod-scoped volume (destroyed when the Pod ceases to exist), and cluster-scoped storage (not destroyed). Then the volume types that sit on the middle rung: `emptyDir` (including `medium: Memory` counting against the writing container's memory limit, and `sizeLimit`), `hostPath` with its `type` field and its security warning, `configMap` and `secret` as volume sources, `projected` as the multiplexer, `downwardAPI`, generic ephemeral volumes, and `subPath` with its no-updates exception. `nfs` and `local` get named as examples of the third rung to set up §2, not taught.

**Objectives.** D2.4.

**Introduces.** volume · volume-lifetime-ladder · emptydir (+ medium, sizeLimit) · hostpath (+ type field, security risk) · configmap-volume · secret-volume (tmpfs-backed) · projected-volume · downwardapi-volume · generic-ephemeral-volume · subpath (+ no-updates exception).

**Figure.** `ch11-fig01-volume-lifetime-ladder` — the chapter's spine figure.

**Fixed Point.** The ladder itself, stated as a count of three with the *event* that crosses each boundary named. Ch 10 promised the reader three rungs; deliver three.

**⚠ Navigational Hazards.** `hostPath`. The documentation's own framing is the right one — *"a powerful escape hatch"* with *"many security risks"* and a best practice of avoiding it — and it plants Ch 12 §5 without resolving it.

**Debts paid.** `chapter-05:349` (pinned §1) · `chapter-04:722` · `chapter-04:762` (the `subPath` exception, by name) · `chapter-05:775` (projected volumes) · `chapter-10:1846` (three rungs).

**Cross-bearings out.** Back: Ch 2 §2 (the writable container layer, and why the bottom rung is bottom), Ch 5 §1 (the shared `emptyDir` named there), Ch 4 §4 (ConfigMap and Secret as objects), Ch 5 §6 (the projected token volume the reader already has). Forward: Ch 12 §4 (file mounts over env vars), Ch 12 §5 (`hostPath` and workload-to-host isolation).

**Checkpoint after.** No.

**Note.** Resist enumerating every volume type the documentation lists. B6 forced types and the ladder into one section because of the `chapter-05:349` pin; the section earns its keep by making the ladder the organising idea and hanging types off it, not by being a catalogue. `nfs` and `local` are mentioned only as the rung-three teaser.

---

### §2 — ⚪ The Claim and the Supply

**Must cover.** PersistentVolume as a piece of cluster storage with a lifecycle independent of any Pod. PersistentVolumeClaim as a user's *request* for a size and an access mode. The documentation's own proportion — Pods consume node resources as PVCs consume PV resources — which is the cleanest way in. Who creates which. That a Pod references a claim, never a volume. Binding as a control-loop match that is **exclusive and one-to-one**, and that an unmatched claim stays unbound **indefinitely**, binding later only if a match appears. PV phases.

**Objectives.** D2.4.

**Introduces.** persistentvolume · persistentvolumeclaim · supply-and-demand-split · pv-lifecycle-independence · binding · exclusive-one-to-one-binding · unbound-claim · pv-phase · released-not-available.

**Figure.** `ch11-fig02-pv-pvc-storageclass-binding`.

**Fixed Point.** PV is supply, PVC is demand, and **a Pod references the claim, never the volume**. B1 trap 64 is exactly this reversal.

**Debts paid.** `chapter-04:540` (partially) · `chapter-06:868` (the *requested* and *sized* verbs).

**Cross-bearings out.** Back: Ch 4 §3 — and this is a *use*, not a restatement. The reason a PVC is namespaced and a PV is not is the supply/demand split itself, which turns a memorized scope fact into a derived one. Back: Ch 3 §6 — the binder is a control loop, and naming it as one is free retrieval on the book's spine concept. Forward: Ch 13 §2 (a claim that never binds is a Pod that never starts).

**Checkpoint after.** **Yes — ☆ Taking Your Bearings #1.**

**Note.** This section opens by disposing of the `Volume` / `PersistentVolume` near-miss (see Chapter-type note). Do it in one sentence, before the supply/demand material, quoting the documentation's own *"volume plugins like Volumes"* phrasing and then separating them.

---

### §3 — 🔵 Provisioning on Demand

**Must cover.** StorageClass as the resource that lets administrators offer varieties of storage — performance tiers and so on — without exposing implementation. Static provisioning (admin pre-creates PVs carrying real storage details) versus dynamic (no static PV matches, so the cluster creates one for the claim). That dynamic provisioning requires *both* that the claim requests a class *and* that the administrator configured that class for it. The `provisioner` and `parameters` fields. The default StorageClass. That a claim requesting class `""` **disables** dynamic provisioning for itself. `volumeBindingMode` and `WaitForFirstConsumer`.

**Objectives.** D2.4.

**Introduces.** storageclass · static-provisioning · dynamic-provisioning · provisioner · storageclass-parameters · default-storageclass · empty-storage-class-opt-out · volume-binding-mode · wait-for-first-consumer.

**Figure.** `ch11-fig03-static-vs-dynamic-provisioning`.

**Fixed Point.** Dynamic provisioning needs two conditions, not one — the claim must name a class *and* the class must be configured to provision. One without the other yields a claim that waits forever.

**Debts paid.** `chapter-04:540` (StorageClasses) · `chapter-06:868` (the *provisioned* verb) · **`chapter-10:1870`** — the arrangement where *"a claim sits unbound because the thing that would satisfy it has not been installed."*

**Cross-bearings out.** Back: **Ch 10 §3 and Ch 3 §4 — retrieve the phrase verbatim: *an object without its component does nothing.*** A StorageClass naming an uninstalled provisioner is the fourth sighting, and Ch 10 explicitly set the reader up to recognise it. Back: **Ch 7 §2** — `WaitForFirstConsumer` exists because binding a volume before the scheduler has picked a node can bind it somewhere the Pod cannot go. This is a four-back retrieval that is genuinely load-bearing rather than decorative, and it is the cleanest available demonstration that scheduling and storage are one decision. Forward: Ch 13 §2.

**Checkpoint after.** No.

**Note.** `WaitForFirstConsumer` is above KCNA's stated depth (the blueprint asks the reader to *distinguish* PV from PVC from StorageClass, not to tune binding modes). Put the mechanism in a `🔭 Closer Look` so the depth signal is honest, but keep the *consequence* — that volume binding can wait on scheduling — in body prose, because it is what makes the storage/scheduling connection visible.

---

### §4 — 🔵 Access Modes and What Happens After

**Must cover.** The four access modes as statements about **node count**: RWO (one node, and multiple Pods on that node may still share it), ROX (many nodes, read-only), RWX (many nodes, read-write), RWOP (one Pod, cluster-wide). The unit changes only in the fourth, which is the whole reason the fourth exists. Then reclaim: what happens to the PV after its claim is deleted. Retain (PV becomes `released`, not `available`; data remains; manual admin reclamation required). Delete (removes the PV object *and* the backing storage asset; **the default inherited from the StorageClass for dynamically provisioned volumes**). Recycle (deprecated).

**Objectives.** D2.4.

**Introduces.** access-mode · readwriteonce · readonlymany · readwritemany · readwriteoncepod · node-count-semantics · reclaim-policy · retain · delete · recycle-deprecated · inherited-reclaim-policy.

**Figure.** `ch11-fig04-access-modes-and-reclaim-policies` — two-panel, hard label budget. See § Required figures.

**Fixed Point ×2.** (a) RWO counts **nodes**; RWOP is the one that counts Pods. (b) Dynamically provisioned volumes inherit the StorageClass's reclaim policy, which defaults to **Delete** — so the decision that determines whether the data survives was made by whoever wrote the StorageClass, before the reader existed.

**`— Dead Reckoning`.** This section carries the chapter's required Dead Reckoning block: four access modes and three reclaim policies, stated flat, no metaphor, no register. This is exactly the material a reader wants delivered without ornament the night before an exam, and it is the block The Lodestar will draw from.

**⚠ Navigational Hazards.** The reclaim cluster: Delete is the default for dynamic volumes; Retain does not mean reusable.

**Debts paid.** `chapter-06:868` (the *reclaimed* and *shared* verbs — both, and this is the section where Ch 6's five-verb promise finishes).

**Cross-bearings out.** Back: Ch 6 §6, closing the enumerated deferral. Forward: none required.

**Checkpoint after.** **Yes — ☆ Taking Your Bearings #2.**

**Note.** Five of B1's seven sourced storage traps (63, 65, 66, 67, 68) live in §2 and §4. This section is the chapter's densest exam surface at the lowest conceptual difficulty — worth saying to the reader in as many words, because the difficulty glyph (🔵) and the exam yield are pulling in opposite directions and readers calibrate on the glyph.

---

### §5 — 🔵 Who Actually Provides the Storage

**Must cover.** CSI as the interface that lets vendors introduce new storage systems *without editing core Kubernetes code* — the same move as CRI, CNI and CRDs, at the fourth socket. What a CSI driver is and what installing one puts into the cluster. In-tree volume plugins and the migration away from them. **And the ordinal: this is the last of the four, not the third** (§ Open questions #1).

**Objectives.** D2.4.

**Introduces.** csi · csi-driver · in-tree-volume-plugin · csi-migration · fourth-pluggable-interface · absent-component-pattern (second sighting this chapter).

**Figure.** None. Deliberate — see § Open questions #6.

**Fixed Point.** CSI is where storage stops being Kubernetes' problem and starts being a vendor's, on a published contract. The reader should be able to state the shape of all four interfaces from this one, which is what Ch 17 §4 will ask.

**Debts paid.** `chapter-02:600` (*"CSI and storage drivers"* — the word *drivers* is in the promise) · `chapter-10:1866` (the set closes here).

**Cross-bearings out.** Back: Ch 2 §4 (CRI), Ch 6 §8 (CRDs), Ch 9 §1 (CNI) — all three, because the point is the set. Back: Ch 10 §3 again — a PVC bound to a StorageClass whose CSI driver was never installed is the same rule a third time in three sections, and saying so is the retrieval. Forward: Ch 17 §4.

**Checkpoint after.** No.

**Note.** Keep CSI's internals behind a `🔭 Closer Look`. KCNA asks for recall — name the storage interface, say what it is for. The driver architecture and the in-tree migration are legitimately deeper than the exam requires, and the depth signal should say so rather than implying the reader must memorise it. **This section is fully blocked on research — see § Open questions #2.**

---

### §6 — 🔵 Pods That Are Not Interchangeable, Revisited

**Must cover.** `volumeClaimTemplates`: for each entry, every Pod receives one PersistentVolumeClaim. The naming, so the reader can recognise `www-web-0` in a cluster. That the same PVC stays bound to a Pod throughout its lifecycle. That when a Pod is rescheduled onto a *different* node, its mounts follow — the claim, not the node, is what the storage is attached to. That the PVCs are **not deleted** when the Pod or the StatefulSet is deleted, and must be removed manually. That the storage must be either dynamically provisioned from the requested class or pre-provisioned by an admin — which is §3, arriving as a consequence rather than a rule.

**Objectives.** D2.4.

**Introduces.** volumeclaimtemplates · per-replica-pvc · pvc-survives-deletion.

**Figure.** `ch11-fig05-statefulset-pvc-pairing` — **reciprocal pair with `ch06-fig05`**. See § Required figures.

**Fixed Point.** A StatefulSet's PVCs outlive the StatefulSet. Deleting the workload does not delete the data, and nobody cleans it up for you.

**Debts paid.** `chapter-09:758` (pinned §6) · `chapter-06:868` · `chapter-10:1848` (*"outlives not just the Pod but the rescheduling"* — both halves, and the rescheduling half is the one to lead with, because it is the under-weighted one).

**Cross-bearings out.** Back: Ch 6 §6 (identity — the half the reader has) and Ch 9 §6 (the headless-Service DNS half, met two chapters ago). Forward: Ch 16 §6 (debugging a StatefulSet from the application side).

**Checkpoint after.** **Yes — ☆ Taking Your Bearings #3.**

**Note.** This section must *complete* Ch 6 §6, not restate it. Per the B7 ledger, Ch 6 §6 owns identity and Ch 11 §6 owns the storage pairing — a reciprocal pair in which neither half redefines the other. Open by naming the debt explicitly: the reader was told in Chapter 6 that the explanation was incomplete, and this is the missing half arriving on schedule. That framing converts a deferral the reader might have read as a dodge into a promise kept, which is worth more than the technical content of the section.

---

### §7 — ☀️ Outliving the Pod That Asked

**Must cover.** No new material. The synthesis: every question in this chapter was one question — *what survives what?* — and the answer at every rung was decided by something other than the workload. The container does not decide whether its files survive a restart; the Pod does not decide whether its volume survives deletion; the claim does not decide whether the data survives the claim. The StorageClass decided that, before anyone wrote a manifest. That is the same shape as every other separation in the book, and it is why a developer can be handed an unfamiliar cluster and be productive on it.

**Objectives.** D2.4.

**Figure.** `ch11-zenith-outliving-the-pod`.

**`☀️ Zenith`.** Required inline block, in addition to the `☀️` heading glyph.

**Cross-bearings out.** Back: Ch 3 §6, Ch 4 §1 (intent is durable; the record outlives the thing that acts on it — which is the same sentence as this chapter's title). Forward: Ch 17 §4.

**Checkpoint after.** No — Exam Alert follows.

---

## 5. Taking Your Bearings checkpoints

Three checkpoints of five, totalling **15** against B4's floor of 10, matching the shape Chapters 3–10 shipped without exception. Retrieval target **20%** per B3 — **3 of 15 items** drawn from earlier chapters, distributed one per checkpoint so no single checkpoint carries the whole retrieval load.

Every checkpoint follows house form: trap answers targeting named misconceptions, why-wrong explanations for all options, and a revision prompt naming the specific section for a 0–2 score.

### ☆ Taking Your Bearings #1 — after §2

- **Topic.** The lifetime ladder and the supply/demand split.
- **Count.** 5.
- **Retrieval.** 1 of 5 — **Ch 2 §2**, nine back, satisfying the ≥4-back floor on the chapter's first checkpoint. Item: what the writable container layer means for a file written by a process that then crashes, now that the reader can place it on the ladder.
- **Traps targeted.** B1 trap 64 (reversing PV and PVC) · B1 trap 63 (a PVC binds to any PV that is big enough) · the `emptyDir`-survives-Pod-deletion misconception, which is sourced in `k8s-docs-volumes` but **absent from B1's trap inventory** (see § Open questions #4).

### ☆ Taking Your Bearings #2 — after §4

- **Topic.** Provisioning, access modes, reclaim.
- **Count.** 5.
- **Retrieval.** 1 of 5 — **Ch 7 §2**, four back. Item: a claim with `WaitForFirstConsumer` and a Pod the scheduler cannot place, asking what state each object is in. This tests the storage/scheduling join in both directions and is the chapter's best single integration item.
- **Traps targeted.** B1 trap 65 (RWO means one Pod) · B1 trap 66 (deleting a PVC always keeps the data) · B1 trap 67 (Retain means immediately reusable) · B1 trap 69 (class `""` uses the default).
- **Difficulty note.** This is the chapter's **challenge checkpoint** per Part 10B. Label it as intentionally hard, normalise the struggle, and follow it with the achievable §5. Four of B1's seven storage traps are concentrated here and that concentration is not accidental — it is where the material is genuinely counter-intuitive.

### ☆ Taking Your Bearings #3 — after §6

- **Topic.** CSI, the interface pattern, and the StatefulSet pairing.
- **Count.** 5.
- **Retrieval.** 1 of 5 — **Ch 6 §6**, five back. Item: given a StatefulSet deleted and its PVCs still present, what the reader should conclude about the relationship between identity and storage.
- **Traps targeted.** "Deleting a StatefulSet cleans up its PVCs" — **sourced in `k8s-docs-statefulset-2026-08-24` but absent from B1's inventory** (§ Open questions #4) · treating CSI as a storage *product* rather than an interface · the absent-component pattern applied to an uninstalled CSI driver.

---

## 6. Exam Alert plan

**High-priority topics** — in the order the blueprint's own language justifies:

1. **PV vs PVC vs StorageClass.** B1's domain analysis records that D2 expects the candidate to *"distinguish PV from PVC from StorageClass"* — this three-way distinction is named in the published expectation, which makes it the highest-confidence claim in the chapter's Exam Alert. Frame it as *frequently tested*, which the source supports.
2. **Access modes, and what unit each counts.**
3. **Reclaim policy, and where the decision was actually made.**
4. **Static vs dynamic provisioning, and the two conditions dynamic requires.**

**Common traps** — all seven of B1's storage traps are `[source]`, none `[inferred]`, so all seven may be framed as exam targets rather than merely "easy to confuse." Per Ethical Guardrail #8 this is a meaningful licence and this chapter is unusual in having it across the board:

| B1 # | Trap | Correction |
|---|---|---|
| 63 | "A PVC binds to any PV that's big enough" | Binding is exclusive and one-to-one; an unmatched claim stays unbound indefinitely |
| 64 | Reversing PV and PVC | PV is supply, PVC is demand, Pods reference claims |
| 65 | "ReadWriteOnce means one Pod" | It means one **node**; RWOP is the one-Pod mode |
| 66 | "Deleting a PVC always keeps the data" | Dynamic volumes inherit the class's policy, defaulting to Delete |
| 67 | "Retain means the PV is immediately reusable" | It becomes `released`, not `available` |
| 68 | Expecting `Recycle` to be live | Deprecated |
| 69 | "Class `\"\"` uses the default class" | It disables dynamic provisioning for that claim |

**Two additions, both sourced, neither in B1's inventory** (§ Open questions #4): `emptyDir` survives container crashes but not Pod removal; a StatefulSet's PVCs survive deletion of the Pod and of the StatefulSet and must be deleted manually.

---

## 7. Practice Questions plan

**Target: 17**, per B4. Interleaved, not section-ordered.

**Distribution by section:**

| Section | Items | Rationale |
|---|---|---|
| §1 volume types and lifetimes | 3 | Broad surface, low difficulty |
| §2 PV / PVC / binding | 4 | The named blueprint expectation; highest single allocation |
| §3 provisioning | 3 | |
| §4 access modes and reclaim | 4 | Four of seven sourced traps live here |
| §5 CSI | 1 | Recall-depth on the exam; one item is proportionate |
| §6 StatefulSet pairing | 2 | Including one that requires Ch 6 §6 |
| **Total** | **17** | |

**Retrieval within the 17: 20% ≈ 3–4 items**, per B3, drawn from Ch 6–10 with the ≥4-back floor already satisfied twice in the Bearings. Candidates: ConfigMap/Secret as objects versus as volume sources (Ch 4, seven back); the absent-component pattern applied to a missing provisioner (Ch 10 §3 / Ch 3 §4); StatefulSet identity (Ch 6 §6).

**Interleaving strategy.** Do not group by section. The productive pairings are the ones that force discrimination across the chapter's own near-misses:

- an access-mode item immediately followed by a reclaim item, so the reader must switch axes rather than pattern-match on "storage question, answer RWO"
- a `subPath` item placed near a ConfigMap-update item, since the exception only means something against the rule
- at least two items that require §2 **and** §3 together — a claim's fate is not determinable from either alone, and single-section items quietly teach that it is

**Framing constraint.** All seven B1 traps here are `[source]`, so "frequently tested" framing is available and should be used where it is accurate. Do not extend that framing to the two additions in § Exam Alert — they are sourced as *facts* but B1 never assessed them as *exam frequency*, and the distinction is exactly what Guardrail #8 protects.

---

## 8. Required figures

Six anchors, matching the arc outline verbatim. Every one carries a `<!-- FIGURE: … -->` comment on the line immediately before its fenced block, and a matching entry in the chapter's `image-specs.md` with a `yaml-figure-spec` block.

### `ch11-fig01-volume-lifetime-ladder` — §1

**Purpose.** The chapter's spine. Dual-codes the Fixed Point that everything else hangs from, and delivers the three-rung shape Ch 10 promised the reader before they opened the chapter.

**Content.** Three nested scopes, innermost to outermost: container filesystem → Pod-scoped volume → cluster-scoped storage. The two boundaries are the load-bearing elements and must be annotated with the *event* that crosses each — container restart crosses the first and the data does not survive it; Pod deletion crosses the second and the data does not survive it; nothing in the Pod's lifecycle crosses the third. Label budget: 3 scope labels + 3 boundary-event labels = 6, inside the ~7 ceiling of Part 18.12.

### `ch11-fig02-pv-pvc-storageclass-binding` — §2

**Purpose.** Distinguishes three similar-sounding objects — the §18.9 criterion that most strongly warrants illustration — and encodes the one relationship readers reverse.

**Content.** Two columns: supply (PV, cluster-scoped, created by an administrator) and demand (PVC, namespaced, created by a user), with the binding control loop between them and a one-to-one exclusive arrow. **The Pod's line must terminate at the PVC, not at the PV** — that single routing decision is the figure's whole pedagogical job, and it should be visually impossible to misread. StorageClass appears as a third element off to the side, deliberately unexplained here, so that §3 has something to connect to.

### `ch11-fig03-static-vs-dynamic-provisioning` — §3

**Purpose.** Two paths that produce the same end state by different routes; prose handles this badly and a diagram handles it well.

**Content.** Two parallel sequences sharing an end state. Static: admin creates PV → user creates PVC → binder matches. Dynamic: user creates PVC naming a class → provisioner creates PV → binder matches. Mark the branch point (does a matching PV already exist?) and mark the *third* path — the claim naming a class with no configured provisioner, which terminates in a claim that waits indefinitely. That third path is what makes the figure worth drawing rather than tabulating, and it is the visual form of the absent-component rule.

### `ch11-fig04-access-modes-and-reclaim-policies` — §4

**Purpose.** Two quantitative-relationship concepts that are routinely conflated because they appear adjacent in the documentation.

**Content.** **Strict two-panel with a hard per-panel label budget of four.** Left panel: the four access modes drawn as counts, with the unit made visually explicit — three modes count nodes, one counts Pods, and the eye should catch that before the reader reads a word. Right panel: reclaim policies as what remains after the claim is deleted, across three columns (PV object? backing asset? data?). Recycle appears struck through or greyed, labelled deprecated.

**⚠ Anti-pattern risk, flagged.** Two concepts in one anchor is the over-labelled-diagram failure mode from §18.12. The arc outline specifies one anchor and this outline honours it, but the two-panel structure and the four-label-per-panel budget are not optional — they are what keeps this figure legal. If the image-spec stage cannot hold it to eight total labels, split rather than crowd, and record the split as a deviation. See § Open questions #5.

### `ch11-fig05-statefulset-pvc-pairing` — §6

**Purpose.** Closes the book's one deliberate forward reference. **Reciprocal pair with `ch06-fig05-statefulset-vs-deployment-identity`** (present at `chapter-06` line 816).

**Content.** Three ordinal Pods, each wired to its own named claim (`www-web-0`, `www-web-1`, `www-web-2`). Two states shown: a Pod rescheduled onto a different node with its claim line following it, and a Pod deleted with its claim persisting. **The figure must visually rhyme with `ch06-fig05`** — same ordinal arrangement, same left-to-right reading order — because the payoff is recognition. A reader who does not feel they have seen this figure before has been given the information but not the reward. Before drafting, open `chapter-06` at line 816 and match the layout deliberately rather than approximately.

### `ch11-zenith-outliving-the-pod` — §7

**Purpose.** The chapter's single Zenith, per Part 18.10.

**Content.** Two timelines on one axis. The Pod's line begins, ends, begins again as a replacement, ends again. The storage line runs continuously beneath all of it, unbroken, with the claim as the thing that connects them at each Pod's start. It should read as `ch11-fig01` seen from further away — the ladder collapsed into the one relationship that matters. Do not add labels beyond three; this figure is carrying a feeling, and the argument was already made in prose.

---

## 9. Open questions for the author

### 1. **BLOCKING — CSI is "the third" in both binding contracts and "the last" in shipped text.**

B6 §5 reads *"Third of the four pluggable interfaces."* The arc outline agrees. But `chapter-10` line 1866 has already told the reader, in the Voyage Ahead they read immediately before this chapter:

> *"you will meet the last of the four pluggable interfaces. You have three of them already, collected one chapter at a time: CRI at the container runtime in Chapter 2, CRDs at the API itself in Chapter 6, CNI at the network last chapter. Chapter 11 brings CSI, at storage, and that closes the set."*

Shipped text is right and the contracts are wrong. B6's "third" is an artifact of the order the interfaces are *listed* in the skeleton document; the reader's *reading* order is CRI (Ch 2) → CRDs (Ch 6) → CNI (Ch 9) → CSI (Ch 11), and Ch 10 counted it correctly.

**Recommendation: §5 says "the last," or "the fourth," and never "the third."** Shipped text outranks an unshipped skeleton, and the alternative — telling a reader who was told two pages ago that they hold three that this is number three — is the kind of small contradiction that costs more trust than it looks like it should. No edit to shipped text is needed. **Flagged for B6 correction** so Ch 17 §4 does not inherit the same error.

### 2. **BLOCKING research — G11 (CSI) is still open, and §5 cannot be drafted without it.**

The corpus has exactly two sentences on CSI: `k8s-docs-volumes` line 23 (*"CSI volumes are a GA feature; vendors with external CSI drivers can implement csi volumes to introduce new storage systems into Kubernetes without ever having to edit the core Kubernetes code"*) and `k8s-docs-extending-kubernetes`, which lists it. That is enough to *name* CSI. It is not enough to write §5, which owes what a CSI driver installs and the in-tree-to-CSI migration.

**Needed at Stage 2:** `kubernetes.io/docs/concepts/storage/volumes/#csi` in full, and the CSI-migration material (`kubernetes.io/blog` or the storage concepts page's migration section). If neither can be sourced, §5 shrinks to the one-paragraph naming treatment the exam actually requires and the `🔭 Closer Look` is cut — **which is an acceptable outcome, and the author should know it is available.** The chapter does not fail without it; §5 just gets shorter.

### 3. **Four unanticipated research gaps, all in-scope for B6-assigned material.**

None was flagged by B1 because B1 assessed CSI and volume-types coverage but not these:

| Gap | B6 assigns it to | Corpus status | Needed |
|---|---|---|---|
| **PV phases** (Available / Bound / Released / Failed) | §2 | `k8s-docs-persistent-volumes` describes `released` informally but never enumerates the four | The Phase section of the same page — the cached snapshot is truncated before it |
| **StorageClass fields** — `provisioner`, `parameters`, the default-class annotation | §3 | No StorageClass source exists at all | `kubernetes.io/docs/concepts/storage/storage-classes/` |
| **`volumeBindingMode` / `WaitForFirstConsumer`** | §3 | Absent | Same page |
| **Generic ephemeral volumes** | §1 | `k8s-docs-volumes` mentions ephemeral lifetime in Background but not the `ephemeral:` volume source | `kubernetes.io/docs/concepts/storage/ephemeral-volumes/` |

**`subPath` is a partial fifth.** `k8s-docs-volumes` line 14 supports the no-updates exception (which is what `chapter-04` line 762 actually promised), but not `subPath` as a general mechanism. The promise is payable from the current corpus; a fuller treatment is not.

**Note the interaction with an existing flag:** `chapter-04` line 761 already carries a `RESEARCH GAP` comment saying the ConfigMap auto-update hedge is uncited. §1's citation of `k8s-docs-volumes` line 14 will be the first time the `subPath` half of that claim is sourced anywhere in the book. Worth telling the Ch 4 retrofit, if one happens.

### 4. **B1's storage trap inventory is missing two sourced traps.**

Traps 63–69 cover D2.4 and all seven are `[source]`. Two more are equally sourced and equally exam-shaped, and B1 did not list them:

- **`emptyDir` survives container crashes but not Pod removal.** `k8s-docs-volumes` line 16 states both halves explicitly. This is the §1 Fixed Point's trap form and it is at least as likely on an exam as trap 68 (Recycle is deprecated).
- **A StatefulSet's PVCs are not deleted with the Pod or the StatefulSet.** `k8s-docs-statefulset` line 57: *"the PersistentVolumeClaim(s) associated with the Pod's PersistentVolume(s) are not deleted when the Pod, or the StatefulSet is deleted. This must be done manually."*

**Recommendation: use both, framed as sourced facts.** They may be called common mistakes; they may **not** be called frequently tested, because B1 never assessed their frequency and Guardrail #8 draws the line there. **Flagged as a B1 addendum** so Ch 19 §2's confusion-pair matrix and Ch 20's distractor pool pick them up.

### 5. **`ch11-fig04` carries two concepts in one anchor.**

The arc outline specifies one figure for both access modes and reclaim policies. This outline honours it with a strict two-panel layout and a four-label-per-panel budget, but the risk is real and named in §18.12. **Author's call:** accept the two-panel constraint, or authorise a seventh anchor (`ch11-fig04a` / `ch11-fig04b`). Recommendation is to accept the constraint — the two concepts genuinely belong side by side, because *what you may do with the volume* and *what happens when you stop* are the two halves of one question — but if the image-spec stage cannot hold eight total labels, split rather than crowd.

### 6. **§5 has no figure, and that is a decision rather than an oversight.**

Five of seven sections carry one; §5 (CSI) and §7 (which carries the Zenith) are the exceptions, and §5's absence is the one worth defending explicitly. **Recommendation: leave it at six anchors.** The figure §5 would want is *the four pluggable interfaces side by side*, and that figure belongs to Ch 17 §4, which B6 designates the collection point. Drawing it here spends the payoff two chapters before the chapter built to receive it, and Ch 10's closing has already told the reader that Ch 17 is where the gathering happens. Recorded so a later stage does not read the gap as an omission and fill it.

### 7. **Non-blocking: does §4's difficulty glyph mislead?**

§4 is marked 🔵 Standard on conceptual difficulty, which is accurate — access modes and reclaim policies are enumerable facts. But it carries four of the chapter's seven sourced traps and the blueprint's named three-way distinction sits next door in §2. A reader calibrating effort on the glyph will under-invest exactly where the exam yield is highest.

**Recommendation: keep 🔵 and say so in prose.** Adding a difficulty tier to signal exam yield would conflate two different axes, and the difficulty indicators are a locked brand element. One sentence at the top of §4 — this material is not hard, and it is where the points are — costs nothing and fixes the mis-calibration. Recorded because it is the kind of thing a reviewer flags as an inconsistency when it is actually a deliberate choice.

### 8. **Non-blocking: the `Volume` / `PersistentVolume` near-miss is not in the B7 Canonical forms table.**

B7 lists eleven homonym pairs; this is not one of them, because strictly it is not a homonym — `Volume` and `PersistentVolume` are different words. But the reader-facing failure is the same shape as the ones B7 does list, the documentation's own *"volume plugins like Volumes"* phrasing actively invites it, and this chapter is the only place in the book where both appear in adjacent sections. The Chapter-type note above instructs §2 to dispose of it explicitly. **Recommendation: add it to B7's Canonical forms table as a near-miss row**, so Ch 13 §2 and Ch 16 §6 inherit the same discipline. Author's call; not load-bearing for this chapter, which handles it locally either way.
```

---

**Three things worth your attention before Stage 2:**

1. **Open question #1 is the one to answer first.** Shipped Chapter 10 has already committed the book to CSI being the *last* of the four pluggable interfaces; B6 and the arc outline both call it the third. I've planned for "last" and flagged B6 for correction so Ch 17 §4 doesn't inherit the error — but if you'd rather the contracts win, the fix has to happen in `chapter-10` line 1866, not here.

2. **§5 is genuinely research-blocked.** The corpus has two sentences on CSI. There's a clean fallback — shrink §5 to the naming treatment KCNA actually tests — so this doesn't stall drafting, but you should choose it deliberately rather than discover it. Three further gaps (PV phases, StorageClass fields, generic ephemeral volumes) are smaller and all live on two un-fetched kubernetes.io pages.

3. **B1's trap inventory is two short on this domain**, both sourced and both good exam material. I've flagged them as an addendum so Ch 19 and Ch 20 pick them up rather than rediscovering them.