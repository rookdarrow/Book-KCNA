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
