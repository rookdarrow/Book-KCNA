The Write was declined — consistent with the pipeline design where this stage's stdout is the artifact. Emitting the document.

# Curriculum-Alignment Audit — KCNA Chapter 3

**Draft audited:** `.pipeline-state/ch-03/draft-v1.md` (1,078 lines, voice pass applied 03:24).
**Note on inputs:** the stage prompt reported the voiced draft as `draft-voice.md` / *file not available*. The voice stage wrote `draft-v1.md` instead (`draft-v1-prevoice.md` preserves the pre-voice text). This audit reads the on-disk voiced draft. **The stage-prompt cached-source block is also stale** — it carries only the 08-23 snapshots and omits the five snapshots Stage 2 fetched for this chapter on 08-24. Both are pipeline-wiring defects, not authoring defects, but the second one materially affects the findings below.

**Authority used.** `cncf-kcna-curriculum-pdf-2026-08-23.md`, `lf-kcna-exam-page-2026-08-23.md`, and `lf-kcna-program-changes-2026-08-23.md`. All three publish **four domains and twelve named competencies, with no numbering and no sub-competency weights.** The `D1.1`-style identifiers below are a Lodestar convention (`book-outline/domain-analysis.md:33`), and the sub-letters `(a)`–`(k)` are this audit's decomposition of the arc-outline's Chapter 3 "Covers" line. Neither is a curriculum artifact. Chapter 3 claims exactly one published competency: **Kubernetes Core Concepts**, under **Kubernetes Fundamentals (44%)**.

---

## Objectives the outline claims to cover

Every section in `outline.md` tags `objectives: ["D1.1"]`. Decomposed against `arc-outline.md:106`:

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.1 (a) | Deployment eras — traditional / virtualized / container | YES — §1 "The three deployment eras" + `ch03-fig03` | appropriate |
| D1.1 (b) | What Kubernetes provides (published capability list) | YES — §1, all ten published capabilities as a table | appropriate (generous) |
| D1.1 (c) | What Kubernetes is **not** | YES — §1, all six published items + PaaS framing + orchestration disclaimer planted | appropriate — deliberately deep, justified |
| D1.1 (d) | Control-plane components ×5 (kube-apiserver, etcd, kube-scheduler, kube-controller-manager, cloud-controller-manager) | YES — §2, each with its one job; optionality marked on CCM | appropriate |
| D1.1 (e) | Node components ×3 (kubelet, kube-proxy, container runtime) | YES — §3, each with its one job; optionality marked on kube-proxy | appropriate |
| D1.1 (f) | Addons | YES — §4, all four published addons + the addon/component distinction | appropriate |
| D1.1 (g) | Controllers (pattern; control via API server vs direct control; the four named built-ins) | YES — §6 for the pattern, §2 for the four named built-ins | appropriate |
| D1.1 (h) | **The control loop** — reconciliation, non-terminating | YES — §6, ★ Fixed Point + `ch03-fig02` + Extended Analogy | deep — justified by the six-chapter downstream contract |
| D1.1 (i) | Desired vs current state, incl. the never-stable-state claim | YES — §6 "Desired versus current state" | appropriate |
| D1.1 (j) | Kubernetes origin and history | YES — §1 "Where it came from" | **over-covered** (see Depth mismatches) |
| D1.1 (k) | The hub arrangement / API server as front end | YES — §5, ⚓ Worth Securing + submission story + `ch03-fig04` | prose appropriate, **assessment shallow** |
| — | Retrieval from Ch 2 (D1.4 Containerization): CRI boundary, image immutability, container-vs-VM | YES — Bearings #1 Q5, Practice Q19, §1 back-bearing; all tagged `[retrieval: ch2]` | on-plan (10% target, 3 of 32 items) |

**Nothing the outline claimed is missing.** All 42 `kb_tags.concepts` entries appear in the draft, all planned markers are present (3 ★ Fixed Points, 1 Dead Reckoning, 2 ⚠ Navigational Hazards, 1 ☀️ Zenith, 1 Extended Analogy, 2 🪝 Snags, 2 🔭 Closer Looks, 4 ⚓ Worth Securing, 1 🪢 Mnemonic, 🏆 Safe Harbor), and the question budget lands exactly as planned (8 Soundings · 13 Bearings across 3 checkpoints · 19 Practice = 40).

**Scope boundaries held — worth recording, because four of them were live risks.** The draft does not name `spec`/`status` (Ch 4), does not name a kube-proxy mode (Ch 9), does not teach filter → score → bind (Ch 7), and does not teach Pod phases or probes (Ch 5). Outline Open question #3 was resolved as recommended: §6 teaches the loop in plain language and cross-bears the field names forward.

---

## Objectives covered in the draft but NOT in the outline

