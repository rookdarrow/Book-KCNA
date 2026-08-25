I have everything I need. All three orphans, both canon conflicts, and a third conflict the integration report missed are verified against shipped text.

# Knowledge-Base Manifest — KCNA Chapter 10

**Stage 14 · Book:** Kubernetes and Cloud Native Associate · **Date:** 2026-08-25

> **Greenfield notice.** `Book-KCNA/knowledge-base/` **does not exist**, and no sibling book in the workspace has one either — this is the first knowledge base in the project. Chapters 1–9 shipped without Stage 14 running. Every file below is therefore *created*, not appended to, and covers **Chapter 10 only**. I have not backfilled Ch 1–9; inventing coverage/retrieval rows I did not verify would be canon drift of exactly the kind Rule 6 forbids. Each file carries an explicit `BACKFILL REQUIRED` block naming what is missing.

---

## Glossary entries added to `../Book-KCNA/knowledge-base/glossary.md`

Four terms. Three are the orphans the integration report identified; I verified all three against the B7 acronym register (74 entries) and confirmed none has a row. The fourth (CIDR) is assigned to the glossary by the ledger itself.

| Term | Definition (from chapter) | First appearance |
|---|---|---|
| **CIDR (Classless Inter-Domain Routing)** | "a way of writing a range of IP addresses as an address plus a prefix length: `172.17.0.0/16` means 'the addresses whose first sixteen bits are those of 172.17.0.0.' An `except` list carves ranges back out of the block" | Chapter 10 §6 |
| **OSI** | ⚠ **No chapter definition exists.** Chapter uses the bare acronym four times, including Practice Question 1's stem. B7 expands it only *inside* the `L4 / L7` row: "OSI Layer 4 / Layer 7" | Chapter 10 §1 |
| **SNI** | ⚠ **No chapter expansion exists.** Chapter supplies function only: "an earlier tell in the SNI field of the TLS handshake — traffic for several hostnames can be multiplexed on a single port that way, where the proxy terminating TLS supports SNI" | Chapter 10 🧭 Soundings A1 |
| **reverse proxy** | ⚠ **No chapter definition exists.** Used as assumed vocabulary: "for a Gateway implemented as a reverse proxy… the reverse proxy receives the HTTP request and uses the `Host:` header to match a configuration" | **Chapter 9** 🧭 Soundings A8 (*not* Ch 10 — corrects the integration report) |

**Three of the four cannot be resolved by a glossary entry alone.** B7's orphan doctrine is explicit: *"a term used in question text or an answer key may not be glossary-only, because a reader who meets it there has no place to look it up mid-question."* All three reach graded material — OSI in a Practice stem, SNI in a Soundings answer, reverse proxy in a Soundings answer in *two* chapters. The glossary rows below are the lookup path; the in-text fixes are Stage 11/12 work and are recorded as such.

Per Rule 5 I have not paraphrased. Where the chapter supplies no definition, the entry says so rather than inventing one.

---

## Concept shards added at `../Book-KCNA/knowledge-base/concepts/{slug}.md`

Seven concepts clear the ≥200-word threshold. All seven are **created** (directory is greenfield), so no shard is being overwritten and Rule 6's contradiction check has no prior shard to run against — but see **Contradictions** below, where Chapter 10 conflicts with *shipped chapter text*, which is the same hazard by another route.

- `concepts/ingress.md` — created
- `concepts/ingress-controller.md` — created (includes IngressClass and the default-class mechanism)
- `concepts/ingress-freeze.md` — created (frozen ≠ deprecated)
- `concepts/gateway-api.md` — created
- `concepts/network-policy.md` — created (§6 + §7; **sole definition home** — Ch 12 §9 refers, never redefines)
- `concepts/absent-component-pattern.md` — created — **highest-value shard in this batch**, see below
- `concepts/layer-boundary-and-traffic-direction.md` — created (L4/L7, north-south/east-west, edge router)

**Why `absent-component-pattern.md` matters more than the rest:** B6 and B3 both require Ch 13 §7 and Ch 17 §7 to retrieve this pattern ***by name*** rather than re-derive it. There are currently **four competing surface forms** for that name, and the one B7 designates is the only one that appears nowhere in shipped text. Without a shard pinning the headword, those two chapters will coin a fifth. Detailed under **Canonical-form defect**, below.

Not shard-worthy this chapter (under threshold, adequately carried by the glossary or a parent shard): default backend, `pathType`, TLS termination, the three NetworkPolicy identifiers, GRPCRoute.

---

## Voice-exemplar candidates nominated

**Nominations only — not written to `voice-exemplars.md`.** Per Rule 1, the author promotes to LOCKED. The current anchor is CAPM Ch 1; these are offered as KCNA-side candidates.

| Function | Excerpt | Recommendation |
|---|---|---|
| **Ethical guardrail — refusing a number** | "What this book will not tell you is how often any of them appears on the exam. The published curriculum gives four domain weights and nothing finer — no question counts, no per-competency split, nothing that would let anyone honestly attach a number to a single trap. Inventing one would be worse than saying nothing." | **Strong candidate.** The catalog has no exemplar for *declining* to supply a figure the reader wants. Skill Part 14 forbids fabricated statistics but shows no model of the refusal in voice. This is that model, and it stays warm rather than defensive. |
| **Zenith / synthesis** | "An object is a record of intent. Intent does not act. Something has to be watching, and willing, and *present*. Every object in this book works this way… These four are simply the cases where the watcher is missing, and the appearance falls away." | **Strong candidate.** Skill §18.9 names Zenith moments as the illustration crux, but there is no prose exemplar of one. Note the restraint: the payoff sentence is eight words and carries no nautical figure at all. |
| **Provenance separation** | "That is not a documented claim; the source states the plugin dependency and the no-effect consequence and stops there. The characterisation of the failure as *silent*… is this book's reasoning… We think it is sound, it is the most valuable thing in this chapter, and it is still an inference." | **Strong candidate.** Directly serves the "Order/Truth Balance" and "Uncertainty Signals" patterns in skill Part 11, which currently have no canonical passage. Distinctive move: the book argues *for* its own claim while conceding its status. |
| **Desirable difficulty — normalizing struggle** | "If you spent a while looking for the deny rule before accepting there isn't one, that is the correct experience of this question. Every firewall you have configured had one. The absence is genuinely strange…" | **Moderate.** Clean instance of skill Part 10B, and it names the reader's prior experience as the *cause* of the difficulty rather than a deficiency. Slightly context-bound. |
| **Dead Reckoning** | §7's out-of-scope block: "The source states this list as current 'as of' whichever release you happen to be reading — a version-templated claim with no fixed version behind it, so there is no release number to pin here without asserting more than the documentation does." | **Moderate.** Good facts-only register, but the passage is doing version-caveat work more than exemplifying Dead Reckoning as a mode. |
| **Cross-chapter debt collection** | "Chapter 3 gave you the sentence… and told you that you would meet it four more times. This is where that debt comes due in full." | **Weak — do not promote.** Effective in place, but it only reads as voice with seven chapters of setup behind it. An exemplar needs to work excerpted. |

