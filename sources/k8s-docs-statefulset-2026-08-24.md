---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/"
fetched_at: "2026-08-24T07:57:36-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D1.1", "D1 Core Concepts"]
concepts_covered: ["statefulset", "stable-pod-identity", "pod-interchangeability", "workload-resource", "pod-template", "rolling-update"]
---
# StatefulSets (kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

## What a StatefulSet is

A StatefulSet runs a group of Pods, and maintains a sticky identity for each of those Pods. This is useful for managing applications that need persistent storage or a stable, unique network identity.

StatefulSet is the workload API object used to manage stateful applications.

Manages the deployment and scaling of a set of Pods, *and provides guarantees about the ordering and uniqueness* of these Pods.

Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec. Unlike a Deployment, a StatefulSet maintains a sticky identity for each of its Pods. These pods are created from the same spec, but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling.

## Using StatefulSets

StatefulSets are valuable for applications that require one or more of the following:

- Stable, unique network identifiers.
- Stable, persistent storage.
- Ordered, graceful deployment and scaling.
- Ordered, automated rolling updates.

## Limitations

- The storage for a given Pod must either be provisioned by a PersistentVolume Provisioner based on the requested *storage class*, or pre-provisioned by an admin.
- Deleting and/or scaling a StatefulSet down will *not* delete the volumes associated with the StatefulSet. This is done to ensure data safety, which is generally more valuable than an automatic purge of all related StatefulSet resources.
- StatefulSets currently require a Headless Service to be responsible for the network identity of the Pods. You are responsible for creating this Service.
- StatefulSets do not provide any guarantees on the termination of pods when a StatefulSet is deleted. To achieve ordered and graceful termination of the pods in the StatefulSet, it is possible to scale the StatefulSet down to 0 prior to deletion.
- When using Rolling Updates with the default Pod Management Policy (`OrderedReady`), it's possible to get into a broken state that requires manual intervention to repair.

## Pod Identity

StatefulSet Pods have a unique identity that consists of an ordinal, a stable network identity, and stable storage. The identity sticks to the Pod, regardless of which node it's (re)scheduled on.

### Ordinal Index

For a StatefulSet with N replicas, each Pod in the StatefulSet will be assigned an integer ordinal, that is unique over the Set. By default, pods will be assigned ordinals from 0 up through N-1. The StatefulSet controller will also add a pod label with this index: `apps.kubernetes.io/pod-index`.

### Stable Network ID

Each Pod in a StatefulSet derives its hostname from the name of the StatefulSet and the ordinal of the Pod. The pattern for the constructed hostname is `$(statefulset name)-$(ordinal)`. The example above will create three Pods named `web-0,web-1,web-2`. A StatefulSet can use a Headless Service to control the domain of its Pods. The domain managed by this Service takes the form: `$(service name).$(namespace).svc.cluster.local`, where "cluster.local" is the cluster domain. As each Pod is created, it gets a matching DNS subdomain, taking the form: `$(podname).$(governing service domain)`, where the governing service is defined by the `serviceName` field on the StatefulSet.

Depending on how DNS is configured in your cluster, you may not be able to look up the DNS name for a newly-run Pod immediately. This behavior can occur when other clients in the cluster have already sent queries for the hostname of the Pod before it was created. Negative caching (normal in DNS) means that the results of previous failed lookups are remembered and reused, even after the Pod is running, for at least a few seconds.

As mentioned in the limitations section, you are responsible for creating the Headless Service responsible for the network identity of the pods.

### Stable Storage

For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim. In the nginx example above, each Pod receives a single PersistentVolumeClaim named `www`. This PersistentVolumeClaim will either be provisioned by a PersistentVolume Provisioner based on the StorageClass named `my-storage-class` or it will be pre-provisioned by an administrator. The same PersistentVolumeClaim will be bound to a Pod throughout its lifecycle.

When a Pod is (re)scheduled onto a (different) Node, its volumeMounts mount the PersistentVolumeClaim(s) associated with its PersistentVolume(s). Note that, the PersistentVolumeClaim(s) associated with the Pod's PersistentVolume(s) are not deleted when the Pod, or the StatefulSet is deleted. This must be done manually.

### Pod Name Label

FEATURE STATE: Kubernetes v1.33 [stable]

When a StatefulSet controller creates a Pod, it adds a label, `statefulset.kubernetes.io/pod-name`, that is set to the name of the Pod. This label allows you to attach a Service to a specific Pod in the StatefulSet.

## Deployment and Scaling Guarantees

- For a StatefulSet with N replicas, when Pods are being deployed, they are created sequentially, in order from {0..N-1}.
- When Pods are being deleted, they are terminated in reverse order, from {N-1..0}.
- Before a scaling operation is applied to a Pod, all of its predecessors must be Running and Ready.
- Before a Pod is terminated, all of its successors must be completely shut down.

The StatefulSet should not specify a pod.Spec.TerminationGracePeriodSeconds of 0. This practice is unsafe and strongly discouraged.

In the nginx example above, if you tried to scale the StatefulSet down from 3 replicas to 1 replica, the StatefulSet would not delete `web-0`. The StatefulSet controller would wait until `web-2` was Running and Ready, prior to deleting `web-1`. If, after `web-1` is deleted, `web-2` becomes not Ready, the StatefulSet controller would wait until `web-2` is Running and Ready again, before attempting any further deletions.

### Pod Management Policies

StatefulSet allows you to relax its ordering guarantees while maintaining its uniqueness guarantees via the `.spec.podManagementPolicy` field.

#### OrderedReady Pod Management

`OrderedReady` pod management is the default for StatefulSets. It implements the behavior described above.

#### Parallel Pod Management

`Parallel` pod management tells the StatefulSet controller to launch or terminate all Pods in parallel, and not to wait for Pods to become Running and Ready or completely terminated prior to launching or terminating other Pods. This option only affects the behavior for scaling operations. Updates are not affected.

## Update strategies

StatefulSet's `.spec.updateStrategy` field allows you to configure and disable automated rolling updates for containers, labels, resource request/limits, and annotations for the Pods in a StatefulSet.

### OnDelete

`OnDelete` update strategy implements the legacy (1.6 and prior) behavior. With this strategy, the StatefulSet controller will not automatically update the Pods in a StatefulSet. Users must manually delete Pods to cause the controller to create new Pods that reflect modifications made to the StatefulSet's `.spec.template`.

### RollingUpdate

The `RollingUpdate` update strategy implements automated, rolling update for the Pods in a StatefulSet. When `.spec.updateStrategy.type` is not specified, `RollingUpdate` is the default strategy. The StatefulSet controller will delete and recreate each Pod in the StatefulSet. It will proceed in the same order as Pod termination (from the largest ordinal to the smallest), updating each Pod one at a time.
