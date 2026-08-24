# Fact-Accuracy Audit — Chapter 6

**Mode detected: STANDARD.** The `Cached sources` block contains 21 populated snapshots, and the draft carries ~214 inline `[source: …]` tags. Neither adoption-mode trigger fires. Untagged factual claims are therefore reported as FAIL.

**Location convention:** the draft supplied to this stage is the reconstruction assembled from `.draft-v1.md.progress.log`, not the 4,050-byte truncated `draft-v1.md` on disk. Line numbers against that file would be meaningless, so every finding below is anchored by **section + verbatim quote**, with an approximate line number against the reconstructed text. Search the quote, not the line number.

---

## Summary

- Total factual claims inspected: **236** — 214 `[source: …]` tag instances (≈130 distinct assertions; many repeat across body, checkpoint, Exam Alert and Chapter Summary) plus 22 untagged sentences carrying factual weight
- Tagged claims verified: **214** (100% of tag instances resolve to a supplied snapshot and match it)
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0** — every tag resolves. 20 of the 21 supplied snapshots are cited; `k8s-docs-autoscaling-2026-08-23` is supplied but uncited, which is not a defect
- **Untagged factual claims (FAIL): 5 findings covering 11 instances**
- **Contradicted claims (FAIL): 0**
- Minor discrepancies (WARN): **10**

**Three standing AUTHOR-REVIEW questions are settled by this audit** (detail in PASS): the rolling-update ceiling is **13, not the outline's 12**; the selector/template mismatch is **an API rejection, not a live runaway**; the DaemonSet `replicas` claim **must stay in its hedged form** until the API reference is cached.

---

## FAIL — Untagged factual claims

### F-1 · Metadata line (approx. line 4): "**Domain: Kubernetes Fundamentals — competency D1.1, Kubernetes Core Concepts | Authored weight: ~6% of this book**"

**Why it's a factual claim:** it asserts, about the certifying body, (a) that a domain named *Kubernetes Fundamentals* exists in the credential, and (b) that it contains a competency numbered **D1.1** named *Kubernetes Core Concepts*. Both are claims about third-party authority and neither carries a tag.

No snapshot in this corpus is a curriculum document. The `objectives_covered` frontmatter in the snapshots is **pipeline metadata, not authority**, and it is internally inconsistent — across the 21 files it uses `D1 Core Concepts`, `D1.1`, `D1 Containerization`, `D1 Administration`, `D2 Storage`, `D2 Networking`, `D2 Troubleshooting`, `D3 Application Delivery`, and `D4 Cloud Native Ecosystem and Principles`. At least two different domain schemes are represented there. Citing it would be citing ourselves.

Related, and also untagged: the draft's own AUTHOR-REVIEW comment (approx. line 7) asserts "*CNCF publishes four domain weights and twelve named competencies with no sub-weights*." That is itself an unverifiable claim about the vendor, and it sits in tension with the metadata line directly above it, which uses a **sub-numbered** competency ID (`D1.1`) while the comment says there are no sub-weights.

**Fix:** open a research gap for the official KCNA curriculum / exam-objectives page and cache it as `cncf-kcna-curriculum-YYYY-MM-DD.md`. Until it exists, no domain name, competency ID, or competency count can be stated. The `~6%` figure itself is fine as written — it is explicitly labelled *authored weight*, which is an internal fact about this book, not an external one; only the phrasing-consistency point in the existing AUTHOR-REVIEW comment applies to it.

---

### F-2 · Exam-format and exam-likelihood claims (six instances)

**Why they're factual claims:** each asserts something about how the certification exam is constructed or weighted. None carries a tag, and no cached snapshot is an exam document.

| Approx. line | Section | Quote |
|---|---|---|
| ~46 | Soundings, reading strategy | "That is the highest exam-points-per-minute route through this chapter." |
| ~102 | Why This Chapter Matters | "is exactly the kind of thing a recognition exam asks about in one sentence" |
| ~437 | §4, The two bounds | "these are the exam-checkable content of this chapter" |
| ~516 | §5, The rule stated exactly | "precisely the kind of boundary a recognition exam tests" |
| ~902 | Exam Alert, header | "**High-priority topics, in descending order of likelihood.**" |
| ~890 | §8, Closer Look | "For associate-level purposes: CRD is the common path, aggregation is the rarer one" |

The Exam Alert header is the load-bearing one: *descending order of likelihood* asserts a ranking of question frequency across eight topics. Nothing in the corpus supports a ranking.

