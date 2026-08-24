# Integration Check — KCNA Chapter 3

## Summary

- Terminology consistency: **pass** — 4 low-severity drift items, none semantic
- Callbacks to earlier chapters: **9 correct / 1 incorrect** (backward, to Ch 1–2). Forward cross-bearings: 20 checked against `chapter-lineup.md` — 18 land, 2 flagged
- Retrieval-practice accuracy: **pass** — 4/4 `[retrieval: ch2]` tags land on material Ch 2 actually teaches; rate 10.5% against B3's 10% rung (v1's short-by-1 is fixed)
- Glossary coverage: **21 concepts introduced, 19 defined in-chapter, 12 require glossary entries**
- Contradictions with earlier canon: **3 flagged**, plus 1 forward-numbering conflict
- Ethical guardrails (skill Part 14): **fail on one item** — unverifiable exam-frequency claims (Guardrail #8). All other items pass, several unusually well.

**Access note (rule 2):** no knowledge-base shards were tagged for this stage, so nothing was inferred about earlier chapters. Everything below was verified directly against `chapter-01-taking-departure.md`, `chapter-02-cargo-in-standard-crates.md`, and `.pipeline-state/book-outline/chapter-lineup.md`. Chapters 4–20 do not exist yet; forward bearings are checked against the lineup's objective column only, and section numbers inside undrafted chapters cannot be verified at all.

**Confirmed still-open blocker.** The draft's §2 AUTHOR-REVIEW (line 220) is accurate as written: `ls sources/` returns 87 files, all dated `-2026-08-23`, zero dated `-2026-08-24`. The five snapshots the draft cites on 14 lines are not on disk. This is not re-auditing facts — it is confirming that the recovery the revision stage requested has not run. No re-fetch is needed; the bodies are in `research-manifest.md`.

---

## Terminology consistency

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| kubelet | `kubelet`, lowercase (ch02:545) | 65 lines | No — never capitalized, never "Kubelet" |
| container runtime | `container runtime` (ch02:539) | throughout §3 | No |
| CRI / Container Runtime Interface | expanded on first use, then CRI (ch02:539) | §3, Bearings #1 Q5 | No — expanded at first use here too |
| containerd / CRI-O | exact casing (ch02:539) | §3, Practice Q13 | No |
| control plane | two words, lowercase; hyphenated attributively | 46 lines | No — `control-plane component` vs `the control plane` used correctly throughout |
| kube-apiserver / the API server | component name vs prose reference | 15 / 61 lines | No — the split matches upstream docs, but it is **established here**; record it so Ch 4–8 follow it |
| kube-proxy, kube-scheduler, kube-controller-manager, cloud-controller-manager | lowercase, hyphenated | census + Fixed Point | No |
| etcd | lowercase always | §2, §5, Summary | No |
| Pod | capitalized (ch01:178, ch02:318) | throughout | No |
| PodSpec | one word, camel (ch02:545) | 15 lines | No |
| addon | `addon`, per docs | 19 lines | **Yes, once** — line 466 reads "add-on" |
| operating system / kernel | ch02:281 holds both registers deliberately | §1, Practice Q2 | **Yes, attribution** — see Contradiction 2 |
| "Kubernetes defines an interface…" (named pattern) | ch02:598, reader explicitly asked to name it | §3, line 325 | **Yes** — re-derived in new words, not named, not beared back. See Contradiction 3 |

**Structural-convention drift (book-level, not a Ch 3 defect).** Three conventions now differ across three shipped chapters. Ch 3 is not the outlier in every case, so these belong to the reconcile pass rather than to a Ch 3 edit:

1. **Checkpoint headings.** Ch 2 numbers them (`## ☆ Taking Your Bearings #1: Containers, Images, and Identity`). Ch 1 and Ch 3 do not. Ch 3 is *internally* inconsistent: its Attention Budget table (lines 17, 20, 22) names "#1 / #2 / #3" and its remediation prose says "Taking Your Bearings #3", but the three headings (341, 536, 696) carry no number. Cheapest fix is to number the Ch 3 headings, which also matches Ch 2.
2. **Answer-block heading.** Ch 2 uses `### Practice Question Answers` (ch02:1146). Ch 3 uses a bolded `**Answers with Explanations:**` (382, 570, 730, 1023).
3. **Metadata line.** Ch 1 carries `Chapter Type` and `Prerequisites`; Ch 2 carries exam domain, competency, source tags, and the authored-allocation disclosure inline; Ch 3 carries neither Chapter Type nor Prerequisites and states only `~6% of exam (authored estimate)`. Ch 3's ethical disclosure is fully present in prose (§Why This Chapter Matters), so this is format, not compliance. The lineup assigns Ch 3 prerequisite "2", which the metadata line does not state.

---

## Callback correctness

**Backward references — 9 of 10 correct.**

| # | Claim in Ch 3 | Verified against | Verdict |
|---|---|---|---|
| 1 | §1 line ~118 → Ch 2 §4, kubelet/CRI/runtime chain | ch02:533 `## §4 — 🔵 The Container Runtime Interface` | ✓ exact |
| 2 | §1 → Ch 2 §1, container-vs-VM contrast; "Chapter 2 did that in detail" | ch02:267 `## §1 — ⚪ What a Container Actually Is`, ¶277–314 | ✓ exact |
| 3 | §3 → Ch 2 §4 again; "Chapter 2 walked the chain: kubelet speaks CRI… below that sits the low-level runtime" | ch02:553, 582 Fixed Point `kubelet → CRI → containerd or CRI-O → runC → a running process` | ✓ exact, including the third hop |
| 4 | Soundings A4: "Chapter 2 taught the chain from the kubelet down through the CRI to the runtime" | ch02:545, 582 | ✓ |
| 5 | Soundings rubric: "Chapter 1 told you that Chapters 2 and 3 carry the conceptual load everything else rests on" | ch01:463 — verbatim | ✓ exact, and addressed to the same reader segment |
| 6 | §Why This Chapter Matters: "Chapter 1 established that this exam measures discrimination rather than memorization" | ch01:178, 302, 553 | ✓ — and Ch 3's "layer attribution" framing is a direct extension of ch01:178's "given a symptom, can you name the layer where the problem lives" |
| 7 | §1 Snag: "this book used it that way in Chapter 1" | ch01:144 | ✓ |
| 8 | §7 quotation: *"Kubernetes is an orchestrator — it decides what should run where."* | ch01:144 — verbatim | ✓ |
| 9 | §7 "Chapters 8, 12, and 13 all depend on you knowing which" | lineup rows 8, 12, 13 (etcd backup / encryption at rest / node health) | ✓ |
| 10 | §7 line 792 → `see Ch 1 §2` | Ch 1 has **no §-numbered sections**, and the orchestrator line lives in Ch 1's 🧭 Soundings answer key (A2), before any body section | ✗ **unresolvable pointer** |

**Fix for #10:** `*[cross-bearing: see Ch 1 🧭 Soundings A2 — where this book first called Kubernetes an orchestrator, in the industry's loose sense]*`. The quotation itself is correct; only the address is wrong.

**Reciprocity holds.** Ch 2 makes two forward promises into this chapter and both are honored exactly: ch02:588 → "Ch 3 §1 — how the cluster got the shape it has" (Ch 3 §1 title matches word for word) and ch02:602 → "Ch 3 §3 — node components in context" (likewise). Ch 2's header comment warns that its own section numbering is load-bearing because Ch 1 names it; Ch 3 now adds two more citations of Ch 2 §1 and §4, so that lock has tightened. Worth recording for stage 14.

**Forward cross-bearings — 18 of 20 land.** Checked against the lineup's per-chapter objective column: Ch 4 (spec/status, manifests) ✓ ×2 · Ch 5 (Pods, probes) ✓ · Ch 6 (ReplicaSet, controllers) ✓ ×2 · Ch 7 (scheduler internals) ✓ · Ch 8 (etcd backup; auth→authz→admission gates) ✓ ×2 · Ch 9 (Services + kube-proxy; CoreDNS + DNS records) ✓ ×2 · Ch 10 (Ingress controller) ✓ · Ch 12 (Secrets, encryption at rest) ✓ · Ch 13 (crictl §5 — agrees with ch02:602's identical §5 pointer; `kubectl top` + metrics-server) ✓ ×2 · Ch 15 (Argo CD, Git as desired state) ✓ ×3 · Ch 17 (VPA as add-on; declarative APIs) ✓ ×2.

