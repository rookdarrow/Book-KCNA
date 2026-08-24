# Fact-Accuracy Audit — Chapter 4

**Mode detected: STANDARD.** The `Cached sources` section contains 36 populated snapshots (no `[sources directory is empty]` marker), and the draft carries inline `[source: ...]` tags throughout (32 distinct snapshots referenced). Untagged factual claims are therefore FAIL, not advisory.

**Locator convention:** line numbers below are approximate — this stage received the draft as text, not as a numbered file. Every finding is anchored by **section + verbatim excerpt**, which is the authoritative locator for the revision stage. Cite against `draft-v2.md`.

**Counting rule used:** 118 distinct external factual assertions inspected. Restatements in *Exam Alert*, *Common Traps*, and *Chapter Summary* are counted once against their originating section, with the restatement locations listed inside the finding. Analogies (harbormaster, ship's log, signal flag, hull/ports), prose quality, and internal cross-bearings are out of scope per rules 3 and 4.

---

## Summary

- Total factual claims inspected: **118**
- Tagged claims verified: **105** (of which **8** carry a WARN for scope or attribution drift, listed below)
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0** — every one of the 32 snapshot IDs cited in the draft is present in the corpus
- **Untagged factual claims (FAIL): 7**
- **Contradicted claims (FAIL): 3**
- Minor discrepancies (WARN): **11** (8 tagged-claim drifts + 3 untagged-but-corroborated groupings)

Corpus snapshots present but unused by this chapter: `cncf-kcna-curriculum-pdf-2026-08-23`, `k8s-docs-cluster-addons-2026-08-24`, `k8s-docs-dns-cluster-addon-2026-08-24`, `lf-lfs250-course-outline-2026-08-23`. Two of these are the correct fix targets for findings below.

---

## FAIL — Untagged factual claims

### Line ~8 (front matter, weight note): "CNCF does not publish weights for individual competencies inside a domain"

**Why it's a factual claim:** an assertion about what the certification vendor does and does not publish. It is the load-bearing justification for the book's `~6%` estimate on the same line.
**Corpus status:** supportable by absence — `cncf-kcna-curriculum-pdf-2026-08-23` lists the competencies inside each domain ("44% – Kubernetes Fundamentals: Kubernetes Core Concepts; Administration; Scheduling; Containerization") with **no** per-competency percentages, and `cncf-kcna-certification-page-2026-08-23` publishes only the four domain weights.
**Fix:** append `[source: cncf-kcna-curriculum-pdf-2026-08-23]` to the clause. Low severity, one-token fix, but the claim currently rests on nothing a reader or a later auditor can check.

---

### Line ~318 (§2, 🪝 Snag): "You can type a `status` block into a manifest and apply it; the system will simply overwrite it with what is actually true."

**Why it's a factual claim:** a specific assertion about API-server write behavior (what happens to a client-supplied `status` on apply). Restated untagged at Bearings #1 answer 2, option C: *"writing `status` has no effect. The system overwrites it with what is actually true."*
**Corpus status:** unsupported. `k8s-docs-objects-2026-08-23` establishes only that status is *"supplied and updated by the Kubernetes system and its components"* — that authorship statement does not entail the stronger mechanical claim about what an apply containing `status` does.
**Fix:** either (a) soften to the sourced authorship claim — "`status` is supplied and updated by the system, so anything you write there is not what the object will report" `[source: k8s-docs-objects-2026-08-23]`; or (b) open a research gap for the status-subresource semantics (kubernetes.io/docs/reference/using-api/api-concepts/ or the API conventions doc), since the current corpus has no page covering subresource write behavior.

---

### Line ~635 (§4, figure `ch04-fig05-configmap-secret-contrast`), Secret column: "command and args … read via the Kubernetes API"

**Why it's a factual claim:** the figure asserts a four-way consumption-path parity between ConfigMap and Secret. The figure carries no `[source:]` tag anywhere.
**Corpus status:** the four consumption paths are documented **for ConfigMap only** (`k8s-docs-configmap-2026-08-23`). For Secret, `k8s-docs-secret-2026-08-23` lists uses as *"Set environment variables for a container; provide credentials such as SSH keys or passwords to Pods; allow the kubelet to pull container images from private registries"* — no command-and-args path, no API-read path. The volume path alone is corroborated by `k8s-docs-volumes-2026-08-23` ("secret — used to pass sensitive information … backed by tmpfs").
**Fix:** tag the two supportable rows (`k8s-docs-secret-2026-08-23`, `k8s-docs-volumes-2026-08-23`), and either drop the two unsupported Secret cells or open a research gap for `kubernetes.io/docs/concepts/configuration/secret/` §"Using a Secret" to cache the Secret-side consumption list. As written, the figure's most memorable structural claim (identical middle block, differing only in the last row) is the part the corpus cannot back.

---

### Line ~715 (Bearings #2, answer 3, option B): "in some configurations the projected file content does eventually change on disk"

**Why it's a factual claim:** an assertion about kubelet volume-projection behavior over time, and it partially concedes the opposite of what the chapter's main claim says.
**Corpus status:** unsupported, and in tension with the cited framing. `k8s-docs-configmap-2026-08-23` states only that *"For the first three methods, the kubelet uses the data from the ConfigMap when it launches the container(s) for a Pod."* Nothing in the corpus describes eventual on-disk update of a mounted ConfigMap.
**Fix:** open a research gap for the "Mounted ConfigMaps are updated automatically" section of `kubernetes.io/docs/concepts/configuration/configmap/` (the current snapshot is a partial transcription that stops short of it). This is the single most valuable gap in the chapter: the hedge is doing real pedagogical work in a distractor explanation, and it is currently unciteable. Do **not** delete the hedge — it is the accurate half of a genuinely tricky behavior; source it instead.

---

### Line ~895 (Bearings #3, answer 4, option B): "A namespaced query operates within its namespace scope; it does not cross the boundary"

**Why it's a factual claim:** an assertion about how label-selector queries interact with namespace scope — and it is the *correct answer* to a graded question, so it carries exam weight.
**Corpus status:** unsupported directly. `k8s-docs-namespaces-2026-08-23` establishes namespaces as a scope for names and for resource division, but never states the query-scoping behavior. The tag that *is* present on that answer (`k8s-docs-network-policies-2026-08-23`) supports only the forward-pointer sentence about NetworkPolicy, not the answer itself.
**Fix:** cite `k8s-docs-namespaces-2026-08-23` for the scoping principle, and open a research gap for list-request scoping semantics (`kubernetes.io/docs/reference/kubectl/` on `-n` / `--all-namespaces`, or the API concepts page on namespaced collection URLs) so the graded answer rests on an explicit source.

---

### Line ~672 (§4, forward pointer): "a methodology that predates Kubernetes"

**Why it's a factual claim:** a chronology claim about a third-party authority (The Twelve-Factor App relative to the Kubernetes project).
**Corpus status:** unverifiable. `twelve-factor-app-2026-08-23` carries no publication date; no snapshot dates the Kubernetes project either.
**Fix:** drop the clause (the sentence loses nothing — "Store config in the environment is the third of the twelve factors, and these two objects implement it almost exactly" stands on its own), or open a research gap for a dated source. Low severity; trivially avoidable.

---

### Line ~790 (§5, "The bridge to what you will actually see"): "Older Kubernetes APIs took selectors as flat strings."

**Why it's a factual claim:** an assertion about the historical shape of the Kubernetes API's selector fields.
**Corpus status:** unsupported, and imprecise as stated. `k8s-docs-labels-selectors-2026-08-23` draws only the contrast the draft needs: *"Newer resources such as Job, Deployment, ReplicaSet, and DaemonSet support set-based requirements via matchLabels and matchExpressions."* It says nothing about flat strings; the flat-string form in the corpus is the *query* syntax (`environment = production`), not the older objects' field shape.
**Fix:** replace with the sourced contrast — "Some resource types take only equality-based selectors; the newer resources (Job, Deployment, ReplicaSet, DaemonSet) support set-based requirements through two structured fields" `[source: k8s-docs-labels-selectors-2026-08-23]`. The paragraph's payload (`matchLabels` ≡ `matchExpressions` + `In`) is fully verified and unaffected.

---

## FAIL — Contradicted claims

### Line ~250 (§2, Dead Reckoning): "Four required top-level fields, every object, every time. … Nothing else is structurally required."

**Tag:** `[source: k8s-docs-objects-2026-08-23]`

**Snapshot says:** *"Almost every Kubernetes object includes two nested object fields that govern the object's configuration: the object spec and the object status. **For objects that have a spec**, you have to set this when you create the object…"* — and, listing the manifest fields, *"you'll need to set values for the following fields"* (not "every object, every time").

**Draft says:** "Four required top-level fields, every object, every time." / "That is the complete structural vocabulary. Not a starting subset that gets extended for advanced resources. The complete thing." / "Nothing else is structurally required."

**Why this is a contradiction, not a paraphrase:** the source hedges twice ("Almost every", "For objects that have a spec") and the corpus supplies the counterexample the chapter itself teaches one section later. `k8s-api-ref-secret-v1-2026-08-24` enumerates Secret's fields as `data`, `stringData`, `immutable`, and `type` — **there is no `spec`**. `k8s-docs-configmap-2026-08-23` likewise describes ConfigMap contents as `data` and `binaryData`, never `spec`. So of the six object types this chapter teaches, two do not have the field the chapter calls universally required.

**Restated at (fix all):**
- §2 body, ~line 240: "A Pod manifest has those four fields… A custom resource … has those four fields."
- Bearings #1 answer 1, ~line 378: "`spec` (the desired state, whose internal shape is defined by `kind`)" presented as universal
- Q4 answer, ~line 1118: "The four fields to set are `apiVersion`, `kind`, `metadata`, and `spec`"
- Q16 answer, option C, ~line 1165: "the four required top-level fields are `apiVersion`, `kind`, `metadata`, and `spec`, and `type` is not even among those" — this one is the sharpest instance, because the object under discussion *is* a Secret: `type` is a genuine top-level Secret field, and `spec` is not a field of a Secret at all
- Exam Alert item 1, ~line 968; Chapter Summary row "The four fields", ~line 1213

**Recommended fix:** keep the four-field frame — it is the chapter's best teaching move and is well within the source — but restore the source's own hedge at each site. Suggested wording for the Dead Reckoning: "`apiVersion`, `kind`, and `metadata` on every object; `spec` on almost every object — the documentation's own phrasing is *'for objects that have a spec'*. A few configuration-holding types (ConfigMap, Secret) carry their payload in `data` instead `[source: k8s-api-ref-secret-v1-2026-08-24]`." For Q16 option C, rewrite the rebuttal so it does not assert that a Secret has a `spec`: `type` is a real top-level field of a Secret, it is simply not required, and it defaults to `Opaque` `[source: k8s-docs-secret-2026-08-23]`.

---

### Line ~275 (§2, figure `ch04-fig01-object-anatomy-spec-status`): `uid: ...` placed inside the "YOU AUTHOR THIS" box

**Tag:** figure is untagged; the surrounding section cites `[source: k8s-docs-names-and-uids-2026-08-24]`

**Snapshot says:** *"UIDs — A Kubernetes **systems-generated** string to uniquely identify objects."*

**Draft says:** the figure's upper box is captioned "YOU AUTHOR THIS" and lists `metadata: name / uid / namespace` inside it; the caption below reinforces the reading — *"Four fields above it are yours. The field below it is not."*

**Why this is a contradiction:** the figure asserts client authorship of a field the cited snapshot calls system-generated — and it contradicts the draft's own prose two paragraphs above ("A **UID** is a system-generated string"). Since the figure exists specifically to teach the authorship boundary, this is the one cell in the chapter where a reader is most likely to absorb the wrong fact. The Dead Reckoning block at ~line 250 repeats the error in text: "`metadata`: an object holding identity. `name` (a string), `uid`, and an optional `namespace`" appears under the heading "Four required top-level fields" — implying `uid` is something you supply.

**Recommended fix:** in the figure, annotate the `uid` line as system-supplied — e.g. `uid: ...            (system-generated)` — or move it below the authorship rule with `status`. In the Dead Reckoning, change to: "`metadata`: an object holding identity. `name` (you supply), `uid` (the system supplies), and an optional `namespace`." Note that listing `uid` under `metadata` is itself correct and sourced — `k8s-docs-objects-2026-08-23` describes metadata as *"including a name string, UID, and optional namespace"*. Only the authorship attribution is wrong.

---

### Line ~1141 (Practice Questions, Q9 answer, rebuttal to option B): "an object whose manifest omits a namespace lands in `default`"

**Tag:** `[source: k8s-docs-namespaces-2026-08-23]`

**Snapshot says:** *"default — Kubernetes includes this namespace so that you can start using your new cluster without first creating a namespace."* That is a statement about why the namespace exists. The snapshot nowhere states a fallback rule for manifests that omit `metadata.namespace`.

**Counter-evidence in the corpus:** `k8s-docs-kubectl-overview-2026-08-23` states that *"When kubectl runs in a cluster it acts against the namespace of the ServiceAccount unless `--namespace` is given"* — a documented case where an omitted namespace resolves to something other than `default`. The target namespace comes from the request context (kubeconfig current-context, in-cluster ServiceAccount, or `--namespace`), not from an unconditional platform default.

**Draft says:** "an object whose manifest omits a namespace lands in `default`, which exists precisely so that you can start using a new cluster without first creating a namespace."

**Recommended fix:** narrow to the context-dependent truth and keep the sourced second half: "an object whose manifest omits a namespace lands in whichever namespace the request context supplies — `default` on a fresh kubeconfig, the ServiceAccount's namespace when `kubectl` runs inside the cluster `[source: k8s-docs-kubectl-overview-2026-08-23]` — and `default` exists precisely so that you can start using a new cluster without first creating a namespace `[source: k8s-docs-namespaces-2026-08-23]`." The distractor rebuttal's actual job (killing "`kube-system` is the fallback") survives intact.

---

## WARN — Minor discrepancies

**1. Line ~400, ~1103, ~68 — "Every read and write of cluster state goes through the API server."** Tagged `[source: k8s-docs-cluster-architecture-2026-08-23]`. That snapshot supports only *"The API server is the front end for the Kubernetes control plane"* and *"etcd — … backing store for all cluster data."* The absolute form is better supported by `k8s-docs-control-plane-node-communication-2026-08-24` plus `k8s-docs-etcd-access-control-2026-08-24`, and the latter states it as an ideal, not an invariant: *"ideally only the API server should have access to it."* Appears at Bearings #1 answer 5, Q1 answer, and (untagged) Soundings answer 4. **Fix:** add the two corroborating tags, or soften to "every read and write of cluster state is *meant* to go through the API server."

**2. Line ~1112 — Q3, rebuttal to option B: "all API usage terminates at the API server."** Tagged `[source: k8s-docs-control-plane-node-communication-2026-08-24]`. Snapshot: *"All API usage **from nodes (or the pods they run)** terminates at the API server."* The dropped qualifier widens the claim beyond what the source establishes. The second half the draft quotes — *"None of the other control plane components are designed to expose remote services"* — is verbatim and is the sentence that actually kills the distractor. **Fix:** restore the qualifier or lead with the second sentence.

**3. Line ~250 — Dead Reckoning: "`apiVersion`: a string naming the API group and version this object belongs to."** Tagged `[source: k8s-docs-objects-2026-08-23]`, which says only *"which version of the Kubernetes API you're using to create this object."* API *groups* appear nowhere in that snapshot. The statement is not wrong, but it is attributed to a source that does not contain it. **Fix:** trim to the source's wording, or open a small gap for the API-groups page if the group/version shape is wanted at associate tier.

**4. Line ~838 — §5 comparison table, label value row: "Character set — Constrained: alphanumerics, dashes, underscores, dots."** Tagged `[source: k8s-docs-labels-selectors-2026-08-23]`, whose only statement about *values* is *"Valid label values must be 63 characters or less (can be empty)."* The alphanumeric/dash/underscore/dot rule in that snapshot governs **key name segments**, not values. The "constrained" claim itself is corroborated obliquely by `k8s-docs-annotations-2026-08-24` (*"unlike label values, annotation values may contain any string"*). **Fix:** cite the annotations snapshot for "constrained" and open a research gap to re-snapshot the labels page's value-syntax sentence, or reduce the cell to the sourced length limit.

**5. Line ~845 — §5: "Both keys and values must be strings in either case: you cannot use numbers, booleans, or lists."** Tagged `[source: k8s-docs-annotations-2026-08-24]`, which states this about annotations only (*"The keys and the values in the map must be strings"*). Extending "in either case" to labels has no labels-page citation in the corpus. **Fix:** scope the sentence to annotations, or source the label side separately.

**6. Line ~508 — §4 opening: "Chapter 2 established that images are immutable."** Tagged `[source: k8s-docs-containers-2026-08-23]`, which says *"**Containers** are intended to be stateless and immutable."* In the corpus, image-level immutability attaches specifically to digests — `k8s-docs-images-2026-08-23`: *"Digests are a unique identifier for a specific version of an image … and are immutable; **tags can be moved** to point to different images."* Calling images flatly immutable is loose against a corpus that explicitly says tags are not. The rest of the sentence ("build a new image and recreate the container") is verbatim-supported. **Fix:** "Chapter 2 established that a running container is not edited in place."

**7. Line ~635 — figure `ch04-fig05`, "Stored" row, ConfigMap cell: "unencrypted, in etcd"** with no "(by default)" qualifier, while the Secret cell gets one. Encryption at rest is a cluster configuration that covers API objects generally — `k8s-docs-cloud-native-security-2026-08-23`: *"enable encryption at rest for API objects."* The asymmetry implies a ConfigMap cannot be encrypted at rest where a Secret can. **Fix:** apply "(by default)" to both cells. This matters because the figure caption tells the reader the third row is "the row people get wrong."

**8. Line ~808 — §5: "Kubernetes' permission model … names its subjects and its resources explicitly; it does not select them by label."** Tagged `[source: k8s-docs-rbac-2026-08-23]`. The snapshot supports the positive half — a role binding *"holds a list of subjects (users, groups, or service accounts), and a reference to the role being granted"* — but never states the negative. The claim is inferred from absence. **Fix:** rephrase as the positive ("RBAC binds to an explicit list of subjects") and let the contrast with selectors do the work implicitly, or mark it as an authorial inference.

**9. Line ~812 — §5 aside: "field selectors, which select on an object's field values rather than its labels."** Tagged `[source: k8s-docs-objects-2026-08-23]`, which lists "Field Selectors" in a related-topics line and supplies no definition. **Fix:** drop the definitional clause (the aside's stated purpose is name-recognition only) or gap the field-selectors page.

**10. Line ~205 / ~948 / ~1130 — "`kubectl scale` … edits a number in a `spec`."** Tagged `[source: k8s-docs-kubectl-overview-2026-08-23]`, which says only *"scale — Update the size of the specified replication controller / deployment."* The mechanism — which field is written, and through which endpoint — is not in the corpus. The observable outcome the chapter builds §6 on (the imperative command changes a declaration, then a controller reconciles) is consistent with `k8s-docs-objects-2026-08-23`'s replica worked example, so this is attribution drift rather than an error. **Fix:** pair the `kubectl` tag with `[source: k8s-docs-objects-2026-08-23]` where the spec-editing reading is asserted.

**11. Untagged but fully corroborated elsewhere — tag recommended, no correction needed.** Three groupings, all restating material the chapter sources properly a few pages later: (a) 🧭 Soundings answers 1–8, ~lines 62–86 — the declarative/imperative distinction (`k8s-docs-custom-resources-2026-08-23`), the control-loop triad (`k8s-docs-controllers-2026-08-23`), the base64 answer (`k8s-docs-secrets-good-practices-2026-08-24`), and the namespace answer (`k8s-docs-namespaces-2026-08-23`); (b) §2, ~line 240 — "a Pod, for now, being the unit Kubernetes schedules and runs" (`k8s-docs-workloads-2026-08-23`, `k8s-docs-pod-lifecycle-2026-08-23`); (c) §6, ~lines 918–930 — the noun-inventory recap, which restates §§1–5. If the chapter's convention is that pre-chapter diagnostics stay untagged, state that convention once in the front matter so this audit and the next one can score it consistently.

---

## PASS — Verified claims

Sampled tagged claims whose text matches the referenced snapshot. Grouped by snapshot for coverage evidence; this list is a sample of the 105, weighted toward exam-critical facts.

**`k8s-docs-objects-2026-08-23`** — "record of intent" and *"constantly work to ensure that the object exists"* (§1, verbatim); the three things objects describe — running applications and their nodes, available resources, behavior policies (§1); *"Almost every Kubernetes object includes two nested object fields"* and the spec/status authorship split (§2); the Deployment three-replicas worked example, including *"a status change"* and the correction (§2); the four field definitions as listed in the manifest section (§2); `kubectl apply -f <manifest>` (§2); the control plane *"continually and actively manages every object's actual state to match the desired state you supplied"* (§2, §6, Q6, Bearings #1 answer 3).

**`k8s-docs-overview-2026-08-23`** — the epigraph *"It shouldn't matter how you get from A to C"* (attributed to *Overview*, correct page); the full "not a mere orchestration system" block quote (§1, verbatim including *"first do A, then B, then C"*).

**`k8s-docs-object-management-2026-08-24`** — the three-technique table, all four reproduced columns (§1); *"the recommended way to get started or to run a one-off task in a cluster"*; *"it provides no history of previous configurations"*; `kubectl create deployment nginx --image nginx`; the imperative-object-configuration file requirement; *"Create, update, and delete operations are automatically detected per-object by kubectl"*; the undefined-behavior warning (verbatim); the source-control / review / template advantages and the schema-understanding cost (Closer Look).

**`k8s-docs-names-and-uids-2026-08-24`** — *"Only one object of a given kind can have a given name at a time"* and name reuse after deletion; *"Every object created over the whole lifetime of a Kubernetes cluster has a distinct UID"*; *"intended to distinguish between historical occurrences of similar entities"* (§2, Chapter Summary, and reused correctly in *The Voyage Ahead*).

**`k8s-docs-namespaces-2026-08-23`** — the isolation/unique-within-not-across opener; the many-users guidance including *"you should not need to create or think about namespaces at all"*; no nesting, one namespace per resource; the versions-belong-in-labels correction (§3, Bearings #2 answer 2, Q8); cluster-wide examples StorageClass / Nodes / PersistentVolumes and *"namespace resources are not themselves in a namespace"*; all four initial namespaces with their documented purposes; *"the public aspect of this namespace is only a convention, not a requirement"* (§3, Exam Alert, Q9); the production advice against `default`; the `<service-name>.<namespace-name>.svc.cluster.local` form and FQDN requirement; resource quota as the division mechanism; `kubectl api-resources --namespaced=true|false`.

**`k8s-docs-configmap-2026-08-23`** — the ConfigMap definition and portability rationale; the `DATABASE_HOST` local/cloud worked example; the **1 MiB** ceiling and the volume/database/file-service alternative (§4, Q14, Exam Alert); the same-namespace requirement (§4, Q15); the four consumption paths and the first-three-at-launch / fourth-subscribes asymmetry (§4, Bearings #2 answer 3, Q12); v1.19 `immutable`, its irreversibility, and `data`/`binaryData` coverage (§4, Q13); *"ConfigMap does not provide secrecy or encryption."*

**`k8s-docs-secret-2026-08-23`** — the Secret definition (*"a small amount of sensitive data such as a password, a token, or a key"*, correctly reused to rebut Q14 option C); the unencrypted-in-etcd caution block including the Pod-creation and Deployment indirect-access clauses (§4 quote, Fixed Point, Q11); the four safety steps; **all eight rows** of the built-in Secret types table, checked individually against the snapshot table; `Opaque` as the default (§4, Q16); `kubernetes.io/service-account-token` as legacy long-lived, superseded since v1.22.

**`k8s-docs-secrets-good-practices-2026-08-24`** — *"Base64 encoding is not an encryption method, it provides no additional confidentiality over plain text"* (§4, Hazards, Exam Alert, Q11, Chapter Summary); *"Secret values are encoded as base64 strings and are stored unencrypted by default, but can be configured to be encrypted at rest"*; the shared-manifest / source-repository consequence.

**`k8s-api-ref-secret-v1-2026-08-24` / `k8s-docs-secret-config-file-2026-08-24`** — `data` as base64-encoded and the serialized-form statement (dual-tagged, both support it); *"facilitate programmatic handling of secret data"* as the purpose of `type` (§4, Q16).

**`k8s-docs-labels-selectors-2026-08-23`** — the labels definition including *"do not directly imply semantics to the core system"*; the loosely-coupled organizational-mapping sentence; all five example label families reproduced exactly; key syntax (63-char name segment, optional ≤253-char DNS-subdomain prefix, reserved `kubernetes.io/` and `k8s.io/`) and the 63-char value limit (§5, Q20 options A/B/D); *"the label selector is the core grouping primitive in Kubernetes"* (Fixed Point, Q19, Q21); equality-based `=` `==` `!=` and set-based `in` `notin` `exists` with `!partition` negation (§5, Q17); more-expressive and comma-ANDed (Q17 option C rebuttal); the four newer resources (Job, Deployment, ReplicaSet, DaemonSet); **`matchLabels` ≡ `matchExpressions` with operator `In`** (§5, Bearings #3 answer 2, Q18).

**`k8s-docs-annotations-2026-08-24`** — *"arbitrary non-identifying metadata"*; the labels-select / annotations-do-not contrast (verbatim); the full recorded-information list (build/release info, logging pointers, client library info, rollout metadata, pager numbers); shared key syntax and reserved prefixes; *"no character set restrictions"* for values; the **256 KiB** per-object total (§5 table, Q20 option D).

**`k8s-docs-controllers-2026-08-23`** — desired-vs-current comparison and acting on the difference (§2, Q2); *"non-terminating loop that regulates the state of a system"* (Q2 rebuttal); the Job-controller passage including *"the Job controller does not run any Pods or containers itself"* and *"tells the API server to create or remove Pods"* (Q3, verbatim).

**`k8s-docs-cluster-architecture-2026-08-23`** — etcd as *"backing store for all cluster data"*; the scheduler's job as watching for Pods with no assigned node (Q1 option C rebuttal).

**`k8s-docs-control-plane-node-communication-2026-08-24` / `k8s-docs-etcd-access-control-2026-08-24`** — *"None of the other control plane components are designed to expose remote services"*; *"Access to etcd is equivalent to root permission in the cluster so ideally only the API server should have access to it"* (Q3 option C rebuttal, verbatim).

**`k8s-docs-images-2026-08-23`** — the **five** private-registry mechanisms, all five enumerated correctly (§4, Bearings #2 answer 4); `imagePullSecrets` as a Secret of type `kubernetes.io/dockerconfigjson`.

**`k8s-docs-service-accounts-2026-08-23`** — ServiceAccounts namespaced, every namespace getting a `default` on creation (Bearings #2 answer 1, Q7); TokenRequest short-lived rotating tokens since v1.22.

**`k8s-docs-volumes-2026-08-23`** — configMap and secret as volume types; the `subPath` mount exception (*"will not receive updates when the ConfigMap changes"*, Bearings #2 answer 3).

**`k8s-docs-containers-2026-08-23`** — build-a-new-image-and-recreate as the correct change path (§4, Q13 option A rebuttal).

**`k8s-docs-nodes-2026-08-23`** — node controller updating the Ready condition and triggering eviction when a node stays unreachable (§3 `kube-node-lease` forward pointer).

**`k8s-docs-service-2026-08-23` / `k8s-docs-assign-pod-node-2026-08-23` / `k8s-docs-network-policies-2026-08-23` / `k8s-docs-rbac-2026-08-23`** — the four §5 forward pointers: Service selecting its backing Pods; *"the recommended approaches all use label selectors to facilitate the selection"*; NetworkPolicy using a selector to specify allowed traffic to and from matching Pods; RBAC's explicit subject lists.

**`k8s-docs-cloud-native-security-2026-08-23`** — *"Kubernetes uses TLS to protect API traffic"* (Q11 option B rebuttal).

**`k8s-docs-workloads-2026-08-23` / `k8s-docs-pod-lifecycle-2026-08-23`** — *"a Pod represents a set of one or more running containers on your cluster"*; *"relatively ephemeral (rather than durable)"*; *"A Pod is never 'rescheduled' to a different node; instead, it is replaced by a new, near-identical Pod with a different UID"* (*The Voyage Ahead* — the UID callback is correctly grounded in both snapshots).

**`cncf-kcna-certification-page-2026-08-23`** — Kubernetes Fundamentals at 44% of the exam (front matter). The `~6%` competency figure is correctly disclosed as a book estimate rather than presented as published.

**`twelve-factor-app-2026-08-23`** — "Store config in the environment" as factor **III** (§4 forward pointer).