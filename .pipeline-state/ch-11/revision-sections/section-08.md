## ☆ Taking Your Bearings #1

Five questions on the lifetime ladder and the supply/demand split. Answers and explanations follow; attempt them first.

**1.** A Pod runs a single container that writes `/data/cache.db`, where `/data` is an `emptyDir` volume. The container hits a null pointer and exits with code 1. The kubelet restarts it. Then, ten minutes later, you run `kubectl delete pod` and the Deployment's ReplicaSet creates a replacement. What is the state of `cache.db` after each event?

A) Gone after the crash; gone after the delete
B) Present after the crash; gone after the delete
C) Present after the crash; present after the delete
D) Gone after the crash; present after the delete

**2.** *[retrieval: ch2]* A different container in a different Pod writes `/tmp/scratch.log`, with no volume mounted anywhere. The process crashes and the kubelet restarts the container. Where was that file written, and is it still there?

A) To the image's read-only layers; still there, because image layers are immutable
B) To the container's writable layer; still there, because the layer persists across restarts
C) To the container's writable layer; gone, because the restarted container is assembled fresh from the image
D) To the container's writable layer; gone, because the Pod was replaced

**3.** Which statement correctly describes what a Pod references in order to use persistent storage?

A) The Pod's `volumes` block names a PersistentVolume directly, and Kubernetes finds a matching claim
B) The Pod's `volumes` block names a PersistentVolumeClaim, and the cluster uses the claim to find the bound PersistentVolume
C) The Pod's `volumes` block names a StorageClass, which selects a PersistentVolume at mount time
D) The Pod names both the PersistentVolume and the PersistentVolumeClaim, so the binding can be verified

**4.** A cluster has one PersistentVolume: 100Gi, `Available`, no StorageClass, no labels. A user creates a 10Gi PVC with no class and no selector; it binds. A second user then creates a 5Gi PVC with no class and no selector. What happens to the second claim?

A) It binds to the same PV, since 90Gi of capacity remains unused
B) It binds to the same PV and the first claim is evicted, since binding is exclusive
C) It remains unbound indefinitely, and will bind only if a matching volume becomes available
D) It fails immediately with an error, since no `Available` PV exists

**5.** An administrator deletes a PersistentVolumeClaim whose PV has the `Retain` reclaim policy. Immediately afterward, what phase is the PersistentVolume in, and what does that phase mean?

A) `Available` — the volume is free and the next matching claim will bind to it
B) `Released` — the claim is gone, but the volume has not been reclaimed and is not yet reusable
C) `Failed` — deleting a bound claim is an error condition
D) `Bound` — the reclaim policy `Retain` preserves the binding until an admin intervenes

---

**Answers with Explanations:**

**1 — B.** Present after the crash. Gone after the delete. If you reached for C, you reached for the trap this question was built around, and you are in large company.

- **A is wrong** because a container crash does not remove the Pod from the node, and *the data in an `emptyDir` volume is safe across container crashes* [source: k8s-docs-volume-types-depth-2026-08-25]. The file survives the restart.
- **B is correct.** Crash → survives (rung two beats a container restart). Delete → gone, because *when a Pod is removed from a node for any reason, the data in the `emptyDir` is deleted permanently* [source: k8s-docs-volume-types-depth-2026-08-25]. And the replacement Pod is a *different Pod*; its `emptyDir` is created empty when it is assigned to a node.
- **C is wrong** and is the single most common `emptyDir` misconception: assuming that because a volume survived a container restart, it must be persistent. It survives one boundary and not the other.
- **D is wrong** in both halves, and each half is a belief worth naming. "Gone after the crash" is *restart means fresh everything* — true of the container filesystem, false of the volume. "Present after the delete" is *the controller restores the volume along with the Pod* — the ReplicaSet restores the Pod, and an `emptyDir` in a new Pod is new and empty. D has the ladder exactly inverted.

**2 — C.** The file went to the container's writable layer, and the restarted container gets a clean state assembled from the image [source: k8s-docs-volumes-2026-08-23]. Rung one survives nothing.
- **A is wrong** because image layers are read-only; a write to a path backed by an image layer is copied up into the writable layer, not written into the image.
- **B is wrong** because it confuses the writable layer's *location* (correct) with its *lifetime* (wrong). This is the misconception the whole ladder exists to correct.
- **D is wrong** on the event, and it is the near-miss worth sitting with. The location is right and the outcome is right — the file is gone — but nothing replaced the Pod. The container exited and the kubelet restarted it inside the same Pod, on the same node. Rung one is erased by the *container* boundary, several rungs below the one D names. Arriving at the right outcome through the wrong boundary is still arriving wrongly, and the exam will offer you that option.

**3 — B.** *Pods use claims as volumes. The cluster inspects the claim to find the bound volume and mounts that volume for a Pod* [source: k8s-docs-persistent-volumes-2026-08-23].
- **A is wrong**, and it is the reversal to watch for. It has the direction of the relationship backwards: claims find volumes, not the other way around, and the Pod's reference terminates at the claim.
- **C is wrong**: a StorageClass is not something a Pod mounts. §3 covers what it actually does.
- **D is wrong**: the Pod names only the claim. It has no field for a PV.

**4 — C.** *Claims will remain unbound indefinitely if a matching volume does not exist. Claims will be bound as matching volumes become available* [source: k8s-docs-persistent-volumes-2026-08-23]. The only PV is `Bound`, so there is nothing to match.
- **A is wrong** because *a PVC to PV binding is a one-to-one mapping* and binds are exclusive [source: k8s-docs-persistent-volumes-2026-08-23]. Leftover capacity is not shareable. This is the "big enough, so it fits" trap.
- **B is wrong**: binding exclusivity protects the existing bind; it does not preempt it.
- **D is wrong** in an instructive way. There is no immediate error. The claim sits, quietly, and the Pod that references it sits in `Pending`. "Fails immediately" would at least be visible; "waits forever" is what actually happens.

**5 — B.** *When the PersistentVolumeClaim is deleted, the PersistentVolume still exists and the volume is considered 'released'. But it is not yet available for another claim because the previous claimant's data remains on the volume* [source: k8s-docs-persistent-volumes-depth-2026-08-25].
- **A is wrong**, and this specific wrong answer is worth more than the right one. `Released` ≠ `Available`. The volume is not reusable. §4 covers what an administrator has to do to make it so.
- **C is wrong**: the `Failed` phase records a volume whose automatic reclamation did not succeed [source: k8s-docs-persistent-volumes-depth-2026-08-25]. That is a later event and a different one. Deleting a bound claim is routine, not an error.
- **D is wrong**: the binding does not survive the claim's deletion. The claim is gone.

---

**If you scored 0–2:** Go back to §1's ladder figure and §2's Fixed Point specifically, about eight minutes of re-reading. The rest of the chapter builds directly on those two.

**If you scored 3–4:** Solid. Review the ones you missed, understand *why*, and continue.

**If you scored 5:** You have the foundation. §3 and §4 are where the exam yield concentrates, and you are in good shape to absorb them.

---

**Checkpoint: You've Now Mastered**
✓ The three-rung lifetime ladder and the two boundaries that define it
✓ Which volume types live on which rung, and what `subPath` cuts off
✓ PV as supply, PVC as demand, and why a Pod references only the claim
✓ Binding as an exclusive, one-to-one control-loop match that waits indefinitely
✓ The PV phases, and that `Released` is not `Available`

Two questions remain open, and they are the ones that matter: where does a PV come from if nobody made one, and what happens to the data when the claim is gone?

🗺️→🌊→🌅 · **Voyage Progress: two sections of seven. The vocabulary is set; the mechanics start now.**

---