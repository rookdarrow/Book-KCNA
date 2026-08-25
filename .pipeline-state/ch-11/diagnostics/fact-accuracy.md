# Fact-Accuracy Audit — Chapter 11

**Mode detected: STANDARD.** The `Cached sources` section is populated (19 snapshots), and the draft carries dense inline `[source: ...]` tags throughout. Untagged factual claims are therefore FAIL, not advisory.

**Input note:** `draft-v2.md` was not available; this audit was run against the draft supplied in the prompt body (the stage's fallback, `draft-v1.md`). Line references are approximate and given as section-anchored positions, since the supplied text carries no line numbering.

## Summary

- Total factual claims inspected: 118
- Tagged claims verified: 103
- Tagged claims unverifiable (source tag points to missing/empty snapshot): 0
- **Untagged factual claims (FAIL): 6**
- **Contradicted claims (FAIL): 3**
- Minor discrepancies (WARN): 7

The chapter is unusually well-sourced. Every substantive storage mechanic traces to a cached snapshot, and the tags are accurate at the sentence level rather than gestured at the paragraph level. The failures cluster in three places: (a) claims about *this book's own* prior chapters, which are internally-verifiable rather than externally-sourced and are correctly untagged — those are **not** flagged below; (b) a small set of assertions about Kubernetes behavior that carry no tag and are not derivable from a tagged neighbour; and (c) three places where a quoted or near-quoted sentence has drifted from the snapshot's wording in a way that changes what is being asserted.

Two of the three contradictions are the same root cause: the draft quotes the *superseded* Stable Storage wording, which the 2026-08-25 snapshot explicitly flags as load-bearing drift.

---

## FAIL — Untagged factual claims

### §1, "The volumes that live on rung two", `configMap`/`secret` paragraph: "Both are always mounted read-only [source: k8s-docs-volume-types-depth-2026-08-25]."

**Status:** Tagged, verified — listed here only to contrast with the next item, which sits two sentences later in the same paragraph and is not covered.

### §1, `hostPath` paragraph: "whether the path must already exist, must be a directory, may be created, must be a socket, and so on"

**Why it's a factual claim:** It enumerates the semantics of the `hostPath` `type` field — a specific API behavior. The sentence carries `[source: k8s-docs-volume-types-depth-2026-08-25]`, but that snapshot records only *"In addition to the required `path` property, you can optionally specify a `type` for a `hostPath` volume"* — it does not record the enumerated values or what they check. The enumerated values (`DirectoryOrCreate`, `Directory`, `FileOrCreate`, `File`, `Socket`, `CharDevice`, `BlockDevice`) **are** in `k8s-docs-volumes-2026-08-23`, which is not the tag used.
**Fix:** Retag this clause to `[source: k8s-docs-volumes-2026-08-23]`, which carries the type list, or split the sentence so the `type`-exists claim keeps the depth tag and the enumeration takes the volumes-2026-08-23 tag.

### §2, "Phases" subsection: "A PersistentVolume reports where it stands in its own lifecycle through a phase. There are four, and the third one is the one that catches people."

**Why it's a factual claim:** "There are four" is a count assertion about the API. The table beneath it is tagged, but the count claim precedes the tag and is contradicted by another cached source — `k8s-api-ref-persistentvolume-v1-2026-08-25` enumerates **five** phase values, adding `Pending`, and that snapshot carries an explicit ⚠ SOURCE DISAGREEMENT marker naming exactly this conflict. The draft asserts a bare count without acknowledging the disagreement.
**Fix:** Either scope the count ("the concept documentation names four") with the concept-page tag, or drop the numeral and let the table stand. Do not leave an unqualified "there are four" when a cached, equally-authoritative source says five and flags the conflict itself. This also affects the Chapter Summary row "`Available` → `Bound` → `Released` → (`Failed`)".

### §3, "Defaults, and one opt-out that surprises people": "Most clusters do not make every developer name a class explicitly, because most clusters have a default."

**Why it's a factual claim:** "Most clusters have a default" is an empirical assertion about the installed base. No cached snapshot supports a prevalence claim. The nearest sourced statements are the *mechanism* (a class can be marked default) and the explicit counter-case (*"You can have a cluster without any default StorageClass"*).
**Fix:** Rewrite to the sourced mechanism — "Clusters commonly ship a default class, and where one exists, a PVC that names no class gets it" — or open a research gap for a source establishing prevalence. The following sentence ("why a developer can write a five-line PVC on a managed cloud cluster and get a working disk") inherits the same problem and should be softened with it.

### §5, "What a driver is": "the AWS EBS CSI driver, the Ceph CSI driver, the vSphere CSI driver, each implementing the same contract against different hardware" (🪝 Snag)

**Why it's a factual claim:** Names three specific third-party products and asserts each implements CSI. No cached snapshot names any CSI driver implementation. `kubernetes-csi-docs-deployment-2026-08-25` describes driver *shape* generically; the glossary describes the pattern. The provisioner string `ebs.csi.aws.com` appears again in Taking Your Bearings #3 question 2, likewise unsourced.
**Fix:** These are almost certainly correct, but "almost certainly correct" is what the audit exists to catch. Either open a research gap for a source enumerating well-known CSI drivers (the kubernetes-csi drivers list would serve), or genericize to "a driver per storage system — one for each cloud's block store, one for each software-defined storage project" and keep the untagged sentence non-specific.

### §5, "Why it exists: the world before": "A storage vendor wanting Kubernetes support had to submit code to the Kubernetes project, have it reviewed by Kubernetes maintainers, and wait for a Kubernetes release. Their bug fixes shipped on Kubernetes' schedule. Their code ran inside Kubernetes' binaries, and a defect in it was a defect in the kubelet."

**Why it's a factual claim:** Four consecutive assertions about the historical in-tree development process — review flow, release coupling, blast radius. The tagged sentence immediately above supports only that in-tree plugins were *"built, linked, compiled, and shipped with the core Kubernetes binaries"* and that adding one *"required checking code into the core Kubernetes code repository."* The review-and-release-cadence consequences and the "a defect in it was a defect in the kubelet" claim are reasonable inference, not recorded text.
**Fix:** Mark the paragraph as authored inference explicitly ("Sit with the consequences of that" already gestures at this — make it do the work: "Which meant, in practice: …"), or tag the two derivable clauses to `k8s-docs-volumes-csi-and-subpath-2026-08-25` and cut the kubelet-blast-radius sentence, which is the one genuinely not supported.

### §6, "The reschedule": "That is why a StatefulSet can survive a node failure with its data intact"

**Why it's a factual claim:** A durability guarantee under node failure. It appears *before* the 🔭 Closer Look that supplies the sourced version (*"If a Pod associated with a StatefulSet fails due to node failure … The existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch"* [k8s-docs-statefulset-storage-2026-08-25]). The support exists in the corpus; it is just not attached at the point of assertion.
**Fix:** Attach `[source: k8s-docs-statefulset-storage-2026-08-25]` here. Cheap fix; the snapshot already says it.

---

## FAIL — Contradicted claims

### §6, ★ Fixed Point: "A StatefulSet's PersistentVolumeClaims are not deleted when the Pod is deleted, or when the StatefulSet is deleted."

**Tag:** `[source: k8s-docs-statefulset-storage-2026-08-25]`
**Snapshot says:** *"Note that, the **PersistentVolumes** associated with the Pods' **PersistentVolume Claims** are not deleted when the Pods, or StatefulSet are deleted. This must be done manually."*
**Draft says:** The Fixed Point headline asserts the **PVCs** are not deleted, then quotes the sentence above as its first support — and the quotation as reproduced in the draft is accurate to the snapshot, which means the quoted sentence is about PersistentVolumes, not PersistentVolumeClaims. The headline and its lead evidence are about different objects.
**Why this matters:** The snapshot flags this precise trap in its own NOTE FOR §6: *"the second support is the stronger one … which is a cleaner claim than the Stable Storage sentence (which, in its current wording, is about PersistentVolumes rather than PersistentVolumeClaims). Lead §6's citation with the retention text."* The draft leads with the weaker one and presents it as if it proved the headline.
**Recommended fix:** Reorder the Fixed Point's evidence exactly as the snapshot's note directs. Lead with *"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted"* plus *"The default for policies is Retain"* — both of which are genuinely about PVCs — and demote the Stable Storage sentence to a secondary note about the PersistentVolumes behind them, or cut it. The headline claim is true; the citation order makes it look supported by a sentence that supports something adjacent.

### §6, "One claim per Pod, from a template": "**For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim** [source: k8s-docs-statefulset-2026-08-24]."

**Tag:** `k8s-docs-statefulset-2026-08-24`
**Snapshot says:** The 08-24 snapshot does carry this sentence verbatim. However, `k8s-docs-statefulset-storage-2026-08-25` opens with an explicit ⚠ WORDING DRIFT warning: *"The 'Stable Storage' text recorded below … differs from the text recorded at k8s-docs-statefulset-2026-08-24.md lines 55–57. Where they differ, the difference is load-bearing … This file's version is the one that was verifiable on 2026-08-25."* The 08-25 version reads *"each Pod receives one PersistentVolumeClaim. In the nginx example above, each Pod receives a single **PersistentVolume** with a StorageClass of my-storage-class…"*
**Draft says:** Cites the superseded snapshot for a sentence the newer capture explicitly supersedes, and does so twice more in §6 — for *"The same PersistentVolumeClaim will be bound to a Pod throughout its lifecycle"* and *"when a Pod is (re)scheduled onto a (different) Node, its volumeMounts mount the PersistentVolumeClaim(s) associated with its PersistentVolume(s)"*, neither of which survives into the 08-25 capture in that form. The second is quoted as though verbatim.
**Recommended fix:** Retag the first sentence to `k8s-docs-statefulset-storage-2026-08-25` (which carries it identically and is the verified capture). For the two reschedule sentences, either drop the quotation marks and state the substance as authored prose, or requote from the 08-25 Stable Storage text. Also applies to Practice Question 16's answer explanation, which quotes the reschedule sentence as verbatim from the 08-24 snapshot. The chapter should not quote a snapshot that a later cached capture flags as unverifiable wording.

### §2, "Phases" table, `Released` and `Failed` rows

**Tag:** `[source: k8s-docs-persistent-volumes-depth-2026-08-25]`
**Snapshot says:** The four phase names are recorded — and immediately followed by a RETRIEVAL NOTE: *"The exact prose of the framing sentence and of the `Released` / `Failed` bullets could NOT be independently re-verified … Cite the FOUR NAMES and the substance … **Do NOT reproduce these bullets inside quotation marks in the drafted chapter** without one more verification pass."*
**Draft says:** The table reproduces the bullet prose near-verbatim ("A free resource, not yet bound to a claim" / "The claim has been deleted, but the resource is not yet reclaimed by the cluster" / "The volume has failed its automatic reclamation") under a source tag. The table format arguably avoids literal quotation marks, but the same prose is then quoted *with* quotation marks in Taking Your Bearings #1 answer 5 (*"`Failed` means the volume has failed its automatic reclamation"*, italicized-as-quotation) and again in Taking Your Bearings #2 answers 3 and 4.
**Recommended fix:** Honor the retrieval note. Keep the four names and paraphrase the meanings in the book's own words in the table; strip the quotation formatting from the three checkpoint answers that reproduce the `Released`/`Failed` bullet prose as though verified. The *substance* is cleared for use — only the wording is not.

---

## WARN — Minor discrepancies

**§1, projected volumes source list.** The draft enumerates all six projectable sources (`secret`, `downwardAPI`, `configMap`, `serviceAccountToken`, `clusterTrustBundle`, `podCertificate`), correctly tagged to the 08-25 projected-volumes snapshot. That snapshot's NOTE FOR §1 recommends either that list *or* "several existing volume sources … enumerate only the four the reader has met," noting the older cached snapshot records four. The draft took the six-item option, which is defensible and correctly sourced. Flagged only because `k8s-docs-volumes-2026-08-23` in the same corpus says four, and a reader cross-checking will hit the discrepancy. No edit required.

**§1, generic ephemeral volumes.** The draft never states the stability version (*"Generic ephemeral volumes are stable as of Kubernetes v1.23"*), which the snapshot carries. Not an error — an omission — but the chapter states version facts nowhere, and the KCNA audience may benefit. Optional.

**§3, StorageClass YAML example.** Reproduced faithfully from the snapshot including inline comments. The draft's gloss "`guaranteedReadWriteLatency: "true"` means something to that vendor's driver and nothing at all to the API server" is authored interpretation of a `# provider-specific` comment. Reasonable, unsourced, low risk.

**§4, Dead Reckoning reclaim-policy block.** Compresses two snapshots cleanly, but renders *"Valid options are Retain (default for manually created PersistentVolumes), Delete (default for dynamically provisioned PersistentVolumes), and Recycle (deprecated)"* as a three-clause list with a single trailing tag. The parenthetical defaults are the API reference's exact contribution and are correctly attributed; the `Retain`/`Delete`/`Recycle` descriptions preceding them come from the concept page under a different tag. Consider splitting the tags so the sentence boundary matches the source boundary.

**§4, "Access modes count nodes" opening.** *"two independent filesystem drivers each caching metadata for the same device will corrupt it"* — restated from the Soundings answer, which is itself authored. This is standard storage knowledge and not contradicted by anything cached, but it is a technical assertion carrying no tag anywhere in the chapter. It reads as background rather than as a Kubernetes claim, which is why it is a WARN rather than a FAIL. If the revision wants full coverage, it needs an external source (clustered-filesystem reference) or an explicit "authored" framing.

**§5, "Once installed, the driver's volumes are usable in three ways."** Correctly tagged and accurate. Minor: the draft says *"The first is the path §2 through §4 described"* — true, but the snapshot lists the three ways without ranking them, so "the first" is the draft's ordering, inherited from the snapshot's bullet order. Harmless.

**Exam Alert, item 1: "The KCNA domain expectation names this three-way distinction explicitly."** The CNCF curriculum snapshot lists "Storage" as a competency under Container Orchestration (28%) but does **not** enumerate PV/PVC/StorageClass as a named sub-expectation. The claim that the blueprint "names this three-way distinction explicitly" overstates what the cached curriculum records. Same issue in §3's 🔭 Closer Look: *"The blueprint expects you to distinguish PersistentVolume from PersistentVolumeClaim from StorageClass."* Downgrade to "this chapter's three-way distinction is the highest-confidence exam surface in the Storage competency," or open a research gap for a source that enumerates KCNA sub-competencies at that granularity. Borderline FAIL — recorded as WARN because the domain-and-weight attribution in the chapter header is correct and sourced.

**Chapter header allocation line.** *"Chapter allocation within domain: ~5% of total exam (authored allocation — CNCF publishes four domain weights and no sub-competency weights)"* — this is exemplary. The claim is authored, says so, and states exactly what the source does and does not publish. Noted as the pattern the two items above should follow.

---

## PASS — Verified claims (sampled)

Coverage evidence; each was checked sentence-against-snapshot.

| Claim | Tag | Verdict |
|---|---|---|
| Domain weight 28% for Container Orchestration | `cncf-kcna-curriculum-pdf-2026-08-23` | Exact |
| "the kubelet restarts the container with a clean state" | `k8s-docs-volumes-2026-08-23` | Exact |
| "for any kind of volume in a given Pod, data is preserved across container restarts" | `k8s-docs-volumes-2026-08-23` | Exact |
| "When a Pod ceases to exist, Kubernetes destroys ephemeral volumes" | `k8s-docs-volumes-2026-08-23` | Exact |
| emptyDir: crash-safe, deleted on Pod removal (both halves) | `k8s-docs-volume-types-depth-2026-08-25` | Exact, both sentences |
| tmpfs writes count against the writing container's memory limit | `k8s-docs-volume-types-depth-2026-08-25` | Exact |
| "no limit on how much space an emptyDir or hostPath volume can consume" | `k8s-docs-volumes-csi-and-subpath-2026-08-25` | Exact |
| Full hostPath security warning block (six quoted sentences) | `k8s-docs-volume-types-depth-2026-08-25` | All six exact |
| secret volumes backed by tmpfs, never written to non-volatile storage | `k8s-docs-volume-types-depth-2026-08-25` | Exact |
| `expirationSeconds` defaults to 1 hour, minimum 10 minutes (600s) | `k8s-docs-projected-volumes-2026-08-25` | Exact |
| subPath no-update rule, all three variants (ConfigMap / Secret / downwardAPI) | `k8s-docs-volume-types-depth-2026-08-25` | All three exact |
| Ephemeral volume controller creates a real PVC, deleted with the Pod | `k8s-docs-ephemeral-volumes-2026-08-25` | Exact |
| Deterministic PVC naming + the `pod-a-scratch` collision | `k8s-docs-ephemeral-volumes-2026-08-25` | Exact |
| nfs preserved-and-unmounted vs emptyDir erased | `k8s-docs-volume-types-depth-2026-08-25` | Exact |
| local: static PV only, dynamic provisioning not supported | `k8s-docs-volume-types-depth-2026-08-25` | Exact |
| "Pods consume node resources and PVCs consume PV resources" | `k8s-docs-persistent-volumes-2026-08-23` | Exact |
| PV "captures the details of the implementation of the storage" | `k8s-docs-persistent-volumes-2026-08-23` | Exact |
| Glossary PVC definition (size / access / reclamation split) | `k8s-glossary-storage-terms-2026-08-25` | Exact |
| Claims must exist in the same namespace as the Pod | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| Binding control loop; exclusive one-to-one; unbound indefinitely | `k8s-docs-persistent-volumes-2026-08-23` | All three exact |
| `volumeName`, `storageClassName` match, selector ANDing | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| Storage Object in Use Protection + `kubernetes.io/pvc-protection` | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| StorageClass "classes of storage"; "Kubernetes itself is unopinionated" | `k8s-docs-storage-classes-2026-08-25` | Exact |
| `provisioner`/`parameters`/`reclaimPolicy` field triad | `k8s-docs-storage-classes-2026-08-25` | Exact |
| Static vs dynamic provisioning definitions | `k8s-docs-persistent-volumes-2026-08-23` | Exact |
| Dynamic provisioning's two conditions (Fixed Point) | `k8s-docs-persistent-volumes-2026-08-23` | Exact |
| `storageClassName: ""` disables dynamic provisioning | both PV snapshots | Exact, both |
| No-default-class behavior + retroactive control-plane update | `k8s-docs-storage-classes-2026-08-25` | Exact |
| `volumeBindingMode` / `Immediate` default / unschedulable Pods | `k8s-docs-storage-classes-2026-08-25` | Exact |
| WaitForFirstConsumer constraint list; `nodeName` caveat | `k8s-docs-storage-classes-2026-08-25` | Exact |
| local volumes' independent WFFC argument | `k8s-docs-volume-types-depth-2026-08-25` | Exact |
| All four access modes + CLI abbreviations + one-mode-at-a-time | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| "RWO still can allow multiple Pods … on the same node" | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact — the chapter's load-bearing quote |
| Access mode does not enforce write protection (ROX example) | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| Retain: released, not available, prior claimant's data remains | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| Three-step manual reclamation + "create a new PersistentVolume" | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact, all steps |
| Delete removes PV object *and* external asset | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| Recycle deprecated + `rm -rf /thevolume/*` | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| Dynamic volumes inherit class policy, defaulting to Delete | `k8s-docs-persistent-volumes-depth-2026-08-25` | Exact |
| StorageClass reclaimPolicy unspecified → Delete | `k8s-docs-storage-classes-2026-08-25` | Exact |
| Manually created PVs default to Retain | `k8s-api-ref-persistentvolume-v1-2026-08-25` | Exact |
| CSI standard-interface definition | `k8s-docs-volumes-csi-and-subpath-2026-08-25` | Exact |
| "without ever having to edit the core Kubernetes code" | `k8s-docs-volumes-2026-08-23` | Exact |
| CSI spec Objective sentence (quoted in Fixed Point) | `csi-spec-objective-2026-08-25` | Exact — verbatim-cleared by the snapshot |
| In-tree plugins "built, linked, compiled, and shipped" | `k8s-docs-volumes-csi-and-subpath-2026-08-25` | Exact |
| FlexVolume deprecated; out-of-tree CSI recommended | `k8s-docs-volumes-csi-and-subpath-2026-08-25` | Exact |
| Driver = controller component + per-node DaemonSet | `kubernetes-csi-docs-deployment-2026-08-25` | Exact |
| CSIDriver "captures information about a … driver deployed on the cluster" | `k8s-api-ref-csidriver-v1-2026-08-25` | Exact |
| Three ways to use a csi volume | `k8s-docs-volumes-csi-and-subpath-2026-08-25` | Exact |
| "you must first deploy it to your cluster" | `k8s-glossary-storage-terms-2026-08-25` | Exact |
| "The core of Kubernetes does not install that software for you" | `k8s-docs-volumes-csi-and-subpath-2026-08-25` | Exact |
| CSIMigration behavior + compatibility promise + operations list | `k8s-docs-volumes-csi-and-subpath-2026-08-25` | Exact, all three |
| `volumeClaimTemplates` nginx YAML block | `k8s-docs-statefulset-storage-2026-08-25` | Exact |
| Storage "provisioned by a PersistentVolume Provisioner … or pre-provisioned" | `k8s-docs-statefulset-2026-08-24` | Exact |
| `persistentVolumeClaimRetentionPolicy`, whenDeleted / whenScaled, Retain default | `k8s-docs-statefulset-storage-2026-08-25` | Exact, all parts |
| Node-failure exemption from retention policies | `k8s-docs-statefulset-storage-2026-08-25` | Exact |
| "data safety … more valuable than an automatic purge" | `k8s-docs-statefulset-2026-08-24` | Exact |
| Generic-ephemeral GC contrast (the §6 Snag) | `k8s-docs-ephemeral-volumes-2026-08-25` | Exact |
| Extension-points grouping of CRI/CNI/CSI + CRDs | `k8s-docs-extending-kubernetes-2026-08-23` | Supports the grouping; see note below |

**One note on the last row.** The draft's Practice Question 5 answer says the four interfaces are attested by `k8s-docs-extending-kubernetes-2026-08-23`. That snapshot does list CRI, CNI, CSI (infrastructure extensions) and CRDs (API extensions) — so the *membership* claim is sound. But `k8s-glossary-storage-terms-2026-08-25` carries an explicit NOTE ON ORDINALS: *"the glossary does not rank CSI against CRI, CNI or CRDs, and neither does /docs/concepts/extend-kubernetes/ … Nothing in any source contradicts shipped Ch 10's 'last of the four.'"* The chapter's repeated framing of CSI as "the last of the four" and "the fourth socket" is therefore an **internal-consistency decision inherited from Ch 10, not a sourced fact** — correctly so, and correctly untagged, but the revision stage should know it rests on the book's own prior commitment rather than on Kubernetes documentation. No fix needed; recorded so it isn't mistaken for a citation gap later.

---

## Recommended research gaps to open

1. **KCNA sub-competency granularity** — a source establishing that the blueprint names PV/PVC/StorageClass as an explicit expectation, or confirmation that it does not (in which case soften two passages).
2. **Named CSI driver implementations** — kubernetes-csi drivers list, to support the EBS/Ceph/vSphere enumeration in §5 and the `ebs.csi.aws.com` provisioner string in the §6 checkpoint.
3. **PV phase count reconciliation** — one more retrieval of `/docs/concepts/storage/persistent-volumes/#phase` to settle four-vs-five and clear the `Released`/`Failed` bullet prose for quotation, as the depth snapshot's retrieval note requests.