# Fact-Accuracy Audit — Chapter 16

**Mode detected: STANDARD.** The draft carries ~60 inline `[source: ...]` tags and the cached-sources section is populated (24 snapshots). Untagged factual claims are therefore reported as FAIL.

**Anchoring note:** the draft was supplied inline without line numbers, so every finding is anchored by section + verbatim excerpt rather than by line. Anchors are exact strings; the revision stage can locate each by search.

**Corpus caveat that shapes this report — read first.** Several packed snapshots terminate at their first code fence, mid-page:

| Snapshot | Packed body ends at |
|---|---|
| `k8s-docs-debug-init-containers-2026-08-31` | "Display your pod's status:" |
| `k8s-docs-debug-service-2026-08-31` | "...run an interactive busybox Pod:" |
| `k8s-docs-debug-pods-2026-08-31` | "...with the following command:" |
| `k8s-docs-debug-statefulset-2026-08-31` | "...you can use the following:" |
| `k8s-docs-kubectl-debug-reference-2026-08-31` | "## Synopsis" |
| `k8s-docs-debug-running-pod-2026-08-31` | "...look at the logs of the affected container:" |
| `k8s-docs-get-shell-running-container-2026-08-31` | "...then get a shell to it:" |
| `k8s-docs-determine-reason-pod-failure-2026-08-31` | end of the exercise intro |
| `k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31` | "...using `kubectl run`:" |
| `k8s-docs-port-forward-2026-08-31` | "...to port forward to." |
| `k8s-docs-troubleshoot-kubectl-2026-08-31` | "Check kubectl version:" |

Nine tagged claims are reported **unverifiable** solely because of this. Their frontmatter (`concepts_covered`, `transcription_note`) asserts the passage exists on disk. **Do not edit those claims on the strength of this report** — re-run the audit against the untruncated snapshot files first. Everything in the FAIL and CONTRADICTED sections below was assessed against snapshot text that *is* present, and stands on its own.

## Summary

- Total factual claims inspected: **97**
- Tagged claims verified: **44**
- Tagged claims unverifiable (packed snapshot truncated before the cited passage): **9**
- **Untagged factual claims (FAIL): 24**
- **Contradicted claims (FAIL): 1 claim family, 6 instances**
- Minor discrepancies (WARN): **15**

---

## FAIL — Contradicted claims

### The endpoint-list model: "not Ready ⇒ absent from the list"

**Tag:** `[source: k8s-docs-debug-pods-2026-08-23]` (§4 Fixed Point and Exam Alert item 4); untagged at the other four instances.

**Snapshot says** (`k8s-docs-endpointslices-2026-08-24`):

> "The control plane automatically creates EndpointSlices for any Kubernetes Service that has a selector specified. **These EndpointSlices include references to all the Pods that match the Service selector.**"

and, in the Conditions section:

> "The EndpointSlice API stores conditions about endpoints that may be useful for consumers. The three conditions are `serving`, `terminating`, and `ready`. ... The `serving` condition indicates that the endpoint is currently serving responses... For endpoints backed by a Pod, this maps to the Pod's `Ready` condition."

**Draft says**, in six places:

1. §4 Break 2 — "The Pods match perfectly. The selector is correct. And every one of them is `0/1 READY`, **so none of them is in the list**. Readiness gates endpoint membership — a Pod that is not ready is not a valid target, and **the control plane removes it**."
2. §4 Fixed Point — "**A Service with no endpoints** is not broken... There are two causes... the selector does not match the Pod labels, **or the Pods match but are not Ready**."
3. §4 figure `ch16-fig04` — "BREAK 1+2 / **LIST EMPTY** / 1 selector mismatch / 2 not Ready".
4. Soundings A3 — "**It has been removed from the endpoint list**, or was never added."
5. Checkpoint 2, Q1 stem (graded) — "returns a slice with **zero endpoints**. `kubectl get pods -l app=api` returns three Pods, all `Running`, all `0/1 READY`."
6. Exam Alert item 4 — "**An empty endpoint list** has two causes — selector mismatch, or Pods not Ready."

