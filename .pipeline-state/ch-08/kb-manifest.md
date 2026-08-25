I have everything verified. Three of my checks changed conclusions the integration report reached, so those lead the manifest.

```markdown
# Knowledge-Base Manifest — KCNA Chapter 8

**Book:** Kubernetes and Cloud Native Associate · **Chapter:** 8 — Standing the Watch
**Stage:** 14 — Knowledge Base Update · **Date:** 2026-08-24

**Inputs consulted:** the finalized chapter; `ch-08/integration.md`; `ch-08/outline.md` frontmatter (`kb_tags` — 58 concepts, 9 commands, `objectives: ["D1.2"]` on all eight sections); shipped `chapter-01` … `chapter-07`; the seven prior `kb-manifest.md` files; `sources/` (137 files, enumerated); `certcomp/pipeline/stages.py`.

---

## Structural findings — all four verified on disk

**1. ⚑ The `=== WRITE` / `=== APPEND` blocks are inert, and the knowledge base still does not exist.**

Re-verified rather than inherited. `stages.py:225-234` defines stage 14 with exactly one output, `{ch}/kb-manifest.md`. A repo-wide search of `certcomp/**/*.py` for `=== WRITE` and `=== APPEND` returns **zero** parsers. `C:\dev\lodestar\Book-KCNA\knowledge-base\` **does not exist** — no `glossary.md`, no `concepts/`, no `objective-coverage.md`, no `retrieval-log.md`.

Every row below is therefore an append to a file that has never been created. **Eight chapters' knowledge base now sits unapplied inside eight manifests.** Replay order is load-bearing — this manifest appends to nine shards that earlier chapters create:

> ch-01 → ch-02 → ch-03 → ch-04 → ch-05 → ch-06 → ch-07 → **ch-08**

**2. ✅ Correction to the integration report — the metadata BLOCKING item closes completely, and more cheaply than reported.**

The integration report resolves two of the three unattested metadata claims (domain name, 44%) and proposes *eliminating* the third by adopting Ch 7's wording, on the grounds that the "four domains" count is not sourceable. **It is sourceable.** `cncf-kcna-curriculum-pdf-2026-08-23.md:13-16` enumerates exactly four domains summing to 100%:

```
- 44% – Kubernetes Fundamentals: Kubernetes Core Concepts; Administration; Scheduling; Containerization
- 28% – Container Orchestration: Networking; Security; Troubleshooting; Storage
- 16% – Cloud Native Application Delivery: Application Delivery; Debugging
- 12% – Cloud Native Architecture: Observability; Cloud Native Ecosystem and Principles; Cloud Native Community and Collaboration
```

All three claims — **name, percentage, and count** — tag against that one snapshot, which is on disk. The chapter may keep its "four domains" sentence rather than drop it. `concepts/domain-weights-44-28-16-12.md` (created by ch-01) already carries this table; the metadata line should cross-reference it.

The same line also settles the competency name the integration report left open: it is **"Administration"**, not the chapter's "Cluster Administration". Ch 2, 5 and 7 each use the curriculum's own competency name verbatim.

**3. ⚑ New finding — the British-spelling regression is 32 instances, not 26, and one of them collides with a branded marker.**

The integration report counts 26 across eleven word-families. It does not count the `harbour` family, which adds six:

| Form | Ch 8 | Ch 1–6 | Ch 7 |
|---|---|---|---|
| `harbour` / `harbours` | 3 | 0 | 1 |
| `harbourmaster` | 3 | **0 — Ch 4 uses `harbormaster` ×2** | 0 |
| `Harbor` (branded) | 1 | 7 | 1 |

Chapter 8 spells the same role two ways inside one chapter: `harbourmaster` ×3 in §2's Extended Analogy, and `🏆 Safe Harbor` as the locked branded marker. **Chapter 4 already coined `harbormaster`** — American, twice. This is not merely a spelling drift; it is the analogy's central character renamed against the chapter that introduced it, sitting three sections from a brand-locked marker spelled the other way.

This gates a voice-exemplar nomination — see that section.

**4. ⚑ Inherited caveat.** The finalized chapter carries roughly twenty live AUTHOR-REVIEW comments plus the integration report's four ship-blockers. I confirmed the largest claim among them directly: none of the ten "landed-but-unwritten" snapshots is in `sources/` — no `controlling-access`, `resource-quota`, `limit-range`, `reserve-compute`, `node-status`, or `audit` file exists. Those comments are accurate, not stale, and the gap rows below depend on them.

Two fixes the chapter's own comments treat as needing a fetch **do not**, because the snapshots are already on disk: `k8s-docs-taints-tolerations-2026-08-23.md` (Soundings A5, Bearings #2 item 1) and `k8s-docs-resource-management-2026-08-23.md` (Practice Q7). Both need only a reference-list addition.

---

## Glossary entries added to `Book-KCNA/knowledge-base/glossary.md`

**63 terms contributed — 51 defined · 7 partial · 5 gap-only.**

Two counts are in play and are not in conflict. Stage 13 flags **9** terms with an open definitional gap; skill Part 16 requires the glossary to carry every technical term introduced (100-term floor). Chapters 4, 5 and 7 set the precedent of contributing the full set. Both are below, separated. Appended as a Chapter 8 section rather than merged into one A–Z — re-transcribing prior prose to preserve a single alphabet is exactly the drift Rule 5 forbids; book assembly merges alphabets mechanically.

### Priority rows — the 9 gaps Stage 13 flagged, plus 2 inherited

Rule 5 forbids inventing wording. Where the chapter defines nothing, the row records what the chapter *does* say and names the gap rather than laundering a paraphrase into canon.

| Term | Definition (from chapter) | Status |
|---|---|---|
| **dynamic admission control / admission webhook** | "Dynamic admission control means the cluster calls out to a webhook *you* supplied. Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend," and this "adds a potential point of failure." | **partial** — mechanism sketched; the mutating/validating phase split is never named. Outline judged it above associate tier |
| **auditing** | "Alongside the three gates, the cluster-administration guidance on securing a cluster lists **Auditing**… auditing exists, it is part of securing a cluster, and it is what tells you afterwards what happened." | ⚑ **gap** — the chapter's own PARTIAL objective, **D1.2-08**. Closer sits unwritten in `research-manifest.md` |
| **ResourceQuota** | "Namespaces are a way to divide cluster resources between multiple users, via resource quota." "A quota is a ceiling on a **namespace, in aggregate**: the team's total, not any one Pod's numbers." | ⚑ **gap** — scope stated; *what it counts*, the 403 rejection, and the requests-must-be-specified rule all absent. **BLOCKING** |
| **LimitRange** | "use LimitRanges to ensure that Pods specify their resource requirements" — "a constraint on **individual objects**, and a mechanism that has to be able to act on a manifest that says nothing at all." | ⚑ **gap** — function stated; min/max/default structure and the admission-stage-only caveat absent. **BLOCKING** |
| **`node-monitor-grace-period`** | Named inside the `Ready` definition: "**Unknown** if the node controller has not heard from the node in the last `node-monitor-grace-period`." | **partial — deliberate.** "This book will not give you a number for it, because the examinable fact is what `Unknown` *asserts*" |
| **node `Capacity`** | Nothing. The chapter states only that "Capacity and Allocatable are two different numbers on the same Node object, and the second is the one the scheduler uses." | ⚑ **gap — REGRESSION, see below** |
| **kubelet TLS bootstrapping** | "Automating the provisioning of those certificates is what kubelet TLS bootstrapping is for." | **partial** — purpose stated, mechanism absent; nothing in the book defines it |
| **bearer token** | "Kubernetes automatically injects the public root certificate and a valid bearer token into the Pod when it is instantiated." | ⚑ **gap** — used as a term of art, undefined here and in all prior chapters |
| **managed vs self-hosted duty split** | "some operational aspects sit with whoever runs the control plane, and which ones move is a per-provider question." | **partial — permanently, absent a new source.** kubernetes.io does not document commercial providers' responsibility models |
| **`PriorityClass`** | Does not appear in Chapter 8 except inside a scope-guard comment. | ⚑ **gap — inherited, still unowned. See G4** |
| **admission plugin / policy plugin** | Six surface forms in-chapter (`admission control`, `admission controllers`, `admission gate`, `admission plugin`, `policy plugin`). | ⚑ **headword unsettled — Ch 8 is the designated owner. See below** |

### Three of these need an author decision, not just a glossary row

**⚑ `node Capacity` is now undefined anywhere in the book, and Chapter 8 is the chapter that was supposed to define it.** ch-07's manifest recorded it as "⚑ gap — cross-ref Ch 8" on the strength of Chapter 7 §2's explicit deferral: *"What makes the two differ, and how it's configured, is Chapter 8's material."* Chapter 8 §4 was **right** to cut the arithmetic — `k8s-docs-node-allocatable-2026-08-24`'s own extraction note forbids stating a Capacity → Allocatable relationship, because it appears only as an image. But the effect is a regression: a term handed forward under a named promise is now dropped by its designated owner, and Ch 7 L408's cross-bearing points at a definition that no longer exists.

Two honest discharges, in preference order: (a) land the `reserve-compute-resources` snapshot and take `kube-reserved` / `system-reserved` plus the motivation sentence — two sentences, no arithmetic, and the block gets *shorter*; or (b) soften Ch 7 L408 from a promise to a chapter-scoped deferral. Do not leave a forward pointer aimed at a cut definition.

**⚑ `PriorityClass` — ch-07's G4 is now two chapters old and still unowned.** ch-07 escalated it after searching all seven shipped chapters and `chapter-lineup.md` and finding zero hits. Chapter 8 §3's scope guard declines it explicitly ("do NOT take … priority-class quota — all above associate tier"). The tier call is defensible; the consequence is that **no chapter will now define it**, so the glossary row is the floor and an author decision is required on whether any chapter adopts it.

**⚑ The admission headword is Chapter 8's to settle and it did not settle it.** ch-07's manifest recorded NodeRestriction as "partial — behaviour defined; 'admission plugin' as a *category* undefined until Ch 8." Chapter 8 defines the category well but under six surface forms, one of which (`policy plugin`, in Bearings #1 item 4's key) is a coinage anchored to nothing. Recommended ruling, carried in the glossary and in `concepts/admission-control.md`: **"admission controller" is the category; "admission plugin" names a specific built-in** (NodeRestriction, per Ch 7's sourced phrasing); `policy plugin` is retired.

### Full Part-16 coverage — the 51 defined rows

Verbatim from the chapter, organised by section. Full text in the append block; representative rows:

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **`kubectl` grammar** | "`kubectl [command] [TYPE] [NAME] [flags]`." Four slots; NAME and flags optional. | Ch 8 §1 |
| **case asymmetry** ★ | "Resource types are case-insensitive, and you may use the singular, plural, or abbreviated form… Resource *names* are case-sensitive." | Ch 8 §1 |
| **kubeconfig precedence** | "`kubectl` looks for a file named `config` in the `$HOME/.kube` directory… other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag." Flags override environment variables. | Ch 8 §1 |
| **in-cluster authentication** | Three checks — `KUBERNETES_SERVICE_HOST`, `KUBERNETES_SERVICE_PORT`, and a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. "If all three are found, in-cluster authentication is assumed," and `kubectl` "acts against the namespace of the ServiceAccount." | Ch 8 §1 |
| **the three gates** ★ | "Authentication, then authorization, then admission. Authentication asks **who**. Authorization asks **may you**. Admission asks **should this, exactly as written, be allowed to happen** — and it is the only one of the three that can change your request instead of refusing it." | Ch 8 §2 |
| **hub-and-spoke API pattern** | "All API usage from nodes, or from the Pods they run, terminates at the API server. None of the other control plane components are designed to expose remote services." | Ch 8 §2 — ⚑ see Rule 6 flag 1 |
| **`cordon`** | "Marks a node unschedulable… prevents the scheduler from placing new Pods onto that Node, without affecting the existing Pods on the Node." | Ch 8 §1, §4 |
| **`drain`** | "`kubectl drain` evicts the Pods." | Ch 8 §4 |
| **`Ready: Unknown`** ★ | "The node controller has not heard from the node in the last `node-monitor-grace-period`." Distinct from `False`: "`Unknown` is not a fourth failure mode. It is the control plane declining to guess." | Ch 8 §4 |
| **node heartbeats** | "Two forms: updates to the `.status` of a Node, and Lease objects within the `kube-node-lease` namespace, with each Node having an associated Lease object." | Ch 8 §4 — **closes Ch 4's forward bearing** |
| **the generating rule** ★ | "**Nothing in the cluster may be newer than the API server it talks to.**" | Ch 8 §6 |
| **`kubectl` skew** ★ | "Supported within **one** minor version, **older or newer**, of kube-apiserver." The sole exception. | Ch 8 §6 |
| **etcd access** ★ | "Access to etcd is equivalent to root permission in the cluster, so ideally only the API server should have access to it." | Ch 8 §7 |
| *(38 further rows in the append block)* | | |

---

## Concept shards at `Book-KCNA/knowledge-base/concepts/`

### Created — 12 shards

`kubectl-grammar.md` · `kubeconfig.md` · `api-access-gates.md` · `admission-control.md` · `resource-quota-and-limitrange.md` · `node-lifecycle.md` · `node-conditions.md` · `node-controller.md` · `cluster-bootstrap-tooling.md` · `version-skew.md` · `release-cadence.md` · **`etcd.md`**

`etcd.md` is not discretionary. ch-03's manifest states: *"**Not created, with reasons:** `etcd` — Chapter 8 owns backup/restore and Chapter 12 owns encryption at rest… **Ch 8's Stage 14 creates it.**"* That obligation is discharged here.

`resource-quota-and-limitrange.md` is one shard rather than two, following ch-07's `predicates-priorities.md` precedent: neither mechanism reaches 200 words alone, and the discrimination between them *is* the content.

`node-controller.md` is a short reconciliation shard rather than a full concept shard. It exists specifically to close ch-07's registered three-casings gap.

### ⚑ Rule 6 — three conflicts against prior canon. None overwritten.

**FLAG 1 — `api-server-hub.md`. Chapter 8 restates in absolute form a claim Chapter 3 deliberately narrowed, and supplies its own counterexample two sections earlier.**

This is the integration report's single canon contradiction, and the shard makes it sharper than the report does. ch-03's `api-server-hub.md` carries an explicit standing instruction:

> **2. The hub describes STATE movement, not every connection.** "The API server does open connections to kubelets: that is how fetching Pod logs, attaching to a running container, and port-forwarding work." … An earlier draft asserted the absolute form; a prior AUTHOR-REVIEW records that it was softened deliberately after the source was fetched. **Do not restore the absolute phrasing.**

Chapter 8 §2 reads "Three gates on one door would be an incomplete access-control story if there were other doors… **There are not.**" Figure 8.6's caption reads "**There are no side channels.**" And §1's verb table, two sections earlier, lists `logs` and `exec` — the exact two paths Chapter 3 carved out.

The three-gate argument is unaffected: those paths originate *at* the API server, so all inbound API usage still terminates there. This is a scope-of-phrasing defect, not a false statement. **The shard is APPENDED, not rewritten**, and the appended note re-states Chapter 3's carve-out rather than Chapter 8's absolute. A naïve replay that overwrote this shard with Chapter 8's wording would delete a precision the author installed on purpose.

Recommended prose fix: scope both to *inbound API usage*.

**Verified alongside:** Chapter 8's etcd-access modality complies with the other standing instruction in that shard. Ch 3 requires the "**ideally**… should" hedge on etcd confinement and says "do not harden it downstream." Chapter 8 preserves the hedge in all three places it appears — §7 prose, §7 Fixed Point, §8. No flag.

**FLAG 2 — `taint.md` / `built-in-node-condition-taints.md`. Do not let the replay harden the cordon↔taint link.**

ch-07's `built-in-node-condition-taints.md` ends its `unschedulable` row with "Chapter 8's opening move," which invites Chapter 8's Stage 14 to close the loop by asserting that `kubectl cordon` applies `node.kubernetes.io/unschedulable`. **No cached source states this**, and `k8s-docs-taints-tolerations-depth-2026-08-24` pulls the other way ("The taint will be added to a node when initializing the node to avoid race condition"). Chapter 8 caught this in revision — §8's paragraph and Practice Q10 were both narrowed, and Bearings #2 item 1's stem was rewritten.

The appended shard notes record **three separately-sourced facts and the absence of a link between them**. It does not assert the link. The closer — "cordoned nodes are marked Unschedulable in their spec" — sits unwritten in `research-manifest.md`.

**FLAG 3 — `namespace.md`. Chapter 8 discharges one inherited debt fully and one thinly.**

ch-04's `namespace.md` carries two forward assignments to Chapter 8, both now due:

- **`Lease` ownership** — settled by B2 in Chapter 8's favour and recorded so Ch 5 and Ch 12 would not re-litigate it. **Fully discharged** at §4: both heartbeat forms named, `kube-node-lease` named, the node controller that watches them named. Chapter 4 L584's cross-bearing is answered.
- **"ResourceQuota is named and handed to Chapter 8."** **Thinly discharged.** §3 establishes scope and the functional contrast and nothing else, because the two snapshots that would carry the rest never landed. Not a contradiction — an under-delivery against a bearing, and it is why the two glossary rows above are BLOCKING rather than partial.

### Appended — 9 shards earlier chapters created that Chapter 8 extends

| Shard | Created by | What Ch 8 adds | Conflict? |
|---|---|---|---|
| `api-server-hub.md` | ch-03 | The three gates as "what the door *does*"; §7's etcd-side restatement | ⚑ **FLAG 1 — scope, do not overwrite** |
| `taint.md` | ch-07 | §8's scheduler-checks-taints restatement | ⚑ **FLAG 2 — link unsourced** |
| `built-in-node-condition-taints.md` | ch-07 | The `unschedulable` promise, discharged as far as sources allow; DaemonSet toleration confirmed from the Ch 8 side | ⚑ **FLAG 2** |
| `namespace.md` | ch-04 | Lease debt closed; ResourceQuota debt part-paid | ⚑ **FLAG 3 — under-delivery** |
| `cluster-scoped-resource.md` | ch-04 | **The operational payoff.** "You can quota a team. You cannot quota a machine" — the first time the boundary has a consequence, and the base Ch 12 derives the RBAC matrix from | no — extension |
| `control-loop.md` | ch-03 | The node controller as an instance: observe heartbeats → compare → act | no — extension |
| `serviceaccount.md` | ch-05 | `kubectl`-in-a-Pod: the SA as an *identity `kubectl` assumes*, and the namespace default that follows | no — extension |
| `cri.md` | ch-02 | The boundary's first operational consequence: a runtime must already be on every node | no — promise paid |
| `resource-request.md` | ch-05, ch-07 | A third actor — LimitRange defaulting a request the manifest never declared | no — extension, but see below |

**`control-loop.md` note for B3.** ch-03 recorded the control-loop theme's retrieval chain as Ch 3→4→6→11→15→17. **Chapter 8 is not on that list and bears the theme anyway**, explicitly and by name ("The node controller is a control loop… This is the sixth"). Either B3's chain is stale or Chapter 8 has done unbudgeted retrieval work. Worth recording before Ch 11, which ch-03 flagged as "still unbeared."

**`resource-request.md` note.** ch-07 already merged two framings into this shard (Ch 5's runtime "floor, not a ceiling" and Ch 7's scheduler-side booking) with an explicit do-not-overwrite instruction. Chapter 8 adds a third, non-conflicting: a request can arrive **defaulted by a LimitRange** rather than written by the author. Appended under its own heading; the two prior framings are untouched.

---

## Voice-exemplar candidates nominated

Nominations only. Not written to `voice-exemplars.md` — the author ratifies exemplars explicitly (Rule 1).

| Function | Excerpt | Recommendation |
|---|---|---|
| **epistemic honesty / self-narrowing** | "One honest correction, because the claim as stated is slightly too neat and you would notice. §5 and §6 are not consequences of the architecture… These are facts about a *project*, made by people in meetings… The parts that can be reasoned about should be reasoned about, and the residue should be admitted as residue." | **Strongest in the chapter.** A chapter retracting its own thesis to the version that survives the exam. Textbook Part 11 order/truth execution, and the register Ch 1 established. ⚑ *excerpt as quoted — the surrounding paragraph contains `memorisation`* |
| **☀️ Zenith** | "One door, and behind it controllers you have already met. Everything in this chapter is a write to the first, reconciled by the second — which is why a chapter that looked like four unrelated subjects turns out to have a single spine." | **Strong.** Synthesis compression that pays off a doubt planted 8,000 words earlier in *Why This Chapter Matters* |
| **stakes without inflation** | "The stakes, stated plainly: about five points on this book's allocation, which is not many. What the number understates is the *shape* of those points… That is the whole case for reading this chapter carefully, and it does not need inflating." | **Strong.** The cleanest instance in the book of Part 14 guardrail #8 — a chapter arguing its own importance *down* and then earning it back structurally |
| **⚓ Worth Securing** | "A snapshot that lives only on the machines it exists to protect you against losing is not a backup. It is a copy that goes down with the original — the maritime word for which is *ballast*, not *lifeboat*." | **Strong.** Model §18.14 length discipline; the metaphor lands the security point rather than decorating it |
| **Logbook Entry** | "Teams that self-host successfully are almost always teams that budgeted for that calendar deliberately… Teams that regret it are usually teams that priced the machines and not the Thursdays." | **Strong.** Composite, attributed to nobody, no invented statistic, and it argues *against* the obvious framing (cost) rather than for it |
| **— Dead Reckoning** | §6's skew table, introduced flat: "This section is a table. There is no honest way around that, and printing the table is the wrong way to teach it: a table you memorised in August is a table you have half-lost by October." | **Moderate–strong.** Announces the register change and its own limits. ⚑ *contains `memorised`* |
| **Extended Analogy** | The pilot boat / harbourmaster / customs officer sequence in §2 — three offices, three questions, and a third option only the last one has. | ⚑ **DO NOT NOMINATE as written.** Pedagogically the best analogy in Part II — the customs officer's "dock provided this container stays sealed" *is* mutating admission — but it spells the character `harbourmaster` ×3 against Ch 4's established `harbormaster`, three sections from the `🏆 Safe Harbor` marker. Re-nominate after the spelling sweep |
| **Exam Alert framing** | "Common traps. Each of these catches real candidates." | ⚑ **DO NOT NOMINATE.** Unverifiable empirical claim about candidate behaviour, in a sentence that then disclaims statistics. Same class as ch-03's Guardrail #8 hold |

**Note on the register generally.** Chapter 8 is the strongest chapter so far on Part 14 compliance — it labels its own priority ordering "authored judgement, not a published ranking," states outright that no invented statistic appears, and does not repeat ch-07's E1 strawman (its nearest neighbour, "any study guide," is self-inclusive and immediately self-implicating). Five of the seven live nominations turn on that discipline.

---

## Objective coverage log

`D1.2` = the second competency under CNCF domain **D1, Kubernetes Fundamentals (44%)** — *"Kubernetes Core Concepts; **Administration**; Scheduling; Containerization"* (`cncf-kcna-curriculum-pdf-2026-08-23.md:13`).

All eight sections carry `objectives: ["D1.2"]`. Chapter 8 is the sole owner of this competency; no earlier chapter claims it.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.2 — Kubernetes Fundamentals › Administration | Chapter 8 | **deep (1 sub-objective partial)** | — |

**One sub-objective ships PARTIAL: `D1.2-08` (auditing).** The chapter names it, places it correctly alongside the three gates, and states what it is for — deliberately, per the outline's Open Question #4 option (b). The closing fetch that would upgrade it completed but never landed on disk. This is the chapter's only incomplete objective and should be recorded as such rather than rounded up.

**Cross-chapter note.** D1.2 is the third of four D1 competencies to ship: D1.1 (Ch 3), D1.4 (Ch 2 — ⚑ still unrecorded because Ch 2's Stage 14 never ran, per ch-03), D1.3 (Ch 7), D1.2 (Ch 8). With D1 complete at 44%, the objective-coverage file now has enough rows for a first domain-level audit — worth running before Part III.

---

## Retrieval-practice ledger

**6 tagged items across 33 graded questions (15 Bearings + 18 Practice) = 18.2%. Below `arc-outline.md:414`'s 20% target for this chapter.** All six tags are accurate — each points at a chapter that genuinely covers the material, verified against shipped text.

| Tested topic | Original chapter | Retested in |
|---|---|---|
| namespaces divided via resource quota | ch 4 §3 | ch 8 — ☆ Bearings #1 item 5 |
| `node.kubernetes.io/unschedulable`, `NoSchedule` semantics | ch 7 §4 | ch 8 — ☆ Bearings #2 item 1 |
| the CRI and the container-runtime boundary | ch 2 §4 | ch 8 — ☆ Bearings #2 item 4 |
| Nodes are cluster-scoped, so no quota can cap them | ch 4 §3 | ch 8 — Practice Q6 |
| requests are what the scheduler filters on | ch 5 §8 | ch 8 — Practice Q7 |
| the control loop — observe, compare, act | ch 3 §6 | ch 8 — Practice Q11 |

**The recommended fix is already in the chapter and needs no fetch.** `arc-outline.md:414` names two mandatory anchors for Chapter 8: "Namespaces under ResourceQuota" (delivered, tagged twice) and "**node conditions**" — which is Ch 4 §3's `kube-node-lease` forward bearing. Chapter 8 delivers it as **Bearings #2 item 5** and leaves it **untagged**, reasoning that it tests §4's own material.

Tagging that item `[retrieval: ch4]` yields **7/33 = 21.2%**, inside the 20–25% band, *and* discharges the outline's second mandatory anchor as a labelled retrieval item. It is defensible on the merits: the item's second half — "say which namespace holds the objects the second one uses" — is answerable **only** from Ch 4 §3's four-namespace table, and the answer key already credits Chapter 4 explicitly. This is preferable to the two fixes the chapter proposes for itself, one of which depends on a snapshot that has not landed and the other of which adds a question.

**Both ≥4-back floor items are satisfied** — `arc-outline.md:414` requires "Ch 2 CRI **or** Ch 3 control loop" and the chapter delivers **both** (Bearings #2 item 4, six chapters back; Practice Q11, five back). This is the first chapter at which B3's ≥4-back floor binds.

**Two accounting corrections.** The chapter's own AUTHOR-REVIEW note states "6 of 34 = 17.6%" — the denominator is 33, not 34, so the rate is 18.2%. And that note's fallback proposal (add a `[retrieval: ch6]` DaemonSet item) is sound but unnecessary if Bearings #2 item 5 is tagged.

**⚑ Standing gap, third chapter running.** `book-outline/retrieval-architecture.md` is still not the B3 document — it is a permission-failure message plus a prose summary. The per-chapter schedule was never written to disk. This ledger remains the only durable record of what has actually been retrieved, which is the strongest single argument for replaying these eight manifests.
```

