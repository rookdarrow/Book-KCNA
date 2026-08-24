---
source_url: "https://kubernetes.io/docs/concepts/storage/persistent-volumes/"
fetched_at: "2026-08-23T22:30:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Storage"]
concepts_covered: ["persistentvolume", "persistentvolumeclaim", "storageclass", "static-provisioning", "dynamic-provisioning", "binding", "reclaim-policy", "access-modes"]
---
# Persistent Volumes (kubernetes.io/docs/concepts/storage/persistent-volumes/)

## Introduction
A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. It is a resource in the cluster just like a node is a cluster resource. PVs are volume plugins like Volumes, but have a lifecycle independent of any individual Pod that uses the PV. This API object captures the details of the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage system.

A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a Pod. Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., they can be mounted ReadWriteOnce, ReadOnlyMany, ReadWriteMany, or ReadWriteOncePod).

While PersistentVolumeClaims allow a user to consume abstract storage resources, it is common that users need PersistentVolumes with varying properties, such as performance, for different problems. Cluster administrators need to be able to offer a variety of PersistentVolumes that differ in more ways than size and access modes, without exposing users to the details of how those volumes are implemented. For these needs, there is the StorageClass resource.

## Lifecycle of a volume and claim
**Provisioning.** Static: a cluster administrator creates a number of PVs. They carry the details of the real storage, which is available for use by cluster users. Dynamic: when none of the static PVs the administrator created match a user's PersistentVolumeClaim, the cluster may try to dynamically provision a volume specially for the PVC. This provisioning is based on StorageClasses: the PVC must request a storage class and the administrator must have created and configured that class for dynamic provisioning to occur. Claims that request the class "" effectively disable dynamic provisioning for themselves.

**Binding.** A control loop in the control plane watches for new PVCs, finds a matching PV (if possible), and binds them together. Once bound, PersistentVolumeClaim binds are exclusive, regardless of how they were bound. A PVC to PV binding is a one-to-one mapping. Claims will remain unbound indefinitely if a matching volume does not exist. Claims will be bound as matching volumes become available.

**Using.** Pods use claims as volumes. The cluster inspects the claim to find the bound volume and mounts that volume for a Pod. Users schedule Pods and access their claimed PVs by including a persistentVolumeClaim section in a Pod's volumes block.

**Reclaiming.** When a user is done with their volume, they can delete the PVC objects from the API that allows reclamation of the resource. The reclaim policy for a PersistentVolume tells the cluster what to do with the volume after it has been released of its claim. Retain — allows for manual reclamation of the resource; when the PVC is deleted, the PV still exists and the volume is considered "released", but it is not yet available for another claim because the previous claimant's data remains on the volume; an administrator can manually reclaim it. Delete — removes both the PersistentVolume object from Kubernetes, as well as the associated storage asset in the external infrastructure; volumes that were dynamically provisioned inherit the reclaim policy of their StorageClass, which defaults to Delete. Recycle — deprecated.

## Access modes
- ReadWriteOnce (RWO) — the volume can be mounted as read-write by a single node. ReadWriteOnce access mode still can allow multiple pods to access the volume when the pods are running on the same node.
- ReadOnlyMany (ROX) — the volume can be mounted as read-only by many nodes.
- ReadWriteMany (RWX) — the volume can be mounted as read-write by many nodes.
- ReadWriteOncePod (RWOP) — the volume can be mounted as read-write by a single Pod. Use ReadWriteOncePod access mode if you want to ensure that only one pod across the whole cluster can read that PVC or write to it.
