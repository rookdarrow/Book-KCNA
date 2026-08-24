# Fact-Accuracy Audit — Chapter 5

## Mode detected: **STANDARD**

Both detection signals point the same way: the cached-sources block is populated (115 snapshots), and the draft carries 93 `[source: ...]` tags across 16 distinct snapshots. Untagged factual claims are therefore FAIL.

**Input note — read before acting on this report.** The stage prompt's declared inputs were both absent (`draft-v2.md`, `draft-voice.md` — neither exists in `ch-05/` at this point in the pipeline). Rather than repeat Chapter 4's blocked-stage outcome, this audit was run against the draft that actually exists on disk:

    ../Book-KCNA/.pipeline-state/ch-05/draft-v1.md   (1,195 lines, 109,592 bytes, post-voice-swap, written 06:39)

The Stage 6 input resolution should be corrected to `draft-v1.md` for the pre-`draft-v2` position in the graph. Chapter 4's `diagnostics/fact-accuracy.md` is a false clean bill of health for the same reason and should be re-run.

---

## Root cause — one upstream failure produces most of the FAILs below

Chapter 5's research stage **completed its research but could not write its snapshots.** From `ch-05/research-manifest.md` line 3:

> "## Blocker: this session has no filesystem write access — `Write` is denied for every path… The research itself is **complete**… the five snapshots need a materialization pass."

