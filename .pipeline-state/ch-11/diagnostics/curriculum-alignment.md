I can't write files at this stage — the orchestrator holds stage output to stdout. Emitting the document.

---

# Curriculum-Alignment Audit — KCNA Chapter 11

**Stage:** 7 (curriculum-alignment) · **Target:** `draft-v1.md` · **Verdict:** PASS with four actionable findings, one of which is P1 and mechanical.

## Method note (read first)

**Authority used.** `cncf-kcna-curriculum-pdf-2026-08-23.md` and `lf-kcna-exam-page-2026-08-23.md`. Between them these publish *four domain weights and nothing else*: no numbered objective IDs, no sub-competency weights, no question count, no per-topic frequency data. Every objective ID in this audit (`D2.4`, `D1.3`, etc.) is a **house-inferred** ID derived from the order competencies are listed under each domain in the CNCF PDF — the same convention the outline uses. CNCF numbers nothing. Where a finding turns on that distinction, it is stated.

**Line numbers.** The stage prompt asks for line citations against `draft-v1.md`. The draft reached this stage as inline text, not as a file on disk, so line numbers cannot be produced without fabricating them — which would send the revision stage to the wrong places. Every finding below is anchored by **section heading + verbatim quoted phrase** instead, which is unambiguous under `Ctrl-F`. Flagged so a later stage doesn't read the substitution as an omission.

---

## Objectives the outline claims to cover

The outline tags all seven sections `objectives: ["D2.4"]` — a single value. At that granularity the table has one row and detects nothing, so it is given first as published, then decomposed against the arc outline's own "Covers" list.

### As published

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D2 (28%, published) | Container Orchestration | partial by design | Storage competency only; three sibling competencies belong to other chapters |
| D2.4 (house-inferred) | Container Orchestration → **Storage** | **YES** | appropriate, at the upper bound |

### Decomposed against the arc outline's "Covers" list

