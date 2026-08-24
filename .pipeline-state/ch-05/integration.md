# Integration Check — KCNA Chapter 5

## Summary

- Terminology consistency: **pass** — 0 semantic drifts; 4 structural/format drifts flagged below
- Callbacks to earlier chapters: **7 correct / 2 incorrect** (section-numbered back-references); all un-numbered chapter-level callbacks verified accurate
- Retrieval-practice accuracy: **pass** — 10/10 tagged items land on material the named chapter actually publishes
- Glossary coverage: **29 concepts introduced, 28 defined in the chapter, 24 require glossary entries** (1 introduced without definition — see `projected volume`)
- Contradictions with earlier canon: **none** — 1 collision risk and 3 forward-section conflicts flagged for author decision
- Ethical guardrails (skill Part 14): **pass**, conditional on the five unmaterialized snapshots landing before publication

**Scope note.** No knowledge-base shards were supplied to this stage. I verified against the four published chapters on disk (`chapter-01`…`chapter-04`), `.pipeline-state/book-outline/arc-outline.md`, `retrieval-architecture.md`, and `.pipeline-state/ch-05/image-specs.md`. Chapters 6–20 are undrafted, so forward cross-bearings are verified at chapter granularity against the arc outline and at section granularity only where an already-published chapter has pinned that section.

---

## Terminology consistency

No term in this chapter is *named* differently from how an earlier chapter named it. Every drift below is structural or presentational.

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| Pod | `Pod` (capitalized) — Ch 2/3/4 | ~200, uniform | No |
| kubelet | `kubelet` (lowercase) — Ch 2 §4, Ch 3 §3 | uniform | No |
| kube-scheduler | `kube-scheduler` for the component; "the scheduler" in prose — Ch 3 §2 | uniform | No |
| PodSpec | `PodSpec` — Ch 2 §4, Ch 3 §3 | uniform | No |
| `ImagePullBackOff` | code-formatted — Ch 2 §6 | uniform | No |
| `imagePullSecret` / Secret | Ch 2 §3, Ch 4 §4 | uniform | No |
| UID | `UID` — Ch 4 §2 | uniform | No |
| `spec` / `status` | code-formatted — Ch 4 §2 | uniform | No |
| control plane / control-plane | both, per noun/adjective — Ch 3 (36/31), Ch 4 (10/5) | 6 / 2 | No — matches book usage |
| API server | "API server" in prose — Ch 3 §5 | 9 | No |
| ServiceAccount | `ServiceAccount` — Ch 4 §4 uses it 8×, exclusively | 21 `ServiceAccount`, 3 `serviceAccountName`, **2 lowercase "service account"** | **Minor** |
| Zenith anchor slug | `chNN-zenith-<slug>` — Ch 2 ships `ch02-zenith-standard-crate`; arc outline prescribes this form for all 20 chapters | `ch05-zenith-smallest-deployable-unit` | **No — see correction below** |
| Bearings heading | `## ☆ Taking Your Bearings #N: <Topic>` — Ch 2 (3×), Ch 3 (3×) | `## ☆ Taking Your Bearings #N` + separate `**Topic:**` line | **Yes** |
| Exam Alert heading | `## Exam Alert! 🚨` — Ch 3, Ch 4; Ch 2 uses `## Exam Alert 🚨` | `## Exam Alert` — no emoji, no `!` | **Yes** |
| Chapter metadata line | three different forms across Ch 2/3/4 | a fourth form | **Yes** |
| Voyage Progress | `🗺️ **Chapter N · Voyage Progress:** …` (Ch 3, mid-chapter ×3); `**Voyage Progress:** 🗺️ → 🌊 → 🌅 — …` (Ch 4, closing) | bare unlabeled glyph strip `🗺️ → 🌊 → 🌅` | **Yes** |

**T1 — `ServiceAccount` casing (low).** Two lowercase instances, both inside sourced sentences ("A service account is a type of non-human account…"; "The `default` service accounts get no permissions by default"). Ch 4 established `ServiceAccount` as the canonical form. Keep lowercase only inside the verbatim definition; use `ServiceAccount` everywhere else.

