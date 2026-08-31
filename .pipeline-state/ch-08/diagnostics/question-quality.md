# Question-Quality Audit — Chapter 8

## Summary

- Chapter type: **content**
- Total questions inspected: **41**
  - 🧭 Soundings questions: **8**
  - ☆ Taking Your Bearings questions: **15** (across 3 checkpoints of 5)
  - Practice questions: **18**
- Question budget compliance: **met** (Practice over-by-1; permitted headroom per skill Part 8)
- Weak distractors (WARN): **7**
- Trap answers that don't target real misconceptions (WARN): **3** (subset of the 7 above)
- Missing or incomplete why-wrong explanations (FAIL): **0** (2 present-but-thin, 3 open-response items missing the chapter's own wrong-turn convention — WARN)
- Retrieval-practice spacing: **non-compliant** — 18.2% against a 20% floor, short by one item
- Soundings spoiler check: **clean** — 0 of 8 reveal a ★ Fixed Point

Two structural findings dominate this audit, and both are cheap to fix:

1. **P13 is effectively a two-option question**, and it is §5's only assessment item.
2. **Retrieval sits below the [B3] floor**, and the draft's own accounting note miscounts the pool (says 34; the shipped pool is 33), so the shortfall is slightly different from what the note records.

A third finding is a coverage gap rather than a defect: **four of §4's five node conditions, the whole node-registration subsection, `kubectl explain`, auditing, and the DaemonSet-tolerates-unschedulable fact are taught and never tested.** The DaemonSet item is the single best fix available, because it closes a coverage gap and the retrieval shortfall with one question.

---

## Question-budget compliance

| Category | Target | Actual | Status |
|---|---|---|---|
| Soundings | 8 | 8 | met |
| Taking Your Bearings (total) | 15 | 15 | met |
| Taking Your Bearings (checkpoints) | ≥2 (outline: 3) | 3 | met |
| Practice Questions | 17 | 18 | over-by-1 — **acceptable** |
| **Chapter total** | **40** | **41** | over-by-1 |

Over-budget is explicitly sanctioned ("Above-target is fine — headroom for cutting weak questions during audit"). Given the weak-distractor findings below, that headroom is the right place to spend the revision: no question needs cutting outright, but P13 needs rebuilding.

### Practice-block distribution vs. the outline's plan

The outline allocated by exam-point density rather than section count. The draft has drifted from that allocation, and the drift runs against the reasoning:

| Block | Planned | Actual | Notes |
|---|---|---|---|
| §1–§2 | 5 (incl. 1 retrieval) | 4 (P1–P4), **0 retrieval** | Lost the planned spec-vs-status retrieval when P10 was rewritten |
| §3 | 2 (incl. 1 retrieval) | 2 (P5, P6) + P7 floating | met |
| §4 | 3 (incl. 1 retrieval) | 4 (P8–P11) | over by 1 |
| §5 | 2 | 2 (P12, P13) | met |
| §6 | 4 (incl. 1 retrieval) | 3 (P14–P16), **0 retrieval** | short by 1 |
| §7 | 1 | 1 (P17) | met |
| Synthesis | — | 1 (P18) | the "Everything + §8" interleaving item |

§6 carries 4 of the 11 Exam Alert priority topics; §4 carries 2. §6 losing a question to §4 inverts the density argument. **Recommendation:** the retrieval item added to close the spacing shortfall should go in the §6 block, which fixes the density drift and the retrieval floor together.

### Constraints verified as met

- **Interleaving ("at least four questions require two sections at once")** — met. P4 (§2+§3), P7 (§3+§4+Ch 5), P8 (§1+§4), P10 (§4+§8), P13 (§5+§3/§7), P18 (all+§8). Six.
- **Lookup ceiling ("no more than six of seventeen pure lookup")** — met, exactly at the ceiling. Pure-lookup items: P1, P2, P5, P9, P12, P15 = 6. P14 and P16 are application/derivation, not lookup, which is what keeps the count down.
- **"No question may turn on a specific minor version number"** — met. P14 uses 1.36/1.33/1.37/1.35, but only as *relative* offsets; its answer key states this explicitly and the four verdicts hold at any API-server version. Nothing in the set turns on which minors are currently supported.
- **≥4-back spacing floor** — met, twice. B2.4 (Ch 2, six back) and P11 (Ch 3, five back).

---

## Soundings spoiler check

The chapter ships **six** ★ Fixed Points (§1 grammar/case, §2 three gates + mutation, §3 quota/LimitRange scope, §4 cordon/drain/uncordon, §6 skew rule + kubectl exception, §7 etcd/root/snapshot). Each Soundings stem and answer was checked against all six.

| Soundings Q # | Tests topic | Spoils Fixed Point? | Evidence |
|---|---|---|---|
| S1 | client config priors (address, credential, two-server state) | **no** | FP#1 is the four-slot grammar and the case asymmetry. S1 names no path, no precedence, no in-cluster detection. Answer stops at "an address and a credential, at minimum" |
| S2 | Ch 3 retrieval — the single door; where a check belongs | **no** | Asks *where*, never *how many* / *in what order* / *with what powers*. Key ends "One door means one set of locks" — FP#2's three names, order and mutation property all withheld |
| S3 | the distinct questions a server must answer; can any *change* the request | **no** (borderline — see finding S3 below) | Stem raises mutation as a possibility without asserting it. Key declines to name authentication/authorization/admission, and declines to confirm the "changed" clause: "if you said no, you are in the majority." FP#2 intact |
| S4 | Ch 4 retrieval — the namespace-division mechanism | **no** | Reader retrieves a name Ch 4 already gave them. FP#3 is the *contrast* with LimitRange; LimitRange is never named, and the key deliberately leaves the guess unsharpened ("Hold on to what you guessed; §3 will sharpen it") |
| S5 | Ch 7 retrieval — `NoSchedule` and already-running Pods | **no** — adjacency noted | Hands the reader the first clause of FP#4's content ("touches nothing already aboard"), but from Ch 7, where it was already taught. Withholds all three command names and the existence of a second step. Key closes forward, not back: "raises an obvious follow-up question that §4 answers" |
| S6 | Ch 4 retrieval — Leases stop renewing; what to conclude | **no** | No Fixed Point covers node conditions. Key answers "it should conclude that it cannot tell" and never says `Unknown`, which is §4's payoff |
| S7 | client/server skew intuition | **no** — adjacency noted | Key confirms the general intuition and signals an exception exists ("§6 is where it stops being reliable") without naming `kubectl`, the direction, or any number. FP#5 is entirely the numbers and the exception; both intact |
| S8 | managed vs self-hosted duty split | **no** | §5 carries no Fixed Point. Key's duty list ("patching and upgrades; backups; …") does not touch FP#6's etcd/root/snapshot content |

**Verdict: clean.** The set does what a pre-test should — S3 is engineered to produce an incomplete answer the reader can feel, and S5/S7 lean toward their sections without handing over the payoff. No FAIL.

**Rubric check (rule 8): PASS.** All three branches present (6+ / 3–5 / 0–2), with a specific 0–2 remediation naming Ch 3 §2 and Ch 4 §6.

**Answer-disclosure check (rule 9): PASS.** Answers are inside `<details><summary>Answers + reading strategy</summary>`.

---

## Per-question findings

### S3: "A server receives a request to do something expensive. List the distinct questions it must answer before it does the work…"

**Issue:** The answer key is **not scorable**, and the block asks the reader to compute a score out of 8.

**Distractor analysis:** n/a — open response.

**Why-wrong explanation status:** present but deliberately verdict-free.

The key reads: *"Most people produce two questions… If you produced two, that is the expected answer and you have just found the gap this chapter's §2 exists to fill. On the 'changed' clause: if you said no, you are in the majority."*

This is excellent curiosity-gap design and poor rubric design. The reader is told their answer was *common* and never told whether it was *right*. Every other Soundings item resolves to a scorable verdict (S1 "an address and a credential"; S5 "Nothing"; S6 "it should conclude that it cannot tell"; S8 "any two of these is a pass"). S3 is the only one that does not, and the 6+/3–5/0–2 rubric immediately below it requires a count. A reader who produced two gates cannot determine whether to count this item.

**Recommended fix:** add one scoring sentence, without closing the gap. Something on the shape of: *"Score this one correct if you produced three or more distinct questions, or if you answered 'yes' to the 'changed' clause. If you produced two and said no — the majority answer — score it incorrect and read §2 slowly; the third question is the one this chapter exists to give you."* That preserves the pretesting effect (the third question is still unnamed) and makes the item countable.

---

### P13: "Two teams run the same application. Team A uses a cloud provider's managed Kubernetes service; Team B self-hosts…"

**Issue:** Two of four options are eliminable on question *form* rather than on knowledge, reducing this to a coin flip between C and D — and this is **§5's only assessment item**, since the outline's planned managed-vs-self-hosted Bearings item was displaced by the heartbeat item (B2.5). The stem's two-team setup is also now vestigial.

**Distractor analysis:**
- **A)** "Both duties sit with the control-plane operator: taking etcd backups, and writing the application's Deployment manifests" — **implausible on form.** The stem asks for a pairing that *separates* a control-plane duty from a non-control-plane duty. A asserts both are on the same side, so it fails the stem's own requirement before any Kubernetes knowledge is applied.
- **B)** "Neither duty sits with the control-plane operator: choosing container images, and setting resource requests" — **implausible on form**, same failure. The answer key concedes this outright: *"names no control-plane duty at all, so it does not answer the question asked."* An explanation that rejects a distractor on form is a report that the distractor was never doing work.
- **C)** "Taking etcd backups sits with the control-plane operator; setting the namespace's ResourceQuotas does not" — correct.
- **D)** "Installing a container runtime on each node sits with the control-plane operator; taking etcd backups does not" — **strong.** A genuine inversion, both halves sound like platform work, and it forces the reader to separate "runs on cluster infrastructure" from "is the control-plane operator's duty." The key correctly identifies it as the sharpest.