---

## Objective coverage log → `../Book-KCNA/knowledge-base/objective-coverage.md`

Objective IDs are the **Lodestar convention** from B1 (`D2.1`, `D2.2`, …) — CNCF publishes named competencies but does not number them and publishes no sub-competency weights.

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D2.1 — Networking | Chapter 9 | deep (completed Ch 10) | — |
| D2.2 — Security | Chapter 10 (boundary only) | partial — NetworkPolicy taught here per B2; full coverage lands Ch 12 | — |

**Concept-level audit, D2.1 concepts assigned to Ch 10 by B1: 7 of 7 covered.** Ingress · Ingress controller · Ingress capabilities · Ingress-is-frozen · Gateway API · Edge router · NetworkPolicy. No gaps.

B2's identified research gap for this chapter (**G25 — Gateway API detail**) is closed: the chapter carries the three role-mapped resources, the role split, cardinality, the request flow, the four design principles, and the CRD-installation fact, all source-tagged to `k8s-docs-gateway-api-depth-2026-08-24`.

---

## Retrieval-practice ledger → `../Book-KCNA/knowledge-base/retrieval-log.md`

| Tested topic | Original chapter | Retested in |
|---|---|---|
| Service-type ladder; HTTP vs non-HTTP exposure | ch 9 §3 | ch 10 — Bearings #1 Q1, Practice Q2 |
| The absent-component rule, stated back | ch 3 §4 | ch 10 — Bearings #1 Q5, Practice Q18 |
| Control loop / the controller pattern | ch 3 §6 | ch 10 — Practice Q7 |
| Labels and selectors as the universal join | ch 4 §5 | ch 10 — Bearings #3 Q1, Practice Q16 |

**Spacing compliance.** 7 tagged items across 33 graded items (15 Bearings + 18 Practice) = **21.2%**, inside B3's 20–25% band for Ch 10. B3's floor — *"from Ch 8 on, at least one item must come from ≥4 chapters back"* — is met with room: the Ch 3 items are seven chapters back. All 7 verified against shipped target text; none tests material the target chapter does not carry.

**Forward obligations Ch 10 creates** (recorded so later stages do not re-derive):

| Topic Ch 10 owns | Must be retrieved in | How |
|---|---|---|
| Absent-component pattern | Ch 13 §7, Ch 17 §7 | **by name** — see canonical-form defect |
| NetworkPolicy | Ch 12 §9 | cross-bear only; Ch 12 may **not** redefine |
| Additive/no-deny semantics | Ch 12 §9 | named retrieval — Ch 12 builds the RBAC argument on it |
| Labels and selectors | Ch 16 §4 | continues the Ch 4 → 6 → 7 → 9 → 10 chain |

**One taught-but-unassessed topic: north-south / east-west.** Taught in §1, given a 🪢 Mnemonic, and carried into the Chapter Summary — but it appears in **zero of the 41 questions**. The chapter's own AUTHOR-REVIEW comment at §1 kept the mnemonic conditionally, on the assumption the question pass would add an item; it did not. Logged here as an open retrieval gap rather than silently absorbed.

---

## Contradictions with earlier canon — flagged, not resolved

Rule 6 requires these be raised loudly rather than smoothed over. **Two of the three are defects in shipped Chapter 9, not in Chapter 10.**

### ⚑ A. The pluggable-interface count — Ch 9 is the outlier, not Ch 10

The integration report framed this as Ch 10 vs Ch 9 and left it as an author's toss-up. It isn't a toss-up. **Chapter 2 settles it, and Chapter 9 disagrees with both its neighbours.**

- **Ch 2 line 914 (shipped):** "This is the **first** of four times you will see this move. **Storage** does it. **Networking** does it. **The API itself** does it." — Ch 2 enumerates CSI, CNI, and **CRDs**. CRDs are in.
- **Ch 2 line 600 (shipped):** cross-bears to `Ch 6 §8 — CRDs and extending the API` as one of the four.
- **Ch 10 line 1866 (shipped):** reader holds three — CRI (Ch 2), CRDs (Ch 6), CNI (Ch 9). **Consistent with Ch 2.**
- **Ch 9 lines 1149 and 1650 (shipped):** CNI is "the **second** instance" / "**Second** of the four pluggable interfaces." **Inconsistent with both.** By Ch 9 the reader has met CRI at Ch 2 §4 and CRDs at Ch 6 §8, making CNI the third.

B7's canonical-forms row fixes the set as **CRI + CNI + CSI + CRDs** and notes Ch 2 §4 already points at that wording. **Recommendation: retrofit Ch 9 §8 (prose at line 1149 and the summary row at line 1650) from "second" to "third."** Do not weaken Ch 10 — it is the one that agrees with the contract and with Ch 2.

### ⚑ B. Canonical-form defect — the pattern has four names and B7 picked the one nobody uses

The pattern must be retrieved **by name** at Ch 13 §7 and Ch 17 §7. Four surface forms are live:

| Form | Where | Status |
|---|---|---|
| **"the absent-component pattern"** | Shipped **Ch 3 §4** — reader-facing ×4: a ⚓ Worth Securing header, a checkpoint bullet, answer key Q14, and the Ch 3 summary table | **The shipped name.** Recommend this as headword. |
| "an object without its component does nothing" | Shipped Ch 3 §4 and Ch 10 ×9 | The **rule sentence** — keep, but it is a sentence, not a name |
| "The object exists; nothing happens without the component" | **B7 ledger only** | Appears in **no shipped chapter**. |
| "Nothing Happens Without a Controller" | Ch 10 §8 heading | Section title, not a term |

Note the ownership inversion: B7 assigns the *named* pattern to Ch 10 §3, but **Ch 3 §4 is where the name is actually coined**, and Ch 10 never uses "absent-component pattern" in reader-facing prose at all — only in front-matter metadata and an AUTHOR-REVIEW comment. **Recommendation: pin headword = "the absent-component pattern" (naming home Ch 3 §4), rule sentence = "an object without its component does nothing," instance ledger owned by Ch 10 §3.** The shard below encodes exactly this. Without it, Ch 13 and Ch 17 draft against B7 and coin a fifth form.

### ⚑ C. Shipped Ch 9 has eight sections; the B6 skeleton gives it seven

Confirmed and consequential — a drafting stage that trusts B6 over shipped text will emit broken Ch 9 pointers. The integration report's own line-754 fix (`Ch 9 §6` → `Ch 9 §7`) is correct under shipped text and *wrong* under the skeleton. B7's tie-break rule ("where the shipped text and the B6 skeleton disagree, the shipped text wins") governs. **Recommendation: amend the skeleton's Ch 9 block to the shipped eight-section form before Ch 11 drafts.** Outside Stage 14's write remit — flagged, not actioned.

### Not a contradiction (closing an open AUTHOR-REVIEW)