**Why this is a contradiction, not a paraphrase.** Under the EndpointSlice API documented in the snapshot, a Pod that matches the selector but is not Ready is **present in the slice with `ready: false`** — it is not removed and the slice is not empty. What goes to zero is the count of *ready* endpoints, not the endpoint count. The draft is describing the pre-EndpointSlice `Endpoints` behaviour, where not-ready addresses landed in `notReadyAddresses` and `kubectl get endpoints` printed `<none>`. Instance 5 is the sharpest failure: the stem asserts a state (`zero endpoints` alongside three selector-matching Pods) that the cited API does not produce, and the reader is graded on it.

Note that `k8s-docs-debug-pods-2026-08-23` — the snapshot the draft tags — does **not** license the stronger claim. It says only:

> "Make sure that the endpoints in the EndpointSlices match up with the number of pods that you expect to be members of your service. If they don't, the Service's selector probably does not match the Pods' labels, or the Pods are not Ready."

That is a claim about a *count mismatch against expectation*, which is compatible with both models. The two-cause diagnosis survives; "empty list" does not.

**Recommended fix** — a precision edit, not a restructure. The section's whole architecture (upstream/downstream, two causes two files) is sound and worth keeping.

- Replace "empty list" with **"no ready endpoints"** throughout §4, the figure, Soundings A3, and Exam Alert 4.
- §4 Break 2: replace "so none of them is in the list... the control plane removes it" with something like: *"and every endpoint in the slice carries `ready: false`. Readiness does not remove an endpoint from the slice — it marks it. Service proxies skip it, which is the same outcome for your traffic and a different thing on the screen."* Tag `[source: k8s-docs-endpointslices-2026-08-24]`.
- Checkpoint 2 Q1 stem: change "returns a slice with zero endpoints" to "returns a slice whose three endpoints all show `ready: false`". Answer B and the distractor rationales for A, C and D all remain correct as written.
- The §4 Snag's one-command discriminator still works and is arguably *strengthened* by the correction: an empty label query means mismatch; a populated slice with `ready: false` conditions means readiness. Consider saying so explicitly.
- Practice Q10 is unaffected (its stem has **no** matching Pods, so a genuinely empty slice is correct). Practice Q11 is unaffected.

---

## FAIL — Untagged factual claims

Each entry is marked **[tag only]** — the supporting snapshot is already in this chapter's corpus and the fix is adding a tag — or **[research gap]** — no cached snapshot supports it, and the research manifest needs an entry.

### §"Why This Chapter Matters": "That domain doubled from the previous blueprint, which means prep material written against the old five-domain shape under-serves this material more than any other part of the exam."

**Why it's a factual claim:** two assertions about a retired CNCF exam blueprint — that it had five domains, and that Cloud Native Application Delivery was weighted at half its current 16%.
**Status:** **[research gap]** — `cncf-kcna-curriculum-pdf-2026-08-23` documents only the current four-domain shape (44/28/16/12). Nothing in the corpus describes any prior blueprint.
**Fix:** Open a research gap for an archived/retired KCNA curriculum PDF or a dated CNCF changelog. Until one is cached, either cut the sentence or reduce it to something the current snapshot supports — e.g. "Cloud Native Application Delivery is 16% of the exam, and Debugging is one of its two competencies" — with no comparative claim. **This is the highest-priority untagged claim in the chapter**: it is an exam-structure assertion, it is the chapter's stated justification for its own weight, and it is exactly the class of claim a reader will act on when choosing study material.

### Epigraph: *"The first step in troubleshooting is triage. What is the problem?"* — Kubernetes documentation, *Debug Pods*

**Why it's a factual claim:** a direct quotation attributed to a named external authority.
**Status:** **[tag only]** — present verbatim in `k8s-docs-debug-pods-2026-08-31`. Page attribution is correct.
**Fix:** Add `[source: k8s-docs-debug-pods-2026-08-31]`. See also WARN-1 (truncation).

### §3 Navigational Hazards: "The ephemeral container you are injecting is subject to the same Pod Security Admission enforcement as any other container in that namespace. In a namespace enforcing the `restricted` standard, a debug image that wants to run as root... is going to be refused at the admission gate."

