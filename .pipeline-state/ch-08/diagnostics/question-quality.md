# Question-Quality Audit — Chapter 8

## Summary

- Chapter type: **content**
- Total questions inspected: **40**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **15** (across **3** checkpoints of 5)
  - Practice questions: **17**
- Question budget compliance: **met** (all four categories exactly on target)
- Weak distractors (WARN): **6 questions** carry at least one weak or non-isolating option (P1, P2, P6, P8, P13, P16)
- Trap answers that don't target real misconceptions (WARN): **3 options** (P1/C's plural clause, P4/C, P13/D)
- Missing or incomplete why-wrong explanations (FAIL): **0** — all 17 Practice items address every wrong option specifically
- Retrieval-practice spacing: **compliant** — 7 of 32 (21.9%), ≥4-back floor satisfied twice
- Soundings spoiler check: **clean** — no stem reveals a ★ Fixed Point; one answer-key rationale (S7) carries a partial forward reveal, logged as WARN

**The headline finding is not a defect in any single question — it is a distribution problem.** §6 (version skew, supported releases, cadence, upgrade order) received **2 Practice questions against an outline allocation of 4**, while §3 and §4 each ran one over. §6 supplies four of this chapter's ten Exam Alert high-priority topics and is flagged **[B3]** as the book's worst decay risk. Three of its concepts — the three-supported-minors rule, the patch-support window, and the release cadence — are tested **only** in Taking Your Bearings #3 item 3 and appear nowhere in the Practice set. Upgrade order is tested nowhere at all. See § Question-budget compliance → *Within-budget distribution*.

Two things this chapter does markedly better than its budget requires and that should not be lost in revision: every Practice answer key explains all three wrong options with a named misconception rather than a restatement of the correct answer, and all three checkpoints carry the 5/5 ÷ 3–4 ÷ 0–2 revision-prompt branch with a specific section and a time estimate attached to the low branch. Both are skill Part 11 requirements that are routinely skipped.

---

## Question-budget compliance

Compared against `question_budget` in the outline frontmatter:

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | **met** |
| Taking Your Bearings (total) | 15 | 15 | **met** |
| Taking Your Bearings (checkpoints) | ≥2 (outline: 3) | 3 | **met** |
| Practice Questions | 17 | 17 | **met** |
| **Chapter total** | **40** | **40** | **met** |

Each checkpoint carries exactly 5 questions, satisfying the skill's "2+ checkpoints of ≥5 questions each."

### Within-budget distribution — deviation from the outline's Practice allocation

Total is met; the allocation across sections is not. Attributing each Practice item to its primary section (interleaved items attributed to the section supplying the correct answer):

| Block | Outline target | Actual | Items | Status |
|---|---|---|---|---|
| §1–§2 — grammar, kubeconfig, gates | 5 | 4 | P1, P2, P3, P4 | short by 1 |
| §3 — quota / limit range | 2 | 3 | P5, P6, P7 | over by 1 |
| §4 — node lifecycle | 3 | 4 | P8, P9, P10, P11 | over by 1 |
| §5 — ownership / tooling | 2 | 1 | P12 | short by 1 |
| **§6 — versions and skew** | **4** | **2** | **P14, P15** | **short by 2** |
| §7 — etcd | 1 | 1 | P16 | met |
| §8 — synthesis | (folded into 17) | 1 | P17 | met |

**Why the §6 shortfall matters more than the arithmetic suggests.** The outline's §6 allocation was not padding. It carried three constraints the draft cannot now satisfy with two items:

- *"At least 2 must require applying a rule to a scenario rather than reciting the rule."* P14 applies; P15 recites. One of two, not two of four.
- *"#28 must appear at least twice in two different question shapes."* Satisfied — P14 (B vs D contrast) and P15 (option A) — but with zero slack.
- *"Includes 1 retrieval item."* P7 was designated "§6 block or §3 block, drafter's choice" and was drafted §3-flavoured. **§6 now carries no retrieval item.**

