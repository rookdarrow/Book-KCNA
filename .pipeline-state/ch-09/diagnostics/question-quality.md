Write isn't permitted for this stage — per the project's executor design, stage output flows through stdout for the orchestrator to capture. Emitting the artifact:

# Question-Quality Audit — Chapter 9

Audited against `draft-v1.md` (`draft-voice.md` does not exist at this stage). All line numbers cite `draft-v1.md`. Budget targets read from `outline.md` frontmatter lines 117–121.

## Summary

- Chapter type: **content**
- Total questions inspected: **44**
  - 🧭 Soundings questions: **8** (lines 47–61; answers 66–80)
  - ☆ Taking Your Bearings questions: **15** (across **3** checkpoints — #1 line 338, #2 line 563, #3 line 838)
  - Practice questions: **21** (lines 1026–1216; answer key 1219–1352)
- Question budget compliance: **met** on all four frontmatter targets — **but the per-section Practice distribution is violated: §7 planned 3, delivered 1.** See § Question-budget compliance.
- Weak distractors (WARN): **5** — Q14 C, Q14 D, Q16 A, Q16 D, Q17 D
- Trap answers that don't target real misconceptions (WARN): **3** — Q14 D, Q16 A, Q17 D (subset of the weak-distractor set; the answer keys concede these are invented)
- Missing or incomplete why-wrong explanations (FAIL): **2** — Q5 (options A and D unexplained), Q11 (option C unexplained). A further **5** are present-but-vague (WARN): Q7, Q10, Q14, Q16, Q17.
- Retrieval-practice spacing: **compliant** — 7 of 36 (19.4%), allocated 3 Bearings / 4 Practice, exactly the split the outline ratified. ≥4-back floor met, with redundancy.
- Soundings spoiler check: **1 question (Soundings Q5) reveals a ★ Fixed Point — FAIL** by the letter of the rule. A mitigating prerequisite argument exists and a one-line fix is available; see analysis.

**The single most consequential finding is not in the summary counts.** §7 (DNS and names) is one of the two sections the chapter's own Attention Budget names as where its exam points concentrate — and it received **1 of its 3 budgeted Practice questions**. Five of its seven teaching items are never tested anywhere in the chapter. See § Coverage vs concepts.

---

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 15 | 15 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 (outline plans 3) | 3 (5 + 5 + 5) | **met** |
| Practice Questions | 21 | 21 | **met** |
| **Chapter total** | 44 | 44 | **met** |

Frontmatter compliance is clean. The problem is one level down.

### Practice-question distribution vs the outline's § 7 plan

The outline's Practice plan allocates questions per section by exam-point density. Actual placement:

| Block | Planned | Actual | Questions | Status |
|---|---|---|---|---|
| §1–§2 — network model, CNI, why a Service exists | 4 | 4 | Q1–Q4 | met |
| §3 — the type ladder | 5 | 5 | Q5–Q9 | met |
| §4 — selector, EndpointSlice, readiness | 4 | 6 | Q10–Q15 | **over by 2** |
| §5 — headless and selectorless | 2 | 2 | Q16–Q17 | met |
| §6 — kube-proxy | 3 | 3 | Q18–Q20 | met |
| §7 — DNS and names | 3 | **1** | Q21 | **short by 2** |

Two further outline requirements attached to the §7 block are unmet:

- *"At least one must require the reader to **write** a name rather than recognise one."* Q21 is a four-option recognition item about the search-list mechanism. **No Practice question asks the reader to write a DNS name.** ☆ Bearings #3 item 4 (line 848) does — but that is a checkpoint, not the end-of-chapter set the reader drills before an exam.
- Of the outline's five named interleaving items, **three are absent**, and two of the three are the DNS-involving pairs: **Types + DNS (§3 + §7)** and **Headless + DNS + StatefulSet (§5 + §7 + Ch 6)**. The third absence is the **Zenith item** — see below.

Raw interleaving count is met (≈7 Practice questions require two sections: Q2, Q9, Q10, Q12, Q13, Q17, Q20). It is the *composition* that drifted: every surviving interleave routes through §4 or §6, and none touches §7.

### The Zenith is untested

The outline specified one Practice item testing §8: *"a Kubernetes networking behaviour the chapter did not cover. What object holds the declaration, and which loop is publishing its answer? The correct answer is the **method**, not a fact, and it is the only question in the set that tests the Zenith."*

**No such question exists.** Q15 comes closest — its key uses the phrase "being reconciled correctly against a set that is currently empty" — but Q15 is a §4 diagnosis item, and its correct option (B) can be selected without any grasp of the control-loop framing. The chapter's synthesis moment (line 950) is delivered and never assessed.

### Recall-vs-prediction calibration: compliant

The outline warned that this chapter's failure mode as a question set is recognition inflation, and budgeted "about eight of the twenty-one" for near-pure recall. Actual: 8 recall-shaped items (Q1, Q3, Q5, Q8, Q11, Q14, Q16, Q18) against 13 prediction/diagnosis items. **On target.** Q8 is the one that misses on a different axis — see its per-question block.

---

## Soundings spoiler check

Fixed Points the chapter teaches, checked against each Soundings item. Chapter Fixed Points are at lines 180, 194, 230, 287, 309, 469, 526, 694, 764, 776.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 (L47) | Generic indirection over a changing backend set | **no** | Answer (L66) names "a load balancer with a fixed VIP", "a DNS name re-pointed", "a service registry". Never names a Service, a selector, or a type. FP#3 (L230) — *an API object whose premise is that the set changes* — is not reachable from a generic instinct for indirection. |
| 2 (L49) | Shared Pod network namespace; port space; `localhost` | **partial — prerequisite half only** | Answer (L68) ends *"The Pod has one IP address; the containers share it."* That clause is the second half of FP#1 (L180) verbatim in substance. **Mitigation:** it is Ch 5 material, cited as such (*"(Chapter 5 §2.)"*), and skill Part 11 Rule 2 requires Soundings be answerable from prerequisites. FP#1's chapter-new content — *cluster-wide* uniqueness, no NAT, no proxies, cross-node — is fully withheld. **Not counted as the FAIL.** |
| 3 (L51) | Churn under a rolling update | **near-miss — soft WARN** | Answer (L70): *"a name or an address belonging to the **set** rather than to any member of it."* That is the shape of FP#3 (L230) without its name. The outline anticipated the reader reaching *"it wouldn't care if it were using something that didn't move"* and called that the ideal outcome; the draft's key goes one step further by supplying the set-versus-member framing. Recommend trimming to the outline's version. |
| 4 (L53) | Selector as a query; two controllers, one label set | **no** | Answer (L72) names selectors and non-coordination. Withholds every new element of FP#6 (L469): the EndpointSlice object, the controller that writes it, and readiness as a gate. Clean as a pre-test. *(But see Practice Q10 — this answer creates a downstream problem.)* |
| 5 (L55) | Service DNS name form; bare-name resolution across namespaces | **YES — FAIL** | Answer (L74) supplies `<service-name>.<namespace-name>.svc.cluster.local` **and** *"A bare `database` from inside `payments` resolves to the `database` Service **in `payments`**."* Compare FP (L776): *"`<service>.<namespace>.svc.<cluster-domain>`. A **bare name resolves in the client Pod's own namespace only**…"* Both factual halves of the Fixed Point are disclosed before the chapter begins. |
| 6 (L57) | NAT and what the receiver sees | **no** | Answer (L76) deliberately stays outside Kubernetes. This is the item priming FP#1's *prohibition*, and it does that job without stating it. Working as designed. |
| 7 (L59) | Pluggability as a design pattern | **no** | Answer (L78) names neither Kubernetes nor CNI, so FP#2 (L194) is intact. *Note, not a finding:* the answer asserts *"you must choose and install something before the platform functions at all"* as a general design fact, while §1 deliberately declines the equivalent Kubernetes claim pending the `network-plugins` fetch (AUTHOR-REVIEW, L190). A reader who scores this right gets no confirmation in §1. Sourcing is the fact-accuracy stage's call; flagged here only because it affects the pre-test's payoff. |
| 8 (L61) | External exposure; who supplies the terminating box | **no** | Answer (L80) attributes the load balancer to "**the provider**" in a generic setting. FP#5 (L309) — *Kubernetes provides none* — is primed, not stated. Working as designed. |

**Rubric check (rule 8):** ✅ Present and complete at L82–L86 — the 6+ / 3–5 / 0–2 branches are all there, and the 0–2 branch carries the outline's required specific instruction (*"if questions 2, 3 and 4 were among your misses, go back to Chapter 5 §2 and Chapter 6 §4"*).

**Answer disclosure (rule 9):** ✅ `<details><summary>Click for answers + reading strategy</summary>` at L63–L64, closed at L88. Answers are not visible before attempt.

---

## Per-question findings

### Q Practice 5 (L1062): "A Service is created with no `type` field specified. What type is it, and from where is it reachable?"

**Issue:** Why-wrong explanations missing for two of three distractors. **FAIL (rule 3).**

**Distractor analysis:**
- A) NodePort; from any node's IP at a static port — *plausible to a reader who remembers NodePort as "the basic one"; genuinely tempting and worth explaining*
- B) ClusterIP; from inside the cluster only — **correct**
- C) ClusterIP; from inside the cluster and from any node's IP — *plausible to someone who has over-generalised additivity into running downward as well as upward; the key handles this one well*
- D) LoadBalancer; from wherever the provider's load balancer is reachable — *plausible to a reader whose only exposure is a managed cluster where LoadBalancer is what everyone types*

