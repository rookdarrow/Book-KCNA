I have what I need. Producing the manifest.

---

I verified the integration report's headline blocker independently rather than passing it through, and it resolves decisively rather than needing an author coin-flip. I also found that **eleven of this chapter's snapshot files are truncated on disk while their frontmatter asserts they are complete** — which invalidates the premise of the draft's own chapter-wide sourcing note, and closes most of its flagged gaps for free.

# Knowledge-Base Manifest — KCNA Chapter 16

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-31

> **Greenfield notice, re-verified directly, not inherited.** `Book-KCNA/knowledge-base/` **still does not exist on disk** — checked this run. Fifteen manifests exist (`ch-01` … `ch-15`); none has been applied. Chapter 16 adds the sixteenth.
>
> **Ordering contract, inherited unchanged from Ch 12–15.** **APPEND** for the three shared registers and for every shard that already exists; **WRITE** only for filenames that collide with nothing. I enumerated every `concepts/*.md` reference across `ch-01`–`ch-15` and checked all 21 proposed Ch 16 slugs against it: **no collisions.** Chapter 16 introduces **no new full-file WRITE to a shared register**, so ⚑ I1's blast radius is unchanged.

---

## ⚑ The finding that changes what everyone downstream should do

### ⚑ C0. CRITICAL — eleven snapshot files are truncated on disk, and their frontmatter says they are complete

The draft carries a chapter-wide `AUTHOR-REVIEW` explaining that nine tagged claims cite passages "absent from the *packed* snapshot corpus, because packing truncated eleven Kubernetes pages at their first code fence," retains the tags "because each snapshot's own frontmatter asserts the passage is on disk," and instructs: *"Re-run the fact-accuracy audit against the untruncated snapshot files before print."*

**There are no untruncated snapshot files.** The truncation is on disk, in `sources/`, not in the packing step. Measured this run:

| Snapshot | Lines on disk | Complete? |
|---|---|---|
| `k8s-docs-debug-service-2026-08-31.md` | **16** | ends mid-page at the first ` ```none ` fence |
| `k8s-docs-kubectl-debug-reference-2026-08-31.md` | **13** | ends after `## Synopsis`; **no Flags table** |
| `k8s-docs-get-shell-running-container-2026-08-31.md` | **16** | truncated |
| `k8s-docs-determine-reason-pod-failure-2026-08-31.md` | **18** | truncated |
| `k8s-docs-port-forward-2026-08-31.md` | **18** | truncated |
| `k8s-docs-port-forward-authorization-2026-08-31.md` | **19** | truncated |
| `k8s-docs-debug-init-containers-2026-08-31.md` | **21** | ends before the `Init:N/M` status table |
| `k8s-docs-debug-pods-2026-08-31.md` | **25** | truncated |
| `k8s-docs-debug-statefulset-2026-08-31.md` | **25** | truncated |
| `k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31.md` | **23** | truncated |
| `k8s-docs-local-debugging-telepresence-2026-08-31.md` | **25** | truncated |
| — compare the 08-23/24/25 captures — | | |
| `k8s-docs-statefulset-storage-2026-08-25.md` | 132 | complete |
| `k8s-docs-statefulset-2026-08-24.md` | 98 | complete |
| `k8s-docs-endpointslices-2026-08-24.md` | 82 | complete |
| `k8s-docs-init-containers-2026-08-24.md` | 75 | complete |

**Every 2026-08-31 capture is truncated; every earlier capture is intact.** The cut lands at the first fenced code block in each file. `debug-service`'s frontmatter meanwhile reads `transcription: "verbatim"` and *"Everything bearing on selectors, ports, DNS and EndpointSlices is complete."* The file is 16 lines and contains one quotation.

**The full text was captured and is not lost.** `ch-16/research-manifest.md` (76 KB) transcribed all twelve pages *before* the write to `sources/`. Every one of the nine claims the draft flagged as unverifiable is recoverable verbatim from it, at no cost and with no re-fetch:

| Draft's flagged claim | Recovered verbatim from `research-manifest.md` |
|---|---|
| `Init:N/M` / `Init:Error` / `Init:CrashLoopBackOff` vocabulary | the full status table, A5 §"Understanding Pod status" |
| `-c` flag form for init logs | `kubectl logs <pod-name> -c <init-container-2>`, A5 |
| The `--` argument boundary | *"The double dash (`--`) separates the arguments you want to pass to the command from the kubectl arguments."* |
| port-forward is TCP-only | *"`kubectl port-forward` is implemented for TCP ports only. The support for UDP protocol is tracked in issue 47862."* |
| `debug node/` description | the four-bullet block: name auto-generated, root filesystem at `/host`, host IPC/Network/PID namespaces, **pod is not privileged** |
| the three `debug-service` quotes | A6, all marked `[VERBATIM]` |
| the profile names | A4 Flags table |
| `--target`'s own behavior | **see ⚑ C1 — this one closes a gap the draft says is open** |
| `describe pod` shows init containers with state and exit code | **see ⚑ C2 — this one reverses a revision-stage cut** |

**Recommended action, in order:** (1) reconcile `sources/*.md` against `ch-16/research-manifest.md` for the eleven files — mechanical, free, and it must happen before the fact-accuracy re-audit, not after; (2) **check whether the same truncation hit chapters 08–15**, whose 2026-08-31 captures were written by the same code path — this is a book-level integrity question, not a Chapter 16 one; (3) correct the frontmatter completeness assertions, which are the reason no earlier stage caught this.

---

## ⚑ Contradictions, conflicts, and corrections — flagged, not resolved

Rule 6 requires these loud. Three of the draft's own open items close on evidence already in the corpus, and the integration report's blocker resolves in a direction it did not consider.

### ⚑ C1. HIGH — `--target` **is** documented in the corpus. The draft's gap note is stale.

The draft cut its specific `--target` claim and left: *"The flag's own behavior is documented on no cached page — verify against the untruncated generated CLI reference … and restore the specific claim with a tag if so."*

It is there, verbatim, in the A4 transcription:

> `--target string` — *"When using an ephemeral container, target processes in this container name"* — `k8s-docs-kubectl-debug-reference-2026-08-31`

That is precisely the claim draft-v1 made and the revision removed. **Restore it with the tag** once C0's reconciliation puts the Flags table back on disk. The process-namespace-sharing quote the revision correctly re-attached should stay where it is — it supports the principle, and `--target` now supports itself.

Two further flags from the same table that the chapter should know about:

- `--replace` — *"When used with '--copy-to', delete the original Pod"*. The §3 ★ Fixed Point says *"the original Pod is not touched — and that is the feature."* True for `--copy-to` alone, and Practice Q4's stem uses `--copy-to` alone, so **Q4 is safe**. But the Fixed Point is stated unconditionally and `--replace` is the documented exception. One clause fixes it; the shard below carries the caveat so a later chapter does not inherit an overclaim.
- `--share-processes` defaults to **true** with `--copy-to`. The draft's §3 example passes it explicitly, which is fine and clearer, but it is not required.

### ⚑ C2. MEDIUM — the revision over-corrected the §2 Snag. Restore the cut detail.

Draft-v1's Snag said `kubectl describe pod` lists init containers *"in order, along with each one's state and exit code."* The revision cut the specifics as unsourced, leaving only "listed," and asked a later stage to verify.

A5's transcription carries the exact `describe` output, and it shows all three:

```
Init Containers:
  <init-container-1>:
    State:           Terminated
      Reason:        Completed
      Exit Code:     0
  <init-container-2>:
    State:           Waiting
      Reason:        CrashLoopBackOff
    Last State:      Terminated
      Reason:        Error
      Exit Code:     1
```

Ordering, `State`, and `Exit Code` are all present. **Restore draft-v1's wording with `[source: k8s-docs-debug-init-containers-2026-08-31]`.** The revision's caution was right in method and wrong on the facts, because it was reading the truncated file.

### ⚑ C3. HIGH — the Pod Security Admission gap is already closed. Three PSA snapshots are cached.

The draft's second-highest-priority flag says the ⚠ Navigational Hazard on admission refusing a debug container *"has NO cached snapshot behind it,"* that *"there is no PSA or Pod Security Standards page in this chapter's corpus,"* and instructs: *"**Cache** `.../pod-security-admission/` and `.../pod-security-standards/` **before print**."

Three are already on disk:

- `k8s-docs-pod-security-admission-2026-08-31.md`
- `k8s-docs-pod-security-standards-2026-08-23.md`
- `k8s-docs-pod-security-standards-profiles-2026-08-31.md`

And the third one supports the Hazard's exact mechanism. Under **Restricted**:

> **Running as Non-root** — require non-root execution.
> Fields: `spec.securityContext.runAsNonRoot` **and the container/init/ephemeral variants.**
> Allowed: `true`.
> — `k8s-docs-pod-security-standards-profiles-2026-08-31:80–82`

`ephemeralContainers[*]` appears in the field lists for HostProcess, privileged containers, host-namespace probe/lifecycle fields, and `runAsNonRoot`. **The Pod Security Standards constrain ephemeral containers by name.** A debug image running as root, injected into a `restricted` namespace, violates a control that explicitly names the ephemeral variant.

**The Hazard is sourceable as written, with no fetch.** Tag it to `k8s-docs-pod-security-standards-profiles-2026-08-31`, and keep the `[cross-bearing: see Ch 12 §6]` — the reciprocity is already good (`chapter-12:1342` states the claim and points forward at Ch 16 §3). **Practice Q9's correct answer, which the draft flagged as resting entirely on unsourced canon, now rests on a snapshot.**

One caveat for the tag: that snapshot condenses the upstream field enumeration as *"and the container/init/ephemeral variants."* Cite it for the fact that the standards reach ephemeral containers — do not present the condensation as a verbatim field list.

*Note the shape of C1–C3 together: all three were flagged by the draft as "verify before print," and all three were already answered inside the repository. That is C0's cost showing up as wasted downstream work, and it will keep happening until `sources/` is reconciled.*

### ⚑ C4. BLOCKER — the EndpointSlice contradiction, adjudicated. **Ch 16 is right, and Ch 9's error has a traceable cause.**

The integration report frames this as two chapters each citing snapshots, with *"the upstream docs themselves inconsistent across pages,"* and hands the ruling to stage 6 as a coin-flip. **It is not a coin-flip, and the docs are not inconsistent — they describe two different API objects.**

**What Ch 16 cites**, from a complete on-disk snapshot:

> *"The control plane automatically creates EndpointSlices for any Kubernetes Service that has a selector specified. These EndpointSlices include references to **all the Pods that match the Service selector**."* — `k8s-docs-endpointslices-2026-08-24:32`

> *"The `serving` condition indicates that the endpoint is currently serving responses… For endpoints backed by a Pod, this maps to the Pod's `Ready` condition."* — `:64`

Membership is by selector. Readiness is a **condition on the endpoint**, not a filter on membership.

**What Ch 9 cites** — and this is the decisive part:

> *"readinessProbe — … if it fails, **the endpoints controller removes the Pod's IP address from the endpoints** of all Services that match the Pod."* — `k8s-docs-pod-lifecycle-2026-08-23:27`

That is the **legacy `Endpoints` object's** behavior, quoted from the Pod-lifecycle page, which is not the EndpointSlice page and is not describing the object Ch 9 teaches.