**Stem problem, separate from the distractors:** Team A and Team B do no work. C's correct answer references neither, and the managed/self-hosted axis is not the axis being tested — the rewrite moved to "whoever operates the control plane," which is provider-independent by design. The setup primes the reader to look for a distinction the answer does not use, and a reader who takes the stem seriously will hunt for a managed-vs-self-hosted split among four options that don't offer one.

**Why-wrong explanation status:** present and specific for all three, but A's and B's explanations argue from question form rather than from domain knowledge, which is a symptom rather than a defect of the explanations.

**Recommended fix:** rebuild A and B as genuine separations with the wrong split, and cut the two-team framing to a one-line stem. Suggested:

> **13.** Which pairing correctly separates a duty that sits with whoever operates the control plane from one that does not?
>
> A) Taking etcd backups does not sit with the control-plane operator; installing a container runtime on each node does *(inverts the correct answer's first half against D's — targets the reader who thinks backups are a workload concern because they protect workload data)*
> B) Setting a namespace's ResourceQuotas sits with the control-plane operator; taking etcd backups does not *(targets the reader who treats "administrative-sounding" as "control-plane" — quota is administrative but namespace-scoped, and §3's hinge is the disproof)*
> C) Taking etcd backups sits with the control-plane operator; setting the namespace's ResourceQuotas does not **[correct]**
> D) *(unchanged — it is the best option in the set)*

