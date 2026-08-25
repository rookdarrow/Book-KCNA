Verification complete. Here is the artifact.

```markdown
# Integration Check — KCNA Chapter 11

## Summary

- Terminology consistency: **fail** (scoped — every canonical-form rule holds; the acronym-expansion rule is breached on 4 terms)
- Callbacks to earlier chapters: **56 correct / 3 flagged** (59 checks: 44 bracketed cross-bearings + 15 prose attributions)
- Retrieval-practice accuracy: **fail** (6 of 7 tags clean; 1 materially misaligned)
- Glossary coverage: **40 concepts introduced, 34 defined in-chapter, 6 require glossary entries**
- Contradictions with earlier canon: **2 flagged**
- Ethical guardrails (skill Part 14): **pass**

Chapters 1–10 are shipped and were read directly, so nothing in this report is inferred from the absence of knowledge-base shards. The `[no knowledge-base shards tagged]` input was worked around by verifying against `chapter-01`…`chapter-10` in the book repo.

Section numbering verifies clean: all seven section numbers and titles match the B6 skeleton exactly, the heading form is the recommended Ch 5–8 pattern (`## <difficulty> §N — Title`), and §7 carries `☀️` per skeleton recommendation #4.

---

## Terminology consistency

### Canonical forms — all clean

| Term | Canonical form | Occurrences | Drift? |
|---|---|---|---|
| PersistentVolume | `PersistentVolume` CamelCase | 49 | no |
| PersistentVolumeClaim | `PersistentVolumeClaim` CamelCase | 48 | no |
| StorageClass | `StorageClass` CamelCase | 59 | no |
| StatefulSet | `StatefulSet` CamelCase | 48 | no |
| Pod | `Pod` capitalized for the object | 181 | no — zero bare lowercase `pod`/`pods` |
| `emptyDir` / `hostPath` | code style, exact casing | 18 / 13 | no |
| kubectl | lowercase, code style | 11 | no — zero `Kubectl` |
| etcd | lowercase | 0 | n/a |
| cloud native | never hyphenated | 0 | n/a — zero `cloud-native` |
| Taking Your Bearings | never bare "Bearings" in reader-facing text | 3 full uses | no — the 2 bare uses are inside `AUTHOR-REVIEW` comments, which the ledger permits |
| Secret / Service | capitalized for the object | — | no lowercase-object drift |
| "Storage Class" (two words) | `StorageClass` | 2 | **exempt** — both are inside direct quotations from Kubernetes documentation, which writes it that way |
| the four pluggable interfaces | exact phrase, = CRI + CNI + CSI + CRDs | 3 | no — matches ledger and matches Ch 10's closing |
| binding (PV/PVC sense) | bare use licensed in its owning chapter | — | no |

### The one breach: acronym expansion

The ledger's acronym register is explicit: *"Every acronym is expanded on its first use in the book, without exception, even where the expansion is obvious."* Four acronyms in this chapter appear **nowhere in Chapters 1–10** — verified by grep across all ten shipped files, zero hits — so Chapter 11 is their first appearance in the book, and none is expanded here. None is in the ledger's 74-entry register either.

| Acronym | Occurrences | Where it does work | Severity |
|---|---|---|---|
| **NFS** | 9 | Defines a volume type in §1's rung-three teasers; load-bearing for §4's access-mode argument (*"NFS in particular can be mounted by multiple writers simultaneously"*); the subject of graded Practice Q7 and Q11 | **High** — a reader is asked to answer graded questions about a technology the book has never named in full |
| **LUN** | 2 | Soundings Q5 and its answer | Medium — reader-facing question text |
| **EBS** | 4 | §2 Fixed Point and "Why This Chapter Matters", as an illustrative backing store | Low |
| **iSCSI** | 2 | Both inside direct quotations from the docs | Low — quoted, but still first appearance |

