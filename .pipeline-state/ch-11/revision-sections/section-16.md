## Exam Alert! 🚨

**High-Priority Topics:**

1. **PersistentVolume vs PersistentVolumeClaim vs StorageClass.** CNCF publishes the Storage competency as a single word under Container Orchestration. This book's reading of it puts the three-way PV/PVC/StorageClass distinction at the centre, which is why it leads this list. Know: PV is supply and cluster-scoped; PVC is demand and namespaced; StorageClass describes *classes* of storage and enables dynamic provisioning. And know that a Pod references the claim [source: k8s-docs-persistent-volumes-2026-08-23].

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