## 🔵 §5 — Who Actually Provides the Storage

Chapter 10 closed by telling you that this chapter brings the last of the four pluggable interfaces, and that with it the set closes. Here it is.

You have three already, collected one chapter at a time. CRI at the container runtime *[cross-bearing: see Ch 2 §4 — the Container Runtime Interface]*. CRDs at the API itself *[cross-bearing: see Ch 6 §8 — the control loop, extended]*. CNI at the network *[cross-bearing: see Ch 9 §1 — four rules and a plugin]*. The fourth is CSI, at storage.

**The Container Storage Interface (CSI) defines a standard interface for container orchestration systems (like Kubernetes) to expose arbitrary storage systems to their container workloads** [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].

The glossary states the consequence: *CSI allows vendors to create custom storage plugins for Kubernetes without adding them to the Kubernetes repository (out-of-tree plugins)* [source: k8s-glossary-storage-terms-2026-08-25]. And from the volumes page, the same claim in the sharpest available form: vendors *can implement `csi` volumes to introduce new storage systems into Kubernetes without ever having to edit the core Kubernetes code* [source: k8s-docs-volumes-2026-08-23].

*Without ever having to edit the core Kubernetes code.* If that phrasing feels familiar, it should. It is structurally identical to what CRI bought at the runtime boundary and what CNI bought at the network boundary. Same move, fourth socket.

### Why it exists: the world before

The reason CSI was necessary takes one paragraph, and it makes the argument concrete rather than architectural.

*Previously, all volume plugins were "in-tree". The "in-tree" plugins were built, linked, compiled, and shipped with the core Kubernetes binaries. This meant that adding a new storage system to Kubernetes (a volume plugin) required checking code into the core Kubernetes code repository* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].

Sit with the consequences of that. The documentation records the arrangement, not what it cost the people living inside it, so what follows is this book's reading rather than a sourced claim. A storage vendor wanting Kubernetes support had to submit code to the Kubernetes project, have it reviewed by Kubernetes maintainers, and wait for a Kubernetes release. Their bug fixes shipped on Kubernetes' schedule, not their own. Meanwhile, Kubernetes maintainers were reviewing and carrying storage code for hardware they did not own and could not test.

*Both CSI and FlexVolume allow volume plugins to be developed independently of the Kubernetes code base, and deployed (installed) on Kubernetes clusters as extensions* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. FlexVolume was the earlier attempt and is now deprecated: *using an out-of-tree CSI driver is the recommended way to integrate external storage with Kubernetes* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].

> ★ **Fixed Point**
>
> **CSI is a published contract between two parties, and one of them is not Kubernetes.**
>
> The specification states its own purpose in a sentence that says more than any Kubernetes documentation can: CSI exists to *"define an industry standard 'Container Storage Interface' (CSI) that will enable storage vendors (SP) to develop a plugin once and have it work across a number of container orchestration (CO) systems"* [source: csi-spec-objective-2026-08-25].
>
> Read *"across a number of container orchestration systems."* CSI is not a Kubernetes feature that vendors happen to use. It is a cross-orchestrator standard that Kubernetes happens to implement, the same shape as OCI at the image and runtime boundary *[cross-bearing: see Ch 2 §5 — the Open Container Initiative]*. Storage stops being Kubernetes' problem and becomes a vendor's, on terms both parties agreed to in public.
>
> With this you hold all four: **CRI, CNI, CSI, CRDs.** Chapter 17 will ask you to state the shape they have in common without help *[cross-bearing: see Ch 17 §4 — every place Kubernetes lets you in]*.

### What a driver is, and what installing one puts in the cluster

Chapter 2 promised you "CSI and storage drivers," with *drivers* in the promise. So: what is a driver, concretely?

A CSI driver is software you deploy into the cluster, and it deploys as ordinary Kubernetes workloads. *A CSI driver is typically deployed in Kubernetes as two components: a controller component and a per-node component* [source: kubernetes-csi-docs-deployment-2026-08-25]. The controller component *can be deployed as a Deployment or StatefulSet on any node in the cluster*, and the node component *should be deployed on every node in the cluster through a DaemonSet* [source: kubernetes-csi-docs-deployment-2026-08-25].