**Why-wrong explanation status:** **present for C only.** The key (L1243–1247) explains C at length — *"the additivity runs one way only"* — and says nothing whatever about A or D.

**Recommended fix:** add two clauses to the key. For A: *"NodePort is never a default; it must be requested, and requesting it would additionally allocate the cluster IP that B describes."* For D: *"LoadBalancer is never a default either — and per §3 it is the one type that cannot function without a component Kubernetes does not ship."* The D clause is worth the words because it reinforces FP#5 at no extra cost.

---

### Q Practice 11 (L1116): "Where does Kubernetes record the set of Pods currently backing a Service, and what writes it?"

**Issue:** Why-wrong explanation missing entirely for one distractor. **FAIL (rule 3).**

**Distractor analysis:**
- A) In the Service's `status` field, written by kube-proxy — *plausible: conflates the reader of the answer with its writer; the key names this precisely*
- B) In EndpointSlice objects, written by the EndpointSlice controller — **correct**
- C) In the Pods' annotations, written by the kubelet — *plausible to a reader who has absorbed "the kubelet writes Pod-level state" from Ch 5 and Ch 8 and generalises it; a real and specific misconception*
- D) In cluster DNS, written by CoreDNS — *plausible: DNS is the most visible consumer of the answer; the key handles this well ("confuses a publisher with a source of truth")*