Five fully-formed snapshot files sit inside `research-manifest.md` under `## Files to write`, never materialized into `../Book-KCNA/sources/` (that directory's newest file is `04:49`; the research stage ran at `06:26`):

| Pending snapshot | Manifest line | Closes |
|---|---|---|
| `k8s-docs-pods-2026-08-24.md` | 76 | §1, §2, §9 — "smallest deployable unit", "two main ways" |
| `k8s-docs-init-containers-2026-08-24.md` | 210 | **all of §3** |
| `k8s-docs-pod-qos-2026-08-24.md` | 293 | §8 movement four |
| `k8s-docs-sidecar-containers-2026-08-24.md` | 361 | §2, §7 qualifier |
| `k8s-docs-pod-termination-2026-08-24.md` | 434 | §4 (currently omitted by design) |

The drafting stage never saw these, which is why the draft's own six AUTHOR-REVIEW comments correctly describe the gaps as open. **Materializing those five files closes 11 of the 17 untagged-claim FAILs mechanically.** Do that before the revision stage runs, then re-run this audit.

Per Rule 2 this audit does **not** treat manifest-embedded text as cached. Where a pending snapshot would resolve a finding, that is noted as remediation, not verification.

---

## Summary

- Total factual claims inspected: **148** (88 tagged assertion sites; ~60 untagged sentences carrying external-fact content)
- Tagged claims verified: **81**
- Tagged claims unverifiable (source tag points to missing/empty snapshot): **0** — all 16 distinct tags resolve to files present in `sources/`
- **Untagged factual claims (FAIL): 17**
- **Contradicted claims (FAIL): 3**
- Minor discrepancies (WARN): **17** (of which 6 are *over-tagged* — the cited snapshot exists but does not carry the assertion)

Six of the 17 untagged claims recur at multiple line numbers; those are consolidated into single findings below.

---

## FAIL — Untagged factual claims

Each entry is marked **BLOCKING** (no cached snapshot supports it) or **TAG-ONLY** (a cached snapshot does support it; only the tag is missing). Fix TAG-ONLY items now; BLOCKING items wait on materialization.

### U1 — Line ~214: "Init containers run before the app containers, in the order they are declared, and each must run to completion successfully before the next one starts. Only when all of them have succeeded does the kubelet start the Pod's app containers."

**Why it's a factual claim:** states the execution contract of a Kubernetes API object.
**Status:** BLOCKING. No cached snapshot covers init containers. The only cache mention is `k8s-docs-debug-overview-2026-08-23`, which lists "debugging Init Containers" as a docs topic — not a semantics source.
**Fix:** Materialize `k8s-docs-init-containers-2026-08-24.md` (manifest line 210), then tag. The claim is recoverable close to verbatim: *"Init containers always run to completion. Each init container must complete successfully before the next one starts."*

### U2 — Line ~237: "The app containers are **parallel** — they all start together once the init sequence completes."

**Why it's a factual claim:** asserts kubelet startup behavior.
**Status:** BLOCKING. Same gap.
**Fix:** Recoverable from the pending snapshot: *"Once preconditions are met, all of the app containers in a Pod can start in parallel."* Tag after materialization.

### U3 — Lines ~241–244: "If an init container fails, the kubelet restarts it according to the Pod's `restartPolicy`… With the default policy, a Pod with a broken init container sits there retrying… With a `restartPolicy` of `Never`, the Pod fails outright."

**Why it's a factual claim:** asserts failure-handling semantics.
**Status:** BLOCKING — **and imprecise even once sourced.** The pending snapshot adds a wrinkle the draft flattens: *"if the Pod `restartPolicy` is set to Always, the init containers use `restartPolicy` OnFailure."* That is not straight inheritance. The `Never` half is exactly right: *"if the Pod has a restartPolicy of Never, and an init container fails during startup of that Pod, Kubernetes treats the overall Pod as failed."*
**Fix:** Materialize, then rewrite the mechanism sentence — the observable outcome the draft describes is correct, but "according to the Pod's `restartPolicy`" is not. This also affects Bearings #1 answer 3 (~L292) and Q10's rebuttal of distractor C (~L1100).

### U4 — Line ~252: "…classic init containers don't carry the probes §7 is about"

**Why it's a factual claim:** asserts which API fields an object type supports.
**Status:** BLOCKING.
**Fix:** Recoverable, but the qualifier is load-bearing: *"Regular init containers (in other words: excluding sidecar containers) do not support the `lifecycle`, `livenessProbe`, `readinessProbe`, or `startupProbe` fields."* The draft's "classic" ≈ "regular" is a good instinct; the *because-sidecars-do* exclusion is missing and should be added if §2 names the sidecar mechanism.

### U5 — Lines ~254, ~256, ~292, ~296–300, ~1074–1076, ~1100: restatements of U1–U4 in the Fixed Point, the Mnemonic, Bearings #1 answers 3 and 4, and Practice Q4 and Q10 answers

**Why it's a factual claim:** these are the assessment surface of §3 — a Fixed Point, a memory device, and two graded answer keys resting on unsourced semantics.
**Status:** BLOCKING (same gap as U1–U4).
**Fix:** Tag all of them once materialized. Do not ship a ★ Fixed Point or a graded answer key on untagged claims.

### U6 — Line ~185: "Pods are used in two main ways. Overwhelmingly the most common is **one container per Pod**… The other is **multiple tightly-coupled containers**…"

**Why it's a factual claim:** characterizes documented usage patterns and asserts relative frequency.
**Status:** BLOCKING. Correctly self-flagged by the AUTHOR-REVIEW at ~L187.
**Fix:** Recoverable verbatim from `k8s-docs-pods-2026-08-24.md` (manifest line 109): *"Pods in a Kubernetes cluster are used in two main ways… The 'one-container-per-Pod' model is the most common Kubernetes use case."* Note the pending source also carries a caution the draft omits and should probably absorb: *"Grouping multiple co-located and co-managed containers in a single Pod is a relatively advanced use case."*

### U7 — Lines ~104, ~125, ~811 (§9 title), ~1152 (Chapter Summary): "It is the smallest unit Kubernetes schedules" / "the smallest thing you can ask Kubernetes to run" / "The Smallest Deployable Unit" / "The smallest deployable unit"

**Why it's a factual claim:** a definitional assertion about Kubernetes, and it is the chapter's organizing thesis and its §9 heading.
**Status:** BLOCKING. `k8s-docs-workloads-2026-08-23` supplies the *Pod represents a set of containers* half (tagged, verified) but nowhere says "smallest deployable unit." `k8s-docs-kube-scheduler-2026-08-23` establishes that the scheduler places Pods, which entails the claim but does not state it.
**Fix:** Recoverable verbatim from the pending Pods page: *"Pods are the smallest deployable units of computing that you can create and manage in Kubernetes."* Tag §9's premise and the Chapter Summary row.

### U8 — Line ~706: "How you fill in requests and limits determines a Pod's **Quality of Service class** — Guaranteed, Burstable, or BestEffort. The class is not something you set directly; it's derived from what you declared, and it governs how the Pod is treated when a node comes under pressure and something has to give."

**Why it's a factual claim:** names three API-assigned classes, asserts a derivation rule, and asserts an eviction consequence.
**Status:** BLOCKING — **and the accompanying guard note is inaccurate.** The AUTHOR-REVIEW at ~L708 claims "The paragraph above states only what can be inferred from the requests/limits material." It does not. `Guaranteed`, `Burstable`, `BestEffort`, "derived from what you declared", and node-pressure treatment appear nowhere in the cached set — a grep of all 115 snapshots returns nothing for any of the three class names. The prose exceeds the restraint its own guard note claims for it.
**Fix:** Either cut the three class names and the eviction clause until `k8s-docs-pod-qos-2026-08-24.md` (manifest line 293) is materialized, or materialize now and tag. Correct the guard note either way — a note that misdescribes the prose it guards is worse than no note.

### U9 — Line ~460: "You'll meet `CrashLoopBackOff` in the same position: a container in `Waiting` with that reason, meaning it has started, failed, and is now serving its backoff delay before the next attempt."

**Why it's a factual claim:** defines a specific container status reason string.
**Status:** BLOCKING. `CrashLoopBackOff` appears in **no** cached snapshot. `k8s-docs-images-2026-08-23` covers `ImagePullBackOff` only; `k8s-docs-deployment-2026-08-23` uses the prose phrase "crash looping" but never the status reason.
**Fix:** Open a research gap for the status-reason vocabulary (`kubernetes.io/docs/tasks/debug/debug-application/debug-pods/` did not carry it either). **This interacts with C1 below** — the recommended fix for C1 wants `CrashLoopBackOff`, so source it.

### U10 — Line ~169: "The **PodSpec is simply the `spec` field of a Pod**."

**Why it's a factual claim:** a definitional identity between an API term and a field.
**Status:** BLOCKING-lite. `k8s-docs-cluster-architecture-2026-08-23` uses "PodSpecs" without defining the term; `k8s-docs-objects-2026-08-23` establishes `spec` generically. The identity is entailed but nowhere stated.
**Fix:** The pending Pods page carries `podspec` in `concepts_covered`. Tag after materialization, or mark explicitly as an authorial gloss.

### U11 — Lines ~163 and ~192: "Containers in a Pod can share volumes, which is how two processes in one Pod read and write the same files" / "**They read and write the same files**, because they share a volume."

**Why it's a factual claim:** asserts a Kubernetes storage mechanism, and it is one of the two legs of §2's decision rule.
**Status:** **TAG-ONLY.** Supported now by `k8s-docs-volumes-2026-08-23`: *"Another problem occurs when multiple containers are running in a Pod and need to share files"* and *"all containers in the Pod can read and write the same files in the emptyDir volume."*
**Fix:** Add `[source: k8s-docs-volumes-2026-08-23]` at both sites. The ⚓ Worth Securing at ~L194 rests on this leg; it should not be half-tagged (the `localhost` leg at ~L191 is tagged, the volume leg is not).

### U12 — Line ~196: "The helper container in a multi-container Pod has a name you'll meet constantly: the **sidecar**. A log-shipping agent that reads files the app writes to a shared volume. A proxy that intercepts the app's network traffic on `localhost`."

**Why it's a factual claim:** names an industry/Kubernetes term and asserts two concrete deployment patterns.
**Status:** **TAG-ONLY.** `k8s-docs-logging-architecture-2026-08-23` supports the log-shipping sidecar exactly: *"Include a dedicated sidecar container for logging in an application pod — either a streaming sidecar… or a sidecar container with a logging agent configured to pick up logs from an application container."* `istio-service-mesh-2026-08-23` supports the proxy case: *"sidecar mode, which deploys an Envoy proxy alongside each pod."*
**Fix:** Add both tags. The chapter can source "sidecar" today without waiting on the pending sidecar-containers page.

### U13 — Line ~204: "Asking for 'the logs' of a two-container Pod is an incomplete request — you have to say which container."

**Why it's a factual claim:** asserts CLI behavior.
**Status:** **TAG-ONLY.** `k8s-docs-logging-architecture-2026-08-23`: *"`kubectl logs <pod>` prints them; for a multi-container Pod use `-c <container>`."*
**Fix:** Add `[source: k8s-docs-logging-architecture-2026-08-23]`.

### U14 — Line ~498: "A manifest that appears to place one inside a container definition is either being silently ignored or rejected — either way, the intent is unachievable."

**Why it's a factual claim:** asserts API-server validation behavior, and names two mutually exclusive outcomes without committing to either.
**Status:** BLOCKING. Nothing in the cache describes validation of a container-level `restartPolicy`. This is speculation presented as fact inside a graded answer key.
**Fix:** Cut the sentence. The preceding sentence — *"`restartPolicy` is a field on the Pod's `spec`, and it applies to all containers in the Pod"* [source: k8s-docs-pod-lifecycle-2026-08-23] — is verified and carries the answer on its own. See also W3.

### U15 — Line ~791: "Nothing in the Pod's status changes at all — the phase stays `Running`, the container state stays `Running`, and **no event announces it**." (also ~L670: "Nothing in the Pod's status changes.")

**Why it's a factual claim:** an absolute negative about the Events API.
**Status:** BLOCKING. Events are not covered by any cached snapshot. The phase/state half is a sound entailment; "no event announces it" is not supportable from the cache and absolute negatives are the least safe unsourced claim shape.
**Fix:** Cut "and no event announces it", or soften to "and neither of §5's two vocabularies reports it" — which the cache does support. The pedagogical point survives intact.

### U16 — Line ~846: "**Requests are declared per container, but scheduling happens per Pod** — because the scheduler is placing the wrapper, and it needs the wrapper's total."

**Why it's a factual claim:** asserts an aggregation rule (Pod-level request = sum of container requests).
**Status:** BLOCKING. `k8s-docs-resource-management-2026-08-23` covers per-container specification and the scheduler's use of requests, but never states the summation.
**Fix:** Recoverable from the pending QoS snapshot: *"The resource request of a Pod is equal to the sum of the resource requests of its component Containers."* Tag after materialization. (Note the pending init-containers page complicates this for Pods with init containers — see W10.)

### U17 — Line ~1080: "*D* describes `nodeSelector`, which is about node labels constraining placement, not Pod labels."

**Why it's a factual claim:** asserts what a specific API field does, inside an answer key.
**Status:** **TAG-ONLY.** `k8s-docs-assign-pod-node-2026-08-23`: *"nodeSelector is the simplest recommended form of node selection constraint… Kubernetes only schedules the Pod onto nodes that have each of the labels you specify."*
**Fix:** Add `[source: k8s-docs-assign-pod-node-2026-08-23]`.

---

## FAIL — Contradicted claims

### C1 — Lines ~404–411: the WORKED OVERLAY inside `ch05-fig02-pod-phases-and-container-states`

```
┌─ POD  phase: Running ──────────────────────────────────────┐
│   ┌─ app     state: Running    ─────────────────────────┐  │
│   ┌─ helper  state: Waiting    Reason: ImagePullBackOff ┐   │
```

**Tag:** the figure is untagged; the surrounding section is `[source: k8s-docs-pod-lifecycle-2026-08-23]`.
**Snapshot says:** "Running — The Pod has been bound to a node, and **all of the containers have been created.** At least one container is still running, or is in the process of starting or restarting." And, on the Waiting state: "the container is still running the operations it requires in order to complete start up (**pulling the container image**, applying Secret data)."
**Draft says:** a Pod in phase `Running` containing a container in `Waiting` with `Reason: ImagePullBackOff`.
**Why it's contradicted:** a container blocked on an image pull has **not** been created, so "all of the containers have been created" is false and the phase cannot be `Running`. The draft knows this — its own §5 table at ~L452–456 maps the identical scenario to phase **`Pending`**, and Bearings #2 answer 4 (~L506) and Practice Q7 (~L1086) both do the same. The figure and the prose disagree with each other, and the figure loses.
**Recommended fix:** Change the helper's `Reason` in the overlay to a **post-creation** waiting reason — a container that has been created, has run, has crashed, and is serving its backoff. `CrashLoopBackOff` is the natural choice and preserves the entire pedagogical point (two true readings at two scopes). **Blocked on U9** — source the reason string first, or use a neutral label such as `Reason: <restart backoff>` and tag the phase definition. Do not ship the figure as drawn; it is the one artifact in the chapter that teaches the opposite of §5's centerpiece.

### C2 — Line ~258: "Debugging a Pod stuck behind a failing init container is a named skill in the exam curriculum, and it's Chapter 16's."

**Tag:** untagged.
**Snapshot says:** `cncf-kcna-curriculum-pdf-2026-08-23` enumerates the curriculum exhaustively — four domains and twelve competencies: "Kubernetes Core Concepts; Administration; Scheduling; Containerization… Networking; Security; Troubleshooting; Storage… Application Delivery; Debugging… Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration." No skill finer than a competency is named anywhere in it.
**Draft says:** that debugging init containers is "a named skill in the exam curriculum."
**Why it's contradicted:** it isn't named. The nearest cached appearance of the phrase is `k8s-docs-debug-overview-2026-08-23`, which lists "debugging Init Containers" as a **Kubernetes documentation topic** — a different authority making a different kind of statement. This is precisely the published-vs-commonly-reported failure that Chapter 1 §2 is built to teach against, and it would not survive that chapter's own standard.
**Recommended fix:** "Debugging a Pod stuck behind a failing init container falls under **Troubleshooting**, a named KCNA competency [source: cncf-kcna-curriculum-pdf-2026-08-23], and the method is Chapter 16's."

### C3 — Lines ~488–490 (Bearings #2, answer 1): "A second container sitting in `Waiting` doesn't contradict **any part** of that."

**Tag:** `[source: k8s-docs-pod-lifecycle-2026-08-23]`
**Snapshot says:** "Running — The Pod has been bound to a node, and **all of the containers have been created.**"
**Draft says:** that a container in `Waiting` contradicts no part of the `Running` definition.
**Why it's contradicted:** it contradicts one specific clause whenever the waiting reason is a *pre-creation* one (image pull, Secret application — both named in the snapshot's own Waiting definition). The answer is right for post-creation waits (restart backoff) and wrong for pre-creation waits, and the question stem at ~L474 does not specify which.
**Recommended fix:** Two edits. (a) Stem: name the reason, e.g. "…one of its containers is in the state `Waiting`, serving a restart backoff." (b) Answer: replace "doesn't contradict any part of that" with "doesn't contradict that — the container has been created; it is between runs." Then add the discriminating half, which is worth more than the current answer: *a container waiting because its image has not been pulled has not been created, and that Pod reports `Pending`.* That turns a contradiction into the chapter's sharpest phase/state item.

