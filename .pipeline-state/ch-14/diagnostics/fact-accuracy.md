# Fact-Accuracy Audit — Chapter 14

**Mode detected: STANDARD.** The cached corpus contains 27 populated snapshots, and the draft carries ~150 inline `[source: …]` tag instances. Untagged factual claims are therefore FAIL.

**Audit convention used for cross-bearings.** Claims that carry an explicit `[cross-bearing: see Ch N §M]` are treated as owned by the referenced chapter and are *not* failed merely for lacking a tag here — **unless** the claim is a discriminating detail in a Fixed Point, an answer key, or a graded distractor, in which case this chapter is relying on it and must be able to defend it. Those are failed. This convention is stated so the revision stage can overrule it deliberately rather than by accident.

---

## Summary

- Total factual claims inspected: **118** distinct externally-checkable assertions (~150 tag instances; several claims are cited repeatedly)
- Tagged claims verified: **92**
- Tagged claims unverifiable (tag points to missing/empty snapshot): **0** — every tag in the draft resolves to a snapshot present in this corpus
- **Untagged factual claims (FAIL): 11**
- **Contradicted / tag-does-not-support claims (FAIL): 2**
- Minor discrepancies (WARN): **16**

**Headline findings, in order of ship-risk:**

1. The **8% → 16% domain-weight change** is cited twice to a snapshot that states only the current 16% and says nothing about any prior weight. This is the chapter's stakes claim and its outdated-material argument rests on it.
2. The **entire `appVersion` subsection** — a Fixed-Point-adjacent distinction with a mnemonic, a Bearings question, and a Practice question built on it — has **no supporting snapshot text anywhere in the corpus**. Three snapshots list `chart-version-versus-appversion` in `concepts_covered`, but none of the captured text defines `appVersion`.
3. **"a Helm that has not existed since 2019"** — a bare date, twice, with no source.
4. **"You could `kubectl apply -f` the base directory directly and it would work"** is untagged and appears to be *false* on the chapter's own terms.

The draft's two existing `AUTHOR-REVIEW` comments (Helm rollback revision-counter behaviour; Kustomize patch semantics and `configMapGenerator` name-hash) are **correctly declared gaps** and are handled exactly as the pipeline wants: prose declines to assert, figure shows `???`. Both are registered below as research gaps rather than counted as failures.

---

## FAIL — Contradicted claims

### ~Line 133 (Why This Chapter Matters, ¶6): "Cloud Native Application Delivery went from 8% of the exam to 16% under the current blueprint"

**Tag:** `[source: lf-kcna-exam-page-2026-08-23]`

**Snapshot says:** the only weight statement in that snapshot is the current blueprint:
> "Cloud Native Application Delivery 16%"

The snapshot contains no prior weight, no reference to a previous blueprint, and no statement that any weight changed. Its `concepts_covered` list includes `domain-weights-44-28-16-12` only. `cncf-kcna-curriculum-pdf-2026-08-23` likewise gives only the current four weights.

**Draft says:** "went from 8% of the exam to 16% under the current blueprint [source: lf-kcna-exam-page-2026-08-23], and study material built for the old one under-serves this material by half."

**Recommended fix:** The `8%` figure and the "under-serves by half" corollary are unsupported by anything in this corpus. Either (a) locate the Chapter 1 snapshot that established the prior blueprint and re-tag both sentences to it, or (b) open a research gap for a snapshot of the superseded KCNA curriculum (an archived `cncf/curriculum` KCNA PDF revision, or an LF changelog announcing the blueprint revision), or (c) rewrite to what the corpus supports: *"Cloud Native Application Delivery carries 16% of the current blueprint [source: lf-kcna-exam-page-2026-08-23]."* Option (c) costs the chapter its "doubled" rhetoric and should be a deliberate choice, not a default.

### ~Line 1000 (Exam Alert!, closing ¶): "This domain doubled in weight under the current blueprint"

