## ⚪ §2 — The Claim and the Supply

Before anything else, dispose of a collision that the documentation itself sets up.

You have just spent a section learning that a **volume** is a field in a PodSpec: a thing declared inside a Pod, mounted into its containers, scoped to its lifetime. Now you are going to meet an object called a **PersistentVolume**, and the natural reading is that it is the same noun with a modifier — a volume, but persistent.

It is not. The documentation describes a PersistentVolume as being *volume plugins like Volumes, but* with *a lifecycle independent of any individual Pod that uses the PV* [source: k8s-docs-persistent-volumes-2026-08-23]. That "like Volumes" is precisely what invites the confusion. A `volume` is a field in a PodSpec. A `PersistentVolume` is a cluster-scoped API object with its own name, its own lifecycle, and its own existence independent of every Pod in the cluster. Different things. Similar words. Keep them apart.

Here is the arrangement. The cleanest way in is the documentation's own proportion:

> **Pods consume node resources and PVCs consume PV resources.** [source: k8s-docs-persistent-volumes-2026-08-23]

Read that as an analogy with four terms. A Pod does not create CPU; it requests some, and the scheduler finds a node that has it *[cross-bearing: see Ch 7 §2 — what makes a node feasible]*. A PersistentVolumeClaim does not create storage; it requests some, and a control loop finds a PersistentVolume that has it. The parallel is exact, which is why the documentation reaches for it.

**A PersistentVolume (PV) is a piece of storage in the cluster** that has been provisioned by an administrator or dynamically provisioned using StorageClasses. *It is a resource in the cluster just like a node is a cluster resource.* This API object *captures the details of the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage system* [source: k8s-docs-persistent-volumes-2026-08-23]. That is the supply side: a real piece of storage, described to Kubernetes, sitting in the cluster waiting to be used.

**A PersistentVolumeClaim (PVC) is a request for storage by a user** [source: k8s-docs-persistent-volumes-2026-08-23]. The glossary is even blunter about what it does and does not contain: a claim *specifies the amount of storage, how the storage will be accessed (read-only, read-write and/or exclusive) and how it is reclaimed (retained, recycled or deleted)*, while *details of the storage itself are described in the PersistentVolume object* [source: k8s-glossary-storage-terms-2026-08-25]. A claim says *how much* and *how*. It does not say *which array*.

That split explains something you learned seven chapters ago and probably filed as a fact to memorize. Chapter 4 taught you that a PersistentVolume is cluster-scoped while a PersistentVolumeClaim is namespaced *[cross-bearing: see Ch 4 §3 — where a name lives]*. You now have the reason rather than the rule. Supply is a cluster-wide resource, like a node: it belongs to no team, and the administrator who provisioned it did so for the cluster. Demand comes from a specific application in a specific namespace, and belongs to whoever owns that namespace. The scoping is not an arbitrary API decision; it is the supply/demand split expressed in the API's own vocabulary. The hold belongs to the ship. The claim belongs to whoever is shipping.

And the claim's namespace is load-bearing at consumption time too: *claims must exist in the same namespace as the Pod using the claim. The cluster finds the claim in the Pod's namespace and uses it to get the PersistentVolume backing the claim* [source: k8s-docs-persistent-volumes-depth-2026-08-25].

That leaves the routing detail this whole section exists to fix.

> ★ **Fixed Point**
>
> **PV is supply. PVC is demand. A Pod references the claim — never the volume.**
>
> *Pods use claims as volumes. The cluster inspects the claim to find the bound volume and mounts that volume for a Pod. Users schedule Pods and access their claimed PVs by including a `persistentVolumeClaim` section in a Pod's `volumes` block* [source: k8s-docs-persistent-volumes-2026-08-23].
>
> The Pod's line terminates at the PVC. It never touches the PV. That single routing fact is what lets a developer write a manifest that works on a cluster backed by EBS and on a cluster backed by Ceph without changing a character.

<!-- FIGURE: ch11-fig02-pv-pvc-storageclass-binding -->
```
        SUPPLY                                   DEMAND
   (cluster-scoped)                            (namespaced)
   created by an admin                       created by a user

   ┌───────────────────┐                  ┌────────────────────┐
   │ PersistentVolume  │                  │ PersistentVolume-  │
   │   pv-fast-01      │                  │   Claim  "data"    │
   │   50Gi   RWO      │                  │   requests 20Gi    │
   │   [NFS / EBS /    │                  │   requests RWO     │
   │    Ceph / …]      │                  │   ns: production   │
   └─────────┬─────────┘                  └─────────┬──────────┘
             │                                      │
             │      ┌────────────────────────┐      │
             └─────▶│   BINDING control loop │◀─────┘
                    │  watches for new PVCs, │
                    │  finds a matching PV,  │
                    │  binds them together   │
                    └───────────┬────────────┘
                                │
                       EXCLUSIVE, ONE-TO-ONE
                                │
                                ▼
                    ┌────────────────────────┐
   ┌──────────┐     │   PVC "data" is BOUND  │
   │   Pod    │────▶│   to PV pv-fast-01     │
   └──────────┘     └────────────────────────┘
        ▲
        └── the Pod's line terminates HERE, at the claim.
            It never reaches the PersistentVolume.

   ┌──────────────┐
   │ StorageClass │  ← a third object, off to one side.
   └──────────────┘     Not explained yet. See §3.
```

