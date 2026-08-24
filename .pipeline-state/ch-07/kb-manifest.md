I have everything I need. Two structural findings are verified on disk before the manifest content.

```markdown
# Knowledge-Base Manifest — KCNA Chapter 7

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 7 — Assigning the Berth
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-24

**Inputs consulted:** the finalized chapter; `ch-07/integration.md`; `ch-07/outline.md` frontmatter (`kb_tags` — 44 concepts, 4 commands, `objectives: ["D1.3"]`); `book-outline/retrieval-architecture.md`; `sources/cncf-kcna-curriculum-pdf-2026-08-23.md`; shipped `chapter-01` … `chapter-06`; the prior manifests for `ch-01` … `ch-07`; `certcomp/pipeline/stages.py`.

---

## Two structural findings, both verified on disk

**1. ⚑ The `=== WRITE` / `=== APPEND` blocks are inert. Nothing below reaches disk without a manual step.**

I checked rather than inheriting this from the four prior manifests that assert it. `stages.py:228-229` defines stage 14 with exactly one output, `{ch}/kb-manifest.md` — the orchestrator captures stdout to that path and does nothing else. A repo-wide search for `=== WRITE` returns **one** file: `pipeline/prompts/14_knowledge_base_update.md`, the prompt asking for the blocks. No parser consumes them.

`C:\dev\lodestar\Book-KCNA\knowledge-base\` **does not exist.** No `glossary.md`, no `concepts/`, no `objective-coverage.md`, no `retrieval-log.md`. Every "append" below is therefore an append to a file that has never been created, and every row of the book's knowledge base for Chapters 1–7 is currently sitting unapplied inside seven manifests.

**2. ✅ Correction to the prior ch-07 manifest: the replay set is now complete.**

That manifest (11:05) recorded "Chapters 2 and 6 have no manifest to replay." Both have since been produced — `ch-02/kb-manifest.md` at 15:24 and `ch-06/kb-manifest.md` at 15:01, today. All seven chapters now have one.

**Replay order is load-bearing** (later chapters emit appends that assume earlier rows exist, and two shards below are *updates* to shards ch-04 and ch-05 propose):

> ch-01 → ch-02 → ch-03 → ch-04 → ch-05 → ch-06 → ch-07

**3. ⚑ Inherited caveat.** The finalized chapter still carries the integration report's three ship-blocking findings — E1 (the Safe Harbor strawman), T1 (23 British spellings), C2 (two stale AUTHOR-REVIEW comments). None of them touch a definition I inherit below, with one exception I've flagged: the voice-exemplar section refuses to nominate the Safe Harbor passage while E1 stands.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**60 terms contributed — 49 defined · 6 partial · 5 gap-only.**

Two counts are in play and they are not in conflict. Stage 13's coverage table flags **11** terms with an open definitional gap — what a reader could be graded on without ever having been told what it means. Skill Part 16 requires the book glossary to carry *all* technical terms introduced (100-term floor). Chapters 4 and 5 set the precedent of contributing the full set. Both are below, separated.

Appended as a Chapter 7 section rather than merged into a single A–Z. Re-transcribing prior chapters' prose to preserve one alphabet is exactly the drift Rule 5 forbids; book assembly merges alphabets mechanically.

### Priority rows — the 11 gaps Stage 13 flagged

Rule 5 forbids me inventing wording. Where the chapter defines nothing, the row records what the chapter *does* say and names the gap rather than laundering a paraphrase into canon.

| Term | Definition (from chapter) | Status |
|---|---|---|
| **data locality** | Named only, in §1's list of factors a scheduling decision takes into account. No definition given. | ⚑ **gap** — no cached snapshot defines it either |
| **inter-workload interference** | Named only, same list. No definition given. | ⚑ **gap** |
| **node `Capacity`** | "A node's status reports both **Capacity** and **Allocatable**." The relationship between them is explicitly deferred: "What makes the two differ, and how it's configured, is Chapter 8's material." | ⚑ **gap** — cross-ref Ch 8 |
| **Pod overhead** | "a Pod running under a sandboxed runtime doesn't consume only what its containers asked for, and the overhead exists so the scheduler's arithmetic accounts for the runtime's own cost rather than pretending it's free." | **partial** — mechanism deliberately withheld; chapter records gap **G-7F**, fetch = `/concepts/scheduling-eviction/pod-overhead/` |
| **`PriorityClass`** | Named only: "they're configured with a `PriorityClass`". *Preemption* is defined — "If a Pod cannot be scheduled, the scheduler tries to preempt — evict — lower priority Pods to make scheduling of the pending Pod possible." | ⚑ **gap — escalated, see G4** |
| **NodeRestriction admission plugin** | "The NodeRestriction admission plugin prevents the kubelet from setting labels with a `node-restriction.kubernetes.io/` prefix." | **partial** — behaviour defined; "admission plugin" as a *category* undefined until Ch 8 |
| **`node.cloudprovider.kubernetes.io/uninitialized`** | "added when the kubelet starts with an external cloud provider" | **partial** — trigger stated, effect not |
| **node controller / node lifecycle controller** | §4 uses both: "the control plane, using the node controller, automatically creates taints…" and "the node lifecycle controller evicts them." Neither is defined here. Ch 3 defines a third casing: "the **Node** controller (noticing and responding when nodes go down)". | ⚑ **gap — three casings, one referent; see G7/T2** |
| **`OutOfmemory` / `OutOfcpu`** | "If the named node does not have the resources to accommodate the Pod, the Pod will fail and its reason will indicate why, for example OutOfmemory or OutOfcpu." | **partial — escalated, see G10** |
| **`schedulerName` / custom scheduler** | "`kube-scheduler` is designed so that, if you want and need to, you can write your own scheduling component and use that instead"; Pods name their scheduler via `.spec.template.spec.schedulerName`. | **partial** — function stated, nothing more |
| **`QueueSort` / `Reserve` / `Permit`** | Named in §6's list of profile plugin stages. Only `Filter`, `Score` and `Bind` are explained. | ⚑ **gap** — fetch = `/reference/scheduling/config/` |

### Two of the eleven need an author decision, not just a glossary row

**G4 — `PriorityClass` and preemption have no owner anywhere in the book.** §2 names both and correctly declares them out of scope "so that nothing in this chapter reads as a lie later." I searched `chapter-01` … `chapter-06` **and** `chapter-lineup.md`: `priorityclass` and `preempt` return **zero** hits in all seven. No chapter owns them. A glossary row is the floor; the real question is whether Ch 8 should pick them up.

**G10 — `OutOfmemory` will be confused with `OOMKilled`, and I can now say the confusion is worse than Stage 13 stated.** The integration report says "ch05 already taught the runtime one." It doesn't — `chapter-05:969` and `:1027` both *name* `OOMKilled` and forward-defer it to **Ch 13 §4**, which is unwritten. So Chapter 7 introduces `OutOfmemory` (a scheduling-admission failure) into a book where the near-identical `OOMKilled` (a runtime kill) is named twice and defined nowhere. The glossary row below states the contrast explicitly; it is currently the only place in the book that does.

### Full Part-16 coverage — the 49 defined rows

Verbatim from the chapter. Full text in the append block; representative rows:

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **feasible node** | "The nodes that meet a Pod's scheduling requirements are called **feasible nodes**." | Ch 7 §1 |
| **filtering** | "finds the set of nodes where it is feasible to schedule the Pod. After this step the node list contains any suitable nodes — often more than one. If the list is empty, that Pod isn't yet schedulable." | Ch 7 §1 |
| **scoring** | "the scheduler assigns a score to each node that survived filtering, based on the active scoring rules, and then assigns the Pod to the node with the highest ranking." | Ch 7 §1 |
| **binding** ★ | "The scheduler notifies the API server about its decision, and *that* is what the word binding names." Concretely, from §6: the scheduler "binds the Pod to the target host by setting the `.spec.nodeName` field." | Ch 7 §1, §6 — **closes Ch 3's reservation** |
| **random tie-break** | "If there is more than one node with equal scores, `kube-scheduler` selects one of them **at random**." | Ch 7 §1 |
| **`Allocatable`** | "'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods"; "the scheduler treats 'Allocatable' as the available `capacity` for pods." The scheduler does not over-subscribe it. | Ch 7 §2 |
| **taint** | Lives on the **node**. "One or more taints are applied to a node; this marks that the node should not accept any Pods that do not tolerate the taints." | Ch 7 §4 |
| **toleration** | Lives on the **Pod**. "Tolerations are applied to Pods, and they allow the scheduler to schedule Pods with matching taints." ⚠ "Tolerations allow scheduling but don't guarantee scheduling." | Ch 7 §4 |
| **`topologyKey`** | "the key for the node label that the system uses to denote the domain." Nodes with that key and identical values are in the same topology. | Ch 7 §5 |
| **`nodeName`** | "if it is not empty, the scheduler ignores the Pod" and the kubelet on the named node tries to place it. "Overrules using `nodeSelector` or affinity and anti-affinity rules." | Ch 7 §6 |
| *(39 further rows in the append block)* | | |

---

## Concept shards at `Book-KCNA/knowledge-base/concepts/`

### Created — 13 shards (≥200 words of chapter treatment each)

`scheduling.md` · `feasible-node.md` · `pending-pod.md` · `nodeselector.md` · `node-affinity.md` · `taint.md` · `toleration.md` · `built-in-node-condition-taints.md` · `inter-pod-affinity.md` · `topology-domain.md` · `topology-spread-constraints.md` · `nodename.md` · `predicates-priorities.md`

### ⚑ Rule 6 — one genuine collision, flagged loudly, NOT overwritten

**`resource-request.md` is claimed by two chapters with two different framings.**

- **ch-05's manifest proposes it**, and shipped `chapter-05:884` reads: *"So a request is a floor, not a ceiling. Exceeding your request on a node with spare capacity is normal, expected behavior, not a violation of anything. One number gets you a berth. The other keeps you inside it."*
- **ch-07 §2 reads:** *"A request is a **booking**. Not an estimate, not a hint, not a starting point for measurement. Once a Pod is placed, its requests are taken off the node's available balance and stay off, whether the container ever touches that memory or not."*

Read side by side these look like a contradiction, and a naïve Stage 14 would overwrite the ch-05 shard with the ch-07 wording. **That would be canon drift, and it would delete the true half.** They describe different actors: ch-05 describes the *kubelet's* runtime tolerance of a container that exceeds its request; ch-07 describes the *scheduler's* accounting, which never sees runtime usage at all. Chapter 7 resolves it in its own prose — "A node can be busy and empty at the same time, and only one of those two states is the scheduler's business."

**Action: `resource-request.md` is UPDATED, not replaced.** The shard below carries both framings under an explicit "two actors" heading, with ch-05's sentence preserved verbatim. Flagged here for author review because it is the one place in the book where two chapters' canonical sentences about the same object appear to disagree.

### Updated — 5 shards proposed by earlier chapters that Chapter 7 extends

| Shard | Proposed by | What Ch 7 adds | Contradiction? |
|---|---|---|---|
| `resource-request.md` | **ch-05** | The scheduler-side accounting: a request is booked at placement whether or not used | ⚑ **apparent — reconciled above, do not overwrite** |
| `label-selector.md` | ch-04 | **Direction inversion** — every prior use was an object selecting Pods; §3 is a Pod selecting nodes | no — extension |
| `control-loop.md` | ch-03, ch-04 | §7: the scheduler watches for unbound Pods and acts on the difference — "another instance of it, wearing a specialised hat" | no — extension |
| `pod-lifetime.md` | ch-05 | §1 reinforces scheduled-once under a *new* motivation (a better node appears, not a node failure) | no — reinforcement |
| `runtimeclass.md` | ch-02 | Discharges both Ch 2 promises: the `nodeSelector` half (§3) and the overhead half (§2, partial) | no — promise paid |

`pod-phase.md` (ch-05) also gains a Chapter 7 note that `Pending` covers time waiting to be scheduled, and is a state rather than an error. Recorded as a one-line cross-reference rather than a shard rewrite.

---

## Voice-exemplar candidates nominated

Nominations only. Not written to `voice-exemplars.md` — the author ratifies exemplars explicitly (Rule 1).

| Function | Excerpt | Recommendation |
|---|---|---|
| **stakes / chapter-opening** | "The machine a Pod lands on is the machine it dies on. Every label, every affinity rule, every taint in this chapter exists for one reason: that decision is irreversible, and you get exactly one chance to influence it." | **strong** — the seasoned-navigator register at full strength; stakes without inflation |
| **☀️ Zenith** | "Every mechanism in this chapter plugs into one of exactly two slots… Six vocabularies. Two slots. That's the chapter." | **strong** — synthesis compression; the payoff lands because four earlier sections planted the required/preferred pair |
| **— Dead Reckoning** | "Here the metaphors run out. Four rules, no narrative, stated flat." + the toleration-matching block | **strong** — the cleanest instance of the marker's actual function in the book so far: it *announces* the register change rather than just switching |
| **Logbook Entry** | The eight-GPU-nodes story, ending "Keeping a berth clear and being steered into it are two different acts, and only one of them had been performed." | **strong** — composite, attributed to nobody, no invented statistic; illustrates a mechanism instead of manufacturing dread |
| **desirable difficulty** | "⚠ **This one is intentionally hard, and the intuitive answer is wrong.** Struggle is the point — missing it is expected and is exactly what makes the correct answer stick." | **moderate** — textbook skill Part 10B framing; slightly more explicit than the brand usually is |
| **wry beat, subject-dignity compliant** | "If you proposed one of the clever answers in Soundings question 2, you were in good company and you were wrong, and being wrong first is exactly why this will stick." | **moderate** — humour aimed squarely at the practitioner's own experience, which is the guardrail |
| **🏆 Safe Harbor** | "Scheduling is the material that most study guides present as a catalogue of six unrelated features…" | ⚑ **DO NOT NOMINATE while E1 stands.** This is the passage the integration report fails on skill Part 14 guardrail #3. Re-nominate only after the strawman clause is replaced. |

---

## Objective coverage log

`D1.3` = the third competency under CNCF domain **D1, Kubernetes Fundamentals (44%)** — "Kubernetes Core Concepts; Administration; **Scheduling**; Containerization" (`cncf-kcna-curriculum-pdf-2026-08-23.md:13`). This independently confirms both figures the chapter's own metadata AUTHOR-REVIEW asked to be verified: the **44%** domain weight and the competency name **Scheduling**. That open item can be closed.

CNCF publishes domain weights but not competency weights, so the chapter's ~5% remains an authored allocation and is disclosed as such in front matter.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.3 — Scheduling | Chapter 7 | deep | — |

All seven sections carry `objectives: ["D1.3"]`. Chapter 7 is the sole owner of this competency; no earlier chapter claims it and none is scheduled to revisit it, which is exactly why B3 flagged scheduling as one of the two "thin" areas needing a named retrieval anchor later in the book.

---

## Retrieval-practice ledger

Seven tagged items, all verified against shipped text. 7 of 33 graded items = **21%**, inside B3's 20–25% band for Chapter 7.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| request vs limit — which one the scheduler reads | ch 5 §8 | ch 7 — ☆ Bearings #1 Q3 |
| ReplicaSet creates a Pod with nowhere to run | ch 6 §2 | ch 7 — ☆ Bearings #1 Q5 |
| label selectors as the universal join | ch 4 §5 | ch 7 — ☆ Bearings #2 Q1 |
| a Pod is scheduled once, never rescheduled | ch 5 §4 | ch 7 — Practice Q5 |
| scheduler records / kubelet acts | ch 3 §2 | ch 7 — Practice Q6 |
| set-based label selector operators | ch 4 §5 | ch 7 — Practice Q12 |
| DaemonSet one-per-node distribution | ch 6 §7 | ch 7 — Practice Q15 |

Sources reach back to Chapters 3, 4, 5 and 6 — four distinct chapters, furthest four back. B3's "≥4 chapters back" floor doesn't bind until Ch 8 but is met anyway. Soundings are excluded from the budget per B3 decision #2 while still doing retrieval work (Q3, Q4, Q6 draw on Ch 5 and Ch 6).

**⚑ Note for the author's file, not a defect in this chapter.** `book-outline/retrieval-architecture.md` is not the B3 document. I read it: it is a permission-failure message ("The write to `Book-KCNA` is blocked… I just can't put it on disk") followed by a prose summary of what B3 concluded. The per-chapter retrieval schedule was never written to disk. The surviving summary was sufficient to audit Chapter 7 — it states the spacing targets, the three structural decisions and the four never-retrieve items — but **Ch 8's "≥4 chapters back" floor has no artifact to check against.** The ledger above is the first durable record of what has actually been retrieved, which is part of why it matters that it reach disk.
```

