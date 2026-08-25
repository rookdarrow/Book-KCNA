## Chapter Summary

| Concept | Remember This |
|---|---|
| **The lifetime ladder** | Three rungs, two boundaries. Container restart kills rung one. Pod deletion kills rung two. Nothing in a Pod's lifecycle reaches rung three. |
| **`emptyDir`** | Safe across container crashes, deleted permanently when the Pod is removed. `medium: Memory` makes it tmpfs and charges it to the writing container's memory limit. |
| **`hostPath`** | A powerful escape hatch with many security risks. Avoid it; prefer a `local` PersistentVolume. Makes Pods silently node-dependent. |
| **`subPath`** | Cuts the update wire. ConfigMap, Secret, and downwardAPI mounts via `subPath` do not receive updates. |
| **PersistentVolume** | Supply. Cluster-scoped. Created by an administrator or by a provisioner. Captures the real storage's implementation details. |
| **PersistentVolumeClaim** | Demand. Namespaced. Requests a size and an access mode. **A Pod references this, never the PV.** |
| **Binding** | A control loop match. Exclusive, one-to-one, and filtered on more than size — class, selector, and `volumeName` each narrow the field, and every requirement is ANDed. An unmatched claim stays unbound indefinitely: not an error, just silence. |
| **PV phases** | The concept documentation names four: `Available` → `Bound` → `Released` → (`Failed`). `Released` is not `Available`. The API reference documents a fifth, `Pending`; if you meet it on an answer sheet, recognize it rather than rule it out. |
| **StorageClass** | Describes classes of storage. Names a `provisioner`, carries opaque `parameters`, sets `reclaimPolicy`. The name is the interface. |
| **Dynamic provisioning** | Two conditions: the claim names a class **and** the class is configured to provision. One without the other waits forever. |
| **`storageClassName: ""`** | Opts *out* of dynamic provisioning. Not the same as omitting the field, which gets the default. |
| **Access modes** | RWO / ROX / RWX count **nodes**. RWOP counts **Pods**, and exists because people assume RWO already does. One mode at a time. |
| **Reclaim policies** | `Retain` (kept, released, manual three-step reclamation), `Delete` (PV object and backing asset both destroyed), `Recycle` (deprecated). |
| **The inherited default** | Dynamic volumes inherit the class's policy, defaulting to `Delete`. Manually created PVs default to `Retain`. |
| **CSI** | The fourth pluggable interface. A cross-orchestrator standard, not a Kubernetes feature. A driver is a Deployment plus a DaemonSet, and Kubernetes will not install it for you. |
| **`volumeClaimTemplates`** | One PVC per Pod, named `<template>-<set>-<ordinal>`. Follows the Pod across reschedules because it was never on a node. |
| **PVC survival** | A StatefulSet's claims outlive the Pod *and* the StatefulSet, by design. Cleanup is manual, and nobody will remind you. |

<!-- AUTHOR-REVIEW: The PV-phases row now hedges the four-vs-five count, per the fact-accuracy FAIL on §2 ("there are four" asserted against k8s-api-ref-persistentvolume-v1-2026-08-25, which enumerates five and carries its own SOURCE DISAGREEMENT marker) and curriculum-audit P3. That fix is scoped to §2 as a 🪝 Snag; the summary must not be the first place the reader meets `Pending`. If §2's hedge is not applied, either apply it or revert this row to the bare four-phase chain. -->

---