# Fact-Accuracy Audit — Chapter 8

**Mode detected: STANDARD.** The `Cached sources` section carries 18 populated snapshots, and the draft carries ~68 inline `[source:` tags. Untagged factual claims are therefore FAIL, not advisory.

**Input note.** `draft-v2.md` was unavailable; this audit was run against `draft-v1.md` and all line numbers below are that file's.

**Tag-integrity note.** Every one of the 17 distinct snapshot names cited by the draft resolves to a snapshot present in the corpus. There are zero dangling tags. `k8s-keps-and-feature-stages-2026-08-23` is the only cached snapshot the chapter never cites (see WARN-19).

---

## Summary

- Total factual claims inspected: **129**
- Tagged claims verified: **68**
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0**
- **Untagged factual claims (FAIL): 59** — across 7 clusters and 7 singletons
- **Contradicted claims (FAIL): 2**
- Minor discrepancies (WARN): **19** (overlapping the above pools)

Seven `AUTHOR-REVIEW` comments are already in the draft (lines 8, 281, 291, 313, 499, 712, and the §2 block at 224). This audit confirms all of them and finds **five further FAIL clusters the author did not flag**: the managed/self-hosted duty split (C), the cordon→spec→taint mechanism chain (D), the control-plane-loss survivability claim (E), the `NoSchedule` semantics gap (F), and an answer-key leak past the author's own §3 scope guard (B-4).

---

## FAIL — Untagged factual claims

### Cluster A — Sequential-gate semantics: order, position, and mutation (19 instances)

Author-flagged at line 224. **Confirmed and unchanged.**

No cached snapshot states (i) that a request traverses authentication → authorization → admission *in that order*, (ii) that admission runs *after* authorization and *before* persistence, or (iii) that admission can *modify* a request. The two tagged sentences at lines 222–224 establish only the three *names* and their order *in a documentation table of contents* — which is a claim about a web page's link list, not about a request pipeline.

Primary instances:

#### Line 242: "Admission controllers see a request that has already been authenticated and authorized, and act on it before it is written down."
#### Line 244: "Admission may answer yes, no, or *yes — but not as you wrote it*."
#### Line 246 (Fixed Point): "Authentication, then authorization, then admission... it is the only one of the three that can change your request instead of refusing it."
#### Line 232 (gate-two definition): "Authorization decides whether the identity established at gate one is permitted to perform *this action* on *this object*."
#### Line 263 (Navigational Hazards): "Authorization has no opinion about the contents of your request; admission has no opinion about your identity."

**Why they're factual claims:** each asserts a specific mechanism and ordering in the Kubernetes API server's request path — vendor behaviour, not analogy.

Downstream instances inheriting the same gap: **Figure 8.2 (lines 248–260)**, the "who, may, and how" mnemonic, **line 279** ("it takes effect at this gate"), **line 362**, Bearings #1 Q3/A3 (**line 389**), Bearings #1 Q4/A4, Exam Alert items 1 and 2 (**line 862ff**), Common Traps row (**line 884**), **PQ2 options C/D (lines 908–909)** and its explanation (**line 1024**), PQ3, PQ4, and Chapter Summary rows (**lines 1080–1081**).

**Fix:** fetch `kubernetes.io/docs/concepts/security/controlling-access/` — it closes (i), (ii) and (iii) outright. Secondary: `.../reference/access-authn-authz/admission-controllers/` for the mutating/validating split. Until then, do not ship the ordering or mutation claims untagged; §2's Fixed Point, Figure 8.2, and PQ2's key are all unsupportable without it.

---

### Cluster B — ResourceQuota / LimitRange mechanics (14 instances)

Author-flagged at line 313 as a **BLOCKING GAP**. **Confirmed, and one instance escaped the author's own scope guard.**