"One external address per Service" is untagged in Ch 10 but is **not** a research gap. Shipped **Ch 9 §3 line 540** states it — *"A LoadBalancer Service gives you one external address per Service"* — and line 546 frames the fifty-Service arithmetic as *"this book's own argument."* It is Ch 9-owned book reasoning, correctly inherited. No source tag is needed or possible.

---

```
=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/glossary.md ===
# Glossary — KCNA

Pipeline-maintained glossary. Format follows skill Part 16 (alphabetical, expansion
for every acronym, cross-reference to the chapter of introduction) so this file can be
promoted to the shipped back-of-book glossary without conversion.

**Provenance rule:** definitions are inherited verbatim from the chapter that introduces
the term. Where a chapter uses a term without defining it, the entry says so explicitly
rather than supplying an invented definition — the fix belongs in the chapter, not here.

> **BACKFILL REQUIRED.** Chapters 1–9 shipped before Stage 14 existed. Their terms are
> not in this file. The B7 term-ownership ledger
> (`.pipeline-state/book-outline/term-ownership.md`) is the authoritative inventory —
> 19 chapters of owned vocabulary, an ambient tier, a 74-entry acronym register, and
> nine routed orphans. A backfill pass should walk Ch 1–9 against it.
> Ch 10's entries below are complete.

---

## C

**CIDR (Classless Inter-Domain Routing)** — A way of writing a range of IP addresses as
an address plus a prefix length: `172.17.0.0/16` means "the addresses whose first sixteen
bits are those of 172.17.0.0." An `except` list carves ranges back out of the block.
(Chapter 10 §6)

*Ledger note: B7 assigns the gloss to Ch 10 §6 and the expansion to this glossary. Both
halves are now in place.*

---

## O

**OSI (Open Systems Interconnection)** — The seven-layer reference model whose layer
numbers this book uses to place network mechanisms. Layer 3 is the IP address level;
layer 4 is the port level; layer 7 is the application-protocol level, where the content
of an HTTP request becomes readable. (Chapter 10 §1)

> ⚠ **ENTRY IS PROVISIONAL — chapter fix required.** Chapter 10 uses the bare acronym
> four times (§1 line 156; §6 line 829; **Practice Question 1 stem, line 1249**; answer
> key line 1381) and **never expands it**. The B7 acronym register has no `OSI` row — it
> is expanded only inside the `L4 / L7` row ("OSI Layer 4 / Layer 7"). The definition
> above is supplied by this stage, not inherited from the chapter, because no chapter
> text exists to inherit.
>
> Two things must happen before this entry is anything but a stopgap:
> 1. Expand OSI on first use at Ch 10 §1 (the book's rule is absolute: *"Every acronym
>    is expanded on its first use in the book, without exception"*).
> 2. Add an `OSI` row to the B7 acronym register pointing at Ch 10 §1.
>
> B7 orphan doctrine: *"a term used in question text or an answer key may not be
> glossary-only."* OSI is in a Practice stem. This entry does not by itself satisfy the
> doctrine.

---

## R

**reverse proxy** — A server that terminates a client's connection at the network edge
and forwards the request onward to a backend on the client's behalf. In this book it is
what an Ingress controller and a Gateway implementation typically are: the thing that
reads the `Host:` header, applies match and filter rules, and forwards to one or more
backends. (First appears Chapter 9; used substantively Chapter 10 §5)

> ⚠ **ENTRY IS PROVISIONAL — no chapter defines this term.** Used as assumed vocabulary
> in Ch 9 (🧭 Soundings answer 8) and seven times in Ch 10, including the whole of §5's
> request flow. Not in the B7 ledger; not in B7's ambient-technical-vocabulary tier. The
> definition above is this stage's, assembled from how the chapters use the term.
>
> **Recommended resolution: add to B7's ambient tier** ("assumed of an adult professional
> reader… any chapter may use them bare"), which is where it plainly belongs alongside
> HTTP, TLS, and "load balancing (the general technique)." That is a B7 amendment and an
> author call; Stage 14 does not edit binding contracts. This entry is the interim
> lookup path.
>
> Note the first appearance is **Chapter 9**, not Chapter 10.

---

## S

**SNI (Server Name Indication)** — A field in the TLS handshake carrying the hostname the
client is trying to reach, sent before the encrypted session begins. Chapter 10 describes
its function: *"HTTPS carries an earlier tell in the SNI field of the TLS handshake —
traffic for several hostnames can be multiplexed on a single port that way, where the
proxy terminating TLS supports SNI"* `[source: k8s-docs-ingress-depth-2026-08-24]`.
(Chapter 10 🧭 Soundings answer 1)

> ⚠ **ENTRY IS PROVISIONAL — chapter supplies function, not expansion.** The functional
> gloss above is inherited verbatim. The expansion "Server Name Indication" is **not in
> any chapter** and is supplied by this stage. `SNI` appears **nowhere else in the book**
> (zero occurrences across Ch 1–9) and has no row in the 74-entry B7 acronym register.
>
> Required fixes:
> 1. Expand on first use at Ch 10 Soundings A1 — a two-word edit.
> 2. Add an `SNI` row to the B7 acronym register.
>
> B7 orphan doctrine applies: SNI sits in a Soundings answer, which is graded material,
> so glossary-only handling is not sufficient on its own.

---

*Stage 14 · Chapter 10 · 2026-08-25. Four entries, three of them provisional pending
chapter-side fixes recorded in the Ch 10 KB manifest.*
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/absent-component-pattern.md ===
# Concept — The absent-component pattern

**Naming home:** Ch 3 §4 (where the name is coined)
**Instance ledger + full treatment:** Ch 10 §3 and Ch 10 §8 (Zenith)
**B3 cross-cutting theme:** #3 — retrieved *by name* at Ch 13 §7 and Ch 17 §7
**Status:** canonical form contested — see Canonical form, below. Read that first.

---

## The rule

> **An object without its component does nothing.**

Verbatim from shipped Ch 3 §4. Reproduced verbatim in Ch 10 §3 and again in the Ch 10 §8
Zenith. Do not paraphrase this sentence in any chapter — it is retrieved as a quotation.

Ch 3 §4's fuller statement: *"An object can exist while nothing at all happens, if the
component that would act on it is absent. The object is real; it's stored; `kubectl get`
will show it to you. But an object is a description, and descriptions don't do anything
by themselves. Something has to be watching for it and willing to act."*

Ch 10 §8's compression, which is the form later chapters should reach for:

> An object is a record of intent. Intent does not act.

## Canonical form — ⚑ CONTESTED, resolve before Ch 13 drafts

Four surface forms are live in the corpus, and the one B7 designates appears in no
shipped chapter:

| Form | Where it lives | Verdict |
|---|---|---|
| **"the absent-component pattern"** | Shipped Ch 3 §4, reader-facing ×4 (⚓ Worth Securing header, checkpoint bullet, answer key Q14, Ch 3 summary table) | **Recommended headword** — it is what the book actually calls it |
| "an object without its component does nothing" | Shipped Ch 3 §4; Ch 10 ×9 | The **rule sentence**. Keep. Not a name. |
| "The object exists; nothing happens without the component" | B7 ledger only | **Zero occurrences in shipped text.** Do not adopt. |
| "Nothing Happens Without a Controller" | Ch 10 §8 heading | A section title, not a term |

**Ownership inversion to be aware of:** B7 assigns the *named* pattern to Ch 10 §3, but
Ch 3 §4 is where the name is coined, and Ch 10 never uses "absent-component pattern" in
reader-facing prose — only in front-matter metadata and an AUTHOR-REVIEW comment.

**Recommendation:** headword = *the absent-component pattern* (naming home Ch 3 §4);
rule sentence = *an object without its component does nothing*; instance ledger owned by
Ch 10 §3. Ch 13 §7 and Ch 17 §7 retrieve using the headword plus the rule sentence.
Without this pinned, those chapters coin a fifth form.

## The instances (the reader's own count, in encounter order)

| # | Instance | Where | Announces itself? |
|---|---|---|---|
| 1 | `type: LoadBalancer` Service on a cluster with no provider — external address stays `<pending>` | Ch 9 §3 | Yes — visible pending state |
| 2 | Service whose selector matches no Pods — real ClusterIP, real DNS record, empty EndpointSlice | Ch 9 §4 | Yes — traffic fails |
| 3 | Ingress with no Ingress controller | Ch 10 §3 | Yes — requests fail loudly |
| 4 | NetworkPolicy on a plugin that does not implement NetworkPolicy | Ch 10 §7 | **No — silent** |
| 5 | `kubectl top` with no metrics-server | Ch 13 §7 (planned) | Yes — command errors |
| 6 | VPA, which is an addon and not shipped by default | Ch 17 §7 (planned) | Yes |

## The asymmetry — the chapter's most valuable claim, and its provenance

Instances 1–3 announce themselves. Instance 4 does not: traffic flows exactly as before,
`kubectl get` and `kubectl describe` both show the object correctly parsed, and an
unenforced policy is observationally identical to a perfectly enforced policy against
traffic nobody is sending.

**Provenance, and keep this split when retrieving:** the plugin dependency and the
"no effect" consequence are **documented**
`[source: k8s-docs-network-policies-depth-2026-08-24]`. The characterisation of that
failure as *silent* and as harder to detect than a broken Ingress is **the book's own
inference**, and Ch 10 §7 labels it as one in the reader-facing text. Do not promote the
inference to a sourced claim downstream.

## Two counts, deliberately kept apart

Ch 10 runs two distinct tallies and a later chapter must not merge them:

- **Chapter 3's four** = the recurrences Ch 3 §4 lined up ahead of the reader
  (Ingress §3, NetworkPolicy §7, Ch 13, Ch 17). Ch 3's cross-bearing calls the Ingress
  case the *"first recurrence."*
- **The reader's own count** = instances personally watched fail, which started at two in
  Ch 9 and reaches four by Ch 10 §8.

Ch 10 §3 and §8 both reconcile these explicitly. Ch 3's "first recurrence" wording is
correct on Ch 3's count and looks wrong on the reader's; Ch 10 is the only place in the
book that squares them. **Do not "fix" either count in isolation.**

## The transferable question

> **What is watching this, and is it installed?**

Ch 10 §8 hands this to the reader as a tool for objects the book never covers. Ch 13 §7
and Ch 17 §7 should invoke it in these words.

## Constraints on later chapters

- Ch 13 §7 and Ch 17 §7: retrieve **by name**; do **not** re-derive the pattern.
- Any chapter adding a fifth instance: extend the table above, do not restate the rule.
- Never illustrate an instance as a *blocked* or *broken* object. Every genuine instance
  is a **correct** object with nothing wrong with it. Ch 10 Practice Q18 option D is
  built on exactly this distinction (a mismatched `pathType` is a manifest bug, not an
  instance) — an illustration implying breakage would invalidate the item.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/network-policy.md ===
# Concept — NetworkPolicy

**Sole definition home:** Ch 10 §6 (semantics) and Ch 10 §7 (limits)
**Objective:** D2.1 Networking primary; D2.2 Security boundary
**B2 rule:** taught **once**, in Networking. **Ch 12 §9 cross-bears in and must never redefine.**
**Sources:** `k8s-docs-network-policies-depth-2026-08-24`, `k8s-docs-network-model-2026-08-23`

---

## Scope

NetworkPolicies specify rules for traffic flow **at the IP address or port level — OSI
layer 3 or 4** — within the cluster and between Pods and the outside world. They are an
**application-centric construct** and apply to a connection with a **Pod on one or both
ends**; they are not relevant to other connections.

Not host isolation. The workload-to-host axis is a separate concern (Ch 2 §7 RuntimeClass;
Ch 12 §5).

## The three identifiers

1. **Pods** — with the exception that a Pod cannot block access to itself
2. **Namespaces**
3. **IP blocks (CIDR ranges)** — with the exception that traffic to and from the node
   where a Pod is running is always allowed

Pod- and namespace-based rules use selectors; IP-based rules use CIDR. `ipBlock` is **not
a selector** — CIDR ranges have no labels.

## The four load-bearing semantics

1. **Non-isolated by default, per direction.** A Pod is non-isolated for ingress and for
   egress until some policy both **selects it** and names that direction in `policyTypes`.
   No policy means no restriction. The two directions are declared **independently**.
2. **Additive, allow-only, order-independent.** Policies never conflict; the permitted set
   is the **union** of what all applicable policies allow. **There is no deny rule** — the
   API has no syntax for one. Removing access means removing the grant.
3. **Both ends must allow it.** The source's egress policy *and* the destination's ingress
   policy. Either refusing kills the connection.
4. **Default-deny by construction.** Empty `podSelector` (selects every Pod in the
   namespace) + both `policyTypes` + no rules. Isolation without permission *is* denial.

**`policyTypes` default:** if omitted, `Ingress` is always set, and `Egress` is set only
if the policy has egress rules. An omitted `policyTypes` is never "neither."

**Reply traffic** for allowed connections is implicitly allowed — the mechanism is
connection-aware, not packet-by-packet.

## Selector positions — one grammar, two jobs

The single most structurally interesting fact, planted at Ch 4 §5 (*"a NetworkPolicy
selects both its subject and its peers"*) and paid off here:

- **Top-level `spec.podSelector`** → chooses the **subject**: which Pods the policy governs
- **`podSelector` / `namespaceSelector` under `ingress.from` / `egress.to`** → chooses
  **peers**: who may connect

`namespaceSelector` + `podSelector` in **one** `from` entry = AND (particular Pods within
particular namespaces). As **two** entries = OR. One YAML hyphen changes the meaning.

**Consequence worth carrying:** relabelling a Pod out from under a top-level selector
makes it **less** restricted, not more — it reverts to non-isolated. Nothing announces this.

## What it cannot do (published out-of-scope list, snapshot 2026-08-24)

No forced common gateway · **no TLS** · no node-specific policies by Kubernetes identity ·
**no targeting Services by name** · no third-party "policy requests" · no default policies
across all namespaces/Pods · no advanced querying or reachability tooling · **no logging**
of blocked/accepted connections · **no explicit deny** · no preventing loopback or
resident-node traffic.

The source states this list as current "as of" a version-templated release with no fixed
version behind it. Ch 10 §7 flags it as a list that **shrinks over time** and tells the
reader to re-check. Preserve that caveat if the list is restated.

## Plugin dependency

NetworkPolicies are **implemented by the network plugin**. On a plugin that does not
implement NetworkPolicy the resource has **no effect**. See
[[absent-component-pattern]] — this is instance #4, and the only silent one.

Reasoning path (Ch 10 §7 offers this so readers derive rather than memorize): the CNI
plugin is what moves the packets, so layer-3/4 enforcement has nowhere else it could live.

## Constraints on later chapters

- **Ch 12 §9** — retrieves *additive, never deny* **by name** and builds the RBAC argument
  on the shared semantic ("the model has no subtraction operator"). Refers; never redefines.
- **Ch 17 §5** — service mesh owns the encryption gap NetworkPolicy explicitly cannot fill.
- Any figure must show exclusion as **absence of a grant**, never as a barrier, crossed-out
  arrow, or red X. Drawing denial contradicts the no-deny-rule Fixed Point.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/ingress.md ===
# Concept — Ingress (the object)

**Definition home:** Ch 10 §2 · **Objective:** D2.1 Networking
**Source:** `k8s-docs-ingress-depth-2026-08-24`
**Casing (B7):** `Ingress` capitalized for the object and the controller. Lowercase
`ingress` **only** for the NetworkPolicy traffic direction. Ch 10 carries both senses in
adjacent sections (§2 and §6) and each marks which it means.

---

## Definition

**Ingress exposes HTTP and HTTPS routes from outside the cluster to Services within the
cluster. Traffic routing is controlled by rules defined on the Ingress resource.**

Both halves matter. The backends are ordinary **Services** (ClusterIP is sufficient), and
the routing decisions live in the object, not in the controller's config file.

## The four capabilities

Externally-reachable URLs for Services · load balancing · SSL/TLS termination ·
name-based virtual hosting.

## The hard limit

**An Ingress does not expose arbitrary ports or protocols.** Anything other than HTTP and
HTTPS uses `Service.Type=NodePort` or `Service.Type=LoadBalancer`.

Frame this as **specialisation, not replacement**: Ingress takes over one class of traffic
and the Ch 9 Service ladder remains correct for everything else. This framing is what
makes §4's freeze survivable rather than alarming.

## The four shapes

| Shape | Splits on | Manifest tell |
|---|---|---|
| Single-Service (degenerate) | nothing — `defaultBackend` only | no `rules` |
| **Simple fanout** | the **HTTP URI / path** | several entries under `paths`, one `host` |
| **Name-based virtual hosting** | the **host** | several entries under `rules`, each with its own `host` |
| TLS | — | `spec.tls` + a `kubernetes.io/tls` Secret |

Fanout and virtual hosting put the same number of Services behind the same single address.
**They differ only in which part of the request the rule reads.** That discriminator is the
examinable fact, not either definition.

## TLS termination

Secured by a Secret containing a TLS private key and certificate. Single TLS port, **443**.
Keys must be named `tls.crt` and `tls.key`. The resource **assumes termination at the
ingress point — traffic to the Service and its Pods is in cleartext.** That cleartext leg
is a different problem with a different owner (Ch 17 §5). Retrieves `kubernetes.io/tls`
from Ch 4 §4.

## Path types

| `pathType` | Behaviour |
|---|---|
| `Exact` | Exact URL path match, case-sensitive |
| `Prefix` | Prefix match **split by `/`, element by element**, case-sensitive |
| `ImplementationSpecific` | Up to the IngressClass |

Required on every path; paths without an explicit `pathType` are not validated.

**`Prefix` is not a string prefix.** `/aaa/bb` does **not** match `/aaa/bbb` — the last
element `bb` is only a substring of `bbb`, not equal to it. This is the chapter's sharpest
manifest-level trap.

## Rules and default backend

Each HTTP rule has an **optional host** (absent = applies to all inbound HTTP through that
IP) and a list of paths, each with a backend naming a `service.name` plus a
`service.port.name` or `service.port.number`. **Both host and path must match.**

If no `.spec.rules` are specified, `.spec.defaultBackend` **must** be. Unmatched requests
route to the default backend, which is conventionally a controller config option rather
than a per-Ingress field.

## Do not separate from

[[ingress-controller]] — an Ingress alone has no effect. [[ingress-freeze]] — the API is
frozen, which constrains what may ever be added to anything on this page.

## Distinction Ch 9 flagged by name

DNS-based service discovery vs name-based virtual hosting sit on **opposite sides of the
connection**: DNS resolves a name to an address *before any traffic moves*; virtual hosting
sorts traffic that has *already arrived* at one address by reading the `Host` header back
out of the request. Ch 9 §7 warned about this conflation by name and pointed here.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/ingress-controller.md ===
# Concept — Ingress controller and IngressClass

**Definition home:** Ch 10 §3 · **Objective:** D2.1 Networking
**Sources:** `k8s-docs-ingress-depth-2026-08-24`, `k8s-docs-ingress-controllers-2026-08-24`

---

## The sentence

> **You must have an Ingress controller to satisfy an Ingress. Only creating an Ingress
> resource has no effect.**

Not "less effect." None. A well-formed Ingress on a controller-less cluster is accepted by
the API server, returned by `kubectl get`, and routes nothing.

## What it is

**Responsible for fulfilling the Ingress, usually with a load balancer, though it may also
configure your edge router or additional frontends.** Structurally this is Ch 3 §6's
control loop with the nouns filled in: desired state in an object, a controller watching,
external reality reconciled toward the description.

**`kubectl get ingress` returning the object is a fact about etcd storage. It is not
evidence that any component has ever read it.**

## IngressClass

Any number of controllers may run in one cluster; **ingress class** tells them apart. Each
Ingress should name its intended controller via **`ingressClassName`**, referencing an
**IngressClass** resource that carries configuration including the controller name.

**The default-class mechanism, stated precisely because the arithmetic is counterintuitive:**

- `ingressClassName` omitted **+ exactly one** IngressClass marked default → that class is
  applied. Marked via annotation `ingressclass.kubernetes.io/is-default-class: "true"`
  (the string).
- **More than one** marked default → an Ingress omitting `ingressClassName`
  **cannot be created at all**. Resolution: ensure at most one carries the marking.
- `ingressClassName` is **optional**, which is why the default mechanism exists.

More defaults is not more coverage — it is **less**. Two defaults do not give an unclassed
Ingress two chances; they remove the one chance it had, because the cluster cannot choose.
Ch 10 Bearings #1 Q4 is built on exactly this inversion.

**Contrast worth preserving:** a missing controller fails *silently at runtime*; a second
default class fails *loudly at apply time*. Same end state — an object that never reaches
a controller — but only one of them tells you.

## The portability caveat

> **Ideally, all Ingress controllers should fit the reference specification. In reality,
> the various Ingress controllers operate slightly differently.**

Documented twice, on both the Ingress and Ingress Controllers pages. The gap between a
reference specification and a particular implementation is where a config that worked for
a year breaks after a migration, and where the failure looks like a manifest bug.

**Boundary:** do not over-apply this caveat. `pathType: Prefix` semantics are pinned by
the specification with a worked example — reaching for "it depends on the controller"
there is the caveat used where it does not belong (Ch 10 Practice Q5 option D).

## See also

[[absent-component-pattern]] — this is instance #3 and the pattern's full-treatment site.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/ingress-freeze.md ===
# Concept — Frozen ≠ deprecated (the Ingress feature freeze)

**Definition home:** Ch 10 §4 · **Objective:** D2.1 Networking
**Sources:** `k8s-docs-ingress-depth-2026-08-24`, `k8s-docs-deprecation-policy-2026-08-24`
**B2 note:** *"one of the most precise facts in the whole curriculum"* — the reason
Ch 9/Ch 10 were split rather than merged.

---

## The statement, in full

> The Kubernetes project recommends using Gateway instead of Ingress. The Ingress API has
> been frozen. This means that:
> - The Ingress API is generally available, and is subject to the stability guarantees for
>   generally available APIs. The Kubernetes project has no plans to remove Ingress from
>   Kubernetes.
> - The Ingress API is no longer being developed, and will have no further changes or
>   updates made to it.

**Two bullets. Both load-bearing. Collapsing either produces a wrong answer.**

| Half dropped | Wrong belief produced | Wrong decision it drives |
|---|---|---|
| Stability half | "Ingress is deprecated" | Planning a migration you do not need |
| No-development half | "Ingress is fine, ignore the note" | Designing new systems on an API that stopped growing |

Both distractors are attractive, which is why this builds a clean four-option item. Ch 10
Bearings #2 Q1 and Q2 test the two directions separately, and Practice Q9 offers **both**
one-sided options — offering only one would teach the other.

## Why "deprecated" is a different word

- **Deprecation is a statement about future removal.** Kubernetes has a formal published
  deprecation policy; GA API versions **may be marked deprecated, but must not be removed
  within a major version**. It is the first step on a defined path to an exit.
- **A freeze is a statement about future development.** The thing is finished. It says
  **nothing about removal**, and a frozen API can be permanent.

Kubernetes said one and not the other, deliberately. The Ingress note's phrase "subject to
the stability guarantees for generally available APIs" links to that same deprecation policy.

## What "recommends" obliges — provenance split, preserve it

**The project's wording, unqualified:** *the Kubernetes project recommends using Gateway
instead of Ingress.* Not "for new work." Not "by some deadline." One sentence.

**The book's operational gloss, labelled as such in Ch 10 §4, in the Exam Alert, and again
in Bearings #2 A2:** don't panic about what you run; think hard before building new work
on an API that will never gain a feature.

⚠ **Any downstream chapter restating this must keep the split.** "Use Gateway for new work"
is a practitioner's reading, not the project's scope. On an exam the question is what the
project *said*, not what a sensible engineer does about it.

## Mnemonic (shipped)

> *Frozen things keep. They just don't grow.*

## Concrete cost of the freeze

Gateway API supports common cases — header-based matching, traffic weighting — *"that were
only possible in Ingress by using custom annotations."* That is the answer to "what does
the freeze cost me": whatever Ingress cannot do today, it never will.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/gateway-api.md ===
# Concept — Gateway API

**Definition home:** Ch 10 §5 · **Objective:** D2.1 Networking
**Closes B2 research gap G25** (Gateway API detail)
**Source:** `k8s-docs-gateway-api-depth-2026-08-24`
**Casing (B7):** *Gateway API* names the project and specification. Bare *Gateway* names
only the resource kind, and only in a sentence where GatewayClass or HTTPRoute is present.
**Never bare "Gateway" to mean the API.**

---

## Definition

**A family of API kinds providing dynamic infrastructure provisioning and advanced traffic
routing**, making network services available through an **extensible, role-oriented,
protocol-aware** configuration mechanism.

**`Role-oriented` is the load-bearing word.** Teach the three roles *first*; the resources
then read as a consequence rather than three arbitrary names to memorize.

## The three organisational roles

| Role | Concern |
|---|---|
| **Infrastructure Provider** | Infrastructure letting multiple isolated clusters serve multiple tenants — e.g. a cloud provider |
| **Cluster Operator** | Clusters; policies, network access, application permissions |
| **Application Developer** | An application in a cluster; application-level config and Service composition |

⚠ **Homonym, and B7 requires Ch 10 §5 to say so explicitly:** *cluster operator* here is a
**role name — a job a person or team holds — not the operator pattern** from Ch 6 §8. B7
canonical form: never use "operator" for a person except in this two-word Gateway API role
name. This is the only place in the book the two senses sit near each other.

## The resource model

Four stable API kinds; three carry the role split:

| Resource | Role | What it defines |
|---|---|---|
| **GatewayClass** | Infrastructure provider | A set of gateways with common configuration, managed by a controller implementing the class |
| **Gateway** | Cluster operator | An instance of traffic-handling infrastructure, such as a cloud load balancer |
| **HTTPRoute** | Application developer | HTTP-specific rules mapping traffic from a Gateway listener to backends, often Services |

`GRPCRoute` does the same for gRPC-specific rules.

## Cardinality — examinable, state it as such

**A Gateway is associated with exactly one GatewayClass. Many Routes may attach to one
Gateway.** A Gateway can filter which routes may attach to its `listeners`, forming a
bidirectional trust model.

The trap is the **Ingress-shaped** expectation: in Ingress one object carries the entry
point *and* every routing rule, so readers expect a Gateway to carry its routes. It does
not — routes attach from outside, and they belong to a different role.

The cardinality *encodes* the design: one class per Gateway because the provider defines
one kind of thing and the operator instantiates it; many Routes per Gateway because many
app teams share one entry point without asking each other's permission.

## Where the seam falls

The Gateway names its class, listeners, and which namespaces may attach routes — and says
nothing about `/login`. The HTTPRoute names its parent under **`parentRefs`**, its
hostnames, path matches, and `backendRefs` — and says nothing about ports, protocols, or
the load balancer underneath. **The seam between the manifests is the seam between the
roles.**

⚠ *Wording note:* "an HTTPRoute attaches to a Gateway via `parentRefs`" is the **book's
gloss**. The source attests `parentRefs` inside the example manifest, not in a prose
sentence of that form. Mechanism sourced; phrasing ours.

## Request flow (Gateway implemented as a reverse proxy)

1. Client prepares an HTTP request for `http://www.example.com`
2. Client's DNS resolver learns IP address(es) associated with the Gateway
3. Request reaches the Gateway IP; the reverse proxy uses the **`Host:` header** to match
   a configuration derived from the Gateway and attached HTTPRoute
