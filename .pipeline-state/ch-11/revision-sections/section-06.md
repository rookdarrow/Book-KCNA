## ⚪ §1 — Three Lifetimes, and the Volumes That Have Them

Chapter 10 told you, in its closing pages, that this chapter opens with a ladder of three different lifetimes, only one of which survives the thing that created it. Here is that ladder, and the count is exactly three.

Start at the bottom, where you already are.

A container's filesystem is assembled from the image's read-only layers with a single writable layer on top *[cross-bearing: see Ch 2 §2 — the writable container layer]*. Everything the process writes goes into that writable layer. When the container stops — crash, OOM kill, a `SIGTERM` it handled badly — the kubelet restarts it, and the restarted container gets a clean state assembled fresh from the image [source: k8s-docs-volumes-2026-08-23]. The writable layer is discarded. That is rung one, and the boundary that crosses it is **a container restart**.

Now attach a volume. A volume declared in the PodSpec and mounted into a container is not part of the container's filesystem stack; it is mounted into it. When the container restarts, the volume is still there, because the volume belongs to the Pod, not to the container. The documentation states this as a flat rule: *for any kind of volume in a given Pod, data is preserved across container restarts* [source: k8s-docs-volumes-2026-08-23]. That is rung two. It survives the boundary that killed rung one.

But rung two has a boundary of its own. **When a Pod ceases to exist, Kubernetes destroys ephemeral volumes** [source: k8s-docs-volumes-2026-08-23]. Not when the Pod is unhealthy, not when a container inside it dies: when the Pod object itself is gone. Delete the Pod, and its `emptyDir` goes with it.

Rung three is what is left when you ask for storage whose lifetime is not tied to any Pod at all. **Kubernetes does not destroy persistent volumes** [source: k8s-docs-volumes-2026-08-23]. That is the entire distinction — and it is the hold the epigraph was describing: aboard before this watch, aboard after. §2 onward is about how you get one.

<!-- FIGURE: ch11-fig01-volume-lifetime-ladder -->
```
   ┌──────────────────────────────────────────────────────────────┐
   │  CLUSTER-SCOPED STORAGE                          (rung 3)    │
   │  survives the Pod's deletion                                 │
   │                                                              │
   │   ┌────────────────────────────────────────────────────┐     │
   │   │  POD-SCOPED VOLUME                     (rung 2)    │     │
   │   │  survives a container restart                      │     │
   │   │                                                    │     │
   │   │   ┌──────────────────────────────────────────┐     │     │
   │   │   │  CONTAINER WRITABLE LAYER    (rung 1)    │     │     │
   │   │   │  survives nothing                        │     │     │
   │   │   └──────────────────────────────────────────┘     │     │
   │   │        ▲                                           │     │
   │   │        └── boundary: CONTAINER RESTART             │     │
   │   │            (data below this line is discarded)     │     │
   │   └────────────────────────────────────────────────────┘     │
   │            ▲                                                 │
   │            └── boundary: POD CEASES TO EXIST                 │
   │                (data below this line is discarded)           │
   │                                                              │
   │   nothing in a Pod's lifecycle crosses this outer boundary   │
   └──────────────────────────────────────────────────────────────┘
```

> ★ **Fixed Point**
>
> **Three lifetimes, two boundaries.** The container's writable layer is destroyed by a **container restart**. A Pod-scoped (ephemeral) volume survives that, and is destroyed when **the Pod ceases to exist**. Cluster-scoped persistent storage survives both, because nothing in a Pod's lifecycle reaches it. Every storage question in Kubernetes is a question about which rung you are standing on.

### The volumes that live on rung two

With the ladder in place, the volume types hang off it cleanly. Nearly all of the ones you will meet on the exam are rung-two types: their lifetime is the Pod's.

**`emptyDir`** is the plain one. The volume is created when the Pod is assigned to a node, and as the name says, it is initially empty [source: k8s-docs-volume-types-depth-2026-08-25]. Every container in the Pod can read and write the same files in it, which is the shared-filesystem half of what Chapter 5 told you a Pod's containers have in common *[cross-bearing: see Ch 5 §1 — the Pod's shared context]*. Chapter 5 named it and left it; here it is.