---

## WARN — Minor discrepancies

### Over-tagged — the cited snapshot exists but does not carry the assertion

**O1 — Line ~576, probe mechanisms table, `grpc` row: "Success means: The gRPC health check reports serving."** The snapshot gives success criteria for `exec` ("exit status 0"), `httpGet` ("status ≥200 and <400"), and `tcpSocket` ("the port is open"), but for gRPC says only "grpc (gRPC health check)". The fourth cell is authorial. Either soften to "the gRPC health check passes" or source it.

**O2 — Lines ~578 and ~1126–1128: "Any probe type can use any mechanism" / "The four check mechanisms… are orthogonal to the three probe types."** The snapshot lists mechanisms and types in adjacent sentences; it never asserts orthogonality. The claim is correct in fact, but it is the entire answer to Practice Q17 and three of that question's distractors depend on it. Fetch the probes section of the Pod-lifecycle page (or the Pod API reference) and tag properly — a graded item should not rest on an inference from document layout.

**O3 — Line ~385 (Dead Reckoning): "Phase is a Pod-level field in `status`."** `k8s-docs-pod-lifecycle-2026-08-23` does not locate `phase` within `status`. `k8s-docs-objects-2026-08-23` does the general spec/status work and is already cited elsewhere in the chapter. Add it as a second tag here.

