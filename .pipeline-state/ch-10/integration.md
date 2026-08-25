Verification complete. All claims checked against shipped text; here is the artifact.

Per the pipeline contract in `CLAUDE.md` (stage output flows through stdout so the orchestrator captures it atomically), I'm emitting this rather than writing the file — also because `.integration.md.heartbeat` shows a stage run live at 02:11 and I don't want to race it.

```markdown
# Integration Check — KCNA Chapter 10

## Summary

- Terminology consistency: **pass** — 3 low-severity fixes, no conceptual drift
- Callbacks to earlier chapters: **13 claims verified / 13 correct**; cross-bearings **35 of 36 correct**
- Retrieval-practice accuracy: **pass** — 7 of 7 tagged questions land on covered material
- Glossary coverage: 24 concepts introduced, 21 defined in-chapter, **3 require glossary entries** (SNI, OSI, reverse proxy)
- Contradictions with earlier canon: **2 flagged** (one shipped-text conflict, one book-level numbering conflict)
- Ethical guardrails (skill Part 14): **pass** — exemplary on fabricated-statistics and subject-dignity

Section titles match the B6 skeleton **exactly, all eight**. Heading form (`## <difficulty> §N — Title`) and the `☀️` Zenith marking both follow the skeleton's Collision #3 and #4 recommendations. Attention-budget arithmetic checks (66 min before the split, 58 after, ~124 total).

---

## Terminology consistency

| Term | Canonical form (B7) | Occurrences in this chapter | Drift? |
|---|---|---|---|
| NetworkPolicy | `NetworkPolicy`, unspaced CamelCase | many | No — lowercase hits are `kubectl get networkpolicy` and a figure slug, both sanctioned |
| Ingress / ingress | Capital = object+controller; lowercase = policy direction | many, both senses | **No** — §6 opens with an explicit housekeeping paragraph marking the switch. This is the ledger's flagged Ch 10 risk and the chapter handles it deliberately |
| Ingress controller | Capitalized in book voice | many | No — every lowercase instance sits inside source-tagged quoted text (lines 416, 443). Faithful quotation; see fix 5 |
| IngressClass / `ingressClassName` | CamelCase object, camelCase field | 9 | No — lowercase hits are the `ingressclass.kubernetes.io/is-default-class` annotation key |
| cluster operator | Role name, two words, must be marked as *not* the operator pattern | 5 | No — §5 carries the required disambiguation note, and Bearings #2 A3 repeats it |
| operator (pattern) | Ch 6 §8 sense | 2 | No — both pointered to Ch 6 §8 |
| EndpointSlice | Unspaced CamelCase | 3 | No |
| Gateway API / Gateway | Full name for the API; bare `Gateway` only beside GatewayClass/HTTPRoute | many | No |
| GatewayClass · HTTPRoute · GRPCRoute | Exact CamelCase | many | No |
| kubectl / etcd | Always lowercase | many | No |
| cloud native | Never hyphenated | 0 | No — Ch 10 introduces **zero** new instances of the ⚑8 hyphenation defect affecting Ch 1–8 |
| Taking Your Bearings | Never "Bearings" alone in reader-facing text | 4 correct, 1 bare | **YES** — line 41 |
| service mesh | Name only + pointer until Ch 17 §5 | 6 | Borderline — line 166 names it without a pointer inside a sourced attribution; a pointer follows at line 190. Acceptable |

No conceptual drift. Every earlier-chapter term is named identically to its shipped form.

---

## Callback correctness

Every attributed claim was checked against the shipped chapter text, not from memory.

