I fetched and verified the storage corpus. **G11 (CSI) is now closed** — §5 is no longer research-blocked — as are all four unanticipated gaps (PV phases, StorageClass fields, `volumeBindingMode`, generic ephemeral volumes). Three new problems surfaced that the outline could not have known about; they're in § Notes.

---

# Research Manifest — KCNA Chapter 11

## Snapshots fetched

| Snapshot | Authority | Objectives | Concepts |
|---|---|---|---|
| `k8s-docs-storage-classes-2026-08-25.md` | Kubernetes project (kubernetes.io/docs) | D2.4 | storageclass, provisioner, storageclass-parameters, default-storageclass, reclaim-policy, volume-binding-mode, wait-for-first-consumer, dynamic-provisioning |
| `k8s-docs-persistent-volumes-depth-2026-08-25.md` | Kubernetes project (kubernetes.io/docs) | D2.4 | pv-phase, released-not-available, reclaim-policy, retain, delete, recycle-deprecated, inherited-reclaim-policy, access-mode, readwriteonce, readonlymany, readwritemany, readwriteoncepod, node-count-semantics, empty-storage-class-opt-out, binding |
| `k8s-api-ref-persistentvolume-v1-2026-08-25.md` | Kubernetes project (API reference) | D2.4 | pv-phase, reclaim-policy, inherited-reclaim-policy |
| `k8s-docs-volumes-csi-and-subpath-2026-08-25.md` | Kubernetes project (kubernetes.io/docs) | D2.4 | csi, csi-driver, csi-migration, in-tree-volume-plugin, fourth-pluggable-interface, subpath, subpath-no-updates |
| `k8s-docs-volume-types-depth-2026-08-25.md` | Kubernetes project (kubernetes.io/docs) | D2.4 | emptydir, emptydir-medium-memory, emptydir-size-limit, hostpath, hostpath-type-field, hostpath-security-risk, configmap-volume, secret-volume, secret-volume-tmpfs, projected-volume, downwardapi-volume, nfs-volume, local-volume |
| `k8s-docs-ephemeral-volumes-2026-08-25.md` | Kubernetes project (kubernetes.io/docs) | D2.4 | generic-ephemeral-volume, ephemeral-volume, csi, wait-for-first-consumer, inherited-reclaim-policy |
| `k8s-docs-projected-volumes-2026-08-25.md` | Kubernetes project (kubernetes.io/docs) | D2.4 | projected-volume, secret-volume, configmap-volume, downwardapi-volume |
| `k8s-docs-statefulset-storage-2026-08-25.md` | Kubernetes project (kubernetes.io/docs) | D2.4 | volumeclaimtemplates, per-replica-pvc, pvc-survives-deletion, persistent-volume-lifetime |
| `k8s-glossary-storage-terms-2026-08-25.md` | Kubernetes project (kubernetes.io/docs glossary) | D2.4 | persistentvolume, persistentvolumeclaim, storageclass, csi, supply-and-demand-split |
| `csi-spec-objective-2026-08-25.md` | Container Storage Interface project (CNCF) | D2.4 | csi, fourth-pluggable-interface |
| `kubernetes-csi-docs-deployment-2026-08-25.md` | Kubernetes CSI community docs (kubernetes-csi.github.io, SIG Storage) | D2.4 | csi-driver, csi, absent-component-pattern |
| `k8s-api-ref-csidriver-v1-2026-08-25.md` | Kubernetes project (API reference) | D2.4 | csi-driver, csi |

**Delivery note on formatting:** every snapshot body below uses **4-space-indented code blocks** rather than triple-backtick fences, so that inner YAML and terminal output do not terminate the outer harvest fence. If the harvester prefers fenced blocks, they can be converted mechanically; the text is unaffected.

---

### A1 · `k8s-docs-storage-classes-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/storage/storage-classes/"
fetched_at: "2026-08-25T02:31:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["storageclass", "provisioner", "storageclass-parameters", "default-storageclass", "reclaim-policy", "inherited-reclaim-policy", "volume-binding-mode", "wait-for-first-consumer", "dynamic-provisioning", "empty-storage-class-opt-out"]
---
# StorageClass (kubernetes.io/docs/concepts/storage/storage-classes/)

Closes the outline's Open-question-#3 gaps "StorageClass fields" and
"volumeBindingMode / WaitForFirstConsumer". Verbatim.

## Introduction

"This document describes the concept of a StorageClass in Kubernetes. Familiarity with volumes and persistent volumes is suggested."

"A StorageClass provides a way for administrators to describe the *classes* of storage they offer. Different classes might map to quality-of-service levels, or to backup policies, or to arbitrary policies determined by the cluster administrators. Kubernetes itself is unopinionated about what classes represent."

"The Kubernetes concept of a storage class is similar to 'profiles' in some other storage system designs."

## StorageClass objects

"Each StorageClass contains the fields `provisioner`, `parameters`, and `reclaimPolicy`, which are used when a PersistentVolume belonging to the class needs to be dynamically provisioned to satisfy a PersistentVolumeClaim (PVC)."

"The name of a StorageClass object is significant, and is how users can request a particular class. Administrators set the name and other parameters of a class when first creating StorageClass objects."

"As an administrator, you can specify a default StorageClass that applies to any PVCs that don't request a specific class."

Example StorageClass given on the page:

    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: low-latency
      annotations:
        storageclass.kubernetes.io/is-default-class: "false"
    provisioner: csi-driver.example-vendor.example
    reclaimPolicy: Retain # default value is Delete
    allowVolumeExpansion: true
    mountOptions:
      - discard # this might enable UNMAP / TRIM at the block storage layer
    volumeBindingMode: WaitForFirstConsumer
    parameters:
      guaranteedReadWriteLatency: "true" # provider-specific

## Default StorageClass

"You can mark a StorageClass as the default for your cluster."

"When a PVC does not specify a `storageClassName`, the default StorageClass is used."

"If you set the `storageclass.kubernetes.io/is-default-class` annotation to true on more than one StorageClass in your cluster, and you then create a PersistentVolumeClaim with no `storageClassName` set, Kubernetes uses the most recently created default StorageClass."

Note: "You should try to only have one StorageClass in your cluster that is marked as the default. The reason that Kubernetes allows you to have multiple default StorageClasses is to allow for seamless migration."

"You can create a PersistentVolumeClaim without specifying a `storageClassName` for the new PVC, and you can do so even when no default StorageClass exists in your cluster. In this case, the new PVC creates as you defined it, and the `storageClassName` of that PVC remains unset until a default becomes available."

"You can have a cluster without any default StorageClass. If you don't mark any StorageClass as default (and one hasn't been set for you by, for example, a cloud provider), then Kubernetes cannot apply that defaulting for PersistentVolumeClaims that need it."

"If or when a default StorageClass becomes available, the control plane identifies any existing PVCs without `storageClassName`. For the PVCs that either have an empty value for `storageClassName` or do not have this key, the control plane then updates those PVCs to set `storageClassName` to match the new default StorageClass. If you have an existing PVC where the `storageClassName` is `""`, and you configure a default StorageClass, then this PVC will not get updated."

"In order to keep binding to PVs with `storageClassName` set to `""` (while a default StorageClass is present), you need to set the `storageClassName` of the associated PVC to `""`."

## Provisioner

"Each StorageClass has a provisioner that determines what volume plugin is used for provisioning PVs. This field must be specified."

"You are not restricted to specifying the 'internal' provisioners listed here (whose names are prefixed with 'kubernetes.io' and shipped alongside Kubernetes). You can also run and specify external provisioners, which are independent programs that follow a specification defined by Kubernetes. Authors of external provisioners have full discretion over where their code lives, how the provisioner is shipped, how it needs to be run, what volume plugin it uses (including Flex), etc."

"For example, NFS doesn't provide an internal provisioner, but an external provisioner can be used. There are also cases when 3rd party storage vendors provide their own external provisioner."

RETRIEVAL NOTE: one further sentence in this section names the external-provisioner
library repository. The retrieval returned that repository name twice in a way that
looks like a rendering artifact, so the sentence is omitted rather than recorded
with possibly-wrong wording. Do not cite a repository name for external provisioners
from this snapshot.

## Reclaim policy

"PersistentVolumes that are dynamically created by a StorageClass will have the reclaim policy specified in the `reclaimPolicy` field of the class, which can be either `Delete` or `Retain`. If no `reclaimPolicy` is specified when a StorageClass object is created, it will default to `Delete`."

"PersistentVolumes that are created manually and managed via a StorageClass will have whatever reclaim policy they were assigned at creation."

## Volume expansion

"PersistentVolumes can be configured to be expandable. This allows you to resize the volume by editing the corresponding PVC object, requesting a new larger amount of storage."

"The following types of volumes support volume expansion, when the underlying StorageClass has the field `allowVolumeExpansion` set to true."

Table on the page — volume type / required Kubernetes version for volume expansion:
Azure File 1.11 · CSI 1.24 · FlexVolume 1.13 · Portworx 1.11 · rbd 1.11

Note: "You can only use the volume expansion feature to grow a Volume, not to shrink it."

## Mount options

"PersistentVolumes that are dynamically created by a StorageClass will have the mount options specified in the `mountOptions` field of the class."

