# Fact-Accuracy Audit — Chapter 7

**Mode detected: STANDARD.** The draft carries 146 inline `[source:]` tags across 16 distinct snapshots, and the cached-sources block is fully populated (20 snapshots).

**Input substitution (read this first — it affects line numbers).** Neither `draft-v2.md` nor `draft-voice.md` exists in `../Book-KCNA/.pipeline-state/ch-07/`. The voice stage wrote in place: the current voiced draft is **`draft-v1.md`** (1123 lines, 2026-08-24 10:07), with the pre-voice text preserved as `draft-v1-prevoice.md`. **This audit was run against `draft-v1.md`, and all line numbers below refer to it.** The two findings under *Contradicted* appear at identical line numbers in both files, so they originated at drafting, not at voicing.

---

## Summary

- Total factual claims inspected: **164** — 146 `[source:]`-tagged claim instances (exact census) plus ≈18 untagged sentences asserting Kubernetes or CNCF behaviour
- Tagged claims verified: **144**
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0** — every tag resolves to a snapshot present in this stage's cached-source block
- **Untagged factual claims (FAIL): 6**
- **Contradicted claims (FAIL): 2**
- Minor discrepancies (WARN): **10**

Overall this is a high-fidelity draft. Quotation discipline is unusually good: every `> ` block quote I checked reproduces its snapshot word-for-word, the `[PARTIAL]` / `[VERBATIM]` boundary from the 2026-08-24 fetch set is respected almost everywhere, and the two research-manifest prohibitions (G-7A "do not compose a skew formula", G-7C "must not assert a formula") are both honoured. The failures below are narrow.

---

## FAIL — Untagged factual claims

### Line 4 and 6: "**Domain: Kubernetes Fundamentals — competency: Scheduling | Authored weight: 5%**" / "*CNCF publishes four domain weights and a list of named competencies; it does not publish sub-weights.*"

**Why it's a factual claim:** It names a CNCF domain, asserts that "Scheduling" is a CNCF-named competency, and makes a positive claim about what the vendor does and does not publish. All three are vendor facts, and the whole metadata line carries no source tag.

**This is also a break with shipped house convention**, which is the cheapest thing to fix in this report. Chapters 2 and 5 ship the same line fully tagged and in a different shape:

> `chapter-05-the-smallest-vessel.md:190` — **Exam domain: Kubernetes Fundamentals (44% of the exam) — competency: Kubernetes Core Concepts** `[source: cncf-kcna-certification-page-2026-08-23]` `[source: cncf-kcna-curriculum-pdf-2026-08-23]` **| Estimated share of the exam: ~7% (authored allocation — CNCF publishes domain weights, not competency weights** `[source: cncf-kcna-curriculum-pdf-2026-08-23]`**; see front matter) | …**

Chapter 7's version drops the published 44% domain weight *and* both source tags, and moves the disclosure into a separate italic line.

**Fix:** Replace lines 4 and 6 with the ch-02/ch-05 form, substituting `competency: Scheduling` and `~5%`. Both snapshots (`cncf-kcna-certification-page-2026-08-23`, `cncf-kcna-curriculum-pdf-2026-08-23`) exist in `sources/` — they simply weren't in this stage's referenced-snapshot slice, so I could not verify the 44% figure directly; ch-02 and ch-05 shipped it tagged, so copy rather than re-derive.

---

### Line 203: "And not observed usage, which the scheduler never consults at all." (recurs at 215, 297–298, 882, 1038)

**Why it's a factual claim:** An absolute negative about scheduler behaviour, and it is load-bearing — Practice Question 3's distractor **A** is graded wrong on exactly this basis ("**A** is the trap: it does the arithmetic against *usage*, which the scheduler never consults").

The *positive* half of the argument is fully sourced and correct: `PodFitsResources` checks requests, the kubelet "reserves at least the request amount", and "the scheduler does not over-subscribe 'Allocatable'". No cached snapshot states the negative — that the scheduler never reads live utilisation.

