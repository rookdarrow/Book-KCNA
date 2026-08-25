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