If the managed-vs-self-hosted framing is wanted back, it depends on the §5 shared-responsibility sourcing gap the draft flags as BLOCKING; do not restore it before that resolves.

---

### P4: "A developer submits a Pod whose resource requests would push their namespace past its ResourceQuota…"

**Issue:** One implausible distractor.

**Distractor analysis:**
- **A)** Authorization; yes — admin has broader permissions — **plausible.** Targets the real "permissions override policy" misconception.
- **B)** Admission control; no — correct.
- **C)** "Authentication; no — the API server rejects the request before identity is established" — **implausible, internally incoherent.** Rejecting *at* the authentication gate *is* the identity determination; "before identity is established" describes nothing the API server does, and the stem has already identified the submitter as a developer. No reader holds this belief, because it isn't a belief — it's a malformed sentence about a gate.
- **D)** Admission control; yes — quota skipped for cluster-admin — **plausible and valuable.** Right gate, invented exemption; targets the same permissions-override instinct as A but from inside a correct gate model, which is the sharper version.

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** replace C with a distractor that targets a real gate confusion. Suggested: *"Admission control; yes — the quota applies to the namespace's owner, and an administrator's requests are attributed to the cluster rather than the namespace."* That is wrong in a way somebody could believe (it misapplies §3's scope hinge), and it preserves the question's two-axis structure.

---

### P2: "In what order does a request pass the API server's access-control gates…"

**Issue:** One distractor bundles two errors, making it eliminable on either half.

**Distractor analysis:**
- **A)** "Authorization → authentication → admission; only authentication can modify" — **weak.** Two independent errors in one option. A reader who knows either the order or the mutator eliminates it without engaging the other. Worse, the second clause is not a misconception anyone holds: authentication modifying a request is not a plausible model of anything, so the option is really only testing order.
- **B)** correct order, mutation attributed to authorization — **strong.** The real second-place misconception.
- **C)** correct.
- **D)** correct order, "any of the three can modify" — **strong.** Targets the collapse-into-one-security-check model precisely.

