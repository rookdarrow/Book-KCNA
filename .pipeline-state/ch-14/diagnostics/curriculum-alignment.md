I audited the draft against the cached CNCF/LF objective snapshots, the outline's authored sub-objective claims, and the outline's own budgets. Output follows (stdout, per stage contract).

---

# Curriculum-Alignment Audit — KCNA Chapter 14

## Authority note (read before the tables)

The only objective granularity CNCF publishes for this domain is the **competency name**. `cncf-kcna-curriculum-pdf-2026-08-23` (line 15) and `lf-kcna-exam-page-2026-08-23` (line 43) both resolve to *"Cloud Native Application Delivery 16% — Application Delivery; Debugging"* and stop. Neither contains the string "Helm" or "Kustomize"; neither does `lf-lfs250-course-outline-2026-08-31`, which exists in the corpus specifically as negative evidence.

Consequences for this audit, stated once:

1. **Sub-objective IDs below `D3.1` are authored**, taken from the outline's own section-level ownership claims. They are not CNCF identifiers and must not be treated as such downstream.
2. **Depth-versus-weight cannot be assessed against a published figure.** The published 16% covers Ch 14–16 jointly; the 5-point allocation to Ch 14 is authored (B1 gap G33, B2 disclosure #1). Every depth judgment below is therefore made against the *authored* allocation and the outline's own budgets, not against CNCF. This is a limit of the source base, not a defect in the draft.
3. The draft handles this correctly and prominently — the mandatory honesty beat is present in Why This Chapter Matters, carries three source tags, and states the inference plainly. **Open Question 2 is discharged.**

---

## Objectives the outline claims to cover

| Objective ID | Description | Covered in draft? | Depth |
|---|---|---|---|
| **D3.1** | **Application Delivery** (published competency name; 16% domain, authored 5-pt chapter allocation) | **YES** | **appropriate overall** |
| D3.1-a *(authored)* | Why declarative manifests stop scaling: the four named failures | YES — §1, all four named and demonstrated; closed arithmetically in §6 | appropriate |
| D3.1-b *(authored)* | Helm chart anatomy: `Chart.yaml`, `values.yaml`, `templates/`, `charts/`, `crds/`, `NOTES.txt`, `_helpers.tpl`, subcharts | YES — §2, every entry explained by purpose | appropriate |
| D3.1-c *(authored)* | Chart / Helm release / release revision as three distinct things | YES — §3, two Fixed Points, figure, extended analogy | deep — correctly so; this is the chapter |
| D3.1-d *(authored)* | `helm rollback` vs `kubectl rollout undo` | YES — §3 Fixed Point, three-axis split, mnemonic, PQ8/PQ9 | appropriate; **one fact unresolved, see Gaps** |
| D3.1-e *(authored)* | Chart distribution: chart repositories, OCI registries | YES — §4 | slightly deep (see mismatches) |
| D3.1-f *(authored)* | Chart `version` vs `appVersion` | YES — §4, mnemonic, TYB1 Q5, PQ13 | appropriate |
| D3.1-g *(authored)* | Kustomize: template-free, `apply -k`, base and overlay | YES in prose — §5, Fixed Point + figure | appropriate in prose, **thin in graded text** |
| D3.1-h *(authored)* | Strategic-merge vs JSON 6902 patches | YES — §5, one clause each, PQ15 | appropriate for tier; **sourcing weak** |
| D3.1-i *(authored)* | `configMapGenerator` / `secretGenerator` | **partial** — one prose paragraph, **zero graded items anywhere** | shallow |
| D3.1-j *(authored)* | Choosing between them (distribute vs adapt) | YES — §6, decision figure, four-failure closure table | appropriate |
| D3.1-k *(authored)* | `crds/` and the CRD ordering problem, with its limits | YES — §6, best-sourced section in the chapter | deep; justified (discharges chapter-06:1036) |
| D3.1-l *(authored)* | Go templating in Helm | YES — one templated line beside its render, then stop | **correctly calibrated** — Open Question 8's recommendation followed exactly |
| D3.2 | **Debugging** (the domain's other published competency) | Not claimed, not covered | correct — belongs to Ch 16 |

No objective the outline claims is absent from the draft. Coverage is complete at the claimed granularity.

---

## Objectives covered in the draft but NOT in the outline

Ordered by size of expansion. None is a curriculum failure; item 1 is the only one warranting an author decision.

**1. Helm 2 → Helm 3 migration surface (moderate expansion — author decision).**
The outline authorized *one* thing here: a Tiller trap in the Exam Alert, conditional on a source fetch (Open Question 5). The fetch landed (`helm-changes-since-helm2-2026-08-31`, the richest snapshot in the chapter's corpus) and the draft drew on it far more broadly. Current footprint:

- §2 — `requirements.yaml` consolidation (clause); ⚓ Worth Securing on the `apiVersion` v1→v2 bump (full callout)
- §3 — install name now mandatory + `--generate-name`; release-name namespace scoping with explicit Helm 2 contrast; `helm list` default-scope change
- §4 — two paragraphs on chart-repository drawbacks and the Distribution project's history, as rationale for the OCI shift
- Exam Alert — Tiller row plus two follow-up paragraphs
- **Graded: PQ6 distractor A (Tiller), PQ10 (Helm 2 auto-naming) — 2 of 17 practice questions**

Judgment: the *namespace-scoping* change is load-bearing (§3's release model depends on it) and the *Tiller* trap is genuinely valuable — it connects to B2 disclosure #3 and gives the reader a mechanical test for outdated study material, which is exactly the honest register this chapter established. The `helm list` default and the `apiVersion` bump are the trimmable ones. Recommend keeping the thread, trimming the two weakest touches, and adding a `helm-2-to-helm-3` concept to `kb_tags` so the index stops under-claiming a topic the chapter now teaches.

**2. `helm push` and OCI push-reference syntax (declared-command drift).**
Demonstrated in §4 and *graded* in PQ17. `helm push` is absent from the outline's `commands` list — a list the outline built deliberately short, with an explicit standing rule: *"If drafting demonstrates one of them, add it here rather than letting the concept index under-claim."* This is that case. Add `helm-push`.

**3. `helmCharts` chart-inflation generator (§5 Closer Look).**
The outline authorized "both together" at name-only depth, in §6. The draft has a §5 Closer Look plus the §6 paragraph. The Closer Look self-labels as beyond exam scope, which is the correct hedge. Acceptable as written; do not grow it.

**4. `HELM_DRIVER` and its three backends (§3 Worth Securing).**
Open Question 3(b) authorized the *fact* (release state in Secrets, in the release namespace). The draft adds the env var and the `configmap | secret | sql` value set. Well-sourced, one clause, harmless. No action.

**5. Chart archive** (tarred, gzipped, optionally signed) — §4, one sentence, sourced. Not in `kb_tags`. Low priority; add if the concept index is being touched anyway.

**6. Distractor-only command mentions.** `helm uninstall` (PQ7 explanation) and `kubectl rollout pause` (TYB1 Q4 option D, sourced). Both are correct-and-useful distractor hygiene, neither is taught. Recommend *not* adding to `commands` — the list should mean "demonstrated."

**7. Undeclared cross-domain touch (D2 Security).** §3's ⚓ Worth Securing observes that whoever can read Secrets in the release namespace can read Helm's bookkeeping, and whoever can delete them can make Helm forget. That is a Security-competency observation the outline did not declare. It is one paragraph, it is accurate, and it is the best sentence in the callout. Keep it; note it in the index.

**Index-level note:** `kb_tags.objectives` is `["D3.1"]` alone, while the outline's own practice-question plan declares deliberate interleaves with **D1.1** (workload rollback) and **D1.4** (containerization / OCI), and the draft executes both (PQ8, PQ9, PQ17, TYB1 Q4). The under-claim originates in the outline, not the draft, but this is the stage to fix it.

---

## Depth mismatches

Weight column is the **authored** allocation, per the authority note. No published sub-objective weight exists.

| Objective | Weight (authored) | Draft depth | Mismatch |
|---|---|---|---|
| D3.1-c chart / release / revision | core of the 5 pts | deep — Fixed Point ×2, figure, extended analogy, 6 PQ | OK — the outline designated this the chapter |
| D3.1-k `crds/` + ordering | high (discharges a shipped promise) | deep, best-sourced | OK |
| D3.1-a the four failures | high (frames everything) | appropriate; explicitly closed in §6 | OK |
| D3.1-l Go templating | deliberately capped | one line + render, then stops | OK — **exemplary restraint**; the depth ruling was honored |
| D3.1-e distribution / OCI | medium | 4 PQ (planned 3) + full rationale paragraph | mildly **over-covered** — see PQ redistribution below |
| D3.1-l′ Helm 2 → Helm 3 | 1 Exam Alert row authorized | 2 PQ + 1 Worth Securing + 2 Exam Alert paragraphs + 5 prose touches | **over-covered** vs. plan (item 1 above) |
| D3.1-g Kustomize base/overlay | medium — the chapter's *only* Kustomize exposure | strong prose; **2 PQ (planned 3)** | **under-covered in graded text** |
| D3.1-i generators | medium — a named owned concept | 1 prose paragraph, **0 graded items** | **under-covered** |
| D3.1-b chart anatomy | high | 3 PQ (planned 4) | mildly under-covered |
| `helm list` (declared command) | — | named once, only inside a Helm-2-vs-3 aside | **under-covered, and it leaves a loop open** — see below |

**Practice-question distribution, planned vs. actual:**

| Section | Planned | Actual | Δ |
|---|---|---|---|
| §1 problem | 1 | 1 | — |
| §2 chart anatomy | 4 | 3 | **−1** |
| §3 chart/release/revision | 5 | 6 | +1 |
| §4 repositories and versions | 3 | 4 | +1 |
| §5 Kustomize | 3 | 2 | **−1** |
| §6 the decision | 1 | 1 | — |
| **Total** | **17** | **17** | ✓ |

The count is right; the *allocation* drifted one item each from §2 and §5 into §3 and §4 — that is, out of the two thinnest-exposure areas and into the two already strongest. §5 is the one that matters: the outline allocated it 3 with a stated reason (*"blocking gap G19; the reader has one section of exposure and needs the reps"*), and it received 2. Counting checkpoints, Kustomize's total graded footprint is **4 items** (TYB2 Q1, Q2; PQ14, PQ15) against Helm's **~20**. For a section that owns half the chapter's authored topic list, that is thin.

**The open loop.** §1's failure three is posed as a question: *"what is currently installed on this cluster?"* The chapter answers the *versioning* half (charts carry a required SemVer version) but never closes the *interrogation* half — `helm list` is the command that answers the three-in-the-morning question, and it appears only as a footnote to a Helm 2 comparison. §6's four-failures-closed table inherits the gap: its Versioning row says "chart version, required on every chart" and stops. One clause fixes it.

**Reinforcement budget, noted not flagged.** The `charts/`-is-not-a-repository trap now appears seven times (fig02 annotation, §2 Snag, §4 Snag, TYB1 Q2, PQ11 distractor C, Exam Alert row, Summary row). Four were mandated. It is the chapter's designated highest-value confusion and the spacing is defensible — but it is at the top of its budget and should not grow during revision.

---

## Gaps the research stage flagged

Open Question 1 named eight required fetches. Seven landed in the corpus. Status against what each was supposed to feed:

| Fetch | Landed? | Discharged? |
|---|---|---|
| `helm.sh/docs/topics/charts/` (full page) | partial | **NO.** `helm-charts-2026-08-31` is truncated — it ends at *"Helm will expect a structure that matches this:"* with the structure itself absent. The `Chart.yaml` field reference, `version`/`appVersion`, and dependency semantics are **not** in it. The draft routed around this by sourcing those claims to `helm-glossary-2026-08-31` instead, which supports them. Legitimate, but the gap is still open for later chapters. |
| `kubernetes.io/.../kustomization/` (**G19**) | nominal | **NO.** `k8s-docs-kustomization-2026-08-31` is two sentences. G19 is *not* discharged. |
| `helm.sh/docs/intro/using_helm/` | yes | partially — install/upgrade/rollback/values precedence covered; **the revision-counter behavior is not** |
| `chart_repository` | yes | YES |
| `registries` | yes | YES |
| `chart_best_practices/custom_resource_definitions/` | yes | YES — §6 is the chapter's best-sourced section |
| kubectl-book kustomization fields | yes | field *names* only, no *semantics* |
| `changes_since_helm2` | yes | YES (fully) |

**How the draft handles the residue — correct in all three cases, and worth recording as such:**

1. **`helm rollback` and the revision counter** (Open Question 3a). Unresolved. The draft declines to state it, prints `rev 4 ???` in fig03, and raises an inline `AUTHOR-REVIEW` naming the exact fetch needed. This is the discriminating detail in the chapter's central contrast, and writing it from memory would have been the single worst available error. **Correctly deferred.**
2. **Kustomize patch semantics and the `configMapGenerator` name-hash suffix.** The field *list* is sourced; the *semantics* of strategic-merge vs JSON patch are written from field names plus general knowledge. The draft raises a second `AUTHOR-REVIEW` saying so, and explicitly **omits** the name-hash behavior rather than asserting it untagged — despite noting its pedagogical value. That is house practice executed exactly (*"write the shape and drop the specific"*).
3. **Tiller** (Open Question 5). Source obtained; the trap is stated with direct quotation rather than cut. Correct.

Per Rule 3, none of the above is a curriculum-alignment failure. The one that has *curriculum* consequence is **G19**: Kustomize is the chapter's least-sourced topic, and it is also — independently — its least-graded topic. Those two thinnesses compound, and that compounding is this audit's main finding.

---

## Recommended fixes

For the revision stage. One per issue, ordered by priority.

1. **Restore §5's third practice question, and make it the generator item.** Fixes both the §5 under-allocation and D3.1-i's zero-graded-items gap in one move. Build the stem on what `configMapGenerator` is *for* — generating the objects that vary most by environment, inside the layer that is about environment variation, which the §5 prose already argues. **Do not** write an item that depends on the name-hash suffix; that behavior is unsourced and deliberately omitted. Take the slot back from §4 (PQ17, the OCI push-reference item, is the most specialized of the four and the least load-bearing).

2. **Close the `helm list` loop.** §1 asks "what is currently installed on this cluster?" and the chapter never answers it with the command that does. Add one clause in §3 or §4 — `helm list` names the releases in your current namespace, `--all-namespaces` widens it — and extend §6's four-failures-closed table so the Versioning row reads *"chart version, required on every chart; `helm list` answers what's installed."* Also promotes `helm list` from footnote to demonstrated, matching its `kb_tags` declaration.

3. **Trim two Helm-2 touches, keep the thread.** Cut or compress the `helm list` default-scope change (subsumed by fix 2) and the ⚓ `apiVersion` v1→v2 Worth Securing. Keep Tiller, keep namespace scoping, keep mandatory naming. Consider converting PQ10 (Helm 2 auto-naming) into a Helm 3 behavior question that does not require knowing Helm 2 — it currently tests version history rather than the delivery competency.

4. **Recover §2's fourth practice question.** Currently 3 of a planned 4 on the chapter's largest vocabulary load. Subchart is the thinnest owned concept in §2 (one sentence of prose, graded only obliquely via PQ3's distractor C). A subchart item would take the slot from §3, which is one over plan and already the best-covered section in the chapter.

5. **Update `kb_tags` to stop under-claiming.** Add to `commands`: `helm-push` (demonstrated §4, graded PQ17). Add to `concepts`: `helm-2-to-helm-3` (or `tiller`), `chart-archive`. Add to `objectives`: `D1.1` and `D1.4` as declared interleaves — the outline's own PQ plan declares them and the draft executes them. Do **not** add `helm uninstall` or `kubectl rollout pause`; both appear only as distractors, and the list should continue to mean "demonstrated."

6. **Resolve or preserve the two AUTHOR-REVIEW blocks — do not let a later stage quietly close them.** Both are correct as raised. The rollback-counter one blocks a factual claim in the chapter's central contrast; if the fetch does not happen, `rev 4 ???` and the surrounding prose must ship as-is rather than being resolved from memory.

7. **Low priority — one clause on the Exam Alert heading.** The standing "High-Priority Topics" header sits in mild tension with the chapter's own disclosure that nobody outside the exam authority knows what is prioritized in this competency. The header is contract-mandated, so do not remove it; a single lead-in clause ("high-priority *for this chapter's material*, on the reasoning given above") reconciles the two at negligible cost. Every individual claim underneath is already compliant — the draft consistently uses conditional constructions (*"if a question puts both in play…"*) rather than frequency claims, which is the right pattern and should be preserved verbatim.

**Noted, out of scope for this stage:** PQ3 carries five options (A–E) in a set that is otherwise uniformly four, with "E) Both A and D" separated by a blank line from the A–D block. Flagging for the structural/QA stage; it is not a coverage issue.