**And Ch 9's own manifest records why it had to.** `ch-09/kb-manifest.md:693`:

> ⚑ *"`ready` / `serving` / `terminating` appear individually, each where the Pod-termination snapshot states it — never as* the *documented condition set, because `k8s-docs-endpoint-slices-2026-08-24` **was fetched and never written** (body in `research-manifest.md` §2)."*

**Chapter 9 was drafted without the EndpointSlice page body on disk.** It reasoned from the nearest available page, which describes the older object. The page is on disk now — as `k8s-docs-endpointslices-2026-08-24.md`, note the un-hyphenated filename, which is why nobody found it later — and it says something different.

A contributing cause worth recording: that snapshot's own frontmatter tags itself `concepts_covered: [… "readiness-gated-membership" …]`, which contradicts its body. The metadata says membership is readiness-gated; the body says it is not.

**Recommendation to stage 6: rule for Ch 16 and repair Ch 9.** Not because Ch 16 is newer, but because Ch 9 cited a page about a different object under documented duress, and the correct page is now available. The repair is contained exactly as the integration report scoped it — `chapter-09` Fixed Point at `:740`, one Bearings answer (3→4) at `:844`/`:874`, Practice Q11's answer, two table rows, plus the inbound gloss at `:766` — and Ch 9 already carries the machinery, since `:750` and `:754` describe terminating endpoints staying in the slice with `ready: false`.

**Both chapters move in one commit, and `concepts/endpointslice.md` must be rewritten rather than appended to** — see ⚑ C5. Do not apply Chapter 16's writes for `endpointslice.md` piecemeal.

Two knock-on items for whoever makes the edit:

- Ch 9's shard deliberately excludes `publishNotReadyAddresses` because it *"would undercut the Fixed Point."* Under the corrected model there is no readiness gate on membership to undercut, and `publishNotReadyAddresses` becomes an ordinary note rather than a suppressed exception. The exclusion can be lifted.
- Ch 9's shard says *"the list is **not a boolean membership test** — it carries state."* **That sentence is already correct under the new model** and is the seed of the repair. Ch 9 got the principle right in the termination paragraph and then contradicted it in the Fixed Point.

### ⚑ C5. HIGH — two of the outline's own slugs, and one B7 row, encode the error C4 corrects

This is the part that will outlive the prose fix if nobody catches it now.

| Artifact | String | Problem |
|---|---|---|
| `ch-16/outline.md:193` | `kb_tags.concepts: "empty-endpointslice-as-symptom"` | The revision established that the two causes leave **different** traces: a selector mismatch leaves the slice empty; a readiness failure leaves it **populated and not ready**. The slug names only the first. |
| `ch-16/outline.md:195` | `kb_tags.concepts: "readiness-gating-endpoints"` | "Gating" is the membership-filter model. Readiness **conditions** an endpoint; it does not gate its membership. |
| `term-ownership.md:517` | `\| Empty EndpointSlice (as a symptom) \| Ch 16 §4 \|` | Same defect, in the binding ledger. |
| `research-manifest.md:1293` Gaps item 4 | *"An empty endpoint list has two causes"* | Same. |

If the shard tree is built from the kb_tags list verbatim, the corrected prose ships above a concept index that still says "empty" and "gating," and the next chapter that reads the index inherits the error the chapter just fixed.

**Recommended renames, applied in the same commit as C4:**

- `empty-endpointslice-as-symptom` → **`no-ready-endpoints-two-signatures`**
- `readiness-gating-endpoints` → **`readiness-as-endpoint-condition`**
- B7 row 517 → **`No ready endpoints (empty slice vs. ready:false)`**

I have used the corrected slugs in the write blocks below. **If stage 6 rules for Ch 9 instead, do not apply this manifest's `§4` shards at all** — they would then be wrong under a new name, which is worse than wrong under the old one.

### ⚑ C6. MEDIUM — two inbound B7 obligations were never discharged, and both land here

| B7 row | Requires | Actual |
|---|---|---|
| `:512` **Distroless image** — first appears **Ch 2**, "name only, always with a pointer" | a named mention in Ch 2 | **grep across all 15 shipped chapters: zero occurrences of "distroless."** Ch 16 §3 is both definer and first appearance. |
| `:511` **`kubectl exec`** — first appears **Ch 3**, "name only, always with a pointer" | a named mention in Ch 3 | **zero occurrences in `chapter-03`.** Its actual first appearance is `chapter-13:390`, which names it and defers to Ch 16 §3. |

Neither is a Chapter 16 defect — Ch 16 does exactly what it was told. Both are **shipped-chapter retrofit decisions**, and for `kubectl exec` the cheaper fix is amending the row to `Ch 13` (which already delivers the name-only-with-pointer treatment the row asks for) rather than editing Ch 3.

**The draft's own `distroless` AUTHOR-REVIEW is wrong and should be deleted before it propagates.** It says the term *"has no owner in the term ledger and no ambient-tier row."* B7 `:512` assigns it to Ch 16 §3 in bold. The integration report caught this; recorded here so stage 14's successor does not chase it a third time.

**Not a finding, checked and clean:** "ephemeral container" does appear in `chapter-13`, but only inside an HTML `AUTHOR-REVIEW` comment at `:392`, never in reader-facing prose. B7's `Ch 16 §3 †` first-appearance dagger stands.

### ⚑ C7. MEDIUM — question inventory exceeds B4 by eight, and B4's own arithmetic is now twice wrong

| | B4 budget (`length-budget.md:66`) | Actual | Verdict |
|---|---|---|---|
| Soundings | 8 | 8 | ✅ |
| Taking Your Bearings | 10 | **16** (6 · 5 · 5) | ⚑ +6 |
| Practice | 15 | **17** | ⚑ +2 |
| **Chapter total** | **33** | **41** | ⚑ **+8** |

Above the skill's floor and above budget, same shape as Ch 15's ⚑ C7 (+6). Not a defect — the Practice pool grew by two because the question-quality audit's two highest-ranked coverage gaps were closed (Q16 `debug node/`, Q17 config-at-init), and both are good items. But **B4 has now been silently wrong for two consecutive chapters**, and the book's 715-question total is computed from it. Update B4 rather than leaving the arithmetic to drift a third time.

### ⚑ C8. GOOD NEWS — Chapter 16 breaks the three-chapter retrieval-tag drift on both counts

Ch 15's manifest raised two book-level tag problems. Chapter 16 resolves both without being asked.

**⚑ C5 from Ch 15 — "Practice pool reads as 0% retrieval for the third consecutive chapter."** Broken. Chapter 16 carries **3 `[retrieval:]` tags in the Practice pool** (Q12 `ch9`, Q13 `ch9`, Q14 `ch11`), which is the outline's stated floor of three, met exactly.

**⚑ C3 from Ch 15 — "the interleave tag now has three surface forms."** No fourth form. Grep across the draft returns **7 `[retrieval: chN]` tags and zero `[interleaved:]` or `[cross-domain:]`**. Chapter 16 emits no cross-domain tag at all, so the drift is frozen at three forms rather than growing. The book-level ratification sweep for Ch 13/14/15 is still owed, but Chapter 16 does not add to the bill.

| Chapter | Bearings retrieval | Practice retrieval | Verdict |
|---|---|---|---|
| Ch 13 | present | 0 | flagged |
| Ch 14 | 2 of 10 | 0 | flagged |
| Ch 15 | 4 of 16 | 0 | flagged, third running |
| **Ch 16** | **4 of 16** | **3 of 17** | ✅ **streak broken** |

### ⚑ C9. GOOD NEWS — the retired-blueprint ruling held, unprompted

Ch 14's and Ch 15's manifests both ruled: **do not restore the 8% figure**, because `cncf-curriculum-repo-kcna-versions-2026-08-23:36–44` records the retired PDF as text-not-extracted and says *"DO NOT draft the retired weights from memory or from third-party study guides,"* and `lf-kcna-program-changes-2026-08-23:11–15` carries a CORRECTION confirming that page never displayed them.

**Chapter 16's own outline carried the violation forward** — `ch-16/outline.md:244` reads *"D3 **doubled** from 8% to 16% in the 2025-11-24 revision [B1]."* Draft-v1 wrote it into the prose. **The revision stage cut it**, with a correct AUTHOR-REVIEW that reaches the same conclusion the two prior manifests did, apparently independently.

That is the ruling holding across three chapters and surviving a contaminated outline. Recorded as good news, with one carried debt: **`ch-16/outline.md:244` and `domain-analysis.md:39` still carry the claim** and will re-inject it into any later stage that reads them. Fix at the source, not per chapter.

### ⚑ C10. MEDIUM — the profile conflict is already adjudicated; the draft's note asks for work that is done

The draft's profile AUTHOR-REVIEW says the two snapshots disagree and asks the revision stage to *"confirm against a single dated snapshot before print."*

`research-manifest.md:1346–1351` already ran that adjudication and issued the ruling:

> *"§3 should name the five profiles both pages agree on, state that the default is `general` on current kubectl, and describe the shape … rather than presenting the set as fixed. … Tag the count to A4, not A2."*

**The draft followed it correctly** — it introduces the list with "include" rather than as complete, tags A4, teaches the shape, and grades nothing on the names. The item is closed; only the AUTHOR-REVIEW comment asking for it is outstanding. Delete the comment.

Worth carrying into the shard: the task page's `legacy` default is documented as *"planned to be deprecated in the near future,"* which is why the generated reference no longer lists it. The two pages are not in conflict so much as at different points in a deprecation.

### ⚑ C11. MEDIUM — the retrieval failure at Bearings 3 Q2 is real, and the fix is narrower than it looks

Confirmed independently. `persistentVolumeClaimRetentionPolicy`, `whenDeleted`, and `whenScaled` appear **nowhere in shipped `chapter-11`**, which teaches the Retain default (`:1235`, `:1412`) without naming the field. Q2 is tagged `[retrieval: ch11]` and its distractor C (*"Retain for whenDeleted, Delete for whenScaled"*) cannot be evaluated by a reader who has only Chapter 11.

But note what the stem asks: *"What is the default … for both the `whenDeleted` and `whenScaled` cases?"* The **answer** (Retain, both) is squarely Chapter 11's; only the **field vocabulary** is new. So the cheapest repair keeps the item and the tag:

> *"A StatefulSet's PersistentVolumeClaims are retained by default when a Pod is deleted **and** when the StatefulSet is scaled down. Which is true?"*

with options phrased in behavior rather than field names. That preserves a genuinely load-bearing retrieval — Q1 of the same checkpoint is undiagnosable without it — and moves the field-name vocabulary into the glossary, where §6's 🔭 Closer Look already introduces it as new material.

### ⚑ C12. LOW — three exam-frequency claims cross a ratified convention

Confirmed against the four sites integration cites (`chapter-12:1873`, `chapter-14:34`, `chapter-15:411`, `chapter-lineup:184`). Three lines assert what the exam favors:

- Why This Chapter Matters — *"What gets tested here is not flag syntax"*
- §3 ★ Fixed Point — *"the fact the exam reaches for"*
- Exam Alert #1 — *"the shape the exam favors"*

§3's *"the constraints are exam material"* is fine; `chapter-11:559` uses the same construction. The three above predict question design, which the convention reserves. All three are one-clause rewrites toward B1's actual, sourceable posture — *"know which kubectl verb answers which question"* (`domain-analysis.md:39`) — which says the same thing and is quotable.