**Fix:** two options, and they can be mixed. (1) Cache the curriculum page (same gap as F-1) and re-anchor the ranking to published domain weights, stating explicitly that ordering within a domain is authored judgement. (2) Re-frame as authored guidance rather than exam fact — "in descending order of how much of this chapter depends on them," "the kind of boundary that is easy to get backwards." Option 2 costs nothing and is defensible today; option 1 is stronger and is needed anyway for F-1.

---

### F-3 · §3, after the rejection rule (approx. line 300): "it is nearly the only place in Kubernetes where the API says *no* instead of accepting your intent and reconciling toward it"

**Why it's a factual claim:** it asserts a general property of the Kubernetes API surface — the scarcity of hard rejection — and the reader will carry it as a rule.

It is untagged, and the cached corpus supplies three counterexamples in the opposite direction:

- "once a DaemonSet is created, its `.spec.selector` can not be mutated" [`k8s-docs-daemonset-2026-08-24`]
- "Cross-namespace owner references are disallowed by design." [`k8s-docs-garbage-collection-2026-08-24`]
- dynamic admission control is listed as a first-class API-access extension point whose whole job is refusing writes [`k8s-docs-extending-kubernetes-2026-08-23`]

**Fix:** drop the superlative and keep the pedagogical point, which is sound and needs no source: *"This is one of the few validations Kubernetes performs by refusing the object outright rather than accepting it and reconciling toward it — because what you wrote has no reachable steady state at all."* No tag required once the scarcity claim is gone.

---

### F-4 · §1, Three layers, not two (approx. line 133): "The most common workload resource is the **Deployment**."

**Why it's a factual claim:** a frequency/popularity assertion about ecosystem usage. Nothing in the corpus ranks workload-resource usage.

The corpus supports a nearby but different claim — *recommendation*, not *frequency*: "Usually, you define a Deployment and let that Deployment manage ReplicaSets automatically" and "we recommend using Deployments instead of directly using ReplicaSets" [`k8s-docs-replicaset-2026-08-24`].

**Fix:** one-clause rewrite to the sourced form: *"The workload resource you will reach for most often, and the one the documentation recommends over managing ReplicaSets yourself [source: k8s-docs-replicaset-2026-08-24], is the **Deployment**."*

---

### F-5 · Practice Q16 answer, option C (approx. line 1103): "though you will see the word in `kubectl get pods` output as a container-state reason, which is exactly why the distractor works"

**Why it's a factual claim:** it asserts what a specific CLI command prints. It sits inside a sentence that is otherwise correctly tagged, so the untagged half reads as covered by the tag.

`k8s-docs-pod-lifecycle-2026-08-23` supports the tagged half — the five phases, and `Completed` not being among them. It describes container states as `Waiting` / `Running` / `Terminated` with a `Reason` field, but **no cached sentence says `Completed` is surfaced in `kubectl get pods` output**, and `k8s-docs-kubectl-overview-2026-08-23` documents `get` only as "List one or more resources."

**Fix:** either open a research gap for a snapshot covering Pod status printing (the `kubectl get pods` STATUS column derivation), or soften to something the corpus carries: *"…though `Completed` is a word you will meet in tooling output, which is exactly why the distractor works."* The pedagogical value survives the softening intact.

---

## FAIL — Contradicted claims

**None.** Every one of the 214 tag instances was checked against the sentence it points to. No tagged claim disagrees with its snapshot. The numeric claims most at risk of transposition — `maxSurge`/`maxUnavailable` defaults and rounding direction, both worked examples, `revisionHistoryLimit`, `progressDeadlineSeconds`, `minReadySeconds`, and both `replicas` defaults — are all correct and are itemised in PASS below.

Two corpus hazards were checked for exposure and found clean:

- `k8s-docs-job-2026-08-24` warns that a first-pass fetch reported `.spec.backoffLimit` as 4 where the raw source says 6. **The draft never mentions `backoffLimit`.** No exposure.
- `k8s-docs-replicationcontroller-2026-08-24` is truncated and its "Alternatives" section is not cached. The draft's ReplicationController comparison ("does not support set-based selector requirements") is correctly sourced to the ReplicaSet page, where that sentence *is* cached, exactly as the snapshot's own note directs. Handled correctly.

---

## WARN — Minor discrepancies

### W-1 · §1, The template (approx. line 185) — citation scope

> "`.spec.template` is a Pod template with exactly the same schema as a Pod, except that it is nested and carries no `apiVersion` or `kind` of its own [source: k8s-docs-daemonset-2026-08-24]"

