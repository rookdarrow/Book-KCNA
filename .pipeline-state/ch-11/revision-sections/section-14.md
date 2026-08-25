## ☆ Taking Your Bearings #3

Five questions on CSI, the driver behind it, and the StatefulSet pairing.

**1.** Which statement most accurately describes what CSI is?

A) A storage system maintained by the CNCF that Kubernetes clusters can deploy for persistent volumes
B) A standard interface allowing storage vendors to write one plugin that works across container orchestration systems, without editing core Kubernetes code
C) A Kubernetes-internal API used by the kubelet to mount volumes, not exposed to external vendors
D) The successor to StorageClass, replacing dynamic provisioning with vendor-managed volumes

**2.** An administrator creates a StorageClass whose `provisioner` field names `blockstore.example.com`. The corresponding CSI driver has never been deployed to the cluster. A developer creates a PVC requesting that class and a Pod that mounts it. What is observed?

A) The API server rejects the StorageClass at creation time, since the provisioner does not exist
B) The PVC binds to an existing `Available` PersistentVolume of a different class, since the requested class cannot be satisfied
C) The StorageClass exists and looks correct, the PVC remains unbound, and the Pod stays `Pending`
D) Kubernetes automatically installs the named CSI driver on first use

**3.** *[retrieval: ch6]* You run `kubectl get statefulset` in a namespace and get "No resources found." You then run `kubectl get pvc` in the same namespace and see `www-web-0`, `www-web-1`, and `www-web-2`, all `Bound`. What is the most likely explanation, and what does it tell you about identity and storage?

A) The claims are orphaned by a bug; StatefulSet deletion is supposed to remove them
B) A StatefulSet named `web` was deleted; its per-replica PVCs survive by design and must be removed manually
C) The claims belong to a Deployment, since Deployments also generate per-replica claims
D) The StatefulSet is in a different namespace; PVCs are cluster-scoped and appear everywhere

**4.** A StatefulSet has three replicas and one `volumeClaimTemplate`. `web-1` is running on `node-b`. `node-b` fails and the control plane schedules the replacement `web-1` onto `node-e`. What happens to `web-1`'s storage?

A) A new PVC is created for the replacement Pod on `node-e`, and the old data is lost with the failed node
B) The existing PVC is retained, and the cluster attaches the existing volume to the node where the new Pod launches
C) The data is copied from `node-b` to `node-e` by the StatefulSet controller before the Pod starts
D) The Pod cannot be rescheduled, because a StatefulSet's storage is pinned to its original node

**5.** A StatefulSet named `cache` declares three replicas and two entries in `volumeClaimTemplates`, named `data` and `wal`. Once all three Pods are running, how many PersistentVolumeClaims exist in the namespace, and what are they named?

A) Three — `cache-0`, `cache-1`, and `cache-2`; each Pod receives one claim regardless of how many templates the set declares
B) Six — `data-cache-0` through `data-cache-2`, and `wal-cache-0` through `wal-cache-2`
C) Two — `data-cache` and `wal-cache`; each template produces one claim, which all three Pods mount
D) Six — `cache-data-0` through `cache-data-2`, and `cache-wal-0` through `cache-wal-2`

---

**Answers with Explanations:**

**1 — B.** The specification's own objective: to *"enable storage vendors (SP) to develop a plugin once and have it work across a number of container orchestration (CO) systems"* [source: csi-spec-objective-2026-08-25], and vendors can introduce new storage systems *without ever having to edit the core Kubernetes code* [source: k8s-docs-volumes-2026-08-23].
- **A is wrong** and is the most common CSI misconception: treating an interface as a product. There is no "CSI storage." There are CSI *drivers*, one per storage system.
- **C is wrong** in the crucial respect: CSI is explicitly out-of-tree and vendor-facing. That is its entire purpose.
- **D is wrong**: CSI and StorageClass are complementary. A StorageClass names a provisioner; a CSI driver is what that provisioner often is.

**2 — C.** *To use a CSI driver from a storage provider, you must first deploy it to your cluster* [source: k8s-glossary-storage-terms-2026-08-25], and *the core of Kubernetes does not install that software for you* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. The object exists; the component does not; nothing happens.
- **A is wrong**: the API server does not validate that a provisioner is running. The StorageClass is a perfectly valid object.
- **B is wrong**, and it is the one worth sitting with, because it is the reasonable answer rather than the careless one. Binding is not best-effort matching. A claim that names a class is filtered against that class, and the filter is a requirement, not a preference — alongside capacity, access mode, label selector, and `volumeName`, all ANDed together [source: k8s-docs-persistent-volumes-depth-2026-08-25]. A claim that no volume satisfies stays unbound indefinitely rather than settling for a near miss [source: k8s-docs-persistent-volumes-2026-08-23].
- **D is wrong**, and stating why matters more than the right answer: nothing in Kubernetes installs drivers. This is the fourth instance of the pattern named at Ch 10 §3.

