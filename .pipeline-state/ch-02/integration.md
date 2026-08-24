# Integration Check — KCNA Chapter 2

## Summary

- Terminology consistency: **pass** (2 low-severity ambiguities flagged, no drift)
- Callbacks to earlier chapters: **1 correct / 0 incorrect** — but **4 of 15 forward cross-bearings are broken or at risk**, and **1 shipped back-reference in Chapter 1 now contradicts this draft**
- Retrieval-practice accuracy: **pass** (0 retrieval items in this chapter, which is correct per B3; 12 inbound items from Ch 3–5 all verified supported)
- Glossary coverage: **57 concepts introduced, 41 defined in the chapter, 17 require glossary entries**
- Contradictions with earlier canon: **1 flagged** (Ch 1 "The Voyage Ahead" vs. this chapter's opening)
- Ethical guardrails (skill Part 14): **pass with one qualification** (frequency-flavored claims hedged unevenly)

**Scope note on method.** The knowledge-base shards were empty for this run, so rather than declare callbacks unverifiable I checked them directly against the drafted chapters on disk (`../Book-KCNA/chapter-01` through `chapter-07`) and against `.pipeline-state/book-outline/chapter-lineup.md` for Ch 8–20. Findings below distinguish *verified against a drafted chapter* from *inferred from the lineup*. No fact-accuracy re-audit was performed.

---

## Terminology consistency

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| kubelet | `kubelet` (lowercase) | 34 | No — 231/231 lowercase book-wide |
| containerd | `containerd` | 21 | No — 30/30 book-wide |
| CRI-O | `CRI-O` | 22 | No — sole lowercase instance is the `kb_tags` machine tag |
| runC | `runC` | 16 | No — sole lowercase instances are the `kb_tags` tag and a verbatim README quote inside an AUTHOR-REVIEW |
| Container Runtime Interface / CRI | expanded once, then `CRI` | — | No |
| Open Container Initiative / OCI | expanded once, then `OCI` | — | No |
| `image-spec` / `distribution-spec` / `runtime-spec` | backticked lowercase | — | No — consistent with Ch 3's single OCI reference |
| control plane | `control plane` (two words, lowercase in prose) | 1 | No — title case appears only in Ch 3 headings |
| RuntimeClass / `runtimeClassName` | object name capitalized, field backticked | — | No — matches Ch 7 §3–4 usage |
| `imagePullPolicy`, `ImagePullBackOff` | backticked, exact casing | — | No — matches Ch 5 §5 and Ch 13's lineup entry |
| Pod | capital P | — | No — matches Ch 4–7 |
| Branded markers (⚠ Navigational Hazards, ☀️ Zenith) | skill v5.5 names | — | No — 0 instances of retired "Shoals Ahead"/"Landfall" book-wide |

**Two ambiguities, neither drift but both worth an author decision:**

1. **`manifest` carries two unrelated senses in this chapter.** §2 and §5 use it in the OCI sense (the file that names an image's layers). §3's Bearings #1 Q3 ("You deploy a manifest referencing `myapp:v2`") and the Logbook Entry ("The manifest is checked… line by line") use it in the Kubernetes YAML sense, which Ch 4 §2 formally defines. Ch 2 is the first chapter to use either, and it uses both without naming the collision. One clause in §2 ("this is the image's manifest, a different thing from the Kubernetes manifests you'll meet in Chapter 4") would close it.

2. **`namespace` carries two senses.** §1 line 318 uses the Linux sense ("shared network namespace", "process space"); Practice Q10's rebuttal uses the registry-path sense ("drops the `library` namespace"). The Kubernetes sense arrives in Ch 4 §3 as a third. Lower severity than `manifest` because neither Ch 2 sense is load-bearing, but Stage 14 should give `namespace` a disambiguating glossary entry rather than a single definition.

**Formatting variance (book-level, not a Ch 2 defect):** the Voyage Progress line uses three different emphasis conventions across the book — Ch 1 italicizes the word only, Ch 6 bolds the word only, Ch 2 bolds glyph *and* word (`**🌊 Passage**`). Ch 3, 4, 5, and 7 omit the line entirely. Ch 2 is substantively correct; the book needs one convention picked.

---

## Callback correctness

### Backward references — 1 of 1 correct

| Reference | Target | Verdict |
|---|---|---|
| §Why This Chapter Matters → `Ch 1 §Soundings A2 — orchestrator versus runtime` | chapter-01 line 142 | **Correct.** Ch 1 A2 reads "Kubernetes is an **orchestrator**… A separate **container runtime** on each machine does the work." Ch 2's characterization is exact. |

### Inbound pins from Chapter 1 — both honored

Ch 2's frontmatter records that Ch 1 pinned `Ch 2 §1` and `Ch 2 §4`. Verified: Ch 1 line 140 → §1 "What a Container Actually Is" ✅; Ch 1 line 142 → §4 "The Container Runtime Interface" ✅.

### Forward cross-bearings — 15 total

**Verified correct against drafted chapters (7):**

| Cross-bearing | Target section as drafted | Verdict |
|---|---|---|
| `Ch 3 §1 — how the cluster got the shape it has` | Ch 3 §1 "How the Cluster Got the Shape It Has" | Section correct (but see finding **C4** — content promise unmet) |
| `Ch 3 §3 — node components in context` | Ch 3 §3 "Node Components in Context" | ✅ Ch 3's frontmatter explicitly pins both to honor Ch 2 |
| `Ch 4 §4 — Secrets, and the dockerconfigjson type` | Ch 4 §4 "Configuration Kept Outside the Image"; `kubernetes.io/dockerconfigjson` at line 665 | ✅ Ch 4's frontmatter names this pin by line number and honors it |
| `Ch 5 §1 — the Pod as the unit of scheduling` | Ch 5 §1 "The Pod as the Unit of Scheduling" | ✅ verbatim |
| `Ch 5 §5 — Pod phases and container states` | Ch 5 §5 "Pod Phases and Container States" | ✅ verbatim; Ch 5 line 656 returns the pointer reciprocally |
| `Ch 7 — node selection, tolerations, and accounting for overhead` | Ch 7 §2 ("One clause about overhead"), §3 (`nodeSelector`), §4 (tolerations) | ✅ chapter-level, all three topics present; Ch 7 line 576 discharges the promise by name |
| `Ch 10 — NetworkPolicy` | Ch 10 lineup entry | ✅ chapter-level, topic confirmed |

**Broken (1):**

**C1 — `Ch 6 §3 — CRDs and extending the API` (line 600) is wrong. CRDs are Ch 6 §8.**

Ch 6 §3 is "How a Controller Knows Its Own" (selectors and ownership). CRDs are §8, "The Control Loop, Extended." Chapter 6 caught this itself and left a standing note at its line 973:

> `chapter-02 line 600 carries a published cross-bearing reading "*[see Ch 6 §3 — CRDs and extending the API]*". CRDs are §8 in this chapter… the recommended fix is a one-token edit in chapter-02: §3 → §8. Not fixable from inside this draft.`

The revision stage did not make that edit. It is a one-token fix.

**One correction to Ch 6's note, which matters for how the fix is reasoned about:** Ch 6 states that "§3 is pinned by chapter-04 line 688 and cannot move." That premise is false. Chapter 4 contains no §-numbered cross-bearing to Chapter 6 at all — all four of its Ch 6 pointers are chapter-level (lines 353, 415, 834, plus Ch 5's). Line 688 of chapter-04 is a ConfigMap/Secret comparison table. The actual second claimant on Ch 6 §3 is **Chapter 1 line 436**, which uses `*[cross-bearing: see Ch 6 §3 — StatefulSets and stable identity]*` as its worked example of the cross-bearing convention — and StatefulSets are Ch 6 §6. So Ch 6 §3 is mis-pinned by two shipped chapters for two different topics, and neither is the one Ch 6 blames. The Ch 2 edit is still the right fix; Ch 1 line 436 needs the same treatment.

**At risk — no collision yet, but the target chapters are undrafted and the lineup ordering contradicts the numbers (5):**

| Cross-bearing | Risk |
|---|---|
| `Ch 11 §2 — CSI and storage drivers` | Ch 11's lineup orders CSI **ninth** (volume types → PV → PVC → StorageClass → provisioning → binding → reclaim policies → access modes → CSI). §2 is implausible. |
| `Ch 12 §1 — securing the image supply chain` | Ch 12's lineup opens with the security lifecycle phases and 4Cs framing; supply-chain security sits second-from-last. |
| `Ch 12 §2 — signing, attestation, and the software supply chain` | Same. Also note §1 and §2 both describe supply chain, which would require Ch 12 to open with two consecutive supply-chain sections. |
| `Ch 12 §3 — restricting who can pull what` | Registry-side pull authorization does not appear in Ch 12's lineup topic list at all. This may be a content gap, not just a numbering one. |
| `Ch 12 §4 — runtime protection for compute` | Sandboxed runtimes are the **last** item in Ch 12's lineup. |

These are recoverable — the chapters aren't written — but only if the numbers are pinned in Ch 11's and Ch 12's frontmatter now, the way Ch 3 and Ch 4 pinned Ch 1's and Ch 2's. Ch 6 §3 is what happens when nobody does that.

**Collision — two shipped chapters claim the same section for different content (1):**

**C2 — `Ch 17 §4` is double-pinned.**

- Chapter 1, line 182: `*[cross-bearing: see Ch 17 §4 — the cloud native certification landscape]*`
- Chapter 2, lines 600 **and** 914: `*[cross-bearing: see Ch 17 §4 — the four pluggable interfaces, collected]*`

Ch 17 cannot be both. This is the Ch 6 §3 failure with the fuse still burning, and it is on this chapter's most load-bearing forward promise: §8's Zenith stakes the book's closing argument on that pointer ("the collecting is meant to feel like recognition"). Recommend resolving before Ch 17 outlines. Ch 17's lineup places extension-points synthesis fifth in its topic list and the certification ladder dead last, which suggests the interfaces claim should win §4 and Ch 1 line 182 should be retargeted.

*Consistent by contrast:* `Ch 17 §2` (governance/maturity) is pinned identically by Ch 1 line 144 and Ch 2 line 671 ✅. `Ch 13 §5` (crictl) is pinned identically by Ch 2 line 602 and Ch 3 line 451 ✅. `Ch 9 §1` (CNI) has no competing claim and is plausible against the lineup ordering.

**Unmet content promise (1):**

**C4 — §4's 🪝 Snag defers "the era that produced the shorthand" to Ch 3 §1. Chapter 3 does not deliver it.**

Ch 3 §1 narrates the *deployment* eras (physical → virtualized → container) and the Kubernetes origin story. It contains three mentions of Docker in the whole chapter: "a container moment that Docker had opened the year before" (line 342), "announced publicly at DockerCon" (line 344), and a distractor rebuttal (line 1186). Nothing explains why "Kubernetes runs Docker containers" was ever accurate — no Docker Engine, no dockershim, no runtime-history narrative. A reader who follows the pointer to find out why the shorthand existed will not find out.

This chapter's own AUTHOR-REVIEW at that Snag already identifies the material (`A3`, the dockershim FAQ) and says "the dockershim narrative itself belongs to Chapter 3." Chapter 3 is drafted and does not have it. Author decision: add one or two sourced sentences to Ch 3 §1, or soften Ch 2's Snag to stop promising a treatment that doesn't exist.

---

## Retrieval-practice accuracy

**Outbound: 0 retrieval items in this chapter, which is correct.** Per `book-outline/retrieval-architecture.md`, Chapter 1 is excluded from retrieval entirely (orientation chapter, 0% weight), and Ch 3 is the first chapter to carry retrieval items, drawing from Ch 2. Chapter 2 is the first content chapter and has nothing earlier to retrieve. No finding.

**Inbound: 12 `[retrieval: ch2]` items across Ch 3, 4, and 5. All verified as supported by this draft** — this matters because Stage 12 revised the chapter after those items were written, and a cut passage would have orphaned them.

| Source | Item topic | Supported by |
|---|---|---|
| Ch 3 Soundings Q4 + answer | kubelet as the component ensuring containers run | §4 ✅ |
| Ch 3 Bearings #1 Q5 | kubelet reaches the runtime through CRI | §4 Fixed Point ✅ |
| Ch 3 Practice Q2 | what containers share that VMs don't | §1 ✅ |
| Ch 3 Practice Q24 | correct process for changing a running container | §2 immutability ✅ |
| Ch 3 Practice Q25 | what a container image contains | §2 ✅ |
| Ch 4 Bearings Q4 | "one of the **five** mechanisms Chapter 2 listed" for private-registry access — *name two of the other four* | §3 lists exactly five ✅ (node auth, credential provider, pre-pulled images, `imagePullSecrets`, vendor/local extensions). The count is exact; do not drop one from §3 without editing Ch 4. |
| Ch 5 Soundings Q8 + answer | `ImagePullBackOff`, and that Ch 2 said it is reported **as a container in the Waiting state** | §6 states exactly that ✅ |
| Ch 5 Bearings #2 Q4 | phase / state / reason for a Pod that can't pull | §6 supplies the name and the `Waiting` state; Ch 5 supplies phase ✅ |
| Ch 5 Practice Q20 | "Chapter 2 established that containers are immutable" | §2 ✅ |
| Ch 5 Practice Q22 | init container that can't pull its image | §6 ✅ |
| Ch 5 line 307 back-reference | "containers are not the unit Kubernetes schedules; something wraps them" | §1 line 318 ✅ verbatim in substance |
| Ch 7 line 576 | "Chapter 2 also told you a RuntimeClass can carry `nodeSelector` and tolerations" | §7 ✅ |

**One loose item, flagged for the author but not this chapter's defect:** Ch 4 Practice Q13 is tagged `[retrieval: ch2]` but tests ConfigMap immutability in v1.19 — Ch 4's own material. The Ch 2 link is analogical (its answer key at Ch 4 line 1250 rebuts distractor A by invoking Ch 2's build-a-new-image rule). Defensible as interleaving; not accurate as retrieval. Belongs to Ch 4's integration check, noted here only because it is the one inbound item that doesn't test Ch 2 content.

---

## Glossary coverage

**41 of 57 concepts are defined in-chapter and need no separate entry under the stage rule.** Defined and well-scoped: container; container-vs-VM; kernel sharing; container image; image layer; layer stacking and shared bases; immutability; buildpack; builder; stack; platform; lifecycle phases (detect/build/export); reproducible layers; registry; tag; digest; `:latest`; image reference and its three defaults; container runtime; CRI; containerd; CRI-O; runC; kubelet; OCI; `image-spec`; `distribution-spec`; `runtime-spec`; filesystem bundle; `imagePullPolicy`; the three policy values; the four conditional defaults; `ImagePullBackOff`; RuntimeClass; `runtimeClassName`; runtime handler; Kata Containers; gVisor; Pod overhead; CNCF graduated status; kubeconfig; and the four control-plane components glossed in distractor rebuttals.

**17 require glossary entries:**

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| Pod | no — explicitly deferred to Ch 5 | yes (from Ch 5) |
| PodSpec | no — appears inside the quoted kubelet definition | yes (from Ch 5) |
| namespace (Linux/network sense) | no — "shared network namespace", "process space" used bare | yes — **disambiguating entry**, three senses in this book |
| `manifest` | yes, OCI sense only | yes — **disambiguating entry**, OCI vs. Kubernetes sense |
| `imagePullSecrets` | no — named as one of five paths | yes (Ch 2 introduces it) |
| Secret / `kubernetes.io/dockerconfigjson` | no — deferred to Ch 4 | yes (from Ch 4) |
| kubelet credential provider | no — named once, no gloss | yes (Ch 2 introduces it) |
| `crictl` | partial — "a node-level diagnostic" | yes (from Ch 13) |
| NetworkPolicy | no — appears in Bearings #3 Q4 distractor + rebuttal | yes (from Ch 10) |
| Deployment | no — appears in Practice Q12 distractor D | yes (from Ch 6) |
| Waiting (container state) | no — named, deferred to Ch 5 | yes (from Ch 5) |
| CNI | expansion + one-line function only | yes (from Ch 9) |
| CSI | expansion + one-line function only | yes (from Ch 11) |
| device plugin | no — named once in the §4 ⚓ callout | yes (from Ch 17) |
| custom resource / CRD / "API extensions" | no — named as the fourth socket | yes (from Ch 6) |
| SBOM / "bills of materials" | no — named once in §2 | yes (from Ch 12) |
| attestation | no — used in §2's 🔭 Closer Look | yes (from Ch 12) |

Two of these — `Deployment` in Practice Q12's distractor and `NetworkPolicy` in Bearings #3 Q4's distractor — are Kubernetes object names appearing in *answer options and rebuttals* before the reader has met them. Neither breaks the item (both are answerable without knowing the object), but if a lighter touch is wanted, Q12 D could say "the same application" instead of "the same Deployment."

**Tension worth surfacing to the author:** the stage rule says defined-in-chapter needs no entry, but skill Part 16 requires the book glossary to carry "all technical terms introduced in the book" at a 100-term floor. Under the stage rule Ch 2 contributes 17 entries; under Part 16 it contributes closer to 57. Stage 14 should be told which rule governs, because Ch 2 is the largest single vocabulary contributor in the book and the difference is roughly 40 terms.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** No statistics appear anywhere in the chapter. The Exam Alert closes with an explicit disclaimer: *"they are conceptually slippery, not because this book has data on how often they show up. The book does not make frequency claims it cannot support."* This is the strongest form of the guardrail and it is genuinely honored in the trap table.
- [x] **Fear-based content uses real examples.** The §3 Logbook Entry describes a rollback that fails because a tag moved upstream. Every mechanism it depends on is sourced elsewhere in the chapter (tags are movable; identical references don't guarantee identical bytes). It names no company, cites no figures, and claims no frequency. One observation for the author, not a violation: it is written in first-person plural ("we spent an hour proving the manifest hadn't changed"), which reads as lived experience. If house style requires composite anecdotes to be signalled as composite, this is the place it would apply — skill §18.15 defines Logbook Entry loosely enough that it may not.
- [x] **Simplification is acknowledged.** Unusually well. §1 carries both the "operating system" and "kernel" registers and says which to use when. §2 marks the no-kernel claim as *derived, not quoted* ("deliberately not presented here as a quotation, because no authority states it as a negative"). §2's 🔭 flags the "reproducible" gloss as the author's. §5's and §7's 🔭 callouts each say explicitly that they exceed exam depth. §6 opens with a Dead Reckoning block that states the whole exam surface flat before interpreting it.
- [x] **Authority claims cite legitimate sources.** Source tagging is dense and specific throughout. The one substantive untagged passage — §8's containerization history — is flagged by its own AUTHOR-REVIEW, which also correctly refuses to ship the unverifiable McLean attribution and substitutes an original Lodestar epigraph per Part 15. That is the guardrail working.
- [ ] **"Frequently tested" claims verifiable — partial.** The chapter sets itself an explicit standard in the Exam Alert and then applies it unevenly in body prose. Properly hedged: the Attention Budget ("in the author's judgment"), §6's opening ("in the author's judgment the highest value per minute"). Not hedged, and reading as fact: §1 *"That is the phrasing the exam is likeliest to use"*; §5's 🔭 *"What the exam is more likely to ask is which specification governs the registry API"*; §6 *"This is a favorite distractor"*; §7's 🔭 *"an exam item is far likelier to ask why RuntimeClass exists than to ask which sandbox uses which technique."* None is a fabricated statistic and none is harmful — but four unsourced predictions about exam behavior sit alongside a closing paragraph promising the book doesn't make them. Recommend attributing all four to authorial judgment, which costs four words each and makes the disclaimer true chapter-wide.
- [x] **No strawmanning of alternative study methods.** None present.
- [x] **Subject dignity (skill v5.7 Part 14).** All wry beats point at practitioners — "three defaults stacked in a trench coat," "the afternoon turns philosophical," "four competent people have just realized." No harm to third parties is treated as amusing. Clean.

---

## Recommended fixes

The diagnostics were substantially addressed — sourcing gaps are flagged rather than papered over, the epigraph refuses an unverifiable attribution, and the §5 and §7 callouts were correctly trimmed to what their snapshots carry. Everything below is new to this stage.

**Blocking — fix before this chapter is considered final:**

1. **`Ch 6 §3` → `Ch 6 §8`** (line 600). One token. Chapter 6 is drafted, has CRDs at §8, and left a standing request for this edit. Note while you're there that Ch 6's stated reason for not renumbering (a Ch 4 pin at line 688) does not exist — the real second claimant is Ch 1 line 436, which pins §3 for StatefulSets and is also wrong (they're §6).

2. **Reconcile Chapter 1's "The Voyage Ahead" with this chapter's opening.** Ch 1 lines 580–586 tell the reader: *"Chapter 2 opens with a shipping container. An actual one: corrugated steel, standardized corner fittings… it's why Chapter 2 starts there rather than with a definition. You'll get the definition too. But you'll get it after you can already see why it had to be that way."* This draft opens with "Kubernetes cannot run a container," gives the definition in §1, and delivers the crate in §8. The promised order is inverted. Both chapters are shipped, so a reader meets the contradiction across a page turn. Either revise Ch 1's handoff to promise what §8 actually does (crate as payoff, not premise), or move the crate forward — the former is far cheaper and arguably better, since §8's Zenith earns more as a synthesis than as an opening.

3. **Resolve the `Ch 17 §4` collision** before Ch 17 outlines. Ch 1 line 182 claims it for the certification landscape; Ch 2 lines 600 and 914 claim it for the four pluggable interfaces. Ch 2's claim is load-bearing (it is the Zenith's payoff pointer and appears twice); Ch 1's is a single navigational aside. Recommend Ch 2 wins §4 and Ch 1 line 182 is retargeted.

4. **Fix the frontmatter question count.** Frontmatter declares `practice_questions: 25` and `total_this_chapter: 45`. The body has 27 (verified — Q27 present, and the "seven integrative" claim matches exactly seven `[integrative:]` tags at Q9, 14, 20, 22, 24, 26, 27). Actual total is 47. The Bearings count was updated 10 → 12 during revision but the practice count was not, even though an AUTHOR-REVIEW documents adding "the new integrative Practice Q26." Stage 14 and the book-level 300-question floor both read frontmatter, so this under-counts the book by two.

5. **Decide on Ch 3's Docker-era gap** (finding **C4** above): add the dockershim/Docker-Engine sentences to Ch 3 §1, or soften Ch 2 §4's Snag to stop promising them.

**Should fix:**

6. **§4's ⚓ callout says "Four sockets" after naming five things** — CRI, CSI, CNI, device plugins, and API extensions. The book's canon is four everywhere else (Exam Alert item 5: "CRI, CNI, CSI, and API extensions"; §8: "Storage does it. Networking does it. The API itself does it"; the Chapter Summary's last row). Drop "device plugins" from the callout, or change "Four sockets" to "One design instinct, applied in several places." Worth noting that Ch 17's lineup collects *seven* extension points, so if the four-count is a deliberate simplification it should probably say so.

7. **The §1 AUTHOR-REVIEW's second instruction is stale.** It directs: *"DELETE Chapter 1's parallel AUTHOR-REVIEW at its line ~140 so the two chapters agree before the reconcile pass runs."* No AUTHOR-REVIEW exists at Ch 1 line 140 — Ch 1's remaining comments are at 248, 280, 442, and 584, none about the kernel/OS registers. The question was resolved book-wide on 2026-08-24 and Chapter 3 line 273 records the resolution as *"book-level status — handled here; no further edits elsewhere."* Leaving the instruction in implies a live cross-chapter disagreement that no longer exists. Delete that sentence; keep the A13/A14 harvest request, which is still open.

   Minor related note: Ch 3 line 271 calls the kernel sharpening *"this book's, not the documentation's… our gloss."* Ch 2 §1 presents it as an entailment from `k8s-docs-runtime-class`'s "user-space kernel" phrasing. Both land in the same place for the reader, and Ch 3 explicitly defers to Ch 2, so this is a posture difference rather than a contradiction — but if the A13/A14 snapshots land and Ch 2 gets a direct citation, Ch 3's "our gloss" framing should be revisited.

8. **Pin Ch 11 and Ch 12 section numbers now.** Five cross-bearings from this chapter name sections in undrafted chapters whose lineup ordering contradicts the numbers (table above). The book already has the mechanism — Ch 3's and Ch 4's frontmatter both carry `WARNING SECTION NUMBERING IS LOAD-BEARING` blocks naming the pinning chapter and line. Ch 11 and Ch 12 have no such blocks yet. Separately, `Ch 12 §3 — restricting who can pull what` may be a content gap rather than a numbering one: registry-side pull authorization doesn't appear anywhere in Ch 12's lineup topic list.

9. **Hedge the four unsourced exam-frequency predictions** in §1, §5, §6, and §7 (listed in the guardrails section), so the Exam Alert's closing disclaimer holds chapter-wide.

10. **Add the `manifest` disambiguation clause in §2**, per the terminology section.

**Note only — no action required from this chapter:**

11. §8's containerization-history sourcing gap is the *same* gap Chapter 1 flagged at its line 584 ("Cache an authority during Chapter 2's research pass — Levinson, *The Box*, or ISO 668 — and tag it there"). Two chapters, one fix. Ch 2's AUTHOR-REVIEW correctly identifies ISO 668 / ISO 1161 as the route and notes iso.org returns 403 to WebFetch. Whoever closes this should close both.

12. **Pipeline fault worth escalating.** `.pipeline-state/book-outline/retrieval-architecture.md` on disk is not the B3 artifact — it is a captured "the write is blocked, here's what I would have written" message. The substantive design summary survived inside it and was usable for this check, but the structured artifact is gone. This is the same executor fault this chapter's own AUTHOR-REVIEW documents for Stage 2 ("researched 17 new snapshots… and could not write them to disk"), and Chapter 1 hit it too. Three occurrences across two stages makes it a pipeline defect, not a per-chapter one. The `../Book-KCNA/` write permission is the common factor.

13. Book-level formatting variance, for a later sweep: Voyage Progress uses three emphasis conventions and appears in only 3 of 7 chapters; Safe Harbor appears as an H2 heading in Ch 4 and Ch 6 but inline in Ch 1, 2, 3, 5, and 7. Ch 2 is in the majority on both.