The sentence sits in the Deployment/ReplicaSet discussion but is sourced to the DaemonSet page, which states it **about DaemonSet's template**. The corpus carries no equivalent sentence for a Deployment or ReplicaSet template — the Deployment API-reference excerpt says only "Template describes the pods that will be created." The generalisation is almost certainly right; it just isn't cached. **Fix:** attribute it visibly ("the DaemonSet page states the rule most explicitly") or cache the ReplicaSet/Deployment API reference.

### W-2 · §3, Membership is a query (approx. line 285) — paraphrase sharpens a loose snapshot into an error

> "newer resources such as Job, Deployment, ReplicaSet and DaemonSet support set-based requirements through both [source: k8s-docs-labels-selectors-2026-08-23]"

"Through both" attributes set-based support to `matchLabels`. The same snapshot defines `matchLabels` as "a map of {key,value} pairs equivalent to matchExpressions with operator In" — i.e. equality-shaped. The imprecision originates in the snapshot's compression of the source page, and the draft faithfully inherited it. **Fix:** *"…support set-based requirements, expressed through `matchExpressions`; `matchLabels` is the equality-shaped shorthand, equivalent to `matchExpressions` with the operator `In` [source: k8s-docs-labels-selectors-2026-08-23]."*

### W-3 · §6, The resource (approx. line 655) — dropped hedge

Draft: "each Pod is assigned an integer ordinal unique across the set, **from 0 through N−1**."
Snapshot: "**By default**, pods will be assigned ordinals from 0 up through N-1." [`k8s-docs-statefulset-2026-08-24`]

The hedge is load-bearing — the start ordinal is configurable. **Fix:** restore "by default." One word.

### W-4 · §1, Fixed Point (approx. line 172) — simplification that §4 later contradicts in spirit

> "The Deployment sets it on the ReplicaSet it currently considers current."

During a rollout the Deployment controller sets counts on **all** active ReplicaSets: "the Deployment controller balances the additional replicas in the existing active ReplicaSets (ReplicaSets with Pods)… This is called proportional scaling" [`k8s-docs-deployment-spec-fields-2026-08-24`]. §4 gets this right ("deciding, moment to moment, what those two counts should be"). **Fix:** hedge §1 — "on the ReplicaSet it currently considers current; §4 shows what happens when there are two."

### W-5 · §2, The demonstration (approx. line 243) — terminal transcript, and one suspect Pod name

The `kubectl get pods` / `kubectl delete pod` / `kubectl scale` transcripts assert what the tool prints (column set, `ContainerCreating`, `deployment.apps/web scaled`, generated name shape). No cached snapshot covers CLI output formatting, so none of it is verifiable here. That is normal for a teaching transcript and I am not proposing tags on every code block — but one specific item should be checked before print:

> `web-7d4b9c6f8-qq81z`

Kubernetes' generated-name alphabet is believed to exclude vowels and the digits `0`, `1`, and `3`, which would make `1` impossible in a generated Pod suffix. **I cannot verify that from this corpus** — flagging it as a check, not as a finding. The other three suffixes (`mn4pq`, `x9k2r`, `z7rtc`) and the ReplicaSet hash (`7d4b9c6f8`) are consistent with that alphabet, which is itself weak evidence the constraint was being followed and `qq81z` is a slip. **Fix:** change `qq81z` → e.g. `qq8jz`, or cache a source covering name generation.

### W-6 · Figure anchors and captions are transposed (approx. lines 690 and 787) — structural, not factual

- `<!-- FIGURE: ch06-fig05-statefulset-vs-deployment-identity -->` is captioned "**Figure 6.4**"
- `<!-- FIGURE: ch06-fig04-workload-resource-decision-tree -->` is captioned "**Figure 6.5**"
- `<!-- FIGURE: ch06-zenith-control-loop-instantiated -->` is captioned "**Figure 6.6**" but carries no `figNN` token

Caption numbering is internally consistent (6.1–6.6, and all six in-text references match their captions), so the reader sees nothing wrong. Outside this audit's remit, logged because Stage 10 emits `yaml-figure-spec` blocks keyed off these anchors and the transposition will propagate into the diagram pipeline. **Fix:** swap the two `figNN` tokens; decide whether the Zenith figure wants `ch06-fig06-`.

### W-7 · Practice Q9 answer, option C (approx. line 1063) — tag covers less than the sentence claims

> "revision history is a property of Pod-template changes and is unaffected by strategy [source: k8s-docs-deployment-2026-08-23]"