| Sub-topic (outline's own enumeration) | Covered in draft? | Depth | Note |
|---|---|---|---|
| Volume types — `emptyDir`, `hostPath`, `configMap`/`secret`, `projected`, ephemeral | YES | **deep — over-covered** | See Depth §A |
| PersistentVolume | YES | appropriate | |
| PersistentVolumeClaim | YES | appropriate | |
| StorageClass | YES | appropriate | |
| Static vs dynamic provisioning | YES | appropriate | Two-condition Fixed Point is well-pitched |
| **Binding** (exclusive, one-to-one, unbound-indefinitely) | YES in prose | **under-assessed** | Taught well in §2; **zero of 17 practice questions test it.** See Depth §B |
| Reclaim policies — Retain / Delete / Recycle | YES | appropriate | Dead Reckoning block is correctly flat |
| Access modes — RWO / ROX / RWX / RWOP | YES | appropriate | Node-count Fixed Point is the chapter's strongest |
| CSI | YES | **deep — over-covered, self-flagged** | See Depth §C |
| StatefulSet + PV pairing | YES | appropriate | |
| `volumeMode` (Filesystem / Block) | **NO** | — | Sourced at `k8s-docs-persistent-volumes-depth-2026-08-25` §"Volume Modes", tagged D2.4, absent from outline *and* draft. Low priority; omission is defensible for a recall-level exam. Recorded so it isn't rediscovered. |

**No objective the outline claims is missing from the draft.** All ten planned sub-topics land. The failures below are allocation and attribution failures, not coverage failures.

---

## Objectives covered in the draft but NOT in the outline

Drift, ranked by volume. All house-inferred IDs. Column 3 records whether the outline explicitly authorized the excursion — most did, which changes the recommended action from "cut" to "re-tag."

| Drifted-into | Where | Authorized by outline? | Assessment |
|---|---|---|---|
| **D1.3 Scheduling** | §3 `WaitForFirstConsumer` subsection + Closer Look (`nodeName` bypass, plugin-support list); **Bearings #2 Q3** is a full scheduler-interaction item | Yes — outline §3 Note mandates Closer Look framing | Handled honestly (draft says "above what KCNA asks of you"). But it consumes 1 of 5 items in the chapter's hardest checkpoint. Keep the prose, reconsider the item. |
| **D2.2 Security** | §1 ⚠ Navigational Hazards on `hostPath` — six consecutive verbatim quotations on container escape, kubelet credentials, runtime socket, admission-time validation; plus `secret` tmpfs; plus "access mode does not enforce write protection" | Yes — planted for Ch 12 §5 | Discipline is good ("Named here, and left here"). By volume it is the longest callout in §1. Plant is fine; the *quotation density* is what pushes it past a plant. |
| **D4.2 Cloud Native Ecosystem and Principles** | §5's four-interface taxonomy, the OCI comparison, **Bearings #3 Q5** (zero storage content), Practice Q12 | Yes — Ch 2/Ch 10 debts; Ch 17 §4 owed forward | Arguably a coverage *win* for an under-served domain, but it is unbudgeted here and the outline assigns the collection to Ch 17. See Depth §C. |
| **D1.1 Core Concepts** | §6 StatefulSet identity/ordinal restatement and the ⚓ "Worth Securing" on same-ordinal recreation; §5's driver-as-Deployment-plus-DaemonSet | Partly — outline said §6 must *complete* Ch 6, not restate it | Mild. The ordinal-recreation block is genuinely new *reasoning* on old material, which is the good version of this. |
| **D2.3 Troubleshooting** | `Pending` Pods, unbound-claim silence, "no error event that says so" | Yes | **Clean — no action.** Mechanism stays here, diagnosis defers to Ch 13 every time. This is the model the other four should follow. |

**Consequence worth surfacing:** `kb_tags.objectives: ["D2.4"]` is a single-value field describing a chapter that demonstrably teaches across five competencies in four domains. If `kb_tags` feed downstream selection the way B1's trap inventory feeds Ch 19 §2 and Ch 20, this chapter's D1.3/D2.2/D4.2 content is invisible to those stages. Author decision: widen the tag, or accept that this chapter's non-storage teaching is untracked.

---

## Depth mismatches

Published weight for D2 is **28% across four competencies**, with no split published. The chapter's authored allocation is **5% of total exam** — below an even four-way split of D2 (7%), i.e. a deliberate downweight. Chapter-level delivery: 7 sections, 6 figures, 40 questions. Against the book's own calibration (Ch 9 and Ch 10 each ran 8 sections for Networking), **7 sections for Storage is proportionate.** The mismatches are all at sub-topic level.

| Sub-topic | Weight signal | Draft depth | Mismatch |
|---|---|---|---|
| Access modes + reclaim (§4) | highest-yield per outline; 4/17 practice | deep | **OK** — best-calibrated section in the chapter |
| Binding cardinality (§2) | Exam Alert priority #1; trap 63 `[source]` | taught, **not assessed** | **under-covered** — see §B |
| §2 overall (PV/PVC/StorageClass) | outline allocated **4/17** practice | delivered **2/17** | **under-covered** |
| §1 volume types | outline allocated **3/17**; "broad surface, low difficulty" | delivered **5/17** + longest section | **over-covered** — see §A |
| CSI (§5) | outline: "one item is proportionate", **1/17** | 1/17 practice but **3/5 of Bearings #3** | **internally inconsistent** — see §C |
| `WaitForFirstConsumer` (§3) | outline: Closer Look, consequence-only | Closer Look **+ a full Bearings #2 item** | over-covered (mild) |
| Generic ephemeral volumes (§1) | not named in any published competency | full mechanism + naming + Closer Look + Q17 + contrast Snag | over-covered (moderate, low confidence — defensible as D2.4) |
| CSI migration (§5) | self-flagged "deeper than the exam requires" | longest block in §5 | over-covered, honestly labelled — accept or trim |

### §A — §1 breached the outline's own catalogue guardrail

The outline's §1 Note is explicit: *"Resist enumerating every volume type the documentation lists… the section earns its keep by making the ladder the organising idea and hanging types off it, not by being a catalogue."*

The ladder *is* the organising idea and it works. But §1 then delivers: `emptyDir` (+ `medium`, `sizeLimit`, + a Snag on the absent default cap), `hostPath` (+ `type` + six-quote security block), `configMap`, `secret` (+ tmpfs), `projected` (+ **all six** sources + `audience` + `expirationSeconds` numerics), `downwardAPI`, generic ephemeral (+ controller mechanism + deterministic naming + Closer Look on `pod-a`/`a-scratch` collisions), `subPath` (+ three no-update rules), `nfs`, `local` (+ node affinity + no-dynamic-provisioning + unhealthy-node). That is a catalogue with a spine.

It is also the section that absorbed the two practice questions §2 was supposed to get.

**Specific over-reach against a research instruction.** `k8s-docs-projected-volumes-2026-08-25` NOTE FOR §1 says: *"Prefer this file's list, or say 'several existing volume sources' and enumerate only the four the reader has met."* The draft enumerates all six, including `clusterTrustBundle` and `podCertificate` — two sources the reader has never met, which appear nowhere else in the book, and which are not KCNA material. The research stage anticipated this exact choice and recommended against it.

### §B — the chapter's #1 exam claim is untested in the practice set

Exam Alert priority #1 is the PV/PVC/StorageClass distinction. Trap 63 — *"A PVC binds to any PV that's big enough"* — is listed in the Common Traps table as a documented target, and the §2 Fixed Point is built to defeat it.

Walking all 17 practice questions: Q1 `emptyDir`/`secret`, Q2 which-object, Q3 reclaim inheritance, Q4 scoping, Q5 `subPath`, Q6 dynamic-provisioning conditions, Q7 access mode, Q8 absent component, Q9 `hostPath`, Q10 StatefulSet claims, Q11 one-mode-at-a-time, Q12 four interfaces, Q13 `storageClassName: ""`, Q14 tmpfs OOM, Q15 Retain sequence, Q16 StatefulSet reschedule, Q17 generic ephemeral.

**None tests binding cardinality or unbound-indefinitely.** Q8 tests *unbound because no provisioner* — a §3 cause, not the §2 mechanism. The only assessment of trap 63 anywhere in the chapter is Bearings #1 Q4, which a reader who skims checkpoints will miss entirely.

PV phases are similarly thin in the practice set: touched only obliquely via Q15's distractor A.

### §C — Bearings #3 and the practice set disagree about how much CSI is worth

The outline says §5 gets **1 of 17** practice items: *"Recall-depth on the exam; one item is proportionate."* The draft honors that (Q12).

Bearings #3 then spends **3 of 5** on the same material: Q1 (what CSI is), Q2 (uninstalled driver), Q5 (which is *not* one of the four pluggable interfaces — a pure book-taxonomy item with no storage content and no CNCF-published referent). Two items remain for StatefulSet.

Both allocations cannot be right. The checkpoint is where a reader calibrates effort; it currently signals that CSI is worth 3× what the practice set says it is worth.

### Secondary: Attention Budget arithmetic

The table sums to **95 minutes** (15+12+6+12+14+8+8+10+6+4); the header states **~85 minutes**. The table also omits Soundings, Why This Chapter Matters, What You'll Learn, Exam Alert, 17 Practice Questions, Chapter Summary, and The Voyage Ahead — of which the practice set alone is 15–20 minutes. Real demand is meaningfully above the stated figure, which under-signals depth for a 5%-allocation chapter. May belong to the structural stage rather than this one; recorded here because it is a depth-signal accuracy problem.

---

## Gaps the research stage flagged

**All blocking gaps are closed.** The outline's Open Questions #2 and #3 named five gaps as blocking or consequential; four new snapshots have since landed and the draft cites all of them.

| Flagged gap | Status | Draft handling |
|---|---|---|
| **G11 — CSI** (outline: "BLOCKING… §5 cannot be drafted") | **CLOSED** | Four snapshots now cited: `csi-spec-objective`, `k8s-docs-volumes-csi-and-subpath`, `k8s-glossary-storage-terms`, `kubernetes-csi-docs-deployment`. The fallback "shrink §5 to naming treatment" was not needed. |
| G12 — volume types | CLOSED | `k8s-docs-volume-types-depth` cited throughout §1 |
| PV phases | CLOSED | Four phases delivered as a table — see disagreement below |
| StorageClass fields | CLOSED | `provisioner`, `parameters`, default annotation, full YAML |
| `volumeBindingMode` / `WaitForFirstConsumer` | CLOSED | §3 + Closer Look |
| Generic ephemeral volumes | CLOSED | §1, full mechanism |
| `subPath` "partial fifth" | CLOSED | General mechanism *and* the Ch 4 promised exception; draft carries an `AUTHOR-REVIEW` comment feeding the Ch 4 retrofit |

### Retrieval-note compliance

**Handled correctly — no action:**

- **`StatefulSetAutoDeletePVC` feature gate** (note: *"DO NOT state a feature-gate requirement or a stability stage"*). Omitted, with an `AUTHOR-REVIEW` comment recording why. Exemplary.
- **PV phase wording** (note: *"Do NOT reproduce these bullets inside quotation marks… without one more verification pass"*). Rendered as an unquoted table. Correct.
- **CSI spec Goals/Non-Goals** (note: recorded as SUMMARY, *"Do not present them inside quotation marks"*). Only the verbatim Objective sentence is quoted. Correct.
- **External-provisioner repository name** (note: omitted as a possible rendering artifact). Not cited. Correct.
- **"Reserving a PersistentVolume"** (note: NOT captured; *"Do not draft any claim about reserving a PV by `volumeName`"*). §2's Snag cites only the verified "Volume Name" fact. Correct.
- **Guardrail #8 on the two trap additions.** The Exam Alert states them as sourced facts and explicitly says they *"have not been assessed for exam frequency the way the seven above have."* This is the discipline the outline demanded, executed precisely.

**Not handled — two findings:**

1. **StatefulSet wording drift.** `k8s-docs-statefulset-storage-2026-08-25` opens with a ⚠ WORDING DRIFT warning: the 08-24 "Stable Storage" text differs from the 08-25 text, *"the difference is load-bearing"* (PersistentVolume**s** vs PersistentVolumeClaim**s**), and the 08-25 version *"is the one that was verifiable on 2026-08-25."* Its NOTE FOR §6 says plainly: **"Lead §6's citation with the retention text."**
   - The §6 ★ Fixed Point leads with the *Stable Storage* sentence and demotes the retention text to "And as a policy default" — the reverse of the instruction.
   - Worse, **Bearings #3 Q3 and Practice Q10 both quote the superseded 08-24 wording** (*"The PersistentVolumeClaim(s) associated with the Pod's PersistentVolume(s) are not deleted…"*), cited to `k8s-docs-statefulset-2026-08-24`. Not a fabrication — the snapshot exists and is cited honestly — but it is the wording the research stage flagged as not re-verifiable, reproduced verbatim in two graded items.

2. **PV phase count: four vs five, unacknowledged.** `k8s-api-ref-persistentvolume-v1-2026-08-25` carries an explicit **⚠ SOURCE DISAGREEMENT**: the API reference enumerates **five** phases (adding `Pending`); the concept page enumerates **four**. Both are Kubernetes-project sources. The draft states four as settled fact — table, Chapter Summary, and Bearings #1 Q5 — with no hedge. Defensible editorially (the concept page is the teaching source), but on a multiple-choice exam a `Pending` distractor is live, and the reader has been given no defense against it.

**Correctly identified as a non-gap:** the CSI ordinal ("third" vs "last"). The corpus states outright that *"the glossary does not rank CSI against CRI, CNI or CRDs, and neither does /docs/concepts/extend-kubernetes/"* — this is an internal-consistency decision, not a curriculum question. The draft's choice of "last," matching shipped Ch 10, is correct and outside this stage's remit.

---

## Recommended fixes

Ordered by priority. Each is scoped to a single issue so the revision stage can take them independently.

### P1 — Reattribute four "exam blueprint" claims to the internal analysis

**The finding.** The cached CNCF curriculum PDF lists D2's competencies as four bare nouns: *"Networking; Security; Troubleshooting; Storage."* It contains no verbs, no learning outcomes, and no phrase resembling "distinguish PV from PVC from StorageClass." The Linux Foundation exam page adds domain percentages and nothing else. **No published KCNA source states what the draft attributes to it, four times:**

| Site | Current text |
|---|---|
| What You'll Learn, bullet 2 | *"the three-way distinction the exam blueprint names explicitly"* |
| §3 🔭 Closer Look | *"The blueprint expects you to distinguish PersistentVolume from PersistentVolumeClaim from StorageClass, not to tune binding modes."* |
| §5 🔭 Closer Look | *"KCNA asks you to name the storage interface and say what it is for."* |
| Exam Alert, priority 1 | *"The KCNA domain expectation names this three-way distinction explicitly, which makes it the highest-confidence claim in this chapter's exam surface."* |

The underlying source is B1's domain analysis — a Lodestar artifact. The *advice* is sound and should stay; the *attribution* transfers a house judgment onto the certifying body, and it is precisely the claim a reader will trust hardest when deciding what to study.

The draft already demonstrates the correct form elsewhere: §4 opens with *"five of the seven exam traps this chapter's domain analysis identified"* — internal, attributed internally. And the Exam Alert's two additions are hedged exactly right. The chapter can do this; it just didn't do it here.

**Fix.** Reword all four to attribute internally. E.g. Exam Alert priority 1 → *"CNCF publishes the Storage competency as a single word. This book's reading of it puts the three-way PV/PVC/StorageClass distinction at the centre, which is why it leads this list."* Same treatment at the other three sites. Mechanical; no content changes.

**Related, P4:** Bearings #3 Q5's answer cites `k8s-docs-extending-kubernetes-2026-08-23` for *"The four are CRI, CRDs, CNI, and CSI."* That page lists those four among a longer set (device plugins, image credential providers, API aggregation, scheduler plugins, webhooks) and does not establish a closed set of four. Practice Q12's stem gets this right — *"described in this book as the four pluggable interfaces"* — so copy Q12's framing into Q5's answer and drop or requalify the citation.

### P1 — Rebalance the practice set toward §2; add a binding-cardinality item

Two changes, one edit pass:

1. **Convert one §1 practice item to a §2 binding item.** Q17 (generic ephemeral volumes) is the best candidate: it is the deepest-below-waterline topic in the set, and its discrimination value against StatefulSet is already carried by the §6 Snag. Replace with an item testing **exclusive one-to-one binding and unbound-indefinitely** — trap 63, currently assessed nowhere in the practice set. The scenario already exists and works: Bearings #1 Q4 (100Gi PV, 10Gi claim binds, 5Gi claim arrives). Rewrite rather than reuse so the checkpoint keeps its item.
2. **Convert a second §1 item.** Q1 and Q14 both test `emptyDir` lifetime from different angles; Q1 additionally overlaps the ladder work done in Bearings #1 Q1. Fold Q1 into §2 as a PV-phase item (`Available`/`Bound`/`Released`/`Failed`), which is currently assessed only obliquely.

Result: §1 5→3, §2 2→4 — the outline's original allocation, restored.

### P2 — Trim §1 to the outline's own guardrail

Two cuts, both surgical:

1. **Projected volumes:** enumerate the four sources the reader has met (`secret`, `downwardAPI`, `configMap`, `serviceAccountToken`), introduced as *"several existing volume sources"* — the research manifest's explicit recommendation. Drop `clusterTrustBundle` and `podCertificate`. Drop the `audience`/`expirationSeconds` numerics, or move them behind a 🔭 marker; they are ServiceAccount-token parameters, not volume-type material, and the reader met the token in Ch 5.
2. **`hostPath` Navigational Hazards:** six consecutive verbatim quotations is a plant that has become a treatment. Keep the two load-bearing ones — *"presents many security risks / if you can avoid using a hostPath volume, you should"* and the container-escape sentence — plus the node-dependence consequence, which is the operationally distinctive one. Compress the admission-time-validation and read-write-subversion quotations to a single sentence. The Ch 12 §5 handoff is unaffected.

### P2 — Rebalance Bearings #3, or revise the outline's §5 allocation

Bearings #3 currently runs 3 CSI / 2 StatefulSet against a practice allocation of 1 CSI / 2 StatefulSet. Pick one:

- **Recommended:** cut Q5 (the four-interfaces taxonomy item — no storage content, no published referent, and it duplicates Practice Q12). Replace with a `volumeClaimTemplates` naming item, taking the checkpoint to 2 CSI / 3 StatefulSet and matching the section's actual teaching weight.
- **Alternative:** if the interface pattern is judged worth the checkpoint slot on cross-chapter grounds, record the deviation against the outline's *"one item is proportionate"* note so Ch 17 §4 doesn't budget for a payoff already spent.

Separately, consider whether Bearings #2 Q3 (`WaitForFirstConsumer` + unschedulable Pod) should survive. It is the chapter's best integration item and its best case of over-depth simultaneously; if it stays, no change is needed, but the outline's own Closer Look framing argues against grading it.

### P2 — Fix the StatefulSet citations to the verified wording

1. **§6 ★ Fixed Point:** invert the citation order. Lead with the retention text (*"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted"* + *"The default for policies is Retain"*), which is the stronger and PVC-accurate claim, then the Stable Storage sentence as support. This is the research manifest's explicit instruction and it is currently reversed.
2. **Bearings #3 Q3 answer and Practice Q10 answer:** both quote the 08-24 wording flagged as not re-verifiable. Replace with the 08-25 text from `k8s-docs-statefulset-storage-2026-08-25`, or restate unquoted and cite. Note the load-bearing difference while editing: the 08-24 wording says *PersistentVolumeClaim(s)… are not deleted*; the 08-25 wording says *PersistentVolumes… are not deleted*. The chapter's Fixed Point is about **PVCs**, so the retention text is the citation that actually supports it.

### P3 — Add one hedge on the PV phase count

The four-phase table is fine as taught. Add one sentence, or a 🪝 Snag, acknowledging that the Kubernetes API reference for `PersistentVolume` v1 additionally documents a `Pending` phase — *"used for PersistentVolumes that are not available"* — while the concept page enumerates four. Two Kubernetes-project sources, two counts. A reader who meets `Pending` as a distractor should recognize it rather than eliminate it.

### P3 — Widen `kb_tags.objectives`

Change `["D2.4"]` to reflect what the chapter teaches: D2.4 primary, with D1.3 (Scheduling), D2.2 (Security), D1.1 (Core Concepts), and D4.2 (Cloud Native Ecosystem and Principles) as secondary. If per-section tagging is available, tag §3 and §5 individually rather than tagging the chapter as a whole. Author's call whether downstream stages should see the secondaries — but the current single tag asserts something measurably false about the chapter.

### P3 — Two small housekeeping items

1. **Orphaned YAML fields.** The §3 StorageClass example carries `allowVolumeExpansion: true` and `mountOptions: [discard]`, both quoted verbatim from the docs and neither glossed anywhere. Either add a half-sentence on volume expansion (it is sourced: *"you can only use the volume expansion feature to grow a Volume, not to shrink it"*) or note that unexplained fields in the example are deliberate and out of scope.
2. **Metadata line denominator.** *"Chapter allocation within domain: ~5% of total exam"* mixes two denominators in one clause — 5% of the total exam is ~18% of the 28% domain. Reword to *"Authored chapter allocation: ~5% of the total exam."* The published-28%-with-source-tag half is correct and should not change.

---

**Summary for the revision stage.** Coverage is complete: every objective the outline claims is delivered, all blocking research gaps are closed, and retrieval-note compliance is strong (the `StatefulSetAutoDeletePVC` omission and the Guardrail #8 hedge on the two trap additions are both handled exactly as instructed). The chapter fails nothing. What it needs is one mechanical reattribution pass on four sentences that credit a house judgment to CNCF, and an allocation correction that moves two practice questions from §1 to §2 so the chapter's stated highest-yield topic is actually assessed.