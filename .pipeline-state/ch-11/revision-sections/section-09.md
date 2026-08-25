## 🔵 §3 — Provisioning on Demand

Everything in §2 assumed a PersistentVolume already existed. Somebody made one, it sat there `Available`, and a claim found it.

That model works, and it has a name, but it does not scale past a certain point, for a reason that becomes obvious the moment you try it. An administrator pre-creating PVs has to guess: how many, what sizes, what performance tiers, for which teams. Guess low and claims sit unbound. Guess high and you have provisioned storage nobody asked for. Guess wrong about the size distribution and you have forty 10Gi volumes and a team that needs one 400Gi volume. It is stocking the hold for a manifest nobody has written yet.

The object that fixes this is the StorageClass, and it is the third element that has been sitting off to the side of the figure since §2.

### What a StorageClass is

*A StorageClass provides a way for administrators to describe the classes of storage they offer. Different classes might map to quality-of-service levels, or to backup policies, or to arbitrary policies determined by the cluster administrators. Kubernetes itself is unopinionated about what classes represent* [source: k8s-docs-storage-classes-2026-08-25].

That last sentence is doing real work. Kubernetes does not know what `fast` means, or `bulk`, or `archive`. It knows those are names an administrator chose and attached to a provisioning configuration. The documentation offers a comparison that lands well for anyone with a storage background: *the Kubernetes concept of a storage class is similar to "profiles" in some other storage system designs* [source: k8s-docs-storage-classes-2026-08-25].

The problem it solves is stated back in the PersistentVolumes documentation, and it reads as a problem statement rather than a feature description: *cluster administrators need to be able to offer a variety of PersistentVolumes that differ in more ways than size and access modes, without exposing users to the details of how those volumes are implemented. For these needs, there is the StorageClass resource* [source: k8s-docs-persistent-volumes-2026-08-23].

*Without exposing users to the details.* That is the supply/demand split from §2, extended one level: the user asks for `fast`, and never learns what `fast` is made of.

*Each StorageClass contains the fields `provisioner`, `parameters`, and `reclaimPolicy`, which are used when a PersistentVolume belonging to the class needs to be dynamically provisioned to satisfy a PersistentVolumeClaim* [source: k8s-docs-storage-classes-2026-08-25]. And *the name of a StorageClass object is significant, and is how users can request a particular class* [source: k8s-docs-storage-classes-2026-08-25]. The name is the API. When a developer writes `storageClassName: low-latency`, they are using that name as the entire interface to a provisioning system they know nothing else about.

Here is what one actually looks like:

```yaml
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
```
[source: k8s-docs-storage-classes-2026-08-25]

Note `parameters`. That field is a passthrough: its contents are meaningful to the provisioner and opaque to Kubernetes. `guaranteedReadWriteLatency: "true"` means something to that vendor's driver and nothing at all to the API server.

Two fields in that example — `allowVolumeExpansion` and `mountOptions` — get no treatment in this chapter, and that is deliberate rather than an oversight. They are real provisioning-behavior knobs, and they are reproduced here so you are looking at an actual StorageClass rather than a trimmed one. They sit outside this chapter's scope; nothing later depends on them.

<!-- AUTHOR-REVIEW: the curriculum-alignment audit suggested optionally glossing allowVolumeExpansion with the storage-classes page's "you can only use the volume expansion feature to grow a Volume, not to shrink it." That sentence is not attested in any snapshot this chapter has cited, so it is not quoted here. If a verification pass confirms it in k8s-docs-storage-classes-2026-08-25, swap the paragraph above for a one-sentence sourced gloss. -->

The `provisioner` field is the one that makes the class do anything: *each StorageClass has a provisioner that determines what volume plugin is used for provisioning PVs. This field must be specified* [source: k8s-docs-storage-classes-2026-08-25]. Provisioners come in two flavors: internal ones shipped alongside Kubernetes with `kubernetes.io`-prefixed names, and *external provisioners, which are independent programs that follow a specification defined by Kubernetes*, whose authors *have full discretion over where their code lives, how the provisioner is shipped, how it needs to be run* [source: k8s-docs-storage-classes-2026-08-25]. Hold that phrase — *independent programs* — because §5 is about what happens when nobody runs one.

### Two ways a volume comes to exist