**Why-wrong explanation status:** **missing entirely for C.** The key (L1281–1285) covers A and D and skips C.

**Recommended fix:** *"**C** puts the answer on the wrong object and names a component that never participates — the kubelet reports a Pod's own status, but endpoint membership is computed centrally by a controller reading the API, not written per-Pod by each node."* This is worth stating because it reinforces the §4 Snag's point that the two empty-endpoint causes live in the control plane, not on the node.

---

### Q Practice 14 (L1143): "`kubectl get endpointslices -l …=web` returns a slice with no endpoints. The Pods you expect are Running. What are the two usual causes?"

**Issue:** Two distractors are weak, and the key concedes as much rather than repairing them. The question effectively collapses to A-versus-B. **WARN (rules 1, 2).**

**Distractor analysis:**
- A) kube-proxy is not running, or the CNI plugin is misconfigured — *strongly plausible; this is the designed trap (a networking symptom with non-networking causes) and the key defuses it precisely*
- B) The Service's selector does not match the Pods' labels, or the Pods are not Ready — **correct**
- C) The Pods are on nodes without a cluster IP allocated, or DNS has not propagated — **weak.** The first clause is not a coherent concept in this material — nodes do not have cluster IPs allocated to them. The second clause ("DNS has not propagated") *is* a real and common misattribution and would carry the option on its own.
- D) The Service has no `type` set, or the EndpointSlice controller is disabled — **weak.** The first clause is eliminable by anyone who answered Q5 nine questions earlier (no `type` defaults to ClusterIP). The second is not a belief an associate-tier reader plausibly holds; it is fabricated for symmetry, and the key says so.