**Fix:** Either soften to what the sources support ("…and not observed usage: the filter is stated against requests, and the reservation stands whether or not the container touches it"), or open a research gap for `kubernetes.io/docs/concepts/scheduling-eviction/resource-bin-packing/` (or the scheduler-config plugin reference), which would source the point properly. The conclusion is right; only the absolute phrasing is unsupported.

---

### Line 229: "Some of that total is spoken for by things that aren't Pods."

**Why it's a factual claim:** It asserts a relationship between node Capacity and Allocatable — that Capacity exceeds Allocatable and that the difference is non-Pod reservation.

`k8s-docs-node-allocatable-2026-08-24` carries an explicit instruction on this exact sentence position: *"**§2 must not state an arithmetic relationship between capacity and allocatable.** … The source presents this as an image (`node-capacity.svg`) with no text equivalent."* (research-manifest Gap **G-7C**). The draft does not state a *formula*, so it complies with the letter of the guardrail, but it does assert the relationship the guardrail exists to prevent, and it does so untagged.

**Fix:** Lowest-cost option — drop the sentence and let the existing Chapter 8 deferral carry the weight: *"…do it against Allocatable, not against the machine's total RAM. What makes the two differ, and how it's configured, is Chapter 8's material."* Alternatively re-fetch `reserve-compute-resources` at the depth the current snapshot deliberately skipped (`kube-reserved`, `system-reserved`, eviction thresholds) — but note that snapshot's `scope_note` assigns that material to Chapter 8 on purpose.

---

### Line 522 and 1105: "`node.kubernetes.io/unschedulable` — … **Something puts it there on purpose, as a deliberate administrative act**"

**Why it's a factual claim:** It asserts the *cause* of a specific built-in taint, and it is the chapter's hand-off hook into Chapter 8 (repeated in The Voyage Ahead at 1105).

It is also the one place where an untagged claim sits in mild tension with a cached source. `k8s-docs-well-known-labels-2026-08-24` describes that taint's origin differently: **[PARTIAL]** — *"The taint will be added to a node when initializing the node to avoid race condition."* Nothing cached links `kubectl cordon` to the `unschedulable` taint; `k8s-docs-nodes-2026-08-23` says only that cordon "prevents the scheduler from placing new pods onto that Node."

**Fix:** Tag the administrative reading to `k8s-docs-nodes-2026-08-23` and phrase it through cordon rather than through the taint's origin — e.g. "marking a node unschedulable is a deliberate administrative act `[source: k8s-docs-nodes-2026-08-23]`, and that act is Chapter 8's opening move." That keeps the Chapter 8 hook intact without asserting an unsourced causal chain.

---

### Line 622 and 796: "Identical Pods are equally feasible on every node and **score identically on every node**, and the scheduler is entirely free to pick the same node twice."

**Why it's a factual claim:** It asserts what the scoring step produces for identical Pods, and it is the stated justification for Bearings #3 answer 1.

The cached kube-scheduler snapshot says only that the scheduler "assign[s] a score to each Node that survived filtering, basing this score on the **active scoring rules**." Nothing cached describes which rules are active by default, so nothing supports the claim that a second identical Pod scores the same everywhere *after* the first has been placed and has consumed capacity.

**Fix:** The conclusion needs no source and is the part that matters. Re-cast as the absence of a constraint rather than as a scoring outcome: "Nothing in their specs distinguishes one node from another, and nothing tells the scheduler these two Pods are related — so it is entitled to pick the same node twice." Same teaching beat, no unsourced mechanism.

---

### Line 1052 (Practice Q10 answer key) and the §7 figure at 844–846: `PreferNoSchedule` "…the node stays in the running with a worse rank, **which is scoring**"

**Why it's a factual claim:** Q10's whole answer key turns on assigning each taint effect to a named scheduler stage, and the §7 figure assigns eight mechanisms to the FILTER and SCORE columns. No cached snapshot places any of them in a stage. `k8s-docs-taints-tolerations-2026-08-23` says only that with `PreferNoSchedule` "the control plane will try to avoid placing a Pod… but it is not guaranteed." The same applies to Q13's answer at 1058 ("Pod affinity is also evaluated as part of feasibility — it can only ever *narrow* the surviving set").