Now the write intentions.

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

## Chapter 7 — Assigning the Berth (Scheduling · D1.3)

> Definitions inherited verbatim from Chapter 7 per Stage 14 Rule 5. Rows marked
> ⚑ carry an open definitional gap: the chapter names the term but does not
> define it. Do not paraphrase these into definitions — either fetch the named
> source or have the author supply wording.

### The decision (§1)

**Feasible node** — "The nodes that meet a Pod's scheduling requirements are called feasible nodes." (Chapter 7 §1)

**Filtering** — The first of the scheduler's two steps. "Finds the set of nodes where it is feasible to schedule the Pod. After this step the node list contains any suitable nodes — often more than one. If the list is empty, that Pod isn't yet schedulable." (Chapter 7 §1)

**Scoring** — The second step. "The scheduler assigns a score to each node that survived filtering, based on the active scoring rules, and then assigns the Pod to the node with the highest ranking." (Chapter 7 §1)

**Binding** — "The scheduler notifies the API server about its decision, and *that* is what the word binding names." Concretely, the default scheduler "binds the Pod to the target host by setting the `.spec.nodeName` field." Not an act of starting anything. (Chapter 7 §1, §6)

**Random tie-break** — "If there is more than one node with equal scores, kube-scheduler selects one of them at random." Not lowest hostname, not least-loaded, not round-robin. (Chapter 7 §1)