The two missing items also account for four of the thirteen untested concepts below. **Recommended fix:** convert P7 to its §6 framing (the outline permits it) and add one item on the three-branch / one-year / three-per-year trio, which is currently a Bearings-only fact and an Exam Alert priority topic (#5). If a third slot can be found, upgrade order is the best-value derivable item in the chapter and is untested.

### Interleaving requirement

The outline required at least four Practice items spanning two sections. All four named items are delivered: **P4** (§2+§3), **P8** (§1+§4), **P13** (§5+§6+§7), **P17** (everything+§8). ✓

### Lookup-vs-application calibration

The outline capped pure-lookup items at 6 of 17. Actual: **6** (P1, P2, P5, P9, P12, P15); 11 require application or diagnosis. **At the ceiling, compliant.** Note that if the §6 shortfall is fixed by adding recall items, this ceiling will be breached — the added items should be scenario-shaped.

---

## Soundings spoiler check

The chapter marks six ★ Fixed Points: FP1 §1 grammar/case asymmetry · FP2 §2 three gates in order, only admission mutates · FP3 §3 quota-namespace vs LimitRange-object · FP4 §4 cordon/drain/uncordon · FP5 §6 nothing newer than the API server, kubelet three back, kubectl the exception · FP6 §7 all objects in etcd, etcd access = root.

All eight Soundings are free-response, so there are no distractors to inspect; the check runs on stems and, secondarily, on the `<details>` rationales.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| 1 | Client tool config; the two-server problem | **no** | Stem names nothing Kubernetes-specific. FP1 is the grammar and case asymmetry; nothing here touches it. Priors only. |
| 2 | **[retrieval: ch3]** Single-door architecture | **no** | Asks for one component and one inference. FP2 requires three named gates in order with differentiated powers; "put the check at the door" supplies none of that. |
| 3 | The distinct questions a server must answer; whether one can *change* a request | **no — but note** | Stem names none of the three gates and asserts nothing. It does raise mutation as an open question, which is deliberate pre-test design. The key's "who are you, and are you allowed to do this" glosses two of three gates, but withholds the third and the order — i.e. withholds the Fixed Point. Inside `<details>`, which is the correct containment. |
| 4 | **[retrieval: ch4]** Namespaces and the division mechanism | **no** | Requires the reader to *produce* "resource quota" from Chapter 4. LimitRange is not named anywhere in the stem or key, so FP3's contrast — the whole content of FP3 — is untouched. |
| 5 | **[retrieval: ch7]** `unschedulable` taint, `NoSchedule` timing | **no — but note** | Stem and key establish that running Pods are unaffected, which is one clause of FP4's cordon behaviour. It arrives as Chapter 7 retrieval, not Chapter 8 teaching, and FP4's content — that a *second command* exists to evict what cordon spared — is fully withheld. The key even flags the gap ("raises an obvious follow-up question that §4 answers"). Working as designed. |
| 6 | **[retrieval: ch4]** Leases stop renewing; what to conclude | **no** | `Ready: Unknown` is taught in §4 prose but is not marked as a ★ Fixed Point. The key answers "it should conclude that it cannot tell" without supplying the status value or the two heartbeat forms. |
| 7 | Client/server version-mismatch direction | **no (stem) — WARN (key)** | Stem is clean and reveals no numbers. **The key overreaches:** *"That intuition is correct in general and, for exactly one component in Kubernetes, wrong. §6 names it."* That pre-delivers FP5's structural shape — one generating rule plus exactly one exception — before §6 teaches it, and it is the exact structure Bearings #3 item 2 later tests as a derivation. |
| 8 | Managed vs self-hosted duty split | **no** | §5 carries no ★ Fixed Point. Priors only. |

**Verdict: clean.** No stem reveals a Fixed Point; no question is answerable only from this chapter (skill Part 11 rule 2 satisfied on all eight).

**One WARN, S7's key.** Trim the final two sentences to *"That intuition is correct in general. §6 is where it stops being reliable."* That preserves the pre-test's honest feedback and the forward pointer while withholding "exactly one component," which is the payload of both FP5 and Bearings #3 item 2.

**Rubric check (skill Part 11 rule 6):** present and complete — 6+ / 3–5 / 0–2, each with a distinct reading strategy, and the 0–2 branch carries the outline's specific prerequisite instruction naming Ch 3 §2 and Ch 4 §6. **PASS.**

**Answer-disclosure check (rule 5):** all eight answers are inside a single `<details>` collapsible with a summary line. **PASS.** All three Bearings checkpoints use the same containment, which exceeds requirement.

**Pre/post symmetry (rule 1).** Seven of eight Soundings have a matching post-test:

| Soundings | Post-tested at |
|---|---|
| S1 kubeconfig / two servers | B1.2 |
| S2 single door | B1.3, B1.4 |
| S3 the three gates | B1.3, P2, P3 |
| S4 namespaces / quota | B1.5, P6 |
| S5 unschedulable taint | B2.1, P8 |
| **S6 leases / heartbeats** | **partial — see below** |
| S7 version direction | B3.1, B3.2, P14, P15 |
| S8 managed vs self-hosted | B2.5, P13 |

**S6 is the break.** It pre-tests the Lease mechanism and what an absent heartbeat licenses you to conclude. B2.3 post-tests the *conclusion* (`Unknown` vs `False`), but **nothing in Bearings or Practice tests the two heartbeat forms or the Lease objects themselves** — which is also a discharged cross-bearing (`chapter-04` line 584, "node conditions and heartbeats") left unassessed. See the coverage table.

---

## Per-question findings

### QPractice 2: "In what order does a request pass the API server's access-control gates, and which of them can result in the request being modified…?"

**Issue:** Two variables (order, mutating gate) are confounded across the option set, so the "authorization can mutate" misconception is never isolable. The outline required a distractor "attributing mutation to authorization"; B nominally does, but it scrambles the order as well, so any reader who knows the order eliminates it without ever confronting the mutation error.

**Distractor analysis:**
- A) Authorization → authentication → admission; only authentication can modify — *double-wrong (order + mutator); eliminable on order alone*
- B) Authentication → admission → authorization; only authorization can modify — *double-wrong; the intended "authorization mutates" probe is neutralised by the scrambled order*
- C) Authentication → authorization → admission; only admission can modify — **correct**
- D) Authentication → authorization → admission; any of the three can modify — *strong; isolates the collapse-the-gates error cleanly and is the only option that tests one variable*

