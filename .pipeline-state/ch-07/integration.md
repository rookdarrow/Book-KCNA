Verification is complete. I read the shipped `chapter-01` … `chapter-06` directly (the stage prompt passed `[no knowledge-base shards tagged]`, and Chapter 6 has shipped since the last integration run), plus the book outline's `chapter-lineup.md` and `retrieval-architecture.md`, and every inbound cross-bearing that points at Chapter 7.

Per the `--allowed-tools` contract in CLAUDE.md, emitting to stdout for the orchestrator rather than writing the file myself.

```markdown
# Integration Check — KCNA Chapter 7

**Draft audited:** `.pipeline-state/ch-07/draft-v2.md` (1,143 lines, 2026-08-24 15:41)
**Verified against:** shipped `chapter-01` … `chapter-06`; `.pipeline-state/book-outline/chapter-lineup.md`; `.pipeline-state/book-outline/retrieval-architecture.md`; every inbound cross-bearing that names Chapter 7.

**Note on inputs.** The stage prompt passed `[no knowledge-base shards tagged]`, so nothing below is inferred from shards. Every callback is verified against real shipped text and cited by line number. **Chapter 6 shipped at 15:01 today** (`chapter-06-fleets-not-vessels.md`, 1,468 lines), which retires the largest unverifiable block in the previous integration run — both Chapter 6 back-bearings now check out against real headings.

---

## Summary

- Terminology consistency: **fail** — one systematic drift (British spellings, 23 prose instances, against a corpus that is uniformly American), plus two minor casing items
- Callbacks to earlier chapters: **19 correct / 0 incorrect** (8 back-bearings + 11 forward; 1 forward pointer soft — see Ch 12 below). One **inbound** pointer from Chapter 6 is wrong and cannot be fixed from inside this chapter.
- Retrieval-practice accuracy: **pass** — 7 tagged items, 7 verified, 21% of graded items (B3 band is 20–25%)
- Glossary coverage: **60 concepts/commands introduced, 49 defined in-chapter, 11 require glossary entries**
- Contradictions with earlier canon: **none** — 2 near-misses recorded, both benign
- Ethical guardrails (skill Part 14): **fail** — one item, guardrail #3, unchanged since draft-v1

**Two things worth saying before the detail.** First, the fact-accuracy findings that the previous integration run reported as unapplied *have been applied*: the unsourced absolute negative ("the scheduler never consults observed usage") is gone from prose everywhere it appeared, the untagged Capacity/Allocatable relationship in §2 has been replaced with a sourced Allocatable treatment and a deferral to Chapter 8, the `node.kubernetes.io/unschedulable` causal claim now carries `[source: k8s-docs-nodes-2026-08-23]` at both sites, and the metadata line matches the ch-02 / ch-05 house form byte-for-byte. This draft is in materially better shape than the one that failed this gate at 10:49.

Second, the single ethical finding from that run **survived unedited**. It is one sentence and the fix is one sentence. See Finding E1.

---

## Terminology consistency

| Term | Canonical form (evidence) | Occurrences in this chapter | Drift? |
|---|---|---|---|
| American spelling generally | `behavior` ×46, `recognize` ×8, `judgment` ×7, `utilization` ×3, `organiz*` ×7, `neighbor(s)` ×2, `minimized`, `optimization`, `Prioritize`, `license` ×3 — ch01–ch06 | 23 British forms in prose | **YES — see Finding T1** |
| `kubelet` (lowercase) | ch03 §3, ch05 §8 | 45 | no — zero `Kubelet` anywhere |
| `kube-scheduler` | ch03 §2 L413 | 46 | no |
| `Pod` (capitalized resource noun) | ch05, ch06 | 249 `Pod` / 123 `Pods`; the 61 lowercase are inside `[source: k8s-docs-pod-*]` tags and verbatim doc quotes | no — same pattern as ch05/ch06 |
| `` `Pending` `` (backticked) | ch05 L579/L670/L704, ch06 | backticked throughout | no |
| `DaemonSet`, `ReplicaSet` | ch06 §1, §7 | 19 / 5 | no |
| `nodeSelector` (code-formatted) | new here; ch04 L834 names the concept | 47 | no |
| control plane / control-plane | ch03: 36 noun / 31 adjectival | same split | no |
| Node controller | ch03 L421 writes **`Node controller`** (capital N) | ch07 writes `node controller` (§4) and `node lifecycle controller` (§4, TYB2 A3) | **minor — see Finding T2** |
| Pod affinity / pod affinity | book capitalizes `Pod` as a resource noun | `Pod affinity` ×4, `pod affinity` ×5 (some inside verbatim doc quotes, which legitimately lowercase it) | **minor — see Finding T3** |
| `Allocatable` | zero occurrences in ch01–ch06 | first use in the book | n/a — new term, glossary row exists |
| Metadata-line house form | ch02 L132 and ch05 L190 use the long form with both CNCF source tags inline | identical form, `~5%`, competency `Scheduling` | no — **and the 44% figure and the competency name `Scheduling` are both confirmed in `sources/cncf-kcna-curriculum-pdf-2026-08-23.md:13`**, which closes the draft's own metadata AUTHOR-REVIEW open item |

### Finding T1 — British spellings, systematic, against a uniformly American corpus (**fix before ship**)

The shipped corpus is unambiguous: 46 `behavior`, 8 `recognize`, 7 `judgment`, 3 `utilization`, 1 `minimized`, 1 `optimization`, 2 `neighbor(s)`, 3 `licens*`. The one counter-example in six chapters is a single `labelled` at ch04. Chapter 7 inverts the convention.

23 instances across 19 lines of shipping prose (plus 4 more inside `AUTHOR-REVIEW` comments, which persist in the shipped file per ch05/ch06 practice):

| Line | Token | Line | Token |
|---|---|---|---|
| 32 | judgement | 696 | recognise |
| 68 | behaviour | 755 | behaviour |
| 114 | Recognise | 1009 | neighbouring |
| 130 | recognise | 1016 | minimise |
| 336 | internalised | 1056 | behaviour ×2 |
| 370 | prioritised | 1058 | optimise |
| 380 | labelled | 1070 | behaviour |
| 489 | behaviour | 1074 | neighbourhood |
| 568 | organisation, licence | 1076 | prioritising, minimise ×2 |
| 660 | labelled | | |
| | | *(comments: 212 utilisation; 869 organising, behaviours, behaviour)* | |

Two of these are worse than cosmetic:

- **L568** puts `licence` (British noun) in the same sentence as the taint key `license=cad`. A reader scanning for the label sees two spellings of the same word one clause apart.
- **L703 vs L1016/L1076** spell *the same documented sentence* two different ways. §5's table quotes the source correctly — "prioritizing nodes that minimize the skew" — and Practice Q14's option D and answer key paraphrase it back as "minimise" / "prioritising nodes that minimise the skew". A reader comparing the table to the answer key sees the source sentence change spelling.

Mechanical fix, low risk. Per CLAUDE.md, do it with a Python script rather than the Edit tool.

### Finding T2 — `Node controller` vs `node lifecycle controller` (minor)

Chapter 3 L421 introduces "the **Node** controller (noticing and responding when…)" with a capital N. Chapter 7 §4 writes "the control plane, using the node controller, automatically creates taints…" and, three paragraphs later, "the **node lifecycle** controller evicts them". Both are upstream doc terms and neither is wrong, but a reader who memorized Chapter 3's list now meets two lowercase variants and has no way to know whether "node lifecycle controller" is the same thing they already met. One clause fixes it — or a glossary row (see G7 below).

### Finding T3 — `Pod affinity` / `pod affinity` (minor)

Four capitalized, five lowercase. Some lowercase instances are inside verbatim quotes from the upstream docs (§5's ⚑ Closer Look quote, and the `podAffinity` field name) and must stay. The prose ones — notably Practice Q13's answer key, "pod affinity is evaluated after taints" — should match §5's own bolded "**Pod affinity attracts**". Same for "Inter-pod" vs "Inter-Pod" outside quotes.

---

## Callback correctness

### Back-bearings out of this chapter — 8 of 8 correct

| Line | Callback | Verified against | Verdict |
|---|---|---|---|
| 122 | Ch 3 §2 — the control plane components | ch03 L354 `§2 — ⚪ The Control Plane`; L411–415 is the `kube-scheduler` entry, and L417 is Chapter 3's own reciprocal pointer forward. The claim that Chapter 3 "told you, in as many words, that *how* it chooses was being held back" is exact. | ✅ |
| 192 | Ch 5 §4 — the Pod's lifecycle | ch05 L525 `§4 — Scheduled Once, Replaced Never` | ✅ |
| 204 | Ch 5 §8 — requests and limits | ch05 L864 `§8 — What a Pod Is Owed`; L969 states verbatim "requests are the input to the scheduler's filtering step" and carries the reciprocal pointer to **Ch 7 §2** | ✅ (and reciprocity discharged at the pinned section) |
| 232 | Ch 5 §8 — QoS classes | ch05 L930–L958 define the QoS classes and their role in eviction ordering | ✅ |
| 242 | Ch 2 §7 — RuntimeClass | ch02 L787 `§7 — 🟡 Not All Isolation Is Equal: RuntimeClass`; L807 promises "the reasoning behind them arrives later" for both overhead and scheduling constraints | ✅ |
| 334 | Ch 4 §5 — labels and selectors | ch04 L776 `§5 — 🔵 The Universal Join` — so "Chapter 4 taught label selectors as the universal join" is the section's literal title. L834 lists exactly **four** uses (ReplicaSet, Service, node scheduling constraints, NetworkPolicy), so "one of the four things they're used for" is exact. | ✅ |
| 536 | Ch 6 §7 — DaemonSets | ch06 L878 `§7 — One Per Node, and Work That Ends`; L894 is the matching promise — "you have already met the mechanism that makes this possible, in disguise… Chapter 7 unmasks it" — in near-identical wording | ✅ (best reciprocal pair in the chapter) |
| 635 | Ch 6 §1 — Deployments and ReplicaSets | ch06 L306 `§1 — The Resource That Holds the Intent`; L316–L320 introduce Deployment → ReplicaSet → Pod | ✅ |
| 899 | Ch 3 §2 — the control plane (Exam Alert) | ch03 L979 defuses "The scheduler places the Pod on the node" explicitly and closes with "(How the scheduler chooses is Chapter 7's.)" — so "you were told it would come back" is literally true | ✅ |

Untagged prose callbacks were checked too and are all accurate: "Chapters 4 through 6 made you someone who can write down what should exist"; "Chapter 3 told you the scheduler selects a node and records that choice" (ch03 L415); "Chapter 2 mentioned that a RuntimeClass can carry a Pod overhead" (ch02 L807). The figure reference `ch05-fig05-requests-limits-qos-classes` resolves — ch05 L938.

**§1's six scheduling factors reconcile with Chapter 3.** ch03 L413 lists six (resource requirements, hardware/software/policy constraints, affinity and anti-affinity, data locality, inter-workload interference, **deadlines**) and Practice Q10 grades the reader on them. §1 reproduces all six and names deadlines separately with its own architecture-overview tag. The unpaid-promise finding from the previous run is discharged.

### Forward pointers — 10 of 11 verified against the chapter lineup

`Ch 8 — node administration` ✅, `quotas and limit ranges` ✅ (lineup: ResourceQuota and LimitRange), `admission control` ✅ (lineup: authentication → authorization → admission), `taking a node out of service` ✅ (lineup: cordon/drain/uncordon), `cluster administration` ✅ (general, acceptable). `Ch 9 — Services and endpoints` ✅. `Ch 13 — reading Pod failure signatures` ✅ and `diagnosing Pending` ✅ (lineup names `Pending` explicitly). `Ch 17 — the cluster's extension points` ✅ and `reacting to unschedulable Pods` ✅ (lineup: Cluster Autoscaler, Karpenter).