| Ch 10 claim | Target | Verdict |
|---|---|---|
| "Chapter 9 ended by naming a ceiling" — one address per Service, fifty Services | Ch 9 §3, lines 538–546 | **Correct.** Ch 9 states the ratio and the fifty-Service arithmetic, and points to `Ch 10 §1` |
| Ch 9 "warned you by name" — DNS discovery vs name-based virtual hosting | Ch 9 §7, line 1058 | **Correct**, near-verbatim, and Ch 9 points to `Ch 10 §2` |
| Ch 9 promised Ch 10 would name a shape "met twice" | Ch 9 lines 517, 727, 1558, 1708 | **Correct.** Ch 9 says "two instances now. Chapter 10 will meet a third and give the pattern a name" |
| Ch 3 gave the sentence *an object without its component does nothing* | Ch 3 §4, line 601 | **Correct, verbatim** |
| Ch 3 said "you would meet it four more times" | Ch 3 §4, line 601 | **Correct, verbatim** — "You're going to meet it four more times in this book" |
| Ch 3 "published the pointer to this exact paragraph" | Ch 3 §4 | **Correct.** Ch 3 §4 emits `see Ch 10 — an Ingress with no Ingress controller does nothing at all: the same pattern, first recurrence` |
| Ch 3 "published both of those pointers" (Ch 13, Ch 17) | Ch 3 §4 | **Correct.** Both forward pointers present |
| Ch 4 said "a NetworkPolicy selects both its subject and its peers" | Ch 4 §5, line 835 | **Correct, verbatim** — the phrase is Ch 4's own cross-bearing text |
| Ch 2 told you "on a graded question" (workload-to-host isolation) | Ch 2 §7 + graded Q4 (lines 845, 868) | **Correct** |
| Ch 6 introduced StatefulSet as identity-not-disk, then deferred storage | Ch 6 §6, lines 850–868 | **Correct.** Ch 6 carries both the "it writes to disk" Snag and the explicit deferral |
| Ch 4 §4 catalogued `kubernetes.io/tls` | Ch 4 §4, line 668 | **Correct** |
| Ch 9's second network-model rule + "barring intentional network segmentation" | Ch 9 §1, line 407 | **Correct**, and Ch 9 points back to `Ch 10 §6` |
| Ch 5 §1 — the Pod IP | Ch 5 §1, line 363 | **Correct** (gloss, not definition home; see fix 8) |

**Cross-bearings: 36 pointers across 34 lines. 35 correct, 1 defect.**

**Defect — line 754.** `*[cross-bearing: see Ch 9 §6 — the client's resolver…]*` is wrong. Shipped Ch 9 §6 is *"The Component That Makes It Real"* (kube-proxy). The resolver material is shipped Ch 9 §7, *"Names, and Where They Resolve."*

This is provably wrong on internal evidence alone: Ch 10 line 196 already points at **Ch 9 §7** for the same DNS material. Both cannot be right. **Fix: `Ch 9 §6` → `Ch 9 §7`.**

Forward pointers into undrafted chapters (Ch 11, 12, 13, 16, 17) all resolve against the skeleton: Ch 12 §5, Ch 12 §9 ×2, Ch 13 §7 ×2, Ch 17 §4 ×2, Ch 17 §5 ×3, Ch 17 §7 ×2 — every one matches the skeleton's assigned owner.

---

## Retrieval-practice accuracy

| Question | Tag | Topic | Verified in |
|---|---|---|---|
| Bearings 1 Q1 | `ch9` | Service types vs Ingress for non-HTTP | Ch 9 §3 ✓ |
| Bearings 1 Q5 | `ch3` | absent-component rule + two Ch 9 instances | Ch 3 §4 line 601 ✓ |
| Bearings 3 Q1 | `ch4` | NetworkPolicy selects subject and peers | Ch 4 §5 line 835 ✓ |
| Practice 2 | `ch9` | HTTP app + binary broker exposure | Ch 9 §3 ✓ |
| Practice 7 | `ch3` | controller watches objects, drives reality | Ch 3 §6 ✓ |
| Practice 16 | `ch4` | selector positions; relabelling consequence | Ch 4 §5 ✓ |
| Practice 18 | `ch3` | the rule + all four instances | Ch 3 §4 ✓ |

**7 of 7 accurate.** No wasted retrieval. Practice 18's answer-key enumeration (Ch 9 §3, Ch 9 §4, Ch 10 §3, Ch 10 §7) is correct against shipped text.

Question inventory: 8 Soundings + 15 Bearings (3 checkpoints × 5) + 18 Practice = **41**, meeting the per-chapter floor (8 Soundings, ≥10 Bearings across ≥2 checkpoints).

---

## Glossary coverage

| Concept/command introduced | Defined in-chapter? | Needs glossary entry? |
|---|---|---|
| edge router | yes | no |
| L4 / L7 (layer boundary) | yes | no |
| north-south / east-west | yes | no |
| Ingress; rules, host, path | yes | no |
| `pathType` (Exact/Prefix/ImplementationSpecific) | yes | no |
| simple fanout | yes | no |
| name-based virtual hosting | yes | no |
| TLS termination | yes | no |
| default backend | yes | no |
| Ingress controller | yes | no |
| IngressClass; default-class annotation | yes | no |
| absent-component pattern | yes (named here per ledger) | no |
| frozen ≠ deprecated | yes | no |
| Gateway API; GatewayClass, Gateway, HTTPRoute | yes | no |
| role-oriented design (three roles) | yes | no |
| `parentRefs` / `backendRefs` / `listeners` | yes | no |
| GRPCRoute | one clause, as HTTPRoute's sibling | no |
| NetworkPolicy; `podSelector`, `namespaceSelector`, `ipBlock` | yes | no |
| CIDR notation | glossed; chapter defers expansion | **yes** (ledger already assigns: "Ch 10 §6 gloss; glossary owns the expansion") |
| ingress/egress isolation; non-isolated default | yes | no |
| additive allow-only / no deny rule | yes | no |
| default-deny by construction | yes | no |
| policy inertness on unsupporting plugin | yes | no |
| **SNI** | no — used unexpanded | **yes** |
| **OSI** | no — used unexpanded | **yes** |
| **reverse proxy** | no — used as assumed vocabulary | **yes** |