**To be clear about scope:** §7's Zenith itself — "hard rules filter, soft rules score" — is the chapter's organising synthesis and is not a target of this audit. The FAIL is narrower: an exam-style answer key grades a reader wrong on a stage assignment that no cached source states.

**Fix:** Open a research gap for `kubernetes.io/docs/reference/scheduling/config/`, which enumerates each plugin against its extension points (`TaintToleration` appears at both `Filter` and `Score`; `InterPodAffinity` at `Filter`, `PreFilter` and `Score`). One snapshot upgrades the §7 figure, Q10 and Q13 together, and it is the single highest-value fetch this chapter is missing.

---

## FAIL — Contradicted claims

### Line 362 and 830: "The word is **thirty-nine characters**; the meaning is six." / "one of them has a field name **thirty-nine characters long**"

**Tag:** *(untagged — but the field name is cached verbatim in `k8s-docs-assign-pod-node-2026-08-23` and `k8s-docs-assign-pod-node-depth-2026-08-24`, so the claim is checkable against the snapshot text.)*

**Snapshot says:** `requiredDuringSchedulingIgnoredDuringExecution` — **46 characters** (verified: `printf '%s' requiredDuringSchedulingIgnoredDuringExecution | wc -c` → `46`). `preferredDuringSchedulingIgnoredDuringExecution` is 47. The only nearby figure is 38, the length of the shared tail `DuringSchedulingIgnoredDuringExecution` — which is not what either sentence refers to.

**Draft says:** thirty-nine, in two places.

**Recommended fix:** Change both to **forty-six**. The mnemonic's rhetorical shape survives unchanged ("forty-six characters; the meaning is six" is if anything a better line). Note that "the meaning is six" is correct — *required when scheduling, ignored once running* is six words — so only the character count moves. Present in `draft-v1-prevoice.md` at the same lines, so this is a drafting-stage error the voice pass carried forward.

---

### Line 526: "the DaemonSet controller automatically adds tolerations for **all seven** of the built-in condition taints to the Pods it creates"

**Tag:** `[source: k8s-docs-daemonset-2026-08-24]`

**Snapshot says:** the toleration table has seven rows, but the seventh is explicitly conditional — *"`node.kubernetes.io/network-unavailable` | `NoSchedule` | **Only added for DaemonSet Pods that request host networking, i.e., Pods having `spec.hostNetwork: true`.** Such DaemonSet Pods can be scheduled onto nodes with unavailable network."* The snapshot's own framing is the unquantified *"The DaemonSet controller automatically adds **a set of** tolerations to DaemonSet Pods."*

**Draft says:** "all seven … to the Pods it creates" — unqualified, and the numeral makes the overreach explicit rather than incidental.

**Recommended fix:** Drop the numeral: "…automatically adds tolerations for the built-in condition taints to the Pods it creates." If the count is wanted for its rhetorical punch, qualify it: "six of the seven unconditionally — the seventh, `network-unavailable`, only for DaemonSet Pods that request host networking." The ch-07 outline (line 434) also says "all of them", so this propagated from planning; the surrounding claims at 526 (the `unschedulable` toleration, and the `NoExecute` tolerations carrying no `tolerationSeconds`) are both exact and need no change.

---

## WARN — Minor discrepancies

**1. Line 284 — tag over-reach.** *"binding notifies the API server, and the kubelet on the chosen node starts the containers* `[source: k8s-docs-kube-scheduler-2026-08-23]`*."* That snapshot never mentions the kubelet. The claim is properly sourced elsewhere in the chapter — Practice Q6's answer at 1044 tags it to `k8s-docs-cluster-architecture-2026-08-23` — so the fix is to add that second tag at 284. (The Fixed Point at 169 restates the same claim untagged; I treated Fixed Points and Checkpoints as summaries of adjacent sourced prose and did not flag them as separate untagged claims. Flagging this convention so the revision stage can override it if it disagrees.)