"If the volume plugin does not support mount options but mount options are specified, provisioning will fail. Mount options are **not** validated on either the class or PV. If a mount option is invalid, the PV mount fails."

## Volume binding mode

"The `volumeBindingMode` field controls when volume binding and dynamic provisioning should occur. When unset, `Immediate` mode is used by default."

"The `Immediate` mode indicates that volume binding and dynamic provisioning occurs once the PersistentVolumeClaim is created. For storage backends that are topology-constrained and not globally accessible from all Nodes in the cluster, PersistentVolumes will be bound or provisioned without knowledge of the Pod's scheduling requirements. This may result in unschedulable Pods."

"A cluster administrator can address this issue by specifying the `WaitForFirstConsumer` mode which will delay the binding and provisioning of a PersistentVolume until a Pod using the PersistentVolumeClaim is created. PersistentVolumes will be selected or provisioned conforming to the topology that is specified by the Pod's scheduling constraints. These include, but are not limited to, resource requirements, node selectors, pod affinity and anti-affinity, and taints and tolerations."

"The following plugins support `WaitForFirstConsumer` with dynamic provisioning:
* CSI volumes, provided that the specific CSI driver supports this"

"The following plugins support `WaitForFirstConsumer` with pre-created PersistentVolume binding:
* CSI volumes, provided that the specific CSI driver supports this
* `local`"

Note: "If you choose to use `WaitForFirstConsumer`, do not use `nodeName` in the Pod spec to specify node affinity. If `nodeName` is used in this case, the scheduler will be bypassed and PVC will remain in `pending` state."

## Allowed topologies

"When a cluster operator specifies the `WaitForFirstConsumer` volume binding mode, it is no longer necessary to restrict provisioning to specific topologies in most situations. However, if still required, `allowedTopologies` can be specified."

"This example demonstrates how to restrict the topology of provisioned volumes to specific zones and should be used as a replacement for the `zone` and `zones` parameters for the supported plugins."
```

---

### A2 · `k8s-docs-persistent-volumes-depth-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/storage/persistent-volumes/"
fetched_at: "2026-08-25T02:31:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["pv-phase", "released-not-available", "reclaim-policy", "retain", "delete", "recycle-deprecated", "inherited-reclaim-policy", "access-mode", "readwriteonce", "readonlymany", "readwritemany", "readwriteoncepod", "node-count-semantics", "persistentvolumeclaim", "empty-storage-class-opt-out", "binding", "unbound-claim"]
---
# PersistentVolumes — depth capture (kubernetes.io/docs/concepts/storage/persistent-volumes/)

Companion to k8s-docs-persistent-volumes-2026-08-23.md, which captured the
Introduction and a condensed Lifecycle summary. This file captures the sections
that snapshot was truncated before: Phase, the full Reclaiming sub-parts, Storage
Object in Use Protection, the full Access Modes section, the PersistentVolumeClaims
section, and Claims As Volumes.

## Phase

"A volume will be in one of the following phases:

- `Available` - a free resource that is not yet bound to a claim
- `Bound` - the volume is bound to a claim
- `Released` - the claim has been deleted, but the resource is not yet reclaimed by the cluster
- `Failed` - the volume has failed its automatic reclamation"

"The CLI shows the name of the PVC bound to the PV."

"The `lastPhaseTransitionTime` field in the status shows when a PersistentVolume transitioned to a different phase."