Now the write intentions.

```
=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===

## Chapter 8 — Standing the Watch (Administration · D1.2)

> Definitions inherited verbatim from Chapter 8 per Stage 14 Rule 5. Rows marked ⚑
> carry an open definitional gap: the chapter names the term but does not define it.
> Do not paraphrase these into definitions — either land the named snapshot or have
> the author supply wording.

### The command surface (§1)

**`kubectl` grammar** — "Every `kubectl` invocation takes the form `kubectl [command] [TYPE] [NAME] [flags]`." Four slots, of which NAME and flags are optional. (Chapter 8 §1)

**command (slot)** — "The operation you want performed on one or more resources: `create`, `get`, `describe`, `delete`." (Chapter 8 §1)

**TYPE (slot)** — The resource type. "Resource types are case-insensitive, and you may use the singular, plural, or abbreviated form." (Chapter 8 §1)

**NAME (slot)** — "The name of the specific resource. If the name is omitted, details for all resources are displayed." **Resource names are case-sensitive.** (Chapter 8 §1)

**flags (slot)** — Optional. "Flags you specify on the command line override default values and any corresponding environment variables." (Chapter 8 §1)

**★ Case asymmetry** — "The tool is relaxed about what kind of thing you meant and exacting about which one." Types are case-insensitive and abbreviable; names are case-sensitive. `Node worker-3` works; `node Worker-3` does not. (Chapter 8 §1)

**`kubectl explain`** — "Get documentation of various resources." One of only two verbs in the table that answers a question about something other than your cluster. (Chapter 8 §1)

**`kubectl config`** — "Modify kubeconfig files." The other verb that is not about your cluster — it is about your laptop. (Chapter 8 §1)

**kubeconfig** — "For configuration, `kubectl` looks for a file named `config` in the `$HOME/.kube` directory. You can specify other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag." (Chapter 8 §1)

**kubeconfig precedence** — Default location, then environment variable, then flag. Per the general rule, **the flag wins over the environment variable**. (Chapter 8 §1)

**In-cluster authentication** — "By default `kubectl` first determines whether it is running within a Pod… It starts by checking for the `KUBERNETES_SERVICE_HOST` and `KUBERNETES_SERVICE_PORT` environment variables, and for the existence of a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. If all three are found, in-cluster authentication is assumed." (Chapter 8 §1)

**Namespace override (in-cluster)** — "When `kubectl` runs in a cluster it acts against the namespace of the ServiceAccount, unless `--namespace` is given." (Chapter 8 §1)

### The three gates (§2)

**★ The three gates** — "Authentication, then authorization, then admission. Authentication asks **who**. Authorization asks **may you**. Admission asks **should this, exactly as written, be allowed to happen** — and it is the only one of the three that can change your request instead of refusing it." (Chapter 8 §2)

**Authentication** — Establishes the identity behind the request. "The API server is configured to listen for remote connections on a secure HTTPS port, typically 443, with one or more forms of client authentication enabled." (Chapter 8 §2)

**Authorization** — "Decides whether the identity established at gate one is permitted to perform *this action* on *this object*." "Securing your cluster means implementing effective authentication *and* authorization for API access: the pair, not either alone." (Chapter 8 §2)

**Admission control** — "Admission controllers see a request that has already been authenticated and authorized, and act on it before it is written down." The distinguishing property: "Authentication and authorization answer yes or no. Admission may answer yes, no, or *yes — but not as you wrote it*." (Chapter 8 §2)

⚑ **ORDERING AND MUTATION — SOURCING NOTE.** The three names and their relative order in a documentation table of contents are sourced (`k8s-docs-cluster-administration-2026-08-23`, `k8s-docs-extending-kubernetes-2026-08-23`). The **sequential-gate semantics** are NOT sourced in Chapter 8's referenced snapshot set: (i) that a request passes the three in order, (ii) that admission runs after authorization and before persistence, (iii) that admission may mutate rather than only accept or reject. The closer is `k8s-docs-controlling-access-*`, reported complete by the research stage but never written to `sources/`. Do not harden these downstream until it lands.

⚑ **Admission plugin / admission controller (headword)** — Chapter 8 uses six surface forms. **Recommended ruling, pending author ratification:** "admission controller" is the category; "admission plugin" names a specific built-in (NodeRestriction); `policy plugin` is retired. See `concepts/admission-control.md`.

⚑ **Dynamic admission control / admission webhook** — "Dynamic admission control means the cluster calls out to a webhook *you* supplied. Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend," which "adds a potential point of failure." PARTIAL — the mutating/validating phase split is never named; the outline judged it above associate tier. (Chapter 8 §2)

⚑ **Auditing** — Named only, and placed: "the cluster-administration guidance on securing a cluster lists **Auditing**. It sits in the same list, at the same level, as the three access-control pages." Functionally, "it is what tells you afterwards what happened." GAP — no cached snapshot in this chapter's set defines what an audit record contains, what stages are recorded, or that auditing is policy-driven. **This is the chapter's one PARTIAL objective, D1.2-08.** (Chapter 8 §2)

**Hub-and-spoke API pattern** — "All API usage from nodes, or from the Pods they run, terminates at the API server. None of the other control plane components are designed to expose remote services." (Chapter 8 §2)

⚑ **SCOPE — READ BEFORE REUSING.** Chapter 3's canonical treatment scopes this to the **state/API path**: the API server *does* open connections to kubelets for logs, attach and port-forward, and those paths carry a session, not an instruction. Chapter 8 restates the claim unscoped ("There are not [other doors]"; "There are no side channels") while its own §1 verb table lists `logs` and `exec`. See `concepts/api-server-hub.md` § Rule 6. **Do not restore the absolute phrasing.**

⚑ **Kubelet TLS bootstrapping** — "Automating the provisioning of those certificates is what kubelet TLS bootstrapping is for." PARTIAL — purpose stated, mechanism absent. Nothing else in the book defines it. (Chapter 8 §2)

⚑ **Bearer token** — Used as a term of art: "Kubernetes automatically injects the public root certificate and a valid bearer token into the Pod when it is instantiated." GAP — undefined here and in all prior chapters. (Chapter 8 §2)

**NodeRestriction admission plugin** — "Prevents the kubelet from setting labels with a `node-restriction.kubernetes.io/` prefix." **Closes ch-07's registered partial** — Chapter 7 defined the behaviour and deferred the category; Chapter 8 §2 supplies the category as the enforcement point. (Chapter 8 §2; introduced Chapter 7 §3)

**Pod Security Admission** — "The Pod Security Standards are enforced by the built-in Pod Security Admission controller." One clause; Chapter 12 owns the three profiles and three modes. Registered here as an *instance of the third gate*, which is the derivation Chapter 12 depends on. (Chapter 8 §2)

### Dividing a shared cluster (§3)

⚑ **ResourceQuota** — "Namespaces are a way to divide cluster resources between multiple users, via resource quota." Chapter 8's compression: "A quota is a ceiling on a **namespace, in aggregate**: the team's total, not any one Pod's numbers." GAP — what a quota counts, its rejection behaviour (403), and the requests-must-be-specified rule are all absent, because `k8s-docs-resource-quotas-*` never landed in `sources/`. **BLOCKING.** (Chapter 8 §3; handed forward from Chapter 4 §3)

⚑ **LimitRange** — "Use LimitRanges to ensure that Pods specify their resource requirements." Chapter 8's compression: "a constraint on **individual objects**, and a mechanism that has to be able to act on a manifest that says nothing at all." GAP — the min/max/default structure and the "validations occur only at Pod admission stage, not on running Pods" caveat are both absent. **BLOCKING.** (Chapter 8 §3)

**★ The discrimination** — "**ResourceQuota counts the namespace. LimitRange constrains the object.** One is a ceiling on a team; the other is a rule about a manifest." The two diagnostic questions: *what is being counted*, and *what happens to a manifest that says nothing about resources* — "The quota may refuse it. The LimitRange may fill it in." (Chapter 8 §3)

**★ The scope hinge** — "**You can quota a team. You cannot quota a machine.** There is no ResourceQuota that limits how many Nodes a group may consume, because a Node is not in a namespace and a quota is a statement about a namespace." The first operational consequence of Chapter 4's namespaced/cluster-scoped boundary, and the base Chapter 12 derives the RBAC four-way matrix from. (Chapter 8 §3)

### The node (§4)

**Node registration** — "There are two main ways to have Nodes added to the API server: the kubelet on a node self-registers to the control plane, which is the default, or you (or another human user) manually add a Node object." Both routes produce the same artefact at the same door. (Chapter 8 §4)

**Node validation** — "After you create a Node object, the control plane checks whether it is valid — whether a kubelet has registered with the API server matching the `metadata.name` field of the Node — and if the node is healthy… then it is eligible to run a Pod." The name "must be a valid DNS subdomain name and must be unique." (Chapter 8 §4)

**★ `cordon`** — "Marking a node as unschedulable with `kubectl cordon $NODENAME` prevents the scheduler from placing new Pods onto that Node, but does not affect existing Pods on the Node; this is useful as a preparatory step before a node reboot or other maintenance." **Stops arrivals and touches nothing already aboard.** (Chapter 8 §1, §4)

**`drain`** — "`kubectl drain` evicts the Pods." The command that empties what `cordon` deliberately left running. (Chapter 8 §4)

**`uncordon`** — "`kubectl uncordon` restores scheduling." (Chapter 8 §4)

**⚠ A cordoned node is not an empty node** — "If you cordon a node and then reboot it for maintenance, every Pod still on that node goes down with the machine." The maintenance sequence needs `cordon` **and** `drain`. (Chapter 8 §4)

**DaemonSet exception** — "Pods that are part of a DaemonSet tolerate being run on an unschedulable Node," because "the DaemonSet controller automatically adds a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect to DaemonSet Pods." (Chapter 8 §4)

**Node status** — "A Node's status contains Addresses (HostName, ExternalIP, InternalIP); Conditions; Capacity and Allocatable; and Info such as kernel version, container runtime and kubelet version." Shown by `kubectl describe node <name>`. (Chapter 8 §4)

**Node conditions** — Five: `Ready`, `DiskPressure`, `MemoryPressure`, `PIDPressure`, `NetworkUnavailable`. (Chapter 8 §4)

**`Ready`** — "The node is healthy and ready to accept Pods. **False** if the node is not healthy and is not accepting Pods. **Unknown** if the node controller has not heard from the node in the last `node-monitor-grace-period`." (Chapter 8 §4)

**★ `Ready: Unknown`** — "Not a fourth failure mode. It is the control plane declining to guess." `False` means the node reported *itself* unhealthy — it is talking to you. `Unknown` means nobody has heard from it, "which could equally be a dead machine or a network partition." (Chapter 8 §4)

⚑ **`node-monitor-grace-period`** — Named inside the `Ready` definition; the value is deliberately withheld. "This book will not give you a number for it, because the examinable fact is what `Unknown` *asserts*, not how many seconds preceded it." PARTIAL BY DESIGN. (Chapter 8 §4)

**Node heartbeats** — "For nodes there are two forms of heartbeat: updates to the `.status` of a Node, and Lease objects within the `kube-node-lease` namespace, with each Node having an associated Lease object." **Closes Chapter 4 §3's forward bearing.** (Chapter 8 §4)

**Node controller** — "A Kubernetes control plane component that manages several aspects of nodes: assigning a CIDR block to the node when it is registered; keeping its internal list of nodes up to date with the cloud provider's list of available machines; and monitoring the nodes' health — updating the `Ready` condition to `Unknown` when a node becomes unreachable, and triggering API-initiated eviction of all the Pods from the node if it stays unreachable." **It is a control loop.** (Chapter 8 §4) — ⚑ **Closes ch-07's three-casings gap (G7/T2).** Ratify one form: recommended **"node controller"**, with "node lifecycle controller" recorded as an alias and Chapter 3's capitalised "Node controller" swept to match. See `concepts/node-controller.md`.

**Allocatable** — "'Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods." "The scheduler treats 'Allocatable' as the available capacity for Pods, and does not over-subscribe it." (Chapter 8 §4; introduced Chapter 7 §2)

⚑ **Capacity (node)** — **GAP, AND A REGRESSION.** Chapter 8 states only that "Capacity and Allocatable are two different numbers on the same Node object, and the second is the one the scheduler uses." No definition of Capacity, and no relationship between the two — correctly, since `k8s-docs-node-allocatable-2026-08-24`'s extraction note records that the relationship appears only as an image and instructs that no arithmetic relationship be stated in words. **But Chapter 7 §2 deferred this term to Chapter 8 by name**, and Chapter 8 is now its designated owner with nothing to give. Either land `reserve-compute-resources` (which supplies `kube-reserved` / `system-reserved` and the motivation sentence, with no arithmetic) or soften Chapter 7 L408's promise to a deferral.

### Who owns the control plane (§5)

**Cluster planning axes** — Five documented questions: local vs high-availability multi-node; hosted vs self-hosted; on-premises vs cloud; bare-metal vs virtual machines; running a cluster vs developing Kubernetes itself. (Chapter 8 §5)

**minikube** — "Runs a single- or multi-node local Kubernetes cluster." A learning tool. (Chapter 8 §5)

**kind** — "Kubernetes IN Docker — runs local clusters using Docker containers as nodes." A learning tool. "Nodes-as-containers is what makes a kind cluster cheap to create and destroy." (Chapter 8 §5)

**kubeadm** — "The officially supported tool for creating clusters, used to install the control plane and join nodes." (Chapter 8 §5)

**k3s** — "A lightweight distribution." An ecosystem tool, not the official bootstrapper. (Chapter 8 §5)

**Container runtime requirement** — "A container runtime — containerd or CRI-O — must be installed on every node, and `kubectl` is the command-line tool for managing any cluster." Kubernetes reaches it "through the CRI, the Container Runtime Interface, which exists precisely to support alternative container runtimes." **The first operational consequence of Chapter 2's interface boundary.** (Chapter 8 §5)

⚑ **Managed vs self-hosted duty split** — "Some operational aspects sit with whoever runs the control plane, and which ones move is a per-provider question." PARTIAL, and permanently so absent a new source: `k8s-docs-setup-tooling-2026-08-23` licenses only the *existence* of a split ("consider which aspects of operating a Kubernetes cluster… you want to manage yourself and which you prefer to hand off to a provider"), and kubernetes.io does not document commercial providers' responsibility models. Needs a vendor-neutral shared-responsibility source or permanent acceptance of the narrowed form. (Chapter 8 §5)

### Version skew (§6)

**Semantic versioning** — "Kubernetes versions are expressed as `x.y.z`, where x is the major version, y is the minor version, and z is the patch version." (Chapter 8 §6)

**Supported releases** — "The Kubernetes project maintains release branches for the most recent **three** minor releases." (Chapter 8 §6)

**Patch support window** — "Kubernetes 1.19 and newer receive approximately one year of patch support; 1.18 and older received approximately nine months." (Chapter 8 §6)

**Release cadence** — "Since 2021 the project ships **three minor releases per year**, approximately every fifteen weeks… patch releases are cut monthly from the supported branches." (Chapter 8 §6)

**★ The generating rule** — "**Nothing in the cluster may be newer than the API server it talks to.**" Generates three of the five skew rows. (Chapter 8 §6)

**kube-apiserver skew (HA)** — "In highly-available clusters, the newest and oldest kube-apiserver instances must be within **one** minor version of each other." A mutual bound between API servers, not a bound relative to one. (Chapter 8 §6)

**kubelet skew** — "Must not be newer than kube-apiserver. May be up to **three** minor versions older. (A kubelet older than 1.25 may only be up to two minor versions older.)" (Chapter 8 §6)

**kube-proxy skew** — "Must not be newer than kube-apiserver. May be up to three minor versions older than kube-apiserver, and up to three minor versions older *or newer* than the kubelet instance it runs alongside." (Chapter 8 §6)

**Controller-manager / scheduler / cloud-controller-manager skew** — "Must not be newer than the kube-apiserver instances they communicate with. Expected to match the kube-apiserver minor version, but may be up to **one** minor version older, to allow live upgrades." (Chapter 8 §6)

**★ `kubectl` skew** — "Supported within **one** minor version, **older or newer**, of kube-apiserver." **The single exception**, and the only symmetric window in the table, "because `kubectl` is a user tool that addresses the cluster from outside, not a component running as part of it." (Chapter 8 §6)

**Upgrade order** — "If nothing may be newer than the API server, then the API server must be upgraded first; everything else follows behind it, within its permitted window. There is no second rule to learn here." (Chapter 8 §6)

### etcd (§7)

**etcd** — "A consistent and highly-available key value store used as Kubernetes' backing store for all cluster data." "**All Kubernetes objects are stored in etcd.**" (Chapter 8 §7; introduced Chapter 3 §2)

**Why backup matters** — "Periodically backing up the etcd cluster data is important to recover Kubernetes clusters under disaster scenarios, such as **losing all control plane nodes**." What is lost is "the entire record of *intent*… Nothing can be reconciled, scheduled, scaled or healed against a record that no longer exists." (Chapter 8 §7)

**`etcdctl snapshot save`** — One of two backup methods: "a built-in snapshot, `etcdctl snapshot save backup.db`, or a volume snapshot of etcd's storage." Takes optional `--endpoints`, `--cacert`, `--cert` and `--key` for a TLS-protected cluster. (Chapter 8 §7)

**`etcdutl snapshot restore`** — "Operates directly on the etcd data files; after a restore, the control plane components are restarted against the restored data directory." A maintenance event, not an operation against a running cluster. (Chapter 8 §7)

**★ etcd access** — "**Access to etcd is equivalent to root permission in the cluster**, so ideally only the API server should have access to it." Note the modality: a strong recommendation, not an invariant. **Do not harden downstream** (standing instruction from Chapter 3). (Chapter 8 §7)

**Snapshot handling** — "The snapshot file contains all the Kubernetes state and critical information; keep it encrypted and store it outside the control plane nodes." Together with the access rule: "an unencrypted etcd snapshot sitting on a control-plane node is simultaneously your only disaster recovery and a complete compromise of the cluster." (Chapter 8 §7)

### Synthesis (§8)

**★ The chapter's claim, in its narrowed form** — "**Every administrative *act* in this chapter is a write through one door, reconciled by a controller you already know. The project's *policies* are not, and those are the parts you memorise.**" The narrowing is deliberate and follows Chapter 4 §6's established habit. (Chapter 8 §8)

**The two diagnostic questions** — "Faced with an unfamiliar Kubernetes administrative feature, ask two questions in this order: **what object does it write**, and **what controller is watching that object?**" (Chapter 8 §8)

### Commands introduced

**`kubectl explain`** · **`kubectl config`** · **`kubectl cordon $NODENAME`** · **`kubectl drain`** · **`kubectl uncordon`** · **`kubectl describe node <name>`** · **`etcdctl snapshot save backup.db`** · **`etcdutl snapshot restore`**

⚑ **Deferred, named only:** `kubectl logs` and `kubectl exec` — listed in §1's verb table and handed to Chapter 13. Chapter 13 owns their definitions.

=== END APPEND ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubectl-grammar.md ===
# Concept: The `kubectl` grammar

**Home:** Chapter 8 §1 · **Competency:** D1.2 · **Status:** canonical

## The four slots (verbatim)

> `kubectl [command] [TYPE] [NAME] [flags]`

NAME and flags are optional.

| Slot | What it holds |
|---|---|
| **command** | "The operation you want performed on one or more resources: `create`, `get`, `describe`, `delete`" |
| **TYPE** | The resource type |
| **NAME** | "The name of the specific resource. If the name is omitted, details for all resources are displayed" |
| **flags** | Optional. "Flags you specify on the command line override default values and any corresponding environment variables" |

Two commands omit slots in instructive ways. `kubectl get pods` omits NAME and flags, and gets every Pod. `kubectl cordon node-7` omits TYPE entirely, "because the verb already implies what kind of thing it operates on" — which is why the documented form is `kubectl cordon $NODENAME` and not a three-token command.

## ★ The examinable half — the case asymmetry

> Resource **types** are case-insensitive, and you may use the singular, plural, or abbreviated form.
> Resource **names** are case-sensitive.

Chapter 8's compression: "The tool is relaxed about what kind of thing you meant and exacting about which one."

`Node worker-3` works. `node Worker-3` does not.

The two symmetrical answers — "both insensitive," "both sensitive" — are the standard distractor pair, and the permissive one is the more common error because the tool's tolerance about types invites the generalisation.

⚑ The abbreviated form `po` is used in Figure 8.1's callout as an instantiation of the sourced singular/plural/abbreviated rule, but the specific string `po` appears in no cached snapshot. Near-certain, low-risk, unsourced.

## The verb surface

`get` · `describe` · `apply` · `create` · `delete` (Ch 4) · `scale` · `rollout` (Ch 6) · `explain` · `config` (Ch 8) · `logs` · `exec` (**Ch 13 owns these**).

Two of the eleven answer a question about something other than your cluster: **`explain`** queries the API's own documentation, and **`config`** modifies kubeconfig files — a question about your laptop.

## Related

`[[kubeconfig]]` · `[[declarative-configuration]]` — Chapter 4's point stands unchanged: the objects are declarations, and the imperative verbs work by changing declarations · `[[node-lifecycle]]` · `[[kubernetes-object]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/kubeconfig.md ===
# Concept: kubeconfig, and where `kubectl` finds its cluster

**Home:** Chapter 8 §1 · **Competency:** D1.2 · **Status:** canonical

## The precedence chain

> "For configuration, `kubectl` looks for a file named `config` in the `$HOME/.kube` directory. You can specify other kubeconfig files by setting the `KUBECONFIG` environment variable or by setting the `--kubeconfig` flag."

Three sources, and per the general flags-override-environment rule, **the flag wins**:

```
--kubeconfig  >  KUBECONFIG  >  $HOME/.kube/config
```

The file holds an address and a credential — and the answer to the two-server problem: which cluster you are *currently* talking to.

*Common wrong turn:* "the environment variable, because it is set for the whole session." The general rule runs the other way.

## The surprising case — `kubectl` inside a Pod

> "By default `kubectl` first determines whether it is running within a Pod, and thus inside a cluster. It starts by checking for the `KUBERNETES_SERVICE_HOST` and `KUBERNETES_SERVICE_PORT` environment variables, and for the existence of a ServiceAccount token file at `/var/run/secrets/kubernetes.io/serviceaccount/token`. If all three are found, in-cluster authentication is assumed."

And: "when `kubectl` runs in a cluster it acts against the namespace of the ServiceAccount, unless `--namespace` is given."

**Three checks, an assumed identity, and a different default namespace.** Not your kubeconfig, not you, not the namespace of your current context — and *not necessarily* `default` either, which is the second-order error.

> 🪝 **Snag (verbatim):** "`kubectl` inside a Pod is not you, and does not look where you expect… Every practitioner who has ever run a debugging shell inside a cluster has been surprised by this at least once, usually by an empty `kubectl get pods` that they were certain should have returned something."

⚑ Chapter 8 §2 says the injected bearer token is "what `kubectl` is looking for" here. Two snapshots are being fused — `kubectl-overview` names the token *path*, `control-plane-node-communication` says a bearer token is *injected*. Neither states they are the same artefact. The phrasing was deliberately softened to stop short of asserting identity. Do not tighten it.

## Related

`[[kubectl-grammar]]` · `[[serviceaccount]]` · `[[api-access-gates]]` · `[[namespace]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-access-gates.md ===
# Concept: The three gates at the API server's door

**Home:** Chapter 8 §2 · **Competency:** D1.2 · **Status:** canonical
**Chapter 8's most important idea, and the derivation Chapter 12 depends on.**

## ★ Fixed Point (verbatim — canonical retrieval string)

> **Authentication, then authorization, then admission.** Authentication asks **who**. Authorization asks **may you**. Admission asks **should this, exactly as written, be allowed to happen** — and it is the only one of the three that can change your request instead of refusing it.

Mnemonic: ***Who, may, and how.*** The third is the odd one because "how" is a question about the *request* rather than about *you*.

## The gates

**1. Authentication — who are you?** "The API server is configured to listen for remote connections on a secure HTTPS port, typically 443, with one or more forms of client authentication enabled." Nodes arrive with a client certificate (provisioned, or automated via kubelet TLS bootstrapping); Pods arrive with an injected root certificate and bearer token.

**2. Authorization — may you do this?** Decides whether the identity may perform *this action* on *this object*. "Securing your cluster means implementing effective authentication **and** authorization for API access: the pair, not either alone." RBAC lives here and is Chapter 12's.

**3. Admission — should this, exactly as written, be allowed?** "Admission controllers see a request that has already been authenticated and authorized, and act on it before it is written down."

## ⚠ Navigational Hazard (verbatim)

> **Authorization has no opinion about the contents of your request; admission has no opinion about your identity.** A request can be fully authenticated, entirely authorized, and still be rejected — or quietly rewritten — at the third gate.

The diagnostic value is the point: when a request you were definitely allowed to make is refused anyway, the gate model tells you where to look.

## ⚑ SOURCING — the load-bearing semantics are NOT sourced

The three names and their **relative order in a documentation table of contents** are sourced (`cluster-administration`, `extending-kubernetes`). Three claims this shard is built on are **not** sourced in Chapter 8's referenced snapshot set:

1. that a request passes the three **in order**
2. that admission runs **after authorization and before persistence**
3. that admission may **mutate** rather than only accept or reject

The closer — `k8s-docs-controlling-access-*` — was fetched by the research stage and **never written to `sources/`**. It reportedly carries all three verbatim, plus two free upgrades: the **quorum contrast** (authorization = any module approves and the request proceeds; admission = any module rejects and it is refused immediately), and **"admission does not see reads."**

Until it lands, treat 1–3 as the book's working model, not as cited fact.

## Why three gates at one door is a *complete* story

> "Three gates on one door would be an incomplete access-control story if there were other doors; you would be securing one entrance out of several. There are not."

⚑ **SCOPE.** See `[[api-server-hub]]` § Rule 6 before reusing that sentence. Chapter 3 scopes the single-door claim to the **state/API path** and explicitly preserves the outbound kubelet paths (logs, attach, port-forward). Chapter 8 states it absolutely. The three-gate argument survives the narrowing — those paths originate *at* the API server, so all inbound API usage still terminates there.

## Related

`[[admission-control]]` · `[[api-server-hub]]` · `[[serviceaccount]]` · `[[resource-quota-and-limitrange]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/admission-control.md ===
# Concept: Admission control

**Home:** Chapter 8 §2 · **Competency:** D1.2 · **Status:** canonical
**Closes ch-07's registered partial:** "'admission plugin' as a *category* undefined until Ch 8."

## The distinguishing property

> Authentication and authorization answer yes or no. **Admission may answer yes, no, or *yes — but not as you wrote it*.**

That third option is "the entire reason it is a separate office rather than one more line on the harbourmaster's form."

## ⚑ HEADWORD RULING — recommended, pending author ratification

Chapter 8 uses six surface forms: `admission control`, `admission controllers`, `admission gate`, `admission plugin`, `policy plugin`. Chapter 8 is the designated owner of this category (ch-07 manifest). Proposed:

| Form | Use |
|---|---|
| **admission controller** | the category headword |
| **admission plugin** | a specific built-in (NodeRestriction) — matches Chapter 7's sourced phrasing |
| **admission control** | the gate/stage, when talking about the request path |
| ~~policy plugin~~ | **retire.** A coinage in Bearings #1 item 4's key, anchored to nothing |

## Two instances the reader has already met

**NodeRestriction** — "prevents the kubelet from setting labels with a `node-restriction.kubernetes.io/` prefix." Chapter 7 stated the rule and pointed here for the enforcement. This gate *is* the enforcement, and it is why node-isolation labels can be trusted not to have been forged by the node they describe.

**Pod Security Admission** — "The Pod Security Standards are enforced by the built-in Pod Security Admission controller." One clause only; Chapter 12 owns the three profiles and three modes.

**The derivation matters more than either fact:** when Pod Security Admission arrives in Chapter 12, it is not a new kind of thing. It is one instance of the third gate.

## Dynamic admission control

> "Kubernetes makes synchronous HTTP requests to a remote service, a webhook backend," and the documentation is candid that this "adds a potential point of failure."

Practically: once you install a validating webhook, your webhook being down can stop your cluster accepting requests.

⚑ PARTIAL — the **mutating/validating phase split is never named** in Chapter 8. The outline judged it above associate tier and Chapter 12 does not need it. Not a defect; do not add it without an author decision.

## ⚑ ResourceQuota and LimitRange enforcement

Chapter 8 §3 closes by observing that both "take effect at the admission gate. Neither is a separate subsystem with its own enforcement path." **No snapshot in Chapter 8's referenced set states this.** Standard and near-certain, but unsourced — closed by the same `controlling-access` landing.

## Related

`[[api-access-gates]]` · `[[resource-quota-and-limitrange]]` · `[[api-server-hub]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-quota-and-limitrange.md ===
# Concept: ResourceQuota and LimitRange

**Home:** Chapter 8 §3 · **Competency:** D1.2 · **Status:** ⚑ **canonical but under-delivered**
**Discharges (thinly):** Chapter 4 §3's "ResourceQuota is named and handed to Chapter 8," and Chapter 7 §2's IOU on the mechanisms that stop other people booking the cluster.

## What is sourced

Exactly two claims:

1. "Namespaces are a way to divide cluster resources between multiple users, **via resource quota**." [namespaces]
2. "Define ResourceQuotas to **fairly allocate shared resources**, and use LimitRanges to **ensure that Pods specify their resource requirements**." [cloud-native-security]

## ★ The discrimination

> **ResourceQuota counts the namespace. LimitRange constrains the object.**
> One is a ceiling on a team; the other is a rule about a manifest.

Two diagnostic questions that survive better than definitions:

| Question | ResourceQuota | LimitRange |
|---|---|---|
| **What is being counted?** | the namespace's total | one object's numbers |
| **What happens to a manifest that says nothing about resources?** | may **refuse** it | may **fill it in** |

The second question is the sharper one, and it is the §2 mutate-versus-reject distinction "showing up one gate later in the same request's life."

## ⚑ WHAT IS MISSING — BLOCKING

Everything about **scope, defaulting, and what a quota counts** is unsourced: the aggregate/per-object framing, the ★ Fixed Point above, Figure 8.3's `min ≤ … ≤ max` per-Pod bound, and Practice Q6's rebuttal of distractor A.

Both closing fetches **completed and were never written to `sources/`**. They reportedly supply:

- what a quota counts (compute totals, object counts, storage — **names only**; G-8C forbids quoting the row descriptions)
- the 403 rejection
- **the most examinable fact available here:** "If you enforce a resource quota in a namespace for either `cpu` or `memory`, you and other clients **must** specify either `requests` or `limits`."
- LimitRange: "Enforce minimum and maximum compute resources usage per Pod or Container in a namespace" — which resolves Figure 8.3 **in the figure's favour**; bring the prose up, do not cut the figure down
- "validations occur only at Pod admission stage, not on running Pods"

**Scope guard, unchanged:** do NOT take quota scopes, scope selectors, priority-class quota, or the full countable-resource roster. All above associate tier.

## ⚑ An internal inconsistency the fetch resolves

Chapter 8's ⚓ Worth Securing was softened in revision because draft-v1's version (a quota with no LimitRange lets one request-less Pod consume the whole allocation) contradicts this section's own "the quota may refuse it." The requests-must-be-specified rule settles it **in favour of "the quota refuses it."** When the snapshot lands, the callout and the "manifest that says nothing" line move together.

## The hinge — and it is what Chapter 12 derives from

Both objects are **namespaced**. Nodes are not.

> **You can quota a team. You cannot quota a machine.**

"There is no ResourceQuota that limits how many Nodes a group may consume, because a Node is not in a namespace and a quota is a statement about a namespace." See `[[cluster-scoped-resource]]`.

## Related

`[[cluster-scoped-resource]]` · `[[namespace]]` · `[[resource-request]]` · `[[admission-control]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-lifecycle.md ===
# Concept: Node lifecycle — registration, cordon, drain, uncordon

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical

## Where Nodes come from

> "There are two main ways to have Nodes added to the API server: the kubelet on a node **self-registers** to the control plane, which is the default, or you (or another human user) **manually add a Node object**."

Validation follows either route: "the control plane checks whether it is valid — whether a kubelet has registered with the API server matching the `metadata.name` field of the Node — and if the node is healthy… it is eligible to run a Pod." The name "must be a valid DNS subdomain name and must be unique."

**What the two routes have in common is the point.** A kubelet joining a cluster and a human joining a machine to a cluster produce the same artefact: a Node object at the API server. "The kubelet does not open a private channel. It arrives at the same door you do."

## ★ The three commands

> `cordon` stops arrivals and touches nothing already aboard. `drain` clears what is aboard. `uncordon` reopens. **The maintenance sequence needs the first two.**

- **`kubectl cordon $NODENAME`** — "prevents the scheduler from placing new Pods onto that Node, but **does not affect existing Pods on the Node**; this is useful as a preparatory step before a node reboot or other maintenance."
- **`kubectl drain`** — "evicts the Pods."
- **`kubectl uncordon`** — "restores scheduling."

## ⚠ A cordoned node is not an empty node

"If you cordon a node and then reboot it for maintenance, every Pod still on that node goes down with the machine."

This is the chapter's single most consequential confusion and, unlike most exam traps, it has a real operational cost. The instinct that "take out of service" means "empty" is reasonable — Kubernetes splits it in two because there are real cases where you want arrivals stopped and current occupants left in place. **The split is a feature. It is also a trap.**

> 🪢 A cordon is a rope across a doorway. It stops people coming in. It does not remove the people already inside.

## The DaemonSet exception

"Pods that are part of a DaemonSet tolerate being run on an unschedulable Node," because "the DaemonSet controller automatically adds a `node.kubernetes.io/unschedulable` toleration with a `NoSchedule` effect to DaemonSet Pods."

Chapter 6 taught one-Pod-per-eligible-node; Chapter 7 taught the built-in condition tolerations. This is where they turn out to have been the same fact.

## ⚑ What is NOT established

**No cached source connects `kubectl cordon` to the `node.kubernetes.io/unschedulable` taint.** Three facts are separately sourced — cordon prevents new placements [nodes]; the taint exists with a `NoSchedule` effect [daemonset, taints-depth]; the scheduler checks taints [taints-depth] — and **no cached sentence links the first to the second.** `taints-tolerations-depth` attributes automatic taint creation to node *conditions*, and unschedulability is not one.

The closer — "cordoned nodes are marked Unschedulable in their spec" — sits unwritten in `research-manifest.md`. Until then: **do not assert that cordon writes the taint, and do not assert `.spec.unschedulable`.** See `[[built-in-node-condition-taints]]`.

## Related

`[[node-conditions]]` · `[[node-controller]]` · `[[built-in-node-condition-taints]]` · `[[taint]]` · `[[api-server-hub]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-conditions.md ===
# Concept: Node conditions and heartbeats

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical
**Discharges:** Chapter 4 §3's forward bearing on `kube-node-lease` and node failure detection.

## Node status

"A Node's status contains **Addresses** (HostName, ExternalIP, InternalIP); **Conditions**; **Capacity and Allocatable**; and **Info** such as kernel version, container runtime and kubelet version." Shown by `kubectl describe node <name>`.

## The five conditions

| Condition | True when |
|---|---|
| `Ready` | The node is healthy and ready to accept Pods. **False** if not healthy and not accepting Pods. **Unknown** if the node controller has not heard from the node in the last `node-monitor-grace-period` |
| `DiskPressure` | Pressure exists on the disk size |
| `MemoryPressure` | Pressure exists on the node memory |
| `PIDPressure` | Pressure exists on the processes |
| `NetworkUnavailable` | The network for the node is not correctly configured |

## ★ `Ready` is three-valued, and the third value is the teaching

> `Unknown` "is not a fourth failure mode. It is the control plane declining to guess."

- **`False`** — the node reported *itself* unhealthy. **The node is talking to you.**
- **`Unknown`** — nobody has heard from it, "which could equally be a dead machine or a network partition between the machine and the control plane."

Those two situations call for different interventions, "which is why the distinction is preserved rather than collapsed."

*Common wrong turns:* `False` (the intuitive answer), and `NotReady` — **not one of the condition's three documented values.**

⚑ `node-monitor-grace-period` is named and its value **deliberately withheld**: "the examinable fact is what `Unknown` *asserts*, not how many seconds preceded it, and a number you half-remember is worse than a parameter name you can look up." The landed-but-unwritten `node-status` snapshot documents a default of 50 seconds; per the outline's standing instruction it may be added **only as a dated illustration, never as a rule**. That snapshot also supplies a ready-made 🪝 Snag: "SchedulingDisabled is not a Condition in the Kubernetes API."

## Two heartbeat forms

> "For nodes there are two forms of heartbeat: updates to the **`.status` of a Node**, and **Lease objects within the `kube-node-lease` namespace**, with each Node having an associated Lease object."

Chapter 4 §3 listed `kube-node-lease` among the four initial namespaces and pointed here. **That debt is settled.** The Lease is the form readers forget, "because it lives somewhere you have to have looked."

*Common wrong turn:* placing the Leases in `kube-system` — the namespace for system objects generally, not the one dedicated to node leases.

## Capacity and Allocatable

"Allocatable' on a Kubernetes node is defined as the amount of compute resources that are available for pods," and "the scheduler treats 'Allocatable' as the available capacity for Pods, and does not over-subscribe it."

⚑ **Chapter 8 states only that the two numbers differ and that Allocatable is the one the scheduler uses.** `node-allocatable`'s extraction note records that the Capacity → Allocatable relationship appears **only as an image** and instructs that no arithmetic relationship be stated — including in words ("what is left after overheads are set aside" is an arithmetic relationship). **Capacity is therefore undefined book-wide**, against a Chapter 7 §2 promise that named Chapter 8 as its owner. See the glossary's Capacity row for the two honest discharges.

## Related

`[[node-lifecycle]]` · `[[node-controller]]` · `[[namespace]]` · `[[resource-request]]` · `[[feasible-node]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/node-controller.md ===
# Concept: The node controller

**Home:** Chapter 8 §4 · **Competency:** D1.2 · **Status:** canonical
**Purpose of this shard:** close ch-07's registered gap **G7/T2 — "three casings, one referent."**

## Definition (verbatim)

> "A Kubernetes control plane component that manages several aspects of nodes: **assigning a CIDR block** to the node when it is registered; **keeping its internal list of nodes up to date** with the cloud provider's list of available machines; and **monitoring the nodes' health** — updating the `Ready` condition to `Unknown` when a node becomes unreachable, and triggering API-initiated eviction of all the Pods from the node if it stays unreachable."

## ⚑ THE CASING GAP — ratification needed

| Form | Where |
|---|---|
| **`node controller`** | Chapter 8 ×11 (body), Chapter 7 ×2 |
| `Node controller` | Chapter 3 ×5; Chapter 8 ×1 (Chapter Summary row — internally inconsistent with its own body) |
| `node lifecycle controller` | Chapter 7 ×2 |

**Recommended ruling:** ratify **`node controller`** lowercase, record **`node lifecycle controller`** as an alias in one clause where Chapter 8 §4 defines it, and sweep Chapter 3's five capitalised instances to match. Chapter 8 is the chapter that defines the component, so it is the right place to carry the alias.

## ★ It is a control loop, and that is the sixth instance

Read the third job as a shape: **it observes** (heartbeats), **compares** against what it expects, and **acts** (condition update, then eviction).

> "Controllers read an object's `.spec`, possibly do things, and then update the object's `.status`."

Chapter 8 §8 makes this explicit — "The node controller is a control loop… This is the sixth" — and it buys §8 half its synthesis argument for one sentence.

⚑ **Note for B3.** ch-03 recorded the control-loop retrieval chain as Ch 3→4→6→11→15→17. **Chapter 8 is not on that list and bears the theme anyway**, by name. Either the chain is stale or this is unbudgeted retrieval work. Worth settling before Ch 11, which ch-03 flagged as still unbeared.

## Related

`[[control-loop]]` · `[[node-conditions]]` · `[[control-plane-components]]` · `[[built-in-node-condition-taints]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cluster-bootstrap-tooling.md ===
# Concept: Cluster bootstrap tooling, and what ownership means

**Home:** Chapter 8 §5 · **Competency:** D1.2 · **Status:** canonical

## The five planning questions

Before choosing how to build a cluster, the documentation asks: local trial vs high-availability multi-node; hosted vs self-hosted; on-premises vs cloud; bare-metal vs virtual machines; running a cluster vs developing Kubernetes project code.

Chapter 8's honest gloss: "in most working lives the answers arrive already decided — by budget, by a compliance requirement, by what the platform team standardised on two years ago. Knowing the axes still buys you something, because it tells you what was traded away."

## The tools, split by purpose

**For learning:** **minikube** — "runs a single- or multi-node local Kubernetes cluster." **kind** — "Kubernetes IN Docker — runs local clusters using Docker containers as nodes."

**For production:** managed and turnkey certified services from cloud providers, or self-managed clusters bootstrapped with **kubeadm**, "the officially supported tool for creating clusters, used to install the control plane and join nodes." **k3s** is "a lightweight distribution."

> ⚓ kind and minikube are not two names for the same thing, and the documented difference is architectural: **kind runs its nodes as Docker containers.** Nodes-as-containers is what makes a kind cluster cheap to create and destroy.

⚑ Draft-v1 asserted that kind is "the usual choice inside CI pipelines" and minikube "the usual choice when a human is sitting in front of it." **Unattested prevailing-practice claims, removed.** Only the nodes-as-containers difference is sourced. If the ecosystem claim is wanted, reframe it explicitly as the author's operational judgement.

## ★ The requirement none of these removes

"A container runtime — **containerd** or **CRI-O** — must be installed on every node, and `kubectl` is the command-line tool for managing any cluster." Kubernetes reaches it "through the **CRI**, the Container Runtime Interface, which exists precisely to support alternative container runtimes."

**This is the first time Chapter 2's interface boundary has an operational consequence.** `kubeadm` will build a control plane and join nodes, and a runtime must already be present — because a runtime is on the other side of a line the project deliberately drew.

⚑ Draft-v1 said kubeadm "will not put a container runtime on those nodes." That is an unsourced negative assertion about a tool's scope. The snapshot establishes the **requirement**, not that kubeadm declines to satisfy it. The narrowed form carries the same pedagogical weight. Same fix applied to Bearings #2 item 4 and Practice Q12.

## ⚑ What ownership means — deliberately narrow

"Some operational aspects sit with whoever runs the control plane, and which ones move is a **per-provider question**."

Draft-v1 said "a managed control plane means the provider decides when you upgrade, and the provider holds the etcd backup." **`setup-tooling` licenses only the existence of a split**, and kubernetes.io does not document commercial providers' responsibility models — so no fetch from that tree closes it. The claim was load-bearing in three places (this paragraph, Bearings #2 item 5's key, Practice Q13's correct answer); Q13 was rewritten so its axis is "which duties belong to whoever operates the control plane," which is sound on the architecture alone.

Needs a vendor-neutral shared-responsibility source, or permanent acceptance of the narrowed form.

## Related

`[[cri]]` · `[[container-runtime]]` · `[[etcd]]` · `[[version-skew]]` · `[[control-plane-components]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/version-skew.md ===
# Concept: Version skew

**Home:** Chapter 8 §6 · **Competency:** D1.2 · **Status:** canonical
**The single most mechanically checkable block in the curriculum.**

## ★ The generating rule — take this before any numbers

> **Nothing in the cluster may be newer than the API server it talks to.**

Every component is a client of one door. "A client that is *newer* than its server is a client that may ask for things the server has never heard of." That one sentence generates **three of the five rows**. The numbers are then not five unrelated facts; they are *the sizes of the windows*.

## The five rules (verbatim)

| Component | Rule |
|---|---|
| **kube-apiserver** | In HA clusters, newest and oldest instances within **one** minor version of each other |
| **kubelet** | Must not be newer. May be up to **three** minors older. (Older than 1.25: two.) |
| **kube-proxy** | Must not be newer than kube-apiserver. Up to three minors older than it, and up to three older *or newer* than its kubelet |
| **kube-controller-manager, kube-scheduler, cloud-controller-manager** | Must not be newer. Expected to match; may be up to **one** minor older, to allow live upgrades |
| **kubectl** | Within **one** minor version, **older or newer** |

## ★ The exception, which is where the points are

> **`kubectl` is the only component permitted to be *newer* than the API server** — one minor, either direction.

The reason is worth more than the fact: `kubectl` is "a **user tool that addresses the cluster from outside**, not a component running as part of it. It is not participating in the cluster's internal consistency, so its compatibility window is about human convenience." That is why it is the only symmetric window.

## ⚠ The two rows that are not generated by the rule

- **`kubectl`** — for the reason above.
- **The HA kube-apiserver row** — for a *different* reason: "it is not a bound *relative to* an API server at all. It is a mutual bound *between* API servers," symmetric in both directions, so it cannot be produced by a rule about what may be newer than the API server.

Deriving the table this way leaves a residue of two rows, both with reasons — "small enough to hold."

## ⚠ Navigational Hazard

> **kubelet: three minors, older only. `kubectl`: one minor, either direction.** Not the same number and not the same shape.

Candidates who half-remember the kubelet's generous window reach for it when the question is about `kubectl`, "and lose the point twice over: wrong number, wrong direction."

> 🪢 ***Three back, three a year, three branches.*** The kubelet's window, the release cadence, and the supported-branch count are all three. A coincidence, and a useful one — it leaves only `kubectl`'s one to hold separately.

## Upgrade order falls out of the rule

"If nothing may be newer than the API server, then the API server must be upgraded first; everything else follows behind it… **There is no second rule to learn here.**" Reverse it and you spend the upgrade window with components newer than the server they talk to.

## On the numbers

The rules are stable; the roster is not. The supported set at source-capture was 1.36 / 1.35 / 1.34. **Learn the rule and treat the numbers as an illustration.** Nothing in the book's practice questions turns on which minor is current.

## Related

`[[release-cadence]]` · `[[api-server-hub]]` · `[[cluster-bootstrap-tooling]]` — Chapter 13 revisits skew as a cause of misdiagnosed failures.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/release-cadence.md ===
# Concept: Release cadence and supported versions

**Home:** Chapter 8 §6 · **Competency:** D1.2 · **Status:** canonical
**Ch 17 dependency:** `arc-outline.md` requires Ch 17 to retrieve this material inside the release-governance section.

## The three numbers

- **Three** — "The Kubernetes project maintains release branches for the most recent three minor releases."
- **~1 year** — "Kubernetes 1.19 and newer receive approximately one year of patch support; 1.18 and older received approximately nine months."
- **~3 per year** — "Since 2021 the project ships three minor releases per year, approximately every fifteen weeks… patch releases are cut monthly from the supported branches."

Applicable fixes, including security fixes, "may be backported to those three release branches depending on severity and feasibility."

## Why they agree — which is what makes them memorable

"Three releases a year, across three supported branches, is close to a year of coverage, which is what the patch-support figure says. **The three-branch rule is not an arbitrary number somebody picked. It is roughly what 'about a year of support' costs at this release cadence.**"

Chapter 8's own honesty note: close, not exact — three fifteen-week cycles is about forty-five weeks, against a documented "approximately 1 year."

> 🪝 **Snag:** "Kubernetes supports the last two releases" is a common half-memory and it is wrong. It is **three**.

## Retrieval note

This trio "is among the most forgettable material in this book," and Chapter 8 deliberately routes it forward: the Chapter 17 pass, inside SIG Release and the KEP process, "is when it gets its second look." That forward bearing is mandated by `arc-outline.md` and should not be dropped in a later revision.

## Related

`[[version-skew]]` · `[[cluster-bootstrap-tooling]]`
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/etcd.md ===
# Concept: etcd — backup, restore, and why it is the largest single risk

**Home:** Chapter 8 §7 · **Competency:** D1.2 · **Status:** canonical
**Created on assignment.** ch-03's manifest: *"`etcd` — Chapter 8 owns backup/restore and Chapter 12 owns encryption at rest… **Ch 8's Stage 14 creates it.**"*

## Definition

"A consistent and highly-available key value store used as Kubernetes' backing store for all cluster data." (Introduced Chapter 3 §2.)

**"All Kubernetes objects are stored in etcd."** Every Deployment, ConfigMap, Secret, Service — and every Node object, "including the ones a kubelet wrote itself."

## Why backup matters

> "Periodically backing up the etcd cluster data is important to recover Kubernetes clusters under disaster scenarios, such as **losing all control plane nodes**."

Chapter 8's framing of what that loss actually takes: **not the objects' *effects*, but "the entire record of *intent*** — every declaration that says what should be running, which is the only thing that lets the cluster put itself back together when something changes. Nothing can be reconciled, scheduled, scaled or healed against a record that no longer exists."

⚑ Draft-v1 added "Losing every control-plane node does not stop your worker nodes. The kubelets keep running the containers they were last told to run." **Unsourced** — `etcd-backup` names the disaster scenario and says nothing about what survives it, and no snapshot in Chapter 8's set describes kubelet behaviour when the API server is unreachable. Near-certainly true and better teaching; **do not restore it without a source.** Likely closers: `/concepts/architecture/#kubelet`, static-pod or node-shutdown material.

## Mechanics

**Backup** — two ways: "a built-in snapshot, `etcdctl snapshot save backup.db`, or a volume snapshot of etcd's storage." The `etcdctl` form takes optional `--endpoints`, `--cacert`, `--cert`, `--key` for a TLS-protected cluster.

**Restore** — `etcdutl snapshot restore`, which "operates directly on the etcd data files; after a restore, the control plane components are restarted against the restored data directory."

> 🔭 Restore is not a command you run against a running cluster. It is "a maintenance *event*, with a window, a plan, and somebody watching."

⚑ No etcd TLS *configuration* guidance is given, deliberately: the `etcd-access-control` snapshot's note records that the source page's TLS guidance was not verbatim-verified. Do not expand without a fresh fetch.

## ★ The fact that matters more than the commands

Two sentences, read together:

> "The snapshot file contains all the Kubernetes state and critical information; **keep it encrypted and store it outside the control plane nodes**."
>
> "**Access to etcd is equivalent to root permission in the cluster**, so **ideally** only the API server should have access to it."

Together: "an unencrypted etcd snapshot sitting on a control-plane node is simultaneously your only disaster recovery and a complete compromise of the cluster… Not a credential *for* the cluster. Root *in* the cluster, in one file, at rest."

> ⚓ "A snapshot that lives only on the machines it exists to protect you against losing is not a backup. It is a copy that goes down with the original — the maritime word for which is *ballast*, not *lifeboat*."

## ⚑ MODALITY — preserve the hedge

"**Ideally** only the API server should have access." Chapter 3's standing instruction: *"Read that as what it is: a strong recommendation with a security reason behind it, not a law of physics. Do not harden it downstream."* **Chapter 8 complies in all three places** — §7 prose, §7 Fixed Point, §8. Verified. Keep it that way.

## The architecture, stated from the other side

§2 says every request terminates at the API server. §7 says only the API server should reach the store behind it. "Same claim, different direction."

## Related

`[[api-server-hub]]` · `[[control-plane-components]]` · `[[secret]]` — Chapter 12 covers encryption at rest, which is why "keep it encrypted" is in the sentence.
=== END WRITE ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/api-server-hub.md ===

## ⚑ RULE 6 — Chapter 8 restates the hub claim in ABSOLUTE form. Do not adopt its wording.

Chapter 8 §2 and Figure 8.6 assert the unscoped version:

> "Three gates on one door would be an incomplete access-control story if there were other
> doors… **There are not.**"  ·  Figure 8.6: "**There are no side channels.**"

This shard's precision #2 above stands and is **not** superseded. The API server does open
connections to kubelets — logs, attach, port-forward — and Chapter 8's own §1 verb table
lists `logs` and `exec` two sections before the absolute claim. **Do not restore the
absolute phrasing** (standing instruction from Chapter 3, recorded after an author review).

Not a false statement — a scope-of-phrasing defect. Those paths originate *at* the API
server, so all **inbound API usage** still terminates there, and Chapter 8's three-gate
argument survives the narrowing intact. Recommended fix in both chapters: scope to
**inbound API usage**.

## ✅ Two source-availability flags on this shard are now stale

Both snapshots this shard marked "⚑ NOT ON DISK" have since landed and were verified in
`sources/` on 2026-08-24:

- `k8s-docs-control-plane-node-communication-2026-08-24.md` ✓ (fact 3, the hub-and-spoke sentence)
- `k8s-docs-etcd-access-control-2026-08-24.md` ✓ (precision 1, the "ideally" hedge)

Chapter 8 cites both directly. The flags may be cleared.

## Chapter 8 addition — what the door *does*

Chapter 3 established that every request terminates here. Chapter 8 §2 supplies the
"and then what": **three gates — authentication, authorization, admission** — run before
anything is written down, and the third can rewrite the request rather than only refusing
it. See `[[api-access-gates]]`.

§7 states the same architecture from the far side: only the API server should reach etcd.
"Same claim, different direction."

Related: `[[api-access-gates]]` · `[[admission-control]]` · `[[etcd]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/namespace.md ===

## Chapter 8 — both forward assignments come due

**1. ✅ `Lease` ownership — DISCHARGED IN FULL.** B2 settled this in Chapter 8's favour and
this shard recorded the evidence so Ch 5 and Ch 12 would not re-litigate it. Chapter 8 §4
delivers: "for nodes there are two forms of heartbeat: updates to the `.status` of a Node,
and **Lease objects within the `kube-node-lease` namespace**, with each Node having an
associated Lease object" — plus the node controller that watches them and the `Unknown`
condition that follows when they stop. Chapter 4 L584's cross-bearing is answered.

**2. ⚑ ResourceQuota — DISCHARGED THINLY.** This shard recorded "ResourceQuota is named and
handed to **Chapter 8**." Chapter 8 §3 delivers the scope (a ceiling on a namespace in
aggregate) and the LimitRange contrast, and **nothing else** — the two snapshots carrying
what a quota counts, the 403 rejection, and the requests-must-be-specified rule completed
but were never written to `sources/`. Not a contradiction; an under-delivery against a
bearing. See `[[resource-quota-and-limitrange]]`, which carries the full gap list.

## Chapter 8 addition — the namespace boundary acquires a consequence

Chapter 4 established that Nodes are not namespaced. Chapter 8 §3 is the first place that
costs anything:

> **You can quota a team. You cannot quota a machine.**

Related: `[[resource-quota-and-limitrange]]` · `[[cluster-scoped-resource]]` · `[[node-conditions]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cluster-scoped-resource.md ===

## Chapter 8 — the theme's first operational consequence

This theme originates at Chapter 4 §3 as a structural fact. Chapter 8 §3 is where it first
*costs* something:

> "There is no ResourceQuota that limits how many Nodes a group may consume, because a Node
> is not in a namespace and a quota is a statement about a namespace."
>
> **You can quota a team. You cannot quota a machine.**

Both halves of "stop people using too much" sit on opposite sides of a boundary the reader
already has. ResourceQuota and LimitRange are namespaced; the Nodes of §4 are not.

## The Chapter 12 dependency, stated by Chapter 8 in advance

Chapter 8 §3 flags this explicitly: *"Chapter 12 is going to **derive** the RBAC four-way
matrix from exactly this boundary rather than asking you to memorise four combinations."*

That makes this shard load-bearing for Ch 12's design, not just its content. If Chapter 8
§3's hinge is cut or weakened in a later revision, Chapter 12 loses its derivation and
falls back to four memorised combinations.

Chapter 8 also re-states the source wording verbatim: namespace-based scoping is applicable
"only for namespaced objects — Deployments, Services and so on — and not for cluster-wide
objects such as StorageClass, Nodes and PersistentVolumes."

⚑ Minor: Chapter 8 §3 writes `StorageClass` singular while its own Exam Alert row and
Chapter 4 §3 both use the plural. Reconcile to the plural.

Related: `[[resource-quota-and-limitrange]]` · `[[namespace]]` · `[[node-lifecycle]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/control-loop.md ===

## Chapter 8 addition — the node controller is the sixth instance

Chapter 8 §4 names the pattern outright rather than leaving it to be noticed:

> The node controller "observes (heartbeats), it compares against what it expects, and it
> acts (condition update, then eviction). That is the control-loop pattern exactly…
> **The node controller is a control loop.** You met the pattern in Chapter 3, and you have
> seen five instances of it since. This is the sixth."

Chapter 8 §8 then uses that identification as half its synthesis argument — that every
administrative act in the chapter is a write through one door, reconciled by a controller
the reader already knows.

⚑ **B3 accounting flag.** This shard records the control-loop retrieval chain as
Ch 3 → 4 → 6 → 11 → 15 → 17. **Chapter 8 is not on that list and bears the theme anyway**,
explicitly and by name. Either the chain is stale or Chapter 8 has done unbudgeted
retrieval work on the book's structural spine. Worth settling before Chapter 11, which
ch-03's manifest flagged as **still unbeared**.

Related: `[[node-controller]]` · `[[node-conditions]]` · `[[api-server-hub]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/built-in-node-condition-taints.md ===

## Chapter 8 — the `unschedulable` promise, discharged as far as sources allow

This shard's `unschedulable` row ends "Chapter 8's opening move." Chapter 8 §1 and §4
deliver the command: **`kubectl cordon $NODENAME`**, which "prevents the scheduler from
placing new Pods onto that Node, without affecting the existing Pods on the Node."

## ⚑ RULE 6 — DO NOT CLOSE THE LOOP. The link is not sourced.

The obvious completion — *"`kubectl cordon` applies the `node.kubernetes.io/unschedulable`
taint"* — is **not stated by any cached source**, and Chapter 8 was revised specifically to
stop asserting it. Three facts are separately sourced and no cached sentence joins them:

1. `cordon` prevents the scheduler placing new Pods on the node [`nodes`]
2. `node.kubernetes.io/unschedulable` exists as a built-in taint with `NoSchedule` [`daemonset`, `taints-depth`]
3. the scheduler checks taints when it makes scheduling decisions [`taints-depth`]

`taints-tolerations-depth` pulls the other way on the mechanism — "The taint will be added
to a node when initializing the node to avoid race condition" — and it attributes automatic
taint creation to node **conditions**, which unschedulability is not.

The closer, *"cordoned nodes are marked Unschedulable in their spec,"* sits unwritten in
`research-manifest.md`. Until it lands: **do not assert the link, and do not assert
`.spec.unschedulable`.** Chapter 8's §8 paragraph, Practice Q10 and Bearings #2 item 1 were
all narrowed for exactly this reason.

## ✅ DaemonSet toleration — confirmed from the Chapter 8 side

"Pods that are part of a DaemonSet tolerate being run on an unschedulable Node," because
"the DaemonSet controller automatically adds a `node.kubernetes.io/unschedulable` toleration
with a `NoSchedule` effect to DaemonSet Pods." Chapter 6's one-Pod-per-eligible-node and
Chapter 7's built-in condition tolerations turn out to be the same fact.

Related: `[[node-lifecycle]]` · `[[taint]]` · `[[node-controller]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/taint.md ===

## Chapter 8 note — the scheduler-checks-taints fact, reused

Chapter 8 §8 reuses this shard's sourced fact — "it checks taints when it makes scheduling
decisions" — to argue that `kubectl cordon` is not a special-purpose maintenance channel
but an ordinary write that the scheduler subsequently observes.

⚑ **The argument is sound; the causal chain is not fully sourced.** See
`[[built-in-node-condition-taints]]` § Rule 6. Chapter 8 asserts only what is cached: that
`cordon` is a write through the API server and that the scheduler subsequently places
nothing on the marked node. **It does not assert that cordon writes the taint.** Preserve
that restraint on replay.

## Chapter 8 reference-set note — no fetch required

Two Chapter 8 answer keys (Soundings A5, Bearings #2 item 1) depend on `NoSchedule`
governing **new placements only**. That semantics lives in
`k8s-docs-taints-tolerations-2026-08-23`, which is **on disk** but is *not* in Chapter 8's
referenced-snapshot set — the depth cut (`…-depth-2026-08-24`) deliberately does not restate
effect semantics, and says so in its own header. **The reference list is what is wrong, not
the prose.** Adding the base snapshot to Chapter 8's set closes both items with no fetch.
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/serviceaccount.md ===

## Chapter 8 addition — the ServiceAccount as an identity a *tool* assumes

Chapter 5 §6 established the ServiceAccount as a Pod's identity. Chapter 8 §1 and §2 add the
two places that identity is *acted on* from the reader's side of the keyboard.

**At the gate (§2):** "Pods connect by leveraging a ServiceAccount: Kubernetes automatically
injects the public root certificate and a valid **bearer token** into the Pod when it is
instantiated." That is how a Pod authenticates at gate one — a different route from a
node's, which uses a client certificate.

**At the terminal (§1):** `kubectl` running inside a Pod detects the ServiceAccount token
file, **authenticates as the ServiceAccount**, and "acts against the namespace of the
ServiceAccount, unless `--namespace` is given."

> The practical consequence, and the reason this belongs in a study guide: a debugging shell
> inside a cluster is **not you**. An empty `kubectl get pods` that you were certain should
> have returned something is usually this.

⚑ Chapter 8 stops short of asserting that the injected bearer token and the token at
`/var/run/secrets/kubernetes.io/serviceaccount/token` are the same artefact. Two snapshots,
neither stating the identity. Do not tighten.

⚑ `bearer token` is used as a term of art and **is not defined anywhere in the book.**
Glossary gap row filed.

Related: `[[kubeconfig]]` · `[[api-access-gates]]` · `[[namespace]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/cri.md ===

## Chapter 8 addition — the boundary's first operational consequence

Chapter 2 taught the CRI as an interface question: the line between Kubernetes and the thing
that actually starts containers. Chapter 8 §5 is the first time in the book that line has a
cost attached.

> "A container runtime — containerd or CRI-O — **must be installed on every node**, and
> `kubectl` is the command-line tool for managing any cluster."

Chapter 8's reading: `kubeadm` will build a control plane and join nodes, "and a container
runtime must already be present on those nodes, because a container runtime is on the other
side of a line the project deliberately drew."

Six chapters after it was taught as architecture, it becomes a checklist item.

**The retrieval item built on it** (Bearings #2 item 4, six chapters back — one of the two
items satisfying B3's ≥4-back floor for Chapter 8) turns on rejecting **"Docker"** as the
answer. That distractor works precisely because Chapter 2's point was that Kubernetes
reaches *a* runtime through the CRI.

⚑ Chapter 8 does **not** claim kubeadm declines to install a runtime — draft-v1 did, and it
was removed as an unsourced negative assertion about a tool's scope. The requirement is
sourced; the tool's abstention is not.

Related: `[[container-runtime]]` · `[[cluster-bootstrap-tooling]]` · `[[node-components]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/resource-request.md ===

## Chapter 8 addition — a third actor, and a request you did not write

This shard already reconciles two framings under an explicit do-not-overwrite instruction:
Chapter 5's runtime rule ("a request is a floor, not a ceiling") and Chapter 7's scheduler
accounting ("a request is a booking"). **Both stand untouched.**

Chapter 8 §3 adds a third, non-conflicting: a request can arrive **defaulted by a
LimitRange** rather than written by the author.

> 🪝 "A LimitRange that supplies a default request changes what your manifest means without
> changing your manifest. The Pod you get is not the Pod you wrote, and
> `kubectl get pod <name> -o yaml` is where you find out."

The consequence is a scheduling one, and it closes the loop back to Chapter 5 and Chapter 7:
a Pod that previously declared nothing now **books capacity against Allocatable that it did
not book before**, so nodes that would have accepted it may now fail to fit it.

⚑ Chapter 8's Practice Q7 attributes "requests are the number the scheduler filters on" to
Chapter 5. That attribution is **correct at book level** — `chapter-05:872` states it,
sourced to `k8s-docs-resource-management-2026-08-23`, which is **on disk** — but that
snapshot is not in Chapter 8's referenced set. The chapter's own AUTHOR-REVIEW calls this
unverifiable; it is verifiable, and adding the snapshot to the reference list closes it with
no fetch.

Related: `[[resource-quota-and-limitrange]]` · `[[resource-limit]]` · `[[node-conditions]]`
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D1.2 — Kubernetes Fundamentals › Administration | Chapter 8 | deep (1 sub-objective partial) | — |

<!--
D1.2 notes (Stage 14, ch-08, 2026-08-24):

- Competency name is "Administration", NOT "Cluster Administration". Source:
  cncf-kcna-curriculum-pdf-2026-08-23.md:13 — "44% - Kubernetes Fundamentals:
  Kubernetes Core Concepts; Administration; Scheduling; Containerization".
  Chapters 2, 5 and 7 each use the curriculum's competency name verbatim; the
  Ch 8 metadata line should be conformed.

- ALL THREE of the chapter's BLOCKING metadata claims are closable against that
  one snapshot, which is on disk. Lines 13-16 enumerate exactly FOUR domains
  summing to 100% (44 + 28 + 16 + 12), so the domain COUNT is sourceable too --
  the integration report's recommendation to drop the "four" claim rather than
  source it is unnecessary. See concepts/domain-weights-44-28-16-12.md (ch-01),
  which already carries this table.

- CNCF publishes DOMAIN weights only, not COMPETENCY weights. The chapter's ~5%
  remains an authored allocation, disclosed in front matter. Unchanged from Ch 7.

- ONE SUB-OBJECTIVE SHIPS PARTIAL: D1.2-08 (auditing). The chapter names it,
  places it correctly alongside the three access-control gates, and states its
  function -- deliberately, per outline Open Question #4 option (b). The closing
  fetch completed but was never written to sources/. Record as PARTIAL, not deep.

- All eight sections carry objectives: ["D1.2"]. Chapter 8 is the sole owner.

- DOMAIN D1 IS NOW COMPLETE at 44%: D1.1 (Ch 3), D1.2 (Ch 8), D1.3 (Ch 7),
  D1.4 (Ch 2 -- STILL UNRECORDED, because Ch 2's Stage 14 never ran; flagged by
  ch-03 and unresolved). Enough rows exist for a first domain-level coverage
  audit; worth running before Part III.

- ADJACENT-BUT-UNOWNED, second chapter running: PriorityClass and preemption
  (ch-07 G4). Ch 8 declined them on tier grounds in its §3 scope guard, which is
  defensible -- but no chapter will now define them. Glossary row is the floor;
  author decision still pending.
-->
=== END APPEND ===

=== APPEND C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===

| Tested topic | Original chapter | Retested in |
|---|---|---|
| namespaces divided via resource quota | ch 4 §3 | ch 8 — ☆ Bearings #1 item 5 |
| `node.kubernetes.io/unschedulable` and `NoSchedule` semantics | ch 7 §4 | ch 8 — ☆ Bearings #2 item 1 |
| the CRI and the container-runtime boundary | ch 2 §4 | ch 8 — ☆ Bearings #2 item 4 |
| Nodes are cluster-scoped, so no quota can cap them | ch 4 §3 | ch 8 — Practice Q6 |
| requests are the number the scheduler filters on | ch 5 §8 | ch 8 — Practice Q7 |
| the control loop — observe, compare, act | ch 3 §6 | ch 8 — Practice Q11 |

<!--
Chapter 8 retrieval accounting (Stage 14, 2026-08-24):

- 6 tagged items / 33 graded items (15 Bearings + 18 Practice) = 18.2%.
  arc-outline.md:414 sets Ch 8 at 20%. BELOW FLOOR.

- The chapter's own accounting note says "6 of 34 = 17.6%". The denominator is
  33, not 34. Conclusion unchanged; the rate is 18.2%.

- CHEAPEST FIX, needs no fetch and no new question: tag Bearings #2 item 5
  (the two heartbeat forms + which namespace holds the Leases) as
  [retrieval: ch4]. That yields 7/33 = 21.2%, inside the 20-25% band, AND
  discharges arc-outline.md:414's SECOND mandatory anchor ("node conditions"),
  which is the Ch 4 kube-node-lease handoff. Defensible on the merits: the
  item's second half is answerable only from Ch 4 §3's four-namespace table,
  and the answer key already credits Chapter 4 explicitly.
  Preferable to the chapter's own two proposals -- one depends on a snapshot
  that has not landed, the other adds a question.

- BOTH >=4-BACK FLOOR ITEMS SATISFIED. arc-outline.md:414 requires "Ch 2 CRI or
  Ch 3 control loop"; Chapter 8 delivers BOTH -- Bearings #2 item 4 (ch 2, six
  chapters back) and Practice Q11 (ch 3, five back). Chapter 8 is the first
  chapter at which B3's >=4-back floor binds.

- All six tags verified accurate against shipped chapter text on disk. No tag
  points at a chapter that does not cover the material.

- Practice Q7's Ch 5 attribution is sound at book level (chapter-05:872,
  sourced to k8s-docs-resource-management-2026-08-23, on disk) even though the
  chapter's own AUTHOR-REVIEW calls it unverifiable -- that snapshot is simply
  missing from Ch 8's referenced set.

- UNBUDGETED: Chapter 8 §4/§8 bears the control-loop cross-cutting theme by
  name, but ch-03 records that theme's chain as Ch 3->4->6->11->15->17, which
  does not include Ch 8. Settle before Ch 11 (still unbeared per ch-03).

- STANDING GAP, THIRD CHAPTER RUNNING: book-outline/retrieval-architecture.md
  is NOT the B3 document -- it is a permission-failure message plus a prose
  summary. The per-chapter schedule was never written to disk. This log remains
  the only durable record of what has actually been retrieved.
-->
=== END APPEND ===
```

---

Three things worth your attention before you act on any of this:

**Nothing above reaches disk on its own.** I re-verified rather than inheriting: `stages.py:225-234` gives stage 14 exactly one output (`kb-manifest.md`), no Python file in `certcomp` parses `=== WRITE` or `=== APPEND`, and `Book-KCNA/knowledge-base/` does not exist. Eight chapters' knowledge base now sits unapplied across eight manifests. Replay must run ch-01 → ch-08 in order, and three shards must be **appended, not overwritten** — `api-server-hub.md`, `resource-request.md`, and `built-in-node-condition-taints.md` each carry a prior author decision that a naïve overwrite would delete.

**Three of my checks changed the integration report's conclusions.** The metadata BLOCKING item closes fully rather than partially — `cncf-kcna-curriculum-pdf-2026-08-23.md:13-16` enumerates four domains summing to 100%, so the "four domains" count is sourceable and needn't be dropped; the same line settles the competency name as **"Administration"**, not "Cluster Administration". The British-spelling count is **32, not 26**: the `harbour`/`harbourmaster` family adds six, and Chapter 4 already coined `harbormaster` — so §2's Extended Analogy renames its own central character against the chapter that introduced it, three sections from the locked `🏆 Safe Harbor` marker. That gates what would otherwise be a strong exemplar nomination.

**Two of the chapter's own AUTHOR-REVIEW comments overstate what's needed.** Both `k8s-docs-taints-tolerations-2026-08-23` and `k8s-docs-resource-management-2026-08-23` are on disk; the Soundings A5, Bearings #2 item 1, and Practice Q7 flags close with a reference-list addition, no fetch. The ten genuinely-missing snapshots I confirmed absent — the BLOCKING gaps at §2, §3, and the Capacity regression at §4 are real and still need the research-manifest writer script run.