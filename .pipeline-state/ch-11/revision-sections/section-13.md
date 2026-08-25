## 🔵 §6 — Pods That Are Not Interchangeable, Revisited

In Chapter 6, you were told that this explanation was incomplete. Not implied. Told, in as many words, with the deferred material enumerated and the deferral labelled deliberate.

This is the missing half, arriving on schedule.

Chapter 6 §6 gave you StatefulSet identity: Pods with stable ordinals, `web-0` and `web-1` and `web-2`, names that stick across rescheduling rather than being regenerated with each replacement *[cross-bearing: see Ch 6 §6 — when Pods are not interchangeable]*. Chapter 9 §6 gave you the network half of that identity: the headless Service and the per-Pod DNS names it produces *[cross-bearing: see Ch 9 §6 — names, and where they resolve]*. What was missing both times was storage, and storage needed the whole of §2 through §4 before it could be explained without hand-waving.

### One claim per Pod, from a template

The mechanism is a field on the StatefulSet: `volumeClaimTemplates`. It looks like this, in the documentation's own nginx example:

```yaml
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      storageClassName: "my-storage-class"
      resources:
        requests:
          storage: 1Gi
```
[source: k8s-docs-statefulset-storage-2026-08-25]

That is a PersistentVolumeClaim spec — the same fields §2 taught you, in the same shapes — sitting inside a workload controller as a template rather than as an object. And the rule for what the controller does with it is one sentence:

**For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim** [source: k8s-docs-statefulset-storage-2026-08-25].

Not one claim for the set. One claim *per Pod*, minted from the template as each Pod is created. A three-replica StatefulSet named `web` with a template named `www` yields three claims, and the naming follows the same ordinal identity Chapter 6 taught, so you can read a cluster's storage from its Pod names and vice versa.

Where those claims get their storage is §3, arriving as a consequence rather than as a rule: *the storage for a given Pod must either be provisioned by a PersistentVolume Provisioner based on the requested storage class, or pre-provisioned by an admin* [source: k8s-docs-statefulset-2026-08-24]. Dynamic or static. The two paths from §3, with nothing special added for StatefulSets.

<!-- FIGURE: ch11-fig05-statefulset-pvc-pairing -->
```
   StatefulSet "web"  ·  volumeClaimTemplates: [ www ]  ·  replicas: 3

     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │  web-0  │        │  web-1  │        │  web-2  │
     └────┬────┘        └────┬────┘        └────┬────┘
          │                  │                  │
          ▼                  ▼                  ▼
     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │ PVC     │        │ PVC     │        │ PVC     │
     │ www-    │        │ www-    │        │ www-    │
     │ web-0   │        │ web-1   │        │ web-2   │
     └─────────┘        └─────────┘        └─────────┘

   ── STATE 1: web-1 is RESCHEDULED to a different node ──────────

     node-a              node-c              node-b
     ┌─────────┐        ┌─────────┐        ┌─────────┐
     │  web-0  │        │  web-1  │◀── moved from node-b
     └────┬────┘        └────┬────┘        └────┬────┘
          │                  │  the claim line   │
          ▼                  ▼  FOLLOWS the Pod  ▼
     [www-web-0]        [www-web-1]        [www-web-2]

   ── STATE 2: web-1 is DELETED ──────────────────────────────────

     ┌─────────┐             ✕             ┌─────────┐
     │  web-0  │        (Pod gone)         │  web-2  │
     └────┬────┘             ╎             └────┬────┘
          │                  ╎                  │
          ▼                  ▼                  ▼
     [www-web-0]        [www-web-1]        [www-web-2]
                        ↑ THE CLAIM REMAINS.
                          Nothing cleans it up.
```

### The reschedule, which is the under-weighted half

Chapter 10 promised you two things about per-replica claims: that they outlive the Pod, and that they outlive *the rescheduling*. Most readers weight the first and skim the second. The second is the more interesting one.

A StatefulSet's Pod keeps the same PersistentVolumeClaim for the whole of its lifecycle, and when that Pod is rescheduled onto a different node, its `volumeMounts` mount that same claim wherever it lands [source: k8s-docs-statefulset-2026-08-24].

<!-- AUTHOR-REVIEW: the 2026-08-25 capture of the StatefulSet "Stable Storage" section flags the 08-24 wording of these two sentences as differing load-bearingly (PersistentVolumes vs PersistentVolumeClaims) and records itself as the verifiable version. The substance is stated here in the book's own words rather than quoted, and the verified 08-25 statement of the same behavior is quoted in the Closer Look below. -->

Note what that does *not* say. It does not say the storage moves. It does not say the data is copied. It says the mount happens wherever the Pod lands, because the Pod's storage is attached to *the claim*, and the claim is not attached to a node at all. The claim is a namespaced API object with no node in it, lashed to no particular deck. The volume behind it is cluster-scoped. Neither one cares which machine `web-1` is running on today.