The lifetime rules for `emptyDir` are the ladder restated in one type. *When a Pod is removed from a node for any reason, the data in the `emptyDir` is deleted permanently.* And immediately after: *A container crashing does not remove a Pod from a node*, therefore *the data in an `emptyDir` volume is safe across container crashes* [source: k8s-docs-volume-types-depth-2026-08-25].

Two knobs matter. Setting `emptyDir.medium` to `"Memory"` makes Kubernetes mount a tmpfs — a RAM-backed filesystem — instead of using disk [source: k8s-docs-volume-types-depth-2026-08-25]. Fast, and with a catch the documentation states directly: *while tmpfs is very fast, be aware that, unlike disks, files you write count against the memory limit of the container that wrote them* [source: k8s-docs-volume-types-depth-2026-08-25]. A process that fills a memory-backed `emptyDir` gets OOM-killed for it *[cross-bearing: see Ch 5 §8 — requests, limits, and what a Pod is owed]*. The second knob is `sizeLimit`, which caps the volume's capacity on the default medium [source: k8s-docs-volume-types-depth-2026-08-25].

> 🪝 **Snag:** By default there is *no* cap. The documentation is blunt: *there is no limit on how much space an `emptyDir` or `hostPath` volume can consume, and no isolation between containers or Pods* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. A runaway log writer in one Pod can fill the node's disk and put every other Pod on that node into disk pressure. `sizeLimit` exists because the default is unbounded.

**`hostPath`** mounts a file or directory from the host node's filesystem into your Pod [source: k8s-docs-volume-types-depth-2026-08-25]. It has an optional `type` field alongside the required `path` [source: k8s-docs-volume-types-depth-2026-08-25]. That field controls what Kubernetes checks before mounting: whether the path must already exist, must be a directory, may be created, must be a socket, and so on [source: k8s-docs-volumes-2026-08-23]. The documentation's own framing of `hostPath` is exactly right: *this is not something that most Pods will need, but it offers a powerful escape hatch for some applications* [source: k8s-docs-volume-types-depth-2026-08-25].

An escape hatch is precisely what it is, and escape hatches open both ways.

> ⚠ **Navigational Hazards: `hostPath` is a hole in the wall**
>
> The documentation opens its warning with a sentence that does not hedge: *using the `hostPath` volume type presents many security risks.* *If you can avoid using a `hostPath` volume, you should.* [source: k8s-docs-volume-types-depth-2026-08-25]
>
> Why it is dangerous is more instructive than that it is. *Access to the host filesystem can expose privileged system credentials (such as for the kubelet) or privileged APIs (such as the container runtime socket) that can be used for container escape or to attack other parts of the cluster* [source: k8s-docs-volume-types-depth-2026-08-25]. A Pod that can read `/var/lib/kubelet` can read the node's credentials. A Pod that can write to the container runtime socket can start a privileged container of its own choosing. The Pod boundary you have spent ten chapters trusting is only as strong as the mounts you allow through it.
>
> Restricting access to specific host directories through admission-time validation only holds if those mounts are additionally required to be read-only; give an untrusted Pod a read-write mount and its containers may be able to subvert the restriction [source: k8s-docs-volume-types-depth-2026-08-25].
>
> There is a second-order problem too, and it is the kind that bites in production rather than on an exam: *Pods with identical configuration (such as created from a PodTemplate) may behave differently on different nodes due to different files on the nodes* [source: k8s-docs-volume-types-depth-2026-08-25]. A `hostPath` mount silently makes your Pods node-dependent. The replica that works and the replica that doesn't are running the same image.
>
> This is the workload-to-host boundary problem, and it is why an entire security apparatus exists to police it. Named here, and left here: *[cross-bearing: see Ch 12 §5 — what a Pod may do to its node]*.

