## ☀️ §7 — Outliving the Pod That Asked

Look back at what you did in this chapter, and notice that you only ever asked one question.

*Does the file survive the container restart?* *Does the volume survive the Pod?* *Does the claim survive the workload?* *Does the data survive the claim?* Four questions, one shape: **what survives what?** Every section widened the scope by exactly one step, and the ladder in §1 was the whole chapter drawn small.

Here is what makes it worth the walk. At every rung, the thing that would seem to have the most at stake in the answer is not the thing that decides it.

The container does not decide whether its files survive a restart. The image layout decided that, before the container existed. The Pod does not decide whether its volume survives deletion; the volume's *type* decided it, chosen in a manifest by whoever wrote the PodSpec. And the claim does not decide whether the data survives the claim's deletion. The StorageClass decided that, in a `reclaimPolicy` field, in a manifest written by an administrator who was configuring a cluster and had never heard of your application.

The workload never gets a vote. That is not a defect. It is the same separation that runs through everything you have learned:

A Pod does not decide which node it lands on; the scheduler does, by filtering and scoring *[cross-bearing: see Ch 7 §1 — one decision, made once]*. A Deployment does not decide how many replicas exist right now; a control loop does, reconciling toward the number in the spec *[cross-bearing: see Ch 3 §6 — controllers and the control loop]*. And an object does not decide whether anything happens to it; the component that watches for it does, if somebody installed one *[cross-bearing: see Ch 10 §3 — the object is not the implementation]*.

Storage is that pattern applied to durability. And the reason for naming it is practical rather than aesthetic: it is why a developer can be handed a cluster they have never seen and be productive on it the same afternoon. They write a claim. Somebody else — possibly years ago, possibly a vendor they will never meet, possibly a CSI driver running as a DaemonSet on nodes they will never log into — arranged for that claim to be satisfiable. The developer does not need to know how. That ignorance is not a gap in their knowledge. It is the interface working.

Go back to the epigraph. *The cargo does not belong to the crew. It was aboard before this watch, and it will be aboard after.* Watches change. What sits below the waterline is not consulted about the handover, and that is exactly why the handover works — a ship that renegotiated its cargo at every change of watch would not be carrying anything, it would be holding a meeting. The Pod is a watch. The claim is the entry in the papers. What becomes of the cargo when the papers are torn up was settled in a `reclaimPolicy` field, long before this watch came aboard.

> ☀️ **Zenith:** Chapter 4 taught you that a Kubernetes object is a record of intent, and that the record outlives the thing that acts on it *[cross-bearing: see Ch 4 §1 — you file a declaration]*. That is the same sentence as this chapter's title.
>
> The claim is a record of intent about storage. It outlives the Pod that asked for it, because it was never the Pod's to begin with. It was filed on the Pod's behalf, against a supply the Pod knows nothing about, under terms settled before the Pod was scheduled. **Storage outlives the Pod that asked for it**, not because storage is special, but because *records of intent outlive the things that act on them*, and a claim is a record of intent.
>
> Ten chapters of Kubernetes, and it is one idea wearing different clothes.

<!-- FIGURE: ch11-zenith-outliving-the-pod -->
```
   Pod    ├──web-1──┤        ├──web-1──┤    ├──web-1──┤
           (node-b)           (node-e)       (node-e)
              ╎                  ╎              ╎
              ╎ claims           ╎ claims       ╎ claims
              ▼                  ▼              ▼
 Storage ═══════════════════════════════════════════════════▶
          www-web-1 — one continuous line, never broken

                    time ──────────────────────────────────▶
```

---