**Why it's a factual claim:** asserts specific admission-controller behaviour toward the `ephemeralcontainers` subresource, and a specific enforcement outcome under a named Pod Security Standard.
**Status:** **[research gap]** — no Pod Security Admission or Pod Security Standards snapshot exists in this chapter's corpus. `k8s-docs-ephemeral-containers-concept-2026-08-31` lists the API-level restrictions on ephemeral containers and says nothing about admission.
**Fix:** Cache `https://kubernetes.io/docs/concepts/security/pod-security-admission/` and `.../pod-security-standards/`. **Second-highest priority**: the claim is stated at maximum confidence ("the single most likely way `kubectl debug` fails on a cluster you do not own"), it anchors a Hazard, it is re-tested as **Practice Q9**, and its correct answer B depends entirely on it. It is also the load-bearing justification for the `restricted` debug profile sentence below.

### §3 Debug profiles: "The `restricted` profile exists precisely so that a debug container can be injected into a namespace enforcing the restricted standard."

**Why it's a factual claim:** asserts design intent and a compatibility guarantee between a kubectl flag value and a Pod Security Standard.
**Status:** **[research gap]** — depends on the PSA gap above plus the truncated profile reference.
**Fix:** Same snapshots. Soften to a shape claim until sourced.

### Practice Q6, distractor D rationale: "`kubectl cp` depends on `tar` being present *in the container image*. A distroless image does not have it either."

**Why it's a factual claim:** a specific implementation dependency of a kubectl subcommand.
**Status:** **[research gap]** — no `kubectl cp` snapshot in the corpus.
**Fix:** Cache `https://kubernetes.io/docs/reference/kubectl/generated/kubectl_cp/`. This is graded text; a wrong distractor rationale teaches a wrong fact.

### §4 Break 3 / Soundings A4 / Checkpoint 2 Q2 / Practice Q11: the `port` vs `targetPort` definition — "`port` is the port the Service is reachable at. `targetPort` is the port on the Pod that traffic is forwarded to, and it is the one that has to match what the container actually binds."

**Why it's a factual claim:** the semantics of two Service API fields.
**Status:** **[research gap in the packed corpus]** — `k8s-docs-debug-service-2026-08-31` lists `port-versus-targetport` in `concepts_covered`, but its packed body ends before any port discussion, and no other snapshot defines either field.
**Fix:** Re-verify against the untruncated `debug-service` snapshot; if the definition genuinely is not on that page, cache `https://kubernetes.io/docs/concepts/services-networking/service/`. This claim appears **four times**, twice in graded text (Checkpoint 2 Q2, Practice Q11), and Checkpoint 2 Q2's distractor D turns on a fine distinction between `containerPort` and `targetPort` that no cached snapshot supports at all.

### Soundings A5 / §4 Break 4: "The in-cluster form is `<service>.<namespace>.svc.<cluster-domain>` and a short name resolves relative to the *client's* namespace, not the service's."

**Why it's a factual claim:** the DNS record shape Kubernetes publishes, and search-domain resolution order.
**Status:** **[tag only]** — `k8s-docs-dns-pod-service-2026-08-23` carries both halves: "a name of the form my-svc.my-namespace.svc.cluster-domain.example" and "By default, a client Pod's DNS search list includes the Pod's own namespace and the cluster's default domain."
**Fix:** Tag `[source: k8s-docs-dns-pod-service-2026-08-23]` at both locations. Also reachable at Checkpoint 2 Q5 and Practice Q12, both graded on it.

### Soundings A2: "Init containers run in order and each must exit successfully before the next starts. The Pod stays in `Pending` with the `Initialized` condition false."

**Status:** **[tag only]** — `k8s-docs-init-containers-2026-08-24`: "Each init container must complete successfully before the next one starts" and "A Pod that is initializing is in the `Pending` state but should have a condition `Initialized` set to false."
**Fix:** Tag. Same claim recurs untagged in §2 ("The Pod's phase is `Pending` throughout, with the `Initialized` condition false") and in Practice Q3 distractor D.

### Soundings A3: readiness and endpoint membership