4. *Optionally* — request header and/or path matching, per the HTTPRoute's match rules
5. *Optionally* — request modification, per its filter rules
6. Forward to one or more backends

**Step 3 is the discriminator and it is first.** The common wrong answer is *the path* —
recency, because §2 spends far longer on paths. Path matching is an **optional later**
step, after `Host:` has already selected the configuration.

Steps 2→3 are the DNS-vs-virtual-hosting distinction drawn in the specification's own hand.

## Design principles

**Role-oriented** (above) · **Portable** — defined as custom resources, many
implementations · **Expressive** — header-based matching and traffic weighting, only
possible in Ingress via custom annotations · **Extensible** — custom resources linkable at
various layers.

## Not built in

**Gateway API is not natively implemented by Kubernetes.** The specifications are **Custom
Resources**; you install the CRDs or follow your implementation's instructions. The docs
describe it as "an add-on containing API kinds" and the cluster addon list carries it.

Structurally notable: **the successor to a built-in API is an extension**
*[Ch 6 §8 — CRDs]*. Ch 10 §5 marks this 🔭 Closer Look — deeper than the exam requires.

## Relationship to Ingress

See [[ingress-freeze]]. Gateway API is not a rename of Ingress — one object with one owner
versus three objects with three owners. A reader who thinks it is a rename cannot say why
anyone bothered.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/concepts/layer-boundary-and-traffic-direction.md ===
# Concept — The L4/L7 boundary, traffic direction, and the edge router

