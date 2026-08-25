## ☆ Taking Your Bearings #2

⚠️ **These questions are intentionally challenging.** Struggle is the point here. Four of the exam traps this chapter's domain analysis identified are tested in this checkpoint alone, and that concentration is not accidental. It is where the material is genuinely counter-intuitive.

Two of the four turn on a decision made by someone who was gone before you came aboard — a reclaim policy inherited from a class nobody named, set by an administrator who is not going to be consulted when the claim is deleted. That is the shape of most storage surprises.

If you find these easy, you have genuinely mastered the highest-yield section of the chapter. If you struggle, you are encoding deeply, and §5 immediately afterward is a straightforward win.

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

<!-- AUTHOR-REVIEW: The curriculum-alignment audit asked whether question 3 should be graded at all, since §3 frames `WaitForFirstConsumer` as 🔭 Closer Look depth above what KCNA asks. Retained: it is the chapter's strongest storage/scheduling integration item, it carries this checkpoint's Ch 7 retrieval tag, and dropping it would put the chapter under its 15-question Bearings budget. Distractors C and D revised per the question-quality audit — C replaced, D's self-defeating justification repaired. -->

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

**5.** A developer writes a PVC with `storageClassName: ""`, on a cluster that has one default StorageClass backed by a working CSI provisioner and no classless PersistentVolumes. What happens?

A) The default StorageClass is used, since an empty string means "unspecified"
B) The PVC is rejected by the API server as invalid
C) The PVC is created, dynamic provisioning is disabled for it, and it remains unbound because no PV without a class exists
D) The PVC binds to the first `Available` PV of any class, since an empty class matches all classes

---

**Answers with Explanations:**

**1 — B.** *ReadWriteOnce access mode still can allow multiple Pods to access the volume when the Pods are running on the same node* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. `pod-a` and `pod-b` share node-1 and can share the volume. `pod-c` is on a different node and cannot.
- **A is wrong**, and it is *the* access-mode trap. RWO counts nodes. The mode that means exactly one Pod is `ReadWriteOncePod`, and its existence is the proof that RWO does not mean that [source: k8s-docs-persistent-volumes-depth-2026-08-25].
- **C is wrong**: the "Once" is a real constraint on nodes, and `pod-c` on node-2 is blocked. Its Pod will not start.
- **D is wrong**: RWO is entirely valid and extremely common; nothing about it prevents binding.

**2 — C.** Follow the chain: no `storageClassName` → the default class applies → that class specifies no `reclaimPolicy` → *if no `reclaimPolicy` is specified when a StorageClass object is created, it will default to `Delete`* [source: k8s-docs-storage-classes-2026-08-25] → *volumes that were dynamically provisioned inherit the reclaim policy of their StorageClass* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Deleting the claim destroys the PV object and the backing asset.
- **A is wrong**: a PVC has no reclaim policy of its own to default. Reclaim policy lives on the PV.
- **B is wrong** in a subtle and instructive way. `Retain` *is* the default for manually created PVs [source: k8s-api-ref-persistentvolume-v1-2026-08-25], but this volume was dynamically provisioned, and the dynamic path has the opposite default. Choosing B means you knew a real fact and applied it to the wrong provisioning path.
- **D is wrong**: deleting a PVC does not *always* delete the storage. It does what the reclaim policy says. Getting the outcome right for the wrong reason is still getting it wrong, and the exam will offer you that option.

**3 — B.** `WaitForFirstConsumer` *will delay the binding and provisioning of a PersistentVolume until a Pod using the PersistentVolumeClaim is created*, and the volume is then *selected or provisioned conforming to the topology that is specified by the Pod's scheduling constraints* [source: k8s-docs-storage-classes-2026-08-25]. The Pod is unschedulable, because no node satisfies its memory request during the filter phase *[cross-bearing: see Ch 7 §2 — what makes a node feasible]*, so the scheduler never picks a node, so binding never proceeds. Both objects sit `Pending`.
- **A is wrong**: that is `Immediate` mode's behavior, which is precisely what `WaitForFirstConsumer` exists to avoid.
- **C is wrong**, and it is the most reasonable of the three, because it assumes the provisioner has some sensible policy of its own — free capacity, spare headroom, whichever zone looks emptiest. It does not. The mode provisions to the topology the *Pod's* scheduling constraints specify, and there are no such constraints to conform to until the scheduler has chosen a node [source: k8s-docs-storage-classes-2026-08-25]. Zone capacity is not an input here. The Pod's node is the input, and there is not going to be one.
- **D is wrong**. `Failed` is a PersistentVolume phase, describing a volume whose automatic reclamation did not succeed [source: k8s-docs-persistent-volumes-depth-2026-08-25] — a storage-lifecycle outcome, not a scheduling one. Nothing here has been reclaimed, or attempted. A Pod that no node can hold waits in `Pending`; it is not marked failed for waiting, and neither is its claim.

**4 — B.** The documented manual reclamation sequence is exactly: delete the PV, clean up the data on the storage asset, delete the asset. And *if you want to reuse the same storage asset, create a new PersistentVolume with the same storage asset definition* [source: k8s-docs-persistent-volumes-depth-2026-08-25].
- **A is wrong**, and it is the `Retain` trap. `Released` is not `Available`: *it is not yet available for another claim because the previous claimant's data remains on the volume* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Nothing binds to it, and no new claim inherits the data.
- **C is wrong**: automatic scrubbing is `Recycle`, which is deprecated [source: k8s-docs-persistent-volumes-depth-2026-08-25]. `Retain` scrubs nothing.
- **D is wrong**: `Retain` never attempts automatic reclamation at all, so it cannot fail at it. The volume is waiting for a person, not for a controller.

**5 — C.** *A PVC with its `storageClassName` set to `""` is explicitly stating that it is bound with a PV with no class, hence the PV's `storageClassName` must also be empty* [source: k8s-docs-persistent-volumes-depth-2026-08-25], and *claims that request the class `""` effectively disable dynamic provisioning for themselves* [source: k8s-docs-persistent-volumes-2026-08-23]. No classless PVs exist, so nothing matches, and nothing will be provisioned.
- **A is wrong** and is the whole point of the question. Omitting the field and setting it to `""` are different acts with different meanings. Only the omission gets the default.
- **B is wrong**: the empty string is entirely valid API input with a defined meaning.
- **D is wrong**: a claim requesting class `""` binds only to PVs whose class is also empty. It matches nothing else.

---

**If you scored 0–2:** This is the hard checkpoint and a low score here is common. Re-read §4 in full, about fourteen minutes, with particular attention to the two ★ Fixed Points and the ⚠ Navigational Hazards block. If only question 3 went wrong, the gap is §3's `WaitForFirstConsumer` subsection rather than §4.

**If you scored 3–4:** Good. This checkpoint was built to be hard. Work out *why* the ones you missed were wrong before continuing; the wrong answers here are all real misconceptions, not filler.

**If you scored 5:** You have the highest-yield material in the chapter and you have it cold. §5 is short and §6 is a payoff.

---

**Checkpoint: You've Now Mastered**
✓ Access modes as node-count semantics, and RWOP as the one exception
✓ The three reclaim policies, including which one is retired
✓ That dynamically provisioned volumes inherit `Delete` by default, from the class
✓ That `Released` requires three manual steps and a new PV object to become reusable
✓ Chapter 6's five deferred verbs, all five closed

One question left, and it is the one that has been implicit since §3: when a provisioner creates a volume, what is actually doing the creating? Something below the waterline has been doing that work for four sections now, and you have not been introduced to it yet.

---