### ⚑ C13. LOW — `kubectl cp` and `--copy-to` label handling remain genuinely open

The only two flagged gaps that **do not** close from the corpus. Both were correctly handled by the revision.

- **`kubectl cp`** (Practice Q6 option D). No snapshot exists. The revision re-led the rationale on the live-view distinction, which §3 establishes, and demoted the tooling dependency to an unnamed secondary clause. **Sound as written.** Restoring the `tar` specific needs `kubernetes.io/docs/reference/kubectl/generated/kubectl_cp/`.
- **`--copy-to` label inheritance.** No snapshot documents it. The revision cut draft-v1's hedge rather than pushing verification onto the reader. **Correct call** — the A4 Flags table lists no label-handling flag, so the behavior is genuinely undocumented in the corpus.

---

## Glossary entries added to `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md`

Two tiers, following Ch 11–15. The integration report marked **6 terms** as needing entries and **4** as needing new ledger rows; skill Part 16 requires every technical term the book introduces, so the **11 B7-owned Chapter 16 rows** (`term-ownership.md:505–519`) are harvested alongside them, plus four terms the chapter introduces that the ledger does not assign at all.

### Tier 1 — entries whose definition is unsourced, provisional, orphaned, newly graded, or corrected

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **`Init:N/M` status family** | `Init:N/M` = N of M init containers complete; `Init:Error` = an init container failed; `Init:CrashLoopBackOff` = failed repeatedly `[source: k8s-docs-debug-init-containers-2026-08-31]` — ⚠ **appears in NO shipped chapter** (Ch 13 uses `PodInitializing`) yet is graded twice, at Bearings 1 Q2 and Practice Q3 | Chapter 16 §2 |
| **Termination message** | *"Termination messages provide a way for containers to write information about fatal events to a location where it can be easily retrieved and surfaced by tools like dashboards and monitoring software"* `[source: k8s-docs-determine-reason-pod-failure-2026-08-31]`; written to `/dev/termination-log` — ⚠ **new to the book; no ledger row; appears nowhere in Ch 13** | Chapter 16 §2 |
| **Distroless image** | *"distroless images enable you to deploy minimal container images that reduce attack surface and exposure to bugs and vulnerabilities. Since distroless images do not include a shell or any debugging utilities, it's difficult to troubleshoot distroless images using `kubectl exec` alone"* `[source: k8s-docs-ephemeral-containers-concept-2026-08-31]` — ⚠ **B7 `:512` requires a Ch 2 first appearance that never shipped.** See ⚑ C6 | Chapter 16 §3 |
| **`persistentVolumeClaimRetentionPolicy`** (`whenDeleted` · `whenScaled`) | Two settings, each taking `Delete` or `Retain`; *"The default for policies is Retain"* `[source: k8s-docs-statefulset-storage-2026-08-25]` — ⚠ **field names appear in no shipped chapter but are graded at Bearings 3 Q2.** See ⚑ C11 | Chapter 16 §6 |
| **Silently dropped manifest field** | *"Often a section of the pod description is nested incorrectly, or a key name is typed incorrectly, and so the key is ignored"* `[source: k8s-docs-debug-pods-2026-08-23]` — ⚠ **introduced at revision; no ledger row; the concept `exec` provably cannot reach** | Chapter 16 §3 |
| **`ready` / `serving` (EndpointSlice conditions)** | *"The `serving` condition indicates that the endpoint is currently serving responses, and so it should be used as a target for Service traffic"*; for Pod-backed endpoints *"this maps to the Pod's `Ready` condition"* `[source: k8s-docs-endpointslices-2026-08-24]` — ⚑ **CONTRADICTS shipped Ch 9. See ⚑ C4. Do not enter this row until stage 6 rules.** | Chapter 16 §4 (Ch 9 §4 under repair) |
| **Telepresence** | *"a tool to ease the process of developing and debugging services locally while proxying the service to a remote Kubernetes cluster"*, which *"allows you to use custom tools, such as a debugger and IDE, for a local service and provides the service full access to ConfigMap, secrets, and the services running on the remote cluster"* `[source: k8s-docs-local-debugging-telepresence-2026-08-31]` — ⚠ named once; no ledger row | Chapter 16 §7 |
| **Debug profile** | A preset for how much privilege the debug container requests. Names *include* `general`, `baseline`, `restricted`, `netadmin`, `sysadmin`, default `general` `[source: k8s-docs-kubectl-debug-reference-2026-08-31]` — ⚠ **two cached pages conflict on the set; the chapter deliberately grades nothing on it.** See ⚑ C10 | Chapter 16 §3 |
| **The four triage questions** | Is it running · is it healthy and configured as you think · is it reachable · which replica — ⚠ **authored frame** (`research-manifest.md` Gaps item 6), correctly presented as the book's own | Chapter 16 §1 |
| **`kind` · `minikube` · `k3s`** | Named as local-cluster options in §7's 🔭 Closer Look — ⚠ **not in any cached snapshot**; carried because Ch 8 §5 already names all three. Low severity | Chapter 16 §7 (Ch 8 §5) |

### Tier 2 — the 11 ledger rows plus 4 unassigned terms, harvested per skill Part 16

The four triage questions · init-container debugging · init-container ordering deadlock · init-container idempotency · config errors visible at init · `kubectl logs -c` · `kubectl exec` · the `--` argument boundary · distroless image · ephemeral container · `ephemeralcontainers` API handler · `kubectl debug` · debug profile · `--copy-to` · `--target` · `--replace` · `kubectl debug node/` · selector/label mismatch · no ready endpoints · `port` vs `targetPort` · `kubernetes.io/service-name` label · `kubectl get endpointslices` · `kubectl describe service` · `kubectl port-forward` · `pods/portforward` subresource · StatefulSet ordinal triage · per-replica PVC survival · headless-Service peer DNS · DNS negative caching · local development loop · in-cluster-only reproduction.

**Four terms Chapter 16 introduces that the ledger does not assign:** termination message · silently dropped manifest field · `persistentVolumeClaimRetentionPolicy` · Telepresence.

---

## Concept shards at `C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/{slug}.md`

**Twenty-one created.** Slugs follow the outline's `kb_tags.concepts` list **except the two corrected under ⚑ C5**, and consolidate where the discrimination is the content, per the `oomkilled-vs-evicted.md` / `tag-vs-digest.md` precedent.

| Slug | § | Note |
|---|---|---|
| `four-triage-questions.md` | §1 | **absorbs `application-scope-triage`** — the chapter's spine; the deliberate doubling of "is it configured" |
| `init-container-debugging.md` | §2 | `Init:N/M` vocabulary; why plain `logs` returns misleading silence |
| `init-container-ordering-deadlock.md` | §2 | ⚑ authored synthesis, correctly reframed at revision as a consequence of three sourced facts |
| `init-container-idempotency.md` | §2 | the one §2 failure mode that **is** sourced; "ensure X exists," not "create X" |
| `config-errors-visible-at-init.md` | §2 | ⚑ **weakest sourcing in the chapter** — see the shard's own flag |
| `termination-message.md` | §2 | new to the book; `/dev/termination-log`; summary-not-substitute |
| `kubectl-exec.md` | §3 | the `--` boundary; what the *process* read vs. what the manifest says |
| `silently-dropped-manifest-field.md` | §3 | ⚑ **new at revision**; the half of "is it configured" `exec` cannot reach |
| `distroless-image-debugging.md` | §3 | hardening win, debugging cost; ⚑ carries the C6 ledger gap |
| `ephemeral-containers.md` | §3 | ★ the immutability Fixed Point; the five constraints as one design intent |
| `kubectl-debug-three-shapes.md` | §3 | **absorbs `debug-copy-to` and `debug-node`** — the three are only distinguishable by question |
| `debug-profiles.md` | §3 | ⚑ carries the C10 source conflict and the deprecation reading |
| `service-selector-mismatch.md` | §4 | break 1; two files, two sides |
| `no-ready-endpoints-two-signatures.md` | §4 | ⚑ **renamed per C5.** ★ empty slice vs. `ready:false` — the trace *is* the diagnosis |
| `readiness-as-endpoint-condition.md` | §4 | ⚑ **renamed per C5. BLOCKED on stage 6 — see C4** |
| `port-versus-targetport.md` | §4 | break 3; downstream of readiness, which is what makes it distinguishable |
| `service-dns-name-shape.md` | §4 | break 4; short names resolve in the *client's* namespace |
| `port-forward-as-diagnostic.md` | §5 | **absorbs `service-path-versus-api-path`** — ★ elimination, not a clean bill of health |
| `statefulset-ordinal-triage.md` | §6 | **absorbs `statefulset-application-debugging`** — "which replica" comes first |
| `per-replica-pvc-debugging.md` | §6 | ⚠ the surviving-PVC signature that impersonates a platform fault |
| `headless-service-peer-dns.md` | §6 | **absorbs `headless-service-dns-names`**; negative caching; you create the Service |
| `in-cluster-only-reproduction.md` | §7 | **absorbs `local-development-loop`** — the five-item dividing line, flagged as authored |
| `the-boundary-is-the-method.md` | §8 | **the Zenith.** Own file, per `package-not-template.md` / `control-loop-pointed-at-a-repository.md` |

*That is 23 kb_tags concepts mapped onto 21 files, with four consolidations and two renames.*

**Sixteen amended by append.**

- `platform-scope-vs-application-scope.md` (ch-13) — ⚑⚑ **the most important append in this chapter.** The far side of the handoff, plus §1's addition: the boundary is also a statement about *what you can see*
- `triage-order.md` (ch-13) — the application-side ordering, and why it is the same move at a different altitude
- `read-the-phase-first.md` (ch-13) — ⚑ where the rule runs out; the phase has nothing left to say
- `endpointslice.md` (ch-09) — ⚑⚑ **DO NOT APPEND. Rewrite under the C4 ruling or leave untouched.** Appending Ch 16's model beneath Ch 9's Fixed Point produces a shard that contradicts itself in two paragraphs
- `probe.md` (ch-05) — readiness disqualifies an endpoint; liveness restarts a container; zero restarts rules liveness out
- `init-container.md` (ch-05) — the re-run guarantee, now carrying its diagnostic consequence
- `pod-lifetime.md` (ch-05) — ⚑ **carries the C4 provenance note**: this shard's Pod-lifecycle source is where Ch 9's error entered
- `service.md` (ch-09) — the four break points as a path, not a list
- `label-selector.md` (ch-04) — selector and Pod-template labels drift because they live in two files
- `service-dns-records.md` (ch-09) — the client-namespace search-list consequence
- `headless-and-selectorless-services.md` (ch-09) — you create it; a missing one leaves healthy Pods that cannot find each other
- `statefulset-storage.md` (ch-11) — ⚑ the retention-policy **field names**, which Ch 11 taught behaviorally without naming. See C11
- `pod-security-standards-and-admission.md` (ch-12) — ⚑ **C3's closure**: the standards name `ephemeralContainers[*]`
- `container-image.md` (ch-02) — an image contains what was put in it; distroless is that fact weaponized
- `api-access-gates.md` (ch-08) — RBAC passes, admission refuses; two gates, two failures
- `absent-component-pattern.md` (ch-03/10/11) — the headless Service nobody created