**2. Line 328 — "populates a standard set of labels on **all nodes**" + zone/region.** The two claims are individually sourced but read together they overstate. `k8s-docs-well-known-labels-2026-08-24` marks the zone entry **[PARTIAL]** and says it is "populated by the kubelet **or cloud-controller-manager**" — i.e. not guaranteed present on a cluster with no cloud provider, which is precisely the learner's `kind`/`minikube` cluster. §5 then depends on zone labels existing. Suggest: "`kubernetes.io/hostname`, `kubernetes.io/os` and `kubernetes.io/arch` are populated by the kubelet; `topology.kubernetes.io/zone` and `…/region` are populated by the kubelet or the cloud-controller-manager, so they appear where the cluster has a cloud provider to ask." The label *keys* are all correctly cited — G-7B's instruction ("cite the keys freely, quote the descriptions only for `kubernetes.io/hostname`") is followed exactly, which is worth noting as done right.

**3. Line 633 — "genuinely the same machinery … not a second system to learn."** `k8s-docs-assign-pod-node-depth-2026-08-24` records, as **[PARTIAL]**, that "`Gt` and `Lt` are not available for `podAffinity`." Since §3 line 353 hands the reader six operators and §5 says the machinery is the same, a reader will reasonably infer six operators apply to inter-Pod rules. One clause fixes it: "…the same machinery pointed at a different set of labels — with the one exception that `Gt` and `Lt` are node-affinity-only." Existence of the restriction is confirmed by the snapshot even though the sentence is not quotable.

**4. Line 673 — authored causal reasoning inside a sourced Closer Look.** The quoted large-cluster caveat is verbatim and correct. The explanation preceding it — "the scheduler now has to know what's already running everywhere else in the domain: the answer for node-a depends on the contents of node-b" — is the draft's own. research-manifest **note 8** anticipated this precisely: *"The 🔭 Closer Look on why it is expensive is authored reasoning, not sourced — the docs assert the cost without explaining the mechanism. **Mark it as authored colour or drop the causal explanation and keep the assertion.**"* Neither was done. Recommend the marking option; the explanation is good and is almost certainly right.