**Why-wrong explanation status:** present and specific for all three.

**Recommended fix:** unbundle A. Make it order-only: *"Authorization → authentication → admission; only admission can modify."* That isolates the order error and makes the option survive a reader who already knows the mutator, which is the whole point of a distractor.

**Note on the two-gate model:** the chapter's headline misconception (only two gates) cannot appear in P2, because every option must present an ordering. It is tested at **P3 option D** ("None; a request that passes authentication and authorization is always persisted"), which is the right home for it. No gap — recording the cross-reference so a later pass doesn't "fix" P2 by adding a two-gate option that breaks the stem.

---

### P12: "Which statement about cluster bootstrap tooling is correct?"

**Issue:** One distractor bundles two errors.

**Distractor analysis:**
- **A)** kubeadm/kind categories swapped — **strong.**
- **B)** correct.
- **C)** kubeadm/k3s swapped — **strong.**
- **D)** "minikube is the officially supported tool for creating clusters; kubeadm removes the need for a container runtime on each node" — **weak.** The second clause is implausible standalone; no reader believes a bootstrapper eliminates the runtime requirement, so the option collapses to its first clause, which duplicates A's error.

**Why-wrong explanation status:** present, and D's explanation does useful pedagogical work (reinforces the CRI boundary). That work is worth keeping even if the option is rebuilt.

**Recommended fix:** make D a single, real error. Suggested: *"kubeadm is the officially supported tool for creating clusters; it installs a container runtime on each node as part of joining them."* Same reinforcement in the explanation, and the misconception is one a reader could actually hold after §5 — that the officially supported bootstrapper handles everything.

---

### P17: "An operations team stores its nightly etcd snapshots, unencrypted, on the primary control-plane node…"

**Issue:** One distractor with no misconception behind it; one hedged explanation.

**Distractor analysis:**
- **A)** no problem with correct filesystem permissions — **strong.** Real; the "ACLs are sufficient" instinct is common.
- **B)** encrypt, but the location is fine — **strong.** Targets the reader who catches one of two failures, which is the modal partial answer.
- **C)** correct.
- **D)** "The snapshots should be taken with `etcdutl` rather than `etcdctl`, which encrypts them automatically" — **weak.** Nobody believes either utility encrypts. The tool-name half might attract a reader confusing `etcdctl`/`etcdutl`, but the encryption clause is invented, so the option is a bundled double-wrong of the P2/P12 kind.

**Why-wrong explanation status:** present, but D's is **hedged where the others are declarative**: *"no cached documentation attributes automatic encryption to either utility."* An answer key that reports what documentation was consulted rather than what is true reads as uncertainty about the distractor, and it leaks pipeline vocabulary into reader-facing text.

**Recommended fix:** replace D with the real tool confusion, stripped of the invented behaviour: *"The snapshots should be taken with `etcdutl snapshot save`; `etcdctl` is the restore utility."* That inverts the actual `etcdctl save` / `etcdutl restore` split — a genuine and likely confusion, since the two names differ by two letters — and lets the explanation be declarative.

---

### Lower-priority findings

