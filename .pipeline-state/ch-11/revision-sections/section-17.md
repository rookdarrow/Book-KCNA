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

**4.** *[retrieval: ch4]* Which pair correctly describes the scoping of these two objects?

A) PersistentVolume namespaced; PersistentVolumeClaim namespaced
B) PersistentVolume cluster-scoped; PersistentVolumeClaim namespaced
C) PersistentVolume cluster-scoped; PersistentVolumeClaim cluster-scoped
D) PersistentVolume namespaced; PersistentVolumeClaim cluster-scoped

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
- **C** is wrong on the PersistentVolumeClaim, and it is the most reasonable wrong answer here: having correctly placed the PV at cluster scope, it assumes the claim follows its supply. It does not. The claim is the tenant's half of the arrangement, and it lives where the tenant lives — in the same namespace as the Pod that mounts it.
- **D** is wrong on both halves; it inverts the relationship entirely, putting supply inside a namespace and demand outside every namespace.

**5 — C.** *A container using a ConfigMap as a `subPath` volume mount will not receive updates when the ConfigMap changes* [source: k8s-docs-volume-types-depth-2026-08-25].
- **A** and **B** describe whole-volume mount behavior, which is the rule this is the exception to. **D** invents a failure mode. Nothing errors; it simply does not update, which is worse, because it is silent.

**6 — A.** *The PVC must request a storage class and the administrator must have created and configured that class for dynamic provisioning to occur* [source: k8s-docs-persistent-volumes-2026-08-23]. Two conditions.
- **B** describes static provisioning; in fact dynamic provisioning is what happens when *no* matching PV exists. **C** invents a field usage; `volumeName` binds to an existing PV. **D** attaches the mechanism to the wrong thing. A default class decides what happens to a claim that names *no* class; it is not a precondition for provisioning. A claim that names `fast` provisions against `fast` whether or not any class is marked default — and *you can have a cluster without any default StorageClass* [source: k8s-docs-storage-classes-2026-08-25], on which every classless claim simply waits.

**7 — C.** *ReadWriteMany — the volume can be mounted as read-write by many nodes* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Three nodes, all writing.
- **A** would permit only one node. **B** would forbid the writes. **D** would permit only one Pod cluster-wide, which is even more restrictive than A.

**8 — A.** *To use a CSI driver from a storage provider, you must first deploy it to your cluster* [source: k8s-glossary-storage-terms-2026-08-25], and *the core of Kubernetes does not install that software for you* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. The claim stays unbound indefinitely.
- **B** is wrong because there is no retry that ends in a bind. *Claims will remain unbound indefinitely if a matching volume does not exist* [source: k8s-docs-persistent-volumes-2026-08-23] — the binder is a control loop, and a loop reconciling toward a volume that nothing will ever create converges on waiting. This is not a delay before success; it is the terminal state.
- **C** is worth rejecting explicitly: the API server validates schema, not the existence of running components. A StorageClass naming a provisioner nobody deployed is a valid object.
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