**Status:** **[tag only]**, but see the CONTRADICTED section — this instance needs the correction applied before the tag is added.

### Soundings A7: "The default retention policy is `Retain` for both the scale-down and the delete case, and a Pod replaced after a node failure keeps its existing claim entirely."

**Status:** **[tag only]** — `k8s-docs-statefulset-storage-2026-08-25` supports both clauses verbatim (the same two sentences §6 already quotes correctly).
**Fix:** Tag `[source: k8s-docs-statefulset-storage-2026-08-25]`.

### §2: "If you don't know its name, `kubectl describe pod <pod>` lists the init containers in order, along with each one's state and exit code."

**Why it's a factual claim:** asserts specific fields present in a specific command's output.
**Status:** **[research gap]** — `k8s-docs-debug-pods-2026-08-23` mentions `kubectl describe pods` only generically ("Check the current state of the Pod and recent events"); nothing documents init-container state or exit codes in that output.
**Fix:** Likely present on the untruncated `debug-init-containers` page. Verify there first.

### §2: "Init containers are your only ordering primitive inside a Pod"

**Why it's a factual claim:** an absolute claim about what Kubernetes does and does not provide.
**Status:** **[research gap]**, and overstated — `k8s-docs-init-containers-2026-08-24` documents sidecar containers as a distinct mechanism with lifecycle and probe support, and the corpus contains no statement that init containers are the *only* ordering primitive.
**Fix:** Soften to "your primary ordering primitive inside a Pod," or scope it: "the only mechanism that blocks app-container startup until a precondition is met" — which `init-containers` *does* support ("init containers offer a mechanism to block or delay app container startup until a set of preconditions are met").

### §2 "Ordering" subsection (the deadlock shape) — entire subsection

**Why it's a factual claim:** describes a specific, reproducible Kubernetes failure mode and its observable signature (`Init:0/1`, no error, no restarts).
**Status:** **[research gap]** — explicitly acknowledged by the corpus itself. `k8s-docs-debug-init-containers-2026-08-31` `scope_note`: *"It does NOT cover init-container ordering deadlocks, idempotency/re-run hazards, or ConfigMap/Secret mount failures at init. Those parts of Ch 16 section 2 are NOT sourced here — see manifest Gaps item 3."*
**Fix:** The gap is already recorded. Either cache a source that documents the deadlock shape, or mark the subsection as authored practitioner analysis rather than documented behaviour. Note that the ordering premise it rests on *is* sourced (init containers block app-container start), so only the deadlock synthesis is unsupported. Also reaches **Practice Q5**, graded.

### §2 "Configuration errors visible at init" subsection

**Status:** **[research gap]** — same `scope_note`, same manifest Gaps item 3. Same disposition.

### §3: "The double dash matters. Everything after `--` is the command run inside the container; everything before it belongs to kubectl."

**Why it's a factual claim:** CLI argument-parsing semantics.
**Status:** **[research gap in the packed corpus]** — `k8s-docs-get-shell-running-container-2026-08-31` is truncated before any command form.
**Fix:** Verify against the untruncated snapshot; its `transcription_note` says "Commands are exact," so the form is likely there.

### §3: "The `--target` flag matters for a distroless container specifically: it puts the debug container in the target container's process namespace, so you can see and interact with the target's processes."

**Why it's a factual claim:** specific behaviour of a specific flag.
**Status:** **[research gap]** — and the sentence that follows it does *not* support it; see WARN-5.
**Fix:** Verify against the untruncated `kubectl-debug-reference` flag table, which should carry a `--target` description.

### §3: "This creates a Pod on the target node with the node's filesystem mounted and access to the host namespaces." (`kubectl debug node/`)

**Status:** **[research gap in the packed corpus]** — `k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31` covers this section on disk (its note says "Complete from the 'Debugging using a copy of the Pod' heading to end of document") but the packed body stops well short.
**Fix:** Verify against the untruncated snapshot and tag.

### §3 Worth Securing: "if the copy inherits the original's labels, it may start receiving live traffic. Some copy modes strip labels for exactly this reason; check what yours did before assuming."