**5. Lines 500 vs 504–514 — two mechanisms presented as one.** The block quote states that the node controller "automatically creates taints with a `NoSchedule` effect for node conditions"; the table immediately below lists `not-ready` and `unreachable` at `NoExecute`. Both are individually correct and sourced (and G-7D explicitly blesses taking the effects from the DaemonSet snapshot), but the sources treat them as two separate features — *Taint Nodes by Condition* (`NoSchedule`) and *Taint-based Evictions* (the node controller's `NoExecute` taints). As written, an attentive reader hits an apparent contradiction one line after a Fixed-Point-adjacent quote. One transition sentence resolves it.

**6. Line 516 — leans on a [PARTIAL] description.** "`node.cloudprovider.kubernetes.io/uninitialized`, added when the kubelet starts with an external cloud provider" paraphrases a condensed **[PARTIAL]** list entry. research-manifest **note 12** asks that `[PARTIAL]` blocks be treated as "existence-confirmation only, not as quotable evidence." The draft paraphrases rather than quotes, which is the right instinct — this is the only place in the chapter where a `[PARTIAL]` description carries a factual clause, and it is low-stakes. Noting it for completeness rather than asking for a change.

**7. Lines 734, 736 and 1076 — "binding *is* writing `.spec.nodeName`" is a two-snapshot synthesis.** `k8s-docs-kube-scheduler-2026-08-23` says binding is notifying the API server; `k8s-docs-daemonset-2026-08-24` says the default scheduler "binds the Pod to the target host by setting the `.spec.nodeName` field." Neither states the identity on its own. The draft *shows its work* in the prose at 734, which is why this is a WARN and not a FAIL — but the Chapter Summary at 1076 states it flat ("A notification to the API server — concretely, writing `.spec.nodeName`") with no tag and no visible derivation. Consider carrying both tags into the summary row.

**8. Lines 810 and 1062 — dropped hedge.** Both render `k8s-docs-daemonset-2026-08-24`'s "the default scheduler **typically** takes over" as unhedged ("the ordinary default scheduler then placed it", "the default scheduler takes over and binds the Pod"). Line 732 keeps "typically" correctly. Grading Q15's distractor **C** partly on the unhedged form is the only place it matters, and **C** is wrong on independent grounds, so this is cosmetic — restore "typically" in the two answer keys.

**9. Lines 32, 76, 100 and 115 — unsourced exam-yield claims.** "That is the highest exam-points-per-minute route in the chapter" (32), "it is worth more exam points than it looks" (76), "four separate exam-checkable facts" (100), "saves more exam points than anything else in the chapter" (115). CNCF publishes domain weights only — the book's own front matter says so — so nothing supports per-fact or per-section yield. These read as authorial study guidance rather than vendor claims, and the chapter's weight disclosure covers the adjacent territory, so I have not raised them to FAIL. Flagging the cluster once because it is the pattern a cert-guide audit exists to catch: if the house rule is that exam-behaviour claims must be visibly authorial, these four need the same hedging the weight line gets.

**10. Line 12 — attention budget arithmetic.** "Total time: ~120 minutes" against a table summing to **127** (10+15+8+15+25+8+18+14+8+6). The tilde absorbs some of it. Likely the structural linter's territory rather than mine; noted in case it isn't.

---

## AUTHOR-REVIEW comments adjudicated

The draft embeds five `<!-- AUTHOR-REVIEW -->` comments, one of which explicitly routes to this stage. All five, resolved:

- **Line 235 (RuntimeClass overhead mechanism) — UPHELD, no change.** The prose is correctly held to what `k8s-docs-runtime-class-2026-08-23` supports ("a Pod overhead so the scheduler accounts for the runtime's resource cost") and does not assert that overhead is added to the Pod's effective request. If the revision stage wants the mechanism, `kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/` is the fetch; §2 does not need it.
- **Line 702 (topology spread, outline OQ #2) — CONFIRMED CLOSED.** Matches research-manifest note 2. §5's four-field block is verbatim-accurate against `k8s-docs-topology-spread-constraints-2026-08-24`. The comment can be deleted.
- **Line 762 (Scheduling Policies currency risk) — RESOLVED; DELETE THE COMMENT.** research-manifest **note 1** already ran this down: the live kube-scheduler page was re-fetched and is *character-identical* to the cached snapshot on this passage, and the manifest states outright, *"Remove the 'currency risk' flag from the fact-accuracy stage's queue — I checked it, and there is nothing to reconcile."* I concur, with one observation in the draft's favour: line 748 says "There are two **documented** ways to configure…", which is exactly the precision note 1 asks for (it establishes what the docs say, not what the binary accepts). The prose is safe as written under both readings. **Do not** let the revision stage add a "Policies have been removed" claim — that assertion appears nowhere in the cached corpus and would itself be an untagged factual claim.
- **Lines 1121 and 1123 (ch-02 cross-bearing `§3`; ch-06 section numbering) — out of scope for fact-accuracy, but verified as described.** Book-KCNA ships chapters 01–05 only; `chapter-06-*.md` does not exist, matching research-manifest note 9. That means §4's DaemonSet callback at 526 ("Chapter 6 told you…") and the back-bearings at 622 and 526 point at unshipped text. Sequencing decision for the author; flagged here only because I confirmed it on disk.

---

## PASS — Verified claims (sampled)

Every quotation I spot-checked reproduces its snapshot exactly. A representative sample:

| Line | Claim | Snapshot | Verdict |
|---|---|---|---|
| 96, 187 | Pods scheduled once; never rescheduled; replaced with a new UID; node death → deletion after timeout | `pod-lifecycle-2026-08-23` | Verbatim |
| 123–133 | Watches unbound Pods; feasible nodes; 2-step filter/score; empty list → not yet schedulable; highest ranking; binding = notifying the API server | `kube-scheduler-2026-08-23` | Verbatim |
| 177, 290, 1036 | "If there is more than one node with equal scores, kube-scheduler selects one of these at random" | `kube-scheduler-2026-08-23` | Verbatim |
| 201, 209 | `PodFitsResources` checks requests; kubelet "reserves at least the request amount" | `kube-scheduler-2026-08-23`, `resource-management-2026-08-23` | Verbatim |
| 227 | Both Allocatable quotes + "does not over-subscribe" | `nodes-2026-08-23`, `node-allocatable-2026-08-24` | Verbatim |
| 239 | Preemption stated as the single exception, PriorityClass named and scoped out | `pod-priority-preemption-2026-08-24` | Verbatim; and it follows research-manifest note 5's precision hazard exactly — framed as the exception, §2's `Pending` Fixed Point left intact |
| 333–334, 427–428 | `kubectl get nodes --show-labels`, `kubectl label nodes …`, `kubectl taint nodes …` and the trailing-minus removal form | `assign-pods-nodes-task-2026-08-24`, `taints-tolerations-depth-2026-08-24` | Verbatim, character-exact |
| 339 | NodeRestriction / `node-restriction.kubernetes.io/` prefix | `assign-pod-node-2026-08-23` | Verbatim |
| 343, 351, 353, 357–358, 368 | `nodeSelector` "each of the labels"; affinity more expressive; six operators; both DuringScheduling forms; `IgnoredDuringExecution` | `assign-pod-node-2026-08-23` | Verbatim |
| 360 | `weight` 1–100; sum added to other scoring functions; highest total prioritised | `assign-pod-node-depth-2026-08-24` | Verbatim |
| 364 | `nodeSelectorTerms` ORed / `matchExpressions` ANDed | `assign-pod-node-depth-2026-08-24` | Verbatim — closes outline OQ #6 |
| 418, 420, 435, 445–449, 485 | Taint/toleration inversion; "allow but don't guarantee"; all three effects; all four matching rules | `taints-tolerations-2026-08-23` | Verbatim; the matching table at 487–492 is a faithful restatement with no invented rows |
| 439, 494, 500, 520 | Dedicated-nodes prescription (elision accurate); multiple-taint procedure; taints-not-conditions; `tolerationSeconds=300` | `taints-tolerations-depth-2026-08-24` | Verbatim; 520's "five-minute grace period" correctly renders 300s |
| 633, 641, 679–700 | Required/preferred anti-affinity semantics; `topologyKey`; `maxSkew`, `labelSelector`, `whenUnsatisfiable`, `minDomains`; cluster defaults; scale-down limitation | `topology-spread-constraints-2026-08-24` | Verbatim; **no skew formula composed** — G-7A honoured |
| 673 | Large-cluster cost caveat | `assign-pod-node-depth-2026-08-24` | Verbatim (see WARN 4 for the surrounding explanation) |
| 714–726 | `nodeName` bypasses; overrules; all three failure caveats; "unusual and is only done in special cases" | `assign-pod-node-2026-08-23`, `…-depth-2026-08-24`, `kube-scheduler-2026-08-23` | Verbatim |
| 732, 742 | DaemonSet sets `nodeAffinity`; default scheduler "typically takes over" and binds via `.spec.nodeName`; `schedulerName` | `daemonset-2026-08-24` | Verbatim |
| 748–751 | Policies (Predicates/Priorities) and Profiles, with the six named plugin stages | `kube-scheduler-2026-08-23` | Verbatim; see adjudication above |

Arithmetic in worked examples was checked independently and is correct throughout: §2's 16 GiB / 4×4 GiB example (213–217, 297–298), Practice Q3's 32 − 24 = 8 < 12 (925, 1038), and Q14's 12 nodes → 12 domains vs 2 zones → 2 domains leaving four of six replicas `Pending` (1002, 1060). Stated question counts also check out: eight Soundings items with three retrieval questions, three Bearings sets of five, and seventeen practice questions with four retrieval tags (Q5/ch5, Q6/ch3, Q12/ch4, Q15/ch6).