Net effect: a reader who knows only the order faces a 50/50 between C and D; a reader who knows only the mutation fact lands on C directly. The item is doing roughly one question's work with four options.

**Why-wrong explanation status:** present and specific. The key explicitly names D's error as "the error that collapses three distinct gates into one undifferentiated 'security check'," which is exactly right.

**Recommended fix:** change B to *"Authentication → authorization → admission; only authorization can modify."* A then remains the sole order probe, B becomes a clean single-variable mutation probe, and D stays as the collapse probe. No other edits needed.

---

### QPractice 6: "Why can they not [cap a team's Node consumption] with a ResourceQuota?" **[retrieval: ch4]**

**Issue:** Option A asserts a claim about ResourceQuota's capabilities that **the chapter never gives the reader any basis to evaluate**, and the answer key refutes it with knowledge the chapter does not contain. §3 carries an explicit blocking source gap: what a quota can count (compute totals, object counts, storage) is not cached and is not taught. A reader who has read §3 attentively cannot rule out A from the text.

**Distractor analysis:**
- A) ResourceQuota cannot count objects, only compute resources — *unanswerable from the chapter; the key's rebuttal ("wrong as a claim about quota's capabilities") depends on the un-fetched `resource-quotas/` source*
- B) Nodes are not namespaced objects, and a ResourceQuota constrains a namespace — **correct**
- C) Evaluated at the authorization gate, which has no visibility into Nodes — *plausible; targets the authorization/admission collapse*
- D) A ResourceQuota in `kube-system` applies cluster-wide — *strong; targets a genuine and common misconception about privileged namespaces*

**Why-wrong explanation status:** present and specific for C and D. For A it is present but **unsupported by the chapter** — the key partially recovers with "more importantly, misses the point: the obstacle is scope, not counting," which is the right instinct but leaves the factual claim hanging.

**Recommended fix:** two options, in order of preference. **(a)** If the §3 fetch lands (`kubernetes.io/docs/concepts/policy/resource-quotas/`), teach what a quota counts and A becomes a legitimate distractor with no edit needed. **(b)** If the fetch does not land, replace A with a scope-flavoured distractor the chapter *does* support — e.g. *"A ResourceQuota can only constrain objects the team creates, and the team does not create Nodes"* — which targets a real near-miss (right conclusion, wrong reason) and is fully answerable from §3's hinge and §4's registration material.

---

### QPractice 13: "Which set of duties belongs to Team B and not to Team A?"