`ENOSPC` (Practice Q14 distractor B) is a fifth unglossed jargon token, though not an acronym in the register's sense.

**Recommended fix:** expand NFS and LUN in place on first use (`NFS (Network File System)`, `LUN (Logical Unit Number)`), and add all four to the register for stage 14. This is a four-token edit, not a rewrite.

### One pre-existing divergence, recorded not charged

Shipped Ch 2 names the canon set as **"CRI, CNI, CSI, and API extensions"** (lines 598 and 930). The ledger, Ch 10's closing (line 1866), and this chapter all say **CRDs**. Chapter 11 follows the binding ledger and is correct. Ch 2's own inbound pointer at line 600 already links its "API extensions" slot to `Ch 6 §8 — CRDs`, so the two surface forms are reconciled in shipped text — but **Ch 17 §4, which collects all four, will meet both forms** and should be told to expect them. Not a Chapter 11 defect; flagged for the Ch 17 drafting stage.

---

## Callback correctness

### Bracketed cross-bearings: 43 of 44 resolve

Verified mechanically against the B6 skeleton, not against my reading of the target chapters. All targets in Ch 2, 3, 4, 5, 6, 7, 10 and the forward targets in Ch 12, 13, 17 resolve exactly — including the label-only variants (`Ch 4 §3 — namespaced vs cluster-scoped` and `Ch 4 §3 — where a name lives` both resolve, since §3 owns both the title and the topic).

**One broken pointer:**

> **`*[cross-bearing: see Ch 9 §6 — names, and where they resolve]*` — §6 is the wrong number.**
>
> Confirmed against shipped `chapter-09` headings: **§6 is "The Component That Makes It Real"** (kube-proxy, line 862). **§7 is "Names, and Where They Resolve"** (line 947). The pointer's *label* matches §7's title verbatim, so this reads as a single mistyped digit.
>
> The surrounding prose has the same fault and needs fixing with it. §6 of this chapter says: *"Chapter 9 §6 gave you the network half of that identity: the headless Service and the per-Pod DNS names it produces."* Neither topic is in §6. **Headless Services are Ch 9 §5** ("When You Don't Want a Single Address", line 737); **the DNS names are Ch 9 §7**. As written, a reader who follows the pointer lands in the service-proxy section and finds neither thing they were promised.
>
> **Recommended fix:** retarget to `Ch 9 §7 — names, and where they resolve`, and adjust the sentence to attribute the headless Service to §5 — e.g. *"Chapter 9 gave you the network half of that identity: the headless Service in §5, and the per-Pod DNS names it produces in §7."*

### Prose attributions: 13 of 15 accurate

Everything Chapter 11 claims an earlier chapter said, checked against that chapter's text. The four hand-off promises Chapter 10 made verify **verbatim**:

| Claim in Ch 11 | Source | Verdict |
|---|---|---|
| Ch 10 promised "a ladder of three different lifetimes, only one of which survives the thing that created it" | `chapter-10:1846` | ✅ verbatim |
| Ch 10 promised "objects that describe storage without providing any… a claim sits unbound because the thing that would satisfy it has not been installed" | `chapter-10:1870` | ✅ verbatim |
| Ch 10 promised "the last of the four pluggable interfaces" | `chapter-10:1866` | ✅ verbatim |
| Ch 10 promised claims "outlive not just the Pod but the rescheduling" | `chapter-10:1848` | ✅ verbatim |
| Ch 6 §6 deferred storage as "provisioned, requested, sized, reclaimed, or shared. That is deliberate." | `chapter-06:862` | ✅ verbatim (see nit below) |
| Ch 6 §6 taught ordinal identity `web-0`/`web-1`/`web-2` | `chapter-06:810` | ✅ |
| Ch 2 promised "CSI and storage drivers" with *drivers* in the promise | `chapter-02:600` | ✅ verbatim |
| Ch 5 §6 delivered the ServiceAccount token via a projected volume | `chapter-05:775` | ✅ |
| Ch 10 §3 named "an object without its component does nothing" | `chapter-10:601` | ✅ |
| Ch 10 §6 established "no deny rule" (the Voyage Ahead tease) | `chapter-10:1113` — *"There is no deny rule. None."* | ✅ |
| Ch 5 §1 taught that a Pod's containers share a network namespace and volumes | `chapter-05` §1 | ✅ |
| Ch 7 §2's filter-phase inputs match the `WaitForFirstConsumer` constraint list | `chapter-07` §2 | ✅ |
| Ch 4 §3 taught that PersistentVolumes are cluster-scoped | `chapter-04:540,563,1005,1308` | ✅ |
| **Ch 4 §3 taught that PersistentVolumeClaims are namespaced** | — | ❌ **see below** |
| **Ch 9 §6 gave the headless Service and per-Pod DNS** | — | ❌ **see above** |