**Why it's a factual claim:** asserts label-handling behaviour of `kubectl debug --copy-to`, hedged to the point of being unfalsifiable.
**Status:** **[research gap]**, and the hedge is doing real work — "some copy modes" names nothing checkable, and the advice ("check what yours did") pushes verification onto the reader because the draft could not verify it.
**Fix:** Verify against the untruncated `kubectl-debug-reference`, then state the actual behaviour flatly. If it cannot be pinned, cut the second sentence and keep only the cleanup instruction, which needs no source.

### §4: "That label is not arbitrary — the control plane puts a `kubernetes.io/service-name` label on every EndpointSlice it creates"

**Status:** **[tag only]**, with a wording caveat — `k8s-docs-endpointslices-2026-08-24`: "**In most use cases**, EndpointSlices are owned by the Service... This ownership is indicated by an owner reference on each EndpointSlice as well as a `kubernetes.io/service-name` label."
**Fix:** Tag `[source: k8s-docs-endpointslices-2026-08-24]` and see WARN-7 on "every."

### §5 figure `ch16-fig03`: "kubectl ──▶ API server ──▶ **kubelet** ──▶ Pod:port"

**Why it's a factual claim:** a diagram asserting the hop sequence of a request path.
**Status:** **[research gap]** — already flagged by the draft's own AUTHOR-REVIEW comment, and confirmed here. `k8s-docs-port-forward-authorization-2026-08-31`'s `significance` note says exactly this: *"the full path (API server -> kubelet -> Pod) is still NOT stated on any page found."* The API-server hop is established by the `pods/portforward` subresource; the kubelet hop is not.
**Fix:** Redraw the figure to stop at the API server (`kubectl ──▶ API server ──▶ Pod:port`, annotated `pods/portforward subresource`). The section's argument — that the two paths share no step but the Pod — does not need the kubelet hop and is fully carried by the subresource evidence.

### §5: "Also: it is TCP only, and it terminates when you stop the command."

**Status:** **[research gap in the packed corpus]** — `k8s-docs-port-forward-2026-08-31`'s note says "the command forms, **the TCP-only note**, and the Discussion section are complete," but the packed body stops before all three.
**Fix:** Verify against the untruncated snapshot and tag.

### §6 Snag: "A StatefulSet whose `serviceName` names a Service that does not exist will run, and its Pods will have no resolvable per-Pod DNS names."

**Why it's a factual claim:** asserts the controller's behaviour when a referenced object is absent.
**Status:** **[research gap]** — `k8s-docs-statefulset-2026-08-24` establishes that a headless Service is required and that you must create it, but says nothing about what happens when it is missing. The consequence is a reasonable inference; it is not documented.
**Fix:** Either source it or reframe as inference: "...which means a `serviceName` pointing at a Service nobody created leaves you with Pods that run and cannot find each other." The first half of the Snag (creation responsibility) is correctly tagged and verified — keep it.

### §6: "Each StatefulSet replica gets its own PersistentVolumeClaim from `volumeClaimTemplates`, and that claim follows the identity"

**Status:** **[tag only]** — `k8s-docs-statefulset-2026-08-24`: "For each VolumeClaimTemplate entry defined in a StatefulSet, each Pod receives one PersistentVolumeClaim... The same PersistentVolumeClaim will be bound to a Pod throughout its lifecycle."
**Fix:** Tag `[source: k8s-docs-statefulset-2026-08-24]`.

### §7 Closer Look: "running a small local cluster — kind, minikube, or k3s"

**Why it's a factual claim:** names three third-party products as fit for a stated purpose.
**Status:** **[research gap]** — `k8s-docs-local-debugging-telepresence-2026-08-31`'s `scope_warning` is explicit that the page "names exactly ONE third-party tool (Telepresence)." No snapshot mentions kind, minikube or k3s.
**Fix:** Low severity — these are ubiquitous and the claim about them is mild. Either cache `https://kubernetes.io/docs/tasks/tools/` (which documents kind and minikube; k3s is not a Kubernetes-project tool and would need separate treatment) or drop the product names and keep the pattern.