**Why-wrong explanation status:** **present but vague.** *"**C** and **D** invent failure modes"* (L1303) does not name a misconception for either, because there isn't one to name.

**Recommended fix:** rebuild C and D from real misattributions rather than inventions. C → *"DNS has not propagated the Service record yet, or the Pods' probes have not run for the first time"* (both real; the second is a near-miss on the correct answer, which makes it genuinely discriminating). D → *"The Pods are in a different namespace from the Service, or the Service was created before the Pods existed"* — the namespace half is a real and frequent cause of an empty slice, and forcing the reader to reject the ordering half tests whether they understand that a control loop is continuous rather than one-shot.

---

### Q Practice 16 (L1161): "What does setting `.spec.clusterIP` to `None` do, and which workload type requires it?"

**Issue:** All three distractors pair a definition clause with a workload clause, and **every distractor is eliminable on the workload clause alone.** The `clusterIP: None` half — the actual Fixed Point (L526) — is never tested. Separately, one distractor's first clause is closer to true than the key acknowledges. **WARN (rules 1, 2).**

**Distractor analysis:**
- A) Deletes the Service's address after creation; required by DaemonSets — **weak.** "Deletes after creation" is incoherent as a mechanism, and DaemonSets have no relationship to headless Services. Fabricated for symmetry.
- B) Makes the Service internal-only; required by Deployments with more than one replica — *half-plausible and the best of the three: "internal-only" is a real confusion (readers conflate headless with ClusterIP's cluster-internal scope). The key's blanket "each invent a behaviour" mischaracterises it.*
- C) Creates a headless Service — DNS returns the Pod addresses directly instead of one virtual IP; required by StatefulSets for Pod network identity — **correct**
- D) Disables kube-proxy for that Service only; required by Jobs — **weak, and unfairly so.** The first clause is *substantially correct*: §6 (L694) establishes that kube-proxy programs a virtual IP for every type except ExternalName, and a headless Service has no cluster IP to intercept, so kube-proxy has nothing to do for it. A reader who has understood §6 well may find D's first clause defensible and be penalised for it. The key does not address this at all.

**Why-wrong explanation status:** **present but vague** — three distractors dismissed in one clause (L1317), with no per-option reasoning and one active mischaracterisation.

**Recommended fix:** two changes. (1) Split the question so the definition half is tested independently of the workload half — the current construction lets a reader who knows only "StatefulSets need a headless Service" score without engaging `clusterIP: None` at all. (2) Retire D or rewrite its first clause; as written it rewards a shallower reading of §6 than the chapter wants. Suggested replacement: *"Reserves the Service's name without allocating any endpoints; required by CronJobs."*

---

### Q Practice 17 (L1170): "You are migrating a database into the cluster… What do you configure today?"

**Issue:** One fabricated distractor, and a terse key. **WARN (rules 1, 2, 3).**

**Distractor analysis:**
- A) `type: ExternalName` pointing at the database's hostname — *strongly plausible and correctly the near-miss; the key handles it well, naming the proxying difference as the discriminator*
- B) A headless Service with no selector — *plausible: the reader knows selectorless is involved and may over-reach to headless. Key explains it in five words but they are the right five ("removes the single address, which the clients want").*
- C) A Service with no selector, plus manually managed EndpointSlices — **correct**
- D) `type: LoadBalancer` with the external address in an annotation — **weak.** Nothing in the chapter suggests an annotation-driven external address; there is no misconception here to catch. Fabricated.

