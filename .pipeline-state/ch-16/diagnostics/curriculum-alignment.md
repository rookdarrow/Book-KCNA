# Curriculum-Alignment Audit — KCNA Chapter 16

**Chapter:** 16 — *Your Application, Their Cluster*
**Artifact audited:** `draft-v1.md` (no `draft-voice.md` at this stage)
**Authority:** `cncf-kcna-curriculum-pdf-2026-08-23.md` (CNCF, four published domain weights)
**Audited:** 2026-08-31

**Citation convention for this report.** The draft was presented without line numbering, so findings cite `§N` plus a distinctive quoted phrase rather than a line number. Every quoted phrase is unique in the draft and greppable.

**Objective-ID note — read before the tables.** CNCF publishes **four** domain weights (44 / 28 / 16 / 12) and names competencies inside each, but publishes **no sub-competency weights and no enumerated sub-objectives**. The `D<n>.<m>` IDs used below are the book's authored scheme (`D3.2` = Cloud Native Application Delivery › Debugging; `D2.3` = Container Orchestration › Troubleshooting), and the finer decomposition of D3.2 below is *this audit's* decomposition, taken from the canonical page set the Kubernetes documentation itself groups under Troubleshooting Applications [source: k8s-docs-troubleshooting-applications-index-2026-08-31]. It is used because auditing two coarse IDs would yield "both covered" and tell the revision stage nothing. It is not a CNCF structure and must not be presented to the reader as one.

---

## Objectives the outline claims to cover