Not shard-worthy, adequately carried by the glossary: `--replace` · `--share-processes` · `kubectl describe service` · `kubernetes.io/service-name` · Telepresence · kind/minikube/k3s · `Unknown`/`Terminating` controller stall.

⚑ **Infrastructure gap, new.** There is **no `statefulset.md` shard** anywhere in the tree. `ch-06/kb-manifest.md` is a lean 589-line early run that wrote only `custom-resource.md` and `operator-pattern.md`; ordinal identity from Ch 6 §6 was never sharded. §6's two shards therefore have no parent to append to and carry the retrieval inline. **Create `statefulset.md` from shipped Ch 6 §6 at the replay**, before Ch 17 reads the index and concludes the workload set is covered.

---

## Infrastructure flags — the knowledge base itself

**⚑ I0 — CRITICAL, new. See ⚑ C0.** Eleven `sources/*.md` files truncated on disk with frontmatter asserting completeness. Recovery text is free, in `ch-16/research-manifest.md`. **Check chapters 08–15 for the same fault** before trusting any prior fact audit that ran against a 2026-08-31 capture.

**⚑ I1 — HIGH, unchanged and now sixteen chapters expensive.** Chapters 03, 10 and 11 emit full **WRITE** blocks for `glossary.md`, `objective-coverage.md` and `retrieval-log.md`; `absent-component-pattern.md` is written as a full file three separate times. Replaying `ch-01` → `ch-16` in order discards everything written before each of those points. Chapter 16 adds only APPENDs to shared registers. **Convert those WRITE blocks to APPENDs before any replay.**

**⚑ I2 — MEDIUM, unchanged.** `concepts/pluggable-interface-pattern.md` (ch-02) and `concepts/pluggable-interfaces.md` (ch-11) are one concept under two slugs. Chapter 16 touches neither. **Merge at the replay, leaving a stub**, before Ch 17 §4 reads one file and concludes it has the set.

**⚑ I3 — LOW, unchanged and now blocking a fourth thing.** `.pipeline-state/book-outline/retrieval-architecture.md` is **still 19 lines** of permissions-failure message plus the stage's own summary — verified again this run. Every B3 figure cited below is recovered from that summary. **Re-run before Ch 19**, which is built by exactly the audit B3 was supposed to specify.

**⚑ I4 — MEDIUM, new.** `ch-16/outline.md:244` and `domain-analysis.md:39` still carry the retired-blueprint "doubled from 8% to 16%" claim that three consecutive manifests have now ruled must not ship. The revision caught it in the prose; the **upstream artifacts are unrepaired** and will re-inject it. See ⚑ C9.

**⚑ I5 — LOW, new.** `sources/k8s-docs-endpointslices-2026-08-24.md` frontmatter tags itself `concepts_covered: [… "readiness-gated-membership" …]`, which its own body contradicts. That mis-tag is a plausible contributor to ⚑ C4 and will mislead any concept-index build that reads frontmatter rather than body. Retag to `readiness-as-endpoint-condition`.

**⚑ I6 — LOW, new.** `ch-16/outline.md` declares `kb_tags.commands` with eight entries including `kubectl-get-endpointslices` and `kubectl-describe-service`. The draft demonstrates both, plus `kubectl delete pod` (cleanup, twice) and `nslookup` inside a container. *Add `kubectl-delete-pod`; leave `nslookup` out — it is a container-image utility, not a kubectl verb.*

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1 the author promotes to LOCKED.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Chapter opening as a received handoff** | "Three chapters ago, the platform finished its work and handed you back your own problem. That is where this chapter starts. Not with an introduction — with the far side of a handoff you were given in Chapter 13 and have been carrying ever since. … Every instrument you have trusted for two hundred pages reads fair, and the system is broken anyway. **So what do you actually look at?**" | **Strong candidate.** The catalog has no opening that begins mid-arc rather than at a topic. It refuses the introductory move on purpose and earns it, and the four-word question does the work three paragraphs of framing usually do. |
| **Zenith / synthesis** | "These were never two chapters about two subjects. **The boundary is the method.** … Chapter 13 taught you to read the phase first, and the phase's last and most valuable answer, the one it works toward, is *'this is no longer mine.'* … **Same move. Different altitude.**" | **Strong candidate.** Reveals that the *structure* was the argument, which is a distinct move from Ch 15's substitution Zenith and Ch 14's altitude Zenith. Three synthesis techniques, three chapters, no repetition — the catalog should hold all three. |
| **Naming a tool as out of place, and keeping it** | "It is genuinely useful and it is, unmistakably, the moment you step back across the boundary §1 drew. … **Which makes it an argument for the boundary rather than an exception to it.** The tool exists, it is on the same documentation page as the others, and the reason it feels out of place here is that it *is* out of place here. **Notice the feeling. It is the boundary doing its job.**" | **Strong candidate.** Turns an inconvenient fact into the section's proof instead of hiding it. "Notice the feeling" recruits the reader's own discomfort as evidence — a move the book has not used before. |
| **Refusing a comfortable conclusion** | "The instinct at this moment is relief — *the app is fine.* And that instinct, left alone, is where the diagnosis stops being useful, because 'the app is fine' is not a conclusion. **It is half of one.**" → and the ★: "It means the application is fine ***and the Service path is not.*** It is a narrowing step, not a clean bill of health." | **Strong candidate.** Names the reader's actual felt response, validates it, then shows exactly where it fails. Loss-aversion framing without fear-mongering, which is the ethical line skill Part 14 draws. |
| **Defending the platform team inside a chapter about their cluster** | "None of which makes the platform team an adversary. 'Their cluster' in this chapter's title is a statement of scope, not of blame. They own the machinery; you own the workload; the boundary is where those two responsibilities meet, and **the entire value of being able to place a fault on the correct side is that neither of you spends an afternoon on the other's half.**" | **Strong candidate.** Subject-dignity guardrail applied to an *organizational* relationship rather than to harmed third parties — a case the guardrail's examples do not cover. Pre-empts an us-vs-them reading the title invites. |
| **Closing on ownership rather than answers** | "What is different here is that the narrowing crosses an ownership boundary, which means the last step is not 'I found it' but 'I know whose it is.' On somebody else's cluster, those are equally valuable outcomes, and **knowing which one you have reached, and being able to show your work for it, is what makes you good to work with.**" | **Moderate to strong.** Identity framing (skill Part 3) aimed at collegiality rather than expertise — rare, and it lands the chapter's professional argument without a competence claim. Held at moderate only because it sits inside the Zenith already nominated above. |
| **A question that teaches by comparing two of its own sections** | Practice Q17 — "Which is the harder diagnosis, and why?" with the key: "Same class of bug, two entirely different signatures, which is exactly why this chapter answers 'is it configured' in two separate places. … **If both produced the same signature, §2 and §3 would be one section.**" | **Moderate.** A graded item whose answer explains the chapter's own architecture. Desirable-difficulty done structurally rather than by making the stem harder. New construction for the book. |

---

## Objective coverage log

Appended to `objective-coverage.md`. Audited against `domain-analysis.md:39`, `:298–300`, and the B1 trap table at `:578–580` and `:600`.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| **D3.2 — Debugging** | **Chapter 16** | **deep — the whole competency** | 2026-08-31 |
| **D2.3 — Troubleshooting (application-scope half)** | Chapter 13 (platform half) | **deep — Chapter 16 covers the far side** | 2026-08-31 |

**D3.2 coverage: 5 of 5 concept rows.** `domain-analysis.md:300` enumerates the competency as *"Troubleshooting Applications, determining Pod failure reasons, init-container and running-Pod debugging, `kubectl debug`, and developing/debugging services locally."* All five land in Chapter 16 at depth — §1, §2, §2–§3, §3, §7 respectively. **No D3.2 row is deferred.**

**Trap coverage: 3 of 3, all addressed, all graded.**

| # | Trap | Where addressed |
|---|---|---|
| 70 | Jumping to `kubectl logs` for a Pod stuck in `Pending` | §2's 🪝 Snag; Bearings 1 Q2 (A is the keyed distractor); Practice Q3; Practice Q17 option D |
| 71 | Treating "debugging the application" and "debugging the cluster" as one activity | §1's opening quotation; §8's Zenith; Practice Q1, Q2, Q16 |
| 87 | Treating D3.2 Debugging as identical to D2.3 Troubleshooting | Common Traps final row, verbatim on the split-is-scope-not-tooling reading |

⚠ **Trap 87's Common Traps row writes "D3 Debugging" and "D2 Troubleshooting"** where the trap and the objective index use `D3.2` / `D2.3`. Harmless to a reader, but it is the string a mechanical audit greps. Align to the sub-competency form.

**Research gaps CLOSED by Chapter 16:**

| Gap | Status |
|---|---|
| **G1 — `kubectl` command surface** (*"the entire book depends on … `exec` / `port-forward` / `debug`, and no cached source documents them"*) | **Closed for this chapter's verbs.** Nine snapshots now document `exec`, `debug` and its three shapes, `port-forward`, `logs -c`, `get endpointslices`. ⚠ Eleven of them are truncated on disk — see ⚑ C0. |
| **G2 — Pod failure signatures by name** | **Closed for the init family.** `Init:N/M`, `Init:Error`, `Init:CrashLoopBackOff` now sourced; the crash/OOM/pull family was Ch 13's. |
| **Gaps item 3 — §2's ordering and idempotency hazards** | **Half closed.** Idempotency is sourced to `k8s-docs-init-containers-2026-08-24` as the manifest instructed. The ordering deadlock is authored synthesis, correctly reframed at revision. Config-at-init remains the least-sourced — see below. |
| **Gaps item 4 — "two causes" is authored** | **Closed better than asked.** Each cause is tagged to its own snapshot and the *count* is untagged, exactly as instructed — and the revision went further, distinguishing the two by their on-screen trace. |
| **PSA reaching ephemeral containers** (draft-flagged, "cache before print") | **Already closed. See ⚑ C3.** Three PSA snapshots on disk; `pod-security-standards-profiles` names `ephemeralContainers[*]` under `runAsNonRoot`. |
| **`--target` behavior** (draft-flagged, "documented on no cached page") | **Already closed. See ⚑ C1.** Verbatim in A4's Flags table. |
| **`describe pod` init detail** (revision-cut as unsourced) | **Already closed. See ⚑ C2.** Verbatim in A5. |

**Still open and touching Chapter 16:**

- **`config-errors-visible-at-init`** — `k8s-docs-determine-reason-pod-failure-2026-08-31` carries the concept in its frontmatter tags but its body is termination-message material. **This reaches graded text at Practice Q17.** Either source it or mark it as practitioner analysis. The chapter's weakest sourcing.
- **`kubectl cp`'s in-image tooling dependency** — no snapshot. Practice Q6 option D's rationale is sound as re-led; the specific claim needs `kubectl_cp/`.
- **`--copy-to` label inheritance** — no snapshot; correctly cut rather than hedged.
- **The retired KCNA blueprint** — ⚠ **STILL OPEN, STILL MUST NOT BE DRAFTED.** Fourth chapter running. The prose is clean; `ch-16/outline.md:244` and `domain-analysis.md:39` are not. See ⚑ C9 / ⚑ I4.
- **`debug-statefulset` is a stub** — the research manifest's own "one significant gap." §6 is built from Ch 6 / Ch 11 / Ch 9 snapshots as instructed, and the draft flags this itself. **Not closable**; no other official page exists.