**3 — B.** The citation that speaks about *claims* is the retention policy. A StatefulSet's `persistentVolumeClaimRetentionPolicy` has two settings — `whenDeleted`, for deletion of the StatefulSet itself, and `whenScaled`, for a scale-down — and *the default for policies is `Retain`* [source: k8s-docs-statefulset-storage-2026-08-25]. Unless somebody changed it, deleting `web` left `www-web-0`, `www-web-1`, and `www-web-2` exactly where they were. The documentation adds that the PersistentVolumes behind those claims are not deleted either, and that removing them is manual [source: k8s-docs-statefulset-storage-2026-08-25]. The naming, `<template>-<statefulset>-<ordinal>`, tells you the set was called `web` and had a template called `www`. What it says about identity and storage: the claim is attached to the *name*, not to the workload object, which is why deleting the workload does not disturb it.
- **A is wrong**: this is documented, deliberate behavior, chosen because *data safety... is generally more valuable than an automatic purge* [source: k8s-docs-statefulset-2026-08-24].
- **C is wrong**: Deployments have no `volumeClaimTemplates` field. A Deployment's replicas share whatever claim the PodSpec names, if any.
- **D is wrong** twice over: PVCs are namespaced, not cluster-scoped *[cross-bearing: see Ch 4 §3 — where a name lives]*, and `kubectl get` was run in the namespace.

**4 — B.** *If a Pod associated with a StatefulSet fails due to node failure, and the control plane creates a replacement Pod, the StatefulSet retains the existing PVC. The existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch* [source: k8s-docs-statefulset-storage-2026-08-25].
- **A is wrong**: the replacement `web-1` reuses `www-web-1`, which is the entire point of stable identity.
- **C is wrong**: nothing is copied. The volume is cluster-scoped storage attached at mount time; it was never *on* `node-b` in the sense this answer implies.
- **D is wrong**: this inverts the mechanism. The claim's independence from any node is what *permits* the reschedule.

**5 — B.** *For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim* [source: k8s-docs-statefulset-storage-2026-08-25]. Three Pods against two templates is six claims, and each name is assembled `<template>-<statefulset>-<ordinal>` — template first.
- **A is wrong**, and it is the most reasonable wrong answer here: it remembers "each Pod receives one PersistentVolumeClaim" and drops the clause standing in front of it. The rule is one claim per Pod *per template*.
- **C is wrong**, and it is Deployment-shaped thinking. A single shared claim is what a Deployment's replicas get when the PodSpec names a PVC directly. `volumeClaimTemplates` exists precisely because that is not what a StatefulSet wants *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*.
- **D is wrong** on ordering alone, which is what makes it worth a second look. It gets the count right and the components right, and still names six claims that do not exist. `cache-data-0` looks entirely plausible and matches nothing.

---

**If you scored 0–2:** Re-read §5 and §6, about eighteen minutes. If the misses clustered in questions 3 through 5, the gap is §6 alone, and it repays a re-reading with one question held in mind: what is the claim actually attached to? Every answer in this checkpoint follows from that.

**If you scored 3–4:** Good. You have the interface pattern and the StatefulSet pairing.

**If you scored 5:** You have closed the book's one deliberate forward reference, and with §5 behind you, you hold all four interfaces. Chapter 17 will be a collection exercise rather than a learning one.

---

**Checkpoint: You've Now Mastered**
✓ CSI as the fourth pluggable interface, and as a cross-orchestrator standard rather than a Kubernetes feature
✓ What a CSI driver is — a Deployment plus a DaemonSet, written by somebody outside the project
✓ `volumeClaimTemplates`, the one-claim-per-Pod-per-template rule, and the `<template>-<set>-<ordinal>` name it produces
✓ Why a StatefulSet's storage follows a reschedule, and why identity is the mechanism that makes it possible
✓ That the claims outlive the workload, deliberately, and that cleanup is yours

<!-- AUTHOR-REVIEW: Coverage gap #4 from the question-quality audit — CSI driver architecture (controller Deployment plus per-node DaemonSet, promised at chapter-02:600) — is still untested. The curriculum-alignment audit's prescribed rebalance claimed this checkpoint's fifth slot for a volumeClaimTemplates item, so the two findings compete for the same seat and only one could be seated. The driver-architecture bullet above is therefore asserted from §5's prose rather than confirmed by a graded item. If a slot is found for it, the Practice set is the right home: adding it back here would return CSI to 3 of 5 in this checkpoint against a practice allocation of 1 of 17, which is the imbalance the rebalance was correcting. -->

---