### Checkpoint 1, Q3 distractor D rationale: "RBAC can grant permissions on the ephemeral containers subresource."

**Status:** **[research gap]** — `k8s-docs-ephemeral-containers-concept-2026-08-31` documents the `ephemeralcontainers` API handler but says nothing about RBAC over it.
**Fix:** Low severity and almost certainly true, but it is graded text. Either source it or rewrite the rationale to lean on the part that *is* sourced: the constraint is architectural (the container list is fixed at creation), which is sufficient to eliminate D without any RBAC claim.

---

## FAIL/UNVERIFIABLE — Tagged claims whose cited passage is absent from the packed corpus

Listed for completeness. **These are truncation artifacts, not defects.** Re-audit against the untruncated snapshot files before editing any of them.

| Claim (excerpt) | Tag | Why unverifiable |
|---|---|---|
| "A Pod mid-sequence reports `Init:N/M` — N init containers complete out of M total. A Pod whose init container is failing reports `Init:Error` or `Init:CrashLoopBackOff`." | `k8s-docs-debug-init-containers-2026-08-31` | Packed body ends before the status table. Frontmatter asserts "The status STRINGS and their meanings are accurate." |
| "What you need is the `-c` flag naming the specific init container" | same | same; `concepts_covered` lists `kubectl-logs-c-init-container` |
| Practice Q3 — "`Init:N/M` counts *completed init containers* out of the total" | same | same |
| Trap table — "Running plain `kubectl logs` on a Pod stuck in init... Name the init container with `-c`" | same | same |
| "The available profile names include `general`, `baseline`, `restricted`, `netadmin`, and `sysadmin`, with `general` as the default" | `k8s-docs-kubectl-debug-reference-2026-08-31` | Packed body is `## Synopsis` only. Frontmatter confirms five profiles with `general` default; the five *names* are not visible. |
| *"Make sure that the Pods you ran are actually selected by the Service"* | `k8s-docs-debug-service-2026-08-31` | Packed body ends at the busybox line |
| *"Is the Service correct?"* | same | same |
| *"Is the Service defined correctly?"* | same | same |
| "a Pod in `Unknown` or `Terminating` state can block the StatefulSet controller from making progress" | `k8s-docs-debug-statefulset-2026-08-31` | Packed body ends at "you can use the following:". Frontmatter simultaneously claims the page is complete *and* describes an "Unknown/Terminating pointer" not present in the packed text — worth resolving at the snapshot, since if the pointer genuinely is absent this becomes a research gap. |

---

## WARN — Minor discrepancies

**WARN-1 — Epigraph truncated mid-quotation without ellipsis.** Draft: *"The first step in troubleshooting is triage. What is the problem?"* Snapshot continues: "...What is the problem? **Is it your Pods, your Replication Controller or your Service?**" Add an ellipsis or extend the quote. (Extending it would also strengthen the epigraph — the full sentence names the triage axes the chapter goes on to use.)

**WARN-2 — §1 quote drops source emphasis.** Snapshot: "This is *not* a guide for people who want to debug their cluster." Draft renders "not" unemphasized. Content identical; restore the italic if quoting verbatim.

**WARN-3 — §3 distroless quote drops a leading connective.** Snapshot begins "**In particular,** distroless images enable you to deploy..."; draft opens at "distroless images enable...". Add an opening ellipsis or lowercase-bracket convention.

**WARN-4 — §2 "by default `/dev/termination-log`."** The path string is verified (`k8s-docs-determine-reason-pod-failure-2026-08-31`: "writes 'Sleep expired' to the `/dev/termination-log` file"), but the snapshot never states that it is the *default* value of `terminationMessagePath`. The default is almost certainly documented further down the untruncated page. Verify, or drop "by default."

**WARN-5 — §3: the quote does not support the claim it is attached to.** The draft asserts what `--target` does, then supports it with *"When using ephemeral containers, it's helpful to enable process namespace sharing so you can view processes in other containers."* That sentence is about process namespace sharing (the `--share-processes` mechanism, which the draft correctly uses in the `--copy-to` example), not about `--target`. The quote is verbatim and correctly tagged; it is simply attached to the wrong claim. Either source `--target` properly (see the FAIL entry) or move this quote to a sentence about process namespace sharing.