**O4 — Line ~428: "A crash-looping Pod reports the phase `Running`."** Entailed, not stated. The draft handles this well — it quotes the definition immediately before and reasons in the open — so no edit is required. Recorded so the revision stage does not "upgrade" it into a quoted fact.

**O5 — Line ~438: "You cannot set it per container."** Entailed from "The `restartPolicy` applies to all containers in the Pod", not stated. Acceptable as drafted; see W3.

**O6 — Line ~573: `exec` — "Executes a command **inside the container**".** Snapshot omits "inside the container". Trivially true, harmless; noted only for completeness.

### Other

**W1 — Unsourced prevalence claims** at ~L175 ("the single most common carry-over error"), ~L285 ("the most common error on this topic"), ~L424 ("Three of the **most commonly-missed** facts"), ~L859 ("the seven **most likely** to be tested directly"), ~L869 ("Seven **documented** misconceptions"), ~L1064, ~L1120 ("the single most common probe error"). Nothing in the cache measures error frequency or exam emphasis. This is the constraint `k8s-blog-dockershim-faq-2026-08-24` states explicitly for this book: *"Write 'easy to confuse', never 'frequently tested'."* Recommend converting each to a confusability or consequence claim, and replacing "documented" with "recurring" at ~L869.

**W2 — Line ~859: "in descending order of confidence."** Presents an authorial ranking as a property of the exam. Recommend: "in the order we'd study them" or drop the ranking clause.