RETRIEVAL NOTE — READ BEFORE CITING WORDING. The four phase NAMES above are
cross-confirmed against the Kubernetes API reference (see
k8s-api-ref-persistentvolume-v1-2026-08-25.md). The exact prose of the framing
sentence and of the `Released` / `Failed` bullets could NOT be independently
re-verified: a second retrieval of this page was truncated before the Phase
subsection, and a third returned a differently-worded framing sentence. Cite the
FOUR NAMES and the substance ("Released = the claim has been deleted but the
resource is not yet reclaimed") with confidence. Do NOT reproduce these bullets
inside quotation marks in the drafted chapter without one more verification pass.

## Reclaiming

"When a user is done with their volume, they can delete the PVC objects from the API that allows reclamation of the resource. The reclaim policy for a PersistentVolume tells the cluster what to do with the volume after it has been released of its claim. Currently, volumes can either be Retained, Recycled, or Deleted."

### Retain

"The `Retain` reclaim policy allows for manual reclamation of the resource. When the PersistentVolumeClaim is deleted, the PersistentVolume still exists and the volume is considered 'released'. But it is not yet available for another claim because the previous claimant's data remains on the volume. An administrator can manually reclaim the volume with the following steps."

"1. Delete the PersistentVolume. The associated storage asset in external infrastructure still exists after the PV is deleted.
2. Manually clean up the data on the associated storage asset accordingly.
3. Manually delete the associated storage asset."

"If you want to reuse the same storage asset, create a new PersistentVolume with the same storage asset definition."

### Delete

"For volume plugins that support the `Delete` reclaim policy, deletion removes both the PersistentVolume object from Kubernetes, as well as the associated storage asset in the external infrastructure. Volumes that were dynamically provisioned inherit the reclaim policy of their StorageClass, which defaults to `Delete`. The administrator should configure the StorageClass according to users' expectations; otherwise, the PV must be edited or patched after it is created."

### Recycle

"**Deprecated:** The `Recycle` reclaim policy is deprecated. Instead, the recommended approach is to use dynamic provisioning."

"If supported by the underlying volume plugin, the `Recycle` reclaim policy performs a basic scrub (`rm -rf /thevolume/*`) on the volume and makes it available again for a new claim."

## Storage Object in Use Protection

"The purpose of the Storage Object in Use Protection feature is to ensure that PersistentVolumeClaims (PVCs) in active use by a Pod and PersistentVolume (PVs) that are bound to PVCs are not removed from the system, as this may result in data loss."

Note: "PVC is in active use by a Pod when a Pod object exists that is using the PVC."

"If a user deletes a PVC in active use by a Pod, the PVC is not removed immediately. PVC removal is postponed until the PVC is no longer actively used by any Pods. Also, if an admin deletes a PV that is bound to a PVC, the PV is not removed immediately. PV removal is postponed until the PV is no longer bound to a PVC."

"You can see that a PVC is protected when the PVC's status is `Terminating` and the `Finalizers` list includes `kubernetes.io/pvc-protection`:"

    kubectl describe pvc hostpath
    Name:          hostpath
    Namespace:     default
    StorageClass:  example-hostpath
    Status:        Terminating
    Volume:
    Labels:        <none>
    Annotations:   volume.beta.kubernetes.io/storage-class=example-hostpath
                   volume.beta.kubernetes.io/storage-provisioner=example.com/hostpath
    Finalizers:    [kubernetes.io/pvc-protection]
    ...

"You can see that a PV is protected when the PV's status is `Terminating` and the `Finalizers` list includes `kubernetes.io/pv-protection` too:"

    kubectl describe pv task-pv-volume
    Name:            task-pv-volume
    Labels:          type=local
    Annotations:     <none>
    Finalizers:      [kubernetes.io/pv-protection]
    StorageClass:    standard
    Status:          Terminating
    Claim:
    Reclaim Policy:  Delete
    Access Modes:    RWO
    Capacity:        1Gi
    Message:
    Source:
        Type:          HostPath (bare host directory volume)
        Path:          /tmp/data
        HostPathType:
    Events:            <none>

## Access Modes

"A PersistentVolume can have any access mode supported by the resource provider. For example, NFS can support multiple read/write clients, but an iSCSI volume can only be used by one client at a time. Each PV gets its own set of access modes describing that specific PV's capabilities."

"The access modes are:

- `ReadWriteOnce` - the volume can be mounted as read-write by a single node. ReadWriteOnce access mode still can allow multiple Pods to access the volume when the Pods are running on the same node. For single Pod access, use ReadWriteOncePod.
- `ReadOnlyMany` - the volume can be mounted as read-only by many nodes.
- `ReadWriteMany` - the volume can be mounted as read-write by many nodes.
- `ReadWriteOncePod` - the volume can be mounted as read-write by a single Pod. Use ReadWriteOncePod access mode if you want to ensure that only one Pod across whole cluster can read and write that PVC. This is only supported for some volume types."

"In the CLI, the access modes are abbreviated as:

- RWO - ReadWriteOnce
- ROX - ReadOnlyMany
- RWX - ReadWriteMany
- RWOP - ReadWriteOncePod"

Important: "A volume can only be mounted using one access mode at a time, even if it supports many. For example, a NFS volume can be mounted as ReadWriteOnce on one node and read-only on another node at the same time, but not on the same node for both read-write and read-only. Additionally, a volume access mode does not enforce write protection. For example, if you provision a ReadOnlyMany volume, it does not prevent an application from writing to the mounted volume if the Pod's securityContext allows write access."

## PersistentVolumeClaims

"A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a Pod. Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., they can be mounted ReadWriteOnce, ReadOnlyMany, ReadWriteMany, or ReadWriteOncePod, see AccessModes)."

"While PersistentVolumeClaims allow a user to consume abstract storage resources, it is common that users need PersistentVolumes with varying properties, such as performance, for different problems. Cluster administrators need to be able to offer a variety of PersistentVolumes that differ in more ways than size and access modes, without exposing users to the details of how those volumes are implemented. For these needs, there is the *StorageClass* resource."

### Access Modes (of a claim)

"Claims can request a particular access mode. For example, a claim might request read-write access or read-only access."

### Volume Modes

"Kubernetes supports two volumeModes of PersistentVolumes: `Filesystem` and `Block`."

"`volumeMode` is an optional API parameter. `Filesystem` is the default mode used when the parameter is omitted."

"A volume with `volumeMode: Filesystem` is *mounted* into Pods into a directory. If the volume is backed by a block device and the device is empty, Kubernetes creates a filesystem on the device before mounting it for the first time."

"You can set the value of `volumeMode` to `Block` to use a volume as a raw block device. Such volumes are presented into a Pod as a block device, without any filesystem on it. This mode is useful to provide a Pod the fastest possible way to access a volume, without any filesystem layer between the Pod and the volume. On the other hand, the application running in the Pod must know how to handle a raw block device."

### Volume Name

"A PVC can specify a particular PersistentVolume by name using the `volumeName` field. For example, if a user prefers a volume named `my-pv`, they can create a PVC with `volumeName: my-pv`. This binds the PVC to the specified PV."

### Resources

"Just as a Pod can request CPU and memory, a claim can request a particular size and access modes. While Claims can only request storage resources, their semantics are expected to evolve to cover other resource types in the future."

### Selector

"Claims can specify a label selector to further filter the set of volumes. Only the volumes whose labels match the selector can be bound to the claim. The selector can consist of two fields:

- `matchLabels` - the volume must have a label with this value
- `matchExpressions` - a list of label requirements to match. Valid operators include In, NotIn, Exists, and DoesNotExist."

"All of the requirements, from both `matchLabels` and `matchExpressions`, are ANDed together – they must all be satisfied for a match."

### Class

"A claim can request a particular class by specifying the name of a StorageClass using the attribute `storageClassName`. Only PVs of the requested class, ones with the same `storageClassName` as the PVC, can be bound to the claim."

"PVCs do not necessarily have to request a class. A PVC with its `storageClassName` set to `""` is explicitly stating that it is bound with a PV with no class, hence the PV's `storageClassName` must also be empty. A PVC with no `storageClassName` is not quite the same and is treated differently by the cluster depending on whether the `DefaultStorageClass` admission plugin is turned on."

"- If the admission plugin is turned on, an administrator may specify a default StorageClass. All PVCs that have no `storageClassName` can be bound only to PVs of that default class. Specifying a default StorageClass is done by setting the annotation `storageclass.kubernetes.io/is-default-class` to `true` in a StorageClass object. If an administrator does not specify a default, the cluster behaves as if the admission plugin is turned off.
- If the admission plugin is turned off, there is no notion of a default StorageClass. All PVCs that have no `storageClassName` can be bound to any PV that has no class. In this case, PVCs with no `storageClassName` are treated the same as PVCs with `storageClassName` set to `""`."

## Claims As Volumes

"Pods access storage by using the claim as a volume. Claims must exist in the same namespace as the Pod using the claim. The cluster finds the claim in the Pod's namespace and uses it to get the PersistentVolume backing the claim. The volume is then mounted into the host and into the Pod."

## NOT captured

The "Reserving a PersistentVolume" section is present on the page but the retrieval
returned it in a form that reads as reworded rather than verbatim. It is deliberately
omitted. Do not draft any claim about reserving a PV by `volumeName` from this file;
the `volumeName` fact recorded under "Volume Name" above is the verified portion.
```

---

### A3 · `k8s-api-ref-persistentvolume-v1-2026-08-25.md` (new)
```markdown
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
```

---

### A4 · `k8s-docs-volumes-csi-and-subpath-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/storage/volumes/#csi"
fetched_at: "2026-08-25T02:34:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["csi", "csi-driver", "csi-migration", "in-tree-volume-plugin", "fourth-pluggable-interface", "subpath", "subpath-no-updates", "emptydir-size-limit"]
---
# Volumes — CSI, subPath and out-of-tree plugins (kubernetes.io/docs/concepts/storage/volumes/)

CLOSES arc-outline blocking gap G11. Retrieved from the page's Markdown source in
the kubernetes/website repository, so the wording below is the docs' own.

## csi

"Container Storage Interface (CSI) defines a standard interface for container orchestration systems (like Kubernetes) to expose arbitrary storage systems to their container workloads."

Note: "Support for CSI spec versions 0.2 and 0.3 is deprecated in Kubernetes v1.13 and will be removed in a future release."

Note: "CSI drivers may not be compatible across all Kubernetes releases. Please check the specific CSI driver's documentation for supported deployment steps for each Kubernetes release and a compatibility matrix."

"Once a CSI-compatible volume driver is deployed on a Kubernetes cluster, users may use the `csi` volume type to attach or mount the volumes exposed by the CSI driver."

"A `csi` volume can be used in a Pod in three different ways:

* through a reference to a PersistentVolumeClaim
* with a generic ephemeral volume
* with a CSI ephemeral volume if the driver supports that"

"The following fields are available to storage administrators to configure a CSI persistent volume:"

* "`driver`: A string value that specifies the name of the volume driver to use. This value must correspond to the value returned in the `GetPluginInfoResponse` by the CSI driver as defined in the CSI spec. It is used by Kubernetes to identify which CSI driver to call out to, and by CSI driver components to identify which PV objects belong to the CSI driver."
* "`volumeHandle`: A string value that uniquely identifies the volume. This value must correspond to the value returned in the `volume.id` field of the `CreateVolumeResponse` by the CSI driver as defined in the CSI spec. The value is passed as `volume_id` in all calls to the CSI volume driver when referencing the volume."
* "`readOnly`: An optional boolean value indicating whether the volume is to be 'ControllerPublished' (attached) as read-only. Default is false. This value is passed to the CSI driver via the `readonly` field in the `ControllerPublishVolumeRequest`."
* "`fsType`: If the PV's `VolumeMode` is `Filesystem`, then this field may be used to specify the filesystem that should be used to mount the volume. If the volume has not been formatted and formatting is supported, this value will be used to format the volume."
* "`volumeAttributes`: A map of string to string that specifies static properties of a volume. This map must correspond to the map returned in the `volume.attributes` field of the `CreateVolumeResponse` by the CSI driver as defined in the CSI spec."
* "`controllerPublishSecretRef`: A reference to the secret object containing sensitive information to pass to the CSI driver to complete the CSI `ControllerPublishVolume` and `ControllerUnpublishVolume` calls. This field is optional, and may be empty if no secret is required."
* "`nodeExpandSecretRef`: A reference to the secret containing sensitive information to pass to the CSI driver to complete the CSI `NodeExpandVolume` call. This field is optional and may be empty if no secret is required."
* "`nodePublishSecretRef`: A reference to the secret object containing sensitive information to pass to the CSI driver to complete the CSI `NodePublishVolume` call. This field is optional and may be empty if no secret is required."
* "`nodeStageSecretRef`: A reference to the secret object containing sensitive information to pass to the CSI driver to complete the CSI `NodeStageVolume` call. This field is optional and may be empty if no secret is required."

### CSI raw block volume support

"Vendors with external CSI drivers can implement raw block volume support in Kubernetes workloads."

"You can set up your PersistentVolume/PersistentVolumeClaim with raw block volume support as usual, without any CSI-specific changes."

### CSI ephemeral volumes

"You can directly configure CSI volumes within the Pod specification. Volumes specified in this way are ephemeral and do not persist across Pod restarts."

### Windows CSI proxy

"CSI node plugins need to perform various privileged operations like scanning of disk devices and mounting of file systems. These operations differ for each host operating system. For Linux worker nodes, containerized CSI node plugins are typically deployed as privileged containers. For Windows worker nodes, privileged operations for containerized CSI node plugins are supported using csi-proxy, a community-managed, stand-alone binary that needs to be pre-installed on each Windows node."

### Migrating to CSI drivers from in-tree plugins

"The `CSIMigration` feature directs operations against existing in-tree plugins to corresponding CSI plugins (which are expected to be installed and configured). As a result, operators do not have to make any configuration changes to existing Storage Classes, PersistentVolumes, or PersistentVolumeClaims (referring to in-tree plugins) when transitioning to a CSI driver that supersedes an in-tree plugin."

Note: "Existing PVs created by an in-tree volume plugin can still be used in the future without any configuration changes, even after the migration to CSI is completed for that volume type, and even after you upgrade to a version of Kubernetes that doesn't have compiled-in support for that kind of storage."

"As part of that migration, you - or another cluster administrator - must have installed and configured the appropriate CSI driver for that storage. The core of Kubernetes does not install that software for you."

"After that migration, you can also define new PVCs and PVs that refer to the legacy, built-in storage integrations. Provided you have the appropriate CSI driver installed and configured, the PV creation continues to work, even for brand-new volumes. The actual storage management now happens through the CSI driver."

"The operations and features that are supported include: provisioning/delete, attach/detach, mount/unmount, and resizing of volumes."

## Using subPath

CLOSES the outline's "partial fifth" gap: subPath as a general mechanism, not only
its no-updates exception.

"Sometimes, it is useful to share one volume for multiple uses in a single Pod. The `volumeMounts[*].subPath` property specifies a sub-path inside the referenced volume instead of its root."

"The following example shows how to configure a Pod with a LAMP stack (Linux, Apache, MySQL, PHP) using a single, shared volume. This sample `subPath` configuration is not recommended for production use."

"The PHP application's code and assets map to the volume's `html` folder and the MySQL database is stored in the volume's `mysql` folder. For example:"

    apiVersion: v1
    kind: Pod
    metadata:
      name: my-lamp-site
    spec:
        containers:
        - name: mysql
          image: mysql
          env:
          - name: MYSQL_ROOT_PASSWORD
            value: "rootpasswd"
          volumeMounts:
          - mountPath: /var/lib/mysql
            name: site-data
            subPath: mysql
        - name: php
          image: php:7.0-apache
          volumeMounts:
          - mountPath: /var/www/html
            name: site-data
            subPath: html
        volumes:
        - name: site-data
          persistentVolumeClaim:
            claimName: my-lamp-site-data

### Using subPath with expanded environment variables

"Use the `subPathExpr` field to construct `subPath` directory names from downward API environment variables. The `subPath` and `subPathExpr` properties are mutually exclusive."

## Resources

"The storage medium (such as Disk or SSD) of an `emptyDir` volume is determined by the medium of the filesystem holding the kubelet root dir (typically `/var/lib/kubelet`). There is no limit on how much space an `emptyDir` or `hostPath` volume can consume, and no isolation between containers or Pods."

## Out-of-tree volume plugins

"The out-of-tree volume plugins include Container Storage Interface (CSI), and also FlexVolume (which is deprecated). These plugins enable storage vendors to create custom storage plugins without adding their plugin source code to the Kubernetes repository."

"Previously, all volume plugins were 'in-tree'. The 'in-tree' plugins were built, linked, compiled, and shipped with the core Kubernetes binaries. This meant that adding a new storage system to Kubernetes (a volume plugin) required checking code into the core Kubernetes code repository."

"Both CSI and FlexVolume allow volume plugins to be developed independently of the Kubernetes code base, and deployed (installed) on Kubernetes clusters as extensions."

### flexVolume (deprecated)

"FlexVolume is an out-of-tree plugin interface that uses an exec-based model to interface with storage drivers. The FlexVolume driver binaries must be installed in a pre-defined volume plugin path on each node, and in some cases, the control plane nodes as well."

Note: "FlexVolume is deprecated. Using an out-of-tree CSI driver is the recommended way to integrate external storage with Kubernetes."
```

---

### A5 · `k8s-docs-volume-types-depth-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/storage/volumes/"
fetched_at: "2026-08-25T02:41:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["emptydir", "emptydir-medium-memory", "emptydir-size-limit", "hostpath", "hostpath-type-field", "hostpath-security-risk", "configmap-volume", "secret-volume", "secret-volume-tmpfs", "projected-volume", "downwardapi-volume", "nfs-volume", "local-volume", "subpath-no-updates"]
---
# Volume types — sentence-level depth capture (kubernetes.io/docs/concepts/storage/volumes/)

Companion to k8s-docs-volumes-2026-08-23.md, which recorded these types in a
condensed one-line-per-type form. This file records the individual sentences
verbatim so §1 can quote rather than restate. Every line below is a direct
quotation from the named section.

## emptyDir

"For a Pod that defines an `emptyDir` volume, the volume is created when the Pod is assigned to a node."

"As the name says, the `emptyDir` volume is initially empty."

"When a Pod is removed from a node for any reason, the data in the `emptyDir` is deleted permanently."

"A container crashing does *not* remove a Pod from a node."

"The data in an `emptyDir` volume is safe across container crashes."

"If you set the `emptyDir.medium` field to `"Memory"`, Kubernetes mounts a tmpfs (RAM-backed filesystem) for you instead."

"While tmpfs is very fast, be aware that, unlike disks, files you write count against the memory limit of the container that wrote them."

"A size limit can be specified for the default medium, which limits the capacity of the `emptyDir` volume."

## configMap

"A container using a ConfigMap as a `subPath` volume mount will not receive updates when the ConfigMap changes."

"A ConfigMap is always mounted as `readOnly`."

## hostPath

"A `hostPath` volume mounts a file or directory from the host node's filesystem into your Pod."

"This is not something that most Pods will need, but it offers a powerful escape hatch for some applications."

Warning box, in full:

"Using the `hostPath` volume type presents many security risks."

"If you can avoid using a `hostPath` volume, you should."

"For example, define a local PersistentVolume, and use that instead."

"If you are restricting access to specific directories on the node using admission-time validation, that restriction is only effective when you additionally require that any mounts of that `hostPath` volume are **read only**."

"If you allow a read-write mount of any host path by an untrusted Pod, the containers in that Pod may be able to subvert the read-write host mount."

"Access to the host filesystem can expose privileged system credentials (such as for the kubelet) or privileged APIs (such as the container runtime socket) that can be used for container escape or to attack other parts of the cluster."

"Pods with identical configuration (such as created from a PodTemplate) may behave differently on different nodes due to different files on the nodes."

"`hostPath` volume usage is not treated as ephemeral storage usage."

"You need to monitor the disk usage by yourself because excessive `hostPath` disk usage will lead to disk pressure on the node."

Type field and uses:

"In addition to the required `path` property, you can optionally specify a `type` for a `hostPath` volume."

"Some uses for a `hostPath` are: running a container that needs access to node-level system components (such as a container that transfers system logs to a central location, accessing those logs using a read-only mount of `/var/log`)"

"making a configuration file stored on the host system available read-only to a static Pod; unlike normal Pods, static Pods cannot access ConfigMaps"

## secret

"A `secret` volume is used to pass sensitive information, such as passwords, to Pods."

"You can store secrets in the Kubernetes API and mount them as files for use by Pods without coupling to Kubernetes directly."

"`secret` volumes are backed by tmpfs (a RAM-backed filesystem), so they are never written to non-volatile storage."

"You must create a Secret in the Kubernetes API before you can use it."

"A Secret is always mounted as `readOnly`."

"A container using a Secret as a `subPath` volume mount will not receive Secret updates."

## projected

"A projected volume maps several existing volume sources into the same directory."

## downwardAPI

"A `downwardAPI` volume makes downward API data available to applications."

"Within the volume, you can find the exposed data as read-only files in plain text format."

"A container using the downward API as a `subPath` volume mount does not receive updates when field values change."

## nfs

"An `nfs` volume allows an existing NFS (Network File System) share to be mounted into a Pod."

"Unlike `emptyDir`, which is erased when a Pod is removed, the contents of an `nfs` volume are preserved, and the volume is merely unmounted."

"This means that an NFS volume can be pre-populated with data, and that data can be shared between Pods."

"NFS can be mounted by multiple writers simultaneously."

"You must have your own NFS server running with the share exported before you can use it."

"Also note that you can't specify NFS mount options in a Pod spec."

"You can also mount NFS volumes via PersistentVolumes, which do allow you to set mount options."

## local

"A `local` volume represents a mounted local storage device such as a disk, partition or directory."

"Local volumes can only be used as a statically created PersistentVolume."

"Dynamic provisioning is not supported."

"Compared to `hostPath` volumes, `local` volumes are used in a durable and portable manner without manually scheduling Pods to nodes."

"The system is aware of the volume's node constraints by looking at the node affinity on the PersistentVolume."

"However, `local` volumes are subject to the availability of the underlying node and are not suitable for all applications."

"If a node becomes unhealthy, then the `local` volume becomes inaccessible to the Pod."

"The Pod using this volume is unable to run."

"Applications using `local` volumes must be able to tolerate this reduced availability, as well as potential data loss, depending on the durability characteristics of the underlying disk."

"You must set a PersistentVolume `nodeAffinity` when using `local` volumes."

"The Kubernetes scheduler uses the PersistentVolume `nodeAffinity` to schedule these Pods to the correct node."

"When using local volumes, it is recommended to create a StorageClass with `volumeBindingMode` set to `WaitForFirstConsumer`."

"Delaying volume binding ensures that the PersistentVolumeClaim binding decision will also be evaluated with any other node constraints the Pod may have, such as node resource requirements, node selectors, Pod affinity, and Pod anti-affinity."

"The local PersistentVolume requires manual cleanup and deletion by the user if the external static provisioner is not used to manage the volume lifecycle."

NOTE FOR §3 — the last two `local` sentences are the docs' own, independent
statement of WHY `WaitForFirstConsumer` exists, phrased as a scheduling-constraint
argument. That is the outline's Ch 7 §2 four-back retrieval, sourced, and it is
worth quoting alongside the StorageClass page's version.
```

---

### A6 · `k8s-docs-ephemeral-volumes-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/storage/ephemeral-volumes/"
fetched_at: "2026-08-25T02:34:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["generic-ephemeral-volume", "ephemeral-volume", "emptydir", "configmap-volume", "secret-volume", "downwardapi-volume", "csi", "wait-for-first-consumer", "inherited-reclaim-policy", "per-replica-pvc"]
---
# Ephemeral Volumes (kubernetes.io/docs/concepts/storage/ephemeral-volumes/)

CLOSES the outline's Open-question-#3 gap "generic ephemeral volumes".

## Introduction

"Some applications need additional storage but don't care whether that data is stored persistently across restarts. For example, caching services are often limited by memory size and can move infrequently used data into storage that is slower than memory with little impact on overall performance."

"Other applications expect some read-only input data to be present in files, like configuration data or secret keys."

"Ephemeral volumes are designed for these use cases. Because volumes follow the Pod's lifetime and get created and deleted along with the Pod, Pods can be stopped and restarted without being limited to where some persistent volume is available."

"Ephemeral volumes are specified inline in the Pod spec, which simplifies application deployment and management."

## Types of ephemeral volumes

"Kubernetes supports several different kinds of ephemeral volumes for different purposes:
- emptyDir: empty at Pod startup, with storage coming locally from the kubelet base directory (usually the root disk) or RAM
- configMap, downwardAPI, secret: inject different kinds of Kubernetes data into a Pod
- image: allows mounting container image files or artifacts, directly to a Pod.
- CSI ephemeral volumes: similar to the previous volume kinds, but provided by special CSI drivers which specifically support this feature
- generic ephemeral volumes, which can be provided by all storage drivers that also support persistent volumes"

"emptyDir, configMap, downwardAPI, secret are provided as local ephemeral storage. They are managed by kubelet on each node."

"CSI ephemeral volumes must be provided by third-party CSI storage drivers."

"Generic ephemeral volumes can be provided by third-party CSI storage drivers, but also by any other storage driver that supports dynamic provisioning. Some CSI drivers are written specifically for CSI ephemeral volumes and do not support dynamic provisioning: those then cannot be used for generic ephemeral volumes."

"The advantage of using third-party drivers is that they can offer functionality that Kubernetes itself does not support, for example storage with different performance characteristics than the disk that is managed by kubelet, or injecting different data."

## CSI ephemeral volumes

"CSI ephemeral volumes are stable as of Kubernetes v1.25."

Note: "CSI ephemeral volumes are only supported by a subset of CSI drivers."

"Conceptually, CSI ephemeral volumes are similar to configMap, downwardAPI and secret volume types: the storage is managed locally on each node and is created together with other local resources after a Pod has been scheduled onto a node. Kubernetes has no concept of rescheduling Pods anymore at this stage. Volume creation has to be unlikely to fail, otherwise Pod startup gets stuck. In particular, storage capacity aware Pod scheduling is not supported for these volumes."

Example manifest for a Pod that uses CSI ephemeral storage:

    kind: Pod
    apiVersion: v1
    metadata:
      name: my-csi-app
    spec:
      containers:
        - name: my-frontend
          image: busybox:1.28
          volumeMounts:
          - mountPath: "/data"
            name: my-csi-inline-vol
          command: [ "sleep", "1000000" ]
      volumes:
        - name: my-csi-inline-vol
          csi:
            driver: inline.storage.kubernetes.io
            volumeAttributes:
              foo: bar

"The volumeAttributes determine what volume is prepared by the driver. These attributes are specific to each driver and not standardized."

### CSI driver restrictions

"CSI ephemeral volumes allow users to provide volumeAttributes directly to the CSI driver as part of the Pod spec. A CSI driver allowing volumeAttributes that are typically restricted to administrators is NOT suitable for use in an inline ephemeral volume. For example, parameters that are normally defined in the StorageClass should not be exposed to users through the use of inline ephemeral volumes."

## Generic ephemeral volumes

"Generic ephemeral volumes are stable as of Kubernetes v1.23."

"Generic ephemeral volumes are similar to emptyDir volumes in the sense that they provide a per-pod directory for scratch data that is usually empty after provisioning. But they may also have additional features:

- Storage can be local or network-attached.
- Volumes can have a fixed size that Pods are not able to exceed.
- Volumes may have some initial data, depending on the driver and parameters.
- Typical operations on volumes are supported assuming that the driver supports them, including snapshotting, cloning, resizing, and storage capacity tracking."

Example:

    kind: Pod
    apiVersion: v1
    metadata:
      name: my-app
    spec:
      containers:
        - name: my-frontend
          image: busybox:1.28
          volumeMounts:
          - mountPath: "/scratch"
            name: scratch-volume
          command: [ "sleep", "1000000" ]
      volumes:
        - name: scratch-volume
          ephemeral:
            volumeClaimTemplate:
              metadata:
                labels:
                  type: my-frontend-volume
              spec:
                accessModes: [ "ReadWriteOnce" ]
                storageClassName: "scratch-storage-class"
                resources:
                  requests:
                    storage: 1Gi

### Lifecycle and PersistentVolumeClaim

"The key design idea is that the parameters for a volume claim are allowed inside a volume source of the Pod. Labels, annotations and the whole set of fields for a PersistentVolumeClaim are supported. When such a Pod gets created, the ephemeral volume controller then creates an actual PersistentVolumeClaim object in the same namespace as the Pod and ensures that the PersistentVolumeClaim gets deleted when the Pod gets deleted."

"That triggers volume binding and/or provisioning, either immediately if the StorageClass uses immediate volume binding or when the Pod is tentatively scheduled onto a node (WaitForFirstConsumer volume binding mode). The latter is recommended for generic ephemeral volumes because then the scheduler is free to choose a suitable node for the Pod. With immediate binding, the scheduler is forced to select a node that has access to the volume once it is available."

"In terms of resource ownership, a Pod that has generic ephemeral storage is the owner of the PersistentVolumeClaim(s) that provide that ephemeral storage. When the Pod is deleted, the Kubernetes garbage collector deletes the PVC, which then usually triggers deletion of the volume because the default reclaim policy of storage classes is to delete volumes. You can create quasi-ephemeral local storage using a StorageClass with a reclaim policy of retain: the storage outlives the Pod, and in this case you need to ensure that volume clean up happens separately."

"While these PVCs exist, they can be used like any other PVC. In particular, they can be referenced as data source in volume cloning or snapshotting. The PVC object also holds the current status of the volume."

### PersistentVolumeClaim naming

"Naming of the automatically created PVCs is deterministic: the name is a combination of the Pod name and volume name, with a hyphen (-) in the middle. In the example above, the PVC name will be my-app-scratch-volume. This deterministic naming makes it easier to interact with the PVC because one does not have to search for it once the Pod name and volume name are known."

"The deterministic naming also introduces a potential conflict between different Pods (a Pod 'pod-a' with volume 'scratch' and another Pod with name 'pod' and volume 'a-scratch' both end up with the same PVC name 'pod-a-scratch') and between Pods and manually created PVCs."

"Such conflicts are detected: a PVC is only used for an ephemeral volume if it was created for the Pod. This check is based on the ownership relationship. An existing PVC is not overwritten or modified. But this does not resolve the conflict because without the right PVC, the Pod cannot start."

Caution: "Take care when naming Pods and volumes inside the same namespace, so that these conflicts can't occur."

### Security

"Using generic ephemeral volumes allows users to create PVCs indirectly if they can create Pods, even if they do not have permission to create PVCs directly. Cluster administrators must be aware of this. If this does not fit their security model, they should use an admission webhook that rejects objects like Pods that have a generic ephemeral volume."

"The normal namespace quota for PVCs still applies, so even if users are allowed to use this new mechanism, they cannot use it to circumvent other policies."

NOTE FOR §1 AND §6 — the generic-ephemeral-volume deletion sentence ("When the Pod
is deleted, the Kubernetes garbage collector deletes the PVC") is the exact MIRROR
of the StatefulSet rule (§6: the PVCs are NOT deleted). Two mechanisms that both
create a PVC per Pod, with opposite deletion behaviour, is a genuinely useful
discrimination item — and the contrast is fully sourced on both sides.
```

---

### A7 · `k8s-docs-projected-volumes-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/storage/projected-volumes/"
fetched_at: "2026-08-25T02:44:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["projected-volume", "secret-volume", "configmap-volume", "downwardapi-volume"]
---
# Projected Volumes (kubernetes.io/docs/concepts/storage/projected-volumes/)

Pays the chapter-05:775 debt ("Ch 11 — projected volumes"), which was dropped where
TokenRequest tokens are mounted.

## Introduction

"A `projected` volume maps several existing volume sources into the same directory."

## Volume sources that can be projected

"Currently, the following types of volume sources can be projected:

* `secret`
* `downwardAPI`
* `configMap`
* `serviceAccountToken`
* `clusterTrustBundle`
* `podCertificate`"

## serviceAccountToken projected volumes

"You can inject the token for the current service account into a Pod at a specified path."

"The `audience` field contains the intended audience of the token."

"The `expirationSeconds` is the expected duration of validity of the service account token. It defaults to 1 hour and must be at least 10 minutes (600 seconds)."

NOTE FOR §1 — the source list above is the payable form of the Ch 5 promise: the
projected volume the reader already met carrying a ServiceAccount token is the same
mechanism with `serviceAccountToken` as one of six named sources. Note also that the
current list has SIX entries (adding `clusterTrustBundle` and `podCertificate`),
whereas the cached k8s-docs-volumes-2026-08-23.md line 19 records FOUR
(secret, downwardAPI, configMap, serviceAccountToken). Prefer this file's list, or
say "several existing volume sources" and enumerate only the four the reader has met.
```

---

### A8 · `k8s-docs-statefulset-storage-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/"
fetched_at: "2026-08-25T02:36:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["volumeclaimtemplates", "per-replica-pvc", "pvc-survives-deletion", "persistent-volume-lifetime", "statefulset"]
---
# StatefulSets — storage sections (kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

Companion to k8s-docs-statefulset-2026-08-24.md. Captures the example manifest (for
the volumeClaimTemplates block and the PVC naming the outline needs) and the
PersistentVolumeClaim-retention section, which that snapshot does not contain.

⚠ WORDING DRIFT — READ BEFORE CITING. The "Stable Storage" text recorded below,
retrieved 2026-08-25 from the page's Markdown source, differs from the text recorded
at k8s-docs-statefulset-2026-08-24.md lines 55–57. Where they differ, the difference
is load-bearing. See the manifest's Notes section. This file's version is the one
that was verifiable on 2026-08-25.

## Components (the example)

"The example below demonstrates the components of a StatefulSet."

    apiVersion: v1
    kind: Service
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      ports:
      - port: 80
        name: web
      clusterIP: None
      selector:
        app: nginx
    ---
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
      name: web
    spec:
      selector:
        matchLabels:
          app: nginx # has to match .spec.template.metadata.labels
      serviceName: "nginx"
      replicas: 3 # by default is 1
      minReadySeconds: 10 # by default is 0
      template:
        metadata:
          labels:
            app: nginx # has to match .spec.selector.matchLabels
        spec:
          terminationGracePeriodSeconds: 10
          containers:
          - name: nginx
            image: registry.k8s.io/nginx-slim:0.24
            ports:
            - containerPort: 80
              name: web
            volumeMounts:
            - name: www
              mountPath: /usr/share/nginx/html
      volumeClaimTemplates:
      - metadata:
          name: www
        spec:
          accessModes: [ "ReadWriteOnce" ]
          storageClassName: "my-storage-class"
          resources:
            requests:
              storage: 1Gi

Note: "This example uses the ReadWriteOnce access mode, for simplicity. For production use, the Kubernetes project recommends using the ReadWriteOncePod access mode instead."

"In the above example:

* A Headless Service, named nginx, is used to control the network domain.
* The StatefulSet, named web, has a Spec that indicates that 3 replicas of the nginx container will be launched in unique Pods.
* The volumeClaimTemplates will provide stable storage using PersistentVolumes provisioned by a PersistentVolume Provisioner."

## Stable Storage

"For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim. In the nginx example above, each Pod receives a single PersistentVolume with a StorageClass of my-storage-class and 1 GiB of provisioned storage. If no StorageClass is specified, then the default StorageClass will be used. When a Pod is (re)scheduled onto a node, its volumeMounts mount the PersistentVolumes associated with its PersistentVolume Claims. Note that, the PersistentVolumes associated with the Pods' PersistentVolume Claims are not deleted when the Pods, or StatefulSet are deleted. This must be done manually."

## PersistentVolumeClaim retention

"The optional .spec.persistentVolumeClaimRetentionPolicy field controls if and how PVCs are deleted during the lifecycle of a StatefulSet."

"there are two policies you can configure for each StatefulSet:"

"whenDeleted: Configures the volume retention behavior that applies when the StatefulSet is deleted."

"whenScaled: Configures the volume retention behavior that applies when the replica count of the StatefulSet is reduced; for example, when scaling down the set."

"For each policy that you can configure, you can set the value to either Delete or Retain."

"Delete: The PVCs created from the StatefulSet volumeClaimTemplate are deleted for each Pod affected by the policy. With the whenDeleted policy all PVCs from the volumeClaimTemplate are deleted after their Pods have been deleted. With the whenScaled policy, only PVCs corresponding to Pod replicas being scaled down are deleted, after their Pods have been deleted."

"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted. This is the behavior before this new feature."

"Bear in mind that these policies only apply when Pods are being removed due to the StatefulSet being deleted or scaled down. For example, if a Pod associated with a StatefulSet fails due to node failure, and the control plane creates a replacement Pod, the StatefulSet retains the existing PVC. The existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch."

"The default for policies is Retain, matching the StatefulSet behavior before this new feature."

Example policy shown on the page:

    apiVersion: apps/v1
    kind: StatefulSet
    ...
    spec:
      persistentVolumeClaimRetentionPolicy:
        whenDeleted: Retain
        whenScaled: Delete
    ...

"The StatefulSet controller adds owner references to its PVCs, which are then deleted by the garbage collector after the Pod is terminated. This enables the Pod to cleanly unmount all volumes before the PVCs are deleted (and before the backing PV and volume are deleted, depending on the retain policy). When you set the whenDeleted policy to Delete, an owner reference to the StatefulSet instance is placed on all PVCs associated with that StatefulSet."

RETRIEVAL NOTE — the retrieval also returned a sentence stating that the
`StatefulSetAutoDeletePVC` feature gate must be enabled on the API server and the
controller manager to use `persistentVolumeClaimRetentionPolicy`. That sentence
almost certainly sits adjacent to a feature-state marker that the retrieval stripped,
and the gate's current stage could not be confirmed in this pass. DO NOT state a
feature-gate requirement or a stability stage for this field in the drafted chapter.
The behaviour that IS safe to state is the default: Retain, for both policies.

NOTE FOR §6 — the PVC-survival Fixed Point is supported here TWICE, and the second
support is the stronger one. "Retain (default): PVCs from the volumeClaimTemplate are
not affected when their Pod is deleted" plus "The default for policies is Retain"
establishes PVC survival as a default policy value, which is a cleaner claim than the
Stable Storage sentence (which, in its current wording, is about PersistentVolumes
rather than PersistentVolumeClaims). Lead §6's citation with the retention text.
```

---

### A9 · `k8s-glossary-storage-terms-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes.io/docs/reference/glossary/?all=true"
fetched_at: "2026-08-25T02:33:00-0400"
authority: "Kubernetes project (kubernetes.io/docs standardized glossary)"
objectives_covered: ["D2.4"]
concepts_covered: ["persistentvolume", "persistentvolumeclaim", "storageclass", "csi", "csi-driver", "supply-and-demand-split", "static-provisioning", "dynamic-provisioning"]
---
# Kubernetes glossary — storage terms

Four canonical one-paragraph definitions. These are the project's own controlled
vocabulary and are the shortest defensible definitions available for §2, §3 and §5.
Individual term source files, all under kubernetes/website content/en/docs/reference/glossary/.

## Persistent Volume
(term id: persistent-volume · full_link: /docs/concepts/storage/persistent-volumes/)

short_description: "API object that represents a piece of storage in the cluster."

"An API object that represents a piece of storage in the cluster. Representation of as a general, pluggable storage resource that can persist beyond the lifecycle of any individual Pod."

"PersistentVolumes (PVs) provide an API that abstracts details of how storage is provided from how it is consumed. PVs are used directly in scenarios where storage can be created ahead of time (static provisioning). For scenarios that require on-demand storage (dynamic provisioning), PersistentVolumeClaims (PVCs) are used instead."

## Persistent Volume Claim
(term id: persistent-volume-claim · full_link: /docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)

short_description: "Claims storage resources defined in a PersistentVolume so that it can be mounted as a volume in a container."

"Claims storage resources defined in a PersistentVolume, so that the storage can be mounted as a volume in a container."

"Specifies the amount of storage, how the storage will be accessed (read-only, read-write and/or exclusive) and how it is reclaimed (retained, recycled or deleted). Details of the storage itself are described in the PersistentVolume object."

## Storage Class
(term id: storageclass · full_link: /docs/concepts/storage/storage-classes)

short_description: "A StorageClass provides a way for administrators to describe different available storage types."

"StorageClasses can map to quality-of-service levels, backup policies, or to arbitrary policies determined by cluster administrators. Each StorageClass contains the fields `provisioner`, `parameters`, and `reclaimPolicy`, which are used when a Persistent Volume belonging to the class needs to be dynamically provisioned. Users can request a particular class using the name of a StorageClass object."

## Container Storage Interface (CSI)
(term id: csi · full_link: /docs/concepts/storage/volumes/#csi · tags: storage)

short_description: "The Container Storage Interface (CSI) defines a standard interface to expose storage systems to containers."

"The Container Storage Interface (CSI) defines a standard interface to expose storage systems to containers."

"CSI allows vendors to create custom storage plugins for Kubernetes without adding them to the Kubernetes repository (out-of-tree plugins). To use a CSI driver from a storage provider, you must first deploy it to your cluster. You will then be able to create a Storage Class that uses that CSI driver."

NOTE FOR §5 AND §3 — the last CSI sentence is the sourced form of the outline's
absent-component payoff. The docs state the ORDER as a requirement: deploy the driver
FIRST, then you are able to create a StorageClass that uses it. A StorageClass naming
an undeployed driver is therefore not an edge case the reader has to imagine — it is
the documented prerequisite, unmet.

NOTE ON ORDINALS — the glossary does not rank CSI against CRI, CNI or CRDs, and
neither does /docs/concepts/extend-kubernetes/ (see the cached
k8s-docs-extending-kubernetes-2026-08-23.md, which lists them without ordering).
Nothing in any source contradicts shipped Ch 10's "last of the four." Open question
#1 is an internal-consistency decision, not a factual one; the sources are silent.
```

---

### A10 · `csi-spec-objective-2026-08-25.md` (new)
```markdown
---
source_url: "https://github.com/container-storage-interface/spec/blob/master/spec.md"
fetched_at: "2026-08-25T02:39:00-0400"
authority: "Container Storage Interface project (CNCF; container-storage-interface/spec)"
objectives_covered: ["D2.4"]
concepts_covered: ["csi", "fourth-pluggable-interface", "csi-driver"]
---
# Container Storage Interface specification — Objective

The interface's own statement of purpose, from the specification document rather than
from Kubernetes documentation about it. This is the right citation for §5's Fixed
Point, because the Fixed Point is about CSI being a *published contract between two
parties* rather than a Kubernetes feature — and the spec is the contract.

## Objective

"define an industry standard 'Container Storage Interface' (CSI) that will enable storage vendors (SP) to develop a plugin once and have it work across a number of container orchestration (CO) systems."

## Goals in MVP (as summarised by the specification's own bullet list)

The specification's stated goals include: enabling SP authors to write one CSI
compliant Plugin that "just works" across all COs that implement CSI; defining APIs
(RPCs) for dynamic provisioning and deprovisioning of volumes, attaching and
detaching volumes from nodes, mounting and unmounting volumes, consumption of block
and mountable volumes, support for local storage providers, and creation and deletion
of snapshots; and defining plugin protocol recommendations.

## Non-Goals in MVP

The specification explicitly does not define mechanisms for Plugin Supervisor
lifecycle management, deployment/installation/upgrade/uninstall/monitoring, a
first-class message structure for storage grades, protocol-level authentication and
authorization, plugin packaging, or POSIX compliance guarantees.

"SHALL NOT obstruct a Plugin Supervisor or CO from interacting with Plugin-managed volumes in a POSIX-compliant manner."

RETRIEVAL NOTE — the Objective sentence and the closing POSIX sentence are verbatim
quotations. The "Goals in MVP" and "Non-Goals in MVP" paragraphs are the retrieval's
condensation of the spec's bullet lists and are recorded as SUMMARY, not verbatim.
Do not present them inside quotation marks in the drafted chapter. The Objective
sentence alone carries everything §5 actually needs.

NOTE FOR §5 — the phrase "across a number of container orchestration (CO) systems"
is worth noticing: CSI is not a Kubernetes interface that vendors happen to use, it
is a cross-orchestrator standard that Kubernetes happens to implement. That is a
sharper version of the §5 Fixed Point than the Kubernetes docs can supply, and it is
the same claim shape as OCI in Ch 2 (see the cached oci-overview snapshot).
```

---

### A11 · `kubernetes-csi-docs-deployment-2026-08-25.md` (new)
```markdown
---
source_url: "https://kubernetes-csi.github.io/docs/introduction.html"
fetched_at: "2026-08-25T02:36:00-0400"
authority: "Kubernetes CSI Developer Documentation (kubernetes-csi.github.io; Kubernetes SIG Storage)"
objectives_covered: ["D2.4"]
concepts_covered: ["csi", "csi-driver", "absent-component-pattern"]
---
# Kubernetes CSI Developer Documentation — introduction and deployment shape

Pays the chapter-02:600 debt, which used the word *drivers*: this is what a CSI
driver is and what deploying one puts into a cluster. Linked to from the Kubernetes
glossary entry for CSI as the canonical deployment reference.

## Introduction (https://kubernetes-csi.github.io/docs/introduction.html)

"This site documents how to develop, deploy, and test a Container Storage Interface (CSI) driver on Kubernetes."

"The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Container Orchestration Systems (COs) like Kubernetes."

"Using CSI third-party storage providers can write and deploy plugins exposing new storage systems in Kubernetes without ever having to touch the core Kubernetes code."

## Deploying a CSI driver (https://kubernetes-csi.github.io/docs/deploying.html)

"A CSI driver is typically deployed in Kubernetes as two components: a controller component and a per-node component."

"The controller component can be deployed as a Deployment or StatefulSet on any node in the cluster."

"The node component should be deployed on every node in the cluster through a DaemonSet."

"Deploying a CSI driver onto Kubernetes is highlighted in detail in [Recommended Mechanism for Deploying CSI Drivers on Kubernetes]"

RETRIEVAL NOTE — these four are short exact quotations. A request for the full text
of both pages was declined by the retrieval tool, so this snapshot is a
quotation-level capture rather than a full-page transcription. It is sufficient for
KCNA depth (recall: name the interface, say what it is for) and sufficient for the
outline's 🔭 Closer Look, which needs only "controller component + per-node
component + sidecars, and you install it yourself."

NOTE FOR §5 — combined with the glossary sentence "you must first deploy it to your
cluster" and the volumes-page sentence "The core of Kubernetes does not install that
software for you", these three independent statements make the absent-component
payoff airtight: nothing in Kubernetes ships the driver, so a StorageClass naming a
driver nobody installed is the ordinary, documented failure — not an exotic one.
```

---

### A12 · `k8s-api-ref-csidriver-v1-2026-08-25.md` (new)
```markdown
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
```

---

## Gaps

Objectives and concepts I could **not** source. Drafting must not invent facts to fill these.

### GAP 1 — `[BLOCKING FOR THE EXAM ALERT AS WRITTEN]` No published KCNA sub-competency detail exists for Storage

The outline's Exam Alert plan opens with: *"B1's domain analysis records that D2 expects the candidate to 'distinguish PV from PVC from StorageClass' — this three-way distinction is named in the published expectation, which makes it the highest-confidence claim in the chapter's Exam Alert."*

**No published CNCF or Linux Foundation source states this.** I re-checked all three authority captures:

- `cncf-kcna-curriculum-pdf-2026-08-23.md` — the curriculum PDF publishes four domains with weights and a flat list of competencies. Under Container Orchestration 28% it lists exactly: *"Networking; Security; Troubleshooting; Storage."* No sub-bullets, no verbs, no named objects.
- `lf-kcna-exam-page-2026-08-23.md` — identical granularity, verbatim: *"Container Orchestration 28%" — Networking; Security; Troubleshooting; Storage.*
- `lf-lfs250-course-outline-2026-08-23.md` — seven module titles, none storage-specific.

I attempted a fresh extraction of the current (2025-11-24) `KCNA_Curriculum.pdf` from `raw.githubusercontent.com/cncf/curriculum/master/` this pass. The fetch returned the PDF as binary; text extraction failed, exactly as it did on 2026-08-23. **This is the same unresolved gap, now confirmed twice.**

**Consequence for drafting:** the word *"distinguish"* and the three-way framing are almost certainly a B1 inference from the Kubernetes documentation's own structure, not a quotation from a blueprint. Per Ethical Guardrail #8 the Exam Alert may say this material is central to the Storage competency (published), and may say the three objects are routinely confused (sourced — B1 trap 64). It may **not** say the blueprint names the distinction. Recommended repair: promote the access-mode and reclaim-policy items — both backed by `[source]` traps 65/66/67 — and demote item 1 to "the three objects the documentation itself introduces in sequence," which A2 and A9 support directly.

### GAP 2 — Exam frequency for any storage topic

Unchanged and structural. Neither authority publishes question counts, per-competency question distribution, or topic frequency. `lf-kcna-exam-page` explicitly states no question count. The outline's framing constraint on the two B1-addendum traps is correct and should be extended: no storage topic in this chapter may be described as *"frequently tested"* on the strength of a published source, because none exists. B1's `[source]` tag on traps 63–69 licenses *"commonly confused"*, which is a claim about the material; frequency is a claim about the exam.

### GAP 3 — `[PARTIAL]` Per-plugin in-tree removal timeline

A4 captures the `CSIMigration` mechanism verbatim and the two facts §5 needs (operators need no config changes; the core of Kubernetes does not install the driver). What is **not** captured is any table of which in-tree plugins were removed in which Kubernetes release. Do not state a version number for the removal of any specific in-tree plugin. The outline's 🔭 Closer Look can be written entirely from A4 without one.

### GAP 4 — `[PARTIAL]` "Reserving a PersistentVolume"

Retrieved but in evidently-reworded form; deliberately excluded from A2. Only the `volumeName` field description is recorded, and only from the PVC "Volume Name" subsection. Do not draft the reserving-a-PV behaviour. Nothing in the outline requires it.

### GAP 5 — `[PARTIAL]` Full `kubectl get pv` / `kubectl get pvc` walkthrough output

The task page `/docs/tasks/configure-pod-container/configure-persistent-volume-storage/` returned HTTP 404 on two attempts, from both the rendered URL and the repository path. The `kubectl-get-pv` and `kubectl-get-pvc` entries in `kb_tags.commands` therefore have **no sourced sample output**.

What IS sourced: `kubectl describe pvc` and `kubectl describe pv` full output blocks, verbatim, in A2 (Storage Object in Use Protection) — including a `Status:` line, a `Reclaim Policy: Delete` line, an `Access Modes: RWO` line and a `Claim:` line. That covers `kubectl-describe-pvc` completely and demonstrates the fields `kubectl get` would column-ise. Draft `get` invocations without inventing their column output, or show `describe` instead.

### GAP 6 — `[PARTIAL]` CSIDriver / CSINode object depth

A11 and A12 give the deployment shape and the CSIDriver object's purpose and three fields. Full transcriptions of `kubernetes-csi.github.io/docs/deploying.html` and `csi-driver-object.html` were declined by the retrieval tool. Do not describe the sidecar container set (external-provisioner, external-attacher, node-driver-registrar, etc.) by name — those names are not in this corpus.

### GAP 7 — The "CSI volumes are a GA feature" sentence could not be re-verified

`k8s-docs-volumes-2026-08-23.md` line 23 records: *"CSI volumes are a GA feature; vendors with external CSI drivers can implement csi volumes to introduce new storage systems into Kubernetes without ever having to edit the core Kubernetes code."* My 2026-08-25 retrieval of the same page's `csi` section did not contain that sentence. It may have been removed upstream, or it may be a rendering artifact of the 08-23 capture.

This matters because that sentence is the most quotable single line for the `chapter-02:600` debt. **Two currently-verifiable replacements exist**, both in this delivery:

- A11: *"Using CSI third-party storage providers can write and deploy plugins exposing new storage systems in Kubernetes without ever having to touch the core Kubernetes code."*
- A4: *"These plugins enable storage vendors to create custom storage plugins without adding their plugin source code to the Kubernetes repository."*

Use one of those. Do not quote the 08-23 line 23 sentence.

---

## Notes for the author

### 1. G11 is closed. §5 is no longer research-blocked — and you should decide the depth question on the merits, not on scarcity.

Open question #2 offered a fallback ("§5 shrinks to the one-paragraph naming treatment") in case CSI could not be sourced. That contingency is now moot. §5 can be drafted at full planned depth: what CSI is (A4, A9, A10), what a driver is and where its two components run (A11), what installing one registers in the cluster (A12), the in-tree story and `CSIMigration` (A4). The 🔭 Closer Look is fully supported.

I'd still keep it short — the KCNA depth argument in the outline's §5 Note was always the better argument, and it stands independent of source availability. But choose it because the exam asks for recall, not because the corpus is thin.

### 2. Open question #1 (CSI's ordinal): the sources are silent, so shipped text should win uncontested.

I checked. Neither `/docs/concepts/extend-kubernetes/` (cached), the CSI glossary entry, nor the CSI spec ranks CSI against CRI, CNI or CRDs. There is no external fact that makes "third" or "last" correct. This is purely an internal-consistency question between shipped Ch 10 and an unshipped skeleton, which resolves the way you already planned it. Nothing found here complicates the recommendation.

### 3. ⚠ The StatefulSet "Stable Storage" citation needs to change, and the change strengthens §6.

This is the most consequential finding of the pass.

`k8s-docs-statefulset-2026-08-24.md` line 57 — the sentence the outline quotes as §6's Fixed-Point support — reads:

> *"the PersistentVolumeClaim(s) associated with the Pod's PersistentVolume(s) are not deleted when the Pod, or the StatefulSet is deleted."*

The 2026-08-25 retrieval of the same section reads:

> *"the PersistentVolumes associated with the Pods' PersistentVolume Claims are not deleted when the Pods, or StatefulSet are deleted."*

The nouns are swapped. The cached version says **PVCs** survive; the current version says **PVs** survive. §6's Fixed Point as written in the outline — *"A StatefulSet's PVCs outlive the StatefulSet"* — is stated by the cached snapshot and **not** stated by the current page.

**The Fixed Point is still correct**, and A8 gives you a better citation for it: the `persistentVolumeClaimRetentionPolicy` section states *"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted"* and *"The default for policies is Retain."* That is a stronger claim than the Stable Storage sentence in either wording, because it names the mechanism (a policy field with a default) rather than describing a behaviour. It also sets up a genuinely better §6 beat: the survival is not an accident of implementation, it is a default someone chose, which rhymes exactly with §4's reclaim-policy Fixed Point ("the decision was made before you existed"). Two sections, same shape, one section apart.

**Recommended:** lead §6's citation with the retention-policy text from A8; use Stable Storage only for the per-Pod-one-PVC and follows-on-reschedule claims, which both wordings agree on. Do not quote the cached line 57. It should probably also be corrected in the Ch 9 retrofit ledger, since it is the citation Ch 9 §6 leaned on.

*Caveat I could not resolve:* A8's retrieval also returned a sentence requiring the `StatefulSetAutoDeletePVC` feature gate. That reads like text adjacent to a stripped feature-state marker and I could not confirm the gate's current stage. Do not state a gate requirement or a stability level for this field. The default value is the safe, load-bearing fact.

### 4. Source disagreement on PV phases: four or five.

The concept page enumerates four (`Available`, `Bound`, `Released`, `Failed`). The API reference enumerates five, adding `Pending` — *"used for PersistentVolumes that are not available."* Both are Kubernetes-project sources; both are in this delivery (A2, A3).

**Recommendation: teach four, and do not mention the fifth.** The concept page is what a KCNA candidate reads and what a KCNA item would be written from; `Pending` is an API-level state a beginner will never observe deliberately. If §2 wants to be scrupulous, the footnote-shaped move is to say the phases are what the *concept documentation* enumerates, which is true and requires no hedging. Recorded here so a later integration or audit stage does not read the four-item list as an omission and helpfully add a fifth.

### 5. The §1 ladder is now sourceable rung by rung, in the docs' own sentences.

Ch 10 promised the reader exactly three rungs and A5 lets you deliver each with a quotation rather than a restatement:

- **Rung 1→2 boundary (container restart):** *"A container crashing does not remove a Pod from a node."* / *"The data in an `emptyDir` volume is safe across container crashes."*
- **Rung 2→3 boundary (Pod removal):** *"When a Pod is removed from a node for any reason, the data in the `emptyDir` is deleted permanently."*
- **Rung 3 (survives):** *"Unlike `emptyDir`, which is erased when a Pod is removed, the contents of an `nfs` volume are preserved, and the volume is merely unmounted."*

That last one is a small gift: the docs draw the rung-2/rung-3 contrast themselves, with `emptyDir` on one side and `nfs` on the other, which is precisely the teaser the outline wanted `nfs` and `local` to carry into §2. The figure `ch11-fig01`'s two boundary-event labels can both be lifted straight from source.

### 6. A sourced discrimination item the outline could not have planned, and it is a good one.

Generic ephemeral volumes and StatefulSet `volumeClaimTemplates` are the two mechanisms in Kubernetes that create one PVC per Pod automatically. Their deletion behaviour is **opposite**, and both halves are now sourced:

- Generic ephemeral (A6): *"When the Pod is deleted, the Kubernetes garbage collector deletes the PVC."*
- StatefulSet (A8): *"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted."*

Both even use the word *template*. This is a genuine near-miss of exactly the kind B7's Canonical forms table exists to police, it lives in §1 and §6 respectively — the chapter's two ends — and it makes an excellent Bearings #3 item or Practice-Question pairing. It is also the strongest argument for teaching generic ephemeral volumes in §1 rather than mentioning them: without it, §6's survival rule reads like a fact; with it, §6's survival rule reads like a *choice someone made differently elsewhere*.

Worth flagging as a second B1 addendum alongside the two you already identified.

### 7. §3's `WaitForFirstConsumer` argument is sourced twice, and the second one is better than the first.

The StorageClass page (A1) explains `WaitForFirstConsumer` in terms of topology-constrained backends and unschedulable Pods. The `local` volume section (A5) explains it in terms the reader already holds from Ch 7: *"Delaying volume binding ensures that the PersistentVolumeClaim binding decision will also be evaluated with any other node constraints the Pod may have, such as node resource requirements, node selectors, Pod affinity, and Pod anti-affinity."*

That second sentence names four scheduling inputs the reader met in Chapter 7 by name. It is the four-back retrieval the outline wanted, handed over pre-assembled. Prefer it for body prose; keep A1's version for the 🔭 Closer Look, where the topology framing belongs.

### 8. Two small corrections to inherited material, neither load-bearing.

- **Projected volume sources are now six, not four.** `k8s-docs-volumes-2026-08-23.md` line 19 lists four (`secret`, `downwardAPI`, `configMap`, `serviceAccountToken`); the current projected-volumes page adds `clusterTrustBundle` and `podCertificate` (A7). §1 should either use the six or say "several" and enumerate only the four the reader has met — the latter is better pedagogy and stays true.
- **`subPath` is now fully sourced as a mechanism**, not only as an exception (A4). The outline called this a "partial fifth" gap; it is closed. And the no-updates rule turns out to hold for *three* volume types, not one — ConfigMap, Secret and downwardAPI each carry their own version of the sentence (A5). Stating it once as a property of `subPath` rather than three times as a property of each source is both shorter and more true, and it is what makes the `chapter-04:762` promise land as a rule rather than a trivium.