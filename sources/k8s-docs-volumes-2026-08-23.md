---
source_url: "https://kubernetes.io/docs/concepts/storage/volumes/"
fetched_at: "2026-08-23T23:40:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2 Storage"]
concepts_covered: ["volume", "ephemeral-volume", "emptydir", "hostpath", "configmap-volume", "secret-volume", "projected", "downwardapi", "nfs", "local", "csi-volume"]
---
# Volumes (kubernetes.io/docs/concepts/storage/volumes/)

## Background
On-disk files in a container are ephemeral, which presents some problems for non-trivial applications when running in containers. One problem occurs when a container crashes or is stopped; the container state is not saved, so all of the files that were created or modified during the lifetime of the container are lost. After a crash, kubelet restarts the container with a clean state. Another problem occurs when multiple containers are running in a Pod and need to share files. Kubernetes supports many types of volumes. A Pod can use any number of volume types simultaneously. Ephemeral volume types have a lifetime linked to a specific Pod, but persistent volumes exist beyond the lifetime of any individual Pod. When a Pod ceases to exist, Kubernetes destroys ephemeral volumes; however, Kubernetes does not destroy persistent volumes. For any kind of volume in a given Pod, data is preserved across container restarts.

## Volume types
- configMap — provides a way to inject configuration data into Pods; the data stored in a ConfigMap can be referenced in a volume of type configMap and consumed by containerized applications. A ConfigMap is always mounted as readOnly. A container using a ConfigMap as a subPath volume mount will not receive updates when the ConfigMap changes.
- downwardAPI — makes downward API data (Pod and container fields) available to applications as read-only files.
- emptyDir — created when the Pod is assigned to a node; initially empty; all containers in the Pod can read and write the same files in the emptyDir volume. When a Pod is removed from a node for any reason, the data in the emptyDir is deleted permanently. A container crashing does not remove a Pod from a node, so data in an emptyDir volume is safe across container crashes. Uses: scratch space, checkpointing a long computation, holding files that a content-manager container fetches while a webserver container serves them. Setting emptyDir.medium to "Memory" mounts a tmpfs (RAM-backed filesystem); files written count against the memory limit of the container that wrote them. sizeLimit caps the capacity.
- hostPath — mounts a file or directory from the host node's filesystem into your Pod. This is not something that most Pods will need, but it offers a powerful escape hatch for some applications. The optional type field (DirectoryOrCreate, Directory, FileOrCreate, File, Socket, CharDevice, BlockDevice) controls checks before mounting. Warning: HostPath volumes present many security risks, and it is a best practice to avoid the use of HostPaths when possible; when one must be used, scope it to only the required file or directory and mount it read-only.
- persistentVolumeClaim — used to mount a PersistentVolume into a Pod; a way for users to "claim" durable storage without knowing the details of the particular cloud environment.
- projected — maps several existing volume sources (secret, downwardAPI, configMap, serviceAccountToken) into the same directory.
- secret — used to pass sensitive information, such as passwords, to Pods; backed by tmpfs so never written to non-volatile storage. You must create a Secret before you can use it.
- nfs — allows an existing NFS share to be mounted into a Pod; contents are preserved when the Pod is removed; data can be pre-populated and handed off between Pods.
- local — represents a mounted local storage device such as a disk, partition or directory; can only be used as a statically created PersistentVolume; the system is aware of the volume's node constraints by looking at the node affinity on the PersistentVolume; subject to the availability of the underlying node.
- csi — CSI volumes are a GA feature; vendors with external CSI drivers can implement csi volumes to introduce new storage systems into Kubernetes without ever having to edit the core Kubernetes code.