Four items. None is large; two need an author decision, two need a fix.

**1. Objective-tagging drift on §5 — needs a tag correction, not a content change.**
§5 is tagged `objectives: ["D1.1"]`. The book's own concept map assigns **"Control-plane ↔ node communication — the trust and traffic paths between the API server and node components"** to **D1.2 Administration** (`domain-analysis.md:119`), which is Chapter 8's. The *"API server is the front end"* fact is genuinely D1.1 (it sits in the D1.1 concept map under kube-apiserver), so the drift is narrow, and the draft holds the depth boundary correctly — it defers authentication, authorization, admission, TLS, and Konnectivity to Ch 8. **Recommendation: tag §5 `["D1.1", "D1.2 (touch)"]` so the reconcile pass sees the overlap, and leave the prose alone.**

**2. Kubelet behavior during a control-plane partition — scope creep plus an unsourced claim. §7, line 773.**
> "A kubelet whose control plane is unreachable doesn't sit waiting for orders. It keeps the containers it already knows about running..."

This is a claim about node behavior under control-plane failure. It is not in any cached or newly-fetched snapshot, and node/control-plane failure behavior belongs to D1.2 (Ch 8, node lifecycle) and D2.3 (Ch 13, node health). The claim is true and it is doing real rhetorical work — it is the concrete payoff for "no component was taking instructions." But it is currently asserted with no source tag, in a Zenith section, one paragraph after the draft correctly refuses to overclaim resilience. **Either source it or reframe it as a consequence of the architecture rather than as a reported behavior.**

**3. Docker / PyCon 2013 / Solomon Hykes origin paragraph — §1, line 200.**
Sourced (`k8s-history-ten-years-2026-08-23`) and accurate, but not in the outline's §1 specification, which stopped at Borg / Omega / Go / 2014-06-06 / DockerCon / v1.0 / CNCF / helmsman / K8s. It reads as ecosystem history adjacent to D4.2, which is Ch 17's. Low severity; flagged for author decision, and it is the first thing to cut if §1 needs to come down.

**4. The etcd consistency gloss — §2, line 260.** Expands past both available sources; treated under Gaps below.

---

## Depth mismatches

CNCF publishes no sub-competency weights, so "exam weight" below is the arc-outline's authored 6-point allocation distributed across the chapter by documented exam surface. Depth is measured as prose time (from the draft's own Attention Budget) **plus assessment coverage**, because an objective with a stated learning outcome and no question testing it is not covered to depth.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| (d)+(e) Component census | Largest pure-recall surface in the chapter | 25 min · 7 practice · 5 Bearings · ★ Fixed Point · Dead Reckoning | OK |
| (g)+(h)+(i) Controllers and the control loop | Highest value in chapter; 6 downstream retrievals | 14 min · 4 practice · 4 Bearings · ★ Fixed Point | OK — deep by design, justified |
| (c) What Kubernetes is not | Moderate-high; Exam Alert #5 | ~4 min · 2 practice (Q2, Q18) | OK |
| (a) Deployment eras | Modest; partly a retelling of Ch 2 §1 | 3 paragraphs · figure · 1 practice | OK |
| (f) Addons and optionality | Small documented surface, high per-item value | 6 min · **4 of 19 practice questions** (plan: 2) · 3 Bearings | **over-assessed** — Q11, Q12, Q13, Q14 all land here |
| (k) The hub arrangement | Learning outcome #3 ("Trace what happens between a submitted request and a running container"); load-bearing for §7's Zenith and for Ch 15 | 10 min prose (rated High attention) · **1 practice question, and it is pure recall** (Q4, "which component is the front end") | **under-assessed** — plan was 2 practice items |
| (b) What Kubernetes provides | Modest — the is-not list is the tested half | 10-row table with a bespoke "problem it solves" column | slightly over-covered — acceptable, and the right-hand column earns its keep by setting up §6 |
| (j) Origin and history | **Not a published competency.** No CNCF or LF source lists Kubernetes history as examinable | 5 paragraphs · 🔭 Closer Look · Practice Q3 · Soundings Q7 | **over-covered** — trim, do not cut |

**On (k), precisely.** The *content* is assessed once, well, in Taking Your Bearings #2 Q4 — which the draft itself flags as the integrative item. But the Practice bank contains nothing on watching-not-telling, the submission sequence, or the absence of lateral communication. The outline also required **≥5 of 19 practice questions to combine two sections**; the draft delivers roughly three (Q12, Q14, Q18), and the two pairings the outline named as highest-value are both absent: **§2+§6** ("given a controller's job, name the component that houses it and the loop it runs" — the outline called this the single best integrative item in the chapter) and **§3+§5** ("given a node component, say what it talks to and what it does not").