**kube-scheduler** — "A scheduler watches for newly created Pods that have no node assigned; for every such Pod it discovers, it becomes responsible for finding a node for that Pod to run on." Runs as part of the control plane. (Chapter 7 §1)

**Scheduling factors** — The documented list a scheduling decision takes into account: "individual and collective resource requirements, hardware / software / policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and so on," with deadlines named alongside them in the architecture overview. (Chapter 7 §1)

⚑ **Data locality** — Named in Chapter 7 §1's factors list. No definition given in-chapter, and no cached snapshot defines it. GAP.

⚑ **Inter-workload interference** — Named in Chapter 7 §1's factors list. No definition given in-chapter, and no cached snapshot defines it. GAP.

**Scheduled once per lifetime** — "Pods are created, assigned a unique ID, and scheduled to run on nodes where they remain until termination or deletion. A Pod is never 'rescheduled' to a different node; instead, it is replaced by a new, near-identical Pod with a different UID." (Chapter 7 §1; established Chapter 5 §4)

### Feasibility (§2)

**`PodFitsResources`** — The documentation's own example of a filter: "checks whether a candidate node has enough available resources to meet a Pod's specific resource requests." Named as *an example* of a filter, not the only one. (Chapter 7 §2)

**Request (as scheduling input)** — "When you specify a resource request for a container, the kube-scheduler uses that information to decide which node to place the Pod on, and the kubelet reserves at least the request amount of that resource specifically for that container to use." A request is a booking: "Once a Pod is placed, its requests are taken off the node's available balance and stay off, whether the container ever touches that memory or not." (Chapter 7 §2) — See also Chapter 5 §8, which states the complementary runtime rule: "a request is a floor, not a ceiling." Both are true; they describe different actors. See `concepts/resource-request.md`.

**Allocatable** — "'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods," and "the scheduler treats 'Allocatable' as the available capacity for pods." The scheduler does not over-subscribe Allocatable. (Chapter 7 §2)

⚑ **Capacity (node)** — "A node's status reports both Capacity and Allocatable." The relationship between the two is explicitly deferred: "What makes the two differ, and how it's configured, is Chapter 8's material." GAP until Chapter 8. (Chapter 7 §2)

