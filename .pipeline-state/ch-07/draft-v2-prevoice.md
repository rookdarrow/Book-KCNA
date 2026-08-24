here in this chapter. Here nothing performed the feasibility check, so there is nothing waiting for conditions to improve.

**17 — B.** Scheduling Policies configure the scheduler with Predicates for filtering and Priorities for scoring [source: k8s-docs-kube-scheduler-2026-08-23]. The names changed; the two steps didn't.
- **A inverts the mapping.** Predicates decide feasibility, which is filtering; priorities rank the survivors, which is scoring.
- **C is wrong on its specific claim** that filtering had no configurable component: Predicates *were* exactly that component, and `PodFitsResources` is one of them.
- **D denies a correspondence the source states directly**, naming Predicates against filtering and Priorities against scoring in a single sentence.

**18 — B.** With `operator: Exists` and no value specified, the toleration matches any value for that key; and an empty effect matches all effects with the given key [source: k8s-docs-taints-tolerations-2026-08-23].
- **A treats an empty effect as a default rather than a wildcard.** It widens the match to every effect, rather than narrowing it to `NoSchedule`.
- **C wildcards the wrong field.** `Exists` wildcards the *value*; wildcarding the *key* requires an empty key — and if the key is empty, the operator must be `Exists` [source: k8s-docs-taints-tolerations-2026-08-23].
- **D is wrong because an empty effect is explicitly permitted and explicitly meaningful** [source: k8s-docs-taints-tolerations-2026-08-23]. And remember the multi-taint procedure while you're here: start with all of a node's taints, ignore the ones the Pod tolerates, and the remainder still apply [source: k8s-docs-taints-tolerations-depth-2026-08-24]. Tolerating three of four taints does not get you aboard.

---

## Chapter Summary

| Concept | Remember This |
|---|---|
| **The two-step operation** | Filter, then score. Filtering produces the feasible set; scoring ranks it. |
| **Scheduling factors** | Resource requirements, hardware/software/policy constraints, affinity and anti-affinity, data locality, inter-workload interference, deadlines [source: k8s-docs-kube-scheduler-2026-08-23] [source: k8s-docs-cluster-architecture-2026-08-23]. You state the first three; the rest are the scheduler's own business. |
| **Binding** | A notification to the API server [source: k8s-docs-kube-scheduler-2026-08-23] — concretely, writing `.spec.nodeName` [source: k8s-docs-daemonset-2026-08-24]. Not an act of starting anything. |
| **Who starts the container** | The kubelet on the chosen node [source: k8s-docs-cluster-architecture-2026-08-23]. Never the scheduler. |
| **Tie-break** | Equal scores are broken **at random**. Not deterministically, not by load. |
| **Feasibility** | Requests fitted against Allocatable. Booked capacity — the limit is the kubelet's business, after placement. |
| **`Pending`** | A state, not an error. Nothing times out, nothing retries with looser rules, nothing gives up. |
| **Scheduled once** | A Pod is never rescheduled to a different node. It is replaced, with a new UID. |
| **Node labels** | Same selector mechanism as Chapter 4, pointed the other way: the Pod selects nodes. |
| **`nodeSelector`** | An AND of exact label matches. Blunt, readable, hard. |
| **Node affinity** | Same idea, richer operators (`In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt`, `Lt`), plus a soft mode. `Gt` and `Lt` are node-affinity-only. |
| **`IgnoredDuringExecution`** | A node's labels changing after binding does not move the Pod. |
| **Taints** | Live on the **node**. A refusal. Three effects. |
| **Tolerations** | Live on the **Pod**. An exemption from the refusal. They permit; they never attract. |
| **Toleration matching** | Same key, same effect, plus `Equal`+value or `Exists`. Empty key wildcards the key (and requires `Exists`); empty effect wildcards the effect. Untolerated taints still apply. |
| **Effect timing** | Only `NoExecute` touches Pods that are already running. `tolerationSeconds` buys a tolerating Pod a fixed stay. |
| **Dedicated nodes** | Taint to exclude, label + affinity to attract. Both. Always. |
| **Inter-Pod rules** | Constrain a Pod against the labels of Pods already placed, within a topology domain. |
| **`topologyKey`** | The node label whose values define the domain boundaries. It's a variable, not "the node." |
| **Topology spread** | The purpose-built mechanism for even distribution. `DoNotSchedule` filters; `ScheduleAnyway` scores. |
| **`nodeName`** | Bypasses the scheduler. Overrules everything. Fails instead of waiting. |
| **Predicates / Priorities** | Older names for filtering and scoring. |
| **The whole chapter** | Every mechanism is a filter or a score. `nodeName` is neither — it deletes the choice. |

---

## The Voyage Ahead

You can now say where a Pod should go, where it must not go, and what it should be near. What you cannot yet say is anything about the machine itself.

You have no way to take a node out of service before you reboot it. No way to stop one team booking the entire cluster's memory with requests they'll never use. No idea which versions of which components are allowed to disagree with each other, or what happens when they do. And no vocabulary for the three gates every request passes through on its way into the API server — which is the same API server this whole chapter has been quietly writing to.

There's a clue already in your hands. In §4 you met a built-in taint called `node.kubernetes.io/unschedulable`, sitting in the family table with a `NoSchedule` effect, and it wasn't put there by a failing disk or an exhausted process table. Marking a node unschedulable is something an administrator does on purpose — it stops the scheduler placing new Pods there without disturbing what's already running, and it is the standard preparatory step before a reboot or other maintenance [source: k8s-docs-nodes-2026-08-23]. The command that does it, the command that clears the node out afterwards, and everything else in the `kubectl` surface that a cluster administrator actually uses — that's Chapter 8, and it's the last chapter of Part II.

Chapter 8 is where the rules you've been learning turn into consequences.

---

🏆 **Safe Harbor**

You have finished the hardest five points in Part II. Scheduling is the material that most study guides present as a catalogue of six unrelated features, and you have it as one pipeline with two slots.

The next time you see a Pod stuck in `Pending`, you will not wonder whether something is broken. You will ask which filter emptied the list, and that is the question a practitioner asks.

🗺️ → 🌊 → 🌅 · **Part II · Chapter 7.** One chapter left before Part III.

> *"You cannot move a berth once it is assigned. You can only be careful about what you said before it was."*

<!-- AUTHOR-REVIEW: outline Open Question #1 — chapter-02 line 807 carries *[cross-bearing: see Ch 7 §3 — node selection, tolerations, and accounting for overhead]*. Those three topics land in §3, §4 and §2 respectively, so the "§3" is partially wrong. This draft honors the chapter-05 §2 pin exactly and does not attempt to edit shipped Chapter 2 text. Recommended fix remains the one-token deletion of "§3" from that pointer, matching the two other unnumbered Chapter 7 pointers. Not actionable from inside this chapter. -->

<!-- AUTHOR-REVIEW: outline Open Question #11 — this draft back-bears to Ch 6 §1 (Deployments/ReplicaSets) and Ch 6 §7 (DaemonSets) using the ch-06 outline's planned section numbering, since chapter-06's shipped file is incomplete and its final numbering is not verifiable. The curriculum-alignment stage confirmed on disk that Book-KCNA ships chapters 01–05 only, so §4's DaemonSet callback and the §5 back-bearing both point at unshipped text. Sequencing decision for the author. Re-verify both pointers after the ch-06 harvest is re-run. -->