**On (j).** The outline argued at Soundings Q7 that history is "genuinely tested content, not trivia." No authoritative source supports that. Keep the Borg/Omega lineage and the helmsman etymology — both are widely reproduced in KCNA prep and cost two sentences — and treat the rest as brand-voice material rather than exam material. That is a defensible authorial choice; it just should not be defended on exam-weight grounds.

---

## Gaps the research stage flagged

`research-manifest.md` closed the outline's one blocking gap and fetched five new snapshots. **The draft cites none of them.** Every `[source:]` tag in `draft-v1.md` points at an 08-23 cached file; a search for `2026-08-24` returns zero matches. The manifest's three named gaps and its two most consequential author notes were therefore not acted on. This is the single largest finding in this audit, and it is almost certainly caused by the stale cached-source block in the stage prompt rather than by drafting judgment.

| Manifest item | Status | How the draft handled it |
|---|---|---|
| **G-A** — "operating system" vs "operating system **kernel**"; **UNSOURCED**, third chapter running | **mishandled** | §1 line 126 writes "share the operating system kernel" and closes the sentence group with `[source: k8s-docs-overview-2026-08-23]`. That snapshot says "share the **Operating System (OS)**." The sharpening is technically correct and is the book's own precision call — but it is now *attributed to a source that does not say it*. The AUTHOR-REVIEW comment at line 128 is honest about the history and does not fix the attribution. The Chapter Summary (line 1046) repeats "OS kernel shared" unqualified. |
| **G-B** — a reader-facing gloss on etcd "consistent"; **PARTIALLY SOURCED** | **partially mishandled** | §2 line 260 writes the exact sentence the manifest said is not sourceable ("every component that reads from etcd through the API server gets the same answer as every other component"), as flat exposition, opening with "Two words deserve unpacking." It carries no false `[source:]` tag, so nothing is misattributed — but it sits immediately after sourced text and reads as documentation-derived. The manifest asked for it to be visibly framed as explanation. Low severity; the gloss itself is good and the depth ceiling (no quorum, no Raft) was respected. |
| **G-C** — "cluster DNS is effectively mandatory"; **PARTIALLY SOURCED after this pass** | **partially mishandled** | §4 line 448 frames it as observation (correct), and the AUTHOR-REVIEW comment at line 450 says so. But that comment is **stale**: it instructs the author to fetch `kubernetes.io/docs/concepts/cluster-administration/addons/`, which Stage 2 fetched (snapshot A2), and Stage 2 also found the stronger sentence in A4 — *"DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on."* That sentence supports most of what §4 wants and is unused. Separately, **Bearings #2 Q3's explanation (line 570) restates the empirical claim as bare fact** — "Cluster DNS in particular is present in essentially every working cluster" — inside an answer key, where the observation framing from the body text is lost. |
| **Manifest Note #1** — "only the API server talks to etcd" is sourced as a **recommendation** ("*ideally* only the API server should have access to it"), not an invariant | **mishandled, four places** | The draft states it as an absolute at line 488 (figure caption: "only the API server reaches etcd"), line 577 (Q4-D explanation: "components don't reach past the API server into etcd"), line 584 (checkpoint: "only the API server to etcd"), and line 1060 (Chapter Summary: "Only the API server reaches etcd"). The manifest recommended the softer, truer framing — the API server is the component that reads and writes etcd, and anything else with etcd access holds root-equivalent power — and noted it sets up Ch 12's encryption-at-rest decision better. |
| **Manifest Note #2** — `ch03-fig04` must not imply that nothing flows outward from the hub; the API server **does** open connections to kubelets for logs, `attach`, and port-forward | **not handled** | The figure draws kubelet→apiserver arrows only, and the caption directs the reader to "look for the arrows that aren't drawn." No sentence acknowledges the API server → kubelet path. §5's "Neither one knows the other exists" and Q4-A's "there is no such dedicated channel" will read as contradicted the moment Ch 13 introduces `kubectl logs`. The manifest's recommendation — scope §5 and the figure explicitly to the **state/API path**, add one acknowledging sentence, cross-bear to Ch 13 — is unimplemented. The Zenith survives this intact; its claim is about direction, not connectivity. |
| **Manifest Note #3** — the Zenith's narrow claim is now directly quotable: "None of the other control plane components are designed to expose remote services" | **unused opportunity** | §7 rests on the overview page's orchestration passage alone. The new sentence is unusually clean support for the precise thesis (*no component tells another what to do*) because it describes an absence of capability rather than a policy. |
| **Manifest Note #4** — Bearings #2 Q4 is unblocked and can be written as designed | **handled** ✓ | The item is written as designed and is the strongest question in the chapter. Its explanation would be stronger still quoting the sentence above. |
| **Outline Open question #6** — the 6% chapter weight is authored judgment, not CNCF data | **handled well** ✓ | The metadata line reads "~6% of exam (authored estimate)" and "Why This Chapter Matters" states plainly that CNCF publishes weights per domain, not per competency. This satisfies Ethical Guardrail #1 and needs no change. |
| **Stale BLOCKING comment** — `draft-v1.md:490` | **must be removed** | The comment instructs Stage 2 to fetch `control-plane-node-communication`, warns the section may need narrowing, and says the figure may need redrawing. Stage 2 fetched it (manifest A1). Left in place, this comment will send the revision stage chasing a gap that is closed, and it obscures the two real qualifications (Notes #1 and #2) that *did* survive the fetch. |

---

## Recommended fixes

Ordered by severity. Items 1–5 are corrections; 6–8 are calibration; 9 is optional.

1. **Re-cite §2, §4, §5 and §7 against the five 08-24 snapshots before any other edit.** The revision stage must read `research-manifest.md` directly rather than the stage prompt's cached-source block, which predates Stage 2. Nothing else in this list can be closed without it.

2. **Soften the etcd absolutism in four places** (lines 488, 577, 584, 1060) to the sourced claim: the API server is the component that reads and writes etcd, and anything else with etcd access holds root-equivalent power in the cluster. Cite `k8s-docs-etcd-access-control-2026-08-24`. This is truer, it preserves the whole pedagogical point of §5, and it plants Ch 12's encryption-at-rest decision instead of contradicting it.

3. **Scope §5 and `ch03-fig04` to the state/API path, and add one sentence acknowledging the API server → kubelet connections** used for pod logs, `kubectl attach`, and port-forwarding, cross-beared to Ch 13. Cite `k8s-docs-control-plane-node-communication-2026-08-24`. Adjust the figure caption from "the arrows that aren't drawn" to the narrower and still-strong claim: **no arrow between two non-apiserver components**. Q4-A's explanation ("there is no such dedicated channel") needs the same narrowing — the point is that no component *directs* another, not that no connection exists.

4. **Fix the G-A attribution in §1.** Either quote the snapshot verbatim ("share the Operating System (OS) among the applications") and add the kernel sharpening as a visible authorial gloss outside the `[source:]` tag, or move the source tag off that sentence. Whichever Chapter 2 chose, match it exactly — this is the third chapter to hit the phrase and the reconcile pass will surface any divergence. Apply the same fix to the Chapter Summary row.

5. **Rewrite the two stale AUTHOR-REVIEW comments** (lines 450 and 490). Line 490 should be deleted outright and replaced, if anything, by a note carrying Manifest Notes #1 and #2 forward. Line 450 should be replaced by the fix in item 6.

6. **Upgrade §4's cluster-DNS claim using the now-available source.** Use "DNS is a built-in Kubernetes service launched automatically using the addon manager cluster add-on" (`k8s-docs-dns-cluster-addon-2026-08-24`) for the built-in / launched-automatically half, and keep the "almost every real cluster" half as an explicit author observation. **Then fix Bearings #2 Q3's explanation (line 570)**, which currently asserts the unsourced half as bare fact inside an answer key — the one place the reader has no way to see the framing.

7. **Rebalance two practice questions from §4 to §5, and add the §2+§6 integrative item.** Concretely: retire or merge one of Q13/Q14 (they test the same optionality surface from two angles), and add (i) a §3+§5 item — given a node component, what does it talk to and what does it not — and (ii) the §2+§6 item the outline named as the chapter's best: *given a controller's job, name the component that houses it and the loop it runs*. That restores §5 to its planned 2 items, moves interleaving from ~3 to ~5, and costs nothing in total count.

8. **Frame the etcd "consistent" gloss as explanation** (§2, line 260). One clause is enough — "in plain terms, what that buys you is..." — and cite `etcd-io-what-is-etcd-2026-08-24` for "strongly consistent" if the stronger adjective is wanted. Per manifest Note #5, prefer the Kubernetes wording in exam-facing text and keep the two formulations out of the same paragraph.

9. **Source or reframe the kubelet-partition claim in §7 (line 773), and consider trimming the Docker/PyCon paragraph in §1 (line 200).** The first is a correctness item with a scope component; the second is purely an author's call about how much D4.2-flavored history a D1.1 chapter should carry.

---

*Audit complete. Coverage against the outline's claims: **complete** — 11 of 11 claimed objective slices covered, no omissions, all planned structural elements present, all four cross-chapter scope boundaries held. The findings are not about what the chapter covers but about **sourcing discipline on five newly-fetched snapshots the draft never saw**, two claims stated more absolutely than the evidence supports, and an assessment imbalance that under-tests §5 and over-tests §4.*