The snapshot supports "a new revision is created if and only if the Deployment's Pod template is changed." The added clause *"and is unaffected by strategy"* follows logically but is not stated. Low risk. **Fix:** trim to the sourced form.

### W-8 · §5, What is kept (approx. line 566) — snapshot-internal tension, correctly handled; do not "fix"

`k8s-docs-deployment-2026-08-23` says "By default, all of the Deployment's rollout history is kept in the system." `k8s-docs-deployment-spec-fields-2026-08-24` says "By default, 10 old ReplicaSets will be kept." The draft reproduces both and reconciles them explicitly ("the default answer is yes, ten deep"). **This is the correct handling.** Logged so a downstream stage does not read it as a contradiction and "correct" one of the two away.

### W-9 · Chapter Summary, DaemonSet row (approx. line 1140) — hedge weaker than in the body

Body, Fixed Point and Exam Alert all use the defensible form ("the count is a consequence of the cluster, not a setting" / "expresses *per node*, not a number"). The summary row states "**Not a replica count**," which reads closer to asserting field absence. `k8s-docs-daemonset-2026-08-24` flags this exact gap in its own trailer: "no fetched sentence states explicitly that a DaemonSet has no `replicas` field… See research-manifest Gaps, G-6A." **Fix:** align the summary row to the body's phrasing, or close G-6A by caching the DaemonSet API reference.

### W-10 · Practice Q19 answer (approx. line 1119) — inference stated as given

> "while the built-in controllers ship with the control plane"

Supported only obliquely: the HPA controller is described as "running within the Kubernetes control plane" [`k8s-docs-hpa-2026-08-24`], and the operator page contrasts with "outside of the control plane" [`k8s-docs-operator-pattern-2026-08-23`]. No cached sentence states the general rule for built-in controllers. Low risk. **Fix:** add the HPA citation as the worked instance, or soften to "while the controllers Kubernetes ships run in the control plane, as the HPA controller does [source: k8s-docs-hpa-2026-08-24]."

---

## PASS — Verified claims

Full verification of every tag instance was performed; this lists the load-bearing and exam-checkable ones, plus the three questions the draft's AUTHOR-REVIEW comments raised.

### The three open AUTHOR-REVIEW questions — settled

**1. Rolling-update ceiling: the draft's 13 is correct; the outline's 12 is wrong.**
Snapshot: "`.spec.strategy.rollingUpdate.maxSurge` … The absolute number is calculated from the percentage by **rounding up**. The default value is 25%." and "`maxUnavailable` … The absolute number is calculated from percentage by **rounding down**. The default value is 25%." [`k8s-docs-deployment-spec-fields-2026-08-24`]. Corroborated by the API reference in the same snapshot ("Absolute number is calculated from percentage by rounding up" / "…by rounding down"). For 10 replicas: ceil(2.5)=3 → ceiling 13; floor(2.5)=2 → floor 8. The draft's §4 worked example, Figure 6.2, Bearings #2 Q1 (answer B, 13/8), and Practice Q7 (answer C, 13) are **all correct and mutually consistent**. The outline's 12 must be corrected, not the draft.

**2. Selector/template mismatch: the draft's rejection reading is correct.** All three cached sources agree, in the same words:
- "In the ReplicaSet, `.spec.template.metadata.labels` must match `spec.selector`, or it will be rejected by the API." [`k8s-docs-replicaset-2026-08-24`]
- "`.spec.selector` must match `.spec.template.metadata.labels`, or it will be rejected by the API." [`k8s-docs-deployment-spec-fields-2026-08-24`]
- "The `.spec.selector` must match the `.spec.template.metadata.labels`. Config with these two not matching will be rejected by the API." [`k8s-docs-daemonset-2026-08-24`]

The outline's live-runaway reading is unsupported. The draft's handling — teach the rejection, use the runaway as the *reason* for it, and make Bearings #1 item 3 and Practice Q3 both land on "the API rejects the object" with option A explicitly named as the right intuition — is the correct resolution.

**3. DaemonSet `replicas`: keep the hedged form.** Confirmed against the snapshot's own trailer note. The draft's phrasing ("the count is a consequence of node eligibility") is exactly what the corpus supports, via "The DaemonSet controller creates a Pod for each eligible node" [`k8s-docs-daemonset-2026-08-24`] plus "Horizontal pod autoscaling does not apply to objects that can't be scaled (for example: a DaemonSet.)" [`k8s-docs-hpa-2026-08-24`]. The stronger form needs G-6A closed. See W-9 for the one row that drifts stronger.