**T2 — Bearings heading form (medium).** Ch 2 and Ch 3 both put the topic in the heading; Ch 5 is the only chapter that moves it to a body line. Ch 4 is a third variant (no `#N`). Recommend Ch 5 conform to the Ch 2/Ch 3 majority: `## ☆ Taking Your Bearings #1: What a Pod Is`, `#2: Lifetime, Phase, and State`, `#3: Identity, Health, and What a Pod Is Owed`. Ch 4 should be retrofitted separately.

**T3 — Exam Alert heading (medium).** Chapter 5 drops the 🚨 entirely. Three of three published chapters carry it, and the skill's Part 15 template specifies `## Exam Alert! 🚨`. Set to `## Exam Alert! 🚨`.

**T4 — Metadata line (medium; this answers the draft's own AUTHOR-REVIEW at line 6).** The chapter asks whether the `7%` line matches what Chapters 2–4 published. **It does not — and Chapters 2, 3, and 4 do not match each other:**

- **Ch 2:** `**Exam domain: Kubernetes Fundamentals (44% of the exam) — competency: Containerization** [source: cncf-kcna-certification-page-2026-08-23] [source: cncf-kcna-curriculum-pdf-2026-08-23] **| Estimated share of the exam: ~9% (authored allocation — CNCF publishes domain weights, not competency weights** [source: cncf-kcna-curriculum-pdf-2026-08-23]**; see front matter) | Complexity: Mixed | Novelty: Moderate**`
- **Ch 3:** `**Domain Weight: ~6% of exam (authored estimate) | Complexity: Mixed | Novelty: Paradigm-shifting**`
- **Ch 4:** `**Domain: Kubernetes Fundamentals — Kubernetes Core Concepts | Estimated chapter weight: ~6%**`
- **Ch 5:** `**Domain: Kubernetes Fundamentals (Kubernetes Core Concepts) | This book's allocation: 7% | Complexity: Mixed | Novelty: Moderate**`

Ch 2 is the only one that carries source tags and states the authored-allocation disclosure inline, which is what Ch 1's published promise (§ "The disclosure I promised in §3") commits the book to. **Recommend: conform Ch 5 to Ch 2's shape**, naming the competency and carrying the disclosure with its source tag. Chapters 3 and 4 need the same retrofit — that is a book-level item for `reconcile.py`, not Ch 5's to fix. Also note the competency separator drifts three ways (`— competency: X` / `— X` / `(X)`); pick one.

**T5 — Voyage Progress strip (low).** Ch 5 closes with a bare `🗺️ → 🌊 → 🌅` carrying no label. Ch 3 uses labelled mid-chapter lines; Ch 4 uses a labelled closing line; Ch 1 and Ch 2 use the strip not at all, and **Ch 1's marker legend never introduces Voyage Progress**. An unlabeled glyph strip doesn't identify itself to a reader who has met no legend for it. Recommend either adopting Ch 4's labelled closing form or dropping it, and separately adding Voyage Progress to Ch 1's marker table.

### Two corrections to the draft's own AUTHOR-REVIEW notes

These are the findings only a cross-chapter check produces, and in both cases the in-draft note would make Chapter 5 *less* consistent if acted on.

**T6 — The Zenith anchor is NOT malformed. Do not rename it.** The draft (at §9) and `image-specs.md` (lines 513, 558, 615) both flag `ch05-zenith-smallest-deployable-unit` as malformed against `ch{NN}-fig{MM}-{slug}` and propose `ch05-fig06-smallest-deployable-unit`. Against the book, that is backwards:

- `arc-outline.md` prescribes `chNN-zenith-<slug>` as the required anchor stub for **every** chapter's Zenith figure — `ch02-zenith-standard-crate`, `ch03-zenith-nobody-is-in-charge`, `ch05-zenith-smallest-deployable-unit`, `ch17-zenith`.
- **Chapter 2 already shipped `<!-- FIGURE: ch02-zenith-standard-crate -->` in published prose.**

Renaming would make Chapter 5 the only chapter in the book deviating from an established, published convention, and would break the pattern for the fifteen chapters still to be drafted. **Recommendation: close the note as "not a defect," keep the anchor, and add `chNN-zenith-<slug>` to the structural contract as a sanctioned second anchor form so the linter stops re-raising it.** The proposed-filename note in `image-specs.md` line 558 should be struck at the same time.

**T7 — The figure numbering is not out of order relative to its contract. Do not renumber.** The draft's note at §3 flags fig01 → fig03 → fig02 → fig04 → fig05 → zenith as out of document order. The five `figMM` slugs are prescribed verbatim by `arc-outline.md`, and Chapter 2 shipped with the same property (`ch02-fig04-cri-runtime-chain` appears before `ch02-fig03-oci-three-specs` in the published file). The anchors are the join key into `image-specs.md` and the numbering matches the outline. **Recommendation: close as "matches outline; precedent set in Ch 2."** The draft was right to preserve them unrenamed.

---

## Callback correctness

### Back-references to earlier chapters — 7 correct, 2 incorrect

| # | Callback in Ch 5 | Target actually covers | Verdict |
|---|---|---|---|
| 1 | §1 — `Ch 2 §1 — containers are not the schedulable unit` | Ch 2 §1, line 318: *"containers are not the unit Kubernetes schedules. Something wraps them."* | ✅ |
| 2 | §1 — `Ch 3 §5 — the kubelet and what it ensures` | Ch 3 §5 is **"The Only Door In"** (API server hub). The kubelet is **Ch 3 §3**, "Node Components in Context," line 441 | ❌ |
| 3 | §4 — `Ch 4 §7 — what Chapter 5 introduces` | **Ch 4 has six numbered sections.** The text quoted ("Chapter 5 introduces the disposable thing") is Ch 4's **The Voyage Ahead**, line 1192 — an unnumbered closing section | ❌ |
| 4 | §5 — `Ch 2 §6 — ImagePullBackOff and where its state is defined` | Ch 2 §6, line 783: *"`ImagePullBackOff` is reported as a container in the **Waiting** state… container states are Chapter 5's material"* | ✅ |
| 5 | §6 — `Ch 4 §3 — namespaced and cluster-scoped objects` | Ch 4 §3 "Where a Name Lives" → "Not everything lives in a namespace" | ✅ |
| 6 | §6 — `Ch 4 §4 — the service-account-token Secret type` | Ch 4 §4 → "Types of Secret," line 517/531 | ✅ |
| 7 | Bearings #1 A5 — `Ch 3 §6 — controllers and control loops` | Ch 3 §6 "Controllers and the Control Loop" | ✅ |
| 8 | Soundings A7 — *"re-read Chapter 4 §2"* | Ch 4 §2 → "The two fields that matter most" (spec/status) | ✅ |
| 9 | Soundings A8 — *"re-read Chapter 2 §6"* | Ch 2 §6 (lines 743–786) contains the `ImagePullBackOff` treatment | ✅ |

**Fix C1 (§1, "The PodSpec, finally"):** `*[cross-bearing: see Ch 3 §5 — the kubelet and what it ensures]*` → `*[cross-bearing: see Ch 3 §3 — the kubelet and what it ensures]*`. Note Ch 4 already uses "Chapter 3 §5" correctly for the API-server/etcd material (Ch 4 line 356), so §5 is genuinely spoken for.

**Fix C2 (§4, opening):** `*[cross-bearing: see Ch 4 §7 — what Chapter 5 introduces]*` → `*[cross-bearing: see Ch 4 — The Voyage Ahead]*`. (Chapter 4's own headings render as `## ⚪ 2. …` without the `§` glyph but the chapter refers to itself as "§2", so the `§N` convention holds for Ch 4 — there simply is no §7.)

### Un-numbered chapter-level callbacks — all verified

- §4, "The same instinct, one level up" — Ch 2 §2 "Immutability, and why it's a rule rather than a preference" ✅
- §1 — Chapter 3's kubelet sentence quoted verbatim; matches Ch 3 line 443 word for word ✅
- Why This Chapter Matters — "since Chapter 2, where it arrived with an IOU attached"; Ch 2 line 318 is exactly that IOU ✅
- §5 opening — "Chapter 2's second promise comes due"; Ch 2 line 783 ✅
- §4 ⚓ Worth Securing — quotes Ch 4's UID definition verbatim (Ch 4 line 226) ✅

### Inbound promises from earlier chapters — 4 of 4 honored

This is the strongest result in the check. Every section number an earlier chapter published about Chapter 5 resolves correctly:

| Published in | Promise | Ch 5 delivers |
|---|---|---|
| Ch 2 §1 | `Ch 5 §1 — the Pod as the unit of scheduling` | §1 "The Pod as the Unit of Scheduling" ✅ |
| Ch 2 §6 | `Ch 5 §5 — Pod phases and container states` | §5 "Pod Phases and Container States" ✅ |
| Ch 3 §3 | `Ch 5 — Pods, PodSpecs, and what "running and healthy" means precisely` (no §) | §1 + §7 ✅ |
| Ch 4 §4 | `Ch 5 §6 — a Pod's identity` | §6 "A Pod's Identity" ✅ |

### Forward cross-bearings — chapter assignments all correct; 3 section conflicts

All 17 forward pointers land on the chapter that the arc outline says owns the material. Sections are unverifiable except where an already-published chapter pinned them. Three conflicts:

**F1 — HARD COLLISION: `Ch 9 §1`.** Chapter 5 §1 pins `*[cross-bearing: see Ch 9 §1 — why a Service is necessary]*`. **Chapter 2 already published `*[cross-bearing: see Ch 9 §1 — CNI and pod networking]*`.** Two different topics, same section, and Chapter 9 is undrafted so neither is yet true. The arc outline's coverage order for Ch 9 is *network model → Pod IP → CNI → Service → ClusterIP…*, which favors Ch 2's claim. **Recommend Ch 5 move to `Ch 9 §2` or `§3`** — author decision, but it must be resolved before Ch 9 drafts, or Ch 9 will be authored against contradictory published promises.

**F2 — PROBABLE ORDERING CONFLICT: `Ch 17 §2` and `§3`.** Chapter 5 pins autoscaling at `Ch 17 §2` and the mesh data plane at `Ch 17 §3`. Chapter 2 published `Ch 17 §4 — the four pluggable interfaces, collected`. The arc outline's Ch 17 order is *cloud-native definition → characteristics → **extension-points synthesis** → service mesh → serverless → **autoscaling landscape** → governance*. If extension points are §4, mesh and autoscaling both fall at §5+, and autoscaling comes **after** mesh, not before it. Chapter 5's §2/§3 are almost certainly wrong on both counts. **Recommend dropping the section numbers to chapter-level (`see Ch 17 — the mesh data plane`) until Ch 17 is outlined**, which is a sanctioned form (Ch 3 line 447 already does this).

**F3 — `Ch 12 §2` (low confidence, no conflict).** `Ch 12 §2 — ServiceAccounts as RBAC subjects`. The outline's Ch 12 order puts the lifecycle/4Cs framing first, RBAC second, ServiceAccounts/TokenRequest third. §2 is defensible if SAs-as-subjects is treated inside the RBAC section, but §3 is likelier. No published claim conflicts with it; flagging only so it is a decision rather than an accident.

**Verified clean:** `Ch 6 §1` (matches Ch 4's published `Ch 6 §1 — Deployments and ReplicaSets`), `Ch 7 §2` (compatible with Ch 2's `Ch 7 §3`), `Ch 11 §1` (matches the outline's volume-types-first ordering), `Ch 13 §2/§3/§4` (compatible with Ch 2's `Ch 13 §2`), `Ch 15 §4`, `Ch 16 §1/§2`, `Ch 18 §1/§3`.

---

## Retrieval-practice accuracy

**All 10 tagged items verified against the published chapters. Zero misaligned.**

| Item | Tag | Topic | Present in target chapter? |
|---|---|---|---|
| Soundings Q7 | ch4 | `spec` / `status`; which reports what is true now | ✅ Ch 4 §2, "The two fields that matter most" |
| Soundings Q8 | ch2 | `ImagePullBackOff`; reported as **Waiting** | ✅ Ch 2 §6, line 783 — including the "Waiting" half |
| Bearings #1 Q5 | ch3 | kubelet ensures PodSpec containers running and healthy | ✅ Ch 3 §3, line 443 (verbatim source sentence) |
| Bearings #2 Q4 | ch2 | `ImagePullBackOff` as a container `Reason` | ✅ Ch 2 §6 |
| Bearings #2 Q5 | ch4 | which of `spec`/`status` carries `phase`; who writes it | ✅ Ch 4 §2 + the 🪝 Snag at line 275 (*"`status` is not something you write"*) |
| Practice Q5 | ch4 | labels as identifying attributes in `metadata`, selectable | ✅ Ch 4 §5, "The Universal Join" |
| Practice Q13 | ch4 | `kubernetes.io/service-account-token` as legacy; TokenRequest since v1.22 | ✅ Ch 4 §4, line 531 — Ch 4 publishes the v1.22/TokenRequest fact itself, so this is genuine retrieval, not new material wearing a retrieval tag |
| Practice Q20 | ch2 | container immutability as a design principle | ✅ Ch 2 §2, "Immutability, and why it's a rule rather than a preference" |
| Practice Q21 | ch3 | the control loop; kubelet as reconciliation | ✅ Ch 3 §6; distractor A ("queries etcd directly") is correctly rebutted from Ch 3 §5's hub-and-spoke |
| Practice Q22 | ch2 | image pull failure gating the init sequence | ✅ Ch 2 §6 for the ch2 half |

**Rate.** 8 tagged items across 15 Bearings + 23 Practice = **21.1%**, against the arc outline's Ch 5 target of **20% [B3]** drawn from Ch 2–4. On target. The draft's own arithmetic (line in the Practice preamble) checks out. Soundings retrieval sits outside this count, correctly — `retrieval-architecture.md` line 12 excludes Soundings from the budget while noting they do the spacing work anyway, and Ch 3 already tags Soundings items the same way (`*[retrieval: ch2]*`, Ch 3 line 210), so Ch 5's tagged Soundings are established practice.

**R1 — one prescribed anchor only partially hit (low).** The outline names three anchors for Ch 5: *"`imagePullPolicy` (Ch 2) as a cause of a container state; spec/status (Ch 4) read against Pod phase; labels (Ch 4) on a Pod."* The second and third are hit exactly (Bearings #2 Q5; Practice Q5). The first is hit in its neighborhood — the chapter retrieves `ImagePullBackOff` and the BackOff retry behavior three times but **never names `imagePullPolicy` itself**, which is the field the outline specified and which Ch 2 spent §6 on. Cheapest fix: one distractor or one clause in Practice Q22's rebuttal that names `imagePullPolicy`. Author's call whether it's worth it.

**R2 — retrieval tags absent from the answer keys (low).** Ch 4 repeats the tag in its answers (`**Q3. [retrieval: ch3] Answer: D.**`, line 1055; `**5. [retrieval: ch3]**`, line 356). Ch 5 tags only the stems. Repeating it in the key tells a reader who missed the item *which chapter to go back to* — which is the whole point of the tag. Recommend matching Ch 4.

---

## Glossary coverage

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| Pod | yes (§1) | yes |
| PodSpec | yes (§1) | yes |
| shared network namespace (Pod-scoped) | yes (§1) | yes |
| sidecar | yes (§2, functional) | yes |
| init container | yes (§3) | yes |
| Pod phase (`Pending`/`Running`/`Succeeded`/`Failed`/`Unknown`) | yes (§5) | yes — one entry |
| container state (`Waiting`/`Running`/`Terminated`) | yes (§5) | yes — one entry |
| `Reason` (container status field) | yes (§5) | yes |
| `restartPolicy` | yes (§5) | yes |
| restart backoff (exponential, 5-min cap, 10-min reset) | yes (§5) | yes |
| ServiceAccount | yes (§6) | yes |
| `default` ServiceAccount | yes (§6) | fold into ServiceAccount |
| TokenRequest API | partial — one sentence (§6) | yes (or defer definition to Ch 12 and cross-reference) |
| **projected volume** | **no — named only (§6)** | **yes — or add a cross-bearing to Ch 11** |
| probe | yes (§7) | yes |
| `livenessProbe` | yes (§7) | yes |
| `readinessProbe` | yes (§7) | yes |
| `startupProbe` | yes (§7) | yes |
| probe mechanisms (`exec`/`httpGet`/`tcpSocket`/`grpc`) | yes (§7) | yes — one entry |
| probe parameters (`initialDelaySeconds` etc.) | partial, deliberately (§7) | optional |
| resource request | yes (§8) | yes |
| resource limit | yes (§8) | yes |
| CPU throttling | yes (§8) | yes |
| OOM kill | yes (§8) | yes — see G2 |
| resource units (`m` millicpu, `M` vs `Mi`, 1 cpu = 1 core) | yes (§8) | yes — one entry |
| extended resources | yes — one line (§8) | yes |
| `ephemeral-storage`, `hugepages-<size>` | named only (§8) | optional |
| workload resource | yes — brief (§4) | yes |
| endpoints controller / Service endpoints | no — deferred with cross-bearing to Ch 9 §4 | no — Ch 9 owns |
| `emptyDir` | named only, cross-beared to Ch 11 §1 | no — Ch 11 owns |
| `kubectl logs -c` | named, cross-beared to Ch 13 §3 | no — Ch 13 owns |

**Totals: 29 introduced · 28 defined in-chapter · 24 require book-level glossary entries · 1 introduced without definition.**

**G1 — `projected volume` is used undefined and uncross-referenced (medium).** §6: *"mounts it as a **projected volume**."* Chapter 11 owns `projected` in its volume-types list. Right now a reader meets a bolded technical term with no definition and no pointer. Every other deferred term in this chapter carries a cross-bearing (`emptyDir` → Ch 11 §1; `kubectl logs -c` → Ch 13 §3; RBAC → Ch 12 §2), so this is an omission rather than a policy. **Fix: append `*[cross-bearing: see Ch 11 §1 — projected volumes]*`.** Cheapest of any fix in this report.

**G2 — reserve the `OOMKilled` status string for Ch 13 (low).** §8 correctly teaches the *mechanism* ("OOM kills," "OOM-killed") and routes the *status string* forward via `*[cross-bearing: see Ch 13 §4 — OOMKilled and Evicted]*`. The arc outline confirms Ch 13 owns `OOMKilled` as a Pod failure signature. Current handling is right; the glossary entry should be filed under Chapter 13, not Chapter 5, so Stage 14 doesn't cross-reference it to the wrong chapter.

**G3 — `StatefulSet` named without a pointer (low).** §4's 🪝 Snag: *"why StatefulSets are different."* Chapter 6 introduces StatefulSet. Either add a cross-bearing or drop the clause. **Caution:** do not pin it to `Ch 6 §3` — that section is already double-claimed (Ch 1's format example says StatefulSets, Ch 2 says CRDs). Use a chapter-level pointer until Ch 6 is outlined.

---

## Contradictions with earlier canon

**None found.** Every factual claim in Chapter 5 that overlaps published material is consistent with it:

- Ch 3 §2 (line 415): *"the scheduler selects a node and records that choice. It does not start anything"* ↔ Ch 5 §8: kube-scheduler reads requests "to choose a node." Consistent.
- Ch 4's Voyage Ahead (line 1188) already published *never rescheduled → replaced → different UID*, sourced to the same snapshot Ch 5 §4 uses. Identical, not contradictory — and a legitimate spaced-repetition beat.
- Ch 4 (line 1186): the phase is *"the first thing you look at when something is wrong"* ↔ Ch 5 §5: *"the phase cannot tell you"* whether the app is healthy. Compatible (first ≠ sufficient), and Ch 5 harmonizes them explicitly with Ch 13's *"read the phase before you read the logs."* No fix needed.
- Ch 2 §1: Pods come "with a shared network namespace" ↔ Ch 5 §1's expansion. Consistent.

### One collision risk worth an author decision

**X1 — two different "five minute" caps, fifteen lines apart (medium).** §5 states the kubelet's restart backoff is *"capped at five minutes,"* and then the `ImagePullBackOff` worked example states the image-pull backoff retries *"up to a compiled-in limit of 300 seconds (five minutes)"* — the same figure Chapter 2 §6 already published for a **different** mechanism. Both numbers are correct and both are sourced. But a reader meeting them in one section will reasonably conclude they are one cap, and the chapter never says they are not. Recommend one clause: *"a separate backoff from the container-restart backoff above, governing pulls rather than restarts."* This is precisely the sort of thing that only surfaces when the two chapters are read together.

### Adjacent findings in earlier chapters (NOT Chapter 5 defects — for `reconcile.py`)

Surfacing these because they are the same class of error and the reconciliation pass should see them; none blocks Chapter 5.

- **Ch 4 line 1176 says "Chapter 4 of 15 complete."** The book has **20** chapters (`arc-outline.md`, `total_chapters: 20`). Chapter 5 correctly avoids a count in its Safe Harbor line.
- **Ch 4 line 617** directs readers to *"re-read Chapter 2 §4"* for the registry-credentials list. That list is Ch 2 **§3** (line 457); §4 is the CRI section.
- **`Ch 6 §3` is double-claimed** — Ch 1's cross-bearing format example says "StatefulSets and stable identity," Ch 2's real cross-bearing says "CRDs and extending the API." The outline's Ch 6 ordering supports neither (CRDs are last).
- **`Ch 11 §2 — CSI` (Ch 2)** looks wrong against the outline, which places CSI at the end of Ch 11's coverage. Chapter 5's `Ch 11 §1 — volume types` is the one that matches.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** The chapter contains no statistics of any kind — no "73% of breaches," no invented pass rates. Every number is a sourced mechanism value (300 s, 10 s/20 s/40 s, 5-minute cap, 10-minute reset, HTTP ≥200/<400, v1.22, `1m` floor). Cross-referenced against the fact-accuracy stage's scope; not re-audited here per rule 3.
- [x] **Fear-based content uses real examples.** The two arousal beats — *"a terminal at two in the morning with a pager still buzzing"* and *"at three in the morning"* — are practitioner-experience framings, not exam-failure threats. §5's *"Chapter 13 will be unusable for them"* is a stated structural fact about the book, not manufactured urgency. Also clean against the v5.7 subject-dignity guardrail: no humor beat in this chapter is aimed at anyone harmed by a failure. Every wry line lands on the practitioner ("unless you plan to sit watching a terminal forever"; "usually at two in the morning, while trying to make a stuck object look healthy" — Ch 4's register, matched).
- [x] **Simplification acknowledged.** Two `Dead Reckoning` blocks (Why This Chapter Matters; §5's phase/state split). §7 explicitly declines to teach probe tuning and says why. §8 names `ephemeral-storage`/`hugepages`/extended resources and stops. §5 states outright that *"the phase cannot tell you that,"* which is the Order/Truth balance done properly.
- [x] **Authority claims cite legitimate sources.** All inline claims carry `[source: …]` tags against cached snapshots. **One condition, below.**
- [x] **"Frequently tested" claims verifiable.** The chapter makes no unhedged frequency claims. The single soft one — the subtitle's *"worth points"* — is defended structurally in §9 rather than asserted. **One fix:** the `7%` metadata figure is an authored allocation presented without the disclosure Ch 1 promised and Ch 2 modeled. See **T4**; this is the only item on this checklist with an action attached.
- [x] **No strawmanning of alternative study methods.** None present. §2's rebuttal of the "one process per Pod" Docker-era doctrine engages it on the merits and explicitly declines to endorse the opposite absolutism.

**Condition on the "authority claims" pass.** Five load-bearing claim clusters are stated confidently in prose while carrying no source tag, flagged only in HTML comments the reader never sees: init-container semantics (§3, including a ★ Fixed Point, a 🪢 Mnemonic, Bearings #1 items 3–4, and Practice 4/10/22), the "two main ways Pods are used" framing (§2), "smallest deployable unit" (§9 title, Summary, anchor slug), the PodSpec-equals-`spec` identity (§1), and probe-type/mechanism orthogonality (§7, on which Practice Q17's correct answer rests). Against guardrail #4 — *never claim certainty where legitimate uncertainty exists* — flagging in an invisible comment is not the same as hedging to the reader. The draft handled this correctly by **not** fabricating tags, and the material is retrievable (all five snapshots were fetched by the research stage and preserved in `research-manifest.md`; they were simply never materialized into `sources/`). **This checklist item passes on the condition that the five snapshots are materialized and the claims tagged before publication.** If any cannot be, the affected prose must be softened to an explicit authorial gloss rather than shipped as a bare assertion — and the two graded items whose correct answers depend on untagged claims (Practice Q17, Practice Q10's distractor C rebuttal) must be reworked or cut.

---

## Recommended fixes

The revision stage caught a great deal — the phase/`Running` contradiction in the worked overlay, the unsourced QoS paragraph, the `restartPolicy` absolute negative, and the §9 aggregation claim were all correctly identified and handled. Everything below is new at this stage, because all of it requires reading Chapter 5 against the other four chapters and the outline.

**Blocking — must resolve before Chapter 6 drafts**

1. **C1.** §1: `Ch 3 §5` → **`Ch 3 §3`** for the kubelet. (§5 is the API-server hub and is already correctly cited as such by Ch 4.)
2. **C2.** §4: `Ch 4 §7` → **`Ch 4 — The Voyage Ahead`**. Chapter 4 has six sections.
3. **F1.** §1: resolve the `Ch 9 §1` collision with Chapter 2's published claim. Author decision; Ch 2's claim has precedence and the outline's ordering supports it.

**Should fix before publication**

4. **T4.** Conform the metadata line to Chapter 2's form, with the authored-allocation disclosure and source tags. This is also the answer to the draft's own AUTHOR-REVIEW at line 6: it does not currently match, and neither do Ch 3 and Ch 4 — flag those for `reconcile.py`.
5. **T6 / T7.** Close the two figure-anchor AUTHOR-REVIEWs as **not defects**. `ch05-zenith-smallest-deployable-unit` and the outline-prescribed `figMM` order are both book convention with published precedent in Chapter 2. Renaming would create the inconsistency the notes are trying to prevent. Strike the rename proposal from `image-specs.md` line 558 at the same time, and consider adding `chNN-zenith-<slug>` to the structural contract so the linter stops re-raising it.
6. **G1.** §6: add `*[cross-bearing: see Ch 11 §1 — projected volumes]*`. One-line fix for the chapter's only undefined-and-unpointed term.
7. **T3.** `## Exam Alert` → `## Exam Alert! 🚨`.
8. **T2.** Move the Bearings topics into their headings, matching Ch 2 and Ch 3.
9. **X1.** One clause distinguishing the image-pull 300 s cap from the container-restart 5-minute cap.
10. **F2.** Drop the section numbers from the two `Ch 17` cross-bearings until Ch 17 is outlined; the current §2/§3 conflict with Ch 2's published `Ch 17 §4` and with the outline's own ordering.

**Optional / author's call**

11. **T1.** `ServiceAccount` casing outside the verbatim definition. **T5.** Label or drop the Voyage Progress strip (and add it to Ch 1's marker legend either way). **R1.** Name `imagePullPolicy` once so the outline's first retrieval anchor is hit precisely. **R2.** Repeat retrieval tags in the answer keys, as Ch 4 does. **G3.** Cross-bearing or cut for the StatefulSet mention in §4.

**Two open items this stage cannot close, carried forward for the author**

- **QoS classes are outline-mandated and absent.** `arc-outline.md` lists them under Ch 5's *Covers*, *Key concepts introduced*, and the `ch05-fig05-requests-limits-qos-classes` anchor, and `image-specs.md` line 507 marks the figure **BLOCKED** on the same gap. The draft was right to cut rather than write from memory — Open question #2 forbids it — but Chapter 5 currently under-delivers against its own contract, assesses zero QoS items, and ships a figure with a deliberately empty strip. `k8s-docs-pod-qos-2026-08-24` is preserved in `research-manifest.md` line 293 and needs only materializing. Note the guard the draft correctly identified: that page's loose *"Any Container exceeding a resource limit will be killed and restarted"* contradicts §8's verified CPU-throttles/memory-OOM-kills asymmetry and must not overwrite it.
- **Graceful termination is absent** though the outline's `kb_tags` claim `pod-termination` under D1.1. Snapshot retrieved, never materialized (`research-manifest.md` line 434). One short paragraph at the altitude Open question #5 specified would close it and strengthen Chapter 15's twelve-factor disposability callback.

Question budget, for the record: 8 Soundings + 15 Bearings + 23 Practice = **46**, against the outline's 8/10/21 = 39. Bearings are explicitly *"minimums to exceed"* per the outline, so 15 is sanctioned; Practice is +2, justified in-draft by the two interleaving items (Q22, Q23) that close the only path to testing `phase: Succeeded`. Both additions earn their place. No action needed.