| Item | Issue | Recommended fix |
|---|---|---|
| **P8 option D** ("`kubectl uncordon`, then `kubectl drain`") | Borderline weak. Eliminable on vocabulary alone — a reader who knows what `uncordon` means discards it without reasoning about the sequence. It does catch a genuine cordon/uncordon prefix reversal, so it is not empty | Optional. If rebuilt: *"`kubectl drain worker-3` alone — draining marks the node unschedulable as part of evicting"*, which targets the real belief that `drain` subsumes `cordon` |
| **P10 correct answer (B)** | B is the only option that does not assert a specific mechanism ("observes the node's marked state"), a consequence of the §8 sourcing narrowing. Test-wise readers can pattern-match the hedge | Resolves itself if the node snapshot lands and the spec-vs-status framing is restored, as the draft's AUTHOR-REVIEW already contemplates. No action needed now |
| **P16 option B** | Longest option in the set by a clear margin (two clauses of reasoning where A/C/D carry one). Classic length tell | Move half of B's reasoning into the answer key, where it already appears anyway. B should read: *"kube-apiserver first, because nothing may be newer than it, and every other component's window is expressed relative to it"* |
| **P18 stem** ("Based on §8's synthesis…") | Cites its own section, which no exam question does, and tells the reader where to look | Cut the clause. The question stands alone: *"You encounter a Kubernetes administrative feature this book has not covered. What are the two most productive questions to ask about it first?"* |
| **P6 option C** | Why-wrong present but thin: *"C is wrong on the gate."* Adequate only because the gate model is explained at length in P2–P4 | Optional. One clause: *"authorization has no view of object scope; quota is evaluated at admission"* |
| **P8 option C** | Why-wrong is one clause for the chapter's headline trap: *"`cordon` does not empty anything"* | Worth expanding to name the operational consequence, matching the weight §4's Navigational Hazard gives it |

---

### B3.1, B3.2, B3.3: missing the chapter's own wrong-turn convention

**Issue:** Checkpoints #1 and #2 establish a convention — every item's key closes with an explicit *"Common wrong turns"* paragraph naming the specific misconceptions that produce the wrong answer. Nine of the ten items in #1 and #2 carry it. **Checkpoint #3 drops it for items 1, 2 and 3**, and #3 covers the chapter's densest examinable material (four of the 11 Exam Alert priority topics).

**Why-wrong explanation status:** not a rule-3 FAIL — these are open-response items with no enumerated wrong answers, and the correct-answer derivation is present and thorough in each. But the chapter set the standard itself and then dropped it exactly where the exam points are.

Items 4 and 5 do carry the treatment in substance: B3.4's key names the misconception outright (*"Plenty of people's first answer… is 'everything is down,' which conflates the two"*), and B3.5 labels its two answers as distinct failure modes. So the gap is specifically 1, 2 and 3.

**Recommended fix:** one clause each, drawing on misconceptions the chapter has already catalogued.