**W3 — Lines ~430 and ~498: "There is no way to configure one container to restart and another not to."** Unverifiable against the cache, and the draft's own AUTHOR-REVIEW at ~L200 names the mechanism that makes it false — sidecar containers are init containers with `restartPolicy: Always`. The chapter currently omits the mechanism (correct, given the cache) while making an absolute claim the omitted mechanism refutes. Once `k8s-docs-sidecar-containers-2026-08-24.md` is materialized, either scope the claim to app containers or drop the absolute. Highest-priority WARN in this list.

**W4 — Lines ~670 and ~791** — see U15; recorded here as the drift risk if the FAIL is fixed by softening rather than cutting.

**W5 — Line ~686: "GPUs are the example everyone reaches for."** `k8s-docs-resource-management-2026-08-23` names extended resources and device plugins but not GPUs. Low risk; either cut or mark as illustrative.

**W6 — Line 4: "This book's allocation: 7%."** Correctly labeled as the book's own allocation and correctly annotated at L6 against `cncf-kcna-curriculum-pdf-2026-08-23` (44/28/16/12, twelve competencies, no sub-weights). No finding. Confirm the metadata line's phrasing matches Chapters 2–4 before publication, per the draft's own note.

**W7 — Attention Budget arithmetic (internal, not a source claim).** Line 12 declares "~85 minutes"; the table's twelve rows sum to **95** (10+5+8+5+5+15+6+4+12+14+6+5). Reconcile.