The corpus supports exactly two sentences: quota is the mechanism by which namespaces divide cluster resources between users [`k8s-docs-namespaces-2026-08-23`], and the one functional-contrast sentence [`k8s-docs-cloud-native-security-2026-08-23`]. Everything about *scope*, *defaulting*, and *what a quota counts* is unsourced.

#### Line 309: "A quota is a ceiling on a **namespace, in aggregate**: the team's total, not any one Pod's numbers."
#### Line 311: "A LimitRange... is a constraint on **individual objects**, and a mechanism that has to be able to act on a manifest that says nothing at all."
#### Line 321: "The quota may refuse it. The LimitRange may fill it in."
#### Line 325 (Fixed Point): "**ResourceQuota counts the namespace. LimitRange constrains the object.**"
#### Figure 8.3 (lines 327–346): renders `min ≤ … ≤ max` per Pod, and "defaults FILLED IN."

The author's note at line 313 states LimitRange's min/max/default structure is **NOT cached and therefore NOT asserted below**. Figure 8.3 asserts it anyway. The figure is draft content and must be held to the same guard as the prose.

#### **B-4 — Line 1036 (PQ6 explanation): "**A is wrong** as a claim about quota's capabilities..."

**Why it's a factual claim:** distractor A reads "ResourceQuota cannot count objects, only compute resources." Calling A wrong is an affirmative assertion that a ResourceQuota *can* count objects — which is precisely the item line 313 lists as not cached. The body was guarded; the answer key was not. **This is the leak worth fixing first**, because an answer key that asserts an unsourced capability is harder to catch on a later pass than body prose is.

#### Line 354: "ResourceQuota and LimitRange are namespaced objects." (repeated in PQ5's explanation D)
#### Line 362: "both of these mechanisms take effect at the admission gate."

Further instances: line 348 (see WARN-1 — this one is also internally inconsistent), the §3 Snag box, Bearings #1 Q5/A5, Exam Alert item 8, two Common Traps rows, PQ5, PQ7, and Chapter Summary rows at **lines 1083–1084**.

**Fix:** fetch `kubernetes.io/docs/concepts/policy/resource-quotas/` and `.../limit-ranges/`, per the author's own scope guard at line 313. Then re-check Figure 8.3 and PQ6's explanation against what actually comes back.

---

### Cluster C — The managed vs. self-hosted duty split (6 instances) — NOT author-flagged

#### Line 543: "A managed control plane means the provider decides when you upgrade, and the provider holds the etcd backup. A self-hosted control plane means both are yours."

**Why it's a factual claim:** it asserts what third-party managed Kubernetes services do and do not do on a customer's behalf. That is vendor-behaviour, not architecture.

**What the corpus actually supports:** `k8s-docs-setup-tooling-2026-08-23` says only "consider which aspects of operating a Kubernetes cluster (or abstractions) you want to manage yourself and which you prefer to hand off to a provider." That licenses the *existence* of a split. It does not license naming upgrade timing and etcd custody as the two items on the managed side of it.

