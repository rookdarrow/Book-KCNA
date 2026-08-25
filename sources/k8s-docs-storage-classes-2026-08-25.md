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
