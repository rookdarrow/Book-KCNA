I inspected the book's knowledge base on disk, then verified the integration report's claims against shipped text, the B7 ledger, the source corpus, and the eleven earlier Stage 14 manifests rather than taking them on trust. Four of its findings need correcting or extending, and I found three obligations it missed — one of them a canon breach in the chapter's own Zenith payoff.

# Knowledge-Base Manifest — KCNA Chapter 13

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-31

> **Greenfield notice — and Chapter 12's count was wrong.** `Book-KCNA/knowledge-base/` **does not exist on disk**, verified directly. Ch 12's manifest recorded "twenty-three write blocks pending across three manifests." The real figure is **twelve manifests** — `ch-01` through `ch-12` all carry `kb-manifest.md` — and **136 pending write blocks**. Nothing has ever been applied.
>
> **This matters, because Ch 10's and Ch 11's glossary blocks are built on a false premise.** Both open with: *"BACKFILL REQUIRED. Chapters 1–9 shipped before Stage 14 existed. Their terms are not in this file."* Chapters 1–9 each ran Stage 14 and each composed a glossary block. The terms are absent from the file only because no block was ever applied. See **Infrastructure ⚑ I1** — replaying in chapter order silently destroys nine chapters of work.
>
> **Ordering contract, inherited from Ch 12 and extended.** Chapter 13 uses **APPEND** for the three shared registers and for every existing shard; **WRITE** only for filenames that collide with nothing. Appends cannot clobber, so the worst failure mode if the order is wrong is a headless fragment — recoverable, and no verbatim definition is put at risk. Rule 5 treats definitional drift as worse than a fragment, and this chapter carries ~40 definitions inherited verbatim from documentation.

---

## Glossary entries added to `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md`

Two tiers, following Ch 11 and Ch 12. The integration report marked **14 concepts** as needing entries; skill Part 16 requires *all* technical terms the book introduces, so the **24 B7-owned Chapter 13 rows** (`term-ownership.md:427–450`) are harvested alongside them, plus five terms Chapter 13 introduces that the ledger does not assign at all.

### Tier 1 — entries whose definition is unsourced, provisional, or contested

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **`CreateContainerConfigError`** | *"If a referenced ConfigMap does not exist, or a referenced Secret does not exist, or a named key inside one of them is missing, the kubelet cannot finish assembling the container. It stops, and reports `CreateContainerConfigError`."* — ⚠ **UNSOURCED. Zero occurrences across all 198 snapshots**, verified independently | Chapter 13 §2 |
| **Admission refusal leaves no Pod object** | *"there is no Pod object to describe"*; the reason goes to whoever issued the create — the terminal, or the ReplicaSet — ⚠ **UNSOURCED** | Chapter 13 §2 |
| **cAdvisor** | *"Daemon for collecting, aggregating and exposing container metrics included in Kubelet."* `[source: k8s-docs-resource-metrics-pipeline-2026-08-31]` — ⚠ **no ledger row anywhere** | Chapter 13 §7 |
| **Metrics API** | *"Kubernetes API supporting access to CPU and memory used for workload autoscaling. To make this work in your cluster, you need an API extension server that provides the Metrics API."* `[source: k8s-docs-resource-metrics-pipeline-2026-08-31]` — ⚠ **no ledger row; reaches graded text** (TYB 3 Q1, Q3; Practice Q15) | Chapter 13 §7 |
| **static Pod · mirror Pod** | *"managed directly by the kubelet and represented by mirror Pods"* `[source: k8s-docs-pod-failure-signatures-2026-08-31]` — ⚠ **first appearance in the book is inside a graded answer key** | Chapter 13, Practice Q13 |
| **`ProgressDeadlineExceeded`** | Named, not defined: *"a condition which says the rollout did not finish in time and says nothing at all about why"* — ⚠ **taught at Ch 6 §4; no ledger row; the book's promised cause count is now unrecoverable — see ⚑ C1** | **Chapter 6 §4** |
| **Event retention window / `--event-ttl`** | *"it is deleted automatically after a retention window. The API server's `--event-ttl` flag sets that window."* `[source: k8s-apiserver-event-ttl-and-toleration-defaults-2026-08-31]` — ⚠ **the snapshot is 14 lines and stops at the flag heading; it holds no duration.** Verified | Chapter 13 §3 |

**I verified the two highest-severity gaps independently rather than accepting the draft's flags.** `CreateContainerConfigError` returns **zero matches across all 198 files in `sources/`**. The `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31.md` snapshot is **13 lines long** — frontmatter and one heading, no command lines at all — so B1 gap **G1** is essentially untouched despite that snapshot claiming to close it. The `k8s-docs-crictl-2026-08-31.md` snapshot is 37 lines and contains `crictl ps` / `crictl logs` **only inside its frontmatter `depth_note`**, never in the transcribed body. Every draft AUTHOR-REVIEW on these three points is accurate.

### Tier 2 — the 24 ledger rows plus 5 unassigned terms, harvested per skill Part 16

Platform scope vs application scope · triage order (S-P-C-E-L) · `ErrImagePull` · `ImagePullBackOff` (diagnosis) · `ImageInspectError` · `ErrImageNeverPull` · `ContainerCreating` · `PodInitializing` · Event (the object) · `kubectl describe` · `kubectl events` · `kubectl logs` / `-c` / `--all-containers` / `--previous` · `kubectl config current-context` · `CrashLoopBackOff` · restart backoff curve · `OOMKilled` · `Evicted` / node-pressure eviction · API-initiated eviction · eviction order by QoS class · probe failure signatures · node conditions as a diagnostic · kubelet health · `crictl` / `crictl ps` / `crictl logs` / `--runtime-endpoint` · version-skew symptom shapes · release known issues · resource metrics pipeline · metrics-server · `kubectl top` · cluster-level logging.

**`OOM` is expanded correctly and in the right place.** The register (`term-ownership.md:689`) assigns *Out Of Memory* to Ch 13 §4, and §4 delivers it — *"**Out Of Memory**, since the acronym has now appeared twice without being spelled out"* — after two uses rather than before. Slightly late by the book's own convention, but expanded, sourced to nothing because it needs nothing, and self-aware about the delay. No fix.

**Node-level logging agent is correctly *not* a Chapter 13 entry.** The ledger routes it to Ch 18 §6 with "gloss in one clause + pointer," and §7 gives exactly one clause and a pointer. Contract honoured.

---

## Concept shards at `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/{slug}.md`

**Sixteen created.** Every section clears the 200-word threshold; §8 gets its own shard because the synthesis is the chapter's transferable output and two later chapters inherit it.

- `platform-scope-vs-application-scope.md` — **created** (§1; the mechanical test and the clause everyone drops)
- `triage-order.md` — **created** (§1; S-P-C-E-L and the argument for logs-last)
- `pod-failure-never-started.md` — **created** (§2; the family and what separates its members)
- `admission-refusal-leaves-no-pod.md` — **created** (§2; ⚠ wholly unsourced, graded twice)
- `createcontainerconfigerror.md` — **created** (§2; ⚠ wholly unsourced, graded three times)
- `image-pull-failure-family.md` — **created** (§2; four reasons as one family at four moments)
- `kubernetes-events.md` — **created** (§3; events as a first-class surface, and their expiry)
- `reading-container-logs.md` — **created** (§3; the three flags, and the one-terminated-container cap)
- `pod-failure-started-then-died.md` — **created** (§4; the restart count as the family key)
- `crashloopbackoff.md` — **created** (§4; the backoff *is* the signature)
- `oomkilled-vs-evicted.md` — **created** (§4; trigger / scope / outcome — ⚑ and the fourth axis)
- `crictl.md` — **created** (§5; the layer stack and the disagreement it exists to resolve)
- `version-skew-symptoms.md` — **created** (§6; symptom shapes only — states no skew numbers)
- `resource-metrics-pipeline.md` — **created** (§7; the dashed box is the lesson)
- `cluster-level-logging.md` — **created** (§7; why `kubectl logs` is not an archive)
- `read-the-phase-first.md` — **created** (§8; phase → stage → component → source)

**Sixteen amended by append.** This is the highest append-to-create ratio in the book, and that is the correct shape: Chapter 13 is almost entirely applied prior material, so most of its knowledge-base value lands on shards that already exist.

- `container-state.md` — **appended** · ⚑ **closes an open research gap the shard itself opened**
- `restart-policy.md` — **appended** · ⚑ **discharges the "other five minutes" clause**, from a different chapter
- `resource-limit.md` — **appended** · ⚑ **kernel-versus-kubelet agency contradiction**
- `resource-request.md` — **appended** · what a request buys you when the kubelet is choosing
- `probe.md` — **appended** · the two diagnostic shapes, including the silent one
- `pod-phase.md` — **appended** · the phase as a lookup key, not a status word
- `pending-pod.md` — **appended** · Ch 7's "go and ask" promise discharged in full
- `imagepullbackoff.md` — **appended** · Ch 2's explicit diagnosis deferral discharged cleanly
- `imagepullpolicy.md` — **appended** · the availability cost of `Always`
- `node-conditions.md` — **appended** · ⚑ ledger ⚑1 partially breached; the fix is one column
- `node-controller.md` — **appended** · the node-death timeline, and the humility clause
- `node-heartbeats.md` — **appended** · what an absent heartbeat leads to, not just what it licenses
- `version-skew.md` — **appended** · pointer only; the rule stays here, the symptoms go there
- `absent-component-pattern.md` — **appended** · ⚑⚑ **Conflict 2 resolved by demonstration; Conflict 1 newly breached**
- `control-loop.md` — **appended** · §8's closing reading of `Pending`
- `cri.md` — **appended** · the boundary `crictl` attaches below

Not shard-worthy, adequately carried by the glossary: `kubectl config current-context`, the `--runtime-endpoint` configuration, `journalctl -u kubelet`, the individual `Waiting` reason strings.

---

## ⚑ Contradictions and conflicts — flagged, not resolved

Rule 6 requires these loud. **Three are new. Two correct the integration report.**

### ⚑ C1. NEW, HIGH — the chapter retrieves the absent-component pattern by a name that appears in no shipped chapter

The integration report says: *"Ch 13 conforms to the skeleton; Ch 6 and Ch 11 are the outliers."* That is true against the B6 skeleton and **backwards against the book**.