<!-- FIGURE: ch11-fig03-static-vs-dynamic-provisioning -->
```
                        A PVC IS CREATED
                               │
                               ▼
              ┌────────────────────────────────┐
              │ Does a matching PV already     │
              │ exist and is it Available?     │
              └───────┬────────────────┬───────┘
                      │ YES            │ NO
                      ▼                ▼
        ═════ STATIC ═════      ┌─────────────────────────┐
                                │ Does the claim name a   │
   admin pre-created a PV       │ StorageClass, AND is a  │
   carrying the real storage    │ provisioner configured  │
   details                      │ for that class?         │
              │                 └───┬─────────────────┬───┘
              │                     │ BOTH            │ EITHER
              │                     │ TRUE            │ MISSING
              ▼                     ▼                 ▼
     ┌─────────────────┐  ═══ DYNAMIC ═══     ┌──────────────────┐
     │  binder matches │                      │  CLAIM WAITS,    │
     │  claim ↔ PV     │  provisioner creates │  INDEFINITELY    │
     └────────┬────────┘  a PV for this claim │                  │
              │                    │          │  Pod stays in    │
              │                    ▼          │  Pending.        │
              │           ┌─────────────────┐ │  No error event  │
              │           │  binder matches │ │  that says so.   │
              │           │  claim ↔ new PV │ └──────────────────┘
              │           └────────┬────────┘        ▲
              │                    │                 │
              └────────┬───────────┘        an object without its
                       ▼                    component does nothing
              ┌─────────────────┐
              │   PVC is BOUND  │
              │  Pod can mount  │
              └─────────────────┘
```

**Static provisioning** is the §2 model, named. *A cluster administrator creates a number of PVs. They carry the details of the real storage, which is available for use by cluster users* [source: k8s-docs-persistent-volumes-2026-08-23]. Supply exists first; demand arrives later and matches against it.

**Dynamic provisioning** inverts the order. *When none of the static PVs the administrator created match a user's PersistentVolumeClaim, the cluster may try to dynamically provision a volume specially for the PVC* [source: k8s-docs-persistent-volumes-2026-08-23]. Demand arrives first, and supply is manufactured to fit it.

Note the word *may*. It is doing precise work, and the next sentence explains why.

> ★ **Fixed Point**
>
> **Dynamic provisioning requires two conditions, not one.**
>
> *This provisioning is based on StorageClasses: the PVC must request a storage class and the administrator must have created and configured that class for dynamic provisioning to occur* [source: k8s-docs-persistent-volumes-2026-08-23].
>
> The claim must name a class **and** that class must be configured to provision. One without the other yields a claim that waits forever, which, per §2, is not an error, not a timeout, and not a failure event. It is silence.

### Defaults, and one opt-out that surprises people

A cluster does not have to make every developer name a class explicitly. *You can mark a StorageClass as the default for your cluster. When a PVC does not specify a `storageClassName`, the default StorageClass is used* [source: k8s-docs-storage-classes-2026-08-25]. The mark is an annotation: `storageclass.kubernetes.io/is-default-class: "true"` [source: k8s-docs-persistent-volumes-depth-2026-08-25].

Where a default exists, that is what lets a developer write a five-line PVC and get a working disk without knowing any of this. Whether a given cluster has one is a question worth asking rather than assuming — the ⚓ below covers what happens when the answer is no.

Now the case that catches people. There are two ways a PVC can appear to "not ask for a class," and they behave differently:

| What the PVC has | What happens |
|---|---|
| No `storageClassName` field at all | The default StorageClass is used, if one exists |
| `storageClassName: ""` (empty string) | Dynamic provisioning is **disabled for that claim** |

*A PVC with its `storageClassName` set to `""` is explicitly stating that it is bound with a PV with no class, hence the PV's `storageClassName` must also be empty. A PVC with no `storageClassName` is not quite the same and is treated differently by the cluster* [source: k8s-docs-persistent-volumes-depth-2026-08-25]. And from the lifecycle section, stated as a consequence: *claims that request the class `""` effectively disable dynamic provisioning for themselves* [source: k8s-docs-persistent-volumes-2026-08-23].

> 🪝 **Snag:** `storageClassName: ""` is not "use whatever the cluster's default is." It is the opposite: "do not use a class at all, and do not provision anything for me." A reader who writes it expecting the default gets a claim that will only ever bind to a classless PV, and on a cluster where every PV comes from a StorageClass, that means it never binds. Empty string is an opt-out, not a shrug.

> ⚓ **Worth Securing:** A cluster can have no default at all: *if you don't mark any StorageClass as default (and one hasn't been set for you by, for example, a cloud provider), then Kubernetes cannot apply that defaulting for PersistentVolumeClaims that need it* [source: k8s-docs-storage-classes-2026-08-25]. Such a PVC is not rejected: *the new PVC creates as you defined it, and the `storageClassName` of that PVC remains unset until a default becomes available* [source: k8s-docs-storage-classes-2026-08-25]. And if a default appears later, the control plane retroactively updates those waiting PVCs to point at it [source: k8s-docs-storage-classes-2026-08-25]. This is a control loop doing exactly what control loops do: the desired state was underspecified, and the moment the information arrived, it reconciled *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*.

### The claim that waits because nobody installed the thing