**`configMap` and `secret` as volume sources.** Chapter 4 taught you both objects and then told you they would reappear here as volume types mounted into a filesystem *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. This is that reappearance. A ConfigMap's data can be referenced in a volume of type `configMap` and consumed as files by the containerized application [source: k8s-docs-volumes-2026-08-23]. A `secret` volume does the same for a Secret: *you can store secrets in the Kubernetes API and mount them as files for use by Pods without coupling to Kubernetes directly* [source: k8s-docs-volume-types-depth-2026-08-25].

Both are always mounted read-only [source: k8s-docs-volume-types-depth-2026-08-25]. And one detail about `secret` volumes matters more than it looks: *`secret` volumes are backed by tmpfs (a RAM-backed filesystem), so they are never written to non-volatile storage* [source: k8s-docs-volume-types-depth-2026-08-25]. A Secret mounted as a volume does not land on the node's disk. A Secret injected as an environment variable is a different proposition entirely, for reasons Chapter 12 will develop *[cross-bearing: see Ch 12 §4 — Secrets are not encrypted]*. File over environment variable is half an argument already, and you now hold that half.

**`projected`** is the multiplexer. *A `projected` volume maps several existing volume sources into the same directory* [source: k8s-docs-projected-volumes-2026-08-25]. The list of projectable sources runs longer than this chapter needs; the four that matter to you are `secret`, `configMap`, `serviceAccountToken`, and `downwardAPI` [source: k8s-docs-projected-volumes-2026-08-25].

<!-- AUTHOR-REVIEW: the snapshot enumerates six projectable sources (adding `clusterTrustBundle` and `podCertificate`). Trimmed to four on the curriculum-alignment stage's recommendation — the two dropped entries appear nowhere else in the book and are not KCNA material. Full list is in k8s-docs-projected-volumes-2026-08-25 if a later stage wants it restored. -->

