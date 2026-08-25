---
source_url: "https://kubernetes.io/docs/reference/kubernetes-api/config-and-storage-resources/csi-driver-v1/"
fetched_at: "2026-08-25T02:48:00-0400"
authority: "Kubernetes project (kubernetes.io API reference)"
objectives_covered: ["D2.4"]
concepts_covered: ["csi-driver", "csi", "generic-ephemeral-volume"]
---
# CSIDriver v1 — API reference field descriptions

Answers, from a normative source, the narrow question "what object appears in the
cluster when a CSI driver is installed?"

## CSIDriver

"CSIDriver captures information about a Container Storage Interface (CSI) volume driver deployed on the cluster."

## spec.attachRequired

"attachRequired indicates this CSI volume driver requires an attach operation (because it implements the CSI ControllerPublishVolume() method)"

## spec.podInfoOnMount

"podInfoOnMount indicates this CSI volume driver requires additional pod information (like podName, podUID, etc.) during mount operations"

## spec.volumeLifecycleModes

"volumeLifecycleModes defines what kind of volumes this CSI volume driver supports. The default if the list is empty is 'Persistent', which is the usage defined by the CSI specification and implemented in Kubernetes via the usual PV/PVC mechanism. The other mode is 'Ephemeral'. In this mode, volumes are defined inline inside the pod spec with CSIVolumeSource and their lifecycle is tied to the lifecycle of that pod."

NOTE FOR §5 — the CSIDriver object is a cluster-scoped API object whose stated job is
to "capture information about a ... driver deployed on the cluster." It is therefore
a second, cleaner instance of the very pattern §2 teaches: an object that DESCRIBES
storage without providing any. Ch 10 line 1870 promised the reader "several objects
in Chapter 11 that describe storage without providing any" — PV, PVC, StorageClass
and CSIDriver are four, and CSIDriver is the one where the description-vs-provision
gap is most literal. Optional; §5's difficulty budget may not have room.
