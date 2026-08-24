I have everything I need. Here is the audit — note it surfaced a pipeline handoff failure that produced two real coverage holes.

```markdown
# Curriculum-Alignment Audit — KCNA Chapter 5

**Draft audited:** `.pipeline-state/ch-05/draft-v1.md` (1,194 lines, post-voice-swap).
**Note on inputs:** the stage prompt referenced `draft-voice.md`, which does not exist. The voice stage wrote back into `draft-v1.md` and preserved the pre-voice copy as `draft-v1-prevoice.md`. This audit reads `draft-v1.md`, which is the voiced draft. No stage was in flight.

**Authority used:** `cncf-kcna-curriculum-pdf-2026-08-23`, `lf-kcna-exam-page-2026-08-23`, `lf-kcna-program-changes-2026-08-23`, `cncf-kcna-certification-page-2026-08-23`. All four agree and none publishes sub-objective identifiers or sub-weights.

**Standing caveat on objective IDs.** CNCF publishes **four domains and twelve named competencies, with no numbering and no sub-weights**. "D1.1" is this book's internal notation for *Kubernetes Fundamentals (44%) → Kubernetes Core Concepts*. Every row below decomposes that single published competency using the outline's own `kb_tags` concept inventory, which is the auditable contract. The chapter claims exactly one objective for all nine sections, so a one-row table would be useless.

---

## Objectives the outline claims to cover

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.1 | Pod as unit of scheduling; shared network namespace, Pod IP, `localhost`, shared volumes; PodSpec | YES (§1) | appropriate |
| D1.1 | Single- vs multi-container Pods; coupling rule; sidecar | partial (§2) | shallow — pattern named, modern implementation omitted |
| D1.1 | Init containers: ordering, run-to-completion, failure behavior | YES (§3) | appropriate — but **untagged and partly contradicted** (see Gaps) |
| D1.1 | Pod lifetime, UID, scheduled-once, replacement, eviction | YES (§4) | appropriate |
| D1.1 | `pod-termination` | **NO** | — omitted at line 353 by AUTHOR-REVIEW |
| D1.1 | Five Pod phases | YES (§5) | appropriate |
| D1.1 | Three container states + `Reason`/`exitCode`/`startedAt` | YES (§5) | appropriate |
| D1.1 | Phase-vs-state scope distinction | YES (§5) | deep — correctly the chapter's centerpiece |
| D1.1 | `restartPolicy`, restart backoff, backoff reset | YES (§5) | appropriate |
| D1.1 | ServiceAccount identity: namespaced, `default`, auto-assignment, no permissions, `spec.serviceAccountName`, TokenRequest, projected volume | YES (§6) | shallow — correct, plant altitude held |
| D1.1 | Three probe types + four mechanisms + failure behaviors + parameters | YES (§7) | deep — appropriate, highest-yield after §5 |
| D1.1 | Requests vs limits; component attribution; CPU throttling vs OOM kill | YES (§8) | deep — appropriate |
| D1.1 | Resource types and units (`cpu`, `memory`, `ephemeral-storage`, `hugepages`, extended resources, `m`/`M`) | YES (§8) | deep — **over-covered on unit minutiae** |
| D1.1 | `qos-class`, `qos-guaranteed`, `qos-burstable`, `qos-besteffort` | **NO** | — three class names appear in one sentence (line 706); no definitions, no derivation rules, no eviction consequence |
| D1.1 | `pod-template` | **NO** | — appears only as a Ch 6 cross-bearing. Correctly deferred; the **tag is wrong**, not the draft |
| D1.1 | Commands: `kubectl-get`, `kubectl-describe`, `kubectl-explain` | **NO** | — `kubectl get` and `kubectl describe` appear once each, both as prose asides; `kubectl explain` never appears |

**Summary:** 11 of 16 claimed concept clusters land at appropriate depth. Two are genuine content holes (QoS classes, Pod termination). Two are over-claims in `kb_tags` rather than draft failures (`pod-template`, the three commands). One is shallow-by-design with a defensible omission (sidecar implementation).

---

## Objectives covered in the draft but NOT in the outline

**No genuine scope creep.** The draft does not teach any domain the outline didn't claim, and every adjacency to another competency is bounded and cross-referenced rather than developed. Recorded for completeness:

| Material | Competency it edges toward | Verdict |
|---|---|---|
| Requests as the scheduler's placement input (§8) | D1 → Scheduling | **No action.** Outline anticipates this ("applied under D1.3 in Ch 7"); the draft introduces the field and hands filtering to Ch 7 at line 737. |
| ServiceAccounts, TokenRequest, projected tokens (§6) | D2 → Security | **No action.** `k8s-docs-service-accounts-2026-08-23` is itself dual-tagged `["D2 Security", "D1 Core Concepts"]`, which warrants the D1.1 attribution. RBAC is refused explicitly at line 553. |
| `ImagePullBackOff` / `CrashLoopBackOff` (§5) | D2 → Troubleshooting | **No action.** Vocabulary only. Line 462 refuses diagnostics by name and hands method to Ch 13. The boundary Ch 2 published is honored. |
| Readiness failure → Service endpoint removal (§7) | D2 → Networking | **No action.** One clause, EndpointSlice correctly never named, forward-planted to Ch 9 at line 630. |
| OOM-kill under node memory pressure (§8, Bearings #3 item 5) | D2 → Troubleshooting | **No action.** Mechanism only; line 795 explicitly declines to diagnose. |

One item for author decision rather than a drift finding: **Practice Q21's distractor rationale** (line 1144) cites `k8s-docs-control-plane-node-communication-2026-08-24` and `k8s-docs-kube-scheduler-2026-08-23` to explain why the kubelet doesn't read etcd. That is Ch 3 retrieval doing legitimate work in an answer key, not new teaching. Keep.

---

## Depth mismatches

CNCF publishes no sub-weights, so the "exam weight" column is the published **domain** weight plus this book's authored chapter allocation. Both are stated as such, never as an official sub-figure.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| Phase vs container state (§5) | D1 44% · book 7% · chapter centerpiece | deep | OK — correctly the densest block; Ch 13 and Ch 16 both depend on it |
| Probes: three types, failure behaviors (§7) | D1 44% · high recognition yield | deep | OK |
| Pod / shared namespace / one IP (§1) | D1 44% · premise of Ch 9 | deep | OK |
| Requests vs limits, component attribution (§8) | D1 44% · retrieved by 4 later chapters | deep | OK |
| **Resource unit minutiae (§8 movement three)** | associate-tier recognition exam | deep | **over-covered.** `hugepages-<size>`, extended resources, the full `E/P/T/G/M/k` + `Ei/Pi/Ti/Gi/Mi/Ki` ladder, and the "no finer than `1m`" precision floor are below the KCNA waterline. The `m`-vs-`M` hazard and the `0.1 = 100m` equivalence earn their place; the rest is reference padding in the chapter's second-densest section. |
| **QoS classes (§8 movement four)** | D1 44% · named in `kb_tags` · Ch 13 precursor | **named only** | **under-covered.** One sentence asserts the classes exist and are derived; nothing defines Guaranteed/Burstable/BestEffort or their derivation. A reader cannot answer any QoS question from this draft. |
| **Pod termination (§4)** | D1 44% · `kb_tags` claims `pod-termination` | **absent** | **under-covered.** §4 teaches "replaced not repaired" but never that termination is a request with a deadline. Also weakens Ch 15's twelve-factor disposability callback. |
| Sidecar containers (§2) | D1 44% · sidecar named in `kb_tags` | shallow | **borderline.** Pattern and decision rule are correct and sufficient for recognition. The v1.29+ implementation is now sourced and would connect §2↔§3, but its absence does not leave a reader unable to answer. Author's call. |
| ServiceAccount identity (§6) | D1 44% · plant; full treatment Ch 12 | shallow | OK — deliberate, and the four-fact ceiling from outline Open question #4 is held exactly |
| Multi-container decision rule (§2) | D1 44% | shallow | OK — brevity is the register for a "don't do this" section |
| Init containers (§3) | D1 44% | appropriate | OK on depth; see Gaps for a correctness issue |

---

## Gaps the research stage flagged

**This is the chapter's root-cause finding, and it is a pipeline handoff failure rather than a drafting failure.**

The research manifest (`research-manifest.md`, 06:26) opens with a blocker: the stage had **no filesystem write access**, so it could produce only one artifact via stdout. It reports the research itself as complete — *"all four blocking gaps from § Open questions #2 are closed, plus the sidecar page for #3"* and *"**Gaps: None blocking.**"* — but flags that **five snapshots still needed a materialization pass**:

- `k8s-docs-pods-2026-08-24.md`
- `k8s-docs-init-containers-2026-08-24.md`
- `k8s-docs-pod-qos-2026-08-24.md`
- `k8s-docs-sidecar-containers-2026-08-24.md`
- `k8s-docs-pod-termination-2026-08-24.md`

**That materialization pass never ran.** `../Book-KCNA/sources/` holds 115 files; none of the five is present, and the newest snapshots there are all Chapter 2 material from 2026-08-24 01:05. The drafting stage (06:34) therefore worked from the *pre-research* source set and correctly re-flagged as open four gaps the research stage had already closed.

The draft handled this **exactly right** and should not be penalized for it. It carries seven `AUTHOR-REVIEW` markers, each naming the missing page and citing the outline's Open question by number, and — critically — it **refused to draft QoS from memory** (line 708), which is precisely what outline Open question #2 instructed. Structural lint passes 30/30 with 0 fail, 0 warn. Honest under-coverage beats confident fabrication.

Per **rule 3**, an objective with no authoritative snapshot is a research-stage gap, not an alignment failure. Two of these four no longer qualify for that exemption, because the snapshots *were retrieved* and merely failed to land:

| Gap | Research status | Alignment verdict |
|---|---|---|
| QoS classes (G3 second half) | **Retrieved.** Manifest confirms the page was fetched | **Real coverage hole.** Blocked on materialization, not on research |
| Pod termination | **Retrieved.** Manifest: *"now fully sourced: default grace period 30 seconds, `preStop` hook, TERM then KILL, `terminationGracePeriodSeconds`"* | **Real coverage hole.** Outline Open question #5's condition for inclusion is now met |
| Pod concept page | **Retrieved** | Content is correct and sourceable from secondary mentions; only the §2 "two main ways" framing is untagged. Low severity |
| Init containers | **Retrieved** | Content present but untagged — **and now known to be partly wrong**, see below |
| Sidecar page | **Retrieved.** Manifest: implementation *"established plainly"*, so outline Open question #3's condition is met | Author decision, not a hole |

**Two correctness items the research manifest raised that bear directly on whether a claimed objective is covered *correctly*.** Both belong to the fact-accuracy audit; recorded here because each concerns D1.1 material the draft presents as settled:

1. **§3's init-container failure behavior is incomplete.** The draft states a failed init container is restarted "according to the Pod's `restartPolicy`" (line 241). The retrieved source adds: *"if the Pod `restartPolicy` is set to Always, the init containers use `restartPolicy` OnFailure."* The `Never` case the draft describes is correct; the `Always` case is not straight inheritance. Bearings #1 item 3 and Practice Q10 distractor *C* both rest on the simplified version.
2. **§3's "init containers don't carry probes" needs a qualifier.** Sourced as *"**Regular** init containers … do not support the `lifecycle`, `livenessProbe`, `readinessProbe`, or `startupProbe` fields."* Sidecars support all three. If §2 adopts the modern sidecar implementation, line 252's axis needs the word *regular*.

Two minor items the manifest flagged that the draft already honors: it never asserts a `status.qosClass` field name, and it never attempts a worked `kubectl explain` invocation.

---

## Recommended fixes

**1. Materialize the five research snapshots before revision — this is the blocking prerequisite.** Write `k8s-docs-pods-2026-08-24.md`, `k8s-docs-init-containers-2026-08-24.md`, `k8s-docs-pod-qos-2026-08-24.md`, `k8s-docs-sidecar-containers-2026-08-24.md`, and `k8s-docs-pod-termination-2026-08-24.md` into `../Book-KCNA/sources/`. Their content is preserved in `research-manifest.md`. Fixes 2–5 are all blocked on this. Separately, the executor should be given write access for multi-artifact stages, or the research prompt should emit snapshots as fenced blocks the orchestrator can split — this failure will recur on every chapter whose research stage produces more than one file.

**2. Write §8 movement four (QoS classes).** Replace the placeholder paragraph at line 706 and the AUTHOR-REVIEW at 708 with the three classes, their derivation from how requests and limits were filled in, and the eviction-ordering consequence. Complete the lower half of `ch05-fig05` (line 729 currently carries a placeholder pointing at the AUTHOR-REVIEW). Do not name a `status.qosClass` field — the manifest confirms the source's prose does not. Add one Bearings #3 or Practice item so the concept is assessed; the chapter currently assesses zero QoS material despite tagging four QoS concepts.

**3. Add a bounded Pod-termination beat to §4.** Outline Open question #5's condition is met. Hold to the altitude it specified — *"termination is a request with a deadline, not an instant event"* — with the 30-second default grace period, `terminationGracePeriodSeconds`, and TERM-then-KILL. One short paragraph, replacing the AUTHOR-REVIEW at line 353. Do not teach `preStop` hook syntax; that exceeds associate tier and §4 is deliberately a low-cost section.

**4. Correct §3's init-container restart behavior.** Amend line 241 to reflect that a Pod `restartPolicy` of `Always` causes init containers to use `OnFailure`. Re-check Bearings #1 item 3's answer key (line 292) and Practice Q10 distractor *C*'s rationale (line 1100) against the corrected rule — Q10's current explanation asserts init failures follow the Pod's policy without qualification.

**5. Add source tags to §3 and §2.** Once the snapshots land, tag the init-container ordering and run-to-completion claims (currently the only substantive untagged block in the chapter) and the §2 "two main ways Pods are used" framing. Remove the AUTHOR-REVIEW markers at lines 187 and 216.

**6. Author decision on the sidecar implementation (§2).** The condition in outline Open question #3 is now met. If adopted: one clause naming sidecars as init containers with `restartPolicy: Always`, plus the *regular* qualifier in §3 line 252. If declined: delete the AUTHOR-REVIEW at line 200 so it doesn't read as unfinished work. Recommend adopting — it connects §2 and §3, which currently sit adjacent without interacting, and it prevents a wrong model of what a sidecar is.

**7. Trim §8 movement three.** Cut `hugepages-<size>`, extended resources, the full suffix ladder beyond `Mi`/`Gi`, and the `1m` precision floor to a single clause or a 🔭 Closer Look. Keep `0.1 = 100m`, the `m`/`M` hazard, and CPU-as-absolute. §8 is the chapter's second-highest attention cost and this is the cheapest available reduction.

**8. Correct the `kb_tags` over-claims — outline edit, not draft edit.** Drop `pod-template` (the outline's own Ch 6 scope boundary assigns it there, and the draft correctly defers it). Either drop `kubectl-get` / `kubectl-describe` / `kubectl-explain`, or accept them as tags-by-mention — but note that adding worked invocations would breach the Ch 13 method boundary the draft holds deliberately at line 462. **Recommend dropping all four tags.** No draft change.

**9. No action on drift.** Every adjacency to Scheduling, Security, Networking, and Troubleshooting is bounded, cross-referenced, and explicitly refused where it would cross a published chapter boundary. This chapter's scope discipline is its strongest alignment property; the revision stage should not loosen it while fixing the holes above.
```

**Two things worth your attention beyond the audit itself:**

The stage prompt asked for `draft-voice.md`, which doesn't exist — the voice stage writes back into `draft-v1.md` and keeps `draft-v1-prevoice.md` as the backup. Three other diagnostic stages ran against the same prompt template at 06:39, so fact-accuracy, question-quality, and theming-density likely all received the same "file not available" placeholder. Worth checking whether they audited the draft or reported a blocker.

The root cause of the two real coverage holes is that the research stage had no write access and could only emit one artifact through stdout, so five retrieved snapshots never reached `sources/`. The drafting stage then re-flagged four already-closed gaps as open. This will recur on any chapter whose research stage produces more than one file.