**W8 — Figure numbering is out of sequence (for the Stage 10 image-spec handoff).** Anchors appear in this document order: `ch05-fig01` (§1), **`ch05-fig03`** (§3), **`ch05-fig02`** (§5), `ch05-fig04` (§7), `ch05-fig05` (§8), `ch05-zenith`. Either renumber to document order or confirm the diagram pipeline tolerates it. Out of scope for this stage; surfaced so it is not lost.

**W9 — Line ~1193: "Nine sections, five concept diagrams."** Six figure blocks are present (five numbered + `ch05-zenith`). Defensible if the Zenith map is not counted as a concept diagram; confirm the counting convention used in Chapters 1–4.

**W10 — Practice Q10, distractor C is closer to true than the key admits.** C reads "It is set on the Pod and applies only to app containers, never to init containers"; the key (~L1100) calls it "an invented exemption." Once the init-containers snapshot lands, the real behavior is that init containers **do** get special handling — *"if the Pod `restartPolicy` is set to Always, the init containers use `restartPolicy` OnFailure."* C remains wrong (it claims a total exemption), but the rebuttal must not assert that init containers are treated identically. Rewrite the rebuttal when U3 is fixed.

**W11 — Cross-source tension to guard when the QoS snapshot is materialized.** The pending QoS page contains a loose generalization: *"Any Container exceeding a resource limit will be killed and restarted by the kubelet."* The cached `k8s-docs-resource-management-2026-08-23` is more specific and is what §8 correctly follows: CPU limits are enforced by **throttling**, memory limits by OOM kill. Do not let the QoS page's broader sentence overwrite §8's verified CPU/memory asymmetry during revision.