**❌ Flagged — §2 attributes a PVC teaching to Ch 4 that Ch 4 never gave.**

The chapter says: *"Chapter 4 taught you that a PersistentVolume is cluster-scoped while a PersistentVolumeClaim is namespaced… You now have the reason rather than the rule."*

**`chapter-04` contains zero occurrences of "PersistentVolumeClaim".** Ch 4 §3 names Nodes, PersistentVolumes, and StorageClasses as its cluster-scoped examples, four times over — the PV half is solid. But it never mentions PVCs at all. The book's own ledger corroborates this independently: it records PVC's first appearance as **Ch 6 §6**, and its ⚑6 flag lists only "PersistentVolume and StorageClass" as appearing early in Ch 4. Confirmed: PVC appears in exactly one shipped chapter before this one — Ch 6, twice, both name-only in a deferral list at `chapter-06:864`.

The *fact* is correct and Ch 11 §2 sources it properly. What is wrong is the attribution: the reader is told they already learned this and are now getting "the reason rather than the rule," when half of it is new here.

**Recommended fix:** narrow the claim to what Ch 4 delivered — e.g. *"Chapter 4 taught you that a PersistentVolume is cluster-scoped* [pointer]*. It did not tell you where the claim lives: a PersistentVolumeClaim is namespaced, and the reason is the split you have just read."* This preserves the rhetorical move and stops over-crediting Ch 4.

**Nit — §1's characterization of the Ch 4 `subPath` hand-off.** Ch 11 says Ch 4 *"hedged that a mounted ConfigMap picks up changes… and told you the exception had a name and would arrive here."* Ch 4 did point here, and did name `subPath` — but it did not hedge. `chapter-04:762` states the rule flatly and sourced: *"a container using a ConfigMap as a `subPath` volume mount will not receive updates at all."* Ch 11 then presents the same rule as newly arriving ("Here it is, a flat rule with no conditions attached"). Ownership is correct — the ledger gives `subPath` to Ch 11 §1 — so the duplication is Ch 4's forward lean, not this chapter's fault. Only the word "hedged" is inaccurate. One-word fix, author's call.

**Nit — quotation fidelity.** §4 renders the Ch 6 deferral as ending *"That is deliberate."* The original continues *"That is deliberate, and you should know it is deliberate rather than wonder what got skipped."* A clean truncation, substance preserved; noted only because it is presented as a direct quotation.

### Inbound pointers: 8 of 8 honored

Every published pointer aimed at this chapter resolves, including both numbered pins:

| Inbound pointer | Target | Verdict |
|---|---|---|
| `chapter-05:349` → `Ch 11 §1 — volume types and lifetimes` | §1 | ✅ pinned and honored |
| `chapter-09:758` → `Ch 11 §6 — StatefulSets and their per-replica volume claims` | §6 | ✅ pinned and honored |
| `chapter-02:600` → `Ch 11 — CSI and storage drivers` | §5 | ✅ chapter-level |
| `chapter-04:540` → `Ch 11 — PersistentVolumes and StorageClasses` | §2/§3 | ✅ chapter-level |
| `chapter-04:722`, `chapter-04:762` → `Ch 11 — ConfigMap and Secret volumes…` | §1 | ✅ chapter-level |
| `chapter-05:775` → `Ch 11 — projected volumes` | §1 | ✅ chapter-level |
| `chapter-06:868` → `Ch 11 — PersistentVolumes, claims, and how a Pod's storage follows its identity` | §2/§6 | ✅ chapter-level |

---

## Retrieval-practice accuracy

Seven tagged items. Retrieval rate is **7 of 32** graded items (15 Bearings + 17 Practice) = **21.9%**, inside the 20–25% band the skill's Part 10 table sets for chapters 6+.

| Item | Tag | Topic tested | Covered in the tagged chapter? |
|---|---|---|---|
| Bearings #1 Q2 | `ch2` | Container writable layer discarded on restart | ✅ Ch 2 §2 |
| Bearings #2 Q3 | `ch7` | Filter phase; unschedulable Pod sits `Pending` | ✅ Ch 7 §2 |
| Bearings #3 Q3 | `ch6` | StatefulSet ordinal identity behind `www-web-N` | ⚠️ thin but valid — see below |
| Practice Q1 | `ch5` | ServiceAccount token via projected volume | ✅ Ch 5 §6 (`chapter-05:775`) |
| **Practice Q4** | **`ch4`** | **PV/PVC scoping** | ❌ **half unsupported** |
| Practice Q8 | `ch10` | "Object without its component" pattern | ✅ Ch 10 §3 |
| Practice Q12 | `ch2` | The four pluggable interfaces | ✅ Ch 2 §4/§5 |

**❌ Practice Q4 — the same root cause as the §2 callback.** The question asks the reader to pick the pair "PersistentVolume cluster-scoped; PersistentVolumeClaim namespaced" and tags it `[retrieval: ch4]`. Ch 4 supports the PV half only; it never mentions PVCs. As tagged, the item overstates the book's retrieval coverage and asks the reader to retrieve something that was never deposited.

Three fixes, in my order of preference:
1. **Reword to a genuine Ch 4 retrieval** — ask which of a set is cluster-scoped using Ch 4's own named trio (Node, PersistentVolume, StorageClass), which is exactly the distinction `chapter-04:733` and `chapter-04:1308` already test.
2. **Retag as untagged** and let it stand as a current-chapter §2 item.
3. **Leave and accept** the half-anchor, dropping the effective retrieval rate to 6 of 32 (18.8%), below the band.

**⚠️ Bearings #3 Q3 — defensible, worth knowing about.** The item is tagged `ch6`, and the Ch 6 anchor is real: the reader must recognize from `chapter-06:810` that a StatefulSet named `web` produces `web-0`/`web-1`/`web-2`. But the rest of the question — the `<template>-<set>-<ordinal>` PVC name form and the `persistentVolumeClaimRetentionPolicy` default — is Ch 11 §6's own new material, and `chapter-06` contains zero occurrences of `volumeClaimTemplate`, `www-web`, or "per-replica". The retrieval step is one recognition inside a mostly current-chapter question. Valid, but the thinnest of the seven. No change required; recorded so the Ch 19 §1 theme-tracing stage knows the Ch 6→Ch 11 reciprocal pair is carried by this one item.

---

## Glossary coverage

40 concepts introduced; 34 defined in-chapter; **6 require glossary entries**.