**Issue:** The weakest distractor set in the paper. Option D is a throwaway nobody holds, and A and C are the same distractor twice — both are "workload-side concerns misfiled as platform concerns," eliminable on one insight. The item reduces to a two-option question for any reader who has read §5's closing paragraph.

**Distractor analysis:**
- A) Writing Deployment manifests, and choosing container images — *plausible only to a reader who thinks "managed" means the provider runs the applications; a real but shallow misconception*
- B) Deciding when the control plane is upgraded, and taking etcd backups — **correct**
- C) Setting resource requests and limits, and defining namespaces — *duplicate meaning with A; same misconception, same elimination*
- D) Nothing differs; the two teams have identical operational responsibilities — *implausible; fabricated for symmetry. The stem has already stipulated a difference exists by asking which set belongs to B and not A*

**Why-wrong explanation status:** present. A and C are explained mechanically; **D's rebuttal is rhetorical rather than diagnostic** — "is the answer of someone who has not yet asked whose calendar the upgrade goes on" is good prose and does not name a misconception, because there isn't one to name.

**Recommended fix:** replace C and D with mixed options that require discriminating *which* duties move, rather than *whether* any do. Suggested: **C)** *"Deciding when the control plane is upgraded, and setting the namespace's ResourceQuotas"* (one duty that moves, one that doesn't — the sharpest available distractor); **D)** *"Taking etcd backups, and choosing which container runtime is installed on each node"* (both plausible-sounding platform duties, but the second is true for *both* self-hosted teams and for neither managed one in the way the option implies — and it retrieves §5's CRI requirement). Either rewrite converts the item from a two-option question into a genuine four-way discrimination.

---

### QPractice 16: "An operations team stores its nightly etcd snapshots, unencrypted, on the primary control-plane node…"

**Issue:** Not a weak distractor — an **option-length cue**. The correct answer runs ~45 words with two clauses of justification; A, B and D run 12–20 words each. Test-wise readers select the longest, most-hedged option without engaging the content, which is precisely the population this item is meant to catch.

**Distractor analysis:**
- A) No problem, provided filesystem permissions are correct — *plausible; targets the "access control substitutes for encryption and off-host storage" error*
- B) Should be encrypted, but the location is fine because that is where etcd runs — *strong; isolates one of the two failures and inverts the reasoning ("that is where etcd runs" is the reason it must NOT live there)*
- C) Stored outside the control-plane nodes and kept encrypted — otherwise they will not survive the disaster they exist for, and access to etcd data is equivalent to root permission in the cluster — **correct, and visibly the longest**
- D) Taken with `etcdutl` rather than `etcdctl`, which encrypts them automatically — *acceptable; the tool-swap half targets a real confusion, the auto-encryption half is fabricated but plausible-to-hopeful*

**Why-wrong explanation status:** present and specific for all three. B's rebuttal in particular ("etcd running there is the reason the snapshot must *not* live there") is the best single line in the answer key.

**Recommended fix:** compress C to match — *"They should be encrypted and stored off the control-plane nodes"* — and move the two-failure justification into the answer key, where it already appears almost verbatim. The stem asks "which statement best describes the problem," so the option does not need to carry the reasoning.

---

### QPractice 1: "Which statement about `kubectl` command syntax is correct?"

**Issue:** Option C is a compound distractor whose second clause is fabricated, which lets a test-wise reader eliminate it without holding the underlying misconception. The key acknowledges this in passing ("additionally invents a plural requirement that does not exist"). The inverted-asymmetry misconception — the single most useful one to catch here — is therefore not cleanly probed.

**Distractor analysis:**
- A) Both case-insensitive — *strong; the permissive over-generalisation, and the key correctly identifies it as the most common form of the error*
- B) Types case-insensitive and abbreviable; names case-sensitive — **correct**
- C) Names case-insensitive; types must be given in the plural — *half-plausible. The inversion is real; the plural requirement is invented and gives the option away*
- D) Both case-sensitive — *strong; the strict-direction over-generalisation*

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** cut the fabricated clause. **C)** *"Resource types are case-sensitive; resource names are case-insensitive."* That is the clean inversion, it targets a real mistake, and it removes the elimination shortcut. The key's existing sentence for C then shortens to one line.

---

### QPractice 8: "…which commands accomplish this, and in what order?"

**Issue:** Two separate problems, one in the options and one in the stem.