**Tag:** `[source: lf-kcna-exam-page-2026-08-23]`

**Snapshot says:** as above — "Cloud Native Application Delivery 16%", with no prior figure.

**Draft says:** "This domain doubled in weight under the current blueprint [source: lf-kcna-exam-page-2026-08-23], and a great deal of the freely available preparation material for it predates that change, some of it by a wide margin."

**Recommended fix:** Same resolution as the finding above; the two sentences must move together. The trailing clause about preparation material is a separate untagged market claim — see WARN below.

---

## FAIL — Untagged factual claims

### ~Line 512–530 (§4, "Chart version is not application version" — entire subsection)

> "`Chart.yaml` separately carries `appVersion`, the version of the *application the chart installs*. These move independently."

**Why it's a factual claim:** It asserts the existence, name, and semantics of a specific field in a third-party project's file format, and the independence of two version numbers.

**Corpus status:** No snapshot text in this corpus mentions `appVersion`. `helm-glossary-2026-08-31` defines **Chart Version** ("Charts are versioned according to the SemVer 2 spec. A version number is required on every chart") but stops there. `helm-charts-2026-08-31` is truncated at *"Inside of this directory, Helm will expect a structure that matches this:"* — the `Chart.yaml` field table that would carry `appVersion` was not captured. Three snapshots list `chart-version-versus-appversion` under `concepts_covered` without any body text supporting it; per the corpus note, that is not a citation.

**Blast radius:** the ⚓ mnemonic ("Version is the box; `appVersion` is what's in the box"), Taking Your Bearings (1) Q5 and its answer key, Practice Q13 and its answer key, and the Chapter Summary row "version vs appVersion". Four separate places assert it, none tagged.

**Fix:** Open a research gap for `https://helm.sh/docs/topics/charts/#the-chartyaml-file` (which enumerates `version` and `appVersion` and states that `appVersion` "is not related to the `version` field") — the existing `helm-charts-2026-08-31` capture simply stopped short of it. Re-fetch and extend that snapshot rather than adding a new one. Until then, no `appVersion` sentence should ship untagged.

### ~Line 998 (Exam Alert!) and ~Line 1160 (Chapter Summary): "a Helm that has not existed since 2019" / "Any material that explains securing it predates 2019"

**Why it's a factual claim:** a release date for a third-party project, used as a dating heuristic the reader is told to apply to study material.

**Corpus status:** `helm-changes-since-helm2-2026-08-31` establishes *that* Tiller was removed in Helm 3 and *why*, in detail. It gives no date. No snapshot in the corpus dates any Helm 3 release. (The only Helm date in the corpus is "February 28, 2022" for the 3.8.0 OCI blog post, which post-dates 2019 and cannot be used to derive it.)