Other instances: **line 84** (Soundings A8's five-duty list: "patching and upgrades; backups; hardware replacement; capacity planning; certificate rotation"), **line 732** ("on a managed control plane you may not be able to reach etcd at all"), Bearings #2 Q5/A5, **PQ13** and its answer key.

This cluster is load-bearing: PQ13's correct answer B is entirely dependent on it, and §5's closing move ("§6 is which versions are allowed to disagree. §7 is what you cannot get back. Those are the two duties that move") is the chapter's own structural hinge into its two densest sections.

**Fix:** no cached snapshot will close this — kubernetes.io does not document commercial providers' responsibility models. Open a research gap for a vendor-neutral shared-responsibility source, or narrow the claim to what `setup-tooling` licenses ("some operational aspects move to the provider; which ones is a per-provider question") and rewrite PQ13 so its key does not turn on the specific two.

---

### Cluster D — The cordon → `spec` field → built-in taint mechanism (4 instances) — NOT author-flagged

#### Line 814: "It writes a field on a Node object through the API server, and Chapter 7's built-in taint machinery — the `node.kubernetes.io/unschedulable` taint... — was already watching for exactly that."
#### Line 1048 (PQ10 key): "`cordon` marks the node unschedulable, a statement of desired state, which lives in `spec`." / "the mechanism is a taint and an unschedulable marker, not a label."

**Why they're factual claims:** they assert an implementation path — which field cordon writes, and that the built-in `unschedulable` taint is the downstream consequence of that write.

**What the corpus supports, and where it stops.** Three separate facts are cached: cordon prevents scheduling new Pods [`k8s-docs-nodes-2026-08-23`]; `node.kubernetes.io/unschedulable:NoSchedule` exists as a built-in taint [`k8s-docs-daemonset-2026-08-24`, `k8s-docs-taints-tolerations-depth-2026-08-24`]; the scheduler checks taints [`taints-tolerations-depth`]. **No cached sentence connects the first to the second.** The word `spec` appears in no cached snapshot in connection with node unschedulability, and `taints-tolerations-depth` attributes automatic taint creation to *node conditions*, which unschedulability is not.

This is the chapter's Zenith claim (line 820) and PQ10's entire answer. It is the one place where a genuinely elegant synthesis is resting on an unsourced causal link.

**Fix:** fetch `kubernetes.io/docs/reference/generated/kubernetes-api/v1.36/#nodespec-v1-core` (for `.spec.unschedulable`) or `.../docs/concepts/architecture/nodes/#manual-node-administration` at greater depth. If neither closes the taint link, narrow line 814 to what is cached: cordon is a write through the API server that the scheduler subsequently observes — and drop the assertion that the built-in taint is the specific mechanism.

Related: **line 428** ("Note what a kubelet does when it joins a cluster: it writes an object through the API server") — the snapshot says the kubelet "self-registers to the control plane"; "writes an object" is an inference. Lower stakes, same fix family.

---

### Cluster E — Workloads survive control-plane loss (3 instances) — NOT author-flagged

#### Line 704: "Losing every control-plane node does not stop your worker nodes. The kubelets keep running the containers they were last told to run; traffic keeps being served."
#### Line 771 (Bearings #3 A4): "Not the running workloads: kubelets keep running what they were last told to run, and traffic keeps flowing."

**Why it's a factual claim:** it asserts specific failure-mode behaviour of the kubelet under total control-plane loss.

**What the corpus says:** `k8s-docs-etcd-backup-2026-08-23` names the disaster scenario ("such as losing all control plane nodes") and nothing about what survives it. No cached snapshot describes kubelet behaviour when the API server is unreachable.

This is not a throwaway — Bearings #3 Q4 is *constructed* around it ("The scenario is constructed so you have to notice that 'running workloads' and 'cluster state' are different things"), so the pedagogy fails if the claim is wrong.

**Fix:** open a research gap. `kubernetes.io/docs/concepts/architecture/#kubelet` or the node-shutdown/static-pod material are the likely closers. Do not ship the Bearings #3 Q4 construction untagged.

---

### Cluster F — `NoSchedule` semantics (4 instances) — snapshot exists but is not in this chapter's set

#### Line 78 (Soundings A5): "`NoSchedule` governs new placements only. Pods already running on the node keep running."
#### Line 572 (Bearings #2 A1): "`NoSchedule` governs new placements only, so Pods already on the node keep running."

**Why it's unverifiable here:** `k8s-docs-taints-tolerations-depth-2026-08-24`'s own header states that the core snapshot — `k8s-docs-taints-tolerations-2026-08-23` — "holds the core concept, **the three effects** and the four matching rules." That snapshot is **not among this chapter's 18**. The depth cut deliberately does not restate effect semantics. So the corpus available to this chapter contains the *string* `NoSchedule` in two taint tables and nowhere defines what it does.

Also affected: Bearings #2 Q1 (which instructs the reader to apply "Chapter 7's rule about what `NoSchedule` governs"), and line 814's "you met in a table with a `NoSchedule` effect."

**Fix:** this one needs no fetch. Add `k8s-docs-taints-tolerations-2026-08-23` to this chapter's referenced-snapshot set and tag lines 78 and 572 against it. The corpus note is explicit that a claim needing an unlisted snapshot must be named as a gap rather than cited blind — so the reference list, not the prose, is what is wrong.

---

### Cluster G — CNCF domain weight (2 instances)

Author-flagged at line 8. **Confirmed.**

#### Line 4: "**Domain: Kubernetes Fundamentals — 44% of the exam**"
#### Line 6: "The 44% is CNCF's published domain weight... CNCF publishes weights for its **four** domains and not for the competencies within them."

**Why they're factual claims:** both assert what a certifying body publishes about its own exam blueprint — the single most consequential category of claim in a study guide.

**What the corpus says:** nothing. No KCNA curriculum snapshot is cached. Worse, the corpus's own frontmatter is not corroborating: `objectives_covered` fields across the 18 snapshots reference `D1`, `D2` and `D4` — consistent with *at least* four domains, but establishing no total — and **the string "Kubernetes Fundamentals" appears in no cached snapshot at all**. The domain the chapter names as its own is unattested in this corpus.

**Fix:** restore the two inline CNCF tags from the book-level curriculum snapshot, as line 8 instructs. Verify the domain *name* and the domain *count* at the same time, not just the percentage — all three are unattested here.

---

### Singleton untagged claims (7)

#### Line 133: "Four slots, and only the first is mandatory"
**Why it's a factual claim:** asserts which `kubectl` argument slots are optional. The snapshot establishes NAME optional ("if the name is omitted, details for all resources are displayed") and flags optional ("optional flags"). **It says nothing about TYPE being optional.**
**Fix:** either tag it, or narrow to "NAME and flags are optional" — which is fully sourced and costs nothing.

#### Line 186: "`kubectl explain`... works on resource types you have never seen, including Custom Resource Definitions"
**Why it's a factual claim:** vendor feature availability. The snapshot says only "explain — Get documentation of various resources (pods, nodes, services, etc.)." CRDs are named in `k8s-docs-extending-kubernetes-2026-08-23`, but nothing connects `explain` to them.
**Fix:** tag against a kubectl-explain reference, or drop the CRD clause.

#### Line 529: "kind... makes it the usual choice inside CI pipelines. minikube runs a local cluster with a broader set of conveniences... the usual choice when a human is sitting in front of it."
**Why it's a factual claim:** asserts ecosystem-tool suitability and prevailing practice. Only "kind runs its nodes as containers" is sourced (`setup-tooling`: "using Docker containers as nodes"). Everything after it is unattested.
**Fix:** open a research gap, or reframe as the author's operational judgement rather than as documented fact.

#### Line 535: "`kubeadm`... will not put a container runtime on those nodes"
**Why it's a factual claim:** a negative assertion about a tool's scope. `setup-tooling` says a runtime "must be installed on every node" — which implies the requirement, not that kubeadm declines to satisfy it. Repeated at Bearings #2 A4 and PQ12's explanation D.
**Fix:** narrow to the sourced form ("a runtime must already be present on every node"), which carries the same pedagogical weight without the unsourced negative.

#### Line 541: "scheduler profile configuration lives in the control plane's own component configuration, which is a thing you can reach only if you own the control plane"
**Why it's a factual claim:** asserts both where scheduler config lives and what a managed platform withholds. `extending-kubernetes` names "scheduler plugins/profiles" and stops there.
**Fix:** cut, or fetch `.../docs/reference/scheduling/config/`.

#### Line 1045 (PQ9 explanation B): "`NotReady` is a display convention in summary output, not one of the condition's three values"
**Why it's a factual claim:** asserts specific `kubectl` output formatting. The three condition values are sourced; the claim about what summary output *displays* is not. Also at Bearings #2 A3.
**Fix:** the second half is sourced and sufficient. Drop "is a display convention in summary output" or tag it.

#### Line 236: "RBAC is one authorizer among several"
**Why it's a factual claim:** asserts the existence of multiple authorization modes. `extending-kubernetes` lists RBAC only as an example API resource ("such as ResourceQuota, NetworkPolicy and RBAC").
**Fix:** closed by the same `controlling-access/` fetch as Cluster A.

---

## FAIL — Contradicted claims

### Line 497: "Capacity is the machine's total; Allocatable is what is left for your workloads after the node's own overheads are set aside."

**Tag:** untagged, but sits mid-paragraph between two `[source: k8s-docs-node-allocatable-2026-08-24]` sentences, which will read to a reviewer as covered by them.

**Snapshot says** (`k8s-docs-node-allocatable-2026-08-24`, NOT IN THIS SNAPSHOT block):
> "the formula or diagram relating node Capacity to `kube-reserved`, `system-reserved`, `eviction-threshold` and Allocatable. The source presents this as an image (`node-capacity.svg`) with no text equivalent, so no equation is extractable. **§2 must not state an arithmetic relationship between capacity and allocatable.**"

**Draft says:** "Capacity is the machine's total; Allocatable is what is left... after the node's own overheads are set aside."

**Why this is a contradiction and not merely an untagged claim:** "what is left after X is set aside" *is* an arithmetic relationship — subtraction, stated in words. The snapshot does not merely fail to support the sentence; it carries an explicit instruction not to write it. The snapshot also never defines Capacity at all, so "Capacity is the machine's total" is an independent unsourced definition.

The author's note at line 499 identifies the following sentence ("The two differ because...") but reads the quoted sentence as compliant with option (b). It is not — option (b) was to name what the reservation is *for* without the arithmetic, and "what is left after overheads are set aside" supplies the arithmetic.

**Recommended fix:** cut both sentences back to the two verbatim-sourced ones at line 497, plus at most a bare statement that the two numbers differ. Keep line 501's Fixed Point ("Allocatable is the number the scheduler does arithmetic against") — it is fully supported by "The scheduler treats 'Allocatable' as the available `capacity` for pods" and "does not over-subscribe." If the Chapter 7 promise is to be paid properly, fetch `kubernetes.io/docs/tasks/administer-cluster/reserve-compute-resources/` at depth; otherwise adjust Chapter 7's pointer, per line 499.

---

### Line 147 (Figure 8.1): `kubectl   cordon           node          node-7`

**Tag:** figure is untagged; the cordon command form is sourced twice in prose (lines 210, 432) from `k8s-docs-nodes-2026-08-23`.

**Snapshot says** (`k8s-docs-nodes-2026-08-23`):
> "marking a node as unschedulable (`kubectl cordon $NODENAME`)"

— one positional argument.

**Draft says:** Figure 8.1 aligns `cordon` across the TYPE column (`node`) *and* the NAME column (`node-7`), which renders as `kubectl cordon node node-7` — two positional arguments.

**And the draft contradicts itself.** Line 1042 (PQ8's explanation) states the opposite outright:
> "Note the grammar: `cordon` and `drain` take the node's name directly, **without a preceding TYPE**, because the verb already implies the resource type."

PQ8's correct answer B is `kubectl cordon worker-3`; its distractor A opens `kubectl drain node worker-3` and is marked wrong *for ordering only*, leaving the extra TYPE token silently endorsed. A reader who works Figure 8.1 and then works PQ8 gets two incompatible grammars for the same command, and the figure's version is the one the cached source does not use.

**Recommended fix:** move `cordon` in Figure 8.1 to the NAME column with TYPE empty — which also strengthens the figure's stated point ("What to notice is the empty columns"). Then fix **line 210**, which glosses the two-token `kubectl cordon node-7` as "Verb, resource type, name" — three slot names for two tokens. It should read "Verb, name." Optionally add a half-sentence to PQ8's distractor A explanation noting the TYPE token as a second defect.

---

## WARN — Minor discrepancies

1. **Line 348 — internal inconsistency, not just untagged.** "A quota with no LimitRange means a single team member who omits resource requests can, with one Pod, consume the namespace's entire allocation." This sits in direct tension with **line 321** ("The quota may refuse it," of a manifest that says nothing about resources). If the quota refuses request-less manifests, the scenario at line 348 cannot occur. Whichever way the Cluster-B fetch resolves, one of these two sentences will need rewriting — flag them as a pair.

2. **Line 618 — "That single sentence generates four of the five rows below."** The generating rule is "nothing may be newer than the API server." It generates the kubelet row, the kube-proxy row, and the controller-manager/scheduler/CCM row — three. It does **not** generate the kube-apiserver HA row, which is a *mutual* bound ("newest and oldest... must be within one minor version"), symmetric in both directions and describing apiservers relative to each other rather than to an apiserver. Repeated at **line 744** (Bearings #3 Q2) and in that item's answer, which explicitly lists "the constraint on HA API servers relative to one another" among the generated rows. **Fix:** "three of the five," with the HA row and `kubectl` both treated as outside the derivation — or reword the rule to cover it. The table itself is verified correct; only the derivation claim overreaches.

3. **Line 630 — "roughly a year of coverage, which is *exactly* the patch-support figure."** Three releases a year at ~15-week intervals across three branches is ~45 weeks ≈ 10.4 months. The source says "approximately 1 year." "Exactly" overstates a derivation the numbers support only loosely. Same at **line 767** ("about twelve months of coverage"). Soften to "close to."

4. **Line 674 — "`kubectl` is a user tool that lives outside the cluster."** In tension with §1's own "surprising case" (**lines 198–204**), which establishes that `kubectl` frequently runs *inside* a Pod. The skew rationale is sound; the phrasing collides with material 480 lines earlier that the chapter treated as notable.

5. **Line 222 — the securing-a-cluster list is presented as a contiguous five.** The snapshot's list is "Generate Certificates; Kubernetes Container Environment; Controlling Access to the Kubernetes API; Authenticating; Authorization; Using Admission Controllers; Admission Webhook Good Practices; Using Sysctls...; Auditing." Relative order is preserved ✓, but "lists them in this order" implies adjacency, and two items sit between "Using Admission Controllers" and "Auditing." Low risk; a "among other entries" would fix it.

6. **Lines 155, 160 — "`pod`, `pods` and `po` are the same thing."** The rule (singular/plural/abbreviated, case-insensitive) is verbatim-sourced. The specific abbreviation `po` is not in any cached snapshot. Illustrative instantiation of a sourced rule; near-certain, but unattested.

7. **Line 184 — "the only verb in the table that answers a question about *the API* rather than a question about *your cluster*."** `config` ("Modifies kubeconfig files") also answers a question about neither the API nor your cluster. "Only" is one counterexample too strong.

8. **Lines 194, 1078 — kubeconfig precedence is derived, not stated.** The snapshot gives a *general* rule ("flags... override default values and any corresponding environment variables"), not a kubeconfig-specific precedence. Line 194 is honest about this ("Per the general rule above"). **Line 1078's summary row drops the hedge** and states "the flag wins" flat. Keep the signposting in the summary or restore it.

9. **Line 204 — "`kubectl` inside a Pod does not use your kubeconfig."** The snapshot says in-cluster authentication *is assumed* when the three conditions are found; it does not say kubeconfig is ignored. Also "does not default to the `default` namespace" — sourced as "acts against the namespace of the ServiceAccount," which may itself be `default`. Both overreach slightly past a verbatim-verified sentence.

10. **§2, gate one — "That injected token is the same file `kubectl` looks for in §1."** Two snapshots are being fused: `kubectl-overview` names the path `/var/run/secrets/kubernetes.io/serviceaccount/token`; `control-plane-node-communication` says a bearer token is injected. Neither states they are the same artefact. Near-certain, unattested.

11. **Line 477 — "Four of those are two-valued."** The snapshot describes each condition with "True if..."; it does not assert that DiskPressure, MemoryPressure, PIDPressure and NetworkUnavailable are restricted to two values. The framing device is doing real work here (it sets up `Ready`'s three-valuedness), so it is worth either sourcing or softening to "Four of those you will meet as True or False."

12. **Line 491 — "The node controller is a control loop."** Untagged, but `k8s-docs-extending-kubernetes-2026-08-23` defines the pattern outright ("Controllers — client programs that read and/or write to the Kubernetes API, following a control loop: read an object's .spec, possibly do things, and then update the object's .status"). Free tag; take it. Same applies to **PQ11's key (line 1051)** and to PQ10's "Chapter 4's rule" about `spec` vs `status`, which that same sentence supports.

13. **CRI is never tagged anywhere in the chapter.** Lines 535, Bearings #2 A4 and PQ12's explanation all invoke "the CRI, the Container Runtime Interface." `k8s-docs-extending-kubernetes-2026-08-23` defines it verbatim ("Container runtime (CRI, the Container Runtime Interface, to support alternative container runtimes)"). Another free tag.

14. **Line 549 — "Three modest machines will run one [control plane]."** Unattested operational sizing claim. Low stakes inside a Logbook Entry, but it is a number a reader may carry.

15. **Line 1039 (PQ7 key) — "requests are the number the scheduler filters on."** Attributed to Chapter 5. `k8s-docs-node-allocatable-2026-08-24`'s frontmatter lists `requests-as-scheduling-input` and `podfitsresources` under `concepts_covered`, but **no transcribed sentence in the snapshot states it**. Unverifiable in this chapter's corpus even though the topic is nominally covered. Same for the explanation's closing clause ("**D is wrong** on which of requests and limits the scheduler reads").

16. **Line 1051 (PQ11 distractor D) — "etcd compaction is storage maintenance, not reconciliation."** etcd compaction appears in no cached snapshot. It is only a distractor rebuttal, but it asserts a fact.

17. **Line 1066 (PQ16 distractor D) — "neither utility encrypts snapshots for you."** An unsourced negative. The snapshot's "keep it encrypted" implies the responsibility is the operator's, which is adjacent but not the same claim.

18. **Line 862 — "High-priority topics, in descending order of confidence."** No cached snapshot establishes exam topic weighting. The hedge ("confidence," not "weight") makes this defensible as authored judgement, but it is worth a deliberate decision rather than an accident — and it shares a root cause with Cluster G.

19. **Line 1126 — "Every Pod gets an address."** Forward reference to Chapter 9; unsourced in this chapter's corpus. Also "a controller may replace one at any moment, and the replacement is a different Pod." Both are teaser prose, low risk, but they are factual assertions in a chapter with no networking snapshots cached.

**Noticed, outside this stage's scope (flagged for whoever owns them, not counted above):**
- The verb table's "Where you met it" column attributes `logs` and `exec` to **Ch 13** — a forward reference in a column whose header promises a backward one. Structural/cross-bearing integrity, not fact accuracy.
- **Line 480** — "because the cached documentation names the parameter without stating a value" is reader-facing prose that leaks the pipeline's internal vocabulary. Voice stage.
- `k8s-keps-and-feature-stages-2026-08-23` is cached but uncited. §6's two Chapter 17 pointers (SIG Release, the KEP process) could be tagged against it at no cost.

---

## PASS — Verified claims

All 68 tagged claim instances were checked against their named snapshot. Sampled evidence of coverage, by section:

**§1 (14 tagged, all verified).** The four-slot grammar and all four slot definitions match `k8s-docs-kubectl-overview-2026-08-23` near-verbatim, including "if the name is omitted, details for all resources are displayed" and the flags-override-environment-variables rule. **The full 12-row verb table was checked row by row against the snapshot's Operations list — all 12 descriptions match**, with one trivial compression (the `delete` row drops "resource selectors"). The kubeconfig location, the three in-cluster detection conditions, and the ServiceAccount-namespace default are all verbatim. Line 210's cordon description matches `k8s-docs-nodes-2026-08-23`.

**§2 (14 tagged, all verified).** The HTTPS/443 client-authentication sentence, the node client-certificate provisioning guidance, kubelet TLS bootstrapping, the Pod ServiceAccount injection, and the hub-and-spoke paragraph at line 296 all match `k8s-docs-control-plane-node-communication-2026-08-24` word for word. NodeRestriction matches `k8s-docs-assign-pod-node-2026-08-23`; Pod Security Admission matches `k8s-docs-pod-security-standards-2026-08-23`; the webhook "potential point of failure" candour matches `k8s-docs-extending-kubernetes-2026-08-23`.

**§4 (15 tagged, all verified).** Both node-registration paths, the Node-object validity check, the DNS-subdomain naming rule, the cordon/drain/uncordon triad, the DaemonSet unschedulable toleration (cross-verified against *both* `k8s-docs-nodes-2026-08-23` and the seven-row table in `k8s-docs-daemonset-2026-08-24`), the Node status contents, **all five node conditions and all three `Ready` values**, both heartbeat forms, and all three node-controller jobs. The Allocatable definition and the scheduler's non-oversubscription are verbatim `[VERBATIM]` passages from `k8s-docs-node-allocatable-2026-08-24`.

**§5 (6 tagged, all verified).** All five planning questions, minikube and kind, kubeadm's "officially supported" status and its two jobs, k3s as a lightweight distribution, and the containerd/CRI-O node requirement — all match `k8s-docs-setup-tooling-2026-08-23` and `k8s-docs-cluster-administration-2026-08-23`.

**§6 (7 tagged, all verified — checked with extra care as the chapter's highest-stakes block).** Semantic-versioning terminology ✓. Three release branches ✓. ~1 year patch support for 1.19+, ~9 months for 1.18 and older ✓. Backport policy ✓. Three releases per year, ~15 weeks, SIG Release, monthly patches ✓. Current roster 1.36/1.35/1.34 ✓.

**All five skew-table rows verified against `k8s-version-skew-policy-2026-08-23`, including both worked examples.** The kubelet row's parenthetical ("A kubelet older than 1.25 may only be up to two minor versions older") correctly renders the snapshot's "kubelet < 1.25." **Figure 8.5's bar positions were checked against the table independently**: kubelet −3→0 ✓, kube-proxy −3→0 ✓, controller-manager/scheduler/cloud-controller-manager −1→0 ✓, kubectl −1→+1 ✓. **All four answers in Bearings #3 Q1 and all four options in PQ14 were re-derived from the snapshot and are correct** — including PQ14's key (kube-proxy at 1.37 against a 1.36 API server is unsupported) and PQ15's B rebuttal (kube-proxy is older-only relative to the API server).

**§7 (8 tagged, all verified).** The etcd definition and the root-permission-equivalence sentence match `k8s-docs-etcd-access-control-2026-08-24` verbatim. "All Kubernetes objects are stored in etcd," the losing-all-control-plane-nodes scenario, both backup methods, the four TLS flags, the `etcdutl snapshot restore` mechanics, and the encrypt/store-outside instruction all match `k8s-docs-etcd-backup-2026-08-23` verbatim. §7's handling is the strongest in the chapter — line 712's decision not to expand into etcd TLS configuration correctly respects the access-control snapshot's own verification caveat.

**§8 (1 tagged, verified).** "It checks taints when it makes scheduling decisions" matches `k8s-docs-taints-tolerations-depth-2026-08-24`'s `[VERBATIM]` "The scheduler checks taints, not node conditions, when it makes scheduling decisions."