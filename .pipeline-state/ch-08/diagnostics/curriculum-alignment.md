# Curriculum-Alignment Audit — KCNA Chapter 8

**Draft audited:** `.pipeline-state/ch-08/draft-v2.md` (voiced in place; 1224 lines; 2026-08-24T20:09)
**Objective authority:** `sources/cncf-kcna-curriculum-pdf-2026-08-23.md`, corroborated by `sources/cncf-kcna-certification-page-2026-08-23.md`
**Objective decomposition:** `book-outline/domain-analysis.md` §D1.2 (17 concept rows, L106–126) + `book-outline/arc-outline.md` §Chapter 8 *Covers* (L181, 11 further mechanisms)

**Locator convention.** `draft-voice.md` does not exist because the voice stage writes in place; the voiced artefact is `draft-v2.md`, with `draft-v2-prevoice.md` as the backup. All line cites are against `draft-v2.md`.

**Numbering caveat, stated once.** CNCF publishes **four domain weights and twelve named competencies, with no numbering and no sub-competency weights** (`cncf-kcna-curriculum-pdf-2026-08-23.md:13`). `D1.2` is a Lodestar convention, declared as such at `domain-analysis.md:33`, and gap **G33** records that no authoritative basis exists for splitting D1's 44% across its four competencies. The `D1.2-NN` sub-IDs below are **this audit's** decomposition, carried forward unchanged from the Chapter 8 pass of 2026-08-24 for comparability. They are not a CNCF taxonomy and must not leak into shipped text.

---

## ⚠ The corpus changed since the last pass — read this before the tables

The previous curriculum-alignment run (2026-08-24T19:34, against `draft-v1.md`) found that the research stage had completed its ten fetches but never landed them on disk, leaving the snapshots as string literals inside an unexecuted writer script in `research-manifest.md`. The drafting stage read that finding and, correctly, narrowed §2, §3, §4, §5, §7 and several answer keys back to what the pre-research corpus could carry — recording each retreat in an inline `AUTHOR-REVIEW` comment.

**That situation no longer holds.** Verified this pass:

- `research-manifest.md` was rewritten at 2026-08-24T21:15 and is now a clean manifest — snapshot table, "already cached" table, and six gaps G-8A…G-8F.
- All ten snapshots exist in `sources/`, all written 2026-08-24T21:15, all non-empty (928–5093 bytes).
- All ten are in **this chapter's referenced snapshot set** (32 snapshots supplied to this stage), together with `cncf-kcna-curriculum-pdf-2026-08-23`, `k8s-docs-taints-tolerations-2026-08-23` and `k8s-docs-resource-management-2026-08-23`.

**Consequence for this audit.** `draft-v2.md`'s thirty `AUTHOR-REVIEW` comments are stale, and several now assert things that are false against the current corpus — the §2 comment at L233 says "`sources/` contains none of them"; the §3 comment at L330–334 says both closing fetches are "sitting unwritten in `research-manifest.md`"; the metadata comment at L8 says the string "Kubernetes Fundamentals" appears in no referenced snapshot. All three are wrong now. The 2026-08-30 fact-accuracy pass reaches the same conclusion independently.

So the finding has inverted. Last pass, the chapter was **over-claiming against a thin corpus**. This pass, after an honest and correct retreat, the chapter is **under-covering against a corpus that is now adequate**. Four objectives sit below the depth their examinability justifies, and the evidence to lift every one of them is already on disk. **No fetch is required to close anything in this audit except one item** (the managed/self-hosted duty split, §5), which is not closable from kubernetes.io at all.

---

## Objectives the outline claims to cover

