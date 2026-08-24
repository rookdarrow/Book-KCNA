emonset-2026-08-24]. **A** treats the count as fixed, which is the opposite of the resource's purpose. **C** describes something closer to a single-replica Deployment. **D** is the trap: the count is a consequence of node eligibility rather than a field you choose, which is also why HPA does not apply to DaemonSets [source: k8s-docs-hpa-2026-08-24].

**18 — B.** `Succeeded` means all containers terminated in success and will not be restarted [source: k8s-docs-pod-lifecycle-2026-08-23], and a Job continues retrying until a specified number of Pods successfully terminate [source: k8s-docs-job-2026-08-24]. This is where that phase finally earns its place: for a long-running service, `Succeeded` would be a malfunction; for a Job, it's the goal. Note the level the question asks about — `Succeeded` is a *Pod* phase; the Job object itself finishes as `Complete` [source: k8s-docs-job-2026-08-24]. **C** is wrong and is the mirror-image error — it's `Failed` that means at least one container terminated in failure. **A** contradicts run-to-completion. **D** confuses reporting with phase.

**19 — B.** A CronJob creates Jobs on a repeating schedule [source: k8s-docs-cronjob-2026-08-24], and each Job creates the Pods that do the work [source: k8s-docs-job-2026-08-24]. Seven firings, seven Jobs, at least seven Pods. **A** skips the Job layer — this is the misconception the Job-versus-CronJob distinction is meant to prevent. **C** contradicts run-to-completion. **D** imports revision vocabulary from Deployments, where it doesn't belong. (Note the docs' caveat that scheduling is approximate and two Jobs might occasionally be created, or none [source: k8s-docs-cronjob-2026-08-24] — which is why Jobs should be idempotent.)

**20 — C.** A controller tracks at least one Kubernetes resource type whose objects have a `spec` field representing desired state, and the controller is responsible for making current state come closer to it [source: k8s-docs-controllers-2026-08-23]. A custom controller does exactly this, on a custom resource, providing a true declarative API when paired with one [source: k8s-docs-custom-resources-2026-08-23]. Same shape, different resource type, different author. **B** is false — a custom controller normally runs outside the control plane [source: k8s-docs-operator-pattern-2026-08-23]. **A** denies the whole point of §8. **D** confuses privilege with mechanism.

**21 — B.** The operator's controller normally runs outside the control plane, much as you would run any containerized application — for example, as a Deployment [source: k8s-docs-operator-pattern-2026-08-23]. **A** is the intuitive-but-wrong answer: extending Kubernetes doesn't require *being* Kubernetes. **C** describes a client-side tool, but operators are long-running API clients that must keep watching. **D** misunderstands a CRD as executable rather than as a schema.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **Workload resource** | You don't manage Pods; you declare intent and a controller manages Pods for you |
| **Ownership chain** | Deployment → ReplicaSet → Pod. Deployment holds template + strategy; ReplicaSet maintains the count |
| **ReplicaSet** | Maintains a stable set of replica Pods. The control loop, with `.spec.replicas` as desired state |
| **Scaling vs self-healing** | The same operation. The loop can't tell "you asked for more" from "one died" |
| **Selector** | Membership is a query, not a list. Template labels must satisfy the selector |
| **Owner reference** | What makes cascading deletion work — and what adoption sets on Pods a controller acquires |
| **Overlapping selectors** | Two controllers fighting over one Pod population. Documented as a hazard to design around, not as a configuration the API rejects |
| **`RollingUpdate`** | The default. New ReplicaSet up, old one down, at a controlled rate |
| **`maxSurge` / `maxUnavailable`** | Both default to 25%. Surge is above the line (rounds up); unavailable is below (rounds down) |
| **`Recreate`** | All old Pods killed first. Downtime, deliberately chosen, for apps that can't run two versions |
| **What makes a rollout safe** | Readiness. A Pod that never reports ready never counts as available, so it never displaces the old one |
| **Revision** | Created if and only if `.spec.template` changes. Scaling does not create one |
| **Rollback** | Sets the Pod template to a previous value and runs the same rolling update backwards |
| **StatefulSet** | For Pods that are *not interchangeable*. Stable ordinal identity, stable network name, own storage |
| **Stable identity** | `db-1`'s replacement is also `db-1`, and it reattaches to the same claim. The storage belongs to the identity |
| **The disk trap** | "Writes to disk" does not mean StatefulSet. Interchangeability decides |
| **DaemonSet** | One Pod per matching node, automatically as nodes join. The count is a consequence of node eligibility, not a setting |
| **Job** | Runs to completion, once. Its Pods reach phase `Succeeded` or `Failed`; the Job itself finishes as `Complete` or `Failed` |
| **CronJob** | Creates the same Job repeatedly on a cron schedule. Its output is Jobs |
| **Custom resource** | A new API endpoint. On its own, it only stores structured data |
| **Operator pattern** | Custom resource + custom controller. The controller normally runs as a Deployment |
| **The recurring rule** | The object exists, but nothing happens without the component |

---

## The Voyage Ahead

You can now write down what should be true and hand the responsibility to a loop. There is one thing that loop cannot do for you.

It creates a Pod. It does not decide *where the Pod goes*. Every replacement in this chapter, every surge Pod during a rolling update, every DaemonSet Pod on a newly joined node — each one arrives in the world unplaced, and something else has to find it a machine with room. Usually that works so smoothly you never think about it. Sometimes it doesn't, and a Pod sits in `Pending` while the count it was supposed to satisfy stays unsatisfied, and the loop that created it goes on cheerfully wanting one more.

Chapter 7 is about the component that makes that decision, the two-step process it uses, and the vocabulary you have for influencing it — how a Pod expresses what it needs from a machine, and how a machine expresses what it will accept. You've already met the mechanism in disguise: the DaemonSet's tolerations in §7 were a node saying "not for general traffic" and a controller saying "this one's an exception."

> *"You may declare what should exist. Where it exists is a separate question, and the sea does not always have room where you wanted it."*

---

🏆 **Safe Harbor**

Chapter 6 complete. You came in able to read a Pod and left able to author a fleet — six workload resources, one control loop, and the beginning of the recognition that the loop is the whole system rather than a feature of it.

**Voyage Progress:** 🗺️ → 🌊 → 🌅
*Part II, Chapter 6 of 18. The trunk of the book is behind you.*