**Definition home:** Ch 10 §1 · **Objective:** D2.1 Networking
**Sources:** `k8s-docs-network-model-2026-08-23`, `k8s-docs-ingress-depth-2026-08-24`,
`k8s-blog-gateway-api-north-south-east-west-2026-08-24`

---

## The layer boundary

**Everything in Ch 9 operates at layer 4:** a Service moves packets to an address and a
port and has no opinion about their contents. **Everything in Ch 10 §2–§5 operates at
layer 7:** it reads the request — host, path, sometimes headers — and decides on that basis.

> ★ Everything in Ch 9 moves **packets** to an address. Everything in §2–§5 reads
> **requests**. Which side of that boundary a mechanism sits on determines what it can
> know, and therefore what it can decide.

⚠ **Provenance.** The documentation sorts the same two groups **without OSI numbers**,
describing Ingress as protocol-aware HTTP/HTTPS routing using URIs, hostnames and paths,
against `type: LoadBalancer` as the simpler, less-configurable mechanism. The **only**
place it reaches for OSI numbers is **NetworkPolicy**, placed at the IP address or port
level — layer 3 or 4. Layer numbering for Services and Ingress is ordinary practitioner
vocabulary, not a documented label. Preserve this split if restated.

**The chapter is a round trip, not a climb.** §1–§5 ascend to where the request is
readable; **§6 descends again to 3/4**, and the descent is *why* NetworkPolicy's
out-of-scope list has the shape it has (no TLS, no hostname matching, no Service-name
targeting). A reader who loses the ladder experiences NetworkPolicy as an unrelated topic
that landed in the same chapter.

