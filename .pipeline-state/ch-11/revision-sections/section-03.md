## 🧭 Soundings

Before reading this chapter, try these eight questions. Your score determines how to approach the content. No score is a bad score; each one points at a different reading strategy.

1. A container writes a file to `/tmp/report.json`, then the process inside it crashes. The kubelet restarts the container. Is the file still there? Which layer was it written to?

2. Chapter 5 said that every container in a single Pod shares two things. What are they? One of them is what this entire chapter is about.

3. Is a `PersistentVolume` a namespaced resource or a cluster-scoped one? How would you settle the question from the cluster itself, without looking it up?

4. What makes a StatefulSet's Pods non-interchangeable in a way a Deployment's Pods are not? And what did Chapter 6 say, in as many words, that it was deliberately *not* explaining yet?

5. In a traditional storage array, who creates a LUN and who requests one? Does the person requesting need to know the array's vendor?

6. Chapter 10 asked you to hold a count. Name the pluggable interfaces you have met so far in this book, and say what each one hands to somebody outside the Kubernetes project.

7. You delete a virtual machine. Does its attached disk go with it? Does your answer depend on how the disk came to exist in the first place?

8. Can two separate machines mount the same block device read-write at the same time, without a clustered filesystem underneath? What goes wrong if they try?

<details>
<summary>Click for answers + reading strategy</summary>

1. **No — the file is gone.** It was written to the container's writable layer, which is discarded and rebuilt from the image when the container restarts. *[cross-bearing: see Ch 2 §2 — the writable container layer]*

2. **A network namespace (and therefore an IP address) and volumes.** Volumes are this chapter's whole subject. *[cross-bearing: see Ch 5 §1 — the Pod as the unit of scheduling]*

3. **Cluster-scoped.** You settle it from the cluster with `kubectl api-resources --namespaced=false`, which lists every resource kind that does not live inside a Namespace. *[cross-bearing: see Ch 4 §3 — namespaced vs cluster-scoped]*

4. **A stable ordinal identity that survives rescheduling.** `web-0` stays `web-0` on whatever node it lands on. Chapter 6 said outright that it was deferring how that Pod's storage is *provisioned, requested, sized, reclaimed, or shared*. This chapter is where that debt comes due.

5. **The storage administrator creates the LUN; the application team requests one.** The requester specifies a size and a performance need, and does not have to know whether the array is NetApp, Pure, or a pile of disks in a closet.

6. **Three so far.** CRI at the container runtime (Chapter 2), CRDs at the API itself (Chapter 6), CNI at the network (Chapter 9). Each hands a published contract to somebody outside the Kubernetes project so they can plug in an implementation without editing Kubernetes' source. The fourth arrives in §5 of this chapter.

7. **It depends, and the "depends" is the interesting part.** A boot disk created automatically with the VM usually dies with it; a disk you provisioned separately and attached usually survives. Provisioning history determines deletion behavior.

8. **No, not safely.** This is general storage background rather than a Kubernetes rule: two independent filesystem drivers each believing they own the block device will corrupt it, because each caches metadata the other does not know it changed. A clustered filesystem exists to coordinate exactly that.

**Scoring.** Six of the eight questions above ask for two things. Count a question right only if both halves are right — a half-answer is a gap, and the rubric below is calibrated on that basis.

**If you got 6+ right:** Skim this chapter. Focus on the ★ Fixed Points and the ⚠ Navigational Hazards callouts, and go straight to ☆ Taking Your Bearings #2. That checkpoint is where this chapter's domain analysis puts the heaviest exam yield, and where a confident reader is still most likely to lose points.

**If you got 3–5 right:** Read at normal pace. The material is in reach and this chapter is calibrated for you.

**If you got 0–2 right:** Read carefully, but do not go back and re-read whole chapters. Check three *sections*: Ch 5 §1 (what a Pod shares), Ch 4 §3 (cluster-scoped resources), and Ch 6 §6 (StatefulSet identity). That is three sections, not three chapters. This material assumes narrow, specific things rather than everything that came before it.

</details>

---