You were set up for this two chapters ago. Chapter 10's closing said: *you will meet several objects in Chapter 11 that describe storage without providing any, and at least one arrangement where a claim sits unbound because the thing that would satisfy it has not been installed. You know what question to ask about that now.*

You do. The phrase is Chapter 3's, and Chapter 10 §3 named it as a pattern: **an object without its component does nothing** *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*.

A StorageClass is a description of a provisioning capability. It is not the provisioning capability. Create a StorageClass whose `provisioner` names a driver that nobody deployed, and you get a perfectly valid API object that provisions exactly nothing. Claims naming that class sit unbound. Pods referencing those claims sit `Pending`.

This is the third sighting of the same light. An Ingress with no Ingress controller routes nothing. A NetworkPolicy on a CNI plugin that doesn't implement policy blocks nothing. A StorageClass with no running provisioner creates nothing. Each time, the object exists, `kubectl get` shows it, `kubectl describe` shows a sensible spec, and nothing happens, because the object was always only ever a request addressed to a component that has to be separately installed and running.

You will see it a fourth time in §5, and by then the recognition should be automatic.

### When binding waits for the scheduler

One more StorageClass field, and it connects storage to something you learned four chapters ago in a way that is genuinely load-bearing rather than decorative.

*The `volumeBindingMode` field controls when volume binding and dynamic provisioning should occur. When unset, `Immediate` mode is used by default* [source: k8s-docs-storage-classes-2026-08-25]. `Immediate` means what it says: *volume binding and dynamic provisioning occurs once the PersistentVolumeClaim is created* [source: k8s-docs-storage-classes-2026-08-25].

That sounds fine until you think about *where* the volume gets created. Consider a cloud with three availability zones and block storage that can only be attached to instances in the same zone. The claim is created; `Immediate` binding provisions a volume in zone A; then the scheduler tries to place the Pod and discovers the only nodes with enough memory are in zone C. The documentation states the outcome without softening it: *for storage backends that are topology-constrained and not globally accessible from all Nodes in the cluster, PersistentVolumes will be bound or provisioned without knowledge of the Pod's scheduling requirements. This may result in unschedulable Pods* [source: k8s-docs-storage-classes-2026-08-25].

The fix is to make binding wait: *a cluster administrator can address this issue by specifying the `WaitForFirstConsumer` mode which will delay the binding and provisioning of a PersistentVolume until a Pod using the PersistentVolumeClaim is created. PersistentVolumes will be selected or provisioned conforming to the topology that is specified by the Pod's scheduling constraints. These include, but are not limited to, resource requirements, node selectors, pod affinity and anti-affinity, and taints and tolerations* [source: k8s-docs-storage-classes-2026-08-25].

Read that list of constraints again: resource requirements, node selectors, affinity, anti-affinity, taints and tolerations. That is Chapter 7's filter phase, item for item *[cross-bearing: see Ch 7 §2 — what makes a node feasible]*. `WaitForFirstConsumer` exists because scheduling and storage placement are not two decisions that happen to interact. They are one decision, and making them separately produces a Pod that cannot run.

The `local` volume documentation makes the same argument independently, which is a good sign that it is the real reason rather than a rationalization: *when using local volumes, it is recommended to create a StorageClass with `volumeBindingMode` set to `WaitForFirstConsumer`. Delaying volume binding ensures that the PersistentVolumeClaim binding decision will also be evaluated with any other node constraints the Pod may have, such as node resource requirements, node selectors, Pod affinity, and Pod anti-affinity* [source: k8s-docs-volume-types-depth-2026-08-25].

> 🔭 **Closer Look:** `WaitForFirstConsumer` sits above the depth this book judges KCNA to require. CNCF publishes the Storage competency as a single word and nothing more; this book's domain analysis reads that word as centring on the three-way distinction between PersistentVolume, PersistentVolumeClaim, and StorageClass — not on tuning binding modes. What you should carry forward from this subsection is the consequence, not the field name: **volume binding can wait on scheduling, because binding a volume before the scheduler has picked a node can bind it somewhere the Pod cannot go.** If you remember that sentence and forget `volumeBindingMode` entirely, you have taken the right thing.
>
> Two operational notes for the day you meet this in a real cluster. First, the mode is not universally supported: *the following plugins support `WaitForFirstConsumer` with dynamic provisioning: CSI volumes, provided that the specific CSI driver supports this* [source: k8s-docs-storage-classes-2026-08-25]. Second, it interacts badly with one particular shortcut: *if you choose to use `WaitForFirstConsumer`, do not use `nodeName` in the Pod spec to specify node affinity. If `nodeName` is used in this case, the scheduler will be bypassed and PVC will remain in `pending` state* [source: k8s-docs-storage-classes-2026-08-25]. Bypass the scheduler *[cross-bearing: see Ch 7 §6 — overruling the scheduler]* and you have removed the very consumer the binding was waiting for.

---