The outline claims exactly one competency: **D1.2 — Administration** (frontmatter `objectives: ["D1.2"]`, applied uniformly to all eight sections). Twenty-eight auditable sub-objectives: 17 from B1's concept map, 11 added by the arc outline's *Covers* line.

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| D1.2-01 | Cluster planning axes — local vs HA, hosted vs self-managed, on-prem vs IaaS, bare metal vs VM, user vs contributor | YES (§5 L548–558) | appropriate |
| D1.2-02 | Managed vs self-hosted — who owns the control plane | YES (§5 L560–568, L580–603) | **shallow — source-blocked** |
| D1.2-03 | Resource quota — per-namespace division of cluster resources | YES (§3 L326, L338–347) | **shallow — now closable** |
| D1.2-04 | Controlling access to the API — the three **sequential** gates | YES (§2 L225–319) | appropriate — sequencing still untagged |
| D1.2-05 | Authentication — establishing *who* | YES (§2 L239–245) | appropriate |
| D1.2-06 | Authorization — may this identity perform this action | YES (§2 L247–253) | appropriate — "one authorizer among several" wrongly cut |
| D1.2-07 | Admission controllers — intercept before persistence; may mutate or reject | YES (§2 L255–301) | appropriate — mutation still untagged |
| D1.2-08 | Auditing — recording the sequence of activities affecting the cluster | **PARTIAL** (§2 L302–306) | **shallow — named, not defined** |
| D1.2-09 | TLS bootstrapping — how a kubelet obtains its client certificate | YES (§2 L243) | appropriate (one clause) |
| D1.2-10 | Control-plane ↔ node communication — hub-and-spoke, one door | YES (§2 L310–316) | appropriate |
| D1.2-11 | Semantic versioning — `x.y.z` | YES (§6 L675–677) | appropriate |
| D1.2-12 | Supported versions — three minor branches, ~1 year patch support | YES (§6 L677–679) | appropriate |
| D1.2-13 | Version skew — kubelet (never newer; up to three older) | YES (§6 L691–705, L723–735) | deep — justified |
| D1.2-14 | Version skew — kube-proxy | YES (§6 L691–705) | appropriate |
| D1.2-15 | Version skew — controller-manager / scheduler / CCM | YES (§6 L691–705) | appropriate |
| D1.2-16 | Version skew — kubectl (one minor, either direction) | YES (§6 L691–705, L723–735) | deep — justified |
| D1.2-17 | Version skew — HA apiservers within one minor | YES (§6 L691–705, L720) | appropriate |
| D1.2-18 | `kubectl` syntax and verbs (arc *Covers*; gap **G1**) | YES (§1 L132–198) | deep — justified |
| D1.2-19 | kubeconfig and its precedence (arc *Covers*; **G1**) | YES (§1 L199–206) | appropriate |
| D1.2-20 | In-cluster authentication and the ServiceAccount namespace (**G1**) | YES (§1 L207–214) | appropriate |
| D1.2-21 | Bootstrap tooling — kubeadm, minikube, kind, k3s (**G28**) | YES (§5 L560–579) | appropriate |
| D1.2-22 | LimitRange — per-object constraint and defaulting (arc *Covers*) | YES (§3 L328, L336–374) | **shallow — now closable** |
| D1.2-23 | Node lifecycle — cordon / drain / uncordon (**G26**) | YES (§4 L461–491) | deep — justified |
| D1.2-24 | Node conditions — Ready (three-valued), Disk/Memory/PID/Network | YES (§4 L492–515) | appropriate — **miscited, see G-8B** |
| D1.2-25 | Node heartbeats — `.status` updates and `kube-node-lease` Leases | YES (§4 L516–525) | appropriate |
| D1.2-26 | Node registration and the node controller's three jobs | YES (§4 L453–460, L520–524) | appropriate |
| D1.2-27 | Release cadence — ~3 minor releases/year, ~15 weeks, monthly patches | YES (§6 L681–689) | appropriate |
| D1.2-28 | etcd backup and restore (**G27**) | YES (§7 L749–794) | appropriate |

**Totals: 27 covered, 1 partial, 0 uncovered.** Every `kb_tags.concepts` entry in the outline frontmatter appears in the draft.

