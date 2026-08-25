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