The outline claims exactly two: `kb_tags.objectives: ["D3.2", "D2.3"]`.

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| **D3.2** | Cloud Native Application Delivery › **Debugging** (whole competency) | **YES** | appropriate |
| D3.2 · a | Debug Pods — application-scope triage, the audience boundary | YES — §1, quotes the docs' own audience split | appropriate |
| D3.2 · b | Debug Pods — *"my pod is running but not doing what I told it to do"* | **partial** | **shallow — the API-side half is absent (see Finding 1)** |
| D3.2 · c | Debug Init Containers — status strings, `logs -c` | YES — §2, `Init:N/M`, `Init:Error`, `-c` | appropriate |
| D3.2 · d | Debug Running Pods — `exec`, ephemeral containers, `kubectl debug`, `--copy-to`, `node/`, profiles | YES — §3 | appropriate (deepest section, correctly so) |
| D3.2 · e | Get a Shell to a Running Container | YES — §3, `kubectl exec -it … -- /bin/bash` | appropriate |
| D3.2 · f | Debug Services — selector, readiness, ports, DNS | YES — §4, four break points | appropriate |
| D3.2 · g | Debug a StatefulSet | YES — §6 | appropriate (source is a stub; see Gaps) |
| D3.2 · h | Determine the Reason for Pod Failure — termination messages | YES, prose only | **shallow — ungraded and untagged (see Finding 2)** |
| D3.2 · i | Developing and debugging services locally | YES — §7 | appropriate (matches the outline's depth ruling) |
| **D2.3** | Container Orchestration › **Troubleshooting** — the four items Ch 13 deferred here | **YES** | appropriate |
| D2.3 · 1 | `kubectl exec` | YES — §3 | appropriate |
| D2.3 · 2 | `kubectl debug` / ephemeral containers | YES — §3 | appropriate |
| D2.3 · 3 | `kubectl port-forward` | YES — §5 | appropriate |
| D2.3 · 4 | Service / EndpointSlice debugging | YES — §4 | appropriate |

**Mechanical outline-compliance checks (all pass).** Every one of the outline's 23 `kb_tags.concepts` and all 8 `kb_tags.commands` appear in a named section — none is claimed on adjacency. All 6 planned figure anchors are present. Soundings: 8 planned / 8 present, topics matching. Taking Your Bearings: 16 planned across 6+5+5 / 16 present at 6+5+5, with retrieval tags at 1+2+1 = **4/16 = exactly 25.0%**, the arc outline's ceiling, hit precisely. Practice Questions: 15 planned / 15 present, and the per-section allocation matches the outline's table exactly (§1:2, §2:3, §3:4, §4:3, §5:1, §6:1, §7:1). The watched Soundings Q3 spoiler edge held — its answer names readiness only and does not enumerate both empty-list causes.

**One structural precondition is unverified and is load-bearing for the objective index.** `draft-v1.md` as presented **carries no YAML frontmatter block** — it opens directly at `# Chapter 16: Your Application, Their Cluster`. The `objectives: ["D3.2", "D2.3"]` pair therefore currently exists only in the outline artifact. Shipped chapter-13 left this stage an explicit instruction that *"Unless Ch 16's frontmatter carries `objectives: ["D3.2", "D2.3"]`, the book's objective index will show a substantial slice of D2.3 with no owning chapter."* If frontmatter injection is a later-stage responsibility, this is a non-issue; if it is not, D2.3's deferred slice ends the book unowned. **Verify before the integration stage.** This audit cannot determine which from the artifacts available to it.

---

## Objectives covered in the draft but NOT in the outline

Nothing here is scope creep in the damaging sense. Three items are worth an author decision.

**1. Termination messages (D3.2 · h) — new concept, not in `kb_tags`.** §2 carries a paragraph plus a 🔭 Closer Look on `/dev/termination-log`, correctly sourced twice to `k8s-docs-determine-reason-pod-failure-2026-08-31`. The outline never listed `termination-message` in `kb_tags.concepts`. This is *good* drift — it is one of the seven canonical application-debugging pages and it belongs here — but it is currently invisible to the concept index and to every graded surface. See Finding 2.

**2. D2.2 Security, graded.** Practice **Q9** grades a Pod Security Admission fact (a debug container refused by admission under `restricted`), and §3's ⚠ Navigational Hazard teaches it. The outline planned this explicitly as deliberate cross-domain interleaving, and Ch 12 §6 owns D2.2 — so adding D2.2 to `kb_tags.objectives` would overclaim. **No change recommended.** Recorded so a later stage does not read the mismatch as an error.

**3. D1.2 Administration, one paragraph.** §7's Closer Look on kind / minikube / k3s as local clusters. Cross-beared to Ch 8 §5, proportionate, no action.

**4. `kubectl debug node/` sits on the far side of the chapter's own boundary — by design, at the top of its budget.** The outline's Open Question 5 recommended *"in, at one paragraph, explicitly marked as the moment you step back across the line."* The draft delivers three short paragraphs, a dedicated panel (C) in `ch16-fig02`, a Chapter Summary row, and a Practice Q8 distractor. It is marked as crossing the line twice and reads as an argument *for* the boundary, which is what was asked for — but its total footprint is nearer two paragraphs' prominence than one. **Author confirm** (Open Question 5 requested confirmation and the draft resolved it silently). Recommendation: keep as written; the treatment earns its space.

---

## Depth mismatches

Depth is judged against published weight where one exists, and against the chapter's own allocation where CNCF publishes nothing. **CNCF publishes no sub-competency weights** — every figure below marked *(inferred)* is an even-split estimate for calibration only and must never reach the reader as a published number.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| D3.2 · d — exec / ephemeral / `kubectl debug` | ~8% *(inferred; D3 = 16% published)* | **deep** — §3, 16 min, 4 PQ, 3 TYB, 2 ★ Fixed Points | **OK.** Highest new-material density in the chapter; the only section with no prior-chapter analog. Earns 25% of content time. |
| D3.2 · f — Debug Services | ~8% *(inferred)* | **deep** — §4, 12 min, 3 PQ, 1 ★ | OK |
| D3.2 · c — Debug Init Containers | ~8% *(inferred)* | **deep** — §2, 9 min, 3 PQ | OK on volume; **sourcing is thin under it** (see Gaps item 3) |
| D3.2 · g — Debug a StatefulSet | ~8% *(inferred)* | moderate — §6, 7 min, 1 PQ, 3 TYB | OK. Matches the outline's "proportionate to an advanced-band section with one inbound pointer." |
| D3.2 · i — local debugging | lowest in chapter | shallow — §7, 5 min, 1 PQ | **OK, deliberately.** Shortest content section after the Zenith, exactly as the outline's guardrail required. |
| D3.2 · d — debug **profiles** | low | shallow — 2 paragraphs, 0 graded items, hedged with "include" | **OK.** Deliberately shallow because two cached snapshots conflict on the profile set; the draft flags it. Do not deepen. |
| D3.2 · h — termination messages | low but *named page* | **shallow** — prose only, 0 graded items, absent from `kb_tags`, Exam Alert and Chapter Summary | **under-covered** (index gap, not a teaching gap) |
| D3.2 · b — "running but not doing what I told it to do" | ~8% *(inferred)* | **partial** — §3 covers the runtime half only | **under-covered** — see Finding 1 |
| D2.3 · 1–4 — the four deferred tools | D2 = 28% published; this chapter owns a named sliver | deep — §3 + §4 + §5 = 34 of 64 content minutes | **OK.** Dual-tagged material; the same prose serves D3.2's core. Not double-counting. |
| D1.1 / D2.1 / D2.4 (retrieval only) | owned by Ch 5, Ch 9, Ch 11 | 4/16 TYB + 3/15 PQ draw their *answer* from earlier chapters | **OK — at the ceiling, not over it.** 25.0% exactly, and the outline's "at least three Practice items" floor is met by Q11, Q12, Q14. |

**Nothing is over-covered.** The one candidate — §3 at a quarter of content time — is justified by carrying five of the chapter's Fixed Points and by being the only material in the chapter with no earlier analog.

**One planned interleave did not land.** The outline named four deliberate cross-domain Practice stems. Three are present: Q9 (D2.2), Q14 (D2.4), Q15 (D1.1). The fourth — *"one pairs a Service that selects nothing with the readiness probe that caused it (D2.1 + D1.1)"* — is **absent from the Practice set**. Q10's stem resolves explicitly to selector mismatch and never reaches readiness. The pairing exists only at TYB 2 Q1, which is a Bearings item, not a Practice item. Low severity; the fix is one stem.

---

## Gaps the research stage flagged

The research stage's blocking list discharged cleanly. Every one of the nine fetches the outline's Open Question 2 named as blocking is present in the corpus, plus three unrequested bonuses (`get-shell-running-container`, `ephemeral-containers` concept page, `troubleshooting-applications-index`). No citation in the draft is orphaned. The gap-handling below is what remains.

| Recorded gap | Draft's handling | Verdict |
|---|---|---|
| **Manifest Gaps 1** — the *Debug a StatefulSet* page is a stub with nothing on per-replica PVC, ordinal triage, or peer DNS | §6 built from the Ch 6 / Ch 11 / DNS snapshots as instructed, **and carries an `AUTHOR-REVIEW` saying the sourcing is indirect by necessity** | **Handled correctly.** Model treatment. |
| **Notes 1** — the profile set conflicts between the task page (six, default `legacy`) and the generated CLI reference (five, default `general`) | Draft cites the generated reference as authoritative, introduces the list with *"include"* rather than as complete, and carries an `AUTHOR-REVIEW` naming the conflict | **Handled correctly.** |
| **Notes 4** — no page states the full port-forward path (client → API server → kubelet → Pod); the kubelet hop is inferred | Draft carries an `AUTHOR-REVIEW` saying exactly this, and offers the two remedies | **Handled correctly.** |
| **B1 G33** — CNCF publishes no sub-competency weights | Metadata line labels the ~4% as *"Authored allocation for this chapter"*, with an `AUTHOR-REVIEW` explaining why | **Handled correctly.** |
| **Manifest Gaps 3** — the *Debug Init Containers* page covers **only** status-reading and log access; it has nothing on ordering deadlocks, idempotency hazards, or ConfigMap/Secret mount failures at init | Idempotency **is** sourced (`k8s-docs-init-containers-2026-08-24`, correctly cited). **Ordering deadlock and config-errors-at-init carry no source and no `AUTHOR-REVIEW`** | **Not handled.** See Finding 3. |
| **Manifest Gaps 2 / Notes 5** — the local-debugging page names one tool and contains **no** general framing of what is or is not reproducible locally, which is §7's actual subject | Telepresence is sourced correctly. §7's five-item dividing line — cluster identity, DNS, injected config, admission mutation, Service routing — is **unsourced authorial synthesis with no flag** | **Not handled.** See Finding 4. |
| **Notes on the `debug-pods` re-fetch** | The 08-31 snapshot's own `supersedes` note claims the *"running but not doing what I told it to do"* section "is now present," but the visible snapshot body still stops at *"take a look at it."* The material **is** available in full from `k8s-docs-debug-pods-2026-08-23`, so nothing the draft cites is orphaned | **No citation risk**, but the re-fetch may not have fully landed. Bears directly on Finding 1. |
| `k8s-docs-troubleshoot-kubectl-2026-08-31` self-declares as truncated | Chapter never uses kubeconfig/kubectl-connectivity material — that is Ch 13's | **N/A**, correctly out of scope |

---

## Recommended fixes

Ordered by consequence. Each is scoped to one objective issue.

**Finding 1 — §3 owns "is it configured" but delivers only half of it. `[D3.2 · b, under-covered]`**
§1 promises that "is it configured" is answered in two places, and §3 delivers the *runtime* half well (env shadowing, mount masking, the `ls -la /etc/config/` move). The *API-side* half is missing: the manifest that applied cleanly, errored on nothing, and had a key silently dropped because it was misnested or misspelled. This is a distinct signature — the field is simply **absent from what the server stored**, so `exec` cannot help you; the container is faithfully running the spec that actually exists. It is documented and cited-ready: *"Often a section of the pod description is nested incorrectly, or a key name is typed incorrectly, and so the key is ignored… compare `kubectl get pods/mypod -o yaml` against the original"* [source: k8s-docs-debug-pods-2026-08-23].
**Fix:** add a 🪝 Snag to §3 after *"The manifest is a statement of intent; the container's filesystem and environment are the outcome"* — teaching the **round-trip comparison** (apply, then diff `kubectl get pod <name> -o yaml` against what you wrote). Add a concept such as `silently-dropped-manifest-field` to `kb_tags.concepts` and one Chapter Summary row.
**Caution:** the snapshot's prose also names the `--validate` flag. kubectl's field-validation behaviour has moved across releases. Teach the round-trip comparison (version-stable) and either omit the flag or verify its current form against a fresh snapshot before it reaches print.

**Finding 2 — termination messages are taught but not indexed or graded. `[D3.2 · h, under-covered]`**
"Determine the Reason for Pod Failure" is one of the seven canonical D3.2 pages. The draft teaches it correctly and cites it twice, but it appears in no `kb_tags` entry, no Exam Alert row, no Chapter Summary row, and no graded item — so the objective index will not show it as owned anywhere.
**Fix (minimal, preferred):** add `termination-message` to `kb_tags.concepts` and one Chapter Summary row (*"A container can write a one-line fatal reason to `/dev/termination-log`; Kubernetes surfaces it in Pod status, so a failure stays legible from `describe` alone"*). Do **not** expand the prose — the current two-paragraph treatment is correctly proportionate.

**Finding 3 — §2's ordering-deadlock and config-error material rests on a recorded research gap, unflagged. `[D3.2 · c, sourcing]`**
Two of §2's "three ways an init container is wrong" carry no source tag, against a gap the manifest recorded explicitly. The ordering deadlock is nonetheless a **sound deduction from three separately sourced facts** — init containers block app containers, a Pod is not Ready until init succeeds, and readiness gates endpoint membership — so the content is not in question, only its provenance.
**Fix:** add an `AUTHOR-REVIEW` to §2 mirroring §6's, naming manifest Gaps item 3; and present the deadlock as a consequence of the sourced sequencing rules rather than as documented behaviour (one clause: *"which follows from the sequencing rules above"*). Config-errors-at-init is the weaker of the two — `k8s-docs-determine-reason-pod-failure-2026-08-31` carries `config-errors-visible-at-init` in its concept tags but its transcribed body is termination-message material. Either source it properly or mark it as authorial.

**Finding 4 — §7's dividing line is unsourced synthesis and is the chapter's one unflagged gap. `[D3.2 · i, sourcing]`**
The five-item list of what cannot be reproduced locally is §7's entire teaching payload, and the manifest recorded twice that no cached page contains this framing. The draft flagged the equivalent situation in §6 and did not flag it here.
**Fix:** add an `AUTHOR-REVIEW` to §7 stating that the dividing line is authorial synthesis, that the cached page supports only the Telepresence pattern, and that each list item is individually established by earlier chapters. No prose change — the content is right and the depth ruling was followed.

**Finding 5 — two exam-weight claims in "Why This Chapter Matters" have no supporting snapshot. `[curriculum-authority]`**
The draft asserts *"That domain doubled from the previous blueprint"* and *"prep material written against the old five-domain shape."* The cached CNCF snapshot carries **only the current four weights** — it says nothing about a prior blueprint or a five-domain shape. Both claims trace to B1, which is a book artifact, not a dated snapshot, and the chapter's own convention tags weight claims to snapshots (as the adjacent 16% figure correctly does).
**Fix:** tag both to B1 explicitly, or cut them. This is the one place the chapter states something about the exam blueprint that its authority cannot support, and it is the kind of claim a reader will repeat.

**Finding 6 — one planned cross-domain interleave is missing from the Practice set. `[D2.1 + D1.1, coverage]`**
**Fix:** revise **Q10** so the stem pairs an empty endpoint list with the readiness probe that caused it (Pods present under the selector, all `0/1 READY`), or add a sixteenth item doing so. Q10's current form duplicates TYB 2 Q1's discriminator in reverse and is the weakest of the three §4 items.

**Finding 7 — verify frontmatter materialization before integration. `[D2.3, index integrity]`**
Confirm that `objectives: ["D3.2", "D2.3"]` reaches the chapter file itself and not only the outline. Ch 13 named this as the condition on which a substantial slice of D2.3 has an owning chapter. If frontmatter is injected by a later stage, record that here so the question is not re-opened.

---

*Out of this stage's lane, noted once because it is cheap to fix and a later gate will catch it:* the Attention Budget table's rows sum to **80 minutes**, against a stated header total of **~75 minutes**.