You have already used one of these without being told what it was. In Chapter 5, a Pod's ServiceAccount token arrived in the container's filesystem via a projected token volume *[cross-bearing: see Ch 5 §6 — a Pod's identity]*. That was `serviceAccountToken`, one entry in the list above. The mechanism you met carrying an identity token is the same mechanism, generalized: assemble several distinct sources into one directory so the application sees a single coherent config tree instead of four mount points.

**`downwardAPI`** makes a Pod's own metadata available to the application running inside it. *Within the volume, you can find the exposed data as read-only files in plain text format* [source: k8s-docs-volume-types-depth-2026-08-25]. A container that needs to know its own Pod name, namespace, or labels reads them from a file rather than being told at build time.

**Generic ephemeral volumes** are the interesting hybrid, and they are the type most likely to make you re-read the ladder. They are *similar to `emptyDir` volumes in the sense that they provide a per-pod directory for scratch data that is usually empty after provisioning*, but with capabilities `emptyDir` does not have: *storage can be local or network-attached*, *volumes can have a fixed size that Pods are not able to exceed*, and typical volume operations like snapshotting, cloning, and resizing are supported if the driver supports them [source: k8s-docs-ephemeral-volumes-2026-08-25].

Here is the mechanism. Read it twice; it prefigures §6. The Pod spec carries a full PersistentVolumeClaim template inline. When such a Pod is created, *the ephemeral volume controller then creates an actual PersistentVolumeClaim object in the same namespace as the Pod and ensures that the PersistentVolumeClaim gets deleted when the Pod gets deleted* [source: k8s-docs-ephemeral-volumes-2026-08-25]. A real claim, created for you, garbage-collected with the Pod. Rung two behavior, built out of rung three machinery.

Naming is deterministic: *the name is a combination of the Pod name and volume name, with a hyphen (-) in the middle* [source: k8s-docs-ephemeral-volumes-2026-08-25]. A Pod named `my-app` with a volume named `scratch-volume` produces a PVC named `my-app-scratch-volume`.

> 🔭 **Closer Look:** That deterministic naming has a sharp edge the documentation calls out explicitly. A Pod named `pod-a` with volume `scratch` and a Pod named `pod` with volume `a-scratch` both compute to the PVC name `pod-a-scratch` [source: k8s-docs-ephemeral-volumes-2026-08-25]. Kubernetes detects the conflict: a PVC is only used for an ephemeral volume if it was created for that Pod, checked via the ownership relationship, and *an existing PVC is not overwritten or modified* [source: k8s-docs-ephemeral-volumes-2026-08-25]. But detection is not resolution: *without the right PVC, the Pod cannot start* [source: k8s-docs-ephemeral-volumes-2026-08-25]. Below KCNA depth; recorded because it is the kind of thing that costs someone an afternoon.

**`subPath`** is not a volume type at all. It is a mount modifier, and it earns its place here because of one exception you were promised by name in Chapter 4.

The general mechanism first: *sometimes, it is useful to share one volume for multiple uses in a single Pod. The `volumeMounts[*].subPath` property specifies a sub-path inside the referenced volume instead of its root* [source: k8s-docs-volumes-csi-and-subpath-2026-08-25]. One PVC, mounted into a MySQL container at its `mysql` subdirectory and into a PHP container at its `html` subdirectory: two containers, two mount points, one underlying volume.

Now the exception. Chapter 4 hedged that a mounted ConfigMap picks up changes when the ConfigMap is updated, and told you the exception had a name and would arrive here *[cross-bearing: see Ch 4 §4 — configuration kept outside the image]*. Here it is, a flat rule with no conditions attached: *a container using a ConfigMap as a `subPath` volume mount will not receive updates when the ConfigMap changes* [source: k8s-docs-volume-types-depth-2026-08-25].

The same applies to the two neighbors: *a container using a Secret as a `subPath` volume mount will not receive Secret updates* [source: k8s-docs-volume-types-depth-2026-08-25], and *a container using the downward API as a `subPath` volume mount does not receive updates when field values change* [source: k8s-docs-volume-types-depth-2026-08-25].

> 🪢 **Mnemonic:** **`subPath` cuts the wire.** A whole-volume mount stays connected to the object that feeds it. A `subPath` mount takes a snapshot of one path and stops listening. If you mount config with `subPath` and then wonder why your rolling ConfigMap update did nothing, this is why.

<!-- AUTHOR-REVIEW: `chapter-04` line 761 carries a RESEARCH GAP comment noting that the ConfigMap auto-update hedge was uncited at the time Ch 4 shipped. The `subPath` half of that claim is now sourced here to k8s-docs-volume-types-depth-2026-08-25. Worth feeding to any Ch 4 retrofit. -->

### The rung-three teasers

Two volume types on the list belong to rung three and are named here only so you recognize the shape when §2 formalizes it.

**`nfs`** allows an existing NFS share to be mounted into a Pod, and the contrast with `emptyDir` is exactly the ladder: *unlike `emptyDir`, which is erased when a Pod is removed, the contents of an `nfs` volume are preserved, and the volume is merely unmounted* [source: k8s-docs-volume-types-depth-2026-08-25]. Preserved, not deleted. Merely unmounted. That sentence is rung three in miniature. It also means the data can be pre-populated before any Pod exists, and shared between Pods. NFS in particular *can be mounted by multiple writers simultaneously* [source: k8s-docs-volume-types-depth-2026-08-25], which will matter a great deal in §4.

**`local`** represents a mounted local storage device: a disk, a partition, a directory [source: k8s-docs-volume-types-depth-2026-08-25]. Unlike `hostPath`, `local` volumes are used *in a durable and portable manner without manually scheduling Pods to nodes*, because *the system is aware of the volume's node constraints by looking at the node affinity on the PersistentVolume* [source: k8s-docs-volume-types-depth-2026-08-25]. It has a hard restriction: *local volumes can only be used as a statically created PersistentVolume. Dynamic provisioning is not supported* [source: k8s-docs-volume-types-depth-2026-08-25]. And an honest limitation: *if a node becomes unhealthy, then the `local` volume becomes inaccessible to the Pod. The Pod using this volume is unable to run* [source: k8s-docs-volume-types-depth-2026-08-25].

Both of those types name a `PersistentVolume`. You have not been told what one is. That is next.

---