---

## Retrieval-practice ledger

Appended to `retrieval-log.md`.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| An image contains exactly what was put into it; no ambient OS underneath | ch 2 §2 | ch 16 — Bearings 1 Q6 *(`[retrieval: ch2]`)* |
| `targetPort` is the port the container listens on; `port` is the Service's | ch 9 §3 | ch 16 — Bearings 2 Q2 *(`[retrieval: ch9]`)* |
| Liveness and readiness are independent; a zero restart count rules liveness out | ch 5 §7 | ch 16 — Bearings 2 Q4 *(`[retrieval: ch5]`)* |
| A StatefulSet's PVCs are retained by default | ch 11 §6 | ch 16 — Bearings 3 Q2 *(`[retrieval: ch11]`)* — ⚑ **FAILS, see C11** |
| A short Service name resolves in the client's own namespace | ch 9 §7 | ch 16 — Practice Q12 *(`[retrieval: ch9]`)* |
| `port` / `targetPort`, applied to a port-number mismatch | ch 9 §3 | ch 16 — Practice Q13 *(`[retrieval: ch9]`)* |
| The per-replica PVC follows ordinal identity across deletion | ch 11 §6 | ch 16 — Practice Q14 *(`[retrieval: ch11]`)* |
| The init sequence: ordered, blocking, each to completion | ch 5 §3 | ch 16 — Soundings Q2 (excluded from budget per B3) |
| Readiness disqualifies an endpoint rather than deleting it | ch 9 §4 | ch 16 — Soundings Q3 (excluded per B3) — ⚑ **contested, see C4** |
| StatefulSet identity survives rescheduling | ch 6 §6 | ch 16 — Soundings Q6 (excluded per B3) |
| A deleted StatefulSet Pod's PVC survives | ch 11 §6 | ch 16 — Soundings Q7 (excluded per B3) |

### Compliance

| Check | B3 target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of **Bearings** | 25% (Ch 16 at the ceiling) | 4 of 16 = **25.0%** | ✅ exactly |
| Retrieval share of the **Practice pool** | same target | **3 of 17 = 17.6%** | ✅ **first non-zero in four chapters** |
| Retrieval share of **all graded items** | 25% | 7 of 33 = **21.2%** | ✅ under ceiling, non-trivial |
| Spacing floor (≥4 chapters back) | ≥1 item | ch 2 is **fourteen** back | ✅ comfortably |
| Retrieval **accuracy** | all items answerable from the shipped source chapter | **6 of 7** | ❌ — ⚑ C11 |
| Question inventory vs B4 | 8 · 10 · 15 · 33 | 8 · **16** · **17** · **41** | ⚑ C7 |
| Tag surface form | one form | `[retrieval: chN]` only, zero cross-domain | ✅ — ⚑ C8 |

**Five mandatory B3 anchors, all discharged.** Ch 13 §1/§8 → §1 (the opening move, and the Soundings 0–2 branch names it by section). Ch 5 §3 → §2. Ch 5 §5/§7 → §1, §4. Ch 9 §3/§4/§7 → §4. Ch 6 §6 + Ch 11 §6 → §6. The outline warned that *"Ch 13 §1 is not optional"* and that a reader who has lost the scope test *"cannot receive §1"* — the chapter honours that in three places: the epigraph's framing, the Soundings 0–2 branch, and Bearings 1's 0–2 rubric, each routing back to **Chapter 13 §1 specifically rather than to Chapter 13**.

### Obligations Chapter 16 discharged — verified by line number against shipped text

| Promise | Shipped at | Discharged by |
|---|---|---|
| *"when the Pod is fine and the application isn't"* | `chapter-13:388`, `:1828` | §1, in the ledger's exact words |
| *"you will not find `kubectl exec`, `kubectl debug`, or `kubectl port-forward` taught here… they belong to the other chapter"* | `chapter-13:390` | §3 and §5 |
| *"Ch 16 §3 — getting inside a container"* | `chapter-13:390` | ⚑ §3, under a **different title** — see below |
| *"Ch 16 §2 — debugging init containers"* | `chapter-13:566` | §2 |
| *"From the application side, 'is anything even selected' is…"* | `chapter-13:972` | §4, title matched exactly |
| *"a debug container is a container… can be refused by admission"* | `chapter-12:1342` | §3's ⚠ Navigational Hazard — ⚑ **and now sourceable, see C3** |
| the D2.3 frontmatter instruction | `chapter-13:392` | `kb_tags.objectives: ["D3.2", "D2.3"]` — ⚑ **see the frontmatter note below** |

⚑ **Two published pointers name §3 differently.** `chapter-13:390` says *"Ch 16 §3 — getting inside a container"*; `chapter-12:1342` says *"Ch 16 §3 — getting inside, and adding what isn't there."* The section shipped under the second. **The draft handles this well** — §3 tells a reader arriving on either pointer that both phrasings name the same section — but that is a repair, not a fix. Either amend `chapter-13:390` to the shipped title in the same commit as the C4 Ch 9 edits, or accept the in-prose reconciliation permanently. It costs one string.

### Forward obligations Chapter 16 creates

| Topic Ch 16 owns | Must be retrieved in | How |
|---|---|---|
| The four pluggable interfaces, collected | **Ch 17 §4** | Ch 16 adds nothing; recorded so §4's collection stage knows this chapter is not a source |
| The control loop's fifth altitude | **Ch 17 §4** | ⚠ **Ch 16 asserts no running ordinal**, honouring `term-ownership.md:754`. Verified: no "third time"/"fourth time" construction anywhere in the draft |
| Service mesh as what canary needs | **Ch 17 §5** | §4's break-3 discussion touches traffic delivery without naming a mesh — correctly, the dependency is Ch 15 §2's |
| Observability as the thing that tells you first | **Ch 18** | The Voyage Ahead states it explicitly: *"You have spent this chapter finding out what went wrong* after *someone told you… Chapter 18 is about the systems that tell you first"* |
| The Ch 1 "cloud native" plant | **Ch 17 §1** | Correctly untouched |

### Frontmatter — the one open question this stage cannot close alone

The integration report asks whether `D2.3` must appear alongside `D3.2` in the materialized frontmatter. **It must**, and the instruction is explicit in shipped text rather than inferred:

> `chapter-13:392` — *"Unless Ch 16's frontmatter carries `objectives: ["D3.2", "D2.3"]`, the book's objective index will show a substantial slice of D2.3 with no owning chapter."*

`ch-16/outline.md:179` already carries both. `exam_domain` stays single-valued at D3.2 per the outline's note at `:40–45`, because that is the domain whose **weight** the chapter draws against and the one-domain string form is what ch-04/-09/-10/-11/-12/-13 shipped.

**What still needs a ruling: which stage materializes the block.** `ch-13/draft-v2.md` also carries no frontmatter and shipped `chapter-13` has one, so the pipeline does inject it somewhere after this stage — the revision was right to leave it rather than risk two YAML blocks. Whoever owns that injection must carry both objective IDs **and** the two `kb_tags.concepts` additions this revision introduced (`termination-message`, `silently-dropped-manifest-field`), **plus the two C5 renames** if stage 6 rules for Ch 16.

### Not flagged — checked and clean, recorded so a later stage does not re-open them

All **19 distinct `[source:]` tags** in the draft resolve to files that exist in `sources/` — enumerated and verified individually this run. (Their *contents* are a separate matter; see ⚑ C0.) The chapter's five highest-risk quotations were checked verbatim against complete snapshots: the ephemeral-container immutability sentence, the four API-level constraints, the "all the Pods that match the Service selector" line, the `serving`-maps-to-`Ready` line, and the StatefulSet PVC-retention defaults. The init-container re-run guarantee and the `restartPolicy: Never` exception are both exact. Margin-icon density (16) sits inside the shipped 5–17 range, matching Ch 11. Ordinal-count convention, heading form (`## <difficulty> §N — Title`), the `☀️`-in-place-of-difficulty closing marker, "The Voyage Ahead", and the eight-question Soundings with its three-branch rubric all conform to B6 and the structural contract. Figure anchors carry no duplicate or missing numbers. The `ch16-zenith-mine-or-the-platforms` anchor deviates from the `ch{NN}-fig{MM}` pattern but **matches shipped `ch14-zenith-package-not-template` and `ch15-zenith-…`** — that is a settled book convention, not a Chapter 16 defect, and the draft's AUTHOR-REVIEW proposing a rename should be resolved as "no change."

---

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

---

# Chapter 16 additions

> ⚠ **MERGE REQUIRED BEFORE PROMOTION.** A further A–Z sequence appended after the
> Chapter 15 block, for the reason recorded there: merging in place would require
> re-transcribing verbatim documentation definitions, and Rule 5 treats definitional
> drift as worse than a duplicated alphabet. Interleave mechanically before promoting
> this file to the shipped back-of-book glossary. No entry below duplicates an entry above.
>
> ⚑ **ONE ENTRY IS BLOCKED.** `ready` / `serving` (EndpointSlice conditions) contradicts
> shipped Chapter 9 and must not be entered until stage 6 rules. See manifest ⚑ C4.

---

## C

**Config error visible at init** — A configuration fault that surfaces as an init container
exiting non-zero with the reason printed in its log: a ConfigMap key that does not exist, a
Secret decoded into the wrong shape, a mount path colliding with something in the image.
(Chapter 16 §2)

> ★ **The good news case.** The *same* config error that gets past init — because the value is
> present but wrong — produces no error, no failed probe, and no status string. See
> [[silently-dropped-manifest-field]] and the "is it configured" doubling in
> [[four-triage-questions]].
>
> ⚠ **WEAKEST SOURCING IN THE CHAPTER, and it reaches graded text at Practice Q17.**
> `k8s-docs-determine-reason-pod-failure-2026-08-31` carries `config-errors-visible-at-init`
> in its `concepts_covered` frontmatter, but its transcribed body is termination-message
> material. Either source it properly or mark it as practitioner analysis before print.

---

## D

**Debug profile** — A preset for how much privilege a `kubectl debug` container requests.
Profile names *include* `general`, `baseline`, `restricted`, `netadmin` and `sysadmin`, with
`general` the default. `[source: k8s-docs-kubectl-debug-reference-2026-08-31]` (Chapter 16 §3)

> ⚠ **TWO CACHED PAGES CONFLICT ON THE SET.** The generated CLI reference (produced from the
> kubectl binary) lists **five** with `general` default. The task page
> (`k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31`) lists **six**, including `legacy`,
> and names `legacy` the default — while also noting `legacy` is *"planned to be deprecated in
> the near future."* The two are best read as different points in a deprecation, not as a
> contradiction. The generated reference is authoritative on the current set.
>
> ★ **The chapter teaches the shape, not the list, and grades nothing on the names.** That is
> deliberate and correct: asking for more privilege than the namespace enforces is what
> triggers the admission refusal. See [[ephemeral-containers]] and manifest ⚑ C10.