*Options:* A is wrong on two independent grounds — reversed order **and** a spurious `node` TYPE slot — so a reader tracking syntax eliminates it without engaging the order error, which is what the item exists to test.

*Stem:* "Using only the four-slot grammar, which commands accomplish this" primes the reader to expect a TYPE slot, and the correct answer omits it. A careful reader can talk themselves out of B on exactly the grounds the stem invited. The key resolves this well ("`cordon` and `drain` take the node's name directly, without a preceding TYPE, because the verb already implies the resource type") — but resolving an ambiguity in the key is a Part 10B *undesirable* difficulty: the reader who gets it wrong got it wrong for reading carefully.

**Distractor analysis:**
- A) `kubectl drain node worker-3`, then `kubectl cordon node worker-3` — *double-wrong (order + syntax); eliminable without the order insight*
- B) `kubectl cordon worker-3`, then `kubectl drain worker-3` — **correct**
- C) `kubectl cordon worker-3` alone — draining is implied — *the chapter's headline trap, and the strongest option in the set*
- D) `kubectl uncordon worker-3`, then `kubectl drain worker-3` — *plausible; targets cordon/uncordon confusion*

**Why-wrong explanation status:** present and specific. A's rebuttal is genuinely good ("the scheduler may place work onto it while you are clearing it").

**Recommended fix:** (1) change A to `kubectl drain worker-3`, then `kubectl cordon worker-3` so order is the only variable; (2) reword the stem to drop the grammar framing — *"Which commands accomplish this, and in what order?"* The grammar callback is already carried by the key.

---

### QBearings 2.1: "Chapter 7 listed `node.kubernetes.io/unschedulable` with a `NoSchedule` effect… What command applies it — and, using Chapter 7's rule about what `NoSchedule` governs, what happens to the Pods already running on that node?"

**Issue:** This is one of the chapter's three **[B3]**-designated retrieval anchors, and the stem pre-loads most of its own answer. It supplies the taint name, the effect, and the fact that it is operator-applied; the phrase "using Chapter 7's rule about what `NoSchedule` governs" then directs the reader to the rule rather than asking them to retrieve it. What remains to be recalled is the command name, taught two pages earlier in the same chapter.

The outline anticipated exactly this and instructed the opposite: *"this item must be the hard version — the identity, not the definition."* Retrieval practice earns its 20% allocation from the *effort* of reaching; a stem that hands over the premises converts a retrieval item into a comprehension item.

**Why-wrong explanation status:** present in substance — the key's "the point of the question is the identity rather than the definition" is exactly the right framing — but **no wrong turns are named.** The plausible errors here are answering "drain" (the command that does empty a node) and answering "they are evicted."

**Recommended fix:** strip the scaffolding and make the reader supply the bridge. Suggested: *"You cordon a node. Chapter 7 taught you a built-in taint with a `NoSchedule` effect that is applied deliberately rather than by a failing component. Name that taint, and say what `cordon` therefore does — and does not do — to the Pods already running."* Add to the key: *"Common wrong turns: answering `drain` (the command that does empty the node), and answering that the running Pods are evicted."*

The chapter's other two retrieval anchors are clean by contrast and need no change: **B2.4** (Ch 2, CRI) supplies no premises and requires three separate recalls, and **P11** (Ch 3, control loop) requires the reader to both name a pattern and produce two unnamed instances.

---

### Group finding — five Bearings items name no wrong turns

All 15 Taking Your Bearings questions are free-response, so the skill's "explain why wrong answers are wrong" has no options to attach to. The draft's substitute — a *"Common wrong turns:"* line in the answer key — is a sound adaptation and is used well where it appears. It appears in **10 of 15** items.

| Item | Wrong-turn line | Note |
|---|---|---|
| B1.1 | ✓ | Both symmetrical errors named |
| B1.2 | **✗** | No misconception named |
| B1.3 | ✓ | Names the two-gate model, the reversed order, and the authorization-mutates error — this is where the outline's trap requirement is actually discharged |
| B1.4 | **✗** | The obvious wrong answer is "authorization"; unnamed |
| B1.5 | **✗** | The obvious wrong answer is swapping quota and LimitRange; unnamed |
| B2.1 | **✗** | See block above |
| B2.2 | ✓ | Exemplary — explains the reasonable-but-wrong intuition at length and, per the outline's subject-dignity requirement, does not moralise about the outage |
| B2.3 | ✓ | `False` and `NotReady` both named |
| B2.4 | **✗** | **"Docker" is the single most likely wrong answer here and is unnamed** |
| B2.5 | ~ | Partial — "the version is not what differs" names the error implicitly |
| B3.1–B3.5 | ✓ | All five explain the reasoning per sub-answer; B3.4 names the common first answer ("the applications are down") |