That is why a StatefulSet can survive a node failure with its data intact [source: k8s-docs-statefulset-storage-2026-08-25], and stating it explicitly explains something otherwise mysterious: the identity you learned in Chapter 6 is not just a naming convention. `web-1` is a name that carries a claim with it. Reschedule the Pod and the claim comes along, because the claim was never anywhere else.

> ⚓ **Worth Securing:** This also explains the constraint you may have wondered about back in Chapter 6: why StatefulSets recreate a Pod with the *same* ordinal rather than just adding a new one. A Deployment's replacement Pod is a new Pod with a new name and no history. A StatefulSet's replacement for `web-1` must be *named* `web-1`, because the name is how it finds `www-web-1`. Identity and storage are one mechanism seen from two sides.

### The claims survive the workload

Now the part that costs people real money.

> ★ **Fixed Point**
>
> **A StatefulSet's PersistentVolumeClaims are not deleted when the Pod is deleted, or when the StatefulSet is deleted. This must be done manually.**
>
> The claims are governed by a retention policy, and that policy's default is to keep them: *Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted* [source: k8s-docs-statefulset-storage-2026-08-25], and *the default for policies is Retain* [source: k8s-docs-statefulset-storage-2026-08-25].
>
> The volumes behind those claims persist alongside them: *the PersistentVolumes associated with the Pods' PersistentVolume Claims are not deleted when the Pods, or StatefulSet are deleted. This must be done manually* [source: k8s-docs-statefulset-storage-2026-08-25]. Read that second sentence carefully and notice which object it is about — the PersistentVolumes, not the claims. Both survive, for different reasons stated in different places. The claims are the ones you will find still sitting in the namespace afterward.
>
> `kubectl delete statefulset web` removes the workload and leaves `www-web-0`, `www-web-1`, and `www-web-2` sitting in the namespace, bound, billing, and invisible to anyone who thinks deleting a workload cleans up after itself.

The reason is stated as a deliberate choice rather than an oversight: *deleting and/or scaling a StatefulSet down will not delete the volumes associated with the StatefulSet. This is done to ensure data safety, which is generally more valuable than an automatic purge of all related StatefulSet resources* [source: k8s-docs-statefulset-2026-08-24].

Read that as a judgment call, because that is what it is. Kubernetes chose the failure mode where the hold stays full of cargo nobody remembers loading over the failure mode where one command puts a database over the side. Given the two, it chose correctly. But it means the cleanup is yours, and nobody will remind you.

> 🔭 **Closer Look: the retention policy field**
>
> That default is configurable. *The optional `.spec.persistentVolumeClaimRetentionPolicy` field controls if and how PVCs are deleted during the lifecycle of a StatefulSet* [source: k8s-docs-statefulset-storage-2026-08-25], with two independently settable policies: `whenDeleted`, which *configures the volume retention behavior that applies when the StatefulSet is deleted*, and `whenScaled`, which *configures the volume retention behavior that applies when the replica count of the StatefulSet is reduced* [source: k8s-docs-statefulset-storage-2026-08-25]. Each takes `Delete` or `Retain`, and `Retain` is the default for both [source: k8s-docs-statefulset-storage-2026-08-25].
>
> One boundary to know: these policies apply only to *voluntary* removal. *If a Pod associated with a StatefulSet fails due to node failure, and the control plane creates a replacement Pod, the StatefulSet retains the existing PVC. The existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch* [source: k8s-docs-statefulset-storage-2026-08-25]. A node dying is not a scale-down. Your data does not get cleaned up because a machine crashed.
>
> <!-- AUTHOR-REVIEW: the retrieval for k8s-docs-statefulset-storage-2026-08-25 also returned a sentence about a StatefulSetAutoDeletePVC feature gate whose current stability stage could not be confirmed. Deliberately omitted rather than stated with a possibly-stale stage. The Retain default is the safe claim and is what is stated above. -->

> 🪝 **Snag:** There is a mechanism elsewhere in this chapter that does the *opposite*, and the contrast is worth holding. A **generic ephemeral volume** also creates a PVC per Pod, and *when the Pod is deleted, the Kubernetes garbage collector deletes the PVC, which then usually triggers deletion of the volume because the default reclaim policy of storage classes is to delete volumes* [source: k8s-docs-ephemeral-volumes-2026-08-25]. Two mechanisms, both creating one claim per Pod, with exactly opposite deletion behavior. The difference is intent: an ephemeral volume is scratch space that happens to be provisioned like real storage, and a StatefulSet's claim is real storage that happens to be created by a controller.

---