`concepts/absent-component-pattern.md` (Ch 11's Stage 14 block, lines 1625–1633) already ruled on this and named the exact form Chapter 13 went on to adopt:

| Form | Where it lives | Ch 11 shard's verdict |
|---|---|---|
| *"an object without its component does nothing"* | shipped Ch 3, Ch 10, Ch 11 | **the rule sentence** |
| *"The object exists; nothing happens without the component"* | B7 ledger only | **"Zero occurrences in shipped text. Do not adopt."** |

I re-verified against the shipped files rather than the shard. The rule sentence appears at `chapter-03:1302`, `chapter-10:286`, `:341`, `:628`, `:641`, `:730`, `:1354`, `:1394`, `:1802`, `:1856`, `chapter-11:811`, `:1123`, `:1473`, `:1630` — **and verbatim in all four options of Ch 10 Practice Q18** (`chapter-10:1574–1577`). It is the most heavily graded sentence in the book.

**Chapter 13 never uses it.** `draft-v2.md` returns zero matches for *"without its component does nothing"*. What it uses instead, at `:86`, `:1041` and `:1043`, is the ledger form — bolded at `:1041` as though it were the retrieved name.

And `chapter-06:1082` instructed the reader, in a graded answer key: ***"Name the pattern, because you will retrieve it by name."*** Chapter 13 is where that retrieval comes due, and it arrives under a name Ch 10 grades four options on and Chapter 13 does not say.

**Fix: one clause in §7**, reproducing the shipped sentence verbatim before the paraphrase. The cross-bearing text may stay as-is — it is a pointer, not the name. **Do not** renormalize Ch 6 and Ch 11 toward Ch 13's form; that inverts the book's own canon.

### ⚑ C2. GOOD NEWS — Conflict 2 is resolved by demonstration, and Chapter 13 is the proof

The same shard carried `⛔ DO NOT DRAFT Ch 13 §7 OR Ch 17 §7 UNTIL THE COUNT IS RESOLVED` — two counting conventions differing by exactly two, and either ordinal contradicting a graded item in the other chapter.

**Chapter 13 asserts no ordinal.** Verified: no count, no "instance," no "sighting" anywhere near §7. It retrieves the rule, applies it to a new case, and says nothing about how many cases there have been — which is the shard's own **preferred** resolution (*"stop numbering instances in prose… the list transfers; the number breaks"*), executed rather than argued.

**The block on Ch 13 §7 is lifted. The block on Ch 17 §7 should be lifted too**, on the same terms: retrieve the rule, add the instance to the shard's table, never state the count. Chapter 13 also declines to number the control loop and the pluggable interfaces, so it is fully compliant with the "state the pattern, never the count" convention ratified at the Ch 8 gate.

### ⚑ C3. NEW, MEDIUM — Chapter 12 hands three things forward and Chapter 13 takes two

`chapter-12:2223`, in the Voyage Ahead, reader-facing and explicitly enumerated: *"Bring three things with you from this chapter."*

1. *The shape of a Pod that was rejected rather than one that failed* → **§2's top branch delivers.** ✓
2. *"the `securityContext` fields, because a container that cannot write where it expects to write is a permissions failure wearing an application error's clothing"* → **not delivered.** `runAsUser`, `runAsNonRoot`, `securityContext` and `readOnlyRootFilesystem` return **zero occurrences** in `draft-v2.md`.
3. *A Pod referencing a Secret that does not exist never gets a running container* → **§2 delivers**, as `CreateContainerConfigError`. ✓

The integration report found two broken promises. This is a third, and the report missed it because it audited section-pinned cross-bearings and this one is unpinned prose.

**The natural home is §4, not Ch 16.** Ch 12's phrasing — *"wearing an application error's clothing"* — is precisely the platform-cause-with-application-symptom case that §1 exists to separate, and a container that starts, cannot write, and exits presents as `CrashLoopBackOff`. §4 already quotes the documented cause list (*"application errors, configuration errors, resource constraints, failing health checks, or probe failures"*) and never says which configuration. **One clause naming `securityContext` among the configuration errors discharges the promise and needs no fetch.**

### ⚑ C4. MEDIUM — the OOM-kill agency contradiction, with the source the draft was missing

The integration report is right that the book asserts two agents and reconciles neither. The relevant text, which I read rather than inferred:

- `chapter-05:1025`, sourced: *"when it uses more than its memory limit, **the kernel** may terminate it, but terminations only happen when the kernel detects memory pressure, so a container that over-allocates may **not be killed immediately**"* `[source: k8s-docs-resource-management-2026-08-23]`
- Chapter 13 §4, sourced: *"killed and restarted by **the kubelet**"* `[source: k8s-docs-pod-qos-2026-08-24]`

`concepts/resource-limit.md` already carries the Ch 5 quotation verbatim, so the kernel framing is in the knowledge base today.

**Two consequences the report did not draw.** First, the draft cut its kernel/cgroup axis for want of a source, and the source is already in the book's corpus — the discrimination can be restored without a fetch. Second, Ch 5's *"may not be killed immediately"* clause has no counterpart in Chapter 13, and **Practice Q6 grades on a container that exceeds its limit being killed**. Q6's key is not wrong, but a reader holding Ch 5's clause has a defensible reason to hesitate. One clause in §4 fixes both: the kernel terminates on detected pressure; the kubelet observes the termination, records the reason, and applies the restart policy.

### ⚑ C5. The `Terminated`-state comment should be **amended, not deleted**

The integration report says shipped Ch 5 §8 places `OOMKilled` on the `Terminated` state and instructs *"Delete the comment; do not soften the prose."* The first half is close; the instruction overshoots.

What Ch 5 §8 actually states, sourced, is that **the memory-limit kill** reaches `Terminated` *"with a reason and an exit code recorded"* `[source: k8s-docs-pod-lifecycle-2026-08-23]`. It deliberately never says the string. `concepts/container-state.md` makes the reservation explicit: *"⚑ The **status string** `OOMKilled` is **not** defined here and must not be. Chapter 13…"*

So the *framing* is established canon and needs no softening — the report is right about that. But the *join* (this `Terminated` reason is spelled `OOMKilled`) is the book's own, soundly made and nowhere cited. Chapter 13's TYB 2 Q1 stem prints `Terminated` with `Reason: OOMKilled` as literal product output. **Amend the comment to record the join as the book's; do not delete it, and do not change the prose.**

### ⚑ C6. Ledger ⚑1 is partially breached, and the fix is one column

Ledger flag ⚑1: *"Ch 13 §5 retrieves them as a diagnostic and **must not restate the table**."*

§5 announces compliance and then carries a middle column that reproduces Ch 8 §4's definitions from the same snapshots — including the `False`-versus-`Unknown` distinction that `concepts/node-conditions.md` already holds as a ★ callout (*"`Unknown` is not a fourth failure mode. It is the control plane declining to guess"*) and that shipped Ch 8 states three times. The integration report found this; I confirm it against the shard and add that the shard's own framing is *better* than §5's, so the duplication also loses ground.

**No contradiction — §5 and Ch 8 §4 agree.** Drop the middle column, keep "Your next move," which is genuinely new. Two of §5's rows would then read as instructions rather than definitions, which is what the flag asked for.

### ⚑ C7. NEW — the Practice pool carries no tagged retrieval at all

See **Retrieval-practice ledger** below. B3 puts Chapter 13 at the **25% ceiling** and instructs that the target apply to the Practice pool as well as to Bearings. Bearings hit 23.5%; **Practice is 0 of 16.** The integration report's 23.5% is a checkpoint-only denominator and is correct under the skill's literal wording, but it is not the number Ch 12's Stage 14 reported and not the number a book-close audit will compute.

---

## Infrastructure flags — the knowledge base itself

### ⚑ I1. HIGH — replaying the twelve manifests in chapter order destroys nine chapters of work

Three files are written by a **full WRITE** at three separate points, each of which clobbers everything before it:

| File | WRITE at | What each WRITE discards |
|---|---|---|
| `glossary.md` | ch-01, **ch-03**, **ch-10**, **ch-11** | ch-03 discards ch-01–02 · ch-10 discards ch-03–09 · ch-11 discards ch-10 |
| `objective-coverage.md` | ch-01, **ch-03**, **ch-10**, **ch-11** | same three points |
| `retrieval-log.md` | ch-01, **ch-03**, **ch-10**, **ch-11** | same three points |
| `concepts/absent-component-pattern.md` | ch-03, **ch-10**, **ch-11** | ch-10 discards ch-03 + ch-09's append · ch-11 discards ch-10 |

Ch 10's and Ch 11's blocks justify their full WRITEs with *"Chapters 1–9 shipped before Stage 14 existed."* Whatever the drafting history, **the blocks exist on disk now** — `ch-01/kb-manifest.md` through `ch-09/kb-manifest.md`, all with glossary content — so the premise no longer holds and the replay is destructive.

**Recommendation, and it is mechanical:** before any replay, convert Ch 03's, Ch 10's and Ch 11's four WRITE blocks to APPENDs and delete their file-header preambles (three headers, one preamble each). Then apply ch-01 → ch-13 in order. No content is at risk because appends do not clobber, and the only cost is header duplication, which is cosmetic and easier to fix than a silent loss.

### ⚑ I2. MEDIUM — one concept, two shard filenames

`concepts/pluggable-interface-pattern.md` (created ch-02, appended ch-09) and `concepts/pluggable-interfaces.md` (created ch-11, appended ch-12) are the same concept under two slugs. Ch 12's manifest recorded three live conflicts inside `pluggable-interfaces.md` and did not notice that half the thread lives in the other file — including Ch 9's CNI ordinal, which is one of the conflicts it was tracking.

**Chapter 13 touches neither and adds nothing to the thread.** Recorded here so the Ch 17 §4 collection stage, which meets every conflict at once, does not read one file and conclude it has the set. **Recommendation: merge into `pluggable-interfaces.md` at the replay, leaving a stub.**

### ⚑ I3. LOW — a book-outline artifact was never written

`.pipeline-state/book-outline/retrieval-architecture.md` contains a permissions-failure message, not the B3 document. Its substance survives only in the stage's own summary paragraphs and in `.retrieval-architecture.md.progress.log`. Everything I cite from B3 below is recovered from those two places and is flagged as such. **This should be re-run before the Ch 19 synthesis chapter**, which is 100% retrieval by construction and has no other contract to build on.

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Argument in place of assertion** | "Three completely different causes. One identical output. **The logs cannot distinguish between them, and the phase distinguishes between them instantly.** … The order is not arbitrary and it is not a ritual." | **Strong candidate.** The catalog has exemplars that *state* a rule well; this one anticipates the reader's resistance, names it ("that is the part everyone resists, so it gets an argument rather than an assertion"), and then earns the rule from three worked cases. A distinct move. |
| **Method over recall / identity framing** | "When an experienced operator meets a Pod they have never seen fail in this particular way, they do not consult a mental glossary. **They take a bearing, then another, and read the answer off the intersection** — each question they ask the cluster eliminates a whole category of cause." | **Strong candidate.** Skill Part 3 identity transformation with the brand's navigational vocabulary doing analytical work rather than decoration — the cross-bearing convention's own logic, restated as a diagnostic method. Best instance of functional theming in the book so far. |
| **Zenith / synthesis compression** | "**the phase names a stage, the stage names a component, and the component names a source.** Three steps from symptom to the right place to look, and none of them requires you to have seen this particular failure before." | **Strong candidate.** Three clauses that collapse a whole chapter into something retrievable. Compare Ch 10 §8's "An object is a record of intent. Intent does not act." — same compression discipline, different shape. |
| **Engineering humility** | "**A compass that reads north in every direction is telling you about the compass.** When every node looks dead, the most likely explanation is that the observer is wrong, not that every machine died simultaneously." | **Strong candidate.** One sentence, brand-native, and it teaches a real epistemic move. The shortest excerptable passage among these nominations, which matters for a catalog entry. |
| **The epistemics of an absent signal** | "**The absence of an event is not evidence.** … Something happened. The record of it expired. **A log that nobody keeps is a passage nobody can reconstruct.** … Never conclude 'there was no error' from an absent event. Conclude 'I need a different source.'" | **Strong candidate**, with a note. Adjacent to Ch 12's nominated "naming what a control does not cover," but distinct: that one bounds a control's scope, this one bounds what a *reader may infer from silence*, and the chapter lands it twice from two directions (§3 events, §7 logs). Promote at most one of the two §3/§7 statements. |
| **Extended Analogy** | The three accounts of the same night — "`kubectl` is the harbormaster's ledger… `crictl` is the individual ship's own log… the kubelet's service logs are the account of the officer who was supposed to send the report and did not. **You do not read all three every time. You read down the stack only as far as the disagreement takes you.**" | **Strong candidate, gated.** Each panel maps to one layer *and* to one diagnostic decision, and the closing line converts the analogy into a rule — the contract-carrying construction Ch 12's nominated triptych also had. ⚑ **Gated on the era question the draft raises:** this is the chapter's only era commitment, and it commits to age-of-sail. Confirm KCNA's placement in `illustrator-brief.md` first. |
| **Teaching distrust of a memorized default** | "The window is bounded and it is short… **Read the flag on your own cluster rather than assuming a figure.**" | **Moderate.** A small move the book makes repeatedly and has never nominated: refusing to hand over a number the reader would memorize and then be wrong about on a cluster configured differently. Worth an exemplar if the catalog has no instance; not worth crowding out the four above if it does. |

---

## Objective coverage log

Appended to `objective-coverage.md`. Concept-level audit walked row by row against `domain-analysis.md:214–230`.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D2.3 — Troubleshooting** | **Chapter 13** | **deep — primary home, platform scope** | — |

**D2.3 concept coverage: 10 of 14 taught here, 3 deferred to Ch 16 by design, 1 split to Ch 18.**

Two audiences · resource metrics pipeline · logging architecture · `crictl` · known issues · Pod phase as first signal · container `Waiting` `Reason` · probe failure signatures · node lease heartbeats · node death handling — **all in Chapter 13.**

- **Troubleshooting Applications** (debugging Pods, Services, StatefulSets; init containers; running Pods) → Ch 16, per B1 implication #7. §1 signposts explicitly and does not encroach.
- **`kubectl debug`** → Ch 16 §3. Named and deferred by name.
- **Local service debugging** → Ch 16 §5, as "bypassing the Service on purpose."
- **Monitoring tools** (from the *Troubleshooting Clusters* row) → Ch 18. §7 states the boundary: metrics-server *"is meant only for autoscaling purposes."*
- **Auditing** (same row) → Ch 8 §2, already shipped. §3 cross-bears rather than re-teaching, and correctly notes the audit log answers a different question with its own retention.

**⚑ The D2.3 objective hole is wider than the draft's own comment states.** The draft flags `kubectl exec`/`debug`/`port-forward` and Service/EndpointSlice debugging as deferred to a chapter filed under D3.2. Against the concept table, the deferral also carries **an entire D2.3 row** — *Troubleshooting Applications* — plus *local service debugging* from a second row. That is not a slice of D2.3; it is roughly a third of it. **Unless Ch 16's frontmatter carries `objectives: ["D3.2", "D2.3"]`, the book-close coverage report will show a third of D2.3 with no owning chapter.** The deferrals themselves are correct and well signposted; the fix belongs entirely in Ch 16's frontmatter.

**Trap coverage: 3 of 3 D2.3 traps addressed** (`domain-analysis.md:578–580`), verified line by line — #70 *jumping to `kubectl logs` for a `Pending` Pod* is the chapter's opening move and a ★ Fixed Point; #71 *treating application and cluster debugging as one activity* is §1's entire subject; #72 *expecting `kubectl top` to work without metrics-server* is §7's ★ Fixed Point and Practice Q15. Two D1 traps are reinforced in passing — #6 (phase versus container state) and #26 (an unschedulable Pod does not error out). The Exam Alert adds **nine** traps the inventory does not carry.

**Research gaps closed by Chapter 13:**

| Gap | Status |
|---|---|
| **G2** — Pod failure signatures by name; *"the single most likely troubleshooting question material"* and B1's **highest-risk single gap in the book** | **5 of 6 closed** — `CrashLoopBackOff`, `ImagePullBackOff`, `ErrImagePull`, `OOMKilled`, `Evicted` all now sourced. **`CreateContainerConfigError` remains open**, verified against all 198 snapshots. |
| **G26** — node lifecycle, conditions, eviction | **Closed** by §4 and §5, jointly with shipped Ch 8 §4. |
| **`container-state.md`'s own open gap** — *"`CrashLoopBackOff` … appears in **no cached snapshot**. Open a research fetch"* | **Closed** by `k8s-docs-container-restart-backoff-2026-08-31`. Ch 5 §5's placeholder can be filled from Chapter 13's corpus. See the shard append. |
| **`restart-policy.md`'s "other five minutes"** — two distinct backoffs sharing a 300s cap, never distinguished | **Substantially discharged** by §4's ⚠ Hazards (*"one retries a pull, the other retries a start"*), one clause short of saying outright that these are two mechanisms that happen to share a number. |

**Still open and touching Chapter 13:** **G1** (the `kubectl` command surface — the cheatsheet snapshot is 13 lines and empty; `kubectl events --for`, `--sort-by`, `--all-containers`, `current-context` and the `RESTARTS`/`READY`/`STATUS` column semantics are all untagged), `CreateContainerConfigError`, admission-refusal outcomes and the ReplicaSet `FailedCreate` event, the Deployment failed-rollout cause list (**⚑ C1 of the integration report**), the storage/`volumeBindingMode` fetch, `crictl`'s command examples, `--event-ttl`'s default, and the Kubernetes release cadence.

---

## Retrieval-practice ledger

| Tested topic | Original chapter | Retested in |
|---|---|---|
| A tag is a mutable pointer; a digest is content identity | ch 2 §3 | ch 13 — Bearings #1 Q6 |
| The `Guaranteed` QoS criteria are evaluated per container | ch 5 §8 | ch 13 — Bearings #2 Q6 |
| kubelet skew — three minors behind, never ahead | ch 8 §6 | ch 13 — Bearings #3 Q2 |
| An object without its component does nothing | ch 10 §3 | ch 13 — Bearings #3 Q3 |

### ⚑ Compliance — and the number depends on the denominator

| Check | B3 target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of **Bearings** | **25%** (Ch 13 is one of five chapters at the ceiling) | 4 of 17 = **23.5%** | ✅ inside the band |
| Retrieval share of the **Practice pool** | same target, *"applied to it once sized"* | **0 of 16 = 0%** | ❌ |
| Retrieval share of **all graded items** (Ch 12's denominator) | 20–25% | 4 of 33 = **12.1%** | ❌ |
| Spacing floor (≥4 chapters back, from Ch 8 on) | ≥1 item | ch 2 is **eleven** back; ch 5 eight; ch 8 five | ✅ comfortably |
| Question inventory | 8 Soundings · ≥10 Bearings across ≥2 checkpoints | 8 + 17 (6+6+5) + 16 = **41** | ✅ |
| Tagged items land on material the named chapter owns | 4 of 4 | **4 of 4**, re-checked against shipped text | ✅ |

**The integration report's 23.5% is correct and incomplete.** Its denominator is checkpoint questions, which is the skill's own literal wording (Part 10: *"20-25% of later **checkpoints** should test EARLIER content"*). B3 goes further — *"B4 sizes the Practice Questions pool; **apply the same target percentage to it once sized**"* — and Ch 12's Stage 14 reported over Bearings + Practice. Under either of those, Chapter 13 is short.

**All four `[retrieval:]` tags are in Bearings. The Practice pool has none** — verified by tag search, not by reading. Chapter 12, by contrast, put five of its eight in Practice.

**In substance the gap is smaller than the number.** Practice carries three `[interleaved: …]` items that genuinely reach back — Q2 to Ch 7's scheduling, Q8 to Ch 6's rollouts, Q9 to Ch 12's Secrets — and each requires holding an earlier-chapter fact and a Chapter 13 fact simultaneously, which is exactly what skill Part 10's interleaving row asks for. The defect is that **a mechanical audit greps `[retrieval:` and reads this pool as empty**, and Ch 19 is built by exactly such an audit.

**Cheapest fix, and it needs no new questions:** dual-tag Q2, Q8 and Q9 as `[retrieval: ch7]`, `[retrieval: ch6]` and `[retrieval: ch12]` alongside their interleave tags. That puts Practice at 3 of 16 = 18.8% and the chapter at 7 of 33 = 21.2%, inside the band on every denominator. Adding one further item on requests-versus-limits — which the Exam Alert already names as the easiest error in the material — reaches the 25% ceiling B3 assigned.

**Soundings note.** All eight are retrieval and the block says so correctly, naming two as deliberate decay probes. Excluded from the budget per B3, and sourced from B2's Prerequisites column exactly as B3's drafting instruction requires.

### Obligations Chapter 13 discharged — fourteen

Ch 2 §3 (tags and digests → Bearings #1 Q6) · Ch 2 §6 (`imagePullPolicy` and `:latest` → §2) · Ch 2 §6 (**diagnosis**, deferred by name in `imagepullbackoff.md` → §2) · Ch 3 §4 (`crictl` and why a node-level tool exists → §5) · Ch 3 §6 (the control loop → §8's close) · Ch 4 §4 (ConfigMaps and Secrets → §2) · Ch 5 §2 (multi-container logs and `-c` → §3, pinned) · Ch 5 §5 (phase versus container state → §1, §2, §4) · Ch 5 §8 (`OOMKilled` and `Evicted`, string released → §4, pinned) · Ch 7 §2/§4 (`Pending` is a report; capacity and taints are indistinguishable without the event → §2, pinned) · Ch 8 §4 (node conditions as a diagnostic → §5) · Ch 8 §6 (version skew *used* rather than recited → §6, pinned) · Ch 10 §3 (the absent-component rule → §7, pinned — **see ⚑ C1 for the form**) · Ch 12 §6 (a refused Pod leaves no object → §2, pinned).

**Three obligations arrived incomplete.** Ch 6 §4's *"which of the six causes"* (twice, once in a graded key) · Ch 11 §2's *"tell those two apart from the symptoms"* · Ch 12's Voyage Ahead promise #2 (**⚑ C3**, new here).

### Forward obligations Chapter 13 creates

| Topic Ch 13 owns | Must be retrieved in | How |
|---|---|---|
| Platform scope hands over when the Pod is `Running`, `Ready`, and the trouble is confined to one workload | **Ch 16 §1** | Reciprocal cross-bearings, both emitted. §8 restates the test in the reader's hearing. |
| `kubectl exec` · `kubectl debug` / ephemeral containers · `kubectl port-forward` | **Ch 16 §3, §5** | Named, withheld, and the withholding is *explained* — "every one of those requires a running container." ⚠ **Ch 16's frontmatter must carry D2.3.** |
| "Is anything even selected" — the Service-side failure | **Ch 16 §4** | §4's readiness material sets it up from the endpoints side. |
| The absent-component pattern, one layer up | **Ch 17 §7** | ⛔ **UNBLOCKED** — see ⚑ C2. Retrieve the rule, add the instance, state no count. |
| metrics-server versus a monitoring system | **Ch 18 §3** | §7 draws the line and cross-bears. Ledger row already assigns it. |
| Node-level logging agents and cluster-level logging backends | **Ch 18 §6** | §7 gives one clause and a pointer, exactly as the ledger requires. |
| The release cadence | **Ch 17 §8** | §6 declines to state it — correctly, since no snapshot holds it and Ch 17 §8 owns it. |
| "Somebody has to install that" as a chapter-to-chapter bridge | **Ch 14** | The Voyage Ahead names metrics-server, a logging backend and an Ingress controller together and asks how anything gets installed at all. |

### Ledger and glossary debts to record at the glossary build

New ledger rows for **cAdvisor**, **Metrics API**, **`ProgressDeadlineExceeded`** (assign to Ch 6 §4, where line 663 already teaches it) and **static Pod / mirror Pod** if the Practice Q13 distractor is kept. Correct the **VPA** row's first appearance from Ch 17 §7 to **Ch 3**, and expand the acronym in place at `chapter-03:606`. Carried forward unchanged from earlier gates: **CNAME**, **BGP**, **eBPF**, **IPVS**, **CIDR** (first used at Ch 8 §4, register wrongly assigns Ch 10 §6), and the sixteen hyphenated "cloud-native" instances.

---

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 13 additions

> ⚠ **MERGE REQUIRED BEFORE PROMOTION.** A further A–Z sequence appended after the
> Chapter 12 block. Appended rather than merged in place because merging would require
> re-transcribing verbatim documentation definitions, and Rule 5 treats definitional drift
> as worse than a duplicated alphabet. Interleave mechanically before promoting this file
> to the shipped back-of-book glossary. No entry below duplicates an entry above.

---

## A

**Admission refusal (as a failure signature)** — A create request rejected at admission
leaves **no Pod object at all**: "there is no Pod object to describe. The refusal happened
at the harbor entrance, and there is no vessel inside to inspect." `kubectl get pod`
returns `NotFound`, which reads like a deletion or a wrong namespace and is neither. The
reason goes to whoever issued the create — your terminal, or the ReplicaSet.
(Chapter 13 §2)

> ⚠ **PROVISIONAL — wholly unsourced.** Neither the "no object is created" consequence nor
> the ReplicaSet-carries-the-reason claim appears in any of the 198 snapshots;
> `k8s-docs-pod-security-admission-2026-08-31` documents the enforce/audit/warn modes only,
> and validating webhooks and ResourceQuota have no snapshot at all. **Graded twice**
> (Bearings #1 Q4 keyed correct; Practice Q9 distractor D). Fetch PSA enforcement outcomes
> and ReplicaSet status conditions / the `FailedCreate` event before this ships.

**API-initiated eviction** — Eviction requested through the API server, as distinct from
node-pressure eviction: *"Node-pressure eviction is not the same as API-initiated
eviction."* `[source: k8s-docs-node-pressure-eviction-2026-08-31]` The node controller uses
this path when a node stays unreachable. (Chapter 13 §4, §5)

> The practical difference is what each respects. A kubelet acting under local pressure
> *"does not respect your configured PodDisruptionBudget or the pod's
> `terminationGracePeriodSeconds`."* `[source: k8s-docs-node-pressure-eviction-2026-08-31]`
> **A node in trouble stops negotiating.**

---

## C

**cAdvisor** — *"Daemon for collecting, aggregating and exposing container metrics included
in Kubelet."* `[source: k8s-docs-resource-metrics-pipeline-2026-08-31]`
(Chapter 13 §7)

> ⚠ **No B7 ledger row and no register row.** *Included in* is the load-bearing phrase: it
> is part of the kubelet binary, present on every node, and nobody installs it. That is what
> makes the metrics-server gap a gap and not an outage.

**Cluster-level logging** — *"In a cluster, logs should have a separate storage and
lifecycle independent of nodes, pods, or containers. This concept is called cluster-level
logging."* And the consequence, stated by the project itself: *"Cluster-level logging
architectures require a separate backend to store, analyze, and query logs. **Kubernetes
does not provide a native storage solution for log data.** Instead, there are many logging
solutions that integrate with Kubernetes."*
`[source: k8s-docs-logging-architecture-2026-08-31]` (Chapter 13 §7)

**`ContainerCreating`** — A container `Waiting` reason: the container is being created.
Normal, briefly; the cause lives nowhere.
`[source: k8s-docs-pod-failure-signatures-2026-08-31]` (Chapter 13 §2)

**`CrashLoopBackOff`** — The documented state: *"This indicates that the backoff delay
mechanism is currently in effect for a container in a crash loop."*
`[source: k8s-docs-container-restart-backoff-2026-08-31]` The chapter's expansion, which is
the examinable content: **"The container started. It ran. It exited. Kubernetes restarted
it. It exited again. Kubernetes is now waiting before trying a third time."**
(Chapter 13 §4; the string is named at Ch 5 §4)

> ★ **It names the waiting between crashes, not the crash.** When you see it, the container
> is neither running nor failing; it is sitting out a delay. Documented causes are broad —
> *"application errors, configuration errors, resource constraints, failing health checks,
> or probe failures"* `[source: k8s-docs-container-restart-backoff-2026-08-31]` — which is
> the point: it tells you the container is dying, not why.
>
> ⚠ **It is the strongest available evidence that the image is fine.** The pull succeeded,
> the configuration resolved, the process started. You cannot loop something that never ran
> once. The shared "BackOff" with `ImagePullBackOff` makes them look like siblings; they are
> opposites — one retries a *pull*, the other retries a *start*.

**`CreateContainerConfigError`** — The kubelet could not assemble the container's
configuration. From the chapter: *"If a referenced ConfigMap does not exist, or a referenced
Secret does not exist, or a named key inside one of them is missing, the kubelet cannot
finish assembling the container. It stops, and reports `CreateContainerConfigError`."*
(Chapter 13 §2)

> ⚠ **PROVISIONAL — the highest-severity gap in this chapter.** The string appears in
> **zero of the corpus's 198 snapshots**, verified by search. It is deliberately lifted out
> of the `Waiting` reason table in §2 rather than presented as sourced from it, because the
> documented fourteen-reason table does not carry it. It cannot be cut: it carries a
> ★ Fixed Point, it is the keyed correct answer to **Bearings #1 Q1** and **Practice Q5**,
> and it is the diagnosis in **Practice Q9**. Fetch the ConfigMap/Secret consumption docs.
>
> The diagnostic value is the distance between symptom and cause: **the Pod scheduled, the
> node was feasible, the image pulled, the registry answered.** Every earlier stage worked.
> The failure is at the last step before the container runs and is caused by an object in a
> different manifest. A missing ConfigMap and a misspelled key *inside* an existing one
> produce the same reason string; `describe` names which.

**`crictl`** — *"a command-line interface for CRI-compatible container runtimes. You can use
it to inspect and debug container runtimes and applications on a Kubernetes node."* Stable
since Kubernetes v1.11; *"requires a Linux operating system with a CRI runtime."*
`[source: k8s-docs-crictl-2026-08-31]` (Chapter 13 §5)

> **What it is for, in one sentence: when the cluster's view and the node's view disagree,
> `crictl` is how you see the node's view.** A container `kubectl` cannot account for but
> `crictl` lists is a container the kubelet failed to register — which localizes the fault
> to the kubelet, not the workload. A container neither can see was never started.
>
> Connects through an endpoint set by `--runtime-endpoint`, the
> `CONTAINER_RUNTIME_ENDPOINT` variable, or `/etc/crictl.yaml`; unconfigured, it *"attempts
> to connect to a list of known endpoints, which might result in an impact to performance."*
> `[source: k8s-docs-crictl-2026-08-31]`

**`crictl logs <id>`** — Reads a container's logs from the runtime directly, bypassing the
API server and the kubelet. (Chapter 13 §5)

**`crictl ps`** — Lists the containers the runtime is actually running on this node.
(Chapter 13 §5)

> ⚠ **PROVISIONAL — both command forms.** `k8s-docs-crictl-2026-08-31` declares `crictl-ps`
> and `crictl-logs` in its frontmatter `concepts_covered`, but the transcription stops at
> the `/etc/crictl.yaml` section and **neither command appears in the body** — verified; the
> file is 37 lines. Every other `crictl` claim in §5 is verbatim-clean. Re-transcribe the
> snapshot's "General usage" examples.
>
> ⚠ **`crictl ps` lists containers; `kubectl get pods` lists Pods.** Comparing the two counts
> is not a diagnosis — **Practice Q13** is built on exactly that error. The real signal
> requires matching identities across `--all-namespaces`, not counting rows.

---

## E

**`ErrImageNeverPull`** — *"The image pull policy is set to `Never`, but the image is not
present locally."* `[source: k8s-docs-pod-failure-signatures-2026-08-31]` Kubernetes does
precisely what it was told: it does not fetch, so the container cannot start. Usually a
locally-built-image pattern from `minikube` or `kind` that has moved to a node without the
image. (Chapter 13 §2)

**`ErrImagePull`** — *"There was a general error pulling the image."*
`[source: k8s-docs-pod-failure-signatures-2026-08-31]` The cause lives in the image name,
the registry, or the credentials — documented as *"invalid image name, or pulling from a
private registry without an imagePullSecret."* `[source: k8s-docs-images-2026-08-23]`
(Chapter 13 §2)

**Event (the Kubernetes object)** — An object like any other: it lives in etcd, it appears
in the API, and — unlike most objects — it is deleted automatically after a retention
window. Events are how the cluster's components report what they did and why, and for
several failure modes they are the **only** place the reason is written: the scheduler's
explanation of why no node was feasible, the kubelet's report of what the registry said, the
Deployment controller's report that a rollout exceeded its deadline.
(Chapter 13 §3; glossed at Ch 8 §2)

**Event retention window (`--event-ttl`)** — The API server's `--event-ttl` flag sets how
long `Event` objects survive.
`[source: k8s-apiserver-event-ttl-and-toleration-defaults-2026-08-31]`
(Chapter 13 §3)

> ⚠ **No duration is stated, deliberately.** The cited snapshot is **14 lines** and stops at
> the `--event-ttl` heading; it holds no default value, despite its own frontmatter claiming
> the retention default is pinned. Verified. **Amend that snapshot's frontmatter** so a later
> chapter reading only the header does not cite a number the corpus does not hold.
>
> ★ **The absence of an event is not evidence.** A Pod that failed overnight shows
> `Events: <none>` in the morning, which reads exactly like "nothing happened." Never
> conclude "there was no error" from an absent event; conclude "I need a different source."

**`Evicted` / node-pressure eviction** — *"Node-pressure eviction is the process by which
the kubelet proactively terminates pods to reclaim resource on nodes."* The kubelet
*"monitors resources like memory, disk space, and filesystem inodes on your cluster's
nodes"* and, at threshold, *"can proactively fail one or more pods on the node to reclaim
resources and prevent starvation."* The outcome is Pod-scoped: *"the kubelet sets the phase
for the selected pods to `Failed`, and terminates the Pod."*
`[source: k8s-docs-node-pressure-eviction-2026-08-31]` (Chapter 13 §4)

> The Pod does not restart in place. If a controller owns it, *"the control plane
> (`kube-controller-manager`) creates new pods in place of the evicted pods."* A bare Pod is
> simply gone. Before touching workloads the kubelet tries to help itself: *"it removes
> unused container images when disk resources are starved."*
>
> ⚠ The literal string `Evicted` as a `Reason` value is **not** in the corpus — the
> node-pressure snapshot documents the *phase* transition to `Failed` and no accompanying
> reason string. It is printed as literal product output in figure `ch13-fig05` and in
> Practice Q6 distractor A. Low risk; source it or paraphrase.

**Eviction order by QoS class** — *"When a Node runs out of resources, Kubernetes will first
evict `BestEffort` Pods running on that Node, followed by `Burstable` and finally
`Guaranteed` Pods."* With one refinement that changes the advice: *"When this eviction is
due to resource pressure, only Pods exceeding resource requests are candidates for
eviction."* `[source: k8s-docs-pod-qos-2026-08-24]` (Chapter 13 §4; QoS classes at Ch 5 §8)

> ⚠ **"BestEffort asks for nothing, so it is the humblest and therefore the safest" is
> exactly backwards.** BestEffort is evicted **first**. A Pod living within its requests is
> not a candidate at all — that is what a request buys you: standing, when the kubelet is
> choosing.

---

## I

**`ImageInspectError`** — *"There was an error inspecting the container image."*
`[source: k8s-docs-pod-failure-signatures-2026-08-31]` (Chapter 13 §2)

> The odd sibling, and the one most treatments skip. The fetch is **not** the problem — the
> runtime has the image and cannot read it. Diagnostically it points at the image or the
> runtime's view of it (a corrupt or truncated layer, an unparseable manifest, a
> partly-populated cache) and **away** from the registry, the image name and the pull
> credentials, which are the first three things anyone checks. Rare, and unmistakable once
> you know what it rules out.

**`ImagePullBackOff` (as a diagnosis)** — *"The container image pull has failed, and kubelet
will keep trying."* `[source: k8s-docs-pod-failure-signatures-2026-08-31]` The retry
behaviour: *"Kubernetes will keep trying to pull the image, with an increasing back-off
delay, up to a compiled-in limit of 300 seconds (5 minutes)."*
`[source: k8s-docs-images-2026-08-23]` (Chapter 13 §2; the string and its taxonomic slot are
Ch 2 §6 and Ch 5 §5, per ledger ⚑2)

> ★ **`ErrImagePull` and `ImagePullBackOff` are the same problem at two moments in time**,
> not two diagnoses. Refresh an `ErrImagePull` and you will usually watch it become
> `ImagePullBackOff`; nothing has changed but the elapsed time.
>
> The three checks, in order: *"make sure that you have the name of the image correct; have
> you pushed the image to the registry?; try to manually pull the image to see if the image
> can be pulled."* `[source: k8s-docs-debug-pods-2026-08-23]` The third is underrated — it
> collapses "Kubernetes problem or registry problem?" in about five seconds.

---

## K

**`kubectl config current-context`** — Confirms which cluster and context answered before
you trust a line of output. Prevents an entire category of confident, well-formatted,
entirely irrelevant diagnosis. (Chapter 13 §3)

> ⚠ Untagged. The command form is not in the corpus — B1 gap **G1**.

**`kubectl describe`** — *"The first step in debugging a Pod is taking a look at it. Check
the current state of the Pod and recent events."* `[source: k8s-docs-debug-pods-2026-08-31]`
It *"shows the state for each container within that Pod."*
`[source: k8s-docs-pod-failure-signatures-2026-08-31]` The reading instruction is
deliberately unglamorous: *"Look at the state of the containers in the pod. Are they all
Running? Have there been recent restarts?"* `[source: k8s-docs-debug-pods-2026-08-23]`
(Chapter 13 §3)

**`kubectl events` · `kubectl get events --sort-by=...`** — Reads the event stream as a
first-class surface rather than as the footer of `describe` output. The sorted form is what
to reach for when you do not yet know which object is at fault: a namespace's events read in
creation order are a chronology of everything the cluster recently tried to do.
(Chapter 13 §3)

> ⚠ **PROVISIONAL — both forms untagged.** `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31`
> claims in its frontmatter to close B1 gap **G1** and is **13 lines long** — frontmatter and
> one heading, no command lines — and its own note concedes `kubectl events` is not covered.
> Verified. Fetch `kubernetes.io/docs/reference/kubectl/generated/kubectl_events/` for the
> `--for` selector.

**`kubectl logs` · `-c` · `--all-containers` · `--previous`** — Kubernetes *"captures logs
from each container in a running Pod"*
`[source: k8s-docs-logging-architecture-2026-08-31]`. `-c <container>` names one container
in a multi-container Pod `[source: k8s-docs-logging-architecture-2026-08-23]`;
`--all-containers` returns all of them; and `--previous` *"retrieves logs from a previous
instantiation of a container."* `[source: k8s-docs-logging-architecture-2026-08-23]`
(Chapter 13 §3)

> ★ **On a crash-looping Pod, `kubectl logs` reads the container that has not started yet
> and returns nothing. `kubectl logs --previous` reads the container that died.** If a Pod
> is restarting and its logs are empty, you have used the wrong command, not discovered a
> silent application.
>
> One bounded resource: *"By default, if a container restarts, the kubelet keeps one
> terminated container with its logs."*
> `[source: k8s-docs-logging-architecture-2026-08-23]` One. `--previous` gets the most recent
> death; the one before that is gone.

**`kubectl top`** — Queries the Metrics API for CPU and memory usage. Requires
metrics-server. (Chapter 13 §7; named at Ch 3 §4)

> ★ **An error from `kubectl top` is a statement about what is installed on the cluster, not
> about the workload you asked about.** Note the *shape* of the error: not "no data" but "no
> such resource," because the API itself is not being served. A metrics-server that were
> installed but had not finished a scrape would return empty *data* — a different error, and
> the difference is the diagnosis (**Bearings #3 Q1**).

---

## M

**Metrics API** — *"Kubernetes API supporting access to CPU and memory used for workload
autoscaling. To make this work in your cluster, you need an API extension server that
provides the Metrics API."* `[source: k8s-docs-resource-metrics-pipeline-2026-08-31]`
(Chapter 13 §7)

> ⚠ **No B7 ledger row, and it reaches graded text** — Bearings #3 Q1 and Q3, Practice Q15.
> Needs a row, not just a glossary entry.
>
> It is not part of the core API server. The API exists as a specification; it does not exist
> on your cluster until something serves it.

**metrics-server** — *"Cluster addon component that collects and aggregates resource metrics
pulled from each kubelet. The API server serves Metrics API for use by HPA, VPA, and by the
`kubectl top` command. Metrics Server is a reference implementation of the Metrics API."*
And, blunter: it *"is a cluster addon component (not deployed by default in all
distributions)."* `[source: k8s-docs-resource-metrics-pipeline-2026-08-31;
k8s-docs-resource-metrics-pipeline-2026-08-23]` (Chapter 13 §7; named at Ch 3 §4)

> **Scope, stated by the source:** it *"is meant only for autoscaling purposes — for example,
> don't use it to forward metrics to monitoring solutions, or as a source of monitoring
> solution metrics."* `[source: k8s-docs-resource-metrics-pipeline-2026-08-23]` It holds
> current values. It keeps no history. It is not a monitoring system.
>
> ⚠ **Do not name which distributions install it.** The corpus goes exactly as far as "not
> deployed by default in all distributions" and no further; an earlier draft's per-distribution
> breakdown was cut for that reason.

**mirror Pod** — The API-side representation of a static Pod. Static Pods are *"managed
directly by the kubelet and represented by mirror Pods"* in the API server.
`[source: k8s-docs-pod-failure-signatures-2026-08-31]`
(Chapter 13, Practice Q13 answer key)

> ⚠ **PROVISIONAL — first appearance in the book is inside a graded answer key.** Confirmed
> absent from Chapters 1–12. This is the weakest possible teaching position and it breaches
> the B7 orphan doctrine's rule that a term in an answer key may not be glossary-only.
> **Precedent: the Ch 9 gate rebuilt a Practice Q16 distractor from taught material so that
> no graded item depended on eBPF.** Do the same — Q13's distractor D can be rebuilt from
> §5's own kubelet-registration material — or add ledger rows for both terms.

---

## N

**Node conditions as a diagnostic** — The reading that turns a condition into an
instruction. `Ready=True` → the node is not your problem, return to the workload.
`Ready=False` → somebody is reporting a problem; read the kubelet's own logs on that machine.
`Ready=Unknown` → nobody is reporting at all; suspect the kubelet process, the machine, or
the network to the control plane. `MemoryPressure=True` → expect evictions, and your Pod's
failure is probably not its own fault. `DiskPressure=True` → expect image garbage collection
and evictions, and suspect pull failures. `PIDPressure=True` → container starts will fail
confusingly; look for a process-leaking workload. (Chapter 13 §5)

> **The conditions themselves are Ch 8 §4's** and are not redefined here — ledger ⚑1. See
> `concepts/node-conditions.md`, which holds the definitions and the ★ callout on
> `False` versus `Unknown`.
>
> ⚓ When several unrelated Pods on one node fail in *different* ways at the same time, stop
> diagnosing the Pods and describe the node. Correlated, heterogeneous failures on one node
> are almost never a coincidence of workloads.

---

## O

**`OOMKilled`** — *"The container ran out of memory."*
`[source: k8s-docs-pod-failure-signatures-2026-08-31]` Container-scoped by design: *"Any
Container exceeding a resource limit will be killed and restarted by the kubelet without
affecting other Containers in that Pod."* `[source: k8s-docs-pod-qos-2026-08-24]` The Pod
survives, the other containers survive, the killed container restarts in place per its
`restartPolicy`, and the restart count goes up. (Chapter 13 §4; the mechanism is Ch 5 §8)

> ⚑ **The book asserts two different agents for this kill and reconciles neither.** Shipped
> Ch 5 §8 says *"the kernel may terminate it… terminations only happen when the kernel
> detects memory pressure"* `[source: k8s-docs-resource-management-2026-08-23]`; Chapter 13
> says the kubelet. Both are true at different altitudes. The kubelet version sits in two
> graded keys (Bearings #2 Q1, Practice Q6). **See `concepts/resource-limit.md` before
> editing either.**
>
> ⚠ The cited reason table places `OOMKilled` among the **`Waiting`** reasons. §4 and
> Bearings #2 Q1's stem frame it as a **`Terminated`** reason with an exit code, which is
> what practitioners see under Last State and what shipped Ch 5 §8 establishes for the
> memory-limit kill. The framing is canon; the *string's* placement on `Terminated` is the
> book's own join, soundly made and nowhere cited.
>
> 🪢 **OOM** = **O**ne container, **O**ver its own limit, **O**n the same node afterward.
> Repeated OOM kills surface in `kubectl get pods` as `CrashLoopBackOff`; the two are not
> alternatives but two altitudes of one event, and `describe` shows the lower one.

---

## P

**Platform scope vs application scope** — The two-audience split the Kubernetes
documentation makes about itself: the application guide *"is to help users debug
applications that are deployed into Kubernetes and not behaving correctly. This is *not* a
guide for people who want to debug their cluster"*
`[source: k8s-docs-debug-pods-2026-08-31]`, and the cluster guide assumes *"you have already
ruled out your application as the root cause."*
`[source: k8s-docs-debug-cluster-2026-08-31]` (Chapter 13 §1)

> ★ **The mechanical test:** *"If the Pod is `Running` and `Ready`, the failure is confined
> to that one workload, and the behavior is still wrong, you have crossed into application
> scope."*
>
> ⚠ **The middle clause is load-bearing and is the one people drop.** A cluster-wide network
> fault — DNS not resolving, the CNI plugin not wiring Pods up, the service proxy not
> programming its rules — produces Pods that are `Running` and `Ready` and behave wrongly,
> and is unambiguously the platform's problem. The tell is that it is not confined to one
> workload. Several unrelated applications wrong at once: do not cross the line; go to the
> network.

**`PodInitializing`** — A container `Waiting` reason: the Pod is being initialized — an init
container has not finished, or is failing.
`[source: k8s-docs-pod-failure-signatures-2026-08-31]` A single looping init container holds
the whole Pod at the gate indefinitely. (Chapter 13 §2)

> Platform scope identifies *which* init container is stuck and whether it is running or
> looping — a `describe` question. What it is doing wrong is application scope, Ch 16 §2.

**Probe failure signatures** — The two shapes, and one of them is silent.
**Liveness fails** → the kubelet kills the container and applies the restart policy
`[source: k8s-docs-pod-lifecycle-2026-08-23]`; from outside, indistinguishable from an
application crashing on its own. **Readiness fails** → the Pod stays `Running`, does not
restart, reports `0/1 Ready`, and *"the endpoints controller removes the Pod's IP address
from the endpoints of all Services that match the Pod."*
`[source: k8s-docs-pod-lifecycle-2026-08-23]` (Chapter 13 §4; the probes are Ch 5 §7)

> ★ **A liveness failure restarts the container. A readiness failure removes the Pod from
> Service endpoints and changes nothing else.** The second is the chapter's quietest failure:
> `Running`, `0/1 Ready`, zero restarts, no traffic. Anyone reading only `STATUS` concludes
> the Pod is healthy. **The `READY` column is the tell** — `1/1` and `0/1` both print
> `Running` beside them.
>
> The liveness case matters because the fixes are opposite. If the application is crashing,
> fix the application. If the probe is wrong — too short a timeout, too aggressive an
> `initialDelaySeconds`, a health endpoint slow under load — the application is *fine* and
> the probe is manufacturing an outage.

**`ProgressDeadlineExceeded`** — A Deployment condition reporting that the rollout did not
finish in time. It says nothing at all about why; several quite different underlying causes
produce the identical condition, and the actual reason lives in the events on the new
ReplicaSet and on its Pods. (**Chapter 6 §4**; used diagnostically at Chapter 13 §3 and in
Practice Q8)

> ⚠ **PROVISIONAL, and the book currently disagrees with itself.** No Deployment or rollout
> snapshot is in Chapter 13's corpus, so neither the condition, the `progressDeadlineSeconds`
> mechanism, nor the cardinality of its causes is tagged. **Shipped Ch 6 promises "the six
> causes" twice — once in a graded answer key at `chapter-06:778` — and Chapter 13 §3 names
> none.** Fetch
> `kubernetes.io/docs/concepts/workloads/controllers/deployment/#failed-deployment` and
> either restore a sourced count in §3 or amend both Ch 6 sites. **No ledger row exists;
> assign one to Ch 6 §4.**

---

## R

**Resource metrics pipeline** — The path from container to consumer, of which only one link
is optional. **cAdvisor** gathers, inside the kubelet binary, on every node. **The kubelet**
exposes what it gathered: *"Resource metrics are accessible using the `/metrics/resource`
and `/stats` kubelet API endpoints."* **metrics-server** — the missing piece — collects and
aggregates across kubelets. **The Metrics API** is what HPA, VPA and `kubectl top` query.
`[source: k8s-docs-resource-metrics-pipeline-2026-08-31]` (Chapter 13 §7)

> ★ **Everything except metrics-server is already running on your cluster right now.** The
> measurements exist; nothing is publishing them. Nothing needs *enabling* — the kubelet
> endpoints are already serving — which is the misreading **Practice Q15 distractor D**
> exists to catch.
>
> The same absence has a second consequence people meet separately and never connect: **a
> HorizontalPodAutoscaler reads the same Metrics API.** An HPA created without metrics-server
> is accepted like any other object, has no metric source, and never scales anything.
> *[[absent-component-pattern]], one layer up.*

**Restart backoff curve** — *"After containers exit, the kubelet restarts them with an
exponential backoff delay: 10s, 20s, 40s, …, capped at 300 seconds (5 minutes). Once a
container executes successfully for 10 minutes without problems, the kubelet resets the
restart backoff timer."* `[source: k8s-docs-container-restart-backoff-2026-08-31]`
(Chapter 13 §4; owned at Ch 5 §4)

> Two consequences worth carrying. A long-crashing Pod appears to do nothing for up to five
> minutes at a stretch — that is the cap, not a hang. And the reset requires **ten minutes of
> successful running**, so a container that dies every eight minutes never resets and
> escalates to the cap forever, while technically "working" most of the time.
>
> ⚑ **This is a *different* backoff from `ImagePullBackOff`'s**, which also caps at 300
> seconds. One governs restarts, the other pulls. See `concepts/restart-policy.md` — the
> shard has been asking for this distinction since Chapter 5.

---

## S

**static Pod** — A Pod *"managed directly by the kubelet and represented by mirror Pods"* in
the API server. `[source: k8s-docs-pod-failure-signatures-2026-08-31]`
(Chapter 13, Practice Q13 answer key)

> ⚠ Same PROVISIONAL status as **mirror Pod** above. Note the diagnostic point Q13 makes:
> because static Pods *are* represented in the API, they are **not** a source of containers
> hidden from `kubectl`.

---

## T

**Triage order (S-P-C-E-L)** — **Scope → phase → conditions → events → logs.**
(Chapter 13 §1)

> 🪢 If you are typing `kubectl logs` and cannot say out loud what phase the Pod is in, you
> have skipped four steps.
>
> **Why logs come last, argued rather than asserted.** A `Pending` Pod has no container. A
> `CrashLoopBackOff` Pod's current container has not started. An `Evicted` Pod is off the
> node. All three return nothing, and "nothing" is indistinguishable from "the app is quiet."
> **Three causes, one output. The phase separates them instantly.** Logs are not useless;
> they are the last signal to become *trustworthy*, because they only mean what you think
> they mean once you know the container ran.

---

## V

**Version-skew symptom shapes** — Skew as something you meet as a symptom rather than
recite as a rule. **A skewed client:** a resource type reported not to exist, a valid field
rejected, output missing columns another engineer sees — because *"`kubectl` is supported
within one minor version (older or newer) of `kube-apiserver`."* Neither error says "your
client is old"; both send you to your YAML. **A skewed kubelet:** one node behaving
differently, a feature working everywhere else — because an old kubelet is *supported*
(*"up to three minor versions older"*) but does not implement API fields added after its
release, and **accepts a spec containing them and silently does not act on them.**
`[source: k8s-version-skew-policy-2026-08-31]` (Chapter 13 §6; the rule is Ch 8 §6)

> **Ruling it out costs a minute:** `kubectl version` for the client, `kubectl get nodes -o
> wide` for each node's kubelet version. The project asks for both when you report a
> problem — *"Kubernetes version: `kubectl version`"* and *"container runtime version"*
> `[source: k8s-docs-troubleshooting-overview-2026-08-31]` — which tells you how often it is
> the answer.
>
> ⚓ **Known issues are a legitimate triage step, not a defeat.** The same troubleshooting
> page closes with *"You should also check the known issues for the release you're using."*
> `[source: k8s-docs-troubleshooting-overview-2026-08-31]` The project *"maintains release
> branches for the most recent three minor releases,"* each with *"approximately 1 year of
> patch support"* `[source: k8s-version-skew-policy-2026-08-31]`, so a genuine, already-known
> bug is described in the notes of the version you are running.
>
> ⚠ **No release cadence is stated here.** The corpus holds the three-release support window
> and the ~1 year of patch support and nothing about releases per year; Ch 17 §8 owns the
> cadence.

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/platform-scope-vs-application-scope.md ===
# Concept: Platform scope vs application scope

**Home:** Chapter 13 §1 · **Competency:** D2.3 · **Status:** canonical
**Reciprocal:** Ch 16 §1 (application scope) · **B1 trap #71** · **D3.2 trap #87**

## The split is the documentation's own

The two Kubernetes debugging guides each assume the other's work is done. The application
guide: *"This is **not** a guide for people who want to debug their cluster."*
`[source: k8s-docs-debug-pods-2026-08-31]` The cluster guide: *"we assume you have already
ruled out your application as the root cause."* `[source: k8s-docs-debug-cluster-2026-08-31]`

That is not an oversight. There are two audiences, and the first move in any investigation
is deciding which one you are.

## ★ The mechanical test — and the clause everyone drops

> If the Pod is `Running` **and** `Ready`, the failure is **confined to that one workload**,
> and the behavior is still wrong — you have crossed into application scope.

**All three conditions, not two.** A cluster-wide network fault (DNS not resolving, the CNI
plugin not wiring Pods up, the service proxy not programming rules) produces Pods that are
`Running` and `Ready` and behave wrongly, and is unambiguously the platform's problem. The
tell is that it is **not confined to one workload**. Several unrelated applications wrong at
once → go to the network, not to the code.

## The handoff runs one way

Platform scope asks whether Kubernetes did its job: did the Pod get scheduled, did the image
pull, did the container start, is the node healthy, did something kill it. Application scope
asks whether the code is doing its job. You cross the line **exactly once per investigation,
and only in that direction.**

## Why `exec`, `debug` and `port-forward` are absent from Chapter 13

They are real tools, they are on the D2.3 competency list, and every one of them **requires a
running container** — a question you only ask once the platform has succeeded. Chapter 13
names all three and routes them to Ch 16 §3 and §5 rather than leaving the reader to wonder.

⚑ **Objective-tagging consequence.** Those tools, plus the whole *Troubleshooting
Applications* concept row and *local service debugging*, are D2.3 material living in a
chapter filed under D3.2. **Ch 16's frontmatter must carry `objectives: ["D3.2", "D2.3"]`**
or roughly a third of D2.3 shows no owning chapter in the coverage report.

## Related

[[triage-order]] · [[read-the-phase-first]] · [[pod-phase]] · [[node-conditions]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/triage-order.md ===
# Concept: The triage order — S-P-C-E-L

**Home:** Chapter 13 §1 · **Competency:** D2.3 · **Status:** canonical
**Closes B1 trap #70** (jumping to `kubectl logs` for a `Pending` Pod)

## The order

> **Scope → phase → conditions → events → logs.**

🪢 **S-P-C-E-L.** If you are typing `kubectl logs` and cannot say out loud what phase the Pod
is in, you have skipped four steps.

## ★ Why logs come last — an argument, not a rule

This is the part every reader resists, so the chapter argues it rather than asserting it.

| Failure | What `kubectl logs` returns | Why |
|---|---|---|
| `Pending` | nothing | no container exists |
| `CrashLoopBackOff` | nothing | the *current* container has not started; the kubelet is waiting out a backoff |
| `Evicted` | nothing | the Pod is off the node; its logs went with it |

**Three completely different causes. One identical output.** The logs cannot distinguish
between them; the phase distinguishes between them instantly.

Logs are not useless. They are the **last signal to become trustworthy**, because they only
mean what you think they mean once you already know the container ran. The phase tells you
whether the container ran. So the phase goes first.

## Each reading narrows the next

Scope tells you which cluster you are looking at; the phase tells you which shore; the
conditions tell you which rock; the events tell you what the lookout actually called. By the
time you reach the logs there is very little water left — which is exactly why the logs can
finally be read for what they say rather than for what you hope they say.

## The order maps to components, not to commands

Each position in the platform's start-up sequence has an owner: **the scheduler** owns
placement, **the kubelet** owns pulling and starting, **the container runtime** owns running,
**the node controller** owns whether the node is answering at all. Reading the phase is not
recognizing a string — it is taking the bearing that tells you which coast the rest of the
fix is measured against.

## Related

[[platform-scope-vs-application-scope]] · [[read-the-phase-first]] · [[kubernetes-events]] ·
[[reading-container-logs]] · [[pod-phase]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-failure-never-started.md ===
# Concept: The never-started failure family

**Home:** Chapter 13 §2 · **Competency:** D2.3 · **Status:** canonical
**Closes:** most of B1 gap **G2**, the book's highest-risk single gap

## The property every member shares

> **No container ever executed.**

Nothing ran, so nothing logged, so no amount of log-reading will help. What separates the
members is **how far into the start-up sequence the platform got before it stopped.**

## ★ The restart count halves your search space for free

Zero restarts and not running → never started; you are in this family.
Non-zero restarts → it started and something ended it; you are in
[[pod-failure-started-then-died]].

One column of `kubectl get pods`, read before you describe anything.

⚠ The `RESTARTS`, `READY` and `STATUS` column semantics are **untagged** — B1 gap **G1**.
Two graded items rely on them (Bearings #1 Q2, Practice Q3).

## The branch structure

The first question is not "what is the error" but **"is there a Pod at all."**

1. **No Pod object** → admission refused it. See [[admission-refusal-leaves-no-pod]].
2. **`Pending`** → not scheduled. See [[pending-pod]].
3. **Scheduled, containers `Waiting`** → read the container `Reason`:
   - the pull family → [[image-pull-failure-family]]
   - `CreateContainerConfigError` → [[createcontainerconfigerror]]
   - `PodInitializing` → an init container has not finished

## The documented `Waiting` reasons this family uses

`ContainerCreating` (normal, briefly) · `ErrImagePull` · `ImagePullBackOff` ·
`ImageInspectError` · `ErrImageNeverPull` · `PodInitializing`
`[source: k8s-docs-pod-failure-signatures-2026-08-31]`

**`CreateContainerConfigError` is not in that table** and is deliberately presented outside
it. See its own shard.

## Boundary held — ledger ⚑2

Chapter 2 §6 and Chapter 5 §5 own the *string* and its *taxonomic slot*; Chapter 13 §2 owns
the **diagnosis**. §2 applies the phase/state distinction without re-teaching it, which is
what the flag required.

## Related

[[pod-failure-started-then-died]] · [[triage-order]] · [[container-state]] · [[pod-phase]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/admission-refusal-leaves-no-pod.md ===
# Concept: An admission refusal leaves no Pod object

**Home:** Chapter 13 §2 · **Competency:** D2.3 · **Status:** ⚠ **PROVISIONAL — UNSOURCED**
**Graded:** Bearings #1 Q4 (keyed correct) · Practice Q9 distractor D

## The claim

A Pod rejected at admission — by Pod Security Admission, a validating webhook, or a quota —
leaves **no Pod object to describe.** `kubectl get pod` returns `NotFound`, whose natural
reading is "something deleted it" or "wrong namespace." Neither is true: the object never
existed, and the rejection went to whoever issued the create — your terminal for
`kubectl apply`, the ReplicaSet's status for a controller.

🪝 **A Deployment whose Pods are refused does not fail loudly.** It sits at zero available
replicas and the reason is on the **ReplicaSet**, not on any Pod.
`kubectl describe replicaset <name>` is where the message is. Chasing the missing Pod finds
nothing, because there is nothing to find.

## ⛔ Sourcing status — do not promote

**Neither half of this is supported by any of the corpus's 198 snapshots**, verified by
search:

- `k8s-docs-pod-security-admission-2026-08-31` documents the enforce/audit/warn modes and
  **not** the "no object is created" consequence.
- Validating webhooks and `ResourceQuota` have **no snapshot at all**.
- The ReplicaSet-carries-the-reason claim has no snapshot.

It cannot be cut: it is the top branch of §2's signature map and the keyed answer to a graded
item. **Route a Stage 2 fetch for (a) PSA enforcement outcomes and (b) ReplicaSet status
conditions / the `FailedCreate` event, then tag every occurrence.**

## Why it belongs in the never-started family and not beside it

The whole family means no container executed. This member means *no object executed* — one
stage earlier than everything else, before the scheduler ever sees the request. That is why
`Practice Q9 D` is the sharp distractor: the Pod in that stem exists and is describable,
which rules admission out entirely.

## The Chapter 12 handoff

`chapter-12:1340`: *"it shows up at a different point in the triage flow."* This is that
point, and Chapter 13 §2 says so. Obligation discharged.

## Related

[[pod-failure-never-started]] · [[admission-control]] · [[api-access-gates]] ·
[[pod-security-standards-and-admission]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/createcontainerconfigerror.md ===
# Concept: `CreateContainerConfigError`

**Home:** Chapter 13 §2 · **Competency:** D2.3 · **Status:** ⚠ **PROVISIONAL — UNSOURCED**
**Graded three times:** Bearings #1 Q1 (keyed) · Practice Q5 (keyed) · Practice Q9 (the diagnosis)

## What it means

A container's configuration includes everything the kubelet must gather before handing a
container definition to the runtime: environment variables, mounted volumes, and the contents
of any ConfigMap or Secret the Pod references. If a referenced ConfigMap does not exist, or a
referenced Secret does not exist, or a named key inside one of them is missing, **the kubelet
cannot finish assembling the container.** It stops, and reports this reason.

## ★ The distance between symptom and cause is the whole lesson

Notice what has **not** gone wrong. The Pod scheduled successfully; the node was feasible.
The image pulled successfully; the registry answered. **Every earlier stage worked.** The
failure is at the last step before the container runs, and it is caused by an object in a
completely different part of your manifests.

🪝 A missing ConfigMap and a **misspelled key inside an existing** ConfigMap produce the same
reason string. `describe` names which one it could not resolve. Read the message, not just
the reason.

## ⛔ Sourcing status — the highest-severity gap in Chapter 13

**The string appears in zero of the corpus's 198 snapshots.** Verified by search across
`sources/`, not inferred. The documented `Waiting` reason table
(`k8s-docs-pod-failure-signatures-2026-08-31`) lists fourteen reasons and **this is not one
of them**, which is why §2 lifts it out of that table rather than presenting it as sourced
from it — the right call, and it should not be undone.

It cannot be cut: it carries a ★ Fixed Point, it is the keyed answer to two graded items and
the diagnosis in a third, and it is one of the nine signatures the ☀️ Zenith is built on.

**Fetch:** the ConfigMap and Secret consumption docs — *"the kubelet reports an error if the
ConfigMap doesn't exist"* is the most likely home, since the rendered reason table does not
carry it. **The same fetch covers Practice Q9's answer-key claim** that Kubernetes does not
validate a referenced Secret's existence at admission time.

## Two obligations it discharges

- `chapter-12:1099` — *"a Pod that references a Secret which does not exist does not get a
  running container… a recognizably different shape from a Pod that runs and then dies."*
  Delivered exactly, with the reason string Chapter 12 deliberately withheld.
- Chapter 12's Voyage Ahead promise #3. ✓

## Related

[[pod-failure-never-started]] · [[configmap]] · [[secret]] · [[container-state]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/image-pull-failure-family.md ===
# Concept: The image-pull failure family

**Home:** Chapter 13 §2 · **Competency:** D2.3 · **Status:** canonical
**The string and its slot:** Ch 2 §6 + Ch 5 §5 (ledger ⚑2) · **This shard is the diagnosis**

## Four reasons, one family

| `Reason` | Verbatim | Cause lives in |
|---|---|---|
| `ErrImagePull` | *"There was a general error pulling the image."* | image name, registry, or credentials |
| `ImagePullBackOff` | *"The container image pull has failed, and kubelet will keep trying."* | same — this is `ErrImagePull` after retries began |
| `ImageInspectError` | *"There was an error inspecting the container image."* | the image itself, or the runtime's view of it |
| `ErrImageNeverPull` | *"The image pull policy is set to `Never`, but the image is not present locally."* | the Pod spec's `imagePullPolicy` |

`[source: k8s-docs-pod-failure-signatures-2026-08-31]`

## ★ The first two are one diagnosis at two moments

*"`ImagePullBackOff` is not a different diagnosis from `ErrImagePull`. It is the same
diagnosis, observed a little later."* Refresh an `ErrImagePull` and you will usually watch it
become `ImagePullBackOff`; nothing has changed except elapsed time. The retry behaviour is
documented: *"with an increasing back-off delay, up to a compiled-in limit of 300 seconds
(5 minutes)."* `[source: k8s-docs-images-2026-08-23]`

## The three checks, in order

*"make sure that you have the name of the image correct; have you pushed the image to the
registry?; try to manually pull the image to see if the image can be pulled."*
`[source: k8s-docs-debug-pods-2026-08-23]`

The third is underrated: pulling by hand collapses "is this a Kubernetes problem or a
registry problem?" in about five seconds.

## `ImageInspectError` is the one everyone skips

The fetch is **not** the problem — the runtime has the image and cannot read it. That points
at a corrupt or truncated layer, an unparseable manifest, or a partly-populated cache, and
**away** from the registry, the image name and the credentials, which are the first three
things anyone checks. Rare; unmistakable once you know what it rules out.

## The availability cost hiding in `imagePullPolicy: Always`

A cached image is provisions already aboard, but with `Always` the kubelet still hails the
registry before using them: it *"queries the container image registry to resolve the name to
an image digest"* on every launch, and *"if the kubelet has a container image with that exact
digest cached locally, it uses its cached image."* `[source: k8s-docs-images-2026-08-23]`

**The bandwidth cost is small. The availability cost is not.** A Pod running happily for
weeks on a cached image fails to restart the moment the registry becomes unreachable. A Pod
pinned to a specific tag other than `:latest` gets `IfNotPresent` and rides out the same
outage without noticing.

## Related

[[imagepullbackoff]] · [[imagepullpolicy]] · [[tag-vs-digest]] · [[registry]] ·
[[pod-failure-never-started]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubernetes-events.md ===
# Concept: Events as a diagnostic surface

**Home:** Chapter 13 §3 · **Competency:** D2.3 · **Status:** canonical
**Glossed at:** Ch 8 §2 · **Retention flagged:** see the ⚑ below

## Not the footer of `describe`

Most readers meet events as the bottom third of `describe` output and treat them as
supplementary. They are how the components of the cluster **tell you what they did and why**,
and for several failure modes they are the *only* place the reason is written:

- the scheduler's explanation of why no node was feasible
- the kubelet's report that the pull failed, and what the registry said
- the Deployment controller's report that a rollout exceeded its progress deadline

```
kubectl events --for pod/<pod-name>
kubectl get events --sort-by=.metadata.creationTimestamp
```

The second form is what to reach for when you do not yet know which object is at fault:
events are not sorted usefully by default, and a namespace's stream read in creation order is
a chronology of everything the cluster recently tried to do.

⚠ **Both forms are untagged.** B1 gap **G1**, and the snapshot that claims to close it
(`k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31`) is **13 lines** with no command
lines at all. Verified.

## The ownership chain, worked

A Deployment shows `ProgressDeadlineExceeded`. Describe it → it only says it gave up waiting.
Find the new ReplicaSet → describe it → three Pods. Describe one → container `Waiting`,
`Reason: ImagePullBackOff`, and its events carry the registry's actual refusal: an
authentication failure. **`ProgressDeadlineExceeded` never mentioned images, registries, or
credentials. Three `describe` calls down the ownership chain did.**

## ★ Events expire, and an absent event is not evidence

An `Event` is an object like any other — it lives in etcd, appears in the API, and, unlike
most objects, **is deleted automatically after a retention window** set by the API server's
`--event-ttl`. `[source: k8s-apiserver-event-ttl-and-toleration-defaults-2026-08-31]`

> A Pod that failed overnight shows `Events: <none>` in the morning, which reads exactly like
> "nothing happened." Something happened. The record of it expired.
>
> **Never conclude "there was no error" from an absent event. Conclude "I need a different
> source"** — a monitoring system, a log aggregator, or a reproduction.

⚠ **No duration is stated in the chapter, deliberately.** The cited snapshot is **14 lines**
and stops at the `--event-ttl` heading; it holds no default, despite its own frontmatter
claiming the retention default is pinned. Verified. **Amend that frontmatter.** If a later
fetch pins the default, it may be added as a dated illustration, never as the examinable fact.

## Where to go when the events are gone

The audit log answers a *different* question — who called the API, and what did they change —
and has its own retention, but when events have expired it is sometimes the only surviving
record that a change was made at all. See [[auditing]] (Ch 8 §2).

## Related

[[triage-order]] · [[reading-container-logs]] · [[cluster-level-logging]] · [[auditing]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/reading-container-logs.md ===
# Concept: Reading container logs — the three flags

**Home:** Chapter 13 §3 · **Competency:** D2.3 · **Status:** canonical

## The commands

```
kubectl logs <pod>
kubectl logs <pod> -c <container>
kubectl logs <pod> --all-containers
kubectl logs <pod> --previous
```

Kubernetes *"captures logs from each container in a running Pod"*
`[source: k8s-docs-logging-architecture-2026-08-31]`, and by default `kubectl logs` reads the
**current instantiation** of the container in a single-container Pod.

## `-c` — the misdiagnosis that costs an afternoon

For a multi-container Pod, `-c <container>` is how you say which one you mean
`[source: k8s-docs-logging-architecture-2026-08-23]`. On a Pod with `app`, `cache` and
`log-shipper`, a bare `kubectl logs` cannot know which you intended, and **reading the wrong
container's silence and concluding the application is broken is a real and common
misdiagnosis.**

`chapter-05:392` handed this case here by name. Obligation discharged.

## ★ `--previous` — the flag this chapter exists for

*"retrieves logs from a previous instantiation of a container."*
`[source: k8s-docs-logging-architecture-2026-08-23]`

> **On a crash-looping Pod, `kubectl logs` reads the container that has not started yet, and
> returns nothing. `kubectl logs --previous` reads the container that died, and returns the
> reason.**
>
> If a Pod is restarting and its logs are empty, you have used the wrong command, not
> discovered a silent application.

## One bounded resource

*"By default, if a container restarts, the kubelet keeps one terminated container with its
logs."* `[source: k8s-docs-logging-architecture-2026-08-23]` **One.** Not a history.
`--previous` gets the most recent death; the one before that is gone.

## Related

[[cluster-level-logging]] · [[multi-container-pod]] · [[crashloopbackoff]] ·
[[kubernetes-events]] · [[crictl]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-failure-started-then-died.md ===
# Concept: The started-then-died failure family

**Home:** Chapter 13 §4 · **Competency:** D2.3 · **Status:** canonical

## The property every member shares

> **A container ran.**

That single distinction is the most valuable thing in Chapter 13, and the restart count gives
it to you for free. A container that ran left evidence: an exit code, a termination reason,
and logs readable with `--previous`. The diagnostic question is no longer "why won't it
start" but **"what ended it, and what triggered the ending."**

## Members

| Signature | Trigger | Scope | Outcome |
|---|---|---|---|
| [[crashloopbackoff]] | the process exits, repeatedly | one container | restarted in place, with escalating delay |
| `OOMKilled` | this container's **own limit** | one container | restarted in place, same node |
| `Evicted` | the **node's** pressure | the whole Pod | Pod `Failed`; replacement elsewhere |
| liveness probe failure | the probe, not the process | one container | restart loop |
| readiness probe failure | the probe | the Pod's Service membership | **nothing restarts** — see below |

## The one that leaves no restart count

A readiness failure is the family's outlier and its quietest member: the Pod stays `Running`,
does not restart, reports `0/1 Ready`, and is silently removed from its Service's endpoints.
It belongs to this family by *timing* — the container did run — and to none of it by
*evidence*. See [[probe]].

## The contract with the other family

Zero restarts and not running → [[pod-failure-never-started]].
Non-zero restarts → here.

## ⚑ Chapter 12 handed a fifth trigger forward and it did not arrive

`chapter-12:2223` promised the reader that *"a container that cannot write where it expects
to write is a permissions failure wearing an application error's clothing,"* naming
`securityContext` as the thing to bring. **`runAsUser`, `runAsNonRoot`, `securityContext` and
`readOnlyRootFilesystem` return zero occurrences in Chapter 13.**

§4 already quotes the documented cause list — *"application errors, configuration errors,
resource constraints, failing health checks, or probe failures"*
`[source: k8s-docs-container-restart-backoff-2026-08-31]` — and never says which
configuration. **One clause naming `securityContext` among the configuration errors
discharges the promise and needs no fetch.** This is the right home for it, not Ch 16: a
platform cause producing an application-looking symptom is precisely the discrimination §1
teaches.

## Related

[[pod-failure-never-started]] · [[oomkilled-vs-evicted]] · [[restart-policy]] ·
[[resource-limit]] · [[securitycontext]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/crashloopbackoff.md ===
# Concept: `CrashLoopBackOff`

**Home:** Chapter 13 §4 · **Competency:** D2.3 · **Status:** canonical
**Closes:** the open ⚑ vocabulary gap recorded in [[container-state]] since Chapter 5

## Say it out loud, because the name works against you

> **The container started. It ran. It exited. Kubernetes restarted it. It exited again.
> Kubernetes is now waiting before trying a third time.**

Every one of those steps is a *success* from the platform's point of view. The image pulled.
The config resolved. The process launched. The platform did its entire job correctly, and
your process ended.

## The documented sequence

1. *"**Initial crash**: Kubernetes attempts an immediate restart based on the Pod
   `restartPolicy`."*
2. *"**Repeated crashes**: After the initial crash Kubernetes applies an exponential backoff
   delay for subsequent restarts."*
3. *"**CrashLoopBackOff state**: This indicates that the backoff delay mechanism is currently
   in effect for a container in a crash loop."*
4. *"**Backoff reset**: If a container runs successfully for a certain duration, Kubernetes
   resets the backoff delay."*

`[source: k8s-docs-container-restart-backoff-2026-08-31]`

**Point three is the one to internalize: the string names the waiting between crashes, not
the crash.** When you see it the container is neither running nor failing; it is sitting out
a delay.

## The curve, and two consequences

*"10s, 20s, 40s, …, capped at 300 seconds (5 minutes). Once a container executes successfully
for 10 minutes without problems, the kubelet resets the restart backoff timer."*
`[source: k8s-docs-container-restart-backoff-2026-08-31]`

- A long-crashing Pod appears to do nothing for up to five minutes at a stretch. **That is
  the cap, not a hang.**
- The reset requires **ten minutes** of success, so a container that dies every eight minutes
  never resets and escalates to the cap forever, while technically "working" most of the time.

## ⚠ It is not an image problem — it is the opposite signal

The pull succeeded, the config resolved, the process started. **You cannot loop something
that never ran once.** The trap survives because "BackOff" also appears in
`ImagePullBackOff`, and the two look like siblings. They are opposites: one retries a
**pull**, the other retries a **start**, having already pulled successfully.

⚑ **They also share a 300-second cap and are different mechanisms.** [[restart-policy]] has
been carrying that flag since Chapter 5; §4's ⚠ Hazards discharges it in substance, one
clause short of saying it outright.

## `restartPolicy` is what makes a loop possible

The default is `Always`, and with `Always` a container that exits — *even with code 0, even
successfully* — is restarted. `[source: k8s-docs-container-restart-backoff-2026-08-31]` A
container that runs a task and exits cleanly under the default policy loops forever. That is
not a bug; **it is a Deployment being used where a Job belonged.**

## Related

[[restart-policy]] · [[pod-failure-started-then-died]] · [[reading-container-logs]] ·
[[container-state]] · [[probe]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/oomkilled-vs-evicted.md ===
# Concept: `OOMKilled` versus `Evicted`

**Home:** Chapter 13 §4 · **Competency:** D2.3 · **Status:** canonical *(with one ⚑)*
**The chapter's most confusable pair.** Both mean "something ended your workload over memory."
Everything else about them differs.

## Three axes, and they disagree on all three

| | `OOMKilled` | `Evicted` |
|---|---|---|
| **Trigger** | this container exceeds **its own limit** | the **node** runs low on a resource |
| **Scope** | one container | the whole Pod |
| **Outcome** | restarted in place, same node, restart count up | Pod phase `Failed`; a controller creates a replacement **elsewhere** |

`OOMKilled` — *"The container ran out of memory."*
`[source: k8s-docs-pod-failure-signatures-2026-08-31]` Scoped tightly: *"Any Container
exceeding a resource limit will be killed and restarted by the kubelet without affecting
other Containers in that Pod."* `[source: k8s-docs-pod-qos-2026-08-24]`

`Evicted` — *"Node-pressure eviction is the process by which the kubelet proactively
terminates pods to reclaim resource on nodes,"* watching *"memory, disk space, and filesystem
inodes."* *"the kubelet sets the phase for the selected pods to `Failed`, and terminates the
Pod,"* after which *"the control plane (`kube-controller-manager`) creates new pods in place
of the evicted pods."* `[source: k8s-docs-node-pressure-eviction-2026-08-31]`

## ⚑ THE FOURTH AXIS — agency — IS CONTESTED. Read before editing either chapter.

The draft cut a "different killer" axis (kernel cgroup enforcement vs the kubelet) for want of
a source. **The source is already in this book's corpus, and it is in a shipped chapter.**

- `chapter-05:1025`, sourced: *"when it uses more than its memory limit, **the kernel** may
  terminate it, but terminations only happen when the kernel detects memory pressure, so a
  container that over-allocates **may not be killed immediately**"*
  `[source: k8s-docs-resource-management-2026-08-23]` — and [[resource-limit]] holds that
  quotation verbatim.
- Chapter 13 §4, sourced: *"killed and restarted by **the kubelet**"*
  `[source: k8s-docs-pod-qos-2026-08-24]`

Both are true at different altitudes; **the book asserts both and reconciles neither**, and
the kubelet version sits in two graded keys (Bearings #2 Q1, Practice Q6).

**One clause in §4 reconciles them without a fetch:** the kernel terminates on detected
pressure; the kubelet observes the termination, records the reason, and applies the restart
policy. Restoring the axis makes the discrimination four-deep again.

⚠ **Second, quieter consequence.** Ch 5's *"may not be killed immediately"* has no counterpart
in Chapter 13, and **Practice Q6 grades on the kill happening.** Q6's key is not wrong, but a
reader holding Ch 5's clause has a defensible reason to hesitate. The same clause fixes both.

⚠ **Figure debt.** `ch13-fig05`'s ASCII was rebuilt on three axes; its entry in
`image-specs.md` still describes a "Kernel cgroup enforcement" node and a four-axis caption.
**Regenerate that entry** — and if the fourth axis is restored, regenerate it again.

## The state-placement question

The cited reason table places `OOMKilled` among the **`Waiting`** reasons. §4 and Bearings #2
Q1's stem frame it as a **`Terminated`** reason with an exit code — which is what
practitioners see under Last State and what shipped `chapter-05:1025` establishes for the
memory-limit kill, sourced to `k8s-docs-pod-lifecycle-2026-08-23`. **The framing is canon and
needs no softening. The string's placement on `Terminated` is the book's own join** — soundly
made, nowhere cited. Amend the AUTHOR-REVIEW to say that; do not delete it.

## ⚠ The request/limit discrimination — the easiest error in the material

- The **limit** is what gets your container OOM-killed. Your requests are irrelevant to that
  event.
- The **request**, via its QoS class and via *"only Pods exceeding resource requests are
  candidates for eviction"* `[source: k8s-docs-pod-qos-2026-08-24]`, determines your standing
  when the **node** is under pressure. Your limits are largely irrelevant to that decision.

🪝 **"BestEffort asks for nothing, so it's the humblest and therefore the safest" is exactly
backwards.** Eviction order is `BestEffort` → `Burstable` → `Guaranteed`
`[source: k8s-docs-pod-qos-2026-08-24]`. Asking for nothing does not make you a good citizen;
it makes you first overboard.

## Two evictions, not one

*"Node-pressure eviction is not the same as API-initiated eviction."* The kubelet under
pressure *"does not respect your configured PodDisruptionBudget or the pod's
`terminationGracePeriodSeconds`."* `[source: k8s-docs-node-pressure-eviction-2026-08-31]`
**A node in trouble stops negotiating.** The node controller's eviction of a dead node's Pods
is the *other* kind — see [[node-controller]].

⚑ **PodDisruptionBudget remains unowned book-wide** (ledger ⚑3; shipped Ch 8 has zero
occurrences). Chapter 13's only use is inside the verbatim quotation above, which is the
minimum needed for accuracy and does not teach the term. **Correct handling — preserve it.**

## Related

[[resource-limit]] · [[resource-request]] · [[pod-failure-started-then-died]] ·
[[node-conditions]] · [[crashloopbackoff]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/crictl.md ===
# Concept: `crictl`, and the diagnostic layer stack

**Home:** Chapter 13 §5 · **Competency:** D2.3 · **Status:** canonical *(with one ⚑)*
**Pinned by:** `chapter-03:451` — Chapter 3 promised this framing

## The question it answers

Every other command in Chapter 13 goes through the API server. That is by design: the API
server is the only door in, and everything you read is the cluster's own recorded view of
itself.

**So what do you do when the failure is *in* that path?** If the kubelet cannot register a
container with the API server, then from `kubectl`'s point of view the container does not
exist. You will look at an empty result and conclude nothing is running, while a container
may be running perfectly well on the node in front of you.

```
   kubectl  ──┐
 kube-apiserver│  the cluster's RECORDED view
   kubelet   ──┘
  ═══════════   ◄── the API boundary
     CRI
containerd / CRI-O   ◄── crictl attaches HERE
```

## What it is

*"a command-line interface for CRI-compatible container runtimes. You can use it to inspect
and debug container runtimes and applications on a Kubernetes node."* Stable since Kubernetes
v1.11; *"requires a Linux operating system with a CRI runtime."*
`[source: k8s-docs-crictl-2026-08-31]` It runs **on the node**, not from your laptop.

Connects through an endpoint set by `--runtime-endpoint`, the `CONTAINER_RUNTIME_ENDPOINT`
variable, or `/etc/crictl.yaml`; unconfigured, it *"attempts to connect to a list of known
endpoints, which might result in an impact to performance."*
`[source: k8s-docs-crictl-2026-08-31]`

## ★ The argument, which is the whole point

> **When the cluster's view and the node's view disagree, `crictl` is how you see the node's
> view.**

A container `kubectl` cannot account for but `crictl` lists is a container **the kubelet
failed to register** — which localizes the problem to the kubelet, not the workload. A
container neither can see was never started, which is a different problem entirely.

**It is not a better `kubectl`.** It answers a different question.

## ⚠ Comparing counts is not comparing views

`crictl ps` lists **containers**; `kubectl get pods` lists **Pods**. Two Pods with two
containers each is four containers and nothing is wrong. **Practice Q13 is built on exactly
that error.** The genuine signal requires matching Pod and container identities across
`--all-namespaces`, not counting rows.

And static Pods are *"managed directly by the kubelet and represented by mirror Pods"* in the
API `[source: k8s-docs-pod-failure-signatures-2026-08-31]` — so they are **not** a source of
containers hidden from `kubectl`.

## ⚑ Two command forms are untagged

`k8s-docs-crictl-2026-08-31` declares `crictl-ps` and `crictl-logs` in its frontmatter
`concepts_covered`, but the transcription stops at the `/etc/crictl.yaml` section and
**neither appears in the body** — verified; the file is 37 lines. Every other claim in §5 is
verbatim-clean. **Re-transcribe the "General usage" examples.**

## Where the trail goes next, and where it stops

If the kubelet itself is the suspect, the next honest move is its own service logs on that
machine (`journalctl -u kubelet` on a systemd host). That is Linux administration, not
Kubernetes, and it is past what KCNA asks. **Named because pretending the trail ends at
`crictl` would be dishonest, and because knowing where the trail goes is part of knowing where
your own scope ends.**

## ⚑ Outline debt

`kb_tags.commands` lists `crictl-pods` and `crictl-inspect`. Neither appears in the draft —
correctly, since the outline's own §5 depth ruling authorizes `crictl ps` and `crictl logs`
only. **Remove both entries** so the concept index does not claim coverage the chapter
deliberately declined.

## Related

[[cri]] · [[container-runtime]] · [[node-components]] · [[reading-container-logs]] ·
[[node-conditions]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/version-skew-symptoms.md ===
# Concept: Version skew as a symptom shape

**Home:** Chapter 13 §6 · **Competency:** D2.3 · **Status:** canonical
**The rule lives in [[version-skew]] (Ch 8 §6). This shard states no skew numbers.**

Chapter 8 taught the window and said it would come back *"in a form where you have to use it
rather than recite it."* This is that form: what skew **looks like** when you meet it as a
symptom, and how you would rule it out. **Skew is a diagnosis of last resort, and it is on
the list precisely because nobody thinks of it.**

## The skewed client

**Symptom:** `kubectl` reports that a resource type does not exist, or a field you are certain
is valid is rejected, or output is missing columns another engineer sees.

**Why skew explains it:** *"`kubectl` is supported within one minor version (older or newer)
of `kube-apiserver`."* `[source: k8s-version-skew-policy-2026-08-31]` A client too far behind
does not know about API groups the cluster has since added; one too far ahead sends fields the
server does not understand. **Neither produces an error saying "your client is old." It
produces an error about your *resource*, which sends you to your YAML.**

**Rule it out:** `kubectl version`. More than one minor apart → stop investigating your
manifest. You are debugging your instrument, not the water.

🪝 One engineer, two clusters at different versions, one `kubectl` binary: inside the window
for one and outside it for the other, and the same command gives different results depending
on the active context. **When a manifest applies cleanly to one cluster and is rejected by
another, check `kubectl version` against both before changing a line of YAML.**

## The skewed kubelet

**Symptom:** one node behaves differently. A feature works everywhere except there. Pods with
identical specs fail there and nowhere else.

**Why skew explains it:** an old kubelet is **supported**, not an error state — but it does
not implement API fields added after its release. **It will accept a Pod spec containing a
field it has never heard of and simply not act on it. No error. No event.**

> **That silence is the whole danger.** A misconfiguration produces a message; an unimplemented
> field produces nothing, which reads as "it worked."

**Rule it out:** `kubectl get nodes -o wide` prints each node's kubelet version. The project
asks for this routinely — *"Kubernetes version: `kubectl version`"* and *"container runtime
version"* `[source: k8s-docs-troubleshooting-overview-2026-08-31]` — which tells you how often
it is the answer.

**Forward risk:** *"Running a cluster with `kubelet` instances that are persistently three
minor versions behind `kube-apiserver` means they must be upgraded before the control plane
can be upgraded."* `[source: k8s-version-skew-policy-2026-08-31]` A node at the far edge is
not a curiosity; it is blocking the next control-plane upgrade.

## ⚓ Known issues are a triage step, not a defeat

*"You should also check the known issues for the release you're using."*
`[source: k8s-docs-troubleshooting-overview-2026-08-31]` The project *"maintains release
branches for the most recent three minor releases,"* each with *"approximately 1 year of patch
support"* `[source: k8s-version-skew-policy-2026-08-31]`. **Hours of careful, correct
investigation can arrive at a conclusion someone already wrote down.**

## Two things deliberately not said here

- **No release cadence.** An earlier draft asserted ~3 minor releases a year; that is in no
  snapshot. Ch 17 §8 owns the cadence — a pointer is probably the better answer than a fact.
- **No LTS hazard.** The ledger puts *"Kubernetes has no LTS release"* at **Ch 8 §6**, and
  shipped Ch 8 does not say it. Verified: the skew snapshot contains no use of "LTS" at all.
  Until that retrofit lands, **no question anywhere may hinge on it**, and §6 correctly does
  not raise it.

## Related

[[version-skew]] · [[release-cadence]] · [[kubeadm]] · [[node-conditions]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-metrics-pipeline.md ===
# Concept: The resource metrics pipeline

**Home:** Chapter 13 §7 · **Competency:** D2.3 · **Status:** canonical
**Closes B1 trap #72** · **Pinned by** `chapter-10:677`

## The failure that starts it

`kubectl top pod myapp` returns an error — and the *same* error for every Pod, every node,
every namespace. Nothing is broken. **A stock Kubernetes cluster publishes no usage metrics
at all**, not because nobody is measuring but because nobody installed the component that
gathers the measurements into an API you can query.

## The stack, bottom up

| Layer | What it is | Installed by default? |
|---|---|---|
| **cAdvisor** | *"Daemon for collecting, aggregating and exposing container metrics **included in Kubelet**"* | **Yes** — part of the kubelet binary, every node |
| **kubelet** | *"Resource metrics are accessible using the `/metrics/resource` and `/stats` kubelet API endpoints"* | **Yes** |
| **metrics-server** | *"Cluster addon component that collects and aggregates resource metrics pulled from each kubelet"* | **NO** — *"not deployed by default in all distributions"* |
| **Metrics API** | *"you need an API extension server that provides the Metrics API"* | Only once metrics-server is running |
| **Consumers** | HPA, VPA, `kubectl top` | — |

`[source: k8s-docs-resource-metrics-pipeline-2026-08-31; k8s-docs-resource-metrics-pipeline-2026-08-23]`

## ★ Everything except one box is already running on your cluster

The measurements exist. **Nothing is publishing them.** Note the *shape* of the error: not
"no data" but "no such resource," because the API itself is not being served. A metrics-server
that were installed but had not finished a scrape would return empty *data* — a different
error, and the difference is the diagnosis (**Bearings #3 Q1**).

⚠ **Nothing needs *enabling*.** The kubelet endpoints are already serving. That is the
misreading **Practice Q15 distractor D** exists to catch.

## It is [[absent-component-pattern]], with one twist

The pattern Chapter 10 named applies here with a variation worth stating: **it is not even the
object that is missing, it is the API itself.** The Metrics API is not part of the core API
server; it is served by an extension, and if nobody deployed it the API server has no such
endpoint to route your request to.

**Second consequence people meet separately and never connect:** an HPA reads the same Metrics
API. Created without metrics-server, it is accepted like any other object, has no metric
source, and never scales anything — the same pattern, one layer up.

⚠ What an HPA object visibly *reports* in that state is in no snapshot; the prose and TYB 3
Q3's key state only the sourced consequence.

## Scope, from the source

metrics-server *"is meant only for autoscaling purposes — for example, don't use it to forward
metrics to monitoring solutions, or as a source of monitoring solution metrics."*
`[source: k8s-docs-resource-metrics-pipeline-2026-08-23]` Current values only. **No history.**
You cannot ask it what happened an hour ago. → Ch 18 §3.

⚠ **Do not name which distributions install it.** The corpus goes exactly as far as *"not
deployed by default in all distributions."* A per-distribution breakdown was cut for that
reason; restoring it needs the metrics-server project README.

## Related

[[absent-component-pattern]] · [[cluster-level-logging]] · [[optional-components]] ·
[[node-components]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cluster-level-logging.md ===
# Concept: Cluster-level logging, and why `kubectl logs` is not an archive

**Home:** Chapter 13 §7 · **Competency:** D2.3 · **Status:** canonical
**Agents and architecture:** Ch 18 §6 (ledger-assigned; §7 gives one clause and a pointer)

## What actually happens when you run `kubectl logs`

The request goes to the API server, which routes it to the kubelet on the node, and *"the
kubelet on that node handles the request and reads directly from the log file; the kubelet
returns the content of the log file; **only the latest log file's contents are available**."*
`[source: k8s-docs-logging-architecture-2026-08-23]`

**There is no log database.** There is a file on a node's disk, and a kubelet willing to read
it to you.

## The file is rotated, capped, and destroyed with the Pod

The kubelet *"is responsible for rotating container logs and managing the logging directory
structure, configured via `containerLogMaxSize` (default 10Mi) and `containerLogMaxFiles`
(default 5)."* And: *"if a container restarts, the kubelet keeps one terminated container with
its logs. **If a pod is evicted from the node, all corresponding containers are also evicted,
along with their logs.**"* `[source: k8s-docs-logging-architecture-2026-08-23]`

## ★ An evicted Pod takes its logs with it

Read that against [[oomkilled-vs-evicted]]. **The failure you most want to investigate is the
one whose evidence is most likely gone.** The reader most likely to be caught is the one
investigating the most interesting failure: an eviction, a node that died, a Pod deleted and
recreated by a controller. In every case the evidence is gone *by definition*, and the absence
of logs means nothing about what the application did.

**This is the same lesson as the event retention window, arriving from a second direction.
Two of the platform's diagnostic surfaces are ephemeral by design, and neither one's silence
is evidence.**

## The gap the project states plainly

*"In a cluster, logs should have a separate storage and lifecycle independent of nodes, pods,
or containers. This concept is called cluster-level logging."* And: *"Cluster-level logging
architectures require a separate backend to store, analyze, and query logs. **Kubernetes does
not provide a native storage solution for log data.** Instead, there are many logging
solutions that integrate with Kubernetes."*
`[source: k8s-docs-logging-architecture-2026-08-31]`

The most common answer is *"a node-level logging agent that runs on every node (typically a
DaemonSet) and pushes logs to a backend."*
`[source: k8s-docs-logging-architecture-2026-08-23]` **That is the whole gloss §7 gives, and
it is correct** — the ledger routes the agents and their architecture to Ch 18 §6.

## Related

[[reading-container-logs]] · [[kubernetes-events]] · [[oomkilled-vs-evicted]] ·
[[resource-metrics-pipeline]] · [[daemonset]]
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/read-the-phase-first.md ===
# Concept: Read the phase first — the chapter's synthesis

**Home:** Chapter 13 §8 (☀️ Zenith) · **Competency:** D2.3 · **Status:** canonical
**Inherited by:** Ch 16 §1 · **Retrieved at:** Ch 19

## The move

Nine signatures — `Pending`, `ErrImagePull`, `ImagePullBackOff`, `ImageInspectError`,
`ErrImageNeverPull`, `CreateContainerConfigError`, `CrashLoopBackOff`, `OOMKilled`, `Evicted`
— are not nine facts on a flat list. They are **nine positions on one axis.**

> **The phase names a stage, the stage names a component, and the component names a source.**

Three steps from symptom to the right place to look, and none of them requires having seen
this particular failure before.

| Stage | Owner | Where it writes |
|---|---|---|
| admitted | the admission gate | a response to whoever called it |
| scheduled | the scheduler | events |
| pulled · configured · started | the kubelet | container states, `Reason`s, events |
| node answering at all | the node controller | node conditions |

## Why it survives the unfamiliar

Kubernetes will ship a signature next year that no study guide covers. You will not recognize
it and you will not need to: read the phase, identify the stage, ask the component.
**Instruments change; the way you fix a position does not.**

This is the argument for teaching a method rather than a glossary, and it is the chapter's
whole justification for existing in a book that could have printed a two-column table.

## The turn — §1's question and §8's answer are the same question

*What do you read first* and *whose problem is this* have one answer. A Pod that never started
is not your application's failure — your application has not run. A Pod killed by the node is
not your application's failure either. **Only when the Pod is `Running` and `Ready`, the
trouble is confined to one workload, and the behavior is still wrong has the platform finished
and handed the problem to you.**

Which is why the order is not arbitrary: **the first thing you read is the thing that tells
you whether to keep reading at all.**

## The pattern underneath

A Pod sitting in `Pending` is not a broken thing. It is a control loop that has not
converged — a declaration of intent that no node has yet been able to satisfy, being patiently
re-evaluated by a component that will act the instant it can. *"Diagnosis, in this system, is
mostly reading a loop's report and believing it."* → [[control-loop]]

## ⚑ Figure-anchor note — do not "fix" this

The Zenith anchor is `ch13-zenith-read-the-phase-first`, which conforms to
`structural-contract.yaml`'s `anchor_id_pattern` (the contract explicitly permits `zenith` in
place of `figNN`) and passes the linter. The image-specs stage proposed
`ch13-fig07-zenith-...` against a stricter house rule. **Renaming would break the join key with
`image-specs.md` and with the diagram pipeline's `figures-metadata.yaml`.** If the stricter
rule is the real one, change the contract and sweep all books. Separately: `ch13-fig04` is the
**sixth** figure in reading order — figure number does not imply position in this chapter.

## Related

[[triage-order]] · [[platform-scope-vs-application-scope]] · [[pod-phase]] ·
[[control-loop]] · [[absent-component-pattern]]
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/container-state.md ===

---

## Chapter 13 §2 — ⚑ THE OPEN VOCABULARY GAP IS CLOSED

This shard recorded: *"⚑ Vocabulary gap: `CrashLoopBackOff`. The counterpart `Reason` … appears
in **no cached snapshot.** … **Open a research fetch** for container status reasons."*

**Chapter 13's corpus closes it.** `k8s-docs-container-restart-backoff-2026-08-31` states the
definition directly — *"This indicates that the backoff delay mechanism is currently in effect
for a container in a crash loop"* — and `k8s-docs-pod-failure-signatures-2026-08-31` supplies
the full documented `Waiting` reason table. **Chapter 5 §5's placeholder can now be filled from
material the book already holds.** See [[crashloopbackoff]].

## The `Waiting` reasons, now sourced

`ContainerCreating` · `ErrImagePull` · `ImagePullBackOff` · `ImageInspectError` ·
`ErrImageNeverPull` · `PodInitializing`
`[source: k8s-docs-pod-failure-signatures-2026-08-31]`

⚠ **`CreateContainerConfigError` is NOT in that table** and appears in zero of the corpus's
198 snapshots. Chapter 13 §2 presents it outside the table for exactly that reason. **Do not
fold it in.** See [[createcontainerconfigerror]].

## The `Terminated` question this shard's reservation raises

This shard rightly ruled that *"the status string `OOMKilled` is not defined here and must not
be."* Chapter 13 §4 now defines it — and frames it as a **`Terminated`** reason with an exit
code, while the cited table lists it among **`Waiting`** reasons.

The framing matches shipped `chapter-05:1025` (*"The container reaches the `Terminated` state,
with a reason and an exit code recorded"* `[source: k8s-docs-pod-lifecycle-2026-08-23]`) and is
what practitioners see under Last State. **The framing is canon; the string's placement on
`Terminated` is the book's own join** — soundly made, nowhere cited. Recorded so no later stage
mistakes it for a citation.

## The three-field reading survives contact with Chapter 13

This shard's *"three fields, three levels of specificity, and only the third one is
actionable"* is exactly the move Chapter 13 §2 makes when it says the string that tells you
what is wrong *"lives on the container state, not the phase."* **The handoff worked.** Ch 13
applies the taxonomy without restating it, honouring ledger ⚑2.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/restart-policy.md ===

---

## Chapter 13 §4 — the "other five minutes" is substantially discharged

This shard flagged: *"`ImagePullBackOff` retries 'up to a compiled-in limit of 300 seconds
(five minutes)' — a **separate** backoff governing pulls, not restarts … The chapter never
distinguishes them and a reader will reasonably conclude they are one cap. **One clause fixes
it.**"*

Chapter 13 §4 writes the clause, in a different chapter:

> *"`ImagePullBackOff` means the kubelet is retrying a **pull**. `CrashLoopBackOff` means the
> kubelet is retrying a **start**, having already pulled successfully."*

**Discharged in substance, one clause short of explicit.** §4 distinguishes the two
*mechanisms* clearly and gives both caps as 300 seconds without ever saying outright that
these are two separate backoffs that happen to share a number. If a fix is wanted, that
sentence is it — and it belongs in §4, not retrofitted into Ch 5 §5.

## The curve, confirmed by a second snapshot

`k8s-docs-container-restart-backoff-2026-08-31` independently states the same schedule this
shard recorded from `k8s-docs-pod-lifecycle-2026-08-23`: 10s, 20s, 40s, capped at 300s; reset
after 10 minutes of success. **Two sources agree.** Chapter 13 adds the two consequences the
numbers imply: the cap is not a hang, and a container dying every eight minutes never resets.

## `Always` restarts a *successful* exit

Chapter 13 states what this shard's scope discussion implies but does not say: with the default
`Always`, a container that exits **even with code 0** is restarted, so a task container
deployed under a Deployment loops forever. *"That is not a bug; it is a Deployment being used
where a Job belonged."* `[source: k8s-docs-container-restart-backoff-2026-08-31]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-limit.md ===

---

## Chapter 13 §4 — ⚑ AGENCY CONTRADICTION. READ BEFORE EDITING EITHER CHAPTER.

This shard holds, verbatim and sourced: *"Memory limits are enforced by **the kernel** with out
of memory (OOM) kills. When a container uses more than its memory limit, **the kernel may
terminate it.** However, **terminations only happen when the kernel detects memory
pressure.**"* `[source: k8s-docs-resource-management-2026-08-23]`

Chapter 13 §4 says, also sourced: *"Any Container exceeding a resource limit will be killed and
restarted by **the kubelet** without affecting other Containers in that Pod."*
`[source: k8s-docs-pod-qos-2026-08-24]`

**Both are true at different altitudes. The book asserts both and reconciles neither**, and the
kubelet version sits in two graded keys (Ch 13 Bearings #2 Q1, Practice Q6).

**Good news for the draft:** Chapter 13's AUTHOR-REVIEW cut its kernel/cgroup discrimination
axis for want of a source. **The source is this shard**, already in the book's corpus. One
clause in §4 — the kernel terminates on detected pressure; the kubelet observes it, records the
reason, and applies the restart policy — reconciles the two and lets the cut axis be restored
without a fetch.

⚠ **Second consequence.** This shard's *"a container that over-allocates may not be killed
immediately"* has **no counterpart anywhere in Chapter 13**, and Practice Q6 grades on the kill
happening. Q6's key is not wrong, but a reader holding this clause has a defensible reason to
hesitate. The same one-clause fix covers it.

## The string is released

This shard reserved `OOMKilled` for Chapter 13. **Chapter 13 §4 now owns it** — see
[[oomkilled-vs-evicted]] for the three-axis discrimination and the `Terminated`-state question.

## The limit answers one question only

Chapter 13 sharpens the request/limit split into an exam discrimination worth carrying here:
**the limit is what gets your container OOM-killed** — requests are irrelevant to that event.
Standing under *node* pressure is the request's job. See [[resource-request]].

⚠ **Memory is not throttled.** Chapter 13 Practice Q6 distractor D ("throttled to 256Mi and
continues running") is keyed wrong, and this shard's CPU/memory asymmetry is why.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-request.md ===

---

## Chapter 13 §4 — what a request buys you when the kubelet is choosing

Eviction order is by QoS class: *"When a Node runs out of resources, Kubernetes will first
evict `BestEffort` Pods running on that Node, followed by `Burstable` and finally `Guaranteed`
Pods."* With the refinement that matters most: *"When this eviction is due to resource
pressure, **only Pods exceeding resource requests are candidates for eviction.**"*
`[source: k8s-docs-pod-qos-2026-08-24]`

**A Pod living within its requests is not a candidate at all. That is what a request buys you:
standing, when the kubelet is choosing.**

🪝 "BestEffort asks for nothing, so it is the humblest and therefore the safest" is exactly
backwards. **BestEffort is evicted first.** Specifying no requests does not make you a good
citizen; it makes you the first thing thrown overboard, because the kubelet has no reason to
believe you need anything.

## The two-question split, stated as an exam discrimination

- **Limit** → the threshold that gets *this container* OOM-killed. Requests irrelevant.
- **Request** → your standing when *the node* is under pressure and something has to go.
  Limits largely irrelevant.

A question that hands you a Pod spec and asks "what protects this from eviction" is testing
whether you reach for the limit when you should reach for the request.

## Related

[[oomkilled-vs-evicted]] · [[resource-limit]]
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/probe.md ===

---

## Chapter 13 §4 — the two failure shapes, and the silent one

Chapter 5 §7 taught what probes are. This is what their failures look like from outside, and
the two shapes could hardly be more different.

**Liveness fails → a restart loop.** The kubelet kills the container and applies the restart
policy `[source: k8s-docs-pod-lifecycle-2026-08-23]`. From outside this is **indistinguishable
from an application crashing on its own**: restart count climbing, eventually
`CrashLoopBackOff`. The distinguishing evidence is in the events, where the kubelet records the
probe failure, and in the logs, where a self-crashing application usually leaves a stack trace
and a probe-killed one usually does not.

**The fixes are opposite**, which is why the distinction is worth the effort. Crashing
application → fix the application. Wrong probe (too short a timeout, too aggressive an
`initialDelaySeconds`, a health endpoint slow under load) → **the application is fine and the
probe is manufacturing an outage.**

**Readiness fails → something much quieter.** The Pod stays `Running`. It does not restart. It
reports `0/1 Ready`. And *"the endpoints controller removes the Pod's IP address from the
endpoints of all Services that match the Pod."*
`[source: k8s-docs-pod-lifecycle-2026-08-23]`

> ★ **The Pod is alive, consuming its node's resources, showing `Running`, and receiving no
> traffic at all.** Anyone who reads only the `STATUS` column concludes it is healthy. **The
> `READY` column is the tell** — `1/1` and `0/1` both print `Running` beside them.

This is the chapter's quietest failure: `Running`, `0/1 Ready`, zero restarts, no events after
the first few, and no traffic. It leaves **no restart count and no crash to find**, which means
every other diagnostic in the chapter reads clean.

⚠ The `READY` column's semantics are **untagged** — B1 gap G1 — and two graded items rely on
them (Ch 13 Bearings #2 Q3, Practice Q10).

## Related

[[pod-failure-started-then-died]] · [[endpointslice]] · [[crashloopbackoff]] · [[service]]
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pod-phase.md ===

---

## Chapter 13 — the phase as a lookup key

Chapter 5 §5 taught the phase as a taxonomy. Chapter 13 uses it as **the single key every
diagnosis is looked up on**, and that reframing is the chapter's whole contribution:

> **A Pod's phase tells you which stage of the platform's own start-up sequence stopped. Each
> stage is owned by a different component. Knowing the stage tells you which component to
> interrogate, and interrogating the right component is the whole of diagnosis.**

**The phase is not an error message. It is a position in a sequence.** `kubectl logs`
interrogates the application, which is the last component in that sequence and therefore the
last one worth asking.

## Why it goes first, in one table

| Failure | What a log read returns |
|---|---|
| `Pending` | nothing — no container exists |
| `CrashLoopBackOff` | nothing — the current container has not started |
| `Evicted` | nothing — the Pod is off the node |

Three causes, one output. **The logs cannot distinguish them; the phase does, instantly.**

## The prerequisite this creates

Chapter 13's outline names Ch 5 §5 as the one section a low-scoring reader must re-read
**before** starting, not alongside — *"every section here is a lookup keyed on the phase, and if
that taxonomy has faded, the material degrades into a list of strings to memorize, which is
precisely the failure this chapter exists to prevent."* Chapter 13's Soundings 0–2 branch says
exactly that. **This shard is a load-bearing prerequisite for Chapter 13 and for Ch 16.**

## Related

[[read-the-phase-first]] · [[triage-order]] · [[container-state]] · [[pending-pod]]
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/pending-pod.md ===

---

## Chapter 13 §2 — Chapter 7's promise, paid in full

`chapter-07:426` framed Chapter 13's opening move: nothing retries a `Pending` Pod with relaxed
constraints. Chapter 13 §2 cashes it:

> *"A Pod in `Pending` is not drifting and it is not broken. It is riding at anchor, waiting for
> a berth that has not opened, and nothing in the cluster is quietly slackening the lines to
> make it fit."*

The documentation's own framing: *"If a Pod is stuck in Pending it means that it can not be
scheduled onto a node. Generally this is because there are insufficient resources of one type
or another."* And the instruction that matters: *"Look at the output of the kubectl describe
command; there should be messages from the scheduler about why it can not schedule your pod."*
`[source: k8s-docs-debug-pods-2026-08-23]`

**Note what that assumes. The scheduler *tells you*.** You do not have to deduce anything. You
have to go and read it.

## ⚠ A capacity shortage and a taint look identical from outside

Both produce a Pod in `Pending`, indefinitely, with no containers. `kubectl get pods` shows the
same line for both. **They have opposite fixes** — reduce requests / delete Pods / add nodes,
versus add a toleration or accept that the refusal is correct.

**The only thing that distinguishes them is the scheduler's own event text.** This is why "read
the events" is not a formality: it is the single step that separates two problems with opposite
fixes.

⚠ **No scheduler event string is quoted anywhere in Chapter 13.** No snapshot in the corpus
contains any — `k8s-docs-debug-pods-2026-08-23` establishes that the scheduler writes such
messages and never quotes one. Practice Q2's stem and key were paraphrased rather than shipped
as literal product output; **the graded discrimination survives the paraphrase.** Restoring
literal strings needs a fetch on scheduler event message formats.

## Two `Pending` causes worth naming

- Cluster-wide exhaustion: *"you may have exhausted the supply of CPU or Memory in your cluster,
  in this case you need to delete Pods, adjust resource requests, or add new nodes."*
- `hostPort`: *"when you bind a Pod to a hostPort there are a limited number of places that pod
  can be scheduled; in most cases hostPort is unnecessary."*
  `[source: k8s-docs-debug-pods-2026-08-23]` It silently reduces your feasible-node count to
  "nodes where that port is free," which on a small cluster can be one, or zero.

## ⚑ Chapter 11 promised a discrimination Chapter 13 does not deliver

`chapter-11:588`: *"A claim that never binds is, from the Pod's point of view, indistinguishable
from a scheduling failure… **Chapter 13 will teach you to tell those two apart from the
symptoms.**"*

Chapter 13 §2 gives one sentence of family membership and its own AUTHOR-REVIEW concedes the
mechanism is unstated. The reader arrives expecting a discrimination and does not get one.

**Needs either the storage fetch or a softening edit at `chapter-11:588`.** Note the draft's own
caveat, which makes the fetch genuinely necessary rather than optional: a `WaitForFirstConsumer`
PVC binds *because of* scheduling rather than before it, which **inverts** any flat claim that a
Pod cannot be scheduled until its claim binds.

## Related

[[feasible-node]] · [[taint]] · [[toleration]] · [[persistentvolume-and-claim]] ·
[[pod-failure-never-started]]
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/imagepullbackoff.md ===

---

## Chapter 13 §2 — the deferred diagnosis has arrived

This shard's scope table deferred *"Diagnosis — reading events, checking the name, confirming
the push"* to **Ch 13 §2**. **Delivered exactly**, from the documentation's own checklist:
*"make sure that you have the name of the image correct; have you pushed the image to the
registry?; try to manually pull the image to see if the image can be pulled."*
`[source: k8s-docs-debug-pods-2026-08-23]` **Obligation discharged cleanly.**

## The one thing Chapter 2 could not say

*"`ImagePullBackOff` is not a different diagnosis from `ErrImagePull`. It is the same diagnosis,
observed a little later."* Chapter 2 owned the string and the retry behaviour; it had no
sibling string to contrast with. Chapter 13 supplies the family — `ErrImagePull`,
`ImageInspectError`, `ErrImageNeverPull` — and the relation between them. See
[[image-pull-failure-family]].

## Agreement confirmed

This shard's *"Reported as a container in the **Waiting** state"* and Chapter 13's `Waiting`
reason table agree exactly. **No drift.** Ch 5 Soundings Q8's attribution to Chapter 2 by name
is unaffected and should stay.

## ⚑ A Chapter 2 AUTHOR-REVIEW is now answerable

`chapter-02:604` holds an open comment asking for exactly the `crictl` fetch this chapter now
holds (`k8s-docs-crictl-2026-08-31`). **Chapter 2's softened "beneath Kubernetes" framing can be
restored from Chapter 13's snapshot.**
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/imagepullpolicy.md ===

---

## Chapter 13 §2 — the availability cost of `Always`

Chapter 2 taught the policy and its defaults. Chapter 13 supplies the operational consequence
nobody expects:

*"if the kubelet has a container image with that exact digest cached locally, it uses its cached
image"* `[source: k8s-docs-images-2026-08-23]` — so `Always` does **not** mean "download the
layers every time." **The bandwidth cost is small. The availability cost is not:** the kubelet
still has to hail the registry to resolve the tag before it will use the cache.

> **A Pod running happily for weeks on a cached image will fail to restart the moment the
> registry becomes unreachable.** A Pod pinned to a specific tag other than `:latest` gets
> `IfNotPresent` by default and rides out the same registry outage without noticing.

That is a real production consequence of a default nobody chose deliberately, and it is the
kind of thing a tag-versus-digest question can be built on.

## `ErrImageNeverPull` — the mirror-image mistake

`imagePullPolicy: Never` with no local image produces its own reason string:
*"The image pull policy is set to `Never`, but the image is not present locally."*
`[source: k8s-docs-pod-failure-signatures-2026-08-31]` Usually a `minikube`/`kind`
locally-built-image pattern that has moved to a node without the image. **Kubernetes does
exactly what it was told**; the fix is "put the image on that node" or "stop saying `Never`."

## Related

[[image-pull-failure-family]] · [[tag-vs-digest]] · [[registry]]
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-conditions.md ===

---

## Chapter 13 §5 — conditions as instructions

Ledger ⚑1 rules that **ownership stays at Ch 8 §4** and that Ch 13 §5 *"retrieves them as a
diagnostic and must not restate the table."* The genuinely new material is the **next move**:

| Condition | Your next move |
|---|---|
| `Ready=True` | The node is not your problem. Return to the workload. |
| `Ready=False` | Somebody is reporting a problem. Go to the node and read the kubelet's own logs. |
| `Ready=Unknown` | Nobody is reporting at all. Suspect the kubelet process, the machine, or the network to the control plane. |
| `MemoryPressure=True` | Expect evictions. Your Pod's failure is probably not its own fault. |
| `DiskPressure=True` | Expect image garbage collection and evictions; also a plausible cause of pull failures. |
| `PIDPressure=True` | Container starts will fail confusingly. Look for a process-leaking workload. |

⚓ **When several unrelated Pods on one node fail in *different* ways at the same time, stop
diagnosing the Pods and describe the node.** Correlated, heterogeneous failures on one node are
almost never a coincidence of workloads.

## ⚑ Ledger ⚑1 is partially breached, and the fix is one column

§5 announces compliance (*"This section does not restate that table"*) and then carries a
middle column that reproduces this shard's definitions from the same snapshots — including the
`False`-versus-`Unknown` distinction, which Ch 8 §4 teaches at line 809, warns about at 1128,
and repeats in its summary at 1349.

**No contradiction — the two agree**, and this shard's framing (*"`Unknown` is not a fourth
failure mode. It is the control plane declining to guess"*) is the better of the two, so the
duplication also loses ground. **Compress or drop §5's middle column and keep "Your next
move."** Two rows would then read as instructions rather than definitions, which is what the
flag asked for.

## No conflict on the grace period

§5 quotes *"the node controller has not heard from the node in the last
`node-monitor-grace-period`"* `[source: k8s-docs-node-status-2026-08-24]` **without a number**,
consistent with this shard's ruling that the parameter name is the durable fact and the 50-second
default is an illustration.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-controller.md ===

---

## Chapter 13 §5 — the node-death timeline

This shard recorded the controller's three jobs. Chapter 13 supplies the **timing**, which is
what a diagnostician actually needs:

*"If a node remains unreachable: triggering API-initiated eviction for all of the Pods on the
unreachable node. **By default, the node controller waits 5 minutes between marking the node as
`Unknown` and submitting the first eviction request.**"*
`[source: k8s-docs-node-controller-heartbeats-2026-08-31]`

**Five minutes of apparent inaction, on purpose.** A node that vanishes for ninety seconds
because of a network blip should not have its entire workload torn down and rescheduled.

## The mechanism is Chapter 7's, doing a job you would not have guessed

Not a dedicated timer — taints. *"The node controller also adds taints corresponding to node
problems like node unreachable or not ready. This means that the scheduler won't place Pods onto
unhealthy nodes."* `[source: k8s-docs-node-controller-heartbeats-2026-08-31]` And Pods carry a
default toleration: *"Kubernetes automatically adds a toleration for
`node.kubernetes.io/not-ready` and `node.kubernetes.io/unreachable` with `tolerationSeconds=300`,
unless you, or a controller, set those tolerations explicitly."*
`[source: k8s-docs-taints-tolerations-depth-2026-08-24]`

**So the five-minute wait is not a special case bolted on for node failure.** It is
[[built-in-node-condition-taints]], doing a job the reader met three chapters earlier.

## ★ Engineering humility, worth teaching as such

Above a threshold of unhealthy nodes the eviction rate is reduced, and on small clusters
evictions stop entirely. In the worst case: *"when all zones are completely unhealthy (none of
the nodes in the cluster are healthy)… the node controller assumes that there is some problem
with connectivity between the control plane and the nodes, and doesn't perform any evictions."*
`[source: k8s-docs-node-controller-heartbeats-2026-08-31]`

> **A compass that reads north in every direction is telling you about the compass.** When every
> node looks dead, the most likely explanation is that the observer is wrong. So the controller
> stops acting.

## The Pod-level consequence

*"If a Node dies, the Pods running on (or scheduled to run on) that node are marked for
deletion."* And they do not come back as themselves: *"A given Pod (as defined by a UID) is never
'rescheduled' to a different node; instead, that Pod can be replaced by a new, near-identical
Pod."* `[source: k8s-docs-pod-failure-signatures-2026-08-31]`

**No ordinal is recorded here**, per this shard's standing ruling.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-heartbeats.md ===

---

## Chapter 13 §5 — what an absent heartbeat leads to

This shard established what an absent heartbeat **licenses**: a communication failure, not a
broken node — which is why `Unknown` exists as a distinct value.

Chapter 13 adds what it **causes**, and answers the question readers ask about `Unknown`: *who
wrote it, if the node is not talking?* The node controller did, on the node's behalf, because
the node stopped. *"In the case that a node becomes unreachable, updating the `Ready` condition
in the Node's `.status` field. In this case the node controller sets the `Ready` condition to
`Unknown`."* `[source: k8s-docs-node-controller-heartbeats-2026-08-31]`

**Then it waits five minutes before the first eviction request.** See [[node-controller]].

The `False`/`Unknown` split this shard preserved is exactly the split Chapter 13 §5 uses as a
diagnostic fork: **`False` means somebody is talking to you and telling you they are unwell;
`Unknown` means nobody is talking to you at all.** Two completely different investigations.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/version-skew.md ===

---

## Chapter 13 §6 — the symptom shapes live in a separate shard

Chapter 8 §6 owns the rule; **Chapter 13 §6 owns what skew looks like when you meet it as a
symptom.** The B7 ledger grants Ch 13 §6 that row explicitly, so the material has its own home
rather than being appended here: see **[[version-skew-symptoms]]**.

**This shard keeps every number. That shard states none** — deliberately, so a reader or a later
stage cannot pick up a skew figure from two places and find them disagreeing.

Chapter 13 §6 opens by pointing back here (*"This section will not restate the skew table; go and
re-read it if you need it"*) and honours it. Ch 8 §6's promise that skew returns *"in a form
where you have to use it rather than recite it"* is discharged.

⚠ **The LTS hazard the ledger assigns to Ch 8 §6 is still unwritten.** Verified: shipped Ch 8
does not say Kubernetes has no LTS release, and the skew snapshot contains no use of the term at
all. Chapter 13 §6 correctly declines to raise it, and no graded item anywhere may hinge on it
until the retrofit lands.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===

---

## Chapter 13 §7 — ⚑ CONFLICT 2 RESOLVED · ⚑ CONFLICT 1 NEWLY BREACHED

### ✅ Conflict 2 (the instance count) — the block is lifted

This shard carried `⛔ DO NOT DRAFT Ch 13 §7 OR Ch 17 §7 UNTIL THE COUNT IS RESOLVED`.

**Chapter 13 §7 asserts no ordinal.** Verified against `draft-v2.md`: no count, no "instance,"
no "sighting" anywhere near the retrieval. It states the rule, applies it to a new case
(`kubectl top` with no metrics-server), and says nothing about how many cases there have been.

That is this shard's own **preferred** recommendation — *"stop numbering instances in prose…
the list transfers; the number breaks"* — executed rather than argued. Chapter 13 also declines
to number the control loop and the pluggable interfaces, so it is fully compliant with the
"state the pattern, never the count" convention ratified at the Ch 8 gate.

**Recommendation: lift the block for Ch 17 §7 on the same terms.** Retrieve the rule, add the
instance to the table below, state no count.

**Instance table, extended (un-numbered use recommended):**

| Instance | Where | Announces itself? |
|---|---|---|
| `kubectl top` with no metrics-server | **Ch 13 §7** ✅ shipped | Yes — the command errors |
| An HPA with no metrics-server | **Ch 13 §7** ✅ shipped | Quietly — created, never scales |
| VPA, an addon not shipped by default | Ch 17 §7 (planned) | Yes |

The HPA case is a genuine addition: the pattern **one layer up**, where what is missing is not
the object's controller but the *API* the object depends on.

### ⛔ Conflict 1 (canonical form) — Chapter 13 adopts the form this shard forbade

This shard ruled: *"'The object exists; nothing happens without the component' — **B7 ledger
only. Zero occurrences in shipped text. Do not adopt.**"*

**Chapter 13 adopts it three times** (`draft-v2.md:86`, `:1041`, `:1043`), bolded at `:1041` as
though it were the retrieved name — and **never uses the shipped rule sentence.** Verified:
`draft-v2.md` returns zero matches for *"without its component does nothing."*

That sentence is the most heavily graded in the book. Verified across shipped text:
`chapter-03:1302` · `chapter-10:286, 341, 628, 641, 730, 1354, 1394, 1802, 1856` ·
`chapter-11:811, 1123, 1473, 1630` — **and verbatim in all four options of Ch 10 Practice Q18**
(`chapter-10:1574–1577`).

And `chapter-06:1082` told the reader, in a graded answer key: ***"Name the pattern, because you
will retrieve it by name."*** Chapter 13 is where that retrieval comes due, under a name the
book does not use.

⚠ **The integration report reaches the opposite conclusion** — *"Ch 13 conforms to the skeleton;
Ch 6 and Ch 11 are the outliers"* — because it measured against the B6 skeleton rather than
against shipped reader-facing text. Against the book, **Chapter 13 is the outlier.**

**Fix: one clause in §7 reproducing the shipped sentence verbatim before the paraphrase.** The
cross-bearing text may stay — it is a pointer, not the name. **Do not renormalize Ch 6 and
Ch 11 toward Chapter 13's form; that inverts the book's own canon.**

### Attribution note

§7 and Soundings A8 credit **Chapter 10** with naming the pattern. Ch 10 §3 owns it per the
ledger and §8 is titled for it, so the cross-bearing is right and should stay — but the reader
was told to remember it by name in **Ch 6**. Cheapest fix: *"the book named this for you and
Chapter 10 built a section on it,"* pointer unchanged.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

---

## Chapter 13 §8 — diagnosis as reading a loop's report

Chapter 13's Zenith closes by reading its own central signature through this shard:

> *"A Pod sitting in `Pending` is not a broken thing. It is a control loop that has not
> converged: a declaration of intent that no node has yet been able to satisfy, being patiently
> re-evaluated by a component that will act the instant it can. It is not an error. It is the
> system telling you, accurately, that the world has not yet caught up with what you asked for.*
> *…Diagnosis, in this system, is mostly reading a loop's report and believing it."*

**No ordinal is asserted**, per this shard's standing ruling and the Ch 8 gate's convention.
Chapter 13 states the pattern and points at Ch 3 §6.

⚑ **Ch 15 §7's control-loop payoff is left unspent** — Chapter 13 takes the reading it needs and
does not reach for the synthesis that chapter is holding. Verified by the integration stage and
confirmed here.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cri.md ===

---

## Chapter 13 §5 — the boundary a debugging tool attaches below

The CRI is where `crictl` connects, and Chapter 13 uses the interface the reader already knows
to explain why a second command-line tool exists at all:

```
kubectl → kube-apiserver → kubelet      the cluster's RECORDED view
════════════════════════════════════    ◄── the API boundary
CRI → containerd / CRI-O                ◄── crictl attaches HERE
```

*"`crictl` is a command-line interface for CRI-compatible container runtimes."*
`[source: k8s-docs-crictl-2026-08-31]`

**The argument is the point:** everything above the boundary is what the cluster *believes*;
`crictl` shows what the runtime on this machine is *doing*. When those disagree, the fault is in
the layer between them — the kubelet's registration and reporting path. See [[crictl]].

This also discharges `chapter-03:451`, which promised the framing, and answers the open
AUTHOR-REVIEW at `chapter-02:604` asking for a `crictl` source.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

---

## Chapter 13 — D2.3 Troubleshooting (platform scope)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D2.3 — Troubleshooting** | **Chapter 13** | **deep — primary home, platform scope** | — |

**Declared weight note.** The chapter's metadata line carries the published **28%** for the whole
Container Orchestration domain with its source tag, plus the house disclaimer that the
sub-competency split is authored. The outline's internal 4% is a planning allocation and appears
nowhere in reader-facing text. Correct handling — CNCF publishes no sub-competency weights
(B1 gap G33, B2 disclosure #1).

## Concept-level — D2.3, all 14 B1 concepts

Walked row by row against `domain-analysis.md:214–230`. **10 taught in Chapter 13, 3 deferred to
Ch 16 by design, 1 split to Ch 18.**

| B1 concept | Covered in | Depth |
|---|---|---|
| Two audiences | Ch 13 §1 | deep — the chapter's organizing principle |
| Pod phase as first signal | Ch 13 §1, §2, §8 | deep (taxonomy at Ch 5 §5) |
| Container `Waiting` `Reason` | Ch 13 §2 | deep (taxonomy at Ch 5 §5) |
| Probe failure signatures | Ch 13 §4 | deep (mechanism at Ch 5 §7) |
| Node health | Ch 13 §5 | deep (conditions at Ch 8 §4) |
| Node lease heartbeats | Ch 13 §5 | substantial (mechanism at Ch 8 §4) |
| Node death handling | Ch 13 §5 | deep |
| `crictl` | Ch 13 §5 | deep |
| Known issues | Ch 13 §6 | substantial |
| Resource metrics pipeline | Ch 13 §7 | deep |
| Logging architecture | Ch 13 §7 | substantial — agents to Ch 18 §6 |
| Troubleshooting `kubectl` | Ch 13 §3, §6 | substantial |
| Auditing | **Ch 8 §2** | referred, not re-taught — correct |
| Monitoring tools | **Ch 18** | boundary stated in §7 |
| **Troubleshooting Applications** | **Ch 16** | ⚠ deferred — see below |
| **`kubectl debug`** | **Ch 16 §3** | ⚠ deferred |
| **Local service debugging** | **Ch 16 §5** | ⚠ deferred |

## ⚑ D2.3 has no second owning chapter, and that is a coverage-report bug waiting to happen

The draft's AUTHOR-REVIEW flags `kubectl exec` / `debug` / `port-forward` and Service debugging as
deferred to a chapter filed under D3.2. **Against the concept table the deferral is larger than
that:** it carries an entire D2.3 row — *Troubleshooting Applications* — plus *local service
debugging*. That is roughly a third of the objective.

**The deferrals are correct and explicitly signposted in §1 and in The Voyage Ahead.** The fix
belongs entirely in Ch 16's frontmatter: **`objectives: ["D3.2", "D2.3"]`**. Without it the
book-close coverage report raises a phantom "D2.3 under-covered" finding against a chapter that
covers it deeply.

## Trap coverage — 3 of 3 D2.3 traps, plus nine the inventory does not carry

Verified against `domain-analysis.md:578–580`:

| # | Trap | Where addressed |
|---|---|---|
| 70 | Jumping to `kubectl logs` for a `Pending` Pod | §1's opening argument and a ★ Fixed Point |
| 71 | Treating application and cluster debugging as one activity | §1, the whole section |
| 72 | Expecting `kubectl top` to work without metrics-server | §7 ★ Fixed Point + Practice Q15 |

Two D1 traps reinforced in passing: **#6** (phase vs container state) and **#26** (an
unschedulable Pod does not error out). **D3.2 trap #87** (treating the two domains as identical)
is pre-empted by §1.

**Nine added by the Exam Alert and not in the inventory:** `CrashLoopBackOff` read as an image
problem · empty logs on a crash loop read as a silent app · absent event read as evidence ·
request-versus-limit for OOM · "BestEffort is safest" · omitted `-c` on a multi-container Pod ·
expecting `kubectl` to account for an unregistered container · assuming a non-starting Pod always
exists as an object · expecting `kubectl logs` to be an archive.

## Research gaps

| Gap | Status |
|---|---|
| **G2** — Pod failure signatures by name; B1's **highest-risk single gap in the book** | **5 of 6 closed.** `CrashLoopBackOff`, `ImagePullBackOff`, `ErrImagePull`, `OOMKilled`, `Evicted` now sourced. **`CreateContainerConfigError` open** — zero matches across all 198 snapshots, verified. |
| **G26** — node lifecycle, conditions, eviction | **Closed** by §4 and §5 with shipped Ch 8 §4. |
| **`container-state.md`'s own open fetch** — `CrashLoopBackOff` in no snapshot | **Closed** by `k8s-docs-container-restart-backoff-2026-08-31`. Ch 5 §5's placeholder is now fillable. |
| **`restart-policy.md`'s "other five minutes"** | **Substantially discharged** by §4's ⚠ Hazards; one clause short of explicit. |
| **G1** — the `kubectl` command surface | **Substantially open.** The snapshot claiming to close it is **13 lines** with no command lines — verified. `kubectl events --for`, `--sort-by`, `--all-containers`, `current-context`, and the `RESTARTS`/`READY`/`STATUS` column semantics are all untagged, and five graded items rely on them. |

**Open and touching Chapter 13:** `CreateContainerConfigError` · admission-refusal outcomes and
the ReplicaSet `FailedCreate` event · the Deployment failed-rollout cause list · `volumeBindingMode`
and PVC binding order · `crictl`'s command examples · `--event-ttl`'s default · scheduler event
message formats · the Kubernetes release cadence (Ch 17 §8 owns it).
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

---

## Chapter 13 — backward retrieval

| Tested topic | Original chapter | Retested in |
|---|---|---|
| A tag is a mutable pointer; a digest is content identity | ch 2 §3 | ch 13 — Bearings #1 Q6 |
| The `Guaranteed` QoS criteria are evaluated per container | ch 5 §8 | ch 13 — Bearings #2 Q6 |
| kubelet skew — three minors behind, never ahead | ch 8 §6 | ch 13 — Bearings #3 Q2 |
| An object without its component does nothing | ch 10 §3 | ch 13 — Bearings #3 Q3 |

## ⚑ Chapter 13 compliance — the verdict depends on the denominator

| Check | B3 target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of **Bearings** | **25%** — Ch 13 is one of five chapters at the ceiling | 4 of 17 = **23.5%** | ✅ |
| Retrieval share of the **Practice pool** | same target, *"applied to it once sized"* | **0 of 16 = 0%** | ❌ |
| Retrieval share of **Bearings + Practice** (Ch 12's denominator) | 20–25% | 4 of 33 = **12.1%** | ❌ |
| Spacing floor — ≥1 item ≥4 chapters back | ≥1 | ch 2 is **eleven** back; ch 5 eight; ch 8 five | ✅ |
| Tagged items land on material the named chapter owns | 4 of 4 | **4 of 4**, re-checked against shipped text | ✅ |
| Question inventory | 8 Soundings · ≥10 Bearings across ≥2 checkpoints | 8 + 17 (6+6+5) + 16 = **41** | ✅ |

**All four `[retrieval:]` tags are in Bearings; the Practice pool has none** — verified by tag
search. Chapter 12 put five of its eight in Practice.

**Why the numbers differ.** The integration report's 23.5% uses a checkpoint-only denominator,
which is the skill's literal wording (Part 10: *"20-25% of later **checkpoints**"*). B3 goes
further — *"B4 sizes the Practice Questions pool; **apply the same target percentage to it once
sized**"* — and Ch 12's Stage 14 reported over Bearings + Practice. **Under either of those,
Chapter 13 is short**, and it is short in the chapter B3 designated for the ceiling *because
retrieval is its method*.

**In substance the gap is smaller than the number.** Practice carries three `[interleaved: …]`
items that genuinely reach back — Q2 → Ch 7's scheduling, Q8 → Ch 6's rollouts, Q9 → Ch 12's
Secrets — and each requires holding an earlier-chapter fact and a Chapter 13 fact at once, which
is what skill Part 10's interleaving row asks for. **The defect is that a mechanical audit greps
`[retrieval:` and reads the pool as empty** — and Ch 19 is built by exactly such an audit.

**Cheapest fix, no new questions:** dual-tag Q2, Q8 and Q9 as `[retrieval: ch7]`,
`[retrieval: ch6]` and `[retrieval: ch12]`. Practice → 18.8%; chapter → 21.2%, inside the band on
every denominator. One further item on requests-versus-limits — already named in the Exam Alert as
the easiest error in the material — reaches the 25% ceiling.

**Soundings note.** All eight are retrieval; the block says so and names two as deliberate decay
probes (Ch 7's `Pending`, Ch 8's skew), which is B3's decay-fix schedule executed as designed.
Excluded from the budget per B3.

⚑ **B3's own artifact was never written.** `.pipeline-state/book-outline/retrieval-architecture.md`
contains a permissions-failure message; its substance survives only in the stage summary and the
progress log, from which the targets above are recovered. **Re-run before Ch 19**, which is 100%
retrieval by construction and has no other contract to build on.

## Obligations Chapter 13 discharged — fourteen

Ch 2 §3 (tags and digests → Bearings #1 Q6) · Ch 2 §6 (`imagePullPolicy` and `:latest` → §2) ·
Ch 2 §6 (**diagnosis**, deferred by name in `imagepullbackoff.md` → §2) · Ch 3 §4 (`crictl` and
why a node-level tool exists → §5, pinned) · Ch 3 §6 (the control loop → §8) · Ch 4 §4
(ConfigMaps and Secrets → §2) · Ch 5 §2 (multi-container logs and `-c` → §3, pinned) · Ch 5 §5
(phase vs container state → §1, §2, §4) · Ch 5 §8 (`OOMKilled` and `Evicted`, string released →
§4, pinned) · Ch 7 §2/§4 (`Pending` as a report; capacity vs taints → §2, pinned) · Ch 8 §4 (node
conditions as a diagnostic → §5) · Ch 8 §6 (skew *used* rather than recited → §6, pinned) ·
Ch 10 §3 (the absent-component rule → §7, pinned — ⚑ **see the shard for the form**) · Ch 12 §6
(a refused Pod leaves no object → §2, pinned).

## ⚑ Three obligations arrived incomplete

| Promise | Where made | Status |
|---|---|---|
| *"which of the **six** causes"* of a stalled rollout | `chapter-06:663` and `:778` — **the second is a graded answer key** | Ch 13 §3 names none. The count was cut as unsourced, correctly for this corpus — but the cut **creates** the inconsistency rather than resolving it, because the book already asserts six twice. Needs the Deployment fetch, or edits to both Ch 6 sites. |
| *"Chapter 13 will teach you to tell those two apart **from the symptoms**"* (unbound PVC vs scheduling failure) | `chapter-11:588`, section-pinned at Ch 13 §2 | §2 gives one sentence of family membership. Needs the storage fetch (note the `WaitForFirstConsumer` inversion) or a softening edit at `chapter-11:588`. |
| *"Bring three things with you"* — #2, `securityContext` as *"a permissions failure wearing an application error's clothing"* | `chapter-12:2223`, reader-facing, explicitly enumerated | **NEW — the integration report missed this.** `runAsUser`, `runAsNonRoot`, `securityContext`, `readOnlyRootFilesystem`: **zero occurrences** in Chapter 13. Promises #1 and #3 both land. |

**Fix for the third, and it needs no fetch:** §4 already quotes the documented crash-loop cause list (*"application errors, configuration errors, resource constraints, failing health checks, or probe failures"*) and never says which configuration. **One clause naming `securityContext` among the configuration errors discharges it.** The right home is §4, not Ch 16 — a platform cause producing an application-looking symptom is precisely the discrimination §1 teaches.

## Forward obligations Chapter 13 creates

| Topic Ch 13 owns | Retrieved in | How |
|---|---|---|
| The scope handoff — `Running` + `Ready` + confined + still wrong | **Ch 16 §1** | Reciprocal cross-bearings, both emitted. §8 restates the test in the reader's hearing. |
| `kubectl exec` · `kubectl debug` / ephemeral containers · `kubectl port-forward` | **Ch 16 §3, §5** | Named, withheld, and the withholding *explained*. ⚠ **Ch 16's frontmatter must carry D2.3.** |
| "Is anything even selected" | **Ch 16 §4** | §4's readiness material sets it up from the endpoints side. |
| The absent-component pattern | **Ch 17 §7** | ⛔ **UNBLOCKED** — retrieve the rule, add the instance, state no count. ⚑ Use the *shipped* sentence, not Ch 13's paraphrase. |
| metrics-server vs a monitoring system | **Ch 18 §3** | §7 draws the line and cross-bears; ledger row already assigns it. |
| Node-level logging agents and backends | **Ch 18 §6** | §7 gives one clause and a pointer, as the ledger requires. |
| The release cadence | **Ch 17 §8** | §6 declines to state it — correctly; no snapshot holds it. |
| "Somebody has to install that" as the chapter bridge | **Ch 14** | The Voyage Ahead names metrics-server, a logging backend and an Ingress controller together. |

## Open gaps carried forward, unchanged by Chapter 13

North-south / east-west taught in Ch 10 and assessed in zero questions · Ch 9's *"second instance"* CNI ordinal · Ch 11 Practice Q4's failed `[retrieval: ch4]` anchor · CSI driver architecture taught and never assessed · `PodDisruptionBudget` unowned book-wide (ledger ⚑3) — **Chapter 13 handles this correctly**, its only use being inside a verbatim quotation of what the kubelet does *not* respect.
=== END APPEND ===
```

---

## What needs your decision before this chapter ships

Three things, in order of cost to fix and risk if left:

**1. The Zenith retrieves the pattern under a name the book does not use.** Chapter 13 says *"the object exists; nothing happens without the component."* Chapters 3, 10 and 11 say *"an object without its component does nothing"* — including verbatim in all four options of Ch 10 Practice Q18, and Ch 6 told the reader in a graded answer key to *"name the pattern, because you will retrieve it by name."* Chapter 13 never uses that sentence. The integration report called Chapter 13 conformant because it measured against the B6 skeleton; measured against shipped text, Chapter 13 is the outlier. **One clause in §7.**

**2. Chapter 12 hands three things forward and Chapter 13 takes two.** `securityContext` as a permissions failure in application clothing does not arrive — zero occurrences of `runAsUser` or `securityContext` in the draft. This is a third broken promise; the integration report found two. **One clause in §4's crash-loop cause list.**

**3. The Practice pool carries no tagged retrieval at all.** Bearings hit 23.5%, which is what the integration report reported. B3 puts Chapter 13 at the 25% ceiling and applies the target to the Practice pool too, where the count is 0 of 16. The three `[interleaved:]` items do the work in substance; dual-tagging them fixes the number without writing a question.

Two of the draft's own AUTHOR-REVIEW comments resolve against material the book already holds rather than needing research: the kernel-agency axis it cut is sourced in shipped Ch 5 §8 and sitting in `resource-limit.md`, and `container-state.md`'s open fetch for `CrashLoopBackOff` is closed by this chapter's own corpus.

Separately, and independent of the chapter: **`Book-KCNA/knowledge-base/` does not exist, and twelve manifests are pending against it.** Ch 03, Ch 10 and Ch 11 each open with full WRITEs to the three shared registers, so a naive replay in chapter order destroys nine chapters of glossary, coverage and retrieval content. Ch 10's and Ch 11's blocks justify those WRITEs with *"Chapters 1–9 shipped before Stage 14 existed"* — a premise their own sibling directories disprove. Converting four WRITE blocks to APPENDs before any replay is mechanical and costs nothing.