Two flagged:

- **§5 → "Ch 13 — the debugging commands that ride those outbound paths."** The paths named are logs, attach, and port-forward. The lineup gives `logs --previous` to Ch 13 but `exec` and `port-forward` to **Ch 16**. Suggest splitting: `*[cross-bearing: see Ch 13 — reading logs; and Ch 16 §… — exec and port-forward]*`.
- **§1 line 208 → "Ch 17 §1 — the CNCF, its governance, and the cloud native definition."** Ch 17's section numbers are already spoken for, inconsistently, by two shipped chapters: ch01:376 reserves **§1** for the cloud native definition, ch01:146 reserves **§2** for CNCF governance, ch01:184 reserves **§4** for the certification landscape — while ch02:600 reserves **§4** for the four pluggable interfaces. Ch 3's bearing merges Ch 1's §1 and §2 into one. Three chapters are now pre-committing an undrafted chapter's numbering and they do not agree.

**Recommended book-level rule (for author decision):** drop `§N` from cross-bearings that point into undrafted chapters; keep them only where the target ships. Ch 3 already follows that instinct for 17 of its 20 forward bearings. Stage 14 should record a Ch 17 section-reservation entry either way, since Ch 1's §4-vs-Ch 2's §4 conflict exists independently of this chapter and will otherwise surface at reconcile.