That shape should be recognizable without further explanation. One controller, running somewhere, handling the cluster-wide operations: create this volume, delete that one *[cross-bearing: see Ch 6 §1 — the resource that holds the intent]*. One agent per node, running everywhere, handling the node-local operations: mount this volume into this path on this machine. DaemonSet is exactly the workload type for "one per node" *[cross-bearing: see Ch 6 §7 — one per node, and work that ends]*. A CSI driver is not exotic infrastructure. It is a Deployment and a DaemonSet, running software somebody else wrote.

Installing one also puts an object in the cluster: *CSIDriver captures information about a Container Storage Interface (CSI) volume driver deployed on the cluster* [source: k8s-api-ref-csidriver-v1-2026-08-25]. Which makes it the fourth object in this chapter that describes storage without providing any — PV, PVC, StorageClass, CSIDriver — and the one where the gap is most literal, since its whole documented job is to *capture information about* a driver that exists elsewhere.

Once installed, the driver's volumes are usable in three ways: *through a reference to a PersistentVolumeClaim*, *with a generic ephemeral volume*, or *with a CSI ephemeral volume if the driver supports that* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. The PersistentVolumeClaim path is the one §2 through §4 described.

### The fourth sighting

You have now seen the pattern three times in three sections: an Ingress without a controller, a StorageClass without a provisioner, and now this. Here is the fourth, and the sources state it not as a warning but as a plain ordering requirement:

*To use a CSI driver from a storage provider, you must first deploy it to your cluster. You will then be able to create a Storage Class that uses that CSI driver* [source: k8s-glossary-storage-terms-2026-08-25].

*First.* Then. And from the migration documentation, in case the point needed to be blunter: *as part of that migration, you — or another cluster administrator — must have installed and configured the appropriate CSI driver for that storage. **The core of Kubernetes does not install that software for you**.* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]

**An object without its component does nothing** *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*. A StorageClass naming a CSI driver nobody deployed is not an exotic failure you have to imagine. It is the documented prerequisite, unmet. The claim sits unbound. The Pod sits `Pending`. `kubectl get storageclass` shows the class, healthy and correct, describing a capability that does not exist.

That is the same light, the fourth time. And once you have seen it four times, you stop asking "is the object there?" and start asking "is the *component* there?", which is the question Chapter 10 said you would know to ask.

> 🔭 **Closer Look: CSI migration**
>
> CNCF publishes the Storage competency as a single word. This book's reading of it puts CSI at recall depth — name the storage interface, say what it is for, and stop there. What follows goes deeper than that reading requires, and is here for the day you meet it in a cluster rather than on a test.
>
> The in-tree plugins did not vanish when CSI arrived; they were migrated behind it. *The `CSIMigration` feature directs operations against existing in-tree plugins to corresponding CSI plugins (which are expected to be installed and configured). As a result, operators do not have to make any configuration changes to existing Storage Classes, PersistentVolumes, or PersistentVolumeClaims (referring to in-tree plugins) when transitioning to a CSI driver that supersedes an in-tree plugin* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].
>
> The compatibility promise is unusually strong: *existing PVs created by an in-tree volume plugin can still be used in the future without any configuration changes, even after the migration to CSI is completed for that volume type, and even after you upgrade to a version of Kubernetes that doesn't have compiled-in support for that kind of storage* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. Your manifests keep working; the machinery underneath them was replaced. *The actual storage management now happens through the CSI driver* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25].
>
> The operations CSI covers: *provisioning/delete, attach/detach, mount/unmount, and resizing of volumes* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. That list is the storage lifecycle, and it maps cleanly onto everything §2 through §4 described.

> 🪝 **Snag:** CSI is an interface, not a product. There is no "CSI storage" you can buy or deploy, any more than there is "CNI networking." What you deploy is a *driver*, written by whoever owns the storage it speaks to — one for a cloud provider's block store, one for a software-defined storage project, one for an on-premises array — each implementing the same contract against different hardware. A question that treats CSI as a storage system rather than as the interface storage systems implement is testing exactly this confusion.

<!-- AUTHOR-REVIEW: The three named CSI drivers previously listed here (AWS EBS, Ceph, vSphere) were genericized — no cached snapshot enumerates driver implementations. Research gap to open: the kubernetes-csi drivers list, which would also support the `ebs.csi.aws.com` provisioner string used in this chapter's Taking Your Bearings #3. If that source lands, restore the named examples with a tag. -->

---