## North-south / east-west

**North-south** enters the cluster from outside. **East-west** moves between Pods inside it.

⚠ **Provenance.** The definitions are the **industry's**, not the project's. What the
Kubernetes project supplies is the **pairing**, in a Gateway API blog post rather than in
reference documentation, describing the API's initial focus as ingress "north-south"
traffic and service mesh as the "east-west" case.

Mapping: §1–§5 = north-south · §6–§7 = east-west.

Shipped mnemonic: *North-south goes through the wall; east-west stays inside it.*

⚠ **Open gap.** Taught, mnemonic'd, and summarised — but assessed in **zero of Ch 10's 41
questions**. The chapter's own AUTHOR-REVIEW kept the mnemonic conditionally on a question
being added; it was not. Either add one item or drop the mnemonic and keep the prose.
Logged in `retrieval-log.md`.

## Edge router

**A router that enforces the firewall policy for your cluster** — a cloud-provider-managed
gateway or a physical piece of hardware. Exists because **in most common deployments the
nodes in your cluster are not part of the public internet.**

Named at §1 purely so that §3's "usually with a load balancer, though it may also configure
your edge router" reads without stopping. That is its whole job in the book.

## Supporting terminology (same source block)

- **Node** — a worker machine, part of a cluster
- **Cluster network** — the links, logical or physical, carrying communication within a
  cluster per the Kubernetes networking model