**Fix:** Either tag both instances to a snapshot that dates the Helm 3.0 GA (the Helm blog's Helm 3 release announcement, or the CNCF announcement), or drop the year and rely on the sourced marker — "if a study resource explains how to secure Tiller, it was written for a Helm 2 that Helm 3 removed [source: helm-changes-since-helm2-2026-08-31]" — which loses nothing pedagogically and needs no new fetch.

### ~Line 129 (Why This Chapter Matters, ¶4) and ~Line 244 (§1, failure four): "fetch about forty YAML files" / "It is a forty-file operation"

**Why it's a factual claim:** a numeric count of the artifacts a named third-party component ships.

**Corpus status:** no metrics-server snapshot exists in this corpus.

**Additional concern — internal contradiction.** The draft's own enumeration, two sentences later in §1, is: *"it is a Deployment, a Service, some RBAC, and an APIService registration"* — roughly eight to ten objects, and upstream metrics-server distributes them as a single `components.yaml`. "Forty files" and the draft's own inventory cannot both be describing the same thing. This is checkable without leaving the draft.

**Fix:** Open a research gap for the metrics-server release manifest (`github.com/kubernetes-sigs/metrics-server` releases, `components.yaml`) so the count can be stated correctly. Failing that, delete the number: "fetch a manifest set somebody else wrote, read enough of it to find the values that need to be different on your cluster…" makes the same rhetorical point and asserts nothing countable.

### ~Lines 90, 129, 244, 878 (Soundings A2; Why This Chapter Matters; §1 failure four; Bearings 2 Q5 answer): metrics-server's composition

> "a Deployment, a Service, a ServiceAccount, RBAC rules, an APIService registration"
> "metrics-server is a Deployment that reads from the kubelets, not a per-node binary you install"
> "metrics-server is a separate component, not a feature gate"

**Why it's a factual claim:** the architecture and packaging of a named Kubernetes SIG component, asserted four times, and load-bearing as the **correct answer** to Bearings 2 Q5 and as the disqualifier for distractors A and C.

**Corpus status:** unsupported — no metrics-server snapshot in this corpus. The `[cross-bearing: see Ch 13 §7]` attributes it to Chapter 13, but this chapter grades a question on it, so the convention above does not shield it.

**Fix:** Confirm Chapter 13's corpus contains a metrics-server snapshot and re-tag the Bearings 2 Q5 answer key to it. If Chapter 13 has none either, open one research gap covering both chapters (the metrics-server README/`components.yaml`, plus `kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/`).

### ~Line 91 (Soundings A3) and ~Line 606 (Bearings 1 Q4 answer key): the rollback-is-a-new-revision claim

> "The rollback itself is recorded as a new revision: the history moves forward even though the workload moves backward."
> "**4. A.** … the rollback is itself recorded in the Deployment's revision history"
> "**B is wrong**: the previous ReplicaSet is not recreated, it is scaled back up; it never left."

**Why it's a factual claim:** specific controller and revision-history behaviour, asserted as the sole correct answer to a graded question and as the disqualifier for its nearest distractor.

**Corpus status:** the only relevant snapshot, `k8s-docs-kubectl-rollout-2026-08-24`, is a command reference. It says exactly: *"`kubectl rollout undo` | Undo a previous rollout"* and lists the valid resource types. It says nothing about what happens to the revision history, and nothing about ReplicaSet scaling. Answer 4A's citation covers "undoes a previous rollout" and stops short of the clause the answer turns on.

**Notable inconsistency:** the draft explicitly refuses to assert the *Helm* equivalent of exactly this behaviour (see the `AUTHOR-REVIEW` at §3, which correctly says the counter behaviour "MUST NOT be written from memory"), while asserting the Kubernetes equivalent confidently and untagged twelve lines earlier. Apply the same standard to both.

**Fix:** Open a research gap for `kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment` (which states both the ReplicaSet scale-up behaviour and the revision accounting) and tag the Soundings answer, the §3 Fixed Point bookkeeping bullet, and the Bearings 1 Q4 key to it.

### ~Line 640 (§5, "Template-free" paragraph): "You could `kubectl apply -f` the base directory directly and it would work."

**Why it's a factual claim:** asserted behaviour of a specific `kubectl` invocation against a specific directory layout.

**Corpus status:** untagged, and the corpus points the other way. `kubectl-book-kustomization-fields-2026-08-31` states: *"The kustomization file is a YAML specification of a Kubernetes Resource Model (KRM) object called a Kustomization."* Figure `ch14-fig04` shows `base/` containing `kustomization.yaml` alongside `deployment.yaml` and `service.yaml`. `kubectl apply -f base/` therefore submits a `kind: Kustomization` object to an API server that does not serve that kind — which is precisely failure two from this chapter's own §1: *"the API server does not queue your object for later. It rejects it."* The chapter contradicts itself two sections apart.

**Fix:** narrow the claim to what is true and to what the paragraph actually needs: *"Each manifest in the base is an ordinary, valid, applyable object — `kubectl apply -f base/deployment.yaml` works with no rendering step. (The `kustomization.yaml` beside it is Kustomize's own object, and is the one file in the directory the API server will not take.)"* That parenthetical is a gift: it reinforces §1's CRD lesson instead of tripping over it.

### ~Line 96 (Soundings A6): "A tag is a mutable, human-friendly pointer at an image"

**Why it's a factual claim:** a property (mutability) of an OCI registry construct, offered as the correct answer to a diagnostic question.

**Corpus status:** `oci-distribution-spec-2026-08-24` defines Registry, Repository, Blob, Manifest, and Digest. It does not define **tag** and says nothing about mutability. The second half of the same answer — "A registry is a service implementing the OCI distribution API" — *is* corpus-supported ("a service that handles the required APIs defined in this specification") and merely needs the tag.

**Fix:** Tag the registry and digest halves to `oci-distribution-spec-2026-08-24`. For tag mutability, confirm Chapter 2's corpus carries it (its `[cross-bearing: see Ch 2 §3]` suggests it should); if not, open a gap for the OCI image-spec or the distribution spec's tag section.

### ~Line 214 (§1, failure two, ¶2): "will produce Pods stuck in `CreateContainerConfigError`"

**Why it's a factual claim:** a verbatim Kubernetes status reason string. Reason strings are exactly the kind of detail readers will pattern-match against real clusters, and exactly the kind that drifts.

**Corpus status:** not present in any snapshot here.

**Fix:** confirm Chapter 13's troubleshooting corpus carries the string and re-tag; otherwise open a gap for `kubernetes.io/docs/tasks/debug/debug-application/debug-pods/`. Alternatively, generalize to "Pods that will not start until the ConfigMap appears" and keep only the `[cross-bearing: see Ch 13 §2]`.

### ~Line 336 (§2, `templates/`, ¶after the render example): "It is a Go template dialect with a substantial function library, conditionals, loops, and named partials"

**Why it's a factual claim:** identifies the template language of a third-party tool and characterizes its feature set.

**Corpus status:** only the last item is supported. `helm-named-templates-2026-08-31` establishes `define`, `_helpers.tpl`, and partials. Nothing in the captured text says "Go template", and no snapshot describes a function library, conditionals, or loops. (`go-template-in-helm` appears in two `concepts_covered` lists with no body text behind it.)

**Fix:** open a research gap for `helm.sh/docs/chart_template_guide/` (its opening pages name the Go template language and the Sprig function library explicitly). This is a one-fetch fix that also feeds the §5 patch-semantics gap the draft already declared.

### ~Line 700 (§5, 🔭 Closer Look, 2nd ¶): "`bases` is a separate field from `resources`, a survival from an earlier layout in which they were distinct. Modern kustomizations list the base under `resources`."

**Why it's a factual claim:** a deprecation/lifecycle assertion about a specific configuration field.

**Corpus status:** contradicted in spirit by the cited field list itself. `kubectl-book-kustomization-fields-2026-08-31` presents `bases` — *"Add resources from a kustomization dir"* — in the same undifferentiated list as `resources`, with no deprecation marker. The draft's history claim is inferred from the shape of the list, not read from it.

**Fix:** either tag to a source that states the deprecation (the kustomize `bases` field reference page carries the deprecation notice), or soften to what the list supports: "the list also carries both `bases` and `resources`, which overlap; charts you meet in the wild will use either." Note this sits *inside* a 🔭 Closer Look already framed as "well past what the exam requires," which lowers the stakes but does not change the tagging rule.

### ~Line 690 (§5, "Targeted patches", ¶2): strategic-merge vs JSON-patch semantics, and "RFC 6902"

> "A **strategic merge patch** is a fragment of the object that looks like the object… A **JSON patch**, meaning JSON Patch, RFC 6902, is a list of explicit operations on paths."

**Why it's a factual claim:** the operational semantics of two patch standards, plus a specific RFC number.

**Corpus status:** `kubectl-book-kustomization-fields-2026-08-31` supplies only the field names and the bare strings "the strategic merge patch standard" and "the json 6902 standard". The semantics and the RFC expansion are authored.

**Mitigating:** the draft's `AUTHOR-REVIEW` comment at the end of §5 **already declares this exact gap** and correctly names the fetch needed. It is listed here as FAIL because the prose still asserts it untagged in shipping text — not because the gap went unnoticed. The `configMapGenerator` name-hash behaviour was handled correctly by omission, which is the right instinct applied to the right thing; apply it here too, or close the gap.

**Fix:** as the draft's own note says — fetch the full `kubernetes.io` kustomization task page. Add `datatracker.ietf.org/doc/html/rfc6902` if the RFC expansion is to stay.

---

## WARN — Minor discrepancies

1. **§2, `crds/`, ~line 380 and §6, ~line 790 — "installed first" / "installed before the templates render".** `helm-crd-best-practices-2026-08-31` supports "not templated" and "will be installed by default when running a `helm install`". It does **not** state install *ordering* relative to templated manifests. Since ordering is the whole reason §6 gives for the directory's existence, this deserves a sentence that says so explicitly from source. Recommend capturing the Helm docs sentence on CRD install ordering when the `chart_template_guide` fetch happens.

2. **§4, ~line 490 — "That is how `helm repo add` works: fetch the index once…"** Untagged mechanism claim. `helm-chart-repository-2026-08-31` establishes what `index.yaml` *contains* but never describes `helm repo add`'s fetch behaviour. (`helm-repo-add` appears in `concepts_covered` with no body text.) Low risk, easy tag once the repo-guide snapshot is extended.

3. **§2, ~line 356 — "A chart nested inside another chart this way is a **subchart**."** Terminology assertion; `subchart` appears in two `concepts_covered` lists, in no snapshot body. Recommend tagging to the Helm charts doc subchart section.

4. **§2, ~line 358 and Practice Q3 answer C — "Install the parent, get both" / "installing the parent installs the subcharts, so objects absolutely do come from there."** Untagged behavioural claim doing work as a graded distractor explanation. Same fetch as #3 resolves it.

5. **§3, ~line 424 — "Installing creates a release at revision 1. Upgrading creates revision 2."** The corpus supports only "A sequential counter is used to track releases as they change" [helm-glossary]. That the counter *starts at 1 on install* is inferred. Bundle into the same fetch as the declared `AUTHOR-REVIEW` rollback-counter gap; one page likely settles both.

6. **§2, ~line 344 — "the 'here is how to reach your new installation' text printed after a successful install."** `helm-charts-2026-08-23` supports "optional plain text file containing short usage notes" but not the print-on-install behaviour.

7. **§3 Fixed Point, ~line 458 — "Neither calls the other. `helm rollback` does not run `kubectl rollout undo` underneath."** A negative implementation claim in a must-memorize block, and the disqualifier for Practice Q8 distractor C. It follows defensibly from `helm-changes-since-helm2-2026-08-31` ("fetch information from the Kubernetes API server, render the Charts client-side, and store a record of the installation in Kubernetes"), which the draft could cite here to make the inference visible rather than asserted.

8. **§3, ~line 466 — "When Helm rolls a release back, it computes the objects the target revision described and applies them."** Same family as #7; same fix.

9. **Why This Chapter Matters, ~line 141 — the scope of the Helm/Kustomize negative evidence.** `lf-lfs250-course-outline-2026-08-31` contains an explicit, purpose-built negative-evidence block ("No sentence on this public course page names Helm or Kustomize"), which fully supports the LFS250 third of the claim. `lf-kcna-exam-page-2026-08-23` carries a negative-evidence block too, but scoped **only** to question count and passing score, and it warns in capitals against generalizing. Extending it to Helm/Kustomize is an inference from a partial capture. Recommend either re-fetching the exam page with that negative recorded, or attributing the strong negative to LFS250 and softening the exam-page clause to "and does not appear in the exam page's published domain and competency list [source: lf-kcna-exam-page-2026-08-23]".

10. **Header blockquote, ~line 10 — "CNCF publishes the domain weight and the competency names, and nothing finer."** Untagged assertion about the vendor, duplicating a claim that *is* correctly tagged 120 lines later. Trivial fix: append `[source: cncf-kcna-curriculum-pdf-2026-08-23]`.

11. **Corpus freshness conflict, OCI status (§4, ~line 500).** `helm-changes-since-helm2-2026-08-31` still describes OCI push as *"an experimental feature… set the environment variable `HELM_EXPERIMENTAL_OCI=1`"*, while `helm-blog-oci-ga-2026-08-31` (Feb 2022, Helm 3.8.0) and `helm-oci-registries-2026-08-31` describe it as GA and recommended. **The draft resolved this correctly** — it sources the GA claim to the blog and draws only the *rationale* from the FAQ page. Recorded here so the discrepancy is not "rediscovered" in a later chapter and resolved the wrong way. Consider a snapshot-level note on `helm-changes-since-helm2-2026-08-31` marking its OCI section as superseded.

12. **§6, ~line 760 — "That is why the ecosystem ships operators, controllers, ingress controllers, and monitoring stacks as charts."** Broad untagged claim about ecosystem practice. Effectively unfalsifiable as written and unlikely to mislead, but it is an empirical claim in a chapter that is otherwise disciplined about them.

13. **§6, ⚠ Navigational Hazards, ~line 812 — "Deleting or downgrading a CRD is potentially catastrophic, since it can take every custom resource of that kind with it."** Untagged claim about CRD deletion cascade. Supported by `k8s-docs-custom-resources-2026-08-23` only indirectly. Recommend tagging to the CRD deletion documentation or attributing as authorial reasoning ("the reason for the restriction is defensible: deleting a CRD takes…").

14. **Exam Alert closing, ~line 1001 — "a great deal of the freely available preparation material for it predates that change, some of it by a wide margin."** Untagged claim about the third-party study-material market. Rhetorically the payload of the Tiller row, and unverifiable by construction. Suggest recasting as guidance rather than fact: "treat Tiller as a dating stamp — material that explains securing it is describing a Helm that no longer exists."

15. **Practice Q15 answer C, ~line 1120 — "Kustomize renders client-side, and the server sees ordinary objects."** Untagged. Correct and low-risk, but it is the disqualifier for a distractor.

16. **Internal arithmetic — Attention Budget, ~line 24.** Section times sum to **92 minutes** (10+15+18+8+6+14+10+6+5); the header states **"Total time: ~85 minutes"**. Not a source-accuracy issue, but the linter and the reader both do this addition. Either round the header to ~90 or trim a section estimate.

---

## Research gaps to open

Consolidated so the revision stage can order fetches efficiently. Four fetches close eleven findings.

| Gap | Snapshot to cache | Closes |
|---|---|---|
| **G-14a** | `helm.sh/docs/topics/charts/` — re-fetch **past** the truncation point to capture the `Chart.yaml` field table (`version`, `appVersion`, subcharts) | FAIL #1 (`appVersion`, 4 sites), WARN 3, WARN 4 |
| **G-14b** | `kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment` | FAIL #5 (rollback revision accounting, 3 sites), Bearings 1 Q4 key |
| **G-14c** | `helm.sh/docs/chart_template_guide/` (index + `values_files`) and the full `kubernetes.io` kustomization task page — **already named by the draft's own `AUTHOR-REVIEW`** | FAIL #10 (Go templates), FAIL #11 (patch semantics), WARN 1, WARN 5, and the deferred `configMapGenerator` name-hash beat |
| **G-14d** | metrics-server release manifest (`kubernetes-sigs/metrics-server`, `components.yaml`) — check Ch 13's corpus first | FAIL #3 (file count), FAIL #4 (composition, 4 sites) |
| **G-14e** | Prior KCNA blueprint evidence for the 8% weight — check Ch 1's corpus first | Both CONTRADICTED findings |
| **G-14f** | Helm 3.0 GA release announcement (date) | FAIL #2 (2 sites) |
| **G-14g** | `helm.sh/docs/helm/helm_upgrade/` or Helm release-lifecycle docs — **already named by the draft's `AUTHOR-REVIEW` at §3** | the declared rollback-counter gap; figure `ch14-fig03`'s `rev 4 ???` cell |

---

## PASS — Verified claims (sample, 34 of 92)

Every quotation below was checked verbatim or near-verbatim against the named snapshot.

**Exam and blueprint**
- "Domain Weight: 16%" → `lf-kcna-exam-page-2026-08-23`: "Cloud Native Application Delivery 16%" ✓
- "CNCF publishes the competency name, 'Application Delivery,' and publishes nothing beneath it" → `cncf-kcna-curriculum-pdf-2026-08-23`: "16% – Cloud Native Application Delivery: Application Delivery; Debugging" — no sub-topics ✓
- "nowhere on the public course outline for LFS250" → `lf-lfs250-course-outline-2026-08-31`: "No sentence on this public course page names Helm or Kustomize." ✓
- "the training course the Linux Foundation bundles with the exam" → same snapshot: "Course + KCNA certification exam – $299" ✓

**Helm — identity and charts**
- Epigraph, verbatim → `helm-homepage-2026-08-31` ✓
- "Helm is a package manager for Kubernetes" → `helm-homepage-2026-08-31`: "The package manager for Kubernetes" ✓
- Fixed Point, chart definition → `helm-charts-2026-08-31`, verbatim on "collection of files that describe a related set of Kubernetes resources" and "packaged into versioned archives to be deployed" ✓
- "a chart describing WordPress lives in a `wordpress/` directory" → `helm-charts-2026-08-31`, verbatim ✓
- "Every chart must have this file" → `helm-glossary-2026-08-31` ✓
- "versioned according to the SemVer 2 specification… a version number is required on every chart" → `helm-glossary-2026-08-31`, verbatim ✓
- "having absorbed the older `requirements.yaml` file in Helm 3" → `helm-changes-since-helm2-2026-08-31`, "Consolidation of `requirements.yaml` into `Chart.yaml`" ✓
- "`values.yaml` holds the default configuration values for the chart" → `helm-charts-2026-08-23` ✓
- "`--values` … rightmost file takes precedence; `--set` … merged into `--values` with higher precedence" → `helm-using-helm-2026-08-31`, both clauses ✓
- "when combined with values, generate valid Kubernetes manifest files" → `helm-charts-2026-08-23` ✓
- "`NOTES.txt` is an optional plain-text file containing short usage notes" → `helm-charts-2026-08-23` ✓
- underscore-prefixed files not rendered, available in other templates; `_helpers.tpl` the default location for partials → `helm-named-templates-2026-08-31`, both ✓
- "`charts/` — a directory containing any charts upon which this chart depends" → `helm-charts-2026-08-23` ✓
- `apiVersion` bumped `v1`→`v2` for library charts + requirements consolidation → `helm-changes-since-helm2-2026-08-31` ✓

**Helm — release and revision**
- "A release is an instance of a chart running in a Kubernetes cluster" → `helm-architecture-2026-08-31`, verbatim ✓
- "the Helm library creates a release to track that installation" → `helm-glossary-2026-08-31` ✓
- "the same chart can be installed many times, each creating a separately named release that can be upgraded and rolled back independently" → `helm-charts-2026-08-23`, verbatim ✓
- "Helm 3 throws an error if no name is provided"; `--generate-name` → `helm-changes-since-helm2-2026-08-31` ✓
- release info stored in the release's own namespace; `helm list` namespace-scoped; `--all-namespaces` → `helm-changes-since-helm2-2026-08-31`, all three ✓
- "Secrets, in the namespace of the release, by default"; `HELM_DRIVER` accepts `configmap`, `secret`, `sql` → `helm-storage-backends-2026-08-31` ✓
- "A sequential counter is used to track releases as they change" → `helm-glossary-2026-08-31`, verbatim ✓
- "`helm upgrade` will only update things that have changed since the last release" → `helm-using-helm-2026-08-31` ✓
- rollback argument shape; omitted-or-`0` → previous release → `helm-rollback-cli-2026-08-31`, verbatim ✓
- "`kubectl rollout undo` operates on … a Deployment, DaemonSet, or StatefulSet" → `k8s-docs-kubectl-rollout-2026-08-24`, valid resource types ✓
- Practice Q4 D → `kubectl rollout pause` "Mark the provided resource as paused" → same snapshot ✓

**Distribution**
- Chart repository = "an HTTP server that houses an `index.yaml` file and optionally some packaged charts"; "plethora of options"; index contents → `helm-chart-repository-2026-08-31`, all three verbatim ✓
- "chart archive: a tarred and gzipped (and optionally signed) chart" → `helm-glossary-2026-08-31` ✓
- Registry = "a service that handles the required APIs defined in this specification"; spec defines distribution of *content* → `oci-distribution-spec-2026-08-24`, both verbatim ✓
- Helm 3.8.0 OCI support; charts+images+artifacts in one registry → `helm-blog-oci-ga-2026-08-31` ✓
- "recommended to use container registries with OCI support"; zero-or-more repositories/charts; `oci://` prefix without basename or tag on push; basename from chart name, tag from semantic version → `helm-oci-registries-2026-08-31`, all four ✓
- Chart Repository API drawbacks (security abstraction, optional provenance, multi-tenant duplication, single index file) and the Distribution project's hardening → `helm-changes-since-helm2-2026-08-31`, all five ✓

**Kustomize**
- "template-free way to customize application configuration"; "built into kubectl as `apply -k`"; overlays layer patches "without forking the originals" → `kustomize-overview-2026-08-23`, all three ✓
- "standalone tool to customize Kubernetes objects through a kustomization file"; "Since 1.14, kubectl also supports…" → `k8s-docs-kustomization-2026-08-31`, both verbatim ✓
- Kustomization as a KRM object that "describes how to generate or transform other KRM objects" → `kubectl-book-kustomization-fields-2026-08-31`, verbatim ✓
- Field descriptions for `resources`, `namespace`, `namePrefix`/`nameSuffix` ("names of all resources and references"), `labels`, `commonAnnotations`, `images`, `replicas`, `patches`, `patchesStrategicMerge`, `patchesJson6902`, `configMapGenerator`, `secretGenerator`, `generatorOptions`, `helmCharts` ("Helm chart inflation generator") → `kubectl-book-kustomization-fields-2026-08-31`, **14 of 14 match the snapshot's field list** ✓

**CRDs**
- "the declaration must be registered before any resources of that CRDs kind(s) can be used" → `helm-crd-best-practices-2026-08-31`, verbatim ✓
- "special directory called `crds`… not templated, but will be installed by default" → same, verbatim ✓
- `--skip-crds`; "no support at this time for upgrading or deleting CRDs using Helm"; `--dry-run` not supported for CRDs; Method 2 separate charts "more useful for cluster operators who have admin access" → same, all four verbatim ✓

**Tiller**
- "one of the first decisions we made regarding Helm 3 was to completely remove Tiller" → `helm-changes-since-helm2-2026-08-31`, verbatim ✓
- RBAC default from Kubernetes 1.6 made lockdown "more difficult to manage"; permissive default "could grant a user a broad range of permissions they weren't intended to have"; Helm 3 permissions "evaluated using your kubeconfig file" → same, all three ✓