All 25 terms the ledger assigns to Ch 11 are defined in-chapter — verified one by one against the ledger rows for §1 through §6. No ledger-owned term is used without its definition, and no term the ledger routes elsewhere is over-explained here.

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| Volume (Kubernetes sense); the volume lifetime ladder | yes | no |
| `emptyDir`, incl. `medium: Memory` and `sizeLimit` | yes | no |
| `hostPath` | yes | no |
| `configMap` / `secret` volume source | yes | no |
| `projected` volume | yes | no |
| Generic ephemeral volume | yes | no |
| `subPath` | yes | no |
| `downwardAPI` volume | yes | no |
| PersistentVolume; PersistentVolumeClaim | yes | no |
| PV phase (`Available`/`Bound`/`Released`/`Failed`) | yes | no |
| Binding (PV/PVC sense) | yes | no |
| StorageClass; provisioner; default StorageClass | yes | no |
| Static vs dynamic provisioning | yes | no |
| `volumeBindingMode` / `WaitForFirstConsumer` | yes | no |
| Access modes RWO / ROX / RWX / RWOP | yes | no |
| Reclaim policies `Retain` / `Delete` / `Recycle` | yes | no |
| CSI; CSI driver; in-tree plugin; CSI migration | yes | no |
| `volumeClaimTemplates` | yes | no |
| `nfs` volume type; `local` volume type | yes | no |
| `tmpfs` | yes — glossed as "a RAM-backed filesystem" | no |
| Storage Object in Use Protection | yes | no |
| `persistentVolumeClaimRetentionPolicy` (`whenDeleted`/`whenScaled`) | yes | no |
| Clustered filesystem | yes — glossed by function in Soundings A8 | no |
| `CSIDriver` (the API object) | yes — one clause in §5 | **yes** — an API object no chapter in the ledger owns |
| **NFS** (Network File System) | **no** | **yes** |
| **LUN** (Logical Unit Number) | **no** | **yes** |
| **iSCSI** | **no** | **yes** |
| **EBS** (Elastic Block Store) | **no** | **yes** |
| **finalizer** (`kubernetes.io/pvc-protection`) | **no** — used once, unexplained | **yes** |
| `ENOSPC` | no — appears only in a Practice Q14 distractor | optional |

Stage 14 should additionally harvest the 25 ledger-owned terms into the book glossary per skill Part 16, which requires all technical terms introduced in the book, not merely the undefined ones. The six above are the ones this chapter leaves the reader unable to look up.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** The chapter contains no invented percentages, no "73% of candidates" figures. Its only quantitative claims are the domain weights and the trap counts, both checked below.
- [x] **Fear-based content uses real examples.** The `hostPath` hazard block quotes the Kubernetes documentation's own security language verbatim and sourced (*"presents many security risks"*, *"privileged system credentials"*, *"container escape"*). The "Why This Chapter Matters" stakes line — *"the failure modes in this chapter destroy data rather than merely stop traffic"* — is substantiated by the reclaim-policy material that follows. No manufactured dread.
- [x] **Simplification acknowledged.** Dead Reckoning blocks in "Why This Chapter Matters" and §4. The §2 Snag hedging the four-versus-five PV-phase count is a textbook "Full Picture" move: it teaches the four, then tells the reader `Pending` exists in the API reference and must not be eliminated on an answer sheet. §3's Closer Look explicitly tells the reader to carry the consequence and forget the field name.
- [x] **Authority claims cite legitimate sources.** Every factual claim carries a `[source: …]` tag to a dated snapshot. Two passages go further and mark the book's own reasoning *as* the book's: §5's *"The documentation records the arrangement, not what it cost the people living inside it, so what follows is this book's reading rather than a sourced claim,"* and §4's *"That is not a Kubernetes fact, and no Kubernetes document will tell you so. It is ordinary storage knowledge."* That is the guardrail working as designed.
- [x] **"Frequently tested" claims verifiable.** This is the chapter's strongest area, and it audits clean:
  - The header discloses that *"CNCF publishes four domain weights and no sub-competency weights; the D2.4 identifier is this book's own numbering, not CNCF's."*
  - "Container Orchestration | 28%" and Storage as one of its four competencies match `chapter-01:239–240` exactly.
  - The Exam Alert's **seven** common traps are the domain analysis's traps **#63–#69** — the complete D2 storage block, in order, with faithful corrections. Verified line by line.
  - §4's claim that *"five of the seven… live in this section and the last one, and four of them are here"* is arithmetically correct: #69 in §3, and #65–#68 in §4.
  - Bearings #2's *"Four of the exam traps… are tested in this checkpoint alone"* is correct: Q1→#65, Q2→#66, Q4→#67, Q5→#69.
  - The two additions past the seven are explicitly demoted: *"they have not been assessed for exam frequency the way the seven above have."* This is precisely the skill's "distinguish frequently tested from might be tested" requirement, stated in the text rather than assumed.
