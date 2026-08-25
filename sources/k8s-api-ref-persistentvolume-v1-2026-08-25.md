---
source_url: "https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/persistent-volume-v1/"
fetched_at: "2026-08-25T02:47:00-0400"
authority: "Kubernetes project (kubernetes.io API reference)"
objectives_covered: ["D2.4"]
concepts_covered: ["pv-phase", "released-not-available", "reclaim-policy", "retain", "delete", "recycle-deprecated", "inherited-reclaim-policy"]
---
# PersistentVolume v1 — API reference field descriptions

Independent cross-check on the PV phase enumeration and on the reclaim-policy
defaults. This is the API's own normative field documentation, which is why it is
worth carrying alongside the concept page: the concept page teaches, this defines.

## PersistentVolumeStatus — `phase`

"phase indicates if a volume is available, bound to a claim, or released by a claim."

Enumerated values, each quoted exactly:

- `"Available"` — "used for PersistentVolumes that are not yet bound"
- `"Bound"` — "used for PersistentVolumes that are bound"
- `"Failed"` — "used for PersistentVolumes that failed to be correctly recycled or deleted after being released from a claim"
- `"Pending"` — "used for PersistentVolumes that are not available"
- `"Released"` — "used for PersistentVolumes where the bound PersistentVolumeClaim was deleted"

⚠ SOURCE DISAGREEMENT — the API reference enumerates FIVE phase values (it adds
`Pending`); the concept page at /docs/concepts/storage/persistent-volumes/#phase
enumerates FOUR (Available, Bound, Released, Failed). Both are Kubernetes-project
sources. See the manifest's Notes section for the recommended handling.

## PersistentVolumeStatus — `lastPhaseTransitionTime`

"lastPhaseTransitionTime is the time the phase transitioned from one to another and as per storage class semantics the value may be zero."

## PersistentVolumeSpec — `persistentVolumeReclaimPolicy`

"persistentVolumeReclaimPolicy defines what happens to a persistent volume when released from its claim. Valid options are Retain (default for manually created PersistentVolumes), Delete (default for dynamically provisioned PersistentVolumes), and Recycle (deprecated)."

NOTE FOR §4 — this single sentence states BOTH defaults in one place and is the
cleanest available citation for the chapter's second §4 Fixed Point. The concept
page states the dynamic-provisioning default via StorageClass inheritance; this
states it as an API-level default and additionally supplies the manual-creation
default (Retain), which the concept page does not state in those words.