**Severity: WARN, not FAIL.** Every one of these keys explains the correct answer's reasoning fully; what is missing is the misconception-detection half of the self-correction design.

**Recommended fix:** add one *"Common wrong turns"* line to B1.2, B1.4, B1.5 and B2.4. B2.4's is the highest-value single edit in this audit: *"Common wrong turn: 'Docker.' Chapter 2's whole point was that Kubernetes talks to a runtime through the CRI, and containerd and CRI-O are what the documentation names."* That retrieval item exists to satisfy the ≥4-back spacing floor on its first live chapter, and a reader who answers "Docker" currently receives no correction at all.

### Lower-severity notes (no block required)

- **P4 option C** ("Authentication; no — the API server rejects the request before identity is established") is not a real misconception; a quota violation is not detectable at gate one under any model a reader could hold. It is fabricated for symmetry. The key explains it correctly. Low impact because the item's real work is done by the A/B/D spread, which is a well-designed two-variable set — B and D differ only on the admin-exemption question, which is exactly the discrimination being tested.
- **P14 and Bearings 3.1 substantially overlap** — both present a 1.36 API server and ask for supported/not-supported calls, and both use kubelet 1.33 and kubectl 1.37 as specific cases. This reads as deliberate spaced reinforcement of the chapter's densest recall block rather than as duplicated allocation, and both keys correctly instruct the reader to treat the version numbers as illustration. No change recommended — but note that it is *not* a substitute for the two missing §6 Practice items, since both cover the same rule surface.
- **P9 option D** ("Unreachable") invents a status name. Acceptable — readers do invent plausible status strings, and B (`NotReady`) already carries the genuinely common half-memory.
- **P17** tests the chapter's method rather than a fact. This is the outline's intent for the Zenith item and is correctly executed; flagging only so it is not mistaken for a content-free item during revision.

---

## Retrieval-practice spacing

- Chapter 8 target: **20%** of the combined Bearings + Practice pool (**[B3]**; the outline resolves the B3/B4 discrepancy in favour of 20% and allocates 3 in Bearings + 4 in Practice = 7 of 32)
- Actual: **21.9%** — 7 of 32 items tagged `[retrieval: chN]`
- Status: **compliant**

| Item | Tag | Chapters back | Notes |
|---|---|---|---|
| Bearings 1.5 | `ch4` | 4 | **[B3]** named anchor — namespaces under ResourceQuota. Discharges the `chapter-04` line 590 cross-bearing as an assessment item, as designed |
| Bearings 2.1 | `ch7` | 1 | **[B3]** named anchor — node conditions against scheduling. **Stem over-scaffolded; see per-question findings** |
| Bearings 2.4 | `ch2` | **6** | **[B3]** ≥4-back floor item — the CRI boundary. Clean, three-part retrieval, no scaffolding. Best retrieval item in the chapter |
| Practice 6 | `ch4` | 4 | Namespaced vs cluster-scoped, framed differently from B1.5 as the outline required. Clean stem |
| Practice 7 | `ch5` | 3 | Requests and limits; the LimitRange-default placement consequence |
| Practice 10 | `ch4` | 4 | spec vs status. Doubles as §8's argument tested before §8 makes it, exactly as the outline specified |
| Practice 11 | `ch3` | **5** | Control loop. Second ≥4-back item, carried as redundancy for the floor's first live chapter |

**Per-band rates:** Bearings 3 of 15 (20.0%); Practice 4 of 17 (23.5%). Both inside the skill's 20–25% band for Chapter 6+.

**≥4-back spacing floor: satisfied twice.** Bearings 2.4 at six chapters back and Practice 11 at five. The outline's stated reason for carrying a second item — that a single item is a single point of failure on the floor's first live chapter — is honoured.

**Chapter 1 exclusion:** no item draws from Chapter 1, and no item tests exam mechanics. ✓