**Scope boundaries hold, verified by search.** Konnectivity, SSH tunnels, feature gates, `kubectl top`, `kubectl events`, `kubectl debug`, `port-forward`, ephemeral containers, PodDisruptionBudgets, `--ignore-daemonsets` and metrics-server are all **absent**. The only two matches for Chapter 12 material (`ClusterRoles` at L251, `encryption at rest` at L791) are cross-bearing pointers, which the outline explicitly authorised. This is the cleanest scope discipline of any chapter audited so far.

**Note on D1.2-22 (LimitRange).** It is not in B1's D1.2 concept map — B1 attests only "Resource quota." It enters via the arc outline's *Covers* line and via two published cross-bearings (`chapter-04` L590, `chapter-07` L430), so it is an outline-authorised addition rather than drift. The reason B1 omitted it was corpus thinness at the time; `k8s-docs-limit-range-2026-08-24.md` has since closed that.

---

## Objectives covered in the draft but NOT in the outline

Drift remains very low, and **two of the four items the last pass raised are now resolved**.

**1. Node `Capacity` / `Allocatable` — §4 L526–539. Still the one item needing an author decision, but for a different reason than last time.**
The primary snapshot `k8s-docs-node-allocatable-2026-08-24.md` is tagged `objectives_covered: ["D1.3"]` — Scheduling, not Administration — while the research stage tagged the same source page D1.2 for this chapter. The material sits on a competency boundary and is now touched in both Chapter 7 §2 and Chapter 8 §4. What changed: draft-v1's unsourced arithmetic gloss ("what is left after the node's own overheads are set aside") has been **cut**, correctly, per G-8E. What did not change: the Chapter 7 §2 promise — *"what makes the two differ, and how it's configured, is Chapter 8's material"* — is now **wholly unpaid**. Three sentences that assert the two numbers differ, without saying why, is a weaker discharge than draft-v1's incorrect one. `k8s-docs-reserve-compute-resources-2026-08-24.md` closes this at the outline's own recommended option (b). See Recommended fixes #4.

**2. Verb-table forward rows — §1 L171–182. RESOLVED.** The last pass flagged a column headed *"Where you met it"* containing rows reading "Ch 13," a chapter four ahead. The column is now *"Where it lives in this book"* and those rows read "ahead, in Ch 13." The label bug is fixed and the promise is now correctly framed as a forward pointer. No action.

**3. `Extended Analogy` in §2 (harbour pilot / harbourmaster / customs officer), L~275–281.** Not in the outline's planned marker list for §2. It introduces no objective content and carries the mutate-vs-reject distinction well. **Marker inventory is the theming-density stage's lane — no action here.**

**4. DaemonSet toleration *mechanism* — §4 L489.** The outline planned "one exception worth naming"; the draft adds the mechanism, cited to `k8s-docs-daemonset-2026-08-24`. Sourced, one clause, and it pays a Chapter 6 retrieval. **Keep.**

**5. Upgrade order as an Exam Alert priority topic — §6 L737–743, Exam Alert item 9.** The outline planned ten priority topics; the draft ships eleven, the addition being "upgrade the API server first." The outline did instruct §6 to "close on the upgrade order that falls out of the rules," so the content is authorised; only its promotion to the priority list is new, and it is defensible — it is the one derivable item in the chapter's densest recall block. **Keep.**

**6. Skew-rule arithmetic corrected against the outline — §6 L671, Bearings #3 item 2 (L806).** The outline specifies "the one rule that generates **four of the five** rows." The draft says **three of five**, and names two exceptions rather than one: `kubectl` (a user tool outside the cluster, symmetric window) and the HA kube-apiserver row (a mutual bound *between* API servers, not a bound *relative to* one). **The draft is right and the outline is wrong.** "Nothing may be newer than the API server" generates kubelet, kube-proxy, and controller-manager/scheduler/CCM — three rows. Recording this explicitly so a later reconciliation pass does not revert the draft to the outline's number. See Recommended fixes #9.

Nothing else reaches beyond the outline. §8's use of the D1.3-tagged taints snapshot, Practice Q7's crossing into requests/limits, and the Voyage Ahead's D2.1 preview are all outline-specified retrieval or structural handoff.