---

## PASS — Verified claims

Sampled coverage evidence. All quotations below were matched against the named cached snapshot.

**§1 — the Pod and its shared context**
- L125 "A Pod represents a set of one or more running containers on your cluster" — `k8s-docs-workloads-2026-08-23`, verbatim. ✓
- L125 "co-located and co-scheduled to run on the same node" — `k8s-docs-containers-2026-08-23`, verbatim. ✓
- L133 the three-sentence network-model block (unique cluster-wide IP · private network namespace shared by all containers · `localhost` between containers) — `k8s-docs-network-model-2026-08-23`, verbatim. ✓
- L167 the kubelet's PodSpec sentence — `k8s-docs-cluster-architecture-2026-08-23`, verbatim. ✓
- L169 `apiVersion`/`kind`/`metadata`/`spec` + system-maintained `status` — `k8s-docs-objects-2026-08-23`. ✓

**§4 — lifetime** — all five bullets at L325–329 plus the "relatively ephemeral (rather than durable) entities" quote at L331 match `k8s-docs-pod-lifecycle-2026-08-23` verbatim or near-verbatim. ✓ L335's UID quote ("intended to distinguish between historical occurrences of similar entities") matches `k8s-docs-names-and-uids-2026-08-24` verbatim. ✓ L343 workload-resource sentence matches `k8s-docs-workloads-2026-08-23`. ✓ L349 container immutability matches `k8s-docs-containers-2026-08-23`. ✓

**§5 — phases, states, `restartPolicy`, backoff**
- L365–371 all five phase definitions — `k8s-docs-pod-lifecycle-2026-08-23`, faithful including both breadth clauses (Pending's image-download time; Running's "starting or restarting"). ✓
- L377–381 all three container states with their attached fields (`Reason` / `startedAt` / reason+exit code+times). ✓
- L438 `restartPolicy` values and Pod scope — verbatim. ✓
- L440 backoff "10s, 20s, 40s… capped at five minutes… resets after 10 minutes" — verbatim. ✓
- L448 `ImagePullBackOff`, including "compiled-in limit of 300 seconds (5 minutes)" and both named causes — `k8s-docs-images-2026-08-23`, verbatim. ✓