- [x] **No strawmanning of alternative study methods.** None present.
- [x] **Subject dignity (Part 14 item 9, skill v5.7).** Wry beats are aimed at the practitioner throughout — *"it would be holding a meeting"*, *"the kind of thing that costs someone an afternoon"*, *"bound, billing, and invisible."* Data loss, the one place a third party could be harmed, is handled straight: *"A reclaim policy misunderstood is a deleted volume, and that does not end."* No joke lands on anyone outside the room.

---

## Recommended fixes

The revision stage's diagnostics were largely worked through — the Attention Budget was rebuilt and now sums correctly (136 min against a stated ~135, splitting 71/65 across the two sessions exactly as described), the PV-phase disagreement is hedged, and the practice allocation deviations are documented in place. What follows is what those passes did not catch.

**Fix before ship — two defects, both one-line edits.**

1. **§6 — broken cross-bearing `Ch 9 §6`.** Retarget to `Ch 9 §7 — names, and where they resolve`, and repair the sentence to attribute the headless Service to Ch 9 §5. As written the pointer sends the reader to kube-proxy. *(The only broken pointer of 44; the label already matches §7's title, so this is a mistyped digit.)*

2. **§2 — Ch 4 never taught that PVCs are namespaced.** Narrow the sentence to claim only the PV half, and present the PVC half as new. The same root cause makes **Practice Q4's `[retrieval: ch4]` tag misaligned**; my recommendation is to rewrite that item around Ch 4's own cluster-scoped trio (Node, PersistentVolume, StorageClass), which restores a genuine retrieval anchor and keeps the rate at 21.9%.

**Fix before ship — terminology contract.**

3. **Expand NFS and LUN on first use**, and register NFS, LUN, iSCSI, and EBS. NFS carries graded questions (Practice Q7, Q11) and is never spelled out anywhere in the book. Four tokens.

**Author's call — low severity.**

4. **§5 carries a stale `AUTHOR-REVIEW`.** It flags a research gap needed to support *"the `ebs.csi.aws.com` provisioner string used in this chapter's Taking Your Bearings #3."* That string appears exactly once in the file — inside the comment itself. Bearings #3 Q2 now uses `blockstore.example.com`. Trim the clause so a later stage does not chase a source for text that is no longer there.

5. **Soundings scoring note undercounts by one.** It says *"Six of the eight questions above ask for two things."* By my count seven do — Q1, Q3, Q4, Q5, Q6, Q7, Q8; only Q2 is single-part, its second clause being a hint rather than a question. The rubric is unaffected, but this chapter earns its credibility by being checkable, and a reader can check this one in ten seconds.

6. **§1 says Ch 4 "hedged" the ConfigMap update rule.** Ch 4 stated it flatly and sourced (`chapter-04:762`). One word.

7. **Six terms need glossary entries** (NFS, LUN, iSCSI, EBS, finalizer, `CSIDriver`) — carried forward to stage 14.

**Recorded, not charged to this chapter.**

8. **Ch 2 calls the fourth interface "API extensions"; the ledger, Ch 10, and Ch 11 call it "CRDs."** Chapter 11 correctly follows the ledger. **Ch 17 §4 collects all four and will meet both surface forms** — that stage should be told, since reconciling them is its job, not this one's.
```