**Checkpoint distribution:** Bearings #1 carries 1, #2 carries 2, #3 carries 0. The outline pre-authorised this concentration on the grounds that both §4/§5 anchors belong nowhere else and that a fourth Bearings retrieval would push checkpoint #3 off the topic **[B3]** identifies as most at risk of decay. The draft follows that reasoning. ✓

**Recommended additions:** none required for compliance. If the §6 Practice shortfall is fixed, the outline's designated §6 retrieval item should be restored — reframing P7 to its §6 variant is the cheapest route and was explicitly permitted ("§6 block or §3 block, drafter's choice").

---

## Coverage vs concepts

Every concept and command in the outline's `kb_tags`, checked against the 40 questions. Bold **NO** = introduced in the chapter and tested nowhere.

### §1 — command grammar and configuration

| Concept | Tested in a question? |
|---|---|
| `kubectl`, `kubectl-syntax` | yes (P1, P8, B1.1) |
| `verb-resource-grammar` | yes (P1, P8, B1.1) |
| `resource-type-abbreviation` | yes (P1, B1.1) |
| `kubeconfig` | yes (B1.2, S1) |
| **`kubeconfig-precedence`** | **NO** — flag > env > `$HOME/.kube/config` is stated in §1 and carried in the Chapter Summary ("the flag wins"), but no question requires it. B1.2 mentions the override sources parenthetically without testing the order |
| `in-cluster-authentication` | yes (B1.2) |
| `serviceaccount-token-file` | yes (B1.2) |
| `namespace-override` | yes (B1.2) |
| `kubectl-get`, `kubectl-describe` | yes (B1.2, P1) |
| **`kubectl-explain`** | **NO** — taught in the verb table and given a ⚓ Worth Securing callout arguing it is the table's longest-lived entry. Never tested |
| **`kubectl-config`** | **NO** — named in the verb table only. Low severity |

### §2 — the three gates

| Concept | Tested in a question? |
|---|---|
| `api-access-gates`, `authentication`, `authorization`, `admission-control` | yes (P2, P3, P4, B1.3, B1.4, S2, S3) |
| `admission-controller` | yes (P4) |
| `mutating-admission` | yes (P2, B1.3) |
| `validating-admission` | **NO** — and not taught either; the mutating/validating distinction is blocked by the §2 source gap. Not a question defect. Revisit after the `controlling-access/` fetch |
| `dynamic-admission-control` | **NO** — taught only inside a 🔭 Closer Look, which is explicitly "deeper than the exam requires." Acceptable omission |
| **`auditing`** | **NO** — named in §2, carried in the Chapter Summary, listed in the outline's concept set. Introduced and never tested. Severity depends on Open Question #4: under option (b) the concept is one sentence and a single recognition item would be proportionate; under option (a) it needs one |
| **`tls-bootstrapping`** | **NO** — one clause in §2. Low severity |
| `hub-and-spoke-api-pattern` | yes, indirectly (P10/D "bypasses the object model", P17, S2) |

### §3 — dividing a shared cluster

| Concept | Tested in a question? |
|---|---|
| `resource-quota` | yes (P4, P5, P6, B1.5) |
| `limit-range` | yes (P5, P7, B1.5) |
| `namespaced-vs-cluster-scoped` | yes (P6, B1.5) |

Fully covered — the only fully covered section in the chapter, and it received one more Practice item than allocated.

### §4 — node lifecycle

| Concept | Tested in a question? |
|---|---|
| **`node-registration`, `node-self-registration`** | **NO** — §4 teaches self-registration as the default, manual Node creation, the `metadata.name` validity check, and DNS-subdomain naming. None is tested. This is load-bearing for §8's argument ("a kubelet joins by writing an object, the same as you do") and P10 tests spec-vs-status for `cordon` without ever touching registration |
| `cordon`, `drain`, `uncordon`, `unschedulable-node` | yes (P8, B2.1, B2.2) |
| `node-conditions` | partial (P9, B2.3 — `Ready` only) |
| `ready-condition` | yes (P9, B2.3) |
| **`memorypressure`, `diskpressure`, `pidpressure`, `networkunavailable`** | **NO** — four of the five node conditions are presented as a table in §4 and appear in no question. `Ready` carries all the assessment weight |
| **`node-heartbeats`, `node-lease`** | **NO** — the two heartbeat forms and the `kube-node-lease` Leases. **Pre-tested at Soundings 6 and never post-tested**, breaking the pre/post symmetry, and this is the payoff for the `chapter-04` line 584 cross-bearing ("node conditions and heartbeats") |
| `node-controller` | yes (P11) |
| `api-initiated-eviction` | weak (P11 key mentions eviction; no stem requires it) |
| `node-monitor-grace-period` | weak (B2.3 answer, P9 key; correctly never asks for a value) |