---

## Retrieval-practice accuracy

| Item | Tag | Topic | Covered in Ch 2? |
|---|---|---|---|
| Soundings Q4 (line 49/68) | `[retrieval: ch2]` | kubelet ensures containers described for its node are running | ✓ ch02:545, verbatim source alignment |
| Bearings #1 Q5 (line ~380) | `[retrieval: ch2]` | kubelet reaches the runtime through CRI | ✓ ch02:582 Fixed Point |
| Practice Q2 (853) | `[retrieval: ch2]` | containers share the operating system; VMs each boot their own | ✓ ch02:279, 281 |
| Practice Q24 (1007/1133) | `[retrieval: ch2]` | immutability — rebuild the image, recreate the container | ✓ ch02:336, near-verbatim |
| Practice Q25 (1014/1138) | `[retrieval: ch2]` | image contents: code, runtime, application and system libraries, defaults | ✓ ch02:326, verbatim |

**All five land. No mistagged item, no untagged retrieval.** Tags appear in both stem and answer key, which is the convention later mechanical audits need.

**Rate.** Excluding Soundings (B3 excludes them from the budget by design), the graded pool is 38 items with 4 retrieval = **10.5%** against B3's 10% rung for Ch 3. The v1 audit's "short by 1" finding is resolved: revision shipped the container-vs-VM anchor the outline named and dropped, and added an image-contents item beyond plan. All retrieval draws from Ch 2 with none from Ch 1, exactly as B3 specifies ("Ch 1 is excluded from retrieval entirely").

**One pedagogy note, not an accuracy defect.** Practice Q2's answer is stated verbatim in this chapter's own §1 ("relaxed isolation properties that let them share the operating system among the applications"), roughly 70 minutes of reading before the question. The tag is honest — Ch 2 does teach it — but the item no longer functions as *spaced* retrieval; it is same-chapter recall. Options: re-key it to a Ch 2 fact §1 does not restate (layers, tags vs digests, "an image contains no kernel", or "relaxed isolation is a tradeoff, not a deficiency"), or keep it and accept it as reinforcement. Author's call; the outline did name container-vs-VM specifically, so keeping it is defensible.