⚑ **Pod overhead** — "A Pod running under a sandboxed runtime doesn't consume only what its containers asked for, and the overhead exists so the scheduler's arithmetic accounts for the runtime's own cost rather than pretending it's free." PARTIAL — the mechanism (how overhead enters the Pod's effective request) is deliberately withheld because no cached snapshot states it. Chapter records this as gap G-7F; fetch `kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/`. (Chapter 7 §2)

**Preemption** — "If a Pod cannot be scheduled, the scheduler tries to preempt — evict — lower priority Pods to make scheduling of the pending Pod possible." Out of scope for KCNA; registered so nothing in the chapter reads as a lie later. (Chapter 7 §2)

⚑ **`PriorityClass`** — Named only: priority and preemption "are configured with a `PriorityClass`." GAP — and note that no chapter in the book or the chapter lineup owns this object. Author decision required on whether Chapter 8 should adopt it. (Chapter 7 §2)

**`Pending` (as a scheduling state)** — "If none of the nodes are suitable, the Pod remains unscheduled until the scheduler is able to place it." Its phase is `Pending`, which covers "time a Pod spends waiting to be scheduled." A state, not an error: nothing errors, nothing times out, nothing retries with looser constraints. (Chapter 7 §2; phase established Chapter 5 §5)

### Asking for a node (§3)

**Node labels** — Nodes have labels; you can attach them manually, and Kubernetes populates a standard set on all nodes in a cluster. (Chapter 7 §3)

**Standard node labels** — The kubelet supplies `kubernetes.io/hostname` (populated with the node's hostname), `kubernetes.io/os` and `kubernetes.io/arch`. `topology.kubernetes.io/zone` and `topology.kubernetes.io/region` are populated by the kubelet **or** the cloud-controller-manager, so they may be absent on a cluster with no cloud provider. (Chapter 7 §3)

⚑ **NodeRestriction admission plugin** — "The NodeRestriction admission plugin prevents the kubelet from setting labels with a `node-restriction.kubernetes.io/` prefix." PARTIAL — the behaviour is defined; "admission plugin" as a category is undefined until Chapter 8. (Chapter 7 §3)

**`nodeSelector`** — "The simplest recommended form of node selection constraint. You add the `nodeSelector` field to your Pod specification and name the node labels you want the target node to have, and Kubernetes only schedules the Pod onto nodes that have each of the labels you specify." An AND of exact matches. Each, not any. (Chapter 7 §3)

**Node affinity** — "Functions like the `nodeSelector` field but is more expressive and allows you to specify soft rules." Adds a richer operator set and two hardness levels. (Chapter 7 §3)

**Affinity operators** — `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt` and `Lt`. `Gt` and `Lt` are node-affinity-only and are not available for `podAffinity`. (Chapter 7 §3, §5)

**`requiredDuringSchedulingIgnoredDuringExecution`** — "The scheduler can't schedule the Pod unless the rule is met." (Chapter 7 §3)

**`preferredDuringSchedulingIgnoredDuringExecution`** — "The scheduler tries to find a node that meets the rule, but if a matching node is not available, it still schedules the Pod." Preferred rules carry a weight and feed the node's score. (Chapter 7 §3)

**`IgnoredDuringExecution`** — "If the node's labels change after Kubernetes schedules the Pod, the Pod continues to run." Decodes as: required when scheduling, ignored once running. (Chapter 7 §3)

**`nodeSelectorTerms` / `matchExpressions` combination** — Multiple terms in `nodeSelectorTerms` are ORed: the Pod can be scheduled if one of the terms is satisfied. Multiple expressions in a single `matchExpressions` are ANDed: the Pod can be scheduled only if all the expressions are satisfied. (Chapter 7 §3)

### Refusal (§4)

**Taint** — Lives on the **node**. "One or more taints are applied to a node; this marks that the node should not accept any Pods that do not tolerate the taints." Taints "allow a node to repel a set of pods." (Chapter 7 §4)

**Toleration** — Lives on the **Pod**. "Tolerations are applied to Pods, and they allow the scheduler to schedule Pods with matching taints." Critically: "Tolerations allow scheduling but don't guarantee scheduling: the scheduler also evaluates other parameters as part of its function." A toleration removes a veto; it never attracts. (Chapter 7 §4)

**`NoSchedule`** — "No new Pods will be scheduled on the tainted node unless they have a matching toleration. Pods currently running on the node are not evicted." (Chapter 7 §4)

**`PreferNoSchedule`** — "The soft version of `NoSchedule`. The control plane will try to avoid placing a Pod that does not tolerate the taint on the node, but it is not guaranteed." (Chapter 7 §4)

**`NoExecute`** — The only effect that touches Pods already on the node. "Pods that do not tolerate the taint are evicted immediately. Pods that tolerate the taint without specifying `tolerationSeconds` remain bound forever. Pods that tolerate the taint with a specified `tolerationSeconds` remain bound for that long, after which the node lifecycle controller evicts them." (Chapter 7 §4)

**`tolerationSeconds`** — Meaningful only with `NoExecute`. Kubernetes automatically adds a toleration for `node.kubernetes.io/not-ready` and `node.kubernetes.io/unreachable` with `tolerationSeconds=300`, unless you or a controller set those tolerations explicitly. (Chapter 7 §4)

**Taint/toleration matching** — "A toleration matches a taint when the keys are the same and the effects are the same, and one of two operator conditions holds. If the operator is `Exists`, no value should be specified. If the operator is `Equal`, the values must be equal." Two wildcards modify this: an empty key requires `Exists` and matches all keys and values (the effect must still match); an empty effect matches all effects with the given key. (Chapter 7 §4)

**Multiple taints procedure** — "Start with all of a node's taints, then ignore the ones for which the pod has a matching toleration; the remaining un-ignored taints have the indicated effects on the pod." Tolerating three of four taints does not get you onto the node. (Chapter 7 §4)

**Built-in node-condition taints** — Created automatically by the control plane via the node controller. "The scheduler checks taints, not node conditions, when it makes scheduling decisions." The family: `node.kubernetes.io/not-ready` (NoExecute), `unreachable` (NoExecute), `disk-pressure` (NoSchedule), `memory-pressure` (NoSchedule), `pid-pressure` (NoSchedule), `unschedulable` (NoSchedule), `network-unavailable` (NoSchedule). (Chapter 7 §4)

⚑ **`node.cloudprovider.kubernetes.io/uninitialized`** — "Added when the kubelet starts with an external cloud provider." PARTIAL — trigger stated, effect not stated. (Chapter 7 §4)

**`node.kubernetes.io/unschedulable`** — "Marking a node unschedulable is a deliberate administrative act: it prevents the scheduler from placing new Pods onto that node but does not affect the Pods already there, and it is the preparatory step before a reboot or other maintenance." (Chapter 7 §4)

**DaemonSet automatic tolerations** — "The DaemonSet controller automatically adds tolerations for the built-in condition taints" to the Pods it creates — six of the seven unconditionally, with `network-unavailable` added only for DaemonSet Pods that request host networking. The `NoExecute` tolerations for `not-ready` and `unreachable` carry no `tolerationSeconds`, so DaemonSet Pods on such nodes are not evicted. (Chapter 7 §4)

⚑ **Node controller / node lifecycle controller** — Chapter 7 §4 uses both names without defining either. Chapter 3 defines a third casing: "the Node controller (noticing and responding when nodes go down)," one of the logical controllers inside kube-controller-manager. GAP — three casings, one referent; needs a single reconciling sentence.

**Dedicated nodes (the two-mechanism pattern)** — To dedicate nodes to a group *and* ensure that group only uses them: taint the nodes to exclude everyone else, *and* "add a label similar to the taint to the same set of nodes… and the admission controller should additionally add a node affinity to require that the pods can only schedule onto nodes labeled with `dedicated=groupName`." Taints exclude; affinity attracts; a dedicated-node setup needs both. (Chapter 7 §4)

### Relative placement (§5)

**Inter-Pod affinity** — Constrains Pods against "labels on other Pods" — e.g. "only schedule on nodes in the same zone as a Pod with this label." Attracts: schedule this Pod where a Pod carrying that label already is. (Chapter 7 §5)

**Inter-Pod anti-affinity** — Repels: do not schedule this Pod where a Pod carrying that label already is. The availability tool. In `requiredDuringSchedulingIgnoredDuringExecution` mode, "only a single Pod can be scheduled into a single topology domain"; in `preferred` mode "you lose the ability to enforce the constraint." (Chapter 7 §5)

**Topology domain** — The unit an inter-Pod rule is evaluated within. "Nodes that have a label with that key and identical values are considered to be in the same topology." A variable, not a synonym for "node." (Chapter 7 §5)

**`topologyKey`** — "The key for the node label that the system uses to denote the domain." (Chapter 7 §5)

**Topology spread constraints** — "You can use topology spread constraints to control how Pods are spread across your cluster among failure-domains such as regions, zones, nodes, and other user-defined topology domains. This can help to achieve high availability as well as efficient resource utilization." (Chapter 7 §5)

**`maxSkew`** — "Describes the degree to which Pods may be unevenly distributed. Must be specified and must be greater than zero." (Chapter 7 §5)

**`whenUnsatisfiable`** — "`DoNotSchedule` (the default) tells the scheduler not to schedule the Pod; `ScheduleAnyway` tells the scheduler to still schedule it while prioritizing nodes that minimize the skew." (Chapter 7 §5)

**`labelSelector` (spread-constraint field)** — "Pods matching this selector are counted to determine the number of Pods in their corresponding topology domain." (Chapter 7 §5)

**Spread-constraint limitation** — "There's no guarantee that the constraints remain satisfied when Pods are removed. For example, scaling down a Deployment may result in imbalanced Pods distribution." Scheduling-time constraints describe a decision, not a standing invariant. (Chapter 7 §5)

**Inter-Pod rule cost** — "Inter-pod affinity and anti-affinity require substantial amounts of processing which can slow down scheduling in large clusters significantly. We do not recommend using them in clusters larger than several hundred nodes." (Chapter 7 §5)

### Opting out (§6)

**`nodeName`** — "A more direct form of node selection than affinity or `nodeSelector`." If not empty, "the scheduler ignores the Pod" and the kubelet on the named node tries to place the Pod there. "Using `nodeName` overrules using `nodeSelector` or affinity and anti-affinity rules." It is the field binding writes to — setting it by hand means filling in the scheduler's answer before it was asked the question. (Chapter 7 §6)

**`nodeName` failure modes** — "If the named node does not exist, the Pod will not run, and in some cases may be automatically deleted. If the named node does not have the resources to accommodate the Pod, the Pod will fail and its reason will indicate why, for example OutOfmemory or OutOfcpu. Node names in cloud environments are not always predictable or stable." (Chapter 7 §6)

⚑ **`OutOfmemory` / `OutOfcpu`** — Failure reasons on a Pod pinned with `nodeName` to a node that cannot fit it: "the Pod will fail and its reason will indicate why, for example OutOfmemory or OutOfcpu." PARTIAL, and **actively confusable**: these are *scheduling-admission* failures, distinct from `OOMKilled`, which is a *runtime* kill by the kubelet. `OOMKilled` is named at Chapter 5 §8 and forward-deferred to Chapter 13 §4, where it is not yet written. Until Chapter 13 ships, this row is the only place in the book that draws the contrast. (Chapter 7 §6)

⚑ **`schedulerName` / custom scheduler** — "kube-scheduler is designed so that, if you want and need to, you can write your own scheduling component and use that instead." Pods can name which scheduler should handle them; a DaemonSet exposes `.spec.template.spec.schedulerName`. PARTIAL — function stated, nothing more. (Chapter 7 §6)

**Scheduling Policies** — One of two documented ways to configure filtering and scoring: "Predicates for filtering, and Priorities for scoring." (Chapter 7 §6)

**Predicate** — "A filter — decides whether a node is feasible." The older name for filtering. (Chapter 7 §6)

**Priority** — "A score — ranks the nodes that survived filtering." The older name for scoring. (Chapter 7 §6)

**Scheduling Profiles** — "Plugins that implement different scheduling stages, including `QueueSort`, `Filter`, `Score`, `Bind`, `Reserve` and `Permit`. kube-scheduler can run different profiles." (Chapter 7 §6)

⚑ **`QueueSort` / `Reserve` / `Permit`** — Named in Chapter 7 §6's plugin-stage list; only `Filter`, `Score` and `Bind` are explained. GAP — fetch `kubernetes.io/docs/reference/scheduling/config/`. (Chapter 7 §6)

### Synthesis (§7)

**Filter-or-score taxonomy** — "Every mechanism in this chapter plugs into one of exactly two slots in §1's pipeline. It either removes nodes from consideration — a filter — or it changes the ranking of the nodes that survived — a score." Hard rules filter; soft rules score. `nodeName` is neither: it deletes the choice. NOTE — this synthesis is the chapter's organising frame and follows from documented behaviours by inference; no cached snapshot registers individual mechanisms against named scheduler stages. See the chapter's AUTHOR-REVIEW at §7. (Chapter 7 §7)

### Commands introduced

**`kubectl get nodes --show-labels`** — Lists nodes with their labels. (Chapter 7 §3)

**`kubectl label nodes <node> <key>=<value>`** — Attaches a label to a node. (Chapter 7 §3)

**`kubectl taint nodes <node> <key>=<value>:<EFFECT>`** — Applies a taint. The removal form is the same command with a trailing minus sign: `kubectl taint nodes node1 key1=value1:NoSchedule-`. (Chapter 7 §4)

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/scheduling.md ===
# Scheduling

**Introduced:** Chapter 7 (§1, §7) · **Objective:** D1.3 · **Status:** canonical

## The spine

`kube-scheduler` selects a node in a **2-step operation: filtering, then scoring**.

1. **Filter** — find the set of nodes where it is feasible to schedule the Pod. The survivors are the *feasible set*. If the list is empty, the Pod isn't yet schedulable.
2. **Score** — assign a score to each surviving node based on the active scoring rules; the Pod goes to the highest-ranked node.
3. **Bind** — notify the API server of the decision. Concretely, this is writing `.spec.nodeName`.

The scheduler's third arrow lands on the **API server**, not on the chosen node. Nothing in the scheduler ever touches a container. The kubelet on the chosen node starts the containers because it saw the recorded decision.

## Tie-break

Equal scores are broken **at random**. Not lowest hostname, not least-loaded, not round-robin. This is load-bearing conceptually: the scheduler is not trying to be optimal in a way you can reason about or predict, so influencing placement is never a matter of out-thinking the algorithm. It is a matter of *saying something* the algorithm is obliged to honour.

## The organising frame (§7)

Every placement mechanism is either a **filter** (removes nodes) or a **score** (re-ranks survivors).

| Filters | Scores |
|---|---|
| requests vs allocatable | preferred node affinity |
| `nodeSelector` | `PreferNoSchedule` |
| required node affinity | preferred inter-Pod rules |
| untolerated `NoSchedule` / `NoExecute` | `ScheduleAnyway` spread |
| required inter-Pod rules | other scoring plugins |
| `DoNotSchedule` spread | |

The recurring required/preferred pair — required vs preferred node affinity, `NoSchedule` vs `PreferNoSchedule`, required vs preferred inter-Pod rules, `DoNotSchedule` vs `ScheduleAnyway` — was never four distinctions. It is one: *is this a filter, or is this a score?*

`nodeName` fits neither slot. It deletes the decision.

**Diagnostic question:** is this a filter that excluded every node, or a score that ranked the wrong one first? A filter problem leaves a Pod `Pending` forever; a score problem puts the Pod somewhere you didn't want, immediately and silently.

⚑ **Sourcing note.** The mechanism-by-mechanism assignment above follows from documented behaviours by inference. No cached snapshot registers individual mechanisms against named scheduler stages. The fetch that would source it directly is `kubernetes.io/docs/reference/scheduling/config/`.

## Related

`[[feasible-node]]` · `[[pending-pod]]` · `[[predicates-priorities]]` · `[[nodename]]` · `[[control-loop]]` — §7 notes the scheduler watches for unbound Pods and acts on the difference, making it another instance of the control-loop shape.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/feasible-node.md ===
# Feasible node

**Introduced:** Chapter 7 §1–§2 · **Objective:** D1.3 · **Status:** canonical

"The nodes that meet a Pod's scheduling requirements are called **feasible nodes**."

Feasibility is not only about free memory. The documented factors: individual and collective resource requirements, hardware / software / policy constraints, affinity and anti-affinity specifications, data locality, inter-workload interference, and deadlines.

## The resource filter

`PodFitsResources` — the documentation's own **example** of a filter, not the only one — "checks whether a candidate node has enough available resources to meet a Pod's specific resource **requests**."

Three things it is not reading:
- Not **limits** — the kubelet enforces those on the running container, after placement.
- Not observed usage — a request is booked at placement whether or not it is used. See `[[resource-request]]`.
- Not raw machine RAM — the baseline is **Allocatable**, which the scheduler does not over-subscribe.

**The canonical arithmetic:** a node with 16 GiB allocatable, four Pods each having requested 4 GiB, monitoring reporting 2 GiB in use. A fifth Pod requesting 1 GiB does **not** schedule. Sixteen booked out of sixteen leaves zero. "A node can be busy and empty at the same time, and only one of those two states is the scheduler's business."

## Related

`[[scheduling]]` · `[[resource-request]]` · `[[pending-pod]]` · `[[taint]]` — an untolerated taint makes a node infeasible regardless of capacity.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pending-pod.md ===
# `Pending` — a state, not an error

**Introduced:** Chapter 5 §5 (phase); Chapter 7 §2 (scheduling sense) · **Objective:** D1.3

"If none of the nodes are suitable, the Pod remains unscheduled until the scheduler is able to place it." Its phase is `Pending`, which covers "time a Pod spends waiting to be scheduled."

## What does not happen

Nothing errors. Nothing times out. Nothing retries with different parameters or gives up. The Pod waits indefinitely, and the controller that created it has already done its part — from the controller's point of view its work is complete, because it created the Pod it was missing. A Pod can sit in `Pending` for a week and the cluster considers this an ordinary state of affairs.

No component is quietly retrying with looser constraints, and no timer converts it into a failure.

## The one exception

`nodeName` is the only placement failure in the chapter that is **not** `Pending`. Because setting it skips the feasibility check entirely, a Pod that doesn't fit **fails** — with a reason such as `OutOfmemory` or `OutOfcpu` — rather than waiting. See `[[nodename]]`.

## Structural note

An unschedulable Pod is a standing, machine-readable statement that the cluster is short of somewhere to put work. That is what cluster autoscalers watch for (Chapter 17).

Diagnosing *why* a Pod is `Pending` — `kubectl describe`, the event stream, the scheduler's own message — is Chapter 13.

## Related

`[[scheduling]]` · `[[feasible-node]]` · `[[pod-phase]]` · `[[nodename]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/nodeselector.md ===
# `nodeSelector`

**Introduced:** Chapter 7 §3 · **Objective:** D1.3

"The simplest recommended form of node selection constraint. You add the `nodeSelector` field to your Pod specification and name the node labels you want the target node to have, and **Kubernetes only schedules the Pod onto nodes that have each of the labels you specify**."

**Each. Not any.** An AND of exact matches, offering nothing else — no "one of these," no "anything except," no "greater than."

## Direction inversion

Every prior use of label selectors in this book was an object selecting a set of Pods (a Service selecting backends, a ReplicaSet selecting the Pods it owns). Here it is a **Pod selecting nodes**. Same mechanism, opposite direction. See `[[label-selector]]`.

## Hardness vs expressiveness are independent axes

`nodeSelector` and **required** node affinity fail identically: no matching node, no placement, Pod sits `Pending`. Node affinity does not sit on a single upgrade path from `nodeSelector` — it adds a second, independent axis (soft mode).

Reach for `nodeSelector` first. "A soft rule you didn't need is a rule someone will misread as a guarantee eighteen months from now."

## Related

`[[node-affinity]]` · `[[label-selector]]` · `[[nodename]]` — `nodeName` overrules `nodeSelector` entirely · `[[taint]]` — taints exclude, `nodeSelector` attracts; a dedicated-node setup needs both.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-affinity.md ===
# Node affinity

**Introduced:** Chapter 7 §3 · **Objective:** D1.3

"Functions like the `nodeSelector` field but is more expressive and allows you to specify soft rules."

## Two additions over `nodeSelector`

**1. A richer operator set:** `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt`, `Lt` — against `nodeSelector`'s single implicit "equals." (`Gt` and `Lt` are node-affinity-only; not available for `podAffinity`.)

**2. Two hardness levels:**
- `requiredDuringSchedulingIgnoredDuringExecution` — the scheduler **can't** schedule the Pod unless the rule is met. A **filter**.
- `preferredDuringSchedulingIgnoredDuringExecution` — the scheduler **tries**, but if no matching node is available it still schedules the Pod. Preferred rules carry a weight that feeds the node's score. A **score**.

## Decoding the field names

Read `requiredDuringSchedulingIgnoredDuringExecution` as two clauses joined at the seam: **required when scheduling, ignored once running.** Forty-six characters; six words of meaning. Every `…DuringScheduling…DuringExecution` name decomposes the same way — first half is what happens at placement, second half is what happens afterwards.

`IgnoredDuringExecution` means "if the node's labels change after Kubernetes schedules the Pod, the Pod continues to run." A Pod placed on a node labelled `disktype=ssd` is not evicted when someone strips that label off.

## Combination rules

- Multiple terms in `nodeSelectorTerms` are **ORed** — the Pod can be scheduled if one of the terms is satisfied.
- Multiple expressions in a single `matchExpressions` are **ANDed** — only if all the expressions are satisfied.

## Related

`[[nodeselector]]` · `[[inter-pod-affinity]]` · `[[scheduling]]` · `[[pod-lifetime]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/taint.md ===
# Taint

**Introduced:** Chapter 7 §4 · **Objective:** D1.3

Lives on the **node**. A refusal.

"Node affinity is a property of Pods that attracts them to a set of nodes (either as a preference or a hard requirement). Taints are the opposite — they allow a node to repel a set of pods."

"One or more taints are applied to a node; this marks that the node should not accept any Pods that do not tolerate the taints."

```
kubectl taint nodes node1 key1=value1:NoSchedule     # apply
kubectl taint nodes node1 key1=value1:NoSchedule-    # remove (trailing minus)
```

## The three effects — learn them by *when they act*

| Effect | Arriving Pod, no toleration | Arriving Pod, tolerating | Already-running Pod, no toleration |
|---|---|---|---|
| `NoSchedule` | not placed | may be placed | **unaffected** |
| `PreferNoSchedule` | avoided where possible | may be placed | **unaffected** |
| `NoExecute` | not placed | may be placed | **EVICTED** |

"May be placed" — never "is placed." The other filters and scores still run.

- **`NoSchedule`** — "no new Pods will be scheduled on the tainted node unless they have a matching toleration. Pods currently running on the node are not evicted."
- **`PreferNoSchedule`** — "the control plane will try to avoid placing a Pod that does not tolerate the taint on the node, but it is not guaranteed." Preferences lose; that is correct behaviour, not a bug.
- **`NoExecute`** — the only effect that touches Pods already on the node. Non-tolerating Pods are evicted immediately.

## Multiple taints

"Start with all of a node's taints, then ignore the ones for which the pod has a matching toleration; the remaining un-ignored taints have the indicated effects on the pod." Tolerating three of four taints does not get you onto the node.

## Related

`[[toleration]]` · `[[built-in-node-condition-taints]]` · `[[node-affinity]]` — taints exclude, affinity attracts; a dedicated-node setup needs **both**.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/toleration.md ===
# Toleration

**Introduced:** Chapter 7 §4 · **Objective:** D1.3

Lives on the **Pod**. An exemption from a node's refusal.

"Tolerations are applied to Pods, and they allow the scheduler to schedule Pods with matching taints."

## ★ The qualification that catches everyone

> "**Tolerations allow scheduling but don't guarantee scheduling**: the scheduler also evaluates other parameters as part of its function."

A toleration **removes a veto**. That is the entire extent of its power. It does not make a request, does not raise a node's score, does not reserve anything, and does not create capacity. A GPU workload with a matching toleration is now *allowed* onto the GPU nodes — along with being allowed onto every other node in the cluster, which it already was. Nothing has pulled it toward the GPU nodes.

**Taints exclude. Affinity attracts. A dedicated-node setup needs both** — taint the nodes to keep everyone else off, *and* label them plus a `nodeSelector`/required affinity to pull the right work on. The documentation prescribes exactly this pairing. Using only one of the two is the most common real-world mistake in this material.

## Matching rules

A toleration matches a taint when the **keys** are the same and the **effects** are the same, and one operator condition holds:

| Toleration | Matches | Notes |
|---|---|---|
| key + effect + `Equal` + value | same key, same effect, same value | exact match |
| key + effect + `Exists` | same key, same effect, **any value** | do not specify a value with `Exists` |
| **empty key** + `Exists` + effect | all taints with that effect, any key, any value | empty key *requires* `Exists` |
| key + `Exists` + **empty effect** | all effects for that key | effect wildcard |

## `tolerationSeconds`

Meaningful only with `NoExecute`. A tolerating Pod without it "remains bound forever"; with it, remains bound that long, "after which the node lifecycle controller evicts them." Kubernetes sets `tolerationSeconds=300` automatically for `not-ready` and `unreachable` unless you or a controller set those tolerations explicitly — the five-minute grace period that stops a briefly-unreachable node instantly shedding its work.

## Related

`[[taint]]` · `[[built-in-node-condition-taints]]` · `[[nodeselector]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/built-in-node-condition-taints.md ===
# Built-in node-condition taints

**Introduced:** Chapter 7 §4 · **Objective:** D1.3

"The control plane, using the node controller, automatically creates taints with a `NoSchedule` effect for node conditions. **The scheduler checks taints, not node conditions, when it makes scheduling decisions.** This ensures that node conditions don't directly affect scheduling."

Node health does not get a special channel into the scheduler. It is translated into the *same* mechanism you would use by hand.

| Taint key | Effect |
|---|---|
| `node.kubernetes.io/not-ready` | `NoExecute` |
| `node.kubernetes.io/unreachable` | `NoExecute` |
| `node.kubernetes.io/disk-pressure` | `NoSchedule` |
| `node.kubernetes.io/memory-pressure` | `NoSchedule` |
| `node.kubernetes.io/pid-pressure` | `NoSchedule` |
| `node.kubernetes.io/unschedulable` | `NoSchedule` |
| `node.kubernetes.io/network-unavailable` | `NoSchedule` |

Also `node.cloudprovider.kubernetes.io/uninitialized`, added when the kubelet starts with an external cloud provider. ⚑ Effect not stated in the cached corpus.

**Note:** the family carries *both* effects, not just `NoSchedule` — the `NoExecute` pair is added by the node controller when certain conditions are true, including the API server being unable to communicate with a node's kubelet.

## Two worth singling out

**`not-ready` / `unreachable`** — Kubernetes adds tolerations for these with `tolerationSeconds=300` unless set explicitly.

**`unschedulable`** — not a failure signal. "Marking a node unschedulable is a deliberate administrative act: it prevents the scheduler from placing new Pods onto that node but does not affect the Pods already there, and it is the preparatory step before a reboot or other maintenance." Chapter 8's opening move.

## Why the DaemonSet agent survives

"The DaemonSet controller automatically adds tolerations for the built-in condition taints" — six of the seven unconditionally, `network-unavailable` only for host-networking Pods. Because it sets the `unschedulable:NoSchedule` toleration, DaemonSet Pods run on nodes marked unschedulable; and its `NoExecute` tolerations carry no `tolerationSeconds`, so they are not evicted.

Your log-shipping agent still reporting from a memory-pressured node isn't privileged. It just tolerates almost everything.

## Related

`[[taint]]` · `[[toleration]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/inter-pod-affinity.md ===
# Inter-Pod affinity and anti-affinity

**Introduced:** Chapter 7 §5 · **Objective:** D1.3

Constrains a Pod against the labels of **other Pods** rather than properties of a node.

- **Pod affinity attracts** — schedule this Pod where a Pod carrying that label already is. For co-locating things that talk constantly.
- **Pod anti-affinity repels** — do not schedule this Pod where a Pod carrying that label already is. The availability tool.

Both come in the same `required` / `preferred` flavours as node affinity. Same machinery, different label set — except `Gt` and `Lt`, which are node-affinity-only.

## The gap it fills

Two replicas of a service, created so one machine failing doesn't take the service down, can both land on the same node. Nothing in resource or node-label constraints prevents this: the two Pods have identical requests, labels and affinity, because they came from one Deployment. Nothing distinguishes one node from another and nothing tells the scheduler the two Pods are related.

**Redundancy is a property of a set**, and inter-Pod rules are the only mechanism in the chapter that can express one. Every other rule is about one Pod and one node, evaluated in isolation.

## Evaluated against Pods already placed

Rules are evaluated against the labels of Pods that are **already placed**, within a topology domain defined by a node label. See `[[topology-domain]]` — the domain is the part people forget.

`podAntiAffinity` in `required` mode means only a single Pod can be scheduled into a single topology domain. In `preferred` mode "you lose the ability to enforce the constraint."

## Cost

"Inter-pod affinity and anti-affinity require substantial amounts of processing which can slow down scheduling in large clusters significantly. We do not recommend using them in clusters larger than several hundred nodes."

The reason is structural: to decide whether one node is feasible, the scheduler must know what is already running everywhere else in the domain — the answer for node-a depends on the contents of node-b. A different cost shape from "does this node have 4 GiB free."

## Related

`[[topology-domain]]` · `[[topology-spread-constraints]]` · `[[node-affinity]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/topology-domain.md ===
# Topology domain and `topologyKey`

**Introduced:** Chapter 7 §5 · **Objective:** D1.3 · **Difficulty:** 🟡

The domain is **not always "the node."**

You express it using a **`topologyKey`** — "the key for the node label that the system uses to denote the domain." Nodes that have a label with that key and identical values are considered to be in the same topology.

## The same rule means different things

Same cluster, six nodes, two zones, one rule: *"no two Pods labelled `app=web` in one domain."*

| `topologyKey` | A domain is | Domains | Placeable Pods |
|---|---|---|---|
| `kubernetes.io/hostname` | one node | 6 | up to 6 |
| `topology.kubernetes.io/zone` | one zone | 2 | at most 2 |

One label key changed. The rule's meaning changed with it — from "spread across machines" to "spread across failure zones," which is dramatically stricter and, with only two zones, dramatically more likely to leave Pods `Pending`.

**★ The domain is a variable, not a synonym for "node."**

## Availability caveat

`topology.kubernetes.io/zone` and `/region` are populated by the kubelet **or** the cloud-controller-manager — so they may be absent entirely on a single-machine learning cluster.

## Related

`[[inter-pod-affinity]]` · `[[topology-spread-constraints]]` · `[[pending-pod]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/topology-spread-constraints.md ===
# Topology spread constraints

**Introduced:** Chapter 7 §5 · **Objective:** D1.3

"You can use topology spread constraints to control how Pods are spread across your cluster among failure-domains such as regions, zones, nodes, and other user-defined topology domains." "This can help to achieve high availability as well as efficient resource utilization."

## Why not just anti-affinity

Anti-affinity says "not in the same domain." What people usually *want* is "distributed fairly evenly, and here's how much unevenness I'll tolerate." Different requirement, purpose-built mechanism.

If you find yourself writing anti-affinity rules and then reasoning about how many replicas you're allowed to have, you wanted spread constraints.

## The four fields

| Field | What it says |
|---|---|
| `topologyKey` | The key of node labels. Nodes with this key and identical values are in the same topology. |
| `labelSelector` | Pods matching this selector are counted to determine the number of Pods in their corresponding topology domain. |
| `maxSkew` | The degree to which Pods may be unevenly distributed. Must be specified and greater than zero. |
| `whenUnsatisfiable` | `DoNotSchedule` (default) — don't schedule the Pod. `ScheduleAnyway` — still schedule it while prioritizing nodes that minimize the skew. |

`whenUnsatisfiable` is the required/preferred pair under new names: **`DoNotSchedule` filters; `ScheduleAnyway` scores.**

## Limitation

"There's no guarantee that the constraints remain satisfied when Pods are removed. For example, scaling down a Deployment may result in imbalanced Pods distribution."

These are scheduling-time constraints. They describe a decision, not a standing invariant.

## Related

`[[topology-domain]]` · `[[inter-pod-affinity]]` · `[[scheduling]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/nodename.md ===
# `nodeName`

**Introduced:** Chapter 7 §6 · **Objective:** D1.3

"A more direct form of node selection than affinity or `nodeSelector`." A field in the Pod spec: "if it is not empty, the scheduler ignores the Pod" and the kubelet on the named node tries to place the Pod there.

"Using `nodeName` **overrules** using `nodeSelector` or affinity and anti-affinity rules."

Overrules — not "takes precedence within the same evaluation." The scheduler doesn't run. Nothing else in the Pod spec is consulted, because the component that would have consulted it was skipped.

## ★ It is the scheduler's output, not a separate API

The DaemonSet controller does **not** use `nodeName`. It sets node affinity per Pod, and then "the default scheduler typically takes over and then binds the Pod to the target host by **setting the `.spec.nodeName` field**."

Binding *is* writing `.spec.nodeName`. Setting it by hand means filling in the scheduler's answer before it was asked the question — and skipping every check that would have validated it.

## The one failure that isn't `Pending`

- "If the named node does not exist, the Pod will not run, and in some cases may be automatically deleted."
- "If the named node does not have the resources to accommodate the Pod, the Pod will fail and its reason will indicate why, for example OutOfmemory or OutOfcpu."
- "Node names in cloud environments are not always predictable or stable."

Every other placement failure leaves a Pod waiting patiently. This one fails outright, because the feasibility check never happened.

⚑ `OutOfmemory` is a **scheduling-admission** failure. Do not confuse it with `OOMKilled`, a **runtime** kill by the kubelet (named at Chapter 5 §8, defined at Chapter 13 §4).

## Register

The API does let you specify a node when you create a Pod, "but this is unusual and is only done in special cases" — strong discouragement, coming from reference documentation. `nodeName` is not the most forceful way of asking. It is the absence of asking.

## Related

`[[scheduling]]` · `[[pending-pod]]` · `[[nodeselector]]` · `[[node-affinity]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/predicates-priorities.md ===
# Predicates and Priorities (older scheduler vocabulary)

**Introduced:** Chapter 7 §6 · **Objective:** D1.3

Two documented ways to configure filtering and scoring behaviour:

- **Scheduling Policies** — **Predicates** for filtering, **Priorities** for scoring.
- **Scheduling Profiles** — **plugins** implementing different scheduling stages, including `QueueSort`, `Filter`, `Score`, `Bind`, `Reserve` and `Permit`. `kube-scheduler` can run different profiles.

## Treat this as vocabulary, not configuration choice

| Older name | What it is |
|---|---|
| Predicate | A **filter** — decides whether a node is feasible |
| Priority | A **score** — ranks the nodes that survived filtering |

Predicates are filtering under an older name. Priorities are scoring under an older name. The profile plugin stages are the same pipeline with more seats exposed — and two of those seat names, `Filter` and `Score`, are literally the steps already learned.

If you read an older article about "the `PodFitsResources` predicate," you now know that's a filter, and you can carry on reading. That is what this material is worth on this exam.

## ⚑ Currency — CLOSED, do not re-open

A prior draft flagged the Scheduling Policies model as possibly removed upstream. The research stage re-fetched the live `kube-scheduler` page and found it character-identical to the cached snapshot on this passage. The chapter deliberately teaches Predicates/Priorities as *older names for the two steps* rather than as a currently-selectable configuration option, so it is true under every reading. **Do not add a "Policies have been removed" claim** — that assertion appears nowhere in the cached corpus.

⚑ `QueueSort`, `Reserve` and `Permit` are named but never explained. GAP — fetch `kubernetes.io/docs/reference/scheduling/config/`.

## Related

`[[scheduling]]` · `[[feasible-node]]`
=== END WRITE ===

=== UPDATE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-request.md ===
⚑⚑ CANON-DRIFT WARNING — READ BEFORE APPLYING ⚑⚑

This shard is proposed by BOTH the ch-05 and ch-07 manifests, with framings that
read as contradictory. DO NOT let the ch-07 replay overwrite the ch-05 body.
Apply this as an ADDITIVE SECTION appended beneath ch-05's existing content.
If ch-05's "a request is a floor, not a ceiling" sentence is absent after
replay, the merge was done wrong — stop and re-apply.

---

## Chapter 7 addition — the scheduler's side of the same number

Chapter 5 established the **runtime** rule, from the container's point of view:

> "If the node where a Pod is running has enough of a resource available, it's
> possible — and allowed — for a container to use more of that resource than its
> request specifies. However, a container is not allowed to use more than its
> resource limit."
>
> "So a request is a floor, not a ceiling. Exceeding your request on a node with
> spare capacity is normal, expected behavior, not a violation of anything.
> One number gets you a berth. The other keeps you inside it."

Chapter 7 §2 establishes the **scheduling** rule, from the node's ledger:

> "When you specify a resource request for a container, the kube-scheduler uses
> that information to decide which node to place the Pod on, and the kubelet
> **reserves at least the request amount** of that resource specifically for that
> container to use."
>
> "A request is a **booking**. Not an estimate, not a hint, not a starting point
> for measurement. Once a Pod is placed, its requests are taken off the node's
> available balance and stay off, whether the container ever touches that memory
> or not."

### These are not in conflict — they describe different actors

| | Chapter 5 (floor) | Chapter 7 (booking) |
|---|---|---|
| Actor | the **kubelet**, at runtime | the **scheduler**, at placement |
| Subject | what a container may *use* | what a node has *left to offer* |
| Timing | continuously, while running | once, before the Pod exists |

Chapter 7 resolves the tension in its own words: **"A node can be busy and empty
at the same time, and only one of those two states is the scheduler's business."**

### The canonical arithmetic

16 GiB allocatable · four Pods × 4 GiB requested · monitoring reports 2 GiB in use
· a fifth Pod requests 1 GiB → **does not schedule.** Sixteen booked out of sixteen
leaves zero. The 2 GiB describes what the containers are doing with what they
booked; it does not hand any of it back.

Ten Pods that each requested 1 GiB and each use 50 MiB have filled a 10 GiB node
completely, as far as scheduling is concerned.

### Baseline

The subtraction is against **Allocatable**, not the machine's total RAM. The
scheduler does not over-subscribe Allocatable. What makes Capacity and Allocatable
differ is Chapter 8's material.

### Sourcing note

⚑ The cached corpus supports the positive claims (PodFitsResources checks requests;
the kubelet reserves at least the request amount; the scheduler does not
over-subscribe Allocatable) but states nothing about live utilisation. The absolute
negative "the scheduler never consults observed usage" was removed from the draft
as unsourced. Do not reintroduce it. Gap recorded as **G-7G**; the fetch is
`kubernetes.io/docs/concepts/scheduling-eviction/resource-bin-packing/`.

## Related

`[[resource-limit]]` · `[[feasible-node]]` · `[[pending-pod]]` · `[[scheduling]]`
=== END UPDATE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/label-selector.md ===

## Chapter 7 addition — the direction inverts

Chapter 4 taught label selectors as the universal join and listed **node scheduling
constraints** as one of four uses. Chapter 7 §3 exercises that fourth use, and it
runs backwards relative to the other three.

Every prior use in this book is **an object selecting a set of Pods** — a Service
selecting its backends, a ReplicaSet selecting the Pods it owns. In `nodeSelector`
and node affinity it is **a Pod selecting nodes**. Same mechanism, opposite subject
and object.

Readers who internalised "selectors find Pods" will read §3 as backwards for a page
or two. Naming the inversion out loud is the fix.

**Operator note:** Chapter 4's set-based operators are lowercase (`in`, `notin`,
`exists`). Node affinity's are capitalised and a superset: `In`, `NotIn`, `Exists`,
`DoesNotExist`, `Gt`, `Lt`. `nodeSelector` itself has no operators — implicit
equality only, ANDed.

Related: `[[nodeselector]]` · `[[node-affinity]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

## Chapter 7 addition — the scheduler is another instance

Chapter 7 §7 closes by noting the scheduler "watches for newly created Pods that
have no node assigned," compares what exists against what has been placed, and acts
on the difference.

That is the control-loop shape. "The scheduler is not an exception to the cluster's
architecture; it's another instance of it, wearing a specialised hat."

⚑ Editorial note carried from the integration report: this sentence in the shipped
chapter carries **no cross-bearing**. The loop is defined at Chapter 3 §6 and the
reader watches one work at Chapter 6 §2. A bracketed pointer to either or both would
close the book's strongest recurring theme at its cleanest instance.

Related: `[[scheduling]]` · `[[pending-pod]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-lifetime.md ===

## Chapter 7 addition — scheduled once, under a second motivation

Chapter 5 established scheduled-once with a node-**failure** motivation. Chapter 7 §1
re-establishes it as the reason the whole chapter exists, and Practice Q5 re-tests it
under the opposite motivation: a strictly *better* node joins the cluster and sits
nearly idle. The answer is identical — nothing moves.

"Pods are created, assigned a unique ID, and scheduled to run on nodes where they
remain until termination or deletion. A Pod is never 'rescheduled' to a different
node; instead, it is replaced by a new, near-identical Pod with a different UID."

Kubernetes does not optimise placement continuously. There is no rebalancing loop.

**The consequence Chapter 7 draws:** "everything you want to be true about where a
Pod runs has to be true *before* the Pod is created." Every mechanism in Chapter 7 is
read at scheduling time and none is enforced continuously afterwards — which is what
`IgnoredDuringExecution` names.

Related: `[[node-affinity]]` · `[[scheduling]]` · `[[pod-phase]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/runtimeclass.md ===

## Chapter 7 addition — both Chapter 2 promises discharged

Chapter 2 §7 noted a RuntimeClass can carry (a) a Pod **overhead** so the scheduler
accounts for the runtime's resource cost, and (b) **scheduling constraints** — a
`nodeSelector` and tolerations — so Pods land on nodes supporting the handler, and
deferred the reasoning to Chapter 7.

- **The `nodeSelector` half** is discharged at Chapter 7 §3, and the tolerations half
  at §4.
- **The overhead half** is discharged at §2, partially: "a Pod running under a
  sandboxed runtime doesn't consume only what its containers asked for, and the
  overhead exists so the scheduler's arithmetic accounts for the runtime's own cost
  rather than pretending it's free."

⚑ The cached RuntimeClass snapshot states only that the overhead exists so the
scheduler accounts for the runtime's cost. It does **not** state the mechanism (that
overhead is added to the Pod's effective request). Chapter 7's phrasing is held to
what the snapshot supports. Gap **G-7F**; fetch
`kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/`.

Related: `[[resource-request]]` · `[[nodeselector]]` · `[[toleration]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-phase.md ===

## Chapter 7 note — `Pending` in its scheduling sense

Chapter 7 §2 exercises the `Pending` phase specifically as the state of an
unschedulable Pod: it "covers, among other things, time a Pod spends waiting to be
scheduled." A state, not an error — nothing times out, nothing retries with looser
constraints. See `[[pending-pod]]` for the full treatment.

The one Chapter 7 failure that does **not** produce `Pending` is a `nodeName`-pinned
Pod that doesn't fit: it fails outright. See `[[nodename]]`.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.3 — Kubernetes Fundamentals › Scheduling | Chapter 7 | deep | — |

<!--
D1.3 notes (Stage 14, ch-07, 2026-08-24):
- Domain D1 "Kubernetes Fundamentals" = 44% of the exam; competencies are
  "Kubernetes Core Concepts; Administration; Scheduling; Containerization"
  [source: cncf-kcna-curriculum-pdf-2026-08-23 line 13]. This confirms both
  figures the chapter's metadata AUTHOR-REVIEW asked to verify (44% and the
  competency name "Scheduling"); that open item can be closed.
- CNCF publishes DOMAIN weights only, not COMPETENCY weights. The chapter's
  ~5% is an authored allocation and is disclosed as such in front matter.
- All seven sections of Chapter 7 carry objectives: ["D1.3"]. Chapter 7 is the
  sole owner of this competency; no earlier chapter claims it and none is
  scheduled to revisit it. B3 flagged scheduling as one of two "thin" areas
  needing a named retrieval anchor later in the book (the other is Helm/Ch 14).
- Adjacent-but-unowned: PriorityClass and preemption are named at Chapter 7 §2
  and owned by NO chapter and NO lineup entry. Author decision pending.
-->
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

| Tested topic | Original chapter | Retested in |
|---|---|---|
| request vs limit — which one the scheduler reads | ch 5 §8 | ch 7 — ☆ Bearings #1 Q3 |
| ReplicaSet creates a Pod with nowhere to run | ch 6 §2 | ch 7 — ☆ Bearings #1 Q5 |
| label selectors as the universal join | ch 4 §5 | ch 7 — ☆ Bearings #2 Q1 |
| a Pod is scheduled once, never rescheduled | ch 5 §4 | ch 7 — Practice Q5 |
| scheduler records the decision / kubelet acts on it | ch 3 §2 | ch 7 — Practice Q6 |
| set-based label selector operators | ch 4 §5 | ch 7 — Practice Q12 |
| DaemonSet one-per-node distribution | ch 6 §7 | ch 7 — Practice Q15 |

<!--
Chapter 7 retrieval accounting (Stage 14, 2026-08-24):
- 7 tagged items / 33 graded items (15 Bearings + 18 Practice) = 21%.
  B3 band for Ch 7 is 20-25%. PASS.
- Sources span Ch 3, 4, 5, 6 — four distinct chapters, furthest four back.
  B3's ">=4 chapters back" floor begins binding at Ch 8; met here already.
- Soundings excluded from the budget per B3 decision #2, but Soundings Q3, Q4
  and Q6 do retrieval work against Ch 5 and Ch 6 by design.
- Practice Q15 is a DISCRIMINATION item, not plain recall: "the Pods end up
  spread out" vs "a spreading constraint was enforced" are different claims.
- Practice Q5 deliberately re-tests the Ch 5 scheduled-once rule under a NEW
  motivation (a better node appears, not a node failure).

⚑ Ch 7 is the sole owner of D1.3 and nothing revisits scheduling. B3 called for
a named retrieval anchor for this material later in the book. Not yet placed.

⚑ book-outline/retrieval-architecture.md is NOT the B3 document — it is a
permission-failure message plus a prose summary of B3's conclusions. The
per-chapter retrieval schedule was never written to disk. This log is currently
the only durable record of what has actually been retrieved.
-->
=== END APPEND ===
```

**One thing to flag before you act on any of this:** none of the blocks above will reach disk on their own. I verified that stage 14 writes only `kb-manifest.md`, that nothing in certcomp parses `=== WRITE`/`=== APPEND`, and that `Book-KCNA/knowledge-base/` does not exist — so Chapters 1–7's entire knowledge base is currently sitting unapplied inside seven manifests. Applying them requires a manual replay in order (ch-01 → … → ch-07), and the `resource-request.md` step must be merged rather than overwritten or it will delete Chapter 5's "a request is a floor, not a ceiling" canon.