**Distroless image** — A minimal container image containing the application binary and its
libraries and nothing else — no shell, no package manager, no debugging utilities.
*"distroless images enable you to deploy minimal container images that reduce attack surface
and exposure to bugs and vulnerabilities. Since distroless images do not include a shell or any
debugging utilities, it's difficult to troubleshoot distroless images using `kubectl exec`
alone."* `[source: k8s-docs-ephemeral-containers-concept-2026-08-31]` (Chapter 16 §3)

> ★ **Not a mistake — a deliberate hardening choice with a known debugging cost.** This is the
> whole reason ephemeral containers exist as a mechanism. See [[distroless-image-debugging]].
>
> ⚠ **LEDGER OBLIGATION UNDISCHARGED.** `term-ownership.md:512` assigns the term to Ch 16 §3
> and requires a first appearance in **Ch 2** ("name only, always with a pointer"). Grep across
> all fifteen shipped chapters returns **zero** occurrences of "distroless." Ch 16 §3 is both
> definer and first appearance. Retrofit Ch 2 or amend the row. See manifest ⚑ C6.
>
> ⚑ The draft's own AUTHOR-REVIEW claiming this term has no ledger owner is **wrong** — delete
> it rather than acting on it.

---

## E

**Ephemeral container** — A container run temporarily inside an existing Pod to inspect its
state, created *"using a special `ephemeralcontainers` handler in the API rather than by adding
them directly to `pod.spec`, so it's not possible to add an ephemeral container using
`kubectl edit`."* `[source: k8s-docs-ephemeral-containers-concept-2026-08-31]` (Chapter 16 §3)

> ★ **FIXED POINT — the reason the mechanism exists at all:** *"Since Pods are intended to be
> disposable and replaceable, you cannot add a container to a Pod once it has been created."*
> `[source: k8s-docs-ephemeral-containers-concept-2026-08-31]` A Pod's container list is fixed
> at creation, so a temporary container had to be added outside the normal spec-editing path.
>
> **Four documented constraints, all verbatim from the same snapshot:**
> - *"Ephemeral containers may not have ports, so fields such as `ports`, `livenessProbe`,
>   `readinessProbe` are disallowed."*
> - *"Pod resource allocations are immutable, so setting `resources` is disallowed."*
> - *"Like regular containers, you may not change or remove an ephemeral container after you
>   have added it to a Pod."*
> - *"they will never be automatically restarted, so they are not appropriate for building
>   applications."*
> - *"Note: Ephemeral containers are not supported by static pods."*
>
> ★ **Read the five together and the design intent is one thing: this is an instrument, not a
> workload.** No guarantees because it is not part of your application; not removable because
> the container list, even its ephemeral part, is append-only.
>
> ⚠ **Subject to Pod Security Admission like any other container.** The Pod Security Standards
> name the ephemeral variant explicitly — under Restricted, *"Running as Non-root … Fields:
> `spec.securityContext.runAsNonRoot` and the container/init/ephemeral variants. Allowed:
> `true`."* `[source: k8s-docs-pod-security-standards-profiles-2026-08-31]` A root-running debug
> image in a `restricted` namespace is refused at admission, not at RBAC.
> *(Cite that snapshot for the fact that the standards reach ephemeral containers; its field
> enumeration is condensed — do not quote it as a complete field list.)*

---

## I

**`Init:N/M` (Pod status family)** — The status vocabulary for a Pod that has not finished its
init sequence. `[source: k8s-docs-debug-init-containers-2026-08-31]` (Chapter 16 §2)

| Status | Meaning |
|---|---|
| `Init:N/M` | The Pod has M init containers, and N have completed so far |
| `Init:Error` | An init container has failed to execute |
| `Init:CrashLoopBackOff` | An init container has failed repeatedly |
| `Pending` | The Pod has not yet begun executing init containers |
| `PodInitializing` or `Running` | The Pod has already finished executing init containers |

> ★ **`Init:1/3` tells you the first succeeded and the second is where to look.** The Pod's
> *phase* is `Pending` throughout with `Initialized` false, which is why "read the phase first"
> does not finish the job here — every Pod in this state has the same phase, and the
> discriminating detail is in the status string.
>
> ⚠ **APPEARS IN NO SHIPPED CHAPTER** — Chapter 13 uses `PodInitializing` only — yet Chapter 16
> grades this vocabulary twice, at Bearings 1 Q2 and Practice Q3. **Highest-priority glossary
> entry in this chapter.**
>
> ⚑ `Init:CrashLoopBackOff` exists as a status because a failing init container is retried
> rather than abandoned: *"if a Pod's init container fails, the kubelet repeatedly restarts that
> init container until it succeeds. However, if the Pod has a `restartPolicy` of Never, and an
> init container fails during startup of that Pod, Kubernetes treats the overall Pod as failed."*
> `[source: k8s-docs-init-containers-2026-08-24]`

**Init-container idempotency** — The requirement that an init container tolerate being run more
than once, because *"if the Pod restarts, or is restarted, all init containers must execute
again."* `[source: k8s-docs-init-containers-2026-08-24]` (Chapter 16 §2)

> ★ **Not a nicety — a correctness requirement imposed by restart semantics.** If an init
> container's job is "create X," its actual job is "ensure X exists."
>
> **Signature:** a workload that deploys cleanly and refuses to come back after any disruption.
> The failure is invisible on a fresh deploy and deterministic on every restart after.

**Init-container ordering deadlock** — An init container blocking on a precondition that cannot
be satisfied until this Pod is ready: the init container waits for a Service endpoint, the app
container cannot start until the init container exits, the Pod cannot become ready until the
app container starts, and the Service cannot gain a ready endpoint until the Pod is ready.
(Chapter 16 §2)

> **Tell:** an `Init:0/1` Pod sitting for twenty minutes with no error, no restarts, and a calm
> log line like "waiting for dependency."
>
> ⚠ **AUTHORED SYNTHESIS, correctly framed.** `k8s-docs-debug-init-containers-2026-08-31`'s own
> `scope_note` states the page *"does NOT cover init-container ordering deadlocks."* The
> deduction is sound — it follows from three separately sourced facts (init containers block app
> start; a Pod is not Ready until init succeeds; readiness governs endpoint serving) — and the
> chapter presents it as a consequence of the sequencing rules rather than as documented
> behavior. Keep that framing.

---

## K

**`kubectl debug`** — The verb that attaches an ephemeral container to a running Pod, or builds
a modified copy of one, or opens a shell onto a node. (Chapter 16 §3)

> ★ **Three shapes, three different questions. They are not interchangeable.**
>
> | Shape | Asks |
> |---|---|
> | `kubectl debug -it <pod> --image=<tools> --target=<container>` | what does the running process see *right now*? |
> | `kubectl debug <pod> -it --image=<img> --copy-to=<name>` | what would happen if I *changed* something? |
> | `kubectl debug node/<node> -it --image=<img>` | is the *machine* the problem? — **platform scope** |
>
> `--target` — *"When using an ephemeral container, target processes in this container name"*
> `[source: k8s-docs-kubectl-debug-reference-2026-08-31]`. The supporting principle:
> *"When using ephemeral containers, it's helpful to enable process namespace sharing so you can
> view processes in other containers."* `[source: k8s-docs-ephemeral-containers-concept-2026-08-31]`
>
> ⚑ **`--target`'s own description was flagged in the draft as undocumented. It is documented** —
> in A4's Flags table, which is missing from the truncated on-disk snapshot. See manifest ⚑ C0/⚑ C1.

**`kubectl debug --copy-to`** — Creates a **copy** of the Pod with configuration changed for
debugging. *"you can't run `kubectl exec` to troubleshoot your container if your container image
does not include a shell or if your application crashes on startup. In these situations you can
use `kubectl debug` to create a copy of the Pod with configuration values changed to aid
debugging."* `[source: k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31]` (Chapter 16 §3)

> ★ **The original Pod is not touched, and that is the feature.** You experiment freely on a
> copy while the broken Pod keeps running, keeps serving, and stays in the state that produced
> the bug. Most readers arrive expecting a debugger to modify the running system; `--copy-to`
> inverts that, which is exactly what you want on a cluster you do not own.
>
> ⚠ **One documented exception:** `--replace` — *"When used with '--copy-to', delete the original
> Pod."* `[source: k8s-docs-kubectl-debug-reference-2026-08-31]` The Fixed Point holds for
> `--copy-to` alone. Do not restate it unconditionally.
>
> **Also:** `--share-processes` defaults to **true** with `--copy-to`. Passing it explicitly is
> clearer but not required. A copy is a real Pod and consumes resources — `kubectl delete pod`
> when finished.
>
> ⚑ **Label inheritance is undocumented in the corpus.** Draft-v1 hedged that a copy might
> receive live traffic; the revision cut it. Leave cut until a snapshot pins the behavior.

**`kubectl debug node/`** — Creates a Pod on a target node with host access.
*"If none of these approaches work, you can find the Node on which the Pod is running and create
a Pod running on the Node."* `[source: k8s-docs-kubectl-debug-copy-node-profiles-2026-08-31]`
(Chapter 16 §3)

> Documented behavior, verbatim: the Pod name is auto-generated from the node name; *"The root
> filesystem of the Node will be mounted at `/host`"*; *"The container runs in the host IPC,
> Network, and PID namespaces, although the pod isn't privileged, so reading some process
> information may fail, and `chroot /host` may fail"*; use `--profile=sysadmin` if a privileged
> pod is needed. Clean up with `kubectl delete pod`.
>
> ⚠ **PLATFORM SCOPE.** Reaching for this means either the fault has moved across the boundary —
> in which case hand it to whoever owns the platform, with the evidence — or you *are* that
> person. See [[platform-scope-vs-application-scope]] and Ch 13 §5.

**`kubectl exec`** — Runs a command inside an already-running container.
*"This page shows how to use `kubectl exec` to get a shell to a running container"*
`[source: k8s-docs-get-shell-running-container-2026-08-31]` (Chapter 16 §3; named at Ch 13 §8)

> ★ **The `--` matters:** *"The double dash (`--`) separates the arguments you want to pass to
> the command from the kubectl arguments."*
> `[source: k8s-docs-get-shell-running-container-2026-08-31]` Omit it and kubectl interprets
> your command's flags as its own. Name a container with `-c` in a multi-container Pod.
>
> ★ **What it is actually for:** not "does the ConfigMap say what I meant" — you can read that
> from outside — but **what the process got.** Environment variables shadow, mounts mask, code
> defaults win over empty strings, and a mount path one character off produces an empty
> directory. `ls -la` on the mount path catches more bugs than reading env and config combined.
>
> ⚠ **LEDGER DRIFT.** `term-ownership.md:511` requires a first appearance in **Ch 3**; grep
> returns zero occurrences there. Its actual first appearance is `chapter-13:390`, which gives
> exactly the name-only-with-pointer treatment the row asks for. **Amend the row to Ch 13**
> rather than retrofitting Ch 3. See manifest ⚑ C6.

**`kubectl port-forward`** — Opens a tunnel from a local port to a port on a Pod.
*"`kubectl port-forward` allows using resource name, such as a pod name, to select a matching
pod to port forward to."* `[source: k8s-docs-port-forward-2026-08-31]` (Chapter 16 §5; named at
Ch 3)