### Numeric and field-level claims — all verified

| Claim | Snapshot |
|---|---|
| Deployment `.spec.replicas` optional, defaults to 1 | deployment-spec-fields |
| ReplicaSet `.spec.replicas` defaults to 1 | replicaset |
| `maxSurge` default 25%, rounds **up**; `maxUnavailable` default 25%, rounds **down** | deployment-spec-fields |
| Neither may be 0 if the other is 0 | deployment-spec-fields |
| 6-replica arithmetic in Practice Q8: ceiling 8, floor 5 | derived, correct |
| `.spec.minReadySeconds` defaults to 0 | deployment-spec-fields |
| `.spec.progressDeadlineSeconds` defaults to 600; condition `type: Progressing`, `status: "False"`, `reason: ProgressDeadlineExceeded`; controller keeps retrying | deployment-spec-fields |
| `.spec.revisionHistoryLimit` defaults to 10; 0 means a new rollout cannot be undone | deployment-spec-fields |
| Six named causes of a stuck rollout (draft says "six," lists all six) | deployment-spec-fields |
| `RollingUpdate` is the default strategy; `Recreate` kills all before creating | deployment-2026-08-23 |
| Revision created **iff** `.spec.template` changes; scaling creates none | deployment-2026-08-23 |
| `kubectl rollout`: exactly six subcommands; valid types deployments/daemonsets/statefulsets | kubectl-rollout |
| `--to-revision=<n>`; pause/resume rationale | deployment-2026-08-23 |
| CronJob `0 3 * * 1` = Monday 3 AM; five-field syntax; `.spec.timeZone`; `.spec.jobTemplate` schema | cronjob |
| Derived: `0 2 * * *` for 02:00 daily (Bearings #3 answer 3) | derived from cronjob syntax, correct |
| Job `restartPolicy` limited to `Never` or `OnFailure` | job |
| Pod phases `Succeeded` / `Failed` definitions | pod-lifecycle |
| StatefulSet hostname pattern `$(statefulset name)-$(ordinal)`; `web-0/1/2`; identity survives rescheduling; one PVC per volumeClaimTemplate bound for the Pod's lifecycle; create 0→N−1, terminate N−1→0; predecessors Running and Ready; volumes not deleted on scale-down; Headless Service is the author's responsibility; `statefulset.kubernetes.io/pod-name` label enables per-member Services | statefulset |
| DaemonSet: Pods added as nodes join, GC'd as nodes leave, deleting cleans up; no selector/affinity → all nodes; three typical uses | daemonset |
| ReplicaSet adoption: no-owner-reference + matching selector → immediate acquisition; not limited to its own template; surplus adopted Pod immediately terminated | replicaset |
| Owner references distinct from labels/selectors; cascading deletion; background is the default; EndpointSlice carries both a label relationship and an owner reference | garbage-collection |
| Pod replaced with a new UID, never rescheduled; higher-level controllers create replacements; readiness failure removes the Pod IP from all matching Service endpoints | pod-lifecycle |
| ReplicationController legacy/superseded; ReplicaSets are its successors; no set-based selector support | replicationcontroller + replicaset |
| HPA: API resource + controller, runs in the control plane, intermittent loop, ReplicaSet is a valid target, does not apply to DaemonSets | hpa |
| Custom resources store and retrieve structured data **only**; dynamic registration; accessed with kubectl like built-ins; CRD frees you from writing an API server at the cost of flexibility vs aggregation; operator pattern = custom resource + custom controller; operator controller normally runs outside the control plane, e.g. as a Deployment; six published extension-point categories; controller loop = read `.spec`, act, write `.status` | custom-resources, operator-pattern, extending-kubernetes |
| `spec` = desired state set by you, `status` = current state supplied by the system; the docs' own three-replica Deployment example | objects |

---

## Recommended research gaps to open

1. **`cncf-kcna-curriculum-*`** — official exam objectives/domain weights. Blocks F-1 and the strong form of F-2. Highest priority; it will be needed by every chapter's metadata line, not just this one.
2. **`k8s-api-daemonset-v1-*`** — DaemonSet API reference, to close the existing G-6A gap and let W-9 take the strong form.
3. **`k8s-api-replicaset-v1-*` / `k8s-api-deployment-v1-*` pod-template field description** — closes W-1's citation-scope issue.
4. *(optional)* a source covering `kubectl get pods` status-column derivation and generated-name format — would close F-5 and W-5 together.