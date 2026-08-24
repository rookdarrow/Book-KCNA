I have everything I need. Two findings change what this stage can report, and both are verified on disk.

```markdown
# Knowledge-Base Manifest — KCNA Chapter 7

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 7 — Assigning the Berth
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-24

**Inputs consulted:** the finalized chapter (1,124 lines); `ch-07/integration.md`; `ch-07/outline.md` frontmatter (`kb_tags` — 44 concepts, 4 commands, `objectives: ["D1.3"]`); `Book-KCNA/sources/` (137 files, enumerated); the prior manifests `ch-01`, `ch-03`, `ch-04`, `ch-05`; shipped `chapter-01` … `chapter-05`; `pipeline/prompts/14_knowledge_base_update.md`.

---

## Two verifications that reframe this stage

**1. ✅ The research-plumbing failure did NOT recur. Chapter 7's citations are completely clean.**

I extracted all 146 `[source:]` tags, reduced to 16 unique snapshots, and checked each against `sources/`. **All 16 resolve.** `sources/` has grown 115 → 137 files, so Chapters 6 and 7 both materialized their fetches.

This is the first chapter since the failure appeared where a Stage 14 manifest does not have to open with a snapshot materializer. Chapter 5's manifest listed five missing snapshots gating a ★ Fixed Point, a 🪢 Mnemonic, four Bearings items and three Practice questions. **Chapter 7 has zero.** Every definition below inherits a tag that resolves to a real cached file — which is the precondition for Rule 5 meaning anything.

Worth stating plainly because four consecutive manifests reported the opposite: **this axis is fixed.**

**2. ⚑ The write path is still broken — fifth manifest to say so, and now with a new detail.**

`=== WRITE` appears exactly once in all of `certcomp`: in the prompt that asks for it. No parser consumes these blocks. `Book-KCNA/knowledge-base/` still does not exist. **New this chapter:** `certcomp/tools/` does not exist either, so the materializer scripts Chapters 4 and 5 supplied were never saved, let alone run.

Everything below is composed correctly and none of it will reach disk without a manual step. Recovery order is load-bearing: **ch-01 → ch-03 → ch-04 → ch-05 → ch-07** (ch-01 and ch-03 emit full files; ch-04, ch-05 and ch-07 emit appends). Chapters 2 and 6 have no manifest to replay.

**3. ⚑ Inherited caveat, from Integration Finding 0.** The revision stage applied no diagnostic findings — `draft-v2.md` differs from `draft-v1.md` only in em-dash punctuation. Every definition below is therefore inherited from a draft whose fact-accuracy findings are still open. Rule 5 obliges me to inherit the wording exactly; where a definition rests on an untagged claim, the row carries a ⚑ and says so rather than quietly laundering it into canon.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**56 terms contributed — 49 defined · 2 partial · 5 reserved · 6 status corrections to existing rows.**

Stage 13's coverage table counted **9** terms needing entries. That count is correct *for its own question* — it lists only concepts with an open definitional gap. The book's glossary needs the other 47 too (skill Part 16: "all technical terms introduced in the book," 100-term floor), and Chapter 5 set this precedent explicitly. The two counts are not in conflict; they answer different questions.

Appended as a Chapter 7 section rather than merged into the A–Z, following Chapters 4 and 5. This file is append-only under the current pipeline; re-transcribing prior chapters' prose to preserve one alphabet is exactly the drift Rule 5 forbids. Book assembly merges alphabets mechanically.

Representative rows — full text in the append block:

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **feasible node** | "The nodes that meet a Pod's scheduling requirements are called feasible nodes." | Chapter 7 §1 |
| **filtering** | "finds the set of nodes where it is feasible to schedule the Pod. After this step the node list contains any suitable nodes, often more than one. If the list is empty, that Pod isn't yet schedulable." | Chapter 7 §1 |
| **scoring** | "the scheduler assigns a score to each node that survived filtering, based on the active scoring rules, and then assigns the Pod to the node with the highest ranking." | Chapter 7 §1 |
| **binding** ★ | "The scheduler notifies the API server about its decision, and *that* is what the word binding names." Concretely — from §6 — binding is the default scheduler "setting the `.spec.nodeName` field." | Chapter 7 §1, §6 — **closes Chapter 3's reservation** |
| **random tie-break** | "If there is more than one node with equal scores, `kube-scheduler` selects one of them **at random**." | Chapter 7 §1 |
| **Allocatable** | "'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods"; "the scheduler treats 'Allocatable' as the available `capacity` for pods." The scheduler does not over-subscribe it. | Chapter 7 §2 |
| **taint** | Lives on the **node**. "One or more taints are applied to a node; this marks that the node should not accept any Pods that do not tolerate the taints." | Chapter 7 §4 |
| **toleration** | Lives on the **Pod**. "Tolerations are applied to Pods, and they allow the scheduler to schedule Pods with matching taints." ⚠ "Tolerations allow scheduling but don't guarantee scheduling." | Chapter 7 §4 |
| **`topologyKey`** | "the key for the node label that the system uses to denote the domain." Nodes with that key and identical values are in the same topology. | Chapter 7 §5 |
| **`nodeName`** | "if it is not empty, the scheduler ignores the Pod" and the kubelet on the named node tries to place it. Overrules `nodeSelector` and affinity. | Chapter 7 §6 |
| *(39 further defined rows + 2 partial + 5 reserved — full text in the append block)* | | |

### ⚑ Two rows the reader can now be graded on that rest on untagged claims

Rule 5 forbids me inventing replacement wording, so both are recorded verbatim with the gap named:

- **`node.kubernetes.io/unschedulable` as a deliberate administrative act.** §4 and the Voyage Ahead both assert that "something puts that one there on purpose." The taint key and its `NoSchedule` effect are tagged to `k8s-docs-daemonset-2026-08-24`; the *causal* claim is untagged. It is almost certainly true and Chapter 8 owns it. Recorded as a **reserved** row, not a defined one.
- **Node `Capacity`.** §2 says "Some of that total is spoken for by things that aren't Pods." I checked `k8s-docs-nodes-2026-08-23`: it **names** Capacity and Allocatable in the node-status list and never defines Capacity or states its relationship to Allocatable. The relationship is genuinely absent from cache — research-manifest gap **G-7C** — so the fix is a fetch or a softening, **not a tag.** Recorded reserved → Ch 8.

### ⚑ One row where the draft got it right and should be left alone

**Pod overhead** is Tier 2 (partial) and that is the correct outcome, not a shortfall. I read `k8s-docs-runtime-class-2026-08-23` line 16 directly: it says a RuntimeClass can carry "a Pod overhead so the scheduler accounts for the runtime's resource cost" — **and nothing about the mechanism.** The chapter's `AUTHOR-REVIEW` comment holds the prose to exactly what the snapshot supports and names the URL a fetch would need. That is the behaviour Rule 5 exists to produce. If the author wants the mechanism stated, it costs one fetch; it must not be written from memory.

---

## Rule 6 — canon conflicts, recorded not resolved

**No contradictions found.** I checked Chapter 7 against every shard it could plausibly collide with: `control-plane-components.md`, `node-components.md`, `control-loop.md`, `label-selector.md`, `cluster-scoped-resource.md`, `pod-lifetime.md`, `resource-request.md`, `resource-limit.md`, `pod-phase.md`, `api-server-hub.md`, `kubernetes-object.md`. Chapter 7 is consistent with all eleven.

**Three downstream obligations DISCHARGED — the best result of any chapter so far:**

1. **✅ `control-plane-components.md`'s Chapter 7 row is DISCHARGED.** The shard records: *"Ch 7 | The scheduler's actual selection algorithm. Ch 3 deliberately withholds it."* §1 delivers it. More important, the shard's **"Two boundaries that must not drift" #1** — *"The scheduler selects; it does not start… it notifies the API server about its decision, in a process called binding"* — is reproduced by Chapter 7 from the same snapshot, in the same words, and then **hardened**: `ch07-fig01` draws the third arrow landing on the API server rather than on the node, and Practice Q6 grades it. **Checked specifically because a three-chapter gap is where drift shows up, and there is none.**

2. **✅ `resource-request.md`'s Chapter 7 row is DISCHARGED — the first of its four to land.** The shard records four downstream obligations (Ch 7, 13, 17, 18) and calls them "the longest forward reach in the book." §2 delivers *"Requests as the scheduler's filtering step"* and extends it with a fact Chapter 5 did not have: requests are **booked**, and the scheduler does not over-subscribe Allocatable. Extension, not contradiction — Chapter 5's "a request is a floor, not a ceiling" (a container *may* exceed its request on a node with spare capacity) and Chapter 7's "the node is full as far as scheduling is concerned" are the same rule seen from the kubelet's side and the scheduler's side. Both are true simultaneously. **The shard should be updated, not superseded** — see the concept-shard section.

3. **✅ `label-selector.md`'s ⚓ Worth Securing is DEMONSTRATED.** The shard claims: *"ReplicaSet, Service, NetworkPolicy, and node affinity are not four mechanisms to learn. They are one mechanism."* Chapter 7 §3 is where the fourth item cashes, and it does the harder version of the job — it names the *direction inversion* (previously an object selecting Pods; here a Pod selecting nodes) rather than just reusing the syntax.

**Three notes worth recording, one of them a genuine near-miss:**

**⚑ A. `control-loop.md`'s canonical shape gets its best instance in the book — and the chapter points the reader at the wrong chapter for it.**

The shard's ★ Fixed Point: a controller *"usually acts by asking the API server to change something, **not by doing the thing itself**."* §7's closing paragraph observes that the scheduler "watches for newly created Pods that have no node assigned, compares what exists against what has been placed, and acts on the difference," and calls it "the same shape as every controller in Chapter 6."

The observation is exactly right, and it is **the cleanest instance of the *common* controller shape the book has produced** — the scheduler never touches a node; it writes to the API server and something else acts. That pairs precisely with Chapter 5's kubelet, which Chapter 5's manifest flagged as the *uncommon* direct-control shape. Chapters 5 and 7 now hold one canonical example of each, which is a better teaching position than either chapter alone.

Two problems with where it points:
- It attributes the pattern to **Chapter 6**, which is withdrawn from the repo. The loop is *defined* at Chapter 3 §6, which is where the shard is homed and where the reader can actually go.
- It carries **no cross-bearing at all** (Integration Finding 9).

**Recommend the pointer read Ch 3 §6, not Ch 6.** That is a stronger claim, it survives the Chapter 6 re-draft, and it is one bracketed insertion.

**⚑ B. `cluster-scoped-resource.md` has a free retrieval sitting in this chapter and Chapter 7 doesn't take it.**

The shard's ★ Fixed Point names **Nodes** explicitly: *"Not everything lives in a namespace. **Nodes**, PersistentVolumes, and StorageClasses are cluster-scoped."* Chapter 7 spends a chapter labelling nodes, tainting nodes, and reading node status — and never once retrieves it. The evidence is literally in the chapter's own command lines: `kubectl label nodes <name>` and `kubectl taint nodes node1 …` take no `-n` flag, **because nodes aren't namespaced.**

This theme has one retrieval in the whole book (Ch 5 §6, and that one was by paraphrase). Chapter 7 is the most natural site the book will offer for it — the fact is demonstrable rather than assertable. **One clause on a command line closes it.**

**⚑ C. Chapter 4 already published the capitalized operator vocabulary, and Chapter 7 re-introduces it as new.**

`label-selector.md` records the structured selector form with the set-based operator vocabulary **`In`, `NotIn`, `Exists`, `DoesNotExist`** and the exact-equivalence rule for `matchLabels`. Chapter 7's node-affinity operators are **those same four plus `Gt` and `Lt`**, used inside a field also called `matchExpressions`.

Practice Q12 is tagged `[retrieval: ch4]` and does the *lowercase* half correctly (Chapter 4's `in`/`notin`/`exists` set-based selector syntax). Integration verified that casing distinction and it is right. But the *stronger* fact — that node affinity's `matchExpressions` **is** Chapter 4's structured selector form with two numeric operators bolted on — is never stated. That reframes §3 from "a new syntax" to "the syntax you already know, extended," which is the whole thesis of `label-selector.md`.

Not a contradiction. A missed consolidation, and the cheapest one available in the chapter.

---

## Concept shards added at `Book-KCNA/knowledge-base/concepts/{slug}.md`

**Thirteen created.** Every slug is drawn from `outline.md`'s `kb_tags.concepts` so context-packer lookups round-trip, following the Chapter 4 and 5 precedent.

- `concepts/scheduling.md` — **created** (§1 + §7; the two-step operation, feasible nodes, the coin flip, binding, and the filter-or-score taxonomy as its Zenith)
- `concepts/feasible-node.md` — **created** (§2; requests vs Allocatable, booking not measuring, `PodFitsResources`)
- `concepts/pending-pod.md` — **created** (§2; the state-not-an-error rule) — *Chapter 13's opening move retrieves this*
- `concepts/nodeselector.md` — **created** (§3)
- `concepts/node-affinity.md` — **created** (§3; operators, the two hardness levels, the independence-of-axes figure)
- `concepts/taint.md` — **created** (§4; the refusal, all three effects with timing)
- `concepts/toleration.md` — **created** (§4; the exemption, the four matching cases, permits-never-attracts)
- `concepts/built-in-node-condition-taints.md` — **created** (§4; the seven, the 300 s default, the DaemonSet mechanism)
- `concepts/inter-pod-affinity.md` — **created** (§5; both directions)
- `concepts/topology-domain.md` — **created** (§5; `topologyKey` as a variable)
- `concepts/topology-spread-constraints.md` — **created** (§5; the four fields)
- `concepts/nodename.md` — **created** (§6; the bypass, and binding's actual field write)
- `concepts/predicates-priorities.md` — **created** (§6; the vocabulary map, profiles, ⚑ the currency risk)

**Structural choices, with reasons.**

`taint.md` carries all three effects rather than splitting `noschedule` / `prefernoschedule` / `noexecute` into three files: the discrimination *between their timing* is the pedagogy, and three shards would let the one fact that matters — only `NoExecute` touches running Pods — fall between them. Same reasoning Chapter 5 used for `probe.md`.

`taint.md` and `toleration.md` **are** split, mirroring `resource-request.md` / `resource-limit.md`: a two-term contrast where each half lives on a different object. Splitting them is what makes "the taint is on the node, the toleration is on the Pod" structurally unforgettable, and Integration confirms that inversion is the chapter's most durable error.

`topology-domain.md` is its own shard rather than a section inside `inter-pod-affinity.md` because **both** anti-affinity and spread constraints depend on it. Folding it into either would duplicate it into the other, and duplicated definitions drift.

`nodeselector.md` is deliberately short and **deliberately repeats** one fact that also appears in `node-affinity.md`: `nodeSelector` and required node affinity **fail identically**. That is the fact `ch07-fig02` exists to prevent falling between them, so it is stated in both.

**Not created, with reasons.** `scheduler-plugins`, `scheduling-profiles`, `scheduling-policies`, `custom-scheduler`, `schedulername` — all five fold into `predicates-priorities.md`; individually each is a list or a single sentence, and the *only* transferable payload is the vocabulary map onto §1's spine. `unbound-pod`, `filtering`, `scoring`, `binding`, `random-tie-break` — folded into `scheduling.md`; they are one pipeline described in five words. `node-capacity` — **cannot be created**; not defined in the chapter and not in cache (see G-7C). `pod-overhead` — one clause held correctly to its snapshot; a shard would be mostly a flag. `pod-affinity` / `pod-anti-affinity` — both served by `inter-pod-affinity.md`, which states both directions; recorded here so a lookup on either slug knows where to land. **No `commands/` shards** — the four `kubectl` verbs appear at recognition depth only, and Chapter 8 owns the command surface, per Chapters 4 and 5.

**One update proposed, not applied.** `resource-request.md`'s "Downstream obligations" table needs its **Ch 7** row marked discharged, and its body needs one added sentence recording the booking semantics. I have **not** rewritten the shard — Rule 6's spirit is that a later chapter does not silently mutate an earlier chapter's canon file, and the change is additive enough to be safe but visible enough to be the author's. The exact insertion is in the append block under `## ⚑ Proposed shard update`.

---

## Voice-exemplar candidates nominated

**Not written to `voice-exemplars.md`** — Rule 1. Nominations only, for author ratification.

