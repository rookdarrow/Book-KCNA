All checks complete. Verified against the seven shipped chapter files on disk, the book outline, prior KB manifests, and the sources tree.

# Integration Check — KCNA Chapter 8

**Note on method.** The prompt supplied no knowledge-base shards (`[no knowledge-base shards tagged]`), and `Book-KCNA/knowledge-base/` does not exist — the ch-07 manifest confirms every KB row for Ch 1–7 is still sitting unapplied inside seven manifests. Rather than declare callbacks unverifiable, I checked them against the **shipped chapter files on disk** (`chapter-01` … `chapter-07`), `book-outline/arc-outline.md`, `book-outline/domain-analysis.md`, the seven prior `kb-manifest.md` files, and `sources/`. Nothing below is inferred; every callback verdict cites a line I read.

## Summary

- Terminology consistency: **fail**
- Callbacks to earlier chapters: **34 correct / 7 incorrect**
- Retrieval-practice accuracy: **pass** (all 6 tags point at chapters that cover the material) — but the retrieval *rate* misses the outline's target; see below
- Glossary coverage: **41 concepts introduced, 32 defined in-chapter, 9 require glossary entries**
- Contradictions with earlier canon: **1 flagged**
- Ethical guardrails (skill Part 14): **pass**

---

## Terminology consistency

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| kubelet | `kubelet` (lowercase) | 53 | No — 0 capitalised |
| API server / kube-apiserver | `kube-apiserver` for the component, "API server" in prose | 22 / 54 | No — matches Ch 3 §2/§5 usage |
| ResourceQuota | `ResourceQuota` (object); "resource quota" only when quoting the namespaces snapshot | 30 / 2 | No — both lowercase uses are inside the sourced sentence, as in Ch 4 §3 |
| LimitRange | `LimitRange` | 27 | No |
| etcd | `etcd` (always lowercase) | — | No |
| control plane / control-plane | two words as noun, hyphenated as adjective | 44 / 29 | No — hyphenated uses are all adjectival |
| **node controller** | unsettled book-wide | 11 lowercase + **1 capitalised** | **Yes** — Chapter Summary row (L1184) reads "Node controller"; body uses "node controller" 11×. Ch 3 uses "**Node** controller" ×5; Ch 7 uses "node controller" ×2 and "**node lifecycle** controller" ×2. ch-07's manifest already registered this as "⚑ gap — three casings, one referent; see G7/T2" |
| **admission category** | should be one headword | `admission control` ×6, `admission controllers` ×6, `admission gate` ×2, `admission plugin` ×1/×2, `policy plugin` ×1 | **Yes** — six surface forms. Ch 7's manifest states the category is "undefined until Ch 8," so this chapter owns the headword and does not fix it. `policy plugin` (Bearings #1 item 4 key) is a seventh coinage anchored to nothing |
| StorageClass | plural in Ch 4 §3 | `StorageClass` ×1 (§3), `StorageClasses` ×1 (Exam Alert) | **Yes**, minor — internally inconsistent; Ch 4 §3 and the source both use the plural |
| **British spellings** | American — Ch 1–6 are at **zero** | **26 occurrences across 23 lines** | **Yes — ship-blocking regression** |

### The spelling regression is the fail

`behaviour` ×6 · `memorising` ×4 · `memorised` ×3 · `memorise` ×3 · `memorisation` ×3 · `favour` ×2 · `Recognise` ×1 · `organise` ×1 · `organisations` ×1 · `licence` ×1 · `defence` ×1.

Chapters 1–6 contain **zero** instances. Chapter 7 introduced 3 (by this pattern set; its own integration gate counted 23 by a wider one) and **shipped without the fix** — the ch-07 manifest records T1 as still outstanding in the finalized file. Chapter 8 now has 26. This is the second consecutive chapter and the count is growing, so it is no longer a one-off slip; it is becoming the book's house style by default.

Most conspicuous instances, all reader-facing:

- **L126** — `**Recognise**` is a bolded verb in *What You'll Learn*, sitting in a list whose other five verbs (Decompose / Trace / Distinguish / Take / Name / State) are spelling-neutral. Highest-visibility instance in the chapter.
- **L1151** — `licence` used as a noun ("not a licence to run one ahead"). Ch 7's gate flagged the identical word.
- **L965** — "the exam does not organise itself by chapter section" (Practice Questions preamble).
- **L598** — "plenty of organisations have excellent reasons" (Logbook Entry).
- **L1154** — "a thin defence for something this valuable" (Q17 explanation).

Roughly three `behaviour` instances sit inside AUTHOR-REVIEW comments and will vanish with them; the remaining ~23 will ship. Per the repo's own gotcha list, fix with a Python script, not the Edit tool.

### Metadata-line format drift — and the fix for a BLOCKING fact-accuracy item

The chapter's metadata line diverges from a format that Chapters 2, 5, and 7 already share verbatim:

> **Ch 7 (L174):** `**Exam domain: Kubernetes Fundamentals (44% of the exam) — competency: Scheduling** [source: cncf-kcna-certification-page-2026-08-23] [source: cncf-kcna-curriculum-pdf-2026-08-23] **| Estimated share of the exam: ~5% (authored allocation — CNCF publishes domain weights, not competency weights** [source: cncf-kcna-curriculum-pdf-2026-08-23]**; see front matter) | Complexity: Mixed | Novelty: Moderate**`

> **Ch 8:** `**Domain: Kubernetes Fundamentals — 44% of the exam · Competency: Cluster Administration — ~5% (authored allocation) · Complexity: Mixed · Novelty: Moderate**` — plus a separate italic footnote, and **no source tags**.

Differences: `Exam domain:`→`Domain:`, `competency:`→`Competency:`, `|`→`·`, the inline authored-allocation parenthetical demoted to a standalone paragraph, and both source tags dropped.

**This resolves the chapter's most consequential open BLOCKING item at zero research cost.** The fact-accuracy audit flagged three unattested claims on this line — the 44% figure, the domain name, and the "four domains" count. All three are book canon:

- `domain-analysis.md:37` — "**D1 — Kubernetes Fundamentals** | **44%** | D1.1 Kubernetes Core Concepts · D1.2 Administration · D1.3 Scheduling · D1.4 Containerization"
- `arc-outline.md:48` — "D1 7 (41.2%) · D2 5 (29.4%) · D3 3 (17.6%) · D4 2 (11.8%)" — four domains, D1–D4
- Chapters 2, 5 and 7 each print "Kubernetes Fundamentals (44% of the exam)" tagged to **both** `cncf-kcna-certification-page-2026-08-23` and `cncf-kcna-curriculum-pdf-2026-08-23`

Both snapshots are **on disk now** (confirmed in `sources/`, 137 files). Adopting Ch 7's line verbatim tags the name and the percentage, and its wording ("CNCF publishes domain weights, not competency weights") drops the "four domains" count entirely — eliminating the third claim rather than sourcing it.

One residual: Ch 8 names the competency **"Cluster Administration"**; `domain-analysis.md` calls D1.2 **"Administration"**, and Ch 2/5/7 each use the domain-analysis name exactly (`Containerization`, `Kubernetes Core Concepts`, `Scheduling`). Use "Administration" for consistency, or ratify "Cluster administration" (the `arc-outline` form) across all four.

---

## Callback correctness

I checked 41 cross-chapter references: 21 cross-bearings pointing outside the chapter, 20 prose callbacks. (Four further cross-bearings are intra-chapter — Ch 8 §2/§4/§5/§8 — and all four resolve correctly.)

### ⚑ Six cross-bearings carry the wrong section number

This is the same defect class ch-07's gate escalated as **C1** ("`chapter-06:965` points at 'Ch 7 §5' for taints. Should be `§4`"). Here it is six times, and it clusters on two chapters.

**Chapter 3** — actual structure: §1 How the Cluster Got the Shape It Has · **§2 The Control Plane** · §3 Node Components in Context · §4 Addons · **§5 The Only Door In** · **§6 Controllers and the Control Loop** · §7 Nobody Is in Charge.

| Location | Draft says | Should be | Evidence |
|---|---|---|---|
| Soundings answer rubric | `Ch 3 §2 — the API server as the single door` | **§5** | §5 is titled "The Only Door In" and carries the hub-and-spoke sentence (L614) |
| §4, node controller | `Ch 3 §5 — the control loop` | **§6** | §6 is "Controllers and the Control Loop"; §5 contains no control-loop material |