**Why-wrong explanation status:** **present but vague for D** — *"**D** is invented"* (L1325). Accurate, and that accuracy is the problem: a distractor the key can only describe as invented should not be on the paper.

**Recommended fix:** replace D with a real competing instinct — *"A `type: ExternalName` Service today, and swap it for a selector-based Service on migration day."* That is what many practitioners would actually propose, it is wrong for the stated requirement in an instructive way (the client's connection semantics change under it, and the swap is a visible cutover rather than an invisible one), and it gives the key something worth explaining.

---

### Q Practice 10 (L1107): "A Pod carries labels that a ReplicaSet selects on and labels that a Service selects on…"

**Issue:** Not a distractor problem — a **contamination** problem. The correct answer is stated near-verbatim in the Soundings answer key at the top of the chapter. **WARN.**

Soundings Q4 answer (L72): *"Editing a Pod's labels can remove it from one controller's set, the other's, or both, independently. The two controllers do not coordinate; they are separate queries that happen to read the same field."*

Practice Q10 option C (L1112): *"The Pod may leave the ReplicaSet's set and the Service's endpoint list independently; the controllers do not coordinate, because they are independent queries over the same labels."*

Any reader who opened the Soundings `<details>` — which the rubric instructs all of them to do — can match C by phrase recognition. Q10 is the chapter's designated ≥4-back redundancy item for the retrieval floor, so it is carrying structural weight it can no longer bear as an assessment.

**Distractor analysis:**
- A) Both sets simultaneously; controllers coordinate through the owner reference — *plausible and good; targets the selection/ownership conflation that §4 (L453) exists to prevent*
- B) Only the ReplicaSet is affected; Services select on owner references — *plausible inversion of the same confusion*
- C) **correct** — but pre-disclosed
- D) Nothing happens until the Pod is restarted — *plausible to a reader who thinks selectors are evaluated at admission rather than continuously; the key names this precisely*

**Why-wrong explanation status:** **present, one vague.** A and D are specific. **B is dismissed as *"wrong on both halves"*** (L1279) without saying which halves or why either fails.

**Recommended fix:** two edits. (1) Reword Q10's correct option away from the Soundings phrasing — e.g. *"Each selector is evaluated independently, so the Pod may drop out of either set, both, or neither"*. (2) Expand B's key clause: *"**B** is wrong twice — a Service selects on labels, not owner references (owner references govern cleanup, not membership), and the ReplicaSet is not privileged over the Service in any way; both are ordinary selector evaluations."*

---

### Q Practice 8 (L1089): "Which Service type sets up **no proxying of any kind**?"

**Issue:** Phrase-match recognition item. The stem quotes a string that appears verbatim three times in the chapter, each time attached to ExternalName. **WARN (rule 1 — the question tests table lookup, not understanding).**

The exact phrase "no proxying of any kind" appears at L294 (the §3 definition), L297 (the ⚠ Navigational Hazards callout), and in the Exam Alert trap table. A reader who skimmed can select D without knowing what a CNAME is or why the exclusion follows from kube-proxy's job.

**Distractor analysis:** A) ClusterIP, B) NodePort, C) LoadBalancer — all three are *structurally* fine (they are the ladder types, and the key correctly groups them as "exactly the set kube-proxy covers"). The weakness is in the stem, not the options.

**Why-wrong explanation status:** **present and specific** (L1263–1267), grouped but with the shared reason named precisely.

**Recommended fix:** convert to a scenario so the reader must derive the exclusion rather than recall the phrase. Suggested: *"A Service resolves to `api.vendor.example`. An engineer adds a node-level packet capture expecting to see the traffic leave via a kube-proxy rule, and sees nothing. Which Service type is this, and why is there no rule to capture?"* Same fact, and it forces the §6 connection the chapter builds at L654–L692.

---

