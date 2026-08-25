---
source_url: "https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/"
fetched_at: "2026-08-25T02:36:00-0400"
authority: "Kubernetes project (kubernetes.io/docs)"
objectives_covered: ["D2.4"]
concepts_covered: ["volumeclaimtemplates", "per-replica-pvc", "pvc-survives-deletion", "persistent-volume-lifetime", "statefulset"]
---
# StatefulSets — storage sections (kubernetes.io/docs/concepts/workloads/controllers/statefulset/)

Companion to k8s-docs-statefulset-2026-08-24.md. Captures the example manifest (for
the volumeClaimTemplates block and the PVC naming the outline needs) and the
PersistentVolumeClaim-retention section, which that snapshot does not contain.

⚠ WORDING DRIFT — READ BEFORE CITING. The "Stable Storage" text recorded below,
retrieved 2026-08-25 from the page's Markdown source, differs from the text recorded
at k8s-docs-statefulset-2026-08-24.md lines 55–57. Where they differ, the difference
is load-bearing. See the manifest's Notes section. This file's version is the one
that was verifiable on 2026-08-25.

## Components (the example)

"The example below demonstrates the components of a StatefulSet."

    apiVersion: v1
    kind: Service
    metadata:
      name: nginx
      labels:
        app: nginx
    spec:
      ports:
      - port: 80
        name: web
      clusterIP: None
      selector:
        app: nginx
    ---
    apiVersion: apps/v1
    kind: StatefulSet
    metadata:
      name: web
    spec:
      selector:
        matchLabels:
          app: nginx # has to match .spec.template.metadata.labels
      serviceName: "nginx"
      replicas: 3 # by default is 1
      minReadySeconds: 10 # by default is 0
      template:
        metadata:
          labels:
            app: nginx # has to match .spec.selector.matchLabels
        spec:
          terminationGracePeriodSeconds: 10
          containers:
          - name: nginx
            image: registry.k8s.io/nginx-slim:0.24
            ports:
            - containerPort: 80
              name: web
            volumeMounts:
            - name: www
              mountPath: /usr/share/nginx/html
      volumeClaimTemplates:
      - metadata:
          name: www
        spec:
          accessModes: [ "ReadWriteOnce" ]
          storageClassName: "my-storage-class"
          resources:
            requests:
              storage: 1Gi

Note: "This example uses the ReadWriteOnce access mode, for simplicity. For production use, the Kubernetes project recommends using the ReadWriteOncePod access mode instead."

"In the above example:

* A Headless Service, named nginx, is used to control the network domain.
* The StatefulSet, named web, has a Spec that indicates that 3 replicas of the nginx container will be launched in unique Pods.
* The volumeClaimTemplates will provide stable storage using PersistentVolumes provisioned by a PersistentVolume Provisioner."

## Stable Storage

"For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim. In the nginx example above, each Pod receives a single PersistentVolume with a StorageClass of my-storage-class and 1 GiB of provisioned storage. If no StorageClass is specified, then the default StorageClass will be used. When a Pod is (re)scheduled onto a node, its volumeMounts mount the PersistentVolumes associated with its PersistentVolume Claims. Note that, the PersistentVolumes associated with the Pods' PersistentVolume Claims are not deleted when the Pods, or StatefulSet are deleted. This must be done manually."

## PersistentVolumeClaim retention

"The optional .spec.persistentVolumeClaimRetentionPolicy field controls if and how PVCs are deleted during the lifecycle of a StatefulSet."

"there are two policies you can configure for each StatefulSet:"

"whenDeleted: Configures the volume retention behavior that applies when the StatefulSet is deleted."

"whenScaled: Configures the volume retention behavior that applies when the replica count of the StatefulSet is reduced; for example, when scaling down the set."

"For each policy that you can configure, you can set the value to either Delete or Retain."

"Delete: The PVCs created from the StatefulSet volumeClaimTemplate are deleted for each Pod affected by the policy. With the whenDeleted policy all PVCs from the volumeClaimTemplate are deleted after their Pods have been deleted. With the whenScaled policy, only PVCs corresponding to Pod replicas being scaled down are deleted, after their Pods have been deleted."

"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted. This is the behavior before this new feature."

"Bear in mind that these policies only apply when Pods are being removed due to the StatefulSet being deleted or scaled down. For example, if a Pod associated with a StatefulSet fails due to node failure, and the control plane creates a replacement Pod, the StatefulSet retains the existing PVC. The existing volume is unaffected, and the cluster will attach it to the node where the new Pod is about to launch."

"The default for policies is Retain, matching the StatefulSet behavior before this new feature."

Example policy shown on the page:

    apiVersion: apps/v1
    kind: StatefulSet
    ...
    spec:
      persistentVolumeClaimRetentionPolicy:
        whenDeleted: Retain
        whenScaled: Delete
    ...

"The StatefulSet controller adds owner references to its PVCs, which are then deleted by the garbage collector after the Pod is terminated. This enables the Pod to cleanly unmount all volumes before the PVCs are deleted (and before the backing PV and volume are deleted, depending on the retain policy). When you set the whenDeleted policy to Delete, an owner reference to the StatefulSet instance is placed on all PVCs associated with that StatefulSet."

RETRIEVAL NOTE — the retrieval also returned a sentence stating that the
`StatefulSetAutoDeletePVC` feature gate must be enabled on the API server and the
controller manager to use `persistentVolumeClaimRetentionPolicy`. That sentence
almost certainly sits adjacent to a feature-state marker that the retrieval stripped,
and the gate's current stage could not be confirmed in this pass. DO NOT state a
feature-gate requirement or a stability stage for this field in the drafted chapter.
The behaviour that IS safe to state is the default: Retain, for both policies.

NOTE FOR §6 — the PVC-survival Fixed Point is supported here TWICE, and the second
support is the stronger one. "Retain (default): PVCs from the volumeClaimTemplate are
not affected when their Pod is deleted" plus "The default for policies is Retain"
establishes PVC survival as a default policy value, which is a cleaner claim than the
Stable Storage sentence (which, in its current wording, is about PersistentVolumes
rather than PersistentVolumeClaims). Lead §6's citation with the retention text.
