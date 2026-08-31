I have what I need. Verification is complete — I checked every callback and cross-bearing against the shipped chapter files rather than from memory.

```markdown
# Integration Check — KCNA Chapter 8

## Summary

- Terminology consistency: **pass** (2 low-severity form nits; no drift that changes meaning)
- Callbacks to earlier chapters: **39 correct / 4 incorrect**
- Retrieval-practice accuracy: **pass** (8 of 8 tagged items land in a chapter that covers the topic; 2 carry qualifications)
- Glossary coverage: **43 concepts introduced, 38 defined in the chapter, 5 require glossary entries**
- Contradictions with earlier canon: **2 flagged** (1 hard, 1 soft)
- Ethical guardrails (skill Part 14): **pass**

**Two findings are worth the author's time before anything else.** The chapter tells the reader they have just met the *sixth* control loop in the book; shipped Chapter 6 closes by telling them they have seen it *twice* and that "the third time is the one that matters," which is Chapter 15's designated primary Zenith. And shipped Chapter 10 §4 points into Ch 8 §6 for "semantic versioning **and API stability**," of which §6 supplies only the first half. Everything else is small.

**Verification method.** Cross-bearings were checked mechanically against the B6 section skeleton. Callbacks were checked against the shipped chapter files in `../Book-KCNA/` (`chapter-01` … `chapter-11`), not against recollection. Facts were not re-audited against snapshots (stage 5 owns that).

---

## Terminology consistency

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| `kubectl` | `kubectl`, lowercase, code style | 108 | no |
| etcd | `etcd`, lowercase even sentence-initially | 65 | no |
| API server / kube-apiserver | both sanctioned (B7) | 47 / 24 | no |
| kubelet | `kubelet`, lowercase | 45 | no — zero instances of "Kubelet" |
| LimitRange | CamelCase, unspaced | 37 | no |
| ResourceQuota | CamelCase, unspaced | 31 | no |
| ServiceAccount | CamelCase | 14 | no |
| Allocatable | capitalized (field name) | 14 | no |
| admission controller | headword; `admission plugin` only for a named compiled-in one | 13 | no — `NodeRestriction admission plugin` is correctly qualified |
| DaemonSet | CamelCase, unspaced | 12 | no |
| node controller | lowercase, two words | 10 lowercase + **1 capitalized** | **minor** — see below |
| control loop | lowercase | 9 | no (but see Contradictions) |
| kube-proxy · kube-scheduler | lowercase, hyphenated | 9 / 5 | no |
| `NoSchedule` · `NoExecute` | code style, exact casing | 9 / 1 | no |
| Deployment · StatefulSet · ConfigMap · PersistentVolume · StorageClass | CamelCase, unspaced | 8 / 2 / 1 / 4 / 3 | no |
| Pod | capitalized for the object | throughout | no — every lowercase `pods` is inside a code span (`kubectl get pods`) or a verbatim source quotation (L531, "available for pods") |
| Secret | capitalized for the object | 3 | no |
| Service | capitalized for the object | 1 bare use (L744) | **nit** — see below |
| CustomResourceDefinition | CamelCase, unspaced | 1, as **"Custom Resource Definitions"** | **minor** — see below |
| "cloud native" | never hyphenated | 0 in prose | n/a — appears only inside source tags |
| Branded markers | 🧭 ☆ ★ ⚠ — 🏆 ☀️ ⚓ 🪝 🔭 🪢 | all present | no — no "Shoals Ahead", no "Landfall", no "Road Ahead" |
| The Voyage Ahead | locked closing-section name | 1 | no |

**Two form nits, neither load-bearing:**

- **"Custom Resource Definitions" (§1, spaced).** B7 canonical is `CustomResourceDefinition` / `CRDs`. Note this matches shipped Ch 6's own one-off outlier (Ch 6 uses `CustomResourceDefinition` 4× and the spaced form once), so the chapter is copying an existing blemish rather than inventing one. Suggest "the CustomResourceDefinitions of Chapter 6 §8."
- **"Node controller" capitalized** in the Chapter Summary table (L1163). This is table-label sentence case and reads normally, but B7 explicitly names the capitalized form as drift. Worth knowing: **shipped Ch 3 uses "Node controller" capitalized five times** (L421, L1133, L1263–66), while Ch 4 and Ch 7 use lowercase. The book-wide drift is Chapter 3's; Ch 8's prose is compliant (10/10 lowercase). No action needed in this chapter unless the author wants a global sweep.

**One scope nit.** L744 ("Every Deployment … Every ConfigMap and Secret. **Every Service.**") is a bare use of the Kubernetes `Service` object, which B7 defines at Ch 9 §2 and instructs earlier chapters to "name only, always with a pointer." In an enumeration of object kinds a cross-bearing would be noise, and shipped Ch 3 §3 already tells the reader Service has its own chapter (B7 ⚑5, resolved). **No fix recommended** — recorded so a later stage does not "fix" it into a pointer.

---

## Callback correctness

**Cross-bearings: 29 pointers, 28 resolve correctly, 1 defect.**

All 18 backward pointers (Ch 2–7), all 7 forward pointers (Ch 12/13/17), and all 4 intra-chapter pointers were checked against the section skeleton. Spot-verified against the shipped files: `Ch 3 §5` is "The Only Door In" (L610) and does gloss the three gates and point here (L671); `Ch 7 §3` does introduce NodeRestriction (L519); `Ch 7 §2` does leave both the booking IOU (L~430) and the Capacity/Allocatable IOU; `Ch 4 §3` does carry the four initial namespaces, the `kube-node-lease` heartbeat fact (L584), and the resource-quota sentence (L590); `Ch 3 §2` does point forward for etcd backup (L408).

**The one defect:**

> **[C1] `*[cross-bearing: see Ch 4 §3 — the habit of narrowing a claim until it is true]*` (§8, "Where the claim overreaches") points at the wrong section.**
> Ch 4 §3 is "Where a Name Lives" and owns namespaces and the namespaced/cluster-scoped boundary. The habit being invoked lives at **Ch 4 §1** (L320: *"The accurate claim is narrower and more interesting than the slogan"*) and is named as a shared discipline at **Ch 4 §6** (L995: *"That is the accurate claim, narrower than the chapter subtitle and better. It is the same discipline Chapter 3 applied to 'nobody is in charge'"*).
> **Fix:** retarget to `Ch 4 §6`, and change the accompanying sentence from "Chapter 4 §3 established" to "Chapter 4 §6 established." §6 is the better target because that is where the habit is generalized rather than merely exercised.

**Prose callbacks: 14 checked, 11 correct, 3 incorrect.**

Correct and verified: "Chapter 4 gave `apply` a single sentence and sent you here for the rest" (Ch 4 L316 says exactly this); "Chapter 4 used the second half of that fact once, in passing, in an answer key" (Ch 4 L1234); "Chapter 7 introduced the NodeRestriction admission plugin" (Ch 7 L519); "Chapter 4 pointed at exactly those Leases" (Ch 4 L584); "Chapter 3 introduced etcd … and pointed here" (Ch 3 L406–408); "Chapter 7 closed by saying this chapter is where the rules turn into consequences" (Ch 7 L1297, verbatim); "two sentences you have never been given" about node self-registration (confirmed — zero occurrences of self-registration language anywhere in Ch 1–7).

**The three incorrect:**

> **[C2] "Chapter 7 ended by naming that command, telling you it was this chapter's opening move, and declining to explain it." (§ Why This Chapter Matters)**
> `cordon` appears **zero times in Chapters 1 through 7**. Ch 7's Voyage Ahead (L1295) names the *taint* and the *act* and then explicitly withholds the command: *"The command that does it, the command that clears the node out afterwards … that's Chapter 8."* Ch 7 §4 (L702) likewise says *"That act is Chapter 8's opening move."*
> The chapter's own §1 gets this right ("This is the thing Chapter 7 promised would be Chapter 8's opening move"). Only the opening overstates it.
> **Fix:** "Chapter 7 ended by naming the *act*, telling you the command was this chapter's opening move, and declining to give it." One word changed, and the handoff becomes exactly true — which is also a better beat, because the reader now gets the withheld thing in the first three words.

> **[C3/C4] The §1 verb table maps `get` and `describe` to Chapter 4. Neither appears there.**
> - `kubectl get` — **0 occurrences in Ch 4.** First appears Ch 3 (1×), then Ch 5 (1×), Ch 6 (11×), Ch 7 (1×).
> - `kubectl describe` — **0 occurrences in Ch 4.** First appears Ch 5 (1×), then Ch 6, Ch 7.
> - `apply`, `create`, `delete` are correctly attributed to Ch 4.
> A reader sent back to Chapter 4 to find `kubectl get` will not find it. The table is otherwise the chapter's best navigational asset, which is why the two wrong cells are worth correcting rather than tolerating.
> **Fix:** `get` → "Ch 3, then throughout"; `describe` → "Ch 5, then throughout". Related, and worth one word: §1's opening presents `kubectl apply -f`, `kubectl get pods` and `kubectl scale` as "commands you have been typing since Chapter 4" — true of `apply`, loose for the other two. "since Chapter 3" is accurate for all three.

**One framing item, not a wrong fact:**

> **[C5] §4's DaemonSet exception — "This is the point at which the two facts turn out to have been the same fact."**
> Shipped **Ch 7 §4 (L706)** already joined them, in full: *"Because the controller sets the `node.kubernetes.io/unschedulable:NoSchedule` toleration automatically, Kubernetes can run DaemonSet Pods on nodes that are marked unschedulable."* Ch 8's re-statement is good structured redundancy (skill Part 7) and should stay; only the claim that this is the moment of joining is inaccurate.
> **Fix:** "Chapter 7 §4 already joined these two. Here is what that join buys you during maintenance" — and add `*[cross-bearing: see Ch 7 §4 — the DaemonSet controller's automatic tolerations]*` beside the existing Ch 6 §7 pointer, since Ch 7 §4 is the nearer prior treatment.

**Inbound pointers from shipped chapters — one is broken.**

Chapters 9–11 emit three cross-bearings into Ch 8. Two resolve cleanly against the revised draft: `Ch 8 §4 — node conditions` (Ch 9 L415) and `Ch 8 §1 — a Service is created by the same apply as every other object` (Ch 9 L589). The third does not:

> **[C6 — HIGH] Ch 10 L806 emits `*[cross-bearing: see Ch 8 §6 — semantic versioning and API stability, which is the vocabulary this section spends]*`. Ch 8 §6 has no API-stability material.**
> §6 defines `x.y.z` and Semantic Versioning terminology, the skew window, the three-branch rule and the cadence. It says nothing about alpha/beta/GA or the stability guarantees a GA API carries — and neither does Ch 4 §2, which owns `apiVersion` and API groups (zero alpha/beta/stability discussion there either). Ch 10 §4's argument turns on it: *"the project … continues to extend it the stability guarantees that GA APIs carry."* A reader following that pointer arrives and finds half of what was promised.
> **Two fixes, author's call:**
> 1. **Cheaper, lower risk:** narrow Ch 10 L806 to `see Ch 8 §6 — semantic versioning`. Ch 10 is shipped, but this is a two-word edit to a pointer, not to argument.
> 2. **Better for the book:** add two sentences to §6 on API stability levels, which would give the term an owner it currently lacks book-wide. This is new material outside the outline and would need the curriculum-alignment stage to bless it.
> Recommend (1) now and (2) recorded as a book-level gap, since Ch 17 §4 will also want the vocabulary.

---

## Retrieval-practice accuracy

**8 tagged items across a pool of 33 (15 Bearings + 18 Practice) = 24.2%**, inside the 20–25% band from skill Part 10. This clears the question-quality audit's finding that draft-v1 sat at 18.2%; two items were added and the shortfall is closed.

| Item | Tag | Topic | Covered in the tagged chapter? |
|---|---|---|---|
| Bearings #1 Q5 | `ch4` | namespaces divided by resource quota | **yes** — Ch 4 L590, verbatim |
| Bearings #2 Q1 | `ch7` | `node.kubernetes.io/unschedulable`, `NoSchedule`, running Pods not evicted | **yes** — Ch 7 L693 (taint table), L625 (the `NoSchedule` rule verbatim), L702 |
| Bearings #2 Q4 | `ch2` | container runtime, containerd/CRI-O, the CRI | **yes** — Ch 2 §4 (L533) |
| Practice Q6 | `ch4` | Nodes are not namespaced | **yes** — Ch 4 L540, L563 |
| Practice Q7 | `ch5` | requests are the scheduler's input | **yes** — Ch 5 L872, the exact sentence the answer key attributes to Chapter 5 |
| Practice Q10 | `ch4` | `spec` is what you declare, `status` what the system reports | **yes** — Ch 4 L407, L413 |
| Practice Q11 | `ch3` | the control loop | **yes** — Ch 3 §6 (L750) — *but see qualification* |
| Practice Q17 | `ch6` | DaemonSet | **partly** — *see qualification* |

**Two qualifications:**

> **[R1] Practice Q11's keyed answer names "the scheduler's watch on unscheduled Pods" as a second example of the control-loop pattern.**
> The *watch* language is genuinely Ch 7's (L294: *"A scheduler watches for newly created Pods that have no node assigned"*), so the option is defensible. But Ch 7's entire opening frames the scheduler as the thing the control loop is **not**: L266 — *"The last chapter ended on the one thing the control loop cannot do. It creates a Pod. It does not decide where the Pod goes"* — and §1 is titled "One Decision, Made Once," about a decision that is never revisited. A reader who absorbed Ch 7's thesis will read this key as contradicting it.
> **Fix:** swap the second example to one that is unambiguously a loop and unambiguously earlier — the Job controller (Chapter 3's own documented example, taught at Ch 3 §6) or the ReplicaSet controller (Ch 6 §1–§2). Both are stronger retrieval targets anyway, and neither costs the question anything.

> **[R2] Practice Q17 is tagged `[retrieval: ch6]`, but only its first half is Chapter 6's.**
> The controller's name is Ch 6 §7 ✓, and the stem correctly says "Chapter 6 introduced the controller responsible." The toleration the answer turns on — the automatic `node.kubernetes.io/unschedulable:NoSchedule` — is **Chapter 7 §4** (L706), not Chapter 6.
> **Fix:** either retag `[retrieval: ch6+ch7]`, or add one clause to the answer key: "…which Chapter 7 §4 already told you the DaemonSet controller sets automatically." The second is better — it converts an untagged dependency into a second retrieval hit at no cost.

**Soundings pre-test dependencies also check out.** Q2 (Ch 3's single-door claim, L614), Q4 (Ch 4 L524, *"many users spread across multiple teams, or projects"*), Q5 (Ch 7 L693/L702) and Q6 (Ch 4 L584) are each answerable from the prerequisite chapter, which is the Part 11 rule for Soundings. Q3 and Q7 are deliberately reasoning items with no prerequisite, and the answer key says so.

---

## Glossary coverage

43 concepts receive first substantive treatment in this chapter. 38 are defined in place. Five are introduced or used without definition and need glossary entries at stage 14.

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| `kubectl [command] [TYPE] [NAME] [flags]` grammar | yes | no |
| type case-insensitivity vs name case-sensitivity | yes | no |
| `kubectl explain` | yes | no |
| kubeconfig, and its precedence chain | yes | no |
| **kubeconfig `context`** | **no** | **yes** |
| in-cluster authentication (the three checks) | yes | no |
| transport security / port 6443 / TLS listener | yes (glossed) | no |
| authentication gate; 401; "no `User` object" | yes | no |
| **kubelet TLS bootstrapping** | **no — named once** | **yes** |
| authorization gate; 403; any-module-approves | yes | no |
| admission control; any-module-rejects; the mutation power | yes | no |
| admission controller vs admission plugin | yes (by use) | no |
| **mutating vs validating admission webhook** | **no** | **yes** — see [G1] |
| dynamic admission control / webhook backend | yes (glossed) | no |
| reads bypass admission entirely | yes | no |
| auditing; audit event; the seven questions | yes | no |
| ResourceQuota; the `403` failure; independence from cluster capacity | yes | no |
| `count/<resource>` object-count syntax | yes | no |
| **hugepages** | **no — named in the quota list** | **yes** |
| LimitRange; min/max/ratio; defaulting at admission | yes | no |
| LimitRanger admission controller | yes (named) | no |
| node self-registration; Node-object validity | yes | no — but see [O3] |
| `cordon` / `drain` / `uncordon` | yes | no |
| Eviction API; the `Eviction` object | yes (glossed) | recommended, not required |
| the five node conditions | yes | no |
| `node-monitor-grace-period` | yes | no |
| `SchedulingDisabled` as a display string, not a Condition | yes | no |
| node lease; the two heartbeat forms | yes | no |
| node controller and its three jobs | yes | no |
| **CIDR block** | **no — named, unexpanded** | **yes** — see [G2] |
| Capacity vs Allocatable (completing Ch 7 §2's IOU) | yes | no |
| `kubeReserved` / `systemReserved` | yes | no |
| managed vs self-hosted control plane | yes | no |
| kubeadm · minikube · kind · k3s | yes | no |
| semantic versioning `x.y.z` | yes | no |
| the five version-skew rules | yes | no |
| three supported minor releases; ~1 year patch support | yes | no |
| release cadence (~3/year, ~15 weeks) | yes | no |
| upgrade order (derived, and labelled as derived) | yes | no |
| `etcdctl snapshot save`; volume snapshot | yes | no |
| `etcdutl snapshot restore`; restart against the restored directory | yes | no |
| etcd access is root-equivalent | yes | no |

**The five that need action:**

> **[G0 — the one that matters] `context` is used in an answer key and never defined.**
> B6 gives Ch 8 §1 "kubeconfig; **contexts**; in-cluster auth"; B7 gives Ch 8 §1 "Context (kubeconfig context)". §1 teaches the file's location and the flag/env precedence but never says what a context is. The word then appears in graded material — Bearings #1 answer 2, L415: *"looked in the namespace of the current context."* B7's own rule is explicit: a term reaching an answer key may not be glossary-only.
> The concept is already in the prose, unnamed: §1 says the kubeconfig holds "the answer to the two-server problem: which one you are currently talking to." That *is* a context.
> **Fix — one sentence, in §1, right after the precedence paragraph:** "A kubeconfig can describe several clusters at once; the bundle of cluster, credential and default namespace that `kubectl` is using right now is called the **current context**." That closes the ledger obligation, defuses the answer-key use, and costs nothing.

> **[G1] Mutating vs validating admission webhook — now unowned book-wide.** B7 assigns the pair to Ch 8 §2, but the curriculum-alignment stage deliberately excluded it ("*The mutating/validating phase split stays out: the outline never asked for it and Chapter 12 does not need it*"). That call is upstream and I am not reopening it. Two consequences to record:
> - **B7's row is now stale twice over.** It also claims the term first appears at Ch 6 §8 — shipped Ch 6 contains **zero** occurrences of "webhook."
> - **Ch 17 §4 lists admission webhooks among the extension points** it collects, and collects rather than defines. If nothing defines the pair, Ch 17 §4 will be collecting a term the book never taught.
> **Recommendation:** glossary entry for both, plus a note on the B7 row. If the author wants it in-chapter after all, §2's existing Closer Look is the natural home and the addition reinforces §2's own thesis — a mutating webhook is the third gate's rewrite power, made configurable.

> **[G2] CIDR first appears in the book here, unexpanded.** L523 ("assigning a CIDR block to the node when it is registered") and again in the Chapter Summary (L1163). Zero occurrences in Chapters 1–7; Ch 9's only instance is inside an `AUTHOR-REVIEW` comment, so nothing reader-facing precedes this. B7's acronym register assigns CIDR to Ch 10 §6 with a glossary expansion, which is now wrong about first use.
> This is the same class of debt the Ch 9 gate recorded for CNAME/BGP/eBPF/IPVS and the Ch 10 gate recorded for SNI/OSI. **Fix:** expand at L523 ("a CIDR block — a range of IP addresses in Classless Inter-Domain Routing notation") and correct the register row to Ch 8 §4.

> **[G3] `kubelet TLS bootstrapping` and [G4] `hugepages`** are each named once and never explained. Neither reaches graded text, so glossary entries suffice.

---

## Contradictions with earlier canon

> **[X1 — HIGH] The control-loop ordinal contradicts shipped Chapter 6, and pre-empts Chapter 15.**
>
> This chapter says, twice:
> - §4: *"**The node controller is a control loop.** You met the pattern in Chapter 3, and you have seen five instances of it since. This is the sixth."*
> - §8: *"It is the sixth one in this book, and you could have predicted its structure without being told."*
>
> Shipped **Chapter 6 closes** (L1465): *"you have seen the control loop **twice now, at two altitudes**, and recognized it the second time. Hold onto that recognition. You are going to need it once more, and **the third time is the one that matters**."*
>
> And shipped **Chapter 6 L287** sets the arc out explicitly: *"Chapter 3 introduced the control loop, this chapter instantiates it, and Chapter 15 generalizes it to a loop whose desired state lives in a Git repository. A reader who does not feel the shape here will meet Chapter 15's synthesis as a fifth list to memorize instead of as a recognition."*
>
> The two counts are counting different things — Ch 6 counts *altitudes*, Ch 8 counts *controllers* — and both are internally coherent. But the reader has one head. Having been told at the end of Ch 6 that they have seen it twice and the third is the payoff, they are told two chapters later that this is the sixth. The immediate cost is confusion. The larger cost is that **Chapter 15 §7 is the book's designated PRIMARY ZENITH**, and its entire effect is the recognition Ch 6 spent a paragraph banking. "The third time is the one that matters" does not survive a reader who has been counting to six.
>
> A secondary problem: **"five instances since" is not derivable.** Ch 6 instantiates the loop in six or seven named controllers depending on how you count (ReplicaSet, Deployment, StatefulSet, DaemonSet, Job, CronJob, plus operators at §8), and Ch 7 does not present the scheduler as one — its opening explicitly excludes it. There is no reading of the shipped text that yields five.
>
> **Fix — drop the ordinal, keep the recognition.** The paragraph's actual work is "you could have predicted its structure," and that survives intact:
> > §4: *"**The node controller is a control loop.** You met the pattern in Chapter 3 and you have met it in every chapter since. Noticing that costs one sentence and buys §8 half its argument."*
> > §8: *"It is the same loop, at the same altitude as Chapter 6's, and you could have predicted its structure without being told."*
>
> This is the same failure mode the book has already hit once: B6 Collision note #2 records Ch 9 §8 counting pluggable interfaces as "the second instance" while Ch 10 and Ch 11 count to three, which had to be reconciled in shipped Ch 10. **Running ordinals across chapters have now caused two collisions in this book.** Worth a book-level convention: state the pattern, never the count.

> **[X2 — SOFT, no fix required] Chapter 9's "Chapter 8 pointedly did not tell you that" versus this chapter's Voyage Ahead.**
> Shipped Ch 9 L295 states the four-rule network model and then says *"Chapter 8 pointedly did not tell you that. It had reason not to: the claim wasn't sourceable in that chapter's material."* This chapter's Voyage Ahead says *"Every Pod gets an address."*
> These do not actually collide — Ch 9's "that" refers to the sourced compound claim (unique cluster-wide, directly reachable, no NAT), not to the bare headline, which is also Chapter 9's own title. Recording it only so a later stage does not read it as a contradiction and "fix" a sentence that is fine.
>
> **Worth noting the opposite, because it is the strongest integration result in this check:** Ch 8's Voyage Ahead promises Part III as *"addresses, the abstraction that makes them survivable, how names resolve, and how anything outside the cluster gets in at all"* — and shipped Ch 9 L301 quotes that clause **verbatim** back at the reader before splitting it three-to-Ch-9, one-to-Ch-10. The handoff is intact to the word.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** The only numerals of that shape in the chapter are `44%` and `~5%`, both in the metadata line, both immediately followed by the disclosure paragraph distinguishing CNCF's published domain weight from this book's authored competency allocation. Nothing else in 1,224 lines matches a statistic pattern — no "40% of candidates," no "most test-takers." The Exam Alert says so out loud: *"None of them is dressed up with an invented statistic, because nobody publishes one."* That is the right posture and it is rare.
- [x] **Fear-based content uses real examples.** §4's Navigational Hazards ("cordon a node and then reboot it … every Pod still on that node goes down with the machine") and §7's unencrypted-snapshot argument both describe real mechanisms with real consequences, sourced. Neither invents a scenario.
- [x] **Simplification acknowledged.** Unusually well. §6 flags the version roster as perishable and tells the reader to learn the rule instead. §6 labels its own explanation of the `kubectl` exception as *"this book's own reasoning rather than documented rationale — the version-skew policy states the rules without saying why."* §6's upgrade-order derivation says *"No cached documentation states an upgrade order in those words — this is a derivation."* §8 carries an entire subsection titled "Where the claim overreaches" that retracts the chapter's own thesis to the part that survives. Bearings #2 A5 declines to extend the managed/self-hosted duty list beyond what the architecture decides. This is guardrail 4 and 5 handled better than most published cert prep manages.
- [x] **Authority claims cite legitimate sources.** Every factual sentence carries a `[source: ...]` tag; the three `AUTHOR-REVIEW` comments record deliberate non-assertions with the fetch that would close each gap (G-8G among them).
- [x] **"Frequently tested" claims are verifiable.** The chapter does not make frequency claims. The Exam Alert is explicitly ordered *"in descending order of confidence,"* which is the honest form of that list. §6's "the single most mechanically checkable block in the entire curriculum" is a claim about the *material's shape*, not its exam frequency, and reads as the authorial judgment it is.
- [x] **No strawmanning of alternative study methods.** None present.
- [x] **Subject dignity (skill Part 14, v5.7).** Every wry beat is aimed at the practitioner: the engineer who cordons and reboots, the person who has run a debugging shell and been surprised, "crews that priced the machines and not the Thursdays." Nothing is aimed at anyone harmed by a failure.

**One item recorded, not flagged:** §1's Snag says *"Every practitioner who has ever run a debugging shell inside a cluster has been surprised by this at least once."* It is a universal quantifier, and it is obvious hyperbole in register rather than a claim of fact. It is the only sentence of its kind in the chapter and I do not think it needs changing; noting it so the author knows it was seen and judged.

---

## Recommended fixes

Ordered by what I would do first. Items 1–2 are the ones I would not ship without.

1. **[X1] Remove the control-loop ordinal from §4 and §8.** Contradicts shipped Ch 6's closing and pre-empts Ch 15 §7's primary Zenith. Suggested replacement wording is in the Contradictions section. Two sentences.
2. **[C6] Resolve the broken inbound pointer from shipped Ch 10 L806.** Either narrow that pointer to `see Ch 8 §6 — semantic versioning` (two words, in Ch 10), or add API-stability material to §6 (new scope, needs curriculum-alignment sign-off). Recommend the first now, the second recorded as a book-level gap that Ch 17 §4 will also want closed.
3. **[G0] Define `context` in §1.** One sentence. Currently used in a Bearings answer key with no definition anywhere and no glossary path, against B7's own rule.
4. **[C2] "Chapter 7 ended by naming that command" → "naming the *act*."** Ch 7 names the taint and the act and explicitly withholds the command; `cordon` appears zero times in Ch 1–7. One word, and the opening gets sharper.
5. **[C1] Retarget the §8 cross-bearing** from `Ch 4 §3` to `Ch 4 §6`, and change the sentence to match.
6. **[C3/C4] Correct two cells of the §1 verb table** — `get` → Ch 3, `describe` → Ch 5 — and change "since Chapter 4" to "since Chapter 3" in §1's opening.
7. **[R1] Swap Practice Q11's second keyed example** from the scheduler to the Job or ReplicaSet controller. Ch 7 L266 explicitly frames the scheduler as what the control loop *cannot* do.
8. **[R2] Add one clause to Practice Q17's answer** attributing the toleration to Ch 7 §4, or retag `[retrieval: ch6+ch7]`.
9. **[C5] Soften §4's DaemonSet framing** — Ch 7 §4 L706 already joined the two facts — and add a `Ch 7 §4` cross-bearing beside the Ch 6 §7 one.
10. **[G1–G4] Glossary queue for stage 14:** mutating/validating admission webhook, CIDR (expand in place at §4 as well), kubelet TLS bootstrapping, hugepages, Eviction API (recommended).
11. **Terminology nits, optional:** "Custom Resource Definitions" → "CustomResourceDefinitions"; "Node controller" → "node controller" in the summary table.

### Open author decisions, unchanged by this chapter

- **PodDisruptionBudget (B7 ⚑3).** Still unowned. B6 assigns "PodDisruptionBudget interaction" to Ch 8 §4; the draft contains zero occurrences of `PodDisruptionBudget`, `PDB`, or `disruption`, and §4's `drain` treatment says nothing about what can block or stall an eviction. This is **compliant with B7's fallback branch** ("the term stays out of all graded material") and nothing is broken — but the ledger's preferred fix was a one-clause gloss here, and §4 is the only place in the book where the reader has a question a PDB answers. Author's call, unchanged.
- **"There is no Kubernetes LTS" (B7 orphan).** B7 recommends a ⚠ Navigational Hazards line at Ch 8 §6. Absent. A live misconception for readers arriving from distributions that have LTS, and it sits directly against §6's three-minor window. Author's call.
- **Figure anchors.** `ch08-fig05` and `ch08-fig03` are transposed relative to their captions (Figure 8.3 and Figure 8.5), and `ch08-zenith-consequences-not-rules` does not follow the `chNN-figMM-slug` form. **Both were already caught by stage 10** and are documented under "ANCHOR ANOMALIES" in `image-specs.md` (L19–L36) with recommendations. Not re-raising as new; recorded as still open.

### Ledger and skeleton rows this chapter shows to be stale

Recorded so a later stage does not "correct" the chapter toward a wrong contract. **None of these require a change to Chapter 8.**

- **B7: "Node registration — Defined by Ch 3 §3."** Shipped Ch 3 does not teach it. `register`/`registration` appears in Ch 3 only as a distractor string at L510; there is no self-registration content anywhere in Ch 1–7. **Ch 8 §4 is now the de facto owner, correctly** — do not strip it.
- **B7: "`kubectl describe` — first appears Ch 8 §4."** It first appears at Ch 5 (1×), then Ch 6 and Ch 7.
- **B7: "Mutating vs validating admission webhook — first appears Ch 6 §8."** Ch 6 contains zero occurrences of "webhook." See [G1].
- **B7 acronym register: "CIDR — Ch 10 §6."** First reader-facing use is Ch 8 §4. See [G2].
- **B6 skeleton, Ch 8 §1 owns "output formats."** The draft does not teach `-o yaml` / `-o wide` / `-o json` as a topic; `-o yaml` appears once, incidentally, inside a §3 Snag. Not a defect — the verb table and the kubeconfig material are the section's load-bearing content, and B7 assigns no term for output formats — but recorded in case a later stage expects the coverage.
```

**The two findings I would not ship without** are the control-loop ordinal (§4/§8 tell the reader this is the sixth control loop; shipped Chapter 6 closes by telling them it is the second and that "the third time is the one that matters," which is Chapter 15's designated Zenith) and the broken inbound pointer from shipped Chapter 10 §4, which sends readers to Ch 8 §6 for "semantic versioning **and API stability**" — §6 has no API-stability material, and neither does Ch 4.

Everything else is small and cheap: one cross-bearing aimed at the wrong section, one overstated callback (`cordon` appears zero times in Chapters 1–7, so Chapter 7 cannot have "named that command"), two wrong cells in the §1 verb table, and `context` used in an answer key without ever being defined.

I did not write the file — per the pipeline convention in CLAUDE.md, stage output flows through stdout for the orchestrator to capture, rather than through `Write`.