### Q Soundings 5 (L55): "Chapter 4 gave you, in a single sentence, the DNS name form a Service gets. Write it out…"

**Issue:** The answer discloses both factual halves of the §7 Fixed Point at L776, before the chapter starts. **FAIL (rule 7).**

**Format note:** Soundings items are open-response, so there is no distractor set to analyse. The spoiler lives entirely in the answer key.

**Evidence:** answer at L74 supplies `<service-name>.<namespace-name>.svc.cluster.local` and states that a bare name resolves in the caller's own namespace. FP at L776 states the same name form and the same rule. The only thing the Soundings withholds is the *mechanism* — the DNS search list — which §7 supplies at L768.

**The mitigating argument, stated fairly:** both facts are genuine Ch 4 prerequisites. §7 itself says so at L766: *"Chapter 4 gave you the rule flat."* Skill Part 11 Rule 2 requires Soundings questions be answerable from prerequisites; Rule 3 forbids revealing Fixed Points. **This chapter has a Fixed Point built entirely out of prerequisite material, which makes the two rules unsatisfiable simultaneously.** The Soundings item is not the thing that is wrong.

**Recommended fix — one line, in §7, not in the Soundings.** Rewrite the L776 Fixed Point so its headline claim is the part Chapter 4 did *not* give: the mechanism. E.g.

> ★ **Fixed Point:** A bare name resolves in the client Pod's **own namespace only** — **because that namespace is first in the Pod's DNS search list.** It is not a Kubernetes special case; it is ordinary DNS search-domain resolution, which is also why crossing a namespace requires the full `<service>.<namespace>.svc.<cluster-domain>`.

That keeps the name form available for reference, moves the Fixed Point's *claim* onto material Soundings withholds, and costs nothing — §7 already does the work at L768–L774. Leave Soundings Q5 as written; it is doing exactly the prerequisite-retrieval job the outline designed for it.

---

## Retrieval-practice spacing

- Chapter 9 target: **20%** (outline § Arc-outline inheritance, `[B3]`), allocated **3 in Bearings, 4 in Practice** against a combined pool of 36.
- Actual: **19.4%** — **7 of 36** tagged `[retrieval: chN]`.
  - Bearings: **3 of 15 (20.0%)** — #1 item 2 `[ch5]` (L344), #1 item 4 `[ch6]` (L348), #2 item 1 `[ch6]` (L567)
  - Practice: **4 of 21 (19.0%)** — Q2 `[ch5]` (L1035), Q10 `[ch4]` (L1107), Q12 `[ch5]` (L1125), Q21 `[ch4]` (L1206)
- Status: **compliant.** Within the 10–25% band (rule 4) and matching the outline's ratified allocation exactly. The 19.4% combined figure sits fractionally below skill Part 10's 20–25% guidance for Ch 6+; Bearings alone hit 20.0% on the nose, which is the figure Part 10's table is written about.

**≥4-back spacing floor: met, with the planned redundancy in place.**

| Anchor | Placement | Distance | Status |
|---|---|---|---|
| Pod network namespace (Ch 5 §2) | Bearings #1 item 2 (L344) | 4 back | ✅ floor item |
| Controller churn (Ch 6 §4) | Bearings #1 item 4 (L348) | 3 back | ✅ named anchor |
| Selectors → Service (Ch 6 §2) | Bearings #2 item 1 (L567) | 3 back | ✅ named anchor |
| Pod network namespace (Ch 5 §2) | Practice Q2 (L1035) | 4 back | ✅ |
| Labels and selectors (Ch 4 §7) | Practice Q10 (L1107) | 5 back | ✅ redundancy |
| Readiness probes (Ch 5 §6) | Practice Q12 (L1125) | 4 back | ✅ |
| Namespaces / bare names (Ch 4 §6) | Practice Q21 (L1206) | 5 back | ✅ redundancy |

Bearings #3 carries zero retrieval, which the outline anticipated and justified (a fourth Bearings retrieval would push the chapter's densest recall checkpoint off its own topic). No action.

