job-2026-08-24]. CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24]. |
| **Custom resource** | An API endpoint that is not necessarily present in a default install, registered dynamically, accessed with `kubectl` like anything else [source: k8s-docs-custom-resources-2026-08-23]. |
| **CustomResourceDefinition** | Defines a custom resource with a name and schema; the API then serves and stores it for you [source: k8s-docs-custom-resources-2026-08-23]. |
| **Operator pattern** | Custom resource + custom controller [source: k8s-docs-custom-resources-2026-08-23]. The controller normally runs outside the control plane, as a Deployment [source: k8s-docs-operator-pattern-2026-08-23]. |
| **The one shape** | Six resources, one control loop. Only the desired state differs. |

---

## The Voyage Ahead

The loop noticed a gap and created a Pod. That Pod does not yet run anywhere.

Between "this Pod object exists" and "this container is executing on a machine" sits a decision nobody in this chapter made. Something has to look at a Pod with no node assigned to it, look at every node in the cluster, and choose. It has to know how much memory the Pod asked for and how much each node has left. It has to respect the fact that some nodes are reserved, some are draining, and some are deliberately hostile to workloads that have not been told they are welcome.

Most of the time this happens in milliseconds and you never think about it. The times you do think about it are the times a Pod sits in `Pending` and nothing you do to the Deployment changes anything — because the Deployment's job ended the moment the Pod object existed, and the problem is one layer down. That Pod is a record of intent with nowhere to go, and the reason it has nowhere to go is written in the resource requests you set in Chapter 5 and the node properties you have not met yet.

Chapter 7 introduces the scheduler: how a Pod gets placed, what it is actually weighing, and the four mechanisms — `nodeSelector`, affinity, taints, and tolerations — you use to influence a decision you do not make yourself. You will also finally get a satisfying answer to a question this chapter raised and dropped: a DaemonSet is supposed to run on every node, so what happens when a node has been marked as one that workloads should stay off?

You know how a fleet is described. Next you find out how a berth is assigned.

> *"You can write the standing order in an afternoon. Finding the water to carry it out is the other half of the work."*
> — Lodestar Ledgers

---

## 🏆 Safe Harbor

Chapter 6 complete. Take the measure of what changed.

You arrived able to read what a Pod was telling you. You leave able to state what should be true about a group of them and hand the maintenance of that statement to something that never sleeps and never forgets. That is not a larger vocabulary. It is a different job.

Specifically, you can now:

✓ Trace intent from a Deployment through a ReplicaSet to a running container, and say which layer owns which piece
✓ Explain why a deleted Pod comes back with nobody having done anything
✓ Predict a rolling update's ceiling and floor from two fields and a replica count
✓ Name the thing that makes a rollout safe rather than merely gradual — and know it was already in your hands at the end of Chapter 5
✓ State the revision rule exactly, including the part that catches people
✓ Pick the right workload resource by asking about the work before asking about the software
✓ Define a custom resource, a custom controller, and the pattern that is both — and know why installing one without the other does nothing

And one thing that is not a bullet point: you have seen the control loop twice now, at two altitudes, and recognized it the second time. Hold onto that recognition. You are going to need it once more, and the third time is the one that matters.

🗺️ Chart → 🌊 Passage → 🌅 **Dawn** — Part II's trunk is behind you.