**WARN-6 — §3 profile-list conflict.** Already handled correctly by the draft: it names the generated CLI reference as its authority, matching that snapshot's own `conflict_note` ("AUTHORITATIVE ON PROFILES over the task page"), and introduces the list with "include" rather than as exhaustive. The AUTHOR-REVIEW comment states the right remedy. No change needed beyond verifying the five names against the untruncated reference.

**WARN-7 — §4 "every EndpointSlice it creates."** Snapshot hedges: "**In most use cases**, EndpointSlices are owned by the Service..." and documents manually-managed slices as an alternative. "Every EndpointSlice it creates" is defensible read narrowly (the control plane's own slices do carry the label) but drifts from the source's hedge. Suggest "every EndpointSlice the control plane creates for a Service."

**WARN-8 — §4 busybox quote punctuation.** Snapshot ends with a colon ("...run an interactive busybox Pod:"); draft ends with a period. Trivial; note only because the surrounding quotes are otherwise exact.

**WARN-9 — Practice Q13 distractor D over-attributes.** Draft: "port-forward goes through the API server, not through the Service, ClusterIP, or service proxy `[source: k8s-docs-port-forward-authorization-2026-08-31]`." That snapshot says only that port-forwarding "may bypass network-level controls" and that it uses the `pods/portforward` subresource. The stronger enumeration (Service, ClusterIP, service proxy) is the chapter's inference. Retag or reword to the inference the snapshot licenses: "port-forward is an API-server operation on the `pods/portforward` subresource, and does not travel the Service path."

**WARN-10 — figure `ch16-fig03` presents kube-proxy as *the* service proxy.** `k8s-docs-cluster-architecture-2026-08-23` marks kube-proxy **optional**: "If you use a network plugin that implements packet forwarding for Services by itself... then you do not need to run kube-proxy on the nodes in your cluster." The figure's "service proxy / kube-proxy rules" label is fine if the generic term stays primary; consider dropping the parenthetical or writing "kube-proxy (or its equivalent)". Low severity, and the figure already leads with the generic "service proxy."

**WARN-11 — §6 DNS example is composed, not quoted.** `web-0.nginx.default.svc.cluster.local` does not appear in `k8s-docs-statefulset-2026-08-24`; it is correctly derived from two sentences that do ("The domain managed by this Service takes the form: `$(service name).$(namespace).svc.cluster.local`" and "it gets a matching DNS subdomain, taking the form: `$(podname).$(governing service domain)`"), using the page's own `nginx`/`web-0..2` example. Derivation is sound. Flagged only so the tag is not read as covering the literal string.

**WARN-12 — §6 command form partially verified.** The label `app.kubernetes.io/name=MyApp` is verbatim from `k8s-docs-debug-statefulset-2026-08-31`; the `kubectl get pods -l ...` line itself is past the packed truncation. Almost certainly fine.

**WARN-13 — header "~4%".** Correctly labeled "Authored allocation for this chapter" and correctly flagged in the draft's own AUTHOR-REVIEW comment. CNCF publishes no sub-competency weights, so the label is the only thing keeping this honest. **The label must survive revision** — if the qualifier is dropped and "~4%" is left beside two genuinely CNCF-sourced figures, it reads as a published number.

**WARN-14 — §7's dividing-line list is authored framing.** `k8s-docs-local-debugging-telepresence-2026-08-31`'s `scope_warning` is explicit: "It does NOT contain any general discussion of which failures are or are not reproducible locally — that framing, which is Ch 16 section 7's actual subject, is NOT sourced here." The list's individual items are each sourced elsewhere in the book (Ch 12 for ServiceAccount tokens, Ch 9 for DNS and Service routing, Ch 8 for admission) and the draft carries cross-bearings to all of them. This is analysis built on sourced parts, not an unsourced factual claim — flagged for visibility, not for correction.

**WARN-15 — an omission worth considering.** The chapter never states what happens to a *failing* init container, which `k8s-docs-init-containers-2026-08-24` documents plainly: "If a Pod's init container fails, the kubelet repeatedly restarts that init container until it succeeds. However, if the Pod has a `restartPolicy` of Never, and an init container fails during startup of that Pod, Kubernetes treats the overall Pod as failed." Nothing in the draft contradicts this, and `Init:CrashLoopBackOff` implies it, but Soundings A2 ("The third init container never runs") and Practice Q5 ("waits forever") both sit adjacent to retry semantics the reader has not been given. One sourced sentence in §2 would close it, and the source is already cached. Coverage note rather than an accuracy defect — the revision stage's call.

---

## PASS — Verified claims

Forty-four tagged claims matched their snapshots. Sampled evidence:

**Exam structure (2/2 verified).** "Domain Weight: 16% (Cloud Native Application Delivery)" and "Cloud Native Application Delivery is 16% of the KCNA exam... and Debugging is one of its two competencies" — both match `cncf-kcna-curriculum-pdf-2026-08-23`: "16% – Cloud Native Application Delivery: Application Delivery; Debugging." The chapter's D1–D4 numbering is consistent with the curriculum's published order and with the `objectives_covered` metadata across the corpus.

**Ephemeral containers (12/12 verified).** All five constraint bullets are exact verbatim against `k8s-docs-ephemeral-containers-concept-2026-08-31`, as are the disposability quote, the "sometimes it's necessary" quote, the `ephemeralcontainers`-handler / no-`kubectl edit` quote, the distroless quote, and the process-namespace-sharing quote. The four re-quotations in Practice Q7 are likewise exact. This is the best-sourced material in the chapter.

**StatefulSet storage (6/6 verified).** "Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is deleted", "The default for policies is Retain, matching the StatefulSet behavior before this new feature", and the node-failure passage are all exact against `k8s-docs-statefulset-storage-2026-08-25`. Notably, the §6 Closer Look states the two policy fields and their `Retain` default **without** asserting a feature-gate requirement or stability stage — exactly as that snapshot's RETRIEVAL NOTE instructs ("DO NOT state a feature-gate requirement or a stability stage for this field"). Correct compliance with a snapshot-level constraint.

**StatefulSet identity and DNS (4/4 verified).** The `$(podname).$(governing service domain)` form, the negative-caching passage (exact, at length), and "StatefulSets currently require a Headless Service... You are responsible for creating this Service" all match `k8s-docs-statefulset-2026-08-24`.

**Init containers (4/4 verified).** "If the Pod restarts, or is restarted, all init containers must execute again" supports the §2 claim, the Checkpoint 1 Q5 answer, and Practice Q4. "Regular init containers... do not support the `lifecycle`, `livenessProbe`, `readinessProbe`, or `startupProbe` fields" supports Practice Q5 distractor D.

**port-forward (3/3 verified).** The resource-name sentence, the RBAC permissions sentence ("Typical required permissions include `get` on `pods` and `create` on `pods/portforward`"), and the "may bypass network-level controls" sentence are all exact.

**Termination messages (2/2 verified).** Both the purpose quote and the "should also be written to the general Kubernetes logs" paraphrase match `k8s-docs-determine-reason-pod-failure-2026-08-31`.

**Telepresence (3/3 verified).** Both quotes are exact against `k8s-docs-local-debugging-telepresence-2026-08-31`, and the draft's framing — "Telepresence is one instance of the pattern and the one the Kubernetes docs happen to document" — matches that snapshot's `scope_warning` precisely rather than overclaiming.

**Scope boundary (1/1 verified).** The §1 guide-scope quote is exact against `k8s-docs-debug-pods-2026-08-31`.

**EndpointSlice interpretation (1/1 verified).** The §4 quote — "Make sure that the endpoints in the EndpointSlices match up with the number of pods that you expect... the Service's selector probably does not match the Pods' labels, or the Pods are not Ready" — is exact against `k8s-docs-debug-pods-2026-08-23`. The **quote** is verified; the **empty-list gloss** built on top of it is the CONTRADICTED finding above.

**Debug copy (2/2 verified).** The `--copy-to` rationale quote is exact against `k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31`, both at §3 and in Practice Q8.