> ★ **An API-server operation, not a networking one.** *"To use `kubectl port-forward`, a user
> must have permission to access the target resource (for example, a Pod or Service) and the
> `portforward` subresource. Typical required permissions include `get` on `pods` and `create`
> on `pods/portforward`."* `[source: k8s-docs-port-forward-authorization-2026-08-31]`
>
> The security note is also the diagnostic one: *"Cluster administrators should carefully
> restrict these permissions, as port-forwarding can provide direct network access to workloads
> and may bypass network-level controls."* **If the path skipped nothing, the experiment would
> prove nothing.** See [[port-forward-as-diagnostic]].
>
> **TCP only:** *"`kubectl port-forward` is implemented for TCP ports only. The support for UDP
> protocol is tracked in issue 47862."* `[source: k8s-docs-port-forward-2026-08-31]`
> It terminates when the command stops.

---

## N

**No ready endpoints** — A Service that exists, is correctly written, and has nothing it is
willing to send traffic to. *"Make sure that the endpoints in the EndpointSlices match up with
the number of pods that you expect to be members of your service. If they don't, the Service's
selector probably does not match the Pods' labels, or the Pods are not Ready."*
`[source: k8s-docs-debug-pods-2026-08-23]` (Chapter 16 §4)

> ★ **Two causes, two files — and the slice tells you which.**
> **Zero endpoints in the slice** = nothing matched the selector; the labels live in the
> Deployment's Pod template.
> **Endpoints present but `ready: false`** = readiness is holding them back; that lives in the
> probe definition.
> Same outcome for your traffic, two different readings on the screen, and the difference *is*
> the diagnosis. `kubectl get pods -l <the-service-selector>` settles it in one command:
> nothing returned is a mismatch, Pods returned is a readiness problem.
>
> ⚠ **The count is authored.** `research-manifest.md` Gaps item 4: each cause is separately
> sourced but no page states "two." Tag each cause; do not tag the count.
>
> ⚑ **RENAMED from `empty-endpointslice-as-symptom`.** The old slug — and `term-ownership.md:517`
> — names only one of the two signatures, and the readiness case leaves the slice **populated**.
> See manifest ⚑ C5.

---

## P

**`persistentVolumeClaimRetentionPolicy`** — A StatefulSet field with two settings,
`whenDeleted` and `whenScaled`, each accepting `Delete` or `Retain`.
*"The default for policies is Retain, matching the StatefulSet behavior before this new
feature."* `[source: k8s-docs-statefulset-storage-2026-08-25]` (Chapter 16 §6)

> ★ **Retain, both — which is why deleting a replica does not clear its storage.**
> *"Retain (default): PVCs from the volumeClaimTemplate are not affected when their Pod is
> deleted."* And for the involuntary case: *"if a Pod associated with a StatefulSet fails due to
> node failure, and the control plane creates a replacement Pod, the StatefulSet retains the
> existing PVC. The existing volume is unaffected, and the cluster will attach it to the node
> where the new Pod is about to launch."* `[source: k8s-docs-statefulset-storage-2026-08-25]`
>
> ⚠ **A workload configured `whenScaled: Delete` behaves differently on scale-down.** Check the
> actual policy before reasoning about what a deletion did; the default is only the default.
>
> ⚠ **THE FIELD NAMES APPEAR IN NO SHIPPED CHAPTER.** Chapter 11 teaches the Retain default
> behaviorally (`:1235`, `:1412`) without naming the field, `whenDeleted`, or `whenScaled`.
> Chapter 16 grades the vocabulary at Bearings 3 Q2 under `[retrieval: ch11]`, which the
> retrieval audit correctly fails. See manifest ⚑ C11.

**`port` vs `targetPort`** — `port` is the port the Service itself is reachable on;
`targetPort` is the port on the Pod that traffic is delivered to, and the one that must match
what the container binds. (Chapter 16 §4; defined at Ch 9 §3)

> ★ **A mismatch produces a Service that selects perfectly and routes into nothing.** Endpoints
> ready, request failing — which is what distinguishes it from a selection problem. It sits
> **downstream of readiness** and therefore cannot mark an endpoint not ready.
>
> ⚠ **Sourcing note:** the term ledger assigns both fields to Ch 9 §3, so Chapter 16 glosses and
> points rather than defining, and the definitional source burden sits with Chapter 9.
> `k8s-docs-debug-service-2026-08-31` lists `port-versus-targetport` in `concepts_covered` but
> its on-disk body is truncated before the passage (manifest ⚑ C0). **Verify Ch 9 §3 carries a
> tag for the definition.** The pairing is graded three times in Chapter 16 — Bearings 2 Q2,
> Practice Q11, Practice Q13.

---

## S

**Silently dropped manifest field** — A field that never reached the API server because it was
misnested or misspelled. *"Often a section of the pod description is nested incorrectly, or a
key name is typed incorrectly, and so the key is ignored."*
`[source: k8s-docs-debug-pods-2026-08-23]` (Chapter 16 §3)

> ★ **The half of "is it configured" that `exec` provably cannot reach.** The apply succeeded.
> Nothing errored. The field is simply absent from what the server stored, and the container is
> faithfully running the spec that *exists* rather than the one you wrote.
>
> **The move is a round trip:** apply, then read back what the server kept and compare it
> against your file — `kubectl get pods/mypod -o yaml` against the original, as the docs
> prescribe. `[source: k8s-docs-debug-pods-2026-08-23]`
>
> ⚑ The same passage names a `--validate` flag whose behavior has moved across kubectl releases.
> **Only the version-stable round-trip comparison is taught.** Verify `--validate`'s current
> form against a fresh snapshot before adding it.

---

## T

**Telepresence** — *"a tool to ease the process of developing and debugging services locally
while proxying the service to a remote Kubernetes cluster,"* which *"allows you to use custom
tools, such as a debugger and IDE, for a local service and provides the service full access to
ConfigMap, secrets, and the services running on the remote cluster."*
`[source: k8s-docs-local-debugging-telepresence-2026-08-31]` (Chapter 16 §7)

> ★ **One instance of a pattern: your process, their cluster's dependencies.** The tooling in
> this space changes; the pattern does not. The Kubernetes docs happen to document this one.
>
> ⚠ **No ledger row.** Named once. The *pattern* is what the chapter teaches and what should be
> retained; the tool name is illustrative.

**Termination message** — A file at `/dev/termination-log` a container can write to, whose
contents Kubernetes surfaces in the Pod's status. *"Termination messages provide a way for
containers to write information about fatal events to a location where it can be easily
retrieved and surfaced by tools like dashboards and monitoring software."*
`[source: k8s-docs-determine-reason-pod-failure-2026-08-31]` (Chapter 16 §2)

> ★ **Useful when logs do not capture the failure well.** A one-line reason in the termination
> log makes an init-container failure legible from `kubectl describe` alone.
>
> 🔭 The same source notes that in most cases the information should **also** go to the general
> Kubernetes logs. The termination message is a summary surfaced in status, not a replacement
> for logging.
>
> ⚠ **New to the book; appears nowhere in Chapter 13; no ledger row.**

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

## Chapter 16 update (2026-08-31)

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D3.2 — Debugging | **Chapter 16** | **deep — the entire competency, 5 of 5 concept rows** | 2026-08-31 |
| D2.3 — Troubleshooting (application-scope half) | Chapter 13 (platform half) | **deep — Chapter 16 covers the far side of the boundary** | 2026-08-31 |

### Chapter 16 — D3.2 coverage detail

`domain-analysis.md:300` enumerates D3.2 as "Troubleshooting Applications, determining Pod
failure reasons, init-container and running-Pod debugging, kubectl debug, and
developing/debugging services locally." All five rows land in Chapter 16 at depth:
sec 1 / sec 2 / sec 2-3 / sec 3 / sec 7. NO D3.2 ROW IS DEFERRED.

### D2.3 note — the frontmatter requirement is shipped-text, not inference

chapter-13:392 states it directly: "Unless Ch 16's frontmatter carries
objectives: [D3.2, D2.3], the book's objective index will show a substantial slice of D2.3
with no owning chapter." ch-16/outline.md:179 carries both. exam_domain stays single-valued
at D3.2 (the domain whose WEIGHT this chapter draws against), per the outline's note at :40-45
and the one-domain string form shipped by ch-04/-09/-10/-11/-12/-13.

OPEN: which stage materializes the frontmatter block. ch-13/draft-v2.md also has none and
shipped chapter-13 does, so injection happens after stage 14. Whoever owns it must carry both
objective IDs, the two new kb_tags.concepts (termination-message,
silently-dropped-manifest-field), and the two renames under manifest C5 if stage 6 rules for
Chapter 16.

### Trap coverage — 3 of 3, all addressed, all graded

| # | Trap | Where addressed |
|---|---|---|
| 70 | Jumping to kubectl logs for a Pod stuck in Pending | sec 2 Snag; Bearings 1 Q2 (keyed distractor A); Practice Q3; Practice Q17 option D |
| 71 | Treating app-debugging and cluster-debugging as one activity | sec 1 opening quotation; sec 8 Zenith; Practice Q1, Q2, Q16 |
| 87 | Treating D3.2 Debugging as identical to D2.3 Troubleshooting | Common Traps final row |

WARN: the Common Traps row for trap 87 writes "D3 Debugging" / "D2 Troubleshooting" where the
objective index uses D3.2 / D2.3. Harmless to a reader; it is the string a mechanical audit
greps. Align to the sub-competency form.

### Research gaps CLOSED by Chapter 16

- G1 kubectl command surface. Closed for this chapter's verbs: exec, debug and its three
  shapes, port-forward, logs -c, get endpointslices, describe service. WARNING: eleven of the
  supporting snapshots are TRUNCATED ON DISK - see manifest C0.
- G2 Pod failure signatures. Closed for the init family (Init:N/M, Init:Error,
  Init:CrashLoopBackOff). The crash/OOM/pull family was Chapter 13's.
- Gaps item 3 (sec 2 hazards). Half closed. Idempotency sourced to
  k8s-docs-init-containers-2026-08-24 exactly as instructed. Ordering deadlock is authored
  synthesis, correctly reframed at revision as a consequence of sourced facts.
- Gaps item 4 ("two causes" is authored). Closed better than asked: each cause tagged to its
  own snapshot, the count untagged, and the revision additionally distinguished the two by
  their on-screen trace.
- PSA reaching ephemeral containers. ALREADY CLOSED - the draft's "cache before print" note
  is stale. k8s-docs-pod-security-standards-profiles-2026-08-31 names ephemeralContainers[*]
  under runAsNonRoot. See manifest C3.
- --target flag behavior. ALREADY CLOSED - verbatim in the A4 Flags table. See manifest C1.
- describe pod init detail (cut at revision as unsourced). ALREADY CLOSED - verbatim in A5.
  See manifest C2.

### Still open and touching Chapter 16

- config-errors-visible-at-init. WEAKEST SOURCING IN THE CHAPTER and it reaches graded text at
  Practice Q17. k8s-docs-determine-reason-pod-failure-2026-08-31 carries the concept in
  frontmatter but its body is termination-message material. Source it or mark it as
  practitioner analysis before print.
- kubectl cp's in-image tooling dependency. No snapshot. Practice Q6 option D's rationale is
  sound as re-led on the live-view distinction; the specific claim needs kubectl_cp/.
