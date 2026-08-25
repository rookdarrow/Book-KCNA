# Integration Check — KCNA Chapter 9

**Chapter:** 9 — Every Pod Has an Address
**Checked against:** shipped Chapters 1–8 and 10 (`../Book-KCNA/chapter-*.md`), the BINDING B6 section skeleton, and the BINDING B7 term ownership ledger.
**Note on inputs:** the stage received `[no knowledge-base shards tagged]`, so every claim below about an earlier chapter was verified directly against the shipped file and is cited by line number. **Chapter 10 is drafted and on disk** (`chapter-10-traffic-from-beyond-the-cluster.md`, 2026-08-25) and points into this chapter by section number; it is therefore treated as shipped canon for this check, not as a planned chapter.

---

## Summary

- Terminology consistency: **pass for this chapter** — 1 book-wide drift flagged, and Chapter 9 is on the correct side of it (§ *Terminology consistency*, drift D1)
- Callbacks to earlier chapters: **25 correct / 12 incorrect** (33 body cross-bearings carrying `§N`, plus 4 inline `Chapter N §M` references in Soundings)
- Retrieval-practice accuracy: **pass** — all 7 tagged items land on material the named chapter actually covers; 3 verified verbatim against the source chapter's own wording
- Glossary coverage: **31 concepts introduced, 27 defined in the chapter, 2 ledger-assigned terms absent entirely, 10 require glossary entries**
- Contradictions with earlier canon: **4 flagged** (2 of them created *by* this revision, in already-shipped Chapter 10)
- Ethical guardrails (skill Part 14): **pass with 2 items for author decision** — no fabricated statistics, no fear-mongering, no strawmanning; two unhedged exam-frequency claims fall short of the hedging standard Chapters 2–7 set for themselves

**One structural finding outranks everything else in this report.** The chapter ships **eight** numbered sections; the BINDING skeleton specifies **seven**, and assigns kube-proxy to §5, DNS to §6, and the Zenith to §7. The draft's numbering is `§5 headless/selectorless · §6 kube-proxy · §7 DNS · §8 Zenith`. Chapter 10 — drafted *after* the skeleton — already points into the chapter's **eight-section** numbering in five of six places. The skeleton is stale, not the chapter; but the two must be reconciled before Chapter 11 drafts. See § *Recommended fixes*, item **F1**.

---

## Terminology consistency

Every technical term in this chapter that was introduced in an earlier chapter was checked for surface-form drift against the shipped text and against the B7 ledger's Canonical forms table.

| Term | Canonical form | Occurrences in this chapter | Drift? |
|---|---|---|---|
| Pod (the object) | `Pod`, capitalized | ~120 | No |
| pod networking / pod network | lowercase (sanctioned exception) | 6 | No — matches the ledger's sanctioned lowercase carve-out |
| kubelet | `kubelet`, lowercase | 3 | No |
| kube-proxy | `kube-proxy`, lowercase hyphenated | 34 | No — matches shipped Ch 3 §3 exactly |
| kube-controller-manager | lowercase, hyphenated | 3 | No |
| EndpointSlice | `EndpointSlice` CamelCase | 76 (61 singular, 15 plural) | No — the 11 lowercase hits are all inside `kubectl` commands and the `kubernetes.io/service-name` label |
| ReplicaSet · StatefulSet · DaemonSet · Deployment · CronJob · ConfigMap · NetworkPolicy · RuntimeClass | exact CamelCase, unspaced | all present | No |
| Service (the object) | `Service` capitalized; generic English "service" lowercase and avoided nearby | ~180 | No — the lowercase instances are inside sourced quotations, which is correct |
| ClusterIP (type) vs cluster IP (address) | type CamelCase, address two lowercase words | 21 / 38 | No — the distinction is held consistently and is load-bearing in §6 |
| CoreDNS | `CoreDNS` | 6 | No |
| Calico · Cilium · Flannel | proper case | 8 | No |
| kubectl | lowercase, code style, never sentence-initial | 9 | No |
| etcd | lowercase | 1 (§8) | No |
| Gateway API / Ingress | `Gateway API` two words; `Ingress` capitalized, name-only + pointer before Ch 10 | 2 / 4 | No — both name-only with pointers, as the ledger requires |
| ⚠ Navigational Hazards (not "Shoals Ahead") | post-v5.5 name | 2 | No |
| ☀️ Zenith (not "Landfall") | post-v5.5 name | 1 | No |
| The Voyage Ahead (not "The Road Ahead") | LOCKED 2026-04-19 | 1 | No |
| Voyage Progress `🗺️→🌊→🌅` | post-v5.6 symbols | 1 | No — symbols correct; **denominator wrong**, see C3 |
| cloud native | never hyphenated | 0 hyphenated | No — Ch 9 and Ch 10 are the only two chapters with **zero** `cloud-native` instances, i.e. they are already clean of ledger flag ⚑8 |

### D1 — the fourth pluggable interface is named two different ways in shipped text

This is the one real terminology drift, and **Chapter 9 is on the correct side of it.**