The chapter's "last chapter of Part II" claim ✅ — lineup puts Ch 2–8 in Part II and Ch 9 opens Part III.

**⚑ One soft pointer.** `Ch 12 — workload isolation` (§4, on dedicated nodes) has no matching item in Chapter 12's lineup entry, which covers the 4Cs, RBAC, ServiceAccounts, Secrets, Pod Security Standards, `securityContext`, supply chain, policy engines, and sandboxed runtimes. Node dedication as an *isolation* control is a reasonable neighbour of the sandboxed-runtime material but is not currently scoped there. **Author decision:** either add it to Ch 12's scope, or retarget the pointer (Ch 8 is the closer fit, since that's where cordon/taint administration lives).

### ⚑ Finding C1 — an **inbound** cross-bearing from Chapter 6 points at the wrong section

`chapter-06-fleets-not-vessels.md:965` reads:

> `*[cross-bearing: see Ch 7 §5 — a DaemonSet's Pods still go through scheduling, and taints are how a node opts out]*`

Chapter 7 §5 is *Placing Pods Relative to Each Other* (inter-Pod affinity, topology spread). Taints are **§4**; "DaemonSet Pods still go through scheduling" is **§6**. Chapter 6 gets it right seventy lines earlier — L894 points at "Ch 7 §4 — taints, tolerations, and the fence DaemonSets step over" — so the file contains two pointers to the same topic, one correct and one not.

**Recommended fix:** change `§5` → `§4` at ch06:965, matching its own L894. One token. Not actionable from inside this chapter — flagging for author decision, same class as the ch-02 item below.

**Also soft:** `chapter-06:430` points at "Ch 7 §1 — the Pod this loop just created still has to be placed on a node, **and sometimes it can't be**." §1 covers the placement; the "can't be" half is §2. `§1–§2` or `§2` would be exact. Low severity; the reader lands one section early and reads forward.

### ⚑ Finding C2 — two of the draft's own AUTHOR-REVIEW comments are now stale

Both are at the foot of the file and both assert facts that changed today:

- **L1141** (outline Open Question #1) says `chapter-02` line 807 carries `*[cross-bearing: see Ch 7 §3 — …]*` and recommends deleting the `§3`. **That fix has already been applied upstream.** ch02:807 now reads `*[cross-bearing: see Ch 7 — node selection, tolerations, and accounting for overhead]*`. The comment should be deleted, and with it the stale quoted `§3` pointer it contains (which is otherwise the only wrong Chapter-7 section number in the file).
- **L1143** (outline Open Question #11) says "chapter-06's shipped file is incomplete and its final numbering is not verifiable" and "Book-KCNA currently ships chapters 01–05 only." Both are false as of 15:01 today. Chapter 6 ships complete, and **both** back-bearings verify against its real headings (§1 *The Resource That Holds the Intent*; §7 *One Per Node, and Work That Ends*). Replace with a one-line "verified 2026-08-24 against shipped ch-06" or delete.

Leaving these in ships a note telling the author to fix something already fixed, and telling them Chapter 6 doesn't exist.

---

## Retrieval-practice accuracy

Seven tagged items. All seven verified against shipped text. **Pass.**

| Item | Tag | Question topic | Verified against | Verdict |
|---|---|---|---|---|
| ☆ Bearings #1 Q3 | `ch5` | request vs limit — which the scheduler reads | ch05 §8 (L864–L974); L969 states the scheduler/filtering half explicitly | ✅ |
| ☆ Bearings #1 Q5 | `ch6` | ReplicaSet creates the third Pod; nowhere to put it | ch06 §2 *A Loop You Can Watch Working* (L376); L430 carries the reciprocal pointer for exactly this scenario | ✅ |
| ☆ Bearings #2 Q1 | `ch4` | direction inversion of the label selector | ch04 §5 L776, L834 (four uses, node constraints among them) | ✅ |
| Practice Q5 | `ch5` | a better node appears — Pod does not move | ch05 §4 *Scheduled Once, Replaced Never* | ✅ (correctly re-tests the ch05 rule under a *new* motivation — opportunity rather than failure) |
| Practice Q6 | `ch3` | scheduler records / kubelet acts | ch03 §2 L415, and ch03's own TYB1 Q4 (L701) grades the same split | ✅ |
| Practice Q12 | `ch4` | set-based operators | ch04 L804 gives `in`, `notin`, `exists` (+ negation) in lowercase; Q12 correctly contrasts them with node affinity's capitalized `In`/`NotIn`/`Exists`/`DoesNotExist` + `Gt`/`Lt` | ✅ |
| Practice Q15 | `ch6` | DaemonSet spreads without a spread constraint | ch06 §7 L878 | ✅ (a discrimination item, not just recall — "the Pods end up spread out" ≠ "a spreading constraint was enforced") |

**Spacing.** 33 graded items (15 Bearings + 18 Practice); 7 tagged = **21%**, inside B3's 20–25% band for Ch 7. Sources reach back to Ch 3, 4, 5 and 6 — four distinct chapters, furthest four back. B3's "≥4 chapters back" floor doesn't bind until Ch 8 but is met anyway. Soundings are correctly excluded from the budget (B3 decision #2) while still doing retrieval work — Q3, Q4 and Q6 draw on Ch 5 and Ch 6, which is exactly the design.

Header claims audited and all accurate: Bearings #1 "two of them reach back" (2) ✅; Bearings #2 "one reaches back to Chapter 4" (1) ✅; Practice "four reach back" (4) ✅; Soundings "three of them ask you to retrieve something specific from Chapters 5 and 6" (3) ✅.

**⚑ Finding R1 — the Soundings remediation pointer omits Chapter 6 (minor).** The 0–2 rubric reads: *"If questions 3, 4 and 6 were among your misses, go back and re-read Chapter 5 §8 and Chapter 5 §4 first."* Q3 → ch05 §8 ✅, Q4 → ch05 §4 ✅, but **Q6 is the ReplicaSet-loop question and its home is Chapter 6 §2**, which the rubric never names. A reader who missed Q6 is sent to two Chapter 5 sections that don't contain the answer. Fix: add "and Chapter 6 §2", or drop Q6 from the enumeration.

**⚑ Note (not a defect, for the author's file).** `.pipeline-state/book-outline/retrieval-architecture.md` is not the B3 document — it is a permission-failure message plus a summary of what B3 concluded. The per-chapter retrieval schedule was never written to disk. I audited against the surviving summary (spacing targets, the three structural decisions, the four never-retrieve items), which was sufficient for this chapter, but Ch 8's "≥4 chapters back" floor has no artifact to check against.

---

## Glossary coverage

60 concepts and commands introduced or first used in this chapter; 49 defined in-chapter; **11 carry an open definitional gap and need glossary entries.**

This answers Stage 13's question, which is narrower than the book glossary's. The Stage 12 manifest contributed 56 rows for this chapter under skill Part 16 ("all technical terms introduced in the book," 100-term floor). The two counts are not in conflict — the manifest catalogues everything; this table lists only what a reader could be graded on without ever having been told what it means.

### §1 — the decision

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| feasible node | yes | no |
| filtering (step 1) | yes | no |
| scoring (step 2) | yes | no |
| binding | yes (and made concrete at §6 as writing `.spec.nodeName`) | no |
| random tie-break | yes | no |
| data locality | **no — named in the factors list only** | **yes** |
| inter-workload interference | **no — named only** | **yes** |
| deadlines (as a scheduling factor) | named only; self-explanatory | no |

### §2 — feasibility

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| `PodFitsResources` | yes | no |
| request-as-booking (reservation semantics) | yes | no |
| `Allocatable` | yes (quoted definition) | no — already in the KB block |
| node `Capacity` | **no — named beside Allocatable; relationship deferred to Ch 8** | **yes** |
| Pod overhead | **partial — existence stated, mechanism deliberately withheld (snapshot-limited)** | **yes** |
| preemption | yes (minimal but serviceable) | no |
| `PriorityClass` | **no — named as the configuring object only** | **yes — see G4** |
| `ResourceQuota` / `LimitRange` | no — explicitly deferred | no (Ch 8 owns them) |
| `Pending` as a scheduling state | inherited from ch05 §5, reinforced here | no |

### §3 — asking

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| node labels | yes | no |
| well-known labels (`kubernetes.io/hostname`, `/os`, `/arch`) | yes | no |
| `topology.kubernetes.io/zone` and `/region` | yes (incl. the "may be absent without a cloud provider" caveat) | no |
| `kubectl get nodes --show-labels` | yes | no |
| `kubectl label nodes` | yes | no |
| NodeRestriction admission plugin | **partial — behaviour stated, "admission plugin" as a category undefined until Ch 8** | **yes** |
| `nodeSelector` | yes | no |
| node affinity | yes | no |
| `requiredDuringSchedulingIgnoredDuringExecution` | yes | no |
| `preferredDuringSchedulingIgnoredDuringExecution` | yes | no |
| affinity operators `In` / `NotIn` / `Exists` / `DoesNotExist` / `Gt` / `Lt` | yes | no |
| affinity `weight` | partial (function stated; arithmetic explicitly out of scope) | no |
| `nodeSelectorTerms` OR / `matchExpressions` AND | yes | no |

### §4 — refusing

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| taint | yes | no |
| toleration | yes | no |
| `kubectl taint` (add, and remove via trailing `-`) | yes | no |
| `NoSchedule` | yes | no |
| `PreferNoSchedule` | yes | no |
| `NoExecute` | yes | no |
| `tolerationSeconds` | yes | no |
| toleration matching (`Equal` / `Exists`, empty-key and empty-effect wildcards) | yes (Dead Reckoning block + table) | no |
| built-in node-condition taints (7 keys) | yes (table) | no |
| `node.cloudprovider.kubernetes.io/uninitialized` | partial — trigger stated, effect not | **yes** |
| node controller / node lifecycle controller | **no — two names used, neither defined, and ch03 uses a third casing** | **yes — see T2** |
| DaemonSet automatic tolerations | yes | no |

### §5 — relative placement

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| inter-Pod affinity | yes | no |
| inter-Pod anti-affinity | yes | no |
| topology domain | yes | no |
| `topologyKey` | yes | no |
| topology spread constraints | yes | no |
| `maxSkew` | yes | no |
| `whenUnsatisfiable` (`DoNotSchedule` / `ScheduleAnyway`) | yes | no |
| `labelSelector` (spread-constraint field) | yes | no |

### §6 — opting out

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| `nodeName` | yes | no |
| `OutOfmemory` / `OutOfcpu` | **no — named as failure reasons only** | **yes — see G10** |
| `schedulerName` / custom scheduler | partial — function stated, nothing more | **yes** |
| Scheduling Policies | yes | no |
| Predicates | yes | no |
| Priorities | yes | no |
| Scheduling Profiles | partial | no |
| profile plugin stages `QueueSort` / `Reserve` / `Permit` | **no — named in a list; only `Filter`, `Score` and `Bind` are explained** | **yes** |

### Two of the eleven are worth escalating

**G4 — `PriorityClass` and preemption have no home anywhere in the book.** §2 names both, states preemption's effect, and correctly declares them out of scope "so that nothing in this chapter reads as a lie later." But `priorityclass` and `preempt` return **zero** hits across ch01–ch06 *and zero across `chapter-lineup.md`*. No chapter owns them. Unless Stage 14 gives `PriorityClass` a glossary entry, the reader meets a named Kubernetes object that the book never defines. Recommend a glossary row; the author may also want to decide whether Ch 8 should pick it up.

**G10 — `OutOfmemory` will be confused with `OOMKilled`, and the book never disambiguates.** §6 says a `nodeName` Pod that doesn't fit "will fail and its reason will indicate why, for example `OutOfmemory` or `OutOfcpu`." Chapter 13's lineup entry covers `OOMKilled` and `Evicted` — but not `OutOfmemory`. These are different things (a scheduling-admission failure vs a runtime kill), they read almost identically, and ch05 already taught the runtime one. A glossary row that states the contrast in one clause pre-empts a confusion the book is otherwise setting up.

---

## Contradictions with earlier canon

**None found.** Two near-misses, both checked in full and both benign:

**1. "A request is a floor, not a ceiling" (ch05 L884) vs "a request is a booking" (§2).** ch05 says exceeding your request on a node with spare capacity is normal expected behavior. §2 says the request is spent the moment it is granted. Both are true and they describe different actors — the kubelet's runtime tolerance versus the scheduler's accounting — and §2 resolves the tension explicitly with "A node can be busy and empty at the same time, and only one of those two states is the scheduler's business." No contradiction.

*Optional improvement:* §2 never back-references ch05's actual sentence, which is the one that defuses this on sight — and ch05 ends that same paragraph with "**One number gets you a berth. The other keeps you inside it,**" which plants this chapter's title metaphor six sections early. A half-clause callback would collect a payoff that's already sitting there.

**2. `Node controller` (ch03 L421) vs `node controller` / `node lifecycle controller` (§4).** Naming, not substance. Covered at T2 and G7.

**A note on §7's closing paragraph.** It calls the scheduler "the same shape as every controller in Chapter 6." Verified: ch06 §2 (*A Loop You Can Watch Working*) and ch06 §8 (*The Control Loop, Extended*) both cover it, so the reference is now correct — the Stage 12 manifest's objection to it was based on Chapter 6 being withdrawn, which is no longer true. What remains is that the sentence carries **no cross-bearing at all**, and the loop is *defined* at ch03 §6 (*Controllers and the Control Loop*). One bracketed insertion pointing at Ch 3 §6 (or at both) would close the book's strongest recurring theme at its cleanest instance.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims** — every factual claim carries a `[source: …]` tag; the fact-accuracy stage's four flagged items are all discharged in this draft (verified: no residue of "never consults observed usage," "spoken for by things that aren't Pods," or the untagged `unschedulable` causal claim). The ~5% exam share is disclosed on the metadata line as an authored allocation, not a published CNCF weight, matching ch02/ch05. The 44% domain weight checks against `cncf-kcna-curriculum-pdf-2026-08-23.md:13`.
- [x] **Fear-based content uses real examples** — the GPU Logbook Entry is presented as a generic composite ("A platform team buys eight GPU nodes"), attributed to nobody, and contains no invented statistic. It illustrates a mechanism rather than manufacturing dread.
- [x] **Simplification acknowledged** — §2 names preemption and priority as real and out of scope "so that nothing in this chapter reads as a lie later"; the 🔭 Closer Look flags `PodFitsResources` as *an example* filter rather than the only one; §1 names the three factors the chapter can't teach; the toleration-matching rules get a Dead Reckoning block where the metaphor runs out. This guardrail is handled unusually well.
- [x] **Authority claims cite legitimate sources** — kubernetes.io and CNCF snapshots throughout; no appeals to unnamed authority.
- [x] **"Frequently tested" claims verifiable** — the chapter makes no claim about published exam frequency, question count, or pass mark (B3's never-retrieve list). Its emphasis claims are framed as authored judgment ("in my judgement, the densest fifteen minutes"; "exactly the shape a recognition exam tends to ask about"), which is the honest form.
- [ ] **No strawmanning of alternative study methods** — **FAIL. See E1.**

### ⚑ Finding E1 — the one ethical failure, unchanged since draft-v1

🏆 Safe Harbor, L1130:

> "Scheduling is the material that **most study guides present as a catalogue of six unrelated features**, and you have it as one pipeline with two slots."

This is an unsourced empirical claim about competing books, deployed to flatter this one. Skill Part 14 guardrail #3 is "NEVER strawman alternative study methods," and guardrail #1 forbids creating false beliefs.

It also breaks the standard **this book has already set for itself.** Chapter 1 L286–L290 handles competing material and does it exactly right: "Some of it is excellent," followed by a *verifiable, mechanical test* the reader can run in fifteen seconds ("count the domains"), followed by "That doesn't make its facts wrong." That's the register. The Safe Harbor line abandons it for a comparative claim nobody can check.

**Fix, preserving the whole payoff:**

> "Scheduling is easy to meet as a catalogue of six unrelated features. You have it as one pipeline with two slots."

Same rhetorical beat, no claim about anyone else's book. One sentence.

### One borderline item, not scored as a failure

§7's core synthesis — hard rules filter, soft rules score — is stated to the reader flatly, and the chapter's own AUTHOR-REVIEW at L869 records that no cached snapshot assigns any individual mechanism to a named scheduler stage. The author has already made this call knowingly, documented the gap, and named the one fetch that would close it (`kubernetes.io/docs/reference/scheduling/config/`), so I'm not re-litigating it under guardrail #4. Worth noting only that §5's 🔭 Closer Look models the honest form in the same chapter — "The explanation below is mine rather than theirs" — and §7 could carry the same three words at negligible cost.

---

## Recommended fixes

Ordered by whether the chapter should ship without them.

**Fix before ship**

1. **E1 — the Safe Harbor strawman.** One-sentence replacement supplied above. This is the only hard ethical failure and it has now survived two integration gates.
2. **T1 — British spellings.** 23 prose instances against a uniformly American six-chapter corpus. Priority within it: L568's `licence` (sits beside the `license=cad` taint key) and L1016/L1076 (spell a quoted doc sentence differently from §5's own table). Use a Python script, not the Edit tool.
3. **C2 — the two stale AUTHOR-REVIEW comments (L1141, L1143).** Both assert facts that changed today; L1141 additionally carries the only wrong Chapter-7 section number left in the file, inside its quotation of a pointer that no longer exists. Delete or restamp.

**Author decision — not fixable from inside this chapter**

4. **C1 — `chapter-06:965` points at "Ch 7 §5" for taints.** Should be `§4`, matching ch06's own L894. One token, in a shipped file.
5. **The `Ch 12 — workload isolation` forward pointer** has no matching item in Chapter 12's scope. Add it to Ch 12, or retarget (Ch 8 is closer).
6. **G4 — `PriorityClass` has no owner** anywhere in the book or the lineup. Glossary row at minimum; possibly a line in Ch 8.

**Cheap improvements, take or leave**

7. **R1** — add "and Chapter 6 §2" to the Soundings 0–2 rubric so Q6's remediation points somewhere that contains the answer.
8. **G10** — one clause distinguishing `OutOfmemory` (scheduling admission) from ch05's `OOMKilled` (runtime kill), before Chapter 13 inherits the confusion.
9. **§7's control-loop sentence** — add a cross-bearing. `Ch 3 §6` is where the loop is defined; `Ch 6 §2` is where the reader watched it work. Either or both.
10. **T2 / G7** — one clause saying the node lifecycle controller is the Chapter 3 Node controller, or a glossary row that does it.
11. **§2's request-as-booking passage** — a half-clause back to ch05's "a request is a floor, not a ceiling… one number gets you a berth" collects a metaphor ch05 planted for this chapter and pre-empts the only apparent contradiction in the pair.
12. **T3** — normalize `pod affinity` → `Pod affinity` in prose, leaving verbatim doc quotes alone.

**Confirmed already addressed — no action**

The four fact-accuracy items from the previous gate (the unsourced absolute negative; the untagged Capacity/Allocatable relationship; the untagged `unschedulable` causal claim; the metadata-line house form), the Scheduling-Policies currency question (closed by the research stage and marked do-not-reopen), the Chapter 3 six-factors promise (paid in §1), and the entire Chapter 6 verification debt (discharged by ch-06 shipping — both back-bearings verified).
```