---

## Depth mismatches

**On the weight column.** Rule 2 asks depth to be judged against exam weight. CNCF publishes weight at **domain level only**: D1 Kubernetes Fundamentals is 44%, and its four competencies carry no published split (G33). There is therefore no per-objective weight to measure against, and inventing one would be exactly the error G33 exists to prevent. The column below states the published domain weight, then names the chapter's **own** Exam Alert priority rank as the proxy for examinability — authored judgement, declared as such, which is the same disclosure discipline the shipped metadata line uses.

| Objective | Exam weight | Draft depth | Mismatch |
|---|---|---|---|
| D1.2-04 / -07 gates + admission mutation | D1 44%; Exam Alert **#1, #2** | deep (95 lines, figure, 4 markers) | **OK** — best-taught block in the chapter; sequencing/mutation need tagging only |
| D1.2-13 / -16 version skew | D1 44%; Exam Alert **#3, #4** | deep (84 lines, Dead Reckoning table, figure, derived from one rule) | **OK** — and the derivation is the right pedagogy for a decay-risk block |
| D1.2-12 / -27 supported releases + cadence | D1 44%; Exam Alert **#5** | appropriate | OK |
| D1.2-23 cordon / drain / uncordon | D1 44%; Exam Alert **#6** | deep (31 lines, figure, Hazard, Mnemonic) | **OK** — trap has a real operational cost |
| D1.2-24 node conditions | D1 44%; Exam Alert **#7** | appropriate | OK on depth; **miscited** — see G-8B |
| D1.2-03 ResourceQuota | D1 44%; Exam Alert **#8**; 1 of B1's 17 D1.2 rows | 2 paragraphs; scope, counting and rejection all absent | **under-covered** |
| D1.2-22 LimitRange | D1 44%; Exam Alert **#8**; two published cross-bearings | 1 paragraph + contrast; min/max/default structure absent | **under-covered** |
| D1.2-18 kubectl verbs + grammar | D1 44%; Exam Alert **#10**; gap G1 | deep (67 lines, table, 5 subsections, figure) | mild over-coverage — **accept**, it discharges "kubectl, in full" and G1 |
| D1.2-28 etcd backup | D1 44%; Exam Alert **#11** | appropriate (46 lines) | OK |
| D1.2-08 Auditing | D1 44%; not on the priority list; 1 of B1's 17 rows | 2 sentences, no definition asserted | **under-covered** |
| D1.2-02 managed vs self-hosted | D1 44%; not on the priority list | existence of a split only; no duty named | **under-covered — source-blocked, not a draft failure** |
| Capacity / Allocatable (boundary) | D1.3-tagged snapshot; Ch 7 §2 promise | 3 sentences; the "why" absent | **under-covered against a published promise** |
| D1.2-01 planning axes | not on the priority list | 5 questions, verbatim | OK — correctly the chapter's light section |
| D1.2-21 bootstrap tooling | not on the priority list | appropriate (recognition tier, as specified) | OK |

**No objective is over-covered enough to warrant trimming.** §1's kubectl block is the only candidate, and it is discharging a blocking gap (G1) plus a chapter-scoped published promise, which is what the outline asked for.

### Practice-question allocation is mismatched against examinability

This is a depth question rather than a question-quality question, so it belongs here. Counted: Soundings **8** (budget 8 ✓), Bearings **15** across three checkpoints (budget 15 ✓), Practice **18** (budget **17** — one over). Chapter total 41 against a budgeted 40.

Distribution against the outline's plan:

| Block | Planned | Shipped | Delta |
|---|---|---|---|
| §1–§2 — grammar, kubeconfig, the gates | 5 | 4 (Q1–Q4) | −1 |
| §3 — quota and LimitRange | 2 (→3 if fetch landed) | 3 (Q5–Q7) | ✓ at the raised figure |
| §4 — node lifecycle and conditions | 3 | 4 (Q8–Q11) | **+1** |
| §5 — ownership and bootstrap tooling | 2 | 2 (Q12–Q13) | ✓ |
| §6 — versions and skew | 4 | 3 (Q14–Q16) | **−1** |
| §7 — etcd | 1 | 1 (Q17) | ✓ |
| §8 — synthesis (outline-specified interleave) | — | 1 (Q18) | authorised |