**Also worth doing while Q2 is open** — see Contradiction 2. Its answer key currently marks "The operating system" correct with no reference to the two-register reconciliation Ch 2 spent three paragraphs building. A reader who internalized Ch 1's A1 ("the host's **operating system kernel**") meets this item and sees their answer unlisted. One clause fixes it: *"Ch 2 §1 holds both registers — 'operating system' is the published wording and the one to recognize on an answer sheet; 'kernel' is the mechanism underneath it."* That sentence is Ch 2's own (ch02:281) and costs nothing.

---

## Glossary coverage

**Concepts whose home is this chapter (21 introduced, 19 defined):**

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| control plane | yes | yes (book glossary, Part 16) |
| worker node / node | yes | yes |
| kube-apiserver | yes | yes |
| etcd | yes | yes |
| kube-scheduler | yes | yes |
| kube-controller-manager | yes | yes |
| cloud-controller-manager | yes | yes |
| kube-proxy | yes | yes |
| addon | yes | yes |
| controller | yes | yes |
| control loop | yes (★ Fixed Point) | yes |
| desired state | yes | yes |
| current state | yes | yes |
| control via API server | yes | yes |
| direct control | yes | yes |
| orchestration (technical sense) | yes (★ Fixed Point) | yes |
| absent-component pattern | yes (named + ⚓) | yes — **record the canonical name** |
| hub-and-spoke API pattern | yes | optional |
| Borg / Omega | yes | yes (short) |
| **binding** | **partial** — one clause, "in a process called binding"; full treatment Ch 7 | **yes** |
| **reconciliation** | **no** — used 3× as a synonym for the control loop; its only definition is buried in Practice Q20's distractor rationale | **yes** |

**Concepts used here but owned by another chapter (12 checked, 9 need an entry now):**

| Term | Status in Ch 3 | Owner | Needs glossary entry? |
|---|---|---|---|
| **Pod** | used ~40× with **no definition and no explicit deferral**; ch02:318 promised "It is Chapter 5's whole subject" but Ch 3 never repeats that promise except via a §3 bearing that reads as being about PodSpec | Ch 5 | yes |
| **PodSpec** | partial — "for now, simply the description of what containers should run" | Ch 5 | yes |
| **Service** | used in §3, §4, Bearings, Practice; hedged as "a Kubernetes object with its own chapter" | Ch 9 | yes |
| **PaaS** | **acronym never expanded** — first use in the book (absent from Ch 1 and Ch 2) | — | yes |
| **CI/CD** | **acronym never expanded** — first use in the book | Ch 15 | yes |
| **VPA** | **acronym never expanded** — appears only inside a cross-bearing (line 466) | Ch 17 | yes |
| EndpointSlice, ServiceAccount, Lease | name-dropped in the controller list and in Bearings #1 Q4's rationale | Ch 9 / Ch 5 & 12 | yes |
| kube-system namespace | distractor only (line 364) | Ch 4 | yes |
| Argo CD | named with source tag, forward-beared | Ch 15 | yes |
| metrics-server, `kubectl top`, `crictl` | named, forward-beared | Ch 13 | yes |
| kubelet, container runtime, CRI, containerd, CRI-O | restated and re-defined in §3 | Ch 2 | already carried from Ch 2 |
| CNCF | partial (part of the Linux Foundation) | Ch 1 / Ch 17 | already carried from Ch 1 |

**Total requiring an entry under rule 4 (introduced or used without definition): 12** — reconciliation, binding, PodSpec, Pod, Service, PaaS, CI/CD, VPA, EndpointSlice, ServiceAccount, Lease, kube-system. The remaining 19 in-chapter-defined terms still belong in the book glossary under skill Part 16's completeness requirement, cross-referenced to Chapter 3.

**Two worth acting on inside the chapter rather than deferring to the glossary:**