### §5 — ownership and tooling

| Concept | Tested in a question? |
|---|---|
| **`cluster-planning-axes`** | **NO** — §5's five planning questions. Both of §5's allocated Practice slots went elsewhere (and only one was used). Low-moderate severity: this is recognition material, but it is also §5's opening frame |
| `managed-kubernetes`, `self-hosted-cluster` | yes (P13, B2.5) |
| `kubeadm`, `minikube`, `kind`, `k3s` | yes (P12, B2.4) |

### §6 — versions

| Concept | Tested in a question? |
|---|---|
| **`semantic-versioning`** | **NO** — the `x.y.z` major/minor/patch vocabulary. Low severity; it is scaffolding for the rules rather than an examinable fact |
| `supported-releases`, `three-supported-minors`, `patch-support-window`, `release-cadence` | yes — **but only at Bearings 3.3.** All four facts have zero Practice coverage. "Three supported minor releases, ~1 year patch support, ~3 releases per year" is Exam Alert priority topic #5 and defuses B1 trap #29 |
| `version-skew` | yes (P14, P15, B3.1, B3.2) |
| **`upgrade-order`** | **NO** — §6 derives "API server first, because nothing may be newer than it" from the generating rule. It is the most cleanly derivable fact in the chapter and would make an excellent application item. Untested |

### §7 — etcd

| Concept | Tested in a question? |
|---|---|
| `etcd-backup`, `etcd-snapshot` | yes (P16, B3.4, B3.5) |
| `etcd-access-equals-root` | yes (P16, B3.5) |
| `disaster-recovery` | yes (B3.4) |
| `etcdctl-snapshot-save`, `etcdutl-snapshot-restore` | weak — both appear only inside P16 option D. **By design**: the outline specified §7's single Practice question "should be the security one rather than the command one." ✓ |

### Coverage summary

**13 concepts introduced and never tested.** Two are defensible (`dynamic-admission-control` is Closer Look material; `validating-admission` is not taught at all pending the §2 fetch). The remaining eleven cluster in three places:

1. **§4's node-side material** — registration, the four non-`Ready` conditions, heartbeats and Leases. The largest single gap, and `node-heartbeats` is the most consequential because it is both a Soundings-pre-tested concept with no post-test and a discharged cross-bearing left unassessed.
2. **§6's release-policy facts** — carried by a single Bearings item, with `upgrade-order` untested entirely. This is the same shortfall the budget-distribution finding identifies, seen from the other side.
3. **Scattered singles** — `kubeconfig-precedence`, `auditing`, `kubectl-explain`, `cluster-planning-axes`, `semantic-versioning`, `tls-bootstrapping`.

**Highest-value additions, in order.** Each is one item and each closes a gap that currently has no assessment anywhere:

- **§4 / heartbeats** — *"§4 describes two forms of node heartbeat. Name both, and say which namespace holds the objects the second uses."* Closes the S6 pre/post break and the `chapter-04` line 584 debt in one item. Best candidate for the §4 block, which is already one over allocation and could absorb it by converting rather than adding.
- **§6 / release policy** — an item on the three-branch / one-year / three-per-year trio and why they agree. Closes trap #29's Practice gap and takes one of the two §6 slots the draft owes.
- **§6 / upgrade order** — *"Given only the rule that nothing may be newer than the API server, which component is upgraded first, and why does the rest of the order follow without being separately specified?"* Application-shaped, so it does not breach the six-item lookup ceiling. Takes the second owed §6 slot.
- **§4 / node conditions** — fold the four non-`Ready` conditions into an existing item rather than adding one; P9 could carry a second part asking which condition a full disk would surface.
- **§1 / kubeconfig precedence** — extend B1.2 with a third clause rather than adding an item: *"…and say which wins if both `KUBECONFIG` and `--kubeconfig` are set."*