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

That is not a Kubernetes fact, and no Kubernetes document will tell you so — it is ordinary storage knowledge that the platform inherits from the hardware beneath it. Two independent filesystem drivers, each caching metadata for the same device, will eventually write over each other's bookkeeping and destroy the filesystem. Two crews restowing the same hold from two different manifests lose the cargo, and neither crew notices until somebody goes looking for it.

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

Nobody in that story made a decision about the data's survival. The terms of the arrangement were set once, in a StorageClass manifest, by an administrator who was configuring a cluster and not thinking about this specific developer or this specific volume — standing orders written before this cargo, this shipper, or this voyage existed. The documentation says as much, in the mildest possible terms: *the administrator should configure the StorageClass according to users' expectations; otherwise, the PV must be edited or patched after it is created* [source: k8s-docs-persistent-volumes-depth-2026-08-25].

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