- Shipped **Ch 2** §4 (line 598) and §8 (lines 914, 930) name the canon as **"CRI, CNI, CSI, and API extensions."**
- Shipped **Ch 6** §8 (line 1032) names it **"CRI, CNI, CSI and CRDs."**
- The B6 skeleton (Ch 17 §4), the B7 ledger, and **Chapter 9 §1** all say **CRDs**.

Three sources to one, so Chapter 9 matches the majority and needs no edit. The fix belongs to Ch 2 (three instances) or to a Ch 17 §4 reconciliation. Recorded here because Chapter 9 §1 emits `*[cross-bearing: see Ch 2 §4 — CRI, CNI, CSI and CRDs as the four pluggable interfaces]*` and says "That section named CNI and pointed you here" — which is true of the pointer (Ch 2 line 600 emits `see Ch 9 §1 — CNI and pod networking`) but describes Ch 2's list using Ch 6's vocabulary. A reader who turns back will find a different fourth item than the label promised.

### D2 — an unregulated synonym pair, proposed for the ledger

The chapter uses **"endpoints controller"** and **"EndpointSlice controller"** interchangeably and reconciles them explicitly three times (§4, §5, Bearings #2 answer 2). That handling is correct — both names are the Kubernetes documentation's own, and the draft is right to say "one job, two names." But the B7 Canonical forms table does not govern the pair, and it will recur in Ch 13 §7 and Ch 16 §4. **Recommend adding a row**: headword `EndpointSlice controller`; `endpoints controller` sanctioned only when quoting or paraphrasing the Pod-lifecycle page, and never without the reconciliation sentence.

---

## Callback correctness

### Prose callbacks — all verified against shipped text

| Claim in Ch 9 | Verified against | Verdict |
|---|---|---|
| "Chapter 8 pointedly did not tell you that. It had reason not to: the claim wasn't sourceable in that chapter's material" | Ch 8 line 1408 AUTHOR-REVIEW says exactly this, in the same terms | **Correct — unusually precise** |
| Ch 8 "closed by naming what Part II had carefully avoided asking, and by describing what comes next as addresses, the abstraction that makes them survivable, how names resolve, and how anything outside the cluster gets in at all" | Ch 8 line 1401 ("a question Part II has been carefully not asking") and line 1410 (the four-item list, **verbatim**) | **Correct — verbatim** |
| "Part III of this book opens with this chapter" | Ch 1 line 398: `III Underway · Ch 9–13 · Container Orchestration · 28%` | **Correct** |
| §1: "Chapter 6 noted in passing that cluster networking plugins commonly ship as DaemonSets, one Pod on every node" | Ch 6 §7 line 890: "Cluster networking plugins ship as DaemonSets" | **Correct** (Ch 9 adds "commonly," a defensible softening) |
| §1: "You met the node condition list in Chapter 8" | Ch 8 §4 (lines 638–730) owns node conditions incl. `NetworkUnavailable` | **Correct** |
| §4: "Chapter 6 … Its answer key established that a Service uses labels to allow the control plane to determine which EndpointSlice objects are used for that Service, and that … each EndpointSlice … carries an owner reference" | Ch 6 line 537, answer key to Bearings #1 Q5 — same two mechanisms, same source tag | **Correct** |
| §4: "Chapter 5 taught you readiness probes and told you plainly that this is the mechanism doing the removing" | Ch 5 §7 line 858: "When Chapter 9 explains how a Service knows which Pods to send traffic to, **this is the mechanism doing the removing**" | **Correct — verbatim** |
| §4: "Chapter 6 relied on the mechanism without explaining it … a bad release cannot take a Service down mid-rollout" | Ch 5 line 858 makes the same connection and points at Ch 6 §4 | **Correct** |
| §4: Ch 7 "argued that a Service's backends landing on distinct nodes is what makes it resilient rather than merely load-balanced" | Ch 7 §5 line 881, **verbatim** | **Correct** |
| §5: "Chapter 6 already handed you the answer and then deferred it" (StatefulSet requires a headless Service) | Ch 6 §6 line 870, including "you are responsible for creating it" | **Correct** |
| §6: "Chapter 3 introduced kube-proxy as a node component … and left the 'how' for here" | Ch 3 §3 lines 453–459, which closes with `see Ch 9 — Services, and how kube-proxy implements them` | **Correct** (pointer target wrong — see B6 below) |
| §7: "Chapter 3 promised you CoreDNS by name" | Ch 3 §4 line 603 | **Correct** |
| §7: Chapter 4 "gave you a Service's DNS name in a single sentence and explicitly deferred four things: the mechanism, what serves the records, what else gets one, and how resolution actually proceeds" | Ch 4 §3 line 588, **verbatim four-item list** | **Correct — the best callback in the chapter** |
| §7 / Practice Q21: "Chapter 4 gave you the rule flat: a bare `<service-name>` resolves to the Service local to your namespace" | Ch 4 §3 line 588 | **Correct** |
| §8: "which is exactly what Chapter 6 was telling you when it distinguished selection from ownership" | Ch 6 §3 line 539: "**Ownership is exclusive; selection is not.**" | **Correct** |
| §8: "the second instance of an arrangement you first met in Chapter 2, where CRI does the same thing" | Ch 2 §4 line 598, §8 line 914 ("This is the **first** of four times") | **Correct** |
| **§2: "And Chapter 6 was precise about what 'replaced' means: … never rescheduled … replaced by a new, near-identical Pod with a different UID"** | The sentence is **Ch 5 §4's** (lines 531–533), where it is the section's spine. Ch 6 restates it only in a Practice answer (line 1372) | **Misattributed — see B7** |
| **§8: "That is the sixth control loop in this book, and you should count it."** | Ch 8 §4 line 713 already claims the node controller as **"the sixth"**, and line 1071 repeats it | **Contradiction — see C1** |

### Cross-bearing audit — mechanical, against the B6 skeleton

33 body cross-bearings carry a `§N`. **24 resolve correctly; 9 do not.** All nine are recorded below with the skeleton's number as the fix. Two further pointers resolve to a real section but carry a label that overstates or straddles what that section owns.

| # | Emitted | Skeleton says that section is | Should be | Where |
|---|---|---|---|---|
| B1 | `Ch 5 §2 — the Pod's shared network namespace` | §2 = *More Than One Container Aboard* | **`Ch 5 §1`** | §1 |
| B2 | `Ch 5 §3 — Pod ephemerality` | §3 = *Everything That Must Happen First* (init containers) | **`Ch 5 §4`** | §2 |
| B3 | `Ch 4 §7 — labels and selectors` | **Ch 4 has no §7.** Labels/selectors are §5 | **`Ch 4 §5`** | §2 |
| B4 | `Ch 4 §4 — spec and status` | §4 = *Configuration Kept Outside the Image* | **`Ch 4 §2`** | §2 |
| B5 | `Ch 3 §3 — the controllers inside kube-controller-manager` | §3 = *Node Components in Context* | **`Ch 3 §2`** | §4 |
| B6 | `Ch 3 §4 — kube-proxy as a node component` | §4 = *Addons, and What Else Is Optional* | **`Ch 3 §3`** | §6 |
| B7 | `Ch 17 §3 — a service mesh …` | §3 = *Small Pieces, Replaced Whole* | **`Ch 17 §5`** | §6 |
| B8 | `Ch 6 §2 — selection versus ownership` | §2 = *A Loop You Can Watch Working* | **`Ch 6 §3`** | §8 |
| B9 | `Ch 15 §5 — the control loop … pointed at a Git repository` | §5 = *Ordering the Sync* | **`Ch 15 §7`** | §8 |

B5 and B6 are a **swap**: the controller roster genuinely sits in Ch 3 §2 (shipped line 421, inside §2's span 354–434) and kube-proxy genuinely sits in Ch 3 §3 (shipped lines 453–459). **This resolves the open AUTHOR-REVIEW at §4** that could not adjudicate B5 from the skeleton alone — the shipped text settles it: **Ch 3 §2**. (Incidentally, the B7 ledger's Ch 9 row records EndpointSlice as first appearing at "Ch 3 §3"; that is a ledger erratum — line 421 is §2. No draft change follows from it.)

B8 is also internally inconsistent: §4 and Bearings #2 both point the *same* concept at `Ch 6 §3` correctly; only §8 says `§2`.

**Two labels that resolve but overstate:**

- §1's `Ch 2 §4 — CRI, CNI, CSI and CRDs as the four pluggable interfaces` — the section exists and does name CNI, but calls the fourth member "API extensions." See drift D1.
- §3's `Ch 8 §1 — a Service is created by the same apply, through the same API server door, as every other object` — Ch 8 §1 owns the kubectl grammar; "the API server door" is **Ch 3 §5** (*The Only Door In*). Consider splitting into two pointers or trimming the label to the `apply` half.

**Correct and worth naming, because several were repaired in this revision and the repairs are right:** `Ch 5 §7` (readiness), `Ch 6 §3` (×2), `Ch 6 §4` (×3), `Ch 6 §6` (×3), `Ch 6 §7`, `Ch 7 §5`, `Ch 8 §4`, `Ch 3 §4` (CoreDNS/addons), `Ch 4 §3` (namespaces + Service DNS), `Ch 16 §4`, `Ch 11 §6`, `Ch 17 §4`, `Ch 2 §4` (§8's CRI instance), `Ch 10 §1`, `Ch 10 §2`, `Ch 10 §6` (×2). The §4 and §7 AUTHOR-REVIEW sweeps were accurate; every retarget they made checks out against both the skeleton and the shipped files.

### Inline section references in Soundings — 3 of 4 wrong

These are outside the `cross-bearing` convention and were missed by both sweeps:

- Answer 2: `*(Chapter 5 §2.)*` → **Ch 5 §1**
- Answer 4: `*(Chapter 4 §7, Chapter 6.)*` → **Ch 4 §5**
- Rubric: "go back to **Chapter 5 §2** and Chapter 6 §4" → **Ch 5 §1** (the Ch 6 §4 half is correct)
- Answer 3: `*(Chapter 6 §4.)*` → correct

### B2 needs more than a number change

§2 reads: "`*[cross-bearing: see Ch 5 §3 — Pod ephemerality]*`, where you were told **in as many words** that this fact is the premise of Chapter 9."

Ch 5 §4 is the ephemerality section, but it points forward to **Chapter 6**, not Chapter 9. The "premise of Chapter 9" sentence actually lives in **Ch 5 §1**, line 365 — and it is about *the Pod, not the container, holding the address*, not about ephemerality: *"That one fact is the premise of Chapter 9. When you get to Services, the entire argument for why they must exist rests on the Pod having an IP that changes when the Pod is replaced."* Retargeting to §4 fixes the number but leaves the "in as many words" claim false. **Author's call**, two clean options: point at `Ch 5 §1` and keep the claim, or point at `Ch 5 §4` and drop "in as many words."

---

## Retrieval-practice accuracy

Seven tagged items. **All seven are topically accurate.** Three land on wording the source chapter uses verbatim, which is the strongest possible result for this check.

| Item | Tag | Claim | Verified against | Verdict |
|---|---|---|---|---|
| Bearings #1 · 2 | `ch5` | Two containers, one port space, `localhost`, one address | Ch 5 §1; answer key line 475 calls "two IPs, one per container" the misconception the chapter exists to correct | **Correct** |
| Bearings #1 · 4 | `ch6` | Rolling update → every Pod replaced → every address different | Ch 6 §4; Practice answer line 1372 names name, UID **and IP address** as invalidated | **Correct** |
| Bearings #2 · 1 | `ch6` | "a Service asking the same question … is a *different controller reading the same labels*" | Ch 6 §3 line 485 uses that phrase **verbatim** | **Correct — verbatim** |
| Practice 2 | `ch5` | Three containers → one address, one endpoint | Ch 5 §1 | **Correct** |
| Practice 9 | `ch4` | One Pod, two independent selectors, no coordination | Ch 4 §5 (line 835); Ch 6 asks a near-identical question at Bearings #1 Q5, itself tagged `[retrieval: ch4]` | **Correct** — the near-duplication is deliberate spaced retrieval, not a collision |
| Practice 11 | `ch5` | Readiness probe → which object it acts in | Ch 5 §7 line 858, the explicit forward plant | **Correct** |
| Practice 21 | `ch4` | Bare name resolves in the caller's namespace | Ch 4 §3 line 588 | **Correct** |

**Two observations, neither a defect:**

1. **Bearings #3 carries no retrieval item.** Bearings #1 has two, #2 has one, #3 has none. Skill Part 10 sets 20–25% for chapters 6+; the chapter lands at 3/15 = 20% across checkpoints and 7/37 = 19% across all graded items — at the floor, and just under it on the Practice block. One retrieval item in Bearings #3 would close it. §7's DNS material pairs naturally with Ch 4 §3's namespace scoping.
2. **Soundings items 2–5 are prerequisite pretests against Chapters 4, 5 and 6.** That is correct Soundings design and is not counted above, but it is worth recording that this chapter's pre-test load on earlier chapters is heavier than its post-test load.

**Soundings spoiler item — the ratified remedy was applied, partially.** The Soundings AUTHOR-REVIEW routes the fix to §7: rewrite the Fixed Point so its claim rests on the DNS search list, the one thing Soundings Q5 withholds. §7's second Fixed Point now reads *"A bare name resolves in the client Pod's own namespace only — **because that namespace is in the Pod's DNS search list**"* — the remedy, applied as specified. **Residual:** §7's *first* Fixed Point still turns on the name form `<service>.<namespace>.svc.<cluster-domain>`, which Soundings Q5 discloses in full. The comment can be updated to record the partial closure rather than left describing an unstarted edit.

---

## Glossary coverage

31 concepts and commands are introduced or used in this chapter. 27 are defined in place.

**Ledger-assigned terms this chapter owns and delivers** (no glossary entry required): Kubernetes network model · Pod IP · NAT-free pod-to-pod traffic · CNI · CNI plugin · Calico/Cilium/Flannel · Service · ClusterIP · virtual IP · NodePort · LoadBalancer · ExternalName · Service selector · EndpointSlice · headless Service · Service without selectors · readiness gating endpoint membership · kube-proxy and its modes · CoreDNS · cluster DNS · A/AAAA record · SRV record · FQDN · `svc.cluster.local` · search domain · Pod DNS record · flat network.

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| **`port` / `targetPort` / `nodePort`; node-port range** | **no — absent entirely** | **no — needs teaching, not a glossary line. See F3** |
| **`Endpoints` (the legacy object)** | **no — absent entirely** | **no — needs one contrast sentence in §4. See F4** |
| CNAME record | used 8× as load-bearing to ExternalName; never defined or expanded | **yes** |
| eBPF | named twice (§1, §6) and used as a graded distractor in Practice Q16 | **yes — and see G2** |
| BGP | named once (§1), never expanded to Border Gateway Protocol | **yes** |
| IPVS | named 9×, never expanded to IP Virtual Server | **yes** — and expand on first use in §6 |
| nftables · iptables · kernelspace | named as mode labels; no definition needed at this tier | **yes**, one line each |
| overlay network · native routing · encapsulation | quoted from the addons page; never glossed | **yes**, one combined entry |
| `dnsPolicy` values (`ClusterFirst`, `Default`, `ClusterFirstWithHostNet`, `None`) and `dnsConfig` | glossed in a 🔭 Closer Look, correctly marked out of scope | **yes** |
| `serving` / `terminating` EndpointSlice conditions | glossed in §4 and its Closer Look | **yes** |
| NXDOMAIN | used once, Bearings #3 answer 4, unglossed | **yes** |
| "GA since Kubernetes 1.33" | unglossed release-stage jargon | **yes**, or defer to Ch 17 §8's KEP/feature-stage material |
| `kubectl get endpointslices -l kubernetes.io/service-name=…` | shown and explained in §4 | no |
| `NetworkUnavailable` | named with a pointer to Ch 8 §4, which owns it | no — correct handling |

**Ten glossary entries required.** Six of them (CNAME, BGP, IPVS, eBPF, overlay/encapsulation, NXDOMAIN) are **acronyms or protocol terms making their first appearance in the book in this chapter** — verified: none appears in Chapters 1–8 or 10. The B7 acronym register's rule is "every acronym is expanded on its first use in the book, without exception"; IPVS is in the register (→ *IP Virtual Server*) and is not expanded here, and BGP, CNAME and eBPF are not in the register at all. Stage 14 will need register rows for the three missing ones.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Every numeric claim is either source-tagged or explicitly declared as authored. The metadata line carries the required transparency clause ("CNCF publishes domain weights only, not competency weights; see front matter"), matching the pattern locked in Chapters 2–7. Cross-referenced with the fact-accuracy audit: its findings (F2, F4, F6) are recorded as AUTHOR-REVIEW blocks rather than papered over, and every claim narrowed by the revision was narrowed *downward* to what the corpus supports. No untagged assertion of a number anywhere in the chapter.
- [x] **Fear-based content uses real examples.** The chapter's two "this will cost you" beats — the bare-name silent misresolution (§7 Navigational Hazards, Bearings #3 answer 4) and the two-causes-of-an-empty-endpoint-list diagnostic (§4 Snag) — are both documented behaviours with source tags, not invented scenarios. No manufactured stakes.
- [x] **Simplification acknowledged.** Dead Reckoning blocks in *Why This Chapter Matters* and §7. Four 🔭 Closer Look blocks, each labelled "Deeper than the exam requires." §8's "Where the claim overreaches" is an explicit, unprompted narrowing of the chapter's own thesis — the Order/Truth pattern applied to the book's own argument, which is above standard.
- [x] **Authority claims cite legitimate sources.** All tags resolve to dated snapshots in `sources/`. The three claims the revision could not source are marked absent rather than asserted.
- [ ] **"Frequently tested" claims verifiable against the curriculum snapshot** — **2 items for author decision.** See G1.
- [x] **No strawmanning of alternative study methods.** None present.
- [x] **Subject dignity (skill v5.7, Part 14 item 9).** The wry beats — "explaining at eight the next morning why the logs say every request came from the same three addresses," "the wrong database, answering questions it shouldn't have been asked," "there is nobody ashore to answer it" — are all oriented at the practitioner's own experience. Nothing is aimed at harm borne by people not in the room. **Pass.**

### G1 — two unhedged exam-frequency claims

Chapters 2–7 hold themselves to an explicit standard: every share-of-exam figure carries "authored allocation — CNCF publishes domain weights, not competency weights," and Ch 3 line 238 goes further ("treat that number as an estimate the author is accountable for, not as a figure from the curriculum"). The B7 ledger applies the same discipline to trap material: "`[inferred]` traps described as 'easy to confuse,' never as 'frequently tested'." Two lines in this chapter fall short of that bar:

1. **Attention Budget:** *"That is where this chapter's exam points concentrate."* Stated as fact. The published curriculum gives domain weights only; item-level concentration within a competency is authored judgment.
2. **§3, closing the decision list:** *"The exam tests the definitions and the additivity far more often than it tests the decision."* A relative-frequency claim about exam items, and the strongest one in the chapter.

Neither is dishonest and both are probably right, but both assert knowledge of item distribution that no snapshot supports. Suggested repair, matching house phrasing: "on this book's judgment, that is where this chapter's exam points concentrate" and "definitions and additivity are more testable than the decision, and this book weights them accordingly." A third line — §3's *"Every exam question that presents it as 'the type you use for external things' is testing exactly this"* — is closer to a claim about what a question *would* be testing than about how often one appears, and reads as acceptable.

Worth naming for contrast: **Bearings #3 answer 3 is a model of the standard.** *"it makes no claim about which mode is faster, more scalable, or better … The documentation states the list, the default, and the substitution, and says nothing about relative performance — so neither does this book."* That paragraph is the chapter arguing against its own convenience, and it is the right template for the two above.

### G2 — a graded distractor uses a term the ledger declared ineligible

The B7 ledger routes **eBPF** to the orphan list: *"glossary-only. Any of the three sections may name it as an implementation detail **with a pointer to the glossary**. **Not eligible for graded text.**"*

This chapter names eBPF twice with **no pointer** (§1's Cilium description, §6's Closer Look), and uses it as **distractor C in Practice Q16**, with the answer key explaining "eBPF, which is a plugin data plane rather than a kube-proxy mode." A reader who does not already know what eBPF is has nowhere in this book to look it up, which is precisely the condition the ledger's ruling exists to prevent. Not an ethics failure — the distractor is fair and the fact is true — but it is a ratified-decision violation. **Author's call:** write the glossary entry and add the pointers, or swap the Q16 distractor for one built from taught material.

---

## Contradictions with earlier canon

### C1 — the control-loop ordinal collides with Chapter 8. *High.*

§8: *"That is the **sixth** control loop in this book, and you should count it."*

Shipped Ch 8 §4, line 713: *"You met the pattern in Chapter 3, and you have seen five instances of it since. **This is the sixth**."* Reinforced at Ch 8 line 1071: *"It is the sixth one in this book."*

Chapter 8 has already spent the sixth. Worse, this chapter contains **two** loops it identifies as such — the EndpointSlice controller (§4, §8) and kube-proxy (§6, §8) — so kube-proxy is at least the seventh and arguably the eighth. Because the ordinal is an invitation to count ("and you should count it"), a reader who *does* count will find the book contradicting itself two chapters apart.

**Fix is the author's call, and the choice matters** because Ch 15 §7's Zenith is built on the reader having tracked this sequence: (a) audit the running count across Chapters 3–9 and renumber here, or (b) drop the ordinal in favour of a non-counting formulation ("another control loop, in a reference page about packet forwarding"). Option (b) is cheaper and removes a class of future breakage; option (a) preserves a deliberate running gag that Ch 8 clearly intends. **Do not renumber to "seventh" without the audit** — this chapter itself may consume two.

*Incidental, and Chapter 8's defect rather than this one's:* Ch 8 line 713 points at `Ch 3 §5 — the control loop`. The control loop is **Ch 3 §6**; §5 is *The Only Door In*. Recorded for a future Ch 8 sweep.

### C2 — Chapter 10 attributes to Chapter 9 a claim this revision removed. *High.*

Shipped Ch 10 §6, line 1228: *"Chapter 9 taught that Kubernetes **defines** the network model and **implements none of it**: a CNI plugin does the actual work…"*

This revision deliberately narrowed exactly that claim. Its §1 AUTHOR-REVIEW: *"the stronger 'implements none of it' form is not sourceable here,"* and the §1 Fixed Point and Exam Alert item 12 were both rewritten to "a CNI network plugin **implements** it." Chapter 10 now cites Chapter 9 for something Chapter 9 no longer says.

**This is a revision-induced regression in already-shipped text, not a pre-existing defect**, and it is invisible from inside Chapter 9. Either Ch 10 line 1228 is trimmed to match, or — the better outcome — the pending `k8s-docs-network-plugins-2026-08-24` fetch lands and both chapters are strengthened together, which is what Chapter 9's own AUTHOR-REVIEW anticipates.

### C3 — Chapter 10 says the kubelet executes CNI binaries; Chapter 9 deliberately does not. *Medium.*

Same line, Ch 10 line 1228: *"network plugins are binary plugins **the kubelet executes**."*

This revision dropped the kubelet as executor per curriculum finding R3 (CNI management was removed from the kubelet in Kubernetes 1.24; the container runtime loads the plugins), and §1's AUTHOR-REVIEW instructs: *"Naming no executor is the safe form at associate tier. **Do not restore** 'external programs that the kubelet executes.'"* Practice Q3's option B and explanation were rewritten accordingly.

Chapter 10 still carries the superseded form, sourced to the same snapshot Chapter 9 judged too general to support it. Two adjacent chapters now give a reader two different answers to "who runs the CNI binary." Same fix window as C2.

### C4 — the Voyage Progress denominator is wrong. *Medium — resolves an open AUTHOR-REVIEW.*

The strip reads **"Ch 9 of 17."** The Chapter Summary's AUTHOR-REVIEW flags it and asks for a book-wide check. Here it is:

- Ch 4 line 1323: **"Chapter 4 of 20 complete."**
- Ch 5 line 1476: **"Chapter 5 of 20 complete."**
- B6 skeleton: Ch 1–20 (Ch 19 synthesis, Ch 20 mock exam).

**The denominator is 20**, and the shipped house phrasing is `**Voyage Progress:** 🗺️ → 🌊 → 🌅 — Chapter N of 20 complete.` This chapter's strip also differs in form (`🗺️ → 🌊 **Ch 9 of 17** → 🌅`, arrow-position-as-progress). Chapter 3 uses a third form again (per-section strips at lines 561/746/904). **Recommend**: fix the denominator to 20 now, since that is unambiguously wrong; treat the form divergence as a separate cosmetic sweep, since three forms are already in shipped text and this chapter is not the outlier that created the problem.

### Not a contradiction, recorded so a later stage does not "fix" it

§2 says a Service is "not a workaround for churn; it is the abstraction that makes churn a non-event," while Ch 6 line 431 points forward with "this churn is exactly why something needs a stable name." These are compatible framings of one idea, and Chapter 9's is the sharper one. No action.

---

## Recommended fixes

Ordered by consequence. Items marked **[resolves]** close an open AUTHOR-REVIEW by supplying information the earlier stage lacked; the revision stage did not miss these, it lacked access to the shipped files.

### F1 — reconcile the section count with the skeleton, in the skeleton's direction. *Blocking for Chapter 11 onward.*

The chapter ships **eight** sections; the BINDING B6 skeleton specifies **seven**:

| Skeleton | Draft |
|---|---|
| §5 *How the Traffic Actually Gets There* — kube-proxy | §5 — headless and selectorless Services |
| §6 *Finding It by Name* — CoreDNS/DNS | §6 — kube-proxy |
| §7 *A Stable Name Over Churn* — Zenith | §7 — DNS |
| — | §8 — Zenith |

Under the stage's own rule this is a defect. **The evidence says the skeleton is stale, not the chapter:**

- Both pinned published pointers still land. `Ch 9 §1 — CNI and pod networking` (emitted by shipped Ch 2 line 600) → draft §1 ✓. `Ch 9 §4 — readiness and Service endpoint membership` (emitted by shipped Ch 5 line 858) → draft §4 ✓.
- **Chapter 10, drafted after the skeleton, already assumes the eight-section numbering** in five of six places: `Ch 9 §3 — the Service type ladder` (×3), `Ch 9 §4 — selectors, EndpointSlices, and the empty case`, `Ch 9 §1 — CNI and the Kubernetes network model`, `Ch 9 §1 — the network model's second rule`, `Ch 9 §7 — DNS-based service discovery, and what it is not`, and `(Ch 9 §3)` / `(Ch 9 §4)` in its Practice answers and Chapter Summary.
- The draft's §5 split is pedagogically load-bearing: headless and selectorless Services are framed as *subtractions* from §3 and §4, which only reads if they follow both.

**Recommended action:** amend the B6 skeleton to the shipped eight sections and titles, then fix the two consequences:

- **F1a.** Shipped **Ch 10 line 951** emits `*[cross-bearing: see Ch 9 §6 — the client's resolver, which appears here as one step in a flow rather than as a topic]*`. Under the draft's numbering, §6 is kube-proxy. **Retarget to `Ch 9 §7`.** Chapter 10 is self-inconsistent here — its line 393 already points DNS at `Ch 9 §7` correctly. This is a broken pointer into this chapter in shipped text, and it is the one concrete breakage the renumber has already caused.
- **F1b.** Update the skeleton's Ch 16 §4 note, which reads "Refers to Ch 9 §4 and **§6**" (DNS). Under the shipped numbering that must be **§7**. Ch 16 is undrafted, so this costs nothing if fixed now and costs a rewrite if fixed later.
- **F1c.** Update the B7 ledger's Ch 9 rows: service proxy and kube-proxy modes move §5 → **§6**; CoreDNS, cluster DNS, A/AAAA, SRV, FQDN, `svc.cluster.local`, search domain and Pod DNS record move §6 → **§7**; headless Service and Service-without-selectors move §4 → **§5**.

If the author prefers to hold the skeleton and renumber the chapter instead, F1a inverts (Ch 10 line **393** becomes the broken one) and §5 must be resequenced after DNS — a substantive rewrite, not a renumber. Recommend amending the skeleton.

### F2 — fix the twelve broken section pointers. *High, mechanical.*

Nine cross-bearings (B1–B9 above) and three inline Soundings references. All twelve have an unambiguous correct value; apply as tabulated. **[resolves]** the §4 AUTHOR-REVIEW's open question — B5's target is **Ch 3 §2**, confirmed at shipped Ch 3 line 421, inside §2's span. B2 additionally needs a prose decision (see § *Callback correctness*).

The §7 AUTHOR-REVIEW asked for exactly this sweep at this stage. It is done; the retargets that sweep already made are all correct.

### F3 — the port-field gap is now a downstream contract breakage, not just a local omission. *High.*

`port`, `targetPort`, `nodePort` and the node-port range appear **nowhere in the book** — verified across all ten shipped chapters; the only hits are this chapter's three AUTHOR-REVIEW comments saying so. Two consequences the draft's own notes do not record:

- **Skeleton Ch 16 §4** plans "`port` vs `targetPort`" as an application-side Service failure mode, referring back to Chapter 9. It will refer back to nothing.
- The B7 ledger assigns the row to **Ch 9 §3** as an owned term. An owned term that is never defined leaves the ledger claiming coverage the book does not have.

The blocker is plumbing, not research: Stage 2 fetched `k8s-docs-service-ports-2026-08-24` on 2026-08-24 and could not write it to `sources/`; the body survives verbatim in `research-manifest.md` §3. **Extract the snapshot to `sources/`, re-run corpus assembly, then add the §3 block, the Practice item after Q8, and +2 min to the §3 Attention Budget row.** Until then, record the gap in the B7 orphan section so Ch 16's drafting stage is not surprised by it.

### F4 — the legacy `Endpoints` object is assigned to this chapter and absent from it. *Medium.*

B7 assigns "Endpoints (the legacy object) | Ch 9 §4" and the Canonical forms table reserves the capitalized form "only in Ch 9 §4's contrast." The chapter never mentions it. It is a real KCNA-adjacent term a reader will meet in older material and in `kubectl api-resources` output, and one sentence in §4 discharges it. Either write the sentence or move the row to the orphan list.

### F5 — the Voyage Progress denominator. *Medium.* **[resolves]**

`Ch 9 of 17` → the denominator is **20**. Evidence in § C4.

### F6 — the "sixth control loop" collision. *High, needs an author decision.* See § C1.

### F7 — Chapter 10's two stale attributions to this chapter. *Medium, edits land in Chapter 10.* See § C2 and C3.

### F8 — glossary and acronym-register work for Stage 14. *Medium.*

Ten entries listed above. Three of them (CNAME, BGP, eBPF) need **new rows in the B7 acronym register**, which currently omits them. IPVS is in the register but is unexpanded on its first appearance in the book, which is here — expand it in §6. **[resolves]** the register-rule question by confirming that all four are first-appearing in this chapter, verified across every shipped file.

### F9 — the eBPF graded-text ruling. *Medium, author's call.* See § G2.

### F10 — two exam-frequency claims to hedge. *Low.* See § G1.

### F11 — the DaemonSet source tag has no upstream to inherit. *Low.* **[resolves]**

§1's AUTHOR-REVIEW (fact-accuracy F4) offers option (a): "propagate whatever source tag Chapter 6 §7 carries for the same claim, if it carries one." **It does not.** Shipped Ch 6 line 890 asserts "Cluster networking plugins ship as DaemonSets" with no `[source:]` tag at all. Option (a) is unavailable; option (b) — fetching `kubernetes.io/docs/concepts/workloads/controllers/daemonset/`, whose "Use cases" section covers cluster networking daemons — is the only path, and it would retroactively fix Chapter 6 as well. Update the comment so a later pass does not spend time hunting for a tag that isn't there.

### F12 — three conformance items against the skeleton's own recommendations. *Low.*

- **Zenith glyph.** B6 Collision #4 recommends `☀️` on the closing section for Chapters 9–19. This chapter's §8 heading uses `⚪`. Shipped **Ch 10 §8 uses `☀️`**, as do Ch 5 §9, Ch 6 §9 and Ch 7 §7. Chapter 9 is now the outlier among its immediate neighbours. One-character fix.
- **Heading format.** `## ⚪ §1 — Title` ✓ correct per Collision #3, matching Ch 5–8 and Ch 10.
- **Metadata-line phrasing.** The disclosure is substantively right but does not match the exact wording Chapters 2, 5 and 7 use, and drops the `[source: cncf-kcna-curriculum-pdf-2026-08-23]` tag those lines attach to the disclosure clause. Chapter 6's own AUTHOR-REVIEW (line 192) already carries a ratified instruction to normalize on the Ch 2–5 phrasing; this chapter is in the same bucket as Ch 6 and Ch 8. Book-wide sweep, not a Chapter 9 blocker.

### F13 — optional, for consistency only. *Low.*

- **Bearings headings.** Chapters 1–6 use `#N: Topic`, Chapters 7–8 use `#N — Topic`, and Chapters 9–10 use bare `#N`. Six chapters to two. Adding topic labels here would match the majority; leaving it matches Chapter 10.
- **Sidebars.** No Logbook Entry or Extended Analogy. Seven of ten shipped chapters carry one or two; Chapters 5, 9 and 10 carry none. Skill §18.14 makes these optional, so this is a stylistic note, not a gap.
- **Margin-icon density.** 13 callouts (⚓4 · 🪝3 · 🔭4 · 🪢2) against the skill's "roughly 3–8." **Not a Chapter 9 finding** — the whole book runs high (Ch 2: 13, Ch 8: 15, Ch 5/6: 11, Ch 10: 13). Chapter 9 is at house median. If the band matters, it is a book-wide conversation.

---

## What the diagnostics already caught, and got right

Recorded so the revision stage is not asked to re-do work. Every narrowing this revision made in response to the fact-accuracy audit checks out: the CNI Fixed Point, Exam Alert item 12, the §3 additivity Fixed Point, the Chapter Summary's LoadBalancer row, and the Bearings #1 answer 3 statement were all pulled back to what the cached corpus supports, and each carries an AUTHOR-REVIEW naming the specific snapshot that would restore the stronger form. The §4 and §7 cross-bearing sweeps retargeted eleven pointers and **all eleven are correct** against both the skeleton and the shipped files. The Attention Budget arithmetic is right — rows sum to 99 against a stated ~100. The Soundings Q5 remedy was applied as ratified, with one residual noted above.

The findings in this report are what those passes could not see: the shipped text of the other nine chapters, and Chapter 10's already-drafted pointers back into this one.