| Function | Excerpt | Recommendation |
|---|---|---|
| **☀️ Zenith** | "Every mechanism in this chapter plugs into one of exactly two slots in §1's pipeline. It either removes nodes from consideration — a filter — or it changes the ranking of the nodes that survived — a score. **Six vocabularies. Two slots. That's the chapter.**" | **Strongest in the chapter.** Collapses six sections into one binary without simplifying anything away, and the three-fragment close is the brand's confident register at its most compressed. Nominate as the canonical Zenith exemplar. |
| **Logbook Entry** | *(§4, the GPU nodes)* "The version of this story where the team notices in ten minutes and the version where they notice in three weeks differ only in whether somebody knew that a toleration doesn't attract." | **Strong, and the best §18.15 exemplar the book has.** It is a war story that ends on a *transferable rule* rather than a moral, and the closing sentence makes the stakes concrete without blaming anyone. Subject-dignity clean: the wryness lands on the practitioners, who are in the room. |
| **⚠ Navigational Hazards** | "`Pending` is a **state**, not an error… No component is quietly retrying it with looser constraints, and no timer will eventually convert it into a failure." | **Strong.** Corrects a misconception by enumerating what *doesn't* happen, which is harder to write and much stickier than asserting what does. |
| **★ Fixed Point** | "Filtering fits a Pod's *requests* against a node's *available* capacity. **The scheduler books; it does not measure.** Ten Pods that each requested 1 GiB and each use 50 MiB have filled a 10 GiB node completely, as far as scheduling is concerned." | **Strong.** Rule, then the four-word compression, then the arithmetic that proves it. Structurally identical to Chapter 4's `spec`/`status` and Chapter 5's phase/state Fixed Points — this is now a series signature and worth ratifying as one. |
| **generation-effect prompt** | "**Before reading on:** a node has 16 GiB of memory available to Pods… Monitoring says the node is using 2 GiB in total. A fifth Pod arrives requesting 1 GiB. Does it schedule on this node? **Decide before you keep reading.**" | **Strong.** Textbook Part 10 generation effect, and the numbers are chosen so the intuitive answer is wrong. Best instance of the pattern in the book so far. |
| **🪢 Mnemonic** | "Read `requiredDuringSchedulingIgnoredDuringExecution` as two clauses joined at the seam: **required when scheduling, ignored once running.** The word is thirty-nine characters; the meaning is six." | **Strong.** Turns the material's most intimidating surface feature into a decoding rule that generalizes to every field in the family. |
| **— Dead Reckoning** | *(§4 matching rules)* "A toleration matches a taint when the keys are the same and the effects are the same, and one of two operator conditions holds. If the operator is `Exists`, no value should be specified. If the operator is `Equal`, the values must be equal." | **Strong.** Facts-only register done correctly — zero framing, zero metaphor, and the section that introduces it says outright "Here the metaphors run out," which is the honest signal the register is for. |
| **desirable difficulty** | *(Bearings #2 Q2)* "⚠ **This one is intentionally hard, and the intuitive answer is wrong.** Struggle is the point — missing it is expected and is exactly what makes the correct answer stick." | **Moderate–strong.** Clean Part 10B execution. Marked moderate only because Integration found the Soundings answer key **spends** this item's payload before the reader reaches it — the exemplar is good, its placement is currently undercut. |
| **chapter-opening / stakes** | "The stakes, stated flat. Five points on this book's allocation, which is not a lot. What that number doesn't capture is that scheduling is where four separate exam-checkable facts live that have no home anywhere else… This chapter is short on volume and dense on returns." | **Moderate.** Genuinely good — it declines to inflate a 5% chapter and argues for it on different grounds instead, which is the brand's honesty position doing real work. Held at moderate because "exam-checkable" is a soft frequency claim of the kind Chapter 3's open guardrail #8 finding concerns. |
| **closing epigraph (original)** | "You cannot move a berth once it is assigned. You can only be careful about what you said before it was." | **Strong.** Earns its place — §1 established irreversibility as the chapter's organizing constraint, so the epigraph reads as a summary rather than an ornament. Matches the Chapter 5 closing-epigraph pattern the author may want to ratify as a series convention. |

**⚑ Deliberately not nominated, and one is a hard exclusion.**

**Hard exclusion — the 🏆 Safe Harbor line at L1113.** *"Scheduling is the material that most study guides present as a catalogue of six unrelated features."* Integration marks this a **guardrail #3 FAIL** (never strawman alternative study methods) and I concur without reservation. It is the only competitor-disparagement instance in the book, and promoting anything near it would ratify the move into brand canon. Integration's rewrite — make the claim about the *material* rather than about other publishers — loses nothing and is truer. **Should be fixed before this chapter ships, not merely before it is nominated.**

**Soft exclusions**, consistent with Chapters 3, 4 and 5: every line carrying an unhedged prevalence or exam-frequency claim — *"the single most common misconception about the scheduler," "the most common real-world mistake in this material," "The most durable error in this material," "the most common misconception about this component," "the answers a competent engineer would design."* Chapter 3's guardrail #8 remediation is still open and Chapter 7 is now the **third consecutive chapter** to drift back into the construction. Recorded in the guardrail table below rather than nominated.

**One register note, favourable.** Chapter 5's manifest flagged a repetition risk: three "small hours" beats across Chapters 4 and 5, warning that a signature repeated on schedule becomes a tic. **Chapter 7 has none.** Whether that is deliberate or incidental, the diversification the author was asked to consider has happened on its own.

---

## Objective coverage log

Chapter 7 covers **D1.3 — Scheduling** at **deep** depth. **This is the objective's first and, per B2, only chapter.** Unlike D1.1 (four chapters, still in progress), D1.3 opens and closes here.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.3** | **Chapter 7** | **deep** | **2026-08-24** |

**Registry row change:** `D1.3 | Scheduling | Ch 7` → status becomes **"complete — Ch 7 covered 2026-08-24"**, subject to the coverage shortfall below.

### Chapter 7 — D1.3 coverage detail

| Sub-topic | Depth |
|---|---|
| The two-step operation: filtering then scoring | **deep — discharges `control-plane-components.md`'s Ch 7 obligation** |
| Binding as a notification; concretely, writing `.spec.nodeName` | **deep — closes Chapter 3's reserved term** |
| Feasible nodes; `PodFitsResources` | deep |
| Random tie-break | deep — one sentence, correctly weighted |
| Requests as the filtering input; booked vs measured; Allocatable | **deep — discharges `resource-request.md`'s Ch 7 obligation, first of four** |
| `Pending` as a state, not an error | **deep — Chapter 13's opening move depends on it** |
| Node labels; standard/well-known labels | moderate |
| `nodeSelector` | deep |
| Node affinity: six operators, two hardness levels, `IgnoredDuringExecution` | deep |
| Taints: three effects and their timing | **deep — the chapter's densest recall block** |
| Tolerations: matching rules, permits-never-attracts | **deep — the most durable error in the material, correctly weighted** |
| Built-in node-condition taints; the DaemonSet mechanism | moderate — **pays Chapter 6's "mechanism in disguise" tease** ⚠ see below |
| Inter-Pod affinity / anti-affinity; `topologyKey` | moderate–deep |
| Topology spread constraints: four fields | moderate — recognition depth, correctly scoped |
| `nodeName`; the one failure that isn't `Pending` | deep |
| `schedulerName` / custom scheduler | recognition — correctly scoped to Ch 17 |
| Predicates / Priorities vocabulary map | moderate — ⚑ currency risk, see below |
| **Data locality · inter-workload interference · deadlines** | ⚑ **ABSENT — and Chapter 3 published them to the reader** |
| Priority / preemption / `PriorityClass` | named and scoped out — correct |

### ⚑ The one coverage shortfall, and it is an integration debt rather than a curriculum one

`chapter-03:413` publishes the documentation's six scheduling factors verbatim, including **data locality, inter-workload interference, and deadlines** — and Chapter 7 is the chapter that owes the detail. It delivers three of six and never mentions the other three, not even to scope them out.

Curriculum-alignment logged this as D1.3-09 PARTIAL. The *knowledge-base* cost is different and worth stating separately: a reader who remembers Chapter 3's list gets no acknowledgement that half of it was dropped, which is precisely the "order/truth balance" failure skill Part 11 warns about. **Chapter 7 already models the correct fix twice** — the preemption clause ("Register that they exist so that nothing in this chapter reads as a lie later") and the `minDomains` mention. One sentence in §2 or §7, copying that move, closes it.

### ⚑ Currency risk carried into the ledger

The chapter's §6 `AUTHOR-REVIEW` flags it and the flag is correct, so it is recorded here rather than left inside a comment the reconcile pass may drop: the cached `k8s-docs-kube-scheduler-2026-08-23` snapshot presents Scheduling Policies and Scheduling Profiles as *"two supported ways to configure"* the scheduler. **In current upstream Kubernetes the Policy model has been removed, not deprecated.** The draft handles this well — it teaches Predicates/Priorities as *older names for the two steps* rather than as a currently-selectable option, which is true under both the snapshot and current upstream. **No change needed to the prose.** Recorded so that a future retroactive sweep does not "helpfully" re-align it to the snapshot's framing and reintroduce the error.

### ⚑ Book-level: the domain-allocation alarm has materially eased

Chapter 5's manifest raised this as a blocking pre-Chapter-6 item. Chapter 7's number changes the arithmetic, so the ledger should be updated rather than left to alarm:

| Chapter | Claimed | Objective |
|---|---|---|
| Ch 2 — Containerization | ~9% | D1.1 |
| Ch 3 — Cluster architecture | ~6% | D1.1 |
| Ch 4 — Objects | ~6% | D1.1 |
| Ch 5 — Pods | 7% | D1.1 |
| **Ch 7 — Scheduling** | **5%** | **D1.3** |
| **Subtotal** | **33% of 44%** | |

That leaves **11 points for Chapter 6**, not the 16 Chapter 5's manifest projected. Eleven is large but defensible for the chapter that carries Deployments, ReplicaSets, StatefulSets, DaemonSets and Jobs — it is no longer "larger than Chapters 3, 4 and 5 combined." **The rebalancing decision is no longer blocking; the disclosure decision still is.**

On disclosure, Chapter 7 is the **first chapter to fix the problem in the right direction and the first to break the house form in the wrong one.** Its metadata line moves the authored-allocation disclosure into a dedicated italic line beneath — clearer for the reader than any predecessor. But it drops the 44% domain weight and both source tags that Chapters 2 and 5 carry inline, which Stage 6 flagged and revision did not act on. **The content of Chapter 7's disclosure is the best in the book; the form is the least conformant.** Conform the form, keep the content, and make that the pattern `reconcile.py` sweeps the other five to.

### ⚑ Ethical-guardrail status — Chapter 7

| Chapter | Guardrail #3 (strawmanning) | Guardrail #8 (frequency claims) |
|---|---|---|
| Ch 1 | pass | pass |
| Ch 2 | pass | pass — models the compliant phrasing |
| Ch 3 | pass | **FAIL — open** (six unverifiable exam-frequency assertions) |
| Ch 4 | pass | BORDERLINE (five practitioner-prevalence superlatives) |
| Ch 5 | pass | BORDERLINE (four exam-frequency assertions) |
| **Ch 7** | ⚑ **FAIL — new, single instance, L1113** | BORDERLINE (four unhedged "most common error" superlatives) |

**Guardrail #3 is a new failure mode for this book** and it is the first of its kind in seven chapters. The nearest precedent, `chapter-01:200` ("a disclosure most study guides skip"), is materially different: it claims competitors *omit* something and then supplies it. L1113 claims they *teach it badly*. Integration's one-clause rewrite fixes it.

**Guardrail #8 is now three chapters running.** Chapter 3's finding is still open, Chapters 4, 5 and 7 have each drifted back. This has stopped being a per-chapter observation and become a house-style question the author should rule on once: either the "most candidates get this wrong" register is sanctioned (in which case Chapter 3's finding closes and the skill's Voice Alignment section is the authority) or it isn't (in which case four chapters need a hedging sweep). **Six words per instance either way. It is the ruling that's overdue, not the edit.**

Everything else on the Part 14 checklist passes, several unusually well: no statistics appear anywhere in the chapter; three well-formed uncertainty signals (preemption, the spread-constraint scale-down limitation, and `PodFitsResources`-is-only-an-example); and the **v5.7 subject-dignity guardrail is clean** — the Logbook Entry is the chapter's only extended consequence narrative and every wry beat in it lands on the practitioners, who are in the room.

---

## Retrieval-practice ledger

**7 tagged in-budget items · graded pool 32 (15 Bearings + 17 Practice) · rate = 21.9%.** B3's rung for Chapter 7 is **20%. Cleared.** Three further tagged items sit in Soundings (Q3, Q4, Q6), excluded from the budget by B3 but doing the spacing work.

**Chapter 7 draws from four predecessors** — Ch 3, 4, 5 and 6. Chapter 5 drew from three, Chapter 4 from two, Chapter 3 from one. The breadth is still increasing chapter over chapter.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| requests vs limits; which one the scheduler reads | ch 5 §8 | **ch 7** — Soundings Q3 *(excluded from budget)* |
| a Pod is scheduled once; it is not moved | ch 5 §4 | **ch 7** — Soundings Q4 *(excluded from budget)* |
| the loop creates a Pod it cannot place | ch 6 §1 | **ch 7** — Soundings Q6 *(excluded from budget)* ⚠ |
| request is the scheduler's input; limit is the kubelet's ceiling | ch 5 §8 | **ch 7** — Bearings #1 Q3 |
| ReplicaSet creates a Pod that cannot be placed | ch 6 §1 | **ch 7** — Bearings #1 Q5 ⚠ |
| label selectors — direction inverts for node selection | ch 4 §5 | **ch 7** — Bearings #2 Q1 |
| scheduled once, never rescheduled — replaced, not moved | ch 5 §4 | **ch 7** — Practice Q5 |
| the scheduler records; the kubelet starts | ch 3 §2 | **ch 7** — Practice Q6 |
| set-based selector operators `in`, `notin`, `exists` | ch 4 §5 | **ch 7** — Practice Q12 |
| DaemonSet one-per-node needs no anti-affinity | ch 6 §7 | **ch 7** — Practice Q15 ⚠ |

⚠ **= target is unshipped.** See the Chapter 6 debt block below.

**Quality notes, mostly favourable.**

- **Practice Q5 is the best-designed retrieval item in the chapter.** It takes Chapter 5's scheduled-once rule, which Chapter 5 taught with a node-*failure* motivation, and re-asks it with a strictly *better* opportunity available. Same rule, opposite emotional pull, identical answer. That is discrimination work, not recall.
- **Practice Q15 is a discrimination question wearing a retrieval tag, and the answer key says so** — "'the Pods end up spread out' and 'a spreading constraint was enforced' are not the same claim." Naming the distinction inside the key is a technique the earlier chapters don't use and it is worth propagating.
- **Bearings #2 Q1 is the cleanest conceptual seam so far.** It doesn't test whether the reader remembers selectors; it tests whether they noticed the subject and object swapped. The answer key's "if this felt backwards while reading §3, that reaction was correct and worth keeping" validates the reader's confusion instead of correcting it.
- **✅ Chapter 5's flagged defect is fixed.** Chapter 5's ledger recorded that retrieval tags appeared only on stems, not in answer keys, and recommended matching Chapter 4. **Chapter 7's keys name the source chapter in the explanation body** ("This is the same rule you learned in Chapter 5…", "Chapter 4 publishes the v1.22 fact itself"). A reader who misses an item is told where to go back to. Closed.

**⚑ One preamble/rubric mismatch, low cost.** The Soundings preamble says "Three of them ask you to retrieve something specific from Chapters 5 and 6," but the 0–2 rubric sends the reader only to "Chapter 5 §8 and Chapter 5 §4." Q6's framing is Chapter 6's. The rubric isn't wrong — `chapter-05:551` does cover the replica-shortfall case — just narrower than the preamble promised. Add Ch 6 §1 to the rubric, or drop "and 6."

### ⚑ The Chapter 6 debt — four retrieval items and two assertions point at withdrawn text

`git log` shows `2a78912 Chapter 6: drafted via pipeline` followed by `2bb971b Chapter 6: withdraw truncated draft pending re-run`. `Book-KCNA/` ships chapters 01–05 only. This ledger is the right place to hold the debt, because it survives the re-draft in a way an `AUTHOR-REVIEW` comment in Chapter 7 does not.

**Chapter 6 now owes Chapter 7 six specific things.** Four are retrieval targets; two are assertions about what Chapter 6 *said*, which is the riskier category:

| # | What Chapter 7 assumes | Where |
|---|---|---|
| 1 | Ch 6 **§1** covers Deployments/ReplicaSets and the ReplicaSet's create-the-missing-Pod behaviour | Soundings Q6, Bearings #1 Q5, §5 back-bearing |
| 2 | Ch 6 **§7** covers DaemonSets and their one-per-node distribution | Practice Q15, §4 back-bearing |
| 3 | Ch 6's **Voyage Ahead ends on the scheduler gap** — "the one thing the control loop cannot do" | §1 opening (L96) |
| 4 | Ch 6 **§7 plants the DaemonSet-tolerations tease** — "you'd already met the mechanism in disguise" | §4 callback (L524–526) |
| 5 | Ch 6 exists as the third of "Chapters 4 through 6" | Why This Chapter Matters (L98) |
| 6 | Ch 6 instantiates the control loop visibly enough to carry §7's "same shape as every controller in Chapter 6" | §7 (L862) — **and see Rule 6 note A; this should point at Ch 3 §6 instead** |

Items **3 and 4 are the blocking ones.** The ch-07 outline recorded, from the now-withdrawn draft, that Chapter 6's closing did both — including naming the DaemonSet's tolerations as the mechanism already seen in disguise. But a re-run is not obliged to reproduce a withdrawn sentence.

**Recommend all six be added to `ch-06/outline.md` § *What this chapter owes forward* before the harvest re-runs**, and both §-numbers re-verified after. Otherwise Chapter 7 ships two callbacks to sentences nobody wrote.

### Cross-cutting themes — status after Chapter 7

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **Labels/selectors as the universal join** | Ch 4 §5 | Ch 5 · ✅ **Ch 7 ×2 — first PLANNED retrieval** | Ch 6, Ch 9, Ch 10 |
| **The control loop** (B3 headline) | Ch 3 §6 | Ch 4 · Ch 5 · ⚑ **Ch 7 §7 — unplanned, paraphrased, mis-pointed** | Ch 6, **Ch 11 (still unbeared)**, Ch 15, Ch 17 |
| **Namespaced vs cluster-scoped** | Ch 4 §3 | Ch 5 §6 — ⚑ **Ch 7 missed a free one** (Rule 6 note B) | Ch 12 §3, Ch 10, Ch 11 |
| **The absent-component pattern** | Ch 3 §4, named | — *(still zero, four chapters on)* | Ch 10 ×2, Ch 13, Ch 17 |
| **"Kubernetes defines an interface, the ecosystem implements it"** | Ch 2 §4, named | ⚑ still zero named recurrences | Ch 9 (CNI), Ch 11 (CSI), Ch 17 §4 |

**Chapter 7 is the first chapter to retrieve a theme it was *told* to retrieve.** `label-selector.md` bears the universal-join theme to Chapters 6, 7, 9 and 10; Chapter 7 is the first of those to land, and it lands twice (§3 in prose, Practice Q12 graded). Chapters 4 and 5's theme retrievals were all unplanned — welcome, but not evidence the bearings work. **This one is.**

**⚑ Still retrieved by paraphrase, not by name — and the deadline is now close.** Chapter 7 §3 does the universal-join work without using `label-selector.md`'s canonical string ("the label selector is the core grouping primitive in Kubernetes"), exactly as Chapter 5 did with the namespaced/cluster-scoped string. Two downstream chapters have now each invented their own paraphrase of a string that was fixed precisely to prevent that. **The coinage decision was due before Chapter 10 drafts; three chapters remain.**

**✅ One escalation has paused.** Chapter 5's ledger raised the `reconciliation` gap as worsening: the book was grading readers on a word Chapter 3 promised to define and hasn't. **Chapter 7 does not use the word at all** — I grepped the draft, zero occurrences — despite §7 describing the mechanism in full. The gap has not closed, but it has stopped growing, and Chapter 7 shows the description can be written without the term. The one-appositive fix at Chapter 3's ★ Fixed Point remains the right close.

### Forward commitments — one discharged, one overdue, three new

| # | Commitment | Status |
|---|---|---|
| 1 | Ch 13 must carry a Ch 8 retrieval item (version skew) | **OPEN** — untouched |
| 2 | Ch 11 must retrieve the control loop | ⚑ **OPEN, now four chapters overdue.** Ch 3, 4, 5 and 7 have each passed it forward |
| 4 | Ch 12 must **derive** the RBAC 2×2 from the namespaced boundary | **OPEN** |
| 5 | Ch 9 must retrieve the Pod IP / shared namespace | **OPEN** — Ch 7 §5 bears to Ch 9 but on distribution, not on the IP |
| 6 | Ch 13's method must be "read the phase before you read the logs" | **OPEN** — and Ch 7 adds a second, compatible half; see #10 |
| 7 | Ch 6 must open on "if Pods are designed to be replaced, who does the replacing?" | **OPEN** — folded into the six-item Chapter 6 debt above |
| 8 | Ch 7, 13, 17, 18 must each retrieve requests/limits | ✅ **Ch 7's quarter DISCHARGED** at §2 — the first of four. Ch 13, 17, 18 still open |
| 9 | **Ch 13 must diagnose `Pending` as a filter problem vs a score problem** | **NEW.** §7's ⚓ publishes the diagnostic question outright: *"is this a filter that excluded every node, or a score that ranked the wrong one first?"* — with the symptom pair that separates them. Ch 13 should use that framing, not invent one |
| 10 | **Ch 13 must distinguish `Pending`-from-capacity from `Pending`-from-taint** | **NEW.** §4 closes on it explicitly: the two "look identical from the outside until you go and read the events" |
| 11 | **Ch 17 must collect the pluggable-scheduler socket** | **NEW.** §6 names `schedulerName` and stops, bearing the extension-points story to Ch 17. Correctly scoped — Ch 7 does *not* pre-collect the four-socket synthesis Ch 17's secondary Zenith reserves |
| 12 | **Ch 8 must open on `node.kubernetes.io/unschedulable`** | **NEW.** §4 and the Voyage Ahead both plant it twice as "an administrative act," and the Voyage Ahead makes it Chapter 8's named opening move |

---

## Operator notes

1. **⚑ The write path is broken and this is the fifth manifest to say so.** Nothing in `certcomp` parses `=== WRITE` / `=== APPEND`; `certcomp/tools/` does not exist, so the materializers Chapters 4 and 5 supplied were never even saved. Replay order: **ch-01 → ch-03 → ch-04 → ch-05 → ch-07.** Script below.
2. **✅ Do NOT run a snapshot materializer for Chapter 7.** All 16 cited snapshots are already in `sources/`. This is the first chapter since the failure appeared that needs no recovery step, and it is worth confirming *why* it worked here before assuming it is fixed everywhere.
3. **Blocking, and it outranks everything in this manifest: revision applied nothing** (Integration Finding 0). Every glossary definition below is inherited from a draft carrying unremediated fact-accuracy findings. Two related plumbing causes are named in the integration report and are cheap: `context_packer.py:216` still maps `draft_voice → draft-voice.md` after `apply_voice_swap()` renamed it to `draft-v1.md`, and `draft-v2-prevoice.md` is a 68-line truncated artifact.
4. **Blocking before the Chapter 6 re-run:** add the six-item debt table to `ch-06/outline.md` § *What this chapter owes forward*, then re-verify Chapter 7's §1 and §7 pointers after the harvest.
5. **Should fix before this chapter ships:** the guardrail #3 clause at L1113 (one clause), and the 15 British spellings — L113 sits in *What You'll Learn* and L1042 in a graded answer key, so both are reader-visible. The corpus is 61/0 American across five chapters.
6. **Chapter 2 has now been unaudited for five chapters** — the oldest open item in the book. Chapter 7 back-bears to Ch 2 §7 twice (RuntimeClass) and discharges half of Chapter 2's own forward pointer, and Chapter 2 still has no glossary section to record any of it.
7. **`chapter-02:807`'s `§3` token** (Integration Finding 2) — endorsed, needs author sign-off because it edits shipped text. One-token deletion.
8. **Append-only has a cost, stated plainly.** Six rows in earlier chapters' sections need *editing*, not appending — `kube-scheduler`, `binding`, `Pending`, `resource request`, `ResourceQuota`, and `Pod lifetime`. They are recorded in the append block under "Status changes to existing rows" for the reconcile pass, and `resource-request.md` needs the shard edit under "Proposed shard update."

### Materializer — replay the KB blocks (ch-01 → ch-07)

```python
# save as certcomp/tools/replay_kb_blocks.py
import re, sys
from pathlib import Path
sys.stdout.reconfigure(encoding="utf-8")

BOOK = Path(r"C:\dev\lodestar\Book-KCNA")
MANIFESTS = [BOOK / ".pipeline-state" / c / "kb-manifest.md"
             for c in ("ch-01", "ch-03", "ch-04", "ch-05", "ch-07")]  # order is load-bearing

WRITE  = re.compile(r"^=== WRITE (?P<p>.+?) ===\r?\n(?P<b>.*?)^=== END WRITE ===\r?$",
                    re.MULTILINE | re.DOTALL)
APPEND = re.compile(r"^=== APPEND (?P<p>.+?) ===\r?\n(?P<b>.*?)^=== END APPEND ===\r?$",
                    re.MULTILINE | re.DOTALL)

for man in MANIFESTS:
    if not man.exists():
        print(f"SKIP (absent): {man}"); continue
    text = man.read_text(encoding="utf-8")
    for rx, mode in ((WRITE, "w"), (APPEND, "a")):
        for m in rx.finditer(text):
            tgt = Path(m.group("p").strip().replace("/", "\\")).resolve()
            tgt.parent.mkdir(parents=True, exist_ok=True)
            body = m.group("b")
            if not body.endswith("\n"):
                body += "\n"
            with open(tgt, mode, encoding="utf-8", newline="\n") as fh:
                fh.write(body)
            print(f"{'WROTE ' if mode=='w' else 'APPEND'} {tgt.relative_to(BOOK)}")
```
```

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 7 additions — Assigning the Berth (2026-08-24)

**Appended, not merged.** This file is append-only under the current pipeline. Book
assembly merges alphabets mechanically.

Terms contributed: **56** — 49 defined · 2 partial · 5 reserved · 6 status corrections.

**Citation health: clean.** All 16 snapshots cited by this chapter resolve to files in
`Book-KCNA/sources/`. Unlike Chapter 5, no entry below rests on an unmaterialized fetch.
Two entries rest on *untagged* claims and are marked ⚑ where they occur.

## ⚑ Status changes to EXISTING rows above (apply at reconcile — cannot be done by append)

| Row | Current text | Correction | Evidence |
|---|---|---|---|
| **kube-scheduler** (Ch 3) | "Watches for newly created Pods with no assigned node and selects a node." | **EXTENDED at Ch 7 §1** — the selection algorithm is now published: a 2-step operation, filtering then scoring, followed by binding. Ch 3 deliberately withheld it. | Ch 7 §1 |
| **binding** (Ch 3, surfaced) | "notifies the API server about its decision, in a process called binding" | **CLOSED at Ch 7 §1 and made concrete at §6** — binding is physically the write of `.spec.nodeName`. | Ch 7 §6 [source: k8s-docs-daemonset-2026-08-24] |
| **`Pending`** (Ch 5, as a Pod phase) | "the Pod has been accepted by the cluster, but one or more of its containers has not been set up and made ready to run… includes time spent waiting to be scheduled" | **EXTENDED at Ch 7 §2** — the scheduling reading: `Pending` is a **state, not an error**; nothing times out, nothing retries with looser constraints, and the wait is indefinite. | Ch 7 §2 |
| **resource request** (Ch 5) | "the kube-scheduler uses this information to decide which node to place the Pod on" | **EXTENDED at Ch 7 §2** — requests are **booked**, not measured: "the scheduler books; it does not measure," and it does not over-subscribe Allocatable. Not a contradiction of Ch 5's "a request is a floor, not a ceiling" — that is the kubelet's view, this is the scheduler's. | Ch 7 §2 |
| **ResourceQuota** (Ch 4, reserved → Ch 8) | reserved → Ch 8, "✅ beared" | **CONFIRMED.** Ch 7 §2 names it again and re-bears to Ch 8. Still reserved; Ch 8 owns the definition. | Ch 7 §2 |
| **Pod lifetime / scheduled once** (Ch 5) | "scheduled once in its lifetime"; "never 'rescheduled' to a different node" | **CONFIRMED and RETRIEVED.** Ch 7 §1 restates it from the same snapshot and Practice Q5 grades it against a *better-opportunity* scenario rather than Ch 5's node-failure one. | Ch 7 §1, Practice Q5 |

---

## Tier 1 — Defined at Chapter 7 (prose inherited verbatim)

### A

**affinity operators** — node affinity supports `In`, `NotIn`, `Exists`, `DoesNotExist`,
`Gt` and `Lt`. [source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §3)
> Compare `nodeSelector`'s single implicit "equals." The chapter's framing: this operator
> set plus the soft mode are "the two things affinity adds."
> ⚑ **Consolidation available.** Chapter 4 already published `In`, `NotIn`, `Exists`,
> `DoesNotExist` as the `matchExpressions` vocabulary (see `label-selector.md`). Node
> affinity's operator set **is** that vocabulary plus two numeric operators. Chapter 7
> never says so. See the Chapter 7 manifest, Rule 6 note C.

**Allocatable** — "'Allocatable' on a Kubernetes node is defined as the amount of compute
resources that are available for pods," and "the scheduler treats 'Allocatable' as the
available `capacity` for pods." The scheduler **does not over-subscribe** Allocatable.
[source: k8s-docs-node-allocatable-2026-08-24] (Ch 7 §2)
> Practical rule the chapter states: do the arithmetic against Allocatable, not against the
> machine's total RAM.

### B

**binding** ★ — the scheduler's third act. "The scheduler notifies the API server about its
decision, and *that* is what the word binding names."
[source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §1)
> **Concretely** — the physical content of the operation — the default scheduler "binds the
> Pod to the target host by **setting the `.spec.nodeName` field**."
> [source: k8s-docs-daemonset-2026-08-24] (Ch 7 §6)
> ★ Fixed Point wording, canonical retrieval string: **"The scheduler filters, then scores,
> then binds. Filtering produces the feasible set; scoring ranks it; binding is a
> notification to the API server. The kubelet on the chosen node is what actually starts
> the containers."**
> **Closes Chapter 3's reservation.** `control-plane-components.md` recorded binding as
> named-but-unexplained and beared the algorithm to Ch 7.

**built-in node-condition taints** — "The control plane, using the node controller,
automatically creates taints with a `NoSchedule` effect for node conditions. **The
scheduler checks taints, not node conditions, when it makes scheduling decisions.** This
ensures that node conditions don't directly affect scheduling."
[source: k8s-docs-taints-tolerations-depth-2026-08-24] (Ch 7 §4)

| Taint key | Effect |
|---|---|
| `node.kubernetes.io/not-ready` | `NoExecute` |
| `node.kubernetes.io/unreachable` | `NoExecute` |
| `node.kubernetes.io/disk-pressure` | `NoSchedule` |
| `node.kubernetes.io/memory-pressure` | `NoSchedule` |
| `node.kubernetes.io/pid-pressure` | `NoSchedule` |
| `node.kubernetes.io/unschedulable` | `NoSchedule` |
| `node.kubernetes.io/network-unavailable` | `NoSchedule` |

[source: k8s-docs-daemonset-2026-08-24]
> Plus `node.cloudprovider.kubernetes.io/uninitialized`, added when the kubelet starts with
> an external cloud provider [source: k8s-docs-taints-tolerations-depth-2026-08-24].
> The chapter's gloss on the design: node health "doesn't get a special channel into the
> scheduler; it gets translated into the *same* mechanism you'd use by hand."
> **Links to `node-components.md`:** `k8s-docs-nodes-2026-08-23` lists the node Conditions
> (Ready, DiskPressure, MemoryPressure, PIDPressure, NetworkUnavailable). Five of the seven
> taints above are those conditions translated. Chapter 7 does not draw the line explicitly.

### D

**dedicated nodes (the two-mechanism pattern)** ★ — to reserve a set of nodes for a group
*and* ensure that group's Pods only use them, you need **both** directions: a taint to keep
everyone else off, and a label plus affinity (or `nodeSelector`) to pull the right work on.
The documentation prescribes exactly this — "you should additionally add a label similar to
the taint to the same set of nodes… and the admission controller should additionally add a
node affinity to require that the pods can only schedule onto nodes labeled with
`dedicated=groupName`." [source: k8s-docs-taints-tolerations-depth-2026-08-24] (Ch 7 §4)
> **Taints exclude. Affinity attracts. A dedicated-node setup needs both.** The chapter
> calls this "the single most transferable operational fact in this chapter," and the §4
> Logbook Entry is built entirely on the failure mode of using only one half.

**`DoNotSchedule`** — the default value of a topology spread constraint's
`whenUnsatisfiable`; "tells the scheduler not to schedule the Pod."
[source: k8s-docs-topology-spread-constraints-2026-08-24] (Ch 7 §5)
> A **hard** rule — a filter. Paired with `ScheduleAnyway`, this is the fourth appearance of
> the required/preferred distinction in the chapter under a fourth set of names.

### F

**feasible node** — "The nodes that meet a Pod's scheduling requirements are called feasible
nodes." [source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §1)

**filtering** — step one of the 2-step operation. "Finds the set of nodes where it is
feasible to schedule the Pod. After this step the node list contains any suitable nodes,
often more than one. **If the list is empty, that Pod isn't yet schedulable.**"
[source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §1)
> Older name: **Predicate.** See that entry.

### I

**`IgnoredDuringExecution`** — "if the node's labels change after Kubernetes schedules the
Pod, **the Pod continues to run**." [source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §3)
> 🪢 Mnemonic, verbatim and worth keeping as the decoding rule for the whole field family:
> "Read `requiredDuringSchedulingIgnoredDuringExecution` as two clauses joined at the seam:
> **required when scheduling, ignored once running.** The word is thirty-nine characters;
> the meaning is six. Every one of these field names decomposes the same way: first half is
> what happens at placement, second half is what happens afterwards."

### K

**`kubectl get nodes --show-labels`** — lists nodes with their labels.
[source: k8s-docs-assign-pods-nodes-task-2026-08-24] (Ch 7 §3)

**`kubectl label nodes <node> <key>=<value>`** — attaches a label to a node.
[source: k8s-docs-assign-pods-nodes-task-2026-08-24] (Ch 7 §3)
> ⚑ **Free retrieval sitting unused.** This command takes no `-n` flag because Nodes are
> cluster-scoped — `cluster-scoped-resource.md`'s ★ Fixed Point names Nodes explicitly.
> Chapter 7 never draws the connection. One clause closes it.

**`kubectl taint nodes <node> <key>=<value>:<EFFECT>`** — applies a taint. **The removal
form is the same command with a trailing minus sign:**
`kubectl taint nodes node1 key1=value1:NoSchedule-`
[source: k8s-docs-taints-tolerations-depth-2026-08-24] (Ch 7 §4)
> The chapter's warning, worth keeping: the trailing minus is "easy to miss and easy to
> mistype."

### M

**`maxSkew`** — "describes the degree to which Pods may be unevenly distributed. Must be
specified and must be greater than zero."
[source: k8s-docs-topology-spread-constraints-2026-08-24] (Ch 7 §5)

**`minDomains`** — optional; "indicating a minimum number of eligible domains" — a domain
being "a particular instance of a topology," and an eligible domain "one whose nodes match
the node selector." [source: k8s-docs-topology-spread-constraints-2026-08-24] (Ch 7 §5)

### N

**`NoExecute`** — "the only effect that touches Pods already on the node. Pods that do not
tolerate the taint are **evicted immediately**. Pods that tolerate the taint without
specifying `tolerationSeconds` remain bound forever. Pods that tolerate the taint *with* a
specified `tolerationSeconds` remain bound for that long, after which the node lifecycle
controller evicts them." [source: k8s-docs-taints-tolerations-2026-08-23] (Ch 7 §4)

**`NoSchedule`** — "no new Pods will be scheduled on the tainted node unless they have a
matching toleration. **Pods currently running on the node are not evicted.**"
[source: k8s-docs-taints-tolerations-2026-08-23] (Ch 7 §4)
> ⚠ The classic error is that `NoSchedule` evicts. It does not — "the word *Schedule* in
> the name is telling you so."

**node affinity** — "functions like the `nodeSelector` field but is more expressive and
allows you to specify soft rules." [source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §3)
> Adds exactly two things over `nodeSelector`: a richer operator set (see **affinity
> operators**) and two hardness levels (see **`requiredDuringScheduling…`** and
> **`preferredDuringScheduling…`**).
> ⚠ **The misreading `ch07-fig02` exists to prevent:** node affinity is *not* simply "more
> powerful `nodeSelector`" on a single upgrade path. **`nodeSelector` and required node
> affinity fail identically** — no matching node, no placement, Pod sits in `Pending`.
> Expressiveness and hardness are **independent axes**; only one of the six cells is soft.

**node labels** — nodes have labels; you can attach them manually, "and Kubernetes also
populates a standard set of labels on all nodes in a cluster."
[source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §3)
> **The direction inversion, which is the section's real content:** every previous use of
> labels in this book has been *an object selecting a set of Pods* (a Service selecting
> backends, a ReplicaSet selecting the Pods it owns). Here it is *a Pod selecting nodes*.
> Same mechanism, opposite subject and object. See `label-selector.md`.
> **Isolation caution:** "if you use labels for node isolation, choose label keys the
> kubelet cannot modify. The NodeRestriction admission plugin prevents the kubelet from
> setting labels with a `node-restriction.kubernetes.io/` prefix."
> [source: k8s-docs-assign-pod-node-2026-08-23] "A node that can label itself into a
> privileged group is not an isolation boundary."

**node labels — the standard set** — includes `kubernetes.io/hostname` (populated by the
kubelet with the node's hostname), `topology.kubernetes.io/zone`,
`topology.kubernetes.io/region`, `kubernetes.io/os` and `kubernetes.io/arch`.
[source: k8s-docs-well-known-labels-2026-08-24] (Ch 7 §3)
> The first two become load-bearing in §5 as `topologyKey` values.

**`nodeName`** ★ — "a more direct form of node selection than affinity or `nodeSelector`."
A field in the Pod spec; "**if it is not empty, the scheduler ignores the Pod**" and the
kubelet on the named node tries to place the Pod there.
[source: k8s-docs-assign-pod-node-2026-08-23] Using `nodeName` **overrules** using
`nodeSelector` or affinity and anti-affinity rules.
[source: k8s-docs-assign-pod-node-depth-2026-08-24] (Ch 7 §6)
> **Not the most forceful way of asking — the absence of asking.** The API does let you
> specify a node when you create a Pod, "but this is unusual and is only done in special
> cases" [source: k8s-docs-kube-scheduler-2026-08-23].
> **It is the field binding writes to.** Setting it by hand "means filling in the
> scheduler's answer before it was asked the question."
> See **`OutOfmemory` / `OutOfcpu`** for the failure mode.

**`nodeSelector`** — "the simplest recommended form of node selection constraint." You name
the node labels you want the target node to have, and "**Kubernetes only schedules the Pod
onto nodes that have each of the labels you specify.**"
[source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §3)
> **Each, not any.** An AND of exact matches, and nothing else — no "one of these," no
> "anything except," no "greater than."
> The chapter's selection advice: "Reach for `nodeSelector` first… a soft rule you didn't
> need is a rule someone will misread as a guarantee eighteen months from now."

**`nodeSelectorTerms` / `matchExpressions` combination rules** — "if you specify multiple
terms in `nodeSelectorTerms`, the Pod can be scheduled if **one** of the terms is satisfied
— terms are ORed; if you specify multiple expressions in a single `matchExpressions` field,
the Pod can be scheduled **only if all** the expressions are satisfied — expressions are
ANDed." [source: k8s-docs-assign-pod-node-depth-2026-08-24] (Ch 7 §3)

### O

**`OutOfmemory` / `OutOfcpu`** — the failure reasons a Pod gets when `nodeName` names a node
that cannot fit it. "If the named node does not have the resources to accommodate the Pod,
the Pod will fail and its reason will indicate why, for example OutOfmemory or OutOfcpu."
[source: k8s-docs-assign-pod-node-depth-2026-08-24] (Ch 7 §6)
> **The one placement failure in the chapter that isn't `Pending`.** Every other failure
> leaves a Pod waiting; this one fails outright, "because the feasibility check that would
> have caught the problem in advance never happened."
> Two sibling failure modes from the same source: "if the named node does not exist, the Pod
> will not run, and in some cases may be automatically deleted"; and "node names in cloud
> environments are not always predictable or stable."

### P

**`Pending` (the scheduling reading)** — extends Ch 5's Pod-phase entry. "If none of the
nodes are suitable, **the Pod remains unscheduled until the scheduler is able to place it**"
[source: k8s-docs-kube-scheduler-2026-08-23]; its phase is `Pending`, which covers "time a
Pod spends waiting to be scheduled" [source: k8s-docs-pod-lifecycle-2026-08-23]. (Ch 7 §2)
> ⚠ **Navigational Hazards, verbatim — the canonical retrieval string:** "`Pending` is a
> **state**, not an error. It is the honest report of a Pod that has been accepted by the
> cluster and has nowhere to run yet. **No component is quietly retrying it with looser
> constraints, and no timer will eventually convert it into a failure.**"
> The chapter's structural observation, which Ch 17 retrieves: an unschedulable Pod is "a
> standing, machine-readable statement that the cluster is short of somewhere to put work."

**`PodFitsResources`** — the documentation's own example of a filter; "checks whether a
candidate node has enough available resources to meet a Pod's specific resource
**requests**." [source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §2)
> 🔭 Scope caution the chapter states explicitly: it is named "as *an example* of a filter,
> not as the only one." Resources are one feasibility test among several.

**Pod affinity (inter-Pod)** — "schedule this Pod where a Pod carrying that label already
is." Inter-pod affinity and anti-affinity "let you constrain Pods against **labels on other
Pods**." [source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §5)
> Useful for co-locating things that talk to each other constantly.

**Pod anti-affinity (inter-Pod)** — "do not schedule this Pod where a Pod carrying that label
already is." **The availability tool.**
[source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §5)
> In `requiredDuringSchedulingIgnoredDuringExecution` mode, "only a single Pod can be
> scheduled into a single topology domain"; in `preferredDuringScheduling…` mode "you lose
> the ability to enforce the constraint."
> [source: k8s-docs-topology-spread-constraints-2026-08-24]
> **The gap it fills:** "Redundancy is a property of a **set**, and none of the mechanisms
> so far can express a property of a set." Identical replicas from one Deployment are
> equally feasible and equally well-scored on every node, so the scheduler placing all of
> them together is a legal outcome of a decision made independently N times.

**`PreferNoSchedule`** — "the soft version of `NoSchedule`. The control plane will *try* to
avoid placing a Pod that does not tolerate the taint on the node, but it is not
guaranteed." [source: k8s-docs-taints-tolerations-2026-08-23] (Ch 7 §4)
> 🪝 Snag, verbatim: "preferences lose. Pods that don't tolerate the taint will land on a
> `PreferNoSchedule` node when nothing better is available, and that is correct behaviour,
> not a bug. **If you need 'never,' you need `NoSchedule`.**"

**`preferredDuringSchedulingIgnoredDuringExecution`** — "the scheduler **tries** to find a
node that meets the rule, but if a matching node is not available, it still schedules the
Pod." [source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §3)
> Lands in the **scoring** step, not the filtering step. That placement is the whole of §7.

**Predicate** — the older name for a **filter**: it decides whether a node is feasible.
Scheduling Policies configure the scheduler with "Predicates for filtering and Priorities
for scoring." [source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §6)
> ⚑ **Currency note, do not "correct" this.** The cached snapshot presents Scheduling
> Policies as one of two currently supported configuration methods. In current upstream
> Kubernetes the Policy model has been **removed**, not deprecated. The chapter deliberately
> teaches Predicates/Priorities as *older names for the two steps* rather than as a
> selectable option, which is true under both the snapshot and current upstream. A future
> retroactive sweep must not re-align this to the snapshot's framing.

**Priority** — the older name for a **score**: it ranks the nodes that survived filtering.
[source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §6)
> Same currency note as **Predicate**.

### R

**random tie-break** ★ — "If there is more than one node with equal scores, `kube-scheduler`
selects one of them **at random**." [source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §1)
> Not lowest hostname, not least loaded, not round-robin.
> The chapter's conceptual payload, which is why this one-sentence fact gets a section:
> "the scheduler is not trying to be optimal in a way you can reason about or predict. So
> influencing placement is not a matter of understanding the algorithm well enough to
> out-think it. It's a matter of **saying something**."

**`requiredDuringSchedulingIgnoredDuringExecution`** — "the scheduler **can't** schedule the
Pod unless the rule is met." [source: k8s-docs-assign-pod-node-2026-08-23] (Ch 7 §3)
> Lands in the **filtering** step. Fails identically to `nodeSelector`.

### S

**`ScheduleAnyway`** — "tells the scheduler to still schedule it while prioritizing nodes
that minimize the skew."
[source: k8s-docs-topology-spread-constraints-2026-08-24] (Ch 7 §5)
> A **soft** rule — a score.

**scheduler plugins / Scheduling Profiles** — Profiles configure the scheduler with "plugins
that implement different scheduling stages, including `QueueSort`, `Filter`, `Score`,
`Bind`, `Reserve` and `Permit`. `kube-scheduler` can run different profiles."
[source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §6)
> Treat as "the same pipeline with more seats exposed" — two of the stage names, `Filter`
> and `Score`, are the steps from §1. Recognition depth only; the chapter does not teach
> plugin authoring.

**`schedulerName` / custom scheduler** — "`kube-scheduler` is designed so that, if you want
and need to, **you can write your own scheduling component and use that instead**."
[source: k8s-docs-kube-scheduler-2026-08-23] Pods can name which scheduler should handle
them; a DaemonSet exposes `.spec.template.spec.schedulerName` for the purpose.
[source: k8s-docs-daemonset-2026-08-24] (Ch 7 §6)
> The exam-relevant payload is one sentence: "the seat is pluggable — the default scheduler
> is a default, not a fixture." Collected with its siblings at Ch 17.

**Scheduling Policies** — the older of two documented ways to configure filtering and scoring
behaviour; uses **Predicates** and **Priorities**.
[source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §6)
> Same currency note as **Predicate**.

**scoring** — step two of the 2-step operation. "The scheduler assigns a score to each node
that survived filtering, based on the active scoring rules, and then assigns the Pod to the
node with the highest ranking." [source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §1)
> For preferred affinity rules you can specify a `weight` between 1 and 100 per instance;
> "the resulting sum is added to the node's score from other scoring functions; nodes with
> the highest total score win."
> [source: k8s-docs-assign-pod-node-depth-2026-08-24] Arithmetic not required for this exam.
> Older name: **Priority.**

### T

**taint** ★ — lives on the **node**. "One or more taints are applied to a node; this marks
that the node should not accept any Pods that do not tolerate the taints."
[source: k8s-docs-taints-tolerations-2026-08-23] (Ch 7 §4)
> The framing that makes the direction stick: "Node affinity is a property of Pods that
> attracts them to a set of nodes… **Taints are the opposite — they allow a node to repel a
> set of pods.**" [source: k8s-docs-taints-tolerations-2026-08-23]
> **Multiple taints:** "start with all of a node's taints, then ignore the ones for which
> the pod has a matching toleration; the remaining un-ignored taints have the indicated
> effects on the pod." [source: k8s-docs-taints-tolerations-depth-2026-08-24] Tolerating
> three of four taints does not get you aboard.

**taint / toleration matching** — stated flat, as the chapter's — Dead Reckoning block:
"A toleration matches a taint when the keys are the same and the effects are the same, and
one of two operator conditions holds. If the operator is `Exists`, no value should be
specified. If the operator is `Equal`, the values must be equal. Two wildcards modify this.
If the key is empty, the operator must be `Exists`, which matches all keys and all values —
the effect must still match. An empty effect matches all effects with the given key."
[source: k8s-docs-taints-tolerations-2026-08-23] (Ch 7 §4)

| Toleration | Matches | Notes |
|---|---|---|
| key + effect + `operator: Equal` + value | same key, same effect, same value | the exact-match case |
| key + effect + `operator: Exists` | same key and same effect, **any value** | do not specify a value with `Exists` |
| empty key + `operator: Exists` + effect | **all** taints with that effect, any key, any value | empty key *requires* `Exists` |
| key + `operator: Exists` + **empty effect** | all effects for that key | effect wildcard |

**toleration** ★ — lives on the **Pod**. "Tolerations are applied to Pods, and they allow the
scheduler to schedule Pods with matching taints."
[source: k8s-docs-taints-tolerations-2026-08-23] (Ch 7 §4)
> ⚠ **The chapter's most-emphasized correction, and Integration's "most durable error in
> this material":** "**Tolerations allow scheduling but don't guarantee scheduling**: the
> scheduler also evaluates other parameters as part of its function."
> [source: k8s-docs-taints-tolerations-2026-08-23]
> "A toleration removes a veto. That is the entire extent of its power. It does not make a
> request, it does not raise a node's score, it does not reserve anything, and it does not
> create capacity."
> ★ Fixed Point wording: **"A taint is the node's refusal; a toleration is the Pod's
> exemption from that refusal. Tolerations permit — they never attract. Of the three
> effects, only `NoExecute` affects Pods that are already running."**

**toleration — the automatic 300-second default** — "Kubernetes automatically adds a
toleration for `node.kubernetes.io/not-ready` and `node.kubernetes.io/unreachable` with
`tolerationSeconds=300`, unless you or a controller set those tolerations explicitly."
[source: k8s-docs-taints-tolerations-depth-2026-08-24] (Ch 7 §4)
> Why a briefly-unreachable node doesn't instantly shed everything running on it.

**toleration — the DaemonSet case** — "the DaemonSet controller automatically adds
tolerations for all seven of the built-in condition taints to the Pods it creates." Because
it sets the `node.kubernetes.io/unschedulable:NoSchedule` toleration automatically,
Kubernetes can run DaemonSet Pods on nodes marked unschedulable; and the `NoExecute`
tolerations for `not-ready` and `unreachable` carry **no** `tolerationSeconds`, so DaemonSet
Pods on such nodes are not evicted. [source: k8s-docs-daemonset-2026-08-24] (Ch 7 §4)
> The chapter's payoff line: your log-shipping agent still reporting from a node under
> memory pressure "isn't privileged. It just tolerates everything."
> ⚑ **This is the mechanism Chapter 6 §7 teased as "already met in disguise."** Chapter 6
> is currently withdrawn; see the Chapter 7 manifest's Chapter 6 debt table.

**`tolerationSeconds`** — with `NoExecute`, "Pods that tolerate the taint *with* a specified
`tolerationSeconds` remain bound for that long, after which the node lifecycle controller
evicts them." Pods tolerating without it "remain bound forever."
[source: k8s-docs-taints-tolerations-2026-08-23] (Ch 7 §4)

**topology domain** — the region a spreading or anti-affinity rule applies within. Nodes
"that have a label with that key and identical values are considered to be in the same
topology." [source: k8s-docs-topology-spread-constraints-2026-08-24] (Ch 7 §5)
> ★ Fixed Point wording: **"Inter-Pod rules are evaluated against the labels of Pods that
> are *already placed*, within a topology domain defined by a node label (`topologyKey`).
> The domain is the part people forget — it is a variable, not a synonym for 'node.'"**

**`topologyKey`** — "the key for the node label that the system uses to denote the domain."
[source: k8s-docs-assign-pod-node-depth-2026-08-24] (Ch 7 §5)
> **The hard idea in §5, and what makes it 🟡.** Same rule, same cluster, different meaning
> depending on which label you name: with `kubernetes.io/hostname` each node is a domain;
> with `topology.kubernetes.io/zone` each zone is. In a two-zone cluster, a required
> anti-affinity rule on the zone key caps you at two placeable Pods regardless of node
> count. `ch07-fig04` exists to make exactly this visible.

**topology spread constraints** — "You can use *topology spread constraints* to control how
Pods are spread across your cluster among failure-domains such as regions, zones, nodes, and
other user-defined topology domains… This can help to achieve high availability as well as
efficient resource utilization."
[source: k8s-docs-topology-spread-constraints-2026-08-24] (Ch 7 §5)

| Field | What it says |
|---|---|
| `topologyKey` | the key of node labels; nodes with this key and identical values are in the same topology |
| `labelSelector` | Pods matching this selector are counted to determine the number of Pods in their corresponding topology domain |
| `maxSkew` | the degree to which Pods may be unevenly distributed; must be specified, must be > 0 |
| `whenUnsatisfiable` | `DoNotSchedule` (default) / `ScheduleAnyway` |

All: [source: k8s-docs-topology-spread-constraints-2026-08-24]
> 🪝 Snag, verbatim: "'Spread my replicas evenly across nodes' and 'never put two of these
> together' are different requirements. Anti-affinity states the second and only
> approximates the first."
> **Honest limitation, kept:** "There's no guarantee that the constraints remain satisfied
> when Pods are removed. For example, scaling down a Deployment may result in imbalanced
> Pods distribution." Scheduling-time constraints describe a decision, not a standing
> invariant.

**topology spread constraints — cluster defaults** — you can set defaults; "they apply to a
Pod if and only if it doesn't define any constraints in its own
`.spec.topologySpreadConstraints`, and it belongs to a Service, ReplicaSet, StatefulSet or
ReplicationController." [source: k8s-docs-topology-spread-constraints-2026-08-24] (Ch 7 §5)

### U

**unschedulable (Pod state)** — see **`Pending` (the scheduling reading)**. A Pod for which
filtering produced an empty feasible set. "If the list is empty, that Pod isn't yet
schedulable." [source: k8s-docs-kube-scheduler-2026-08-23] (Ch 7 §1–§2)

### W

**`weight` (preferred affinity)** — 1 to 100 per preferred rule instance; "the resulting sum
is added to the node's score from other scoring functions; nodes with the highest total
score win." [source: k8s-docs-assign-pod-node-depth-2026-08-24] (Ch 7 §3)

**`whenUnsatisfiable`** — see **`DoNotSchedule`** and **`ScheduleAnyway`**.
[source: k8s-docs-topology-spread-constraints-2026-08-24] (Ch 7 §5)

---

## Tier 2 — Partially defined at Chapter 7 (deliberately held to the snapshot)

**Pod overhead** — a RuntimeClass "can carry scheduling constraints, a `nodeSelector` and
tolerations, so that Pods land on nodes that support the handler, and **a Pod overhead so
the scheduler accounts for the runtime's resource cost**."
[source: k8s-docs-runtime-class-2026-08-23] (Ch 7 §2; promised at Ch 2 §7)
> ⚑ **The mechanism is NOT stated, and that is correct.** I read the snapshot directly: it
> states the overhead's *existence and purpose* and nothing about how it is applied (i.e.
> that it is added to the Pod's effective request). The chapter's `AUTHOR-REVIEW` holds the
> prose to exactly what the source supports and names the URL a fetch would need
> (`kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/`).
> **Do not write the mechanism from memory.** One fetch closes it; this is a Rule 5 success,
> not a shortfall.

**preemption / `PriorityClass`** — "If a Pod cannot be scheduled, the scheduler tries to
preempt — evict — lower priority Pods to make scheduling of the pending Pod possible."
Configured with a `PriorityClass`.
[source: k8s-docs-pod-priority-preemption-2026-08-24] (Ch 7 §2)
> **Deliberately out of scope.** The chapter's own reason for naming it anyway is worth
> preserving as a house pattern: "Register that they exist so that nothing in this chapter
> reads as a lie later." Skill Part 11's order/truth balance, executed correctly.
> The **only** circumstance in which the scheduler does something other than wait.

---

## Tier 3 — Reserved (named at Chapter 7, defined elsewhere)

| Term | Owner | Named at | Status |
|---|---|---|---|
| **Capacity** (node status) | **Ch 8** | Ch 7 §2 | ⚑ **RESERVED — and not currently closable.** `k8s-docs-nodes-2026-08-23` names Capacity and Allocatable in the node-status list but never defines Capacity or its relationship to Allocatable. Research-manifest gap **G-7C**. §2's "Some of that total is spoken for by things that aren't Pods" is the untagged claim Stage 6 flagged — the fix is a **fetch or a softening, not a tag** |
| **ResourceQuota** | **Ch 8** | Ch 7 §2 | reserved — **confirmed**; previously beared at Ch 4 §3 |
| **LimitRange** | **Ch 8** | Ch 7 §2 | reserved — new bearing |
| **NodeRestriction admission plugin** | **Ch 8** | Ch 7 §3 | reserved. Ch 7 states its effect (prevents the kubelet setting `node-restriction.kubernetes.io/`-prefixed labels) but not what an admission plugin *is*; Ch 3's `api-server-hub.md` already bears auth → authz → admission to Ch 8 |
| **`node.kubernetes.io/unschedulable` as an administrative act** | **Ch 8** | Ch 7 §4, Voyage Ahead | ⚑ reserved. The taint key and `NoSchedule` effect are tagged; the **causal** claim ("something puts that one there on purpose") is **untagged** in both places. Ch 8 owns the command that does it and the command that clears the node afterwards |

---

## ⚑ Proposed shard update — NOT applied (Rule 6)

`concepts/resource-request.md` needs two edits that a later chapter should not make silently:

1. **Downstream obligations table** — mark the **Ch 7** row `✅ DISCHARGED at Ch 7 §2
   (2026-08-24)`. Ch 13, 17 and 18 remain open. This is the first of the shard's four
   "longest forward reach in the book" obligations to land.
2. **Add a section** recording the scheduler-side semantics Chapter 5 did not have:

   > ## The scheduler's side — added at Chapter 7 §2
   >
   > A request is a **booking**. Once a Pod is placed, its requests are taken off the node's
   > available balance and stay off, whether the container ever touches the resource or not.
   > The scheduler **does not over-subscribe Allocatable**
   > [source: k8s-docs-node-allocatable-2026-08-24].
   >
   > **This does not contradict "a request is a floor, not a ceiling" above.** That is the
   > kubelet's view of a *running* container, which may exceed its request when the node has
   > spare capacity. This is the scheduler's view of *placement*, which counts the booking
   > regardless of use. Both are true at once, and holding both is what lets you diagnose
   > "the cluster has loads of free memory but my Pod won't schedule."
   >
   > ★ Ch 7 Fixed Point: **"The scheduler books; it does not measure."**

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/scheduling.md ===
# Concept: Scheduling — the two-step operation

**Home:** Chapter 7 §1 and §7 · **Competency:** D1.3 · **Status:** canonical
**Discharges:** `control-plane-components.md`'s Ch 7 obligation — "the scheduler's actual
selection algorithm. Ch 3 deliberately withholds it."

## ★ Fixed Point (verbatim — canonical retrieval string)

> **The scheduler filters, then scores, then binds. Filtering produces the feasible set;
> scoring ranks it; binding is a notification to the API server. The kubelet on the chosen
> node is what actually starts the containers.**

## The mechanism

A scheduler "watches for newly created Pods that have no node assigned; for every such Pod
it discovers, it becomes responsible for finding a node for that Pod to run on."
`kube-scheduler` is the default one and runs as part of the control plane. It selects a node
in a **2-step operation: filtering, then scoring.**
[source: k8s-docs-kube-scheduler-2026-08-23]

- **Filtering** — "finds the set of nodes where it is feasible to schedule the Pod. After
  this step the node list contains any suitable nodes, often more than one. If the list is
  empty, that Pod isn't yet schedulable."
- **Scoring** — "the scheduler assigns a score to each node that survived filtering, based
  on the active scoring rules, and then assigns the Pod to the node with the highest
  ranking."
- **Binding** — "the scheduler notifies the API server about its decision." Physically, the
  write of `.spec.nodeName` [source: k8s-docs-daemonset-2026-08-24].

🪢 **Mnemonic:** *Filter, score, bind* — three words, in the order they happen, and they are
printed on the front of the chapter.

## The boundary that must not drift

`control-plane-components.md` records this as boundary #1 and Chapter 7 preserves it exactly:
**the scheduler's arrow lands on the API server, not on the node.** Nothing in the scheduler
ever touches a container. The kubelet on the chosen node starts things "because it saw the
recorded decision. Not because the scheduler told it to."

Chapter 3 called the contrary belief "the highest-value wrong answer on the page." Chapter 7
grades it at Practice Q6 and Bearings #1 Q1, and `ch07-fig01` draws the two arrows separately
for the same reason.

## And then a coin flip

> If there is more than one node with equal scores, `kube-scheduler` selects one of them **at
> random.** [source: k8s-docs-kube-scheduler-2026-08-23]

Not the lowest hostname, not the least loaded, not round-robin. Chapter 7 spends a subsection
on a one-sentence fact because of what it implies:

> The scheduler is not trying to be optimal in a way you can reason about or predict. So
> influencing placement is not a matter of understanding the algorithm well enough to
> out-think it. It's a matter of **saying something.**

That reframes §3–§6 from "six features" into "six ways of saying something the algorithm is
obliged to honour."

## ☀️ Zenith — everything is a filter or a score

> **Every mechanism in this chapter plugs into one of exactly two slots in §1's pipeline. It
> either removes nodes from consideration — a filter — or it changes the ranking of the nodes
> that survived — a score. Six vocabularies. Two slots. That's the chapter.**

| Filters (remove nodes) | Scores (rank what remains) |
|---|---|
| requests vs Allocatable | preferred node affinity |
| `nodeSelector` | `PreferNoSchedule` |
| required node affinity | preferred inter-Pod rules |
| untolerated `NoSchedule` | `ScheduleAnyway` spread |
| untolerated `NoExecute` | other scoring plugins |
| required inter-Pod rules | |
| `DoNotSchedule` spread | |

**The recurring required/preferred pair was never four distinctions.** Required vs preferred
node affinity, `NoSchedule` vs `PreferNoSchedule`, required vs preferred inter-Pod rules,
`DoNotSchedule` vs `ScheduleAnyway` — all one question: *is this a filter, or is this a
score?* **Hard rules filter. Soft rules score.**

`nodeName` fits neither slot and is drawn outside the pipeline: "it does not narrow the
feasible set and it does not adjust a ranking. It removes the decision."

## ⚓ The diagnostic question (Ch 13 retrieves this)

> *Is this a filter that excluded every node, or a score that ranked the wrong one first?*
> A filter problem leaves a Pod `Pending` forever; a score problem puts the Pod somewhere you
> didn't want, immediately and silently.

## ⚑ The control-loop observation, and where it should point

§7 closes by noting the scheduler "watches… compares what exists against what has been
placed, and acts on the difference" — the same shape as every controller. **The observation
is correct and this is the cleanest instance of `control-loop.md`'s *common* shape (control
via API server) in the book so far**, pairing with Chapter 5's kubelet, which is the
*uncommon* direct-control shape.

Two problems: the chapter attributes it to **Chapter 6**, which is withdrawn, and carries
**no cross-bearing**. It should point at **Ch 3 §6**, where the loop is defined and where the
shard is homed. Stronger claim, survives the Ch 6 re-draft, one bracketed insertion.

## Figures

`ch07-fig01-filter-score-bind` — the spine. **The third arrow must land on the API server,
with the kubelet drawn as a separate actor below a dashed separator.** That separation is the
figure's entire pedagogical job; any redraw must preserve it.
`ch07-zenith-berth-assignment` — the two-slot taxonomy, with `nodeName` drawn *outside* the
pipeline.

## Related

[[feasible-node]] · [[pending-pod]] · [[nodename]] · [[predicates-priorities]] ·
[[control-plane-components]] · [[control-loop]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/feasible-node.md ===
# Concept: Feasible nodes — what filtering actually checks

**Home:** Chapter 7 §2 · **Competency:** D1.3 · **Status:** canonical
**Discharges:** `resource-request.md`'s Ch 7 obligation — "requests as the scheduler's
filtering step." **First of that shard's four downstream obligations to land.**

## Definition

> The nodes that meet a Pod's scheduling requirements are called **feasible nodes.**
> [source: k8s-docs-kube-scheduler-2026-08-23]

The documentation's own example of a filter is **`PodFitsResources`**, which "checks whether
a candidate node has enough available resources to meet a Pod's specific resource
**requests**." [source: k8s-docs-kube-scheduler-2026-08-23]

**Requests. Not limits** — the kubelet enforces limits on the running container, after
placement, on a node already chosen [source: k8s-docs-resource-management-2026-08-23]. **And
not observed usage,** which the scheduler never consults.

🔭 `PodFitsResources` is named as *an example* of a filter, not the only one. Resources are
one feasibility test among several; §3–§5 add more and §6 notes the filter set is
configurable.

## ★ Fixed Point (verbatim)

> **Filtering fits a Pod's *requests* against a node's *available* capacity. The scheduler
> books; it does not measure. Ten Pods that each requested 1 GiB and each use 50 MiB have
> filled a 10 GiB node completely, as far as scheduling is concerned.**

## A request is a booking

> When you specify a resource request for a container, the kube-scheduler uses that
> information to decide which node to place the Pod on, and the kubelet **reserves at least
> the request amount** of that resource specifically for that container to use.
> [source: k8s-docs-resource-management-2026-08-23]

Read with an accountant's eye: once a Pod is placed, its requests come off the node's balance
and stay off, whether the container touches them or not.

The chapter's worked case: a node with 16 GiB allocatable, four Pods that each requested
4 GiB, monitoring reporting 2 GiB in use. A fifth Pod requesting 1 GiB **does not schedule.**
"A node can be busy and empty at the same time, and only one of those two states is the
scheduler's business."

**This is the fact that converts "the cluster has loads of free memory but my Pod won't
schedule" from a mystery into arithmetic.**

## ⚑ Not a contradiction of `resource-request.md`

That shard records "a request is a floor, not a ceiling" — a running container *may* exceed
its request when the node has spare capacity. Both are true at once: that is the **kubelet's**
view of a running container; this is the **scheduler's** view of placement, which counts the
booking regardless of use. Holding both is the diagnostic skill. See the proposed shard
update in `ch-07/kb-manifest.md`.

## What "available" is measured against

A node's status reports both **Capacity** and **Allocatable**
[source: k8s-docs-nodes-2026-08-23]. Allocatable is the one that matters:
"'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are
available for pods"; "the scheduler treats 'Allocatable' as the available `capacity` for
pods"; and the scheduler **does not over-subscribe** it
[source: k8s-docs-node-allocatable-2026-08-24].

Do the arithmetic against Allocatable, not the machine's total RAM.

## ⚑ Capacity is named, not defined — and not currently closable

§2 says "Some of that total is spoken for by things that aren't Pods." **That sentence is
untagged**, and I verified why: `k8s-docs-nodes-2026-08-23` lists Capacity and Allocatable in
the node-status fields and never defines Capacity or states the relationship.
**Research-manifest gap G-7C.** The fix is a fetch or a softening — *not* a tag. Chapter 8
owns the term.

## The one exception to waiting

> If a Pod cannot be scheduled, the scheduler tries to preempt — evict — lower priority Pods
> to make scheduling of the pending Pod possible.
> [source: k8s-docs-pod-priority-preemption-2026-08-24]

Named and scoped out, with the chapter's stated reason: "Register that they exist so that
nothing in this chapter reads as a lie later." Skill Part 11's order/truth balance done
correctly; worth copying as a house pattern.

## Related

[[scheduling]] · [[pending-pod]] · [[resource-request]] · [[resource-limit]] ·
[[node-components]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pending-pod.md ===
# Concept: `Pending` — a state, not an error

**Home:** Chapter 7 §2 · **Competency:** D1.3 · **Status:** canonical
**Forward reach:** Chapter 13's opening move depends on this; Chapter 17 retrieves it as a
signal.

## The rule (verbatim)

> If none of the nodes are suitable, **the Pod remains unscheduled until the scheduler is
> able to place it.** [source: k8s-docs-kube-scheduler-2026-08-23]

Its phase is `Pending`, which covers, among other things, "time a Pod spends waiting to be
scheduled" [source: k8s-docs-pod-lifecycle-2026-08-23].

## ⚠ Navigational Hazards (verbatim — canonical retrieval string)

> `Pending` is a **state**, not an error. It is the honest report of a Pod that has been
> accepted by the cluster and has nowhere to run yet. **No component is quietly retrying it
> with looser constraints, and no timer will eventually convert it into a failure.**

Nothing errors. Nothing times out. Nothing retries with different parameters. "A Pod can sit
in `Pending` for a week and the cluster will consider this a perfectly ordinary state of
affairs." The controller that created it has already done its part — its count is satisfied,
because the Pod exists.

## Why it matters more than it looks

The chapter's stated reason this fact is worth exam points: it is one sentence, and it is
"exactly the shape a recognition exam asks about." Four Chapter 7 items grade it (Bearings #1
Q5, Practice Q4, Q7, and Q16's distractor D).

**`Pending` is also the correct answer everywhere in this chapter except one place.** The
`nodeName` bypass fails outright instead — which is precisely why Practice Q16's `Pending`
distractor is the chapter's best-designed trap. See [[nodename]].

## The structural observation Ch 17 retrieves

> An unschedulable Pod is a **standing, machine-readable statement that the cluster is short
> of somewhere to put work.** Something could be watching for exactly that.

## Two diagnoses that look identical from outside

A Pod is `Pending` because a filter emptied the feasible set. **Which** filter is a separate
question, and the two commonest causes are indistinguishable without reading the events:

- **capacity** — requests don't fit against Allocatable ([[feasible-node]])
- **a taint** — an untolerated `NoSchedule` removed every candidate ([[taint]])

Chapter 7 states this explicitly and hands both to Chapter 13. The ⚓ diagnostic frame from
§7 is the tool: *is this a filter that excluded every node, or a score that ranked the wrong
one first?* A filter problem waits forever; a score problem places the Pod somewhere wrong,
immediately and silently.

## ⚑ Deliberately not covered, and that is correct

`kubectl describe`, the event stream, and the scheduler's own message are Chapter 13's
material. Chapter 7's Bearings #1 A5 says so in the answer key: "the fact that you know
exactly what state to look for is what will make that chapter fast."

## Related

[[feasible-node]] · [[scheduling]] · [[pod-phase]] · [[taint]] · [[nodename]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/nodeselector.md ===
# Concept: `nodeSelector`

**Home:** Chapter 7 §3 · **Competency:** D1.3 · **Status:** canonical

## Definition (verbatim)

> `nodeSelector` is the simplest recommended form of node selection constraint. You add the
> `nodeSelector` field to your Pod specification and name the node labels you want the target
> node to have, and **Kubernetes only schedules the Pod onto nodes that have each of the
> labels you specify.** [source: k8s-docs-assign-pod-node-2026-08-23]

**Each. Not any.** An AND of exact matches, offering nothing else: no "one of these," no
"anything except," no "greater than."

The chapter's read on that bluntness: it "is a feature for the ninety percent of requirements
that are genuinely blunt ('this Pod needs an SSD')."

## ⚠ The fact that must not fall between this shard and [[node-affinity]]

**`nodeSelector` and required node affinity fail identically.** No matching node, no
placement, Pod sits in `Pending`. Node affinity is *not* a straight upgrade path — it adds a
second, **independent** axis (soft vs hard), and only one of the six cells in `ch07-fig02` is
soft.

*This fact is stated in both shards deliberately. Do not deduplicate it.*

## Selection advice (from the chapter)

> Reach for `nodeSelector` first. Affinity exists for the requirements `nodeSelector`
> genuinely cannot express, and **a soft rule you didn't need is a rule someone will misread
> as a guarantee eighteen months from now.**

## The direction inversion

Chapter 4 taught label selectors as an object selecting a set of **Pods**. Here it is a **Pod
selecting nodes** — same mechanism, opposite subject and object. See [[node-labels]] and
`label-selector.md`.

## Related

[[node-affinity]] · [[node-labels]] · [[label-selector]] · [[scheduling]] · [[nodename]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-affinity.md ===
# Concept: Node affinity

**Home:** Chapter 7 §3 · **Competency:** D1.3 · **Status:** canonical
**Serves kb_tags:** `node-affinity`, `affinity-operators`, `required-during-scheduling`,
`preferred-during-scheduling`, `ignored-during-execution`

## ★ Fixed Point (verbatim)

> **`nodeSelector` is an AND of exact node-label matches — nothing more. Node affinity is the
> same idea with a richer operator set and an optional soft (`preferred`) mode.
> `IgnoredDuringExecution` means a label change after binding does not move the Pod.**

## What affinity adds — exactly two things

> Node affinity **functions like the `nodeSelector` field but is more expressive and allows
> you to specify soft rules.** [source: k8s-docs-assign-pod-node-2026-08-23]

**1. A richer operator set:** `In`, `NotIn`, `Exists`, `DoesNotExist`, `Gt`, `Lt`
[source: k8s-docs-assign-pod-node-2026-08-23]. Against `nodeSelector`'s single implicit
"equals."

**2. Two hardness levels** [source: k8s-docs-assign-pod-node-2026-08-23]:

| Field | Meaning | Pipeline slot |
|---|---|---|
| `requiredDuringSchedulingIgnoredDuringExecution` | the scheduler **can't** schedule the Pod unless the rule is met | **filter** |
| `preferredDuringSchedulingIgnoredDuringExecution` | the scheduler **tries**; "if a matching node is not available, it still schedules the Pod" | **score** |

For preferred rules you may specify a `weight` of 1–100 per instance; "the resulting sum is
added to the node's score from other scoring functions; nodes with the highest total score
win" [source: k8s-docs-assign-pod-node-depth-2026-08-24]. **The arithmetic is not required
for this exam. Noticing that preferred rules land in scoring is** — that is §7's whole point.

## ⚠ Hardness and expressiveness are INDEPENDENT axes

`ch07-fig02` exists to prevent one misreading: that node affinity is "more powerful
`nodeSelector`" on a single upgrade path.

**`nodeSelector` and required node affinity fail identically** — no match, no placement,
`Pending`. Choosing between the three cells is choosing *how much you want to say*, and
separately, *how badly you want it obeyed*. Only one of the six cells is soft.

*Stated in [[nodeselector]] too, deliberately. Do not deduplicate.*

## 🪢 Decoding the field names

> Read `requiredDuringSchedulingIgnoredDuringExecution` as two clauses joined at the seam:
> **required when scheduling, ignored once running.** The word is thirty-nine characters; the
> meaning is six. **Every one of these field names decomposes the same way:** first half is
> what happens at placement, second half is what happens afterwards.

## `IgnoredDuringExecution`

> If the node's labels change after Kubernetes schedules the Pod, **the Pod continues to
> run.** [source: k8s-docs-assign-pod-node-2026-08-23]

This is Chapter 5's once-only lifetime rule with a name, sitting in plain sight inside a field
the reader will type. A Pod placed on a node labelled `disktype=ssd` is not evicted when
someone strips the label. "The rule was a scheduling-time question and scheduling time is
over." Graded at Bearings #2 Q4 and Practice Q8.

## Combination rules (easy to get backwards)

> Multiple terms in `nodeSelectorTerms` → the Pod can be scheduled if **one** is satisfied
> (**ORed**). Multiple expressions in a single `matchExpressions` → schedulable **only if
> all** are satisfied (**ANDed**).
> [source: k8s-docs-assign-pod-node-depth-2026-08-24]

## ⚑ Missed consolidation with Chapter 4

`label-selector.md` already publishes `In`, `NotIn`, `Exists`, `DoesNotExist` as the
`matchExpressions` vocabulary, and records that `matchLabels` is exactly equivalent to a
`matchExpressions` entry with operator `In`. **Node affinity's operator set is that
vocabulary plus two numeric operators, in a field with the same name.** Chapter 7 never says
so — Practice Q12 correctly handles the *lowercase* set-based selector syntax but not this.

Saying it reframes §3 from "a new syntax" to "the syntax you already know, extended," which
is `label-selector.md`'s whole thesis. Cheapest consolidation available in the chapter.

## Figure

`ch07-fig02-nodeselector-vs-affinity` — a 2×3 grid, hardness against expressiveness, with the
empty cells drawn as empty. **The emptiness is the content**; a redraw that fills them or
collapses the grid to a single arrow destroys the point.

## Related

[[nodeselector]] · [[node-labels]] · [[label-selector]] · [[scheduling]] ·
[[inter-pod-affinity]] · [[taint]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/taint.md ===
# Concept: Taints — the node's refusal

**Home:** Chapter 7 §4 · **Competency:** D1.3 · **Status:** canonical
**Serves kb_tags:** `taint`, `noschedule`, `prefernoschedule`, `noexecute`

## The inversion (verbatim)

> Node affinity is a property of Pods that attracts them to a set of nodes (either as a
> preference or a hard requirement). **Taints are the opposite — they allow a node to repel a
> set of pods.** [source: k8s-docs-taints-tolerations-2026-08-23]

> One or more taints are applied to a node; this marks that the node should not accept any
> Pods that do not tolerate the taints.
> [source: k8s-docs-taints-tolerations-2026-08-23]

**The taint lives on the node.** The toleration lives on the Pod — see [[toleration]].
Getting them the wrong way round is the source of most confusion in this material, which is
why the two are separate shards.

## The three effects — learn them by WHEN they act

| Effect | Arriving, no toleration | Arriving, tolerating | Already running, no toleration |
|---|---|---|---|
| `NoSchedule` | not placed | may be placed | **unaffected** |
| `PreferNoSchedule` | avoided where possible | may be placed | **unaffected** |
| `NoExecute` | not placed | may be placed | **EVICTED** |

- **`NoSchedule`** — "no new Pods will be scheduled on the tainted node unless they have a
  matching toleration. **Pods currently running on the node are not evicted.**"
- **`PreferNoSchedule`** — "the soft version of `NoSchedule`. The control plane will *try* to
  avoid placing a Pod that does not tolerate the taint on the node, but it is not
  guaranteed."
- **`NoExecute`** — "Pods that do not tolerate the taint are **evicted immediately**." Pods
  tolerating without `tolerationSeconds` "remain bound forever"; with it, they remain for
  that long, "after which the node lifecycle controller evicts them."

All: [source: k8s-docs-taints-tolerations-2026-08-23]

> "may be placed" — **never** "is placed." The other filters and scores still run.

⚠ **The classic wrong answer is that `NoSchedule` evicts.** It doesn't, "and the word
*Schedule* in the name is telling you so." Graded at Bearings #2 Q3 and Practice Q11.

🪝 **`PreferNoSchedule` is a preference, and preferences lose.** Non-tolerating Pods will land
on such a node when nothing better is available, "and that is correct behaviour, not a bug.
If you need 'never,' you need `NoSchedule`."

## Multiple taints on one node

> Start with all of a node's taints, then ignore the ones for which the pod has a matching
> toleration; the remaining un-ignored taints have the indicated effects on the pod.
> [source: k8s-docs-taints-tolerations-depth-2026-08-24]

**Tolerating three of four taints does not get you aboard.** The fourth still applies.

## Applying and removing

```
kubectl taint nodes node1 key1=value1:NoSchedule
kubectl taint nodes node1 key1=value1:NoSchedule-
```
[source: k8s-docs-taints-tolerations-depth-2026-08-24]

The removal form is the same command with a **trailing minus** — "easy to miss and easy to
mistype."

⚑ Neither command takes `-n`, because Nodes are cluster-scoped. See
`cluster-scoped-resource.md`; Chapter 7 does not make the connection and should.

## Pipeline slot

An **untolerated `NoSchedule` or `NoExecute` filters** (the node is removed from
consideration). **`PreferNoSchedule` scores** (the node stays in with a worse rank). Graded at
Practice Q10. See [[scheduling]] §7.

## Figure

`ch07-fig03-taints-tolerations-effects` — the refusal originates at the node; three Pods
(arriving-untolerating, arriving-tolerating, already-aboard) against the three effects.
**Pod C is the point of the figure: two of three rows leave it completely alone.** The
outline warns against inflating this figure — its job is reference, not synthesis.

## Related

[[toleration]] · [[built-in-node-condition-taints]] · [[node-affinity]] · [[pending-pod]] ·
[[scheduling]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/toleration.md ===
# Concept: Tolerations — the Pod's exemption

**Home:** Chapter 7 §4 · **Competency:** D1.3 · **Status:** canonical
**Serves kb_tags:** `toleration`, `tolerationseconds`, `taint-toleration-matching`

## ★ Fixed Point (verbatim — canonical retrieval string)

> **A taint is the node's refusal; a toleration is the Pod's exemption from that refusal.
> Tolerations permit — they never attract. Of the three effects, only `NoExecute` affects
> Pods that are already running.**

## Definition

> **Tolerations are applied to Pods**, and they allow the scheduler to schedule Pods with
> matching taints. [source: k8s-docs-taints-tolerations-2026-08-23]

## ⚠ The qualification that catches everyone

> **Tolerations allow scheduling but don't guarantee scheduling**: the scheduler also
> evaluates other parameters as part of its function.
> [source: k8s-docs-taints-tolerations-2026-08-23]

> A toleration **removes a veto.** That is the entire extent of its power. It does not make a
> request, it does not raise a node's score, it does not reserve anything, and it does not
> create capacity.

Your GPU workload with a matching toleration is now *allowed* onto the GPU nodes — along with
being allowed onto every other node in the cluster, which it already was. **Nothing has pulled
it toward the GPU nodes at all.**

Integration marks this "the most durable error in this material." It is graded three times in
Chapter 7 (Bearings #2 Q2 — the designated struggle item — plus Practice Q9 and Q10's
distractor D) and carries the chapter's only Logbook Entry.

## ★ The dedicated-node pattern — both directions required

> If you want to dedicate nodes to a group **and** ensure they only use the dedicated nodes,
> "you should additionally add a label similar to the taint to the same set of nodes… and the
> admission controller should additionally add a node affinity to require that the pods can
> only schedule onto nodes labeled with `dedicated=groupName`."
> [source: k8s-docs-taints-tolerations-depth-2026-08-24]

**Taints exclude. Affinity attracts. A dedicated-node setup needs both.** The chapter calls
this "the single most transferable operational fact in this chapter," and using only one half
"produces a cluster that looks like it's misbehaving when it's doing precisely what you asked."

## — Dead Reckoning: the matching rules

> A toleration matches a taint when the keys are the same and the effects are the same, and
> one of two operator conditions holds. If the operator is `Exists`, no value should be
> specified. If the operator is `Equal`, the values must be equal. Two wildcards modify this.
> If the key is empty, the operator must be `Exists`, which matches all keys and all values —
> the effect must still match. An empty effect matches all effects with the given key.
> [source: k8s-docs-taints-tolerations-2026-08-23]

| Toleration | Matches | Notes |
|---|---|---|
| key + effect + `Equal` + value | same key, effect, value | the exact-match case |
| key + effect + `Exists` | same key and effect, **any value** | do not specify a value with `Exists` |
| empty key + `Exists` + effect | **all** taints with that effect | empty key *requires* `Exists` |
| key + `Exists` + **empty effect** | all effects for that key | effect wildcard |

## `tolerationSeconds`

Applies to `NoExecute` only. Without it, a tolerating Pod "remains bound forever"; with it,
the Pod remains for that long and is then evicted by the node lifecycle controller
[source: k8s-docs-taints-tolerations-2026-08-23].

## ⚑ Where the register is deliberately flat

§4 introduces the matching rules with "Here the metaphors run out. Four rules, no narrative,
stated flat." That is the — Dead Reckoning marker used exactly as skill Part 1 specifies, and
the outline mandated it for this section. **Any revision that adds a berth metaphor here is
working against an explicit contract.**

## Related

[[taint]] · [[built-in-node-condition-taints]] · [[node-affinity]] · [[nodeselector]] ·
[[scheduling]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/built-in-node-condition-taints.md ===
# Concept: Built-in node-condition taints

**Home:** Chapter 7 §4 · **Competency:** D1.3 · **Status:** canonical
**Pays:** Chapter 6 §7's "you'd already met the mechanism in disguise" tease. ⚑ Chapter 6 is
currently withdrawn — see the Chapter 7 manifest's Chapter 6 debt table.

## The design (verbatim)

> The control plane, using the node controller, automatically creates taints with a
> `NoSchedule` effect for node conditions. **The scheduler checks taints, not node conditions,
> when it makes scheduling decisions.** This ensures that node conditions don't directly
> affect scheduling. [source: k8s-docs-taints-tolerations-depth-2026-08-24]

The chapter's read: "Node health doesn't get a special channel into the scheduler; it gets
translated into the *same* mechanism you'd use by hand."

## The family

| Taint key | Effect |
|---|---|
| `node.kubernetes.io/not-ready` | `NoExecute` |
| `node.kubernetes.io/unreachable` | `NoExecute` |
| `node.kubernetes.io/disk-pressure` | `NoSchedule` |
| `node.kubernetes.io/memory-pressure` | `NoSchedule` |
| `node.kubernetes.io/pid-pressure` | `NoSchedule` |
| `node.kubernetes.io/unschedulable` | `NoSchedule` |
| `node.kubernetes.io/network-unavailable` | `NoSchedule` |

[source: k8s-docs-daemonset-2026-08-24]

Plus `node.cloudprovider.kubernetes.io/uninitialized`, "added when the kubelet starts with an
external cloud provider" [source: k8s-docs-taints-tolerations-depth-2026-08-24].

⚑ **Link Chapter 3 did not draw and Chapter 7 did not either.** `k8s-docs-nodes-2026-08-23`
lists the node **Conditions**: Ready, DiskPressure, MemoryPressure, PIDPressure,
NetworkUnavailable. **Five of the seven taints above are those conditions translated.** Saying
so makes the table derivable rather than memorizable. See `node-components.md`.

## The 300-second grace period

> Kubernetes automatically adds a toleration for `node.kubernetes.io/not-ready` and
> `node.kubernetes.io/unreachable` with `tolerationSeconds=300`, unless you or a controller
> set those tolerations explicitly.
> [source: k8s-docs-taints-tolerations-depth-2026-08-24]

Why a briefly-unreachable node doesn't instantly shed everything running on it.

## The DaemonSet mechanism

> The DaemonSet controller automatically adds tolerations for **all seven** of the built-in
> condition taints to the Pods it creates. Because it sets the
> `node.kubernetes.io/unschedulable:NoSchedule` toleration automatically, Kubernetes can run
> DaemonSet Pods on nodes that are marked unschedulable. And the `NoExecute` tolerations for
> `not-ready` and `unreachable` carry **no** `tolerationSeconds`, so DaemonSet Pods running on
> such nodes are **not evicted.** [source: k8s-docs-daemonset-2026-08-24]

The chapter's payoff, worth keeping verbatim:

> Which is exactly why your log-shipping agent is still reporting from a node that's under
> memory pressure and refusing all other work. **It isn't privileged. It just tolerates
> everything.**

Graded at Bearings #3 Q5, whose answer key makes the stronger point: "nothing special
happened. This is the ordinary scheduler doing its ordinary job… There's no privileged path
and no bypass."

## ⚑ `node.kubernetes.io/unschedulable` — Chapter 8's named opening

Both §4 and the Voyage Ahead say something puts this taint there "on purpose, as a deliberate
administrative act." **That causal claim is untagged in both places** — the key and effect are
sourced; the intent is not. Chapter 8 owns the command that applies it and the command that
clears the node afterwards. Recorded as a Tier 3 reserved glossary row.

## Related

[[taint]] · [[toleration]] · [[node-components]] · [[pending-pod]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/inter-pod-affinity.md ===
# Concept: Inter-Pod affinity and anti-affinity

**Home:** Chapter 7 §5 · **Competency:** D1.3 · **Status:** canonical
**Serves kb_tags:** `pod-affinity`, `pod-anti-affinity`
**Difficulty:** 🟡 — the altitude jump, and the reason §5 is not 🔵

## The gap it fills

Everything before §5 constrains a Pod against a property of a **node**. This constrains a Pod
against the properties of **other Pods**.

The chapter starts from the failure: two replicas created for redundancy land on the same
node, and "the service now has exactly the availability it had with one replica, plus double
the resource bill." Nothing earlier prevents it, and the scheduler is not being careless:

> Identical Pods are equally feasible on every node and score identically on every node, and
> the scheduler is entirely free to pick the same node twice. **You never told it these two
> were related.**

> **Redundancy is a property of a set, and none of the mechanisms so far can express a
> property of a set.**

## Definition (verbatim)

> Inter-pod affinity and anti-affinity let you constrain Pods against **labels on other
> Pods**: "only schedule on nodes in the same zone as a Pod with this label," or "spread these
> Pods across nodes." [source: k8s-docs-assign-pod-node-2026-08-23]

- **Pod affinity attracts.** Schedule this Pod where a Pod carrying that label already is.
  For co-locating things that talk to each other constantly.
- **Pod anti-affinity repels.** Do not schedule this Pod where a Pod carrying that label
  already is. **The availability tool.**

Both come in the same `required` / `preferred` flavours as node affinity — "genuinely the same
machinery pointed at a different set of labels, not a second system to learn."

> `podAntiAffinity` in `requiredDuringSchedulingIgnoredDuringExecution` mode means **only a
> single Pod can be scheduled into a single topology domain**; in
> `preferredDuringSchedulingIgnoredDuringExecution` mode "you lose the ability to enforce the
> constraint." [source: k8s-docs-topology-spread-constraints-2026-08-24]

## ★ Fixed Point (verbatim)

> **Inter-Pod rules are evaluated against the labels of Pods that are *already placed*, within
> a topology domain defined by a node label (`topologyKey`). The domain is the part people
> forget — it is a variable, not a synonym for "node."**

See [[topology-domain]] — it is a separate shard precisely because topology spread constraints
depend on it too, and a duplicated definition would drift.

## 🔭 Why these rules are expensive

To decide whether one node is feasible, the scheduler must know what is running everywhere
else in the domain: "the answer for node-a depends on the contents of node-b." A different
cost shape from "does this node have 4 GiB free."

> Inter-pod affinity and anti-affinity require substantial amounts of processing which can
> slow down scheduling in large clusters significantly. **We do not recommend using them in
> clusters larger than several hundred nodes.**
> [source: k8s-docs-assign-pod-node-depth-2026-08-24]

"This is a sharp tool. It is not free."

## When it is the wrong tool

🪝 "'Spread my replicas evenly across nodes' and 'never put two of these together' are
different requirements. Anti-affinity states the second and only approximates the first. If
you find yourself writing anti-affinity rules and then reasoning about how many replicas
you're allowed to have, you wanted [[topology-spread-constraints]]."

## Pipeline slot

**Required inter-Pod rules filter. Preferred inter-Pod rules score.** And — Practice Q13 —
pod affinity "can only ever *narrow* the surviving set, never restore a node that has already
been removed" by an untolerated taint.

## Figure

`ch07-fig04-pod-affinity-anti-affinity-topology` — the same cluster and the same rule drawn
twice, differing only in `topologyKey`. **The two panels must stay side by side**; the figure's
whole argument is that one label key changed and the rule's meaning changed with it.

## Related

[[topology-domain]] · [[topology-spread-constraints]] · [[node-affinity]] ·
[[label-selector]] · [[scheduling]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/topology-domain.md ===
# Concept: Topology domain and `topologyKey`

**Home:** Chapter 7 §5 · **Competency:** D1.3 · **Status:** canonical
**Why its own shard:** both [[inter-pod-affinity]] and [[topology-spread-constraints]] depend
on it. Folding it into either would duplicate it into the other, and duplicated definitions
drift.

## Definition (verbatim)

> You express the topology domain using a **`topologyKey`, which is the key for the node label
> that the system uses to denote the domain.**
> [source: k8s-docs-assign-pod-node-depth-2026-08-24]

> Nodes that have a label with that key and **identical values** are considered to be in the
> same topology. [source: k8s-docs-topology-spread-constraints-2026-08-24]

## The hard idea

**The domain is not always "the node."** The same rule, over the same cluster, means different
things depending on which label you name:

| `topologyKey` | A domain is | Six nodes / two zones |
|---|---|---|
| `kubernetes.io/hostname` | one node | 6 domains → up to 6 Pods placed |
| `topology.kubernetes.io/zone` | one zone | 2 domains → at most 2 Pods placed |

Same cluster, same rule text. "Change one label key and the rule goes from 'spread across
machines' to 'spread across failure zones,' which is dramatically stricter and, if you only
have two zones, dramatically more likely to leave Pods `Pending`."

Both keys are members of the standard node-label set
[source: k8s-docs-well-known-labels-2026-08-24], which is why §3's list of standard labels is
load-bearing here and not merely inventory.

## Where it is graded

Bearings #3 Q2 and Practice Q14. Q14's key states the consequence precisely: "Twelve nodes
gave twelve domains; two zones give two. Four of the six replicas have nowhere legal to go."
Its distractor B has the direction backwards — **fewer, larger domains is stricter, not
looser** — which is the natural wrong intuition.

## Related

[[inter-pod-affinity]] · [[topology-spread-constraints]] · [[node-labels]] · [[pending-pod]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/topology-spread-constraints.md ===
# Concept: Topology spread constraints

**Home:** Chapter 7 §5 · **Competency:** D1.3 · **Status:** canonical
**Depth:** recognition — recognise the four fields, do not compose them.

## Definition (verbatim)

> You can use *topology spread constraints* to control how Pods are spread across your cluster
> among failure-domains such as regions, zones, nodes, and other user-defined topology
> domains… This can help to achieve high availability as well as efficient resource
> utilization. [source: k8s-docs-topology-spread-constraints-2026-08-24]

Like everything in §5, they rely on node labels to identify the topology domain each node is
in. See [[topology-domain]].

## The four fields

| Field | What it says |
|---|---|
| `topologyKey` | the key of node labels; nodes with this key and identical values are in the same topology |
| `labelSelector` | "Pods matching this selector are counted to determine the number of Pods in their corresponding topology domain" |
| `maxSkew` | "describes the degree to which Pods may be unevenly distributed. Must be specified and must be greater than zero" |
| `whenUnsatisfiable` | `DoNotSchedule` (default) — "tells the scheduler not to schedule the Pod"; `ScheduleAnyway` — "tells the scheduler to still schedule it while prioritizing nodes that minimize the skew" |

All: [source: k8s-docs-topology-spread-constraints-2026-08-24]

Optional `minDomains` — "indicating a minimum number of eligible domains," a domain being "a
particular instance of a topology" and an eligible domain "one whose nodes match the node
selector."

## The recurrence that sets up the Zenith

**`DoNotSchedule` is a hard rule; `ScheduleAnyway` is a soft one.** Required and preferred,
once more, under new names — **the fourth appearance of the same pair in the chapter**, and
the chapter says so explicitly right before §7 collects it. See [[scheduling]] § Zenith.

## Cluster defaults

> Default constraints apply to a Pod **if and only if** it doesn't define any constraints in
> its own `.spec.topologySpreadConstraints`, **and** it belongs to a Service, ReplicaSet,
> StatefulSet or ReplicationController.
> [source: k8s-docs-topology-spread-constraints-2026-08-24]

## ⚑ The honest limitation, kept

> There's no guarantee that the constraints remain satisfied when Pods are removed. For
> example, **scaling down a Deployment may result in imbalanced Pods distribution.**
> [source: k8s-docs-topology-spread-constraints-2026-08-24]

"These are scheduling-time constraints. Like everything else in this chapter, they describe a
decision, not a standing invariant." One of the chapter's three well-formed uncertainty
signals.

## ⚑ Outline Open Question #2 — CLOSED

The ch-07 outline recorded topology spread constraints as a **blocking research gap** and
specified a name-it-and-stop fallback. **The fetch landed**
(`k8s-docs-topology-spread-constraints-2026-08-24`, verified present in `sources/`), so §5
teaches the four fields at recognition depth rather than using the fallback. **Open Question
#2 can be closed.**

## Related

[[topology-domain]] · [[inter-pod-affinity]] · [[scheduling]] · [[node-labels]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/nodename.md ===
# Concept: `nodeName` — the bypass

**Home:** Chapter 7 §6 · **Competency:** D1.3 · **Status:** canonical
**Serves kb_tags:** `nodename`, `direct-node-assignment`

## ★ Fixed Point (verbatim)

> **`nodeName` bypasses the scheduler entirely. It overrules `nodeSelector` and every affinity
> rule, and because it skips the feasibility check, a Pod that doesn't fit *fails* rather than
> waiting in `Pending`.**

## Definition

> `nodeName` is a more direct form of node selection than affinity or `nodeSelector`. It's a
> field in the Pod spec, and **if it is not empty, the scheduler ignores the Pod** and the
> kubelet on the named node tries to place the Pod on that node.
> [source: k8s-docs-assign-pod-node-2026-08-23]

> Using `nodeName` **overrules** using `nodeSelector` or affinity and anti-affinity rules.
> [source: k8s-docs-assign-pod-node-depth-2026-08-24]

**Overrules, not "takes precedence within the same evaluation."** The scheduler doesn't run.
Nothing from §2–§5 is consulted, "because the component that would have consulted it was
skipped."

## The one failure in the chapter that isn't `Pending`

> - If the named node does not exist, the Pod will not run, and in some cases may be
>   automatically deleted.
> - If the named node does not have the resources to accommodate the Pod, the Pod will fail
>   and its reason will indicate why, for example **OutOfmemory** or **OutOfcpu**.
> - Node names in cloud environments are not always predictable or stable.
>
> [source: k8s-docs-assign-pod-node-depth-2026-08-24]

> Every other placement failure in this chapter leaves a Pod waiting patiently for conditions
> to improve. This one fails outright, because the feasibility check that would have caught
> the problem in advance never happened. **You took responsibility for it, and nobody is
> going to tell you when you get it wrong.**

This makes Practice Q16's `Pending` distractor the chapter's best trap: `Pending` is the right
answer *everywhere else*. Graded twice more at Bearings #3 Q3 and Practice Q7's contrast case.

## ⚓ The reframe — `nodeName` is the scheduler's output

The clause that makes binding concrete comes from the DaemonSet controller, which does **not**
use `nodeName`: it sets node affinity instead, and then "the default scheduler typically takes
over and then **binds the Pod to the target host by setting the `.spec.nodeName` field**."
[source: k8s-docs-daemonset-2026-08-24]

> **Binding *is* writing `.spec.nodeName`.** So `nodeName` is not a special user-facing
> shortcut at all. It is **the field that binding writes to**, and setting it by hand means
> filling in the scheduler's answer before it was asked the question.

> When you set it yourself you aren't overriding a decision — you're **pre-writing** it, and
> skipping every check that would have validated it. That's why the failure is immediate
> rather than patient.

**This closes Chapter 3's `binding` reservation with a physical referent**, which is a
materially better outcome than defining it as a vocabulary word.

## Neither a filter nor a score

`nodeName` is drawn **outside** the pipeline in `ch07-zenith-berth-assignment`: "it does not
narrow the feasible set and it does not adjust a ranking. **It removes the decision.**" That is
why it is dangerous, and why the documentation calls specifying a node at creation "unusual
and… only done in special cases" [source: k8s-docs-kube-scheduler-2026-08-23] — which, the
chapter notes, "coming from reference documentation, is a stronger discouragement than it
looks."

## Related

[[scheduling]] · [[pending-pod]] · [[nodeselector]] · [[node-affinity]] ·
[[predicates-priorities]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/predicates-priorities.md ===
# Concept: Predicates, Priorities, Profiles — and the pluggable seat

**Home:** Chapter 7 §6 · **Competency:** D1.3 · **Status:** canonical ⚑ **with a currency
caveat — read the flag before editing**
**Serves kb_tags:** `predicates`, `priorities`, `scheduling-policies`, `scheduling-profiles`,
`scheduler-plugins`, `schedulername`, `custom-scheduler`

## The vocabulary map — this is the whole payload

| Older name | What it is |
|---|---|
| **Predicate** | A **filter** — decides whether a node is feasible |
| **Priority** | A **score** — ranks the nodes that survived filtering |

[source: k8s-docs-kube-scheduler-2026-08-23]

"If you read an older blog post that says 'the PodFitsResources predicate,' you now know
that's a filter, and you can carry on reading. **That's what this material is worth on this
exam.**"

## The two documented configuration models

- **Scheduling Policies** — Predicates for filtering, Priorities for scoring.
- **Scheduling Profiles** — plugins implementing different scheduling stages, including
  `QueueSort`, `Filter`, `Score`, `Bind`, `Reserve` and `Permit`. `kube-scheduler` can run
  different profiles.

[source: k8s-docs-kube-scheduler-2026-08-23]

Treat as **a vocabulary mapping onto §1's spine**, not two systems to choose between. "The
profile plugin stages are the same pipeline with more seats exposed, and two of those seat
names, `Filter` and `Score`, are just the steps you already know."

## ⚑ CURRENCY RISK — do not "correct" this to the snapshot's framing

The cached `k8s-docs-kube-scheduler-2026-08-23` snapshot presents Policies and Profiles as
**"two supported ways to configure"** the scheduler. **In current upstream Kubernetes the
Policy model has been removed, not deprecated.**

Chapter 7 handles this deliberately: it teaches Predicates/Priorities as **older names for the
two steps** rather than as a currently-selectable option, so the prose is true under both the
snapshot and current upstream. The chapter's `AUTHOR-REVIEW` comment flags it for the
fact-accuracy stage (outline Open Question #5).

**No change needed to the prose.** Recorded here so a retroactive sweep does not helpfully
re-align it to the snapshot and reintroduce the error.

## The pluggable seat

> `kube-scheduler` is designed so that, if you want and need to, **you can write your own
> scheduling component and use that instead.**
> [source: k8s-docs-kube-scheduler-2026-08-23]

Pods can name which scheduler handles them; a DaemonSet exposes
`.spec.template.spec.schedulerName` for the purpose [source: k8s-docs-daemonset-2026-08-24].

"You do not need to know how to build a scheduler. You need to know that **the seat is
pluggable**: the default scheduler is a default, not a fixture."

**Correctly scoped.** §6 names the fact and bears the extension-points story to Chapter 17
without pre-collecting the four-socket synthesis Chapter 17's secondary Zenith reserves.
Integration verified this restraint.

## Where profile configuration lives

The control plane's own component configuration — "a question about running a cluster rather
than using one." Beared to Chapter 8.

## Related

[[scheduling]] · [[nodename]] · [[control-plane-components]] · [[feasible-node]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 7 update (2026-08-24)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D1.3** | **Chapter 7** *(scheduling)* | **deep** | **2026-08-24** |

**Registry row change:** `D1.3 | Scheduling | Ch 7` → status becomes **"complete — Ch 7
covered 2026-08-24"**, subject to the shortfall recorded below.

**D1.3 opens and closes in one chapter.** Unlike D1.1 (four chapters, still in progress),
this objective has exactly one home. There is no later chapter to absorb a gap, which is why
the shortfall below is worth acting on rather than deferring.

### Chapter 7 — D1.3 coverage detail

`kb_tags.objectives: ["D1.3"]`; all seven sections carry `objectives: ["D1.3"]`.

| Sub-topic | Depth |
|---|---|
| The two-step operation: filtering then scoring | **deep — discharges `control-plane-components.md`'s Ch 7 obligation** |
| Binding as a notification; concretely, writing `.spec.nodeName` | **deep — closes Chapter 3's reserved term, with a physical referent** |
| Feasible nodes; `PodFitsResources` | deep |
| Random tie-break | deep — one sentence, correctly weighted |
| Requests as filtering input; booked vs measured; Allocatable | **deep — discharges `resource-request.md`'s Ch 7 obligation, first of four** |
| `Pending` as a state, not an error | **deep — Chapter 13's opening move depends on it** |
| Node labels; the standard label set | moderate |
| `nodeSelector` | deep |
| Node affinity: six operators, two hardness levels, `IgnoredDuringExecution` | deep |
| Taints: three effects and their timing | **deep — the chapter's densest recall block** |
| Tolerations: matching, permits-never-attracts, dedicated-node pattern | **deep — the most durable error in this material** |
| Built-in node-condition taints; the DaemonSet mechanism | moderate — **pays Chapter 6 §7's tease** ⚠ Ch 6 withdrawn |
| Inter-Pod affinity / anti-affinity; `topologyKey` | moderate–deep |
| Topology spread constraints: four fields | moderate — recognition depth, **outline OQ#2 closed** |
| `nodeName`; the one failure that isn't `Pending` | deep |
| `schedulerName` / custom scheduler | recognition — correctly scoped to Ch 17 |
| Predicates / Priorities vocabulary map | moderate — ⚑ currency risk, recorded in the shard |
| Priority / preemption / `PriorityClass` | named and scoped out — correct |
| **Data locality · inter-workload interference · deadlines** | ⚑ **ABSENT — and Chapter 3 published them** |

### ⚑ The one coverage shortfall — an integration debt, not a curriculum one

`chapter-03:413` publishes the documentation's **six** scheduling factors verbatim:
"individual and collective resource requirements, hardware/software/policy constraints,
affinity and anti-affinity specifications, **data locality**, **inter-workload interference**,
and **deadlines**."

Chapter 7 owes the detail and delivers three of six, never mentioning the other three — not
even to scope them out. Curriculum-alignment logged this as **D1.3-09 PARTIAL**.

The knowledge-base cost is distinct from the coverage cost: a reader who remembers Chapter 3's
list gets no acknowledgement that half of it was dropped. That is the order/truth-balance
failure skill Part 11 warns about, and **Chapter 7 already models the correct fix twice** —
the preemption clause ("Register that they exist so that nothing in this chapter reads as a
lie later") and the `minDomains` mention. One sentence in §2 or §7 closes it.

---

## ⚑ Book-level: the domain-allocation alarm has eased

Chapter 5's ledger raised this as blocking before Chapter 6 drafts. Chapter 7's number changes
the arithmetic.

| Chapter | Claimed | Objective | Metadata form |
|---|---|---|---|
| Ch 2 — Containerization | ~9% | D1.1 | discloses "authored allocation" inline, source-tagged |
| Ch 3 — Cluster architecture | ~6% | D1.1 | "authored estimate" |
| Ch 4 — Objects | ~6% | D1.1 | no caveat |
| Ch 5 — Pods | 7% | D1.1 | "This book's allocation" — no caveat, no tag |
| **Ch 7 — Scheduling** | **5%** | **D1.3** | separate italic disclosure line — **clearest content, least conformant form** |
| **Subtotal** | **33% of 44%** | | |

**Eleven points remain for Chapter 6**, not the sixteen Chapter 5 projected. Eleven is large
but defensible for the chapter carrying Deployments, ReplicaSets, StatefulSets, DaemonSets and
Jobs. **The rebalancing decision is no longer blocking.**

**The disclosure decision still is, and Chapter 7 has half-solved it.** Its dedicated italic
line beneath the metadata — *"Chapter-level weights in this book are the author's allocation.
CNCF publishes four domain weights and a list of named competencies; it does not publish
sub-weights."* — is the clearest statement of the position any chapter has shipped. But the
metadata line itself drops the 44% domain weight and both source tags that Chapters 2 and 5
carry inline, which Stage 6 flagged and revision did not act on.

**Conform the form, keep the content, make that the pattern `reconcile.py` sweeps the other
five to.** The competency separator also still drifts three ways (`— competency: X` / `— X` /
`(X)`); pick one at the same time.

---

## ⚑ Ethical-guardrail status — Chapter 7

| Chapter | Guardrail #3 (strawmanning) | Guardrail #8 (frequency claims) |
|---|---|---|
| Ch 1 | pass | pass |
| Ch 2 | pass | pass — models the compliant phrasing |
| Ch 3 | pass | **FAIL — open** (six unverifiable exam-frequency assertions) |
| Ch 4 | pass | BORDERLINE (five practitioner-prevalence superlatives) |
| Ch 5 | pass | BORDERLINE (four exam-frequency assertions) |
| **Ch 7** | ⚑ **FAIL — new, single instance, L1113** | BORDERLINE (four "most common error" superlatives) |

**Guardrail #3, L1113 (🏆 Safe Harbor):** *"Scheduling is the material that most study guides
present as a catalogue of six unrelated features."* An unsourced negative claim about
competitors' pedagogy in service of a favourable comparison. **First instance of its kind in
seven chapters.** The nearest precedent, `chapter-01:200` ("a disclosure most study guides
skip"), claims competitors *omit* something and then supplies it — materially different from
claiming they teach it badly. Integration's rewrite makes the claim about the material rather
than about publishers, which loses nothing and is truer.

**Guardrail #8 is now three chapters running** (Ch 4, 5, 7 after Ch 3's open FAIL). This has
stopped being a per-chapter observation. **The author should rule once:** either the "most
candidates get this wrong" register is sanctioned — in which case Chapter 3's finding closes
and the skill's Voice Alignment section is the authority — or it isn't, and four chapters need
a hedging sweep. Six words per instance either way. **The ruling is what's overdue, not the
edit.**

**Everything else on the Part 14 checklist passes, several unusually well.** No statistics
appear anywhere in the chapter. Three well-formed uncertainty signals (preemption; the
spread-constraint scale-down limitation; `PodFitsResources`-is-only-an-example). The
**v5.7 subject-dignity guardrail is clean** — the §4 Logbook Entry is the chapter's only
extended consequence narrative and every wry beat in it lands on the practitioners, who are in
the room. And **citation health is perfect**: all 16 cited snapshots resolve to files in
`sources/`, a first for this book since the research-plumbing failure appeared at Chapter 5.

=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 7 update (2026-08-24)

**7 tagged in-budget items · graded pool 32 (15 Bearings + 17 Practice) · rate = 21.9%.**
B3's rung for Chapter 7 is **20%. Cleared.** Three further tagged items sit in Soundings
(Q3, Q4, Q6), excluded from the budget by B3 but doing the spacing work.

**Chapter 7 draws from four predecessors** — Ch 3, 4, 5 and 6. Ch 5 drew from three, Ch 4 from
two, Ch 3 from one. The breadth is still increasing chapter over chapter.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| requests vs limits; which one the scheduler reads | ch 5 §8 | **ch 7** — Soundings Q3 *(excluded from budget)* |
| a Pod is scheduled once; it is not moved | ch 5 §4 | **ch 7** — Soundings Q4 *(excluded from budget)* |
| the loop creates a Pod it cannot place | ch 6 §1 | **ch 7** — Soundings Q6 *(excluded)* ⚠ unshipped |
| request is the scheduler's input; limit is the kubelet's ceiling | ch 5 §8 | **ch 7** — Bearings #1 Q3 |
| ReplicaSet creates a Pod that cannot be placed | ch 6 §1 | **ch 7** — Bearings #1 Q5 ⚠ unshipped |
| label selectors — direction inverts for node selection | ch 4 §5 | **ch 7** — Bearings #2 Q1 |
| scheduled once, never rescheduled — replaced, not moved | ch 5 §4 | **ch 7** — Practice Q5 |
| the scheduler records; the kubelet starts | ch 3 §2 | **ch 7** — Practice Q6 |
| set-based selector operators `in`, `notin`, `exists` | ch 4 §5 | **ch 7** — Practice Q12 |
| DaemonSet one-per-node needs no anti-affinity | ch 6 §7 | **ch 7** — Practice Q15 ⚠ unshipped |

### Quality notes

- **Practice Q5 is the best-designed retrieval item in the chapter.** It takes Chapter 5's
  scheduled-once rule — taught there with a node-*failure* motivation — and re-asks it with a
  strictly *better* opportunity available. Same rule, opposite emotional pull, identical
  answer. Discrimination work, not recall.
- **Practice Q15 is a discrimination question wearing a retrieval tag, and the key says so:**
  "'the Pods end up spread out' and 'a spreading constraint was enforced' are not the same
  claim." Naming the distinction inside the key is a technique earlier chapters don't use and
  it is worth propagating.
- **Bearings #2 Q1 is the cleanest conceptual seam so far.** It doesn't ask whether the reader
  remembers selectors; it asks whether they noticed the subject and object swapped. The key
  validates the reader's confusion — "if this felt backwards while reading §3, that reaction
  was correct and worth keeping" — instead of correcting it.
- **✅ Chapter 5's flagged defect is FIXED.** Chapter 5's ledger recorded that retrieval tags
  appeared only on stems, not in answer keys, and recommended matching Chapter 4. Chapter 7's
  keys name the source chapter inside the explanation body ("This is the same rule you learned
  in Chapter 5…"). A reader who misses an item is told where to go back to. **Closed.**

**⚑ Preamble/rubric mismatch, low cost.** The Soundings preamble says "Three of them ask you
to retrieve something specific from Chapters 5 and 6," but the 0–2 rubric names only "Chapter
5 §8 and Chapter 5 §4." Q6's framing is Chapter 6's. The rubric isn't wrong —
`chapter-05:551` covers the replica-shortfall case — just narrower than promised. Add Ch 6 §1
to the rubric, or drop "and 6."

---

## ⚑ The Chapter 6 debt — six items Chapter 6 now owes Chapter 7

`git log` records `2a78912 Chapter 6: drafted via pipeline` then `2bb971b Chapter 6: withdraw
truncated draft pending re-run`. `Book-KCNA/` ships chapters 01–05 only. This ledger holds the
debt because it survives the re-draft; an `AUTHOR-REVIEW` comment inside Chapter 7 does not.

| # | What Chapter 7 assumes | Where | Kind |
|---|---|---|---|
| 1 | Ch 6 **§1** covers Deployments/ReplicaSets and the create-the-missing-Pod behaviour | Soundings Q6, Bearings #1 Q5, §5 back-bearing | retrieval target |
| 2 | Ch 6 **§7** covers DaemonSets and one-per-node distribution | Practice Q15, §4 back-bearing | retrieval target |
| 3 | Ch 6's **Voyage Ahead ends on the scheduler gap** — "the one thing the control loop cannot do" | §1 opening (L96) | **assertion about what Ch 6 said** |
| 4 | Ch 6 **§7 plants the DaemonSet-tolerations tease** — "you'd already met the mechanism in disguise" | §4 callback (L524–526) | **assertion about what Ch 6 said** |
| 5 | Ch 6 exists as the third of "Chapters 4 through 6" | Why This Chapter Matters (L98) | framing |
| 6 | Ch 6 instantiates the control loop visibly enough for §7's "same shape as every controller in Chapter 6" | §7 (L862) | ⚑ **should point at Ch 3 §6 instead — see below** |

**Items 3 and 4 are blocking.** The ch-07 outline recorded, from the now-withdrawn draft, that
Chapter 6's closing did both — including naming the DaemonSet's tolerations as the mechanism
already seen in disguise. **A re-run is not obliged to reproduce a withdrawn sentence.**

**Add all six to `ch-06/outline.md` § *What this chapter owes forward* before the harvest
re-runs, then re-verify Chapter 7's §-numbers after.** Otherwise Chapter 7 ships two callbacks
to sentences nobody wrote.

---

## Cross-cutting themes — status after Chapter 7

| Theme | Introduced | Retrieved so far | Next |
|---|---|---|---|
| **Labels/selectors as the universal join** | Ch 4 §5 | Ch 5 · ✅ **Ch 7 ×2 — first PLANNED retrieval** | Ch 6, Ch 9, Ch 10 |
| **The control loop** (B3 headline) | Ch 3 §6 | Ch 4 · Ch 5 · ⚑ **Ch 7 §7 — unplanned, paraphrased, mis-pointed** | Ch 6, **Ch 11 (still unbeared)**, Ch 15, Ch 17 |
| **Namespaced vs cluster-scoped** | Ch 4 §3 | Ch 5 §6 — ⚑ **Ch 7 missed a free one** | Ch 12 §3, Ch 10, Ch 11 |
| **The absent-component pattern** | Ch 3 §4, named | — *(still zero, four chapters on)* | Ch 10 ×2, Ch 13, Ch 17 |
| **"Kubernetes defines an interface, the ecosystem implements it"** | Ch 2 §4, named | ⚑ still zero named recurrences | Ch 9 (CNI), Ch 11 (CSI), Ch 17 §4 |

**✅ Chapter 7 is the first chapter to retrieve a theme it was TOLD to retrieve.**
`label-selector.md` bears the universal-join theme to Chapters 6, 7, 9 and 10. Chapter 7 is
the first of those to land, and it lands twice — §3's direction-inversion in prose, and
Practice Q12 graded. Chapters 4 and 5's theme retrievals were all unplanned; welcome, but not
evidence the bearings work. **This one is.**

**⚑ Still retrieved by paraphrase, not by name.** §3 does the universal-join work without
using `label-selector.md`'s canonical string ("the label selector is the core grouping
primitive in Kubernetes"), exactly as Chapter 5 did with the namespaced/cluster-scoped string.
**Two downstream chapters have now each invented their own paraphrase of a string fixed
precisely to prevent that.** The coinage decision was due before Chapter 10 drafts; three
chapters remain.

**⚑ A free retrieval Chapter 7 walked past.** `cluster-scoped-resource.md`'s ★ Fixed Point
names **Nodes** explicitly. Chapter 7 spends a chapter labelling nodes, tainting nodes, and
reading node status without retrieving it once — and the evidence is in the chapter's own
command lines: `kubectl label nodes` and `kubectl taint nodes` take **no `-n` flag**, because
nodes aren't namespaced. This theme has one retrieval in the whole book, by paraphrase.
**Chapter 7 is the most natural site the book will offer, because here the fact is
demonstrable rather than assertable.** One clause on a command line.

**⚑ The control-loop retrieval points at the wrong chapter.** §7's closing observation is
correct and is **the cleanest instance of `control-loop.md`'s *common* shape (control via API
server) in the book** — the scheduler writes to the API server and something else acts —
pairing with Chapter 5's kubelet, which is the *uncommon* direct-control shape. But it
attributes the pattern to **Chapter 6** (withdrawn) rather than **Chapter 3 §6** (where the
loop is defined and the shard is homed), and carries no cross-bearing at all. **Point it at
Ch 3 §6:** stronger claim, survives the Ch 6 re-draft, one bracketed insertion.

**✅ One escalation has PAUSED.** Chapter 5's ledger raised the `reconciliation` gap as
worsening — the book grading readers on a word Chapter 3 promised to define and hasn't.
**Chapter 7 does not use the word at all** (verified: zero occurrences in the draft), despite
§7 describing the mechanism in full. The gap has not closed, but it has stopped growing, and
Chapter 7 demonstrates the description can be written without the term. The one-appositive fix
at Chapter 3's ★ Fixed Point remains the right close.

---

## Forward commitments — one discharged, one overdue, four new

| # | Commitment | Status |
|---|---|---|
| 1 | Ch 13 must carry a Ch 8 retrieval item (version skew) | **OPEN** — untouched |
| 2 | Ch 11 must retrieve the control loop | ⚑ **OPEN, now four chapters overdue.** Ch 3, 4, 5 and 7 have each passed it forward |
| 4 | Ch 12 must **derive** the RBAC 2×2 from the namespaced boundary | **OPEN** |
| 5 | Ch 9 must retrieve the Pod IP / shared namespace | **OPEN.** Ch 7 §5 bears to Ch 9 but on *distribution* ("a Service's backends being on distinct nodes"), not on the IP |
| 6 | Ch 13's method must be "read the phase before you read the logs" | **OPEN** — Ch 7 adds a compatible second half; see #9 |
| 7 | Ch 6 must open on "if Pods are designed to be replaced, who does the replacing?" | **OPEN** — folded into the six-item Ch 6 debt above |
| 8 | Ch 7, 13, 17, 18 must each retrieve requests/limits | ✅ **Ch 7's quarter DISCHARGED** at §2, and extended with the booking semantics. Ch 13, 17, 18 still open |
| 9 | **Ch 13 must diagnose `Pending` as a filter problem vs a score problem** | **NEW.** §7's ⚓ publishes the frame outright — *"is this a filter that excluded every node, or a score that ranked the wrong one first?"* — with the symptom pair that separates them (waits forever vs placed-wrong-silently). Ch 13 should use that framing, not invent one |
| 10 | **Ch 13 must distinguish `Pending`-from-capacity from `Pending`-from-taint** | **NEW.** §4 closes on it: the two "look identical from the outside until you go and read the events" |
| 11 | **Ch 17 must collect the pluggable-scheduler socket** | **NEW.** §6 names `schedulerName` and stops. Correctly scoped — Ch 7 does *not* pre-collect Ch 17's four-socket Zenith |
| 12 | **Ch 8 must open on `node.kubernetes.io/unschedulable`** | **NEW.** §4 and the Voyage Ahead plant it twice as "an administrative act," and the Voyage Ahead makes it Chapter 8's named opening move |

=== END APPEND ===

**The headline for you.** Two things reversed direction this chapter, one good and one not:

**Good, and genuinely new:** the research-plumbing failure that broke Chapter 5 did not recur. I extracted all 146 source tags, reduced them to 16 unique snapshots, and confirmed **every one resolves to a real file in `sources/`**. This is the first chapter since the failure appeared where Stage 14 doesn't have to open with a recovery script. Chapter 7 also discharges three standing obligations — `control-plane-components.md`'s scheduler algorithm, `resource-request.md`'s filtering step (first of that shard's four), and `label-selector.md`'s node-affinity claim — and is the first chapter in the book to retrieve a cross-cutting theme it was actually *told* to retrieve, rather than picking one up by luck. **No Rule 6 contradictions across eleven shards checked.**

**Not good:** the KB write path is still broken and this is the fifth manifest to say so. `=== WRITE` appears exactly once in all of `certcomp` — in the prompt that asks for it. `certcomp/tools/` doesn't exist either, so the materializers Chapters 4 and 5 supplied were never even saved. `Book-KCNA/knowledge-base/` remains empty. **Everything above is composed and none of it reaches disk without one manual script run**, and the replay order matters: ch-01 → ch-03 → ch-04 → ch-05 → ch-07.

Three things need your decision, in order: the Chapter 6 debt (six items, two of which assert what a *withdrawn* chapter said — record them in `ch-06/outline.md` before the re-run); the guardrail #3 clause at L1113, which is a one-clause fix and the first competitor-disparagement instance in seven chapters; and the guardrail #8 ruling, which is now three chapters overdue and is a house-style call rather than an edit.

I did not write any files — per the `--allowed-tools` contract, this is stdout for the orchestrator to capture.