- **Pod.** It is this chapter's most-used undefined primitive and it is load-bearing here (the scheduler assigns Pods, the Job controller creates Pods, a cluster needs a worker node "in order to run Pods"). Ch 2 set the reader up to expect the deferral; Ch 3 should close it in one sentence at first use in §2 — *"A Pod is the unit Kubernetes schedules; Chapter 5 is its whole subject"* — rather than leave it implied.
- **Reconciliation.** §Why This Chapter Matters asks the reader to "sketch a reconciliation loop from memory" before the word has been introduced, and the ★ Fixed Point that would define it says "control loop" instead. One appositive at the Fixed Point ties them together and makes the word retrievable in Ch 6, 11, 15, and 17, where B3's control-loop theme runs.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Every figure is either source-tagged (47,501 lines; 2014-06-06; v1.0 July 2015) or explicitly disclosed as authored. The `~6%` weight carries its disclosure twice — in the metadata line and again in prose: *"CNCF and the Linux Foundation publish weights per domain, with competencies named but not individually weighted… treat that number as an estimate the author is accountable for."* This satisfies lineup disclosure #1 and is the cleanest handling of it in the book so far.
- [x] **Fear-based content uses real examples.** No fabricated breach or outage narrative anywhere. The 3 a.m. framing (Soundings Q2) is a generic operational scenario, not an incident attributed to anyone. Subject-dignity guardrail (skill v5.7): every wry beat is oriented at the practitioner — "Most people with scripting experience answer 'start two more'", "That should bother you" — and none at harms borne by third parties. Pass.
- [x] **Simplification is acknowledged.** §3 carries a Dead Reckoning block; §1 explicitly separates the documentation's "operating system" from the book's kernel-level gloss; §4 marks whose word "optional" is in each row of the table ("The documentation's" / "This book's framing"); §4's DNS passage separates the sourced claim from the author's field observation in as many words ("That second half is an observation, not a documented claim"); §7 volunteers that its own heading overstates and narrows the thesis. This is the strongest item in the chapter.
- [~] **Authority claims cite legitimate sources.** The sources are legitimate; eight of them are not on disk. Conditional pass pending the harvest recovery confirmed above.
- [ ] **"Frequently tested" claims are verifiable against the curriculum snapshot — FAIL.** Five frequency assertions cannot be checked against anything published. CNCF does not release question counts, per-item frequencies, or competency weights (lineup disclosure #2, gaps G33/G34):
  - line 179 — "it is tested more often than people expect"
  - line 279 area — "which is exactly why it gets tested"
  - line 445 and line 598 — "they're both cheap points on exam day"
  - line 826 — "Pure recall, cheaply tested, and it is tested"
  - line 828 — "One sentence in the documentation, disproportionately tested"

  The lineup's own instruction is explicit: chapters "must describe those as 'easy to confuse,' never 'frequently tested' — the distinction Ethical Guardrail #8 requires." **Ch 2 already models the compliant phrasing** at ch02:588: *"These are easy to confuse, and the confusion is historical rather than careless."* Ch 3 drifts from a discipline the previous chapter established.

  Two things the author should know before deciding. First, the *underlying claims are almost certainly right* — the `logically… single binary` sentence and the two optionality markers are exactly the kind of thing a discrimination exam tests. The problem is the epistemic register, not the judgment. Second, at least one of these phrasings **originated in an upstream pipeline stage**: `diagnostics/question-quality.md:319` drafted the missing Bearings #2 rubric and supplied "both are cheap points on exam day" verbatim, which revision adopted in good faith. This is not a drafting lapse so much as a guardrail that isn't being enforced at the stage that writes remediation copy.

  Suggested rewrites, preserving every bit of the emphasis: "tested more often than people expect" → "easier to get wrong than its length suggests"; "cheap points on exam day" → "cheap to get right once you've noticed the word"; "disproportionately tested" → "one sentence, and the whole distinction rides on it."
- [x] **No strawmanning of alternative study methods.** Ch 3 makes no study-method claims at all. Ch 1 handles the topic fairly (ch01:180 calls the hands-on instinct "partially misdirected", ch01:290 concedes "that doesn't make its facts wrong"), and Ch 3 introduces nothing that contradicts it.

---

## Contradictions with earlier canon

**Contradiction 1 — PodSpec is assigned to two different chapters, one line apart.** §3 line 305: *"A PodSpec, for now, is simply the description of what containers should run. **Chapter 4** gives it a proper treatment."* The cross-bearing directly beneath it points to **Ch 5** ("Pods, PodSpecs, and what 'running and healthy' means precisely"), and ch02:318 already told the reader that the Pod "is Chapter 5's whole subject." The lineup gives Ch 4 the generic `spec`/`status` fields and manifests; the PodSpec proper belongs to Ch 5. **Fix:** "Chapter 4 gives you `spec` in general; Chapter 5 gives the PodSpec its proper treatment," or simply change 4 → 5.

**Contradiction 2 — the §1 AUTHOR-REVIEW (line 130) misreports the state of the book, and could cause a bad edit to Chapter 1.** It states that ch02:279 "matches the snapshot and reinforces it," that Ch 1 "sharpens to 'operating system kernel'," and that "the remaining outlier is Chapter 1 — raise it there or at the reconcile pass."

What Chapter 2 actually does (ch02:281–285) is adjudicate both registers as correct and tell the reader to hold both: *"The Kubernetes documentation and the CNCF glossary say a container shares the operating system. That is the phrasing the exam is likeliest to use… Practitioners and the container-runtime documentation usually sharpen it: a container shares the host's kernel… Hold both registers."* It then supplies an in-cache warrant for the sharpening (`k8s-docs-runtime-class`'s "user-space kernel (such as gVisor)"), and its own AUTHOR-REVIEW prescribes the resolution: once harvest items A13/A14 land, tag the paragraph *and* **delete Chapter 1's parallel flag "so the two chapters agree."**

So Chapter 1 is not an outlier in *content* — it uses the kernel register Chapter 2 explicitly blesses. The only live question is an *attribution* one: whether ch01:142's bolded "operating system kernel" may sit on a line tagged `k8s-docs-overview`. That is blocked on the same missing-snapshot harvest as this chapter's eight dangling tags.

The risk of leaving the note as written: an author acting on "the remaining outlier is Chapter 1" would flatten ch01:142 toward "operating system," deleting the register that Ch 2 §1 spends three paragraphs establishing and that Figure 2-1's derivation ("Three guest kernels on one host means three times the baseline resource cost") depends on. **Fix:** rewrite the note to cite ch02:281–285 rather than ch02:279 alone, state that Ch 1 and Ch 2 already agree on substance, and route the single open item — Ch 1's source tag — to the A13/A14 harvest. Ch 3's body prose needs no change; it is already correct and correctly hedged.

**Contradiction 3 — §3 folds etcd into a named pattern that does not cover it, and does so without naming the pattern.** Line 325: *"That is the same architectural instinct you saw with etcd. Where a good general-purpose component already exists, Kubernetes defines an interface and uses it rather than reimplementing it."*

Two problems. (a) Ch 2's pattern is specifically *"Kubernetes defines an interface and lets the ecosystem implement it"* (ch02:598), and its sourced enumeration is CRI, CSI, CNI, device plugins, and API extensions. **etcd is not among them** — Kubernetes does not define an etcd interface; it consumes a general-purpose datastore. Ch 3's sentence is true about the *runtime* and true-but-different about *etcd*, and calling them "the same" broadens a sourced enumeration past what it says. (b) ch02:596–598 is a section literally titled "The pattern to name now," whose ⚓ tells the reader *"Give this move a name in your head, because you are about to see it three more times."* Ch 3 hits the pattern's first recurrence and re-derives it in fresh words, without the name and without a cross-bearing back. That is a missed spaced-retrieval event on a theme B3 tracks and Ch 17's secondary Zenith depends on.

**Fix:** separate the two instincts — keep "Kubernetes defines an interface and lets the ecosystem implement it" for the container runtime, cross-beared to Ch 2 §4; describe the etcd case as the adjacent-but-distinct instinct of reusing an existing general-purpose component rather than building one.

**Forward-numbering conflict (not an earlier-canon contradiction, but flagged here so it doesn't get lost).** Ch 17's section numbers are pre-committed inconsistently by Ch 1 (§1 definition, §2 governance, §4 certification landscape), Ch 2 (§4 pluggable interfaces), and now Ch 3 (§1 = definition *and* governance). Ch 1 vs Ch 2 already disagree about §4 independently of this chapter. See the Callback section for the recommended rule.

---

## Recommended fixes

Everything the diagnostics raised and revision addressed is confirmed applied: the Argo CD direction is corrected and tagged; the retrieval shortfall is closed at 10.5%; Bearings #2 now has a score rubric; the container-vs-VM anchor shipped; the §1 kernel gloss is de-tagged and visibly authorial; the Chapter Summary row uses "operating system"; the stale §5 AUTHOR-REVIEW demanding a fetch that already happened is gone and replaced with two accurate qualifications. The items below are new at this gate.

**Blocking — author decision required**

1. **Guardrail #8 frequency claims** (lines 179, ~279, 445, 598, 826, 828). Rewrite to the "easy to confuse" register Ch 2 already uses, per the suggestions above. Note that line 598's phrasing came from `question-quality.md:319`, so the remediation-copy stages need the same guardrail applied to them, not just the drafting stage.
2. **The §1 AUTHOR-REVIEW at line 130** (Contradiction 2). Rewrite before anyone acts on it. Do not let it drive an edit to Chapter 1.
3. **The five missing `-2026-08-24` snapshots.** Confirmed still absent. Eight tags on 14 lines dangle until the harvest runs. Mechanical extraction from `research-manifest.md`; no re-fetch.

**Should fix before publication**

4. **PodSpec: Chapter 4 → Chapter 5** (line 305).
5. **`see Ch 1 §2` → `see Ch 1 🧭 Soundings A2`** (line 792). Ch 1 has no numbered sections.
6. **§3 line 325** — separate the etcd case from Ch 2's named interface pattern, and cross-bear back to Ch 2 §4.
7. **"Six later chapters retrieve §6 by name"** (lines 30, 78, 96). B3's control-loop theme is Ch 3 → 4 → 6 → 11 → 15 → 17, which is **five** later chapters; the draft's own forward bearings name four (Ch 4, 6, 15, 17) and omit Ch 11. Either change to "five" and add the Ch 11 bearing, or soften to "later chapters." Three occurrences, all identical, so it's one decision.
8. **"You're going to meet it four more times"** (line 461). Three instances follow (Ch 10 Ingress, Ch 13 `kubectl top`, Ch 17 VPA); the Ch 9 CoreDNS bearing is a DNS pointer, not an absent-component instance. B3's fourth instance is **NetworkPolicy on a CNI that doesn't enforce it**, which is also Ch 10 material. Adding that bearing makes the count exact and matches B3's named theme. Ch 2 got the parallel count right at ch02:598 ("three more times," three instances plus a collection) — worth matching that discipline.
9. **Practice Q2 answer key** (line ~1057): add Ch 2 §1's one-clause two-register note, so a reader carrying Ch 1's "kernel" answer isn't silently contradicted.
10. **Define Pod at first use in §2** (one sentence), and **tie "reconciliation" to "control loop"** at the §6 ★ Fixed Point.

**Low severity**

11. `add-on` → `addon` (line 466).
12. Expand PaaS, CI/CD, and VPA on first use, or accept them as glossary-only.
13. Number the three Bearings headings (341, 536, 696) to match the Attention Budget table and Ch 2.

**For stage 14 / reconcile, not for this chapter**

14. Record the **absent-component pattern** under that exact name, so Ch 10, 13, and 17 retrieve the same phrase rather than re-coining it.
15. Record the **`kube-apiserver` (component) vs "the API server" (prose)** convention this chapter establishes.
16. Record a **Ch 17 section-number reservation**, and adopt the no-`§N`-into-undrafted-chapters rule. Ch 1 §4 vs Ch 2 §4 already conflict.
17. Normalize the metadata line and the answer-block heading across Ch 1–3.
18. **Pipeline defect, book-level:** `.pipeline-state/book-outline/retrieval-architecture.md` and `.pipeline-state/ch-03/diagnostics/theming-density.md` do not contain stage output — they contain the assistant's write-permission apology text, captured as the artifact. B3's actual conclusions survive only as a summary inside that message. Any downstream stage that parses `retrieval-architecture.md` as a spec will get nothing usable. Same root cause as the snapshot-harvest failure: the executor cannot write into the book tree.