**§6 is one item short while §4 is one item over.** §6 owns three of the chapter's top five priority topics and is the block `[B3]` names as the book's worst decay risk; §4 owns one. The outline's requirement that "at least 2 [of §6's items] must require applying a rule to a scenario rather than reciting the rule" is currently met by Q14 and Q16 with no margin. See Recommended fixes #7.

---

## Gaps the research stage flagged

`research-manifest.md` records six chapter-level gaps. The four arc-outline blocking gaps are separately resolved.

| Gap | Status | Draft handling |
|---|---|---|
| **G1** kubectl command surface | **CLOSED** for this chapter | §1 covers grammar, verbs, kubeconfig, in-cluster auth. `top`/`events`/`port-forward`/`debug` correctly deferred to Ch 13/16 and absent |
| **G26** node lifecycle | **CLOSED** | §4, deep |
| **G27** etcd backup | **CLOSED** | §7, appropriate |
| **G28** bootstrap tooling | **CLOSED** | §5, appropriate |
| **G-8A** `cordon` not linked to the `unschedulable` taint by any single source; affects a stated answer key | **HANDLED CORRECTLY** | Bearings #2 item 1 (L608) was reworded to the manifest's recommended option (a): name the taint, say what `cordon` does. The unsourceable "what command *applies* it" framing is gone. **However** the draft's own comment at L627 claims the `NoSchedule` semantics are unavailable — that is stale; `k8s-docs-taints-tolerations-2026-08-23` is in this chapter's set and carries them |
| **G-8B** citation drift — conditions table attributed to the concept page, which no longer carries it | **NOT HANDLED** | §4 L504–514 still cites `k8s-docs-nodes-2026-08-23` for the conditions table, three-valued `Ready`, and Capacity/Allocatable/Info. The manifest warned that a downstream audit would read this as a false positive. See fix #6 |
| **G-8C** quota per-row descriptions not verbatim-verified | **HANDLED BY ABSENCE** | §3 enumerates nothing yet. Carry the constraint forward into the §3 rebuild: name the countable resources, never quote a row description |
| **G-8D** audit level definitions not captured | **HANDLED CORRECTLY** | Levels, stages and backends all absent from §2. Keep them out — above budget regardless |
| **G-8E** Capacity→Allocatable arithmetic unextractable | **HANDLED CORRECTLY — the draft's clearest improvement over v1** | The arithmetic gloss was cut at §4 L532. Constraint must survive fix #4: name the reservations, state no equation |
| **G-8F** deliberate non-fetches (Konnectivity, SSH tunnels, feature gates, RBAC/PSS/encryption detail, Ch 13/16 verbs, quota scopes, kubeadm runbooks) | **VERIFIED ABSENT** | Search-confirmed. No oversight to report |
| **G33** sub-competency weights unpublished | **DISCLOSED CORRECTLY** | Metadata line L4 + inline disclaimer L6. The three underlying claims (domain name, domain count, 44%) are now taggable to `cncf-kcna-curriculum-pdf-2026-08-23:13`; that tagging is the fact-accuracy stage's fix, noted here once and not duplicated |

### One new gap to open

**G-8G — the managed vs self-hosted duty split has no vendor-neutral authority.** `k8s-docs-setup-tooling-2026-08-23` licenses only the *existence* of a split ("consider which aspects of operating a Kubernetes cluster you want to manage yourself and which you prefer to hand off to a provider"). It does not name which duties move, and kubernetes.io does not document commercial providers' responsibility models, so **no fetch from that doc tree will close this**. The draft handled it correctly by narrowing (§5 L586) and by rewriting Practice Q13's axis from "which duties does a provider take over" to "which duties belong to whoever operates the control plane" — the second is sound on the architecture alone. Per Rule 3 this is a research-stage gap, not a curriculum-alignment failure. It should be **recorded in `research-manifest.md`** so it is not rediscovered in Chapter 13 or 17, both of which touch operational ownership.

