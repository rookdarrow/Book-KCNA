The heartbeat sidecar confirms this session is the live `question-quality.md` stage, so I'll emit the document to stdout for the orchestrator to capture rather than writing the file myself. Line numbers below are verified against `draft-v1.md` on disk.

```markdown
# Question-Quality Audit — Chapter 14

## Summary

- Chapter type: **content**
- Total questions inspected: **35**
  - 🧭 Soundings questions: **8** (lines 46–60)
  - ☆ Taking Your Bearings questions: **10** (across **2** checkpoints — lines 482, 733)
  - Practice questions: **17** (lines 885–1006)
- Question budget compliance: **met** (35/35, every category exact)
- Weak distractors (WARN): **7 options across 6 items** — 6 of 27 graded items (22%) carry at least one inert option
- Trap answers that don't target real misconceptions (WARN): **1** (P15 option B — the answer key itself calls it "an invented split")
- Missing or incomplete why-wrong explanations (FAIL): **1** (P3, line 1014 — options A and D receive no individual treatment); plus **1 vague** (P10, line 1028 — "C and D are inventions" names no misconception)
- Retrieval-practice spacing: **compliant** (2/10 = 20.0%, exactly the chapter's target)
- Soundings spoiler check: **clean** — no stem or answer states any of the chapter's five ★ Fixed Points

**Overall:** this is a strong question set. Trap fidelity is unusually high — P6, P8, P9, P11, P12, TYB1 Q4 and TYB2 Q1/Q3 are all built around identifiable, documented misconceptions rather than filler. The defects are concentrated and cheap to fix: one malformed item (P3), one recurring habit of letting option D do no work, and two practice questions that re-run checkpoint items instead of extending coverage into material the chapter teaches and never tests.

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 10 | 10 | met |
| Taking Your Bearings (checkpoints) | ≥2 | 2 (5 + 5) | met |
| Practice Questions | 17 | 17 | met |
| **Chapter total** | **35** | **35** | **met** |

Both checkpoints carry ≥5 questions, satisfying the skill Part 8 distribution rule. No override was applied to B4's allocation and none was needed.

**Mechanical compliance is clean; the qualifying note is in the Duplication section below.** Two of the 17 practice items re-test a distinction already tested in TYB, so the chapter meets its budget at 35 but delivers roughly 33 items' worth of distinct discrimination.

## Soundings spoiler check

The chapter's five ★ Fixed Points, for reference: chart-as-versioned-package (215), release-as-instance / one-chart-many-releases (337), `helm rollback` ≠ `kubectl rollout undo` (400), chart-repository-as-HTTP-server (442), Kustomize-as-template-free / `apply -k` (554).

| Soundings Q # | Line | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|---|
| 1 | 46 | `kubectl apply -f <dir>/` and ordering (Ch 4 §1) | no | No packaging vocabulary in stem or answer. |
| 2 | 48 | What "install metrics-server" consists of (Ch 13 §7) | no | Answer stops at "YAML and `kubectl apply`"; names no packaging unit. |
| 3 | 50 | `kubectl rollout undo` (Ch 6 §5) | no | Asks only what `rollout undo` does. Nothing hints a second mechanism claims the word — FP 400 survives intact. |
| 4 | 52 | Unrecognized `kind` (Ch 6 §8) | no | Framed wholly in Ch 6 vocabulary; `crds/` and charts unmentioned. |
| 5 | 54 | Config outside the image (Ch 4 §4) | no | `values.yaml` never named. |
| 6 | 56 | Tag vs digest; what a registry is (Ch 2 §3) | no | Does not touch FP 442 (chart repository). See soft note below. |
| 7 | 58 | Package managers generally | no | Tool-agnostic, as the outline's watch item required. Never reaches chart/release or templating. |
| 8 | 60 | Two clusters, differing replicas/hostnames | no | Answer names copy / `sed` / hand-edit only — none is "patch a base you never modify," so FP 554 survives. |

**Status: clean. 0 FAILs.**

Two supporting checks also pass:

- **Answerable from prerequisites** (Part 11 rule 2). All eight resolve to Ch 2, 4, 6, or 13, or to general professional knowledge. None requires Ch 14 content.
- **Pre/post symmetry** (Part 11 rule 1). Two exact pre/post pairs exist — Soundings Q3 (line 50) ↔ TYB1 Q4 (line 507), and Soundings Q2 (line 48) ↔ TYB2 Q5 (line 765). This is good design and worth preserving through revision; it is the cleanest implementation of the pretesting effect in the chapter.

**Soft note, not a finding.** The Soundings answer to Q6 (line 75) defines a registry as "a service implementing the OCI distribution API: a place that stores and serves content addressed by digest." §4's payoff (lines 456–466) stages the same realization as a surprise — *re-read the OCI definition with fresh eyes; not "a service that stores images."* The answer key partially deflates that beat. It is not a Fixed-Point spoiler and it is inside a `<details>` block, so it does not compromise the pre-test. Flagged only so the revision stage can decide whether to trim Q6's answer to "a service that stores and serves images, addressed by digest" and let §4 do the widening.

**Rubric and disclosure checks:**
- Rubric present with all three branches (6+ / 3–5 / 0–2), lines 83–87. **Pass.** The 0–2 branch correctly names a *section* (Ch 4 §1) rather than a chapter, and conditionally adds Ch 6 §5 if Q3 specifically was missed — this satisfies the outline's load-bearing requirement.
- Answers enclosed in `<details>` / `<summary>`, lines 62–89. **Pass.**

## Per-question findings

### QP3 (line 899): "A chart directory contains `Chart.yaml`, `values.yaml`, `templates/`, and `charts/`. Which of these will *not* result in Kubernetes objects being created in your cluster?"

**Issue:** Three defects compounding. **(1)** Five options where all 26 other graded items use four. **(2)** The correct answer is a combined option (E, "Both A and D") whose components are each independently true — a reader who selects A is substantively correct and formally wrong, so the item tests option-scanning rather than chart anatomy. **(3)** The answer key (line 1014) explains only B and C; A and D are folded into a single sentence, and the pedagogically decisive point — why A alone is insufficient — is never made. This is the chapter's one **FAIL** on rule 3.

**Distractor analysis:**
- A) `Chart.yaml` — **independently true.** Not a distractor at all under the stem as written.
- B) `templates/` — plausible only to a reader who has misread §2 entirely; the weakest of the three genuine options, but acceptable as the "obviously does create objects" anchor.
- C) `charts/` — **the item's real value.** Targets the genuine misconception that subchart directories are inert metadata. The key rightly calls it "the interesting distractor."
- D) `values.yaml` — **independently true.** Not a distractor.
- E) "Both A and D" — a format the book uses nowhere else.

**Why-wrong explanation status:** **incomplete.** A and D receive no individual why-wrong or why-right; the reader who chose A gets no account of their error.

**Recommended fix:** Rebuild as a clean four-option item that keeps the `charts/` insight and drops the combination:

> **3.** Which entry in a chart directory does **not** contribute Kubernetes objects to your cluster?
> A) `templates/` · B) `charts/` · C) `values.yaml` · D) `crds/`

Answer C. A, B and D all contribute — and B and D are precisely the two most commonly assumed inert, so the item gains discrimination rather than losing it. The existing key text for B and C transfers almost verbatim; add one clause for D pointing at line 305 (`crds/` installed by default).

### QTYB1 1 (line 486): "…you run `helm rollback marketing 2`. What happens to the `docs` installation?"

**Issue:** Two of three distractors do no work, leaving what is effectively a two-option item (A vs B). A is excellent and carries the whole question.

**Distractor analysis:**
- A) rolls back too, same chart — **strong.** The chart/release collapse (B1 trap 80), exactly the misconception the item exists to catch.
- B) nothing, independent — correct.
- C) "deleted, because the chart's release name was reused" — **weak.** The stem supplies two different names (`marketing`, `docs`), so the option is refuted by reading the stem rather than by knowing anything. The key concedes this: "C is wrong because the names differ."
- D) "Helm refuses the rollback, because two releases share a chart" — **inert.** No identifiable misconception; the key dismisses it in nine words.

**Why-wrong explanation status:** present and specific for A; thin-but-adequate for C and D, in proportion to how little they carry.

**Recommended fix:** Re-aim C at the real Helm 2→3 namespace-scoping confusion the chapter teaches at lines 358–364, and D at a real scope confusion:

- C) It rolls back only if it shares a namespace with `marketing`
- D) `helm list` will now show `docs` as out of date, since the two releases track the same chart version

Both are wrong for reasons a reader must know the material to supply.

### QP2 (line 892): "Which statement about `values.yaml` is correct?"

**Issue:** Option D is inert.

**Distractor analysis:**
- A) contains the rendered manifests — **strong.** Real confusion between input values and rendered output.
- C) generated at install time from `--set` — **strong.** Inverts the precedence rule taught at lines 253–255.
- D) "required only for charts that have subcharts" — **inert.** Arbitrary; no reader holds this belief. Key rebuttal is a single clause naming no misconception.

**Why-wrong explanation status:** present and specific for A and C; present but vague for D.

**Recommended fix:** Replace D with the genuinely common beginner error, which §2 arms the reader against:

> D) It is the file an installer edits in place before running `helm install`

Wrong because overrides are supplied with `--values`/`-f` or `--set` (line 253), leaving the chart itself unmodified — and the correction reinforces the chapter's "the chart is the unit" thesis.

### QP4 (line 908): "In `templates/`, a file named `_helpers.tpl` is present. What is it for?"

**Issue:** Option D is inert.

**Distractor analysis:**
- A) helper objects created before the main templates — **good.** Plausibly imports the `crds/` ordering idea; a real cross-contamination.
- C) stores defaults that `values.yaml` inherits from — **acceptable.** Inverts the values relationship.
- D) "It is the chart's test suite" — **weak.** No association links "helpers" to chart tests; the key dismisses it in six words.

**Why-wrong explanation status:** present and specific for A and C; vague for D.

**Recommended fix:** Replace D with an ordering misconception about partials:

> D) It is rendered last, after all other templates, so its output can reference them

Wrong because underscore-prefixed files are never rendered to object definitions at all (line 291) — which re-tests the item's own correct answer from a second angle.

### QP5 (line 915): "You install the same chart twice with different release names in different namespaces. You then run `helm upgrade` on the first. What is the effect on the second?"

**Issue:** **Duplicate.** This is TYB1 Q1 (line 486) with `upgrade` substituted for `rollback` — same scenario shape, same correct answer, near-identical option set (A here ≈ A there; D here ≈ C/D there). It adds no discrimination the checkpoint has not already produced. Option C is additionally inert.

**Distractor analysis:**
- A) upgraded too, same chart version — the chart/release collapse again, already caught at line 486.
- C) "enters a pending state until it is also upgraded" — **inert.** Releases have no pending state relative to one another; no misconception named in the key.
- D) uninstalled, one release per cluster — acceptable; targets the Helm 2 name-uniqueness rule, and the key uses it well.

**Why-wrong explanation status:** present and specific.

**Recommended fix:** Re-aim the whole item at material the chapter teaches and never tests. Best candidate is override precedence (lines 253–255, fully sourced):

> **5.** You run `helm install app ./chart -f base-values.yaml -f prod-values.yaml --set replicaCount=12`. Both YAML files set `replicaCount`. Which value wins, and why?

This preserves the practice budget, tests a sourced fact currently examined nowhere, and removes the redundancy with TYB1 Q1.

### QP7 (line 929): "`helm rollback my-app` is run with no revision argument. What happens?"

**Issue:** Option D is inert.

**Distractor analysis:**
- A) errors, revision required — **good.** Plausible for a reader who assumes explicitness.
- B) rolls back to revision 1 — **good.** A real misreading of "previous."
- D) "uninstalls the release entirely" — **inert.** Nobody confuses rollback with uninstall; the key says so plainly.

**Why-wrong explanation status:** present and specific for A and B; vague for D.

**Recommended fix:** Replace D with a semantics misconception the omitted-argument case genuinely invites:

> D) It rolls back to the most recent revision created by `helm install` rather than `helm upgrade`

### QP10 (line 950): "`helm install` is run with no release name and no flags. What happens in Helm 3?"

**Issue:** Why-wrong explanation is **present but vague** for two of three distractors. The key (line 1028) disposes of C and D jointly — "C and D are inventions; neither is Helm's documented behavior." Per rule 3, an answer key must explain *why* a reader would land there and why it fails, not merely assert non-existence. As written, a reader who chose C learns only that they were wrong.

**Distractor analysis:**
- A) auto-generated from the chart name — **strong.** Genuine Helm 2 behavior, and the key handles it well including the `--generate-name` escape hatch.
- C) chart name used as release name — **plausible**, and worth a real rebuttal: it is what many chart READMEs *appear* to do, because the conventional example passes the chart name explicitly as the release name.
- D) `default` namespace with a random suffix — **plausible** to a reader blending the Helm 2 auto-naming with namespace defaulting.

**Recommended fix:** Split the joint dismissal:

> **C is wrong**, though it describes what most chart READMEs look like: the conventional `helm install wordpress bitnami/wordpress` passes the chart name *explicitly* as the release name. Helm does not infer it. **D is wrong** on both halves — no name is generated without `--generate-name`, and namespace defaulting is a kubeconfig-context matter, not something `helm install` invents.

### QP13 (line 971): "…The maintainer fixes a rendering bug in a template. Which number is expected to change in the next publish?"

**Issue:** **Near-verbatim duplicate** of TYB1 Q5 (line 514). Both present a template-level fix that leaves the installed application unchanged; both offer the same four option shapes (appVersion / version / both / neither); both resolve to B with the same reasoning. Two of the chapter's 27 graded items spend themselves on one distinction, and the second adds nothing the first did not establish.

**Distractor analysis:** all three distractors are individually sound — A inverts the pair, C asserts lockstep, D denies versioning. The problem is not construction; it is redundancy.

**Why-wrong explanation status:** present and specific.

**Recommended fix:** Re-aim at untested §2/§3 material. Two good candidates, both sourced in the draft:

> **13.** A chart's `Chart.yaml` declares `apiVersion: v2`. What does that tell you? *(line 313 — v2 was introduced for Helm 3; a v1 chart predates library-chart support and the `requirements.yaml` consolidation.)*

or

> **13.** You run `helm list` and do not see a release you know is installed. What is the most likely explanation? *(lines 366–368 — Helm 3 lists only the current context's namespace; `--all-namespaces` restores Helm 2 behavior.)*

The second is stronger: it tests a behavior change with real operational consequences, and `helm list` is currently in `kb_tags.commands` with no graded coverage at all.

### QP15 (line 985): "Which pair correctly describes Kustomize's two patch styles?"

**Issue:** Trap fidelity on option B. The answer key's own words are "**B is an invented split**" — an explicit admission that the distractor was built for symmetry rather than to catch a real misconception. Rule 2 exists for exactly this.

**Distractor analysis:**
- B) "strategic merge operates on lists only; JSON patch on maps only" — **low fidelity.** It is a scrambled inversion of a real heuristic (reach for JSON patch on list elements), which gives it faint plausibility, but the arrangement it states is one nobody holds.
- C) strategic merge server-side, JSON patch client-side — **strong.** Genuinely plausible: `kubectl patch --type=strategic` *is* a server-side operation in a different context, so the confusion is real and earned.
- D) strategic merge requires a template engine — **acceptable.** Serves as a check on the template-free Fixed Point at line 554.

**Why-wrong explanation status:** present; specific for C and D, and honest-but-thin for B.

**Recommended fix:** Replace B with a real inversion:

> B) A strategic merge patch must restate the whole object; a JSON patch names only the changed fields

Wrong because it inverts the actual relationship — the merge patch is the *fragment* form — and it targets a misconception readers genuinely arrive with from JSON-merge-patch semantics elsewhere.

### QP16 (line 992): "A team keeps their application manifests in their own Git repository, deploys to three clusters they administer, and has no external consumers. Which approach fits best, and why?"

**Issue:** Option D is inert. The rest of the item is excellent — A and C are both real reasoning failures, and the key rebuts A on the *axis* rather than on preference, which is exactly right for a judgment item.

**Distractor analysis:**
- A) Helm, versioning is always required — **strong.** Real dogma, well rebutted.
- C) Helm, three environments exceed overlays — **strong.** Real capability misconception.
- D) "Neither; three environments require a service mesh" — **inert.** A non sequitur by the key's own description. Its only value is the forward cross-bearing to Ch 17 §5, which the chapter can carry elsewhere.

**Recommended fix:** Replace D with a real alternative a practitioner might actually propose:

> D) Kustomize, because overlays remove the need to keep the base under version control

Wrong for an instructive reason: overlays are *deltas against* a base that must be versioned for them to mean anything — which reinforces §6's "Git supplies identity" point (line 1040) instead of gesturing at an unrelated technology.

### QP17 (line 999): "`[interleaved: D1.4]` You push a Helm chart to an OCI registry…"

**Issue:** **Interleave tag is on the wrong item.** P17 tests `helm push` reference syntax; a reader needs no Ch 2 / D1.4 containerization knowledge to answer it. P12 (line 964, "Why can an OCI registry store Helm charts?") is the item that genuinely requires the Ch 2 §5 OCI-spec understanding — content-not-images — and it carries no tag.

Separately, the outline planned **three** cross-domain stems (chart + Deployment rollback → D1.1; OCI registry + image identity → D1.4; chart-installed CRD + ordering → D1.1 extensibility). All three exist in substance — P8/P9, P12, and P1 respectively — but only one carries a tag, so the interleaving is invisible to downstream stages and to the mock-exam assembler.

**Distractor analysis:** P17's own options are sound (B digest-only, C identical-to-repo-URL, D version-lost-on-push are all plausible), and the item needs no rewrite.

**Recommended fix:** Move `[interleaved: D1.4]` from P17 (line 999) to P12 (line 964). Add `[interleaved: D1.1]` to P9 (line 943) and P1 (line 885). No prose changes required.

## Retrieval-practice spacing

- Chapter 14 target: **20%** of checkpoint questions from earlier chapters (the arc outline assigns Ch 14 the 20% target, not the 25% ceiling that governs Ch 13/15/16/17/18)
- Actual: **20.0%** (2 of 10 questions tagged)
  - TYB1 Q4 (line 507) — `[retrieval: ch6]`, `kubectl rollout undo` semantics and revision history
  - TYB2 Q5 (line 765) — `[retrieval: ch13]`, what "install metrics-server" consists of
- Status: **compliant**

Both structural constraints are satisfied: the ≥4-back floor by the Ch 6 draw (eight chapters back), and the Ch 9–13 window by the Ch 13 draw. Both items also pair with a Soundings question on the same material (lines 50 and 48), making them genuine pre/post instruments rather than isolated callbacks.

Retrieval definition is correctly applied under the narrow standard: in both items the *answer* lives in an earlier chapter, not merely the background vocabulary. TYB1 Q4 is a model case — distractor C imports Ch 14's `helm rollback` scope specifically to force discrimination against Ch 6 material.

**One soft finding.** TYB2 Q5's correct option B reads "Applying a set of Kubernetes objects — a Deployment, Service, RBAC rules, an APIService — which somebody has packaged, **commonly as a chart**." That trailing clause is Ch 14 content, and it makes B selectable on current-chapter cues alone by a reader who has retained nothing from Ch 13. The item still qualifies (the first clause is sufficient and is Ch 13's), but it does less retrieval work than the tag claims. **Recommend** trimming the tail to end at "…an APIService — which somebody else wrote," and letting the answer key make the chart connection instead. Costs nothing and restores the item's full retrieval load.

No additions needed; the chapter is at target and should not exceed it.

## Coverage vs concepts

Checked against `kb_tags.concepts` and `kb_tags.commands` in the outline frontmatter. "Tested" means a graded item (TYB or Practice) turns on the concept; Soundings items are pre-tests and are noted separately where they are the only coverage.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| manifest-sprawl (the four failures as a set) | **partial** — components at P1 (ordering) and P16 (distribution); no item tests the set |
| environment-variation | yes (TYB2 Q1, P16) |
| apply-ordering | yes (P1; Soundings Q1) |
| helm | yes (throughout) |
| chart | yes (TYB1 Q1/Q2/Q3, P3, P11) |
| chart-yaml | yes (TYB1 Q3, P13) |
| values-yaml | yes (P2) |
| chart-templates-directory | yes (P3, P4) |
| chart-dependencies-directory (`charts/`) | yes (TYB1 Q2, P3, P11) — the chapter's best-covered trap |
| chart-crds-directory | yes (TYB2 Q3, P1 option D) |
| subchart | **NO** — appears only inside P3's answer key (line 1014), never in a stem or option |
| notes-txt | **distractor-only** (TYB1 Q3 option B) |
| chart-helpers | yes (P4) |
| go-template-in-helm | **partial** — P2 option A and TYB2 Q1 option D touch rendering obliquely; the values→template→manifest mechanism is never the object of a question |
| helm-release | yes (TYB1 Q1, P5, P9) |
| helm-release-revision | yes (P7, P9) |
| helm-rollback-versus-rollout-undo | yes (TYB1 Q4, P8, P9) — correctly the most-tested concept in the chapter |
| chart-repository | yes (TYB1 Q2, P11) |
| oci-registry-as-chart-store | yes (P12, P17) |
| chart-version-versus-appversion | yes (TYB1 Q5, P13) — **over-covered**; see Duplication |
| kustomize | yes (TYB2 Q1/Q2, P14, P15, P16) |
| kustomization-yaml | yes (P14, P15) |
| base-and-overlay | yes (TYB2 Q1, P16) |
| strategic-merge-patch | yes (P15) |
| json-patch | yes (P15) |
| configmap-generator | **NO** |
| secret-generator | **NO** |
| templating-versus-overlay | yes (TYB2 Q4, P16) |
| crd-ordering-problem | yes (TYB2 Q3, P1) |

| Command in `kb_tags.commands` | Tested in a question? |
|---|---|
| `helm install` | yes (P10; TYB1 Q1 stem) |
| `helm upgrade` | yes (P5, TYB2 Q3) |
| `helm rollback` | yes (TYB1 Q1, P7, P8, P9) |
| `helm list` | **NO** — the Helm 3 namespace-scoping change (lines 366–368) is taught and never tested |
| `helm repo add` | **distractor-only** (TYB1 Q2 option C) |
| `kubectl apply -k` | yes (TYB2 Q1, Q2) |

**Also taught with sources and never tested** (not in `kb_tags`, but graded-worthy):
- `--values`/`-f` and `--set` override precedence (lines 253–255) — sourced, operationally important, examined nowhere
- `Chart.yaml` `apiVersion` v1→v2 (line 313, a ⚓ Worth Securing) — untested
- `--skip-crds` and the `--dry-run` CRD gap (lines 700–704) — only the no-upgrade limitation is tested, at TYB2 Q3
- Tiller removal — **distractor-only** (P6 option A). Given that the Exam Alert elevates it to a named trap with its own explanatory paragraph (lines 878–881), testing it solely as a wrong option is thin. Consider promoting it to a stem.

**Recommended coverage additions.** Three of the five re-aim opportunities identified above resolve four of these gaps at zero budget cost:
1. Re-aim **P5** → `--values`/`--set` precedence
2. Re-aim **P13** → `helm list` namespace scoping *(or `Chart.yaml` apiVersion v2)*
3. Add a generator clause to **P14**, which already tests `kustomization.yaml` fields — extending its option set to include `configMapGenerator` covers both generator concepts without adding an item

`subchart` and the go-template mechanism are the remaining gaps. Both are name-only-depth topics per the outline's §2 depth ruling, so leaving them untested is defensible; the revision stage should make that call deliberately rather than by omission.

## Duplication

Not a template category, but the most consequential efficiency finding in the set.

| Pair | Distinction | Assessment |
|---|---|---|
| TYB1 Q1 (486) ↔ P5 (915) | one chart, many independent releases | Same scenario shape, same option architecture, same key logic. The checkpoint item is the stronger of the two. |
| TYB1 Q5 (514) ↔ P13 (971) | chart `version` vs `appVersion` | Near-verbatim. Same four option shapes, same correct answer, same reasoning. |

Spaced re-testing is legitimate — but these are not spaced variants that vary context or difficulty; they are the same item twice with a verb swapped. Against six genuine coverage gaps in the concept table, spending two practice slots this way is the clearest available improvement to the chapter's question set. Both re-aims are specified in the per-question blocks above.

## Recommended action summary

**FAIL — must fix before the chapter ships:**
1. **P3** (899 / 1014) — rebuild as a four-option item; the combined-option format and the incomplete answer key are both disqualifying.

**WARN — should fix:**
2. Replace the seven inert distractors: TYB1 Q1 C and D (486), P2 D (892), P4 D (908), P5 C (915), P7 D (929), P16 D (992). Concrete replacements supplied above.
3. **P15 option B** (985) — replace the acknowledged "invented split."
4. **P10** (1028) — split the joint "C and D are inventions" dismissal into per-option explanations.
5. **P5** and **P13** — re-aim the two duplicates onto untested sourced material.
6. Move `[interleaved: D1.4]` from P17 to P12; tag P1 and P9 `[interleaved: D1.1]`.

**Optional:**
7. Trim TYB2 Q5's correct option to end at the Ch 13 boundary, restoring its full retrieval load.
8. Trim Soundings Q6's answer so §4's OCI reveal keeps its surprise.
9. Consider promoting Tiller from distractor-only (P6) to a stem, given its Exam Alert prominence.

Nothing in this list threatens the question budget: every recommendation is a replacement or a re-aim, and the chapter stays at 35/35.
```