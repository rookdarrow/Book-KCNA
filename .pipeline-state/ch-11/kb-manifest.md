I verified the integration report's findings against shipped text rather than taking them on trust, and found a third canon conflict it missed. Here is the manifest.

# Knowledge-Base Manifest — KCNA Chapter 11

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-25

> **Greenfield notice, still true.** `Book-KCNA/knowledge-base/` **does not exist on disk.** Chapter 10's Stage 14 manifest composed ten write blocks; none was applied — `git status` shows no `knowledge-base/` tree, tracked or untracked. So this stage is still creating the knowledge base, not appending to one.
>
> **Ordering constraint, and it matters.** The blocks below are **self-sufficient**: `glossary.md`, `objective-coverage.md`, `retrieval-log.md`, and `concepts/absent-component-pattern.md` each carry Chapter 10's content merged with Chapter 11's, transcribed from `.pipeline-state/ch-10/kb-manifest.md`. If the orchestrator replays Ch 10's manifest **after** this one, Chapter 11 is silently erased from all four files. Apply Ch 10's blocks first, or not at all. Ch 10's six other concept shards are separate filenames and do not collide — replay them freely.

---

## Glossary entries added to `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md`

Two tiers. The integration report marked **6 terms** as leaving the reader unable to look something up; the same report noted that skill Part 16 requires *all* technical terms introduced in the book, not merely the undefined ones, so the **24 ledger-owned Chapter 11 terms** are harvested alongside them.

### Tier 1 — the six the reader cannot look up (integration report §Glossary)

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **NFS** | ⚠ **No chapter definition or expansion exists.** Chapter supplies function only: *"an `nfs` volume allows an existing NFS share to be mounted into a Pod"* | Chapter 11 §1 |
| **LUN** | ⚠ **No chapter definition exists.** Used bare in Soundings Q5 and its answer key | Chapter 11 🧭 Soundings Q5 |
| **iSCSI** | ⚠ **No chapter definition exists.** Both uses are inside direct quotations from Kubernetes documentation | Chapter 11 §2 |
| **EBS** | ⚠ **No chapter definition exists.** Used as an illustrative backing store | Chapter 11 "Why This Chapter Matters" |
| **finalizer** | ⚠ **No chapter definition exists.** Named once, unexplained: *"You will see it sitting in `Terminating` with `kubernetes.io/pvc-protection` in its finalizers list"* | Chapter 11 §2 |
| **`CSIDriver`** | *"CSIDriver captures information about a Container Storage Interface (CSI) volume driver deployed on the cluster"* `[source: k8s-api-ref-csidriver-v1-2026-08-25]` | Chapter 11 §5 |

**I verified all four acronyms independently of the report.** `NFS`, `LUN`, `iSCSI`, and `EBS` return **zero matches across `chapter-01` … `chapter-10`** and **zero rows in the B7 ledger** — not in the 74-entry acronym register, not in the ambient tier. Chapter 11 is genuinely their first appearance in the book, and none is expanded.

**Two of the six reach graded material, which the B7 orphan doctrine forbids resolving by glossary alone** (*"a term used in question text or an answer key may not be glossary-only, because a reader who meets it there has no place to look it up mid-question"*):

- **NFS** carries **Practice Q7 and Q11** — Q7's correct answer turns on NFS supporting many writers.
- **LUN** carries **Soundings Q5** and its answer.
- **`CSIDriver`** is **Practice Q2 option D**. It clears the doctrine on a technicality — §5 does define it — but on one clause quoting an API reference.

The glossary rows are the lookup path. The in-text expansion is Stage 11/12 work and is recorded under **Recommended fixes**.

### Tier 2 — the 24 ledger-owned terms, harvested per skill Part 16

All 24 B7 rows for Ch 11 (`term-ownership.md:356–379`) are defined in-chapter; I checked each against the chapter text. Definitions are inherited verbatim per Rule 5 — where the chapter quotes the documentation, the glossary quotes the chapter quoting the documentation, tag intact. Full text in the write block.

Volume · volume lifetime ladder · `emptyDir` · `hostPath` · `configMap`/`secret` volume source · projected volume · generic ephemeral volume · `subPath` · `downwardAPI` volume · PersistentVolume · PersistentVolumeClaim · PV phase · binding (PV/PVC sense) · StorageClass · static vs dynamic provisioning · provisioner · default StorageClass · `volumeBindingMode` / `WaitForFirstConsumer` · access mode · reclaim policy · CSI · CSI driver · in-tree plugin / CSI migration · `volumeClaimTemplates`.

Plus four the chapter defines that the ledger does not assign: `nfs` volume, `local` volume, Storage Object in Use Protection, `persistentVolumeClaimRetentionPolicy`. And `tmpfs`, glossed in-chapter as *"a RAM-backed filesystem."* `ENOSPC` is included as provisional — it appears only in Practice Q14 distractor B, and a distractor a reader cannot look up is a badly built distractor.

---

## Concept shards added at `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/{slug}.md`

Thirteen files. Twelve are new; one is a merge that records a conflict rather than resolving it.