---

## Recommended fixes

Ordered by leverage. **Fixes 1–6 require no fetch** — every source named is already in `sources/` and in this chapter's referenced set.

**1. D1.2-08 Auditing: PARTIAL → covered.** Replace §2 L304–306 with three or four sentences tagged to `k8s-docs-audit-2026-08-24`: the definition ("Kubernetes *auditing* provides a security-relevant, chronological set of records documenting the sequence of actions in a cluster"), a compressed gloss of the questions it answers, and the clause that "Audit records begin their lifecycle inside the kube-apiserver" with every request generating an event at each stage of execution. That last clause is the single-door architecture stated a fourth way and costs nothing in a section built on it. Keep stages, levels and backends out — above budget, and G-8D confirms the level definitions were never verbatim-captured. Delete the stale comment at L308.

**2. D1.2-03 / D1.2-22 ResourceQuota + LimitRange: shallow → appropriate.** Rebuild §3 L326–334 on `k8s-docs-resource-quotas-2026-08-24` and `k8s-docs-limit-range-2026-08-24`, taking exactly four things and no more:
   1. what a quota counts — compute totals, object counts, storage (**names only**, per G-8C);
   2. the `403 Forbidden` rejection;
   3. the rule that in a quota'd namespace every new Pod **must** specify requests or limits — the most examinable fact available to this section, and the causal link between its two mechanisms;
   4. LimitRange's min/max/default structure, its automatic injection of defaults, and that "validations occur only at Pod admission stage, not on running Pods."

   This also resolves the internal inconsistency the draft flags at L371: item 3 settles it in favour of "the quota refuses it," so the ⚓ Worth Securing callout can be rewritten to say so outright. Figure 8.3's `min ≤ … ≤ max` per-Pod bound resolves in the **figure's** favour — bring the prose up, do not cut the figure down. Scope guard unchanged: no quota scopes, scope selectors, priority-class quota, or the full countable-resource roster.

**3. D1.2-04 / -06 / -07 gates: asserted → tagged, plus two free upgrades.** Tag §2's Fixed Point (L285), Figure 8.2's caption (L296), and the dependent keys in Bearings #1 items 3–4 and Practice Q2–Q4 to `k8s-docs-controlling-access-2026-08-24`, which states the ordering, the mutation power ("Admission Control modules … can modify or reject requests"), and the persistence boundary ("Once a request passes all admission controllers, it is validated … and then written to the object store"). Tag the ResourceQuota/LimitRanger/NodeRestriction-as-admission-plugins claim at L296 to `k8s-docs-admission-controllers-2026-08-24`. Two upgrades available at no cost: the **quorum contrast** (authorization = any module approves and the request proceeds; admission = any module rejects and the request is refused immediately), which is a sharper Navigational Hazard than the one at L292 and which the source draws itself; and **"admission does not see reads"**, one clause that forecloses a plausible misreading. Restore the clause cut at L253 — controlling-access names ABAC, RBAC and Webhook modes, so "RBAC is one authorizer among several" is now sourced. The mutating/validating phase split stays out: the outline never asked for it and Chapter 12 does not need it.

**4. Capacity / Allocatable: pay the Chapter 7 promise.** Add two sentences after §4 L532 from `k8s-docs-reserve-compute-resources-2026-08-24` — the motivation ("Pods can consume all the available capacity on a node by default. This is an issue because nodes typically run quite a few system daemons that power the OS and Kubernetes itself") and the two reservation names, `kubeReserved` and `systemReserved`. That is the outline's Open Question #6 at its recommended option (b), discharged honestly. **No arithmetic** — G-8E stands regardless. This also shortens the block relative to draft-v1 and relieves the duplication against Chapter 7 §2.