Three orphans, detailed as fixes 6–8 below. All three reach graded material, which the B7 ledger's orphan doctrine treats as disqualifying for glossary-only handling without an in-text gloss.

---

## Ethical guardrails check

- [x] **No fabricated statistics or claims.** Only numeric claim in the chapter is `28%`, sourced and tagged, with an explicit disclosure that the finer allocation is the author's. The Exam Alert closes with a refusal to attach frequency numbers to traps: *"Inventing one would be worse than saying nothing."* This is the strongest instance of this guardrail I have seen in the book.
- [x] **Fear-based content uses real examples.** The NetworkPolicy silent-failure argument is built from two documented facts, with the inference explicitly labelled as the book's own.
- [x] **Simplification acknowledged.** §7's Dead Reckoning block carries a version caveat on the out-of-scope list and tells the reader to re-check the live page. §4 separates the project's wording from the book's operational gloss, and repeats the separation in the Exam Alert and Bearings #2 A2.
- [x] **Authority claims cite legitimate sources.** Dense `[source:]` tagging throughout; every documented claim is attributed and every inference is marked as one.
- [x] **"Frequently tested" claims verifiable.** No frequency claims are made. Two qualitative claims about candidate error ("Candidates get this wrong in both directions," line 586; "reliably… confidently," line 953) plus "Nearly everyone drops one" (§4) are unsourced characterizations of error-propensity, not exam-frequency claims — consistent with the B1 convention of "easy to confuse" over "frequently tested." **Pass**, with a note under fix 9.
- [x] **No strawmanning of alternative study methods.** None present.
- [x] **Subject dignity (v5.7).** Wry beats — "Same chart, different pilot," "an uncharted rock" — target the practitioner's experience. §3 and §7 both explicitly absolve the reader ("Nothing here is a mistake on your colleague's part"; "Nothing about this is careless"). No humor aimed at parties harmed by failures. **Exemplary.**

---

## Recommended fixes

The diagnostics caught most of this. What follows is what they did not.

### 1. `Ch 9 §6` → `Ch 9 §7` — line 754 *(must fix)*
Only outright cross-bearing defect in the chapter. Ch 10 already points correctly at Ch 9 §7 elsewhere, so this is self-contradicting.

### 2. Shipped Ch 9's numbering diverges from the B6 skeleton *(author decision, book-level)*
The skeleton gives Ch 9 seven sections; **shipped Ch 9 has eight**, with a +1 offset from §5 on:

| Skeleton | Shipped |
|---|---|
| §5 How the Traffic Actually Gets There | §6 The Component That Makes It Real |
| §6 Finding It by Name | §7 Names, and Where They Resolve |
| §7 A Stable Name Over Churn | §8 A Query With a Name |
| *(folded into §4)* | §5 When You Don't Want a Single Address |

Consequence: the instruction to verify pointers "against the section skeleton, not your own reading of the target chapter" would have *introduced* the line 754 defect and *broken* the correct line 196. Per B7 ("where the shipped text and the B6 skeleton disagree, the shipped text wins"), I ruled for shipped text. **Recommend amending the skeleton's Ch 9 block to the shipped eight-section form** before Ch 11–19 draft against it. Ch 9's own AUTHOR-REVIEW note (line ~1062) requested exactly this sweep at this stage.

Out of scope but visible while checking: shipped Ch 9 carries three pointers that miss under either authority — `Ch 3 §4 — kube-proxy as a node component` (kube-proxy is Ch 3 §3), `Ch 17 §3 — a service mesh` (mesh is Ch 17 §5), `Ch 15 §5 — the control loop pointed at a Git repository` (that Zenith is Ch 15 §7). Ch 10's equivalents are all correct. Worth a Ch 9 retro.

