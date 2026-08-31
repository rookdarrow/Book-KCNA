# Curriculum-Alignment Audit — KCNA Chapter 13

**Chapter:** 13 — *When the Cluster Won't Answer*
**Draft audited:** `draft-v1.md` (line references are against that file)
**Authority:** `cncf-kcna-curriculum-pdf-2026-08-23.md` (CNCF, `cncf/curriculum`)
**Audit date:** 2026-08-31

---

## Authority note — read before the tables

CNCF publishes **four domains with weights and a list of competency names per domain**. It publishes **no sub-competency weights and no numbered objective IDs**. The `D<n>.<m>` notation used throughout this book is an *authored* index derived from the published competency ordering:

> 28% – Container Orchestration: Networking; Security; **Troubleshooting**; Storage

giving D2.1 Networking, D2.2 Security, **D2.3 Troubleshooting**, D2.4 Storage.

Two consequences govern every judgement below:

1. **The only CNCF-authoritative weight touching this chapter is 28%, for the whole Container Orchestration domain.** Any per-competency figure (7% pro rata, the outline's authored 4%) is an inference, not data. Depth findings are stated against the competency, with the inference named each time.
2. **The granular D2.3 item list — `kubectl exec`, `kubectl debug`, `kubectl port-forward`, probe failure signatures, node lease heartbeats, and so on — is B1's authored expansion, not CNCF text.** Coverage gaps against that list are book-architecture findings, not exam-blueprint failures.

The draft's in-chapter metadata line handles this correctly: it states the published 28% with its source tag and carries the authored-allocation disclaimer. **No change needed there.**

---

## Objectives the outline claims to cover

The outline claims exactly one objective, `D2.3`, across all eight sections. Rows below decompose it into the concept clusters the outline's `kb_tags` commit to.

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| **D2 (published)** | Container Orchestration — 28% | YES (this chapter takes the Troubleshooting competency) | appropriate |
| **D2.3 (authored)** | Troubleshooting | YES | deep — see depth table |
| D2.3 · platform-scope-vs-application-scope | Two-audience split | YES — §1 | appropriate, **but the boundary rule is under-inclusive** (see Fix 1) |
| D2.3 · triage-flow | Scope → phase → conditions → events → logs | YES — §1, fig03 | appropriate |
| D2.3 · pending-diagnosis | Pod stuck in `Pending` | YES — §2 | appropriate |
| D2.3 · errimagepull / imagepullbackoff-diagnosis | Pull-failure family | YES — §2 | appropriate |
| D2.3 · createcontainerconfigerror | Unresolvable ConfigMap/Secret | YES — §2 | appropriate |
| D2.3 · imageinspecterror | Image inspection failure | **table row only** | **shallow** — named in the `Waiting` table and in the fig02 leaf label, never explained in prose. Its sibling `ErrImageNeverPull` gets a full paragraph. |
| D2.3 · admission-rejection-versus-pod-failure | No Pod object at all | YES — §2 | appropriate |
| D2.3 · kubernetes-events / event-retention-window | Events as a first-class surface | YES — §3 | appropriate (retention written as shape, not figure — correct, see Gaps) |
| D2.3 · crashloopbackoff / restart-backoff-curve | Restart throttling | YES — §4 | deep, justified |
| D2.3 · oomkilled-signature / evicted / node-pressure-eviction | The confusion pair | YES — §4, fig05 | deep, justified |
| D2.3 · eviction-order-by-qos-class | BestEffort → Burstable → Guaranteed | YES — §4 | appropriate (retrieval framing) |
| D2.3 · probe-failure-signatures | Liveness loop vs silent readiness drop | YES — §4 | appropriate |
| D2.3 · node-conditions-as-diagnostic / kubelet-health | Condition → next move | YES — §5 | appropriate; correctly does **not** restate Ch 8's table |
| D2.3 · node-lease-heartbeat / node-death-handling | Heartbeats, the 5-minute wait | YES — §5 | appropriate |
| D2.3 · crictl | The layer argument | YES — §5, fig06 | appropriate — matches the outline's ruled depth |
| D2.3 · version-skew-symptoms / release-known-issues | Skew as applied diagnosis | YES — §6 | appropriate; correctly does **not** restate Ch 8's table |
| D2.3 · resource-metrics-pipeline / metrics-server / kubectl-top | Numbers nobody collects | YES — §7, fig04 | appropriate |
| D2.3 · cluster-log-architecture | Where logs live; not an archive | YES — §7 | appropriate; Ch 18 §6 gloss held to one clause as ledgered |
| **D2.3 · `crictl pods`** (kb_tags `crictl-pods`) | — | **NO** | — |
| **D2.3 · `crictl inspect`** (kb_tags `crictl-inspect`) | — | **NO** | — |
| D2.3 · `kubectl get pod -o wide` | — | partial | figure-only (fig03) and once for nodes in §6; never in prose |
| **D2.3 · `kubectl exec` / `kubectl debug` / `kubectl port-forward`** | Getting inside a running container | **deferred** — §1 names all three with pointers to Ch 16 §3/§5 | deferral is explicit and correct at chapter level; **book-level tagging risk, see Fix 2** |
| **D2.3 · Service / EndpointSlice debugging** | `kubectl get endpointslices -l ...`, selector-vs-label mismatch | **deferred** — §4 pointer to Ch 16 §4 | same book-level tagging risk as above |

**The two `crictl` rows are a `kb_tags` defect, not a draft defect.** The outline's own §5 depth ruling says "show `crictl ps` and `crictl logs`," and the draft does exactly that. `kb_tags.commands` over-lists relative to the ruling it sits beside.

---

## Objectives covered in the draft but NOT in the outline

Flagged for author decision. None of these is invented material — all are sourced — but each expands the outline's committed scope.

| Draft material | Location | Status |
|---|---|---|
| **Node controller zone-based eviction rate limiting** — reduced rate on unhealthy zones, evictions stopped on small clusters, all-zones-unhealthy standdown | §5, ~150 words plus a reflective aside | **Scope expansion.** Appears in none of the outline's §5 concepts (`node-conditions-as-diagnostic`, `kubelet-health`, `node-lease-heartbeat`, `node-death-handling`, `crictl`). This is `kube-controller-manager` tuning behaviour — CKA-tier, not associate-tier. **Ungraded**, so exam risk is nil; cost is words in the book's highest section-to-weight chapter. |
| **`journalctl -u kubelet`** | §5, closing paragraph | **Unresolved open question shipped as prose.** Outline Open Question 6 *recommended* one mention and asked for confirmation; no confirmation is recorded. The draft's handling is exactly what was recommended — explicitly marked as leaving the Kubernetes API and as past what KCNA asks. Needs the author to close the question, not the revision stage to change the text. |
| **`crictl` endpoint configuration** — `--runtime-endpoint`, `CONTAINER_RUNTIME_ENDPOINT`, `/etc/crictl.yaml` | §5 Closer Look | **Mild expansion.** The outline ruled "Do not teach its surface." Endpoint configuration is surface. Sourced and short; a trim candidate, not a defect. |
| **`containerLogMaxSize` (10Mi) / `containerLogMaxFiles` (5)** | §7 | **Mild expansion.** kubelet log-rotation tuning is administration depth; not in the outline's §7 concept list. Sourced. Load-bearing for the "not an archive" argument, so defensible — but the specific default values are not. |
| **`hostPort` as a `Pending` cause** | §2, one sentence | Benign. Sourced verbatim from the debug-pods guide. No action. |

**Cross-domain footprint (not outline drift, but worth the author's eye):** §7 is the **definition home** for `metrics-server` and the resource metrics pipeline, which the corpus's own 08-23 snapshots tag `D4 Observability`. Ch 17 §7 and Ch 18 §3 both refer back here by design, so a 12%-domain concept is defined inside a 28%-domain chapter. That is a ledger decision already made; this audit only records that the objective index will show it, and that Ch 18 must not re-derive.

---

## Depth mismatches

Weights below are the published 28% for the domain plus, where useful, the **inferred** 7% pro rata across D2's four named competencies. The outline's `domain_weight_pct: 4` is an authored chapter-count allocation and appears nowhere the reader can see it.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| D2.3 Troubleshooting (whole chapter) | 28% domain; **~7% inferred** | 8 sections, ~95 min, 39 questions, 7 figures | **OK against the competency.** Over-delivered only against the outline's authored 4 — which is a bookkeeping number, not a reader-facing one. |
| §2 never-started family | — | deep (5 of 15 practice items) | **OK.** B1's highest-risk single gap in the book; three shipped chapters point in. Depth is earned. |
| §4 started-then-gone family | — | deep (4 of 15 practice items) | **OK.** Top confusion pair on the exam; four-axis discrimination needs the room. |
| `ImageInspectError` | same family as `ErrImagePull` | **table row + figure label only** | **under-covered.** A named `Waiting` reason with a documented meaning gets zero prose while its siblings get paragraphs. One sentence closes it. |
| Platform-scope **network** failure (CoreDNS, CNI, kube-proxy) | D2.1 Networking is Ch 9's; but the *triage routing* is this chapter's | **absent, and mis-routed by §1's own rule** | **under-covered — highest-severity finding.** See Fix 1. |
| Node controller zone eviction rate limiting | above associate tier | ~150 words, ungraded | **over-covered.** Trim candidate. |
| `crictl` | associate tier | named + 2 commands + layer argument | **OK.** Matches the ruled depth exactly. |
| §6 version skew | Ch 8 owns the policy (D1.2) | applied symptom-shapes only; table not restated | **OK.** The Ch 8 decay-fix works as designed — but the graded item that *verifies* it is broken (see Fix 6). |
| `kubectl exec` / `debug` / `port-forward` | on B1's D2.3 list | one clause + pointers | **OK at chapter level.** Book-level tagging gap; see Fix 2. |

---

## Gaps the research stage flagged

**A systemic finding first, because two snapshots share it.** Two cached files carry frontmatter that **overclaims relative to their transcribed body**. A later stage trusting the frontmatter would cite a fact the corpus does not actually hold:

- `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31.md` — `closes_gap: "B1 gap G1 -- the kubectl command surface"`, but the body is truncated at `## Interacting with running Pods` and carries **no command lines at all**. G1 is effectively still open.
- `k8s-apiserver-event-ttl-and-toleration-defaults-2026-08-31.md` — `closes_gap: "...the event retention default... BOTH ARE NOW PINNED"`, but the body stops at the `## --event-ttl` heading with no value transcribed. The retention default is **not** pinned.

| Gap | Draft handling | Verdict |
|---|---|---|
| **G1 — kubectl command surface** (documented PARTIAL; `kubectl events` explicitly not covered) | §3 writes `kubectl events --for pod/<name>`, `kubectl get events --sort-by=.metadata.creationTimestamp`, `kubectl logs --all-containers`, and `kubectl config current-context` — **four command forms with no `[source:]` tag and no AUTHOR-REVIEW flag** | **NOT handled.** The draft neither sourced nor flagged nor deferred. `--all-containers` and `--for` are the two whose exact syntax matters. |
| **`--event-ttl` default value** (Open Question 4, item 1) | AUTHOR-REVIEW comment states the value is absent from the cached text; prose writes "on the order of an hour by default, not days" as a shape | **Handled, per outline authorization.** The outline pre-approved that exact phrasing. Residual: the *magnitude* claim is still uncited. Acceptable as written; the snapshot's frontmatter should be corrected so no later stage treats it as pinned. |
| **CrashLoopBackOff backoff curve** (Open Question 4, item 2) | 10s/20s/40s → 300s cap, 10-minute reset, all cited to `k8s-docs-container-restart-backoff-2026-08-31` | **Handled.** The snapshot's `conflict_note` (rendered page said 5 min for the reset; two sources say 10) was resolved to 10 minutes, and the draft uses 10. Correct. |
| **Node-death eviction timeout** (Open Question 4, item 3) | 5-minute node-controller wait cited twice, plus the `tolerationSeconds=300` mechanism from the taints snapshot; used in a graded TYB 2 item | **Handled.** Correctly framed as taint-based rather than a dedicated timer. |
| **`troubleshoot-kubectl` snapshot truncated** before permissions / context / API-connectivity / TLS sections | §3's version-check sentence stays inside the transcribed body; the surrounding context-check material does not | **Partially handled.** The citation is honest; the unsourced commands beside it are the G1 problem above. |
| **`debug-cluster` snapshot** `partial_note`: do not cite for failure-mode taxonomy | §5 cites it once, for the node-registration sentence, which **is** in the transcribed body | **Handled correctly.** |
| **`pod-failure-signatures` snapshot** — confabulated sections were discarded at extraction | All draft citations (phase table, container states, `Waiting` reason table, node death, GC) fall inside the retained body | **Handled correctly.** |
| **LTS hazard** (Open Question 3, unresolved) | §6 does not raise it; AUTHOR-REVIEW comment records why; no graded item hinges on it | **Handled, per outline.** |
| **PodDisruptionBudget** (⚑3, unowned book-wide) | Absent from all graded and explanatory text; appears only inside a verbatim quotation about what the kubelet does *not* respect; AUTHOR-REVIEW comment records the reasoning | **Handled, per outline.** |

---

## Recommended fixes

Ordered by severity. One per issue.

**Fix 1 — §1 and §8: the scope boundary excludes platform-scope network failure.**
The mechanical test is stated twice, unhedged: *"If the Pod is `Running` and `Ready` and the behavior is still wrong, you have crossed into application scope"* (§1), restated in the Zenith as *"Only when the Pod is `Running` and `Ready` and the behavior is still wrong has the platform finished its work."* A CoreDNS outage, a CNI failure, or a broken kube-proxy each produce `Running` + `Ready` Pods with wrong behaviour and are **unambiguously platform scope**. The chapter's own rule routes them to Ch 16. Add a qualifying clause in both places — *"...and the failure is confined to that one workload"* — plus a one-clause pointer to Ch 9 for cluster-wide network faults. Both edits are small; the Zenith one matters more, because it is the sentence the reader carries out.

**Fix 2 — Book-level objective tagging: Ch 16 must claim D2.3 as a secondary objective.**
`kubectl exec`, `kubectl debug` / ephemeral containers, `kubectl port-forward`, and Service/EndpointSlice debugging are all on B1's D2.3 list and are all deferred to Ch 16, which is filed under D3.2 Debugging. The deferrals in this chapter are correct and explicitly signposted — no change to Ch 13 text is needed. But unless Ch 16's frontmatter carries `objectives: ["D3.2", "D2.3"]`, the book's objective index will show a substantial slice of D2.3 with no owning chapter. **Author decision, not a revision-stage edit.**

**Fix 3 — §3: source or flag four kubectl command forms.**
`kubectl events --for pod/<name>`, `kubectl get events --sort-by=.metadata.creationTimestamp`, `kubectl logs --all-containers`, and `kubectl config current-context` carry no `[source:]` tag, and the corpus does not hold their syntax — G1 is documented PARTIAL and the cheatsheet snapshot's body transcribes no command lines. Either (a) route a Stage 2 fetch of `kubernetes.io/docs/reference/kubectl/generated/kubectl_events/` and `.../kubectl_logs/` and tag them, or (b) add an AUTHOR-REVIEW comment naming them as unsourced pending that fetch. Do not leave them silently untagged in a chapter where every other command form is cited.

**Fix 4 — §2: give `ImageInspectError` one sentence of prose.**
It is a named `Waiting` reason, it appears as a fig02 leaf label and a table row, and the draft explains every one of its siblings. One sentence after the `ErrImageNeverPull` paragraph — the runtime could not read the image it fetched, so the fault is the image or the runtime's view of it, not the registry — closes the asymmetry at negligible cost.

**Fix 5 — §5: trim the node controller's zone-based eviction rate limiting.**
Reduce the ~150 words on `--unhealthy-zone-threshold` behaviour, small-cluster eviction stops, and the all-zones-unhealthy standdown to two sentences, keeping the all-zones-unhealthy observation (which carries the section's best argument about instrument trust) and cutting the rate-limit mechanics. This is above associate tier, it is ungraded, and it is not in the outline's §5 concept list. In the book's highest section-to-weight chapter, the words are better spent elsewhere.

**Fix 6 — TYB 3, Q2: rebuild the answer key.**
The key walks into answer C, catches its own off-by-one mid-paragraph, and corrects to B in running prose. There is already an AUTHOR-REVIEW comment on it. This is flagged here because of what the item *is*: the designated verification for §6's Ch 8 decay-fix. A broken key means the decay-fix is unverified, which is the one thing this checkpoint exists to do. Rewrite clean to B, and reword option C so 1.33-as-three-behind is still the trap without the key having to enter it.

**Fix 7 — `kb_tags`: drop `crictl-pods` and `crictl-inspect`.**
Both are listed in `kb_tags.commands` and neither appears in the draft, correctly — the outline's own §5 depth ruling authorizes `crictl ps` and `crictl logs` only. Remove the two entries so the concept index does not claim coverage the chapter deliberately declined to give.

**Fix 8 — Research-stage correction: fix two overclaiming snapshot headers.**
Amend `k8s-docs-kubectl-cheatsheet-troubleshooting-2026-08-31.md` to state that G1 remains **open** (body truncated before any command lines), and amend `k8s-apiserver-event-ttl-and-toleration-defaults-2026-08-31.md` to state that the retention default is **not** pinned (body truncated at the heading). Both currently assert closure in frontmatter that the transcribed body does not support, and a later chapter reading only the frontmatter will cite a number the corpus does not hold.

---

## Not in scope for this audit

Three cross-bearings in the draft do not appear in the outline's per-section lists — `Ch 3 §5 — the only door in` (§5), `Ch 16 §2 — debugging init containers` (§2), and `Ch 8 §4 — cordon, drain, and taking a node out of service` in place of the outline's `Ch 8 §7 — etcd backup` (§5). Pointer verification against the section skeleton belongs to Stage 13 (integration check) and is recorded here only so that stage does not read them as new.