Both errors are self-evidently wrong in context because **§2 §7 both cite Ch 3 §5 correctly** for the door, and §7 cites **Ch 3 §2 correctly** for etcd (verified: Ch 3 §2 has a `### etcd` subsection at L400). So each of the two section numbers is used for two different topics inside one chapter — at most one of each pair can be right, and the draft happens to get one right and one wrong in each case.

**Chapter 4** — actual structure: §1 You File a Declaration · §2 The Anatomy of a Record · **§3 Where a Name Lives** · §4 Configuration Kept Outside the Image · §5 The Universal Join · **§6 A Declaration, Not an Order**.

| Location | Draft says | Should be | Evidence |
|---|---|---|---|
| Soundings rubric | `Ch 4 §6 — namespaces and cluster-scoped objects` | **§3** | Ch 4 §3 L540 carries the namespaced/cluster-scoped ★ Fixed Point |
| §3, the hinge | `Ch 4 §6 — namespaces, and what they are for` | **§3** | Ch 4 §3 L524: "Namespaces are intended for use in environments with many users…" |
| §4, heartbeats | `Ch 4 §6 — the four initial namespaces` | **§3** | Ch 4 §3 L570: "### The four initial namespaces" |
| §1, apply | `Ch 4 §2 — apply, and the declarative model` | **§1** (and see below) | Ch 4 §1 L317: "The verb you will use to submit a record is `kubectl apply`… the full command surface… belongs to Chapter 8" |

The §1 case is a double miss worth calling out. Ch 8 §1 pairs that cross-bearing with the sentence *"Chapter 4's larger point stands unchanged: the objects are declarations, and the imperative verbs work by changing declarations."* That claim is Ch 4 **§6**'s payoff verbatim (L995: "**The objects are declarations, and the imperative commands work by changing declarations.** That is the accurate claim, narrower than the chapter subtitle and better"). So the paragraph needs two pointers — §1 for `apply`, §6 for the declarations claim — and currently has one, aimed at neither.

The fourth `Ch 4 §6` cross-bearing, in §8 ("the habit of narrowing a claim until it is true"), is **correct** — §6 is exactly where Ch 4 performs that narrowing.

### ⚑ One prose callback is factually wrong

*Why This Chapter Matters:* **"Chapter 7 ended by naming that command, telling you it was this chapter's opening move, and declining to explain it."**

The string `cordon` appears **zero times in Chapters 1–7**. Chapter 7 named the *act* and the *taint*, not the command:

> Ch 7 L1295: "In §4 you met a built-in taint called `node.kubernetes.io/unschedulable`… **The command that does it**, the command that clears the node out afterwards… that's Chapter 8."

Chapter 7 conspicuously withholds the command name — that is the setup Ch 8's cold open is paying off. Ch 8 §1 gets this right ("the thing Chapter 7 promised would be Chapter 8's opening move"); only the *Why This Chapter Matters* phrasing overstates it. Fix: "Chapter 7 ended by promising that command…" or "…by naming the act and withholding the command."

### The other 34 verify clean

Spot-checks worth recording because they are unusually precise and all hold:

- **§1: "Chapter 4 used the second half of that fact once, in passing, in an answer key."** ✓ Ch 4 L1234, inside a Practice Question explanation: "the ServiceAccount's namespace when `kubectl` runs inside the cluster."
- **§2: "Chapter 3 named them in passing, at the point the API server was introduced, and pointed here."** ✓ Ch 3 L671 is the *only* mention of authentication/authorization/admission in all of Chapter 3, and it is a forward cross-bearing sitting at the end of §5 — so both the "in passing" characterisation and the `Ch 3 §5` pointer are exactly right.
- **Soundings Q5 (Ch 7 taint table)** ✓ Ch 7 L693 table row `node.kubernetes.io/unschedulable | NoSchedule`; L1295 confirms "it wasn't put there by a failing disk."
- **§8: "Chapter 7 closed by saying this chapter is where the rules turn into consequences."** ✓ Ch 7 L1297, verbatim.
- **§3 → Ch 5 §8, §4 → Ch 7 §2, §2 → Ch 7 §3, §1 → Ch 7 §4, §4 → Ch 6 §7, §5 → Ch 7 §6, §5 → Ch 2 (CRI)** — all ✓.
- **Forward pointers to Ch 12, 13, 17** — all ✓ against `arc-outline.md`, and two are *mandated* there: Ch 13's anchor list requires "**version skew (Ch 8)** as a troubleshooting cause," and Ch 17's requires "release cadence + version skew (Ch 8)." Both are delivered. Ch 12's entry requires the "Ch 8 admission gate," and `arc-outline.md:60` confirms the reciprocal.
- **Reciprocity** — three earlier chapters point *into* Ch 8 and all three are answered: Ch 3 L440 ("see Ch 8 — etcd backup and restore in practice") → §7 ✓; Ch 4 L586 ("see Ch 8 — node conditions and heartbeats") → §4 ✓; Ch 4 L592 ("see Ch 8 — ResourceQuota") → §3 ✓ (thinly — see glossary); Ch 4 L317 ("see Ch 8 — kubectl, in full") → §1 ✓; Ch 7 L519 ("see Ch 8 — admission control") → §2 ✓.

One unverifiable claim, noted not flagged: §4's "you have seen five instances of it since" (the control-loop count). Chapter 6 alone plausibly supplies five. Author's call.

---

## Retrieval-practice accuracy

**Every tag points at a chapter that covers the material — accuracy passes.**

| Item | Tag | Verified against |
|---|---|---|
| Bearings #1 item 5 | `ch4` | Ch 4 §3 L592 — namespaces divided "via resource quota" ✓ |
| Bearings #2 item 1 | `ch7` | Ch 7 §4 L693/L702 — the taint table and its semantics ✓ |
| Bearings #2 item 4 | `ch2` | Ch 2 §4 "The Container Runtime Interface" ✓ |
| Practice Q6 | `ch4` | Ch 4 §3 L540 — Nodes are cluster-scoped ✓ |
| Practice Q7 | `ch5` | Ch 5 §8 L872 — "the kube-scheduler uses this information to decide which node to place the Pod on" ✓ |
| Practice Q11 | `ch3` | Ch 3 §6 — control loop ✓ |

Two notes that resolve open flags:

- **Q7's attribution is sound.** The draft's own AUTHOR-REVIEW calls "requests are the number the scheduler filters on" unverifiable. It is verifiable at book level: Ch 5 §8 L872 states it, sourced to `k8s-docs-resource-management-2026-08-23` (on disk), and Ch 7 §2 L374 restates the handoff. Adding that snapshot to this chapter's referenced set closes the flag with no fetch.
- **Both ≥4-back anchors are satisfied.** `arc-outline.md:414` requires "**Ch 2 CRI or Ch 3 control loop**" for Ch 8; the chapter delivers *both* (Bearings #2 item 4, Practice Q11).

### ⚑ The retrieval *rate* misses the target

`arc-outline.md:414` sets Chapter 8 at **20%**, drawing from Chapters 3–7.

Actual: **6 tagged items of 33** (Bearings 5+5+5 = 15, Practice = 18) = **18.2%**. Below floor.

The draft's own accounting note states "6 of 34 = 17.6%" — the denominator is off by one; there are 33 Bearings+Practice questions, not 34. The conclusion is unchanged either way.

**The cheapest fix is already in the chapter and needs no fetch.** `arc-outline.md:414` names two mandatory anchors for Ch 8: "Namespaces under ResourceQuota" (delivered, tagged ×2) and "**node conditions**" — which is the Ch 4 `kube-node-lease` handoff, since Ch 4 §3 L586 is what forward-points here. Chapter 8 delivers it as **Bearings #2 item 5** (the two heartbeat forms and which namespace holds the Leases) but leaves it **untagged**, on the reasoning that it tests §4's own material.

Tagging that item `[retrieval: ch4]` gives **7/33 = 21.2%** — inside the 20–25% band — *and* discharges the outline's second mandatory anchor as a labelled retrieval item. It is defensible on the merits: the item's second half ("say which namespace holds the objects the second one uses") is answerable only from Ch 4 §3's four-namespace table, and the answer key already credits Ch 4 explicitly.

This is preferable to the two fixes the draft proposes for itself, both of which are contingent — one on a snapshot that has not landed, the other on adding a new question.

---

## Glossary coverage

Following stage rule 4 (**yes** = introduced and used without a definition a reader could be graded on). Per the ch-07 manifest precedent, Stage 14 additionally contributes the full introduced-term set to satisfy Part 16's 100-term floor; the column below is the definitional-gap subset only.

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| `kubectl [command] [TYPE] [NAME] [flags]` grammar | yes | no |
| kubeconfig; `KUBECONFIG`; `--kubeconfig` precedence | yes | no |
| in-cluster configuration (the three checks) | yes | no |
| `kubectl explain` / `config` / `cordon` / `drain` / `uncordon` | yes | no |
| `kubectl logs` / `exec` | named only — deferred to Ch 13 | no (Ch 13 owns) |
| authentication (gate) · authorization (gate) | yes | no |
| admission control / admission controller | yes — but under six surface forms | no (needs one headword + variants) |
| NodeRestriction admission plugin | yes — **closes Ch 7's registered partial** ("category undefined until Ch 8") | no |
| **dynamic admission control / admission webhook** | partial — mechanism sketched, neither mutating nor validating named | **yes** |
| RBAC · Pod Security Admission · SIG Release / KEP · scheduler profiles | named only — deferred to Ch 12 / Ch 17 / Ch 7 | no |
| **auditing** | thin functional gloss only; the chapter's own PARTIAL objective (D1.2-08) | **yes** |
| **ResourceQuota** | scope stated; what it counts, the rejection behaviour, and the requests-must-be-specified rule all absent | **yes** |
| **LimitRange** | partial — function stated, min/max/default structure absent | **yes** |
| Node object; node self-registration | yes | no |
| node conditions (all five, `Ready`'s three values) | yes | no |
| **`node-monitor-grace-period`** | named only; value deliberately withheld | **yes** |
| Lease / `kube-node-lease` | yes | no |
| node controller | yes — **closes Ch 7's registered ⚑ gap** | no (but reconcile casing/alias) |
| **node `Capacity`** | **no — the definition was cut in revision** | **yes ⚑ inherited** |
| `Allocatable` | yes (sourced) | no |
| kubeadm · kind · minikube · k3s | yes | no |
| container runtime · containerd · CRI-O · CRI | yes (CRI owned by Ch 2 §4) | no |
| version skew; `x.y.z`; release branch; patch support; release cadence | yes | no |
| `etcdctl snapshot save` / `etcdutl snapshot restore` | yes | no |
| hub-and-spoke API pattern | yes | no |
| **kubelet TLS bootstrapping** | named only — nothing in the book defines it | **yes** |
| **bearer token** | used as a term, undefined here and earlier | **yes** |
| **managed vs self-hosted duty split** | narrowed in revision to "a per-provider question" | **yes**, low priority |

### Two inherited debts, both traceable to ch-07's manifest

**1. `node Capacity` is now undefined anywhere in the book.** ch-07's manifest recorded it as "⚑ **gap** — cross-ref Ch 8," on the strength of Ch 7's own deferral ("What makes the two differ, and how it's configured, is Chapter 8's material"). Chapter 8 was correct to cut the arithmetic — `k8s-docs-node-allocatable-2026-08-24` forbids stating the relationship — but the effect is that a term Ch 7 explicitly handed forward has now been dropped by its designated owner. The chapter's own note identifies the honest two-sentence discharge (`kube-reserved` / `system-reserved` plus the motivation sentence) sitting unwritten in `research-manifest.md`. Until that lands, **Ch 7's pointer should be softened from a promise to a deferral**, or the debt carried explicitly into the glossary.

**2. `PriorityClass` remains unowned.** ch-07's gate escalated this as **G4** — "no owner anywhere in the book or the lineup. Glossary row at minimum; **possibly a line in Ch 8**." Chapter 8's §3 scope guard explicitly declines it ("do NOT take … priority-class quota — all above associate tier"), and the term appears in this chapter only inside that comment. The scope call is defensible; the consequence is that G4 needs a glossary row, since no chapter will now define it.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims** — The chapter is unusually disciplined here. Exam Alert states outright: "None of them is dressed up with an invented statistic, because nobody publishes one," and labels its own priority ordering "authored judgement, not a published ranking." The metadata line's `~5%` is marked "(authored allocation)" with the derivation explained. The `44%` is book canon, untagged (see fix #1) — a missing citation, not a fabrication.
- [x] **Fear-based content uses real examples** — §4's Navigational Hazard (cordon-then-reboot drops running Pods) is a genuine, documented failure mode, presented soberly and without embellishment. §7's etcd-snapshot-as-root-credential is sourced twice.
- [x] **Simplification acknowledged** — Strongly. §4 ("above the associate tier and this book does not cover it"), §6 ("That is as far as this book goes"), §2's auditing block, and above all §8's dedicated *"Where the claim overreaches"* subsection, which retracts the chapter's own thesis to the version that survives contact with the exam. That is Part 11's order/truth pattern executed properly. A formal — Dead Reckoning block carries §6's skew table.
- [x] **Authority claims cite legitimate sources** — All inline tags resolve to cached kubernetes.io snapshots. The three untagged clusters are already flagged by the fact-accuracy stage; I confirmed on disk that the ten "landed-but-unwritten" snapshots are **still absent** from `sources/` (137 files, none matching controlling-access / resource-quota / limit-range / reserve-compute / node-status / audit), so those AUTHOR-REVIEW notes are accurate, not stale.
- [x] **"Frequently tested" claims verifiable** — The chapter consistently marks exam-weight claims as authored judgement rather than published fact. One borderline line, below.
- [x] **No strawmanning of alternative study methods** — **The ch-07 E1 pattern does not recur.** Chapter 7 failed this on "most study guides present [scheduling] as a catalogue of six unrelated features." Chapter 8's nearest neighbour is §8's "A list of administrative rules is among the least memorable material *any* study guide can put in front of you" — which is self-inclusive, and immediately self-implicating ("and this chapter contained a great many of them"). That is the opposite move. Safe Harbor is clean.
- [x] **Subject dignity (v5.7)** — Every wry beat is aimed at practitioners: the debugging-shell surprise in §1, "teams that priced the machines and not the Thursdays" in §5, "*ballast*, not *lifeboat*" in §7. Bearings #2 item 2 ("three services go down") is framed as the engineer's error and immediately normalised — "you got it wrong for a sensible reason" — not as a joke about the outage.

**One borderline line, recommend softening.** Exam Alert: *"Common traps. **Each of these catches real candidates.**"* This is an unverifiable empirical claim about candidate behaviour, presented as fact, in a sentence that then disclaims statistics. It is not a strawman and not inflation, so it does not fail the checklist — but it sits outside the register Chapter 1 established and that ch-07's gate cited approvingly as the standard (a verifiable, mechanical test the reader can run, or an acknowledged authorial judgement). Suggested: *"Each of these is an error the material makes easy to commit."*

The same register applies to a cluster of softer claims — §2's "the answer nearly everyone produces," and several answer keys' "the most common error." These are ordinary pedagogical judgement and are consistent with how the earlier chapters speak; I flag them only as the boundary, not as findings.

---

## Recommended fixes

Everything the revision stage already caught — the three BLOCKING source gaps, the Capacity/Allocatable cut, the Q10 and Q13 rewrites, the anchor-numbering mismatch — is omitted here. These are additional.

**Ship-blocking**

1. **Conform the metadata line to Ch 7 L174's format.** Copy the structure and **both** source tags (`cncf-kcna-certification-page-2026-08-23` + `cncf-kcna-curriculum-pdf-2026-08-23`, both on disk). This closes all three of the fact-accuracy stage's BLOCKING metadata claims at once — and Ch 7's wording ("CNCF publishes domain weights, not competency weights") eliminates the "four domains" count rather than needing to source it. Change "Cluster Administration" → "Administration" to match `domain-analysis.md` and the Ch 2/5/7 precedent.

2. **Fix the six wrong cross-bearing section numbers** (§ Callback correctness above): Ch 3 §2→§5 (Soundings rubric); Ch 3 §5→§6 (§4, control loop); Ch 4 §6→§3 ×3 (Soundings rubric, §3 hinge, §4 heartbeats); Ch 4 §2→§1 (§1, `apply`) — and add a second pointer to Ch 4 §6 for the "objects are declarations" claim in the same paragraph. Same defect class as ch-07's C1; use a script, not the Edit tool.

3. **Correct "Chapter 7 ended by naming that command."** Chapter 7 deliberately withholds `cordon` (0 occurrences in Ch 1–7). Change to "promising that command" / "naming the act and withholding the command."

4. **British spellings — 26 occurrences, 23 lines.** Second consecutive chapter; Ch 1–6 baseline is zero. Priority: L126 `Recognise` (bolded, in *What You'll Learn*), L1151 `licence`, L965 `organise`, L598 `organisations`, L1154 `defence`, then the `memoris*` and `behaviour` families. Python script; reconfigure stdout to UTF-8.

**Should fix**

5. **Tag Bearings #2 item 5 as `[retrieval: ch4]`.** Lifts retrieval from 18.2% to 21.2% (inside the outline's 20–25% band) *and* discharges `arc-outline.md:414`'s second mandatory anchor ("node conditions"). Needs no fetch and no new question. Correct the accounting note's denominator from 34 to 33 while there.

6. **Settle the admission-category headword.** Keep "admission controller" as the category, reserve "admission plugin" for named plugins (NodeRestriction, per Ch 7's sourced phrasing), and drop "policy plugin" from Bearings #1 item 4's key. This chapter is the category's designated owner per ch-07's manifest.

7. **Settle the node-controller casing.** Chapter Summary L1184 reads "Node controller" against the body's 11 lowercase uses. Because §4 is where the book defines it, add the alias in one clause — "the node controller (also called the node lifecycle controller)" — which closes ch-07's registered G7/T2 three-casings gap. Note Ch 3's five capitalised instances will need a sweep to match whichever form is ratified.

8. **`StorageClass` → `StorageClasses`** in §3, matching Ch 4 §3 and the Exam Alert row.

**Author decision**

9. **Scope the single-door claim to match Ch 3.** *This is the one canon contradiction.* Ch 3 §5 was deliberately narrowed after author review, and its surviving note records why: "A1 documents outbound API-server→kubelet paths (logs, attach, port-forward) that this figure does not draw, so the figure and §5 are now explicitly scoped to the **state/API path**." Chapter 8 restates the claim unscoped — §2's "There are not [other doors]" and Figure 8.6's "There are no side channels" — and §1's own verb table lists `logs` and `exec` two sections earlier. The three-gates argument is unaffected (those paths originate *at* the API server; all inbound API usage still terminates there), so this is a scope-of-phrasing issue, not a false statement. But Ch 8 currently asserts more than the chapter it inherits from, and supplies its own counterexample. Recommend scoping both to inbound API usage. **Ch 8's etcd-access modality was checked separately and complies** — it preserves Ch 3's "ideally… should" hedge throughout (§7 prose, §7 Fixed Point, §8), so Ch 3's "do not restore the absolute phrasing" instruction is respected.

10. **`node Capacity` is an inherited gap Ch 8 was designated to close and no longer does.** Either land the reserve-compute snapshot and add the two sourced sentences, or soften Ch 7's promise to a deferral. Do not leave a forward pointer aimed at a definition that was cut.

11. **`PriorityClass` (ch-07 G4) still has no owner.** Ch 8 explicitly declined it on tier grounds. Needs a glossary row, or a nominated chapter.

12. **Soften "Each of these catches real candidates"** (Exam Alert) to a claim the reader can check or that reads as authorial judgement.

13. **Carry-over from ch-07, unresolved here:** that gate suggested retargeting Ch 7's orphaned `Ch 12 — workload isolation` forward pointer to Chapter 8 as the closer fit. Chapter 8 does not absorb it (it touches node-isolation labels in §2 only). Still needs an owner.

**Note for the author, not a fix:** the twenty-odd AUTHOR-REVIEW comments in this draft are all live and accurate — I verified the largest claim among them, that the ten closing-fetch snapshots never landed, directly against `sources/`. Per ch-07's C2 finding, they must be resolved and deleted before ship rather than carried into the finalized chapter.