- --copy-to label inheritance. No snapshot; correctly cut rather than hedged.
- The retired KCNA blueprint. STILL OPEN, STILL MUST NOT BE DRAFTED - fourth chapter running.
  The Chapter 16 prose is clean (the revision cut it, reaching the same ruling as the Ch 14
  and Ch 15 manifests). But ch-16/outline.md:244 and domain-analysis.md:39 STILL CARRY IT and
  will re-inject it into any later stage that reads them. Fix at the source.
- debug-statefulset is a five-sentence stub. Not closable; no other official page exists.
  Section 6 is built from the Ch 6 / Ch 11 / Ch 9 snapshots as the research manifest
  instructed, and the draft flags this itself.

=== END APPEND ===
```

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

## Chapter 16 (2026-08-31)

| Tested topic | Original chapter | Retested in |
|---|---|---|
| An image contains exactly what was put into it; no ambient OS underneath | ch 2 sec 2 | ch 16 - Bearings 1 Q6 [retrieval: ch2] |
| targetPort is the port the container listens on; port is the Service's | ch 9 sec 3 | ch 16 - Bearings 2 Q2 [retrieval: ch9] |
| Liveness and readiness are independent; zero restarts rules liveness out | ch 5 sec 7 | ch 16 - Bearings 2 Q4 [retrieval: ch5] |
| A StatefulSet's PVCs are retained by default | ch 11 sec 6 | ch 16 - Bearings 3 Q2 [retrieval: ch11] - FAILS, see C11 |
| A short Service name resolves in the client's own namespace | ch 9 sec 7 | ch 16 - Practice Q12 [retrieval: ch9] |
| port/targetPort applied to a port-number mismatch | ch 9 sec 3 | ch 16 - Practice Q13 [retrieval: ch9] |
| The per-replica PVC follows ordinal identity across deletion | ch 11 sec 6 | ch 16 - Practice Q14 [retrieval: ch11] |
| The init sequence: ordered, blocking, each to completion | ch 5 sec 3 | ch 16 - Soundings Q2 (excluded per B3) |
| Readiness disqualifies an endpoint rather than deleting it | ch 9 sec 4 | ch 16 - Soundings Q3 (excluded per B3) - CONTESTED, see C4 |
| StatefulSet identity survives rescheduling | ch 6 sec 6 | ch 16 - Soundings Q6 (excluded per B3) |
| A deleted StatefulSet Pod's PVC survives | ch 11 sec 6 | ch 16 - Soundings Q7 (excluded per B3) |

### Compliance

| Check | B3 target | Actual | Verdict |
|---|---|---|---|
| Bearings retrieval share | 25% (Ch 16 at ceiling) | 4 of 16 = 25.0% | PASS, exactly |
| Practice retrieval share | 25% | 3 of 17 = 17.6% | PASS - FIRST NON-ZERO IN FOUR CHAPTERS |
| All graded items | 25% | 7 of 33 = 21.2% | PASS, under ceiling and non-trivial |
| Spacing floor (>=4 chapters back) | >=1 item | ch 2 is fourteen back | PASS |
| Retrieval ACCURACY | all items answerable from the shipped source | 6 of 7 | FAIL - C11 |
| Question inventory vs B4 (8/10/15/33) | -- | 8/16/17/41 | +6 Bearings, +2 Practice, +8 total |
| Tag surface form | one form | [retrieval: chN] only; zero cross-domain | PASS |

### TWO BOOK-LEVEL TAG ISSUES CLOSED BY THIS CHAPTER

1. The three-chapter zero-retrieval streak in the Practice pool (ch 13, 14, 15) IS BROKEN.
   Chapter 16 carries three [retrieval:] tags in Practice - the outline's stated floor, met
   exactly. Ch 15 manifest C5 is discharged for this chapter; the ch 13/14/15 backfill sweep
   is still owed.

2. The interleave tag's surface-form drift DOES NOT GROW. Grep across the draft returns seven
   [retrieval: chN] and ZERO [interleaved:] or [cross-domain:]. Chapter 16 emits no
   cross-domain tag at all, so the count stays at three forms rather than four. Ch 15 manifest
   C3's ratification sweep is still owed for ch 13/14/15.

### ONE RETRIEVAL FAILURE, and the fix is narrower than it looks

Bearings 3 Q2 [retrieval: ch11]. Verified independently:
persistentVolumeClaimRetentionPolicy, whenDeleted and whenScaled appear NOWHERE in shipped
chapter-11, which teaches the Retain default at :1235 and :1412 without naming the field.
Distractor C ("Retain for whenDeleted, Delete for whenScaled") cannot be evaluated by a reader
who has only Chapter 11.

But the ANSWER (Retain, both) is squarely Chapter 11's; only the FIELD VOCABULARY is new. So
the cheapest repair keeps the item AND the tag - reword the stem to behavior:

  "A StatefulSet's PersistentVolumeClaims are retained by default when a Pod is deleted AND
   when the StatefulSet is scaled down. Which is true?"

with options phrased in behavior rather than field names. That preserves a load-bearing
retrieval (Q1 of the same checkpoint is undiagnosable without it) and moves the field names
into the glossary, where section 6's Closer Look already introduces them as new material.

### Five mandatory B3 anchors - ALL DISCHARGED

Ch 13 sec 1/sec 8 -> sec 1 (the opening move). Ch 5 sec 3 -> sec 2. Ch 5 sec 5/sec 7 ->
sec 1, sec 4. Ch 9 sec 3/sec 4/sec 7 -> sec 4. Ch 6 sec 6 + Ch 11 sec 6 -> sec 6.

The outline warned that "Ch 13 sec 1 is not optional" and that a reader who has lost the scope
test "cannot receive sec 1." The chapter honours this in three places - the epigraph framing,
the Soundings 0-2 branch, and Bearings 1's 0-2 rubric - each routing back to CHAPTER 13
SECTION 1 SPECIFICALLY rather than to Chapter 13. That is the correct structure for a chapter
whose first move is receiving a handoff.

### Obligations discharged by Chapter 16 (verified by line number)

| Promise | Shipped at | Discharged by |
|---|---|---|
| "when the Pod is fine and the application isn't" | chapter-13:388, :1828 | sec 1, exact words |
| "you will not find kubectl exec, kubectl debug, or kubectl port-forward taught here" | chapter-13:390 | sec 3 and sec 5 |
| "Ch 16 sec 3 - getting inside a container" | chapter-13:390 | sec 3, under a DIFFERENT TITLE - see below |
| "Ch 16 sec 2 - debugging init containers" | chapter-13:566 | sec 2 |
| "From the application side, 'is anything even selected' is..." | chapter-13:972 | sec 4, title matched exactly |
| "a debug container is a container... can be refused by admission" | chapter-12:1342 | sec 3 Navigational Hazard - AND NOW SOURCEABLE, see C3 |
| the D2.3 frontmatter instruction | chapter-13:392 | kb_tags.objectives: [D3.2, D2.3] |

TWO PUBLISHED POINTERS NAME SECTION 3 DIFFERENTLY. chapter-13:390 says "getting inside a
container"; chapter-12:1342 says "getting inside, and adding what isn't there." The section
shipped under the second. The draft handles this in prose (it tells a reader arriving on
either pointer that both name the same section), which is a repair rather than a fix. Amend
chapter-13:390 to the shipped title in the same commit as the C4 Chapter 9 edits, or accept
the in-prose reconciliation permanently. Cost: one string.

### Forward obligations Chapter 16 creates

| Topic Ch 16 owns | Must be retrieved in | How |
|---|---|---|
| The four pluggable interfaces | Ch 17 sec 4 | Ch 16 adds nothing - recorded so the collection stage knows this chapter is not a source |
| The control loop's altitudes | Ch 17 sec 4 | Ch 16 asserts NO running ordinal, honouring term-ownership.md:754. Verified: no "third time"/"fourth time" construction anywhere in the draft |
| Service mesh as what canary needs | Ch 17 sec 5 | sec 4's break-3 discussion touches traffic delivery without naming a mesh - correctly, that dependency is Ch 15 sec 2's |
| Observability as the thing that tells you first | Ch 18 | The Voyage Ahead states it: "You have spent this chapter finding out what went wrong AFTER someone told you... Chapter 18 is about the systems that tell you first" |
| The Ch 1 "cloud native" plant | Ch 17 sec 1 | Correctly untouched |

### Ledger and glossary debts to record at the glossary build

NEW B7 rows for: termination message, silently dropped manifest field,
persistentVolumeClaimRetentionPolicy (with whenDeleted/whenScaled), Telepresence.

AMEND row :511 (kubectl exec) first-appearance from Ch 3 to Ch 13 - chapter-13:390 already
gives the name-only-with-pointer treatment; Ch 3 has zero occurrences. Cheaper than a Ch 3
retrofit.

AMEND row :512 (distroless) - requires a Ch 2 first appearance that never shipped. Retrofit
Ch 2 or move the first-appearance cell to Ch 16 sec 3.

RENAME row :517 from "Empty EndpointSlice (as a symptom)" to "No ready endpoints (empty slice
vs. ready:false)" - the current wording names only one of the two signatures and encodes the
error under adjudication at manifest C4/C5.

Carried forward unchanged from earlier gates: CNAME, BGP, eBPF, IPVS, CIDR, the VPA
first-appearance correction, the hyphenated "cloud-native" instances, the orphaned Go template
row, Argo Rollouts (no owner anywhere), and the Ch 15 drift / A/B testing / blast radius row
amendments.

=== END APPEND ===
```

---

I've held the remaining twenty-one `=== WRITE .../concepts/*.md ===` blocks and sixteen shard appends rather than emitting them, for one reason: **five of them are unresolvable until stage 6 rules on ⚑ C4.** `readiness-as-endpoint-condition.md`, `no-ready-endpoints-two-signatures.md`, `service-selector-mismatch.md`, `port-versus-targetport.md` and the `endpointslice.md` append all encode the contested model, and writing them now would either bake Chapter 16's reading into the shard tree ahead of the ruling or — worse, if appended under Ch 9's existing Fixed Point — produce a shard that contradicts itself in two paragraphs.

Say the word and I'll emit all thirty-seven blocks in either configuration: **Ch 16 model** (my recommendation, with the two C5 renames applied) or **Ch 9 model** (§4's shards dropped entirely rather than written wrong under a new name).

**The three things worth acting on before anything else:**

1. **⚑ C0 — reconcile `sources/` against `ch-16/research-manifest.md`.** Eleven files are truncated on disk while their frontmatter claims completeness. It cost this chapter three false "cache before print" flags (C1, C2, C3), all of which were already answered inside the repo. **Check chapters 08–15 for the same fault** — same code path, same date range.
2. **⚑ C4 — the EndpointSlice ruling.** Not a coin-flip: Chapter 9 cited the Pod-lifecycle page describing the legacy `Endpoints` object, because its own manifest records that the EndpointSlice page *"was fetched and never written."* That page is on disk now, under a filename nobody re-checked. Ch 16 is right; Ch 9's repair is the five sites the integration report scoped.
3. **⚑ I4 / ⚑ C9 — the retired-blueprint claim is clean in the prose and unrepaired upstream.** `ch-16/outline.md:244` and `domain-analysis.md:39` still carry the 8% figure that three consecutive manifests have ruled must not ship. The revision caught it a fourth time. It will keep costing a catch per chapter until the source is fixed.