**§6 — identity** — all four numbered facts (L537, L539, L541, L543) and the TokenRequest/projected-volume/v1.22 paragraph (L549) match `k8s-docs-service-accounts-2026-08-23`. ✓ L1111's dual tag with `k8s-docs-secret-2026-08-23` for the legacy token type is correct. ✓

**§7 — probes** — L565 probe definition; L571–575 three of four mechanisms with success criteria; L586 liveness (kubelet kills → restart policy); L588 readiness (endpoints controller removes the Pod's IP from all matching Services); L592 startup (all other probes disabled; failure → kill + restart policy); L617 the five parameters. All `k8s-docs-pod-lifecycle-2026-08-23`, verbatim or near. ✓ (See O1, O2 for the two cells that are not.)

**§8 — requests and limits** — L644 the scheduler/kubelet block; L654 the above-request-is-allowed rule; L664 CPU throttling; L666 memory OOM including "enforced reactively"; L677–684 the four resource types; L686 extended resources; L688 CPU units including the `1m` floor; L690 the memory suffix list; L694 the `M`/`m` warning with "0.4 bytes"; L700 CPU as an absolute amount with the 48-core example. All `k8s-docs-resource-management-2026-08-23`, verbatim. ✓ This section is the best-sourced in the chapter through movement three.

**Practice answers** — Q5 (labels, `k8s-docs-labels-selectors-2026-08-23`) ✓ · Q6 ✓ · Q7 ✓ · Q8 ✓ · Q9 ✓ · Q11 ✓ · Q12 ✓ · Q13 ✓ · Q14 ✓ · Q15 ✓ · Q16 ✓ · Q18 ✓ · Q19 ✓ · Q20 ✓ · Q21, including the hub-and-spoke rebuttal against `k8s-docs-control-plane-node-communication-2026-08-24` ("Kubernetes has a 'hub-and-spoke' API pattern. All API usage from nodes… terminates at the API server") and the kube-scheduler rebuttal against `k8s-docs-kube-scheduler-2026-08-23`. ✓

**Scope decisions verified as correct.** Three AUTHOR-REVIEW omissions were checked against the cache and are right to omit as things stand: sidecar-as-init-container (L200), graceful termination (L353), and cgroup/runtime depth. Note that L353's stated reason is accurate — the cached `k8s-docs-pod-lifecycle-2026-08-23` snapshot does truncate after the probes section — and the pending `k8s-docs-pod-termination-2026-08-24.md` would reopen that decision as an editorial choice rather than a sourcing constraint.

---

## Research gaps to open in the research manifest

1. **MATERIALIZE FIRST — no re-fetch needed.** Write the five complete snapshot bodies from `ch-05/research-manifest.md` (`## Files to write`, manifest lines 75–500) into `../Book-KCNA/sources/`: `k8s-docs-pods-2026-08-24.md`, `k8s-docs-init-containers-2026-08-24.md`, `k8s-docs-pod-qos-2026-08-24.md`, `k8s-docs-sidecar-containers-2026-08-24.md`, `k8s-docs-pod-termination-2026-08-24.md`. Closes U1–U8, U10, U16 and unblocks C1.
2. **New fetch required — container status reasons.** `CrashLoopBackOff` (U9) is absent from all 115 cached snapshots and is needed for the C1 figure fix. Candidate: the Pod-lifecycle container-states section, or the Pod API reference `ContainerStateWaiting`.
3. **New fetch required — probe type × mechanism orthogonality** (O2). Needed to properly source Practice Q17 and the §7 framing at L578.
4. **New fetch required — container-level `restartPolicy` validation** (U14, W3), or cut the claim.
5. **Fix Stage 6 input resolution** to `draft-v1.md`, and **re-run Chapter 4's fact-accuracy audit**, which returned a blocked report with all-zero counts that must not be read as a pass.