- **Service** — identifies a set of Pods using label selectors; assumed to have a virtual
  IP **routable only within the cluster network**

That last clause is the whole problem in one line: Ch 9's addresses work inside the harbour
wall and mean nothing beyond it.

## Glossary dependency

**OSI is used bare here and never expanded** — see the ⚠ entry in `glossary.md`. Fixing it
requires a two-word edit at §1 plus a B7 acronym-register row. It reaches Practice Q1's stem.
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/objective-coverage.md ===
# Objective Coverage — KCNA

Objective IDs (`D1.1`, `D2.1`, …) are a **Lodestar convention** from B1 domain analysis.
CNCF publishes named competencies under each domain but does **not** number them and does
**not** publish sub-competency weights. Domain-level weights are the only level the
sources state.

**Domain weights (2025-11-24 four-domain blueprint):** D1 Kubernetes Fundamentals 44% ·
**D2 Container Orchestration 28%** · D3 Cloud Native Application Delivery 16% ·
D4 Cloud Native Architecture 12%.

> **BACKFILL REQUIRED.** Stage 14 did not run for Chapters 1–9. Rows below cover
> Chapter 10 and the D2.1 first-coverage fact verified against shipped Ch 9. Objectives
> D1.x, D2.3, D2.4, D3.x and D4.x are unlogged. Source of truth for the backfill:
> `.pipeline-state/book-outline/chapter-lineup.md` (per-chapter objective assignment) and
> `domain-analysis.md` (concept maps).

---

## Objective-level

| Objective | First covered in | Depth | Last reviewed |
|---|---|---|---|
| D2.1 — Networking | Chapter 9 | deep — completed Chapter 10 | — |
| D2.2 — Security | Chapter 10 (boundary only) | partial — NetworkPolicy only; full coverage lands Chapter 12 | — |

**D2.2 note.** B1 sequencing implication #6: *"NetworkPolicy sits in both D2.1 and D2.2.
Teach it once, in Networking, and cross-bear from the Security chapter."* Chapter 10 is
the sole definition home. Chapter 12 §9 refers and must not duplicate — duplication costs
words and produces two slightly divergent explanations.

## Concept-level — D2.1 concepts assigned to Chapter 10

All seven B1 concept-map entries for Chapter 10 are covered. **7 of 7. No gaps.**