**One caveat on Q10 as a floor item.** It is one of the two ≥4-back redundancy items, and § Per-question findings shows its correct answer is pre-disclosed in the Soundings key. Redundancy that can be answered by phrase-matching an earlier page is not redundancy. Fixing Q10's wording (above) restores it.

**Recommended additions if the §7 shortfall is corrected:** the two missing Practice questions should carry no additional retrieval — the budget is met. Add them as §7 content items (see below).

---

## Coverage vs concepts

Checked against `outline.md` `kb_tags.concepts` (52) and `kb_tags.commands` (3). "Tested" means a question's correct answer, or the rejection of a distractor, requires the concept.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| `network-model`, `no-nat-rule`, `cluster-wide-ip` | yes (B1.1, P1) |
| `pod-ip`, `pod-network-namespace`, `localhost-communication` | yes (S2, B1.2, P2) |
| `pod-network` / `cluster-network` (the terms) | partial — rule 2 is tested (P1); the vocabulary is not |
| **`node-agent-reachability` (rule 4)** | **NO** — appears only inside a *wrong* option (P20 C, L1201) |
| `cni`, `container-network-interface`, `network-plugin` | yes (P3, P20) |
| **`network-unavailable-condition`** | **NO** — taught at L200, never tested |
| `service`, `stable-endpoint` | yes (P4, B1.4) |
| `service-selector` | yes (P10, P11, P14, B2.1) |
| `clusterip`, `service-type-ladder` | yes (P5, P6, B1.3) |
| `nodeport` | yes (P6) |
| `loadbalancer` | yes (P7, B1.5) |
| `externalname`, `cname-record` | yes (P8, P9, B1.5) |
| `virtual-ip` | yes (P19, B3.2) |
| `endpointslice`, `endpointslice-controller` | yes (P11, P13, P14, B2.1) |
| `endpoints-controller` | no — named in §5 (L521) and P12's key; never the subject of an item |
| `readiness-gated-membership` | yes (P12, P13, B2.2) |
| `terminating-endpoint` | yes (P13) |
| `headless-service`, `cluster-ip-none` | yes (P16, B2.4, B3.5) |
| `service-without-selector`, `manually-managed-endpointslice` | yes (P17, B2.5) |
| `service-proxy`, `kube-proxy`, `kube-proxy-optional` | yes (P19, P20, B3.1, B3.3) |
| `kube-proxy-modes` + all four mode concepts | yes (P18, B3.3) |
| **`coredns`** | **NO** — see note below |
| **`dns-addon`** (built-in, launched by the addon manager) | **NO** — taught at L735, never tested |
| `cluster-dns` | partial — P21 tests the search list; nothing tests what *serves* the records |
| `service-dns-record` | yes, but **Bearings only** (B3.4, B3.5) — no Practice item |
| **`a-record` / `aaaa-record`** (as record types) | **NO** — stated at L741 and L828, never tested |
| **`srv-record`** | **NO** — taught at L786, figured at L803, tabled at L825; never tested |
| **`pod-dns-record`** (dashed IP, `pod` not `svc`) | **NO** — taught at L788, figured at L806; never tested |
| **`hostname` + `subdomain` FQDN form** | **NO** — taught at L790, closes the StatefulSet loop; never tested |
| `dns-search-list`, `fqdn`, `cluster-domain` | yes (P21, B3.4) |
| `dns-policy`, `cluster-first` | **no — correctly so.** Outline: *"Not a Fixed Point, not in the Exam Alert, not in a question."* ✅ deliberate |
| **§8 Zenith (the synthesis claim)** | **NO** — see § Question-budget compliance |

### Commands

| Command (outline `kb_tags.commands`) | Taught? | Tested? |
|---|---|---|
| `kubectl-get-endpointslices` | yes (L487) | yes (B2.3, P14) |
| **`kubectl-get-services`** | **NO — absent from the draft entirely** | no |
| **`kubectl-describe-service`** | **NO — absent from the draft entirely** | no |