- `concepts/volume-lifetime-ladder.md` — **created** (the chapter's spine; three rungs, two boundaries)
- `concepts/volume-types-ephemeral.md` — **created** (`emptyDir`, projected, `downwardAPI`, generic ephemeral, `nfs`/`local` teasers)
- `concepts/hostpath.md` — **created** (separate because it carries a named forward obligation to Ch 12 §5)
- `concepts/subpath.md` — **created** (separate because it closes a Ch 4 debt a retrofit must find)
- `concepts/persistentvolume-and-claim.md` — **created** (supply/demand, scoping, binding, the routing fact)
- `concepts/pv-phases.md` — **created** (separate because of a live source disagreement — see below)
- `concepts/storageclass-and-provisioning.md` — **created** (incl. `volumeBindingMode` and the Ch 7 join)
- `concepts/access-modes.md` — **created**
- `concepts/reclaim-policies.md` — **created**
- `concepts/csi.md` — **created**
- `concepts/statefulset-storage.md` — **created** (closes the book's one deliberate forward reference)
- `concepts/pluggable-interfaces.md` — **created** (the Ch 17 §4 collection contract; holds two live naming conflicts)
- `concepts/absent-component-pattern.md` — **created as a merge** — Ch 10's shard content plus a ⚑ **CONFLICT OPEN** block. **Not reconciled.** See below.

Not shard-worthy (under threshold, or adequately carried by the glossary): `configMap`/`secret` as volume sources, provisioner, default StorageClass, in-tree plugin, Storage Object in Use Protection.

---

## ⚑ Contradictions with earlier canon — flagged, not resolved

Rule 6 requires these loud. **The first is new — the integration report did not catch it, and it is the more consequential of the two.**

### ⚑ A. The absent-component instance count. Chapter 11 undercounts, and Chapter 10 grades that exact error as wrong.

Chapter 11 states the count three times, and restarts it at the Ingress:

- `draft-v2.md:587` — *"This is the **third** sighting of the same light."* Enumerates Ingress controller, NetworkPolicy/CNI, StorageClass provisioner.
- `draft-v2.md:889` — *"You have now seen the pattern **three times in three sections**: an Ingress without a controller, a StorageClass without a provisioner, and now this. Here is **the fourth**."*
- `draft-v2.md:1402` — *"the Ingress controller, the network plugin, the provisioner, and the CSI driver — **four sightings**, one light."*

Shipped Chapter 10 sets the reader's count at **four by the end of Chapter 10**, and does it in graded material:

- `chapter-10:634` — *"You have now personally met **three** instances: the LoadBalancer with no provider, the Service with no matching Pods, and this."*
- `chapter-10:1567` — Practice Q18's **correct answer** enumerates four: LoadBalancer with no provider (Ch 9 §3); Service whose selector matches no Pods (Ch 9 §4); Ingress with no controller (Ch 10 §3); NetworkPolicy on an unsupporting plugin (Ch 10 §7).
- `chapter-10:1795` — option B, which names **only Chapter 10's two instances**, is marked wrong with this rationale: *"the common error here is **undercounting**, not misnaming. Recalling only this chapter's two instances leaves the pattern looking like an Ingress quirk."*

Chapter 11 drops both Chapter 9 instances. A reader who answered Ch 10 Q18 correctly is told six pages later that the StorageClass is the third and the CSI driver the fourth. By the count they were just graded on, they are the fifth and sixth.

**And `draft-v2.md:889` is internally inconsistent on its own terms.** Its three-item list — Ingress, StorageClass, *"and now this"* — already includes the CSI case, and the sentence then announces *"Here is the fourth."* It also silently drops the NetworkPolicy instance that line 587 included two sections earlier. The two enumerations in the same chapter are not the same set.

**Downstream cost, which is why this outranks the report's two findings.** B6 and B3 both require Ch 13 §7 and Ch 17 §7 to retrieve this pattern **by name**. Ch 10's shard reserved instance #5 for Ch 13's metrics-server and #6 for Ch 17's VPA. Chapter 11 has inserted two instances and renumbered from a different origin, so both reservations are now wrong and the two conventions diverge by exactly two. Whichever Ch 13 picks, it contradicts a graded item in the other chapter.

**Recommendation — author's call, and I would take the second option.**
1. Amend Ch 11 §3/§5/Voyage Ahead to continue Ch 10's count (StorageClass = fifth, CSI = sixth). Faithful to the graded canon; makes the ordinals clumsy.
2. **Stop numbering instances in prose entirely.** Keep the rule and the enumeration, drop the ordinal. Chapter 10 already demonstrated that two counts can run at once and had to spend a paragraph reconciling them (`chapter-10:625`); Chapter 11 is the third count, and the reconciliation cost now exceeds the rhetorical benefit. The list is what transfers; the number is what breaks.

Either way, `draft-v2.md:889`'s internal contradiction needs fixing regardless of which count wins.

**I have not picked a winner in the shard.** `absent-component-pattern.md` records both counts side by side under a `CONFLICT OPEN` heading with a `DO NOT DRAFT Ch 13 §7 UNTIL RESOLVED` marker.

### ⚑ B. Chapter 4 never taught that PVCs are namespaced — confirmed independently

`grep -c "PersistentVolumeClaim" chapter-04-records-of-intent.md` → **0**. The integration report is right. Chapter 11 §2 tells the reader *"Chapter 4 taught you that a PersistentVolume is cluster-scoped while a PersistentVolumeClaim is namespaced… You now have the reason rather than the rule"* — but half of it is new here, and **Practice Q4 tags the pair `[retrieval: ch4]`**, asking the reader to retrieve something never deposited.

This is B7 flag ⚑6 turning out to be narrower than the ledger recorded: ⚑6 anticipated PV and StorageClass appearing early in Ch 4, and PVC was never in that set. **Recorded in `retrieval-log.md` as a failed retrieval anchor, not as a clean row.**

### ⚑ C. Chapter 9's `§6` pointer — verified against shipped headings

Confirmed by reading Ch 9's heading list: **§5** = "When You Don't Want a Single Address" (headless Services), **§6** = "The Component That Makes It Real" (kube-proxy), **§7** = "Names, and Where They Resolve" (DNS). Chapter 11 §6's pointer and its surrounding prose both send the reader to kube-proxy for two things that are in §5 and §7. Chapter-text defect; Stage 11/12 work; noted here only because `statefulset-storage.md` cites the correct targets and would otherwise silently disagree with the chapter.

### Resolved — Chapter 10 left this open and Chapter 11 closed it

Ch 10's retrieval log flagged an **ordinal collision waiting in Ch 11**: the B6 skeleton labels Ch 11 §5 *"**Third** of the four pluggable interfaces"* (`section-skeleton.md:157`), which would have contradicted Ch 10's closing. **Shipped Ch 11 §5 ignored the skeleton and wrote "The fourth is CSI" / "the last of the four."** Consistent with Ch 10, with Ch 2 line 914, and with the B7 canonical set. The skeleton's annotation is now stale — recommend dropping the skeleton's ordinal annotations entirely, since they encode set-order, not encounter-order. **Ch 9's "second instance" wording remains the outlier and is still open.**

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Stakes without fear-mongering** | "A Service misconfigured badly is an outage, and outages end. A reclaim policy misunderstood is a deleted volume, and that does not end. This is the chapter where reading carefully has a different payoff than it does elsewhere." | **Strong candidate.** Skill Part 14 permits real stakes and forbids manufactured dread, but the catalog has no exemplar of the line between them. This raises the stakes by *comparison to a lesser failure* rather than by adjective, and the register stays flat. |
| **Zenith / synthesis** | "Storage outlives the Pod that asked for it, not because storage is special, but because *records of intent outlive the things that act on them*, and a claim is a record of intent. Ten chapters of Kubernetes, and it is one idea wearing different clothes." | **Strong candidate.** Pairs with the Ch 10 Zenith nomination and shows the same restraint — the payoff reduces a chapter to a clause already in the reader's hands. Note it names the chapter title as the thing being explained rather than repeating it as a slogan. |
| **Provenance separation** | "That is not a Kubernetes fact, and no Kubernetes document will tell you so. It is ordinary storage knowledge that the platform inherits from the hardware beneath it." | **Strong candidate.** Distinct from Ch 10's nominated provenance passage: that one separated *sourced claim from book inference*, this one separates *Kubernetes fact from general practitioner knowledge*. Two different lines, both worth having a canonical instance of. |
| **Extended Analogy** | The ship's-hold passage: "The cargo is not part of the crew… When the claim is released, what happens next… was settled by the terms of the arrangement long before anyone came to collect it. That last sentence is this chapter's whole argument. Hold onto it." | **Strong candidate.** Skill §18.15 formalizes Extended Analogy as a sidebar type and the catalog has no exemplar. This one earns its length by ending on the load-bearing sentence and *saying* which sentence it is. |
| **Wrong-answer teaching** | "Getting the outcome right for the wrong reason is still getting it wrong, and the exam will offer you that option." | **Moderate.** Compact statement of a real principle in the skill's self-correction Part 11, and it recurs verbatim-ish twice in the chapter. Slightly bare excerpted. |
| **Difficulty recalibration** | "This section is marked 🔵 Standard, and that rating is honest… **This material is not hard, and it is where the points are.** Read it as though it were 🔴." | **Moderate.** Useful instance of the skill's Part 12 difficulty signaling being *overridden by exam yield* — a case the skill does not currently address. Worth an author look for that reason rather than for the prose. |
| **Chapter-opening** | "For ten chapters, everything you have learned has rested on a single assumption: a Pod is disposable… That assumption is what makes Kubernetes work. It is also exactly what a database cannot tolerate." | **Weak — do not promote.** Excellent in place, but the turn depends on ten chapters of accumulated assumption. An exemplar has to work excerpted, and this one reads as a generic reversal without its setup. |

---

## Objective coverage log → `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md`

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D2.4 — Storage | Chapter 11 | deep — sole coverage; no other chapter is assigned D2.4 | — |

**Concept-level audit, D2.4 concept map (`domain-analysis.md:232–255`): 20 of 20 covered.** I walked every row. PV · PV lifecycle independence · PVC · Pods:PVCs :: node resources:Pods · StorageClass · static provisioning · dynamic provisioning · disabling dynamic provisioning · binding · unbound claims · using · reclaiming · Retain · Delete · Recycle · RWO · ROX · RWX · RWOP · StatefulSet + PV. **No gaps.** The `Pods consume node resources and PVCs consume PV resources` proportion is quoted directly at §2 rather than paraphrased, which is the one B1 concept most likely to have been dropped.

**Research gaps closed: two, both D2.4 blockers.**

- **G11** — *CNI, CSI, and CRI as the pluggable interfaces; "CSI is entirely absent."* Closed by §5, which sources CSI to the specification's own objective statement rather than to Kubernetes documentation.
- **G12** — *Volume types other than PV/PVC: emptyDir, hostPath, configMap/secret volumes, projected, ephemeral.* Closed by §1, which covers all five plus `downwardAPI`, `subPath`, `nfs`, and `local`.

**Trap coverage: 7 of 7 D2.4 traps (#63–#69) addressed**, and I verified the Exam Alert table against `domain-analysis.md:571–577` line by line. Order preserved, corrections faithful. The chapter's arithmetic claims about trap distribution (§4's *"five of the seven… four of them are here"*; Bearings #2's *"four of the exam traps… in this checkpoint alone"*) both check out.

---

## Retrieval-practice ledger → `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md`

| Tested topic | Original chapter | Retested in |
|---|---|---|
| The writable container layer; what a restart discards | ch 2 §2 | ch 11 — Bearings #1 Q2 |
| The four pluggable interfaces, as a set | ch 2 §4/§5 | ch 11 — Practice Q12 |
| ServiceAccount token delivered by a projected volume | ch 5 §6 | ch 11 — Practice Q1 |
| StatefulSet ordinal identity | ch 6 §6 | ch 11 — Bearings #3 Q3 ⚠️ thin |
| Filter phase; the unschedulable Pod | ch 7 §2 | ch 11 — Bearings #2 Q3 |
| The absent-component pattern | ch 10 §3 | ch 11 — Practice Q8 |
| ~~PV/PVC scoping~~ | ~~ch 4 §3~~ | ch 11 — Practice Q4 ❌ **half-unsupported, see ⚑B** |

**Compliance: 7 of 32 graded items = 21.9%**, inside B3's 20–25% band and above the outline's own 20% target. **≥4-back floor met with room** — Ch 2 is nine chapters back and carries two items. Soundings are excluded from the budget per B3, though Ch 11's block is unusually load-bearing: six of its eight questions are retrieval from shipped chapters.

**If Practice Q4 is retagged rather than rewritten, the rate drops to 6 of 32 = 18.8% — below band.** That is the argument for rewriting it around Ch 4's own cluster-scoped trio (Node, PersistentVolume, StorageClass), which is a genuine Ch 4 anchor and holds the rate.

**Forward obligations Chapter 11 creates:**

| Topic Ch 11 owns | Must be retrieved in | How |
|---|---|---|
| The `secret` volume on tmpfs | **Ch 12 §4** | Ch 11 hands over half an argument by name: *"File over environment variable is half an argument already, and you now hold that half."* Ch 12 §4 owes the other half. |
| `hostPath` as the workload-to-host hole | **Ch 12 §5** | Ch 11 names and defers explicitly. Also owns the `ReadOnlyMany`-is-not-a-permission-system pointer. |
| An unbound claim as a `Pending` Pod | **Ch 13 §2** | Ch 11 supplies the mechanism, Ch 13 the diagnosis — *"This chapter supplies the mechanism; that one supplies the diagnosis."* |
| Per-replica PVC | **Ch 16 §6** | B6 skeleton line 243 — application-side StatefulSet debugging. |
| CSI as the fourth interface | **Ch 17 §4** | **Collects; does not redefine.** ⚑ two naming conflicts live — see `concepts/pluggable-interfaces.md` before drafting. |
| The absent-component pattern | **Ch 13 §7, Ch 17 §7** | ⚑ **BLOCKED** on the instance-count conflict. Do not draft until resolved. |

**Open gaps carried forward from Chapter 10:** north-south/east-west taught but assessed in zero questions — **still open**, untouched by Ch 11. Ch 9's *"second instance"* wording for CNI — **still open**. Ch 9's eight-section shape vs the B6 skeleton's seven — **resolved in the skeleton** by commit `30c9c48`, but Ch 11 §6's pointer was written against the stale numbering anyway (⚑C).

**One coverage gap Chapter 11 leaves in its own material:** CSI driver architecture — the controller Deployment plus per-node DaemonSet, promised at `chapter-02:600` — is taught in §5 and **tested nowhere**. The chapter's own AUTHOR-REVIEW at the Bearings #3 checkpoint records why: the curriculum-alignment audit's rebalance claimed the last slot for a `volumeClaimTemplates` item, and only one could be seated. Logged rather than absorbed.

---

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===
# Glossary — KCNA

Pipeline-maintained glossary. Format follows skill Part 16 (alphabetical, expansion for
every acronym, cross-reference to the chapter of introduction) so this file can be promoted
to the shipped back-of-book glossary without conversion.

**Provenance rule:** definitions are inherited from the chapter that introduces the term,
verbatim wherever the chapter states one. Where a chapter uses a term without defining it,
the entry says so explicitly and marks itself PROVISIONAL rather than supplying an invented
definition — the fix belongs in the chapter, not here.

> **BACKFILL REQUIRED.** Chapters 1–9 shipped before Stage 14 existed. Their terms are not
> in this file. The B7 term-ownership ledger
> (`.pipeline-state/book-outline/term-ownership.md`) is the authoritative inventory — 19
> chapters of owned vocabulary, an ambient tier, a 74-entry acronym register, and nine
> routed orphans. A backfill pass should walk Ch 1–9 against it.
> **Chapters 10 and 11 below are complete.**

---

## A

**Access mode** — A statement of how a PersistentVolume may be mounted. There are four.
`ReadWriteOnce` (RWO): the volume can be mounted as read-write by a **single node**.
`ReadOnlyMany` (ROX): mounted as read-only by many nodes. `ReadWriteMany` (RWX): mounted as
read-write by many nodes. `ReadWriteOncePod` (RWOP): mounted as read-write by a **single
Pod**. *"A volume can only be mounted using one access mode at a time, even if it supports
many."* A volume access mode **does not enforce write protection**.
`[source: k8s-docs-persistent-volumes-depth-2026-08-25]` (Chapter 11 §4)

*Three of the four count nodes. Only RWOP counts Pods.*

---

## B

**Binding (PersistentVolume/PersistentVolumeClaim sense)** — *"A control loop in the control
plane watches for new PVCs, finds a matching PV (if possible), and binds them together."*
Binds are **exclusive**, and *"a PVC to PV binding is a one-to-one mapping."* An unmatched
claim is not an error: *"Claims will remain unbound indefinitely if a matching volume does
not exist."* `[source: k8s-docs-persistent-volumes-2026-08-23]` (Chapter 11 §2)

> ⚠ **Homonym — B7 canonical forms.** Distinct from **scheduler binding** (Ch 7 §1).
> Neither sense may be written bare outside its own chapter. `RoleBinding` and
> `ClusterRoleBinding` (Ch 12 §3) are object names, always in code style, and are never
> shortened to "binding".

---

## C

**CIDR (Classless Inter-Domain Routing)** — A way of writing a range of IP addresses as an
address plus a prefix length: `172.17.0.0/16` means "the addresses whose first sixteen bits
are those of 172.17.0.0." An `except` list carves ranges back out of the block.
(Chapter 10 §6)

**CSI (Container Storage Interface)** — *"Defines a standard interface for container
orchestration systems (like Kubernetes) to expose arbitrary storage systems to their
container workloads."* `[source: k8s-docs-volumes-csi-and-subpath-2026-08-25]` It allows
vendors *"to create custom storage plugins for Kubernetes without adding them to the
Kubernetes repository (out-of-tree plugins)."*
`[source: k8s-glossary-storage-terms-2026-08-25]` (Chapter 11 §5)

*Not a Kubernetes feature. A cross-orchestrator standard Kubernetes implements — the
specification's own objective is to let vendors "develop a plugin once and have it work
across a number of container orchestration (CO) systems"*
`[source: csi-spec-objective-2026-08-25]`.

**CSI driver** — The software that implements CSI for one storage system. *"A CSI driver is
typically deployed in Kubernetes as two components: a controller component and a per-node
component"* — the controller as a Deployment or StatefulSet, the node component *"on every
node in the cluster through a DaemonSet."*
`[source: kubernetes-csi-docs-deployment-2026-08-25]` **Kubernetes does not install it for
you.** (Chapter 11 §5)

**CSI migration** — *"The `CSIMigration` feature directs operations against existing in-tree
plugins to corresponding CSI plugins (which are expected to be installed and configured)."*
Existing PVs, PVCs and StorageClasses referring to in-tree plugins keep working unchanged;
*"the actual storage management now happens through the CSI driver."*
`[source: k8s-docs-volumes-csi-and-subpath-2026-08-25]` (Chapter 11 §5)

**`CSIDriver`** — The API object installing a driver puts in the cluster. *"CSIDriver
captures information about a Container Storage Interface (CSI) volume driver deployed on the
cluster."* `[source: k8s-api-ref-csidriver-v1-2026-08-25]` (Chapter 11 §5)

> ⚠ **Thin.** One clause quoting an API reference is the whole in-chapter treatment, and the
> term appears as **Practice Q2 option D**. It clears the B7 orphan doctrine only just. If a
> later pass expands §5, this entry should be expanded with it.

**`configMap` / `secret` volume source** — Ways of mounting a ConfigMap or Secret into a
container's filesystem as files. A ConfigMap's data *"can be referenced in a volume of type
`configMap` and consumed as files by the containerized application"*; a `secret` volume lets
you *"store secrets in the Kubernetes API and mount them as files for use by Pods without
coupling to Kubernetes directly."* Both are **always mounted read-only**, and *"`secret`
volumes are backed by tmpfs (a RAM-backed filesystem), so they are never written to
non-volatile storage."*
`[source: k8s-docs-volumes-2026-08-23; k8s-docs-volume-types-depth-2026-08-25]`
(Chapter 11 §1; the objects themselves are Chapter 4 §4)

---

## D

**Default StorageClass** — *"You can mark a StorageClass as the default for your cluster.
When a PVC does not specify a `storageClassName`, the default StorageClass is used."* The
mark is the annotation `storageclass.kubernetes.io/is-default-class: "true"`. A cluster may
have **no** default, in which case a classless PVC *"creates as you defined it, and the
`storageClassName` of that PVC remains unset until a default becomes available."*
`[source: k8s-docs-storage-classes-2026-08-25]` (Chapter 11 §3)

**`downwardAPI` volume** — A volume that makes a Pod's own metadata available to the
application running inside it. *"Within the volume, you can find the exposed data as
read-only files in plain text format."*
`[source: k8s-docs-volume-types-depth-2026-08-25]` (Chapter 11 §1)

**Dynamic provisioning** — *"When none of the static PVs the administrator created match a
user's PersistentVolumeClaim, the cluster may try to dynamically provision a volume
specially for the PVC."* It requires **two** conditions: *"the PVC must request a storage
class and the administrator must have created and configured that class for dynamic
provisioning to occur."* `[source: k8s-docs-persistent-volumes-2026-08-23]` (Chapter 11 §3)

---

## E

**EBS** — A cloud provider's block-storage service, used in this book only as an
illustrative backing store behind a PersistentVolume. (Chapter 11, "Why This Chapter
Matters" and §2)

> ⚠ **PROVISIONAL — no chapter defines or expands this.** Four bare uses in Chapter 11 and
> **zero occurrences across Chapters 1–10**. No row in the B7 acronym register. Chapter 11
> is its first appearance in the book. The commonly reported expansion is *Elastic Block
> Store*; this stage has **not** asserted it as the entry, because no cached source in
> `sources/` attests it and Rule 5 forbids inventing a definition. **Fix: either expand it
> on first use from a sourced snapshot, or replace the three illustrative uses with a
> generic phrase** — the chapter already genericized its named CSI drivers for exactly this
> reason (see the §5 AUTHOR-REVIEW comment).

**`emptyDir`** — A Pod-scoped scratch volume. *"The volume is created when the Pod is
assigned to a node, and as the name says, it is initially empty."* Every container in the
Pod can read and write the same files in it. *"A container crashing does not remove a Pod
from a node,"* so *"the data in an `emptyDir` volume is safe across container crashes"* —
but *"when a Pod is removed from a node for any reason, the data in the `emptyDir` is
deleted permanently."* Two knobs: `medium: "Memory"` mounts a tmpfs, and `sizeLimit` caps
capacity on the default medium. `[source: k8s-docs-volume-types-depth-2026-08-25]`
(Chapter 11 §1)

> Files written to a memory-backed `emptyDir` *"count against the memory limit of the
> container that wrote them."* By default there is **no** size cap at all.

**ENOSPC** — The POSIX error a write returns when no space is left on the device.

> ⚠ **PROVISIONAL — supplied by this stage, not by any chapter.** Appears only as Practice
> Q14 distractor B, unglossed. A distractor a reader cannot look up is a badly built
> distractor. **Fix: gloss it inline in the option or the answer key, or reword the
> distractor in plain language.**

---

## F

**finalizer** — A key on an object that blocks its deletion until the responsible controller
removes the key. Chapter 11 names one — `kubernetes.io/pvc-protection` — without explaining
the mechanism: a PVC in active use *"is not removed immediately. PVC removal is postponed
until the PVC is no longer actively used by any Pods,"* and you *"will see it sitting in
`Terminating` with `kubernetes.io/pvc-protection` in its finalizers list."*
`[source: k8s-docs-persistent-volumes-depth-2026-08-25]` (Chapter 11 §2)

> ⚠ **PROVISIONAL — the chapter names the finalizer but never defines what a finalizer is.**
> The definition above is this stage's, assembled from the observed behavior the chapter
> describes. **Zero occurrences in Chapters 1–10**; no B7 row. **Recommended resolution: add
> to B7's ambient tier or assign a one-clause gloss to Ch 11 §2** — one subordinate clause
> ("a key that blocks deletion until a controller clears it") would close it.

---

## G

**Generic ephemeral volume** — A Pod-scoped volume with persistent-storage machinery behind
it. *"Similar to `emptyDir` volumes in the sense that they provide a per-pod directory for
scratch data that is usually empty after provisioning,"* but *"storage can be local or
network-attached,"* volumes *"can have a fixed size that Pods are not able to exceed,"* and
snapshotting, cloning and resizing are supported where the driver supports them. The Pod
spec carries a PersistentVolumeClaim template inline; *"the ephemeral volume controller then
creates an actual PersistentVolumeClaim object in the same namespace as the Pod and ensures
that the PersistentVolumeClaim gets deleted when the Pod gets deleted."* The PVC's name is
*"a combination of the Pod name and volume name, with a hyphen (-) in the middle."*
`[source: k8s-docs-ephemeral-volumes-2026-08-25]` (Chapter 11 §1)

---

## H

**`hostPath`** — A volume that *"mounts a file or directory from the host node's filesystem
into your Pod."* Takes a required `path` and an optional `type` controlling what Kubernetes
checks before mounting. *"This is not something that most Pods will need, but it offers a
powerful escape hatch for some applications."*
`[source: k8s-docs-volume-types-depth-2026-08-25]` (Chapter 11 §1)

> ⚠ *"Using the `hostPath` volume type presents many security risks. If you can avoid using
> a `hostPath` volume, you should."* See `concepts/hostpath.md`.

---

## I

**In-tree volume plugin** — The pre-CSI arrangement. *"All volume plugins were 'in-tree'.
The 'in-tree' plugins were built, linked, compiled, and shipped with the core Kubernetes
binaries. This meant that adding a new storage system to Kubernetes (a volume plugin)
required checking code into the core Kubernetes code repository."*
`[source: k8s-docs-volumes-csi-and-subpath-2026-08-25]` (Chapter 11 §5)

**iSCSI** — A block-storage protocol. Chapter 11 uses it twice, both inside direct
quotations from Kubernetes documentation: a PersistentVolume *"captures the details of the
implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage
system,"* and *"an iSCSI volume can only be used by one client at a time."*
`[source: k8s-docs-persistent-volumes-2026-08-23; k8s-docs-persistent-volumes-depth-2026-08-25]`
(Chapter 11 §2)

> ⚠ **PROVISIONAL — no chapter defines or expands this.** Zero occurrences in Chapters 1–10;
> no B7 row. Both uses are quoted rather than authored, which lowers the severity but does
> not remove it — the second quotation is load-bearing for the access-mode argument in §4
> (it is the documentation's own example of storage that *cannot* support many writers).
> **Recommended resolution: B7 ambient tier**, alongside HTTP and TLS.

---

## L

**`local` volume** — *"Represents a mounted local storage device such as a disk, partition
or directory."* Unlike `hostPath`, `local` volumes are used *"in a durable and portable
manner without manually scheduling Pods to nodes,"* because *"the system is aware of the
volume's node constraints by looking at the node affinity on the PersistentVolume."* Hard
restriction: *"local volumes can only be used as a statically created PersistentVolume.
Dynamic provisioning is not supported."* If the node becomes unhealthy the volume becomes
inaccessible and the Pod cannot run.
`[source: k8s-docs-volume-types-depth-2026-08-25]` (Chapter 11 §1)

**LUN** — A unit of storage presented by a traditional storage array, which an application
team requests and a storage administrator creates.

> ⚠ **PROVISIONAL — no chapter defines or expands this.** The gloss above is this stage's,
> reconstructed from how Soundings Q5 and its answer use the term. Zero occurrences in
> Chapters 1–10; no B7 row. **This reaches graded material** — Soundings Q5 — and B7's
> orphan doctrine is explicit that *"a term used in question text or an answer key may not
> be glossary-only."* **Fix: expand on first use in the Soundings stem
> (`LUN (Logical Unit Number)`) and add a B7 acronym-register row.** Two words.

---

## N

**NFS** — A network file-sharing protocol. Chapter 11 supplies function, not expansion: an
`nfs` volume *"allows an existing NFS share to be mounted into a Pod,"* and *"unlike
`emptyDir`, which is erased when a Pod is removed, the contents of an `nfs` volume are
preserved, and the volume is merely unmounted."* NFS *"can be mounted by multiple writers
simultaneously."* `[source: k8s-docs-volume-types-depth-2026-08-25]` (Chapter 11 §1)

> ⚠ **PROVISIONAL — the expansion is nowhere in the book.** Nine bare uses in Chapter 11,
> **zero occurrences across Chapters 1–10**, no B7 acronym-register row. **This is the most
> serious of the four unexpanded acronyms**, because it reaches two graded items — Practice
> Q7, whose correct answer depends on NFS supporting many simultaneous writers, and Practice
> Q11, built on the documentation's NFS example. A reader is asked to reason about a
> technology the book has never named in full. **Fix: expand on first use at §1
> (`NFS (Network File System)`) and add a B7 acronym-register row.** Two words.

---

## O

**OSI (Open Systems Interconnection)** — The seven-layer reference model whose layer numbers
this book uses to place network mechanisms. Layer 3 is the IP address level; layer 4 is the
port level; layer 7 is the application-protocol level, where the content of an HTTP request
becomes readable. (Chapter 10 §1)

> ⚠ **PROVISIONAL — chapter fix required.** Chapter 10 uses the bare acronym four times,
> including **Practice Question 1's stem**, and never expands it. The B7 acronym register
> has no `OSI` row — it is expanded only inside the `L4 / L7` row. The definition above is
> supplied by this stage. Fix: expand at Ch 10 §1 and add a register row.

---

## P

**PersistentVolume (PV)** — *"A piece of storage in the cluster that has been provisioned by
an administrator or dynamically provisioned using StorageClasses. It is a resource in the
cluster just like a node is a cluster resource."* The API object *"captures the details of
the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage
system."* Its lifecycle is *"independent of any individual Pod that uses the PV."*
**Cluster-scoped.** `[source: k8s-docs-persistent-volumes-2026-08-23]` (Chapter 11 §2)

> ⚠ **Not the same noun as a `volume`.** A `volume` is a field in a PodSpec. A
> `PersistentVolume` is a cluster-scoped API object with its own name and lifecycle.
> Similar words, different things.

**PersistentVolumeClaim (PVC)** — *"A request for storage by a user."*
`[source: k8s-docs-persistent-volumes-2026-08-23]` A claim *"specifies the amount of
storage, how the storage will be accessed (read-only, read-write and/or exclusive) and how
it is reclaimed (retained, recycled or deleted),"* while *"details of the storage itself are
described in the PersistentVolume object."*
`[source: k8s-glossary-storage-terms-2026-08-25]` **Namespaced**, and *"claims must exist in
the same namespace as the Pod using the claim."*
`[source: k8s-docs-persistent-volumes-depth-2026-08-25]` (Chapter 11 §2)

*A Pod references the claim, never the volume.*

**`persistentVolumeClaimRetentionPolicy`** — *"The optional
`.spec.persistentVolumeClaimRetentionPolicy` field controls if and how PVCs are deleted
during the lifecycle of a StatefulSet."* Two independently settable policies: `whenDeleted`
and `whenScaled`. Each takes `Delete` or `Retain`; **`Retain` is the default for both.**
`[source: k8s-docs-statefulset-storage-2026-08-25]` (Chapter 11 §6)

**PV phase** — Where a PersistentVolume stands in its own lifecycle. The concept
documentation names four: `Available` (provisioned, unclaimed), `Bound` (matched to a
claim), `Released` (the claim is gone; the cluster has not finished with the volume),
`Failed` (automatic reclamation was attempted and did not succeed).
`[source: k8s-docs-persistent-volumes-depth-2026-08-25]` (Chapter 11 §2)

> ⚠ **Source disagreement — do not assert "there are four."** The v1 API reference
> additionally documents a `Pending` phase, *"used for PersistentVolumes that are not
> available"* `[source: k8s-api-ref-persistentvolume-v1-2026-08-25]`. See
> `concepts/pv-phases.md` before restating the count anywhere.

**Projected volume** — *"A `projected` volume maps several existing volume sources into the
same directory."* The four that matter to this book are `secret`, `configMap`,
`serviceAccountToken`, and `downwardAPI`.
`[source: k8s-docs-projected-volumes-2026-08-25]` (Chapter 11 §1; first met, unnamed, at
Chapter 5 §6 delivering a ServiceAccount token)

**Provisioner** — *"Each StorageClass has a provisioner that determines what volume plugin
is used for provisioning PVs. This field must be specified."* Internal provisioners ship
with Kubernetes and carry `kubernetes.io`-prefixed names; external provisioners are
*"independent programs that follow a specification defined by Kubernetes."*
`[source: k8s-docs-storage-classes-2026-08-25]` (Chapter 11 §3)

---

## R

**Reclaim policy** — What happens to a PersistentVolume after its claim is deleted. *"The
reclaim policy for a PersistentVolume tells the cluster what to do with the volume after it
has been released of its claim."* `Retain`: the PV still exists, the volume is *"released,"*
and an administrator must manually reclaim it in three steps. `Delete`: *"removes both the
PersistentVolume object from Kubernetes, as well as the associated storage asset in the
external infrastructure."* `Recycle`: **deprecated**.
`[source: k8s-docs-persistent-volumes-2026-08-23; k8s-docs-persistent-volumes-depth-2026-08-25]`
(Chapter 11 §4)

*Defaults differ by origin: `Retain` for manually created PVs*
`[source: k8s-api-ref-persistentvolume-v1-2026-08-25]`*; `Delete` for dynamically
provisioned ones, inherited from the StorageClass.*

**reverse proxy** — A server that terminates a client's connection at the network edge and
forwards the request onward to a backend on the client's behalf. In this book it is what an
Ingress controller and a Gateway implementation typically are. (First appears Chapter 9;
used substantively Chapter 10 §5)

> ⚠ **PROVISIONAL — no chapter defines this.** Recommended resolution: B7 ambient tier.

---

## S

**SNI (Server Name Indication)** — A field in the TLS handshake carrying the hostname the
client is trying to reach, sent before the encrypted session begins. Chapter 10 describes
its function: *"HTTPS carries an earlier tell in the SNI field of the TLS handshake —
traffic for several hostnames can be multiplexed on a single port that way, where the proxy
terminating TLS supports SNI"* `[source: k8s-docs-ingress-depth-2026-08-24]`.
(Chapter 10 🧭 Soundings answer 1)

> ⚠ **PROVISIONAL — chapter supplies function, not expansion.** Zero occurrences in
> Ch 1–9; no B7 register row. Sits in a Soundings answer, which is graded material.

**Static provisioning** — *"A cluster administrator creates a number of PVs. They carry the
details of the real storage, which is available for use by cluster users."* Supply exists
first; demand arrives later and matches against it.
`[source: k8s-docs-persistent-volumes-2026-08-23]` (Chapter 11 §3)

**Storage Object in Use Protection** — *"The purpose of the Storage Object in Use Protection
feature is to ensure that PersistentVolumeClaims in active use by a Pod and
PersistentVolumes that are bound to PVCs are not removed from the system, as this may result
in data loss."* Deleting an in-use PVC postpones removal until no Pod is using it.
`[source: k8s-docs-persistent-volumes-depth-2026-08-25]` (Chapter 11 §2)

**StorageClass** — *"A StorageClass provides a way for administrators to describe the
classes of storage they offer. Different classes might map to quality-of-service levels, or
to backup policies, or to arbitrary policies determined by the cluster administrators.
Kubernetes itself is unopinionated about what classes represent."* Each contains the fields
`provisioner`, `parameters`, and `reclaimPolicy`. *"The name of a StorageClass object is
significant, and is how users can request a particular class."*
`[source: k8s-docs-storage-classes-2026-08-25]` **Cluster-scoped.** (Chapter 11 §3)

**`subPath`** — Not a volume type but a mount modifier. *"The `volumeMounts[*].subPath`
property specifies a sub-path inside the referenced volume instead of its root."*
`[source: k8s-docs-volumes-csi-and-subpath-2026-08-25]` (Chapter 11 §1)

> ⚠ **A `subPath` mount stops receiving updates.** *"A container using a ConfigMap as a
> `subPath` volume mount will not receive updates when the ConfigMap changes."* The same
> holds for Secrets and the downward API.
> `[source: k8s-docs-volume-types-depth-2026-08-25]`

---

## T

**tmpfs** — A RAM-backed filesystem. Used by `emptyDir` when `medium` is set to `"Memory"`,
and by every `secret` volume, which is why Secrets mounted as files *"are never written to
non-volatile storage."* `[source: k8s-docs-volume-types-depth-2026-08-25]` (Chapter 11 §1)

---

## V

**Volume (the Kubernetes volume)** — A directory declared in a PodSpec and mounted into one
or more of the Pod's containers. *"Volumes exist to solve two problems: surviving container
crashes, and sharing files between containers running in one Pod."* *"For any kind of volume
in a given Pod, data is preserved across container restarts."* Ephemeral volume types have a
lifetime linked to a specific Pod; *"when a Pod ceases to exist, Kubernetes destroys
ephemeral volumes"*, while *"Kubernetes does not destroy persistent volumes."*
`[source: k8s-docs-volumes-2026-08-23]` (Chapter 11 §1)

> ⚠ **Homonym — B7 canonical forms.** A *Docker volume* is a different thing; sense B is not
> used in this book. Where a contrast is needed, write "a Docker volume".

**Volume lifetime ladder** — This book's term for the three storage lifetimes and the two
boundaries between them. Rung one is the container's writable layer, destroyed by a
**container restart**. Rung two is a Pod-scoped (ephemeral) volume, which survives that and
is destroyed when **the Pod ceases to exist**. Rung three is cluster-scoped persistent
storage, which survives both, because nothing in a Pod's lifecycle reaches it.
(Chapter 11 §1 — the book's own framing, not a documented term)

**`volumeBindingMode`** — *"Controls when volume binding and dynamic provisioning should
occur. When unset, `Immediate` mode is used by default."* `Immediate` binds as soon as the
PVC is created. `WaitForFirstConsumer` *"delays the binding and provisioning of a
PersistentVolume until a Pod using the PersistentVolumeClaim is created,"* so the volume is
*"selected or provisioned conforming to the topology that is specified by the Pod's
scheduling constraints."* `[source: k8s-docs-storage-classes-2026-08-25]` (Chapter 11 §3)

**`volumeClaimTemplates`** — A StatefulSet field carrying a PersistentVolumeClaim spec as a
template. *"For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives
one PersistentVolumeClaim."* Claim names are assembled `<template>-<statefulset>-<ordinal>`.
`[source: k8s-docs-statefulset-storage-2026-08-25]` (Chapter 11 §6)

---

*Stage 14 · Chapters 10–11 · 2026-08-25. Ten entries provisional pending chapter-side fixes
recorded in the respective KB manifests.*
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/volume-lifetime-ladder.md ===
# Concept — The volume lifetime ladder

**Definition home:** Ch 11 §1 · **Objective:** D2.4 Storage
**Status:** the book's own framing, not a documented Kubernetes term. Every *fact* in it is
sourced; the *ladder* is ours. Keep that split if a later chapter restates it.
**Figure:** `ch11-fig01-volume-lifetime-ladder`

---

## The structure

**Three lifetimes, two boundaries.** The count is exactly three; do not let a later chapter
grow it.

| Rung | What it is | Destroyed by |
|---|---|---|
| 1 | The container's writable layer | **a container restart** |
| 2 | A Pod-scoped (ephemeral) volume | **the Pod ceasing to exist** |
| 3 | Cluster-scoped persistent storage | nothing in a Pod's lifecycle reaches it |

Sourced anchors, one per rung:

- Rung 1 — the restarted container *"gets a clean state"* assembled fresh from the image
  `[source: k8s-docs-volumes-2026-08-23]`
- Rung 2 — *"for any kind of volume in a given Pod, data is preserved across container
  restarts"*, but *"when a Pod ceases to exist, Kubernetes destroys ephemeral volumes"*
  `[source: k8s-docs-volumes-2026-08-23]`
- Rung 3 — *"Kubernetes does not destroy persistent volumes"*
  `[source: k8s-docs-volumes-2026-08-23]`

## Why it is the chapter's spine

Every storage question in Kubernetes is a question about which rung you are standing on. The
chapter's Zenith (§7) is the observation that the same shape recurs one scope out: *does the
claim survive the workload? does the data survive the claim?*

## The misconception it exists to kill

**"It survived the restart, so it is persistent."** This is the single most common
`emptyDir` error and it is what rung two is for: the volume survives **one** boundary and
not the other. Ch 11 Bearings #1 Q1 is built on it, with option C as the trap.

The inverse error is worth knowing too, because it looks like knowledge: **"restart means
fresh everything."** True of the container filesystem, false of the volume. Bearings #1 Q1
option D has the ladder exactly inverted and is the more instructive miss.

## Boundary discipline for later chapters

- **Ch 13 §2** (Pods that never start) may use the ladder to explain data loss on a restart
  loop. It owns the *diagnosis*; this chapter owns the *mechanism*.
- **Ch 16 §6** may use it for per-replica state. Refer; do not redraw.
- Any figure must show the boundaries as **containment**, not as arrows. The shipped figure
  nests three boxes and marks the two boundaries as lines that data below is discarded at.
  A flow diagram would imply the data moves; it does not — it stops existing.

## See also

[[volume-types-ephemeral]] · [[persistentvolume-and-claim]] · [[hostpath]] · [[subpath]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/volume-types-ephemeral.md ===
# Concept — Pod-scoped (rung-two) volume types

**Definition home:** Ch 11 §1 · **Objective:** D2.4 Storage — **closes research gap G12**
**Sources:** `k8s-docs-volumes-2026-08-23`, `k8s-docs-volume-types-depth-2026-08-25`,
`k8s-docs-projected-volumes-2026-08-25`, `k8s-docs-ephemeral-volumes-2026-08-25`

---

Nearly every volume type on the KCNA horizon lives on rung two of
[[volume-lifetime-ladder]]: its lifetime is the Pod's.

## `emptyDir`

Created when the Pod is assigned to a node; **initially empty**. Shared by every container
in the Pod — this is the shared-filesystem half of what Ch 5 §1 said a Pod's containers have
in common.

- Safe across container crashes: *"a container crashing does not remove a Pod from a node."*
- *"When a Pod is removed from a node for any reason, the data in the `emptyDir` is deleted
  permanently."*
- `medium: "Memory"` → tmpfs. **Files written count against the writing container's memory
  limit.** A process that fills it gets OOM-killed.
- `sizeLimit` caps the default medium. **By default there is no cap at all** — *"there is no
  limit on how much space an `emptyDir` or `hostPath` volume can consume, and no isolation
  between containers or Pods."*

## `configMap` / `secret` as volume sources

The objects are Ch 4 §4; the *mounting* is here. Both **always read-only**. The one detail
that carries forward: *"`secret` volumes are backed by tmpfs… so they are never written to
non-volatile storage."*

⚠ **Forward obligation — Ch 12 §4** owes the other half of the file-versus-environment-
variable argument. Ch 11 says so explicitly and hands over half of it.

## `projected`

*"Maps several existing volume sources into the same directory."* Four sources matter:
`secret`, `configMap`, `serviceAccountToken`, `downwardAPI`.

The reader already used one without being told what it was — Ch 5 §6's ServiceAccount token
arrived by a projected token volume. **Teach it as the general case of a mechanism already
met**, not as a new type.

*Trimmed deliberately:* the snapshot enumerates six sources, adding `clusterTrustBundle` and
`podCertificate`. Both were dropped on the curriculum-alignment stage's recommendation — they
appear nowhere else in the book and are not KCNA material. Restore only with a reason.

## `downwardAPI`

A Pod's own metadata as *"read-only files in plain text format."*

## Generic ephemeral volume

The hybrid, and the one most likely to send a reader back to the ladder. Rung-two behavior
built out of rung-three machinery: the PodSpec carries a PVC template inline, and *"the
ephemeral volume controller then creates an actual PersistentVolumeClaim object in the same
namespace as the Pod and ensures that the PersistentVolumeClaim gets deleted when the Pod
gets deleted."* Name = Pod name + volume name, hyphenated.

⚠ **Keep the contrast with [[statefulset-storage]] intact.** Two mechanisms, both producing
one claim per Pod, with **exactly opposite deletion behavior**. Ch 11 Practice Q17 option D
and Q10 option D are both built on it. A later chapter that blurs them invalidates two
graded items.

## Rung-three teasers named in §1

- **`nfs`** — *"unlike `emptyDir`, which is erased when a Pod is removed, the contents of an
  `nfs` volume are preserved, and the volume is merely unmounted."* Can be *"mounted by
  multiple writers simultaneously"* — this is load-bearing for [[access-modes]].
- **`local`** — node-aware via PV node affinity, unlike [[hostpath]]. **Static PVs only;
  dynamic provisioning is not supported.** Node unhealthy → Pod cannot run.

## Glossary dependency

**NFS is used nine times and never expanded**, and it carries Practice Q7 and Q11. See the ⚠
entry in `glossary.md`.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/hostpath.md ===
# Concept — `hostPath` and the workload-to-host boundary

**Definition home:** Ch 11 §1 · **Objective:** D2.4 Storage, with a D2.2 Security edge
**Forward obligation:** **Ch 12 §5 — what a Pod may do to its node.** Ch 11 names the
problem, states the documented warning, and defers the apparatus. Ch 12 §5 must collect it.
**Source:** `k8s-docs-volume-types-depth-2026-08-25`

---

## What it is

*"Mounts a file or directory from the host node's filesystem into your Pod."* Required
`path`, optional `type` controlling pre-mount checks (must exist / must be a directory / may
be created / must be a socket).

*"This is not something that most Pods will need, but it offers a powerful escape hatch for
some applications."*

## The warning, verbatim and unhedged

> *"Using the `hostPath` volume type presents many security risks. If you can avoid using a
> `hostPath` volume, you should."*

**Why is more instructive than that.** *"Access to the host filesystem can expose privileged
system credentials (such as for the kubelet) or privileged APIs (such as the container
runtime socket) that can be used for container escape or to attack other parts of the
cluster."*

Concretely: a Pod that can read `/var/lib/kubelet` reads the node's credentials. A Pod that
can write to the container runtime socket starts a privileged container of its own choosing.

**Read-only is not automatic and not sufficient by itself.** Restricting access to specific
host directories through admission-time validation *"only"* holds if those mounts are
*"additionally required to be read-only"*; give an untrusted Pod a read-write mount and its
containers may subvert the restriction.

## The second-order problem — the one that bites in production

*"Pods with identical configuration (such as created from a PodTemplate) may behave
differently on different nodes due to different files on the nodes."*

A `hostPath` mount silently makes Pods **node-dependent**. The replica that works and the
replica that does not are running the same image. This is the failure mode that survives an
exam and shows up in a postmortem.

## The recommended alternative

A **`local` PersistentVolume**, because *"the system is aware of the volume's node
constraints by looking at the node affinity on the PersistentVolume."* `hostPath` provides
no such awareness. Ch 11 Practice Q9 option D is built on exactly this distinction.

## Constraints on later chapters

- **Ch 12 §5 must not re-derive the risk.** It is stated here in the documentation's own
  words. Ch 12 owns the *apparatus* — what polices the boundary — not the *hazard*.
- Ch 12 §4 may reuse the "credentials on disk" framing when it argues Secrets-as-files
  against Secrets-as-environment-variables. See [[volume-types-ephemeral]].
- Never illustrate `hostPath` as a blocked or forbidden mount. It is permitted, ordinary, and
  occasionally correct. The hazard is what it *grants*, not that it fails.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/subpath.md ===
# Concept — `subPath` cuts the update wire

**Definition home:** Ch 11 §1 · **Objective:** D2.4 Storage
**Closes a debt from Ch 4 §4** — see below. **A Ch 4 retrofit needs to find this file.**
**Sources:** `k8s-docs-volumes-csi-and-subpath-2026-08-25`,
`k8s-docs-volume-types-depth-2026-08-25`

---

## The mechanism

Not a volume type — a **mount modifier**. *"Sometimes, it is useful to share one volume for
multiple uses in a single Pod. The `volumeMounts[*].subPath` property specifies a sub-path
inside the referenced volume instead of its root."*

One PVC, mounted into a MySQL container at its `mysql` subdirectory and a PHP container at
its `html` subdirectory: two containers, two mount points, one underlying volume.

## The rule that is actually examined

> **A `subPath` mount stops receiving updates.**

Three flat statements, no conditions attached:

- *"A container using a ConfigMap as a `subPath` volume mount will not receive updates when
  the ConfigMap changes."*
- *"A container using a Secret as a `subPath` volume mount will not receive Secret updates."*
- *"A container using the downward API as a `subPath` volume mount does not receive updates
  when field values change."*

Shipped mnemonic: **`subPath` cuts the wire.** A whole-volume mount stays connected to the
object that feeds it; a `subPath` mount takes a snapshot of one path and stops listening.

**Nothing errors.** The rolling ConfigMap update simply does nothing, which is worse than a
failure, because it is silent. Ch 11 Practice Q5 option D exists to reject the "it errors"
guess.

## ⚑ The Ch 4 debt, and a wording defect in how Ch 11 describes it

Ch 4 §4 pointed forward to this exception by name. **Ch 11 §1 characterizes that hand-off as
a hedge — "Chapter 4 hedged that a mounted ConfigMap picks up changes" — and Ch 4 did not
hedge.** `chapter-04:762` states the rule flatly and sourced: *"a container using a ConfigMap
as a `subPath` volume mount will not receive updates at all."*

**Ownership is correct** — B7 assigns `subPath` to Ch 11 §1 — so the duplication is Ch 4
leaning forward, not Ch 11 overreaching. Only the word "hedged" is inaccurate. One-word fix.

**More useful for a retrofit:** `chapter-04:761` carries a RESEARCH GAP comment noting the
auto-update claim was uncited when Ch 4 shipped. **The `subPath` half of it is now sourced
here** to `k8s-docs-volume-types-depth-2026-08-25`. Any Ch 4 retrofit should take that tag.

## See also

[[volume-types-ephemeral]] · [[volume-lifetime-ladder]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/persistentvolume-and-claim.md ===
# Concept — PersistentVolume, PersistentVolumeClaim, and binding

**Definition home:** Ch 11 §2 · **Objective:** D2.4 Storage
**B1 places this three-way distinction (with StorageClass) at the centre of the competency.**
**Figure:** `ch11-fig02-pv-pvc-storageclass-binding`
**Sources:** `k8s-docs-persistent-volumes-2026-08-23`,
`k8s-docs-persistent-volumes-depth-2026-08-25`, `k8s-glossary-storage-terms-2026-08-25`

---

## The proportion that organizes everything

> **Pods consume node resources and PVCs consume PV resources.**

Four terms, exact parallel. A Pod does not create CPU; it requests some and the scheduler
finds a node. A PVC does not create storage; it requests some and a control loop finds a PV.

## Supply and demand

| | PersistentVolume | PersistentVolumeClaim |
|---|---|---|
| Is | **supply** — *"a piece of storage in the cluster"* | **demand** — *"a request for storage by a user"* |
| Scope | **cluster-scoped** | **namespaced** |
| Created by | an administrator, or a provisioner | a user |
| Carries | the real storage's implementation details | a size, an access mode, a reclaim expectation |

*"Details of the storage itself are described in the PersistentVolume object."* A claim says
*how much* and *how*. It does not say *which array*.

**The scoping is derived, not arbitrary.** Supply is a cluster-wide resource like a node; it
belongs to no team. Demand belongs to a specific application in a specific namespace. And
the namespace is load-bearing at consumption time: *"claims must exist in the same namespace
as the Pod using the claim."*

## The routing fact — the highest-value sentence in the section

> **A Pod references the claim, never the volume.**
>
> *"Pods use claims as volumes. The cluster inspects the claim to find the bound volume and
> mounts that volume for a Pod."*

This is what lets one manifest work on a cluster backed by EBS and a cluster backed by Ceph
without changing a character. **Trap #64 is the reversal of it.**

## ⚑ Attribution defect a later chapter must not inherit

Ch 11 §2 says *"Chapter 4 taught you that a PersistentVolume is cluster-scoped while a
PersistentVolumeClaim is namespaced."* **`chapter-04` contains zero occurrences of
"PersistentVolumeClaim"** — verified. Ch 4 §3 names Nodes, PersistentVolumes and
StorageClasses as its cluster-scoped examples; the PV half is solid, the PVC half is new in
Ch 11. **Practice Q4's `[retrieval: ch4]` tag is misaligned on the same root cause.** See
`retrieval-log.md`.

## Binding

*"A control loop in the control plane watches for new PVCs, finds a matching PV (if
possible), and binds them together."* Naming it as a control loop is free retrieval on the
book's spine concept (Ch 3 §6) — there is no separate storage subsystem, just a controller
doing what controllers do.

Two properties, both counter-intuitive **in the same direction**: readers expect binding to
be looser than it is.

1. **Exclusive and one-to-one.** *"A PVC to PV binding is a one-to-one mapping."* A 50Gi PV
   satisfying a 20Gi claim has **no** leftover 30Gi for anyone else. **Trap #63.**
2. **An unmatched claim waits forever.** *"Claims will remain unbound indefinitely if a
   matching volume does not exist."* Not an error, not a timeout, not an alertable event.
   The claim sits and the Pod stays `Pending`.

**Capacity is one filter among several.** A claim may also constrain by `storageClassName`,
by label selector (`matchLabels` and `matchExpressions` **ANDed together**, reusing the Ch 4
§5 selector grammar), and by `volumeName` naming a specific PV. "Big enough, so it fits" is
the reasonable wrong answer — Ch 11 Practice Q13 exists for it.

## Storage Object in Use Protection

Kubernetes will not pull storage out from under a running Pod. Deleting an in-use PVC leaves
it `Terminating` with `kubernetes.io/pvc-protection` in its finalizers; *"PVC removal is
postponed until the PVC is no longer actively used by any Pods."* If you have watched
`kubectl delete pvc` hang, this is why.

⚠ **"finalizer" is used here and never defined.** See `glossary.md`.

## Constraints on later chapters

- **Ch 13 §2** owns the *diagnosis*: from the Pod's point of view an unbindable claim is
  indistinguishable from a scheduling failure. Ch 11 supplies the mechanism.
- Any figure must terminate the Pod's line **at the claim**. A line from Pod to PV
  contradicts the section's Fixed Point.

## See also

[[pv-phases]] · [[storageclass-and-provisioning]] · [[access-modes]] · [[reclaim-policies]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pv-phases.md ===
# Concept — PersistentVolume phases

**Definition home:** Ch 11 §2 · **Objective:** D2.4 Storage
**Status:** ⚑ **LIVE SOURCE DISAGREEMENT — do not assert a count.**

---

## The four the teaching documentation names

| Phase | Meaning |
|---|---|
| `Available` | Provisioned, and no claim has taken it |
| `Bound` | Matched to a claim, and spoken for by that claim alone |
| `Released` | The claim is gone; the cluster has not yet finished with the volume |
| `Failed` | Automatic reclamation was attempted and did not succeed |

`[source: k8s-docs-persistent-volumes-depth-2026-08-25]`

## ⚑ The disagreement

The **v1 API reference** additionally documents a **`Pending`** phase, *"used for
PersistentVolumes that are not available"*
`[source: k8s-api-ref-persistentvolume-v1-2026-08-25]`. The cached depth snapshot flags the
disagreement against itself.

**How Ch 11 handles it, and the handling is the canon:** teach the four — they describe the
free → bound → released arc the chapter is built on — but tell the reader that if `Pending`
turns up as an option, **do not eliminate it on the grounds that no such phase exists.**
It exists. It is simply not one of the four the teaching documentation walks through.

**Do not "fix" this by asserting a number.** The chapter's table paraphrases rather than
quotes, per the snapshot's own retrieval note, and the ⚠ hedge is a 🪝 Snag in §2 rather than
buried in the summary — deliberately, so the summary is not where the reader first meets
`Pending`.

**Open research gap:** a further retrieval of `/docs/concepts/storage/persistent-volumes/#phase`
would settle the count and also clear the `Released`/`Failed` prose for direct quotation.
Until then, paraphrase.

## The examinable fact underneath the count

> **`Released` is not `Available`.**

A volume whose claim has been deleted has *left* the bound state without *entering* the free
state. Nothing binds to it. Making it reusable takes three manual steps and produces a
**new** PV object — see [[reclaim-policies]]. **Trap #67.**

`Failed` is a **storage-lifecycle** outcome, not a scheduling one. Ch 11 Bearings #2 Q3
option D exists to reject the reader who reaches for `Failed` to describe an unschedulable
Pod's claim.

## See also

[[persistentvolume-and-claim]] · [[reclaim-policies]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/storageclass-and-provisioning.md ===
# Concept — StorageClass, provisioning, and `volumeBindingMode`

**Definition home:** Ch 11 §3 · **Objective:** D2.4 Storage
**Figure:** `ch11-fig03-static-vs-dynamic-provisioning`
**Sources:** `k8s-docs-storage-classes-2026-08-25`, `k8s-docs-persistent-volumes-2026-08-23`,
`k8s-docs-persistent-volumes-depth-2026-08-25`

---

## What a StorageClass is

*"A StorageClass provides a way for administrators to describe the classes of storage they
offer… Kubernetes itself is unopinionated about what classes represent."*

That last clause does real work. Kubernetes does not know what `fast` means. It knows that
is a name an administrator chose and attached to a provisioning configuration.

The problem statement, from the PV documentation: administrators need to *"offer a variety
of PersistentVolumes that differ in more ways than size and access modes, **without exposing
users to the details of how those volumes are implemented**."*

**The name is the API.** *"The name of a StorageClass object is significant, and is how users
can request a particular class."* A developer writing `storageClassName: low-latency` is
using that name as the entire interface to a system they know nothing else about.

Fields: `provisioner` (**must be specified**), `parameters` (a **passthrough** — meaningful
to the provisioner, opaque to Kubernetes), `reclaimPolicy`.

## Two ways a volume comes to exist

- **Static** — *"A cluster administrator creates a number of PVs. They carry the details of
  the real storage."* Supply first, demand later.
- **Dynamic** — *"When none of the static PVs the administrator created match a user's
  PersistentVolumeClaim, the cluster **may** try to dynamically provision a volume specially
  for the PVC."*

**That "may" is precise, and the two conditions are the Fixed Point:**

> *"This provisioning is based on StorageClasses: the PVC must request a storage class
> **and** the administrator must have created and configured that class for dynamic
> provisioning to occur."*

One without the other is a claim that waits forever — not an error, not a timeout, not a
failure event. Silence.

## The default class, and the opt-out that catches people

| What the PVC has | What happens |
|---|---|
| No `storageClassName` field at all | The default StorageClass is used, if one exists |
| `storageClassName: ""` | Dynamic provisioning is **disabled for that claim** |

*"Claims that request the class `""` effectively disable dynamic provisioning for
themselves."* Such a claim binds **only** to a PV whose class is also empty. **Trap #69**, and
it is an opt-out, not a shrug.

A cluster may have **no** default at all, in which case a classless PVC is not rejected — it
*"creates as you defined it, and the `storageClassName` of that PVC remains unset until a
default becomes available."* If a default appears later, the control plane retroactively
updates the waiting PVCs. A control loop doing exactly what control loops do.

⚠ **Do not turn the default class into a precondition for provisioning.** A claim naming
`fast` provisions against `fast` whether or not any class is marked default. Ch 11 Practice
Q6 option D exists to reject that conflation.

## `volumeBindingMode` — the scheduling join

*"Controls when volume binding and dynamic provisioning should occur. When unset,
`Immediate` mode is used by default."*

`Immediate` binds as soon as the PVC exists, which for topology-constrained storage
*"may result in unschedulable Pods."* `WaitForFirstConsumer` *"delays the binding and
provisioning of a PersistentVolume until a Pod using the PersistentVolumeClaim is created,"*
after which volumes are *"selected or provisioned conforming to the topology that is
specified by the Pod's scheduling constraints. These include, but are not limited to,
resource requirements, node selectors, pod affinity and anti-affinity, and taints and
tolerations."*

**That list is Ch 7 §2's filter phase item for item.** Scheduling and storage placement are
not two decisions that interact; they are one decision, and making them separately produces
a Pod that cannot run.

**Depth note, and preserve it.** Ch 11 marks this 🔭 Closer Look — above what this book's
reading of the KCNA Storage competency requires. What a later chapter should carry forward is
**the consequence, not the field name**: *volume binding can wait on scheduling, because
binding a volume before the scheduler has picked a node can bind it somewhere the Pod cannot
go.* A reader who remembers that sentence and forgets `volumeBindingMode` has taken the right
thing.

Two operational notes: support is per-plugin (*"CSI volumes, provided that the specific CSI
driver supports this"*), and it breaks if you bypass the scheduler — *"if `nodeName` is used
in this case, the scheduler will be bypassed and PVC will remain in `pending` state."*

## The absent-component instance

A StorageClass is a **description of a provisioning capability**, not the capability. Name a
provisioner nobody deployed and you get a valid API object that provisions nothing. See
[[absent-component-pattern]] — ⚑ **the instance numbering is contested; read that shard
before drafting Ch 13 §7.**

## Deliberately out of scope

`allowVolumeExpansion` and `mountOptions` appear in the shipped example manifest and get no
treatment. That is a decision, not an oversight — the example is a real StorageClass rather
than a trimmed one, and nothing later depends on those fields. **Do not gloss
`allowVolumeExpansion` without a source**; the sentence a prior audit proposed
(*"you can only use the volume expansion feature to grow a Volume, not to shrink it"*) is not
attested in any cached snapshot.

## See also

[[persistentvolume-and-claim]] · [[reclaim-policies]] · [[csi]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/access-modes.md ===
# Concept — Access modes

**Definition home:** Ch 11 §4 · **Objective:** D2.4 Storage
**Figure:** `ch11-fig04-access-modes-and-reclaim-policies` (left panel)
**Source:** `k8s-docs-persistent-volumes-depth-2026-08-25`
**Exam weight:** carries **trap #65**, which Ch 11 identifies as the chapter's single
highest-yield fact.

---

## The four

| Mode | CLI | Unit | Meaning |
|---|---|---|---|
| `ReadWriteOnce` | RWO | **node** | mounted read-write by a single node |
| `ReadOnlyMany` | ROX | **nodes** | mounted read-only by many nodes |
| `ReadWriteMany` | RWX | **nodes** | mounted read-write by many nodes |
| `ReadWriteOncePod` | RWOP | **Pod** | mounted read-write by a single Pod |

## The Fixed Point

> **RWO counts nodes. RWOP is the one that counts Pods.**
>
> *"ReadWriteOnce access mode still can allow multiple Pods to access the volume when the
> Pods are running on the same node. For single Pod access, use ReadWriteOncePod."*

**The existence of a fourth mode devoted entirely to the Pod/node distinction is itself the
evidence that the distinction is hard to hold.** Kubernetes shipped a whole access mode
because people kept assuming RWO already meant it. That argument is the most durable form of
the fact and should survive any restatement.

Shipped mnemonic: **read the last word as the unit.** Three modes leave the unit implicit
and one spells it out; the one that spells it out is the one that differs.

## Why the unit is the node

Not a Kubernetes fact, and **Ch 11 labels it as such**: two independent filesystem drivers,
each caching metadata for the same block device, will overwrite each other's bookkeeping.
Ordinary storage knowledge the platform inherits from the hardware. A clustered filesystem
exists to coordinate exactly that.

⚠ **Preserve the provenance split.** *"That is not a Kubernetes fact, and no Kubernetes
document will tell you so."* Do not promote it to a sourced claim downstream.

## Two facts that are easy to state and easy to forget

1. **One mode at a time.** *"A volume can only be mounted using one access mode at a time,
   even if it supports many. For example, a NFS volume can be mounted as ReadWriteOnce on one
   node and read-only on another node at the same time, but not on the same node for both
   read-write and read-only."* Ch 11 Practice Q11 is the documentation's exact counterexample.
2. **It is not a permission system.** *"A volume access mode does not enforce write
   protection. For example, if you provision a ReadOnlyMany volume, it does not prevent an
   application from writing to the mounted volume if the Pod's securityContext allows write
   access."* ⚠ Forward pointer to **Ch 12 §5**.

## Capability, not policy

*"A PersistentVolume can have any access mode supported by the resource provider. For
example, NFS can support multiple read/write clients, but an iSCSI volume can only be used by
one client at a time."* An access mode is something the storage **has**, not something you
choose for it.

## See also

[[reclaim-policies]] (the other half of the same question) · [[persistentvolume-and-claim]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/reclaim-policies.md ===
# Concept — Reclaim policies, and where the decision was made

**Definition home:** Ch 11 §4 · **Objective:** D2.4 Storage
**Figure:** `ch11-fig04-access-modes-and-reclaim-policies` (right panel)
**Exam weight:** carries **traps #66, #67, #68**.
**Sources:** `k8s-docs-persistent-volumes-2026-08-23`,
`k8s-docs-persistent-volumes-depth-2026-08-25`, `k8s-docs-storage-classes-2026-08-25`,
`k8s-api-ref-persistentvolume-v1-2026-08-25`

---

## The three

| Policy | PV object | Backing asset | Data |
|---|---|---|---|
| `Retain` | kept | kept | kept |
| `Delete` | destroyed | destroyed | destroyed |
| `Recycle` | **deprecated** | — | — |

*"The reclaim policy for a PersistentVolume tells the cluster what to do with the volume
after it has been released of its claim."*

## `Retain` means kept and **stuck**, not kept and reusable

*"When the PersistentVolumeClaim is deleted, the PersistentVolume still exists and the volume
is considered 'released'. But it is not yet available for another claim because the previous
claimant's data remains on the volume."*

The documented manual sequence:

1. Delete the PersistentVolume. The storage asset still exists.
2. Manually clean up the data on the associated storage asset.
3. Manually delete the associated storage asset.

And: *"If you want to reuse the same storage asset, create a **new** PersistentVolume with
the same storage asset definition."* The released one never returns to `Available` on its
own. **Trap #67.**

## `Recycle`

Deprecated. *"The recommended approach is to use dynamic provisioning."* Where still
supported it *"performs a basic scrub (`rm -rf /thevolume/*`)."* On an exam it is a name to
recognize and correctly identify as retired. **Trap #68.**

## ★ The inherited default — the chapter's answer to its own opening question

> *"Volumes that were dynamically provisioned inherit the reclaim policy of their
> StorageClass, which defaults to `Delete`."*
>
> And from the class's side: *"If no `reclaimPolicy` is specified when a StorageClass object
> is created, it will default to `Delete`."*

Follow the chain: no `storageClassName` → default class applies → that class set no
`reclaimPolicy` → `Delete` → the volume inherits it → deleting the PVC destroys the disk.

**Nobody in that story made a decision about the data's survival.** It was settled once, in a
StorageClass manifest, by an administrator configuring a cluster who had never heard of the
application. The documentation puts it mildly: *"the administrator should configure the
StorageClass according to users' expectations."*

**Trap #66**, and the safe assumption is the opposite of the intuitive one.

## The two defaults are opposite, and that is correct

- **Manually created PVs default to `Retain`**
  `[source: k8s-api-ref-persistentvolume-v1-2026-08-25]`
- **Dynamically provisioned volumes inherit the class's, defaulting to `Delete`**

Not an inconsistency. If an administrator hand-built a PV pointing at a real NFS export,
deleting the API object should not scrub the export. If a provisioner created a volume on
demand for one claim, cleaning it up when the claim is gone is the point of creating it on
demand. **The defaults differ because the situations differ** — keep that reasoning attached
whenever the two defaults are stated together, or the pair reads as an API inconsistency.

## The through-line worth carrying

Every one of traps #66–#68 is **a wrong guess about a default someone else set**. That is
what makes them dangerous rather than merely wrong: you cannot catch them by reading your own
manifest, because they were settled in somebody else's.

Operational line the chapter gives the reader: `kubectl get storageclass` takes two seconds.

## See also

[[access-modes]] · [[storageclass-and-provisioning]] · [[pv-phases]] · [[statefulset-storage]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/csi.md ===
# Concept — CSI (Container Storage Interface)

**Definition home:** Ch 11 §5 · **Objective:** D2.4 Storage — **closes research gap G11**
**Collected at Ch 17 §4** — see [[pluggable-interfaces]] before drafting that section.
**Sources:** `k8s-docs-volumes-csi-and-subpath-2026-08-25`, `k8s-docs-volumes-2026-08-23`,
`k8s-glossary-storage-terms-2026-08-25`, `csi-spec-objective-2026-08-25`,
`kubernetes-csi-docs-deployment-2026-08-25`, `k8s-api-ref-csidriver-v1-2026-08-25`

---

## Definition

*"The Container Storage Interface (CSI) defines a standard interface for container
orchestration systems (like Kubernetes) to expose arbitrary storage systems to their
container workloads."*

Consequence: *"CSI allows vendors to create custom storage plugins for Kubernetes without
adding them to the Kubernetes repository (out-of-tree plugins)"* — vendors can introduce new
storage systems *"without ever having to edit the core Kubernetes code."*

## ★ The framing that matters more than the definition

> CSI exists to *"define an industry standard 'Container Storage Interface' (CSI) that will
> enable storage vendors (SP) to develop a plugin once and have it work **across a number of
> container orchestration (CO) systems**"* `[source: csi-spec-objective-2026-08-25]`.

**CSI is not a Kubernetes feature that vendors happen to use. It is a cross-orchestrator
standard that Kubernetes happens to implement** — the same shape as OCI at the image and
runtime boundary. Sourcing this to the *specification* rather than to Kubernetes
documentation is deliberate and should be preserved: the point is that the contract's other
party is not Kubernetes.

## Why it exists

*"Previously, all volume plugins were 'in-tree'. The 'in-tree' plugins were built, linked,
compiled, and shipped with the core Kubernetes binaries. This meant that adding a new storage
system to Kubernetes (a volume plugin) required checking code into the core Kubernetes code
repository."*

⚠ **Provenance split, and Ch 11 labels it in reader-facing text.** The documentation records
the arrangement; it does **not** record what it cost the people inside it. The consequences
Ch 11 draws — vendors shipping on Kubernetes' release schedule, maintainers carrying code for
hardware they could not test — are **the book's reading**, explicitly flagged as such. Do not
promote them to sourced claims.

FlexVolume was the earlier attempt and is superseded: *"using an out-of-tree CSI driver is
the recommended way to integrate external storage with Kubernetes."*

## What a driver is, concretely

*"A CSI driver is typically deployed in Kubernetes as two components: a controller component
and a per-node component."* The controller *"can be deployed as a Deployment or StatefulSet
on any node in the cluster"*; the node component *"should be deployed on every node in the
cluster through a DaemonSet."*

**A CSI driver is not exotic infrastructure. It is a Deployment and a DaemonSet running
software somebody else wrote.** The shape is recognizable without further explanation:
cluster-wide operations in one controller, node-local mounts in one agent per node.

Installing one also creates a `CSIDriver` object, which *"captures information about a
Container Storage Interface (CSI) volume driver deployed on the cluster."*

⚠ **Coverage gap:** the two-component driver architecture — promised by name at
`chapter-02:600` — is **taught in §5 and tested in no graded item**. The checkpoint slot it
would have used was claimed by a `volumeClaimTemplates` item during the curriculum rebalance.
Logged in `retrieval-log.md`; the Practice set is the right home if a slot is found.

## The ordering requirement

*"To use a CSI driver from a storage provider, you must **first** deploy it to your cluster.
You will then be able to create a Storage Class that uses that CSI driver."*

And bluntly: *"**The core of Kubernetes does not install that software for you.**"*

See [[absent-component-pattern]] — ⚑ instance numbering contested.

## CSI is an interface, not a product

There is no "CSI storage" to buy, any more than there is "CNI networking." What you deploy is
a **driver**, written by whoever owns the storage it speaks to. A question treating CSI as a
storage system rather than as the interface storage systems implement is testing exactly this
confusion.

**Named driver examples were deliberately removed** from the shipped chapter — no cached
snapshot enumerates driver implementations. Open research gap: the `kubernetes-csi` drivers
list. Do not reintroduce named drivers without it.

## CSI migration (above KCNA depth — 🔭)

*"The `CSIMigration` feature directs operations against existing in-tree plugins to
corresponding CSI plugins."* The compatibility promise is unusually strong: existing PVs
*"can still be used in the future without any configuration changes… even after you upgrade
to a version of Kubernetes that doesn't have compiled-in support for that kind of storage."*
Manifests keep working; the machinery underneath was replaced.

Operations CSI covers: *"provisioning/delete, attach/detach, mount/unmount, and resizing of
volumes"* — the storage lifecycle, mapping cleanly onto §2–§4.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/statefulset-storage.md ===
# Concept — StatefulSet storage: `volumeClaimTemplates` and per-Pod claims

**Definition home:** Ch 11 §6 · **Objective:** D2.4 Storage
**Closes the book's one deliberate forward reference** (Ch 6 §6). Reciprocal pair — **neither
half redefines the other.**
**Figure:** `ch11-fig05-statefulset-pvc-pairing`
**Sources:** `k8s-docs-statefulset-storage-2026-08-25`, `k8s-docs-statefulset-2026-08-24`

---

## Ch 6's five deferred verbs, all closed

Ch 6 §6 said outright it was deferring how a StatefulSet's storage is *provisioned,
requested, sized, reclaimed, or shared*, and that the deferral was deliberate.

| Verb | Closed at |
|---|---|
| provisioned | Ch 11 §3 — statically, or dynamically by a provisioner named in a StorageClass |
| requested | Ch 11 §2 — by a PersistentVolumeClaim |
| sized | Ch 11 §2 — the claim requests capacity; binding matches it |
| reclaimed | Ch 11 §4 — by the reclaim policy, inherited from the class for dynamic volumes |
| shared | Ch 11 §4 — by the access mode |

**What Ch 6 kept and still owns is identity.** Ch 11 §6 joins the two halves; it does not
restate Ch 6's material.

## The rule

> **For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one
> PersistentVolumeClaim.**

**One claim per Pod *per template*** — not one claim per Pod, and not one claim for the set.
Three replicas against two templates is six claims. Names are assembled
**`<template>-<statefulset>-<ordinal>`**, template first.

Ch 11 Bearings #3 Q5 tests exactly this: option A drops the per-template clause, and option D
gets the count right, the components right, and the **order** wrong — `cache-data-0` looks
entirely plausible and matches nothing.

Storage comes from §3's two paths, with nothing special added: *"the storage for a given Pod
must either be provisioned by a PersistentVolume Provisioner based on the requested storage
class, or pre-provisioned by an admin."*

## Why the claim survives a reschedule — the under-weighted half

A StatefulSet's Pod keeps the same PVC for its whole lifecycle, and when rescheduled its
`volumeMounts` mount that same claim wherever it lands.

**Note what that does *not* say.** The storage does not move. Nothing is copied. **The claim
is a namespaced API object with no node in it, and the volume behind it is cluster-scoped.**
Neither cares which machine `web-1` is on today.

For the involuntary case the documentation is quotable directly: *"If a Pod associated with a
StatefulSet fails due to node failure, and the control plane creates a replacement Pod, the
StatefulSet retains the existing PVC. The existing volume is unaffected, and the cluster will
attach it to the node where the new Pod is about to launch."*

**Identity is the mechanism.** A Deployment's replacement is a new Pod with a new name and no
history. A StatefulSet's replacement for `web-1` must be *named* `web-1`, because the name is
how it finds `www-web-1`. Identity and storage are one mechanism seen from two sides — this
is the payoff, and it is what Ch 6 could not say without §2–§4.

⚠ **Wording provenance:** the 2026-08-25 capture flags the 08-24 wording of the reschedule
sentences as differing load-bearingly (PersistentVolumes vs PersistentVolumeClaims). Ch 11
states the reschedule behavior **in the book's own words** and quotes only the verified 08-25
node-failure statement. Preserve that split; do not "upgrade" the paraphrase to a quotation.

## ★ The claims outlive the workload

> **A StatefulSet's PersistentVolumeClaims are not deleted when the Pod is deleted, or when
> the StatefulSet is deleted. This must be done manually.**

Governed by `persistentVolumeClaimRetentionPolicy` — `whenDeleted` and `whenScaled`, each
taking `Delete` or `Retain`, **`Retain` the default for both**. *"PVCs from the
volumeClaimTemplate are not affected when their Pod is deleted."*

The volumes behind them persist too: *"the PersistentVolumes associated with the Pods'
PersistentVolume Claims are not deleted when the Pods, or StatefulSet are deleted. This must
be done manually."* **Two objects, two survival facts, stated in different places** — the
claims are the ones found sitting in the namespace afterward.

The reason is a stated judgment call, not an oversight: *"This is done to ensure data safety,
which is generally more valuable than an automatic purge of all related StatefulSet
resources."* Kubernetes chose the failure mode where forgotten volumes accumulate over the
one where a command destroys a database. Correctly — but the cleanup is yours.

**Boundary:** these policies apply to **voluntary** removal only. A node dying is not a
scale-down.

**Deliberately omitted:** a sentence about a `StatefulSetAutoDeletePVC` feature gate whose
stability stage could not be confirmed. The `Retain` default is the safe claim. Do not
restore the gate reference without a dated snapshot.

## The opposite mechanism, held next to it

A **generic ephemeral volume** also creates one PVC per Pod, and *"when the Pod is deleted,
the Kubernetes garbage collector deletes the PVC."* **Exactly opposite deletion behavior.**
The difference is intent: an ephemeral volume is scratch space provisioned like real storage;
a StatefulSet's claim is real storage created by a controller. See [[volume-types-ephemeral]].

## Constraints on later chapters

- **Ch 16 §6** debugs this from the application side (B6 skeleton). Refers; does not redefine.
- ⚑ **Ch 11 §6's pointer to Ch 9 is broken.** It cites `Ch 9 §6` for the headless Service and
  per-Pod DNS names. Verified against shipped headings: **Ch 9 §5** is the headless Service,
  **Ch 9 §6** is kube-proxy, **Ch 9 §7** is DNS names. Fix before ship; Ch 16 §6 should cite
  §5 and §7, not §6.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pluggable-interfaces.md ===
# Concept — The four pluggable interfaces

**Collected at:** **Ch 17 §4 — "Every Place Kubernetes Lets You In."** *Collects; does not
redefine.*
**Definition homes:** CRI → Ch 2 §4 · CNI → Ch 9 §1 · **CSI → Ch 11 §5** · CRDs → Ch 6 §8
**Status:** ⚑ **two live naming/ordinal conflicts. Read both before drafting Ch 17 §4.**

---

## The set

**CRI, CNI, CSI, CRDs.** B7 canonical form. Ch 11 §5 states it in exactly those four tokens,
and Ch 11 is the chapter where the set closes.

## The shape they share — what Ch 17 §4 asks the reader to state without help

> **Each publishes a contract that lets someone outside the Kubernetes project supply an
> implementation without editing core Kubernetes code.**

CSI states it most explicitly — vendors can introduce new storage systems *"without ever
having to edit the core Kubernetes code"* `[source: k8s-docs-volumes-2026-08-23]` — and the
extension-points documentation groups CSI, CNI and CRI as infrastructure extensions alongside
CRDs as API extensions `[source: k8s-docs-extending-kubernetes-2026-08-23]`.

⚠ **Grouping these four as *the* four pluggable interfaces is this book's framing, not a
Kubernetes ranking.** Ch 11 Practice Q12's answer key says so. Keep that disclosure.

Ch 11 Practice Q12 also fixes the boundaries of the claim: **A** ("all four are DaemonSets")
is false of CRDs and of the CSI controller component; **B** ("all four are cluster-scoped API
objects") is false — CRI is not an API object at all; **D** ("same release, versioned
together") is fabricated. Ch 17 §4 must not accidentally assert any of the three.

## ⚑ Conflict 1 — Chapter 2 calls the fourth one "API extensions"

- `chapter-02:598` and `chapter-02:930` (shipped): **"CRI, CNI, CSI, and API extensions."**
- B7 ledger, `chapter-10:1866`, and Ch 11 §5: **"CRDs."**

Both surface forms are in shipped text. They are partially reconciled already — Ch 2's own
inbound pointer at line 600 links its "API extensions" slot to `Ch 6 §8 — CRDs` — but
**Ch 17 §4 is the section that meets both**, and reconciling them is its job. Chapter 11
follows the ledger and is correct; do not weaken it.

## ⚑ Conflict 2 — Chapter 9 says CNI is the *second*, and it is the outlier

- `chapter-02:914` (shipped): *"This is the **first** of four times you will see this move.
  Storage does it. Networking does it. The API itself does it."* → CRI, CSI, CNI, CRDs.
- `chapter-09:1149` and `:1650` (shipped): CNI is *"the **second** instance"* / *"**Second**
  of the four pluggable interfaces."*
- `chapter-10:1866` (shipped): the reader holds **three** — CRI (Ch 2), CRDs (Ch 6), CNI
  (Ch 9).
- Ch 11 §5: CSI is **"the fourth"** / **"the last of the four."**

By encounter order the reader meets CRI at Ch 2 §4 and CRDs at Ch 6 §8 before CNI, making CNI
the **third**. Ch 2, Ch 10 and Ch 11 agree; **Ch 9 disagrees with all three.**
**Recommendation: retrofit Ch 9 §8 prose and summary row, "second" → "third."**

## Resolved — a collision Ch 10 predicted and Ch 11 avoided

The B6 skeleton labels Ch 11 §5 *"**Third** of the four pluggable interfaces"*
(`section-skeleton.md:157`). Ch 10's Stage 14 manifest flagged that this would land a
"third" on a reader just told they held three. **Shipped Ch 11 ignored the skeleton and wrote
"the fourth" / "the last."** Correct.

**Recommendation: drop the skeleton's ordinal annotations entirely.** They encode set-order,
not encounter-order, and encounter-order is what the reader experiences.

## See also

[[csi]] · [[absent-component-pattern]] — three of the four have a documented absent-component
failure mode, and Ch 11 §5 is where the reader is expected to stop asking *"is the object
there?"* and start asking *"is the component there?"*
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===
# Concept — The absent-component pattern

**Naming home:** Ch 3 §4 (where the name is coined)
**Full treatment:** Ch 10 §3 and Ch 10 §8 (Zenith) · **two further instances at Ch 11 §3 and §5**
**B3 cross-cutting theme:** #3 — retrieved *by name* at Ch 13 §7 and Ch 17 §7
**Status:** ⚑ **TWO CONFLICTS OPEN — canonical form, and instance count.**
**⛔ DO NOT DRAFT Ch 13 §7 OR Ch 17 §7 UNTIL THE COUNT IS RESOLVED.**

---

## The rule

> **An object without its component does nothing.**

Verbatim from shipped Ch 3 §4; reproduced verbatim in Ch 10 §3, Ch 10 §8, and Ch 11's Voyage
Ahead. **Do not paraphrase this sentence in any chapter** — it is retrieved as a quotation.

Ch 10 §8's compression, which later chapters should reach for:

> An object is a record of intent. Intent does not act.

## ⚑ CONFLICT 1 — canonical form (carried from Ch 10's Stage 14)

| Form | Where it lives | Verdict |
|---|---|---|
| **"the absent-component pattern"** | Shipped Ch 3 §4, reader-facing ×4 | **Recommended headword** |
| "an object without its component does nothing" | Shipped Ch 3 §4; Ch 10 ×9; Ch 11 ×3 | The **rule sentence**. Not a name. |
| "The object exists; nothing happens without the component" | B7 ledger only | **Zero occurrences in shipped text.** Do not adopt. |
| "Nothing Happens Without a Controller" | Ch 10 §8 heading | A section title, not a term |

**Recommendation:** headword = *the absent-component pattern* (naming home Ch 3 §4); rule
sentence as above; instance ledger owned by Ch 10 §3.

## ⚑ CONFLICT 2 — the instance count. **NEW at Ch 11. This is the blocking one.**

**Two incompatible counting conventions are now in shipped and finalized text.**

### Convention A — Chapter 10's, and it is graded

`chapter-10:634` has the reader at three by Ch 10 §3, and `chapter-10:1567` — Practice Q18's
**correct answer** — enumerates four by Ch 10 §7:

1. `type: LoadBalancer` Service with no provider — **Ch 9 §3**
2. Service whose selector matches no Pods — **Ch 9 §4**
3. Ingress with no Ingress controller — **Ch 10 §3**
4. NetworkPolicy on a plugin that does not implement NetworkPolicy — **Ch 10 §7** (the only
   silent one)

`chapter-10:1795` marks option B — which names only Ch 10's two instances — wrong, with this
rationale: *"the common error here is **undercounting**, not misnaming."*

### Convention B — Chapter 11's, which restarts at the Ingress

- `draft-v2.md:587` — *"This is the **third** sighting"*: Ingress, NetworkPolicy, StorageClass
- `draft-v2.md:889` — *"three times in three sections: an Ingress without a controller, a
  StorageClass without a provisioner, and now this. Here is **the fourth**"*
- `draft-v2.md:1402` — *"the Ingress controller, the network plugin, the provisioner, and the
  CSI driver — **four sightings**"*

**Chapter 11 drops both Chapter 9 instances** — the exact undercount Ch 10 grades as wrong.
A reader who answered Ch 10 Q18 correctly is told six pages later that the StorageClass is
the third; by the count they were graded on, it is the fifth.

**`draft-v2.md:889` is also internally inconsistent**: its own three-item list already
includes the current (CSI) case, and the sentence then announces "the fourth." It silently
drops the NetworkPolicy instance that line 587 included two sections earlier. **The two
enumerations inside Chapter 11 are not the same set.**

### Why this blocks Ch 13 and Ch 17

Ch 10's Stage 14 shard reserved instance **#5 for Ch 13 §7** (`kubectl top` with no
metrics-server) and **#6 for Ch 17 §7** (VPA as an addon). Chapter 11 has inserted two
instances and renumbered from a different origin. **The conventions now diverge by exactly
two**, and whichever ordinal Ch 13 uses contradicts a graded item in the other chapter.

### Recommendation

1. Amend Ch 11 §3/§5/Voyage Ahead to continue Convention A (StorageClass = fifth, CSI =
   sixth). Faithful to graded canon; the ordinals get clumsy.
2. **Preferred: stop numbering instances in prose.** Keep the rule and the enumeration, drop
   the ordinal. Ch 10 already had to reconcile two counts in a dedicated paragraph
   (`chapter-10:625`); Ch 11 is the third count, and the reconciliation cost now exceeds the
   rhetorical benefit. **The list transfers; the number breaks.**

Either way, `draft-v2.md:889`'s internal contradiction needs fixing regardless.

**This shard deliberately does not pick a winner.** Both conventions are recorded above so
no drafting stage can adopt one without seeing the other.

## The instance ledger (Convention A ordering, origin Ch 9 §3)

| # | Instance | Where | Announces itself? |
|---|---|---|---|
| 1 | `type: LoadBalancer` Service, no provider | Ch 9 §3 | Yes — `<pending>` |
| 2 | Service whose selector matches no Pods | Ch 9 §4 | Yes — traffic fails |
| 3 | Ingress with no Ingress controller | Ch 10 §3 | Yes — requests fail loudly |
| 4 | NetworkPolicy on a plugin that does not implement it | Ch 10 §7 | **No — silent** |
| 5 | **StorageClass naming a provisioner nobody deployed** | **Ch 11 §3** | Yes — claim unbound, Pod `Pending` |
| 6 | **StorageClass naming a CSI driver never installed** | **Ch 11 §5** | Yes — same signature |
| 7 | `kubectl top` with no metrics-server | Ch 13 §7 (planned) | Yes — command errors |
| 8 | VPA, an addon not shipped by default | Ch 17 §7 (planned) | Yes |

*Rows 5–6 are Ch 11's "third" and "fourth" under Convention B. Rows 7–8 were #5 and #6 in
Ch 10's shard and have shifted.*

**Instances 5 and 6 are the same failure at two depths** — a StorageClass whose provisioner
is a CSI driver nobody deployed *is* both — which is an argument for the un-numbered
treatment. Ch 11 §5's sources state it as a plain ordering requirement rather than a warning:
*"To use a CSI driver from a storage provider, you must **first** deploy it to your cluster,"*
and *"the core of Kubernetes does not install that software for you."*

## The asymmetry — provenance, keep the split

Instances 1–3 and 5–8 announce themselves. **Instance 4 does not.** The plugin dependency and
the "no effect" consequence are **documented**
`[source: k8s-docs-network-policies-depth-2026-08-24]`. The characterisation of that failure
as *silent* is **the book's own inference**, labelled as one in Ch 10 §7. Do not promote it.

## The transferable question

> **What is watching this, and is it installed?**

Ch 10 §8 hands this to the reader; Ch 11 §5 restates it as *"you stop asking 'is the object
there?' and start asking 'is the **component** there?'"* Ch 13 §7 and Ch 17 §7 should invoke
it in these words.

## Constraints on later chapters

- Ch 13 §7 and Ch 17 §7: retrieve **by name**; do not re-derive. **Blocked on Conflict 2.**
- Any chapter adding an instance: extend the table, do not restate the rule.
- **Never illustrate an instance as a broken or blocked object.** Every genuine instance is a
  **correct** object with nothing wrong with it. Ch 10 Practice Q18 option D is built on that
  distinction (a mismatched `pathType` is a manifest bug, not an instance), and Ch 11 §3's
  framing depends on it too: *"`kubectl get` shows it, `kubectl describe` shows a sensible
  spec, and nothing happens."*
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===
# Objective Coverage — KCNA

Objective IDs (`D1.1`, `D2.1`, …) are a **Lodestar convention** from B1 domain analysis. CNCF
publishes named competencies under each domain but does **not** number them and does **not**
publish sub-competency weights. Domain-level weights are the only level the sources state.

**Domain weights (2025-11-24 four-domain blueprint):** D1 Kubernetes Fundamentals 44% ·
**D2 Container Orchestration 28%** · D3 Cloud Native Application Delivery 16% ·
D4 Cloud Native Architecture 12%.

> **BACKFILL REQUIRED.** Stage 14 did not run for Chapters 1–9. Rows below cover Chapters 10
> and 11, plus the D2.1 first-coverage fact verified against shipped Ch 9. Objectives D1.x,
> D2.3, D3.x and D4.x are unlogged. Source of truth for the backfill:
> `.pipeline-state/book-outline/chapter-lineup.md` and `domain-analysis.md`.

---

## Objective-level

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D2.1 — Networking | Chapter 9 | deep — completed Chapter 10 | — |
| D2.2 — Security | Chapter 10 (boundary only) | partial — NetworkPolicy only; full coverage lands Chapter 12 | — |
| **D2.4 — Storage** | **Chapter 11** | **deep — sole coverage; no other chapter is assigned D2.4** | — |

**D2.2 note.** B1 sequencing implication #6: NetworkPolicy sits in both D2.1 and D2.2; teach
it once, in Networking, and cross-bear from Security. Chapter 10 is the sole definition home;
Chapter 12 §9 refers and must not duplicate.

**D2.4 note.** B2 sequencing constraint: *"Storage precedes StatefulSet's full treatment —
Ch 6 introduces, Ch 11 completes, cross-beared both ways."* Honored. Ch 6 §6's five deferred
verbs (provisioned / requested / sized / reclaimed / shared) are all closed at Ch 11 §4's
reconciliation table; Ch 6 retains **identity**, which Ch 11 §6 joins rather than restates.

## Concept-level — D2.4, all 20 B1 concepts

Walked row by row against `domain-analysis.md:232–255`. **20 of 20 covered. No gaps.**

| B1 concept | Covered in | Depth |
|---|---|---|
| PersistentVolume (PV) | Ch 11 §2 | deep |
| PV lifecycle independence | Ch 11 §1, §2 | deep |
| PersistentVolumeClaim (PVC) | Ch 11 §2 | deep |
| Pods:PVCs :: node resources:Pods | Ch 11 §2 | deep — quoted, not paraphrased |
| StorageClass | Ch 11 §3 | deep |
| Static provisioning | Ch 11 §3 | deep |
| Dynamic provisioning | Ch 11 §3 | deep |
| Disabling dynamic provisioning (`""`) | Ch 11 §3 | deep |
| Binding | Ch 11 §2 | deep |
| Unbound claims | Ch 11 §2 | deep |
| Using (Pod references a PVC) | Ch 11 §2 | deep — the section's Fixed Point |
| Reclaiming | Ch 11 §4 | deep |
| Retain | Ch 11 §4 | deep |
| Delete | Ch 11 §4 | deep |
| Recycle | Ch 11 §4 | adequate — named, deprecation stated |
| ReadWriteOnce (RWO) | Ch 11 §4 | deep |
| ReadOnlyMany (ROX) | Ch 11 §4 | deep |
| ReadWriteMany (RWX) | Ch 11 §4 | deep |
| ReadWriteOncePod (RWOP) | Ch 11 §4 | deep |
| StatefulSet + PV | Ch 11 §6 | deep |

## Trap coverage — D2.4

**7 of 7 (#63–#69) addressed**, verified line by line against `domain-analysis.md:571–577`.
The Exam Alert reproduces the complete D2 storage block in order with faithful corrections.

| Trap | Where corrected |
|---|---|
| #63 "A PVC binds to any PV that's big enough" | §2 + Bearings #1 Q4 + Practice Q13 |
| #64 Reversing PV and PVC | §2 Fixed Point + Bearings #1 Q3 + Practice Q2 |
| #65 "ReadWriteOnce means one Pod" | §4 Fixed Point + Bearings #2 Q1 |
| #66 "Deleting a PVC always keeps the data" | §4 + Bearings #2 Q2 + Practice Q3 |
| #67 "Retain means immediately reusable" | §2, §4 + Bearings #2 Q4 + Practice Q15 |
| #68 Expecting `Recycle` to be live | §4 |
| #69 Class `""` uses the default | §3 + Bearings #2 Q5 |

The chapter's own arithmetic about trap distribution checks out: §4's *"five of the seven…
four of them are here"* (#69 in §3, #65–#68 in §4) and Bearings #2's *"four of the exam
traps… in this checkpoint alone"* (Q1→#65, Q2→#66, Q4→#67, Q5→#69).

## Research gaps closed

| Gap | Description | Status |
|---|---|---|
| **G11** | *CNI, CSI, and CRI as the pluggable interfaces — "CSI is entirely absent."* | **Closed by Ch 11 §5.** Sourced to the CSI specification's own objective statement, plus the driver's two-component deployment shape. |
| **G12** | *Volume types other than PV/PVC: emptyDir, hostPath, configMap/secret volumes, projected, ephemeral.* | **Closed by Ch 11 §1**, which covers all five plus `downwardAPI`, `subPath`, `nfs`, and `local`. |
| **G25** | Gateway API detail | Closed by Ch 10 §5. |

## Research gaps still open that touch Chapter 11

- **PV phase count.** The concept page enumerates four, the v1 API reference five. A further
  retrieval of `/docs/concepts/storage/persistent-volumes/#phase` would settle it and clear
  the `Released`/`Failed` prose for direct quotation. See `concepts/pv-phases.md`.
- **CSI driver implementations.** No cached snapshot enumerates them; the shipped chapter
  genericized its three named drivers accordingly. Target: the `kubernetes-csi` drivers list.
- **`allowVolumeExpansion` semantics.** The grow-not-shrink sentence is not attested in any
  cached snapshot and was **not** written into the chapter. Do not add it without one.
- **No exam-logistics source is cached.** Unchanged from Ch 10. Chapter 11 complies with the
  standing constraint — its header discloses that *"CNCF publishes four domain weights and no
  sub-competency weights; the D2.4 identifier is this book's own numbering, not CNCF's."*

---

*Stage 14 · Chapters 10–11 · 2026-08-25.*
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===
# Retrieval-Practice Ledger — KCNA

Which earlier-chapter topics have been retrieval-tested, and where. Targets are set by B3
retrieval architecture: Ch 3 at 10%, Ch 4 at 15%, then **20–25% through Ch 18**, with a
**spacing floor from Ch 8 on — at least one item must come from ≥4 chapters back.**

Soundings are **excluded from the budget** by design: skill Part 11 requires them to be
answerable from prerequisites, which in this book means earlier chapters, so every Soundings
block is already a spaced retrieval event. Counting them would distort their calibration
purpose.

> ⚠ **`.pipeline-state/book-outline/retrieval-architecture.md` on disk contains a
> blocked-write error message, not the B3 artifact.** The substantive design survives as
> prose inside that file and the targets above are taken from it, but the file should be
> regenerated.

> **BACKFILL REQUIRED.** Stage 14 did not run for Chapters 1–9. Their `[retrieval: chN]` tags
> are in the shipped files and unlogged here. Chapters 10 and 11 are complete.

---

## Backward — earlier material tested in a later chapter

| Tested topic | Original chapter | Retested in |
|---|---|---|
| Service-type ladder; HTTP vs non-HTTP exposure | ch 9 §3 | ch 10 — Bearings #1 Q1; Practice Q2 |
| The absent-component rule, stated back | ch 3 §4 | ch 10 — Bearings #1 Q5; Practice Q18 |
| Control loop / the controller pattern | ch 3 §6 | ch 10 — Practice Q7 |
| Labels and selectors as the universal join | ch 4 §5 | ch 10 — Bearings #3 Q1; Practice Q16 |
| The writable container layer; what a restart discards | ch 2 §2 | **ch 11 — Bearings #1 Q2** |
| The four pluggable interfaces, as a set | ch 2 §4/§5 | **ch 11 — Practice Q12** |
| ServiceAccount token via a projected volume | ch 5 §6 | **ch 11 — Practice Q1** |
| StatefulSet ordinal identity | ch 6 §6 | **ch 11 — Bearings #3 Q3** ⚠️ thin |
| Filter phase; the unschedulable Pod | ch 7 §2 | **ch 11 — Bearings #2 Q3** |
| The absent-component pattern | ch 10 §3 | **ch 11 — Practice Q8** |

## Chapter 11 compliance

| Check | Target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of graded items | 20–25% (B3); outline target 20% | **7 of 32 = 21.9%** (15 Bearings + 17 Practice) | ✅ |
| Spacing floor (≥4 chapters back) | ≥1 item | ch 2 is **nine** back, ×2 items | ✅ |
| Tagged items land on covered material | 7 of 7 | **6 of 7** — see ⚑ below | ❌ |
| Question inventory | 8 Soundings, ≥10 Bearings across ≥2 checkpoints | 8 + 15 (3 × 5) + 17 = **40** | ✅ |

**Soundings note.** Ch 11's block is unusually load-bearing: **six of its eight questions are
retrieval** from Ch 2 §2/§4, Ch 4 §3, Ch 5 §1/§6, Ch 6 §6, Ch 6 §8, Ch 9 §1 and Ch 10's
closing. Excluded from the budget per B3, but worth recording — the chapter gets substantially
more spaced retrieval than its 21.9% suggests.

## ⚑ One failed retrieval anchor — Chapter 11 Practice Q4

Q4 asks the reader to identify "PersistentVolume cluster-scoped; PersistentVolumeClaim
namespaced" and tags it **`[retrieval: ch4]`**.

**`grep -c "PersistentVolumeClaim" chapter-04-records-of-intent.md` → 0.** Chapter 4 §3 names
Nodes, PersistentVolumes and StorageClasses as its cluster-scoped examples; it never mentions
PVCs. The B7 ledger corroborates independently — it records PVC's first appearance as **Ch 6
§6**, and ⚑6 lists only "PersistentVolume and StorageClass" as appearing early in Ch 4.

The **fact** is correct and Ch 11 §2 sources it properly. The **retrieval tag** is not: the
reader is asked to retrieve something never deposited. The same root cause makes Ch 11 §2's
prose claim (*"Chapter 4 taught you… You now have the reason rather than the rule"*)
over-credit Chapter 4.

**Fixes, in preference order:**
1. **Rewrite Q4 around Chapter 4's own cluster-scoped trio** (Node, PersistentVolume,
   StorageClass) — a genuine Ch 4 anchor, already graded at `chapter-04:733` and `:1308`,
   which holds the rate at 21.9%.
2. Retag as untagged and let it stand as a current-chapter §2 item — **drops the rate to
   6 of 32 = 18.8%, below band.**
3. Leave it. Not recommended; it overstates the book's retrieval coverage.

## Forward obligations Chapter 11 creates

| Topic Ch 11 owns | Must be retrieved in | How |
|---|---|---|
| `secret` volumes on tmpfs | **Ch 12 §4** | Ch 11 hands over **half an argument by name** — file mounts vs environment variables. Ch 12 §4 owes the other half. |
| `hostPath` as the workload-to-host hole | **Ch 12 §5** | Named and deferred explicitly; also owns the `ReadOnlyMany`-is-not-a-permission-system pointer. **Ch 12 must not re-derive the risk.** |
| An unbound claim as a `Pending` Pod | **Ch 13 §2** | Ch 11 supplies the mechanism, Ch 13 the diagnosis. |
| Per-replica PVC; ordinal identity + storage | **Ch 16 §6** | B6 skeleton line 243. Refers; does not redefine. ⚑ cite Ch 9 §5 and §7, **not** §6. |
| CSI as the fourth interface | **Ch 17 §4** | *Collects; does not redefine.* ⚑ two naming conflicts — read `concepts/pluggable-interfaces.md` first. |
| The absent-component pattern | **Ch 13 §7, Ch 17 §7** | ⛔ **BLOCKED** on the instance-count conflict. |

## Open gaps

**1. ⚑ NEW — the absent-component instance count is contested.** Chapter 11 restarts the
count at the Ingress and drops Chapter 9's two instances — the exact undercount Ch 10 Practice
Q18 grades as wrong (*"the common error here is undercounting"*). Chapter 11's own two
enumerations (`draft-v2.md:587` and `:889`) are not the same set, and `:889` calls the third
item in its own three-item list "the fourth." **Blocks Ch 13 §7 and Ch 17 §7.** Full detail
in `concepts/absent-component-pattern.md`.

**2. CSI driver architecture is taught but never assessed.** The controller Deployment plus
per-node DaemonSet — promised by name at `chapter-02:600` — appears in **zero of Ch 11's 40
questions**. The chapter's own AUTHOR-REVIEW records why: the curriculum rebalance claimed
Bearings #3's fifth slot for a `volumeClaimTemplates` item, and the two findings competed for
one seat. **The Practice set is the right home if a slot is found** — restoring it to Bearings
#3 would push CSI to 3 of 5 there against 1 of 17 in Practice, which is the imbalance the
rebalance was correcting.

**3. north-south / east-west is taught but never assessed.** Carried from Chapter 10, where it
appears in zero of 41 questions despite a 🪢 Mnemonic and a Chapter Summary row. **Still
open**; Chapter 11 does not touch it.

**4. ⚑ Chapter 9 undercounts the pluggable interfaces.** Ch 9 §8 calls CNI *"the second
instance"*; Ch 2 line 914, Ch 10, and Ch 11 all make it the third. **Still open.**
Recommended retrofit: Ch 9 §8 prose and summary row, "second" → "third."

## Resolved since Chapter 10

**Ordinal collision at Ch 11 §5 — RESOLVED.** Ch 10's log predicted that the B6 skeleton's
*"Third of the four pluggable interfaces"* label (`section-skeleton.md:157`) would land a
"third" on a reader just told they held three. **Shipped Ch 11 §5 ignored the skeleton and
wrote "The fourth is CSI" / "the last of the four."** Consistent with Ch 2, Ch 10, and the B7
canonical set. **Recommendation: drop the skeleton's ordinal annotations** — they encode
set-order, not encounter-order.

---

*Stage 14 · Chapters 10–11 · 2026-08-25.*
=== END WRITE ===
```

---

## Recommended fixes carried forward from this stage

**Blocking — resolve before Ch 13 §7 drafts.**

1. **The absent-component instance count** (⚑A). Chapter 11 undercounts against a Chapter 10 graded item that names undercounting as the error, and its own two enumerations disagree. My recommendation is to stop numbering instances in prose and keep the list.

**Fix before ship — chapter-text edits, all small.**

2. **§6's `Ch 9 §6` pointer** → `Ch 9 §7`, and attribute the headless Service to Ch 9 §5.
3. **§2's Ch 4 attribution** → claim only the PV half; present the PVC half as new. Rewrite **Practice Q4** around Ch 4's own cluster-scoped trio.
4. **Expand NFS and LUN on first use** and register NFS, LUN, iSCSI, EBS. NFS carries two graded items and is nowhere in the book in full.
5. **`draft-v2.md:889`'s internal contradiction** — a three-item list that includes the current case, followed by "here is the fourth."

**Author's call — low severity.**

6. §5's stale AUTHOR-REVIEW cites `ebs.csi.aws.com` "used in this chapter's Taking Your Bearings #3"; that string now appears only inside the comment.
7. Soundings scoring note says six of eight questions are two-part; seven are.
8. §1 says Ch 4 "hedged" the ConfigMap update rule; `chapter-04:762` states it flatly and sourced. One word.
9. `finalizer` and `ENOSPC` need either a one-clause gloss or a B7 ambient-tier assignment.

**Infrastructure.**

10. **`retrieval-architecture.md` on disk is a blocked-write error message**, not the B3 artifact — unchanged since Chapter 10 flagged it. Regenerate.
11. **The B6 skeleton's ordinal annotations should be dropped.** Chapter 11 correctly ignored one; the next chapter might not.

## What I'd act on first

The instance count, ahead of the integration report's two findings. Both of those are one-line edits with obvious fixes; this one has no obvious fix, a nearer deadline, and no natural discovery point. Ch 13 §7 and Ch 17 §7 are contractually required to retrieve the pattern by name and by count, and the two live conventions now differ by exactly two. Whichever a drafter picks, it contradicts a graded answer key in the other chapter — and nothing downstream will flag it, because both counts are internally coherent and both cite real instances.