| B1 concept | Covered in | Depth |
|---|---|---|
| Ingress | Ch 10 §2 | deep |
| Ingress controller | Ch 10 §3 | deep |
| Ingress capabilities (URLs, LB, TLS termination, virtual hosting, fanout) | Ch 10 §2 | deep |
| Ingress is frozen | Ch 10 §4 | deep |
| Gateway API | Ch 10 §5 | deep |
| Edge router | Ch 10 §1 | adequate — scaffolding for §3 |
| NetworkPolicy | Ch 10 §6–§7 | deep |

## Research gaps closed

| Gap | Description | Status |
|---|---|---|
| **G25** | Gateway API detail | **Closed by Ch 10 §5** — three role-mapped resources, role split, cardinality, request flow, four design principles, CRD-installation fact. All tagged `k8s-docs-gateway-api-depth-2026-08-24`. |

## Research gaps still open that touch this chapter

**No exam-logistics source is cached.** The corpus holds no snapshot of the Linux
Foundation KCNA exam/registration page — no question count, duration, passing score, or
question distribution. Chapter 10 correctly narrows two claims to what
`cncf-kcna-curriculum-pdf-2026-08-23` attests (four domain-level percentages and nothing
finer) and declines to attach frequency figures to traps. **Restoring any stronger claim
about what CNCF does or does not publish requires that snapshot.** Flagged in two
AUTHOR-REVIEW comments in the shipped chapter.

Standing B1 constraint: the book **must not** assert the widely-reported 60-question /
75%-pass figures as fact. Chapter 10 complies.

---

*Stage 14 · Chapter 10 · 2026-08-25.*
=== END WRITE ===

=== WRITE C:\dev\lodestar\certcomp\..\Book-KCNA/knowledge-base/retrieval-log.md ===
# Retrieval-Practice Ledger — KCNA

Which earlier-chapter topics have been retrieval-tested, and where. Targets are set by
B3 retrieval architecture: Ch 3 at 10%, Ch 4 at 15%, then **20–25% through Ch 18**, with a
**spacing floor from Ch 8 on — at least one item must come from ≥4 chapters back.**

Soundings are **excluded from the budget** by design: skill Part 11 requires them to be
answerable from prerequisites, which in this book means earlier chapters, so every
Soundings block is already a spaced retrieval event. Counting them would distort their
calibration purpose.

> **BACKFILL REQUIRED.** Stage 14 did not run for Chapters 1–9. Their `[retrieval: chN]`
> tags are in the shipped files and unlogged here. Chapter 10 is complete.

---

## Backward — earlier material tested in a later chapter

| Tested topic | Original chapter | Retested in |
|---|---|---|
| Service-type ladder; HTTP vs non-HTTP exposure | ch 9 §3 | ch 10 — Bearings #1 Q1; Practice Q2 |
| The absent-component rule, stated back in the reader's own words | ch 3 §4 | ch 10 — Bearings #1 Q5; Practice Q18 |
| Control loop / the controller pattern | ch 3 §6 | ch 10 — Practice Q7 |
| Labels and selectors as the universal join | ch 4 §5 | ch 10 — Bearings #3 Q1; Practice Q16 |

## Chapter 10 compliance

| Check | Target | Actual | Verdict |
|---|---|---|---|
| Retrieval share of graded items | 20–25% | **7 of 33 = 21.2%** (15 Bearings + 18 Practice) | ✅ |
| Spacing floor (≥4 chapters back) | ≥1 item | 4 items from ch 3 (**7 back**) | ✅ |
| Tagged items land on covered material | 7 of 7 | **7 of 7 verified against shipped target text** | ✅ |
| Question inventory | 8 Soundings, ≥10 Bearings across ≥2 checkpoints | 8 + 15 (3 × 5) + 18 = **41** | ✅ |

## Forward obligations Chapter 10 creates

| Topic Ch 10 owns | Must be retrieved in | How |
|---|---|---|
| The absent-component pattern | Ch 13 §7, Ch 17 §7 | **by name** — ⚑ headword contested, see `concepts/absent-component-pattern.md` before drafting |
| NetworkPolicy | Ch 12 §9 | cross-bear only; **may not redefine** (B2/B6 both bind this) |
| Additive / never-deny semantics | Ch 12 §9 | named retrieval — Ch 12's RBAC argument is built on the shared "no subtraction operator" semantic |
| Labels and selectors | Ch 16 §4 | continues the ch 4 → 6 → 7 → 9 → 10 chain |
| Service + NetworkPolicy as the mesh baseline | Ch 17 §5 | what a service mesh adds over both |
| CSI closing the pluggable-interface set | Ch 11 §5 | ⚑ see conflict below |

## Open gaps

**1. north-south / east-west is taught but never assessed.** Ch 10 §1 teaches the pair,
gives it a 🪢 Mnemonic, and carries it into the Chapter Summary — but it appears in **zero
of 41 questions**. The chapter's own AUTHOR-REVIEW kept the mnemonic conditionally on the
question pass adding an item; the pass did not. **Trigger has fired: add one question, or
drop the mnemonic and keep the prose.**

**2. ⚑ Ordinal collision waiting in Ch 11.** Ch 10's closing section tells the reader they
hold **three** of the four pluggable interfaces and that "Chapter 11 brings CSI… and that
closes the set." The B6 skeleton labels Ch 11 §5 *"**Third** of the four pluggable
interfaces."* If Ch 11 drafts to that label the reader hits "third" immediately after being
told they already had three. **Ch 11 §5 should say CSI *closes* the set** — or the
skeleton's ordinal annotations should be dropped, since they are set-order, not
encounter-order.

**3. ⚑ Shipped Ch 9 undercounts the same set.** Ch 9 §8 calls CNI *"the second instance"*
and *"Second of the four pluggable interfaces"*; shipped **Ch 2 line 914** enumerates the
four as CRI + storage + networking + **the API itself (CRDs)**, and Ch 10 counts three by
Ch 10. **Ch 9 is the outlier against both neighbours.** Recommended retrofit: Ch 9 §8
prose and summary row, "second" → "third." Full detail in the Ch 10 KB manifest.

---

*Stage 14 · Chapter 10 · 2026-08-25.*
=== END WRITE ===
```

---

## What I'd act on first

**The absent-component pattern's headword** (⚑ B), ahead of the Ch 9 numbering split the integration report prioritised. Both matter, but this one has a nearer deadline and no natural discovery point: B6 and B3 *require* Ch 13 §7 and Ch 17 §7 to retrieve the pattern by name, B7 designates a name that appears in no shipped chapter, and the name the book actually uses is coined in a chapter B7 doesn't credit with owning it. Ch 13 drafting against B7 will coin a fifth surface form, and nothing downstream will flag it — the pointer will resolve, the prose will read fine, and the reader will meet a differently-named version of a rule they were told to carry.

Two smaller notes: `retrieval-architecture.md` on disk contains a **blocked-write error message**, not the B3 artifact — the substantive content survives in prose inside it, but the file should be regenerated. And this stage produced no writes itself; the ten blocks above are for the orchestrator, per the stage contract.