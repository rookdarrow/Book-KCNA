---
source_url: "https://kubernetes.io/docs/concepts/storage/persistent-volumes/"
fetched_at: "2026-09-04T00:00:00-0400"
authority: "Kubernetes project documentation. Text taken from the page's Markdown source in the kubernetes/website repository (main branch, content/en/docs/concepts/storage/persistent-volumes.md), which builds kubernetes.io/docs/concepts/storage/persistent-volumes/."
objectives_covered: ["D2.4"]
concepts_covered: ["pv-phase", "released-not-available", "reclaim-policy", "retain", "empty-storage-class-opt-out", "default-storageclass", "binding"]
---

# Persistent Volumes — Phase, Retain, and Class (kubernetes.io/docs/concepts/storage/persistent-volumes/)

Closes the retrieval gap recorded in k8s-docs-persistent-volumes-depth-2026-08-25.md, whose
RETRIEVAL NOTE said the Phase bullets could not be reproduced inside quotation marks without one
more verification pass. This capture is taken from the page's Markdown source, so the wording
below is verbatim. Hugo shortcodes (`{{< ... >}}`), reviewer front matter and in-page links are
omitted; the page's definition-list markup (`term` on one line, `: definition` on the next) is
rendered here as "term — definition"; hard-wrapped lines are joined.

## Phase

"A PersistentVolume will be in one of the following phases:

`Available` — a free resource that is not yet bound to a claim

`Bound` — the volume is bound to a claim

`Released` — the claim has been deleted, but the associated storage resource is not yet reclaimed by the cluster

`Failed` — the volume has failed its (automated) reclamation

You can see the name of the PVC bound to the PV using `kubectl describe persistentvolume <name>`."

### Phase transition timestamp

"The `.status` field for a PersistentVolume can include an alpha `lastPhaseTransitionTime` field. This field records the timestamp of when the volume last transitioned its phase. For newly created volumes the phase is set to `Pending` and `lastPhaseTransitionTime` is set to the current time."

NOTE — the phase list names four values; the paragraph immediately below it names `Pending` as
the phase of a newly created volume. The v1 API reference (k8s-api-ref-persistentvolume-v1-2026-08-25.md)
enumerates five. The two sources therefore agree in substance: four phases in the lifecycle arc,
plus `Pending` before `Available`. The "alpha" in the transition-timestamp sentence is the page
source's own word and is not cited by the chapter.

## Reclaiming — Retain

"The `Retain` reclaim policy allows for manual reclamation of the resource. When the PersistentVolumeClaim is deleted, the PersistentVolume still exists and the volume is considered "released". But it is not yet available for another claim because the previous claimant's data remains on the volume. An administrator can manually reclaim the volume with the following steps.

1. Delete the PersistentVolume. The associated storage asset in external infrastructure still exists after the PV is deleted.
1. Manually clean up the data on the associated storage asset accordingly.
1. Manually delete the associated storage asset."

## PersistentVolumeClaims — Class

"A claim can request a particular class by specifying the name of a StorageClass using the attribute `storageClassName`. Only PVs of the requested class, ones with the same `storageClassName` as the PVC, can be bound to the PVC."

"PVCs don't necessarily have to request a class. A PVC with its `storageClassName` set equal to `""` is always interpreted to be requesting a PV with no class, so it can only be bound to PVs with no class (no annotation or one set equal to `""`). A PVC with no `storageClassName` is not quite the same and is treated differently by the cluster, depending on whether the `DefaultStorageClass` admission plugin is turned on."

"* If the admission plugin is turned on, the administrator may specify a default StorageClass. All PVCs that have no `storageClassName` can be bound only to PVs of that default. Specifying a default StorageClass is done by setting the annotation `storageclass.kubernetes.io/is-default-class` equal to `true` in a StorageClass object. If the administrator does not specify a default, the cluster responds to PVC creation as if the admission plugin were turned off. If more than one default StorageClass is specified, the newest default is used when the PVC is dynamically provisioned.
* If the admission plugin is turned off, there is no notion of a default StorageClass. All PVCs that have `storageClassName` set to `""` can be bound only to PVs that have `storageClassName` also set to `""`. However, PVCs with missing `storageClassName` can be updated later once default StorageClass becomes available. If the PVC gets updated it will no longer bind to PVs that have `storageClassName` also set to `""`."

"When a PVC specifies a `selector` in addition to requesting a StorageClass, the requirements are ANDed together: only a PV of the requested class and with the requested labels may be bound to the PVC."

### Retroactive default StorageClass assignment

(Page source marks this feature-state "stable" for v1.28.)

"You can create a PersistentVolumeClaim without specifying a `storageClassName` for the new PVC, and you can do so even when no default StorageClass exists in your cluster. In this case, the new PVC creates as you defined it, and the `storageClassName` of that PVC remains unset until default becomes available."

"When a default StorageClass becomes available, the control plane identifies any existing PVCs without `storageClassName`. For the PVCs that either have an empty value for `storageClassName` or do not have this key, the control plane then updates those PVCs to set `storageClassName` to match the new default StorageClass."

NOTE — the wording of the `""` paragraph differs from the version captured in
k8s-docs-persistent-volumes-depth-2026-08-25.md ("is explicitly stating that it is bound with a PV
with no class, hence the PV's `storageClassName` must also be empty"). Both say the same thing;
the chapter may quote either, tagged to the file it quotes.