- **B3.1** — add: *"If you marked (c) unsupported, you applied the kubelet's never-newer rule to `kubectl`. That is the chapter's most durable error and it costs you twice: wrong number, wrong direction."* This is the chapter's designated B1 trap #28 and it is currently defused only in §6's prose and in P15, never in the checkpoint that immediately follows the section.
- **B3.2** — add: *"The common partial answer names `kubectl` and stops. The HA kube-apiserver row is the one most readers miss, because it is not a bound relative to the API server at all."*
- **B3.3** — add: *"'The last two releases' is the standard half-memory here. It is three."* (B1 trap #29, currently carried only by §6's 🪝 Snag.)

---

## Retrieval-practice spacing

- **Chapter 8 target:** 20% of the combined Bearings + Practice pool ([B3]; the arc outline and the chapter outline both set 20%, resolving B4's ~15% in favour of the later stage)
- **Actual: 18.2%** — 6 of 33 questions tagged `[retrieval: chN]`
- **Status: short-by-1**

| Tagged item | Source chapter | Distance back | Anchor |
|---|---|---|---|
| B1.5 | Ch 4 | 4 | [B3] named anchor — namespaces under ResourceQuota |
| B2.1 | Ch 7 | 1 | [B3] named anchor — node conditions against scheduling |
| B2.4 | Ch 2 | **6** | **[B3] ≥4-back floor item** |
| P6 | Ch 4 | 4 | namespaced vs cluster-scoped |
| P7 | Ch 5 | 3 | requests and limits |
| P11 | Ch 3 | **5** | **≥4-back redundancy** |

**≥4-back floor: compliant, with redundancy.** Two items clear it (six back and five back), which is the right posture for the floor's first live chapter.

**Per-checkpoint distribution:** #1 has 1, #2 has 2, #3 has 0. The outline sanctioned the zero in #3 on the grounds that a fourth Bearings retrieval would push that checkpoint off its own topic. That reasoning still holds — but it was written on the assumption the chapter would clear 20% overall, which it does not. The fix belongs in Practice, not in #3.

**Correction to the draft's own accounting.** The AUTHOR-REVIEW note below the Practice answer key states *"6 of 34 = 17.6%"* and projects *"7 of 34 = 20.6%"* after restoring P10's tag. **The shipped pool is 33, not 34** (15 Bearings + 18 Practice). The likely cause is visible in the note itself: it describes B2.5 (heartbeats) as an *addition*, but comparing against the outline shows it *replaced* the planned managed-vs-self-hosted item, so checkpoint #2 stayed at five. Corrected figures: **6/33 = 18.2% now; 7/33 = 21.2% after one addition.** The conclusion the note reaches is right; the arithmetic under it is not, and the note is the audit trail a later stage will trust.

### Recommended addition (one item closes the floor)

**Preferred: a `[retrieval: ch6]` item on DaemonSet Pods tolerating an unschedulable node, placed in the §6 block.**

This is the best available option for three converging reasons:

1. It closes the retrieval floor (7/33 = 21.2%).
2. It closes a genuine **coverage gap** — the DaemonSet exception is taught in §4 with a fully sourced two-part sentence, carries an explicit Ch 6 cross-bearing, appears in the Chapter Summary, and is tested by **nothing**.
3. Placing it in the §6 block corrects the distribution drift noted above (§6 is short one against its density-based allocation).

Draft shape:

> **[retrieval: ch6]** You `drain` a node for maintenance. Every Pod is evicted except one, which is still running afterwards. Chapter 6 introduced the controller responsible. Name it, and say what its Pods carry that lets them stay.
>
> *Correct answer: a DaemonSet; its Pods carry a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect, added automatically by the DaemonSet controller.*
>
> *Distractors: a StatefulSet (ordinal identity confused with node affinity); a Deployment with a node selector (targets the reader who thinks placement constraints confer eviction immunity); a static Pod (a real mechanism, wrong one here — and not chapter material, so cut this if it reads as out of scope).*

**Alternative, if the node snapshot lands:** restore P10's spec-vs-status framing and its `[retrieval: ch4]` tag, which the draft's AUTHOR-REVIEW already plans. That also reaches 7/33, and additionally restores the §1–§2 block's lost retrieval item. It does *not* close the DaemonSet coverage gap, so if both are affordable, do both — 8/33 = 24.2% is still inside the 20–25% band.

---

## Coverage vs concepts

Concepts and commands from the outline's `kb_tags`, checked against the 41 shipped questions. Grouped; every untested item is enumerated explicitly.

| Concept introduced in chapter | Tested in a question? |
|---|---|
| `kubectl` syntax / verb-resource grammar / type abbreviation / case asymmetry | yes (P1, P8, B1.1) |
| `kubeconfig`, kubeconfig precedence | yes (B1.2 — precedence explicitly asked) |
| in-cluster authentication, ServiceAccount token file | yes (B1.2) |
| namespace override (`--namespace`) | partial — the SA-namespace *default* is tested (B1.2); the explicit override flag is not |
| `kubectl explain` | **NO** — given a dedicated sentence and a ⚓ Worth Securing callout, tested nowhere |
| `kubectl config` | **NO** — one table row; low severity |
| API access gates / authentication / authorization / admission control | yes (P2, P3, P4, B1.3, B1.4) |
| mutating admission (the mutation property) | yes (P2, B1.3) |
| dynamic admission control (webhooks) | **NO** — 🔭 Closer Look material, explicitly "deeper than the exam requires"; low severity, but it is the extension point Ch 17 collects |
| auditing | **NO** — §2 teaches that it exists and is part of securing a cluster, and the chapter frames that existence as the exam-relevant fact. Zero questions |
| TLS bootstrapping | **NO** — one clause of content; low severity |
| hub-and-spoke API pattern | yes, indirectly (P10, P18; S2 pre-tests it) |
| ResourceQuota / LimitRange / namespaced vs cluster-scoped | yes (P4, P5, P6, P7, B1.5) |
| node registration, self-registration, `metadata.name` validity, DNS-subdomain naming | **NO** — an entire §4 subsection, and one of the four administrative acts drawn in the Zenith figure, with no assessment item |
| `cordon` | yes (P8, P10, B2.1, B2.2) |
| `drain` | yes (P8, B2.2) |
| `uncordon` | **thin** — appears only as P8's distractor D. The reader is never asked to produce it, though it is a third of FP#4 |
| unschedulable node | yes (P10, B2.1) |
| `Ready` condition, three-valued; `node-monitor-grace-period` | yes (P9, B2.3) |
| `DiskPressure`, `MemoryPressure`, `PIDPressure`, `NetworkUnavailable` | **NO** — four of the five conditions are taught as a table and never tested. Only `Ready` is assessed |
| node heartbeats, node Lease, `kube-node-lease` | yes (B2.5) |
| node controller | yes (P11, B2.5) |
| API-initiated eviction | **thin** — appears only as stem context in P11, never as what is being tested |
| DaemonSet tolerates an unschedulable node | **NO** — fully sourced, cross-bearinged to Ch 6, in the Chapter Summary, tested nowhere. **Best single fix in this audit** |
| Capacity / Allocatable | partial — P7 requires knowing Allocatable is what the scheduler counts, but no item tests the pair directly |
| cluster planning axes | **NO** — five planning questions, no assessment. Low severity (framing, not examinable fact) |
| managed vs self-hosted | yes, but **only P13**, the weakest question in the set (see finding above) |
| kubeadm / minikube / kind | yes (P12; kubeadm also B2.4) |
| k3s | thin — P12 distractor C only; one-clause content, acceptable |
| container runtime / CRI boundary | yes (B2.4, P12) |
| semantic versioning (`x.y.z`) | **NO** — vocabulary only; low severity |
| supported releases (three branches), patch-support window, release cadence | yes (B3.3) |
| version skew (all five rows) | yes (P14, P15, B3.1, B3.2) |
| upgrade order | yes (P16) |
| etcd backup / snapshot / access-equals-root / disaster recovery | yes (P17, B3.4, B3.5) |
| `etcdctl snapshot save` / `etcdutl snapshot restore` | **not tested by design** — the outline directed §7's single question to the security fact rather than the commands. Defensible; recording it so a later pass does not read it as an oversight |

### Coverage recommendations, in priority order

1. **DaemonSet exception** — add the `[retrieval: ch6]` item drafted above. Closes a coverage gap and the retrieval floor together.
2. **Node conditions beyond `Ready`** — the four pressure/network conditions are exactly the recognition material a comprehension-tier exam asks about, and the chapter prints them as a table without ever asking. One four-option item in the §4 block would cover them: *"A node reports `MemoryPressure: True`. Which of the following is a condition the Node status does not carry?"* — or fold them into B2.3 as a second clause: *"Name the other four conditions a Node's status carries."* The second option is free (no question-count change).
3. **Node registration** — one item, either in P's §4 block or as a sixth clause on B2.5, which already sits in the right place: *"A Node object exists but no Pod is ever scheduled to it. What does the control plane check after a Node object is created, and what would fail that check?"*
4. **Auditing** — one recognition item, or one clause added to an existing Exam Alert-adjacent question. The chapter tells the reader that auditing's *existence* is the examinable fact and then never asks. Cheapest possible fix: add it as a distractor-free clause in B1.3 (*"…and name the fourth item the cluster-administration guidance lists alongside these three"*). Note this interacts with the draft's open sourcing item — if the `controlling-access` snapshot lands and auditing is upgraded from two sentences to four, the question becomes better-founded at the same time.
5. **`uncordon` and `kubectl explain`** — both are currently distractor-only or callout-only. Neither needs its own question; both could be absorbed into existing items (P8's key already names `uncordon`; B1.1 could add *"…and name the verb that answers a question about the API rather than about your cluster"*).

Items 1–3 are worth acting on. Items 4–5 are cheap enough to fold into existing questions without changing the budget.