Two of the three commands the outline tagged for this chapter never appear. A reader finishes the chapter's networking coverage having been shown how to inspect an EndpointSlice but never a Service. Strictly this is a drafting gap rather than a question gap (rule 5 triggers on *introduced-then-untested*), but it is reported here because the question set is where it would have been caught.

### The CoreDNS problem

CoreDNS is taught three times in §7 (L733, L735, L737) as the payoff for two published cross-bearings — Ch 3 line 603 promised it by name, Ch 4 line 588 deferred *"what serves the records"* to this chapter. It then appears in the question set **three times, and every time as a wrong answer**: P11 option D (L1121), P19 option D (L1193), P21 option A (L1208).

A reader who drills only the questions learns that CoreDNS is never the answer. The chapter discharges a two-chapter promise in prose and then trains against it. This is the clearest single argument for restoring the §7 Practice block.

### Recommended additions

Two Practice questions, restoring §7 to its budgeted 3 and closing the largest coverage gaps at once:

1. **A written-name item** (satisfies the outline's *"must require the reader to write a name"* requirement, and can carry the SRV or Pod-record shape as a second part). Suggested: *"A Pod in namespace `billing` must reach the `metrics` port — named `http`, TCP — on a Service called `ledger` in namespace `payments`. Write the SRV name it would query. Then write the name it would use for an ordinary A-record lookup of the same Service."* Tests `srv-record`, the four-label invariant, and the FQDN rule in one item.
2. **A CoreDNS / headless discrimination item**, restoring the outline's missing **Headless + DNS + StatefulSet** interleave. Suggested: *"A StatefulSet's three Pods sit behind a headless Service. A client resolves the Service name and gets three addresses; it then needs to reach one specific member. Name what serves both lookups, and write the name form that reaches an individual member."* Tests `coredns`, `hostname`+`subdomain`, and the headless resolution behaviour — three of the six untested §7 items — and makes CoreDNS a correct answer for the first time.

Optionally, a third addition would restore the Zenith item the outline specified; if the Practice budget is held at 21, the cheapest home for it is as a sixth item on Bearings #3, or in place of Q16 pending that question's rebuild.

---

## What is working

Recorded so the fixes above are read in proportion.

- **All six of the outline's named answer-key requirements are met**, several of them well: B1.3 states additivity as a rule about the ladder rather than a fact about NodePort (L374–376); B1.5 declines to moralise about the bare-metal LoadBalancer surprise (L390); B2.2 connects readiness to Ch 6's rolling updates explicitly (L595); B2.5 names proxying as the discriminator and bolds it (L620); B3.3 explicitly refuses to claim any kube-proxy mode is faster (L876) — a clean Ethical Guardrail #4 hold; B3.4 states the *silent wrong answer* failure rather than settling for "it fails" (L882–884).
- **Bearings #2 item 3 carries its Part 10B difficulty label** (L577), normalises the struggle, and explains why the difficulty is desirable. Its answer key (L597–606) is the strongest in the chapter — four distinct wrong instincts, each named and refuted.
- **Trap coverage is broad.** Seven of B1's eight catalogued Ch 9 traps are defused in both a callout and a question. The each-container-gets-an-IP misconception (#36) appears as a distractor in P1 and across P2's option set as the outline required, in addition to its Bearings appearance.
- **Recall-versus-prediction calibration hit the outline's target** (8 recall / 13 prediction-diagnosis).
- **The retrieval floor has its planned redundancy**, so no single item is load-bearing for `[B3]` compliance.

One trap-coverage shortfall worth logging without a per-question block: the outline required trap **#37** (*"NodePort replaces ClusterIP"*) to appear *"at least twice in two different question shapes."* It appears in its exact wrong form once, at **P6 option A** (L1074). **P5 option C** is the mirror-image error (ClusterIP wrongly credited with node reachability) rather than #37 itself. Bearings #1 item 3 tests the same fact but is open-response, so it presents no wrong option. If the §7 rebuild touches the §3 block, adding #37 to one more distractor set closes this.