### Binding

The matching is done by a control loop, and naming it as one costs nothing and buys a great deal: *a control loop in the control plane watches for new PVCs, finds a matching PV (if possible), and binds them together* [source: k8s-docs-persistent-volumes-2026-08-23]. Watch, compare desired against actual, act, repeat. That is the same machinery that runs Deployments, Jobs, and every other controller in the cluster *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*. There is no separate storage subsystem with its own logic. There is a controller, doing what controllers do.

Two properties of binding are exam material and both are counter-intuitive in the same direction: readers expect binding to be looser than it is.

**Binding is exclusive and one-to-one.** *Once bound, PersistentVolumeClaim binds are exclusive, regardless of how they were bound. A PVC to PV binding is a one-to-one mapping* [source: k8s-docs-persistent-volumes-2026-08-23]. A 50Gi PV satisfying a 20Gi claim does not have 30Gi left over for someone else. It is spoken for, entirely, by that claim.

**An unmatched claim waits forever.** *Claims will remain unbound indefinitely if a matching volume does not exist. Claims will be bound as matching volumes become available* [source: k8s-docs-persistent-volumes-2026-08-23]. Not an error. Not a timeout. Not a failure event you can alert on cleanly. The claim simply sits, and a Pod that references it does not start.

> 🪝 **Snag:** "The claim is 20Gi and the PV is 50Gi, so it will fit" is a reasonable guess and a wrong one, because *fits* is not the only criterion. A claim can also specify a `storageClassName`, and *only PVs of the requested class, ones with the same `storageClassName` as the PVC, can be bound to the claim* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. It can specify a label selector, where *only the volumes whose labels match the selector can be bound to the claim* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. All requirements from both `matchLabels` and `matchExpressions` are ANDed together [source: k8s-docs-persistent-volumes-depth-2026-08-25], reusing the selector grammar you already know *[cross-bearing: see Ch 4 §5 — labels and selectors]*. It can even name a specific volume: *a PVC can specify a particular PersistentVolume by name using the `volumeName` field* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Capacity is one filter among several.

### Phases

A PersistentVolume reports where it stands in its own lifecycle through a phase. The concept documentation names four, and the third one is the one that catches people.

| Phase | Meaning |
|---|---|
| `Available` | Provisioned, and no claim has taken it |
| `Bound` | Matched to a claim, and spoken for by that claim alone |
| `Released` | The claim is gone; the cluster has not yet finished with the volume |
| `Failed` | Automatic reclamation was attempted and did not succeed |

[source: k8s-docs-persistent-volumes-depth-2026-08-25]

`Released` is not `Available`. A volume whose claim has been deleted has *left* the bound state without *entering* the free state. Why that gap exists, and what closes it, is §4's business.

> 🪝 **Snag:** Two Kubernetes-project sources count the phases differently, and you should know it before an exam option makes the point for you. The concept documentation names the four above. The API reference for `PersistentVolume` v1 additionally documents a `Pending` phase, *used for PersistentVolumes that are not available* [source: k8s-api-ref-persistentvolume-v1-2026-08-25]. Learn the four — they describe the arc from free to bound to released that this chapter is built on. But if `Pending` turns up as an option, do not eliminate it on the grounds that no such phase exists. It exists. It is simply not one of the four the teaching documentation walks you through.

<!-- AUTHOR-REVIEW: PV phase count remains an open research gap — the concept page enumerates four phases, the v1 API reference five (adding `Pending`), and the cached depth snapshot flags the disagreement itself. The Snag above hedges the reader; a further retrieval of /docs/concepts/storage/persistent-volumes/#phase would settle the count and also clear the `Released`/`Failed` bullet prose for direct quotation. Until then the table paraphrases rather than quotes, per the snapshot's retrieval note. -->

> ⚓ **Worth Securing:** Kubernetes will not let you pull storage out from under a running Pod by accident. *The purpose of the Storage Object in Use Protection feature is to ensure that PersistentVolumeClaims in active use by a Pod and PersistentVolumes that are bound to PVCs are not removed from the system, as this may result in data loss* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. Delete a PVC that a Pod is using and *the PVC is not removed immediately. PVC removal is postponed until the PVC is no longer actively used by any Pods* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. You will see it sitting in `Terminating` with `kubernetes.io/pvc-protection` in its finalizers list. If you have ever run `kubectl delete pvc` and watched it hang, this is why. It is protecting you.

A claim that never binds is, from the Pod's point of view, indistinguishable from a scheduling failure: the Pod sits in `Pending` and nothing happens. Chapter 13 will teach you to tell those two apart from the symptoms *[cross-bearing: see Ch 13 §2 — Pods that never start]*. This chapter supplies the mechanism; that one supplies the diagnosis.

---