**5. §8's cordon→spec derivation: narrowed → restorable, and it fixes the retrieval rate.** `k8s-docs-node-status-2026-08-24` carries "cordoned nodes are marked Unschedulable in their spec" verbatim. Restore the §8 L866–872 derivation on that citation, and restore **Practice Q10** to its spec-vs-status framing with its `[retrieval: ch4]` tag. Add the adjacent sentence — "`SchedulingDisabled` is not a Condition in the Kubernetes API" — as a 🪝 Snag in §4's conditions subsection: the thing `kubectl` prints is not a thing the API has, which is a ready-made spec/status discrimination.

**6. G-8B citation repoint.** In §4, move the citations for the conditions table (L504–514), the three-valued `Ready`, and Capacity/Allocatable/Info from `k8s-docs-nodes-2026-08-23` to `k8s-docs-node-status-2026-08-24`. Keep the 08-23 file for node registration, cordon/drain/uncordon, heartbeats and the node controller — it remains correct for those. Optional and consistent with the outline's own standing rule: add `node-monitor-grace-period`'s documented default of **50 seconds** as a dated illustration, never as the examinable fact.

**7. Rebalance one Practice item from §4 to §6.** §4 ships four items against a plan of three; §6 ships three against a plan of four while owning Exam Alert topics #3, #4 and #5. Fold or retire one §4 item (Q9 and Bearings #2 item 3 test the same `Ready: Unknown` discrimination) and add a §6 scenario item — an application question, not a lookup, per the outline's calibration note. That also returns the set to its 17-question budget.

**8. Correct the retrieval-accounting denominator.** The comment at L1159 computes against a pool of 34. The actual Bearings + Practice pool is **33** (15 + 18), so tagged retrieval currently stands at 6/33 = 18.2%, not 17.6% — still below the 20% floor either way. Restoring Q10's `[retrieval: ch4]` tag under fix #5 gives 7/33 = **21.2%**, which clears it. Both ≥4-back floor items are intact: Bearings #2 item 4 (Ch 2, six back) and Practice Q11 (Ch 3, five back). Flagging the arithmetic so the question-quality stage is not working from a wrong denominator.

**9. Keep "three of five," and correct the outline.** §6's generating rule accounts for kubelet, kube-proxy and the controller-manager/scheduler/CCM row. `kubectl` and the HA kube-apiserver row are both exceptions, for different reasons. The arc outline and the chapter outline both say "four of five"; the draft says three and is right. Record the correction in the outline rather than in the draft, so a reconciliation pass does not revert it.

**10. Record G-8G in `research-manifest.md`.** Either open a research gap for a vendor-neutral shared-responsibility source, or ratify the narrowed form permanently. If ratified, Soundings answer 8 (L96) should be trimmed the same way §5 L586 and Practice Q13 already have been — it still enumerates five duties as if the split were documented.

**11. Delete the thirty `AUTHOR-REVIEW` comments as each fix lands.** They are a to-do list, not a description of the evidence, and several now assert falsehoods about the corpus (L8, L233, L253, L298, L308, L330–334, L534–536, L627, L1118, L1159). Two of them are also closable outright with no prose change: **L1118** — "requests are the number the scheduler filters on" is sourced by `k8s-docs-resource-management-2026-08-23` ("the kube-scheduler uses this information to decide which node to place the Pod on"); **L627** — the `NoSchedule` semantics are sourced by `k8s-docs-taints-tolerations-2026-08-23`, which needs only to be cited, not fetched.

---

## Verdict

**Curriculum alignment passes.** Twenty-seven of twenty-eight sub-objectives covered, one partial, none missing; every banned topic absent; drift limited to one boundary item that the outline itself anticipated. The chapter covers what it claims to cover.

The work outstanding is **depth, not coverage**, and it is unusually cheap: four under-covered objectives, all closable from snapshots already on disk, plus one citation repoint and one question rebalance. The single item that cannot be closed from the cached corpus — the managed/self-hosted duty split — has already been correctly narrowed in the draft and needs recording rather than rewriting.