### 3. The interface count contradicts shipped Ch 9 §8 *(author decision)*
Ch 10's Voyage Ahead tells the reader they hold **three** of the four interfaces (CRI, CRDs, CNI). Shipped Ch 9 §8 tells the same reader that CNI is "**the second instance** of an arrangement you first met in Chapter 2" — counting CRDs out. A reader who counted with Ch 9 has two and is now told they have three, with no reconciliation.

Ch 10's count is the correct one: both binding contracts fix the set as CRI + CNI + CSI + CRDs, and Ch 10's AUTHOR-REVIEW documents the reasoning. Ch 9's narrower count is defensible on its own terms (CRDs is an extension mechanism, not a delegate-the-implementation interface) — but the two counts are one chapter apart and both reader-facing. **Either add a half-clause to Ch 10 acknowledging Ch 9 counted the arrangement more narrowly, or retrofit Ch 9 §8.**

### 4. Ordinal collision waiting in Ch 11 *(forward-looking)*
Ch 10 says the reader has three and that "Chapter 11 brings CSI… and that closes the set." The skeleton labels Ch 11 §5 "**Third** of the four pluggable interfaces." If Ch 11 drafts to that label, the reader hits "third" immediately after being told they already had three. **Ch 11 §5 should say CSI *closes* the set, not that it is third** — or the skeleton's ordinal annotations should be dropped, since they are set-order, not encounter-order.

### 5. Bare "Bearings #3" — line 41
`take Bearings #3` in the Attention Budget's 15-minute note. B7: *"Never 'Bearings' alone in reader-facing text."* → `take Taking Your Bearings #3`.

### 6. SNI is unexpanded and unowned *(graded material)*
`SNI` appears twice, both in **Soundings answer 1**, and **nowhere else in the book** (zero hits across Ch 1–9). It is not in the 74-entry acronym register. B7's rule is absolute: *"Every acronym is expanded on its first use in the book, without exception."* → expand to **Server Name Indication** on first use, add a register row and a glossary entry. The in-text gloss is otherwise adequate, so this is a two-word fix.

### 7. OSI is unexpanded and reaches a question stem
Used at lines 156, 829, 1249, 1381 — line 1249 is **Practice Question 1's stem**, line 1381 its answer. The register lists OSI only inside the *expansion* of `L4 / L7`; it has no row of its own. → expand at first use (§1, line 156), add a register row.

### 8. "reverse proxy" has no owner
7 uses, including **Soundings answer 8** and the whole of §5's request flow. Not in the ledger, not in the ambient-vocabulary tier. Defensible as ambient for an adult professional reader, but it currently sits in graded text with no lookup path. → add to the ambient tier or give it a glossary entry. Lowest priority of the three.

Related, no action: the `Ch 5 §1` pointer for "the Pod IP" (line 996) lands on Ch 5's *gloss* (a 🪝 Snag) rather than the definition home at Ch 9 §1. Defensible — Ch 5 §1 is where the reader learns a Pod has one address — and Ch 10 points at Ch 9 §1 twice nearby. Leaving as-is.

### 9. north-south / east-west is still unassessed
The chapter's own AUTHOR-REVIEW at §1 kept the mnemonic *"on the assumption the question pass takes the first option — if no question is added, revisit."* **The question pass did not add one.** The pair is taught (§1), mnemonic'd, and summarised, but appears in **zero** of the 41 questions. The revisit trigger has fired: add one question, or drop the mnemonic and keep the prose.

### 10. Two open AUTHOR-REVIEWs I can close
- **"One external address per Service" is untagged** (Soundings A2 and the Chapter Summary row). Not a research gap. Shipped **Ch 9 §3 line 540** states it — *"A LoadBalancer Service gives you one external address per Service"* — and line 546 explicitly frames the fifty-Service arithmetic as *"this book's own argument."* It is Ch 9-owned book reasoning, correctly inherited. The cross-bearing already added to the Summary row is the right treatment; **no source tag is needed or possible.**
- **Ch 3 §4's forward pointer**, questioned implicitly by the §3 counting note, is real and says *"the same pattern, first recurrence."* Ch 10's two-counts reconciliation is correct and needed — Ch 3 labels Ingress the *first* recurrence while the reader met two in Ch 9. Ch 10 is the only place that squares this. Keep it.

11 of the 13 AUTHOR-REVIEW comments in the draft remain open for author decision; none blocks stage 14 except items 1–3 above.
```

**The one thing I'd act on before anything else** is fix 2 — the shipped Ch 9 / skeleton numbering split. It silently inverts the correctness of Ch 9 pointers depending on which authority a drafting stage consults, and Chapters 11–19 will all draft against that skeleton.